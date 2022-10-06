---
title: 設計無障礙HTML5表單
seo-title: Designing accessible HTML5 forms
description: HTML5表單使用ARIAHTML5協助工具標準。 這些表單支援標籤式導覽，經認證可與常見螢幕助讀程式相容。
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

# 設計無障礙HTML5表單 {#designing-accessible-html-forms}

HTML5表單使用ARIAHTML5無障礙標準，產生無障礙HTML表單。 這些表單支援頁簽式導覽（Mozilla FireFox除外），經認證可與常見螢幕助讀程式相容。 若要產生具有良好協助工具功能的HTML5表單，請根據一些基本設計准則來設計XFA表單範本。 設計准則包括配置正確的頁簽順序和為每個表單控制項提供「說話文字」內容。 AEM Forms Designer支援設定這些表單控制項屬性，以產生「可存取」PDF和HTML5表單。

*注：標籤式導航不涵蓋受保護的欄位，如顯示值總和的計算欄位。 要使螢幕助讀程式讀取受保護欄位的值，請將空的只讀欄位置於受保護欄位的頂部或旁邊。 將受保護欄位的值分配給新的只讀欄位。 螢幕助讀程式或頁簽式導航可選擇此只讀欄位，並將其作為受保護欄位的值來說明。*

AEM Forms Designer包含許多可傳遞至螢幕助讀程式的「說話文字」選項。 對於表單中的每個物件，使用者可以為螢幕助讀程式文字指定數個設定之一：

* 自訂螢幕助讀程式文字，可使用協助工具浮動視窗來設定。 作者可在按鈕和欄位的名稱及其用途上加上注釋。
* 工具提示，可在協助工具浮動視窗中設定。
* 表單上欄位的註解。
* 對象的名稱，如「綁定」頁簽的「名稱」選項中指定。

![協助工具](assets/accessibility.png)

當表單控制項上有多個選項(如工具提示、螢幕Reader文字和註解)時，螢幕Reader僅使用其中一個屬性。 預設順序為「自訂螢幕Reader文字」、「工具提示」、「註解」和「名稱」。 您可以使用螢幕Reader覆寫預設順序 **優先順序** 選項。
