---
title: 自訂頁面編寫
seo-title: Customizing Page Authoring
description: AEM提供多種機制，讓您自訂頁面編寫功能
seo-description: AEM provides various mechanisms to enable you to customize page authoring functionality
uuid: 9dc72d98-c5ff-4a00-b367-688ccf896526
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6825dcd6-fa75-4410-b6b2-e7bd4a391224
exl-id: 90594588-db8e-4d4c-a208-22c1c6ea2a2d
source-git-commit: 273836ad0afd6466eac437bf7711e7dbabc1d5e9
workflow-type: tm+mt
source-wordcount: '1383'
ht-degree: 0%

---

# 自訂頁面編寫{#customizing-page-authoring}

>[!CAUTION]
>
>本檔案說明如何在現代化、觸控式的UI中自訂頁面編寫，但不適用於傳統UI。

AEM提供多種機制，讓您可自訂製作例項的頁面製作功能（和[consoles](/help/sites-developing/customizing-consoles-touch.md)）。

* Clientlibs

   Clientlibs可讓您擴充預設實作以實現新功能，同時重複使用標準函式、物件和方法。 自訂時，您可以在`/apps.`下建立自己的clientlib新clientlib必須：

   * 取決於編寫clientlib `cq.authoring.editor.sites.page`
   * 屬於適當的`cq.authoring.editor.sites.page.hook`類別

* 覆蓋

   覆蓋是根據節點定義，並可讓您以您自己的自訂功能（在`/apps`中）覆蓋標準功能（在`/libs`中）。 建立覆蓋時不需要原始資料的1:1副本，因為[sling資源合併](/help/sites-developing/sling-resource-merger.md)允許繼承。

>[!NOTE]
>
>如需詳細資訊，請參閱[JS檔案集](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html)。

這些功能可以用於擴充AEM例項中的頁面編寫功能。 下面將介紹一個選項（在高級別）。

>[!NOTE]
>
>如需詳細資訊，請參閱：
>
>* 使用並建立[clientlibs](/help/sites-developing/clientlibs.md)。
>* 使用並建立[覆蓋](/help/sites-developing/overlays.md)。
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [AEM觸控式UI的結構，以](/help/sites-developing/touch-ui-structure.md) 取得頁面編寫所用結構區域的詳細資訊。

>
>[AEM Gems](https://docs.adobe.com/content/ddc/en/gems.html)工作階段 — [針對AEM 6.0](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-user-interface-customization-for-aem6.html)自訂使用者介面中也涵蓋此主題。

>[!CAUTION]
>
>您&#x200B;***必須***&#x200B;不要變更`/libs`路徑中的任何項目。
>
>這是因為下次升級執行個體時會覆寫`/libs`的內容（而當您套用Hotfix或Feature Pack時，很可能會覆寫）。
>
>設定和其他變更的建議方法為：
>
>1. 在`/apps`下重新建立所需項（即`/libs`中存在的項）
>1. 在`/apps`內進行任何更改


## 添加新圖層（模式） {#add-new-layer-mode}

編輯頁面時，有多種[模式](/help/sites-authoring/author-environment-tools.md#page-modes)可用。 這些模式是使用[layers](/help/sites-developing/touch-ui-structure.md#layer)實現的。 這可讓使用者存取相同頁面內容的不同功能類型。 標準層包括：編輯、預覽、注釋、開發人員和鎖定目標。

### 圖層範例：即時副本狀態 {#layer-example-live-copy-status}

標準AEM例項提供MSM層。 這會存取與[多網站管理](/help/sites-administering/msm.md)相關的資料，並在層中加亮顯示。

若要在實際操作中查看它，您可以編輯任何[We.Retail語言副本](/help/sites-developing/we-retail-globalized-site-structure.md)頁面（或任何其他即時副本頁面），然後選取&#x200B;**即時副本狀態**&#x200B;模式。

您可以在下列位置找到MSM層定義（以供參考）:

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### 程式碼範例 {#code-sample}

此範例套件會示範如何建立新層（模式），這是MSM檢視的新層。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-new-layer-mode專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* 將專案下載為[a ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)

## 新增選取類別至資產瀏覽器 {#add-new-selection-category-to-asset-browser}

資產瀏覽器會顯示各種類型/類別的資產（例如影像、檔案等）。 資產也可依這些資產類別篩選。

### 程式碼範例 {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` 是範例套件，說明如何將新群組新增至資產尋找器。此範例會連結至[Flickr](https://www.flickr.com)的公開資料流，並在側面板中顯示。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-extension-assetfinder-flickr專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* 將專案下載為[a ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)

## 篩選資源 {#filtering-resources}

編寫頁面時，使用者通常必須從資源（例如頁面、元件、資產等）中選取。 這可以採用清單的形式，例如，作者必須從中選擇項目。

為了使清單保持在合理的大小以及與使用案例相關的大小，可以以自訂述詞的形式實施篩選器。 例如，如果使用[`pathbrowser`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui)元件來允許使用者選取特定資源的路徑，則可透過下列方式篩選呈現的路徑：

* 實作[`com.day.cq.commons.predicate.AbstractNodePredicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/predicate/package-summary.html)介面以實作自訂述詞。
* 指定謂語的名稱，並在使用`pathbrowser`時參考該名稱。

如需建立自訂述詞的詳細資訊，請參閱[本文](/help/sites-developing/implementing-custom-predicate-evaluator.md)。

>[!NOTE]
>
>透過實作`com.day.cq.commons.predicate.AbstractNodePredicate`介面來實作自訂述詞，在傳統UI中也能運作。
>
>如需在傳統UI中實作自訂述詞的範例，請參閱[此知識庫文章](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html)。

## 新增動作至元件工具列 {#add-new-action-to-a-component-toolbar}

每個元件（通常）都有工具列，可供存取該元件可採取的一系列動作。

### 程式碼範例 {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` 是範例套件，說明如何建立自訂工具列動作來轉譯元件。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-extension-toolbar — 螢幕擷取專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* 將專案下載為[a ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)

## 新增就地編輯器 {#add-new-in-place-editor}

### 標準就地編輯器 {#standard-in-place-editor}

在標準的 AEM 配置中：

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   保留可用各種編輯器的定義。

1. 編輯器與可使用的每種資源類型（如元件中）之間有連接：

   * `cq:inplaceEditing`

      例如：

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * 屬性: `editorType`

            定義觸發該元件就地編輯時將使用的內嵌編輯器類型；例如`text`、`textimage`、`image`、`title`。

1. 編輯器的其他配置詳細資訊可以使用包含配置的`config`節點以及包含必要插件配置詳細資訊的其他`plugin`節點進行配置。

   以下是定義影像元件的影像裁切外掛程式外觀比例的範例。 請注意，由於螢幕大小可能非常有限，裁切接受率會移至全螢幕編輯器，而且只能在此顯示。

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
   >請注意，在AEM裁切比例中，由`ratio`屬性設定，定義為&#x200B;**height/width**。 這與傳統的寬度/高度定義不同，且是由於舊版相容性原因而完成。 如果您清楚定義`name`屬性，製作使用者將不會察覺到任何差異，因為這是UI中顯示的內容。

#### 建立新的就地編輯器 {#creating-a-new-in-place-editor}

若要實作新的就地編輯器（在您的clientlib內）:

>[!NOTE]
>
>例如，請參閱：
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. 實作：

   * `setUp`
   * `tearDown`

1. 註冊編輯器（包括建構子）:

   * `editor.register`

1. 提供編輯器與可使用的每個資源類型（如元件中）之間的連線。

#### 建立新就地編輯器的程式碼範例 {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` 是範例套件，說明如何在AEM中建立新的就地編輯器。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-extension-inplace-editor專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* 將專案下載為[a ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)

#### 配置多個就地編輯器 {#configuring-multiple-in-place-editors}

您可以設定元件，使元件擁有多個就地編輯器。 設定多個就地編輯器時，您可以選取適當的內容並開啟適當的編輯器。 如需詳細資訊，請參閱[設定多個就地編輯器](/help/sites-developing/multiple-inplace-editors.md)檔案。

## 新增頁面動作 {#add-a-new-page-action}

若要將新頁面動作新增至頁面工具列，例如&#x200B;**返回Sites**（主控台）動作。

### 程式碼範例 {#code-sample-3}

`aem-authoring-extension-header-backtosites` 是範例套件，說明如何建立自訂標頭列動作以跳回Sites主控台。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-extension-header-backtosites專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* 將專案下載為[a ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)

## 自訂啟動工作流程請求 {#customizing-the-request-for-activation-workflow}

現成可用的工作流程&#x200B;**啟動要求**:

* 當內容作者&#x200B;**沒有**&#x200B;適當的復寫權限，但&#x200B;**確實有** DAM-Users和Authors的成員資格時，內容作者會自動出現在適當的功能表中。

* 否則不會顯示任何內容，因為已移除復寫權限。

若要在這類啟動時擁有自訂行為，您可以覆蓋&#x200B;**啟動請求**&#x200B;工作流程：

1. 在`/apps`中覆蓋&#x200B;**Sites**&#x200B;嚮導：

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >這本身會覆寫下列的常見例項：
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. 視需要更新[工作流程模型](/help/sites-developing/workflows-models.md)和相關設定/指令碼。
1. 從所有相關頁面的所有適當使用者移除[ `replicate`動作](/help/sites-administering/security.md#actions)的權利；讓任何使用者嘗試發佈（或復寫）頁面時，將此工作流程觸發為預設動作。
