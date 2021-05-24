---
title: 配置佈局容器和佈局模式
seo-title: 配置佈局容器和佈局模式
description: 了解如何設定「配置容器」和「配置模式」。
seo-description: 了解如何設定「配置容器」和「配置模式」。
uuid: 952b7c86-76ab-4699-8530-8638e46bb50f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 10940000-808a-48ae-8e46-61eccef71eab
legacypath: /content/docs/en/aem/6-2/administer/operations/page-authoring/configuring-responsive-layouting
exl-id: 61152b2d-4c0b-4cfd-9669-cf03d32cb7c7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 1%

---

# 配置佈局容器和佈局模式{#configuring-layout-container-and-layout-mode}

[回應](/help/sites-authoring/responsive-layout.md) 式版面是實現回應式 [網頁設計的機制](https://en.wikipedia.org/wiki/Responsive_web_design)。這可讓使用者建立網頁，其版面和維度取決於其使用者使用的裝置。

>[!NOTE]
>
>這可與[行動Web](/help/sites-developing/mobile-web.md)機制（主要用於傳統UI）進行比較。

AEM使用組合機制來實現頁面的回應式版面：

* [**佈局容**](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode) 器元件

   此元件提供了網格段落系統，允許您在響應式網格中添加和定位元件。 它可作為頁面的預設parsys，和/或讓元件瀏覽器中的作者使用。

   * 預設&#x200B;**Layout Container**&#x200B;元件定義於：

      /libs/wcm/foundation/components/responsivegrid

   * 您可以定義版面容器：

      * 作為使用者可新增至頁面的元件。
      * 作為頁面的預設parsys。
      * 兩者.

         您可以讓版面容器作為頁面的標準，同時讓使用者在此內新增更多版面容器；例如，要實現列控制。

* **[配](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**
置模式一旦將配置容器定位在頁面上，即可使用 
**** 版面模式，以在回應式格線內定位內容。

* [****](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)
模擬器這可讓您建立和編輯回應式網站，透過互動方式調整元件大小，根據裝置/視窗大小重新排列版面。然後，使用者就可以看到使用模擬器呈現內容的方式。

>[!CAUTION]
>
>雖然傳統UI中提供了&#x200B;**版面容器**&#x200B;元件，但其完整功能僅可在觸控式UI中提供。

使用這些回應式格線機制，您可以：

* 使用斷點（表示設備分組）根據設備佈局定義不同的內容行為。
* 根據設備組隱藏元件（定義將隱藏元件的斷點）。
* 使用水準對齊網格（將元件放入網格中，根據需要調整大小，定義它們何時應折疊/重排以並排或在上/下）。
* 實現列控制。

>[!NOTE]
>
>在現成可用的安裝中，已為[We.Retail參考網站](/help/sites-developing/we-retail.md)設定回應式版面。 您仍須為其他頁面啟用「版面容器」元件](#enable-the-layout-container-component-for-page)。[

## 配置響應模擬器{#configuring-the-responsive-emulator}

此任務可讓您在網站上看到回應式&#x200B;**模擬器**。

### 註冊要模擬的頁面元件{#register-your-page-components-for-emulation}

若要讓模擬器支援您的頁面，您必須註冊頁面元件。 請參閱[註冊頁面元件以進行模擬](/help/sites-developing/responsive.md#registering-page-components-for-simulation)。

### 指定設備組{#specify-the-device-groups}

要指定出現在模擬器的「設備」清單中的設備組，請參閱[指定設備組](/help/sites-developing/responsive.md#specifying-the-device-groups)。

### 將站點連結到指定的設備組{#link-your-site-to-the-specified-device-groups}

若要納入您將網站連結至裝置群組所需的模擬器。 請參閱[新增裝置清單](/help/sites-developing/responsive.md#adding-the-devices-list)（適用於傳統和觸控最佳化UI）。

## 啟用網站的佈局模式{#activate-layout-mode-for-your-site}

這些過程用於在您的站點上啟用&#x200B;**Layout**&#x200B;模式。

### 配置斷點{#configure-the-breakpoints}

[中斷點](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate):

* 用於回應式設計。
* 可定義：

   * 在頁面範本上，從中將設定複製到使用該範本建立的任何頁面。
   * 在頁面節點上，任何子頁面都會從中繼承設定。

* 定義標題和寬度：

   * 標題說明一般裝置分組，如有需要，可提供方向；例如phone、tablet、tablelandscape。
   * 寬度以像素定義該通用設備分組的最大寬度。 例如，如果斷點電話的寬度為768，則該寬度為用於電話設備的佈局的最大寬度。

* 使用模擬器時，在頁面編輯器頂端會顯示為標籤。
* 繼承自父節點層次結構，可以隨時覆蓋。
* 有一個預設（現成）斷點，它涵蓋最後&#x200B;*configured*&#x200B;斷點上的所有內容。

可使用CRXDE Lite或XML來定義。

>[!NOTE]
>
>如果您要設定新專案：
>
>* 您需要向模板添加斷點。
>
>
如果您要移轉現有專案（含現有內容），您需要：
>
>* 將斷點添加到模板
>* 將相同的斷點添加到現有頁面

>
>  
由於繼承正在運作，您可以將此限制在內容的根頁面。

#### 使用CRXDE Lite{#configuring-breakpoints-using-crxde-lite}配置斷點

1. 使用CRXDE Lite（或同等項目），導覽至以下任一項目：

   * 您的範本定義。
   * 頁面的`jcr:content`節點。

1. 在`jcr:content`下建立節點：

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

#### 使用XML {#configuring-breakpoints-using-xml}配置斷點

斷點位於`.context.html`的`<jcr:content>`部分內，位於相應的模板（或內容）資料夾下。

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
>只有在頁面元件並非根據基礎頁面元件時，才需要此項。

將下列`cq:infoProviders`節點結構複製到您的上層頁面元件：

`/libs/foundation/components/page/cq:infoProviders/responsive`

## 為頁面{#enable-component-resizing-for-the-page}啟用元件大小調整

需要這些過程，以便您可以在&#x200B;**Layout**&#x200B;模式下調整元件大小。

### 將「佈局容器」設定為主Parsys {#set-layout-container-as-main-parsys}

若要將頁面的主要parsys設為版面容器，您必須將parsys定義為：

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

### 納入回應式CSS {#include-the-responsive-css}

#### 使用LESS {#css-for-breakpoints-using-less}的斷點的CSS

AEM使用LESS來產生部分必要的CSS，這些需要包含在您的專案中。

您還需要建立[用戶端程式庫](https://docs.adobe.com/content/docs/en/aem/6-0/develop/the-basics/clientlibs.html)以提供其他設定和函式呼叫。 以下LESS提取是您需要向項目添加的最低值的示例：

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

#### 樣式考量事項{#styling-considerations}

根據回應式格線大小，保持在回應式容器內的元件會調整大小（連同其各自的HTML DOM元素）。 因此，在這些情況下，建議避免（或更新）固定寬度（包含）DOM元素的定義。

例如：

* 變更前:

   * `width=100px`

* 變更後:

   * `max-width=100px`

#### 調整大小和適應性影像合規性{#resizing-and-adaptive-image-compliance}

網格中元件的任何大小調整都將觸發以下監聽器：

* `beforeedit`
* `beforechildedit`
* `afteredit`

* `afterchildedit`

若要正確調整回應式格線中包含之適用性影像的內容大小並加以更新，您需要將設為`REFRESH_PAGE`監聽器的`afterEdit`新增至每個包含元件的`EditConfig`檔案中。

例如：

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

通過指令碼使自適應影像機制可用，該指令碼控制對窗口當前大小的正確影像的選擇。 DOM準備就緒或收到專用事件時，就會啟用。 目前必須重新整理頁面才能正確反映使用者動作的結果。

>[!CAUTION]
>
>自訂樣式表clientlib必須載入為標題的一部分，才能在製作和發佈上正常運作。

## 為頁面{#enable-the-layout-container-component-for-page}啟用「佈局容器」元件

這些工作可讓作者將&#x200B;**Layout Container**&#x200B;元件的例項拖曳至頁面上。

### 啟用「頁面編輯」的「版面容器」元件{#enable-the-layout-container-component-for-page-editing}

若要允許作者為內容頁面新增更多回應式格線，您必須為頁面啟用「版面容器」元件。 您可以使用下列任一項來執行此作業：

* **製作環境**

   使用[設計模式](/help/sites-authoring/default-components-designmode.md)為頁面激活&#x200B;**層容器**&#x200B;元件。

* **元件定義**

   定義元件時，請使用`allowedComponent`或靜態包含。

### 配置佈局容器的網格{#configure-the-grid-of-the-layout-container}

您可以設定配置容器的每個特定例項可用的欄數：

1. **製作環境**

   您可以設定配置容器的每個特定例項可用的欄數。

   要執行此操作，請使用[設計模式](/help/sites-authoring/default-components-designmode.md)，然後開啟所需容器的設計對話框。 您可以在此處指定定位和調整大小所需的欄數。 預設為12。

1. **XML**

   回應式格線的定義在中指定：

   `etc/design/<*your-project-name*>/.content.xml`

   可定義下列參數：

   * 可用列數：

      * `columns="{String}8"`
   * 可新增至目前元件的元件：

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`
