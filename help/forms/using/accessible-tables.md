---
title: 在HTML5窗體中建立可訪問的複雜表
seo-title: Create accessible complex tables in HTML5 forms
description: 瞭解如何在HTML5窗體中建立可訪問的表。
seo-description: Learn how to create accessible tables in HTML5 forms.
uuid: e52562d2-4dc3-4359-9dbb-c18614921808
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
feature: Mobile Forms
exl-id: 3b8e3323-9ac4-4f5c-8c52-e2186e9169ea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 0%

---

# 在HTML5窗體中建立可訪問的複雜表 {#create-accessible-complex-tables-in-html-forms}

FormsHTML5中表的預設實現使用HTMLDIV元素來呈現表。 渲染包括使用ARIA角色來滿足可訪問性要求。

為避免螢幕閱讀器存在的輔助功能問題，這些螢幕閱讀器不完全支援資料表所使用的ARIA-roles,HTML5Forms為這些表提供了備用格式副本。 這些表基於Designer中引入的新表格式，它還支援：

* 行標題
* 行跨

要在HTML5Forms中使用新格式，請將表標籤為複雜。 要將表標籤為複雜，請添加 `extras` 表子表單的XML源中的標籤，如下所示：

```xml
</extras>
 <text name="complexTable">1</text>
 </extras>
```

標籤為 *複雜表* 遵循本機HTML格式副本，為某些螢幕閱讀器提供更好的輔助功能支援。  要建立行範圍，請選擇同一列中表的連續單元格，按一下右鍵所選內容，然後按一下 **[!UICONTROL 合併單元格]**。

>[!NOTE]
>
>建立行跨僅適用於最左側的單元格。

要將行標籤為行標題，請選擇行中的所有單元格，按一下右鍵所選內容，然後按一下 **[!UICONTROL 標籤標題]**。

要將單元格標籤為列標題，請選擇列中的任何單元格，按一下右鍵所選內容，然後按一下 **[!UICONTROL 標籤標題]**。

新限制 *可訪問表* 格式：

* 如果表中使用行範圍，則不支援可增長欄位
* 不支援嵌套表（表單元格中的表）
* 對行範圍的支援僅限於標題行和標題單元格
* 支助限於常規表
* 不支援行跨度> 1的表中的資料預填充
