---
title: 更改HTML5窗體的預設樣式
seo-title: Changing default styles of HTML5 forms
description: HTML5表單樣式基於CSS。 可以更改窗體的預設樣式。
seo-description: HTML5 forms styling is based on CSS. You can change the default styles of the form.
uuid: 5e23237d-42d8-4d29-b79e-4dc276ef65ff
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 582b0fe8-a92b-4a1d-b859-57f13f53d0d8
docset: aem65
feature: Mobile Forms
exl-id: 4c84cfd1-50a4-416f-b4a5-7f2f4c7f10af
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---

# 更改HTML5窗體的預設樣式{#changing-default-styles-of-html-forms}

HTML5表單使用HTML5功能進行渲染，而渲染表單的樣式使用CSS進行。 HTML5窗體的預設外觀與其PDF格式副本類似。 開發人員可以使用自定義CSS更改HTML5表單的預設外觀。

本文提供逐步資訊以更改HTML5窗體和 [樣式簡介](/help/forms/using/css-styles.md) 文章包含有關HTML5表單各個樣式方面的詳細資訊。 在執行本文中提到的步驟之前，請確保閱讀「樣式簡介」文章。

以下兩幅圖顯示了預設樣式和自定義樣式之間的差異。

![圖片–002小型](assets/pictures-002-small.png)

## 設定窗體樣式 {#style-your-forms}

1. **選擇要添加自定義樣式的配置檔案**

   訪問URL上的CRX DE介面： **https://&lt;server>:&lt;port>/crx/de** 建立配置檔案或選擇現有配置檔案。 要瞭解如何建立配置檔案，請參閱 [建立新配置檔案](/help/forms/using/custom-profile.md)

1. **建立CSS樣式表以設定HTML5表單的樣式**

   導航到已在其中建立配置檔案呈現器的資料夾，然後建立CSS樣式表檔案。 要執行的步驟包括

   1. 按一下右鍵資料夾並選擇 **建立** > **建立檔案** 菜單

   1. 在「建立檔案」(Create file)對話框中，輸入樣式表的名稱。 確保使用副檔名.css（例如stylesheet.css）
   1. 在導航窗格中，開啟已建立的CSS檔案。
   1. 定義要對這些類進行樣式化和添加樣式的元件的CSS類。

   要瞭解要為HTML5窗體中的特定元件建立的CSS類，請參見 [樣式簡介](/help/forms/using/css-styles.md)。

1. **在「輪廓呈現器」中包括樣式表**

   在CRX DE中開啟「配置檔案呈現器」頁（jsp檔案），並將CSS檔案包括在XFA客戶端庫正下方的頁中。 執行這些步驟，將CSS檔案包含在配置檔案中。

   1. 在呈現器頁中搜索以下行：

      &lt;cq:includeClientLib categories=&quot;xfaforms.profile&quot; />

   1. 在上面的行下面插入以下內容以包括樣式表：

      &lt;link href=&quot;/path/to/stylesheet&quot; rel=&quot;stylesheet&quot; type=&quot;text/css&quot;/>

   1. 儲存檔案。
