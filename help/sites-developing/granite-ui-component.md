---
title: 建立新的Granite UI欄位元件
seo-title: 建立新的Granite UI欄位元件
description: Granite UI提供多種元件，設計用於表單，稱為欄位
seo-description: Granite UI提供多種元件，設計用於表單，稱為欄位
uuid: cf26e057-4b0c-45f4-8975-2c658517f20e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 94b9eeee-aae3-4b28-9d6f-1be0e4acd982
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 建立新的Granite UI欄位元件{#creating-a-new-granite-ui-field-component}

Granite UI提供多種元件，可用於表單；這些稱為 *Granite* UI辭彙中的欄位。 標準的Granite表單元件可從以下網址取得：

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>這些Granite UI表格欄位用於元件對話方塊時，會特別受 [到關注](/help/sites-developing/developing-components.md)。

>[!NOTE]
>
>如需欄位的完整詳細資訊，請參閱 [Granite UI檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)。

使用Granite UI Foundation架構來開發及／或擴充Granite元件。 這有兩個要素：

* 伺服器端：

   * 基礎元件的集合

      * 基礎——模組化、可組合、可分層、可重複使用
      * 元件- Sling元件
   * 協助應用程式開發人員


* 用戶端：

   * clientlibs的集合，提供一些辭彙（即HTML語言的擴充功能），以透過Hypermedia導向的UI來達成一般互動模式

通用Granite UI元件 `field` 由兩個感興趣的檔案組成：

* `init.jsp`:處理通用處理；標示、說明，並提供您在轉譯欄位時所需的表單值。
* `render.jsp`:這是執行欄位實際轉譯的地方，您需要針對自訂欄位覆寫；包含於 `init.jsp`。

如需詳細資訊，請 [參閱Granite UI檔案——欄位](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html) 。

如需範例，請參閱：

* `cqgems/customizingfield/components/colorpicker`

   * 由程式碼范 [例提供](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>由於此機制使用JSP，所以i18n和XSS不會立即提供。 這表示您需要國際化並逸出字串。 以下目錄包含標準實例的通用欄位，您可以將這些欄位用作參考：
>
>`/libs/granite/ui/components/foundation/form` 目錄

## 為元件建立伺服器端指令碼 {#creating-the-server-side-script-for-the-component}

您的自訂欄位只應覆寫您 `render.jsp` 為元件提供標籤的指令碼。 您可以將JSP（即渲染指令碼）視為標籤的包裝函式。

1. 建立使用屬性繼承的 `sling:resourceSuperType` 新元件：

   `/libs/granite/ui/components/foundation/form/field`

1. 覆蓋指令碼：

   `render.jsp`

   在此指令碼中，您需要生成超媒體標籤（即富集標籤，包含超媒體可負擔性），以便客戶知道如何與生成的元素交互。 這應遵循Granite UI伺服器端的編碼樣式。

   自訂時，您必須履行的唯 *一合約* ，就是從請求中讀取表單值(初始化 `init.jsp`於)，使用：

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   若需更多詳細資訊，請參閱現成可用的Granite UI欄位實作；例如， `/libs/granite/ui/components/foundation/form/textfield`。

   >[!NOTE]
   >
   >目前，JSP是偏好的指令碼方法，因為在HTL中，將資訊從一個元件傳遞到另一個元件（在表單／欄位中相當常見）並不容易。

## 為元件建立client-library {#creating-the-client-library-for-the-component}

若要將特定用戶端行為新增至元件：

1. 建立類別的clientlib `cq.authoring.dialog`。
1. 建立類別的clientlib, `cq.authoring.dialog` 並在其中定 `JS`義您 `CSS` 的/。

   在clientlib中 `JS`定 `CSS` 義您的/。

   >[!NOTE]
   >
   >目前，Granite UI不提供任何現成可用的監聽程式或勾點，您可直接用來新增JS行為。 因此，若要新增其他JS行為至元件，您必須將JS掛接實作至自訂類別，然後在標籤產生期間指派給元件。

