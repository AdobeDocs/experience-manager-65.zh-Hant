---
title: 為元件啟用JSON匯出
seo-title: Enabling JSON Export for a Component
description: 元件可適合根據建模器架構產生其內容的JSON匯出。
seo-description: Components can be adapted to generate JSON export of their content based on a modeler framework.
uuid: d7cc3347-2adb-4ea5-94a4-a847a2e66d28
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 448ad337-d4bb-4603-a27b-77da93feadbd
exl-id: 6d127e14-767e-46ad-aaeb-0ce9dd14d553
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 4%

---

# 為元件啟用JSON匯出{#enabling-json-export-for-a-component}

元件可適合根據建模器架構產生其內容的JSON匯出。

## 總覽 {#overview}

JSON匯出以 [Sling模型](https://sling.apache.org/documentation/bundles/models.html)，和 [Sling模型導出器](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) 框架(本身依賴 [傑克森注釋](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations))。

這表示如果元件需要匯出JSON，則必須有Sling模型。 因此，您需要依照這兩個步驟，對任何元件啟用JSON匯出。

* [為元件定義Sling模型](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [註解Sling模型介面](#annotate-the-sling-model-interface)

## 為元件定義Sling模型 {#define-a-sling-model-for-the-component}

首先，必須為元件定義Sling模型。

>[!NOTE]
>
>如需使用Sling模型的範例，請參閱文章 [在AEM中開發Sling模型匯出工具](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/sling-model-exporter-tutorial-develop.html).

Sling Model實作類別必須加上下列註解：

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

這可確保您的元件可以自行匯出，使用 `.model` 選取器和 `.json` 擴充功能。

此外，這會指定Sling Model類別可調整至 `ComponentExporter` 介面。

>[!NOTE]
>
>Jackson註解通常不會在Sling Model類別層級指定，而是在Model介面層級指定。 這是為了確保將JSON匯出視為元件API的一部分。

>[!NOTE]
>
>此 `ExporterConstants` 和 `ComponentExporter` 課程來自 `com.adobe.cq.export.json` 捆綁。

### 使用多個選取器 {#multiple-selectors}

雖然不是標準使用案例，但除了 `model` 選取器。

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

然而，在這種情況下， `model` 選取器必須是第一個選取器，擴充功能必須是 `.json`.

## 註解Sling模型介面 {#annotate-the-sling-model-interface}

若要納入JSON匯出工具架構，模型介面應實作 `ComponentExporter` 介面(或 `ContainerExporter`，若為容器元件)。

對應的Sling模型介面( `MyComponent`)，則會使用 [傑克森注釋](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) 以定義匯出（序列化）的方式。

需要正確注釋「模型」介面，以定義應序列化哪些方法。 預設情況下，所有遵循getter通常命名慣例的方法都將序列化，並且會從getter名稱自然導出其JSON屬性名稱。 可以使用 `@JsonIgnore` 或 `@JsonProperty` 重新命名JSON屬性。

## 範例 {#example}

核心元件自發行以來就支援JSON匯出 [核心元件1.1.0](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html) 和可作為參考。

如需範例，請參閱影像核心元件及其註解介面的Sling模型實作。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-core-wcm-components專案](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/archive/master.zip)

## 相關檔案 {#related-documentation}

如需詳細資訊，請參閱：

* 此 [資產使用手冊中的內容片段主題](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
* [使用內容片段製作](/help/sites-authoring/content-fragments.md)
* [內容服務的JSON匯出工具](/help/sites-developing/json-exporter.md)
* [核心元件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) 和 [內容片段元件](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)
