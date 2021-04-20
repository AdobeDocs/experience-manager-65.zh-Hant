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
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---


# 在HTML5表單{#create-accessible-complex-tables-in-html-forms}中建立可存取的複雜表格

HTML5Forms中表格的預設實作使用HTML DIV元素來轉換表格。 演算包括使用ARIA角色來滿足無障礙環境支援需求。

為避免螢幕閱讀程式的無障礙環境支援問題，HTML5Forms提供表格的替代轉譯。 這些表基於Designer中引入的新表格格式，它還支援：

* 列標題
* 列跨

若要在HTML5Forms中使用新格式，請將表格標示為複雜表格。 要將表標籤為複雜，請按如下方式在表子表單的XML源中添加`extras`標籤：

```xml
</extras>
 <text name="complexTable">1</text>
 </extras>
```

標示為&#x200B;*complexTable*&#x200B;的表格會遵循原生HTML轉譯，並為某些螢幕閱讀程式提供更佳的協助工具支援。  要建立行範圍，請選擇同一列中表的連續單元格，按一下右鍵該選項，然後按一下&#x200B;**[!UICONTROL 合併單元格]**。

>[!NOTE]
>
>建立列範圍僅適用於最左側的儲存格。

要將行標籤為行標題，請選擇行中的所有單元格，按一下右鍵選擇內容，然後按一下&#x200B;**[!UICONTROL 標籤標題]**。

要將單元格標籤為列標題，請選擇列中的任何單元格，按一下右鍵選擇內容，然後按一下&#x200B;**[!UICONTROL 標籤標題]**。

新&#x200B;*AccessibleTable*&#x200B;格式的限制：

* 如果表中使用瀏覽範圍，則不支援可擴展欄位
* 不支援嵌套表（表單元格中的表）
* 對rowspan的支援僅限於標題列和標題儲存格
* 支援限於一般表格
* 不支援以瀏覽範圍> 1填入表格的資料預填

