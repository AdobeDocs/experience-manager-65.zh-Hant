---
title: 設定配置容器和配置模式
description: 瞭解如何設定配置容器和配置模式。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
legacypath: /content/docs/en/aem/6-2/administer/operations/page-authoring/configuring-responsive-layouting
exl-id: 61152b2d-4c0b-4cfd-9669-cf03d32cb7c7
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
source-git-commit: 17c4084d9ee93e5fe6652d63438eaf34cbc83c12
workflow-type: tm+mt
source-wordcount: '1479'
ht-degree: 0%

---


# 設定配置容器和配置模式{#configuring-layout-container-and-layout-mode}

瞭解如何設定配置容器和配置模式。

>[!TIP]
>
>本檔案為網站管理員和開發人員提供回應式設計的概覽，說明如何在AEM中實現功能。
>
>對於內容作者，如何在內容頁面上使用回應式設計功能的詳細資訊，可在內容頁面的回應式佈局檔案中取得。[](/help/sites-authoring/responsive-layout.md)

## 概觀 {#overview}

[回應式佈局](/help/sites-authoring/responsive-layout.md)是一種實現[回應式網頁設計](https://en.wikipedia.org/wiki/Responsive_web_design)的機制。 這可讓使用者建立根據其使用者使用之裝置而具有版面配置與尺寸的網頁。

AEM使用一組機製為頁面實現回應式佈局：

* [**配置容器**](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)&#x200B;元件

  此元件提供格線段落系統，讓您在回應式格線內新增及放置元件。 它可作為您頁面的預設Parsys使用，和/或在元件瀏覽器中可供作者使用。

   * 預設&#x200B;**配置容器**&#x200B;元件定義於：

     `/libs/wcm/foundation/components/responsivegrid`

   * 您可以定義配置容器：

      * 作為使用者可新增至頁面的元件。
      * 做為頁面的預設parsys。
      * 兩者。

        您可以將版面容器設為頁面的標準版面容器，同時允許使用者在此容器中新增更多版面容器；例如，實現欄控制。

* **[配置模式](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**
將配置容器放置到頁面上後，您就可以使用**配置**&#x200B;模式在回應式格線內放置內容。

* [**模擬器**](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)
這可讓您建立及編輯回應式網站，這些網站會透過以互動方式調整元件大小，根據裝置/視窗大小重新安排版面。 之後，使用者可以使用模擬器檢視內容的呈現方式。

利用這些回應式格點機制，您可以：

* 使用中斷點（表示裝置分組）可依據裝置配置定義不同的內容行為。
* 根據裝置群組隱藏元件（定義元件將隱藏在哪個中斷點）。
* 使用水準貼齊格點（將元件放入格點，視需要調整大小，定義它們何時應該摺疊/重排成並排或上下對齊）。
* 實現欄控制。

>[!TIP]
>
>Adobe提供回應式版面的[GitHub檔案](https://adobe-marketing-cloud.github.io/aem-responsivegrid/)，作為前端開發人員參考之用，讓他們能夠在AEM之外使用AEM網格，例如在為未來的AEM網站建立靜態HTML模型時。

>[!NOTE]
>
>在現成可用的安裝中，已針對[We.Retail參考網站](/help/sites-developing/we-retail.md)設定回應式配置。 [啟動其他頁面的配置容器元件](#enable-the-layout-container-component-for-page)。

>[!CAUTION]
>
>雖然&#x200B;**Layout Container**&#x200B;元件可在傳統UI中使用，但其完整功能僅可在觸控式UI中使用。

## 設定回應式模擬器 {#configuring-the-responsive-emulator}

此任務可讓您在網站上看到回應式&#x200B;**模擬器**。

### 註冊頁面元件以進行模擬 {#register-your-page-components-for-emulation}

若要讓模擬器支援您的頁面，您必須註冊頁面元件。 請參閱[註冊模擬的頁面元件](/help/sites-developing/responsive.md#registering-page-components-for-simulation)。

### 指定裝置群組 {#specify-the-device-groups}

若要指定出現在模擬器之[裝置]清單中的裝置群組，請參閱[指定裝置群組](/help/sites-developing/responsive.md#specifying-the-device-groups)。

### 將您的網站連結至指定的裝置群組 {#link-your-site-to-the-specified-device-groups}

若要加入模擬器，請將您的網站連結至裝置群組。 請參閱[新增裝置清單](/help/sites-developing/responsive.md#adding-the-devices-list) （針對傳統和觸控最佳化UI）。

## 啟用網站的佈局模式 {#activate-layout-mode-for-your-site}

這些程式用於啟用網站上的&#x200B;**配置**&#x200B;模式。

### 設定中斷點 {#configure-the-breakpoints}

[中斷點](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)：

* 用於回應式設計。
* 可定義：

   * 在頁面範本上，設定會從中複製到使用該範本建立的任何頁面。
   * 在頁面節點上，任何子頁面會從中繼承設定。

* 定義標題和寬度：

   * 標題說明一般裝置群組，必要時會提供方向；例如，手機、平板電腦、桌上型電腦橫向。
   * 寬度會定義該一般裝置群組的最大寬度（畫素）。 例如，如果中斷點電話的寬度為768，那麼就會是電話裝置所使用的配置寬度上限。

* 使用模擬器時，會在頁面編輯器頂端顯示為標籤。
* 繼承自父節點階層，並可隨意覆寫。
* 有一個預設（現成）中斷點，其涵蓋上一個&#x200B;*已設定的*&#x200B;中斷點以上的所有內容。

它們可以使用CRXDE Lite或XML來定義。

>[!NOTE]
>
>如果您要設定新專案：
>
>* 將中斷點新增至範本。
>
>如果您要移轉現有專案（包含現有內容），您必須：
>
>* 將中斷點新增至範本
>* 將相同的中斷點新增至現有頁面
>
>  由於繼承正在運作，您可以將此限製為內容的根頁面。

#### 使用CRXDE Lite設定中斷點 {#configuring-breakpoints-using-crxde-lite}

1. 使用CRXDE Lite（或同等專案），導覽至：

   * 您的範本定義。
   * 您頁面的`jcr:content`節點。

1. 在`jcr:content`下建立節點：

   * 名稱：`cq:responsive`
   * 類型：`nt:unstructured`

1. 在此之下建立節點：

   * 名稱：`breakpoints`
   * 類型：`nt:unstructured`

1. 在中斷點節點下，您可以建立任意數目的中斷點。 每個定義都是具有下列屬性的單一節點：

   * 名稱：`<descriptive name>`
   * 類型：`nt:unstructured`
   * 標題： `String` * `<descriptive title seen in Emulator>`*
   * 寬度： `Decimal` * `<value of breakpoint>`*

#### 使用XML設定中斷點 {#configuring-breakpoints-using-xml}

中斷點位於`.context.html`的`<jcr:content>`區段內，在適當的範本（或內容）資料夾下。

範例定義：

```html
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
>只有在頁面元件不是根據基礎頁面元件時，才需要此專案。

將下列`cq:infoProviders`節點結構複製到您的上層頁面元件中：

`/libs/foundation/components/page/cq:infoProviders/responsive`

## 啟用頁面元件大小調整 {#enable-component-resizing-for-the-page}

需要這些程式，才能在&#x200B;**配置**&#x200B;模式中調整元件大小。

### 將配置容器設定為主要Parsys {#set-layout-container-as-main-parsys}

若要將頁面的主要parsys設定為配置容器，請將parsys定義為：

`wcm/foundation/components/responsivegrid`

在：

* 頁面元件
* 頁面範本（供日後使用）

以下兩個範例說明定義：

* **HTL：**

  ```html
  <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
  ```

* **JSP：**

  ```html
  <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
  ```

### 包含回應式CSS {#include-the-responsive-css}

#### 使用LESS的中斷點CSS {#css-for-breakpoints-using-less}

AEM使用LESS來產生必要CSS的部分，這些需要包含在您的專案中。

您也必須建立[使用者端程式庫](https://experienceleague.adobe.com/docs/)，以提供額外的設定和函式呼叫。 以下LESS擷取是您必須新增至專案的最小值範例：

```css
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

基底格點定義可在下列位置找到：

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### 樣式考量事項 {#styling-considerations}

保持在回應式容器中的元件會根據回應式格線大小調整大小(連同其各自的HTMLDOM元素)。 因此，在這些情況下，建議避免（或更新）固定寬度（包含） DOM元素的定義。

例如：

* 之前：

   * `width=100px`

* 之後：

   * `max-width=100px`

#### 調整大小和調整影像法規遵循 {#resizing-and-adaptive-image-compliance}

在格線內調整元件大小的任何動作，都會視情況觸發下列接聽程式：

* `beforeedit`
* `beforechildedit`
* `afteredit`

* `afterchildedit`

若要正確調整回應式格線中所包含的最適化影像內容大小並加以更新，您必須將設為`REFRESH_PAGE`的`afterEdit`接聽程式新增至每個所包含元件的`EditConfig`檔案。

例如：

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

可透過指令碼使用最適化影像機制，該指令碼控制選擇符合目前視窗大小的正確影像。 在DOM準備就緒或收到專用事件時，它會啟動。 目前必須重新整理頁面，才能正確反映使用者動作的結果。

>[!CAUTION]
>
>自訂樣式表clientlibs必須載入為標頭的一部分，才能在製作和發佈上正確運作。

## 啟用頁面的配置容器元件 {#enable-the-layout-container-component-for-page}

這些工作可讓作者將&#x200B;**配置容器**&#x200B;元件的執行個體拖曳到頁面上。

### 啟用配置容器元件以進行頁面編輯 {#enable-the-layout-container-component-for-page-editing}

若要讓作者更能回應式地新增網格至內容頁面，您必須啟用頁面的「配置容器」元件。 您可以透過以下其中一種方式來達成此目的：

* **作者環境**

  使用[設計模式](/help/sites-authoring/default-components-designmode.md)來啟用頁面的&#x200B;**圖層容器**&#x200B;元件。

* **元件定義**

  定義元件時使用`allowedComponent`或靜態包含。

### 設定配置容器的格線 {#configure-the-grid-of-the-layout-container}

您可以設定可用於配置容器的每個特定執行個體的欄數：

1. **作者環境**

   您可以設定可用於配置容器的每個特定執行個體的欄數。

   若要這麼做，請使用[設計模式](/help/sites-authoring/default-components-designmode.md)，然後開啟所需容器的設計對話方塊。 您可在此指定有多少欄位可供定位和調整大小。 預設值為12。

1. **XML**

   回應式格線的定義指定於：

   `etc/design/<*your-project-name*>/.content.xml`

   可以定義下列引數：

   * 可用的欄數：

      * `columns="{String}8"`

   * 可新增至目前元件的元件：

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`

## 巢狀回應式格點 {#nested-responsive-grids}

在某些情況下，您可能會發現有必要巢狀內嵌回應式格線以支援專案的需求。 不過，請記住，Adobe建議的最佳實務是儘可能將結構保持平坦。

當您無法避免使用巢狀回應式格點時，請確定：

* 所有容器（容器、標籤、摺疊式功能表等）都有屬性`layout = responsiveGrid`。
* 請勿在容器階層中混合屬性`layout = simple`。

這包括頁面範本中的所有結構容器。

內部容器的欄位編號絕不可大於外部容器的欄位編號。 下列範例符合此條件。 雖然在預設的（案頭）畫面中，外部容器的欄位編號為8，但內部容器的欄位編號為4。

>[!BEGINTABS]

>[!TAB 範例節點結構]

```text
container
  @layout = responsiveGrid
  cq:responsive
    default
      @offset = 0
      @width = 8
  container
  @layout = responsiveGrid
    cq:responsive
      default
        @offset = 0
        @width = 4
    text
      @text =" Text Column 1"
```

>[!TAB 產生的HTML範例]

```html
<div class="container responsivegrid aem-GridColumn--default--none aem-GridColumn aem-GridColumn--default--8 aem-GridColumn--offset--default--0">
  <div id="container-c9955c233c" class="cmp-container">
    <div class="aem-Grid aem-Grid--8 aem-Grid--default--8 ">
      <div class="container responsivegrid aem-GridColumn--default--none aem-GridColumn aem-GridColumn--offset--default--0 aem-GridColumn--default--4">
        <div id="container-8414e95866" class="cmp-container">
          <div class="aem-Grid aem-Grid--4 aem-Grid--default--4 ">
            <div class="text aem-GridColumn aem-GridColumn--default--4">
              <div data-cmp-data-layer="..." id="text-1234567890" class="cmp-text">
                <p>Text Column 1</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
```

>[!ENDTABS]
