---
title: 設計無障礙HTML5表單
description: HTML5表單使用ARIAHTML5協助工具標準。 這些表單支援標籤式導覽，並經過認證與常用熒幕閱讀器相容。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms
exl-id: fca2f9b2-11a2-4db0-a370-c4046f32be63
source-git-commit: 524475c8f9dbd02bae30ecd558a376505fbe0aed
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# 設計無障礙HTML5表單 {#designing-accessible-html-forms}

HTML5表單使用ARIAHTML5協助工具標準來產生無障礙的HTML表單。 這些表單支援標籤式導覽（Mozilla FireFox除外），且經認證與一般熒幕閱讀器相容。 若要產生具備良好協助工具功能的HTML5表單，請根據一些基本設計准則來設計XFA表單範本。 設計准則包括設定正確的標籤順序，並為每個表單控制項提供「說文字」內容。 AEM Forms Designer支援這些表單控制項屬性的設定，以產生無障礙的PDF和HTML5表單。

*附註：標籤式導覽不會涵蓋受保護欄位，例如顯示值總和的計算欄位。 若要讓熒幕助讀程式讀取受保護欄位的值，請在受保護欄位的頂端或旁邊，放置空白的唯讀欄位。 將受保護欄位的值指派給新的唯讀欄位。 熒幕助讀程式或索引標籤導覽可挑選此唯讀欄位，並將其朗讀為受保護欄位的值。*

AEM Forms Designer包含數個可傳遞給熒幕閱讀程式的「說話文字」選項。 對於表單中的每個物件，使用者可以為熒幕助讀程式文字指定下列其中一個設定：

* 自訂熒幕助讀程式文字，可使用「協助工具」浮動視窗進行設定。 作者可以標註按鈕和欄位的名稱及其用途。
* 工具提示，可在「協助工具」浮動視窗中設定。
* 表單上欄位的標題。
* 物件的名稱，如「繫結」標籤的「名稱」選項中所指定。

![協助工具](assets/accessibility.png)

當「表單」控制項上有工具提示、「熒幕Reader文字」和「標題」等多個選項可用時，「熒幕」Reader只會使用其中一個屬性。 預設順序為「自訂熒幕Reader文字」、「工具提示」、「標題」和「名稱」。 您可以使用熒幕Reader來覆寫預設順序 **優先順序** 協助工具浮動視窗中的選項。
