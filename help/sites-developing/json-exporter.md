---
title: 內容服務的JSON匯出器
seo-title: 內容服務的JSON匯出器
description: AEM Content Services的設計目的，是將AEM中／來自AEM的內容描述和傳送，從而延伸到網頁。 它們使用可供任何用戶端使用的標準化方法，將內容傳送至非傳統AEM網頁的頻道。
seo-description: AEM Content Services的設計目的，是將AEM中／來自AEM的內容描述和傳送，從而延伸到網頁。 它們使用可供任何用戶端使用的標準化方法，將內容傳送至非傳統AEM網頁的頻道。
uuid: be6457b1-fa9c-4f3b-b219-01a4afc239e7
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 4c7e33ea-f2d3-4d69-b676-aeb50c610d70
translation-type: tm+mt
source-git-commit: a430c4de89bde3b907d342106465d3b5a7c75cc8
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 4%

---


# 內容服務的JSON匯出器{#json-exporter-for-content-services}

AEM Content Services的設計目的，是將AEM中／來自AEM的內容描述和傳送，從而延伸到網頁。

它們使用可供任何用戶端使用的標準化方法，將內容傳送至非傳統AEM網頁的頻道。 這些渠道可以包括：

* [單頁應用程式](spa-walkthrough.md)
* 原生行動應用程式
* AEM外部的其他通道和觸點

透過使用結構化內容的內容片段，您可以使用JSON匯出器來提供內容服務，以JSON資料模型格式傳送(y)AEM頁面的內容。 然後，您自己的應用程式就可使用這個功能。

>[!NOTE]
>
>自[核心元件](https://docs.adobe.com/content/docs/en/core-components/v1.html)的&lt;a0/>1.1.0版以來，此處描述的功能可用於所有核心元件。

## 包含內容片段核心元件{#json-exporter-with-content-fragment-core-components}的JSON匯出器

使用AEM JSON匯出器，您可以以JSON資料模型格式傳送(y)AEM頁面的內容。 然後，您自己的應用程式就可使用這個功能。

在AEM中，傳送是使用選擇器`model`和`.json`擴充功能來完成。

`.model.json`

1. 例如，URL，例如：

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en.model.json
   ```

1. 將提供內容，例如：

   ![chlimage_1-112](assets/chlimage_1-192.png)

您也可以透過明確定位結構化內容片段來提供內容。

這是使用片段的整個路徑（透過`jcr:content`）完成；例如，加上尾碼，如。

`.../jcr:content/root/responsivegrid/contentfragment.model.json`

您的頁面可以包含單一內容片段或多種類型的元件。 您也可以使用清單元件等機制，自動搜尋相關內容。

* 例如，URL，例如：

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en/manchester-airport/jcr:content/root/responsivegrid/contentfragment.model.json
   ```

* 將提供內容，例如：

   ![chlimage_1-193](assets/chlimage_1-193.png)

   >[!NOTE]
   >
   >您可以[調整您自己的元件](/help/sites-developing/json-exporter-components.md)以存取和使用此資料。

   >[!NOTE]
   >
   >雖然不是標準實作，但支援[多個選擇器，](json-exporter-components.md#multiple-selectors)但`model`必須是第一個。

### 更多資訊 {#further-information}

另請參閱:

* Assets HTTP API

   * [Assets HTTP API](/help/assets/mac-api-assets.md)

* Sling Models:

   * [Sling Models —— 將模型類別與自130以來的資源類型關聯](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)

* AEM with JSON:

   * [以JSON格式取得頁面資訊](/help/sites-developing/pageinfo.md)

## 相關文檔{#related-documentation}

如需詳細資訊，請參閱：

* 資產使用指南](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)中的[內容片段主題

* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
* [使用內容片段製作](/help/sites-authoring/content-fragments.md)
* [為元件啟用JSON匯出](/help/sites-developing/json-exporter-components.md)

* [核心](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html) 元件和內 [容片段元件](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)

