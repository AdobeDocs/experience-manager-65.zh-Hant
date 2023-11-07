---
title: Adobe Experience Manager元件 — 基本需知
description: 當您開始開發新元件時，您需要瞭解其結構和設定的基本知識。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
legacypath: /content/docs/en/aem/6-0/develop/components/components-develop
exl-id: 7ff92872-697c-4e66-b654-15314a8cb429
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '4907'
ht-degree: 1%

---

# Adobe Experience Manager (AEM)元件 — 基本需知{#aem-components-the-basics}

當您開始開發新元件時，您需要瞭解其結構和設定的基本知識。

此程式涉及閱讀理論，以及檢視標準AEM例項中廣泛的元件實作。 雖然現在的AEM已改用新的標準、現代化、觸控式UI，但仍可繼續支援傳統UI，因此這種方法稍微複雜一些。

## 概觀 {#overview}

本節說明開發您自己的元件時，所需詳細資訊的主要概念和問題。

### 規劃 {#planning}

開始實際設定元件或為元件編寫程式碼之前，您應該先詢問：

* 您到底需要新元件做什麼？
   * 清晰的規格有助於所有開發、測試和交接階段。 詳細資訊可能會隨著時間而改變，但規格可以更新（不過變更也應記錄在案）。
* 您是否需要從頭開始建立元件，或可從現有元件繼承基本知識？
   * 不需要重新發明輪子。
   * AEM提供幾種機制，可讓您從另一個元件定義繼承和擴充詳細資訊，包括覆寫、覆蓋和 [Sling資源合併](/help/sites-developing/sling-resource-merger.md).
* 您的元件需要邏輯才能選取或操作內容嗎？
   * 邏輯應與使用者介面層分開。 HTL的設計目的是協助確保做到這一點。
* 您的元件是否需要CSS格式？
   * CSS格式應與元件定義分開。 定義命名HTML元素的慣例，以便您可以透過外部CSS檔案來修改它們。
* 我應考慮哪些安全性方面？
   * 另請參閱 [安全性檢查清單 — 開發最佳實務](/help/sites-administering/security-checklist.md#development-best-practices) 以取得更多詳細資料。

### 觸控式與傳統UI {#touch-enabled-vs-classic-ui}

在有關開發元件的任何嚴肅討論開始之前，您必須知道您的作者正在使用哪種UI：

* **觸控式UI**
  [標準使用者介面](/help/sites-developing/touch-ui-concepts.md) 是根據Adobe Experience Cloud的統一使用者體驗，使用下列基礎技術 [Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui) 和 [Granite UI](/help/sites-developing/touch-ui-concepts.md#granite-ui).
* **傳統UI**
以AEM 6.4已淘汰的ExtJS技術為基礎的使用者介面。

另請參閱 [適用於客戶的UI介面Recommendations](/help/sites-deploying/ui-recommendations.md) 以取得更多詳細資料。

可以實作元件以支援觸控式UI和/或傳統UI。 檢視標準執行個體時，您也會看到原本針對傳統UI或觸控式UI （或兩者）設計的現成元件。

本頁會說明兩者的基本知識，以及如何識別它們。

>[!NOTE]
>
>Adobe建議您使用觸控式UI，以受益於最新技術。 [AEM現代化工具](modernization-tools.md) 可讓移轉更輕鬆。

### 內容邏輯和轉譯標籤  {#content-logic-and-rendering-markup}

Adobe建議將負責標籤和轉譯的程式碼，與控制用來選取元件內容的邏輯的程式碼分開。

支援此理念的有 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)，特意限制以確保使用真正的程式語言來定義基礎商業邏輯的範本化語言。 此（選用）邏輯會使用特定命令從HTL叫用。 此機制會醒目顯示呼叫特定檢視的程式碼，並在必要時允許同一元件的不同檢視使用特定邏輯。

### HTL與JSP {#htl-vs-jsp}

HTL是AEM 6.0引進的HTML範本語言。

關於是否使用的討論 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) 或JSP (Java™ Server Pages)在開發自己的元件時應該要簡單明瞭，因為HTL現在是針對AEM的建議指令碼語言。

HTL和JSP都可用來開發傳統和觸控式UI的元件。 雖然我們可能會傾向於假設HTL僅適用於觸控式UI和適用於傳統UI的JSP，但這只是誤解，而且更受時機的影響。 觸控式UI和HTL大約在同一期間併入AEM。 由於HTL現在是建議的語言，因此它被用於新元件，而新元件傾向於用於觸控式UI。

>[!NOTE]
>
>Granite UI Foundation表單欄位除外（在對話方塊中使用）。 這些仍需要使用JSP。

### 開發自己的元件 {#developing-your-own-components}

若要為適當的UI建立您自己的元件，請參閱（閱讀本頁面後）：

* [觸控式UI的AEM元件](/help/sites-developing/developing-components.md)
* [傳統UI的AEM元件](/help/sites-developing/developing-components-classic.md)

快速入門方法是複製現有元件，然後進行您想要的變更。 若要瞭解如何建立自己的元件並將其新增至段落系統，請參閱：

* [開發元件](/help/sites-developing/developing-components-samples.md) （著重於觸控式UI）

### 將元件移動至發佈例項 {#moving-components-to-the-publish-instance}

呈現內容的元件必須部署在與內容相同的AEM執行個體上。 因此，在製作執行個體上用於製作和轉譯頁面的所有元件，都必須部署在發佈執行個體上。 部署時，元件可用於轉譯已啟動的頁面。

使用下列工具將您的元件移至發佈執行個體：

* [使用封裝管理員](/help/sites-administering/package-manager.md) 將您的元件新增至套件，並將它們移至另一個AEM執行個體。
* [使用啟動樹狀結構複製工具](/help/sites-authoring/publishing-pages.md#manage-publication) 以複製元件。

>[!NOTE]
>
>這些機制也可用於在其他執行個體之間傳輸元件，例如，從您的開發到您的測試執行個體。

### 從開始要注意的元件 {#components-to-be-aware-of-from-the-start}

* Page:

   * AEM具有 *頁面* 元件( `cq:Page`)。
   * 這是對內容管理很重要的特定資源型別。
      * 頁面對應至包含您網站內容的網頁。

* 段落系統：

   * 段落系統是網站的重要部分，因為它管理著段落清單。 它可用來儲存和建構儲存實際內容的個別元件。
   * 您可以在段落系統中建立、移動、複製和刪除段落。
   * 您也可以選取可在特定段落系統中使用的元件。
   * 在標準例項中有各種可用的段落系統(例如， `parsys`， ` [responsivegrid](/help/sites-authoring/responsive-layout.md)`)。

## 結構 {#structure}

AEM元件的結構既強大又靈活，主要考量事項為：

* 資源類型
* 元件定義
* 元件的屬性和子節點
* 對話方塊
* 設計對話方塊
* 元件可用性
* 元件及其建立的內容

### 資源類型 {#resource-type}

結構的一個關鍵元素是資源型別。

* 內容結構會宣告意圖。
* 資源型別會實作它們。

這是一項抽象，可協助確保即使表觀和感覺隨著時間而改變，意圖仍會維持在時間上。

### 元件定義 {#component-definition}

#### 元件基本知識 {#component-basics}

元件的定義可劃分如下：

* AEM元件是根據 [Sling](https://sling.apache.org/documentation.html).
* AEM元件（通常）位於以下位置：

   * HTL: `/libs/wcm/foundation/components`
   * JSP： `/libs/foundation/components`

* 專案/網站特定元件（通常）位於下列位置：

   * `/apps/<myApp>/components`

* AEM標準元件的定義為 `cq:Component` 並具備關鍵元素：

   * jcr屬性：

     jcr屬性清單；這些是變數，有些可能是選用的，但元件節點的基本結構、其屬性和子節點由定義。 `cq:Component` 定義

   * 資源:

     這些會定義元件使用的靜態元素。

   * 指令碼:

  用於實作元件之結果例項的行為。

* **根節點**：

   * `<mycomponent> (cq:Component)`  — 元件的階層節點。

* **重要屬性**：

   * `jcr:title`  — 元件標題；例如，當元件列在元件瀏覽器或Sidekick中時作為標籤使用。
   * `jcr:description`  — 元件的說明；可在元件瀏覽器或Sidekick中作為滑鼠懸停提示使用。
   * 傳統 UI:

      * `icon.png`  — 此元件的圖示。
      * `thumbnail.png`  — 如果此元件列在段落系統中，則顯示影像。

   * 觸控式 UI

      * 請參閱區段 [觸控式UI中的元件圖示](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) 以取得詳細資訊。

* **重要子節點**：

   * `cq:editConfig (cq:EditConfig)`  — 定義元件的編輯屬性，並讓元件出現在元件瀏覽器或Sidekick中。

     注意：如果元件有對話方塊，即使cq：editConfig不存在，它也會自動出現在「元件」瀏覽器或Sidekick中。

   * `cq:childEditConfig (cq:EditConfig)`  — 控制未定義其本身的子元件的作者UI方面 `cq:editConfig`.
   * 觸控式UI：

      * `cq:dialog` ( `nt:unstructured`) — 此元件的對話方塊。 定義允許使用者設定元件及/或編輯內容的介面。
      * `cq:design_dialog` ( `nt:unstructured`) — 此元件的設計編輯

   * 傳統 UI:

      * `dialog` ( `cq:Dialog`) — 此元件的對話方塊。 定義可讓使用者設定元件、編輯內容或兩者的介面。
      * `design_dialog` ( `cq:Dialog`) — 為此元件設計編輯。

#### 觸控式UI中的元件圖示 {#component-icon-in-touch-ui}

元件的圖示或縮寫可在開發人員建立元件時，透過元件的JCR屬性來定義。 系統會依下列順序評估這些屬性，並使用找到的第一個有效屬性。

1. `cq:icon`  — 字串屬性，指向 [Coral UI程式庫](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/Coral.Icon.html) 以在元件瀏覽器中顯示
   * 使用Coral圖示的HTML屬性值。
1. `abbreviation`  — 字串屬性，用於自訂元件瀏覽器中元件名稱的縮寫
   * 縮寫應限製為兩個字元。
   * 提供空白字串會建置縮寫，由的前兩個字元組成 `jcr:title` 屬性。
      * 例如，「Image」的「Im」
      * 使用當地語系化的標題來建置縮寫。
   * 只有元件具備以下條件時，才會轉譯縮寫： `abbreviation_commentI18n` 屬性，然後用作翻譯提示。
1. `cq:icon.png` 或 `cq:icon.svg`  — 此元件的圖示，會顯示在元件瀏覽器中
   * 20 x 20畫素是標準元件的圖示大小。
      * 較大的圖示會縮小（使用者端）。
   * 建議的色彩為rgb(112， 112， 112) > #707070
   * 標準元件圖示的背景是透明的。
   * 僅限 `.png` 和 `.svg` 支援檔案。
   * 如果透過Eclipse外掛程式從檔案系統匯入，檔案名稱必須逸出 `_cq_icon.png` 或 `_cq_icon.svg` 例如。
   * `.png` 先決條件優先 `.svg` 如果兩者都存在

如果以上屬性均非( `cq:icon`， `abbreviation`， `cq:icon.png`，或 `cq:icon.svg`)，可以在元件上找到：

* 系統會在超級元件上搜尋下列專案後的相同屬性 `sling:resourceSuperType` 屬性。
* 如果在超級元件層級找不到任何專案或空白縮寫，系統會從 `jcr:title` 目前元件的屬性。

若要取消從超級元件繼承圖示，請將設定為空白 `abbreviation` 元件上的屬性會回覆為預設行為。

此 [元件主控台](/help/sites-authoring/default-components-console.md#component-details) 顯示特定元件圖示的定義方式。

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

定義元件所需的許多節點/屬性對這兩個UI都是通用的，差異保持獨立，以便您的元件可以在兩個環境中運作。

元件是型別的節點 `cq:Component` 和有下列屬性和子節點：

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
   <td>目前元件. 元件屬於節點型別 <code>cq:Component</code>.<br /> </td>
  </tr>
  <tr>
   <td><code>componentGroup</code></td>
   <td><code>String</code></td>
   <td>可在元件瀏覽器（觸控式UI）或Sidekick （傳統UI）中選取元件的群組。<br /> 值 <code>.hidden</code> 用於無法從UI選取的元件，例如實際段落系統。</td>
  </tr>
  <tr>
   <td><code>cq:isContainer</code></td>
   <td><code>Boolean</code></td>
   <td>指出元件是否為容器元件，因此可包含其他元件，例如段落系統。</td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>cq:dialog</code></td>
   <td><code>nt:unstructured</code><br /> </td>
   <td>觸控式UI的編輯對話方塊定義。</td>
  </tr>
  <tr>
   <td><code>dialog</code></td>
   <td><code>cq:Dialog</code></td>
   <td>傳統UI之編輯對話方塊的定義。</td>
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
   <td>當元件沒有對話方塊節點時，涵蓋此案例的對話方塊路徑。<br /> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>cq:cellName</code></td>
   <td><code>String</code></td>
   <td>如果設定，此屬性會視為儲存格ID。 如需詳細資訊，請參閱知識庫文章 <a href="https://helpx.adobe.com/experience-manager/kb/DesigneCellId.html">如何建立設計儲存格ID</a>.<br /> </td>
  </tr>
  <tr>
   <td><code>cq:childEditConfig</code></td>
   <td><code>cq:EditConfig</code></td>
   <td>當元件是容器（例如段落系統）時，它會驅動子節點的編輯組態。<br /> </td>
  </tr>
  <tr>
   <td><code>cq:editConfig</code></td>
   <td><code>cq:EditConfig</code></td>
   <td><a href="#edit-behavior">編輯元件的設定</a>.<br /> </td>
  </tr>
  <tr>
   <td><code>cq:htmlTag</code></td>
   <td><code>nt:unstructured </code></td>
   <td>傳回新增至周圍html標籤的其他標籤屬性。 啟用向自動產生的div新增屬性。</td>
  </tr>
  <tr>
   <td><code>cq:noDecoration</code></td>
   <td><code>Boolean</code></td>
   <td>如果為true，則元件不會使用自動產生的div和css類別轉譯。<br /> </td>
  </tr>
  <tr>
   <td><code>cq:template</code></td>
   <td><code>nt:unstructured</code></td>
   <td>如果找到，從元件瀏覽器或Sidekick新增元件時，此節點會作為內容範本使用。</td>
  </tr>
  <tr>
   <td><code>cq:templatePath</code></td>
   <td><code>String</code></td>
   <td>從元件瀏覽器或Sidekick新增元件時，作為內容範本使用的節點路徑。 這必須是絕對路徑，不是相對於元件節點的路徑。<br /> 除非您想要重複使用其他地方已提供的內容，否則這並非必要操作， <code>cq:template</code> 足夠（請參閱下文）。</td>
  </tr>
  <tr>
   <td><code>jcr:created</code></td>
   <td><code>Date</code></td>
   <td>建立元件的日期。<br /> </td>
  </tr>
  <tr>
   <td><code>jcr:description</code></td>
   <td><code>String</code></td>
   <td>元件的說明。<br /> </td>
  </tr>
  <tr>
   <td><code>jcr:title</code></td>
   <td><code>String</code></td>
   <td>元件的標題。<br /> </td>
  </tr>
  <tr>
   <td><code>sling:resourceSuperType</code></td>
   <td><code>String</code></td>
   <td>設定後，元件會繼承自此元件。<br /> </td>
  </tr>
  <tr>
   <td><code>virtual</code></td>
   <td><code>sling:Folder</code></td>
   <td>啟用建立虛擬元件。 若要檢視範例，請檢視下列位置的接觸元件：<br /> <code>/libs/foundation/components/profile/form/contact</code></td>
  </tr>
  <tr>
   <td><code>&lt;breadcrumb.jsp&gt;</code></td>
   <td><code>nt:file</code><br /> </td>
   <td>指令碼檔案。<br /> </td>
  </tr>
  <tr>
   <td><code>icon.png</code></td>
   <td><code>nt:file</code></td>
   <td>元件的圖示，會出現在Sidekick中的標題旁。<br /> </td>
  </tr>
  <tr>
   <td><code>thumbnail.png</code></td>
   <td><code>nt:file</code></td>
   <td>將元件從Sidekick拖曳至適當位置時顯示的可選縮圖。<br /> </td>
  </tr>
 </tbody>
</table>

如果您檢視 **文字** 元件（任一版本），您會看到下列元素：

* HTL ( `/libs/wcm/foundation/components/text`)

  ![chlimage_1-241](assets/chlimage_1-241.png)

* JSP ( `/libs/foundation/components/text`)

  ![screen_shot_2012-02-13at60457pm](assets/screen_shot_2012-02-13at60457pm.png)

特別感興趣的屬性包括：

* `jcr:title`  — 元件的標題；這可用來識別元件，例如元件出現在元件瀏覽器或sidekick內的元件清單中
* `jcr:description`  — 元件的說明；可用作sidekick內元件清單中的滑鼠懸停提示
* `sling:resourceSuperType`：這表示擴充元件時的繼承路徑（透過覆寫定義）

特別感興趣的子節點包括：

* `cq:editConfig` ( `cq:EditConfig`) — 這可控制視覺方面；例如，可定義長條圖或Widget的外觀，或可新增自訂控制項
* `cq:childEditConfig` ( `cq:EditConfig`) — 這控制沒有自己的定義的子元件的視覺方面
* 觸控式UI：
   * `cq:dialog` ( `nt:unstructured`) — 定義用於編輯此元件內容的對話方塊
   * `cq:design_dialog` ( `nt:unstructured`) — 指定此元件的設計編輯選項
* 傳統 UI:
   * `dialog` ( `cq:Dialog`) — 定義用於編輯此元件內容的對話方塊（專用於傳統UI）
   * `design_dialog` ( `cq:Dialog`) — 指定此元件的設計編輯選項
   * `icon.png`  — 圖形檔案，用作Sidekick中元件的圖示
   * `thumbnail.png`  — 從Sidekick拖曳元件時，做為元件縮圖的圖形檔案

### 對話方塊 {#dialogs}

對話方塊是元件的關鍵元素，因為它們提供介面給作者來設定並提供該元件的輸入。

根據元件的複雜性，您的對話方塊可能需要一個或多個標籤 — 保持對話方塊簡短並對輸入欄位排序。

對話方塊定義是UI專屬的：

>[!NOTE]
>
>* 為相容性目的，當尚未定義觸控式UI的對話方塊時，觸控式UI可以使用傳統UI對話方塊的定義。
>* 此 [AEM現代化工具](/help/sites-developing/modernization-tools.md) 此外，也提供協助您擴充/轉換只有為傳統UI定義對話方塊的元件。
>

* 觸控式UI
   * `cq:dialog` ( `nt:unstructured`)節點：
      * 定義用於編輯此元件內容的對話方塊
      * 觸控式UI專用
      * 是使用Granite UI元件定義的
      * 具有屬性 `sling:resourceType`，作為標準Sling內容結構
      * 可以有屬性 `helpPath` 定義在「說明」圖示(「說明」(Help)圖示 `?` 圖示)已選取。
         * 對於現成可用的元件，這通常會參考檔案中的頁面。
         * 若否 `helpPath` 會指定預設的URL （檔案概觀頁面）。

  ![chlimage_1-242](assets/chlimage_1-242.png)

  在對話方塊中，會定義個別欄位：

  ![screen_shot_2012-02-13at60937pm](assets/screen_shot_2012-02-13at60937pm.png)

* 傳統 UI
   * `dialog` ( `cq:Dialog`)節點
      * 定義用於編輯此元件內容的對話方塊
      * 傳統UI專用
      * 使用ExtJS Widget定義
      * 具有屬性 `xtype`，指ExtJS
      * 可以有屬性 `helpPath` 定義在下列情況下存取的上下文相關說明資源（絕對或相對路徑） **說明** 按鈕已選取。
         * 對於現成可用的元件，這通常會參考檔案中的頁面。
         * 若否 `helpPath` 會指定預設的URL （檔案概觀頁面）。

  ![chlimage_1-243](assets/chlimage_1-243.png)

  在對話方塊中，會定義個別欄位：

  ![chlimage_1-244](assets/chlimage_1-244.png)

  在傳統對話方塊中：

   * 您可以建立對話方塊為 `cq:Dialog`，這會提供單一標籤 — 如文字元件所示，或是如果您需要多個標籤（如文字文字元件一樣），則可將此對話方塊定義為 `cq:TabPanel`.
   * a `cq:WidgetCollection` ( `items`)作為輸入欄位( `cq:Widget`)或其他索引標籤( `cq:Widget`)。 此階層可以延伸。

### 設計對話方塊 {#design-dialogs}

「設計」對話方塊類似於編輯和設定內容時所用的對話方塊，但它們為作者提供介面來設定並提供該元件的設計詳細資訊。

[設計對話方塊在設計模式下可用](/help/sites-authoring/default-components-designmode.md)，但並非所有元件都需要，例如， **標題** 和 **影像** 兩者都有設計對話方塊，但 **文字** 不會。

段落系統的「設計」(design)對話方塊（例如parsys）是特殊情況，因為它允許使用者在頁面上選取特定的其他元件（從元件瀏覽器或sidekick）。

### 將元件新增至段落系統 {#adding-your-component-to-the-paragraph-system}

定義元件後，必須使其可供使用。 若要讓元件可用於段落系統，您可以：

1. 開啟 [設計模式](/help/sites-authoring/default-components-designmode.md) 並啟用必要元件。
1. 將所需元件新增至 `components` 範本定義的屬性，位於：

   `/etc/designs/<*yourProject*>/jcr:content/<*yourTemplate*>/par`

   如需範例，請參閱:

   `/etc/designs/geometrixx/jcr:content/contentpage/par`

   ![chlimage_1-245](assets/chlimage_1-245.png)

### 元件及其建立的內容 {#components-and-the-content-they-create}

如果您建立並設定的執行個體 **標題** 頁面上的元件： `<content-path>/Prototype.html`

* 觸控式UI

  ![chlimage_1-246](assets/chlimage_1-246.png)

* 傳統 UI

  ![screen_shot_2012-02-01at34257pm](assets/screen_shot_2012-02-01at34257pm.png)

然後您可以檢視在存放庫中建立的內容結構：

![screen_shot_2012-02-13at61405pm](assets/screen_shot_2012-02-13at61405pm.png)

特別是，如果您檢視實際文字 **標題**：

* 定義（適用於兩個UI）具有屬性 `name`= `./jcr:title`

   * `/libs/foundation/components/title/cq:dialog/content/items/column/items/title`
   * `/libs/foundation/components/title/dialog/items/title`

* 在內容內，這會產生屬性 `jcr:title` 儲存作者的內容。

定義的屬性取決於個別定義。 雖然這些規則可能比上述更複雜，但仍遵循相同的基本原則。

## 元件階層與繼承 {#component-hierarchy-and-inheritance}

AEM中的元件受到三個不同階層的限制：

* **資源型別階層**

  這是用來使用屬性擴充元件 `sling:resourceSuperType`. 這可讓元件繼承。 例如，文字元件會繼承標準元件的各種屬性。

   * 指令碼（由Sling解析）
   * 對話方塊
   * 說明（包括縮圖影像和圖示）

* **容器階層**

  這可用來將組態設定填入至子元件，且最常用於Parsys案例。

  例如，可以在父元件上定義編輯列按鈕、控制項集配置（編輯列、滑鼠指向效果）、對話方塊配置（內嵌、浮動）的組態設定，並傳播到子元件。

  中的組態設定（與編輯功能相關） `cq:editConfig` 和 `cq:childEditConfig` 都會傳播。

* **包含階層**

  這是在執行階段由include的順序強制執行。

  設計人員會使用此階層，進而做為各種呈現設計層面的基礎，包括版面配置資訊、css資訊、parsys中的可用元件等等。

## 編輯行為 {#edit-behavior}

本節說明如何設定元件的編輯行為。 這包括元件可用的動作、就地編輯器的特性，以及與元件事件相關的接聽程式等屬性。

此設定對觸控式與傳統UI而言都是通用的，不過會有某些特定差異。

元件的編輯行為可透過新增 `cq:editConfig` 型別節點 `cq:EditConfig` 在元件節點（型別）下方 `cq:Component`)，並新增特定屬性和子節點。 下列屬性和子節點可供使用：

* [`cq:editConfig` 節點屬性](#configuring-with-cq-editconfig-properties)：

   * `cq:actions` ( `String array`)：定義可對元件執行的動作。
   * `cq:layout` ( `String`)：定義在傳統UI中編輯元件的方式。
   * `cq:dialogMode` ( `String`)：定義在傳統UI中開啟元件對話方塊的方式

      * 在觸控式UI中，對話方塊在案頭模式中一律為浮動狀態，並在行動中自動開啟為全熒幕。

   * `cq:emptyText` ( `String`)：定義沒有視覺內容時顯示的文字。
   * `cq:inherit` ( `Boolean`)：定義缺少的值是否繼承自繼承的元件。
   * `dialogLayout` （字串）：定義對話方塊的開啟方式。

* [`cq:editConfig` 子節點](#configuring-with-cq-editconfig-child-nodes)：

   * `cq:dropTargets` (節點型別 `nt:unstructured`)：定義可以從內容尋找器的資產接受放置的放置目標清單

      * 只有在傳統UI中才能使用多個放置目標。
      * 觸控式UI中允許單一放置目標。

   * `cq:actionConfigs` (節點型別 `nt:unstructured`)：定義附加至cq：actions清單的新動作清單。
   * `cq:formParameters` (節點型別 `nt:unstructured`)：定義要新增至對話方塊表單的其他引數。
   * `cq:inplaceEditing` (節點型別 `cq:InplaceEditingConfig`)：定義元件的就地編輯設定。
   * `cq:listeners` (節點型別 `cq:EditListenersConfig`)：定義元件上發生動作之前或之後所發生的事件。

>[!NOTE]
>
>在此頁面中，節點（屬性和子節點）會以XML表示，如下列範例所示。

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

存放庫中有許多現有的設定。 您可以輕鬆搜尋特定屬性或子節點：

* 若要尋找 `cq:editConfig` 節點，例如， `cq:actions`，您還可以在以下位置使用查詢工具： **CRXDE Lite** 和搜尋下列XPath查詢字串：

  `//element(cq:editConfig, cq:EditConfig)[@cq:actions]`

* 若要尋找的子節點，請執行下列步驟： `cq:editConfig`例如，您可以搜尋 `cq:dropTargets`，屬於型別 `cq:DropTargetConfig`；您可以使用查詢工具，在**CRXDE Lite**中使用以下XPath查詢字串進行搜尋：

  `//element(cq:dropTargets, cq:DropTargetConfig)`

### 元件預留位置 {#component-placeholders}

元件必須一律呈現某些作者可見的HTML，即使元件沒有內容亦然。 否則，編輯器介面中可能會看不到它，使得它在技術上存在但不會顯示在頁面和編輯器中。 在這種情況下，作者將無法選取空白元件並與之互動。

因此，只要元件在頁面編輯器中轉譯頁面時(當WCM模式為 `edit` 或 `preview`)。
預留位置的一般HTML標示如下：

```HTML
<div class="cq-placeholder" data-emptytext="Component Name"></div>
```

轉譯上述預留位置HTML的典型HTL指令碼如下：

```HTML
<div class="cq-placeholder" data-emptytext="${component.properties.jcr:title}"
     data-sly-test="${(wcmmode.edit || wcmmode.preview) && isEmpty}"></div>
```

在上一個範例中， `isEmpty` 是一個變數，只有在元件沒有內容且作者看不到時才會成立。

為避免重複，Adobe建議元件的實作人員對這些預留位置使用HTL範本， [如核心元件所提供的那種。](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/commons/v1/templates.html)

接著，使用先前連結中的範本並使用下列HTL行：

```HTML
<sly data-sly-use.template="core/wcm/components/commons/v1/templates.html"
     data-sly-call="${template.placeholder @ isEmpty=!model.text}"></sly>
```

在上一個範例中， `model.text` 是變數，只有在內容具有內容且可見時才會成立。

此範本的範例使用可在核心元件中檢視， [例如，在標題元件中。](https://github.com/adobe/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/title/v2/title/title.html#L27)

### 使用cq：EditConfig屬性進行設定 {#configuring-with-cq-editconfig-properties}

### cq：actions {#cq-actions}

此 `cq:actions` 屬性( `String array`)會定義一或多個可在元件上執行的動作。 下列值可供設定：

<table>
 <tbody>
  <tr>
   <td><strong>屬性值</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td><code>text:&lt;some text&gt;</code></td>
   <td>顯示靜態文字值 &lt;some text=""&gt;<br /> 僅顯示在傳統UI中。 觸控式UI不會在內容功能表中顯示動作，因此這不適用。</td>
  </tr>
  <tr>
   <td>-</td>
   <td>新增分隔符號。<br /> 僅顯示在傳統UI中。 觸控式UI不會在內容功能表中顯示動作，因此這不適用。</td>
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
   <td>新增按鈕以刪除元件。</td>
  </tr>
  <tr>
   <td><code>insert</code></td>
   <td>新增按鈕以在目前元件之前插入新元件。</td>
  </tr>
  <tr>
   <td><code>copymove</code></td>
   <td>新增按鈕以複製和剪下元件。</td>
  </tr>
 </tbody>
</table>

下列設定會將編輯按鈕、分隔符號、刪除和插入按鈕新增至元件編輯列：

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit,-,delete,insert]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig"/>
```

下列設定會將「繼承自基礎框架的設定」文字新增至元件編輯列：

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[text:Inherited Configurations from Base Framework]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig"/>
```

### cq：layout （僅限傳統UI） {#cq-layout-classic-ui-only}

此 `cq:layout` 屬性( `String`)定義如何在傳統UI中編輯元件。 可使用下列值：

<table>
 <tbody>
  <tr>
   <td><strong>屬性值</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td><code>rollover</code></td>
   <td>預設值. 元件版本可透過點按和/或內容功能表「在滑鼠懸停上」存取。<br /> 若為進階使用，對應的使用者端物件為： <code>CQ.wcm.EditRollover</code>.</td>
  </tr>
  <tr>
   <td><code>editbar</code></td>
   <td>元件版本可透過工具列存取。<br /> 若為進階使用，對應的使用者端物件為： <code>CQ.wcm.EditBar</code>.</td>
  </tr>
  <tr>
   <td><code>auto</code></td>
   <td>選項會保留在使用者端程式碼中。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>滑鼠指向效果與編輯列的概念不適用於觸控式UI。

下列設定會將編輯按鈕新增至元件編輯列：

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit]"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig">
</jcr:root>
```

### cq：dialogMode （僅限傳統UI） {#cq-dialogmode-classic-ui-only}

元件可連結至編輯對話方塊。 此 `cq:dialogMode` 屬性( `String`)會定義在傳統UI中開啟元件對話方塊的方式。 可使用下列值：

<table>
 <tbody>
  <tr>
   <td><strong>屬性值</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td><code>floating</code></td>
   <td>對話方塊浮動。<br /> </td>
  </tr>
  <tr>
   <td><code>inline</code></td>
   <td>(預設值). 對話方塊錨定在元件上。<br /> </td>
  </tr>
  <tr>
   <td><code>auto</code></td>
   <td>如果元件寬度小於使用者端 <code>CQ.themes.wcm.EditBase.INLINE_MINIMUM_WIDTH</code> 值，則對話方塊為浮動，否則為內嵌。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>在觸控式UI中，對話方塊在案頭模式中一律為浮動狀態，並在行動裝置中自動開啟為全熒幕。

下列設定會定義具有編輯按鈕的編輯列，以及浮動對話方塊：

```
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:actions="[edit]"
    cq:dialogMode="floating"
    cq:layout="editbar"
    jcr:primaryType="cq:EditConfig">
</jcr:root>
```

### cq：emptyText {#cq-emptytext}

此 `cq:emptyText` 屬性( `String`)會定義沒有視覺內容時顯示的文字。 其預設值為： `Drag components or assets here`.

### cq：inherit {#cq-inherit}

此 `cq:inherit` 屬性( `boolean`)定義缺少的值是否繼承自其繼承的元件。 其預設值為 `false`.

### dialogLayout {#dialoglayout}

此 `dialogLayout` 屬性會定義預設開啟對話方塊的方式。

* 值 `fullscreen` 以全熒幕開啟對話方塊。
* 若為空值或屬性不存在，預設會正常開啟對話方塊。
* 使用者一律可以在對話方塊中切換全熒幕模式。
* 不適用於傳統UI。

### 使用cq：EditConfig子節點進行配置 {#configuring-with-cq-editconfig-child-nodes}

### cq：dropTargets {#cq-droptargets}

此 `cq:dropTargets` 節點（節點型別） `nt:unstructured`)定義可接受從內容尋找器拖曳之資產進行拖放作業的拖放目標清單。 它會當做型別節點的集合 `cq:DropTargetConfig`.

>[!NOTE]
>
>只有在傳統UI中才能使用多個放置目標。
>
>在觸控式UI中，只會使用第一個目標。

每個型別的子節點 `cq:DropTargetConfig` 會定義元件中的放置目標。 節點名稱非常重要，因為它必須用於JSP中，才能產生指派給有效放置目標DOM元素的CSS類別名稱，如下所示：

```
<drop target css class> = <drag and drop prefix> +
 <node name of the drop target in the edit configuration>
```

此 `<drag and drop prefix>` 由Java™屬性定義：

`com.day.cq.wcm.api.components.DropTarget.CSS_CLASS_PREFIX`。

例如，類別名稱的定義如下，在下載元件的JSP中( `/libs/foundation/components/download/download.jsp`)，其中 `file` 是下載元件編輯設定中的放置目標節點名稱：

`String ddClassName = DropTarget.CSS_CLASS_PREFIX + "file";`

型別的節點 `cq:DropTargetConfig` 必須具有以下屬性：

<table>
 <tbody>
  <tr>
   <td><strong>屬性名稱</strong></td>
   <td><strong>屬性值<br /> </strong></td>
  </tr>
  <tr>
   <td><code>accept</code></td>
   <td>套用至資產MIME型別的規則運算式，以驗證是否允許卸除。</td>
  </tr>
  <tr>
   <td><code>groups</code></td>
   <td>放置目標群組的陣列。 每個群組都必須符合內容尋找器擴充功能中定義且附加至資產的群組型別。</td>
  </tr>
  <tr>
   <td><code>propertyName</code></td>
   <td>有效放置後要更新的屬性名稱。</td>
  </tr>
 </tbody>
</table>

以下設定是從下載元件中取得。 這可啟用來自以下位置的任何資產（mime型別可以是任何字串）： `media` 從內容尋找器拖放至元件的群組。 放置後，元件屬性 `fileReference` 正在更新：

```
    <cq:dropTargets jcr:primaryType="nt:unstructured">
        <file
            jcr:primaryType="cq:DropTargetConfig"
            accept="[.*]"
            groups="[media]"
            propertyName="./fileReference"/>
    </cq:dropTargets>
```

### cq：actionConfigs （僅限傳統UI） {#cq-actionconfigs-classic-ui-only}

此 `cq:actionConfigs` 節點（節點型別） `nt:unstructured`)會定義新動作的清單，這些動作會附加至由所定義的清單。 `cq:actions` 屬性。 的每個子節點 `cq:actionConfigs` 會透過定義Widget來定義新動作。

以下設定範例會定義新按鈕（傳統UI會使用分隔符號）：

* 分隔符號，由xtype定義 `tbseparator`；

   * 這僅供傳統UI使用。
   * 觸控式UI會忽略此定義，因為會忽略xtype （而且由於動作工具列在觸控式UI中的建構方式不同，因此不需要使用分隔符號）。

* 名為的按鈕 **管理評論** 執行處理常式函式的處理常式 `CQ_collab_forum_openCollabAdmin()`.

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
>另請參閱 [將動作新增至元件工具列](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) 做為觸控式UI的範例。

### cq：formParameters {#cq-formparameters}

此 `cq:formParameters` 節點（節點型別） `nt:unstructured`)會定義新增至對話方塊表單的其他引數。 每個屬性都會對應至一個表單引數。

下列設定會新增引數，稱為 `name`，使用值設定 `photos/primary` 至對話方塊表單：

```
    <cq:formParameters
        jcr:primaryType="nt:unstructured"
        name="photos/primary"/>
```

### cq：inplaceEditing {#cq-inplaceediting}

此 `cq:inplaceEditing` 節點（節點型別） `cq:InplaceEditingConfig`)會為元件定義就地編輯設定。 它可以有以下屬性：

<table>
 <tbody>
  <tr>
   <td><strong>屬性名稱</strong></td>
   <td><strong>屬性值<br /> </strong></td>
  </tr>
  <tr>
   <td><code>active</code></td>
   <td>(<code>boolean</code>) True以啟用就地編輯元件。</td>
  </tr>
  <tr>
   <td><code>configPath</code></td>
   <td>(<code>String</code>)編輯器設定的路徑。 組態可由組態節點指定。</td>
  </tr>
  <tr>
   <td><code>editorType</code></td>
   <td><p>(<code>String</code>)編輯器型別。 可用的型別包括：</p>
    <ul>
     <li>純文字：用於非HTML內容。<br /> </li>
     <li>title：是一種增強型純文字編輯器，可在編輯開始前將圖形標題轉換為純文字。 由Geometrixx標題元件使用。<br /> </li>
     <li>文字：用於HTML內容（使用RTF編輯器）。<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

以下組態可讓您就地編輯元件並定義 `plaintext` 作為編輯器型別：

```
    <cq:inplaceEditing
        jcr:primaryType="cq:InplaceEditingConfig"
        active="{Boolean}true"
        editorType="plaintext"/>
```

### cq：listeners {#cq-listeners}

此 `cq:listeners` 節點（節點型別） `cq:EditListenersConfig`)會定義元件動作之前或之後所發生的事件。 下表定義其可能的屬性。

<table>
 <tbody>
  <tr>
   <td><strong>屬性名稱</strong></td>
   <td><strong>屬性值<br /> </strong></td>
   <td><p><strong>預設值</strong></p> <p>（僅限傳統UI）</p> </td>
  </tr>
  <tr>
   <td><code>beforedelete</code></td>
   <td>處理常式會在移除元件之前觸發。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforeedit</code></td>
   <td>處理常式會在編輯元件之前觸發。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforecopy</code></td>
   <td>處理常式會在複製元件之前觸發。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforemove</code></td>
   <td>處理常式會在移動元件之前觸發。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforeinsert</code></td>
   <td>處理常式會在插入元件之前觸發。<br /> 僅適用於觸控式UI。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>beforechildinsert</code></td>
   <td>處理常式會在元件插入另一個元件（僅限容器）之前觸發。</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>afterdelete</code></td>
   <td>處理常式會在移除元件後觸發。</td>
   <td><code>REFRESH_SELF</code></td>
  </tr>
  <tr>
   <td><code>afteredit</code></td>
   <td>處理常式會在編輯元件後觸發。</td>
   <td><code>REFRESH_SELF</code></td>
  </tr>
  <tr>
   <td><code>aftercopy</code></td>
   <td>處理常式會在元件複製後觸發。</td>
   <td><code>REFRESH_SELF</code></td>
  </tr>
  <tr>
   <td><code>afterinsert</code></td>
   <td>處理常式會在插入元件後觸發。</td>
   <td><code>REFRESH_INSERTED</code></td>
  </tr>
  <tr>
   <td><code>aftermove</code></td>
   <td>處理常式會在元件移動後觸發。</td>
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
>此 `REFRESH_INSERTED` 和 `REFRESH_SELFMOVED` 處理常式只能在傳統UI中使用。

>[!NOTE]
>
>監聽器的預設值僅在傳統UI中設定。

>[!NOTE]
>
>如果有巢狀元件，則定義為屬性之動作在某些方面會有限制 `cq:listeners` 節點：
>
>* 對於巢狀元件，下列屬性的值 *必須* 是 `REFRESH_PAGE`： >
>  * `aftermove`
>  * `aftercopy`

事件處理常式可使用自訂實施來實施。 例如，(其中 `project.customerAction` 是靜態方法)：

`afteredit = "project.customerAction"`

下列範例等同於 `REFRESH_INSERTED` 設定：

`afterinsert="function(path, definition) { this.refreshCreated(path, definition); }"`

>[!NOTE]
>
>若為傳統UI，若要檢視哪些引數可用於處理常式，請參閱 `before<action>` 和 `after<action>` 的事件區段 [`CQ.wcm.EditBar`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.EditBar) 和 [`CQ.wcm.EditRollover`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.wcm.EditRollover) Widget檔案。

使用下列設定時，頁面會在刪除、編輯、插入或移動元件後重新整理：

```
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="REFRESH_PAGE"
        afteredit="REFRESH_PAGE"
        afterinsert="REFRESH_PAGE"
        afterMove="REFRESH_PAGE"/>
```
