---
title: AEM Communities中的使用者和UGC管理服務
description: 使用API來大量刪除和大量匯出使用者產生的內容，並停用使用者帳戶。
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
docset: aem65
role: Admin
exl-id: 526ef0fa-3f20-4de4-8bc5-f435c60df0d0
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---

# AEM Communities中的使用者和UGC管理服務 {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>以下各節以GDPR為例，但說明的詳細資料適用於所有資料保護和隱私權法規，例如GDPR、CCPA等。

AEM Communities會公開現成可用的API，以管理使用者設定檔及大量管理使用者產生的內容(UGC)。 啟用後，**UserUgcManagement**&#x200B;服務可讓有特殊許可權的使用者（社群管理員和版主）停用使用者設定檔，以及大量刪除或大量匯出特定使用者的UGC。 這些API還能讓客戶資料的控管者和處理者遵守歐盟的一般資料保護規範(GDPR)和其他受GDPR啟發的隱私權法令。

如需進一步資訊，請參閱Adobe隱私權中心[&#128279;](https://www.adobe.com/privacy/general-data-protection-regulation.html)的GDPR頁面。

>[!NOTE]
>
>如果您在AEM Communities[&#128279;](/help/communities/analytics.md)網站中設定Adobe Analytics，則擷取的使用者資料會傳送至Adobe Analytics伺服器。 Adobe Analytics提供的API可讓您存取、匯出和刪除使用者資料，以及遵守GDPR。 如需詳細資訊，請參閱[提交存取及刪除要求](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-submit-access-delete.html?lang=zh-Hant)。

若要使用這些API，您必須啟用UserUgcManagement服務以啟用`/services/social/ugcmanagement`端點。 若要啟用此服務，請安裝[GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet)上提供的[範例servlet](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet)。 接著，使用http要求，以適當的引數點選社群網站發佈執行個體上的端點，如下所示：

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`。不過，您也可以建置UI （使用者介面）來管理系統中的使用者設定檔和使用者產生的內容。

這些API允許執行下列功能。

## 擷取使用者的UGC {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver， String user， OutputStream outputStream)**&#x200B;協助從系統匯出使用者的所有UGC。

* **使用者**：使用者的可授權識別碼。
* **outputStream**：結果以輸出資料流傳回，此資料流為zip檔案，包含使用者產生的內容（以json檔案形式）和附件（包含使用者上傳的影像或視訊）。

例如，若要匯出名為Weston McCall且使用weston.mccall@dodgit.com作為可授權ID登入Communities網站之使用者的UGC，您可以傳送類似以下的httpGET請求：

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## 刪除使用者的UGC {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver， String user)**&#x200B;協助從系統中刪除使用者的所有UGC。

* **使用者**：使用者的可授權識別碼。

例如，若要透過http-POST請求刪除具有可授權ID weston.mccall@dodgit.com之使用者的UGC，請使用下列引數：

* 使用者= `weston.mccall@dodgit.com`
* 作業= `deleteUgc`

### 從Adobe Analytics中刪除UGC {#delete-ugc-from-adobe-analytics}

若要從Adobe Analytics刪除使用者資料，請遵循[GDPR Analytics工作流程](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html?lang=zh-Hant)；因為API不會從Adobe Analytics刪除使用者資料。

如需AEM Communities使用的Adobe Analytics變數對應，請參閱下列影像：

Adobe Analytics的![AEM社群變數對應](assets/analytics-communities-mapping.png)

## 停用使用者帳戶 {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver， String user)**&#x200B;協助停用使用者帳戶。

* **使用者**：使用者的可授權識別碼。

>[!NOTE]
>
>停用使用者將會刪除使用者在伺服器上所擁有的所有使用者產生的內容。

例如，若要透過httpPOST請求刪除具有可授權識別碼`weston.mccall@dodgit.com`的使用者設定檔，請使用下列引數：

* 使用者= `weston.mccall@dodgit.com`
* 作業= `deleteUser`

>[!NOTE]
>
>deleteUserAccount() API只會停用系統中的使用者設定檔，並移除UGC。 但是，若要從系統刪除使用者設定檔，請瀏覽至&#x200B;**CRXDE Lite**： [https://&lt;server>/crx/de](https://localhost:4502/crx/de)，找出該使用者節點並將其刪除。
