---
title: 在 HTML5 表單中建立無障礙的複雜表單
description: 瞭解如何在HTML5表單中建立無障礙的表格。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
feature: HTML5 Forms,Mobile Forms
exl-id: 3b8e3323-9ac4-4f5c-8c52-e2186e9169ea
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 5%
---
# 在 HTML5 表單中建立無障礙的複雜表單 {#create-accessible-complex-tables-in-html-forms}

HTML5 Forms中表格的預設實作使用HTML DIV元素來轉譯表格。 轉譯涉及使用ARIA角色來滿足協助工具需求。

為避免熒幕助讀程式無法完整支援資料表格所用ARIA角色的協助工具問題，HTML5 Forms提供表格的替代轉譯。 這些表格是根據Designer中推出的新表格格式，該格式也支援：

* 列標題
* 列範圍

若要在HTML5 Forms中使用新格式，請將表格標籤為複雜。 若要將資料表標籤為複雜，請在資料表子表單的XML來源中新增`extras`標籤，如下所示：

```xml
</extras>
 <text name="complexTable">1</text>
 </extras>
```

標示為&#x200B;*complexTable*&#x200B;的資料表會遵循原生HTML轉譯，並為某些熒幕閱讀程式提供更好的協助工具支援。  若要建立列範圍，請選取相同欄中表格的連續儲存格，以滑鼠右鍵按一下選取範圍，然後按一下&#x200B;**[!UICONTROL 合併儲存格]**。

>[!NOTE]
>
>建立列範圍僅適用於最左側的儲存格。

若要將列標示為列標題，請選取列中的所有儲存格，以滑鼠右鍵按一下選取範圍，然後按一下&#x200B;**[!UICONTROL 標示標題]**。

若要將儲存格標示為欄標題，請選取欄中的任何儲存格，以滑鼠右鍵按一下選取範圍，然後按一下&#x200B;**[!UICONTROL 標示標題]**。

新&#x200B;*AccessibleTable*&#x200B;格式的限制：

* 如果表格中使用了rowspan，將不支援可成長的欄位
* 不支援巢狀表格（表格儲存格內的表格）
* rowspan的支援僅限於標題列和標題儲存格
* 僅支援一般表格
* 在rowspan > 1的表格中不支援資料預填
