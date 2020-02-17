---
title: AEM Communities中的使用者與UGC管理服務
seo-title: AEM Communities中的使用者與UGC管理服務
description: 使用API大量刪除和大量匯出使用者產生的內容，並停用使用者帳戶。
seo-description: 使用API大量刪除和大量匯出使用者產生的內容，並停用使用者帳戶。
uuid: 91180659-617d-4f6c-9a07-e680770d0d8f
contentOwner: mgulati
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
discoiquuid: d305821d-1371-4e4a-8b28-8eee8fafa43b
docset: aem65
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780

---


# AEM Communities中的使用者與UGC管理服務{#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>GDPR在以下幾節中是以範例形式使用，但涵蓋的詳細資訊適用於所有資料保護和隱私權法規；例如GDPR、CCPA等。

AEM Communities提供現成可用的API，以管理使用者設定檔並大量管理使用者產生的內容(UGC)。 啟用後， **UserUgcManagement** service可讓特權使用者（社群管理員和協調者）停用使用者設定檔，並針對特定使用者大量刪除或大量匯出UGC。 這些API還讓客戶資料的掌控者和處理者能夠遵守歐盟的通用資料保護法規(GDPR)和其他受GDPR啟發的隱私權法規。

如需詳細資訊，請 [參閱Adobe隱私權中心的GDPR頁面](https://www.adobe.com/privacy/general-data-protection-regulation.html)。

>[!NOTE]
>
>如果您在 [AEM Communities網站中設定了Adobe Analytics](/help/communities/analytics.md) ，則擷取的使用者資料會傳送至Adobe Analytics伺服器。 Adobe Analytics提供API，可讓您存取、匯出和刪除使用者資料，並符合GDPR。 如需詳細資訊，請參 [閱提交存取權和刪除請求](https://marketing.adobe.com/resources/help/en_US/analytics/gdpr/gdpr_submit_access_delete.html)。

若要使用這些API，您必須啟用 **UserUgcManagement服務，以啟用** /services/social/ugcmanagement端點。 若要啟動此服務，請安 [裝](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-ugc-management-servlet) GitHub.com上提供的範例servlet [](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/master/bundles/communities-ugc-management-servlet)。 然後，使用http請求，使用適當的參數點擊社群網站發佈例項的端點，類似於

**https://localhost:port/services/social/ugcmanagement?user=&lt;可授權ID>&amp;operation=&lt;getUgc>**。 不過，您也可以建立UI（使用者介面）來管理系統中的使用者設定檔和使用者產生的內容。

這些API可執行下列功能。

## 擷取使用者的UGC {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver, String user, OutputStream)**幫助從系統中導出用戶的所有UGC。

* **用戶**:使用者的可授權ID。
* **outputStream**:結果會傳回為輸出串流，此為包含使用者產生之內容（如json檔案）和附件（包括使用者上傳的影像或視訊）的zip檔案。

例如，若要匯出名為Weston mcCall的使用者的UGC，而使用weston.mccall@dodgit.com做為可授權的ID來登入社群網站，您可以傳送類似下列的http GET要求：

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## 刪除用戶的UGC {#delete-the-ugc-of-a-user}

**deleteUserUgc(ResourceResolver resourceResolver, String user)**幫助從系統中刪除用戶的所有UGC。

* **用戶**:使用者的可授權ID。

例如，若要透過http-POST請求刪除具有可授權ID weston.mccall@dodgit.com的使用者的UGC，請使用下列參數：

* user=weston.mccall@dodgit.com
* operation= deleteUgc

### 從Adobe Analytics刪除UGC {#delete-ugc-from-adobe-analytics}

若要從Adobe Analytics刪除使用者資料，請遵循 [GDPR Analytics工作流程](https://marketing.adobe.com/resources/help/en_US/analytics/gdpr/an_gdpr_workflow.html);因為API不會從Adobe Analytics刪除使用者資料。

如需AEM Communities所使用的Adobe Analytics變數映射，請參閱下列影像：

![Adobe Analytics的AEM社群變數對應](assets/analytics-communities-mapping.png)

## 停用使用者帳戶 {#disable-a-user-account}

**deleteUserAccount(ResourceResolver resourceResolver, String user)**幫助禁用用戶帳戶。

* **用戶**:使用者的可授權ID。

>[!NOTE]
>
>停用使用者會刪除使用者在伺服器上產生的所有內容。

例如，若要透過http-POST請求刪除具有可授權ID weston.mccall@dodgit.com的使用者的設定檔，請使用下列參數：

* user=weston.mccall@dodgit.com
* operation= deleteUser

>[!NOTE]
>
>deleteUserAccount()API只會停用系統中的使用者設定檔，並移除UGC。 不過，若要從系統刪除使用者描述檔，請導覽至 **CRXDE Lite**: [https://&lt;server>/crx/de](https://localhost:4502/crx/de)，找出用戶節點並將其刪除。

