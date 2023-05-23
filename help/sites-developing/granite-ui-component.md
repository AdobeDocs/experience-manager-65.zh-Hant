---
title: 建立新花崗岩UI欄位元件
seo-title: Creating a New Granite UI Field Component
description: Granite UI提供了一系列元件，這些元件設計為用於表單，稱為欄位
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

# 建立新花崗岩UI欄位元件{#creating-a-new-granite-ui-field-component}

花崗岩介面提供了一系列設計用於形式的元件；這些 *欄位* 花崗岩用戶介面辭彙。 標準花崗岩形元件可在以下位置獲得：

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>這些花崗岩UI表單域特別受關注，因為它們用於 [元件對話框](/help/sites-developing/developing-components.md)。

>[!NOTE]
>
>有關欄位的完整詳細資訊，請參閱 [花崗岩用戶介面文檔](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)。

使用Granite UI基礎框架開發和/或擴展Granite元件。 這有兩個要素：

* 伺服器端：

   * 基金會的組成

      * 基礎 — 模組化、可組合、可分層、可重複使用
      * 元件 — 吊具元件
   * 幫助應用程式開發


* 客戶端：

   * 提供一些辭彙(即HTML語言的擴展)以通過超媒體驅動的UI實現通用交互模式的客戶端庫的集合

通用Granite UI元件 `field` 由兩個感興趣的檔案組成：

* `init.jsp`:處理通用處理；標籤、說明，並提供呈現欄位時需要的表單值。
* `render.jsp`:這是執行該欄位的實際呈現，並需要替換您的自定義欄位；包含者 `init.jsp`。

請參閱 [花崗岩UI文檔 — 現場](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html) 的雙曲餘切值。

有關示例，請參見：

* `cqgems/customizingfield/components/colorpicker`

   * 由 [代碼示例](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>由於該機制使用JSP，因此i18n和XSS不是現成的。 這意味著您需要將字串國際化並脫離。 以下目錄包含標準實例中的類屬欄位，您可以將這些欄位用作參照：
>
>`/libs/granite/ui/components/foundation/form` 目錄

## 為元件建立伺服器端指令碼 {#creating-the-server-side-script-for-the-component}

您的自定義欄位應僅覆蓋 `render.jsp` 指令碼，其中為元件提供標籤。 可以將JSP（即呈現指令碼）視為標籤的包裝。

1. 建立使用 `sling:resourceSuperType` 從中繼承的屬性：

   `/libs/granite/ui/components/foundation/form/field`

1. 覆蓋指令碼：

   `render.jsp`

   在此指令碼中，您需要生成超媒體標籤（即富集標籤，包含超媒體負擔），以便客戶端知道如何與生成的元素交互。 這應遵循Granite UI伺服器端的編碼樣式。

   在自定義時，您 *必須* fullim是讀取表單值(初始化於 `init.jsp`)，使用：

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   有關更多詳情，請參閱現成Granite UI欄位的實現；比如說， `/libs/granite/ui/components/foundation/form/textfield`。

   >[!NOTE]
   >
   >目前，JSP是首選的指令碼編寫方法，因為HTL中不容易實現從一個元件到另一個元件（在表單/欄位的上下文中是非常頻繁的）的資訊傳遞。

## 為元件建立client-library {#creating-the-client-library-for-the-component}

要向元件添加特定的客戶端行為，請執行以下操作：

1. 建立類別的客戶端庫 `cq.authoring.dialog`。
1. 建立類別的客戶端庫 `cq.authoring.dialog` 定義 `JS`/ `CSS` 在裡面。

   定義 `JS`/ `CSS` 在客戶端庫中。

   >[!NOTE]
   >
   >目前，Granite UI不提供任何可直接用於添加JS行為的現成監聽器或掛接。 因此，要向元件添加其他JS行為，您必須將JS掛接實現到自定義類，然後在標籤生成期間將其分配給元件。
