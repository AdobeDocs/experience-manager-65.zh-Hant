---
title: 建立新的Granite UI欄位元件
seo-title: Creating a New Granite UI Field Component
description: Granite UI提供一系列元件，專門用於表單中，稱為欄位
seo-description: Granite UI provides a range of components designed to be used in forms, called fields
uuid: cf26e057-4b0c-45f4-8975-2c658517f20e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 94b9eeee-aae3-4b28-9d6f-1be0e4acd982
exl-id: e4820330-2ee6-4eca-83fd-462aa0b83647
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---

# 建立新的Granite UI欄位元件{#creating-a-new-granite-ui-field-component}

Granite UI提供多種元件，設計用於表單中；這些稱為 *欄位* 在Granite UI辭匯中。 標準Granite表單元件可從以下位置取得：

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>這些Granite UI表單欄位的用途，因此特別受關注 [元件對話方塊](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>如需欄位的完整詳細資訊，請參閱 [Granite UI檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).

使用Granite UI Foundation架構來開發及/或擴充Granite元件。 這有兩個元素：

* 伺服器端：

   * 基礎元件的集合

      * 基礎 — 模組化，可組合，可分層，可重複使用
      * 元件 — Sling元件
   * 幫助應用程式開發人員


* 用戶端：

   * clientlib的集合，提供一些辭匯(即HTML語言的延伸)，以透過超媒體導向的UI來達成一般互動模式

一般Granite UI元件 `field` 是由兩個感興趣的檔案組成：

* `init.jsp`:處理通用處理；標籤、說明和提供呈現欄位時所需的表單值。
* `render.jsp`:這是執行欄位實際呈現的地方，且需要為自訂欄位覆寫；包含於 `init.jsp`.

請參閱 [Granite UI檔案 — 欄位](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html) 如果您想要更多詳細資訊。

如需範例，請參閱：

* `cqgems/customizingfield/components/colorpicker`

   * 由提供 [程式碼範例](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>由於此機制使用JSP，因此i18n和XSS不會立即提供。 這表示您需要將字串國際化並脫離。 以下目錄包含標準實例中的通用欄位，您可以將這些欄位用作參考：
>
>`/libs/granite/ui/components/foundation/form` 目錄

## 為元件建立伺服器端指令碼 {#creating-the-server-side-script-for-the-component}

您的自訂欄位應僅會覆寫 `render.jsp` 指令碼，您可在此提供元件的標籤。 您可以將JSP（即呈現指令碼）視為標籤的包裝函式。

1. 建立使用 `sling:resourceSuperType` 要繼承的屬性：

   `/libs/granite/ui/components/foundation/form/field`

1. 覆蓋指令碼：

   `render.jsp`

   在此指令碼中，您需要生成超媒體標籤（即包含超媒體可承受性的富集標籤），以便客戶端知道如何與生成的元素交互。 這應該遵循Granite UI伺服器端的編碼樣式。

   自訂時，您唯一 *必須* 完成是讀取表單值(初始化於 `init.jsp`)，透過：

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   如需詳細資訊，請參閱現成可用的Granite UI欄位實作；例如， `/libs/granite/ui/components/foundation/form/textfield`.

   >[!NOTE]
   >
   >目前，JSP是偏好的指令碼方法，因為在HTL中很難將資訊從一個元件傳遞至另一個元件（在表單/欄位的環境中相當常見）。

## 為元件建立用戶端程式庫 {#creating-the-client-library-for-the-component}

若要將特定用戶端行為新增至元件：

1. 建立類別的clientlib `cq.authoring.dialog`.
1. 建立類別的clientlib `cq.authoring.dialog` 定義 `JS`/ `CSS` 裡面。

   定義 `JS`/ `CSS` 在clientlib內。

   >[!NOTE]
   >
   >目前，Granite UI未提供任何可用來直接新增JS行為的現成監聽器或鈎點。 因此，若要新增其他JS行為至元件，您必須將JS連結實作至自訂類別，然後在標籤產生期間指派給元件。
