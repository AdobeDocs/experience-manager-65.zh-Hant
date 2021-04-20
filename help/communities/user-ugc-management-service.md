---
title: 用戶與AEM CommunitiesUGC管理服務
seo-title: 用戶與AEM CommunitiesUGC管理服務
description: 使用API大量刪除和大量匯出使用者產生的內容，並停用使用者帳戶。
seo-description: 使用API大量刪除和大量匯出使用者產生的內容，並停用使用者帳戶。
uuid: 91180659-617d-4f6c-9a07-e680770d0d8f
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
discoiquuid: d305821d-1371-4e4a-8b28-8eee8fafa43b
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---


# AEM Communities的用戶和UGC管理服務{#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>GDPR在以下幾節中是以範例形式使用，但涵蓋的詳細資訊適用於所有資料保護和隱私權法規；例如GDPR、CCPA等。

AEM Communities公開現成可用的API，以管理使用者個人檔案並大量管理使用者產生的內容(UGC)。 啟用後，**UserUgcManagement**&#x200B;服務可讓特權使用者（社群管理員和協調者）停用使用者設定檔，並大量刪除或大量匯出特定使用者的UGC。 這些API還讓客戶資料的掌控者和處理者能夠遵守歐盟的通用資料保護法規(GDPR)和其他受GDPR啟發的隱私權法規。

如需詳細資訊，請參閱Adobe隱私中心](https://www.adobe.com/privacy/general-data-protection-regulation.html)的[ GDPR頁面。

>[!NOTE]
>
>如果您在AEM Communities](/help/communities/analytics.md)網站中設定[Adobe Analytics，則擷取的使用者資料會傳送至Adobe Analytics伺服器。 Adobe Analytics提供API，可讓您存取、匯出和刪除使用者資料，並符合GDPR。 如需詳細資訊，請參閱[提交存取和刪除請求](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/gdpr-submit-access-delete.html)。

若要使用這些API，您必須啟用UserUgcManagement服務以啟用`/services/social/ugcmanagement`端點。 要激活此服務，請安裝[GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet)上提供的[示例servlet](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet)。 然後，使用http請求，以適當參數點擊社群網站發佈例項上的端點，類似：

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`. 不過，您也可以建立UI（使用者介面）來管理系統中的使用者設定檔和使用者產生的內容。

這些API可執行下列功能。

## 檢索用戶{#retrieve-the-ugc-of-a-user}的UGC

**getUserUgc(ResourceResolver resourceResolver, String user, OutputStream)** 有助於從系統中導出用戶的所有UGC。

* **用戶**:使用者的可授權ID。
* **outputStream**:結果會傳回為輸出串流，此為包含使用者產生之內容（如json檔案）和附件（包括使用者上傳的影像或視訊）的zip檔案。

例如，若要匯出名為Weston McCall的使用者的UGC(使用weston.mccall@dodgit.com做為可授權的ID來登入社群網站)，您可以傳送類似下列的httpGET要求：

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## 刪除用戶{#delete-the-ugc-of-a-user}的UGC

**deleteUserUgc(ResourceResolver resourceResolver, String user)** 有助於從系統中刪除用戶的所有UGC。

* **用戶**:使用者的可授權ID。

例如，若要透過http-POST請求刪除具有可授權ID weston.mccall@dodgit.com的使用者的UGC，請使用下列參數：

* 使用者 = `weston.mccall@dodgit.com`
* 操作 = `deleteUgc`

### 從Adobe Analytics刪除UGC {#delete-ugc-from-adobe-analytics}

若要從Adobe Analytics刪除使用者資料，請遵循[GDPR Analytics工作流程](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-workflow.html);因為API不會刪除來自Adobe Analytics的使用者資料。

對於AEM Communities使用的Adobe Analytics變數映射，請參閱以下影像：

![AEMAdobe Analytics社區變數映射](assets/analytics-communities-mapping.png)

## 禁用用戶帳戶{#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, String user)有助於** 禁用用戶帳戶。

* **用戶**:使用者的可授權ID。

>[!NOTE]
>
>停用使用者會刪除使用者在伺服器上產生的所有內容。

例如，若要透過http-POST請求刪除可授權ID為`weston.mccall@dodgit.com`的使用者的設定檔，請使用下列參數：

* 使用者 = `weston.mccall@dodgit.com`
* 操作 = `deleteUser`

>[!NOTE]
>
>deleteUserAccount()API只會停用系統中的使用者設定檔，並移除UGC。 但是，要從系統中刪除用戶配置檔案，請導航至&#x200B;**CRXDE Lite**:[https://&lt;server>/crx/de](https://localhost:4502/crx/de)，找出使用者節點並加以刪除。
