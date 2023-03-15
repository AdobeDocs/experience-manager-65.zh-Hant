---
title: AEM元件 — 基本概念
seo-title: AEM Components - The Basics
description: 開始開發新元件時，您需要了解其結構和配置的基本知識
seo-description: When you start to develop new components you need to understand the basics of their structure and configuration
uuid: 0225b34d-5ac4-40c3-b226-0c9b24bdf782
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 1f9867f1-5089-46d0-8e21-30d62dbf4f45
legacypath: /content/docs/en/aem/6-0/develop/components/components-develop
exl-id: 7ff92872-697c-4e66-b654-15314a8cb429
source-git-commit: 43a30b5ba76ea470cc50a962d4f04b4a1508964d
workflow-type: tm+mt
source-wordcount: '4948'
ht-degree: 1%

---

# AEM元件 — 基本概念{#aem-components-the-basics}

開始開發新元件時，您需要了解其結構和設定的基本知識。

此程式包括閱讀理論，以及查看標準AEM例項中的廣泛元件實作。 雖然AEM已改用新的標準、現代化、觸控式UI，但傳統UI仍可繼續提供支援，這讓後一種方法略為複雜。

## 概觀 {#overview}

本節介紹開發您自己的元件時所需的詳細資訊，並說明重要概念和問題。

### 規劃 {#planning}

開始實際設定或編寫元件程式碼之前，您應先詢問：

* 您到底需要新元件做什麼？
   * 在開發、測試和移交的所有階段，明確的規格都有幫助。 詳細資訊可能會隨時間而改變，但可以更新規格（儘管更改也應記錄在案）。
* 您是否需要從頭建立元件，還是可以從現有元件繼承基本知識？
   * 沒有必要重新發明輪子。
   * AEM提供數種機制，可讓您繼承和延伸其他元件定義的詳細資訊，包括覆寫、覆蓋和 [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md).
* 元件是否需要邏輯才能選取/操控內容？
   * 邏輯應與使用者介面層分開。 HTL的設計目的，是為了協助確保此情況發生。
* 元件是否需要CSS格式？
   * CSS格式應與元件定義分開。 定義命名HTML元素的慣例，以便透過外部CSS檔案修改它們。
* 我應考慮哪些安全方面？
   * 請參閱 [安全性檢查清單 — 開發最佳實務](/help/sites-administering/security-checklist.md#development-best-practices) 以取得詳細資訊。

### 觸控式與傳統UI {#touch-enabled-vs-classic-ui}

在開始進行有關開發元件的嚴肅討論之前，您必須知道您的作者將使用哪個UI:

* **觸控式UI**
   [標準使用者介面](/help/sites-developing/touch-ui-concepts.md) 是以Adobe Marketing Cloud的統一使用者體驗為基礎，使用 [Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui) 和 [Granite UI](/help/sites-developing/touch-ui-concepts.md#granite-ui).
* **傳統UI**
以AEM 6.4淘汰的ExtJS技術為基礎的使用者介面。

請參閱 [適用於客戶的UI介面Recommendations](/help/sites-deploying/ui-recommendations.md) 以取得更多詳細資訊。

可實作元件，以支援觸控式UI、傳統UI或兩者。 查看標準例項時，您也會看到原本為傳統UI、觸控式UI或兩者設計的現成元件。

因此，在本頁中，我們將說明兩者的基本概念，以及如何辨識兩者。

>[!NOTE]
>
>Adobe建議善用觸控式UI，善用最新技術。 [AEM現代化工具](modernization-tools.md) 可讓移轉更輕鬆。

### 內容邏輯和呈現標籤  {#content-logic-and-rendering-markup}

建議您將負責標籤和轉譯的程式碼與控制用來選取元件內容之邏輯的程式碼分開。

這一理念得到了支援 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)，故意限制為確保使用真實寫程式語言來定義基礎業務邏輯的模板語言。 系統會透過特定命令從HTL叫用此（選用）邏輯。 此機制會反白標示為指定檢視所呼叫的程式碼，並視需要為相同元件的不同檢視允許特定邏輯。

### HTL與JSP {#htl-vs-jsp}

HTL是AEM 6.0推出的HTML範本語言。

是否使用 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) 或JSP(Java Server Pages)開發自己的元件時，應該能簡單明瞭，因為HTL現在是AEM的建議指令碼語言。

HTL和JSP皆可用來開發傳統和觸控式UI的元件。 雖然有可能會假設HTL僅適用於傳統UI的觸控式UI和JSP，但這是一種誤解，更多是因為時間的緣故。 大約在相同時段內，觸控式UI和HTL已整合至AEM。 由於HTL現在是建議的語言，因此會用於新元件，而這類元件通常用於觸控式UI。

>[!NOTE]
>
>例外是Granite UI Foundation表單欄位（用於對話方塊）。 這些仍需使用JSP。

### 開發您自己的元件 {#developing-your-own-components}

若要針對適當的UI建立您自己的元件，請參閱（閱讀本頁後）:

* [AEM元件（觸控式UI）](/help/sites-developing/developing-components.md)
* [AEM元件（適用於傳統UI）](/help/sites-developing/developing-components-classic.md)

快速入門的方法是複製現有元件，然後進行您想要的變更。 若要了解如何建立自己的元件並將其新增至段落系統，請參閱：

* [開發元件](/help/sites-developing/developing-components-samples.md) （著重於觸控式UI）

### 將元件移至發佈執行個體 {#moving-components-to-the-publish-instance}

呈現內容的元件必須部署在與內容相同的AEM例項上。 因此，必須在發佈執行個體上部署用於製作和呈現製作執行個體頁面的所有元件。 部署後，元件可用於呈現已激活的頁面。

使用下列工具將元件移至發佈例項：

* [使用套件管理器](/help/sites-administering/package-manager.md) 將元件新增至套件並移至其他AEM例項。
* [使用激活樹複製工具](/help/sites-authoring/publishing-pages.md#manage-publication) 複製元件。

>[!NOTE]
>
>這些機制也可用來在其他例項之間傳輸元件，例如從您的開發將元件傳輸至測試例項。

### 從頭開始要注意的元件 {#components-to-be-aware-of-from-the-start}

* Page:

   * AEM具有 *頁面* 元件() `cq:Page`)。
   * 這是對內容管理非常重要的特定資源類型。
      * 頁面對應於保存網站內容的網頁。

* 段落制度：

   * 段落系統是網站的關鍵部分，因為它管理著段落清單。 它可用來保留和建構包含實際內容的個別元件。
   * 您可以在段落系統中建立、移動、複製和刪除段落。
   * 您也可以選取要在特定段落系統內使用的元件。
   * 標準例項中有各種可用的段落系統(例如 `parsys`, ` [responsivegrid](/help/sites-authoring/responsive-layout.md)`)。

## 結構 {#structure}

AEM元件的結構既強大又靈活，主要考量為：

* 資源類型
* 元件定義
* 元件的屬性和子節點
* 對話方塊
* 設計對話方塊
* 元件可用性
* 元件及其建立的內容

### 資源類型 {#resource-type}

結構的一個關鍵元素是資源類型。

* 內容結構聲明意圖。
* 資源類型會實作它們。

這是抽象，有助於確保即使外觀和感覺隨著時間而改變，意圖仍會持續。

### 元件定義 {#component-definition}

#### 元件基本知識 {#component-basics}

元件的定義可依下列方式劃分：

* AEM元件以 [Sling](https://sling.apache.org/documentation.html).
* AEM元件（通常位於下列位置）:

   * HTL: `/libs/wcm/foundation/components`
   * JSP: `/libs/foundation/components`

* 專案/網站特定元件（通常）位於：

   * `/apps/<myApp>/components`

* AEM標準元件定義為 `cq:Component` 並有關鍵要素：

   * jcr屬性：

      jcr屬性清單；這些是變數，有些可能是選用的，但元件節點的基本結構、其屬性和子節點由 `cq:Component` 定義

   * 資源:

      這些定義元件使用的靜態元素。

   * 指令碼:

   用於實作元件之產生例項的行為。

* **根節點**:

   * `<mycomponent> (cq:Component)`  — 元件的階層節點。

* **重要屬性**:

   * `jcr:title`  — 元件標題；例如，當元件列在元件瀏覽器或sidekick中時，會以標籤的形式使用。
   * `jcr:description`  — 元件的說明；可在元件瀏覽器或sidekick中作為滑鼠移過提示使用。
   * 傳統 UI:

      * `icon.png`  — 此元件的表徵圖。
      * `thumbnail.png`  — 如果此元件列在段落系統中，則顯示的影像。
   * 觸控式 UI

      * 請參閱 [觸控式UI中的元件圖示](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) 以取得詳細資訊。


* **重要子節點**:

   * `cq:editConfig (cq:EditConfig)`  — 定義元件的編輯屬性，並使元件顯示在「元件」瀏覽器或Sidekick中。

      注意：如果元件有對話方塊，則會自動出現在「元件」瀏覽器或Sidekick中，即使cq:editConfig不存在亦然。

   * `cq:childEditConfig (cq:EditConfig)`  — 控制未定義子元件的製作UI方面 `cq:editConfig`.
   * 觸控式UI:

      * `cq:dialog` ( `nt:unstructured`) — 此元件的對話方塊。 定義介面，讓使用者設定元件和/或編輯內容。
      * `cq:design_dialog` ( `nt:unstructured`) — 此元件的設計編輯
   * 傳統 UI:

      * `dialog` ( `cq:Dialog`) — 此元件的對話方塊。 定義介面，讓使用者設定元件和/或編輯內容。
      * `design_dialog` ( `cq:Dialog`) — 此元件的設計編輯。


#### 觸控式UI中的元件圖示 {#component-icon-in-touch-ui}

當開發人員建立元件時，元件的圖示或縮寫會透過元件的JCR屬性定義。 這些屬性的計算順序如下，並使用找到的第一個有效屬性。

1. `cq:icon`  — 指向 [Coral UI程式庫](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) 在元件瀏覽器中顯示
   * 使用Coral圖示的HTML屬性值。
1. `abbreviation`  — 字串屬性，可自訂元件瀏覽器中元件名稱的縮寫
   * 縮寫應限制為兩個字元。
   * 提供空白字串，將會從的前兩個字元建立縮寫 `jcr:title` 屬性。
      * 例如，「Im」代表「Image」
      * 本地化的標題將用於建立縮寫。
   * 僅當元件具有 `abbreviation_commentI18n` 屬性，然後會用作翻譯提示。
1. `cq:icon.png` 或 `cq:icon.svg`  — 此元件的圖示，顯示在元件瀏覽器中
   * 20 x 20像素是標準元件的圖示大小。
      * 較大的圖示會縮小（用戶端）。
   * 建議的顏色為rgb(112, 112, 112)> #707070
   * 標準元件圖示的背景是透明的。
   * 僅 `.png` 和 `.svg` 支援檔案。
   * 如果透過Eclipse外掛程式從檔案系統匯入，檔案名稱需逸出為 `_cq_icon.png` 或 `_cq_icon.svg` 例如，
   * `.png` 先例 `.svg` 如果兩者皆存在

若沒有上述任何屬性( `cq:icon`, `abbreviation`, `cq:icon.png` 或 `cq:icon.svg`)位於元件上：

* 系統會在超級元件上搜尋相同的屬性，如下所示： `sling:resourceSuperType` 屬性。
* 如果在超級元件層級找不到任何縮寫或空白縮寫，則系統會從 `jcr:title` 屬性。

要取消超級元件的表徵圖繼承，請設定空 `abbreviation` 元件上的屬性將回復為預設行為。

此 [元件主控台](/help/sites-authoring/default-components-console.md#component-details) 顯示如何定義特定元件的圖示。

#### SVG圖示範例 {#svg-icon-example}

```xml
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "https://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg version="1.1" id="Layer_1" xmlns="https://www.w3.org/2000/svg" xmlns:xlink="https://www.w3.org/1999/xlink" x="0px" y="0px"
     width="20px" height="20px" viewBox="0 0 20 20" enable-background="new 0 0 20 20" xml:space="preserve">
    <ellipse cx="5" cy="5" rx="3" ry="3" fill="#707070"/>
    <ellipse cx="15" cy="5" rx="4" ry="4" fill="#707070"/>
    <ellipse cx="5" cy="15" rx="5" ry="5" fill="#707070"/>
    <ellipse cx="15" cy="15" rx="4" ry="4" fill="#707070"/>
</svg>
```

### 元件的屬性和子節點 {#properties-and-child-nodes-of-a-component}

定義元件所需的許多節點/屬性在兩個UI中都很常見，差異仍獨立，因此您的元件可在兩個環境中運作。

元件是類型的節點 `cq:Component` 和具有以下屬性和子節點：

<table>
 <tbody>
  <tr>
   <td><strong>名稱 <br /> </strong></td>
   <td><strong>類型 <br /> </strong></td>
   <td><strong>說明 <br /> </strong></td>
  </tr>
  <tr>
   <td>.<br /> </td>
   <td><code>cq:Component</code></td>
   <td>目前元件. 元件屬於節點類型 <code>cq:Component</code>.<br /> </td>
  </tr>
  <tr>
   <td><code>componentGroup</code></td>
   <td><code>String</code></td>
   <td>可在元件瀏覽器（觸控式UI）或Sidekick（傳統UI）中選取元件的群組。<br /> 值 <code>.hidden</code> 用於無法從UI中選取的元件，例如實際段落系統。</td>
  </tr>
  <tr>
   <td><code>cq:isContainer</code></td>
   <td><code>Boolean</code></td>
   <td>指示元件是否為容器元件，因此可以包含諸如段落系統等其他元件。</td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>cq:dialog</code></td>
   <td><code>nt:unstructured</code> </td>
   <td>觸控式UI的編輯對話方塊定義。</td>
  </tr>
  <tr>
   <td><code>dialog</code></td>
   <td><code>cq:Dialog</code></td>
   <td>傳統UI的編輯對話方塊定義。</td>
  </tr>
  <tr>
   <td><code>cq:design_dialog</code></td>
   <td><code>nt:unstructured</code></td>
   <td>觸控式UI的設計對話方塊定義。</td>
  </tr>
  <tr>
   <td><code>design_dialog</code></td>
   <td><code>cq:Dialog </code></td>
   <td>傳統UI的設計對話方塊定義。<br /> </td>
  </tr>
  <tr>
   <td><code>dialogPath</code></td>
   <td><code>String</code></td>
   <td>當元件沒有對話框節點時用於覆蓋大小寫的對話框路徑。<br /> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>cq:cellName</code></td>
   <td><code>String</code></td>
   <td>若已設定，此屬性會視為儲存格ID。 有關詳細資訊，請參閱知識庫文章 <a href="https://helpx.adobe.com/experience-manager/kb/DesigneCellId.html">如何建立設計儲存格ID</a>.<br /> </td>
  </tr>
  <tr>
   <td><code>cq:childEditConfig</code></td>
   <td><code>cq:EditConfig</code></td>
   <td>如果元件是容器（例如段落系統），則這將驅動子節點的編輯配置。<br /> </td>
  </tr>
  <tr>
   <td><code>cq:editConfig</code></td>
   <td><code>cq:EditConfig</code></td>
   <td><a href="#edit-behavior">編輯元件的設定</a>.<br /> </td>
  </tr>
  <tr>
   <td><code>cq:htmlTag</code></td>
   <td><code>nt:unstructured </code></td>
   <td>傳回新增至周圍html標籤的其他標籤屬性。 可將屬性新增至自動產生的div。</td>
  </tr>
  <tr>
   <td><code>cq:noDecoration</code></td>
   <td><code>Boolean</code></td>
   <td>若為true，則不會以自動產生的div和css類別轉譯元件。<br /> </td>
  </tr>
  <tr>
   <td><code>cq:template</code></td>
   <td><code>nt:unstructured</code></td>
   <td>如果找到，則從「元件瀏覽器」或Sidekick新增元件時，此節點將作為內容範本使用。</td>
  </tr>
  <tr>
   <td><code>cq:templatePath</code></td>
   <td><code>String</code></td>
   <td>從「元件」瀏覽器或Sidekick新增元件時，節點用作內容範本的路徑。 此路徑必須是絕對路徑，而非相對於元件節點。<br /> 除非您想要重複使用其他地方已有的內容，否則不需要， <code>cq:template</code> 已足夠（請參閱下文）。</td>
  </tr>
  <tr>
   <td><code>jcr:created</code></td>
   <td><code>Date</code></td>
   <td>元件的建立日期。<br /> </td>
  </tr>
  <tr>
   <td><code>jcr:description</code></td>
   <td><code>String</code></td>
   <td>元件說明。<br /> </td>
  </tr>
  <tr>
   <td><code>jcr:title</code></td>
   <td><code>String</code></td>
   <td>元件的標題。<br /> </td>
  </tr>
  <tr>
   <td><code>sling:resourceSuperType</code></td>
   <td><code>String</code></td>
   <td>設定後，元件會從此元件繼承。<br /> </td>
  </tr>
  <tr>
   <td><code>virtual</code></td>
   <td><code>sling:Folder</code></td>
   <td>啟用虛擬元件的建立。 若要查看範例，請查看以下連絡元件：<br /> <code>/libs/foundation/components/profile/form/contact</code></td>
  </tr>
  <tr>
   <td><code>&lt;breadcrumb.jsp&gt;</code></td>
   <td><code>nt:file</code> </td>
   <td>指令碼檔案。<br /> </td>
  </tr>
  <tr>
   <td><code>icon.png</code></td>
   <td><code>nt:file</code></td>
   <td>元件的圖示會出現在Sidekick中的Title旁。<br /> </td>
  </tr>
  <tr>
   <td><code>thumbnail.png</code></td>
   <td><code>nt:file</code></td>
   <td>從Sidekick拖曳元件至適當位置時顯示的選用縮圖。<br /> </td>
  </tr>
 </tbody>
</table>

如果我們看 **文字** 元件（任一版本），便會看到下列元素：

* HTL ( `/libs/wcm/foundation/components/text`)

   ![chlimage_1-241](assets/chlimage_1-241.png)

* JSP( `/libs/foundation/components/text`)

   ![screen_shot_2012-02-13at60457pm](assets/screen_shot_2012-02-13at60457pm.png)

特定權益物業包括：

* `jcr:title`  — 元件標題；這可用來識別元件，例如，元件會顯示在元件瀏覽器或sidekick內的元件清單中
* `jcr:description`  — 元件的說明；可在sidekick內的元件清單中作為滑鼠移過提示使用
* `sling:resourceSuperType`:這表示延伸元件時的繼承路徑（透過覆寫定義）

特別感興趣的子節點包括：

* `cq:editConfig` ( `cq:EditConfig`) — 此功能可控制視覺效果；例如，它可以定義條形或介面工具集的外觀，也可以添加自定義控制項
* `cq:childEditConfig` ( `cq:EditConfig`) — 這會控制子元件的視覺化方面，這些元件沒有其自己的定義
* 觸控式UI:
   * `cq:dialog` ( `nt:unstructured`) — 定義用於編輯此元件內容的對話框
   * `cq:design_dialog` ( `nt:unstructured`) — 指定此元件的設計編輯選項
* 傳統 UI:
   * `dialog` ( `cq:Dialog`) — 定義用於編輯此元件內容的對話方塊（專用於傳統UI）
   * `design_dialog` ( `cq:Dialog`) — 指定此元件的設計編輯選項
   * `icon.png`  — 要用作Sidekick中元件表徵圖的圖形檔案
   * `thumbnail.png`  — 將元件從Sidekick拖動時用作元件縮圖的圖形檔案

### 對話方塊 {#dialogs}

對話方塊是元件的關鍵元素，因為對話方塊提供介面，供作者設定及提供該元件的輸入。

根據元件的複雜性，您的對話框可能需要一個或多個頁簽，以保持對話框簡短並對輸入欄位進行排序。

對話方塊定義是UI專屬的：

>[!NOTE]
>
>* 為了相容性目的，當未為觸控式UI定義對話方塊時，觸控式UI可使用傳統UI對話方塊的定義。
>* 此 [AEM現代化工具](/help/sites-developing/modernization-tools.md) 也可協助您擴充/轉換僅為傳統UI定義對話方塊的元件。
>


* 觸控式UI
   * `cq:dialog` ( `nt:unstructured`)節點：
      * 定義用於編輯此元件的內容的對話框
      * 特定於觸控式UI
      * 是使用Granite UI元件來定義
      * 有屬性 `sling:resourceType`，作為標準Sling內容結構
      * 可以有屬性 `helpPath` 定義幫助表徵圖(? 圖示)。
         * 若為現成可用的元件，這通常會參照檔案中的頁面。
         * 若否 `helpPath` 指定時，會顯示預設URL（檔案概述頁面）。

   ![chlimage_1-242](assets/chlimage_1-242.png)

   在對話方塊中，會定義個別欄位：

   ![screen_shot_2012-02-13at60937pm](assets/screen_shot_2012-02-13at60937pm.png)

* 傳統 UI
   * `dialog` ( `cq:Dialog`)節點
      * 定義用於編輯此元件的內容的對話框
      * 專屬於傳統UI
      * 是使用ExtJS Widget定義
      * 有屬性 `xtype`，指ExtJS
      * 可以有屬性 `helpPath` 定義上下文相關幫助資源（絕對或相對路徑），此資源在 **說明** 按鈕。
         * 若為現成可用的元件，這通常會參照檔案中的頁面。
         * 若否 `helpPath` 指定時，會顯示預設URL（檔案概述頁面）。

   ![chlimage_1-243](assets/chlimage_1-243.png)

   在對話方塊中，會定義個別欄位：

   ![chlimage_1-244](assets/chlimage_1-244.png)

   在傳統對話方塊中：

   * 您可以建立對話方塊，如 `cq:Dialog`，可提供單一索引標籤（如文字元件中），或如果您需要多個索引標籤（如同文字時間元件），則對話方塊可定義為 `cq:TabPanel`.
   * a `cq:WidgetCollection` ( `items`)可用來提供任一輸入欄位的基礎( `cq:Widget`)或其他頁簽( `cq:Widget`)。 此階層可延伸。


### 設計對話方塊 {#design-dialogs}

設計對話方塊與用來編輯和設定內容的對話方塊非常類似，但提供介面供作者設定及提供該元件的設計詳細資料。

[設計對話框在設計模式中可用](/help/sites-authoring/default-components-designmode.md)，但並非所有元件(例如 **標題** 和 **影像** 都有設計對話，但 **文字** 不會。

段落系統的設計對話框（例如parsys）是特殊情況，因為它允許用戶選擇特定的其他元件（從元件瀏覽器或sidekick）。

### 將元件添加到段落系統 {#adding-your-component-to-the-paragraph-system}

定義元件後，必須將其提供使用。 要使元件可用於段落系統，可以執行以下任一操作：

1. 開啟 [設計模式](/help/sites-authoring/default-components-designmode.md) ，並啟用必要的元件。
1. 將所需元件新增至 `components` 範本定義的屬性：

   `/etc/designs/<*yourProject*>/jcr:content/<*yourTemplate*>/par`

   例如，請參閱：

   `/etc/designs/geometrixx/jcr:content/contentpage/par`

   ![chlimage_1-245](assets/chlimage_1-245.png)

### 元件及其建立的內容 {#components-and-the-content-they-create}

如果我們建立並設定 **標題** 元件： `<content-path>/Prototype.html`

* 觸控式UI

   ![chlimage_1-246](assets/chlimage_1-246.png)

* 傳統 UI

   ![screen_shot_2012-02-01at34257pm](assets/screen_shot_2012-02-01at34257pm.png)

接著，我們便可查看在存放庫內建立的內容結構：

![screen_shot_2012-02-13at61405pm](assets/screen_shot_2012-02-13at61405pm.png)

尤其是，如果您查看 **標題**:

* 定義（適用於兩個UI）皆具有屬性 `name`= `./jcr:title`

   * `/libs/foundation/components/title/cq:dialog/content/items/column/items/title`
   * `/libs/foundation/components/title/dialog/items/title`

* 內容內會產生屬性 `jcr:title` 保存作者的內容。

定義的屬性取決於個別定義。 儘管它們可能比高一些，但它們仍遵循著同樣的基本原則。

## 元件階層和繼承 {#component-hierarchy-and-inheritance}

AEM內的元件受3個不同階層的規範：

* **資源類型層次結構**

   這可用來使用屬性擴充元件 `sling:resourceSuperType`. 這可讓元件繼承。 例如，文本元件將繼承標準元件中的各種屬性。

   * 指令碼（由Sling解析）
   * 對話
   * 說明（包括縮圖影像、圖示等）

* **容器階層**

   這可用來將組態設定填入子元件，且最常用於parsys案例。

   例如，可以在父元件上定義編輯欄按鈕、控制集佈局（編輯欄、變換）、對話框佈局（內聯、浮動）的配置設定，並傳播到子元件。

   配置設定（與編輯功能相關），位於 `cq:editConfig` 和 `cq:childEditConfig` 都會傳播。

* **包含階層**

   這是在執行階段以包含的順序強加。

   此層次結構由設計人員使用，而設計人員又是渲染的各個設計方面的基礎；包括版面資訊、css資訊、parsys中的可用元件等。

## 編輯行為 {#edit-behavior}

本節說明如何設定元件的編輯行為。 這包括可用於元件的動作、就地編輯器的特性以及與元件上的事件相關的監聽器等屬性。

觸控式和傳統UI都會使用此設定，雖然有某些特定差異。

元件的編輯行為是透過新增 `cq:editConfig` 類型節點 `cq:EditConfig` 元件節點下(類型 `cq:Component`)和新增特定屬性和子節點。 下列屬性和子節點可用：

* [ `cq:editConfig` 節點屬性](#configuring-with-cq-editconfig-properties):

   * `cq:actions` ( `String array`):定義可在元件上執行的動作。
   * `cq:layout` ( `String`)::會定義在傳統UI中編輯元件的方式。
   * `cq:dialogMode` ( `String`):定義傳統UI中開啟元件對話方塊的方式

      * 在觸控式UI中，對話方塊一律會在案頭模式中浮動，並在行動裝置中以全螢幕自動開啟。
   * `cq:emptyText` ( `String`):會定義沒有視覺內容時顯示的文字。
   * `cq:inherit` ( `Boolean`):定義是否從它繼承的元件繼承缺少的值。
   * `dialogLayout` （字串）:定義對話方塊的開啟方式。


* [ `cq:editConfig` 子節點](#configuring-with-cq-editconfig-child-nodes):

   * `cq:dropTargets` （節點類型） `nt:unstructured`):定義可接受內容尋找器資產中刪除的刪除目標的清單

      * 傳統UI中僅提供多個放置目標。
      * 在觸控式UI中，允許使用單一放置目標。
   * `cq:actionConfigs` （節點類型） `nt:unstructured`):會定義附加至cq:actions清單的新動作清單。
   * `cq:formParameters` （節點類型） `nt:unstructured`):會定義新增至對話方塊表單的其他參數。
   * `cq:inplaceEditing` （節點類型） `cq:InplaceEditingConfig`):定義元件的就地編輯設定。
   * `cq:listeners` （節點類型） `cq:EditListenersConfig`):定義元件上發生動作之前或之後所發生的動作。


>[!NOTE]
>
>在本頁中，節點（屬性和子節點）以XML表示，如以下示例所示。

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit]"
    cq:dialogMode="floating"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig">
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afteredit="REFRESH_PAGE"/>
</jcr:root>
```

存放庫中有許多現有設定。 您可以輕鬆搜索特定屬性或子節點：

* 若要尋找 `cq:editConfig` 節點，例如 `cq:actions`，您可以在 **CRXDE Lite** 和使用以下XPath查詢字串進行搜索：

   `//element(cq:editConfig, cq:EditConfig)[@cq:actions]`

* 查找的子節點 `cq:editConfig`，例如，您可以搜尋 `cq:dropTargets`，其類型 `cq:DropTargetConfig`;您可以在**CRXDE Lite**中使用查詢工具，並使用下列XPath查詢字串進行搜索：

   `//element(cq:dropTargets, cq:DropTargetConfig)`

### 元件預留位置 {#component-placeholders}

元件必須一律呈現作者可看見的某些HTML，即使元件沒有內容亦然。 否則，它可能會從編輯器的介面中以視覺化方式消失，從技術上而言，它會呈現在頁面上，但在編輯器中則隱藏。 在這種情況下，作者將無法選取空白元件並與其互動。

因此，只要元件在頁面編輯器中轉譯頁面時(當WCM模式為 `edit` 或 `preview`)。
預留位置的典型HTML標籤如下：

```HTML
<div class="cq-placeholder" data-emptytext="Component Name"></div>
```

轉譯上述預留位置HTML的典型HTL指令碼如下：

```HTML
<div class="cq-placeholder" data-emptytext="${component.properties.jcr:title}"
     data-sly-test="${(wcmmode.edit || wcmmode.preview) && isEmpty}"></div>
```

在上一個範例中， `isEmpty` 為true的變數，唯有元件沒有內容，且作者無法看見。

為避免重複，Adobe建議元件實作者為這些預留位置使用HTL範本， [就像核心元件所提供的一樣。](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/commons/v1/templates.html)

接著，您就可使用下列HTL行，在上一個連結中使用範本：

```HTML
<sly data-sly-use.template="core/wcm/components/commons/v1/templates.html"
     data-sly-call="${template.placeholder @ isEmpty=!model.text}"></sly>
```

在上一個範例中， `model.text` 是變數，只有在內容有且可見時，才會設為true。

您可以在核心元件中查看此範本的使用範例， [例如標題元件中。](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/title/v2/title/title.html#L27)

### 使用cq:EditConfig屬性進行設定 {#configuring-with-cq-editconfig-properties}

### cq:actions {#cq-actions}

此 `cq:actions` 屬性( `String array`)會定義一或多個可在元件上執行的動作。 下列值可用於設定：

<table>
 <tbody>
  <tr>
   <td><strong>屬性值</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td><code>text:&lt;some text&gt;</code></td>
   <td>顯示靜態文本值 &lt;some text=""&gt;<br /> 僅顯示在傳統UI中。 觸控式UI不會在內容功能表中顯示動作，因此不適用。</td>
  </tr>
  <tr>
   <td>-</td>
   <td>添加間隔器。<br /> 僅顯示在傳統UI中。 觸控式UI不會在內容功能表中顯示動作，因此不適用。</td>
  </tr>
  <tr>
   <td><code>edit</code></td>
   <td>新增按鈕以編輯元件。</td>
  </tr>
      <tr>
    <td><code>editannotate</code></td>
    <td>新增按鈕以編輯元件，並允許 <a href="/help/sites-authoring/annotations.md">註解</a>.</td>
   </tr>
  <tr>
   <td><code>delete</code></td>
   <td>新增按鈕以刪除元件</td>
  </tr>
  <tr>
   <td><code>insert</code></td>
   <td>新增按鈕，以在目前元件之前插入新元件</td>
  </tr>
  <tr>
   <td><code>copymove</code></td>
   <td>新增按鈕以複製和剪下元件。</td>
  </tr>
 </tbody>
</table>

以下配置將編輯按鈕、間隔器、刪除和插入按鈕添加到元件編輯欄：

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit,-,delete,insert]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig"/>
```

以下配置將「從Base Framework繼承的配置」文本添加到元件編輯欄：

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[text:Inherited Configurations from Base Framework]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig"/>
```

### cq:layout（僅限傳統UI） {#cq-layout-classic-ui-only}

此 `cq:layout` 屬性( `String`)會定義在傳統UI中編輯元件的方式。 可使用下列值：

<table>
 <tbody>
  <tr>
   <td><strong>屬性值</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td><code>rollover</code></td>
   <td>預設值。 元件版本可透過點按和/或內容功能表「滑鼠停留」來存取。<br /> 若需進階使用，請注意對應的用戶端物件為： <code>CQ.wcm.EditRollover</code>.</td>
  </tr>
  <tr>
   <td><code>editbar</code></td>
   <td>可透過工具列存取元件版本。<br /> 若需進階使用，請注意對應的用戶端物件為： <code>CQ.wcm.EditBar</code>.</td>
  </tr>
  <tr>
   <td><code>auto</code></td>
   <td>選項由用戶端代碼決定。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>滑鼠指向圖和編輯列的概念不適用於觸控式UI。

下列設定會將編輯按鈕新增至元件編輯列：

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig">
</jcr:root>
```

### cq:dialogMode（僅限傳統UI） {#cq-dialogmode-classic-ui-only}

元件可連結至編輯對話方塊。 此 `cq:dialogMode` 屬性( `String`)會定義傳統UI中開啟元件對話方塊的方式。 可使用下列值：

<table>
 <tbody>
  <tr>
   <td><strong>屬性值</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td><code>floating</code></td>
   <td>對話框浮動。<br /> </td>
  </tr>
  <tr>
   <td><code>inline</code></td>
   <td>(預設值). 對話方塊會錨定在元件上。<br /> </td>
  </tr>
  <tr>
   <td><code>auto</code></td>
   <td>如果元件寬度小於用戶端 <code>CQ.themes.wcm.EditBase.INLINE_MINIMUM_WIDTH</code> 值，則對話方塊為浮動，否則為內嵌。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>在觸控式UI中，對話方塊一律會在案頭模式中浮動，並在行動裝置中以全螢幕自動開啟。

下列設定會使用編輯按鈕定義編輯列和浮動對話方塊：

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit]"
    cq:dialogMode="floating"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig">
</jcr:root>
```

### cq:emptyText {#cq-emptytext}

此 `cq:emptyText` 屬性( `String`)會定義當沒有視覺內容時顯示的文字。 預設值為： `Drag components or assets here`.

### cq:inherit {#cq-inherit}

此 `cq:inherit` 屬性( `boolean`)定義是否從其繼承的元件繼承缺少的值。 預設為 `false`.

### dialogLayout {#dialoglayout}

此 `dialogLayout` 屬性會定義預設應如何開啟對話方塊。

* 值 `fullscreen` 以全螢幕開啟對話方塊。
* 預設值為空或缺少屬性時，會正常開啟對話方塊。
* 請注意，使用者一律可在對話方塊內切換全螢幕模式。
* 不適用於傳統UI。

### 使用cq:EditConfig子節點進行配置 {#configuring-with-cq-editconfig-child-nodes}

### cq:dropTargets {#cq-droptargets}

此 `cq:dropTargets` 節點（節點類型） `nt:unstructured`)會定義一個下拉目標清單，這些下拉目標可以接受從內容尋找器拖曳的資產中的下拉。 它可作為類型節點的集合 `cq:DropTargetConfig`.

>[!NOTE]
>
>傳統UI中僅提供多個放置目標。
>
>在觸控式UI中，只會使用第一個目標。

類型的每個子節點 `cq:DropTargetConfig` 定義元件中的放置目標。 節點名稱很重要，因為必須在JSP中使用它，如下所示，生成分配給DOM元素的CSS類名稱，該元素是有效放置目標：

```
<drop target css class> = <drag and drop prefix> +
 <node name of the drop target in the edit configuration>
```

此 `<drag and drop prefix>` 由Java屬性定義：

`com.day.cq.wcm.api.components.DropTarget.CSS_CLASS_PREFIX`。

例如，在下載元件的JSP中，類名定義如下( `/libs/foundation/components/download/download.jsp`)，其中 `file` 是下載元件編輯配置中下載目標的節點名稱：

`String ddClassName = DropTarget.CSS_CLASS_PREFIX + "file";`

類型的節點 `cq:DropTargetConfig` 需要有下列屬性：

<table>
 <tbody>
  <tr>
   <td><strong>屬性名稱</strong></td>
   <td><strong>屬性值<br /> </strong></td>
  </tr>
  <tr>
   <td><code>accept</code></td>
   <td>套用至資產mime類型的Regex，以驗證是否允許刪除。</td>
  </tr>
  <tr>
   <td><code>groups</code></td>
   <td>放置目標組的陣列。 每個群組都必須符合內容尋找器擴充功能中定義並附加至資產的群組類型。</td>
  </tr>
  <tr>
   <td><code>propertyName</code></td>
   <td>有效刪除後將更新的屬性名稱。</td>
  </tr>
 </tbody>
</table>

下列設定是從「下載」元件進行。 它會從 `media` 要從內容尋找器拖放到元件中的群組。 拖放後，元件屬性 `fileReference` 正在更新：

```
    <cq:dropTargets jcr:primaryType="nt:unstructured">
        <file
            jcr:primaryType="cq:DropTargetConfig"
            accept="[.*]"
            groups="[media]"
            propertyName="./fileReference"/>
    </cq:dropTargets>
```

### cq:actionConfigs（僅限傳統UI） {#cq-actionconfigs-classic-ui-only}

此 `cq:actionConfigs` 節點（節點類型） `nt:unstructured`)會定義附加至所定義清單的新動作清單 `cq:actions` 屬性。 每個子節點 `cq:actionConfigs` 定義介面工具集以定義新動作。

下列範例設定會定義新按鈕（傳統UI會使用分隔符號）:

* 分隔符，由xtype定義 `tbseparator`;

   * 這僅供傳統UI使用。
   * 觸控式UI會忽略此定義，因為會忽略xtype（而分隔符號則不必要，因為觸控式UI中的動作工具列結構不同）。

* 按鈕的名稱為 **管理注釋** 運行處理程式函式 `CQ_collab_forum_openCollabAdmin()`.

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    cq:actions="[EDIT,COPYMOVE,DELETE,INSERT]"
    jcr:primaryType="cq:EditConfig">
    <cq:actionConfigs jcr:primaryType="nt:unstructured">
        <separator0
            jcr:primaryType="nt:unstructured"
            xtype="tbseparator"/>
        <manage
            jcr:primaryType="nt:unstructured"
            handler="function(){CQ_collab_forum_openCollabAdmin();}"
            text="Manage comments"/>
    </cq:actionConfigs>
</jcr:root>
```

>[!NOTE]
>
>請參閱 [新增動作至元件工具列](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) 做為觸控式UI的範例。

### cq:formParameters {#cq-formparameters}

此 `cq:formParameters` 節點（節點類型） `nt:unstructured`)會定義新增至對話方塊表單的其他參數。 每個屬性都對應至表單參數。

下列設定會新增參數，稱為 `name`，以值設定 `photos/primary` 到對話框表單：

```
    <cq:formParameters
        jcr:primaryType="nt:unstructured"
        name="photos/primary"/>
```

### cq:inplaceEditing {#cq-inplaceediting}

此 `cq:inplaceEditing` 節點（節點類型） `cq:InplaceEditingConfig`)會定義元件的就地編輯設定。 它可以有下列屬性：

<table>
 <tbody>
  <tr>
   <td><strong>屬性名稱</strong></td>
   <td><strong>屬性值<br /> </strong></td>
  </tr>
  <tr>
   <td><code>active</code></td>
   <td>(<code>boolean</code>)true ，啟用元件的就地編輯。</td>
  </tr>
  <tr>
   <td><code>configPath</code></td>
   <td>(<code>String</code>)編輯器設定的路徑。 配置可由配置節點指定。</td>
  </tr>
  <tr>
   <td><code>editorType</code></td>
   <td><p>(<code>String</code>)編輯器類型。 可用類型包括：</p>
    <ul>
     <li>明文：用於非HTML內容。<br /> </li>
     <li>標題：是增強的純文字編輯器，可在開始編輯前將圖形標題轉換為純文字。 供Geometrixx標題元件使用。<br /> </li>
     <li>文字：用於HTML內容（使用RTF編輯器）。<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

下列設定可啟用元件的就地編輯，並定義 `plaintext` 作為編輯器類型：

```
    <cq:inplaceEditing
        jcr:primaryType="cq:InplaceEditingConfig"
        active="{Boolean}true"
        editorType="plaintext"/>
```

### cq:listeners {#cq-listeners}

此 `cq:listeners` 節點（節點類型） `cq:EditListenersConfig`)會定義元件上的動作之前或之後會發生什麼事。 下表定義了其可能的屬性。

<table>
 <tbody>
  <tr>
   <td><strong>屬性名稱</strong></td>
   <td><strong>屬性值<br /> </strong></td>
   <td><p><strong>預設值</strong></p> <p>（僅限傳統UI）</p> </td>
  </tr>
  <tr>
   <td><code>beforedelete</code></td>
   <td>處理常式會在元件移除前觸發。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforeedit</code></td>
   <td>在編輯元件之前會觸發處理常式。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforecopy</code></td>
   <td>處理常式會在複製元件之前觸發。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforemove</code></td>
   <td>處理常式會在元件移動前觸發。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforeinsert</code></td>
   <td>處理常式會在插入元件之前觸發。<br /> 僅適用於觸控式UI。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforechildinsert</code></td>
   <td>處理常式會在元件插入至其他元件（僅限容器）之前觸發。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>afterdelete</code></td>
   <td>移除元件後，就會觸發處理常式。</td>
   <td><code>REFRESH_SELF</code></td>
  </tr>
  <tr>
   <td><code>afteredit</code></td>
   <td>編輯元件後，就會觸發處理常式。</td>
   <td><code>REFRESH_SELF</code></td>
  </tr>
  <tr>
   <td><code>aftercopy</code></td>
   <td>在複製元件後會觸發處理常式。</td>
   <td><code>REFRESH_SELF</code></td>
  </tr>
  <tr>
   <td><code>afterinsert</code></td>
   <td>插入元件後會觸發處理常式。</td>
   <td><code>REFRESH_INSERTED</code></td>
  </tr>
  <tr>
   <td><code>aftermove</code></td>
   <td>移動元件後會觸發處理常式。</td>
   <td><code>REFRESH_SELFMOVED</code></td>
  </tr>
  <tr>
   <td><code>afterchildinsert</code></td>
   <td>將元件插入另一個元件（僅限容器）後，就會觸發處理常式。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>此 `REFRESH_INSERTED` 和 `REFRESH_SELFMOVED` 處理常式僅在傳統UI中可用。

>[!NOTE]
>
>僅在傳統UI中設定偵聽器的預設值。

>[!NOTE]
>
>若是巢狀元件，對定義為上屬性的動作會有某些限制 `cq:listeners` 節點：
>
>* 對於嵌套元件，以下屬性的值 *必須* be `REFRESH_PAGE`:>
>  * `aftermove`
>  * `aftercopy`


事件處理常式可透過自訂實作來實作。 例如(其中 `project.customerAction` 是靜態方法):

`afteredit = "project.customerAction"`

下列範例等同於 `REFRESH_INSERTED` 配置：

`afterinsert="function(path, definition) { this.refreshCreated(path, definition); }"`

>[!NOTE]
>
>對於傳統UI，若要查看哪些參數可用於處理常式，請參閱 `before<action>` 和 `after<action>` 事件區段 [ `CQ.wcm.EditBar`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditBar) 和 [ `CQ.wcm.EditRollover`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.wcm.EditRollover) 介面工具集檔案。

使用下列配置時，在元件被刪除、編輯、插入或移動後刷新頁面：

```
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="REFRESH_PAGE"
        afteredit="REFRESH_PAGE"
        afterinsert="REFRESH_PAGE"
        afterMove="REFRESH_PAGE"/>
```
