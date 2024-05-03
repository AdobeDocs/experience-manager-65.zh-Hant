---
title: 將連結元件內嵌在頁面中
description: 您可以使用連結元件從任何頁面連結最適化檔案或最適化表單。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: eb45adf2-d0f3-4de6-92ac-fb146953e989
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# 將連結元件內嵌在頁面中{#embedding-link-component-in-a-page}

## 先決條件 {#prerequisites}

連結元件是Document Services類別的成員。 請確定AEM元件瀏覽器中顯示Document Services類別。 如果未列出類別，請遵循下列步驟操作： [啟用表單入口網站元件](/help/forms/using/enabling-forms-portal-components.md).

## 連結元件 {#link-component}

連結元件可讓表單入口網站作者從頁面上的任何位置建立最適化表單的連結。 連結元件可在元件瀏覽器的「檔案服務」區段中取得。

執行以下步驟，將連結元件新增至頁面：

1. 拖曳 **連結** 元件時。 選取元件並選取 ![cmppr](assets/cmppr.png). 「編輯連結元件」對話方塊開啟。

   ![edit-link-component](assets/edit-link-component.png)

1. 在 **顯示** 索引標籤中，指定下列專案：

   * **連結標題**：連結的連結文字或標題。
   * **連結工具提示**：連結的工具提示。
   * **版面配置範本**：連結元件配置的範本。

1. 開啟 **資產資訊** 索引標籤並指定資產的型別。 資產可以是 **表單**. 視選取的資產型別而定，畫面會顯示下列選項：

   * **資產路徑**：儲存資產的存放庫路徑。

   * **演算型別**：轉譯器格式 — 「PDF」、「HTML」或「自動」。 「自動」轉譯型別會偵測使用者環境，並據此將表單轉譯為HTML或PDF。 例如，如果表單可從行動裝置存取，則自動轉譯型別會以HTML轉譯表單。
   * **提交URL：**  表單資料提交所在的servlet的URL。
   * **HTML設定檔**：將表單轉譯為HTML的設定檔。
   * **PDF設定檔**：將表單轉譯為PDF檔案的設定檔。

1. 開啟 **進階** 標籤。 您可以使用鍵值配對格式指定其他引數。 按一下連結時，這些額外的引數會與表單一起傳遞。

   選取 **完成** 以儲存組態。

## 使用連結元件的最佳實務 {#best-practices-for-using-link-component-br}

* 如果「表單路徑」中指定的路徑指向的檔案將PDF作為其允許的轉譯格式，請確保您選擇「PDF」作為轉譯型別。
* 表單的提交URL可在數個位置指定，其優先順序如下：

   1. 表單中內嵌的提交URL （在提交按鈕中）具有最高優先順序。
   1. Forms Manager中提到的提交URL具有中優先順序。
   1. Forms入口網站中提到的提交URL優先順序最低。
