---
title: 為多個就地編輯器設定RTE。
description: 透過設定RTF編輯器，在Adobe Experience Manager中建立多個就地編輯器。
contentOwner: AG
exl-id: 03030317-8b7d-408a-bdfd-619824d7260c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 2%

---

# 配置多個就地編輯器 {#configure-multiple-in-place-editors}

您可以在Adobe Experience Manager中設定RTF編輯器，使其具有多個就地編輯器。 設定後，您可以選取適當的內容並開啟適當的編輯器。

![特定就地編輯器](assets/rte-inplace-editor.png)

## 配置多個編輯器 {#configure-multiple-editors}

若要啟用多個就地編輯器，請 `cq:InplaceEditingConfig` 節點類型已透過 `cq:ChildEditorConfig` 節點類型。

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

若要設定多個編輯器，請依照下列步驟操作：

1. 在節點上 `cq:inplaceEditing` （類型） `cq:InplaceEditingConfig`)定義下列屬性：

   * 名稱:`editorType`
   * 類型: `String`
   * 值: `hybrid`

1. 在此節點下，建立一個節點：

   * 名稱: `cq:ChildEditors`
   * 類型: `nt:unstructured`

1. 在 `cq:childEditors` 節點，為每個就地編輯器建立一個節點：

   * 名稱：每個節點的名稱是它所代表的屬性的名稱，刪除目標的情況也是如此。 例如， `image` 和 `text`.
   * 類型: `cq:ChildEditorConfig`

   >[!NOTE]
   >
   >定義的放置目標與子編輯器之間存在關聯。 的名稱 `cq:ChildEditorConfig` 節點會視為放置目標ID，以用作所選子編輯器的參數。 如果可編輯的子區域沒有拖放目標（例如，在文本元件中），則子編輯器的名稱仍被視為標識相應可編輯區域的ID。

1. 在這些節點上(`cq:ChildEditorConfig`)定義屬性：

   * 名稱: `type`.
   * 值：註冊就地編輯的名稱；例如， `image` 和 `text`.

   * 名稱: `title`.
   * 值：可用編輯器的元件選擇清單中顯示的標題。 例如， `Image` 和 `Text`.

### RTF編輯器的其他設定 {#additional-configuration-for-rich-text-editors}

多個RTF編輯器的設定稍有不同，因為您可以個別設定每個RTE例項。 如需詳細資訊，請參閱 [設定RTF編輯器](/help/sites-administering/rich-text-editor.md). 若要讓多個RTE為每個就地RTE建立設定。 Adobe建議在下建立新配置節點 `cq:InplaceEditingConfig` 因為每個RTE都可以有不同的設定。 在新節點下，建立每個個別RTE設定。

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
>但若為RTE, `configPath` 元件中只有一個文字編輯器例項（可編輯的子區域）時，即支援屬性。 此用途 `configPath` 提供以支援與元件之舊版使用者介面對話方塊的回溯相容性。

>[!CAUTION]
>
>請勿將RTE設定節點命名為 `config`. 否則，RTE設定只能供管理員使用，而不能供群組中的使用者使用 `content-author`.

## 程式碼範例 {#code-samples}

您可以在上找到此頁面的程式碼 [在GitHub上執行aem-authoring-hybrideditors專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors). 您可以將完整專案下載為 [郵遞區號封存](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip).

## 新增就地編輯器 {#add-an-in-place-editor}

有關添加就地編輯器的一般資訊，請參見該文檔 [自訂頁面製作](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor).

>[!MORELIKETHIS]
>
>* [在Experience Manager中設定RTF編輯器](/help/sites-administering/rich-text-editor.md).

