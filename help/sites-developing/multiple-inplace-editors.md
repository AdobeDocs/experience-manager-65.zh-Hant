---
title: 為多個就地編輯器設定RTE。
description: 透過設定RTF編輯器，在Adobe Experience Manager中建立多個就地編輯器。
contentOwner: AG
exl-id: 03030317-8b7d-408a-bdfd-619824d7260c
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 1%

---

# 設定多個就地編輯器 {#configure-multiple-in-place-editors}

您可以在Adobe Experience Manager中設定RTF編輯器，使其有多個就地編輯器。 設定後，您可以選取適當的內容並開啟適當的編輯器。

![特定的就地編輯器](assets/rte-inplace-editor.png)

## 設定多個編輯器 {#configure-multiple-editors}

啟用多個就地編輯器的結構 `cq:InplaceEditingConfig` 節點型別已增強，其定義為 `cq:ChildEditorConfig` 節點型別。

例如：

```js
   /**
       * Configures in-place editing of a component.
       *
       * @prop active true to activate in-place editing for the component.
       * @prop editorType ID of in-place editor to use.
       * @prop cq:childEditors collection of {@link cq:ChildEditorConfig} nodes.
       * @prop configPath path to editor's config (optional).
       * @node config editor's config (used if no configPath is specified; optional).
     */
    [cq:InplaceEditingConfig] > nt:unstructured
      - active (boolean)
      - editorType (string)
      + cq:childEditors (nt:base) = nt:unstructured
      - configPath (string)
      + config (nt:unstructured) = nt:unstructured

    /**
      * Configures one child editor for a sub-component. The name of the this node is
      * used as DD ID.
      *
      * @prop type type of the inline editor. For example, ["image"].
      * @prop title Title of the inline editor.
      * @prop icon Icon to represent the inline editor.
    */
    [cq:ChildEditorConfig] > nt:unstructured
      orderable
      - type (string)
      - title (string)
```

若要設定多個編輯器，請遵循下列步驟：

1. 在節點上 `cq:inplaceEditing` (型別 `cq:InplaceEditingConfig`)定義下列屬性：

   * 名稱：`editorType`
   * 類型：`String`
   * 值： `hybrid`

1. 在此節點下方，建立節點：

   * 名稱：`cq:ChildEditors`
   * 類型：`nt:unstructured`

1. 在 `cq:childEditors` 節點，為每個就地編輯器建立一個節點：

   * 名稱：每個節點的名稱是它所代表的屬性名稱，拖放目標也是如此。 例如， `image` 和 `text`.
   * 類型：`cq:ChildEditorConfig`

   >[!NOTE]
   >
   >定義的放置目標和子編輯器之間存在關聯。 的名稱 `cq:ChildEditorConfig` 會將節點視為放置目標ID，以作為所選子編輯器的引數。 如果可編輯的子區域沒有放置目標（例如在文字元件中），則子編輯器的名稱仍會被視為ID，以識別對應的可編輯區域。

1. 在每個節點上(`cq:ChildEditorConfig`)定義屬性：

   * 名稱： `type`.
   * 值：已登入就地編輯器的名稱；例如， `image` 和 `text`.

   * 名稱： `title`.
   * 值：在可用編輯器的元件選取範圍清單中顯示的標題。 例如， `Image` 和 `Text`.

### RTF編輯器的其他設定 {#additional-configuration-for-rich-text-editors}

多個RTF編輯器的設定稍有不同，因為您可以分別設定每個個別RTE執行個體。 如需詳細資訊，請參閱 [設定RTF編輯器](/help/sites-administering/rich-text-editor.md). 若要有多個RTE，請為每個就地RTE建立設定。 Adobe建議在下方建立新的設定節點 `cq:InplaceEditingConfig` 因為每個個別RTE可以有不同的設定。 在新節點下，建立每個單獨的RTE配置。

```xml
    texttext
        cq:dialog
        cq:editConfig
            cq:inplaceEditing
                cq:childEditors
                    someconfig
                        text1
                            rtePlugins
                        text2
                            rtePlugins
```

>[!NOTE]
>
>但若為RTE，則 `configPath` 當元件中只有一個文字編輯器的例項（可編輯的子區域）時，支援屬性。 此用法 `configPath` 提供的目的是支援與元件的舊版使用者介面對話方塊的回溯相容性。

>[!CAUTION]
>
>不要將RTE設定節點命名為 `config`. 否則，RTE設定僅供管理員使用，不適用於群組內的使用者 `content-author`.

## 程式碼範例 {#code-samples}

您可以在此頁面找到程式碼： [GitHub上的aem-authoring-hybrideditors專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors). 您可以將完整專案下載為 [ZIP封存](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip).

## 新增就地編輯器 {#add-an-in-place-editor}

如需新增就地編輯器的一般資訊，請參閱檔案 [自訂頁面製作](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor).

>[!MORELIKETHIS]
>
>* [在Experience Manager中設定RTF編輯器](/help/sites-administering/rich-text-editor.md).
