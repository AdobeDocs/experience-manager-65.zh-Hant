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
role: User, Developer
feature: Adaptive Forms,Foundation Components
source-git-commit: 8a77756e8ba771c8de9950c2323bef8f23cc59b4
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 1%

---

# 根據使用的範本顯示元件{#displaying-components-based-on-the-template-used}

當表單作者使用[範本](../../forms/using/template-editor.md)建立最適化表單時，表單作者可以根據範本原則檢視和使用特定元件。 您可以指定範本內容原則，以讓您選擇表單作者在表單製作時看到的元件群組。

## 變更範本的內容原則 {#changing-the-content-policy-of-a-template}

當您建立範本時，會在內容存放庫中的`/conf`下建立它。 根據您在`/conf`目錄中建立的資料夾，範本的路徑為： `/conf/<your-folder>/settings/wcm/templates/<your-template>`。

執行以下步驟，根據範本的內容原則在側邊欄中顯示元件：

1. 開啟CRXDE Lite。\
   URL： `https://<server>:<port>/crx/de/index.jsp`
1. 在CRXDE中，導覽至建立範本的資料夾。

   例如：`/conf/<your-folder>/`

1. 在CRXDE中，瀏覽至： `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/`

   若要選取元件群組，需要新的內容原則。 若要建立原則，請複製並貼上預設原則，然後將其重新命名。

   預設內容原則的路徑為： `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/default`

   在`gridFluidLayout`資料夾中，複製並貼上預設原則並重新命名。 例如，`myPolicy`。

   ![正在複製預設原則](assets/crx-default1.png)

1. 選取您建立的新原則，並在右側面板中選取型別為`string[]`的&#x200B;**元件**&#x200B;屬性。

   當您選取並開啟components屬性時，您會看到「編輯元件」對話方塊。 「編輯元件」對話方塊可讓您使用&#x200B;**+**&#x200B;和&#x200B;**-**&#x200B;按鈕來新增或移除元件群組。 您可以新增元件群組，其中包含您希望作者使用的元件。

   ![在原則中新增或移除元件](assets/add-components-list1.png)

   新增元件群組後，按一下[確定]以更新清單，然後按一下CRXDE位址列上方的[儲存全部] **並重新整理。**&#x200B;**&#x200B;**

1. 在範本中，將內容原則從預設變更為您建立的新原則。 （在此範例中為`myPolicy`。）

   若要變更原則，請在CRXDE中導覽至`/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/guideContainer/rootPanel/items`。

   在`cq:policy`屬性中，將`default`變更為新的原則名稱( `myPolicy`)。

   ![已更新範本內容原則](assets/updated-policy.png)

   當您使用範本製作表單時，可以在側邊欄中看到新增的元件。
