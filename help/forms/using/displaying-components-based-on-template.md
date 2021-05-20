---
title: 根據所使用的範本顯示元件
seo-title: 根據所使用的範本顯示元件
description: 建立表單時，了解如何根據選取的範本在側邊欄中啟用元件。
seo-description: 建立表單時，了解如何根據選取的範本在側邊欄中啟用元件。
uuid: 790d201b-318d-4d02-9bc5-9d6bc41d057a
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
content-type: reference
discoiquuid: f658da57-0134-4458-9ef9-a99787b66742
docset: aem65
exl-id: 1fc56829-db81-4450-b1d8-b4a31110199e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# 根據所使用的模板顯示元件{#displaying-components-based-on-the-template-used}

當表單作者使用[template](../../forms/using/template-editor.md)建立最適化表單時，表單作者可以根據模板策略查看和使用特定元件。 您可以指定範本內容原則，以選擇表單作者在表單編寫時看到的一組元件。

## 更改模板{#changing-the-content-policy-of-a-template}的內容策略

建立範本時，會建立在內容存放庫的`/conf`下。 根據您在`/conf`目錄中建立的資料夾，範本的路徑為：`/conf/<your-folder>/settings/wcm/templates/<your-template>`。

根據範本的內容原則，執行下列步驟以顯示側欄中的元件：

1. 開啟CRXDE lite。\
   URL: `https://<server>:<port>/crx/de/index.jsp`
1. 在CRXDE中，導覽至建立範本的資料夾。

   例如：`/conf/<your-folder>/`

1. 在CRXDE中，導覽至：`/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/`

   若要選取一組元件，需要新的內容原則。 要建立新策略，請複製並貼上預設策略，然後更名它。

   預設內容策略的路徑為：`/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/default`

   在`gridFluidLayout`資料夾中，複製並貼上預設策略，然後將其更名。 例如， `myPolicy`。

   ![複製預設策略](assets/crx-default1.png)

1. 選擇您建立的新策略，並在右側面板中選擇&#x200B;**components**&#x200B;屬性，類型為`string[]`。

   選取並開啟元件屬性時，您會看到「編輯元件」對話方塊。 「編輯元件」對話框允許您使用&#x200B;**+**&#x200B;和&#x200B;**-**&#x200B;按鈕添加或刪除元件組。 您可以新增元件群組，其中包含您希望作者使用的表單元件。

   ![在策略中添加或刪除元件](assets/add-components-list1.png)

   新增元件群組後，按一下&#x200B;**OK**&#x200B;以更新清單，然後按一下CRXDE位址列上方的&#x200B;**儲存全部**&#x200B;並重新整理。

1. 在範本中，將內容原則從預設變更為您建立的新原則。 （此範例中為`myPolicy`）。

   要更改策略，請在CRXDE中導航到`/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/guideContainer/rootPanel/items`。

   在`cq:policy`屬性中，將`default`更改為新策略名稱(`myPolicy`)。

   ![更新的模板內容策略](assets/updated-policy.png)

   使用範本建立表單時，您可以在側欄中看到新增的元件。
