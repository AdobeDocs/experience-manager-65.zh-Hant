---
title: AEM Communities用戶和UGC管理服務
seo-title: User and UGC Management Service in AEM Communities
description: 使用API批量刪除和批量導出用戶生成的內容，並禁用用戶帳戶。
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
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 1%

---

# AEM Communities用戶和UGC管理服務 {#user-and-ugc-management-service-in-aem-communities}

>[!IMPORTANT]
>
>GDPR在以下各節中用作示例，但所涵蓋的詳細資訊適用於所有資料保護和隱私法規；如GDPR、CCPA等。

AEM Communities公開了現成的API來管理用戶配置檔案和批量管理用戶生成的內容(UGC)。 啟用後， **用戶Ugc管理** 該服務允許特權用戶（社區管理員和審核人）禁用用戶配置檔案，並允許特定用戶批量刪除或批量導出UGC。 這些API還使客戶資料的控制器和處理器能夠遵守歐盟的一般資料保護法規(GDPR)和其他受GDPR啟發的隱私法規。

有關詳細資訊，請參閱 [Adobe隱私中心的GDPR頁](https://www.adobe.com/privacy/general-data-protection-regulation.html)。

>[!NOTE]
>
>如果已配置 [Adobe AnalyticsAEM Communities](/help/communities/analytics.md) 站點，捕獲的用戶資料被發送到Adobe Analytics伺服器。 Adobe Analytics提供API，允許您訪問、導出和刪除用戶資料並遵守GDPR。 有關詳細資訊，請參見 [提交訪問和刪除請求](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-submit-access-delete.html)。

要使用這些API，需要啟用 `/services/social/ugcmanagement` 通過激活UserUgcManagement服務來終結點。 要激活此服務，請安裝 [示例servlet](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet) 可用 [GitHub.com](https://github.com/Adobe-Marketing-Cloud/aem-communities-ugc-migration/tree/main/bundles/communities-ugc-management-servlet)。 然後，使用與以下內容類似的http請求，使用適當的參數在社區站點的發佈實例上按一下終結點：

`https://localhost:port/services/social/ugcmanagement?user=<authorizable ID>&operation=<getUgc>`。但是，您也可以構建UI（用戶介面）來管理系統中的用戶配置檔案和用戶生成的內容。

這些API可以執行以下函式。

## 檢索用戶的UGC {#retrieve-the-ugc-of-a-user}

**getUserUgc(ResourceResolver resourceResolver, String user, OutputStream outputStream)** 幫助從系統導出用戶的所有UGC。

* **用戶**:用戶的可授權ID。
* **輸出流**:結果作為輸出流返回，該流是包含用戶生成的內容（作為json檔案）和附件（包括用戶上傳的影像或視頻）的zip檔案。

例如，要導出名為Weston McCall的用戶的UGC，該用戶使用weston.mccall@dodgit.com作為可授權的ID登錄到社區站點，您可以發送類似於以下內容的httpGET請求：

`https://localhost:port/services/social/ugcmanagement?user=weston.mccall@dodgit.com&operation=getUgc`

## 刪除用戶的UGC {#delete-the-ugc-of-a-user}

**deleteUserUgc（ResourceResolver resourceResolver，字串用戶）** 幫助從系統中刪除用戶的所有UGC。

* **用戶**:用戶的可授權ID。

例如，要通過http-POST請求刪除具有可授權ID weston.mccall@dodgit.com的用戶的UGC，請使用以下參數：

* 使用者 = `weston.mccall@dodgit.com`
* 操作 = `deleteUgc`

### 從Adobe Analytics刪除UGC {#delete-ugc-from-adobe-analytics}

要從Adobe Analytics刪除用戶資料，請 [GDPR分析工作流](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-workflow.html);因為API不會從Adobe Analytics刪除用戶資料。

有關AEM Communities使用的Adobe Analytics變數映射，請參閱以下影像：

![AEMAdobe Analytics社區變數映射](assets/analytics-communities-mapping.png)

## 禁用用戶帳戶 {#disable-a-user-account}

**deleteUserAccount（ResourceResolver resourceResolver，字串用戶）** 幫助禁用用戶帳戶。

* **用戶**:用戶的可授權ID。

>[!NOTE]
>
>禁用用戶將刪除用戶在伺服器上生成的所有內容。

例如，刪除具有可授權ID的用戶的配置檔案 `weston.mccall@dodgit.com` 通過http-POST請求，使用以下參數：

* 使用者 = `weston.mccall@dodgit.com`
* 操作 = `deleteUser`

>[!NOTE]
>
>deleteUserAccount()API僅禁用系統中的用戶配置檔案並刪除UGC。 但是，要從系統中刪除用戶配置檔案，請導航到 **CRXDE Lite**: [https://&lt;server>/crx/de](https://localhost:4502/crx/de)，找到用戶節點並將其刪除。
