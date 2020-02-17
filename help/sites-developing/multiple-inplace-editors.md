---
title: 設定多個就地編輯器
seo-title: 設定多個就地編輯器
description: 您可以設定元件，讓元件擁有多個就地編輯器
seo-description: 您可以設定元件，讓元件擁有多個就地編輯器
uuid: 4abbfcd5-fe1b-4c02-b115-97db20e60e1e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 0fac1e4a-f08f-4c46-b070-cb1d5a05b6e0
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71

---


# 設定多個就地編輯器{#configuring-multiple-in-place-editors}

您可以設定元件，讓元件在觸控式UI中擁有多個就地編輯器。

配置後，您可以選擇適當的內容並開啟相應的編輯器。 例如：

![chlimage_1-8](assets/chlimage_1-8a.png)

## 設定多個編輯器 {#configuring-multiple-editors}

為了啟用多個就地編輯器，節點類 `cq:InplaceEditingConfig` 型的結構已通過節點類型的定 `cq:ChildEditorConfig` 義得到增強。

例如：

```
   /**
       * Configures inplace editing of a component.
       *
       * @prop active true to activate inplace editing for the component
       * @prop editorType ID of inplace editor to use
       * @prop cq:childEditors collection of {@link cq:ChildEditorConfig} nodes.
       * @prop configPath path to editor's config (optional)
       * @node config editor's config (used if no configPath is specified; optional)
     */
    [cq:InplaceEditingConfig] > nt:unstructured
      - active (boolean)
      - editorType (string)
      + cq:childEditors (nt:base) = nt:unstructured
      - configPath (string)
      + config (nt:unstructured) = nt:unstructured

    /**
      * Configures one child editor for a subcomponent. The name of the this node will
      * be used as DD id.
      *
      * @prop type type of the inline editor. eg: ["image"]
      * @prop title totle od the inline editor
      * @prop icon icon to represent the inline editor
    */
    [cq:ChildEditorConfig] > nt:unstructured
      orderable
      - type (string)
      - title (string)
```

若要設定多個編輯器：

1. 在節點( `cq:inplaceEditing` 類型)上 `cq:InplaceEditingConfig`定義屬性：

   * 名稱:`editorType`
   * 類型: `String`
   * 值: `hybrid`

1. 在此節點下，建立新節點：

   * 名稱: `cq:ChildEditors`
   * 類型: `nt:unstructured`

1. 在節點 `cq:childEditors` 下為每個就地編輯器建立新節點：

   * 名稱：每個節點的名稱應是它所代表的屬性的名稱（與drop目標一樣）。 例如， `image`, `text`。
   * 類型：cq: `ChildEditorConfig`
   >[!NOTE]
   >
   >已定義的放置定位與子編輯器之間有關聯。 節點的名 `cq:ChildEditorConfig` 稱將被視為刪除目標ID，用作選定子編輯器的參數。 如果可編輯的子區域沒有放置目標（例如與文本元件一樣），則子編輯器的名稱仍被視為標識相應可編輯區域的ID。

1. 在這些節點( `cq:ChildEditorConfig`)上定義屬性：

   * 名稱: `type`
   * 值：註冊就地編輯器的名稱；例如 `image`, `text`

   * 名稱: `title`
   * 值：要顯示在元件選擇清單（可用編輯器）中的標題；例如 `Image`, `Text`

### Rich Text Editor的其他設定 {#additional-configuration-for-rich-text-editors}

多個Rich Text Editor的設定略有不同，因為您可以個別設定每個RTE例項。

>[!NOTE]
>
>如需詳細資訊，請 [參閱設定Rich Text編輯器](/help/sites-administering/rich-text-editor.md)。

要擁有多個RTE，您需要為每個就地RTE配置：

* 在「定 `cq:InplaceEditingConfig` 義節點」 `config` 下。

   * 在節點 `config` 下定義每個RTE配置。

```xml
    texttext
        cq:dialog
        cq:editConfig
            cq:inplaceEditing
                cq:childEditors
                    config
                        text1
                            rtePlugins
                        text2
                            rtePlugins
```

>[!NOTE]
>
>建議的最佳做法是定義下 `config` 的節點， `cq:InplaceEditingConfig` 因為每個RTE都可以有不同的配置。
>
>但是，對於RTE，當組 `configPath` 件中只有一個文本編輯器實例（可編輯子區域）時，支援該屬性。 此項使用可 `configPath` 支援與元件較舊的UI對話方塊向後相容。

## 程式碼範例 {#code-samples}

**GITHUB代碼**

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-hybridetors專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors)
* 將專案下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-hybrideditors/archive/master.zip)

## 新增就地編輯器 {#adding-an-in-place-editor}

有關添加就地編輯器的一般資訊，請參閱文檔自 [定義頁編輯](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor)。
