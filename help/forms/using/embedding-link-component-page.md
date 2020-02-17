---
title: 將連結元件內嵌在頁面中
seo-title: 將連結元件內嵌在頁面中
description: 您可以使用連結元件，從任何頁面連結最適化檔案或最適化表單。
seo-description: 您可以使用連結元件，從任何頁面連結最適化檔案或最適化表單。
uuid: 22f488fc-bb1a-40aa-a5f4-6d04d7250f29
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9d63152d-41ca-4c7c-bb20-af16c7bdec13
docset: aem65
translation-type: tm+mt
source-git-commit: f9ed171c188a4dfb71f12ae9c98105a4c1895542

---


# 將連結元件內嵌在頁面中{#embedding-link-component-in-a-page}

## 必備條件 {#prerequisites}

連結元件是「檔案服務」類別的成員。 請確定「檔案服務」類別會顯示在AEM元件瀏覽器中。 如果未列出類別，請遵循啟用表單入口元件 [中所列的步驟](/help/forms/using/enabling-forms-portal-components.md)。

## 連結元件 {#link-component}

Link元件可讓表單入口網站作者從頁面上的任何位置建立最適化表單的連結。 「連結」元件可在元件瀏覽器的「檔案服務」區段中使用。

執行以下步驟將連結元件添加到頁面：

1. 拖曳頁 **面上的** Link元件。 選取元件並點選 ![cmppr](assets/cmppr.png)。 「編輯連結元件」(Edit Link Component)對話框開啟。

   ![edit-link-component](assets/edit-link-component.png)

1. 在「顯 **示** 」索引標籤中，指定下列：

   * **連結標題**:連結的文字或標題。
   * **連結工具提示**:連結的工具提示。
   * **版面範本**:連結元件版面的範本。

1. 開啟「 **資產資訊** 」標籤，並指定資產類型。 資產可以是表 **單**。 視選取的資產類型而定，會顯示下列選項：

   * **資產路徑**:儲存資產的儲存庫路徑。

   * **演算類型**:演算格式- PDF、HTML或Auto。 「自動」演算類型會偵測使用者環境，並因此將表單轉譯為HTML或PDF。 例如，如果表單是從行動裝置存取，「自動」演算類型會以HTML格式演算表單。
   * **** 提交URL: 提交表單資料的servlet的URL。
   * **HTML設定檔**:將表單轉譯為HTML的描述檔。
   * **PDF設定檔**:將表單轉譯為PDF檔案的設定檔。

1. 開啟「進 **階** 」標籤。 您可以以鍵值對格式指定其他參數。 當點按連結時，這些額外參數會隨表單一起傳遞。

   點選「 **完成** 」以儲存設定。

## 使用連結元件的最佳範例 {#best-practices-for-using-link-component-br}

* 如果在「表單路徑」中指定的路徑指向具有PDF作為允許的渲染格式的文檔，請確保選擇PDF作為渲染類型。
* 表單的提交URL可在數處指定，其優先順序如下：

   1. 內嵌於表單（在提交按鈕中）的提交URL具有最高優先順序。
   1. Forms manager中提及的提交URL具有中等優先順序。
   1. 表單入口網站中提及的提交URL的優先順序最低。
