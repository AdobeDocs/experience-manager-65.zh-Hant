---
title: 內容服務的 JSON 匯出工具
seo-title: JSON Exporter for Content Services
description: Content Services旨在AEM將內容的描述和交付範圍從關注網AEM頁的範圍延伸出來。 它們使用可供任何客戶使用的標準化方法，將內AEM容交付到非傳統網頁的渠道。
seo-description: AEM Content Services are designed to generalize the description and delivery of content in/from AEM beyond a focus on web pages. They provide the delivery of content to channels that are not traditional AEM web pages, using standardized methods that can be consumed by any client.
uuid: be6457b1-fa9c-4f3b-b219-01a4afc239e7
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 4c7e33ea-f2d3-4d69-b676-aeb50c610d70
exl-id: 647395c0-f392-427d-a998-e9ddf722b9f9
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 11%

---

# 內容服務的 JSON 匯出工具{#json-exporter-for-content-services}

Content Services旨在AEM將內容的描述和交付範圍從關注網AEM頁的範圍延伸出來。

它們使用可供任何客戶使用的標準化方法，將內AEM容交付到非傳統網頁的渠道。 這些渠道可以包括：

* [單頁應用程式](spa-walkthrough.md)
* 本機移動應用程式
* 外部的其它通道和觸AEM點

使用使用結構化內容的內容片段，您可以通過使用JSON導出器以JSON資料模型格式傳遞任AEM何頁的內容來提供內容服務。 然後，您自己的應用程式可以使用此方法。

>[!NOTE]
>
>此處描述的功能適用於所有核心元件，因為 [1.1.0版核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant)。

## 包含內容片段核心元件的JSON導出器 {#json-exporter-with-content-fragment-core-components}

使用AEMJSON導出器，可以以JSON資料模型格式AEM傳遞任何頁的內容。 然後，您自己的應用程式可以使用此方法。

在中AEM，使用選擇器實現遞送 `model` 和 `.json` 擴展。

`.model.json`

1. 例如，URL，如：

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en.model.json
   ```

1. 提供內容，如：

   ![chlimage_1-192](assets/chlimage_1-192.png)

或者，可以通過將結構化內容片段的內容指定為特定目標來傳遞該內容。

使用片段的整個路徑(通過 `jcr:content`);例如，帶有尾碼，如。

`.../jcr:content/root/responsivegrid/contentfragment.model.json`

您的頁面可以包含單個內容片段或多種類型的多個元件。 也可以使用清單元件等機制自動搜索相關內容。

* 例如，URL，如：

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en/manchester-airport/jcr:content/root/responsivegrid/contentfragment.model.json
   ```

* 提供內容，如：

   ![chlimage_1-193](assets/chlimage_1-193.png)

   >[!NOTE]
   >
   >你可以 [調整自己的元件](/help/sites-developing/json-exporter-components.md) 訪問和使用此資料。

   >[!NOTE]
   >
   >雖然不是標準實施， [支援多個選擇器，](json-exporter-components.md#multiple-selectors) 但 `model` 肯定是第一個。

### 更多資訊 {#further-information}

另請參閱:

* Assets HTTP API

   * [Assets HTTP API](/help/assets/mac-api-assets.md)

* Sling 模型:

   * [Sling Models — 將模型類與自130以來的資源類型關聯](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)

* AEMJSON:

   * [獲取JSON格式的頁資訊](/help/sites-developing/pageinfo.md)

## 相關文檔 {#related-documentation}

有關詳細資訊，請參閱：

* 的 [資產使用手冊中的內容片段主題](/help/assets/content-fragments/content-fragments.md)

* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
* [使用內容片段創作](/help/sites-authoring/content-fragments.md)
* [為元件啟用 JSON 匯出](/help/sites-developing/json-exporter-components.md)

* [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 和 [內容片段元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=en)
