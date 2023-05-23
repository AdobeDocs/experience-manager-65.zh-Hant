---
title: 配置表單輸出
seo-title: Configuring form output
description: 瞭解如何配置表單輸出。
seo-description: Learn how to configure form output.
uuid: 70aad14e-c845-4ef3-a751-ad8860d5d505
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 17c9b69a-3c6f-47e3-a828-841bb90eba8b
exl-id: d739806c-ce72-40fd-b304-3262a0988d96
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 1%

---

# 配置表單輸出{#configuring-form-output}

## 指定返回到Web瀏覽器的HTML輸出的類型 {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. 在管理控制台中，按一下「服務」>「表單」。
1. 在「表單輸出」(Form Output)下，在「輸出類型」(Output type)清單中，選擇以下選項之一：

   **完全HTML:** 在完整HTML標籤(完整HTML頁)中呈現表單。 此值為預設值。

   **窗體正文：** 在中呈現窗體 `<BODY>` 標籤(不是完整的HTML頁)。

1. 按一下「儲存」。

## 指定呈現PDF內容的位置 {#specify-the-location-where-pdf-content-is-rendered}

1. 在「表單輸出」(Form Output)下，在「渲染位置」(Render at)清單中，選擇以下選項之一：

   **客戶端：** 在Adobe Acrobat或Adobe Reader內PDF forms。 客戶端渲染提高了表單AEM的效能，並僅應用於PDFForm轉換。

   **伺服器：** 在應用程式伺服器上呈現PDF forms。

   **自動：** 在PDF指定的位置中呈現窗體 `dynamicRender` XDP檔案的配置值。 此值為預設值。

1. 按一下「儲存」。

## 配置在提交表單之前調用自定義指令碼 {#configuring-invocation-of-custom-scripts-before-form-submit}

執行以下步驟以啟用該功能：

1. 登錄到管理控制台。
1. 轉到 **服務** > **表**。
1. 將「輸出」類型指定為「表單主體」。
1. 保存設定。
1. 在HTML代碼的頭部分聲明JavaScript變數__CUSTOM_SCRIPTS_VERSION，並將其值設定為1。

   >[!NOTE]
   >
   >*要禁用該功能，可刪除JavaScript變數或將其值設定為0。*
