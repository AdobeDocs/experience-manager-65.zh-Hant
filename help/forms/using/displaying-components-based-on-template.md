---
title: 根據使用的範本顯示元件
description: 建立表單時，瞭解如何根據選取的範本啟用側邊欄中的元件。
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
content-type: reference
docset: aem65
exl-id: 1fc56829-db81-4450-b1d8-b4a31110199e
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 1%

---

# 根據使用的範本顯示元件{#displaying-components-based-on-the-template-used}

表單作者使用建立最適化表單時 [範本](../../forms/using/template-editor.md)，表單作者就能根據範本原則檢視和使用特定元件。 您可以指定範本內容原則，以讓您選擇表單作者在表單製作時看到的元件群組。

## 變更範本的內容原則 {#changing-the-content-policy-of-a-template}

當您建立範本時，它會建立在 `/conf` 在內容存放庫中。 根據您在中建立的資料夾 `/conf` 目錄，範本的路徑為： `/conf/<your-folder>/settings/wcm/templates/<your-template>`.

執行以下步驟，根據範本的內容原則在側邊欄中顯示元件：

1. 開啟CRXDE Lite。\
   URL： `https://<server>:<port>/crx/de/index.jsp`
1. 在CRXDE中，導覽至建立範本的資料夾。

   例如：`/conf/<your-folder>/`

1. 在CRXDE中，導覽至： `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/`

   若要選取元件群組，需要新的內容原則。 若要建立原則，請複製並貼上預設原則，然後將其重新命名。

   預設內容原則的路徑為： `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/default`

   在 `gridFluidLayout` 資料夾，複製並貼上預設原則並重新命名。 例如，`myPolicy`。

   ![複製預設原則](assets/crx-default1.png)

1. 選取您建立的新原則，然後選取 **元件** 右側面板中的屬性（含型別） `string[]`.

   當您選取並開啟components屬性時，您會看到「編輯元件」對話方塊。 編輯元件對話方塊可讓您使用新增或移除元件群組。 **+** 和 **-** 按鈕。 您可以新增元件群組，其中包含您希望作者使用的元件。

   ![在原則中新增或移除元件](assets/add-components-list1.png)

   新增元件群組後，按一下 **確定** 以更新清單，然後按一下 **全部儲存** 在CRXDE位址列上方並重新整理。

1. 在範本中，將內容原則從預設變更為您建立的新原則。 ( `myPolicy` 在此範例中。)

   若要變更原則，請在CRXDE中導覽至 `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/guideContainer/rootPanel/items`.

   在 `cq:policy` 屬性，變更 `default` 到新原則名稱( `myPolicy`)。

   ![已更新範本內容原則](assets/updated-policy.png)

   當您使用範本製作表單時，可以在側邊欄中看到新增的元件。
