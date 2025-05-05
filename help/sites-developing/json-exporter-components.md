---
title: 為元件啟用 JSON 匯出
description: 元件可調整為根據模組化架構產生其內容的JSON匯出。
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
exl-id: 6d127e14-767e-46ad-aaeb-0ce9dd14d553
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 5%

---

# 為元件啟用 JSON 匯出{#enabling-json-export-for-a-component}

元件可調整為根據模組化架構產生其內容的JSON匯出。

## 概觀 {#overview}

JSON匯出是以[Sling模型](https://sling.apache.org/documentation/bundles/models.html)和[Sling模型匯出工具](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130)架構（本身依賴[Jackson註解](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)）為基礎。

這表示元件必須具有Sling模型（若元件必須匯出JSON）。 因此，請依照這兩個步驟，在任何元件上啟用JSON匯出。

* [為元件定義Sling模型](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [為Sling模型介面加上註釋](#annotate-the-sling-model-interface)

## 為元件定義Sling模型 {#define-a-sling-model-for-the-component}

首先，必須為元件定義Sling模型。

>[!NOTE]
>
>如需使用Sling模型的範例，請參閱[在AEM中開發Sling模型匯出工具](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html)。

Sling模型實作類別必須使用以下專案註釋：

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

這可確保您的元件可以使用`.model`選取器和`.json`副檔名自行匯出。

此外，這會指定Sling模型類別可以調整到`ComponentExporter`介面中。

>[!NOTE]
>
>Jackson註解不是在Sling模型類別層級指定的，而是在「模型」介面層級指定的。 這是為了確保將JSON匯出視為元件API的一部分。

>[!NOTE]
>
>`ExporterConstants`和`ComponentExporter`類別來自`com.adobe.cq.export.json`組合。

### 使用多個選擇器 {#multiple-selectors}

雖然這不是標準使用案例，但除了`model`選擇器之外，還可以設定多個選擇器。

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

不過，在這種情況下，`model`選取器必須是第一個選取器，副檔名必須是`.json`。

## 為Sling模型介面加上註釋 {#annotate-the-sling-model-interface}

若要讓JSON匯出工具架構考慮在內，模型介面應該實作`ComponentExporter`介面（如果存在容器元件，則為`ContainerExporter`）。

接著會使用[Jackson註解](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)標註相對應的Sling模型介面(`MyComponent`)，以定義應如何匯出（序列化）。

模型介面必須正確加上註解，以定義應該序列化哪些方法。 依預設，所有遵守getter一般命名慣例的方法都會序列化，並從getter名稱自然衍生其JSON屬性名稱。 使用`@JsonIgnore`或`@JsonProperty`重新命名JSON屬性可防止或覆寫此專案。

## 範例 {#example}

核心元件自核心元件[&#128279;](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant)發行版本1.1.0起便已支援JSON匯出，並可作為參考使用。

如需範例，請參閱影像核心元件的Sling模型實作及其附註介面。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* 在GitHub上[開啟aem-core-wcm-components專案](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components)
* 將專案下載為[ZIP檔](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/archive/master.zip)

## 相關檔案 {#related-documentation}

如需詳細資訊，請參閱下列內容：

* Assets使用手冊[&#128279;](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)中的內容片段主題

* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
* [使用內容片段製作](/help/sites-authoring/content-fragments.md)
* [內容服務的 JSON 匯出工具](/help/sites-developing/json-exporter.md)
* [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant)和[內容片段元件](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)
