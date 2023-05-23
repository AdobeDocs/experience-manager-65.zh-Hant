---
title: 在頁面中嵌入連結元件
seo-title: Embedding link component in a page
description: 可以使用連結元件從任何頁面連結自適應文檔或自適應表單。
seo-description: You can use the link component to link an adaptive document or an adaptive form from any page.
uuid: 22f488fc-bb1a-40aa-a5f4-6d04d7250f29
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 9d63152d-41ca-4c7c-bb20-af16c7bdec13
docset: aem65
exl-id: eb45adf2-d0f3-4de6-92ac-fb146953e989
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# 在頁面中嵌入連結元件{#embedding-link-component-in-a-page}

## 必備條件 {#prerequisites}

連結元件是「文檔服務」類別的成員。 確保「文檔服務」類別在元件瀏覽器AEM中可見。 如果未列出類別，請按照中列出的步驟操作 [啟用表單門戶元件](/help/forms/using/enabling-forms-portal-components.md)。

## 連結元件 {#link-component}

Link元件允許表單門戶作者從頁面上的任何位置建立指向自適應表單的連結。 「連結」元件可在元件瀏覽器的「文檔服務」部分使用。

執行以下步驟將連結元件添加到頁面：

1. 拖動 **連結** 元件。 選擇元件並點擊 ![招商](assets/cmppr.png)。 將開啟「編輯連結元件」對話框。

   ![編輯連結元件](assets/edit-link-component.png)

1. 在 **顯示** 頁籤，指定以下內容：

   * **連結標題**:連結的文本或標題。
   * **連結工具提示**:連結的工具提示。
   * **佈局模板**:連結元件佈局的模板。

1. 開啟 **資產資訊** 頁籤，然後指定資產類型。 資產可以是 **表格**。 根據所選資產的類型，將顯示下列選項：

   * **資產路徑**:儲存資產的儲存庫路徑。

   * **呈現類型**:渲染格式 — PDF、HTML或自動。 「自動」呈現類型檢測用戶環境，並相應地將表單呈現為HTML或PDF。 例如，如果從移動設備訪問表單，則「自動」呈現類型會以HTML呈現表單。
   * **提交URL:**  提交表單資料的Servlet的URL。
   * **HTML配置檔案**:用於將表單呈現為HTML的配置檔案。
   * **PDF配置檔案**:用於將表單呈現為PDF文檔的配置檔案。

1. 開啟 **高級** 頁籤。 可以以鍵值對格式指定附加參數。 按一下該連結時，這些附加參數會隨窗體一起傳遞。

   點擊 **完成** 的子菜單。

## 使用連結元件的最佳做法 {#best-practices-for-using-link-component-br}

* 如果在「表單路徑」中指定的路徑指向具有PDF作為其允許的呈現格式的文檔，請確保選擇PDF作為呈現類型。
* 表單的提交URL可以在多個位置指定，其優先順序如下：

   1. 在表單（在提交按鈕中）中嵌入的提交URL優先順序最高。
   1. 在Forms管理器中提及的提交URL具有中等優先順序。
   1. 表單門戶中提及的提交URL優先順序最低。
