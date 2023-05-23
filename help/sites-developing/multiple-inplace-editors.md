---
title: 為多個就地編輯器配置RTE。
description: 通過配置富格文本編輯器在Adobe Experience Manager建立多個就地編輯器。
contentOwner: AG
exl-id: 03030317-8b7d-408a-bdfd-619824d7260c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 2%

---

# 配置多個就地編輯器 {#configure-multiple-in-place-editors}

您可以在Adobe Experience Manager配置富格文本編輯器，以便它具有多個就地編輯器。 配置後，您可以選擇適當的內容並開啟相應的編輯器。

![特定就地編輯器](assets/rte-inplace-editor.png)

## 配置多個編輯器 {#configure-multiple-editors}

啟用多個就地編輯器的結構 `cq:InplaceEditingConfig` 節點類型已隨著 `cq:ChildEditorConfig` 節點類型。

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

要配置多個編輯器，請執行以下步驟：

1. 在節點上 `cq:inplaceEditing` （類型） `cq:InplaceEditingConfig`)定義以下屬性：

   * 名稱:`editorType`
   * 類型: `String`
   * 值: `hybrid`

1. 在此節點下，建立一個節點：

   * 名稱: `cq:ChildEditors`
   * 類型: `nt:unstructured`

1. 下 `cq:childEditors` 節點，為每個就地編輯器建立一個節點：

   * 名稱：每個節點的名稱是它所表示的屬性的名稱，與刪除目標的情況一樣。 比如說， `image` 和 `text`。
   * 類型: `cq:ChildEditorConfig`

   >[!NOTE]
   >
   >定義的刪除目標與子編輯器之間存在關聯。 名稱 `cq:ChildEditorConfig` 節點被視為放置目標ID，用作選定子編輯器的參數。 如果可編輯子區域沒有放置目標，則子編輯器的名稱仍被視為標識相應可編輯區域的ID。

1. 在每個節點上(`cq:ChildEditorConfig`)定義屬性：

   * 名稱: `type`.
   * 值：註冊就地編輯器的名稱；比如說， `image` 和 `text`。

   * 名稱: `title`.
   * 值：在可用編輯器的元件選擇清單中顯示的標題。 比如說， `Image` 和 `Text`。

### 富格文本編輯器的其他配置 {#additional-configuration-for-rich-text-editors}

多個RTE編輯器的配置稍有不同，因為您可以單獨配置每個RTE實例。 有關詳細資訊，請參閱 [配置RTF編輯器](/help/sites-administering/rich-text-editor.md)。 要使多個RTE為每個就地RTE建立配置。 Adobe建議在下面建立新配置節點 `cq:InplaceEditingConfig` 因為每個RTE都可以有不同的配置。 在新節點下建立每個單獨的RTE配置。

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
>然而，對於RTE, `configPath` 當元件中只有一個文本編輯器實例（可編輯子區域）時，支援屬性。 此用途 `configPath` 支援向後相容元件的較舊用戶介面對話框。

>[!CAUTION]
>
>不要將RTE配置節點命名為 `config`。 否則，RTE配置僅對管理員可用，對組中的用戶不可用 `content-author`。

## 代碼示例 {#code-samples}

您可以在 [基於GitHub的em-authoring-hybridotors項目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors)。 您可以將整個項目下載為 [ZIP存檔](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip)。

## 添加就地編輯器 {#add-an-in-place-editor}

有關添加就地編輯器的一般資訊，請參閱文檔 [自定義頁面創作](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor)。

>[!MORELIKETHIS]
>
>* [在Experience Manager中配置RTF編輯器](/help/sites-administering/rich-text-editor.md)。

