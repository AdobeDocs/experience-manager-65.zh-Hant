---
title: 配置佈局容器和佈局模式
seo-title: Configuring Layout Container and Layout Mode
description: 了解如何設定「配置容器」和「配置模式」。
seo-description: Learn how to configure Layout Container and Layout Mode.
uuid: 952b7c86-76ab-4699-8530-8638e46bb50f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 10940000-808a-48ae-8e46-61eccef71eab
legacypath: /content/docs/en/aem/6-2/administer/operations/page-authoring/configuring-responsive-layouting
exl-id: 61152b2d-4c0b-4cfd-9669-cf03d32cb7c7
source-git-commit: 30327950779337ce869b6ca376120bc09826be21
workflow-type: tm+mt
source-wordcount: '1288'
ht-degree: 1%

---

# 配置佈局容器和佈局模式{#configuring-layout-container-and-layout-mode}

[回應式版面](/help/sites-authoring/responsive-layout.md) 是實現的機制 [回應式網頁設計](https://en.wikipedia.org/wiki/Responsive_web_design). 這可讓使用者建立網頁，其版面和維度取決於其使用者使用的裝置。

>[!NOTE]
>
>這可與 [行動網站](/help/sites-developing/mobile-web.md) 機制，使用最適化網頁設計（主要用於傳統UI）。

AEM使用組合機制來實現頁面的回應式版面：

* [**版面容器**](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode) 元件

   此元件提供了網格段落系統，允許您在響應式網格中添加和定位元件。 它可作為頁面的預設parsys，和/或讓元件瀏覽器中的作者使用。

   * 預設 **版面容器** 元件定義於：

      /libs/wcm/foundation/components/responsivegrid

   * 您可以定義版面容器：

      * 作為使用者可新增至頁面的元件。
      * 作為頁面的預設parsys。
      * 兩者.

         您可以讓版面容器作為頁面的標準，同時讓使用者在此內新增更多版面容器；例如，要實現列控制。

* **[版面模式](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**
版面容器放置在頁面上後，即可使用 
**版面** 模式來定位回應式格線內的內容。

* [**模擬器**](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)
這可讓您透過互動方式調整元件大小，來建立和編輯回應式網站，以根據裝置/視窗大小重新排列版面。 然後，使用者就可以看到使用模擬器呈現內容的方式。

>[!CAUTION]
>
>雖然 **版面容器** 傳統UI中提供元件，其完整功能僅在觸控式UI中提供。

使用這些回應式格線機制，您可以：

* 使用斷點（表示設備分組）根據設備佈局定義不同的內容行為。
* 根據設備組隱藏元件（定義將隱藏元件的斷點）。
* 使用水準對齊網格（將元件放入網格中，根據需要調整大小，定義它們何時應折疊/重排以並排或在上/下）。
* 實現列控制。

>[!NOTE]
>
>在現成可用的安裝中，已針對 [We.Retail參考網站](/help/sites-developing/we-retail.md). 你必須 [啟動「佈局容器」元件](#enable-the-layout-container-component-for-page) 的其他頁面。

## 設定回應式模擬器 {#configuring-the-responsive-emulator}

此工作可讓您查看回應式 **模擬器** 在您的網站上。

### 註冊頁面元件以進行模擬 {#register-your-page-components-for-emulation}

若要讓模擬器支援您的頁面，您必須註冊頁面元件。 請參閱 [註冊頁面元件以進行模擬](/help/sites-developing/responsive.md#registering-page-components-for-simulation).

### 指定設備組 {#specify-the-device-groups}

要指定出現在模擬器的「設備」清單中的設備組，請參閱 [指定設備組](/help/sites-developing/responsive.md#specifying-the-device-groups).

### 將您的網站連結到指定的設備組 {#link-your-site-to-the-specified-device-groups}

若要包含模擬器，請將您的網站連結至裝置群組。 請參閱 [添加設備清單](/help/sites-developing/responsive.md#adding-the-devices-list) （適用於傳統和觸控最佳化UI）。

## 啟用網站的版面模式 {#activate-layout-mode-for-your-site}

這些程式用於啟用 **版面** 模式。

### 配置斷點 {#configure-the-breakpoints}

[中斷點](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate):

* 用於回應式設計。
* 可定義：

   * 在頁面範本上，從中將設定複製到使用該範本建立的任何頁面。
   * 在頁面節點上，任何子頁面都會從中繼承設定。

* 定義標題和寬度：

   * 標題描述了通用設備分組，如有必要，可以使用方向；例如，手機、平板電腦、平板電腦、平板電腦橫向。
   * 寬度以像素定義該通用設備分組的最大寬度。 例如，如果斷點電話的寬度為768，則該寬度為用於電話設備的佈局的最大寬度。

* 使用模擬器時，在頁面編輯器頂端會顯示為標籤。
* 繼承自父節點層次結構，可以隨時覆蓋。
* 有一個預設（現成）斷點，它涵蓋上一個的所有內容 *已配置* 斷點。

可使用CRXDE Lite或XML來定義。

>[!NOTE]
>
>如果您要設定新專案：
>
>* 將斷點添加到模板。
>
>如果您要移轉現有專案（含現有內容），您必須：
>
>* 將斷點添加到模板
>* 將相同的斷點添加到現有頁面
>
>  由於繼承正在運作，您可以將此限制在內容的根頁面。

#### 使用CRXDE Lite配置斷點 {#configuring-breakpoints-using-crxde-lite}

1. 使用CRXDE Lite（或同等項目），導覽至以下任一項目：

   * 您的範本定義。
   * 此 `jcr:content` 節點。

1. 在 `jcr:content` 建立節點：

   * 名稱: `cq:responsive`
   * 類型: `nt:unstructured`

1. 在此下，建立節點：

   * 名稱: `breakpoints`
   * 類型: `nt:unstructured`

1. 在斷點節點下，可以建立任意數量的斷點。 每個定義都是具有下列屬性的單一節點：

   * 名稱: `<descriptive name>`
   * 類型: `nt:unstructured`
   * 標題: `String` * `<descriptive title seen in Emulator>`*
   * 寬度: `Decimal` * `<value of breakpoint>`*

#### 使用XML配置斷點 {#configuring-breakpoints-using-xml}

斷點位於 `<jcr:content>` 區段 `.context.html` 在適當的範本（或內容）資料夾下。

範例定義：

```xml
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

### 新增回應式資訊提供者 {#add-a-responsive-information-provider}

>[!NOTE]
>
>只有在頁面元件並非根據基礎頁面元件時，才需要此項。

複製下列項目 `cq:infoProviders` 節點結構放入您的上層頁面元件中：

`/libs/foundation/components/page/cq:infoProviders/responsive`

## 為頁面啟用元件大小調整 {#enable-component-resizing-for-the-page}

需要這些步驟，以便您可以調整 **版面** 模式。

### 將配置容器設定為主Parsys {#set-layout-container-as-main-parsys}

若要將頁面的主要parsys設為版面容器，請將parsys定義為：

`wcm/foundation/components/responsivegrid`

在下列任一項中：

* 頁面元件
* 頁面範本（供日後使用）

以下兩個範例說明定義：

* **HTL:**

   ```xml
   <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
   ```

* **JSP:**

   ```
   <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
   ```

### 包含回應式CSS {#include-the-responsive-css}

#### 使用較少的斷點的CSS {#css-for-breakpoints-using-less}

AEM使用LESS來產生部分必要的CSS，這些需要包含在您的專案中。

您也必須建立 [用戶庫](https://experienceleague.adobe.com/docs/) 提供其他設定和函式呼叫。 以下LESS提取是您必須添加到項目中的最小值的示例：

```java
@import (once) "/libs/wcm/foundation/clientlibs/grid/grid_base.less";

/* maximum amount of grid cells to be provided */
@max_col: 12;

/* default breakpoint */
.aem-Grid {
  .generate-grid(default, @max_col);
}

/* phone breakpoint */
@media (max-width: 768px) {
  .aem-Grid {
    .generate-grid(phone, @max_col);
  }
}

/* tablet breakpoint */
@media (min-width: 769px) and (max-width: 1200px) {
  .aem-Grid {
    .generate-grid(tablet, @max_col);
  }
}
```

可在以下位置找到基網格定義：

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### 樣式考量事項 {#styling-considerations}

根據響應網格大小對保持在響應容器內的元件進行調整(連同其各自的HTMLDOM元素)。 因此，在這些情況下，建議避免（或更新）固定寬度（包含）DOM元素的定義。

例如：

* 變更前:

   * `width=100px`

* 變更後:

   * `max-width=100px`

#### 調整大小和適應性影像合規性 {#resizing-and-adaptive-image-compliance}

網格中元件的任何大小調整都將觸發以下監聽器：

* `beforeedit`
* `beforechildedit`
* `afteredit`

* `afterchildedit`

若要正確調整回應式格線中所包含之最適化影像的內容大小和更新內容，您必須新增 `afterEdit` 設為 `REFRESH_PAGE` 接聽器 `EditConfig` 每個包含元件的檔案。

例如：

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

通過指令碼使自適應影像機制可用，該指令碼控制對窗口當前大小的正確影像的選擇。 DOM準備就緒或收到專用事件時，就會啟用。 目前必須重新整理頁面才能正確反映使用者動作的結果。

>[!CAUTION]
>
>自訂樣式表clientlib必須載入為標題的一部分，才能在製作和發佈上正常運作。

## 啟用頁面的版面容器元件 {#enable-the-layout-container-component-for-page}

這些工作可讓作者拖曳 **版面容器** 元件。

### 啟用「版面容器」元件以進行頁面編輯 {#enable-the-layout-container-component-for-page-editing}

若要允許作者為內容頁面新增更多回應式格線，您必須為頁面啟用「版面容器」元件。 您可以使用下列任一項來執行此作業：

* **製作環境**

   使用 [設計模式](/help/sites-authoring/default-components-designmode.md) 啟用 **圖層容器** 元件。

* **元件定義**

   使用 `allowedComponent` 或定義元件時的靜態包含。

### 配置佈局容器的網格 {#configure-the-grid-of-the-layout-container}

您可以設定配置容器的每個特定例項可用的欄數：

1. **製作環境**

   您可以設定配置容器的每個特定例項可用的欄數。

   若要這麼做，請使用 [設計模式](/help/sites-authoring/default-components-designmode.md)，然後開啟所需容器的設計對話方塊。 您可以在此處指定定位和調整大小所需的欄數。 預設為12。

1. **XML**

   回應式格線的定義在中指定：

   `etc/design/<*your-project-name*>/.content.xml`

   可定義下列參數：

   * 可用列數：

      * `columns="{String}8"`
   * 可新增至目前元件的元件：

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`
