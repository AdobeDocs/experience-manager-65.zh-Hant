---
title: 在HTML5表單中建立可存取的複雜表格
seo-title: 在HTML5表單中建立可存取的複雜表格
description: 瞭解如何在HTML5表格中建立可存取的表格。
seo-description: 瞭解如何在HTML5表格中建立可存取的表格。
uuid: e52562d2-4dc3-4359-9dbb-c18614921808
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 在HTML5表單中建立可存取的複雜表格 {#create-accessible-complex-tables-in-html-forms}

HTML5 Forms中表格的預設實作使用HTML DIV元素來轉換表格。 演算包括使用ARIA角色來滿足無障礙環境支援需求。

為避免螢幕閱讀程式的協助功能問題，而這些螢幕閱讀程式無法完全支援資料表格使用的ARIA-roles,HTML5 Forms提供表格的替代轉譯。 這些表基於Designer中引入的新表格格式，它還支援：

* 列標題
* 列跨

若要在HTML5 Forms中使用新格式，請將表格標示為複雜表格。 要將表標籤為複雜，請按如 `extras` 下方式在表子表單的XML源中添加標籤：

```
</extras>
 <text name="complexTable">1</text>
 </extras>
```

標示為complexTable的表格會遵循原 *生的HTML轉譯* ，並為某些螢幕閱讀程式提供更佳的協助工具支援。  要建立行範圍，請選擇同一列中表的連續單元格，按一下右鍵該選項，然後按一下「合 **[!UICONTROL 並單元格]**」。

*****注意：建立列範圍僅適用於最左側的儲存格。*

要將行標籤為行標題，請選擇行中的所有單元格，按一下右鍵選項，然後按一下標 **[!UICONTROL 記標題]**。

若要將儲存格標示為欄標題，請選取欄中的任何儲存格，在選取範圍上按一下滑鼠右鍵，然後按一下「標 **[!UICONTROL 示標題」]**。

新 *AccessibleTable格式的限制* :

* 如果表中使用瀏覽範圍，則不支援可擴展欄位
* 不支援嵌套表（表單元格中的表）
* 對rowspan的支援僅限於標題列和標題儲存格
* 支援限於一般表格
* 不支援以瀏覽範圍> 1填入表格的資料預填

