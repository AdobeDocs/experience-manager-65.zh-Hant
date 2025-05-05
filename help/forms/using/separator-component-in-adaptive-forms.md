---
title: 調適型表單中的分隔符號元件
description: 您可以使用分隔符號元件以視覺化方式分隔表單的區段。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 11cbf865-c8e2-4833-b0b8-a3cb5e42f5cd
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 10%

---

# 調適型表單中的分隔符號元件{#separator-component-in-adaptive-forms}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant)，用來[建立新的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文介紹使用基礎元件製作最適化Forms的舊方法。</span>

您可以使用分隔符號元件，以視覺化方式分隔表單的面板。 您可以指定分隔符號元件的下列屬性，以定義分隔符號元件的整體外觀和樣式：

* **元素名稱：**&#x200B;指定元件的名稱。 SOM運算式會使用「元素名稱」欄位中指定的值來定址元件。
* **厚度：**&#x200B;指定分隔符號元件的厚度（畫素）。

* **CSS類別：**&#x200B;指定分隔符號元件的自訂CSS類別

* **內嵌樣式：**&#x200B;透過AEM Forms，您現在可以將內嵌CSS樣式套用至個別的最適化表單元件，並即時預覽變更。

您可以使用「版面」模式來定義分隔符號元件跨越的欄數。 如需詳細資訊，請參閱[使用配置模式調整元件大小](../../forms/using/resize-using-layout-mode.md)。

若要指定分隔符號元件的屬性：

1. 選取分隔符號元件並選取![cmppr](assets/cmppr.png)。 屬性會在側邊欄中開啟。
1. 按一下「內嵌CSS屬性」區段中的索引標籤，以便指定CSS屬性。 例如： a.在[欄位]索引標籤中，按一下[**新增專案**]。 會新增包含兩個欄位的列。
1. 在左側的第一個欄位中，指定您要套用的CSS3屬性。 例如，**邊框**。 您也可以按一下向下箭頭按鈕來選取屬性。 下拉式清單並非詳盡無遺，您可以在此欄位中指定任何支援的CSS3屬性名稱。
1. 在相鄰的欄位中，指定指定CSS3屬性的有效值。 例如，**3-px實心黑色**。
1. 按一下&#x200B;**新增專案**&#x200B;以指定其他屬性及其值。
1. 按一下&#x200B;**預覽**，以便預覽表單中的變更。
1. 如果要確認變更，請按一下[確定] **&#x200B;**，或按一下[取消] **&#x200B;**&#x200B;結束對話方塊，不做任何變更。
