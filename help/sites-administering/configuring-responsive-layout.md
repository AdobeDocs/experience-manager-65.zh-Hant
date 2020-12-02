---
title: 設定版面容器和版面模式
seo-title: 設定版面容器和版面模式
description: 瞭解如何設定「版面容器」和「版面模式」。
seo-description: 瞭解如何設定「版面容器」和「版面模式」。
uuid: 952b7c86-76ab-4699-8530-8638e46bb50f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 10940000-808a-48ae-8e46-61eccef71eab
legacypath: /content/docs/en/aem/6-2/administer/operations/page-authoring/configuring-responsive-layouting
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 1%

---


# 設定版面容器和版面模式{#configuring-layout-container-and-layout-mode}

[Responsive ](/help/sites-authoring/responsive-layout.md) Layout是一種實現自適應網 [頁設計的機制](https://en.wikipedia.org/wiki/Responsive_web_design)。這可讓使用者建立版面和尺寸視使用者使用的裝置而定的網頁。

>[!NOTE]
>
>這可與使用可調式網頁設計（主要針對傳統UI）的[行動網頁](/help/sites-developing/mobile-web.md)機制進行比較。

AEM使用多種機制組合，為您的頁面實現互動式版面配置：

* [**Layout**](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode) Container元件

   此元件提供格線段落系統，可讓您在回應式格線中新增和定位元件。 它可用作您頁面的預設參數，和／或讓元件瀏覽器中的作者使用。

   * 預設的&#x200B;**版面容器**&#x200B;元件定義於：

      /libs/wcm/foundation/components/responvegrid

   * 您可以定義版面容器：

      * 做為使用者可新增至頁面的元件。
      * 作為頁面的預設參數。
      * 兩者.

         您可讓版面容器做為頁面的標準，同時允許使用者在其中新增更多版面容器；例如，要實現列控制。

* **[版面](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**
模式當版面容器定位在您的頁面上後，您就可以使用 
**「** 版面」模式，將內容定位在回應式格線中。

* [**模擬**](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)
器這可讓您建立和編輯互動式網站，透過互動方式調整元件大小，以根據裝置／視窗大小重新排列版面。然後，使用者就可以看到如何使用模擬器呈現內容。

>[!CAUTION]
>
>雖然傳統UI中提供&#x200B;**版面容器**&#x200B;元件，但其完整功能僅在觸控式UI中提供。

有了這些互動式格點機制，您可以：

* 使用中斷點（表示裝置群組），根據裝置版面來定義不同的內容行為。
* 根據設備組隱藏元件（定義元件將隱藏在哪個斷點上）。
* 使用水準對齊格線（將元件置入格線中、視需要調整大小、定義元件何時應收合／重排以並排或上／下）。
* 實現列控制。

>[!NOTE]
>
>在現成可用的安裝中，已為[We.Retail參考網站](/help/sites-developing/we-retail.md)設定回應式版面。 您仍必須[為其他頁面啟動「版面容器」元件](#enable-the-layout-container-component-for-page)。

## 配置自適應模擬器{#configuring-the-responsive-emulator}

這些工作可讓您在網站上看到回應式&#x200B;**Emulator**。

### 註冊您的頁面元件以進行模擬{#register-your-page-components-for-emulation}

若要讓模擬器支援您的頁面，您必須註冊您的頁面元件。 請參閱[註冊模擬的頁面元件](/help/sites-developing/responsive.md#registering-page-components-for-simulation)。

### 指定設備組{#specify-the-device-groups}

要指定出現在模擬器「設備」清單中的設備組，請參閱[指定設備組](/help/sites-developing/responsive.md#specifying-the-device-groups)。

### 將您的網站連結至指定的裝置群組{#link-your-site-to-the-specified-device-groups}

若要包含模擬器，您必須將網站連結至裝置群組。 請參閱[新增裝置清單](/help/sites-developing/responsive.md#adding-the-devices-list)（適用於傳統和觸控最佳化的UI）。

## 啟用您網站的版面模式{#activate-layout-mode-for-your-site}

這些程式用於啟用站點上的&#x200B;**Layout**&#x200B;模式。

### 配置斷點{#configure-the-breakpoints}

[中斷點](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate):

* 用於互動式設計。
* 可定義：

   * 在頁面範本上，設定將從此處複製至使用該範本建立的任何頁面。
   * 在頁面節點上，任何子頁面都會從中繼承設定。

* 定義標題和寬度：

   * 標題描述了通用設備分組，如果需要，則具有方向；例如手機、平板電腦、平板電腦橫向。
   * 寬度會定義該通用裝置群組的最大寬度（以像素為單位）。 例如，如果斷點電話的寬度為768，則為用於電話設備的佈局的最大寬度。

* 使用模擬器時，在頁面編輯器頂部顯示為標籤。
* 繼承自父節點層次結構，可以隨意覆蓋。
* 有一個預設（現成可用）斷點，它覆蓋最後&#x200B;*configured*&#x200B;斷點之上的所有內容。

它們可使用CRXDE Lite或XML來定義。

>[!NOTE]
>
>如果您要設定新專案：
>
>* 您需要將中斷點新增至範本。
>
>
如果您要移轉現有專案（含現有內容），您需要：
>
>* 將中斷點添加到模板
>* 將相同的中斷點新增至現有頁面

>
>  
繼承正在運作中時，您可以將繼承限制在內容的根頁面。

#### 使用CRXDE Lite {#configuring-breakpoints-using-crxde-lite}配置斷點

1. 使用CRXDE Lite（或相當等級），導覽至下列任一項目：

   * 您的範本定義。
   * 頁面的`jcr:content`節點。

1. 在`jcr:content`下建立節點：

   * 名稱: `cq:responsive`
   * 類型: `nt:unstructured`

1. 在此下，建立節點：

   * 名稱: `breakpoints`
   * 類型: `nt:unstructured`

1. 在中斷點節點下，可以建立任意數量的斷點。 每個定義都是具有以下屬性的單個節點：

   * 名稱: `<descriptive name>`
   * 類型: `nt:unstructured`
   * 標題: `String` * `<descriptive title seen in Emulator>`*
   * 寬度: `Decimal` * `<value of breakpoint>`*

#### 使用XML {#configuring-breakpoints-using-xml}配置斷點

中斷點位於`.context.html`的`<jcr:content>`區段內，位於適當的範本（或內容）資料夾下。

範例定義：

```xml
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

### 新增回應式資訊提供者{#add-a-responsive-information-provider}

>[!NOTE]
>
>只有當頁面元件並非以基礎頁面元件為基礎時，才需要此功能。

將以下`cq:infoProviders`節點結構複製到父頁元件中：

`/libs/foundation/components/page/cq:infoProviders/responsive`

## 啟用頁面{#enable-component-resizing-for-the-page}的元件大小調整

這些過程是必需的，因此您可以在&#x200B;**Layout**&#x200B;模式中調整元件大小。

### 將配置容器設為主參數{#set-layout-container-as-main-parsys}

若要將頁面的主要參數設為版面容器，您必須將參數定義為：

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

### 包含互動式CSS {#include-the-responsive-css}

#### 使用LESS {#css-for-breakpoints-using-less}的中斷點CSS

AEM使用LESS來產生部分必要的CSS，這些必須包含在您的專案中。

您還需要建立[客戶端庫](https://docs.adobe.com/content/docs/en/aem/6-0/develop/the-basics/clientlibs.html)以提供其他配置和函式調用。 以下LESS提取是您需要添加到項目中的最小值示例：

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

可在以下位置找到基本網格定義：

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### 樣式注意事項{#styling-considerations}

根據自適應格線大小，將調整保持在自適應容器中的元件大小（連同其各自的HTML DOM元素）。 因此，在這些情況下，建議避免（或更新）固定寬度（包含）DOM元素的定義。

例如：

* 變更前:

   * `width=100px`

* 變更後:

   * `max-width=100px`

#### 調整大小和最適化影像相容性{#resizing-and-adaptive-image-compliance}

在網格中調整元件大小時，將根據需要觸發以下偵聽程式：

* `beforeedit`
* `beforechildedit`
* `afteredit`

* `afterchildedit`

若要正確調整回應式格線中自適應影像的內容大小並更新，您必須將設定至`REFRESH_PAGE`監聽器的`afterEdit`新增至每個包含元件的`EditConfig`檔案。

例如：

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

自適應影像機制通過控制窗口當前大小的正確影像選擇的指令碼來提供。 在DOM就緒或接收專用事件時啟動。 目前，頁面必須重新整理，才能正確反映使用者動作的結果。

>[!CAUTION]
>
>自訂樣式表clientlibs必須載入為標題的一部分，才能在作者和發佈上正常運作。

## 啟用頁面{#enable-the-layout-container-component-for-page}的版面容器元件

這些工作可讓作者將&#x200B;**Layout Container**&#x200B;元件的例項拖曳至頁面上。

### 啟用頁面編輯的版面容器元件{#enable-the-layout-container-component-for-page-editing}

若要允許作者在內容頁面中新增更多回應式格點，您需要為頁面啟用「版面容器」元件。 您可以使用下列其中一種方式：

* **作者環境**

   使用[設計模式](/help/sites-authoring/default-components-designmode.md)來啟動頁面的&#x200B;**圖層容器**&#x200B;元件。

* **元件定義**

   定義元件時，請使用`allowedComponent`或靜態包含。

### 設定版面容器{#configure-the-grid-of-the-layout-container}的格線

您可以設定每個特定版面容器例項可用的欄數：

1. **作者環境**

   您可以設定每個特定版面容器例項可用的欄數。

   若要這麼做，請使用[設計模式](/help/sites-authoring/default-components-designmode.md)，然後開啟所需容器的設計對話方塊。 您可以在這裡指定定位和調整大小的欄數。 預設值為12。

1. **XML**

   回應式格線的定義在：

   `etc/design/<*your-project-name*>/.content.xml`

   可定義下列參數：

   * 可用欄數：

      * `columns="{String}8"`
   * 可添加到當前元件的元件：

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`


