---
title: 自定義頁面創作
seo-title: Customizing Page Authoring
description: 提供AEM了各種機制，使您能夠自定義頁面創作功能
seo-description: AEM provides various mechanisms to enable you to customize page authoring functionality
uuid: 9dc72d98-c5ff-4a00-b367-688ccf896526
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6825dcd6-fa75-4410-b6b2-e7bd4a391224
exl-id: 90594588-db8e-4d4c-a208-22c1c6ea2a2d
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '1354'
ht-degree: 0%

---

# 自定義頁面創作{#customizing-page-authoring}

>[!CAUTION]
>
>本文檔介紹如何在現代的、支援觸摸的UI中自定義頁面創作，不適用於傳統UI。

提AEM供了各種機制，使您能夠自定義頁面創作功能(以及 [控制台](/help/sites-developing/customizing-consoles-touch.md))。

* Clientlibs

   客戶端允許您擴展預設實現以實現新功能，同時重用標準函式、對象和方法。 自定義時，可以在 `/apps.` 新客戶端庫必須：

   * 取決於創作客戶端庫 `cq.authoring.editor.sites.page`
   * 是適當的 `cq.authoring.editor.sites.page.hook` 類別

* 覆蓋

   疊加基於節點定義，允許您疊加標準功能(在 `/libs`) `/apps`)。 在建立覆蓋時，不需要原件的1:1副本，因為 [Sling資源合併](/help/sites-developing/sling-resource-merger.md) 允許繼承。

>[!NOTE]
>
>有關詳細資訊，請參閱 [JS文檔集](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html)。

這些功能可以通過多種方式擴展實例中的頁面創作AEM功能。 下面將覆蓋選區（在高級別）。

>[!NOTE]
>
>如需進一步詳細資訊，請參閱：
>
>* 使用和建立 [客戶端](/help/sites-developing/clientlibs.md)。
>* 使用和建立 [重疊](/help/sites-developing/overlays.md)。
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [啟用觸摸AEM的UI的結構](/help/sites-developing/touch-ui-structure.md) 的子菜單。
>



>[!CAUTION]
>
>你 ***必須*** 沒有改變 `/libs` 路徑。
>
>這是因為 `/libs` 在下次升級實例時被覆蓋（在應用修補程式或功能包時很可能被覆蓋）。
>
>建議的配置和其他更改方法是：
>
>1. 重新建立所需項(如 `/libs`) `/apps`
>1. 在 `/apps`


## 添加新層（模式） {#add-new-layer-mode}

編輯頁面時，有各種 [模式](/help/sites-authoring/author-environment-tools.md#page-modes) 的下界。 這些模式使用 [層](/help/sites-developing/touch-ui-structure.md#layer)。 這些功能允許訪問相同頁面內容的不同類型的功能。 標準層包括：編輯、預覽、注釋、開發人員和目標。

### 層示例：即時複製狀態 {#layer-example-live-copy-status}

標準實AEM例提供MSM層。 此訪問與 [多站點管理](/help/sites-administering/msm.md) 在圖層中加亮。

要在操作中查看它，您可以編輯任何 [We.Retail語言副本](/help/sites-developing/we-retail-globalized-site-structure.md) 頁（或任何其他即時副本頁），並選擇 **即時複製狀態** 的子菜單。

可在以下位置找到MSM層定義（供參考）:

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### 代碼示例 {#code-sample}

這是一個示例包，它顯示如何建立新層（模式），這是MSM視圖的新層。

GITHUB代碼

可以在GitHub上找到此頁的代碼

* [在GitHub上開啟創作新層模式項目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* 將項目下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)

## 將新選擇類別添加到資產瀏覽器 {#add-new-selection-category-to-asset-browser}

資產瀏覽器顯示各種類型/類別的資產（如影像、文檔等）。 資產也可按這些資產類別進行篩選。

### 代碼示例 {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` 是一個示例包，其中顯示了如何向資產查找器添加新組。 此示例連接到 [Flickr](https://www.flickr.com)在旁邊顯示。

GITHUB代碼

可以在GitHub上找到此頁的代碼

* [在GitHub上開啟aem-authoring-extension-assetfinder-flickr項目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* 將項目下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)

## 篩選資源 {#filtering-resources}

創作頁面時，用戶通常必須從資源（如頁面、元件、資產等）中進行選擇。 這可以採用清單的形式，例如，作者必須從中選擇一個項。

為了使清單保持在合理的大小並且與使用情形相關，可以以自定義謂語的形式實現過濾器。 例如，如果 [`pathbrowser`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) [花崗岩](/help/sites-developing/touch-ui-concepts.md#granite-ui) 元件用於允許用戶選擇特定資源的路徑，所呈現的路徑可以按以下方式過濾：

* 通過實現實現自定義謂詞 [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/predicate/package-summary.html) 。
* 指定謂詞的名稱，並在使用 `pathbrowser`。

有關建立自定義謂詞的詳細資訊，請參見 [這篇文章](/help/sites-developing/implementing-custom-predicate-evaluator.md)。

>[!NOTE]
>
>通過實現實現自定義謂語 `com.day.cq.commons.predicate.AbstractNodePredicate` 介面在經典UI中也有效。
>
>請參閱 [此知識庫文章](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html) 例如，在標準UI中實現自定義謂詞的示例。

## 將新操作添加到元件工具欄 {#add-new-action-to-a-component-toolbar}

每個元件（通常）都有一個工具欄，它提供對可對該元件執行的操作範圍的訪問。

### 代碼示例 {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` 是示例包，說明如何建立用於呈現元件的自定義工具欄操作。

GITHUB代碼

可以在GitHub上找到此頁的代碼

* [在GitHub上開啟創作擴展工具欄螢幕快照項目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* 將項目下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)

## 添加新就地編輯器 {#add-new-in-place-editor}

### 標準就地編輯器 {#standard-in-place-editor}

在標準的 AEM 配置中：

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   保存各種編輯器的定義。

1. 編輯器與可使用的每種資源類型（如元件中）之間有連接：

   * `cq:inplaceEditing`

      例如：

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * 屬性: `editorType`

            定義觸發元件就地編輯時使用的內聯編輯器類型；例如 `text`。 `textimage`。 `image`。 `title`。

1. 可以使用 `config` 包含配置的節點以及 `plugin` 節點以包含必要的插件配置詳細資訊。

   下面是為影像元件的影像裁剪插件定義長寬比的示例。 請注意，由於螢幕大小可能非常有限，因此裁剪適應比已移動到全屏編輯器，只能在全屏編輯器中看到。

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
   >請注意，AEM在裁剪比中，由 `ratio` 屬性，定義為 **高度/寬度**。 這不同於傳統的寬度/高度定義，並且是出於傳統相容性原因。 如果您定義 `name` 屬性，因為這是UI中顯示的內容。

#### 建立新就地編輯器 {#creating-a-new-in-place-editor}

要實施新的就地編輯器（在客戶端庫中）:

>[!NOTE]
>
>例如，請參見：
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. 實施：

   * `setUp`
   * `tearDown`

1. 註冊編輯器（包括建構子）:

   * `editor.register`

1. 提供編輯器與可使用它的每種資源類型（如元件中）之間的連接。

#### 建立新就地編輯器的代碼示例 {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` 是一個示例包，其中顯示了如何在中建立新就地編輯AEM器。

GITHUB代碼

可以在GitHub上找到此頁的代碼

* [在GitHub上開啟創作擴展就地編輯器項目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* 將項目下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)

#### 配置多個就地編輯器 {#configuring-multiple-in-place-editors}

可以配置元件，使其具有多個就地編輯器。 配置多個就地編輯器後，您可以選擇適當的內容並開啟相應的編輯器。 查看 [配置多個就地編輯器](/help/sites-developing/multiple-inplace-editors.md) 的子菜單。

## 添加新頁面操作 {#add-a-new-page-action}

向頁面工具欄添加新頁面操作，例如 **返回站點** （控制台）操作。

### 代碼示例 {#code-sample-3}

`aem-authoring-extension-header-backtosites` 是一個示例包，它顯示如何建立自定義標題欄操作以跳回到「站點」控制台。

GITHUB代碼

可以在GitHub上找到此頁的代碼

* [在GitHub上開啟創作擴展頭 — 回切站點項目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* 將項目下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)

## 自定義激活工作流請求 {#customizing-the-request-for-activation-workflow}

開箱即用的工作流程， **激活請求**:

* 當內容作者 **沒有** 適當的複製權限，但 **有** DAM用戶和作者的成員身份。

* 否則，將不顯示任何內容，因為已刪除複製權限。

要在此類激活時進行自定義行為，可以覆蓋 **激活請求** 工作流：

1. 在 `/apps` 覆蓋 **站點** 嚮導：

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >它本身將覆蓋以下的常見實例：
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. 更新 [工作流模型](/help/sites-developing/workflows-models.md) 以及所需的相關配置/指令碼。
1. 刪除 [ `replicate` 動作](/help/sites-administering/security.md#actions) 向所有相關頁面的適當用戶發送；當任何用戶嘗試發佈（或複製）頁面時，將此工作流觸發為預設操作。
