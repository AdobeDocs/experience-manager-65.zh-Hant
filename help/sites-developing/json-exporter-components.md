---
title: 為元件啟用 JSON 匯出
description: 元件可調整為根據模組化架構產生其內容的JSON匯出。
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
exl-id: 6d127e14-767e-46ad-aaeb-0ce9dd14d553
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 5%

---

# 為元件啟用 JSON 匯出{#enabling-json-export-for-a-component}

元件可調整為根據模組化架構產生其內容的JSON匯出。

## 概觀 {#overview}

JSON匯出是根據 [Sling模型](https://sling.apache.org/documentation/bundles/models.html)，並在上 [Sling模型匯出工具](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) 框架(本身依賴 [Jackson註解](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations))。

這表示元件必須具有Sling模型（若元件必須匯出JSON）。 因此，請依照這兩個步驟，在任何元件上啟用JSON匯出。

* [為元件定義Sling模型](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [為Sling模型介面加上註釋](#annotate-the-sling-model-interface)

## 為元件定義Sling模型 {#define-a-sling-model-for-the-component}

首先，必須為元件定義Sling模型。

>[!NOTE]
>
>如需使用Sling模型的範例，請參閱 [在AEM中開發Sling模型匯出工具](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html).

Sling模型實作類別必須使用以下專案註釋：

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

這可確保您的元件可自行匯出，並使用 `.model` 選擇器和 `.json` 副檔名。

此外，這會指定Sling模型類別可以調整到 `ComponentExporter` 介面。

>[!NOTE]
>
>Jackson註解不是在Sling模型類別層級指定的，而是在「模型」介面層級指定的。 這是為了確保將JSON匯出視為元件API的一部分。

>[!NOTE]
>
>此 `ExporterConstants` 和 `ComponentExporter` 類別來自 `com.adobe.cq.export.json` 套件組合。

### 使用多個選擇器 {#multiple-selectors}

雖然這不是標準使用案例，但除了以下設定外，您也可以設定多個選取器： `model` 選擇器。

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

但在這種情況下， `model` 選取器必須是第一個選取器，而擴充功能必須是 `.json`.

## 為Sling模型介面加上註釋 {#annotate-the-sling-model-interface}

若要JSON匯出程式架構列入考量，模型介面應實作 `ComponentExporter` 介面(或 `ContainerExporter`，如果有容器元件)。

對應的Sling模型介面( `MyComponent`)之後會使用進行註解 [Jackson註解](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) 以定義應如何匯出（序列化）。

模型介面必須正確加上註解，以定義應該序列化哪些方法。 依預設，所有遵守getter一般命名慣例的方法都會序列化，並從getter名稱自然衍生其JSON屬性名稱。 這可以使用防止或覆寫 `@JsonIgnore` 或 `@JsonProperty` 重新命名JSON屬性。

## 範例 {#example}

核心元件自發行以來皆支援JSON匯出 [1.1.0核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant) 和可作為參考。

如需範例，請參閱影像核心元件的Sling模型實作及其附註介面。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-core-wcm-components專案](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/archive/master.zip)

## 相關檔案 {#related-documentation}

如需詳細資訊，請參閱下列內容：

* 此 [Assets使用手冊中的內容片段主題](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
* [使用內容片段製作](/help/sites-authoring/content-fragments.md)
* [內容服務的 JSON 匯出工具](/help/sites-developing/json-exporter.md)
* [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant) 和 [內容片段元件](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)
