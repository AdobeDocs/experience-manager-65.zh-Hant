---
title: 適用性表單中的分隔符號元件
seo-title: Separator component in adaptive forms
description: 您可以使用分隔符號元件以視覺化方式分隔表單的區段。
seo-description: You can use the separator component to visually segregate sections of a form.
uuid: f8d2aed3-52aa-437f-bfe3-0c8779e7986c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: a8aa77fe-5880-4c4e-9e1b-3c5a8772c29d
docset: aem65
feature: Adaptive Forms
exl-id: 11cbf865-c8e2-4833-b0b8-a3cb5e42f5cd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# 適用性表單中的分隔符號元件{#separator-component-in-adaptive-forms}

您可以使用分隔符號元件以視覺化方式分隔表單的面板。 通過指定分隔符元件的以下屬性，可以定義分隔符元件的總體外觀和樣式：

* **元素名稱：** 指定元件的名稱。 SOM表達式用在「元素名稱」欄位中指定的值來處理元件。
* **厚度：** 指定分隔符元件的厚度（像素）。

* **CSS類：** 指定分隔符元件的自定義CSS類

* **內嵌樣式：** 透過AEM Forms，您現在可以將內嵌CSS樣式套用至個別的最適化表單元件，並即時預覽變更。

您可以使用「配置」模式來定義分隔符元件所涵蓋的列數。 如需詳細資訊，請參閱 [使用「版面」模式調整元件大小](../../forms/using/resize-using-layout-mode.md).

要指定分隔符元件的屬性，請執行以下操作：

1. 選取分隔符號元件並點選 ![cppr](assets/cmppr.png). 屬性會在側欄中開啟。
1. 按一下「內嵌CSS屬性」區段中的索引標籤，以指定CSS屬性。 例如：a.在欄位標籤中，按一下 **新增項目**. 新增含有兩個欄位的列。
1. 在左側的第一個欄位中，指定您要套用的CSS3屬性。 例如， **邊框**. 您也可以按一下向下箭頭按鈕來選取屬性。 下拉式清單並非詳盡無遺，您可以在此欄位中指定任何支援的CSS3屬性名稱。
1. 在相鄰欄位中，指定指定CSS3屬性的有效值。 例如， **3px實心黑色**.
1. 按一下 **新增項目** 指定其他屬性及其值。
1. 按一下 **預覽** 以預覽表單中的更改。
1. 按一下 **確定** 確認變更或 **取消** 以退出對話方塊而不進行任何變更。
