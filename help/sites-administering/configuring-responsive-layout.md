---
title: 設定配置容器和配置模式
seo-title: Configuring Layout Container and Layout Mode
description: 瞭解如何設定配置容器和配置模式。
seo-description: Learn how to configure Layout Container and Layout Mode.
uuid: 952b7c86-76ab-4699-8530-8638e46bb50f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 10940000-808a-48ae-8e46-61eccef71eab
legacypath: /content/docs/en/aem/6-2/administer/operations/page-authoring/configuring-responsive-layouting
exl-id: 61152b2d-4c0b-4cfd-9669-cf03d32cb7c7
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 0%

---

# 設定配置容器和配置模式{#configuring-layout-container-and-layout-mode}

[回應式版面](/help/sites-authoring/responsive-layout.md) 是一種用於實現 [回應式網頁設計](https://en.wikipedia.org/wiki/Responsive_web_design). 這可讓使用者建立根據其使用者使用之裝置而具有版面配置與尺寸的網頁。

>[!NOTE]
>
>這可以與 [行動網頁](/help/sites-developing/mobile-web.md) 機制，此機制使用最適化網頁設計（主要用於傳統UI）。

AEM使用一組機製為頁面實現回應式佈局：

* [**配置容器**](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode) 元件

  此元件提供格線段落系統，讓您在回應式格線內新增及放置元件。 它可作為您頁面的預設Parsys使用，和/或在元件瀏覽器中可供作者使用。

   * 預設 **配置容器** 元件定義於：

     /libs/wcm/foundation/components/responsivegrid

   * 您可以定義配置容器：

      * 作為使用者可新增至頁面的元件。
      * 做為頁面的預設parsys。
      * 兩者。

        您可以將版面容器設為頁面的標準版面容器，同時允許使用者在此容器中新增更多版面容器；例如，實現欄控制。

* **[版面模式](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**
將版面容器放置到頁面上後，您就可以使用 **版面** 在回應式格線內放置內容的模式。

* [**模擬器**](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)
這可讓您建立及編輯回應式網站，這些網站會透過以互動方式調整元件大小，根據裝置/視窗大小重新安排版面。 之後，使用者可以使用模擬器檢視內容的呈現方式。

>[!CAUTION]
>
>雖然 **配置容器** 元件可在傳統UI中使用，其完整功能僅在觸控式UI中可用。

利用這些回應式格點機制，您可以：

* 使用中斷點（表示裝置分組）可依據裝置配置定義不同的內容行為。
* 根據裝置群組隱藏元件（定義元件將隱藏在哪個中斷點）。
* 使用水準貼齊格點（將元件放入格點，視需要調整大小，定義它們何時應該摺疊/重排成並排或上下對齊）。
* 實現欄控制。

>[!NOTE]
>
>在現成可用的安裝中，已針對 [We.Retail參考網站](/help/sites-developing/we-retail.md). [啟動配置容器元件](#enable-the-layout-container-component-for-page) 用於其他頁面。

## 設定回應式模擬器 {#configuring-the-responsive-emulator}

此任務可讓您檢視回應式 **模擬器** 在您的網站上。

### 註冊頁面元件以進行模擬 {#register-your-page-components-for-emulation}

若要讓模擬器支援您的頁面，您必須註冊頁面元件。 另請參閱 [註冊模擬的頁面元件](/help/sites-developing/responsive.md#registering-page-components-for-simulation).

### 指定裝置群組 {#specify-the-device-groups}

若要指定顯示在模擬器的「裝置」清單中的裝置群組，請參閱 [指定裝置群組](/help/sites-developing/responsive.md#specifying-the-device-groups).

### 將您的網站連結至指定的裝置群組 {#link-your-site-to-the-specified-device-groups}

若要加入模擬器，請將您的網站連結至裝置群組。 另請參閱 [新增裝置清單](/help/sites-developing/responsive.md#adding-the-devices-list) （適用於傳統和觸控最佳化的UI）。

## 啟用網站的佈局模式 {#activate-layout-mode-for-your-site}

這些程式用於啟用 **版面** 模式。

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
* 有一個預設（現成）中斷點，可涵蓋最後一項以上的所有內容 *已設定* 中斷點。

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
   * 此 `jcr:content` 節點。

1. 在 `jcr:content` 建立節點：

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

中斷點位於 `<jcr:content>` 的區段 `.context.html` 在適當的範本（或內容）資料夾下。

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
>只有在頁面元件不是根據基礎頁面元件時，才需要此專案。

複製下列專案 `cq:infoProviders` 將節點結構放入您的上層頁面元件中：

`/libs/foundation/components/page/cq:infoProviders/responsive`

## 啟用頁面元件大小調整 {#enable-component-resizing-for-the-page}

這些程式是必需的，這樣您就可以在 **版面** 模式。

### 將配置容器設定為主要Parsys {#set-layout-container-as-main-parsys}

若要將頁面的主要parsys設定為配置容器，請將parsys定義為：

`wcm/foundation/components/responsivegrid`

在：

* 頁面元件
* 頁面範本（供日後使用）

以下兩個範例說明定義：

* **HTL：**

  ```xml
  <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
  ```

* **JSP：**

  ```
  <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
  ```

### 包含回應式CSS {#include-the-responsive-css}

#### 使用LESS的中斷點CSS {#css-for-breakpoints-using-less}

AEM使用LESS來產生必要CSS的部分，這些需要包含在您的專案中。

您也必須建立 [使用者端資料庫](https://experienceleague.adobe.com/docs/) 以提供其他設定和函式呼叫。 以下LESS擷取是您必須新增至專案的最小值範例：

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

若要正確調整回應式格線中所包含的最適化影像內容大小並更新其內容，您需要新增 `afterEdit` 設為 `REFRESH_PAGE` 監聽器進入 `EditConfig` 每個包含的元件的檔案。

例如：

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

可透過指令碼使用最適化影像機制，該指令碼控制選擇符合目前視窗大小的正確影像。 在DOM準備就緒或收到專用事件時，它會啟動。 目前必須重新整理頁面，才能正確反映使用者動作的結果。

>[!CAUTION]
>
>自訂樣式表clientlibs必須載入為標頭的一部分，才能在製作和發佈上正確運作。

## 啟用頁面的配置容器元件 {#enable-the-layout-container-component-for-page}

這些工作可讓作者拖曳 **配置容器** 元件移至頁面上。

### 啟用配置容器元件以進行頁面編輯 {#enable-the-layout-container-component-for-page-editing}

若要讓作者更能回應式地新增網格至內容頁面，您必須啟用頁面的「配置容器」元件。 您可以透過以下其中一種方式來達成此目的：

* **作者環境**

  使用 [設計模式](/help/sites-authoring/default-components-designmode.md) 以啟動 **圖層容器** 頁面元件。

* **元件定義**

  使用 `allowedComponent` 或定義元件時的靜態包含。

### 設定配置容器的格線 {#configure-the-grid-of-the-layout-container}

您可以設定可用於配置容器的每個特定執行個體的欄數：

1. **作者環境**

   您可以設定可用於配置容器的每個特定執行個體的欄數。

   若要這麼做，請使用 [設計模式](/help/sites-authoring/default-components-designmode.md)，然後開啟所需容器的「設計」對話方塊。 您可在此指定有多少欄位可供定位和調整大小。 預設值為12。

1. **XML**

   回應式格線的定義指定於：

   `etc/design/<*your-project-name*>/.content.xml`

   可以定義下列引數：

   * 可用的欄數：

      * `columns="{String}8"`

   * 可新增至目前元件的元件：

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`
