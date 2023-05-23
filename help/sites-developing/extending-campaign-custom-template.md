---
title: 使用Adobe CampaignAEM表單元件建立自定義頁面模板
seo-title: Creating Custom AEM Page Template with Adobe Campaign Form Components
description: 生成使用Adobe Campaign表單元件的自定義頁面模板
seo-description: Build a custom page template that uses Adobe Campaign Form components
uuid: 8162ace2-b661-4c39-b0fb-288e1c035b9c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c3f6eed4-bbda-454a-88ce-c7f2041d4217
exl-id: de5c634a-c0d7-4e69-b941-d2fbfe83117d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 1%

---

# 使用Adobe CampaignAEM表單元件建立自定義頁面模板{#creating-custom-aem-page-template-with-adobe-campaign-form-components}

此頁說明如何生成使用 [Adobe Campaign窗體](/help/sites-authoring/adobe-campaign-components.md) 元件：檢查Geometrixx — 室外模板( `/apps/geometrixx-outdoors/components/page_campaign_profile`)，並指出建立您自己的自定義模板時可能需要的重要資訊。

>[!NOTE]
>
>[電子郵件和表單示例僅在Geometrixx中提供](/help/sites-developing/we-retail.md)。 請從包共用下載示例Geometrixx內容。

要使用Adobe CampaignAEM表單元件建立自定義頁面模板，請確保具有以下功能：

1. **正確的資源SuperType**

   確保頁面元件繼承自 `mcm/campaign/components/profile`。

   這是Servlet獲取和保存資訊所必需的

   * `com.day.cq.mcm.campaign.servlets.TemplateListServlet`
   * `com.day.cq.mcm.campaign.servlets.SaveProfileServlet`

   ![chlimage_1-201](assets/chlimage_1-201.png)

1. **ClientContext設定**

   查看客戶端上下文設定時( `/etc/designs/geometrixx-outdoors/jcr:content/page_campaign_profile`)您會看到以下設定：

   * ClientContext指向 `/etc/clientcontext/campaign`
   * 還有一個額外的 *配置* 的下界。

   ![chlimage_1-202](assets/chlimage_1-202.png)

1. **head.jsp(/apps/geometrixx-outdoors/components/page_campaign_profile/head.jsp)**

   在 **head.jsp**，您將看到以下使用 **客戶端上下文 — 配置** 和 **雲服務掛接**:

   ```
   <cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub"/>
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
   ```

1. **body.jsp(/apps/geometrixx-outdoors/components/page_campaign_profile/body.jsp)**

   在 **body.jsp**，雲服務載入到頁面底部：

   ```
   <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
   ```

1. **市場活動頁面屬性**

   要能夠選擇Adobe Campaign模板，使用 **活動** 頁籤：

   `/apps/geometrixx-outdoors/components/page_campaign_profile/dialog/items/tabs/items/campaign`

   ![chlimage_1-203](assets/chlimage_1-203.png)

1. **模板設定**。

   在模板中( `/apps/geometrixx-outdoors/templates/campaign_profile/jcr:content`)會看到以下預設值：

   | **acMapping** | mapRecipient(Adobe Campaign6.1)，簡介(Adobe Campaign Standard) |
   |---|---|
   | **acTemplateId** | 郵件 |

   ![chlimage_1-204](assets/chlimage_1-204.png)
