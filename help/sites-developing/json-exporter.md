---
title: 內容服務的JSON匯出工具
seo-title: JSON Exporter for Content Services
description: AEM Content Services的設計目的，是為了將AEM中/來自的內容的說明和傳送，歸納為網頁上的重點以外。 它們使用可供任何用戶端使用的標準化方法，將內容傳遞至非傳統AEM網頁的頻道。
seo-description: AEM Content Services are designed to generalize the description and delivery of content in/from AEM beyond a focus on web pages. They provide the delivery of content to channels that are not traditional AEM web pages, using standardized methods that can be consumed by any client.
uuid: be6457b1-fa9c-4f3b-b219-01a4afc239e7
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 4c7e33ea-f2d3-4d69-b676-aeb50c610d70
exl-id: 647395c0-f392-427d-a998-e9ddf722b9f9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 5%

---

# 內容服務的JSON匯出工具{#json-exporter-for-content-services}

AEM Content Services的設計目的，是為了將AEM中/來自的內容的說明和傳送，歸納為網頁上的重點以外。

它們使用可供任何用戶端使用的標準化方法，將內容傳遞至非傳統AEM網頁的頻道。 這些管道可包括：

* [單頁應用程式](spa-walkthrough.md)
* 原生行動應用程式
* AEM外部的其他通道和接觸點

透過使用結構化內容的內容片段，您可以使用JSON匯出工具以JSON資料模型格式傳送(y)AEM頁面的內容，以提供內容服務。 然後，您自己的應用程式就可以使用此功能。

>[!NOTE]
>
>此處描述的功能適用於所有核心元件， [核心元件1.1.0版](https://docs.adobe.com/content/docs/en/core-components/v1.html).

## 包含內容片段核心元件的JSON匯出工具 {#json-exporter-with-content-fragment-core-components}

使用AEM JSON匯出工具，您可以以JSON資料模型格式傳送(y)AEM頁面的內容。 然後，您自己的應用程式就可以使用此功能。

在AEM內使用選取器來達到傳送 `model` 和 `.json` 擴充功能。

`.model.json`

1. 例如，URL，例如：

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en.model.json
   ```

1. 將提供以下內容：

   ![chlimage_1-192](assets/chlimage_1-192.png)

或者，您可以明確鎖定結構化內容片段，以傳送其內容。

這是使用片段的整個路徑(透過 `jcr:content`);例如尾碼為，例如。

`.../jcr:content/root/responsivegrid/contentfragment.model.json`

您的頁面可以包含單一內容片段或多種類型的元件。 您也可以使用清單元件等機制來自動搜尋相關內容。

* 例如，URL，例如：

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en/manchester-airport/jcr:content/root/responsivegrid/contentfragment.model.json
   ```

* 將提供以下內容：

   ![chlimage_1-193](assets/chlimage_1-193.png)

   >[!NOTE]
   >
   >您可以 [調整您自己的元件](/help/sites-developing/json-exporter-components.md) 來存取和使用此資料。

   >[!NOTE]
   >
   >雖然不是標準實作， [支援多個選取器，](json-exporter-components.md#multiple-selectors) 但 `model` 必須是第一個。

### 更多資訊 {#further-information}

另請參閱:

* Assets HTTP API

   * [Assets HTTP API](/help/assets/mac-api-assets.md)

* Sling 模型:

   * [Sling模型 — 將模型類與自130年以來的資源類型關聯](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)

* AEM與JSON:

   * [取得JSON格式的頁面資訊](/help/sites-developing/pageinfo.md)

## 相關檔案 {#related-documentation}

如需詳細資訊，請參閱：

* 此 [資產使用手冊中的內容片段主題](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
* [使用內容片段製作](/help/sites-authoring/content-fragments.md)
* [為元件啟用JSON匯出](/help/sites-developing/json-exporter-components.md)

* [核心元件](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html) 和 [內容片段元件](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)
