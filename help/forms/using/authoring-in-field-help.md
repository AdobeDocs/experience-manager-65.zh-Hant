---
title: 製作表格欄位的內容相關說明
seo-title: 製作表格欄位的內容相關說明
description: AEM Forms可讓您將內容相關說明新增至最適化表單欄位和面板，例如文字或多媒體，包括影片。
seo-description: AEM Forms可讓您將內容相關說明新增至最適化表單欄位和面板，例如文字或多媒體，包括影片。
uuid: 1865bf7b-66fc-4f89-bd98-904daa409320
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 78000342-a6a7-4c2e-acab-a88851b82c2a
docset: aem65
translation-type: tm+mt
source-git-commit: 8bc99ed3817398ae358d439a5c1fcc90bbd24327

---


# 製作表格欄位的內容相關說明{#authoring-in-context-help-for-form-fields}

## 簡介 {#introduction}

有些情況下，一般使用者在填寫表格時無法確定如何在特定表格欄位中填寫詳細資料。 為瞭解決這些問題，最適化表單支援在表單欄位中新增文字或豐富式內容說明。 它有助於改善表單填寫體驗，並避免使用者的歧義。

本文討論表單作者在製作最適化表單時如何新增內容相關說明。

## 新增內容相關說明 {#add-in-context-help}

您可以使用側邊欄屬性標籤的「說明內容」區段中的下列選項，來指定內容相關說明。

* [簡短說明](../../forms/using/authoring-in-field-help.md#p-short-description-p)
* [詳細說明](../../forms/using/authoring-in-field-help.md#p-long-description-p)

![表格欄位的內容相關說明](assets/descriptions.png)

>[!NOTE]
>
>詳細說明會覆寫「簡短說明」。 如果您同時指定了兩者，則只會顯示「詳細說明」。

### Short description {#short-description}

「簡短說明」欄位是提供填入表單欄位的快速和簡短提示。 將滑鼠暫留在欄位上時，「簡短說明」欄位中指定的文字會顯示為工具提示。

![新增表格欄位內文說明的簡短說明](assets/tooltip.png)

>[!NOTE]
>
>選擇「 **永遠顯示簡短說明** 」，在欄位下方永久顯示說明文字。

![欄位下方的永久簡短內容相關說明](assets/short1.png)

### Long description {#long-description}

您可以使用「詳細說明」欄位來指定長篇文字或內嵌多媒體內容，包括視訊，做為內容相關說明。 例如，下圖顯示如何將視訊內嵌為內容相關說明。

![新增豐富式媒體作為表格欄位的內容相關說明](assets/long-descriptions.png)

新增詳細說明會顯示 **?** 表徵圖。 按一下圖示會顯示在詳細說明區段中新增的內容。

![豐富式媒體內容相關說明範例](assets/photoshop.png)

### 面板層級說明 {#panel-level-help}

除了表格欄位的內容相關說明外，您也可以在面板編輯對話方塊的「說明內容」索引標籤中，在面板層級指定說明。

![新增表格面板的內容相關說明](assets/panel-level-help.png)

新增面板說明時，會顯示 **?** 表徵圖。 按一下圖示會顯示在面板編輯對話方塊的「說明內容」區段中新增的內容。

![表單面板層級的內容相關說明範例](assets/photoshop-1.png)

