---
title: 'AEM Forms中的預留位置文字 '
seo-title: 'AEM Forms中的預留位置文字 '
description: 預留位置文字旨在在控制項沒有值時，協助使用者輸入資料。 它可以是範例值或預期格式的簡短說明。
seo-description: 預留位置文字旨在在控制項沒有值時，協助使用者輸入資料。 它可以是範例值或預期格式的簡短說明。
uuid: 69f80722-93db-4932-9016-4b530e183d4e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: f9ff2cc5-3f0a-4b2f-a206-2fe0985646ea
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# AEM Forms {#placeholder-text-in-aem-forms}中的預留位置文字

預留位置文字代表單字或短片語。 它旨在幫助用戶在控制項沒有值時輸入資料。 預留位置文字可以是範例值或預期格式的簡短說明。 預留位置文字會在使用者輸入值之前顯示，當使用者輸入或選取值時會移除。

>[!NOTE]
>
>佔位符文本（如果指定）必須具有一個不包含新行字元的值。

![含有和不含預留位置文字的日期元件](assets/dat-picker-place-holder-text.png)

**A.** Date元件，含預留位置文字 **B.** Date元件，不含預留位置文字

AEM Forms支援「密碼」方塊、「日期選擇器」、「數值」方塊和文字方塊欄位的預留位置文字。\
原生HTML5日期介面工具集不支援預留位置文字。 要指定佔位符文本，請執行以下操作：

1. 按一下右鍵支援預留位置文本的元件，然後按一下&#x200B;**編輯**。 將出現「編輯元件」(Edit component)對話框。

1. 開啟&#x200B;**標題和文字**&#x200B;標籤。
1. 在&#x200B;**預留位置文字方塊**&#x200B;中指定字詞或短片。 按一下&#x200B;**「確定」**。

>[!NOTE]
>
>Microsoft Internet Explorer 9不支援預留位置文字。

