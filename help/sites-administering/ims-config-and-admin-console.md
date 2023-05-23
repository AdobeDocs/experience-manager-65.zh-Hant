---
title: Adobe IMS驗證和 [!DNL Admin Console] 支援AEMManaged Services
seo-title: Adobe IMS Authentication and [!DNL Admin Console] Support for AEM Managed Services
description: 瞭解如何使用 [!DNL Admin Console] 的上AEM界。
seo-description: Learn how to use the [!DNL Admin Console] in AEM.
uuid: 3f5b32c7-cf62-41a4-be34-3f71bbf224eb
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f6112dea-a1eb-4fd6-84fb-f098476deab7
exl-id: 95eae97c-01c2-4f5c-8068-f504eab7c49e
feature: Security
source-git-commit: fff35031eaf55b185870da56a0b66f9145b1ec41
workflow-type: tm+mt
source-wordcount: '1676'
ht-degree: 10%

---

# Adobe IMS驗證和 [!DNL Admin Console] 支援AEMManaged Services {#adobe-ims-authentication-and-admin-console-support-for-aem-managed-services}

>[!NOTE]
>
>請注意，此功能僅可供Adobe Managed Services客戶使用。

>[!NOTE]
>
>AEM 目前不支援指派群組到設定檔。應單獨新增使用者。

## 簡介 {#introduction}

6.4.3.0 [!DNL Admin Console] 支援實AEM例和基於Adobe IMS(Identity Management系統)的驗證 **AEMManaged Services** 客戶。

登AEM機 [!DNL Admin Console] 將允許AEMManaged Services客戶在一個控制台中管理所有Experience Cloud用戶。 用戶可以分配到與實例關聯的產AEM品配置檔案，從而允許他們登錄到特定實例。

## 重要焦點 {#key-highlights}

* IMSAEM身份驗證支援僅針對AEM作者、管理員或開發人員，而不針對客戶站點的外部最終用戶（如站點訪問者）
* 的 [!DNL Admin Console] 將Managed ServicesAEM客戶表示為IMS組織，其實例表示為產品上下文。 客戶系統和產品管理員將能夠管理對實例的訪問
* AEMManaged Services將同步客戶拓撲 [!DNL Admin Console]。 在中，每個實AEM例將有一個Managed Services產品上下文實例 [!DNL Admin Console]。
* 產品配置檔案 [!DNL Admin Console] 將確定用戶可以訪問哪些實例
* 支援使用客戶自己的SAML 2相容身份提供程式的聯合身份驗證
* 僅支援企業或聯合ID（用於客戶單一登錄），不支援個人AdobeID。
* [!DNL User Management] (在Adobe [!DNL Admin Console])將繼續歸客戶管理員所有。

## 架構 {#architecture}

IMS認證通過在Adobe IMS端點之AEM間使用OAuth協定進行。 一旦用戶被添加到IMS並且具有Adobe標識，他們就可以使用IMS憑據登AEM錄到Managed Services實例。

用戶登錄流如下所示，用戶將被重定向到IMS，並可選地被重定向到客戶IDP進行SSO驗證，然後被重定向回AEM去。

![image2018-9-23_23-55-8](assets/image2018-9-23_23-55-8.png)

## 如何設定 {#how-to-set-up}

### 加入組織 [!DNL Admin Console] {#onboarding-organizations-to-admin-console}

客戶登入 [!DNL Admin Console] 是使用Adobe IMS進行身份驗證的前AEM提。

作為第一步，客戶應在Adobe IMS中配置一個組織。 Adobe企業客戶在IMS中表示為 [Adobe [!DNL Admin Console]](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)。

AEMManaged Services客戶應該已經配置了一個組織，作為IMS配置的一部分，客戶實例將在 [!DNL Admin Console] 用於管理用戶權利和訪問。

向IMS遷移以進行用戶驗證將是AMS和客戶的共同努力，每個客戶都要完成他們的工作流。

一旦客戶作為IMS組織存在，AMS完成為客戶提供IMS，這就是所需配置工作流的摘要：

![image2018-9-23_23-33-25](assets/image2018-9-23_23-33-25.png)

1. 指定的系統管理員將收到登錄到 [!DNL Admin Console]
1. 系統管理聲明域，用於確認域的所有權（在本例acme.com中）
1. 系統管理員設定用戶目錄
1. 系統管理員將配置 [!DNL Admin Console] SSO設定。
1. 管理AEM員一如既往地管理本地組、權限和權限。 請參閱用戶和組同步

>[!NOTE]
>
>有關AdobeIdentity Management基礎知識（包括IDP配置）的詳細資訊，請參閱文章 [此頁面。](https://helpx.adobe.com/tw/enterprise/using/set-up-identity.html)
>
>有關企業管理和 [!DNL Admin Console] 查看文章 [此頁](https://helpx.adobe.com/tw/enterprise/managing/user-guide.html)。

### 將用戶登錄到 [!DNL Admin Console] {#onboarding-users-to-the-admin-console}

根據客戶的規模和他們的偏好，板載用戶有三種方法：

1. 在中手動建立用戶和組 [!DNL Admin Console]
1. 與用戶上載CSV檔案
1. 從客戶的企業Active Directory同步用戶和組。

#### 手動添加 [!DNL Admin Console] UI {#manual-addition-through-admin-console-ui}

可以在 [!DNL Admin Console] UI。 如果用戶數量不多，則可以使用此方法。 例如，少於50個用戶AEM。

如果客戶已使用此方法管理其他Adobe產品(如分析、目標或Creative Cloud應用程式)，也可以手動建立用戶。

![image2018-9-23_20-39-9](assets/image2018-9-23_20-39-9.png)

#### 檔案上載 [!DNL Admin Console] UI {#file-upload-in-the-admin-console-ui}

為了便於處理用戶建立，可以上載CSV檔案以批量添加用戶：

![image2018-9-23_18-59-57](assets/image2018-9-23_18-59-57.png)

#### 使用者同步工具 {#user-sync-tool}

用戶同步工具（簡稱UST）使企業客戶能夠使用Active Directory或其他經測試的OpenLDAP目錄服務建立或管理Adobe用戶。 目標用戶是IT Identity Administrators（企業目錄和系統管理員），他們將能夠安裝和配置該工具。 可定製開源工具，以便客戶可以讓開發人員修改它以滿足他們自己的特定要求。

運行用戶同步時，它會從組織的Active Directory（或任何其他相容資料源）中提取用戶清單，並將其與組織內的用戶清單進行比較 [!DNL Admin Console]。 然後叫Adobe [!DNL User Management] API，以便 [!DNL Admin Console] 與組織的目錄同步。 變化流完全是單向的；對 [!DNL Admin Console] 不要被推出到目錄。

該工具允許系統管理員將客戶目錄中的用戶組與產品配置和用戶組 [!DNL Admin Console]，新UST版本還允許在 [!DNL Admin Console]。

若要設定「使用者同步」，組織需先透過與 [[!DNL User Management]  API](https://www.adobe.io/apis/cloudplatform/usermanagement/docs/setup.html) 相同的使用方式，建立一組憑證。

![image2018-9-23_13-36-56](assets/image2018-9-23_13-36-56.png)

用戶同步通過AdobeGithub儲存庫分發，位於以下位置：

[https://github.com/adobe-apiplatform/user-sync.py/releases/latest](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)

請注意，預發行版2.4RC1提供動態組建立支援，可在以下位置找到： [https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)

此版本的主要功能是動態映射新LDAP組以使用戶成員身份位於 [!DNL Admin Console]，以及動態用戶組建立。

有關新組功能的詳細資訊，請參閱：

[https://adobe-apiplatform.github.io/user-sync.py/en/user-manual/advanced_configuration.html#additional-group-options](https://adobe-apiplatform.github.io/user-sync.py/en/user-manual/advanced_configuration.html#additional-group-options)

>[!NOTE]
>
>有關用戶同步工具的詳細資訊，請參閱 [文檔頁](https://adobe-apiplatform.github.io/user-sync.py/en/)。
>
>
>用戶同步工具需要使用描述的過程註冊為Adobe I/O客戶端UMAPI [這裡](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html)。
>
>可以找到Adobe I/O控制台文檔 [這裡](https://developer.adobe.com/developer-console/docs/guides/)。
>
>
>的 [!DNL User Management] 用戶同步工具使用的API將在此處介紹 [位置](https://adobe-apiplatform.github.io/umapi-documentation/en/)。

>[!NOTE]
>
>IMSAEM配置將由Adobe托管服務團隊處理。 但是，客戶管理員可以根據其要求修改它（例如「自動組成員資格」或「組映射」）。 IMS客戶端也將由您的Managed Services團隊註冊。

## 使用方式 {#how-to-use}

### 管理產品和用戶訪問 [!DNL Admin Console] {#managing-products-and-user-access-in-admin-console}

當客戶產品管理員登錄到 [!DNL Admin Console]，它們將看到以下AEM所示的Managed Services產品上下文的多個實例：

![screen_shot_2018-09-17at105804pm](assets/screen_shot_2018-09-17at105804pm.png)

在此示例中，組織 *AEM-MS — 板載* 有32個實例，它們跨越不同的拓撲和環境，如Stage、Prod等。

![screen_shot_2018-09-17at105517pm](assets/screen_shot_2018-09-17at105517pm.png)

可以檢查實例詳細資訊以標識實例：

![screen_shot_2018-09-17at105601pm](assets/screen_shot_2018-09-17at105601pm.png)

在每個「產品上下文」實例下，都會有一個關聯的「產品配置檔案」。 此產品配置檔案用於為用戶分配訪問權限。

![image2018-9-18_7-48-50](assets/image2018-9-18_7-48-50.png)

在此產品配置檔案下添加的任何用戶都將能夠登錄到該實例，如下例所示：

![screen_shot_2018-09-17at105623pm](assets/screen_shot_2018-09-17at105623pm.png)

### 登錄AEM到 {#logging-into-aem}

#### 本地管理員登錄 {#local-admin-login}

可AEM以繼續支援管理員用戶的本地登錄，因為登錄螢幕具有本地登錄的選項：

![screen_shot_2018-09-18at121056am](assets/screen_shot_2018-09-18at121056am.png)

#### IMS 登入 {#ims-based-login}

若是其他使用者，在執行個體上設定 IMS 後，即可使用 IMS 登入。用戶將首先按一下 **使用Adobe登錄** 按鈕

![image2018-9-18_0-10-32](assets/image2018-9-18_0-10-32.png)

然後，它們將被重定向到IMS登錄螢幕並輸入其憑據：

![screen_shot_2018-09-17at115629pm](assets/screen_shot_2018-09-17at115629pm.png)

如果在初始時配置了聯合IDP [!DNL Admin Console] 設定後，用戶將被重定向到客戶IDP以進行SSO。

以下示例中的IDP為Okta:

![screen_shot_2018-09-17at115734pm](assets/screen_shot_2018-09-17at115734pm.png)

驗證完成後，系統會將使用者重新導向回 AEM 並登入：

![screen_shot_2018-09-18at120124am](assets/screen_shot_2018-09-18at120124am.png)

### 遷移現有用戶 {#migrating-existing-users}

對於使AEM用另一種身份驗證方法且正在遷移到IMS的現有實例，需要執行遷移步驟。

儲存庫中的現AEM有用戶（通過LDAP或SAML在本地源）可以遷移到IMS，作為IDP使用用戶遷移實用程式。

此實用程式將由您的AMS團隊作為IMS設定的一部分運行。

### 管理權限和ACL AEM {#managing-permissions-and-acls-in-aem}

訪問控制和權限將繼續在中進行管理AEM，這可以通過將來自IMS(如下例中的AEM-GRP-008)的用戶組與定義權限和訪問控制的本地組分離來實現。 可以將從IMS同步的用戶組分配給本地組並繼承權限。

以下範例中，我們會示範將同步的群組新增至本機 *Dam_Users* 群組。

此時，用戶也已分配給 [!DNL Admin Console]。 (請注意，用戶和組可以使用用戶同步工具從LDAP同步，也可以在本地建立，請參閱一節 **將用戶登錄到[!DNL Admin Console]** )。

>[!NOTE]
>
>只有當用戶登錄到實例時，才會同步用戶組。

![screen_shot_2018-09-17at94207pm](assets/screen_shot_2018-09-17at94207pm.png)

使用者屬於 IMS 中的下列群組：

![screen_shot_2018-09-17at94237pm](assets/screen_shot_2018-09-17at94237pm.png)

使用者登入後，系統會同步其群組成員資格，如下所示：

![screen_shot_2018-09-17at94033pm](assets/screen_shot_2018-09-17at94033pm.png)

在中AEM，可以將與IMS同步的用戶組作為成員添加到現有本地組，如DAM用戶。

![screen_shot_2018-09-17at95804pm](assets/screen_shot_2018-09-17at95804pm.png)

如下所示， *AEM-GRP_008* 繼承DAM用戶的權限和權限。 這是管理同步組權限的有效方法，在基於LDAP的身份驗證方法中也常用。

![screen_shot_2018-09-17at110505pm](assets/screen_shot_2018-09-17at110505pm.png)
