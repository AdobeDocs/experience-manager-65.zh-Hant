---
title: 在HTML5表單中建立可存取的複雜表格
seo-title: 在HTML5表單中建立可存取的複雜表格
description: 了解如何在HTML5表單中建立可存取的表格。
seo-description: 了解如何在HTML5表單中建立可存取的表格。
uuid: e52562d2-4dc3-4359-9dbb-c18614921808
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
feature: 行動表單
exl-id: 3b8e3323-9ac4-4f5c-8c52-e2186e9169ea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# 在HTML5表單{#create-accessible-complex-tables-in-html-forms}中建立可存取的複雜表格

HTML5 Forms中表格的預設實作會使用HTML DIV元素來轉譯表格。 演算作業需使用ARIA角色，才能滿足協助工具的需求。

為避免螢幕助讀程式出現無法完全支援資料表使用的ARIA角色的協助工具問題，HTML5 Forms提供表格的替代轉譯。 這些表基於Designer中引入的新表格式，該格式還支援：

* 列標題
* 列跨

若要在HTML5 Forms中使用新格式，請將表格標示為複雜格式。 要將表標籤為複雜表，請按如下方式在表子表單的XML源中添加`extras`標籤：

```xml
</extras>
 <text name="complexTable">1</text>
 </extras>
```

標示為&#x200B;*complexTable*&#x200B;的表會遵循原生HTML格式副本，並為某些螢幕閱讀器提供更好的協助工具支援。  要建立行範圍，請選擇同一列中表的連續單元格，按一下右鍵選擇，然後按一下&#x200B;**[!UICONTROL 合併單元格]**。

>[!NOTE]
>
>建立列跨只適用於最左側的儲存格。

要將行標籤為行標題，請選擇行中的所有單元格，按一下右鍵選擇，然後按一下&#x200B;**[!UICONTROL 標籤標題]**。

要將單元格標籤為列標題，請選擇列中的任何單元格，按一下右鍵選擇內容，然後按一下&#x200B;**[!UICONTROL 標籤標題]**。

新&#x200B;*AccessibleTable*&#x200B;格式的限制：

* 如果表中使用行範圍，則不支援可增長欄位
* 不支援嵌套表（表單元格內的表）
* 對行跨的支援僅限於標題行和標題單元格
* 支援僅限於常規表
* 不支援以rowspan > 1填入表格
