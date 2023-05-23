---
title: 配置佈局容器和佈局模式
seo-title: Configuring Layout Container and Layout Mode
description: 瞭解如何配置佈局容器和佈局模式。
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

[響應佈局](/help/sites-authoring/responsive-layout.md) 是實現 [響應性Web設計](https://en.wikipedia.org/wiki/Responsive_web_design)。 這允許用戶建立佈局和維度取決於用戶使用的設備的網頁。

>[!NOTE]
>
>可以將此值與 [移動Web](/help/sites-developing/mobile-web.md) 機制，使用自適應web設計（主要針對經典UI）。

使AEM用多種機制實現頁面的響應式佈局：

* [**佈局容器**](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode) 元件

   此元件提供了網格段落系統，允許您在響應網格中添加和定位元件。 它可用作頁面的預設參數和/或可供元件瀏覽器中的作者使用。

   * 預設 **佈局容器** 元件定義如下：

      /libs/wcm/foundation/components/responsedgrid

   * 您可以定義佈局容器：

      * 作為用戶可添加到頁面的元件。
      * 作為頁面的預設參數。
      * 兩者.

         您可以將佈局容器作為頁面的標準，同時允許用戶在此中添加更多佈局容器；例如，實現列控制。

* **[佈局模式](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**
佈局容器放置在頁面上後，您可以使用 
**佈局** 在響應網格中定位內容的模式。

* [**模擬器**](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)
這允許您建立和編輯響應性網站，這些網站通過交互調整元件大小來根據設備/窗口大小重新排列佈局。 然後，用戶可以查看如何使用模擬器呈現內容。

>[!CAUTION]
>
>儘管 **佈局容器** 元件在標準UI中可用，其完整功能僅在啟用觸摸的UI中可用。

利用這些響應網格機制，您可以：

* 使用斷點（表示設備分組）根據設備佈局定義不同的內容行為。
* 根據設備組隱藏元件（定義元件將隱藏在哪個斷點上）。
* 使用水準對齊網格（將元件放入網格中，根據需要調整大小，定義它們應在何時折疊/重排並排或在上/下）。
* 實現列控制。

>[!NOTE]
>
>在現成安裝中，已為 [We.Retail參考網站](/help/sites-developing/we-retail.md)。 你必須 [激活佈局容器元件](#enable-the-layout-container-component-for-page) 頁。

## 配置響應模擬器 {#configuring-the-responsive-emulator}

通過此任務，您可以看到 **模擬器** 在你的網站上。

### 註冊要模擬的頁面元件 {#register-your-page-components-for-emulation}

要使模擬器支援您的頁面，必須註冊頁面元件。 請參閱 [註冊模擬的頁面元件](/help/sites-developing/responsive.md#registering-page-components-for-simulation)。

### 指定設備組 {#specify-the-device-groups}

要指定在模擬器的「設備」清單中顯示的設備組，請參見 [指定設備組](/help/sites-developing/responsive.md#specifying-the-device-groups)。

### 將站點連結到指定的設備組 {#link-your-site-to-the-specified-device-groups}

要包括模擬器，請將站點連結到設備組。 請參閱 [添加設備清單](/help/sites-developing/responsive.md#adding-the-devices-list) （適用於經典和觸控優化的UI）。

## 激活網站的佈局模式 {#activate-layout-mode-for-your-site}

這些過程用於啟用 **佈局** 的子菜單。

### 配置斷點 {#configure-the-breakpoints}

[中斷點](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate):

* 用於響應設計。
* 可以定義：

   * 在頁面模板上，將設定從其中複製到使用該模板建立的任何頁面。
   * 在頁面節點上，任何子頁面都從中繼承設定。

* 定義標題和寬度：

   * 標題描述了通用設備分組，必要時可提供方向；例如，手機、平板電腦、平板電腦。
   * 寬度定義該通用設備分組的最大寬度（以像素為單位）。 例如，如果斷點電話的寬度為768，則它為用於電話設備的佈局的最大寬度。

* 在使用模擬器時，在頁面編輯器頂部以標籤形式可見。
* 繼承自父節點層次結構，可以隨意覆蓋。
* 有一個預設（現成）斷點，該斷點覆蓋上一個 *配置* 斷點。

可以使用CRXDE Lite或XML定義它們。

>[!NOTE]
>
>如果要設定新項目：
>
>* 將斷點添加到模板。
>
>如果要遷移現有項目（包含現有內容），必須：
>
>* 將斷點添加到模板
>* 將相同的斷點添加到現有頁面
>
>  繼承操作時，您可以將繼承限制在內容的根頁。

#### 使用CRXDE Lite配置斷點 {#configuring-breakpoints-using-crxde-lite}

1. 使用CRXDE Lite（或等效），導航至以下任一選項：

   * 您的模板定義。
   * 的 `jcr:content` 的子菜單。

1. 下 `jcr:content` 建立節點：

   * 名稱: `cq:responsive`
   * 類型: `nt:unstructured`

1. 在此下建立節點：

   * 名稱: `breakpoints`
   * 類型: `nt:unstructured`

1. 在斷點節點下，可以建立任意數量的斷點。 每個定義都是具有以下屬性的單個節點：

   * 名稱: `<descriptive name>`
   * 類型: `nt:unstructured`
   * 標題: `String` * `<descriptive title seen in Emulator>`*
   * 寬度: `Decimal` * `<value of breakpoint>`*

#### 使用XML配置斷點 {#configuring-breakpoints-using-xml}

斷點位於 `<jcr:content>` 的下界 `.context.html` 的子菜單。

示例定義：

```xml
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

### 添加響應資訊提供程式 {#add-a-responsive-information-provider}

>[!NOTE]
>
>僅當頁面元件不基於基礎頁面元件時才需要這樣做。

複製以下內容 `cq:infoProviders` 節點結構到父頁元件中：

`/libs/foundation/components/page/cq:infoProviders/responsive`

## 為頁面啟用元件調整大小 {#enable-component-resizing-for-the-page}

這些過程是必需的，因此您可以在 **佈局** 的子菜單。

### 將佈局容器設定為主參數 {#set-layout-container-as-main-parsys}

要將頁面的主參數設定為佈局容器，請將參數定義為：

`wcm/foundation/components/responsivegrid`

在以下任一位置：

* 頁面元件
* 頁面模板（供將來使用）

以下兩個示例說明了定義：

* **HTL:**

   ```xml
   <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
   ```

* **JSP:**

   ```
   <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
   ```

### 包括響應CSS {#include-the-responsive-css}

#### 使用LESS的斷點的CSS {#css-for-breakpoints-using-less}

使AEM用LESS生成所需CSS的部分，這些需要包含在項目中。

您還必須建立 [客戶端庫](https://experienceleague.adobe.com/docs/) 提供其他配置和函式調用。 以下LESS提取是必須添加到項目中的最小值的示例：

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

基本網格定義可在以下位置找到：

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### 造型注意事項 {#styling-considerations}

根據響應柵格大小調整保持在響應容器內的部件的大小(連同它們各自的HTMLDOM元件)。 因此，在這些情況下，建議避免（或更新）固定寬度（包含）DOM元素的定義。

例如：

* 變更前:

   * `width=100px`

* 變更後:

   * `max-width=100px`

#### 調整大小和自適應影像符合性 {#resizing-and-adaptive-image-compliance}

網格中任何調整元件大小都將觸發以下偵聽器：

* `beforeedit`
* `beforechildedit`
* `afteredit`

* `afterchildedit`

要正確調整和更新響應網格中包含的自適應影像的內容，需要添加 `afterEdit` 設定為 `REFRESH_PAGE` 監聽器 `EditConfig` 包含的每個元件的檔案。

例如：

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

自適應影像機制通過控制針對窗口的當前大小的正確影像選擇的指令碼而可用。 在DOM就緒或接收專用事件後激活。 當前必須刷新頁面才能正確反映用戶操作的結果。

>[!CAUTION]
>
>自定義樣式表客戶端必須作為標題的一部分載入，以便它們能夠在作者和發佈上正常工作。

## 為頁啟用佈局容器元件 {#enable-the-layout-container-component-for-page}

這些任務允許作者拖動 **佈局容器** 元件。

### 啟用佈局容器元件以進行頁面編輯 {#enable-the-layout-container-component-for-page-editing}

要允許作者向內容頁面添加更多響應的網格，您需要為頁面啟用佈局容器元件。 您可以使用以下任一方法執行此操作：

* **作者環境**

   使用 [設計模式](/help/sites-authoring/default-components-designmode.md) 來激活 **層容器** 元件。

* **元件定義**

   使用 `allowedComponent` 或定義元件時的靜態包括。

### 配置佈局容器的網格 {#configure-the-grid-of-the-layout-container}

您可以配置佈局容器的每個特定實例的可用列數：

1. **作者環境**

   您可以配置佈局容器的每個特定實例的可用列數。

   要執行此操作，請使用 [設計模式](/help/sites-authoring/default-components-designmode.md)，然後開啟所需容器的設計對話框。 在這裡，您可以具體說明有多少列可用於定位和調整大小。 預設值為12。

1. **XML**

   響應網格的定義在以下位置指定：

   `etc/design/<*your-project-name*>/.content.xml`

   可以定義以下參數：

   * 可用列數：

      * `columns="{String}8"`
   * 可添加到當前元件的元件：

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`
