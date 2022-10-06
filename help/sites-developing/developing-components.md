---
title: 開發AEM元件
seo-title: Developing AEM Components
description: AEM元件可用來保留、格式化及轉譯可在您的網頁上使用的內容。
seo-description: AEM components are used to hold, format, and render the content made available on your webpages.
uuid: 1f39daa6-7277-45a2-adcc-74b58c93b8e4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 8cdb6db4-adaa-4eda-af7d-310a0b44b80b
docset: aem65
legacypath: /content/docs/en/aem/6-2/develop/components/components-touch-optimized
exl-id: 573cdc36-e9c3-4803-9c4e-cebd0cf0a56f
source-git-commit: f2a208acfa28f23cbf63d055c5d28698df476892
workflow-type: tm+mt
source-wordcount: '3485'
ht-degree: 1%

---

# 開發AEM元件{#developing-aem-components}

AEM元件可用來保留、格式化及轉譯可在您的網頁上使用的內容。

* 當 [編寫頁面](/help/sites-authoring/default-components.md)，元件可讓作者編輯和設定內容。

   * 建構 [商務](/help/commerce/cif-classic/administering/ecommerce.md) 例如，在站點上，元件可以從目錄收集和呈現資訊。
請參閱 [開發電子商務](/help/commerce/cif-classic/developing/ecommerce.md) 以取得更多資訊。

   * 建構 [社群](/help/communities/author-communities.md) 網站元件可提供資訊給訪客，並從訪客收集資訊。
請參閱 [開發社區](/help/communities/communities.md) 以取得更多資訊。

* 在發佈例項中，元件會呈現您的內容，並依您的網站訪客需求呈現。

>[!NOTE]
>
>本頁是文檔的繼續 [AEM元件 — 基本概念](/help/sites-developing/components-basics.md).

>[!CAUTION]
>
>以下元件 `/libs/cq/gui/components/authoring/dialog` 意在僅用於編輯器（製作中的元件對話方塊）。 如果在其他地方使用（例如在精靈對話方塊中），則可能不會如預期般運作。

## 程式碼範例 {#code-samples}

本頁提供開發AEM新元件所需的參考檔案（或參考檔案的連結）。 請參閱 [開發AEM元件 — 程式碼範例](/help/sites-developing/developing-components-samples.md) 一些實例。

## 結構 {#structure}

頁面會說明元件的基本結構 [AEM元件 — 基本概念](/help/sites-developing/components-basics.md#structure). 該檔案涵蓋觸控式和傳統UI。 即使您不需要在新元件中使用傳統設定，在繼承現有元件時仍可注意這些設定。

## 擴展現有元件和對話框 {#extending-existing-components-and-dialogs}

視您要實作的元件而定，可擴充或自訂現有例項，而非定義和開發整個例項 [結構](#structure) 白手起家。

在擴展或定制現有元件或對話框時，可以在進行更改之前複製或複製對話框所需的整個結構或結構。

### 擴充現有元件 {#extending-an-existing-component}

可以利用 [資源類型層次結構](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance) 以及相關的繼承機制。

>[!NOTE]
>
>元件也可以基於搜索路徑邏輯用覆蓋重新定義。 然而，在此情況下， [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) 不會觸發，且 `/apps` 必須定義整個覆蓋。

>[!NOTE]
>
>此 [內容片段元件](/help/sites-developing/customizing-content-fragments.md) 也可自訂和延伸，不過必須考慮完整結構和與Assets的關係。

### 自訂現有元件對話方塊 {#customizing-a-existing-component-dialog}

您也可以覆寫 *元件對話方塊* 使用 [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) 和定義屬性 `sling:resourceSuperType`.

這表示您只需重新定義所需的差異，而不是重新定義整個對話框(使用 `sling:resourceSuperType`)。 現在建議使用此方法來擴充元件對話方塊

請參閱 [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) 以取得更多詳細資訊。

## 定義標注 {#defining-the-markup}

元件將以呈現 [HTML](https://www.w3schools.com/htmL/html_intro.asp). 您的元件需要定義取得必要內容所需的HTML，然後在製作和發佈環境中視需要呈現。

### 使用HTML範本語言 {#using-the-html-template-language}

此 [HTML範本語言(HTL)](https://docs.adobe.com/content/help/zh-Hant/experience-manager-htl/using/overview.html)，隨AEM 6.0推出，取代JSP(JavaServer Pages)，成為偏好和建議的伺服器端HTML範本系統。 對於需要建立強大企業網站的網頁開發人員，HTL有助於提升安全性和開發效率。

>[!NOTE]
>
>雖然HTL和JSP都可用來開發元件，但我們將在本頁以HTL來說明開發，因為這是AEM的建議指令碼語言。

## 開發內容邏輯 {#developing-the-content-logic}

此可選邏輯選擇和/或計算要呈現的內容。 系統會從具有適當Use-API模式的HTL運算式中叫用它。

將邏輯與外觀分開的機制有助於釐清對指定檢視的呼叫。 它也允許對相同資源的不同檢視提供不同的邏輯。

### 使用Java {#using-java}

[HTL Java Use-API可讓HTL檔案存取自訂Java類別中的Helper方法](https://helpx.adobe.com/experience-manager/htl/using/use-api-java.html). 這可讓您使用Java程式碼來實作邏輯，以選取和設定元件內容。

### 使用JavaScript {#using-javascript}

[HTL JavaScript Use-API可讓HTL檔案存取以JavaScript撰寫的協助程式碼](https://helpx.adobe.com/experience-manager/htl/using/use-api-javascript.html). 這可讓您使用JavaScript程式碼來實作邏輯，以選取和設定元件內容。

### 使用用戶端HTML程式庫 {#using-client-side-html-libraries}

現代網站嚴重依賴由複雜JavaScript和CSS程式碼驅動的用戶端處理。 組織並最佳化此程式碼的服務可能是個複雜的問題。

為協助處理此問題，AEM提供 **用戶端程式庫資料夾**，可讓您將用戶端代碼儲存在存放庫中、將其組織為類別，並定義將每類代碼提供給用戶端的時間和方式。 然後，用戶端程式庫系統會負責在您的最終網頁中產生正確的連結，以載入正確的程式碼。

閱讀 [使用用戶端HTML程式庫](/help/sites-developing/clientlibs.md) 以取得更多資訊。

## 設定編輯行為 {#configuring-the-edit-behavior}

您可以配置元件的編輯行為，包括可用於元件的操作、就地編輯器的特性以及與元件上的事件相關的監聽器等屬性。 觸控式和傳統UI都會使用此設定，雖然有某些特定差異。

此 [配置元件的編輯行為](/help/sites-developing/components-basics.md#edit-behavior) 新增 `cq:editConfig` 類型節點 `cq:EditConfig` 元件節點下(類型 `cq:Component`)和新增特定屬性和子節點。

## 設定預覽行為 {#configuring-the-preview-behavior}

此 [WCM模式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) 在切換為 **預覽** 模式，即使未重新整理頁面亦然。

對於呈現時對WCM模式敏感的元件，必須定義元件以明確重新整理元件，然後仰賴Cookie的值。

>[!NOTE]
>
>在觸控式UI中，只有值 `EDIT` 和 `PREVIEW` 用於 [WCM模式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) cookie。

## 建立和設定對話方塊 {#creating-and-configuring-a-dialog}

對話方塊可讓作者與元件互動。 使用對話方塊可讓作者和/或管理員編輯內容、設定元件或定義設計參數(使用 [設計對話方塊](#creating-and-configuring-a-design-dialog))

### Coral UI和Granite UI {#coral-ui-and-granite-ui}

[Coral UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) 和 [Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) 定義AEM的現代外觀和風格。

[Granite UI提供大量基本元件(Widget)](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) 需要在製作環境中建立對話方塊。 如有必要，您可以擴充此選取範圍，並 [建立自己的介面工具集](#creatinganewwidget).

如需完整詳細資訊，請參閱：

* Coral UI

   * 在所有雲端解決方案中提供一致的UI
   * [AEM觸控式UI的概念 — Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Coral UI 指南](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html)

* Granite UI

   * 提供包裝在Sling元件中的Coral UI標籤，以建立UI主控台和對話方塊
   * [AEM觸控式UI的概念 — Granite UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Granite UI檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)

>[!NOTE]
>
>由於Granite UI元件的性質（以及ExtJS Widget的差異），元件與觸控式UI的互動方式與 [傳統UI](/help/sites-developing/developing-components-classic.md).

### 建立新對話方塊 {#creating-a-new-dialog}

觸控式UI的對話方塊：

* 已命名 `cq:dialog`.
* 定義為 `nt:unstructured` 節點 `sling:resourceType` 屬性集。

* 位於 `cq:Component` 節點，且位於其元件定義旁。
* 會根據其內容結構和 `sling:resourceType` 屬性。
* 使用Granite UI架構。
* 包含描述對話框中欄位的節點結構。

   * 這些節點 `nt:unstructured` 和必要 `sling:resourceType` 屬性。

範例節點結構可能是：

```xml
newComponent (cq:Component)
  cq:dialog (nt:unstructured)
    content
      layout
      items
        column
          items
            file
            description
```

自訂對話方塊類似於開發元件，因為對話方塊本身是元件（亦即元件指令碼呈現的標籤與用戶端程式庫提供的行為/樣式）。

如需範例，請參閱：

* `/libs/foundation/components/text/cq:dialog`
* `/libs/foundation/components/download/cq:dialog`

>[!NOTE]
>
>如果元件未為觸控式UI定義對話方塊，則傳統UI對話方塊會作為相容層內的後援。 若要自訂此類對話方塊，您需要自訂傳統UI對話方塊。 請參閱 [AEM元件（適用於傳統UI）](/help/sites-developing/developing-components-classic.md).

### 自訂對話方塊欄位 {#customizing-dialog-fields}

>[!NOTE]
>
>請參閱：
>
>* AEM Gem課程於 [自訂對話方塊欄位](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html).
>* 下列相關范常式式碼 [程式碼範例 — 如何自訂對話方塊欄位](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields).
>


#### 建立新欄位 {#creating-a-new-field}

觸控式UI的Widget會實作為Granite UI元件。

若要建立新介面工具集以用於觸控式UI的元件對話方塊中，您必須 [建立新的Granite UI欄位元件](/help/sites-developing/granite-ui-component.md).

>[!NOTE]
>
>如需Granite UI的完整詳細資訊，請參閱 [Granite UI檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).

如果您將對話方塊視為表單元素的簡單容器，則您也可以將對話方塊內容的主要內容視為表單欄位。 建立新表單欄位需要建立資源類型；這等同於建立新元件。 為協助您完成該工作，Granite UI提供要繼承的通用欄位元件(使用 `sling:resourceSuperType`):

`/libs/granite/ui/components/coral/foundation/form/field`

更具體來說，Granite UI提供一系列欄位元件，適合用於對話方塊(或更一般地，在 [表單](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html))。

>[!NOTE]
>
>這與傳統UI不同，傳統UI以代表介面工具集 `cq:Widgets` 節點，每個節點具有特定 `xtype` 建立與其對應ExtJS介面工具集的關係。 從實作角度來看，這些Widget是由ExtJS架構在用戶端轉譯。

建立資源類型後，您可以使用屬性在對話方塊中新增節點，以實例化欄位 `sling:resourceType` 指您剛引進的資源類型。

#### 建立樣式和行為的用戶端程式庫 {#creating-a-client-library-for-style-and-behavior}

如果您想要定義元件的樣式和行為，可以建立專用的 [用戶庫](/help/sites-developing/clientlibs.md) 來定義自訂CSS/LESS和JS。

若要讓用戶端程式庫僅為元件對話方塊載入（即不會為其他元件載入），您需要設定屬性 `extraClientlibs`** **對話方塊的類別名稱，以及您剛建立的用戶端程式庫。 如果您的用戶端程式庫相當大，且/或您的欄位是該對話方塊專屬的，且在其他對話方塊中不需要，則建議您這麼做。

若要讓所有對話方塊都載入您的用戶端程式庫，請將用戶端程式庫的類別屬性設為 `cq.authoring.dialog`. 這是呈現所有對話框時預設包含的客戶端庫的類別名稱。 如果客戶端庫很小，且/或欄位是通用欄位，並且可在其他對話框中重複使用，則要執行此操作。

如需範例，請參閱：

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * 由提供 [程式碼範例](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### 延伸（繼承）欄位 {#extending-inheriting-from-a-field}

視您的需求而定，您可以：

* 依元件繼承( `sling:resourceSuperType`)
* 遵循介面工具集API（JS/CSS繼承），從基礎介面工具集程式庫擴充指定介面工具集（若是Granite UI，即為Coral UI）

#### 對對話框欄位的訪問 {#access-to-dialog-fields}

您也可以使用演算條件( `rendercondition`)來控制誰有權存取對話方塊中的特定索引標籤/欄位；例如：

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### 處理欄位事件 {#handling-field-events}

現在已使用完成在對話方塊欄位上處理事件的方法 [自定義客戶端庫中的偵聽器](#listeners-in-a-custom-client-library). 這是舊方法的改變 [內容結構中的聽眾](#listenersinthecontentstructureclassicui).

#### 自定義客戶端庫中的偵聽器 {#listeners-in-a-custom-client-library}

若要將邏輯插入欄位，您應：

1. 將欄位標示為指定的CSS類別( *鈎*)。
1. 在您的用戶端資料庫中，定義與該CSS類別名稱掛鈎的JS接聽程式（這可確保您的自訂邏輯只限於欄位，不會影響相同類型的其他欄位）。

若要達成此目標，您必須了解您要與之互動的基礎Widget程式庫。 請參閱 [Coral UI檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) 以識別您要對哪個事件做出反應。 這與您過去必須使用ExtJS執行的程式非常類似：尋找指定介面工具集的檔案頁面，然後查看其事件API的詳細資訊。

如需範例，請參閱：

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * 由提供 [程式碼範例](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### 內容結構中的監聽器 {#listeners-in-the-content-structure}

在具有ExtJS的傳統UI中，通常會在內容結構中擁有指定Widget的聽眾。 在觸控式UI中達到相同的效果，與內容中不再定義JS接聽程式程式碼（或任何程式碼）不同。

內容結構描述了語義結構；它不應（必須）暗示基礎小工具的性質。 內容結構中沒有JS程式碼，即可變更實作詳細資料，而無須變更內容結構。 換言之，您無需接觸內容結構即可變更介面工具集資料庫。

#### 檢測對話框的可用性 {#dialog-ready}

如果您有自訂JavaScript，只需在對話方塊可用且準備就緒時執行，則應監聽 `dialog-ready` 事件。

每當對話方塊載入（或重新載入）且可供使用時，就會觸發此事件，這表示每當對話方塊的DOM中有變更（建立/更新）時。

`dialog-ready` 可用來在JavaScript自訂程式碼中連結，該程式碼會對對話方塊或類似工作中的欄位執行自訂。

### 欄位驗證 {#field-validation}

#### 必填欄位 {#mandatory-field}

若要將指定欄位標示為必要欄位，請在欄位的內容節點上設定下列屬性：

* 名稱: `required`
* 類型: `Boolean`

如需範例，請參閱：

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title
```

#### 欄位驗證(Granite UI) {#field-validation-granite-ui}

Granite UI和Granite UI元件（等同於Widget）中的欄位驗證是使用 `foundation-validation` API。 [請參閱 `foundation-valdiation` Granite檔案以取得詳細資訊。](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

如需範例，請參閱：

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * 由提供 [程式碼範例](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## 建立和設定設計對話方塊 {#creating-and-configuring-a-design-dialog}

元件具有可在 [設計模式](/help/sites-authoring/default-components-designmode.md).

定義與 [用於編輯內容的對話框](#creating-a-new-dialog)，其差異在於定義為節點：

* 節點名稱： `cq:design_dialog`
* 類型: `nt:unstructured`

## 建立和設定就地編輯器 {#creating-and-configuring-an-inplace-editor}

就地編輯器允許用戶直接編輯段落流中的內容，而無需開啟對話框。 例如，標準的「文字」和「標題」元件都有內置編輯器。

對於每個元件類型，就地編輯器並非必要/有意義的。

請參閱 [延伸頁面編寫 — 新增Inplace編輯器](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor) 以取得更多資訊。

## 自訂元件工具列 {#customizing-the-component-toolbar}

此 [元件工具列](/help/sites-developing/touch-ui-structure.md#component-toolbar) 為使用者提供元件一系列動作的存取權，例如編輯、設定、複製和刪除。

請參閱 [延伸頁面編寫 — 將新動作新增至元件工具列](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) 以取得更多資訊。

## 為參考邊欄配置元件（借/借） {#configuring-a-component-for-the-references-rail-borrowed-lent}

如果您的新元件會參照其他頁面的內容，則您可以考慮是否要影響 **借用內容** 和 **借出內容** 區段 [**參考**](/help/sites-authoring/basic-handling.md#references) 欄。

現成可用的AEM只會檢查「參考」元件。 若要新增元件，您需要設定OSGi套件組合 **WCM製作內容參考設定**.

在定義中建立新條目，指定元件以及要檢查的屬性。 例如：

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>使用AEM時，有數種方法可管理這類服務的組態設定。 請參閱 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以取得詳細資訊和建議的實務。

## 啟用元件並將其添加到段落系統 {#enabling-and-adding-your-component-to-the-paragraph-system}

開發元件後，必須啟用該元件以在適當的段落系統中使用，以便在所需的頁面上使用。

這可透過下列任一方式完成：

* 使用 [設計模式](/help/sites-authoring/default-components-designmode.md) 編輯特定頁面時。
* [定義 `components` 模板段落系統上的財產](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system).

## 配置段落系統以便拖動資產可建立元件實例 {#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

AEM提供在頁面上設定段落系統的可能性，以便 [當使用者將（適當）資產拖曳至該頁面的例項上時，系統會自動建立新元件的例項](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui) （而非一律將空白元件拖曳至頁面）。

此行為和所需的資產對元件關係可以設定：

1. 在頁面設計的段落定義下。 例如：

   * `/etc/designs/<myApp>/page/par`

   建立新節點：

   * 名稱: `cq:authoring`
   * 類型: `nt:unstructured`


1. 在此下，建立新節點以保留所有資產對元件的對應：

   * 名稱: `assetToComponentMapping`
   * 類型: `nt:unstructured`

1. 對於每個資產對元件對應，請建立節點：

   * 名稱：文字；建議名稱指明資產及相關元件類型；例如，影像
   * 類型: `nt:unstructured`

   每個都具有下列屬性：

   * `assetGroup`:

      * 類型: `String`
      * 值：資產所屬之本集團；例如， `media`
   * `assetMimetype`:

      * 類型: `String`
      * 值：相關資產的mime類型；例如 `image/*`
   * `droptarget`:

      * 類型: `String`
      * 值：投放目標；例如， `image`
   * `resourceType`:

      * 類型: `String`
      * 值：相關元件資源；例如， `foundation/components/image`
   * `type`:

      * 類型: `String`
      * 值：例如， `Images`






如需範例，請參閱：

* `/etc/designs/geometrixx/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-outdoors/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-media/jcr:content/article/article-content-par/cq:authoring`

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-project-archetype專案](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/archive/master.zip)

>[!NOTE]
>
>現在，使用時，可在UI中輕鬆設定元件例項的自動建立 [核心元件](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html) 和可編輯的範本。 請參閱 [建立頁面範本](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) 有關定義與指定介質類型自動關聯的元件的詳細資訊。

## 使用AEM Brackets擴充功能 {#using-the-aem-brackets-extension}

此 [AEM Brackets擴充功能](/help/sites-developing/aem-brackets.md) 提供順暢的工作流程，可編輯AEM元件和用戶端程式庫。 其基礎為 [方括弧](https://brackets.io/) 代碼編輯器。

擴充功能：

* 簡化同步（無需Maven或File Vault），以幫助提高開發人員的效率，並幫助具有有限AEM知識的前端開發人員參與項目。
* 提供部分 [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) 支援，此範本語言旨在簡化元件開發並提高安全性。

>[!NOTE]
>
>建議使用括弧來建立元件。 這會取代專為傳統UI所設計的CRXDE Lite — 建立元件功能。

## 從傳統元件移轉 {#migrating-from-a-classic-component}

將專為搭配傳統UI使用而設計的元件移轉至可搭配觸控式UI使用的元件（單獨或共同使用）時，應考量下列問題：

* HTL

   * 使用 [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) 並非強制性，但如果您的元件需要更新，則是考慮的理想時機 [從JSP移轉至HTL](/help/sites-developing/components-basics.md#htl-vs-jsp).

* 元件

   * 移轉 [ `cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code) 使用傳統UI特定功能的程式碼
   * RTE外掛程式，如需詳細資訊，請參閱 [設定RTF編輯器](/help/sites-administering/rich-text-editor.md).
   * [移轉 `cq:listener` 代碼](#migrating-cq-listener-code) 使用傳統UI專屬函式的

* 對話方塊

   * 您必須建立新對話方塊，才能在觸控式UI中使用。 不過，為了相容性目的，當未為觸控式UI定義對話方塊時，觸控式UI可使用傳統UI對話方塊的定義。
   * 此 [AEM現代化工具](/help/sites-developing/modernization-tools.md) 可協助您擴充現有元件。
   * [將ExtJS對應至Granite UI元件](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components) 提供ExtJS xtype和節點類型的相同Granite UI資源類型的便利概述。
   * 自訂欄位，如需詳細資訊，請參閱AEM Gems課程，內容如下： [自訂對話方塊欄位](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html).
   * 從vtype移轉至 [Granite UI驗證](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * 使用JS監聽器，如需詳細資訊，請參閱 [處理欄位事件](#handling-field-events) 和AEM Gem課程 [自訂對話方塊欄位](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html).

### 移轉cq:listener程式碼 {#migrating-cq-listener-code}

如果您要移轉專為傳統UI設計的專案，則 `cq:listener` 程式碼（以及元件相關的clientlibs）可能會使用傳統UI專屬的函式(例如 `CQ.wcm.*`)。 在移轉作業中，您必須使用觸控式UI中的對等物件/函式來更新此類程式碼。

如果您的專案正完全移轉至觸控式UI，則您需要取代此類程式碼，以使用與觸控式UI相關的物件和函式。

不過，如果您的專案在移轉期間（通常的情況）必須同時適用傳統UI和觸控式UI，則您需要實作切換器，以區分參考適當物件的個別程式碼。

此切換機制可實作為：

```
if (Granite.author) {
    // touch UI
} else {
    // classic UI
}
```

## 記錄元件 {#documenting-your-component}

身為開發人員，您需要輕鬆存取元件檔案，以便快速了解：

* 說明
* 預期用途
* 內容結構和屬性
* 公開的API和擴充功能點
* 等

因此，很容易就能在元件本身內使用任何現有的檔案標籤。

你只需把 `README.md` 檔案。 此標籤下拉式清單會顯示在 [元件主控台](/help/sites-authoring/default-components-console.md).

![chlimage_1-7](assets/chlimage_1-7.png)

支援的Markdown與 [內容片段](/help/assets/content-fragments/content-fragments-markdown.md).
