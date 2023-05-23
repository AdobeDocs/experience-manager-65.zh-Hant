---
title: 根據使用的模板顯示元件
seo-title: Displaying components based on the template used
description: 建立表單時，瞭解如何根據所選模板啟用邊欄中的元件。
seo-description: When you create a form, learn how you can enable components in the sidebar based on the template selected.
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
source-wordcount: '352'
ht-degree: 0%

---

# 根據使用的模板顯示元件{#displaying-components-based-on-the-template-used}

當表單作者使用 [模板](../../forms/using/template-editor.md)，表單作者可以根據模板策略查看和使用特定的元件。 您可以指定模板內容策略，該策略允許您選擇表單作者在建立表單時看到的一組元件。

## 更改模板的內容策略 {#changing-the-content-policy-of-a-template}

建立模板時，將在 `/conf` 中。 根據您在 `/conf` 目錄，模板的路徑是： `/conf/<your-folder>/settings/wcm/templates/<your-template>`。

根據模板的內容策略，執行以下步驟以在提要欄中顯示元件：

1. 開啟CRXDE Lite。\
   URL: `https://<server>:<port>/crx/de/index.jsp`
1. 在CRXDE中，導航到建立模板的資料夾。

   例如：`/conf/<your-folder>/`

1. 在CRXDE中，導航到： `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/`

   要選擇一組元件，需要新的內容策略。 要建立新策略，請複製並貼上預設策略，然後更名它。

   預設內容策略的路徑是： `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/default`

   在 `gridFluidLayout` 資料夾，複製並貼上預設策略，然後更名它。 比如說， `myPolicy`。

   ![複製預設策略](assets/crx-default1.png)

1. 選擇您建立的新策略，然後選擇 **元件** 類型為右側面板中的屬性 `string[]`。

   選擇並開啟元件屬性時，將看到「編輯元件」(Edit components)對話框。 使用「編輯元件」對話框，可以使用 **+** 和 **-** 按鈕。 您可以添加包含希望作者使用的元件的元件組。

   ![在策略中添加或刪除元件](assets/add-components-list1.png)

   添加元件組後，按一下 **確定** 以更新清單，然後按一下 **全部保存** 在CRXDE地址欄上並刷新。

1. 在模板中，將內容策略從預設更改為您建立的新策略。 ( `myPolicy` 在本例中。)

   要更改策略，請在CRXDE中導航至 `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/guideContainer/rootPanel/items`。

   在 `cq:policy` 屬性，更改 `default` 到新策略名稱( `myPolicy`)。

   ![更新的模板內容策略](assets/updated-policy.png)

   當您使用模板建立表單時，可以在邊欄中看到添加的元件。
