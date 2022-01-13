---
title: 設定RTF編輯器以在Adobe Experience Manager中製作內容。
description: 了解如何設定Adobe Experience Manager RTF編輯器以在Adobe Experience Manager中編寫內容。
contentOwner: AG
exl-id: 2e7ec22f-0856-44c4-bb15-1086dae0b85a
source-git-commit: d1b4cf87291f7e4a0670a21feca1ebf8dd5e0b5e
workflow-type: tm+mt
source-wordcount: '3022'
ht-degree: 0%

---

# 設定RTF編輯器 {#configure-the-rich-text-editor}

RTF編輯器(RTE)為作者提供多種編輯文字內容的功能。 WYSIWYG文字編輯體驗提供圖示、選取方塊、工具列和功能表。

若要了解如何使用RTE功能進行製作，請參閱 [使用RTF編輯器進行編寫](/help/sites-authoring/rich-text-editor.md). RTE可以設定為啟用、停用和擴充製作元件中可用的功能。 以下工作流程說明在Experience Manager中完成RTE設定工作的建議順序。

![了解如何設定RTE的步驟順序](assets/rte_workflow_v1.png)

*圖：了解如何設定RTE的步驟順序*

## 了解觸控式UI和傳統UI {#understand-touch-enabled-ui-and-classic-ui}

觸控式UI是Experience Manager的標準使用者介面。 Adobe推出觸控式UI，搭配 [回應式設計](/help/sites-authoring/responsive-layout.md) ，以製作環境。 觸控式UI是專為觸控式和桌上型裝置而設計。 介面與原始的傳統UI有很大不同。

![觸控式使用者介面中的RTF編輯器工具列](assets/chlimage_1-35.png)

*圖：觸控式UI中的RTF編輯器工具列*

![傳統UI中的RTF編輯器工具列](assets/rtedefault.png)

*圖：傳統UI中的RTF編輯器工具列*

>[!MORELIKETHIS]
>
>* [UI建議](/help/sites-deploying/ui-recommendations.md)
>* 關於淘汰傳統UI，請參閱 [Experience Manager6.5發行說明](/help/release-notes/deprecated-removed-features.md)
>* 如需UI之間的差異，請參閱 [Touch UI和傳統UI](https://aemcq5pedia.wordpress.com/2018/01/05/touch-enabled-ui-aem6-3/)
>* 若要詳細了解啟用觸控的UI，請參閱 [Experience Manager觸控式UI的概念](/help/sites-developing/touch-ui-concepts.md)


## 各種編輯模式 {#editingmodes}

作者可以使用不同的元件模式，在Experience Manager中建立和編輯文字內容。 用於編寫和格式化內容的工具列選項以及不同編輯模式下啟用RTE的元件的用戶體驗，會因RTE配置而異。

| 編輯模式 | 編輯區域 | 要啟用的建議功能 | 觸控式 UI | 傳統 UI |
|--- |--- |--- |--- |--- |
| 內嵌 | 就地編輯，以快速、微幅編輯；不開啟對話框的格式 | 最小RTE功能 | Y | Y |
| RTE全螢幕 | 涵蓋整個頁面 | 所有必要的RTE功能 | Y | N |
| 對話方塊 | 對話方塊，但不涵蓋整個頁面 | 傳統UI中所有必要的RTE功能；審慎啟用觸控式UI中的功能 | Y | Y |
| 全螢幕對話方塊 | 與全螢幕模式相同；包含與RTE一起顯示的對話框欄位 | 所有必要的RTE功能 | Y | N |

>[!NOTE]
>
>在觸控式UI的內嵌編輯模式中，無法使用來源編輯功能。 您無法以全螢幕模式拖曳影像。 所有其他功能都可在所有模式中運作。

### 內嵌編輯 {#inline-editing}

開啟時（按兩下/按一下速度緩慢），您可以在頁面內編輯內容。 提供了一個緊湊的工具欄，其中包含非常基本的選項。

![在觸控式UI中與基本工具列內嵌編輯](assets/chlimage_1-36.png)

*圖：在觸控式UI中與基本工具列內嵌編輯*

在傳統UI中，按兩下元件時速度緩慢，可進行內嵌編輯，而橘色外框會醒目顯示內容。 如果「內容尋找器」已開啟，則視窗頂端會顯示包含可用RTE格式選項的工具列。 如果「內容尋找器」未開啟，則不會顯示格式選項，您只能編輯基本文字。

### 全螢幕編輯 {#full-screen-editing}

Experience Manager元件可以以全螢幕檢視開啟，隱藏頁面內容並佔據可用螢幕。 請考慮以全螢幕編輯詳細的內嵌編輯版本，因為它提供最多的編輯選項。 可按一下 ![rte_fullscreen](assets/rte_fullscreen.png)，即可在使用內嵌編輯模式時從緊密工具列取得。

在對話框全螢幕模式中，以及詳細的RTE工具欄，還可以使用對話框中可用的選項和元件。 此變數僅適用於包含RTE與其他元件的對話方塊。

![在觸控式UI中以全螢幕模式編輯時，詳細的RTE工具列](assets/chlimage_1-37.png)

*圖：在觸控式UI中以全螢幕模式編輯時，詳細的RTE工具列*

### 對話方塊編輯 {#dialog-editing}

按兩下元件時，將開啟用於編輯內容的對話框。 對話框將在現有頁面的頂部開啟。 在某些特定情況下，對話方塊會以快顯視窗的形式開啟。 例如，當文本元件是多列頁面佈局中列的一部分時，對話框的可用區域較小。

![在觸控式UI中編輯對話方塊模式](assets/dialog_editing_modetouchui.png)

*圖：在觸控式UI中編輯對話方塊模式*

![傳統UI中包含編輯詳細工具列的對話框](assets/chlimage_1-38.png)

*圖：傳統UI中包含編輯詳細工具列的對話框*

## 關於RTE外掛程式和相關功能 {#aboutplugins}

此功能可透過一系列外掛程式提供，每個外掛程式都具備：

* A `features` 屬性：

   * 用於啟用或停用該外掛程式的基本功能
   * 可使用標準化程式來設定

* 需要專門配置的其他屬性和選項（如適用）。

RTE的基本功能會由 `features` 屬性。

下表列出目前的外掛程式，顯示：

* 具有API檔案連結的外掛程式ID。 當 [啟用外掛程式](/help/sites-administering/configure-rich-text-editor-plug-ins.md#activateplugin).
* 允許的值 `features` 屬性。
* 外掛程式所提供功能的說明。

| 外掛程式ID | 功能 | 說明 |
|--- |--- |--- |
| 編輯 | 剪下複製貼上 — 預設貼上 — plaintext paste-wordhtml | [剪下、複製和三種貼上模式](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles). |
| [芬德雷普萊斯](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FindReplacePlugin) | 查找替換 | 查找和替換。 |
| [格式](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.FormatPlugin) | 粗體斜體下划線 | [基本文字格式](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles). |
| [影像](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ImagePlugin) | 影像 | 基本影像支援（從內容或內容尋找器拖曳）。 根據瀏覽器，支援對作者有不同的行為 |
| [鍵](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.KeyPlugin) |  | 若要定義此值，請參閱 [標籤大小](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tabsize). |
| [證明](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.JustifyPlugin) | justifleft justifycenter justifyright | 段落對齊。 |
| [連結](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.LinkPlugin) | 修改連結取消連結錨點 | [超連結和錨點](/help/sites-administering/configure-rich-text-editor-plug-ins.md#linkstyles). |
| [清單](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.ListPlugin) | 已訂購的縮進 | 此外掛程式可同時控制 [縮排和清單](/help/sites-administering/configure-rich-text-editor-plug-ins.md#indentmargin);包括巢狀清單。 |
| [miscools](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.MiscToolsPlugin) | specialchars sourceedit | 其他工具可讓作者輸入 [特殊字元](/help/sites-administering/configure-rich-text-editor-plug-ins.md#spchar) 或編輯HTML來源。 此外，您也可以新增整個 [特殊字元範圍](/help/sites-administering/configure-rich-text-editor-plug-ins.md#definerangechar) 如果您想定義自己的清單。 |
| Paraformat | paraformat | 預設段落格式為段落、標題1、標題2和標題3(`<p>`, `<h1>`, `<h2>`，和 `<h3>`)。 您可以 [添加更多段落格式](/help/sites-administering/configure-rich-text-editor-plug-ins.md#paraformats) 或擴充清單。 |
| 拼字檢查 | 核取文字 | [語言感知拼寫檢查程式](/help/sites-administering/configure-rich-text-editor-plug-ins.md#adddict). |
| 樣式 | 樣式 | 支援使用CSS類別的樣式。 [新增文字樣式](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles) 如果您想要新增（或擴充）您自己的樣式範圍以搭配文字使用。 |
| 上標 | 下標上標 | 基本格式的擴充功能，新增子指令碼和超指令碼。 |
| 表格 | 表remotetable insertrow removerow insertcolumn removecolumn cellprops mergells sliptcellselectrow選擇列 | 請參閱 [配置表格樣式](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tablestyles)，若要為整個表格或個別儲存格新增您自己的樣式。 |
| 復原 | 撤消重做 | 歷史記錄大小 [還原和重做](/help/sites-administering/configure-rich-text-editor-plug-ins.md#undohistory) 操作。 |

>[!NOTE]
>
>對話方塊模式中不支援全螢幕外掛程式。 使用 `dialogFullScreen` 設定，以設定全螢幕模式的工具列。

## 了解設定路徑和位置 {#understand-the-configuration-paths-and-locations}

此 [RTE編輯模式（和UI）](#editingmodes) 提供給作者的設定，會在您 [啟用RTE外掛程式](/help/sites-administering/configure-rich-text-editor-plug-ins.md#activateplugin):

| 編輯模式 | 觸控式UI的位置 | 傳統UI的位置 |
|---|---|---|
| 內嵌 | `cq:editConfig/cq:inplaceEditing` | `cq:editConfig/cq:inplaceEditing` |
| 全螢幕 | `cq:editConfig/cq:inplaceEditing` | 不適用 |
| 對話方塊 | `cq:dialog` | `dialog` |
| 全螢幕對話方塊 | `cq:dialog` | 不適用 |

>[!NOTE]
>
>請勿將節點命名為 `cq:inplaceEditing` as `config`. 開啟 `cq:inplaceEditing` 節點，定義下列屬性：
>* **名稱**: `configPath`
>* **類型**: `String`
>* **值**:包含實際配置的節點的路徑

>
>請勿將RTE設定節點命名為 `config`. 否則，RTE設定只對管理員有效，對群組中的使用者無效 `content-author`.

設定下列僅適用於觸控式UI中對話方塊編輯模式的屬性：

* `useFixedInlineToolbar`:設定RTE節點上定義的此Boolean屬性(一個具有sling:resourceType= `cq/gui/components/authoring/dialog/richtext`) `True`，使RTE工具列固定而非浮動。

   此屬性為true時，RTF編輯預設會在「foundation-contentloaded」事件上啟動。

   若要防止此情況，請設定屬性 `customStart` to `True`並觸發「rte-start」事件以開始RTE編輯。 當此屬性為「true」時，預設行為（點擊時開始的rte）無法運作。

* `customStart`:將RTE節點上定義的此布林屬性設定為 `True`，透過觸發事件來控制何時啟動RTE `rte-start`.

* `rte-start`:在 `contenteditable-div` ，開始編輯RTE時。 只有在 `customStart` 已設為true。

在觸控式對話方塊中使用RTE時，請設定屬性 `useFixedInlineToolbar` 設為true是避免問題的必要項目。

## 就地自訂編輯 {#customizing-in-place-editing}

您可以設定下列屬性，以定義文字編輯器開始的HTML選取器：

* **`editElementQuery`**  — 定義於 `cq:InplaceEditingConfig`，此屬性可用來指定HTML元素的選取器，以便在其中開始內嵌編輯文字元件。 如果未指定，則直接在「文本元件」HTML上啟動內嵌編輯。
* **`textPropertyName`**  — 定義於 `cq:InplaceEditingConfig`，此屬性用於指定要儲存在內容節點上的屬性名稱，文字元件的HTML值在內嵌編輯後將保存在該節點上。

對話方塊模式的對應屬性為 `name`.

## 啟用外掛程式以啟用RTE功能 {#enable-rte-functionalities-by-activating-plug-ins}

可透過一系列外掛程式使用RTE功能，每個外掛程式都具有features屬性。 您可以配置features屬性，以啟用或停用每個外掛程式的各種功能。

如需RTE外掛程式的詳細設定，請參閱 [如何啟用和配置RTE外掛程式](/help/sites-administering/configure-rich-text-editor-plug-ins.md).

**範例**:下載 [此範例設定](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) 說明如何設定RTE。 在此包中，所有功能都已啟用。

>[!NOTE]
>
>此 [核心元件文字元件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor) 允許模板編輯器將GUI中的許多RTE插件配置為內容策略，而無需進行技術配置。 內容原則可搭配RTE UI設定使用，如本檔案所述。
>
>如需詳細資訊，請參閱 [RTE UI設定和內容原則](/help/sites-administering/rich-text-editor.md) 以及 [建立頁面範本](/help/sites-authoring/templates.md) 和 [核心元件開發人員檔案](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/developing.html).

>[!NOTE]
>
>如需參考，可在以下網址找到預設的文字元件（在標準安裝中提供）:
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`

>
>若要建立您自己的文字元件，請複製上述元件，而非編輯這些元件。

## 配置RTE工具欄 {#dialogfullscreen}

AEM可讓您針對不同的編輯模式，以不同方式設定RTF編輯器的介面。 預設設定如下。 您可以根據需求改寫這些預設值。 您只可自訂要提供給作者的工具列功能。 您不需要指定所有工具列組態。

若要為 `dialogFullScreen`，請使用下列範例設定。

```java
<uiSettings jcr:primaryType="nt:unstructured">
  <cui jcr:primaryType="nt:unstructured">
    <inline
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,#justify,#lists,links#modifylink,links#unlink,#paraformat]">
      <popovers jcr:primaryType="nt:unstructured">
        <justify
          jcr:primaryType="nt:unstructured"
          items="[justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify]"
          ref="justify"/>
        <lists
          jcr:primaryType="nt:unstructured"
          items="[lists#unordered,lists#ordered,lists#outdent,lists#indent]"
          ref="lists"/>
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </inline>
    <dialogFullScreen
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify,lists#unordered,lists#ordered,lists#outdent,lists#indent,links#modifylink,links#unlink,table#createoredit,#paraformat,image#imageProps]">
      <popovers jcr:primaryType="nt:unstructured">
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </dialogFullScreen>
    <tableEditOptions
      jcr:primaryType="nt:unstructured"
      toolbar="[table#insertcolumn-before,table#insertcolumn-after,table#removecolumn,-,table#insertrow-before,table#insertrow-after,table#removerow,-,table#mergecells-right,table#mergecells-down,table#mergecells,table#splitcell-horizontal,table#splitcell-vertical,-,table#selectrow,table#selectcolumn,-,table#ensureparagraph,-,table#modifytableandcell,table#removetable,-,undo#undo,undo#redo,-,table#exitTableEditing,-]">
    </tableEditOptions>
  </cui>
</uiSettings>
```

內嵌模式和全螢幕模式會使用不同的UI設定。 工具欄屬性用於指定工具欄的按鈕。

例如，如果按鈕本身是功能(例如 `Bold`)，則會指定為 `PluginName#FeatureName` (例如， `links#modifylink`)。

如果按鈕是彈出視窗（包含外掛程式的某些功能），則會指定為 `#PluginName` (例如， `#format`)。

分隔符號(`|`)，可以使用 `-`.

內嵌或全螢幕模式下的快顯視窗節點包含所使用游標的清單。 「瀏覽器」節點下的每個子節點都以外掛程式（例如格式）命名。 其屬性為「項目」，包含外掛程式的功能清單（例如format#bold）。

## RTE使用者介面設定和內容原則 {#rtecontentpolicies}

管理員可以使用內容原則來控制RTE選項，例如，不必如上所述執行設定。 內容原則會定義元件在 [可編輯的範本](/help/sites-authoring/templates.md). 例如，如果使用RTE的文本元件與可編輯的模板一起使用，則內容策略可以定義粗體選項可用，並可以定義幾個段落格式選項。 內容原則可重複使用，可套用至多個範本。

RTE中的可用選項從用戶介面配置流向內容策略。

* 用戶介面配置設定定義了哪些選項可用於內容策略。
* 如果RTE的用戶介面配置已刪除或未啟用項目，則內容策略無法配置它。
* 作者只能存取使用者介面設定和內容原則所提供的功能。

例如，您可以看到 [文字核心元件檔案](https://docs.adobe.com/help/en/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor).

## 自定義工具欄表徵圖和命令之間的映射 {#iconstoolbar}

您可以自訂RTE工具列上顯示的珊瑚圖示和可用命令之間的對應。 除了Coral圖示，您無法使用其他任何圖示。

1. 建立名為的節點 `icons` 在 `uiSettings/cui`.

1. 為其下的各個表徵圖建立節點。
1. 在每個個別圖示節點上，指定一個Coral圖示和一個命令來對應該圖示。

以下是將命令Bold對應至Coral圖示的范常式式碼片段，命名為 `textItalic`.

```java
<text jcr:primaryType="nt:unstructured" sling:resourceType="cq/gui/components/authoring/dialog/richtext" name="./text" useFixedInlineToolbar="{Boolean}true">
    <rtePlugins jcr:primaryType="nt:unstructured">
        <format jcr:primaryType="nt:unstructured" features="bold,italic"/>
    </rtePlugins>
    <uiSettings jcr:primaryType="nt:unstructured">
        <cui jcr:primaryType="nt:unstructured">
            <inline jcr:primaryType="nt:unstructured"
                toolbar="[format#bold,format#italic,format#underline,links#modifylink,links#unlink]">
            </inline>
            <icons jcr:primaryType="nt:unstructured">
                <bold jcr:primaryType="nt:unstructured"
                    command="format#bold"
                    icon="textItalic"/>
            </icons>
        </cui>
    </uiSettings>
</text>
```

## 切換至CoralUI 2 RTF編輯器 {#switch-to-coralui-rich-text-editor}

在頁面上，您可以包含CoralUI 2 RTE clientlib或CoralUI 3 RTE clientlib。 依預設，RTF編輯器包含CoralUI 3 RTE clientlib。 若要切換至CoralUI 2 RTE，請執行下列步驟。

>[!NOTE]
>
>Adobe不建議將其作為最佳實務。 切換至CoralUI 2 RTE作為最後手段。 如果外掛程式不依賴RTE內部（例如類別）,CoralUI 2 RTE的自訂外掛程式可與CoralUI 3 RTE搭配使用。
>
>如果您使用CoralUI3 RTE的自訂外掛程式，請使用 `rte.coralui3` 程式庫。


1. 覆蓋節點 `/libs/cq/gui/components/authoring/editors/clientlibs/core` 在 `/apps`，並執行下列動作：

   * 取代 `rte.coralui3` with `rte.coralui2` （依賴項屬性）。
   * 取代 `cq.authoring.editor.core.inlineediting.rte.coralui3` with `cq.authoring.editor.core.inlineediting.rte.coralui2` 內嵌屬性。
   * 取代 `cq.authoring.rte.coralui3` with `cq.authoring.rte.coralui2` 內嵌屬性。

1. 覆蓋節點 `/libs/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui3` 和 `/libs/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui2` 在 `/apps`.

   移除類別 `cq.authoring.dialog` 從 `/apps/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui3` 並將其添加到 `/apps/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui2`.

1. 變更包含在頁面上的任何其他相依性，從 `rte.coralui3` to `rte.coralui2`. 例如，在覆蓋節點後 `/libs/mcm/campaign/components/touch-ui/clientlibs/rte` 在 `/apps`，從 `rte.coralui3` to `rte.coralui2`.

1. 覆蓋節點 `cq/ui/widgets` 在 `/apps`. 取代相依性 `cq.rte` 在節點 `/apps/cq/ui/widgets` with `cq.coralui2.rte`.

>[!NOTE]
>
>CoralUI 2 RTE使用handlebars範本進行外掛程式對話。 因此，CoralUI 2 RTE clientlib對handlebars clientlib有相依性。 CoralUI 3 RTE不使用handlebars範本，且沒有任何相關的相依性。 如果您的自訂外掛程式使用handlebars範本，請在網頁中加入handlebars clientlib。

## 更多資訊 {#further-information}

如需設定RTE的詳細資訊，請參閱 [AEM Widget API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.RichText) 參考。

尤其要查看可用的外掛程式和相關選項：

* 此 [CQ.form.RichText](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin) 元件提供用於編輯已設定樣式的文本資訊(rtf)的表單欄位。 若要了解RTF表單可用的所有參數，請參閱設定選項。
* RtfText元件使用下列外掛程式，提供多種功能： [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin). 對於每個外掛程式：

   * 如需可啟用（或停用）功能的詳細資訊，請參閱功能
   * 如需適當外掛程式的詳細設定，請參閱設定選項以取得所有可用參數

* 也提供連結HTML規則的詳細資訊。

這些功能可用來擴充和自訂您自己的RTE。 例如，若要在建立連結時列出頁面中可用的錨點，您可以提供您自己的實作 `LinkPlugin`.

## 已知限制 {#known-limitations}

AEM RTE功能有下列限制：

* 只有AEM元件對話方塊才支援RTE功能。 嚮導或Foundation表單(如 [頁面屬性](/help/sites-developing/page-properties-views.md) 和 [支架](/help/sites-authoring/scaffolding.md) 在觸控式UI上。

* AEM無法使用 [混合裝置](/help/release-notes/release-notes.md).

* 不要為RTE配置節點命名 `config`. 否則，RTE設定只對管理員有效，對群組中的使用者無效 `content-author`.

* RTE不支援內嵌框架或iframe來內嵌內容。

## 最佳實務與秘訣 {#best-practices-and-tips}

* 僅啟用浮動對話方塊的外掛程式，不需要彈出視窗。 不含快顯視窗的外掛程式大小較小，最適合浮動式對話。
* 使用較大的快顯視窗啟用外掛程式，例如 `Paste` 外掛程式，僅限以全螢幕對話方塊模式或全螢幕模式。 具有大型快顯視窗的外掛程式需要更多螢幕空間，才能提供良好的製作體驗。
* 如果您使用CoralUI3 RTE的自訂外掛程式，請使用 `rte.coralui3` 程式庫。

## 疑難排解RTE的常見問題 {#troubleshoot-issues-with-aem-rich-text-editor}

**如何選取多個表格儲存格？**

若要選取表格中的多個儲存格，請按 `Ctrl` 或 `Cmd` 鍵，然後按一下表格儲存格。

現在對選取項目執行操作，例如設定所選儲存格的屬性。

**使用「設定」按鈕編輯元件時，會遺失超連結**

使用「配置」按鈕編輯文本元件，在其中添加超連結。 再次編輯超連結並第二次驗證超連結時，可能會丟失超連結。

因應措施是在第二次顯示編輯對話方塊時按一下文字元件，然後執行連結驗證。

此問題已在AEM 6.3及更新版本中解決。

**HTML在來源編輯模式中新增的內容會遺失**

請勿新增容易發生XSS的HTML。 AEM（而非RTE）可移除某些HTML內容，以遵守XSS反向連結規則。

要驗證貼上的HTML是否已保存，請檢查CRXDE（在內容節點中）中保存的內容。

如果未儲存，則HTML必須已由RTE移除，因為它未遵守RTE的規則。

若儲存在CRXDE中，但未呈現在頁面上(若要檢查呈現，請參閱頁面的 [預覽](/help/sites-authoring/editing-content.md#preview-mode)，則會由AEM XSS規則移除。

**多欄位元件未如預期運作**

若要建立多欄位元件，請只使用CoralUI 3。 請勿使用CoralUI 2元件對話方塊。

此外，請確認您的多欄位實作程式碼和節點結構正確無誤。

**可供管理員使用的設定無法供作者使用**

如果系統為管理員反映介面設定更新，但作者帳戶未反映，請確定未命名設定節點 `config`. 使用 [`configPath` 屬性](/help/sites-developing/components-basics.md#cq-inplaceediting).

>[!MORELIKETHIS]
>
>* [設定RTE外掛程式](configure-rich-text-editor-plug-ins.md)
>* [使用RTF編輯器進行編寫](../sites-authoring/rich-text-editor.md)
>* [為可存取的網站配置RTE](rte-accessible-content.md)
>* [Touch UI與傳統UI功能比較](../release-notes/touch-ui-features-status.md)
>* [建立複合多欄位元件的教學課程範例](https://experience-aem.blogspot.com/2019/05/aem-65-touchui-composite-multifield-with-coral3-rte-rich-text.html)

