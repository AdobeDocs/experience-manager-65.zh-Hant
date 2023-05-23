---
title: 自適應形式中的分隔器元件
seo-title: Separator component in adaptive forms
description: 可以使用分隔符元件以直觀方式分隔窗體的部分。
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

# 自適應形式中的分隔器元件{#separator-component-in-adaptive-forms}

可以使用分隔符元件以可視方式分隔窗體的面板。 可通過指定分隔符元件的以下屬性來定義分隔符元件的總體外觀和樣式：

* **元素名稱：** 指定元件的名稱。 SOM表達式使用在「元素名稱」欄位中指定的值來定址元件。
* **厚度：** 以像素為單位指定分隔符元件的厚度。

* **CSS類：** 指定分隔符元件的自定義CSS類

* **內聯樣式：** 使用AEM Forms，您現在可以將內嵌CSS樣式應用於單個自適應表單元件並即時預覽更改。

可以使用「佈局」模式來定義分隔器元件所跨越的列數。 有關詳細資訊，請參見 [使用佈局模式調整元件大小](../../forms/using/resize-using-layout-mode.md)。

要指定分隔符元件的屬性：

1. 選擇分隔符元件並點擊 ![招商](assets/cmppr.png)。 屬性在邊欄中開啟。
1. 按一下「內聯CSS屬性」部分中的頁籤以指定CSS屬性。 例如：a.在「欄位」頁籤中，按一下 **添加項**。 將添加一行，其中包含兩個欄位。
1. 在左邊的第一個欄位中，指定要應用的CSS3屬性。 比如說， **邊界**。 也可以通過按一下向下箭頭按鈕來選擇屬性。 下拉清單不是詳盡的，您可以在此欄位中指定任何受支援的CSS3屬性名稱。
1. 在相鄰欄位中，為指定的CSS3屬性指定有效值。 比如說， **3px實心黑色**。
1. 按一下 **添加項** 指定另一個屬性及其值。
1. 按一下 **預覽** 來修改選定線條的屬性。
1. 按一下 **確定** 確認更改或 **取消** 對話框。
