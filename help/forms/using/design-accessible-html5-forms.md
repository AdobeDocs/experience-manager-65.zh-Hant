---
title: 設計可訪問的HTML5表單
seo-title: Designing accessible HTML5 forms
description: HTML5表格使用ARIAHTML5輔助功能標準。 這些表單支援頁籤式導航，並且經認證與普通螢幕閱讀器相容。
seo-description: HTML5 forms use the ARIA HTML5 accessibility standard. These forms support tabbed navigation and are certified to be compatible with common screen readers.
uuid: 1ce5ba39-69ea-4d0e-96ea-e2a38b21d6b7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8711ad33-396b-4572-b2ee-71e9f45f4ebe
docset: aem65
feature: Mobile Forms
exl-id: fca2f9b2-11a2-4db0-a370-c4046f32be63
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# 設計可訪問的HTML5表單 {#designing-accessible-html-forms}

HTML5表單使用ARIAHTML5輔助功能標準生成可訪問的HTML表單。 這些表單支援頁籤式導航（Mozilla FireFox除外），並且經認證與普通螢幕閱讀器相容。 要生成具有良好可訪問性功能的HTML5表單，請根據一些基本設計准則設計XFA表單模板。 設計准則包括配置正確的頁籤順序和為每個表單控制項提供「說話文本」內容。 AEM Forms設計器支援設定這些表單控制項屬性以生成可訪問PDF和HTML5表單。

*注：標籤式導航不覆蓋受保護的欄位，如顯示值總和的計算欄位。 要讓螢幕閱讀器讀取受保護欄位的值，請在受保護欄位的頂部或旁邊放置一個空的只讀欄位。 將受保護欄位的值分配給新的只讀欄位。 螢幕閱讀器或頁籤式導航可以選取此只讀欄位並將其作為受保護欄位的值進行顯示。*

AEM Forms設計器包括許多可傳遞給螢幕閱讀器的「講話文本」選項。 對於表單中的每個對象，用戶可以為螢幕閱讀器文本指定以下幾個設定之一：

* 自定義螢幕閱讀器文本，可使用輔助功能面板設定。 作者可以注釋按鈕和欄位的名稱及其用途。
* 工具提示，可在輔助功能面板中設定。
* 窗體中欄位的標題。
* 對象的名稱，如「綁定」頁籤的「名稱」選項中所指定。

![輔助](assets/accessibility.png)

當多個選項(如工具提示、螢幕Reader文本和標題)在表單控制項上可用時，螢幕Reader僅使用這些屬性中的一個。 預設順序為自定義螢幕Reader文本、工具提示、標題和名稱。 您可以使用「螢幕」Reader覆蓋預設順序 **優先** 選項。
