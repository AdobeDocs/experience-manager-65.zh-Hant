---
title: 即時使用者布建
seo-title: 即時使用者布建
description: 使用及時布建功能，在成功驗證後將使用者新增至使用者管理，並動態指派相關角色和群組給新使用者。
seo-description: 使用及時布建功能，在成功驗證後將使用者新增至使用者管理，並動態指派相關角色和群組給新使用者。
uuid: a5ad4698-70bb-487b-a069-7133e2f420c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e80c3f98-baa1-45bc-b713-51a2eb5ec165
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 即時使用者布建 {#just-in-time-user-provisioning}

AEM表格支援使用者管理中尚未存在的使用者即時布建。 使用即時布建功能，使用者憑證成功驗證後，就會自動新增至「使用者管理」。 此外，相關角色和群組會動態指派給新使用者。

## 需要及時的用戶布建 {#need-for-just-in-time-user-provisioning}

傳統驗證的運作方式如下：

1. 當使用者嘗試登入AEM表單時，「使用者管理」會依序將使用者的憑證傳送給所有可用的驗證提供者。 （登錄憑據包括用戶名／密碼組合、Kerberos票證、PKCS7簽名等。）
1. 驗證提供者會驗證憑證。
1. 然後驗證提供者會檢查使用者是否存在於使用者管理資料庫中。 可能會產生下列結果：

   **** 存在：如果使用者是最新且已解除鎖定，「使用者管理」會傳回驗證成功。 不過，如果使用者不是最新或已鎖定，使用者管理會傳回驗證失敗。

   **** 不存在：使用者管理傳回驗證失敗。

   **** 無效：使用者管理傳回驗證失敗。

1. 驗證提供者傳回的結果會進行評估。 如果驗證提供者傳回驗證成功，則允許使用者登入。 否則，使用者管理會檢查下一個驗證提供者（步驟2-3）。
1. 如果沒有可用的驗證提供者驗證使用者憑證，則會傳回驗證失敗。

當實作即時布建時，如果其中一個驗證提供者驗證使用者的認證，就會在使用者管理中動態建立新使用者。 （在傳統驗證程式的步驟3後，請參閱上文。）

## 實作即時使用者布建 {#implement-just-in-time-user-provisioning}

### 適用於即時布建的API {#apis-for-just-in-time-provisioning}

AEM表格提供下列API以供即時布建：

```as3
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

### 建立啟用時間限制的網域時的考量事項 {#considerations-while-creating-a-just-in-time-enabled-domain}

* 建立混合網 `IdentityCreator` 域的自訂時，請確定已為本機使用者指定虛擬密碼。 請勿將此密碼欄位留空。
* 建議：使用 `DomainSpecificAuthentication` 來驗證特定網域的使用者憑證。

### 建立啟用時間的網域 {#create-a-just-in-time-enabled-domain}

1. 在「API for just-in-time provisioning」區段中撰寫實施API的DSC。
1. 將DSC部署到表單伺服器。
1. 建立啟用時間的網域：

   * 在「管理控制台」中，按一下「設定>使用者管理>網域管理>新建企業網域」。
   * 配置域並選擇「Enable Just In Time Provisioning」（啟用準時設定）。 <!--Fix broken link (See Setting up and managing domains).-->
   * 新增驗證提供者。 新增驗證提供者時，在「新增驗證」畫面上，選取已註冊的Identity Creator和Assignment Provider。

1. 儲存新網域。

## 幕後秘辛 {#behind-the-scenes}

假設使用者嘗試登入AEM表單，且驗證提供者接受其使用者認證。 如果使用者尚未存在於「使用者管理」資料庫中，則使用者的身分檢查會失敗。 AEM表格現在會執行下列動作：

1. 使用驗 `UserProvisioningBO` 證資料建立對象，並將其放入憑據映射中。
1. 根據由返回的域信 `UserProvisioningBO`息，讀取並調用已註冊 `IdentityCreator` 域 `AssignmentProvider` 和域的。
1. 叫用 `IdentityCreator`。 如果傳回成功 `AuthResponse`，請從 `UserInfo` 憑證映射擷取。 將其傳遞至群 `AssignmentProvider` 組／角色指派，以及建立使用者後進行的任何其他後處理。
1. 如果用戶建立成功，則返回用戶登錄嘗試的成功。
1. 對於混合域，從提供給驗證提供者的驗證資料中提取用戶資訊。 如果成功擷取此資訊，請即時建立使用者。

>[!NOTE]
>
>即時布建功能隨附於預設實作，您可 `IdentityCreator` 用來動態建立使用者。 建立用戶時，會使用與域中的目錄相關的資訊。

