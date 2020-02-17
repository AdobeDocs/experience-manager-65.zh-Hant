---
title: 根據使用的範本顯示元件
seo-title: 根據使用的範本顯示元件
description: 當您建立表單時，請瞭解如何根據選取的範本啟用側邊欄中的元件。
seo-description: 當您建立表單時，請瞭解如何根據選取的範本啟用側邊欄中的元件。
uuid: 790d201b-318d-4d02-9bc5-9d6bc41d057a
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
content-type: reference
discoiquuid: f658da57-0134-4458-9ef9-a99787b66742
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247

---


# 根據使用的範本顯示元件{#displaying-components-based-on-the-template-used}

當表單作者使用範本建立最適化表 [單](../../forms/using/template-editor.md)，表單作者可以根據範本原則查看和使用特定元件。 您可以指定範本內容原則，讓您選擇表單作者在表單製作時看到的元件群組。

## 變更範本的內容原則 {#changing-the-content-policy-of-a-template}

建立模板時，該模板將在內容儲存庫 `/conf` 中建立。 根據您在目錄中建立的檔案 `/conf` 夾，模板的路徑為： `/conf/<your-folder>/settings/wcm/templates/<your-template>`。

請執行下列步驟，根據範本的內容原則，在側欄中顯示元件：

1. 開啟CRXDE lite。\
   URL: `https://<server>:<port>/crx/de/index.jsp`
1. 在CRXDE中，導航到建立模板的資料夾。

   例如： `/conf/<your-folder>/`

1. 在CRXDE中，導覽至： `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/`

   若要選取一組元件，需要新的內容原則。 若要建立新原則，請複製並貼上預設原則，然後重新命名。

   預設內容原則的路徑為： `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/default`

   在資料 `gridFluidLayout` 夾中，複製並貼上預設原則並重新命名。 例如， `myPolicy`。

   ![複製預設策略](assets/crx-default1.png)

1. 選取您建立的新原則，並在具有 **類型的右側** 面板中選取元件屬性 `string[]`。

   選擇並開啟元件屬性後，將看到「編輯元件」對話框。 「編輯元件」對話方塊可讓您使用+和——按鈕來新增或 **移除元** 件 **群組** 。 您可以新增元件群組，其中包含您希望作者使用之元件。

   ![在策略中添加或刪除元件](assets/add-components-list1.png)

   新增元件群組後，按一下「 **確定** 」以更新清單，然後按一下CRXDE位址列上方的「全 **部儲存** 」並重新整理。

1. 在範本中，將內容原則從預設變更為您建立的新原則。 (在 `myPolicy` 此範例中)。

   要更改策略，請在CRXDE中導航至 `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/guideContainer/rootPanel/items`。

   在屬 `cq:policy` 性中， `default` 更改為新策略名稱( `myPolicy`)。

   ![更新的範本內容原則](assets/updated-policy.png)

   當您使用範本建立表單時，可在側欄中看到新增的元件。

