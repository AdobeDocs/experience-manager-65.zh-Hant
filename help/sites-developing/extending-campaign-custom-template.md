---
title: 使用Adobe Campaign表單元件建立自訂AEM頁面範本
seo-title: 使用Adobe Campaign表單元件建立自訂AEM頁面範本
description: 建立使用Adobe Campaign表單元件的自訂頁面範本
seo-description: 建立使用Adobe Campaign表單元件的自訂頁面範本
uuid: 8162ace2-b661-4c39-b0fb-288e1c035b9c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c3f6eed4-bbda-454a-88ce-c7f2041d4217
exl-id: de5c634a-c0d7-4e69-b941-d2fbfe83117d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# 使用Adobe Campaign表單元件建立自訂AEM頁面範本{#creating-custom-aem-page-template-with-adobe-campaign-form-components}

本頁面說明如何透過檢查Geometrixx — 戶外範本(`/apps/geometrixx-outdoors/components/page_campaign_profile`)的實作方式，建立使用[Adobe Campaign表單](/help/sites-authoring/adobe-campaign-components.md)元件的自訂頁面範本，並指出建立自己的自訂範本時可能需要的重要資訊。

>[!NOTE]
>
>[電子郵件和表單範例僅可在](/help/sites-developing/we-retail.md)中取得。請從「封裝共用」下載Geometrixx內容範例。

若要使用Adobe Campaign表單元件建立自訂AEM頁面範本，請確定您有下列項目：

1. **正確的resourceSuperType**

   確保page-component繼承自`mcm/campaign/components/profile`。

   這是servlet取得和儲存資訊的必要條件

   * `com.day.cq.mcm.campaign.servlets.TemplateListServlet`
   * `com.day.cq.mcm.campaign.servlets.SaveProfileServlet`

   ![chlimage_1-201](assets/chlimage_1-201.png)

1. **ClientContext設定**

   查看clientcontext設定(`/etc/designs/geometrixx-outdoors/jcr:content/page_campaign_profile`)時，您會看到下列設定：

   * ClientContext指向`/etc/clientcontext/campaign`
   * 還有一個額外的&#x200B;*config*&#x200B;節點。

   ![chlimage_1-202](assets/chlimage_1-202.png)

1. **head.jsp(/apps/geometrixx-outdoors/components/page_campaign_profile/head.jsp)**

   在&#x200B;**head.jsp**&#x200B;中，您會看到下列使用&#x200B;**clientcontext-config**&#x200B;和&#x200B;**cloudservice-hook**&#x200B;的行：

   ```
   <cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub"/>
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
   ```

1. **body.jsp(/apps/geometrixx-outdoors/components/page_campaign_profile/body.jsp)**

   在&#x200B;**body.jsp**&#x200B;中，雲端服務會載入至頁面底部：

   ```
   <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
   ```

1. **促銷活動頁面屬性**

   若要能選取Adobe Campaign範本，頁面屬性會以&#x200B;**Campaign**&#x200B;標籤進行擴充：

   `/apps/geometrixx-outdoors/components/page_campaign_profile/dialog/items/tabs/items/campaign`

   ![chlimage_1-203](assets/chlimage_1-203.png)

1. **範本設定**。

   在範本(`/apps/geometrixx-outdoors/templates/campaign_profile/jcr:content`)中，您會看到下列預設值：

   | **acMapping** | mapRecipient(適用於Adobe Campaign 6.1)、設定檔(適用於Adobe Campaign Standard) |
   |---|---|
   | **acTemplateId** | 郵件 |

   ![chlimage_1-204](assets/chlimage_1-204.png)
