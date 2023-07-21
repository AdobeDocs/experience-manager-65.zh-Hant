---
title: 內容服務的 JSON 匯出工具
description: AEM Content Services旨在概括AEM內/外內容的說明和傳遞，而不只是關注網頁。 它們使用可供任何使用者端使用的標準化方法，將內容傳送至非傳統AEM網頁的管道。
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
exl-id: 647395c0-f392-427d-a998-e9ddf722b9f9
source-git-commit: a56d5121a6ce11b42a6c30dae9e479564d16af27
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 11%

---

# 內容服務的 JSON 匯出工具{#json-exporter-for-content-services}

AEM Content Services旨在概括AEM內/外內容的說明和傳遞，而不只是關注網頁。

它們使用可供任何使用者端使用的標準化方法，將內容傳送至非傳統AEM網頁的管道。 這些管道可包括：

* [單頁應用程式](spa-walkthrough.md)
* 原生行動應用程式
* AEM外部的其他管道和接觸點

對於使用結構化內容的內容片段，您可以使用JSON匯出工具提供內容服務，以JSON資料模型格式傳送任何AEM頁面的內容。 然後，您自己的應用程式就可以使用此方法。

>[!NOTE]
>
>此處說明的功能適用於以下期間的所有核心元件： [核心元件1.1.0版](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant).

## 具有內容片段核心元件的JSON匯出工具 {#json-exporter-with-content-fragment-core-components}

您可以使用AEM JSON匯出工具，以JSON資料模型格式傳遞任何AEM頁面的內容。 然後，您自己的應用程式就可以使用此方法。

在AEM中，傳遞是透過選擇器達成 `model` 和 `.json` 副檔名。

`.model.json`

1. 例如，URL，例如：

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en.model.json
   ```

1. 提供下列內容：

   ![chlimage_1-192](assets/chlimage_1-192.png)

或者，您可以透過特別定位來傳送結構化內容片段的內容。

使用片段的整個路徑(透過 `jcr:content`)；例如，尾碼為。

`.../jcr:content/root/responsivegrid/contentfragment.model.json`

您的頁面可包含單一內容片段或多個不同型別的元件。 您也可以使用清單元件等機制來自動搜尋相關內容。

* 例如，URL，例如：

  ```shell
  http://localhost:4502/content/we-retail/language-masters/en/manchester-airport/jcr:content/root/responsivegrid/contentfragment.model.json
  ```

* 提供下列內容：

  ![chlimage_1-193](assets/chlimage_1-193.png)

  >[!NOTE]
  >
  >您可以 [調整您自己的元件](/help/sites-developing/json-exporter-components.md) 以存取及使用此資料。

  >[!NOTE]
  >
  >雖然不是標準實作， [支援多個選擇器，](json-exporter-components.md#multiple-selectors) 但是 `model` 必須為第一個。

### 更多資訊 {#further-information}

另請參閱:

* Assets HTTP API

   * [Assets HTTP API](/help/assets/mac-api-assets.md)

* Sling 模型:

   * [Sling模型 — 自130起將模型類別與資源型別建立關聯](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)

* 使用JSON的AEM：

   * [取得JSON格式的頁面資訊](/help/sites-developing/pageinfo.md)

## 相關檔案 {#related-documentation}

如需詳細資訊，請參閱：

* 此 [Assets使用手冊中的內容片段主題](/help/assets/content-fragments/content-fragments.md)

* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
* [使用內容片段編寫](/help/sites-authoring/content-fragments.md)
* [為元件啟用 JSON 匯出](/help/sites-developing/json-exporter-components.md)

* [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 和 [內容片段元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=en)
