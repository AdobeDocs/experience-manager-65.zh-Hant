---
title: 自訂頁面編寫
description: Adobe Experience Manager (AEM)提供多種機制，讓您自訂頁面製作功能。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 90594588-db8e-4d4c-a208-22c1c6ea2a2d
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 39%

---

# 自訂頁面編寫{#customizing-page-authoring}

>[!CAUTION]
>
>本檔案說明如何在現代、觸控式UI中自訂頁面編寫，且不套用至傳統UI。

Adobe Experience Manager (AEM)提供多種機制，讓您自訂頁面製作功能(以及 [主控台](/help/sites-developing/customizing-consoles-touch.md))。

* Clientlibs

  Clientlibs可讓您擴充預設實作以實現新功能，同時重複使用標準函式、物件和方法。 進行自訂時，您可以在 `/apps.` 下面建立自己的 clientlib。新的 clientlib 必須：

   * 取決於編寫clientlib `cq.authoring.editor.sites.page`
   * 屬於適當的 `cq.authoring.editor.sites.page.hook` 類別

* 覆蓋

  覆蓋是以節點定義為基礎，可讓您覆蓋標準功能(在 `/libs`)搭配您自己的自訂功能(在 `/apps`)。 建立覆蓋圖時，不需要原始影像的1:1復本，因為 [sling資源合併](/help/sites-developing/sling-resource-merger.md) 允許繼承。

>[!NOTE]
>
>如需詳細資訊，請參閱 [JS檔案集](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html).

您可以透過多種方式，在AEM例項中擴充頁面製作功能。 選取範圍會涵蓋在底下（高階）。

>[!NOTE]
>
>如需詳細資訊，請參閱下列內容：
>
>* 使用和建立 [clientlibs](/help/sites-developing/clientlibs.md).
>* 使用和建立 [覆蓋](/help/sites-developing/overlays.md).
>* [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [AEM觸控式UI的結構](/help/sites-developing/touch-ui-structure.md) 以取得用於編寫頁面的結構區域的詳細資訊。
>


>[!CAUTION]
>
>***不要*** 變更 `/libs` 路徑。
>
>原因是因為的內容 `/libs` 下次升級您的執行個體時，即會被覆寫（當您套用hotfix或feature pack時，很可能會遭到覆寫）。
>
>設定和其他變更的建議方法是：
>
>1. 重新建立所需專案（即存在於中的專案） `/libs`)下 `/apps`
>1. 進行任何變更 `/apps`

## 新增「新圖層」(模式) {#add-new-layer-mode}

當您編輯頁面時，有各種[模式](/help/sites-authoring/author-environment-tools.md#page-modes)可使用。這些模式會使用[圖層](/help/sites-developing/touch-ui-structure.md#layer)實作。這些可容許存取相同頁面內容的不同功能類型。標準圖層包括：編輯、預覽、註釋、開發人員和鎖定目標。

### 圖層範例：Live Copy 狀態 {#layer-example-live-copy-status}

標準 AEM 執行個體會提供 MSM 圖層。這會存取和[多網站管理](/help/sites-administering/msm.md)相關的資料並在圖層中將其醒目顯示。

若要檢視其運作情況，您可以編輯任何 [We.Retail語言副本](/help/sites-developing/we-retail-globalized-site-structure.md) 頁面（或任何其他即時副本頁面）並選取 **即時副本狀態** 模式。

您可以在以下位置找到 MSM 圖層定義 (僅供參考)：

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### 程式碼範例 {#code-sample}

這是一個範例套件，說明如何建立圖層（模式），這是MSM檢視的新圖層。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-new-layer-mode專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)

## 將新選擇類別新增到資產瀏覽器 {#add-new-selection-category-to-asset-browser}

資產瀏覽器會顯示各種類型/類別的資產 (例如影像和文件)。還可以依這些資產類別篩選資產。

### 程式碼範例 {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` 是一種範例套件，會顯示如何將群組新增到資產尋找器。此範例會連接到 [Flickr](https://www.flickr.com) 的公用串流並在側邊面板中顯示它們。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-extension-assetfinder-flickr專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)

## 篩選資源 {#filtering-resources}

編寫頁面時，使用者通常必須從資源（例如頁面、元件和資產）中選取。 例如，這可採取清單的形式，作者必須從中選取專案。

若要將清單保持為合理的大小並且和使用案例相關，可以以自訂述詞的形式實作篩選器。例如，如果 [`pathbrowser`](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui) 元件是用來讓使用者選取特定資源的路徑，可依下列方式篩選顯示的路徑：

* 透過實作 [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/predicate/package-summary.html) 介面實作自訂述詞。
* 指定述詞的名稱，並在使用 `pathbrowser` 時參照該名稱。

如需建立自訂述詞的詳細資訊，請參閱 [本文](/help/sites-developing/implementing-custom-predicate-evaluator.md).

>[!NOTE]
>
>透過實作來實作自訂述詞 `com.day.cq.commons.predicate.AbstractNodePredicate` 介面也可在傳統UI中運作。
>
>另請參閱 [此知識庫文章](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html) 在傳統UI中實作自訂述詞的範例。

## 將新動作新增到元件工具列 {#add-new-action-to-a-component-toolbar}

每個元件（通常是）都有一個工具列，可讓您存取可對該元件執行的一系列動作。

### 程式碼範例 {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` 是一種範例套件，會顯示如何建立可轉譯元件的自訂工具列動作。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-extension-toolbar-screens專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)

## 新增就地編輯器 {#add-new-in-place-editor}

### 標準就地編輯器 {#standard-in-place-editor}

在標準的 AEM 安裝中：

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   儲存各種可用編輯器的定義。

1. 編輯器和可以使用它的每種資源類型 (如在元件中) 之間有連結：

   * `cq:inplaceEditing`

     例如：

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * 屬性：`editorType`

           定義觸發該元件的就地編輯時所使用的內聯編輯器的類型；例如，`text`、`textimage`、`image`、`title`。

1. 編輯器的其他設定詳細資料可使用 `config` 包含設定和的節點 `plugin` 節點，以包含必要的外掛程式設定詳細資料。

   以下範例是為影像元件的影像裁切外掛程式定義外觀比例。 由於熒幕大小有限的可能性，裁切外觀比例已移至全熒幕編輯器，並且僅能在該處看到。

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
   >AEM 裁切比例 (由 `ratio` 屬性設定) 的定義為&#x200B;**高度/寬度比**。這和寬度/高度比的傳統定義不同，並且是由於舊有相容性的原因完成的。如果您清楚定義了 `name` 屬性，編寫的使用者並不會看出任何差異，因為這即是 UI 中所顯示的內容。

#### 建立新的就地編輯器 {#creating-a-new-in-place-editor}

若要實作新的就地編輯器 (在您的 clientlib 裡面)：

>[!NOTE]
>
>例如，請參閱：
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. 實作：

   * `setUp`
   * `tearDown`

1. 註冊編輯器 (包括建構函式)：

   * `editor.register`

1. 提供編輯器和可以使用它的每種資源類型 (如在元件中) 之間的連結：

#### 用於建立新的就地編輯器的程式碼範例 {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` 是一種範例套件，會顯示如何在 AEM 中建立就地編輯器。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-extension-inplace-editor專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)

#### 設定多個就地編輯器 {#configuring-multiple-in-place-editors}

您可以設定元件，使其有多個就地編輯器。 設定多個就地編輯器時，您可以選取適當的內容並開啟適當的編輯器。 請參閱 [設定多個就地編輯器](/help/sites-developing/multiple-inplace-editors.md) 檔案以取得詳細資訊。

## 新增「新頁面動作」。 {#add-a-new-page-action}

若要在頁面工具列中新增頁面動作，例如 **返回網站** （主控台）動作。

### 程式碼範例 {#code-sample-3}

`aem-authoring-extension-header-backtosites` 是一種範例套件，會顯示如何建立自訂標頭列動作以跳回 Sites 主控台。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-extension-header-backtosites專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)

## 自訂要求啟動工作流程 {#customizing-the-request-for-activation-workflow}

此現成可用的工作流程，**要求啟動**：

* 會在內容作者&#x200B;**不具有**&#x200B;適當的複製權時自動顯示在適當的選單上，但&#x200B;**確實具有** DAM 使用者和作者的成員資格。

* 不然的話，由於已移除複製權，因此不會顯示任何內容。

若要在這類啟動上自訂行為，您可以覆蓋「**要求啟動**」工作流程：

1. 在 `/apps` 覆蓋 **網站** 精靈：

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >這本身會覆寫下列的共同例項：
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. 更新 [工作流程模型](/help/sites-developing/workflows-models.md) 以及所需的相關設定/指令碼。
1. 移除「 」的許可權 [`replicate` 動作](/help/sites-administering/security.md#actions) 來自所有相關頁面的所有適當使用者；當任何使用者嘗試發佈（或復寫）頁面時，將此工作流程觸發為預設動作。
