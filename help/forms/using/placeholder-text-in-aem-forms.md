---
title: AEM Forms中的預留位置文字
description: 預留位置文字的目的是在控制項沒有值時，協助使用者輸入資料。 它可以是範例值，或是預期格式的簡短說明。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 6b6e27b5-8b4e-489c-9e72-4d256692c1ca
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 19%

---

# AEM Forms中的預留位置文字 {#placeholder-text-in-aem-forms}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant)，用來[建立新的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>

預留位置文字代表單字或短語。 其目的是協助使用者在控制項沒有值時輸入資料。 預留位置文字可以是範例值，或是預期格式的簡短說明。 預留位置文字會在使用者輸入值之前顯示，當使用者輸入或選取值時會移除預留位置文字。

>[!NOTE]
>
>預留位置文字（如果已指定）的值不得包含任何新行字元。

![含和不含預留位置文字的日期元件](assets/dat-picker-place-holder-text.png)

**A.**&#x200B;含有預留位置文字的日期元件&#x200B;**B.**&#x200B;不含預留位置文字的日期元件

AEM Forms支援「密碼」方塊、日期選擇器、數值方塊和文字方塊欄位的預留位置文字。\
原生HTML5日期Widget不支援預留位置文字。 若要指定預留位置文字：

1. 以滑鼠右鍵按一下支援預留位置文字的元件，然後按一下&#x200B;**編輯**。 「編輯元件」對話方塊隨即顯示。

1. 開啟&#x200B;**標題與文字**&#x200B;索引標籤。
1. 在&#x200B;**預留位置文字方塊**&#x200B;中指定文字或短語。 按一下&#x200B;**「確定」**。

>[!NOTE]
>
>Microsoft Internet Explorer 9不支援預留位置文字。
