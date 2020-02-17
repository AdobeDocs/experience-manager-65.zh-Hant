---
title: 為元件啟用JSON匯出
seo-title: 為元件啟用JSON匯出
description: 元件可以根據建模器架構來產生其內容的JSON匯出。
seo-description: 元件可以根據建模器架構來產生其內容的JSON匯出。
uuid: d7cc3347-2adb-4ea5-94a4-a847a2e66d28
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 448ad337-d4bb-4603-a27b-77da93feadbd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 為元件啟用JSON匯出{#enabling-json-export-for-a-component}

元件可以根據建模器架構來產生其內容的JSON匯出。

## 概覽 {#overview}

JSON Export是以 [Sling Models](https://sling.apache.org/documentation/bundles/models.html)，以及 [Sling Model Exporter](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) framework(本身需仰賴 [Jackson註解](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations))為基礎。

這表示如果元件需要匯出JSON，它必須有Sling Model。 因此，您必須依照這兩個步驟，在任何元件上啟用JSON匯出。

* [為元件定義Sling模型](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [註解Sling Model介面](#annotate-the-sling-model-interface)

## 為元件定義Sling模型 {#define-a-sling-model-for-the-component}

首先，必須為元件定義Sling Model。

>[!NOTE]
>
>如需使用Sling Models的範例，請參閱 [Developing Sling Model Exporers in AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/sling-model-exporter-tutorial-develop.html)。

Sling Model實作類別必須加上下列註解：

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

這可確保使用選擇器和擴充功能，自行導 `.model` 出組 `.json` 件。

此外，這會指定Sling Model類別可適用於介 `ComponentExporter` 面。

>[!NOTE]
>
>Jackson註解通常不會在Sling Model類別層級指定，而是在Model介面層級指定。 這是為了確保JSON匯出被視為元件API的一部分。

>[!NOTE]
>
>這 `ExporterConstants` 些 `ComponentExporter` 課程和課 `com.adobe.cq.export.json` 程。

## 註解Sling Model Interface {#annotate-the-sling-model-interface}

若要讓JSON匯出器架構考慮，Model介面應實 `ComponentExporter` 作介面( `ContainerExporter`若是容器元件)。

然後，對應的Sling Model介面( `MyComponent`)會使用 [Jackson Annotations加上註解](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) ，以定義如何匯出（序列化）。

Model介面需要正確加上註解，以定義應序列化哪些方法。 依預設，所有遵循getter通常命名慣例的方法都會序列化，並會自然從getter名稱衍生其JSON屬性名稱。 使用或重新命名JSON屬性 `@JsonIgnore` 時， `@JsonProperty` 可防止或覆寫此動作。

## 例如 {#example}

核心元件自核心元件發行 [1.1.0版起就支援JSON匯出](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) ，可當做參考。

如需範例，請參閱Image Core Component及其註解介面的Sling Model實作。

GITHUB代碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-core-wcm-components專案](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/archive/master.zip)

## 相關檔案 {#related-documentation}

如需詳細資訊，請參閱：

* 「資 [產」使用指南中的「內容片段」主題](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [內容片段模型](/help/assets/content-fragments-models.md)
* [使用內容片段製作](/help/sites-authoring/content-fragments.md)
* [內容服務的JSON匯出器](/help/sites-developing/json-exporter.md)
* [核心元件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) 和內容 [片段元件](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)

