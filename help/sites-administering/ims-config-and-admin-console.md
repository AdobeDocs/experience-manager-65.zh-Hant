---
title: Adobe Experience Manager Managed Services的Adobe IMS驗證和 [!DNL Admin Console] 支援
description: 瞭解如何在Adobe Experience Manager中使用 [!DNL Admin Console] 。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 95eae97c-01c2-4f5c-8068-f504eab7c49e
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 55bf7104dbd9b9fadf6cb37efa28084fe43393c3
workflow-type: tm+mt
source-wordcount: '1603'
ht-degree: 5%

---

# Adobe IMS驗證和對AEM Managed Services的[!DNL Admin Console]支援 {#adobe-ims-authentication-and-admin-console-support-for-aem-managed-services}

>[!NOTE]
>
>此功能僅適用於AdobeManaged Services客戶。

## 簡介 {#introduction}

AEM 6.4.3.0為&#x200B;**AEM Managed Services**&#x200B;客戶引入[!DNL Admin Console]對AEM執行個體和Adobe IMS(Identity Management System)型驗證的支援。

「[!DNL Admin Console]」的AEM上線將允許AEM Managed Services客戶在一個主控台中管理所有Experience Cloud使用者。 您可以將使用者指派給與AEM執行個體相關聯的產品設定檔，讓他們登入特定執行個體。

## 重要焦點 {#key-highlights}

* AEM IMS驗證支援僅適用於AEM作者、管理員或開發人員，不適用於客戶網站的外部一般使用者，例如網站訪客
* [!DNL Admin Console]會將AEM Managed Services客戶顯示為IMS組織，並將其執行個體顯示為產品內容。 客戶系統和產品管理員將能管理執行個體的存取許可權
* AEM Managed Services會將客戶拓撲與[!DNL Admin Console]同步。 在[!DNL Admin Console]中，每個執行個體會有一個AEM Managed Services產品內容的執行個體。
* [!DNL Admin Console]中的產品設定檔將決定使用者可存取的執行個體
* 支援使用客戶自己的符合SAML 2的身分提供者進行同盟驗證
* 僅支援Enterprise ID或Federated ID （適用於客戶的單一登入），不支援個人AdobeID。
* [!DNL User Management] (在Adobe[!DNL Admin Console]中)將繼續由客戶管理員擁有。

## 架構 {#architecture}

IMS驗證在AEM和Adobe IMS端點之間使用OAuth通訊協定來運作。 使用者加入IMS並擁有Adobe身分後，就能使用IMS憑證登入AEM Managed Services執行個體。

使用者登入流程如下所示，系統會將使用者重新導向至IMS，並可選擇重新導向至客戶IDP進行SSO驗證，然後重新導向回AEM。

![image2018-9-23_23-55-8](assets/image2018-9-23_23-55-8.png)

## 設定方法 {#how-to-set-up}

### 將組織加入[!DNL Admin Console] {#onboarding-organizations-to-admin-console}

[!DNL Admin Console]的客戶入門是使用Adobe IMS進行AEM驗證的先決條件。

首先，客戶應在Adobe IMS中布建組織。 Adobe企業客戶在[Adobe [!DNL Admin Console]](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)中會顯示為IMS組織。

AEM Managed Services客戶應先布建組織，而在IMS布建過程中，[!DNL Admin Console]中可提供客戶例項，用以管理使用者權益和存取許可權。

移至IMS進行使用者驗證將由AMS和客戶共同負責，各自的工作流程均需完成。

客戶成為IMS組織存在且AMS完成布建客戶的IMS後，以下是所需的設定工作流程摘要：

![image2018-9-23_23-33-25](assets/image2018-9-23_23-33-25.png)

1. 指定的系統管理員會收到登入[!DNL Admin Console]的邀請
1. 系統管理員宣告網域，以確認網域的所有權(在此範例中為acme.com)
1. 系統管理員設定使用者目錄
1. 系統管理員在[!DNL Admin Console]中設定身分提供者(IDP)以進行SSO設定。
1. AEM管理員可照常管理本機群組、許可權和許可權。 請參閱使用者和群組同步

>[!NOTE]
>
>如需有關AdobeIdentity Management基本知識（包括IDP設定）的詳細資訊，請參閱文章[此頁面。](https://helpx.adobe.com/tw/enterprise/using/set-up-identity.html)
>
>如需有關企業管理和[!DNL Admin Console]的詳細資訊，請參閱文章[此頁面](https://helpx.adobe.com/tw/enterprise/managing/user-guide.html)。

### 將使用者上線到[!DNL Admin Console] {#onboarding-users-to-the-admin-console}

根據客戶的規模和偏好，有三種方法可以吸引使用者：

1. 在[!DNL Admin Console]中手動建立使用者和群組
1. 上傳包含使用者的CSV檔案
1. 從客戶的企業Active Directory同步處理使用者和群組。

#### 透過[!DNL Admin Console] UI手動新增 {#manual-addition-through-admin-console-ui}

您可以在[!DNL Admin Console] UI中手動建立使用者和群組。 如果可供管理的使用者不多，可使用此方法。 例如，少於50名AEM使用者。

如果客戶已使用此方法管理其他Adobe產品(如Adobe Analytics、Adobe Target或Adobe Creative Cloud應用程式)，也可以手動建立使用者。

![image2018-9-23_20-39-9](assets/image2018-9-23_20-39-9.png)

#### 在[!DNL Admin Console] UI中上傳檔案 {#file-upload-in-the-admin-console-ui}

為方便建立使用者，可上傳CSV檔案大量新增使用者：

![image2018-9-23_18-59-57](assets/image2018-9-23_18-59-57.png)

#### 使用者同步工具 {#user-sync-tool}

使用者同步工具（簡稱UST）可讓企業客戶建立或管理使用Active Directory或其他經測試的OpenLDAP目錄服務的Adobe使用者。 目標使用者是IT身分管理員（企業目錄與系統管理員），他們將能安裝及設定此工具。 此開放原始碼工具可供自訂，因此客戶可讓開發人員修改工具，以符合其自身的特定需求。

當使用者同步執行時，它會從組織的Active Directory （或任何其他相容的資料來源）擷取使用者清單，並將其與[!DNL Admin Console]中的使用者清單進行比較。 然後它會呼叫Adobe[!DNL User Management] API，以便[!DNL Admin Console]與組織的目錄同步。 變更流程完全是單向的；在[!DNL Admin Console]中所做的任何編輯都不會推送至目錄。

此工具可讓系統管理員將客戶目錄中的使用者群組與[!DNL Admin Console]中的產品設定和使用者群組對應，新的UST版本也可在[!DNL Admin Console]中動態建立使用者群組。

若要設定「使用者同步」，組織必須建立一組認證，其方式與使用[[!DNL User Management] API](https://www.adobe.io/apis/cloudplatform/usermanagement/docs/setup.html)的方式相同。

![image2018-9-23_13-36-56](assets/image2018-9-23_13-36-56.png)

使用者同步是透過AdobeGithub存放庫提供使用，其位置如下：

[https://github.com/adobe-apiplatform/user-sync.py/releases/latest](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)

請注意，搶鮮版2.4RC1支援建立動態群組，可從此處取得： [https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)

此版本的主要功能是能夠動態對應新的LDAP群組，以取得[!DNL Admin Console]中的使用者成員資格，以及建立動態使用者群組。

有關新群組功能的詳細資訊，請參閱此處：

[https://adobe-apiplatform.github.io/user-sync.py/en/user-manual/advanced_configuration.html#additional-group-options](https://adobe-apiplatform.github.io/user-sync.py/en/user-manual/advanced_configuration.html#additional-group-options)

>[!NOTE]
>
>如需有關使用者同步工具的詳細資訊，請參閱[檔案頁面](https://adobe-apiplatform.github.io/user-sync.py/en/)。
>
>
>使用者同步工具必須使用[這裡](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html)說明的程式，註冊為Adobe I/O使用者端UMAPI。
>
>您可以在[這裡](https://developer.adobe.com/developer-console/docs/guides/)找到Adobe Developer Console檔案。
>
>
>此[位置](https://adobe-apiplatform.github.io/umapi-documentation/en/)包含使用者同步工具使用的[!DNL User Management] API。

>[!NOTE]
>
>AEM IMS設定將由AdobeManaged Services團隊處理。 但是，客戶管理員可以根據他們的需求（例如，自動群組成員資格或群組對應）來修改它。 您的Managed Services團隊也將註冊IMS使用者端。

## 使用方式 {#how-to-use}

### 在[!DNL Admin Console]中管理產品和使用者存取權 {#managing-products-and-user-access-in-admin-console}

當客戶產品管理員登入[!DNL Admin Console]時，他們將看到AEM Managed Services產品內容的多個執行個體，如下所示：

![screen_shot_2018-09-17at105804pm](assets/screen_shot_2018-09-17at105804pm.png)

在此範例中，組織&#x200B;*AEM-MS-Onboard*&#x200B;有32個執行個體，橫跨不同的拓撲和環境，例如Stage、Prod等。

![screen_shot_2018-09-17at105517pm](assets/screen_shot_2018-09-17at105517pm.png)

可以檢查執行個體詳細資訊以識別執行個體：

![screen_shot_2018-09-17at105601pm](assets/screen_shot_2018-09-17at105601pm.png)

在每個「產品內容」例項下，都會有相關聯的「產品設定檔」。 此產品設定檔用於指派存取許可權給使用者。

![image2018-9-18_7-48-50](assets/image2018-9-18_7-48-50.png)

此產品設定檔中新增的任何使用者都可以登入該執行個體，如以下範例所示：

![screen_shot_2018-09-17at105623pm](assets/screen_shot_2018-09-17at105623pm.png)

### 登入AEM {#logging-into-aem}

#### 本機管理員登入 {#local-admin-login}

AEM可繼續為管理員使用者支援本機登入，因為登入畫面具有本機登入的選項：

![screen_shot_2018-09-18at121056am](assets/screen_shot_2018-09-18at121056am.png)

#### IMS登入 {#ims-based-login}

若是其他使用者，在執行個體上設定 IMS 後，即可使用 IMS 登入。使用者先按一下&#x200B;**使用Adobe**&#x200B;登入，如下所示：

![image2018-9-18_0-10-32](assets/image2018-9-18_0-10-32.png)

接著，系統會將使用者重新導向至IMS登入畫面，並輸入其憑證：

![screen_shot_2018-09-17at115629pm](assets/screen_shot_2018-09-17at115629pm.png)

如果在初始[!DNL Admin Console]設定期間已設定同盟IDP，則會將使用者重新導向至客戶IDP，以進行SSO。

在以下範例中，IDP為Okta：

![screen_shot_2018-09-17at115734pm](assets/screen_shot_2018-09-17at115734pm.png)

驗證完成後，系統會將使用者重新導向回 AEM 並登入：

![screen_shot_2018-09-18at120124am](assets/screen_shot_2018-09-18at120124am.png)

### 正在移轉現有使用者 {#migrating-existing-users}

對於使用其他驗證方法且現在正移轉至IMS的現有AEM執行個體，需要移轉步驟。

AEM存放庫中的現有使用者（來源為本機，透過LDAP或SAML）可以使用使用者移轉公用程式移轉為IDP指向IMS。

此公用程式將由您的AMS團隊執行，作為IMS布建的一部分。

### 在AEM中管理許可權和ACL {#managing-permissions-and-acls-in-aem}

存取控制和許可權將繼續在AEM中管理，這可透過將來自IMS(例如，以下範例中的AEM-GRP-008)的使用者群組與定義了許可權和存取控制的本機群組分離來達成。 可將從IMS同步的使用者群組指派給本機群組，並繼承許可權。

以下範例中，我們會示範將同步的群組新增至本機 *Dam_Users* 群組。

在此處，使用者也已被指派到[!DNL Admin Console]中的幾個群組。 (使用者與群組可使用使用者同步工具從LDAP同步或在本機建立。 請參閱先前&#x200B;**將使用者加入[!DNL Admin Console]**。

>[!NOTE]
>
>只有當使用者登入執行個體時，才會同步使用者群組。

![screen_shot_2018-09-17at94207pm](assets/screen_shot_2018-09-17at94207pm.png)

使用者屬於 IMS 中的下列群組：

![screen_shot_2018-09-17at94237pm](assets/screen_shot_2018-09-17at94237pm.png)

使用者登入後，系統會同步其群組成員資格，如下所示：

![screen_shot_2018-09-17at94033pm](assets/screen_shot_2018-09-17at94033pm.png)

在AEM中，與IMS同步的使用者群組可以成員身分新增至現有的本機群組，例如DAM Users。

![screen_shot_2018-09-17at95804pm](assets/screen_shot_2018-09-17at95804pm.png)

如下所示，群組&#x200B;*AEM-GRP_008*&#x200B;繼承DAM使用者的許可權和許可權。 這是管理同步群組許可權的有效方式，也常用於LDAP型驗證方法。

![screen_shot_2018-09-17at110505pm](assets/screen_shot_2018-09-17at110505pm.png)
