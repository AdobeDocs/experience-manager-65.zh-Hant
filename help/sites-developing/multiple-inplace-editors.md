---
title: 為多個就地編輯器配置RTE。
description: 在Adobe Experience Manager中設定Rich Text Editor，以建立多個就地編輯器。
contentOwner: AG
translation-type: tm+mt
source-git-commit: e49411a99a80e91c983afc103a8ea826e75569b8
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 2%

---


# 設定多個就地編輯器{#configure-multiple-in-place-editors}

您可以在Adobe Experience Manager中設定Rich Text Editor，讓它擁有多個就地編輯器。 配置後，您可以選擇適當的內容並開啟相應的編輯器。

![特定就地編輯器](assets/rte-inplace-editor.png)

## 配置多個編輯器{#configure-multiple-editors}

要啟用多個就地編輯器，`cq:InplaceEditingConfig`節點類型的結構已通過`cq:ChildEditorConfig`節點類型的定義得到增強。

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

若要設定多個編輯器，請依照下列步驟進行：

1. 在節點`cq:inplaceEditing`（類型`cq:InplaceEditingConfig`）上定義以下屬性：

   * 名稱:`editorType`
   * 類型: `String`
   * 值: `hybrid`

1. 在此節點下，建立一個節點：

   * 名稱: `cq:ChildEditors`
   * 類型: `nt:unstructured`

1. 在`cq:childEditors`節點下，為每個就地編輯器建立一個節點：

   * 名稱：每個節點的名稱是它所代表的屬性的名稱，drop目標的情況也是如此。 例如，`image`和`text`。
   * 類型: `cq:ChildEditorConfig`

   >[!NOTE]
   >
   >已定義的放置定位與子編輯器之間有關聯。 `cq:ChildEditorConfig`節點的名稱被視為放置目標ID，用作選定子編輯器的參數。 如果可編輯的子區域沒有放置目標（例如，在文本元件中），則子編輯器的名稱仍被視為標識相應可編輯區域的ID。

1. 在這些節點(`cq:ChildEditorConfig`)中，定義屬性：

   * 名稱: `type`.
   * 值：註冊就地編輯器的名稱；例如，`image`和`text`。

   * 名稱: `title`.
   * 值：顯示在可用編輯器元件選擇清單中的標題。 例如，`Image`和`Text`。

### Rich Text Editors {#additional-configuration-for-rich-text-editors}的其他設定

多個Rich Text Editor的設定略有不同，因為您可以個別設定每個RTE例項。 如需詳細資訊，請參閱[設定Rich Text Editor](/help/sites-administering/rich-text-editor.md)。 要讓多個RTE為每個就地RTE建立配置，請執行以下操作： Adobe建議在`cq:InplaceEditingConfig`下建立新配置節點，因為每個RTE都可以有不同的配置。 在新節點下，建立每個單獨的RTE配置。

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
>但是，對於RTE，當元件中只有一個文本編輯器實例（可編輯的子區域）時，支援`configPath`屬性。 此`configPath`的使用可支援與元件較舊的使用者介面對話方塊向後相容。

>[!CAUTION]
>
>不要將RTE配置節點命名為`config`。 否則，RTE配置僅對管理員可用，對組`content-author`中的用戶不可用。

## 程式碼範例{#code-samples}

您可以在GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors)的[aem-authoring-hybrideditors專案中找到此頁面的程式碼。 您可以將完整的專案下載為[a ZIP archive](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip)。

## 新增就地編輯器{#add-an-in-place-editor}

有關添加就地編輯器的一般資訊，請參閱文檔[自定義頁面編寫](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor)。

>[!MORELIKETHIS]
>
>* [在Experience Manager中設定Rich Text Editor](/help/sites-administering/rich-text-editor.md)。

