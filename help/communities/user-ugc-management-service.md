---
title: AEM Communities中的使用者和UGC管理服務
seo-title: User and UGC Management Service in AEM Communities
description: 使用API來大量刪除和大量匯出使用者產生的內容，並停用使用者帳戶。
seo-description: Use APIs to bulk delete and bulk export user generated content, and disable user account.
uuid: 91180659-617d-4f6c-9a07-e680770d0d8f
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
discoiquuid: d305821d-1371-4e4a-8b28-8eee8fafa43b
docset: aem65
role: Admin
exl-id: 526ef0fa-3f20-4de4-8bc5-f435c60df0d0
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# AEM Communities中的使用者和UGC管理服務 {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>GDPR是以下各節中的範例，但涵蓋的詳細資訊適用於所有資料保護和隱私權法規；例如GDPR、CCPA等

AEM Communities會公開API的現成可用功能，以管理使用者設定檔和大量管理使用者產生的內容(UGC)。 啟用後， **UserUgcManagement** 服務可讓有權限的使用者（社群管理員和協調者）停用使用者設定檔，以及為特定使用者大量刪除或大量匯出UGC。 這些API也讓客戶資料的控制者和處理者能符合歐盟一般資料保護規範(GDPR)和其他GDPR啟發的隱私權規範。

如需詳細資訊，請參閱 [Adobe隱私權中心的GDPR頁面](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>如果您已設定 [Adobe Analytics在AEM Communities](/help/communities/analytics.md) 網站上，擷取的使用者資料會傳送至Adobe Analytics伺服器。 Adobe Analytics提供的API可讓您存取、匯出和刪除使用者資料，並遵守GDPR。 如需詳細資訊，請參閱 [提交存取和刪除請求](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-submit-access-delete.html).

若要使用這些API，您必須啟用 `/services/social/ugcmanagement` 端點，方法是啟用UserUgcManagement服務。 若要啟用此服務，請安裝 [範例servlet](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet) 可於 [GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet). 然後，使用類似以下的http要求，以適當的參數點擊您社群網站的發佈執行個體上的端點：

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`. 不過，您也可以建置UI（使用者介面），以管理使用者設定檔和使用者在系統中產生的內容。

這些API可執行下列功能。

## 擷取使用者的UGC {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver, String user, OutputStream outputStream)** 有助於從系統匯出使用者的所有UGC。

* **使用者**:使用者的可授權ID。
* **outputStream**:結果會以輸出資料流傳回，此為zip檔案，包含使用者產生的內容（如json檔案）和附件（包括使用者上傳的影像或影片）。

例如，若要匯出名為Weston McCall的使用者的UGC(使用weston.mccall@dodgit.com作為可授權ID來登入Communities網站)，您可以傳送類似下列的httpGET要求：

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## 刪除用戶的UGC {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, String user)** 有助於從系統中刪除某個用戶的所有UGC。

* **使用者**:使用者的可授權ID。

例如，若要透過http-POST請求刪除具有可授權ID weston.mccall@dodgit.com之使用者的UGC，請使用下列參數：

* 使用者 = `weston.mccall@dodgit.com`
* 操作 = `deleteUgc`

### 從Adobe Analytics刪除UGC {#delete-ugc-from-adobe-analytics}

若要從Adobe Analytics刪除使用者資料，請遵循 [GDPR Analytics工作流程](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html);因為API不會從Adobe Analytics刪除使用者資料。

若為AEM Communities使用的Adobe Analytics變數對應，請參閱下列影像：

![AEM Communities變數對應至Adobe Analytics](assets/analytics-communities-mapping.png)

## 停用使用者帳戶 {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, String user)** 有助於停用使用者帳戶。

* **使用者**:使用者的可授權ID。

>[!NOTE]
>
>禁用用戶將刪除用戶在伺服器上擁有的所有用戶生成的內容。

例如，若要刪除具有可授權ID之使用者的設定檔 `weston.mccall@dodgit.com` 透過http-POST要求，使用下列參數：

* 使用者 = `weston.mccall@dodgit.com`
* 操作 = `deleteUser`

>[!NOTE]
>
>deleteUserAccount()API僅會停用系統中的使用者設定檔，並移除UGC。 不過，若要從系統刪除使用者設定檔，請導覽至 **CRXDE Lite**: [https://&lt;server>/crx/de](https://localhost:4502/crx/de)，找出使用者節點並將其刪除。
