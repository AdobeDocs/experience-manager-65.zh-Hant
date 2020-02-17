---
title: 自訂頁面編寫
seo-title: 自訂頁面編寫
description: AEM提供多種機制，讓您自訂頁面製作功能
seo-description: AEM提供多種機制，讓您自訂頁面製作功能
uuid: 9dc72d98-c5ff-4a00-b367-688ccf896526
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6825dcd6-fa75-4410-b6b2-e7bd4a391224
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 自訂頁面編寫{#customizing-page-authoring}

>[!CAUTION]
>
>本檔案說明如何在現代化、可觸控的UI中自訂頁面製作，而不適用於傳統UI。

AEM提供多種機制，讓您自訂製作例項的頁面製作功 [能](/help/sites-developing/customizing-consoles-touch.md)（和控制台）。

* Clientlibs

   Clientlibs可讓您擴充預設實作，以實現新功能，同時重複使用標準函式、物件和方法。 在自訂時，您可以在「新的clientlib必須： `/apps.`

   * 取決於編寫clientlib `cq.authoring.editor.sites.page`
   * 屬於適當類 `cq.authoring.editor.sites.page.hook` 別

* 覆蓋

   覆蓋以節點定義為基礎，可讓您將標準功能(在 `/libs`)與您自訂的功能(在 `/apps`)覆蓋。 當建立覆蓋時，不需要原稿的1:1復本，因為 [sling resource merger](/help/sites-developing/sling-resource-merger.md) allows for inheritance。

>[!NOTE]
>
>如需詳細資訊，請參 [閱JS檔案集](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html)。

這些功能可以透過許多方式來延伸AEM例項中的頁面編寫功能。 下面將介紹一個選項（在高級別）。

>[!NOTE]
>
>如需詳細資訊，請參閱：
>
>* 使用和建立 [clientlibs](/help/sites-developing/clientlibs.md)。
>* 使用和建立 [覆蓋](/help/sites-developing/overlays.md)。
>* [花崗岩](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [AEM Touch-Enabled UI的結構](/help/sites-developing/touch-ui-structure.md) ，以取得用於頁面製作的結構區域的詳細資訊。
>
>
AEM Gems工作階段- [User interface customization for AEM 6.0中也包含](https://docs.adobe.com/content/ddc/en/gems.html) 此主題 [](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-user-interface-customization-for-aem6.html)。

>[!CAUTION]
>
>您 ***不得*** 更改路徑中的任 `/libs` 何內容。
>
>這是因為下次升級 `/libs` 實例時會覆寫的內容（套用修補程式或功能套件時可能會覆寫）。
>
>配置和其他更改的建議方法為：
>
>1. 重新建立必要項目(如中所 `/libs`示) `/apps`
>1. 在 `/apps`


## 添加新圖層（模式） {#add-new-layer-mode}

當您編輯頁面時，有多種可用 [模式](/help/sites-authoring/author-environment-tools.md#page-modes) 。 這些模式是使用圖層 [實現的](/help/sites-developing/touch-ui-structure.md#layer)。 這些功能可讓您存取相同頁面內容的不同功能類型。 標準層包括：編輯、預覽、註解、開發人員和鎖定目標。

### 圖層範例：即時副本狀態 {#layer-example-live-copy-status}

標準AEM例項提供MSM層。 這可存取與多網站管 [理相關的資料](/help/sites-administering/msm.md) ，並在層中加亮顯示。

若要檢視其實際運作，您可以編輯任何 [We.Retail語言複製頁面](/help/sites-developing/we-retail-globalized-site-structure.md) （或任何其他即時複製頁面），並選取「即時複製狀 **態」模式** 。

可在以下位置找到MSM層定義（供參考）:

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### 程式碼範例 {#code-sample}

此為範例套件，說明如何建立新圖層（模式），這是MSM檢視的新圖層。

GITHUB代碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-new-layer-mode專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)

## 新增選擇類別至資產瀏覽器 {#add-new-selection-category-to-asset-browser}

資產瀏覽器會顯示各種類型／類別的資產（例如影像、檔案等）。 資產也可依這些資產類別篩選。

### 程式碼範例 {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` 是範例套件，說明如何新增群組至資產搜尋器。 此範例會連結 [至Flickr](https://www.flickr.com)的公用串流，並在側面板中顯示。

GITHUB代碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-extension-assetfinder-flickr專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)

## 篩選資源 {#filtering-resources}

在編寫頁面時，使用者通常必須從資源（例如頁面、元件、資產等）中選取。 這可以以清單的形式，例如作者必須從中選擇項目。

為了將清單保持在合理的大小，並且與使用案例相關，篩選器可以以自訂謂詞的形式實施。 例如，如果使用 [`pathbrowser`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) Granite [](/help/sites-developing/touch-ui-concepts.md#granite-ui) （花崗岩）元件來允許使用者選取特定資源的路徑，則可依下列方式篩選顯示的路徑：

* 實施介面，以實作自訂 [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/predicate/package-summary.html) 謂語。
* 指定謂語的名稱，並在使用時參照該名稱 `pathbrowser`。

如需建立自訂述詞的詳細資訊，請參 [閱此文章](/help/sites-developing/implementing-custom-predicate-evaluator.md)。

>[!NOTE]
>
>透過實作介面來實作自訂 `com.day.cq.commons.predicate.AbstractNodePredicate` 述語，在傳統UI中也能運作。
>
>如需 [在傳統UI中實作自訂謂詞的範例](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html) ，請參閱此知識庫文章。

## 將新動作新增至元件工具列 {#add-new-action-to-a-component-toolbar}

每個元件（通常）都有工具列，可讓您存取該元件可執行的動作範圍。

### 程式碼範例 {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` 是示例包，其中顯示如何建立自定義工具欄操作來渲染元件。

GITHUB代碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-extension-toolbar-screenshot專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)

## 新增就地編輯器 {#add-new-in-place-editor}

### 標準就地編輯器 {#standard-in-place-editor}

在標準AEM安裝中：

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   包含各種可用編輯器的定義。

1. 編輯器和每個資源類型（如元件中）之間有一個連接，可以使用它：

   * `cq:inplaceEditing`

      例如：

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * 屬性: `editorType`

            定義在觸發該元件的就地編輯時將使用的內嵌編輯器類型；例如， `text`, `textimage`, `image`, `title`。

1. 可使用包含配置的節點以及包含必要插件配 `config` 置詳細資訊的其他節點來 `plugin` 配置編輯器的附加配置詳細資訊。

   以下是定義影像元件影像裁切外掛程式外觀比例的範例。 請注意，由於螢幕大小可能非常有限，所以裁切對應比率會移至全螢幕編輯器，而且只能在此顯示。

   ```xml
   <cq:inplaceEditing
           jcr:primaryType="cq:InplaceEditingConfig"
           active="{Boolean}true"
           editorType="image">
           <config jcr:primaryType="nt:unstructured">
               <plugins jcr:primaryType="nt:unstructured">
                   <crop jcr:primaryType="nt:unstructured">
                       <aspectRatios jcr:primaryType="nt:unstructured">
                           <_x0031_6-10
                               jcr:primaryType="nt:unstructured"
                               name="16 : 10"
                               ratio="0.625"/>
                       </aspectRatios>
                   </crop>
               </plugins>
           </config>
   </cq:inplaceEditing>
   ```

   >[!CAUTION]
   >
   >請注意，在AEM裁切比例中，如屬性所設 `ratio` 定，會定義為高 **度／寬度**。 這與傳統的寬度／高度定義不同，是由於舊有的相容性原因而完成的。 如果您清楚定義屬性，編寫使用者將不會察覺到任何差 `name` 異，因為這是UI中顯示的內容。

#### 建立新的就地編輯器 {#creating-a-new-in-place-editor}

要實作新的就地編輯器（在您的clientlib中）:

>[!NOTE]
>
>例如，請參閱：
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. 實施：

   * `setUp`
   * `tearDown`

1. 註冊編輯器（包括建構函式）:

   * `editor.register`

1. 提供編輯器與可使用它的每種資源類型（如元件中）之間的連接。

#### 建立新就地編輯器的程式碼範例 {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` is a sample package show to create new in-place editor in AEM.

GITHUB代碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-extension-inplace-editor專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)

#### 設定多個就地編輯器 {#configuring-multiple-in-place-editors}

您可以設定元件，讓元件擁有多個就地編輯器。 當設定多個就地編輯器時，您可以選取適當的內容並開啟適當的編輯器。 如需詳細 [資訊，請參閱設定多個就地編輯器](/help/sites-developing/multiple-inplace-editors.md) 檔案。

## 新增頁面動作 {#add-a-new-page-action}

若要將新的頁面動作新增至頁面工具列，例如「 **返回網站** （主控台）」動作。

### 程式碼範例 {#code-sample-3}

`aem-authoring-extension-header-backtosites` 是範例套件，其中顯示如何建立自訂標題列動作，以跳回Sites主控台。

GITHUB代碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-extension-header-backtosites專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)

## 自訂啟動工作流程的要求 {#customizing-the-request-for-activation-workflow}

當內容作者沒有適當的複製權限時，即 **可立即啟動的工作流程**，即會自動觸發。

若要在啟動後進行自訂行為，您可以覆蓋「 **啟動要求」工作流程** :

1. 在覆 `/apps` 蓋網站 **精靈** :

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >這本身會覆寫下列的常見例項：
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. 視需要 [更新工作流程模](/help/sites-developing/workflows-models.md) 型和相關的組態／指令碼。
1. 移除所有相關頁面 [ 之所 `replicate` 有適當使](/help/sites-administering/security.md#actions) 用者的動作權；讓此工作流程在任何使用者嘗試發佈（或複製）頁面時觸發為預設動作。

