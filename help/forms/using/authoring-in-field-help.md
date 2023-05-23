---
title: 為表單域創作上下文幫助
seo-title: Authoring in-context help for form fields
description: AEM Forms允許您將上下文幫助添加到自適應表單域和面板中，如文本或富媒體，包括視頻。
seo-description: AEM Forms allows you to add in-context help to adaptive form fields and panels, as text or rich media, including videos.
uuid: 1865bf7b-66fc-4f89-bd98-904daa409320
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 78000342-a6a7-4c2e-acab-a88851b82c2a
docset: aem65
feature: Adaptive Forms
exl-id: 6569bfba-9af5-4060-8640-e51d7af46614
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# 為表單域創作上下文幫助{#authoring-in-context-help-for-form-fields}

## 簡介 {#introduction}

有些情況下，填寫表單的最終用戶不確定如何在特定表單欄位中填寫詳細資訊。 要解決這些問題，自適應表單支援將文本或富上下文幫助添加到表單域。 它有助於改善表單填充體驗，避免最終用戶的歧義。

本文討論表單作者在創作Adaptive Forms時如何添加上下文幫助。

## 添加上下文幫助 {#add-in-context-help}

可以使用提要欄中「屬性」頁籤的「幫助內容」部分中的以下選項指定上下文中的幫助。

* [簡短描述](../../forms/using/authoring-in-field-help.md#p-short-description-p)
* [長描述](../../forms/using/authoring-in-field-help.md#p-long-description-p)

![表單域的上下文幫助](assets/descriptions.png)

>[!NOTE]
>
>長說明會覆蓋短說明。 如果已同時指定這兩個，則只顯示「長說明」。

### 簡短描述 {#short-description}

「簡短說明」(Short description)欄位用於提供有關填寫表單域的快速和簡短提示。 在「簡短說明」(Short description)欄位中指定的文本將作為懸停在該欄位上的滑鼠工具提示顯示。

![為表單域添加上下文幫助的簡短說明](assets/tooltip.png)

>[!NOTE]
>
>選擇 **始終顯示簡短說明** 來永久顯示該欄位下的幫助文本。

![域下的永久簡短上下文幫助](assets/short1.png)

### 長描述 {#long-description}

您可以使用「長說明」欄位指定長文本或嵌入富媒體內容（包括視頻），作為上下文幫助。 例如，下圖顯示了如何將視頻嵌入為上下文幫助。

![將富媒體添加為表單域的上下文幫助](assets/long-descriptions.png)

添加長說明顯示 **?** 表徵圖。 按一下該表徵圖將顯示在長說明部分中添加的內容。

![富媒體上下文幫助示例](assets/photoshop.png)

### 面板級幫助 {#panel-level-help}

除了表單域的上下文幫助外，還可以在面板編輯對話框的「幫助內容」頁籤的面板級別指定幫助。

![為表單面板添加上下文幫助](assets/panel-level-help.png)

為面板添加幫助顯示 **?** 表徵圖。 按一下該表徵圖將顯示在面板編輯對話框的「幫助內容」部分中添加的內容。

![窗體面板級上下文幫助示例](assets/photoshop-1.png)
