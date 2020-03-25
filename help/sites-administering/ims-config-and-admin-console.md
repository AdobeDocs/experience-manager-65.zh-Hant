---
title: Adobe IMS驗證和[!DNL Admin Console]支援AEM Managed Services
seo-title: Adobe IMS驗證和[!DNL Admin Console]支援AEM Managed Services
description: 瞭解如何在AEM中使用[!DNL Admin Console]。
seo-description: 瞭解如何在AEM中使用[!DNL Admin Console]。
uuid: 3f5b32c7-cf62-41a4-be34-3f71bbf224eb
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: f6112dea-a1eb-4fd6-84fb-f098476deab7
translation-type: tm+mt
source-git-commit: a9931024f5cd79e2e363ed46edaef5e3e66c6e14

---


# Adobe IMS驗證與支 [!DNL Admin Console] 援AEM Managed Services {#adobe-ims-authentication-and-admin-console-support-for-aem-managed-services}

>[!NOTE]
>
>請注意，此功能僅適用於Adobe Managed Services客戶。

## 簡介 {#introduction}

AEM 6.4.3.0針對 [!DNL Admin Console] AEM Managed Services客戶推出AEM例項和Adobe IMS(Identity Management System)型驗證 **的支援** 。

AEM登入可讓AEM Managed Services客 [!DNL Admin Console] 戶在單一主控台中管理所有Experience Cloud使用者。 「使用者」和「群組」可指派給與AEM例項關聯的產品設定檔，允許他們登入特定例項。

## 重要焦點 {#key-highlights}

* AEM IMS驗證支援僅適用於AEM作者、管理員或開發人員，不適用於客戶網站（如網站訪客）的外部使用者
* 這些 [!DNL Admin Console] 軟體會將AEM Managed Services客戶代表為IMS組織，其例項則代表為產品內容。 客戶系統和產品管理員將能夠管理例項的存取權
* AEM Managed Services將同步客戶拓撲與 [!DNL Admin Console]。 在中，每個例項會有一個AEM Managed Services產品內容例項 [!DNL Admin Console]。
* Product Profiles in [!DNL Admin Console] will determine which instances a user can access
* 支援使用客戶自己的SAML 2相容身分提供者的同盟驗證
* 僅支援Enterprise ID或Federated ID（針對客戶單一登入），不支援個人Adobe ID。
* [!DNL User Management](在Adobe [!DNL Admin Console]中)將繼續歸客戶管理員所有。

## 架構 {#architecture}

IMS驗證可在AEM和Adobe IMS端點之間使用OAuth通訊協定運作。 當使用者新增至IMS並擁有Adobe Identity後，他們就可以使用IMS憑證登入AEM Managed Services例項。

使用者登入流程如下所示，使用者將被重新導向至IMS，或選擇性地重新導向至客戶IDP進行SSO驗證，然後重新導向回AEM。

![image2018-9-23_23-55-8](assets/image2018-9-23_23-55-8.png)

## How To Set Up {#how-to-set-up}

### Onboarding Organizations to [!DNL Admin Console] {#onboarding-organizations-to-admin-console}

The customer onboarding to [!DNL Admin Console] is a pre-requisite to using Adobe IMS for AEM authentication.

首先，客戶應在Adobe IMS中布建組織。 Adobe企業客戶在 [Adobe [!DNL管理控制台]中代表為IMS組織](https://helpx.adobe.com/enterprise/using/admin-console.html)。

AEM Managed Services customers should already have an organization provisioned, and as part of the IMS provisioning, the customer instances will be made available in the [!DNL Admin Console] for managing user entitlements and access.

AMS和客戶將攜手合作，將使用者驗證移轉至IMS，讓每個客戶都能完成工作流程。

一旦客戶以IMS組織形式存在，而AMS完成為IMS布建客戶時，此為所需組態工作流程的摘要：

![image2018-9-23_23-33-25](assets/image2018-9-23_23-33-25.png)

1. The designated System Admin receives an invite to log in to the [!DNL Admin Console]
1. 系統管理員聲明網域，以確認網域的所有權（在此範例中為acme.com）
1. 系統管理員設定用戶目錄
1. 系統管理員在SSO設定中設定身分提供者(IDP)。 [!DNL Admin Console]
1. AEM管理員會照常管理本機群組、權限和權限。 請參閱使用者和群組同步

>[!NOTE]
>
>如需Adobe Identity Management Basics（包括IDP設定）的詳細資訊，請參閱本 [頁文章。](https://helpx.adobe.com/enterprise/using/set-up-identity.html)
>
>如需企業管理的詳細資訊，請 [!DNL Admin Console] 參閱本 [頁文章](https://helpx.adobe.com/enterprise/managing/user-guide.html)。

### 上線使用者至 [!DNL Admin Console]{#onboarding-users-to-the-admin-console}

根據客戶的規模及其偏好設定，有三種方式可讓使用者上線：

1. 在 [!DNL Admin Console]
1. 為使用者上傳CSV檔案
1. 從客戶的企業Active Directory同步用戶和組。

#### Manual Addition through [!DNL Admin Console] UI {#manual-addition-through-admin-console-ui}

Users and Groups can be manually created in the [!DNL Admin Console] UI. 如果沒有大量使用者可管理，則可使用此方法。 例如，少於50位AEM使用者。

如果客戶已使用此方法管理其他Adobe產品，例如Analytics、Target或Creative Cloud應用程式，也可以手動建立使用者。

![image2018-9-23_20-39-9](assets/image2018-9-23_20-39-9.png)

#### UI中的檔案上 [!DNL Admin Console] 傳 {#file-upload-in-the-admin-console-ui}

為方便使用者建立，可上傳CSV檔案以大量新增使用者：

![image2018-9-23_18-59-57](assets/image2018-9-23_18-59-57.png)

#### 使用者同步工具 {#user-sync-tool}

使用者同步工具（簡稱UST）可讓企業客戶使用Active Directory或其他經測試的OpenLDAP目錄服務來建立或管理Adobe使用者。 目標用戶是IT Identity Administrators（Enterprise Directory和系統管理員），他們將能夠安裝和配置此工具。 開放原始碼工具可自訂，讓客戶可讓開發人員修改它以符合其特定需求。

When User Sync runs, it fetches a list of users from the organization’s Active Directory (or any other compatible data source) and compares it with the list of users within the [!DNL Admin Console]. It then calls the Adobe [!DNL User Management] API so that the [!DNL Admin Console] is synchronized with the organization’s directory. 改變流程完全是單向的；在中所做的任何 [!DNL Admin Console] 編輯都不會推送至目錄。

此工具可讓系統管理員將客戶目錄中的使用者群組與產品設定以及新的 [!DNL Admin Console]UST版本中的使用者群組對應，也允許在中動態建立使用者群組 [!DNL Admin Console]。

To set up User Sync, the organization needs to create a set of credentials in the same way they would use the [[!DNL User Management] API](https://www.adobe.io/apis/cloudplatform/usermanagement/docs/setup.html).

![image2018-9-23_13-36-56](assets/image2018-9-23_13-36-56.png)

使用者同步是透過Adobe Github存放庫在以下位置散發：

[https://github.com/adobe-apiplatform/user-sync.py/releases/latest](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)

請注意，2.4RC1搶鮮版已提供動態群組建立支援，您可在以下網址找到： [https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)

The major features for this release are the ability to dynamically map new LDAP groups for user membership in the [!DNL Admin Console], as well as dynamic user group creation.

有關新群組功能的詳細資訊，請參閱：

[https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options)

>[!NOTE]
>
>有關用戶同步工具的詳細資訊，請參閱文 [檔頁](https://adobe-apiplatform.github.io/user-sync.py/en/)。
>
>
>The User Sync Tool needs to register as an Adobe I/O client UMAPI using the procedure described [here](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html).
>
>The Adobe I/O Console Documentation can be found [here](https://www.adobe.io/apis/cloudplatform/console.html).
>
>
>使用者 [!DNL User Management] 同步工具所使用的API會涵蓋在此位 [置](https://www.adobe.io/apis/cloudplatform/umapi-new.html)。

>[!NOTE]
>
>AEM IMS設定將由Adobe Managed Services團隊處理。 但是，客戶管理員可依其需求（例如「自動群組成員資格」或「群組對應」）來修改它。 IMS用戶端也將由您的受管理服務團隊註冊。

## 使用方式 {#how-to-use}

### Managing Products and User Access in [!DNL Admin Console] {#managing-products-and-user-access-in-admin-console}

When the customer Product Administrator logs in to [!DNL Admin Console], they will see multiple instances of the AEM Managed Services Product Context as shown below:

![screen_shot_2018-09-17at105804pm](assets/screen_shot_2018-09-17at105804pm.png)

In this example, the org *AEM-MS-Onboard* has 32 instances spanning different topologies and environments like Stage, Prod, etc.

![screen_shot_2018-09-17at105517pm](assets/screen_shot_2018-09-17at105517pm.png)

可以檢查實例詳細資訊以標識實例：

![screen_shot_2018-09-17at105601pm](assets/screen_shot_2018-09-17at105601pm.png)

在每個「產品內容」例項下，都會有相關聯的產品設定檔。 此產品設定檔用於指派使用者和群組的存取權。

![image2018-9-18_7-48-50](assets/image2018-9-18_7-48-50.png)

在此產品設定檔下新增的任何使用者和群組都可以登入該例項，如下列範例所示：

![screen_shot_2018-09-17at105623pm](assets/screen_shot_2018-09-17at105623pm.png)

### 登入AEM {#logging-into-aem}

#### 本機管理員登入 {#local-admin-login}

AEM可繼續支援管理員使用者的本機登入，因為登入畫面有選項可在本機登入：

![screen_shot_2018-09-18at121056am](assets/screen_shot_2018-09-18at121056am.png)

#### IMS 登入 {#ims-based-login}

若是其他使用者，在例項上設定 IMS 後，即可使用 IMS 登入。The user will first click on the **Sign in with Adobe** button as shown below:

![image2018-9-18_0-10-32](assets/image2018-9-18_0-10-32.png)

然後，會將其重新導向至IMS登入畫面，並輸入其認證：

![screen_shot_2018-09-17at115629pm](assets/screen_shot_2018-09-17at115629pm.png)

If a federated IDP is configured during initial [!DNL Admin Console] setup, then the user will be redirected to the customer IDP for SSO.

IDP為Okta，在以下範例中：

![screen_shot_2018-09-17at115734pm](assets/screen_shot_2018-09-17at115734pm.png)

驗證完成後，系統會將使用者重新導向回 AEM 並登入：

![screen_shot_2018-09-18at120124am](assets/screen_shot_2018-09-18at120124am.png)

### 移轉現有使用者 {#migrating-existing-users}

對於使用其他驗證方法且目前正在移轉至IMS的現有AEM例項，需要移轉步驟。

AEM儲存庫中的現有使用者（透過LDAP或SAML來源於本機）可以移轉至IMS，做為使用者移轉公用程式的IDP。

此公用程式將由您的AMS團隊執行，作為IMS布建的一部分。

### 管理AEM中的權限和ACL {#managing-permissions-and-acls-in-aem}

AEM將繼續管理存取控制和權限，這可透過將來自IMS的使用者群組（例如，下例中的AEM-GRP-008）與定義權限和存取控制的本機群組分開來達成。 與IMS同步的使用者群組可指派給本機群組並繼承權限。

以下範例中，我們會示範將同步的群組新增至本機 *Dam_Users* 群組。

在這裡，用戶也被指派給中的幾個組 [!DNL Admin Console]。 (請注意，使用使用者同步工具或在本機建立使用者和群組可從LDAP同步，請參閱上述的「 **入門使用者[!DNL Admin Console]**」一節)。

&amp;ast；請注意，用戶只有在登錄到實例時，用戶組才會同步，對於擁有大量用戶和組的客戶，AMS可以運行組同步實用程式來預取組，以進行上述訪問控制和權限管理。

![screen_shot_2018-09-17at94207pm](assets/screen_shot_2018-09-17at94207pm.png)

使用者屬於 IMS 中的下列群組：

![screen_shot_2018-09-17at94237pm](assets/screen_shot_2018-09-17at94237pm.png)

使用者登入後，系統會同步其群組成員資格，如下所示：

![screen_shot_2018-09-17at94033pm](assets/screen_shot_2018-09-17at94033pm.png)

在AEM中，從IMS同步的使用者群組可以新增為現有本機群組的成員，例如DAM使用者。

![screen_shot_2018-09-17at95804pm](assets/screen_shot_2018-09-17at95804pm.png)

如下所示，群組 *AEM-GRP_008* 會繼承DAM使用者的權限和權限。 這是管理同步群組權限的有效方式，也常用於LDAP驗證方法。

![screen_shot_2018-09-17at110505pm](assets/screen_shot_2018-09-17at110505pm.png)