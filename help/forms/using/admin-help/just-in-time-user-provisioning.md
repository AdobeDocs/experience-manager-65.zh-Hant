---
title: 及時用戶設定
seo-title: Just-in-time user provisioning
description: 使用即時設定在成功驗證後將用戶添加到用戶管理中，並將相關角色和組動態分配給新用戶。
seo-description: Use just-in-time provisioning to add users to User Management after successfull authentication and dynamically assign relevant roles and groups to the new user.
uuid: a5ad4698-70bb-487b-a069-7133e2f420c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e80c3f98-baa1-45bc-b713-51a2eb5ec165
exl-id: 7bde0a09-192a-44a8-83d0-c18e335e9afa
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# 及時用戶設定 {#just-in-time-user-provisioning}

表AEM單支援對用戶管理中尚不存在的用戶進行即時設定。 使用即時預配，用戶憑據成功驗證後將自動添加到用戶管理。 此外，相關角色和組被動態地分配給新用戶。

## 需要及時的用戶設定 {#need-for-just-in-time-user-provisioning}

這是傳統身份驗證的工作方式：

1. 當用戶嘗試登錄表單時，AEM用戶管理會按順序將用戶的憑據傳遞給所有可用的身份驗證提供程式。 （登錄憑據包括用戶名/密碼組合、Kerberos票證、PKCS7簽名等。）
1. 驗證提供程式驗證憑據。
1. 然後，驗證提供程式檢查用戶是否存在於用戶管理資料庫中。 可能會得到以下結果：

   **存在：** 如果用戶是最新的且未鎖定，則用戶管理將返回驗證成功。 但是，如果用戶不是當前用戶或已鎖定用戶，則用戶管理將返回驗證失敗。

   **不存在：** 用戶管理返回身份驗證失敗。

   **無效：** 用戶管理返回身份驗證失敗。

1. 評估驗證提供程式返回的結果。 如果驗證提供程式返回驗證成功，則允許用戶登錄。 否則，「用戶管理」會與下一個身份驗證提供程式進行檢查（步驟2-3）。
1. 如果沒有可用的身份驗證提供程式驗證用戶憑據，則返回身份驗證失敗。

當實現即時預配時，如果其中一個驗證提供程式驗證用戶的憑據，則在用戶管理中動態地建立新用戶。 （以上是傳統驗證過程中的步驟3之後。）

## 實施即時用戶配置 {#implement-just-in-time-user-provisioning}

### 適用於即時資源調配的API {#apis-for-just-in-time-provisioning}

表AEM單提供了以下API，用於即時預配：

```java
package com.adobe.idp.um.spi.authentication  ;
publ ic interface IdentityCreator {
/**
* Tries  to create a user with the  in formation  provided in the <code>UserProvisioningBO</code> object.
* If the user is successfully created, a valid AuthResponse is returned along with the information using which the user was created.
* It is the responsibility of the IdentityCreator to set the User obje ct  in the cre dential map with th e  ke y  <code>UMA u thenticationUtil.authenticatedUserKey</code>
* The credentials are available in the <code>UserProvisioningBO</code> object in the 'credentials' property.
* If the IdentityCreator is unable to create a user due to any reason, it returns <code>null</code>
* @param userBO An object of <code>com.adobe. i dp.um . spi.authenti c ationUserProvisioningBO</code>
* @return */public AuthResponse create(UserProvisioningBO userBO);
/**
* Returns the name of the IdentityCreator which will be registered in preferences.
* This name is used to associate the IdentityProvider with the Auth Provider Configuration in the domain.
* @return The name of the Identity Creator which is recognized in Configuration.
*/
public String getName();
}
package com.adobe.idp.um.spi.authentication;
import com.adobe.idp.um.api.infomodel.User;
public interface AssignmentProvider {
/**
* Tries to assign roles or permissions or group memberships to users created via Just-in-time provisioning.
* @param user The User created via the Just-in-time provisioning process.
* @return a Boolean flag indicating whether the assignment was successful or not.
*/
public Boolean assign(User user);
/**
* Returns the name of the AssignmentProvider through which it is registered under preferences.
* This name is used to associate the AssignmentProvider with the Auth Provider Configuration in the domain.
* @return The name of the AssignmentProvider which is recognized in Configuration.
*/public String getName();
}
```

### 建立剛啟用時間的域時的注意事項 {#considerations-while-creating-a-just-in-time-enabled-domain}

* 建立自定義 `IdentityCreator` 對於混合域，確保為本地用戶指定了虛擬密碼。 不要將此密碼欄位留空。
* 建議：使用 `DomainSpecificAuthentication` 驗證特定域的用戶憑據。

### 建立啟用時間的域 {#create-a-just-in-time-enabled-domain}

1. 在「APIs for just-in--provisioning」部分中編寫一個DSC來實現API。
1. 將DSC部署到表單伺服器。
1. 建立啟用時間的域：

   * 在管理控制台中，按一下設定>用戶管理>域管理>新建企業域。
   * 配置域，然後選擇「啟用及時預配」。 <!--Fix broken link (See Setting up and managing domains).-->
   * 添加身份驗證提供程式。 添加身份驗證提供程式時，在「新建身份驗證」螢幕上，選擇已註冊的身份建立者和分配提供程式。

1. 保存新域。

## 幕後 {#behind-the-scenes}

假定用戶嘗試登錄表單，驗AEM證提供程式接受其用戶憑據。 如果用戶尚未存在於用戶管理資料庫中，則用戶的身份檢查失敗。 現AEM在表單執行以下操作：

1. 建立 `UserProvisioningBO` 對象，並將其放入憑據映射中。
1. 基於由 `UserProvisioningBO`，獲取並調用已註冊 `IdentityCreator` 和 `AssignmentProvider` 的雙曲餘切值。
1. 調用 `IdentityCreator`。 如果返回成功 `AuthResponse`，提取 `UserInfo` 從憑據映射中。 將其傳遞到 `AssignmentProvider` 用於組/角色分配和建立用戶後的任何其他後處理。
1. 如果用戶建立成功，則用戶登錄嘗試返回成功。
1. 對於混合域，從提供給驗證提供方的驗證資料中提取用戶資訊。 如果獲取此資訊成功，請即時建立用戶。

>[!NOTE]
>
>與預設的 `IdentityCreator` 用於動態建立用戶。 建立用戶時會使用與域中的目錄關聯的資訊。
