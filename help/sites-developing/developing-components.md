---
title: 開發AEM元件
description: AEM元件可用來保留、格式化及轉譯可在網頁上使用的內容。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
legacypath: /content/docs/en/aem/6-2/develop/components/components-touch-optimized
exl-id: 573cdc36-e9c3-4803-9c4e-cebd0cf0a56f
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '3246'
ht-degree: 0%

---

# 開發AEM元件{#developing-aem-components}

AEM元件可用來保留、格式化及轉譯可在網頁上使用的內容。

* 時間 [製作頁面](/help/sites-authoring/default-components.md)，元件可讓作者編輯及設定內容。

   * 建構時 [商務](/help/commerce/cif-classic/administering/ecommerce.md) 舉例來說，元件可以在網站上收集及轉譯目錄中的資訊。
另請參閱 [開發電子商務](/help/commerce/cif-classic/developing/ecommerce.md) 以取得詳細資訊。

   * 建構時 [Communities](/help/communities/author-communities.md) 網站元件可向訪客提供資訊並從中收集資訊。
另請參閱 [開發社群](/help/communities/communities.md) 以取得詳細資訊。

* 在發佈執行個體上，元件會轉譯您的內容，並依您的需求向網站訪客顯示。

>[!NOTE]
>
>本頁是檔案的延續 [AEM元件 — 基本需知](/help/sites-developing/components-basics.md).

>[!CAUTION]
>
>以下的元件 `/libs/cq/gui/components/authoring/dialog` 僅能在編輯器（製作中的元件對話方塊）中使用。 如果在其他地方（例如在精靈對話方塊中）使用這些篩選器，可能無法如預期般運作。

## 程式碼範例 {#code-samples}

本頁提供為AEM開發新元件所需的參考檔案（或參考檔案連結）。 另請參閱 [開發AEM元件 — 程式碼範例](/help/sites-developing/developing-components-samples.md) 以取得一些實用的範例。

## 結構 {#structure}

頁面上會說明元件的基本結構 [AEM元件 — 基本需知](/help/sites-developing/components-basics.md#structure). 該檔案涵蓋觸控式與傳統UI。 即使您不需要在新元件中使用傳統設定，在繼承現有元件時瞭解這些設定也會有所幫助。

## 延伸現有元件和對話方塊 {#extending-existing-components-and-dialogs}

根據您想要實作的元件，可能會擴充或自訂現有例項，而非定義及開發整個 [結構](#structure) 從頭開始。

當延伸或自訂現有元件或對話方塊時，您可以在進行變更之前，複製或複製對話方塊所需的整個結構或結構。

### 擴充現有元件 {#extending-an-existing-component}

擴充現有元件可透過以下方式達成 [資源型別階層](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance) 以及相關的繼承機制。

>[!NOTE]
>
>元件也可以根據搜尋路徑邏輯，以覆蓋重新定義。 然而，在這種情況下， [Sling資源合併](/help/sites-developing/sling-resource-merger.md) 未觸發且 `/apps` 必須定義整個覆蓋。

>[!NOTE]
>
>此 [內容片段元件](/help/sites-developing/customizing-content-fragments.md) 您也可以自訂和擴充，不過必須考量完整結構和與Assets的關係。

### 自訂現有元件對話方塊 {#customizing-a-existing-component-dialog}

您也可以覆寫 *元件對話方塊* 使用 [Sling資源合併](/help/sites-developing/sling-resource-merger.md) 以及定義屬性 `sling:resourceSuperType`.

這表示您只需要重新定義所需的差異，而不必重新定義整個對話方塊(使用 `sling:resourceSuperType`)。 現在建議使用此方法來擴充元件對話方塊

請參閱 [Sling資源合併](/help/sites-developing/sling-resource-merger.md) 以取得更多詳細資料。

## 定義標示 {#defining-the-markup}

您的元件將轉譯為 [HTML](https://www.w3schools.com/htmL/html_intro.asp). 您的元件需要定義所需的HTML，以便在製作和發佈環境中取得所需內容，然後視需要轉譯。

### 使用HTML範本語言 {#using-the-html-template-language}

此 [HTML範本語言(HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)AEM 6.0引進的，取代了JSP (JavaServer Pages)，成為偏好和建議的HTML伺服器端範本系統。 對於需要建立強大企業網站的網頁開發人員而言，HTL有助於提高安全性和開發效率。

>[!NOTE]
>
>雖然HTL和JSP都可用於開發元件，但我們將在本頁說明使用HTL進行開發，因為這是建議的AEM指令碼語言。

## 開發內容邏輯 {#developing-the-content-logic}

此選擇性邏輯會選取及/或計算要呈現的內容。 它會從具有適當Use-API模式的HTL運算式叫用。

從外觀分離邏輯的機制有助於釐清對指定檢視的呼叫內容。 它也會允許同一資源的不同檢視有不同的邏輯。

### 使用Java {#using-java}

[HTL Java Use-API讓HTL檔案能夠存取自訂Java類別中的helper方法](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html). 這可讓您使用Java程式碼來實作選取和設定元件內容的邏輯。

### 使用JavaScript {#using-javascript}

[HTL JavaScript Use-API讓HTL檔案能夠存取以JavaScript撰寫的helper程式碼](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html). 這可讓您使用JavaScript程式碼來實作選取和設定元件內容的邏輯。

### 使用使用者端HTML程式庫 {#using-client-side-html-libraries}

現代網站非常依賴由複雜的JavaScript和CSS程式碼驅動的使用者端處理。 組織和最佳化此程式碼的伺服可能是一個複雜的問題。

為協助處理此問題，AEM提供 **使用者端資料庫資料夾**，可讓您將使用者端程式碼儲存在存放庫中，將其組織成類別，並定義每個類別程式碼何時及如何提供給使用者端。 然後，使用者端程式庫系統會負責在最終網頁中產生正確的連結，以載入正確的程式碼。

讀取 [使用使用者端HTML程式庫](/help/sites-developing/clientlibs.md) 以取得詳細資訊。

## 設定編輯行為 {#configuring-the-edit-behavior}

您可以設定元件的編輯行為，包括元件可用的動作、就地編輯器的特性，以及與元件事件相關的接聽程式等屬性。 此設定對觸控式與傳統UI而言都是通用的，不過會有某些特定差異。

此 [元件的編輯行為已設定](/help/sites-developing/components-basics.md#edit-behavior) 藉由新增 `cq:editConfig` 型別節點 `cq:EditConfig` 在元件節點（型別）下方 `cq:Component`)，並新增特定屬性和子節點。

## 設定預覽行為 {#configuring-the-preview-behavior}

此 [WCM模式](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) 切換至時設定Cookie **預覽** 模式，即使頁面未重新整理。

對於具有對WCM模式敏感的轉譯之元件，需要定義它們以專門重新整理自身，然後依賴Cookie的值。

>[!NOTE]
>
>在啟用觸控的UI中 `EDIT` 和 `PREVIEW` 用於 [WCM模式](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) Cookie。

## 建立和設定對話方塊 {#creating-and-configuring-a-dialog}

對話方塊可用來允許作者與元件互動。 使用對話方塊可讓作者和/或管理員編輯內容、設定元件或定義設計引數(使用 [設計對話方塊](#creating-and-configuring-a-design-dialog))

### Coral UI和Granite UI {#coral-ui-and-granite-ui}

[Coral UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html) 和 [Granite UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) 定義AEM的現代外觀。

[Granite UI提供多種基本元件(Widget)](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) 需要在編寫環境中建立您的對話方塊。 必要時，您可以延伸此選取範圍並 [建立您自己的Widget](#creatinganewwidget).

如需完整詳細資訊，請參閱：

* Coral UI

   * 跨所有雲端解決方案提供一致的UI
   * [AEM觸控式UI的概念 — Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Coral UI指南](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html)

* Granite UI

   * 提供包在Sling元件中的Coral UI標籤，用於建置UI主控台和對話方塊
   * [AEM觸控式UI的概念 — Granite UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Granite UI檔案](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)

>[!NOTE]
>
>由於Granite UI元件的性質（以及ExtJS Widget的差異），元件與觸控式UI的互動方式與 [傳統UI](/help/sites-developing/developing-components-classic.md).

### 建立新對話方塊 {#creating-a-new-dialog}

觸控式UI的對話方塊：

* 已命名 `cq:dialog`.
* 定義為 `nt:unstructured` 節點與 `sling:resourceType` 屬性集。

* 位在其 `cq:Component` 節點及其元件定義旁的。
* 會根據其內容結構和 `sling:resourceType` 屬性。
* 使用Granite UI架構。
* 包含描述對話方塊內欄位的節點結構。

   * 這些節點為 `nt:unstructured` 具有必要的 `sling:resourceType` 屬性。

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

自訂對話方塊類似於開發元件，因為對話方塊本身是元件（也就是說，由元件指令碼轉譯的標示連同使用者端程式庫提供的行為/樣式）。

如需範例，請參閱：

* `/libs/foundation/components/text/cq:dialog`
* `/libs/foundation/components/download/cq:dialog`

>[!NOTE]
>
>如果元件沒有為觸控式UI定義對話方塊，則會使用Classic UI對話方塊作為相容性層級的後援。 若要自訂此類對話方塊，您需要自訂傳統UI對話方塊。 另請參閱 [傳統UI的AEM元件](/help/sites-developing/developing-components-classic.md).

### 自訂對話方塊欄位 {#customizing-dialog-fields}

>[!NOTE]
>
>請參閱：
>
>* 上的AEM Gems研討會 [自訂對話方塊欄位](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html).
>* 下的相關範常式式碼 [程式碼範例 — 如何自訂對話方塊欄位](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields).
>

#### 建立新欄位 {#creating-a-new-field}

觸控式UI的Widget會實作為Granite UI元件。

若要建立Widget以用於觸控式UI的元件對話方塊，需要您 [建立Granite UI欄位元件](/help/sites-developing/granite-ui-component.md).

>[!NOTE]
>
>如需Granite UI的完整詳細資訊，請參閱 [Granite UI檔案](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html).

如果您將對話方塊視為表單元素的簡單容器，則也可以將對話方塊內容的主要內容視為表單欄位。 建立表單欄位需要您建立資源型別；這等同於建立元件。 為協助您完成該工作，Granite UI提供了可供繼承的通用欄位元件(使用 `sling:resourceSuperType`)：

`/libs/granite/ui/components/coral/foundation/form/field`

更具體來說，Granite UI提供了一系列適合用於對話方塊的欄位元件(或更一般地說，在 [表單](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html))。

>[!NOTE]
>
>這與傳統UI不同，在傳統UI中，Widget是由 `cq:Widgets` 節點，每個節點都有特定的 `xtype` 以建立與其對應ExtJS Widget的關係。 從實作觀點來看，這些Widget是在使用者端由ExtJS架構轉譯。

建立資源型別後，您可以在對話方塊中使用屬性新增節點，將欄位例項化 `sling:resourceType` 請參閱您剛才介紹的資源型別。

#### 建立樣式和行為的使用者端程式庫 {#creating-a-client-library-for-style-and-behavior}

如果您想要定義元件的樣式和行為，可以建立專用的 [使用者端資料庫](/help/sites-developing/clientlibs.md) 會定義您的自訂CSS/LESS和JS。

若要讓您的使用者端程式庫僅為您的元件對話方塊載入（也就是說，不會為另一個元件載入程式庫），您需要設定屬性 `extraClientlibs` 對話方塊的類別名稱切換至您已建立的使用者端程式庫的類別名稱。 如果您的使用者端程式庫相當大和/或您的欄位專屬於該對話方塊，且不需要在其他對話方塊中使用，建議您這麼做。

若要讓您的使用者端程式庫載入所有對話方塊，請將使用者端程式庫的類別屬性設定為 `cq.authoring.dialog`. 這是呈現所有對話方塊時預設包含的使用者端程式庫的類別名稱。 如果您使用者端資料庫較小且/或您的欄位是通用的，且可在其他對話方塊中重複使用，則您想要執行此動作。

如需範例，請參閱：

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * 提供者： [程式碼範例](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### 延伸（繼承）欄位 {#extending-inheriting-from-a-field}

視您的需求而定，您可以：

* 透過元件繼承擴充指定的Granite UI欄位( `sling:resourceSuperType`)
* 遵循Widget程式庫API （JS/CSS繼承），從基礎Widget程式庫（如果有Granite UI，則為Coral UI）擴充指定Widget

#### 對話方塊欄位的存取權 {#access-to-dialog-fields}

您也可以使用演算條件( `rendercondition`)來控制誰可以存取您對話方塊中的特定索引標籤/欄位，例如：

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### 處理欄位事件 {#handling-field-events}

處理對話方塊欄位上的事件方法現在已完成 [自訂使用者端資料庫中的監聽器](#listeners-in-a-custom-client-library). 這是由舊有方法所變更的 [內容結構中的監聽器](#listenersinthecontentstructureclassicui).

#### 自訂使用者端資料庫中的監聽器 {#listeners-in-a-custom-client-library}

若要將邏輯插入欄位，您應該：

1. 讓您的欄位標示為指定的CSS類別( *勾點*)。
1. 在您的使用者端程式庫中定義與該CSS類別名稱連結的JS接聽程式（這可確保您的自訂邏輯僅限定在欄位範圍內，不會影響相同型別的其他欄位）。

若要完成此操作，您需要瞭解您要與之互動的基礎Widget程式庫。 請參閱 [Coral UI檔案](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html) 以識別您要回應的事件。 這非常類似於您過去必須使用ExtJS執行的程式：尋找指定Widget的檔案頁面，然後檢查其事件API的詳細資料。

如需範例，請參閱：

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * 提供者： [程式碼範例](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### 內容結構中的監聽器 {#listeners-in-the-content-structure}

在具有ExtJS的傳統UI中，通常內容結構中會有指定Widget的監聽器。 在觸控式UI中達成相同目標的方式與內容中未定義的JS接聽程式程式碼（或任何程式碼）不同。

內容結構可描述語意結構；它應該（必須）不代表基礎Widget的性質。 內容結構中沒有JS程式碼，因此您可以變更實作詳細資料，而無須變更內容結構。 換言之，您可以變更Widget程式庫，而不需要接觸內容結構。

#### 偵測對話方塊的可用性 {#dialog-ready}

如果您有自訂JavaScript，只有在對話方塊可用且準備就緒時才需要執行，則應接聽 `dialog-ready` 事件。

每當對話方塊載入（或重新載入）並準備就緒可供使用時，即代表每當對話方塊的DOM中有變更（建立/更新）時，就會觸發此事件。

`dialog-ready` 可用於掛接JavaScript自訂程式碼，以在對話方塊或類似工作內的欄位上執行自訂。

### 欄位驗證 {#field-validation}

#### 必填欄位 {#mandatory-field}

若要將指定欄位標示為必填，請在欄位的內容節點上設定下列屬性：

* 名稱：`required`
* 類型：`Boolean`

如需範例，請參閱：

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title
```

#### 欄位驗證(Granite UI) {#field-validation-granite-ui}

Granite UI和Granite UI元件（等同於Widget）中的欄位驗證是使用 `foundation-validation` API。 [請參閱 `foundation-valdiation` Granite檔案以取得詳細資訊。](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

如需範例，請參閱：

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * 提供者： [程式碼範例](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## 建立和設定設計對話方塊 {#creating-and-configuring-a-design-dialog}

當元件具有可在其中編輯的設計詳細資訊時，會提供「設計」對話方塊 [設計模式](/help/sites-authoring/default-components-designmode.md).

定義非常類似於 [用於編輯內容的對話方塊](#creating-a-new-dialog)，不同之處在於定義為節點：

* 節點名稱： `cq:design_dialog`
* 類型：`nt:unstructured`

## 建立和設定就地編輯器 {#creating-and-configuring-an-inplace-editor}

就地編輯器可讓使用者直接在段落流程中編輯內容，而不需要開啟對話方塊。 例如，標準的「文字」和「標題」元件都有就地編輯器。

並非每個元件型別都需要/有意義的就地編輯器。

另請參閱 [擴充頁面編寫 — 新增就地編輯器](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor) 以取得詳細資訊。

## 自訂元件工具列 {#customizing-the-component-toolbar}

此 [元件工具列](/help/sites-developing/touch-ui-structure.md#component-toolbar) 可讓使用者存取元件的一系列動作，例如編輯、設定、複製和刪除。

另請參閱 [延伸頁面製作 — 將動作新增至元件工具列](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) 以取得詳細資訊。

## 為「參考」(References)邊欄（借入/借出）設定元件 {#configuring-a-component-for-the-references-rail-borrowed-lent}

如果您的新元件參考其他頁面的內容，則可以考慮是否要使其影響 **借用的內容** 和 **借出內容** 的區段 [**引用**](/help/sites-authoring/basic-handling.md#references) 邊欄。

現成可用的AEM只會檢查「參照」元件。 若要新增元件，您需要設定OSGi套件組合 **WCM製作內容參考設定**.

在定義中建立專案，指定元件以及要檢查的屬性。 例如：

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>使用AEM時，有數種方法可管理此類服務的組態設定。 另請參閱 [設定OSGi](/help/sites-deploying/configuring-osgi.md) 以取得詳細資訊和建議作法。

## 啟用元件並將其新增至段落系統 {#enabling-and-adding-your-component-to-the-paragraph-system}

開發元件後，必須將其啟用以供在適當的段落系統中使用，才能在所需頁面上使用。

您可以透過以下其中一種方式來完成：

* 使用 [設計模式](/help/sites-authoring/default-components-designmode.md) 編輯特定頁面時。
* [定義 `components` 範本的段落系統上的屬性](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system).

## 設定段落系統以便拖曳資產建立元件例項 {#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

AEM可讓您在頁面上設定段落系統，以便 [當使用者將資產拖曳至該頁面的例項時，系統會自動建立新元件的例項](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui) （不必一律將空白元件拖曳至頁面）。

此行為以及所需的資產與元件關係皆可設定：

1. 在頁面設計的段落定義底下。 例如：

   * `/etc/designs/<myApp>/page/par`

   建立節點：

   * 名稱：`cq:authoring`
   * 類型：`nt:unstructured`

1. 在此底下，建立節點以儲存所有資產對元件對應：

   * 名稱：`assetToComponentMapping`
   * 類型：`nt:unstructured`

1. 對於每個資產與元件對應，請建立節點：

   * 名稱：文字；建議名稱指出資產和相關元件型別；例如image
   * 類型：`nt:unstructured`

   每個檔案都具有下列屬性：

   * `assetGroup`：

      * 類型：`String`
      * 值：相關資產所屬的群組；例如， `media`

   * `assetMimetype`：

      * 類型：`String`
      * 值：相關資產的mime型別；例如， `image/*`

   * `droptarget`：

      * 類型：`String`
      * 值：放置目標；例如， `image`

   * `resourceType`：

      * 類型：`String`
      * 值：相關的元件資源；例如， `foundation/components/image`

   * `type`：

      * 類型：`String`
      * 值：型別，例如， `Images`

如需範例，請參閱：

* `/etc/designs/geometrixx/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-outdoors/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-media/jcr:content/article/article-content-par/cq:authoring`

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-project-archetype專案](https://github.com/adobe/aem-project-archetype)
* 將專案下載為 [ZIP檔案](https://github.com/adobe/aem-project-archetype/archive/master.zip)

>[!NOTE]
>
>使用時，現在可在UI中輕鬆設定自動建立元件例項 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant) 和可編輯的範本。 另請參閱 [建立頁面範本](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) 以取得定義哪些元件會自動與特定媒體型別相關聯的詳細資訊。

## 使用AEM Brackets擴充功能 {#using-the-aem-brackets-extension}

此 [AEM Brackets擴充功能](/help/sites-developing/aem-brackets.md) 提供流暢的工作流程來編輯AEM元件和使用者端程式庫。 其基礎為 [括弧](https://brackets.io/) 程式碼編輯器。

擴充功能：

* 簡化同步作業（不需要Maven或File Vault），協助提高開發人員效率，同時協助具備有限AEM知識的前端開發人員參與專案。
* 提供一些 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) 支援，這種範本語言旨在簡化元件開發並提高安全性。

>[!NOTE]
>
>建議使用托架來建立元件。 它取代了專為傳統UI設計的「CRXDE Lite — 建立元件」功能。

## 從傳統元件移轉 {#migrating-from-a-classic-component}

將設計用於傳統UI的元件移轉至可搭配觸控式UI使用的元件時（無論是單獨還是搭配使用），應考量下列問題：

* HTL

   * 使用 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) 不是強制性的，但如果您的元件需要更新，則為考慮的最佳時機 [從JSP移轉至HTL](/help/sites-developing/components-basics.md#htl-vs-jsp).

* 元件

   * 移轉 [`cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code) 使用傳統UI特定函式的程式碼
   * RTE外掛程式，如需進一步資訊，請參閱 [設定RTF編輯器](/help/sites-administering/rich-text-editor.md).
   * [移轉 `cq:listener` 程式碼](#migrating-cq-listener-code) 使用傳統UI專屬的函式

* 對話方塊

   * 建立對話方塊以用於觸控式UI。 不過，為相容性目的，如果沒有為觸控式UI定義對話方塊，觸控式UI可以使用傳統UI對話方塊的定義。
   * 此 [AEM現代化工具](/help/sites-developing/modernization-tools.md) 提供來協助您擴充現有元件。
   * [將ExtJS對應至Granite UI元件](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components) 提供ExtJS xtypes和節點型別及其同等的Granite UI資源型別的便利概述。
   * 自訂欄位，如需詳細資訊，請參閱上的AEM Gems研討會 [自訂對話方塊欄位](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html).
   * 從vtype移轉至 [Granite UI驗證](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * 使用JS監聽器，如需詳細資訊，請參閱 [處理欄位事件](#handling-field-events) 以及上的AEM Gems研討會 [自訂對話方塊欄位](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html).

### 正在移轉cq：listener程式碼 {#migrating-cq-listener-code}

如果您要移轉專案是專為傳統UI所設計，則 `cq:listener` 程式碼（和元件相關的clientlibs）可能會使用傳統UI特有的函式(例如 `CQ.wcm.*`)。 若要進行移轉，您必須使用觸控式UI中對應的物件/函式來更新這類程式碼。

如果您的專案已完全移轉至觸控式UI，您需要取代這類程式碼，才能使用與觸控式UI相關的物件和功能。

不過，如果您的專案在移轉期間（一般情況）必須同時符合傳統UI和觸控式UI，則必須實作交換器以區別參照適當物件的個別程式碼。

此切換機制可實作為：

```
if (Granite.author) {
    // touch UI
} else {
    // classic UI
}
```

## 記錄您的元件 {#documenting-your-component}

身為開發人員，您想要輕鬆存取元件檔案，以便快速瞭解：

* 說明
* 預期用途
* 內容結構和屬性
* 公開的API和擴充功能點
* 等等

因此，只要元件本身包含任何現有的檔案Markdown，都能輕鬆取用。

放置 `README.md` 檔案。 此Markdown會顯示在 [元件主控台](/help/sites-authoring/default-components-console.md).

![chlimage_1-7](assets/chlimage_1-7.png)

支援的Markdown與相同 [內容片段](/help/assets/content-fragments/content-fragments-markdown.md).
