---
title: 開發AEM元件
seo-title: 開發AEM元件
description: AEM元件可用來封存、格式化和轉譯網頁上提供的內容。
seo-description: AEM元件可用來封存、格式化和轉譯網頁上提供的內容。
uuid: 1f39daa6-7277-45a2-adcc-74b58c93b8e4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 8cdb6db4-adaa-4eda-af7d-310a0b44b80b
docset: aem65
legacypath: /content/docs/en/aem/6-2/develop/components/components-touch-optimized
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 開發AEM元件{#developing-aem-components}

AEM元件可用來封存、格式化和轉譯網頁上提供的內容。

* 製作 [頁面時](/help/sites-authoring/default-components.md)，元件可讓作者編輯和設定內容。

   * 建構 [Commerce](/help/sites-administering/ecommerce.md) 網站時，元件可以收集並呈現目錄中的資訊。
如需詳 [細資訊，請參閱](/help/sites-developing/ecommerce.md) 「開發電子商務」。

   * 在建構 [Communities網站](/help/communities/author-communities.md) 時，元件可提供資訊給訪客並從訪客收集資訊。
如需詳 [細資訊](/help/communities/communities.md) ，請參閱開發社群。

* 在發佈例項中，元件會呈現您的內容，並依您的網站訪客要求呈現內容。

>[!NOTE]
>
>本頁是檔案 [AEM元件——基本功能的延續](/help/sites-developing/components-basics.md)。

>[!CAUTION]
>
>以下元 `/libs/cq/gui/components/authoring/dialog` 件僅用於編輯器（「編寫」中的元件對話框）。 如果在其他地方使用（例如在精靈對話方塊中），則可能不會如預期般運作。

## 程式碼範例 {#code-samples}

本頁提供開發AEM新元件所需的參考檔案（或參考檔案的連結）。 如需 [一些實用範例，請參閱「開發AEM元件——程式碼範例](/help/sites-developing/developing-components-samples.md) 」。

## 結構 {#structure}

元件的基本結構會在「 [AEM元件——基本功能」頁面中介紹](/help/sites-developing/components-basics.md#structure)。 該檔案同時涵蓋觸控式和傳統UI。 即使您不需要在新元件中使用傳統設定，在繼承現有元件時也可以注意這些設定。

## 擴展現有元件和對話框 {#extending-existing-components-and-dialogs}

視您要實作的元件而定，可能會延伸或自訂現有的例項，而不是從頭開始定義和開發整 [個結](#structure) 構。

在擴展或定制現有元件或對話框時，可以在進行更改之前複製或複製該對話框所需的整個結構或結構。

### 擴展現有元件 {#extending-an-existing-component}

使用資源類型層次和相關的繼承機 [制可以擴展現有元件](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance) 。

>[!NOTE]
>
>元件也可以根據搜尋路徑邏輯以覆蓋重新定義。 不過，在此情況下， [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) 將不會觸發， `/apps` 且必須定義整個覆蓋。

>[!NOTE]
>
>內容 [片段元件](/help/sites-developing/customizing-content-fragments.md) ，也可加以自訂和擴充，不過必須考慮完整的結構以及與資產的關係。

### 自定義現有元件對話框 {#customizing-a-existing-component-dialog}

您也可以使用 *Sling Resource Merger* ，並定義屬 [性來覆寫元件對話方塊](/help/sites-developing/sling-resource-merger.md)`sling:resourceSuperType`。

這表示您只需要重定義所需的差異，而不是重定義整個對話框(使用 `sling:resourceSuperType`)。 現在建議使用此方法來擴充元件對話方塊

如需詳細 [資訊，請參閱Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) 。

## 定義標籤 {#defining-the-markup}

您的元件將會以 [HTML呈現](https://www.w3schools.com/htmL/html_intro.asp)。 您的元件需要定義需要的HTML，以取得必要的內容，然後在作者和發佈環境中視需要呈現。

### 使用HTML範本語言 {#using-the-html-template-language}

The [HTML Templating Language (HTL)](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html), introduced with AEM 6.0, takes the place of JSP (JavaServer Pages) as the preferred and recommended server-side template system for HTML. 對於需要建立強穩企業網站的網頁開發人員，HTL有助於提高安全性和開發效率。

>[!NOTE]
>
>雖然HTL和JSP都可用來開發元件，但我們將在本頁上使用HTL來說明開發，因為它是AEM的建議指令碼語言。

## 開發內容邏輯 {#developing-the-content-logic}

此可選邏輯選擇和／或計算要渲染的內容。 它會從具有適當Use-API模式的HTL運算式中呼叫。

將邏輯與外觀分開的機制有助於澄清對給定視圖的調用。 它還允許對同一資源的不同視圖使用不同的邏輯。

### 使用Java {#using-java}

[HTL Java Use-API可讓HTL檔案存取自訂Java類別中的輔助方法](https://helpx.adobe.com/experience-manager/htl/using/use-api-java.html)。 這可讓您使用Java程式碼來實作邏輯，以選取和設定元件內容。

### 使用JavaScript {#using-javascript}

[HTL javaScript Use-API可讓HTL檔案存取以JavaScript編寫的協助程式碼](https://helpx.adobe.com/experience-manager/htl/using/use-api-javascript.html)。 這可讓您使用JavaScript程式碼來實作邏輯，以選取和設定元件內容。

### 使用用戶端HTML程式庫 {#using-client-side-html-libraries}

現代網站嚴重依賴由複雜JavaScript和CSS程式碼驅動的用戶端處理。 組織並最佳化此程式碼的服務可能是個複雜的問題。

為協助處理此問題，AEM提供「用戶端程式庫資料夾 ****」，可讓您將用戶端程式碼儲存在儲存庫中，將它組織為類別，並定義每種程式碼的服務時機和方式。 然後用戶端程式庫系統會負責在您的最終網頁中產生正確的連結，以載入正確的程式碼。

閱讀「 [使用用戶端HTML程式庫](/help/sites-developing/clientlibs.md) 」以取得詳細資訊。

## 設定編輯行為 {#configuring-the-edit-behavior}

您可以配置元件的編輯行為，包括元件可用的操作、就地編輯器的特性以及與元件上的事件相關的監聽器等屬性。 此設定是觸控式和傳統UI的常見設定，但有特定的差異。

組 [件的編輯行為是通過在元件節點下添加類型的節點(](/help/sites-developing/components-basics.md#edit-behavior) 類型)和添加特定屬性和子節點來 `cq:editConfig``cq:EditConfig``cq:Component`配置的。

## 設定預覽行為 {#configuring-the-preview-behavior}

切換 [至「預覽](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) 」模式時，即使未重新整理頁面，也會設定 **** WCM模式Cookie。

對於具有對WCM模式敏感的轉譯元件，需要定義這些元件，以明確重新整理它們，然後依賴Cookie的值。

>[!NOTE]
>
>在啟用觸控的UI中，只有值 `EDIT` 和 `PREVIEW` 用於 [WCM模式Cookie](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) 。

## 建立和配置對話框 {#creating-and-configuring-a-dialog}

對話方塊可讓作者與元件互動。 使用對話框可讓作者和／或管理員編輯內容、配置元件或定義設計參數(使用「設 [計」對話框](#creating-and-configuring-a-design-dialog))

### Coral UI與Granite UI {#coral-ui-and-granite-ui}

[Coral UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) 和 [Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) ，定義了AEM的現代外觀和感覺。

[Granite UI提供在製作環境上建立對話方塊所需的各種基本元件(widget)](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) 。 如有需要，您可以延伸此選取范 [圍並建立自己的介面工具集](#creatinganewwidget)。

有關使用Coral和Granite資源類型開發元件的詳細資訊，請參閱：使 [用Coral/Granite資源類型建立Experience Manager元件](https://helpx.adobe.com/experience-manager/using/aem64_coral_resourcetypes.html)。

如需完整詳細資訊，請參閱：

* Coral UI

   * 在所有雲端解決方案中提供一致的UI
   * [AEM Touch-Enabled UI - Coral UI的概念](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Coral UI指南](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html)

* Granite UI

   * 提供包裝在Sling元件中的Coral UI標籤，以建立UI主控台和對話方塊
   * [AEM Touch-Enabled UI - Granite UI的概念](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Granite UI檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)

>[!NOTE]
>
>由於Granite UI元件的性質（以及與ExtJS Widget的差異），元件與觸控式UI和傳統UI的互動方式有 [所差異](/help/sites-developing/developing-components-classic.md)。

### 建立新對話框 {#creating-a-new-dialog}

啟用觸控功能的UI對話方塊：

* 的下界 `cq:dialog`。
* 定義為具有 `nt:unstructured` 屬性集的 `sling:resourceType` 節點。

* 位於其節點 `cq:Component` 下方和其元件定義旁。
* 會根據其內容結構和屬性，在伺服器端（以Sling元件的形式）轉譯 `sling:resourceType` 。
* 使用Granite UI架構。
* 包含描述對話框中欄位的節點結構。

   * 這些節點 `nt:unstructured` 具有必需屬 `sling:resourceType` 性。

示例節點結構可能是：

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

自定義對話框類似於開發元件，因為對話框本身是元件（即元件指令碼呈現的標籤以及客戶端庫提供的行為／樣式）。

如需範例，請參閱：

* `/libs/foundation/components/text/cq:dialog`
* `/libs/foundation/components/download/cq:dialog`

>[!NOTE]
>
>如果元件沒有為觸控式UI定義對話方塊，則傳統UI對話方塊會當做相容層內的備援。 若要自訂此種對話方塊，您必須自訂傳統UI對話方塊。 請參 [閱Classic UI的AEM元件](/help/sites-developing/developing-components-classic.md)。

### 自訂對話方塊欄位 {#customizing-dialog-fields}

>[!NOTE]
>
>請參閱：
>
>* 「自訂對話方塊欄位」上的AEM [Gems工作階段](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html)。
>* 程式碼範例——如何自 [訂對話方塊欄位中涵蓋的相關范常式式碼](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)。
>



#### 建立新欄位 {#creating-a-new-field}

觸控式UI的介面工具集會實作為Granite UI元件。

若要建立新介面工具集，以便用於觸控式UI的元件對話方塊中，您必須 [建立新的Granite UI欄位元件](/help/sites-developing/granite-ui-component.md)。

>[!NOTE]
>
>如需Granite UI的完整詳細資訊，請參閱 [Granite UI檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)。

如果您將對話方塊視為表單元素的簡單容器，則您也可以將對話方塊內容的主要內容視為表單欄位。 建立新表單域需要建立資源類型；這相當於建立新元件。 為協助您完成該工作，Granite UI提供了要繼承的通用欄位元件(使用 `sling:resourceSuperType`):

`/libs/granite/ui/components/coral/foundation/form/field`

更具體地說，Granite UI提供一系列欄位元件，適合用於對話方塊(或更一般地，以 [表單](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html))。

>[!NOTE]
>
>這與傳統UI不同，Widget由節點來表示，每個節點 `cq:Widgets` 都具有特定的節點，以 `xtype` 建立與其對應ExtJS Widget的關係。 從實作的角度來看，這些Widget是由ExtJS架構在用戶端上轉譯的。

建立資源類型後，可以通過在對話框中添加新節點來實例化欄位，該屬性引用您剛剛引入的 `sling:resourceType` 資源類型。

#### 建立樣式與行為的用戶端程式庫 {#creating-a-client-library-for-style-and-behavior}

如果您想要定義元件的樣式和行為，可以建立專用的用戶 [端程式庫](/help/sites-developing/clientlibs.md) ，以定義自訂CSS/LESS和JS。

要僅為元件對話框（即不為其他元件載入）載入客戶端庫，您需要將對話框的屬性 `extraClientlibs`** **設定為剛建立的客戶端庫的類別名稱。 如果您的用戶端資料庫相當大且／或您的欄位是該對話方塊專屬的，且在其他對話方塊中不需要，則建議您這麼做。

若要讓所有對話方塊的用戶端程式庫都已載入，請將用戶端程式庫的category屬性設為 `cq.authoring.dialog`。 這是客戶端庫的類別名稱，在顯示所有對話框時，預設情況下會包含該類別名稱。 如果您的用戶端程式庫較小且／或欄位是通用的，而且可在其他對話方塊中重複使用，您就要這麼做。

如需範例，請參閱：

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * 由程式碼范 [例提供](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### 擴展（繼承自）欄位 {#extending-inheriting-from-a-field}

視您的需求而定，您可以：

* 依元件繼承( `sling:resourceSuperType`)擴充指定的Granite UI欄位
* 從基礎介面工具集程式庫延伸指定介面工具集（如果是Granite UI，則為Coral UI），請遵循介面工具集程式庫API（JS/CSS繼承）

#### 對對話框欄位的訪問 {#access-to-dialog-fields}

您也可以使用演算條件( `rendercondition`)來控制哪些人可以存取對話方塊中的特定標籤／欄位；例如：

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### 處理欄位事件 {#handling-field-events}

現在，處理對話欄位上事件的方法已在自訂用戶端程 [式庫中對聆聽器完成](#listeners-in-a-custom-client-library)。 這與舊式的內容結構中有監聽器 [的方法有所不同](#listenersinthecontentstructureclassicui)。

#### 自訂用戶端程式庫中的監聽器 {#listeners-in-a-custom-client-library}

若要將邏輯插入您的欄位，您應：

1. 將您的欄位標示為指定的CSS類別( *掛接*)。
1. 在用戶端程式庫中，定義一個掛接該CSS類別名稱的JS接聽程式（這可確保您的自訂邏輯僅限於您的欄位，而不會影響同類型的其他欄位）。

若要達成此目的，您必須瞭解您要與之互動的基礎Widget程式庫。 請參 [閱Coral UI檔案](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) ，以識別您要回應的事件。 這與您過去必須對ExtJS執行的程式非常類似：尋找指定介面工具集的檔案頁面，然後檢查其事件API的詳細資訊。

如需範例，請參閱：

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * 由程式碼范 [例提供](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### 內容結構中的監聽器 {#listeners-in-the-content-structure}

在具有ExtJS的傳統UI中，通常在內容結構中有指定Widget的監聽器。 在觸控式UI中達到相同的效果與JS接聽程式碼（或任何程式碼）在內容中不再定義不同。

內容結構描述了語義結構；它不應（必須）暗示基礎介面工具集的性質。 如果內容結構中沒有JS程式碼，您就可以變更實作詳細資訊，而不需變更內容結構。 換言之，您可以變更介面工具集資料庫，而不需觸碰內容結構。

### 欄位驗證 {#field-validation}

#### 必填欄位 {#mandatory-field}

要將指定欄位標籤為強制，請在欄位的內容節點上設定以下屬性：

* 名稱: `required`
* 類型: `Boolean`

如需範例，請參閱：

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title
```

#### 欄位驗證(Granite UI) {#field-validation-granite-ui}

在Granite UI和Granite UI元件（相當於widget）中進行欄位驗證時，會使用 `foundation-validation` API。 [如需詳細資 `foundation-valdiation` 訊，請參閱Granite檔案。](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

如需範例，請參閱：

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * 由程式碼范 [例提供](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## 建立和配置設計對話框 {#creating-and-configuring-a-design-dialog}

當元件具有可在設計模式中編輯的設計詳細資訊時，將提供「設 [計」對話框](/help/sites-authoring/default-components-designmode.md)。

定義與用於編輯內容的對 [話框非常相似](#creating-a-new-dialog)，其區別在於它定義為節點：

* Node name: `cq:design_dialog`
* 類型: `nt:unstructured`

## 建立和配置Inplace編輯器 {#creating-and-configuring-an-inplace-editor}

置入編輯器可讓使用者直接編輯段落流程中的內容，而不需開啟對話方塊。 例如，標準的「文字」和「標題」元件都有置入編輯器。

不需要／不需要對每個元件類型都有意義的就地編輯器。

如需詳 [細資訊，請參閱「擴充頁面編寫功能——新增就地編輯器](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor) 」。

## 自訂元件工具列 {#customizing-the-component-toolbar}

「組 [件工具欄](/help/sites-developing/touch-ui-structure.md#component-toolbar) 」(Component Toolbar)可讓用戶訪問元件的一系列操作，如編輯、配置、複製和刪除。

如需詳 [細資訊，請參閱「擴充頁面編寫功能——新增動作至元件工具列](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) 」。

## 為參照邊欄配置元件（借／借） {#configuring-a-component-for-the-references-rail-borrowed-lent}

如果您的新元件參照了其他頁面的內容，則您可以考慮是否要影響參照邊欄的「借閱內容 **」(** Rowerd Content **)和「借閱內容」(** Lent Content [**)區段&#x200B;**](/help/sites-authoring/basic-handling.md#references)。

現成可用的AEM只會檢查Reference元件。 若要新增元件，您必須設定OSGi搭售 **WCM編寫內容參考設定**。

在定義中建立新條目，指定元件以及要檢查的屬性。 例如：

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>使用AEM時，有數種方法可管理此類服務的組態設定。 如需詳 [細資訊](/help/sites-deploying/configuring-osgi.md) ，請參閱設定OSGi以及建議的實務。

## 啟用元件並將其新增至段落系統 {#enabling-and-adding-your-component-to-the-paragraph-system}

在開發元件後，它需要啟用以便在適當的段落系統中使用，以便用於所需的頁面。

這可以通過以下任一方法完成：

* 在編 [輯特定頁面時](/help/sites-authoring/default-components-designmode.md) ，使用「設計」模式。
* [在模 `components` 板的段落系統上定義屬性](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system)。

## 設定段落系統，以便拖曳資產可建立元件例項 {#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

AEM提供在您的頁面上設定段落系統的可能性，讓當使用者將（適當）資產拖曳至該頁面的例項時 [](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui) （而不必總是拖曳空白元件至頁面），就會自動建立新元件的例項。

此行為，以及必要的資產對元件關係可以設定：

1. 在頁面設計的段落定義下。 例如：

   * `/etc/designs/<myApp>/page/par`
   建立新節點：

   * 名稱: `cq:authoring`
   * 類型: `nt:unstructured`


1. 在此下，建立一個新節點以保存所有資產到元件映射：

   * 名稱: `assetToComponentMapping`
   * 類型: `nt:unstructured`

1. 對於每個資產到元件映射，建立一個節點：

   * 名稱：文字；建議名稱注明資產及相關元件類型；例如，影像
   * 類型: `nt:unstructured`
   每個都包含下列屬性：

   * `assetGroup`:

      * 類型: `String`
      * 值：資產所屬之集團；例如， `media`
   * `assetMimetype`:

      * 類型: `String`
      * 值：相關資產的啞劇型；例如 `image/*`
   * `droptarget`:

      * 類型: `String`
      * 值：落靶；例如， `image`
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

GITHUB代碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-project-archetype專案](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/archive/master.zip)

>[!NOTE]
>
>使用核心元件和可編輯範本時，現在可輕鬆在UI中設定元件例 [項的自動](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) 建立。 如需 [](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) 定義哪些元件會自動與特定媒體類型關聯的詳細資訊，請參閱建立頁面範本。

## 使用AEM Brackets延伸模組 {#using-the-aem-brackets-extension}

AEM Brackets Extension [](/help/sites-developing/aem-brackets.md) 提供順暢的工作流程來編輯AEM元件和用戶端程式庫。 它以 [Brackets程式碼編輯器為基礎](https://brackets.io/) 。

擴充功能：

* 簡化同步（不需Maven或File Vault），以協助提高開發人員的效率，並協助具備有限AEM知識的前端開發人員參與專案。
* 提供 [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) 支援，此範本語言旨在簡化元件開發並提高安全性。

>[!NOTE]
>
>Brackets是建立元件的建議機制。 它取代了專為傳統UI所設計的CRXDE Lite —— 建立元件功能。

## 從傳統元件遷移 {#migrating-from-a-classic-component}

將專為搭配傳統UI使用而設計的元件移轉至可與觸控式UI搭配使用的元件時（單獨或共同使用），應考慮下列問題：

* HTL

   * 使用 [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) 並非強制性，但如果您的元件需要更新，則是考慮從JSP移 [轉至HTL的理想時機](/help/sites-developing/components-basics.md#htl-vs-jsp)。

* 元件

   * 移轉 [ 使用 `cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code) 傳統UI特定功能的程式碼
   * RTE增效模組，如需詳細資訊，請 [參閱Configuring the Rich Text Editor](/help/sites-administering/rich-text-editor.md)。
   * [移轉 `cq:listener` 使用](#migrating-cq-listener-code) 傳統UI專用功能的程式碼

* 對話方塊

   * 您將需要建立新對話方塊，以便在觸控式UI中使用。 不過，為了相容性，當未為觸控式UI定義對話方塊時，觸控式UI可以使用傳統UI對話方塊的定義。
   * 提供 [對話框轉換工具](/help/sites-developing/dialog-conversion.md) ，可幫助您擴展現有元件。
   * [將ExtJS對應至Granite UI元件](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components) ，可方便地概述ExtJS xtypes和節點類型及其等效的Granite UI資源類型。
   * 自訂欄位，如需詳細資訊，請參閱「自訂對話方塊欄位」上的AEM Gems [工作階段](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html)。
   * 從vtypes移轉至 [Granite UI驗證](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * 使用JS監聽器，如需詳細資訊，請參 [閱「自訂對話方塊欄位」上的](#handling-field-events) 「處理欄位事件」和AEM Gems [工作階段](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html)。

### 移轉cq：接聽程式碼 {#migrating-cq-listener-code}

如果您要移轉專為傳統UI設計的專案，則程式碼(和元件相關的 `cq:listener` clientlibs)可能會使用特定於傳統UI的函式(例如 `CQ.wcm.*`)。 在移轉時，您必須使用觸控式UI中的等同物件／函式來更新此類程式碼。

如果您的專案已完全移轉至觸控式使用者介面，您需要取代此類程式碼，以使用與觸控式使用者介面相關的物件和功能。

不過，如果您的專案在移轉期間（通常情形）必須同時符合傳統UI和觸控式UI，則您必須實作切換，以區隔參照適當物件的個別程式碼。

此切換機制可實現為：

```
if (Granite.author) {
    // touch UI
} else {
    // classic UI
}
```

## 記錄您的元件 {#documenting-your-component}

身為開發人員，您希望輕鬆存取元件檔案，以便快速瞭解：

* 說明
* 預定用途
* 內容結構與屬性
* 公開的API和擴充點
* 等等。

因此，很容易將您現有的任何檔案標籤列在元件本身中。

您只需要將檔案放 `README.md` 置在元件結構中。 然後，此標籤會顯示在元件 [主控台](/help/sites-authoring/default-components-console.md)。

![chlimage_1-7](assets/chlimage_1-7.png)

支援的標籤與內容片段的標 [記相同](/help/assets/content-fragments-markdown.md)。
