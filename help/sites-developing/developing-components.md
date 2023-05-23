---
title: 開發組AEM件
seo-title: Developing AEM Components
description: 組AEM件用於保存、格式化和呈現網頁上提供的內容。
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
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '3456'
ht-degree: 1%

---

# 開發組AEM件{#developing-aem-components}

組AEM件用於保存、格式化和呈現網頁上提供的內容。

* 當 [創作頁面](/help/sites-authoring/default-components.md)，這些元件允許作者編輯和配置內容。

   * 構造 [商業](/help/commerce/cif-classic/administering/ecommerce.md) 站點元件可以收集和呈現目錄中的資訊。
請參閱 [發展電子商務](/help/commerce/cif-classic/developing/ecommerce.md) 的子菜單。

   * 構造 [社區](/help/communities/author-communities.md) 站點元件可向訪問者提供資訊並從訪問者收集資訊。
請參閱 [發展中社區](/help/communities/communities.md) 的子菜單。

* 在發佈實例上，這些元件將呈現您的內容，並按您要求向網站訪問者呈現。

>[!NOTE]
>
>此頁面是文檔的繼續 [組AEM件 — 基礎](/help/sites-developing/components-basics.md)。

>[!CAUTION]
>
>以下元件 `/libs/cq/gui/components/authoring/dialog` 僅用於編輯器（創作中的元件對話框）。 如果在其他位置（例如在嚮導對話框中）使用它們，則它們的行為可能不如預期。

## 程式碼範例 {#code-samples}

此頁提供開發新元件所需的參考文檔（或指向參考文檔的連結）AEM。 請參閱 [開發AEM元件 — 代碼示例](/help/sites-developing/developing-components-samples.md) 一些實例。

## 結構 {#structure}

元件的基本結構在頁面上覆蓋 [組AEM件 — 基礎](/help/sites-developing/components-basics.md#structure)。 該文檔既包括啟用觸摸功能的用戶介面，也包括經典用戶介面。 即使您不需要在新元件中使用經典設定，在繼承現有元件時也可以瞭解它們。

## 擴展現有元件和對話框 {#extending-existing-components-and-dialogs}

根據要實施的元件，可能會擴展或定制現有實例，而不是定義和開發整個實例 [結構](#structure) 從頭開始。

在擴展或定制現有元件或對話框時，可以在進行更改之前複製或複製對話框所需的整個結構或結構。

### 擴展現有元件 {#extending-an-existing-component}

可以利用 [資源類型層次結構](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance) 以及相關的繼承機制。

>[!NOTE]
>
>也可以基於搜索路徑邏輯用覆蓋重定義元件。 然而，在此情況下， [Sling資源合併](/help/sites-developing/sling-resource-merger.md) 未觸發並 `/apps` 必須定義整個覆蓋。

>[!NOTE]
>
>的 [內容片段元件](/help/sites-developing/customizing-content-fragments.md) 也可以定制和擴展，但必須考慮與Assets的完整結構和關係。

### 自定義現有元件對話框 {#customizing-a-existing-component-dialog}

也可以覆蓋 *元件對話框* 使用 [Sling資源合併](/help/sites-developing/sling-resource-merger.md) 定義屬性 `sling:resourceSuperType`。

這意味著您只需重定義所需的差異，而不需要重定義整個對話框(使用 `sling:resourceSuperType`)。 現在建議使用此方法來擴展元件對話框

查看 [Sling資源合併](/help/sites-developing/sling-resource-merger.md) 的子菜單。

## 定義標籤 {#defining-the-markup}

將使用 [HTML](https://www.w3schools.com/htmL/html_intro.asp)。 您的元件需要定義獲取所需內容所需的HTML，然後根據需要在作者和發佈環境中呈現它。

### 使用HTML模板語言 {#using-the-html-template-language}

的 [HTML模板語言(HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)在6.0中引AEM入的JSP(JavaServer Pages)代替了JSP(JavaServer Pages)作為首選和推薦的伺服器端模板系統進行HTML。 對於需要構建強健企業網站的Web開發人員，HTL有助於提高安全性和開發效率。

>[!NOTE]
>
>雖然HTL和JSP都可用於元件的開發，但我們將在此頁上用HTL來說明開發，因為它是推薦的指令碼語言AEM。

## 開發內容邏輯 {#developing-the-content-logic}

此可選邏輯選擇和/或計算要呈現的內容。 從HTL表達式中調用該函式，並使用適當的Use-API模式。

將邏輯與外觀分離的機制有助於澄清對給定視圖所調用的內容。 它還允許對同一資源的不同視圖使用不同的邏輯。

### 使用Java {#using-java}

[HTL Java Use-API使HTL檔案能夠訪問自定義Java類中的幫助程式方法](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html?lang=en)。 這樣，您就可以使用Java代碼來實現用於選擇和配置元件內容的邏輯。

### 使用JavaScript {#using-javascript}

[HTL JavaScript Use-API使HTL檔案能夠訪問用JavaScript編寫的幫助程式碼](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html?lang=en)。 這允許您使用JavaScript代碼來實現用於選擇和配置元件內容的邏輯。

### 使用客戶端HTML庫 {#using-client-side-html-libraries}

現代網站在複雜的JavaScript和CSS代碼驅動下，嚴重依賴客戶端處理。 組織和優化此代碼的服務可能是一個複雜的問題。

為幫助處理此問題，提供 **客戶端庫資料夾**，允許您將客戶端代碼儲存在儲存庫中，將其組織為類別，並定義將每類代碼提供給客戶端的時間和方式。 然後，客戶端庫系統會注意在最終網頁中生成正確的連結以載入正確的代碼。

閱讀 [使用客戶端HTML庫](/help/sites-developing/clientlibs.md) 的子菜單。

## 配置編輯行為 {#configuring-the-edit-behavior}

可以配置元件的編輯行為，包括元件可用的操作、就地編輯器的特性以及與元件上的事件相關的監聽器等屬性。 該配置對於啟用觸摸的UI和經典UI都是通用的，儘管有某些特定的差異。

的 [已配置元件的編輯行為](/help/sites-developing/components-basics.md#edit-behavior) 通過添加 `cq:editConfig` 類型節點 `cq:EditConfig` 元件節點下(類型 `cq:Component`)和添加特定屬性和子節點。

## 配置預覽行為 {#configuring-the-preview-behavior}

的 [WCM模式](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) 切換到 **預覽** 模式，即使不刷新頁面。

對於具有對WCM模式敏感的渲染的元件，需要定義這些元件以具體地刷新自身，然後依賴cookie的值。

>[!NOTE]
>
>在啟用觸摸的UI中，僅值 `EDIT` 和 `PREVIEW` 用於 [WCM模式](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) 餅乾。

## 建立和配置對話框 {#creating-and-configuring-a-dialog}

對話框用於允許作者與元件交互。 使用對話框允許作者和/或管理員編輯內容、配置元件或定義設計參數(使用 [設計對話框](#creating-and-configuring-a-design-dialog))

### 珊瑚界和花崗岩界 {#coral-ui-and-granite-ui}

[珊瑚UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html) 和 [花崗岩UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) 定義現代的外觀和感AEM覺。

[Granite UI提供了大量基本元件（小部件）](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) 在創作環境中建立對話框。 必要時，可以擴展此選區並 [建立自己的小部件](#creatinganewwidget)。

有關完整詳細資訊，請參閱：

* 珊瑚UI

   * 跨所有雲解決方案提供一致的UI
   * [啟用觸摸AEM的UI概念 — Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Coral UI 指南](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html)

* 花崗岩UI

   * 提供包裝到Sling元件中的Coral UI標籤，用於構建UI控制台和對話框
   * [啟用觸摸AEM的UI概念 — 花崗岩UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [花崗岩UI文檔](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)

>[!NOTE]
>
>由於Granite UI元件的性質（與ExtJS小部件的不同），元件與啟用觸摸的UI的交互方式與 [經典UI](/help/sites-developing/developing-components-classic.md)。

### 建立新對話框 {#creating-a-new-dialog}

啟用觸摸的UI的對話框：

* 命名 `cq:dialog`。
* 定義為 `nt:unstructured` 節點 `sling:resourceType` 屬性集。

* 位於 `cq:Component` 節點，並且位於其元件定義旁。
* 在伺服器端（作為Sling元件）上根據其內容結構和 `sling:resourceType` 屬性。
* 使用Granite UI框架。
* 包含描述對話框中欄位的節點結構。

   * 這些節點 `nt:unstructured` 需要 `sling:resourceType` 屬性。

節點結構的示例可能是：

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

定制對話框類似於開發元件，因為該對話框本身是元件（即由元件指令碼呈現的標籤與由客戶端庫提供的行為/樣式）。

有關示例，請參見：

* `/libs/foundation/components/text/cq:dialog`
* `/libs/foundation/components/download/cq:dialog`

>[!NOTE]
>
>如果元件沒有為啟用觸摸的UI定義對話框，則標準UI對話框將用作相容層內的回退。 要自定義此對話框，需要自定義經典UI對話框。 請參閱 [傳AEM統UI的元件](/help/sites-developing/developing-components-classic.md)。

### 自定義對話框欄位 {#customizing-dialog-fields}

>[!NOTE]
>
>請參閱：
>
>* Gems會AEM議於 [自定義對話框欄位](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=en)。
>* 下文所涵蓋的相關樣本代碼 [代碼示例 — 如何自定義對話框欄位](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)。
>


#### 建立新欄位 {#creating-a-new-field}

啟用觸摸的UI的小部件作為Granite UI元件實現。

要在啟用觸摸的UI的元件對話框中建立新小部件，需要 [建立新的花崗岩UI欄位元件](/help/sites-developing/granite-ui-component.md)。

>[!NOTE]
>
>有關Granite UI的完整詳細資訊，請參閱 [花崗岩用戶介面文檔](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)。

如果您將對話框視為表單元素的簡單容器，則還可以將對話框內容的主要內容視為表單域。 建立新表單域需要建立資源類型；這相當於建立新元件。 為幫助您完成該任務，Granite UI提供了要繼承的通用欄位元件(使用 `sling:resourceSuperType`):

`/libs/granite/ui/components/coral/foundation/form/field`

更具體地說，Granite UI提供了一系列適合在對話中使用的場元件(或更一般地，在 [表](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html))。

>[!NOTE]
>
>這與經典UI不同，後者用 `cq:Widgets` 節點，每個節點具有 `xtype` 建立與其相應的ExtJS構件的關係。 從實現的角度看，這些小部件是通過ExtJS框架在客戶端上實現的。

建立資源類型後，可以通過在對話框中添加新節點，並使用屬性來實例化欄位 `sling:resourceType` 指您剛介紹的資源類型。

#### 為樣式和行為建立客戶端庫 {#creating-a-client-library-for-style-and-behavior}

如果要為元件定義樣式和行為，可建立專用 [客戶端庫](/help/sites-developing/clientlibs.md) 定義自定義CSS/LESS和JS。

要僅為元件對話框載入客戶端庫（即不會為其他元件載入），需要設定屬性 `extraClientlibs`** **您剛建立的客戶端庫的類別名稱對話框。 如果客戶端庫很大，並且/或您的欄位特定於該對話框，並且在其他對話框中不需要，則建議這樣做。

要為所有對話框載入客戶端庫，請將客戶端庫的category屬性設定為 `cq.authoring.dialog`。 這是客戶端庫的類別名稱，預設情況下，在呈現所有對話框時包括它。 如果客戶端庫較小且/或您的欄位是泛型的，並且可以在其它對話框中重用，則您希望執行此操作。

有關示例，請參見：

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * 由 [代碼示例](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### 擴展（繼承自）欄位 {#extending-inheriting-from-a-field}

根據您的要求，您可以：

* 按元件繼承擴展給定的花崗岩UI欄位( `sling:resourceSuperType`)
* 通過遵循構件庫API（JS/CSS繼承），從基礎構件庫擴展給定構件（在Granite UI中，此為Coral UI）

#### 訪問對話框欄位 {#access-to-dialog-fields}

也可以使用渲染條件( `rendercondition`)控制誰有權訪問對話框中的特定頁籤/欄位；例如：

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### 處理欄位事件 {#handling-field-events}

處理對話框欄位中事件的方法現在已完成 [自定義客戶端庫中的偵聽器](#listeners-in-a-custom-client-library)。 這是與以前的方法 [內容結構中的監聽器](#listenersinthecontentstructureclassicui)。

#### 自定義客戶端庫中的偵聽器 {#listeners-in-a-custom-client-library}

要將邏輯插入您的欄位，您應：

1. 使用給定的CSS類標籤您的欄位( *鈎*)。
1. 在客戶端庫中，定義一個掛接到該CSS類名的JS偵聽器（這可確保您的自定義邏輯僅限於您的欄位，並且不會影響同一類型的其他欄位）。

要實現此目標，您需要瞭解要與之交互的底層構件庫。 查看 [Coral UI文檔](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html) 確定要對哪個事件做出反應。 這與您過去對ExtJS執行的過程非常相似：查找給定小部件的文檔頁面，然後檢查其事件API的詳細資訊。

有關示例，請參見：

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * 由 [代碼示例](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### 內容結構中的偵聽器 {#listeners-in-the-content-structure}

在帶有ExtJS的經典UI中，通常在內容結構中為給定小部件設定偵聽器。 在啟用觸摸的UI中實現相同的功能與在內容中不再定義JS偵聽器代碼（或任何代碼）時不同。

內容結構描述語義結構；它不應（必須）暗示基礎小部件的性質。 通過在內容結構中不使用JS代碼，您可以更改實現詳細資訊，而無需更改內容結構。 換句話說，您可以更改小部件庫，而無需觸摸內容結構。

#### 檢測對話框的可用性 {#dialog-ready}

如果您有一個自定義JavaScript，該自定義JavaScript只需在對話框可用且準備就緒時才需要執行，則您應該偵聽 `dialog-ready` 的子菜單。

只要對話框載入（或重新載入）並準備使用，即會觸發此事件，這意味著只要對話框的DOM中有更改（建立/更新）。

`dialog-ready` 可用於掛接JavaScript自定義代碼，該代碼對對話框或類似任務中的欄位執行自定義。

### 欄位驗證 {#field-validation}

#### 必填欄位 {#mandatory-field}

要將給定欄位標籤為必需，請在欄位的內容節點上設定以下屬性：

* 名稱: `required`
* 類型: `Boolean`

有關示例，請參見：

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title
```

#### 現場驗證（花崗岩UI） {#field-validation-granite-ui}

使用 `foundation-validation` API。 [查看 `foundation-valdiation` 花崗岩文檔，瞭解詳細資訊。](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

有關示例，請參見：

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * 由 [代碼示例](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## 建立和配置設計對話框 {#creating-and-configuring-a-design-dialog}

當元件具有可在中編輯的設計詳細資訊時，將提供「設計」對話框 [設計模式](/help/sites-authoring/default-components-designmode.md)。

定義與 [用於編輯內容的對話框](#creating-a-new-dialog)，區別在於它定義為節點：

* 節點名稱： `cq:design_dialog`
* 類型: `nt:unstructured`

## 建立和配置就地編輯器 {#creating-and-configuring-an-inplace-editor}

原位編輯器允許用戶直接編輯段落流中的內容，而無需開啟對話框。 例如，標準文本和標題元件都具有一個就地編輯器。

對於每個元件類型，不需要/不需要就地編輯器。

請參閱 [擴展頁面創作 — 添加新的就地編輯器](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor) 的子菜單。

## 自定義元件工具欄 {#customizing-the-component-toolbar}

的 [元件工具欄](/help/sites-developing/touch-ui-structure.md#component-toolbar) 允許用戶訪問元件的一系列操作，如編輯、配置、複製和刪除。

請參閱 [擴展頁面創作 — 將新操作添加到元件工具欄](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) 的子菜單。

## 為參照導軌配置元件（借入/借出） {#configuring-a-component-for-the-references-rail-borrowed-lent}

如果新元件引用來自其他頁面的內容，則可以考慮是否希望它影響 **借用內容** 和 **借出內容** 的 [**引用**](/help/sites-authoring/basic-handling.md#references) 鐵軌。

現成僅檢AEM查「參照」(Reference)元件。 要添加元件，您需要配置OSGi捆綁包 **WCM創作內容參考配置**。

在定義中建立新條目，指定元件以及要檢查的屬性。 例如：

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>使用時，AEM有多種方法管理此類服務的配置設定。 請參閱 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 的子菜單。

## 啟用元件並將其添加到段落系統 {#enabling-and-adding-your-component-to-the-paragraph-system}

在開發該元件後，需要啟用該元件以在適當的段落系統中使用，以便可以在所需的頁面上使用。

這可以通過以下任一方式完成：

* 使用 [設計模式](/help/sites-authoring/default-components-designmode.md) 編輯特定頁面時。
* [定義 `components` 模板段落系統上的屬性](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system)。

## 配置段落系統，以便拖動資產建立元件實例 {#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

提AEM供了在頁面上配置段落系統的可能性 [當用戶將一個（適當的）資產拖放到該頁的實例上時，將自動建立新元件的實例](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui) （而不是總是將空元件拖到頁面中）。

可以配置此行為以及所需的資產到元件關係：

1. 在頁面設計的段落定義下。 例如：

   * `/etc/designs/<myApp>/page/par`

   建立新節點：

   * 名稱: `cq:authoring`
   * 類型: `nt:unstructured`


1. 在此下，建立一個新節點以保存所有資產到元件映射：

   * 名稱: `assetToComponentMapping`
   * 類型: `nt:unstructured`

1. 對於每個資產到元件映射，建立一個節點：

   * 名稱：文本；建議名稱指明資產及相關元件類型；例如，影像
   * 類型: `nt:unstructured`

   每個都具有以下屬性：

   * `assetGroup`:

      * 類型: `String`
      * 值：相關資產所屬之組別；比如說， `media`
   * `assetMimetype`:

      * 類型: `String`
      * 值：相關資產的mime類型；例如 `image/*`
   * `droptarget`:

      * 類型: `String`
      * 值：落靶；比如說， `image`
   * `resourceType`:

      * 類型: `String`
      * 值：相關元件資源；比如說， `foundation/components/image`
   * `type`:

      * 類型: `String`
      * 值：例如， `Images`






有關示例，請參見：

* `/etc/designs/geometrixx/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-outdoors/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-media/jcr:content/article/article-content-par/cq:authoring`

GITHUB代碼

可以在GitHub上找到此頁的代碼

* [在GitHub上開啟項目原型項目](https://github.com/adobe/aem-project-archetype)
* 將項目下載為 [ZIP檔案](https://github.com/adobe/aem-project-archetype/archive/master.zip)

>[!NOTE]
>
>使用時，現在可以在UI中輕鬆配置元件實例的自動建立 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 和可編輯模板。 請參閱 [建立頁面模板](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) 的子菜單。

## 使用括弧AEM延伸 {#using-the-aem-brackets-extension}

的 [括弧AEM擴展](/help/sites-developing/aem-brackets.md) 提供了一個平滑的工作流，可編AEM輯元件和客戶端庫。 它基於 [括弧](https://brackets.io/) 代碼編輯器。

擴展：

* 簡化同步（不需要Maven或File Vault），以幫助提高開發人員效率，並幫助知識有限的前AEM端開發人員參與項目。
* 提供一些 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) 支援，模板語言旨在簡化元件開發並提高安全性。

>[!NOTE]
>
>括弧是建立元件的推薦機制。 它替換了為經典UI設計的CRXDE Lite — 建立元件功能。

## 從經典元件遷移 {#migrating-from-a-classic-component}

將設計為與標準UI一起使用的元件遷移到可與啟用觸摸的UI一起使用的元件（單獨或聯合使用）時，應考慮以下問題：

* HTL

   * 使用 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) 不是強制性的，但如果您的元件需要更新，則是考慮 [從JSP遷移到HTL](/help/sites-developing/components-basics.md#htl-vs-jsp)。

* 元件

   * 遷移 [ `cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code) 使用經典UI特定函式的代碼
   * RTE插件，有關詳細資訊，請參閱 [配置富格文本編輯器](/help/sites-administering/rich-text-editor.md)。
   * [遷移 `cq:listener` 代碼](#migrating-cq-listener-code) 使用特定於傳統UI的函式

* 對話方塊

   * 建立對話框以在啟用觸摸的用戶介面中使用。 但是，為了相容性目的，啟用觸摸的UI可以使用標準UI對話框的定義，但是尚未為啟用觸摸的UI定義對話框。
   * 的 [現代化AEM工具](/help/sites-developing/modernization-tools.md) 可幫助您擴展現有元件。
   * [將ExtJS映射到花崗岩UI元件](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components) 提供了ExtJS xtypes和節點類型及其等效花崗岩UI資源類型的方便概述。
   * 自定義欄位，有關詳細資訊，請參AEM閱Gems會話 [自定義對話框欄位](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=en)。
   * 從vtypes遷移到 [花崗岩UI驗證](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * 使用JS偵聽器，有關詳細資訊，請參閱 [處理欄位事件](#handling-field-events) 和GemsAEM會議 [自定義對話框欄位](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=en)。

### 遷移cq：偵聽程式碼 {#migrating-cq-listener-code}

如果要遷移為經典UI設計的項目，則 `cq:listener` 代碼（和與元件相關的客戶端）可能使用特定於經典UI的函式(如 `CQ.wcm.*`)。 對於遷移，必須使用啟用觸摸的UI中的等效對象/函式更新此類代碼。

如果項目完全遷移到啟用觸摸的UI，則需要替換此類代碼以使用與啟用觸摸的UI相關的對象和功能。

但是，如果項目在遷移期間（通常情況）必須同時滿足標準UI和啟用觸摸的UI，則必須實現切換，以區分引用相應對象的單獨代碼。

此切換機制可實現為：

```
if (Granite.author) {
    // touch UI
} else {
    // classic UI
}
```

## 記錄元件 {#documenting-your-component}

作為開發人員，您希望輕鬆訪問元件文檔，以便您能夠快速瞭解：

* 說明
* 預期用途
* 內容結構和屬性
* 暴露的API和擴展點
* 等等

因此，很容易將元件本身中現有的任何文檔標籤為可用。

放置a `README.md` 的子菜單。 此標籤顯示在 [元件控制台](/help/sites-authoring/default-components-console.md)。

![chlimage_1-7](assets/chlimage_1-7.png)

支援的標籤與 [內容片段](/help/assets/content-fragments/content-fragments-markdown.md)。
