---
title: 配置表單輸出
seo-title: Configuring form output
description: 了解如何設定表單輸出。
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

## 指定傳回至網頁瀏覽器的HTML輸出類型 {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. 在管理控制台中，按一下「服務>表單」。
1. 在「表單輸出」(Form Output)下，在「輸出類型」(Output type)清單中，選擇以下選項之一：

   **完整HTML:** 在完整HTML標籤(完整HTML頁面)中呈現表單。 此值為預設值。

   **表單內文：** 在中呈現表單 `<BODY>` 標籤(不是完整的HTML頁面)。

1. 按一下「儲存」。

## 指定PDF內容呈現的位置 {#specify-the-location-where-pdf-content-is-rendered}

1. 在「表單輸出」下，在「呈現於」清單中，選擇以下選項之一：

   **客戶端：** 在Adobe Acrobat或Adobe Reader中呈現PDF forms。 用戶端轉譯可改善AEM表單的效能，且僅適用於PDFForm轉換。

   **伺服器：** 在應用程式伺服器上呈現PDF forms。

   **自動：** 在指定的位置中呈現PDF表單 `dynamicRender` XDP檔案的設定值。 此值為預設值。

1. 按一下「儲存」。

## 在表單提交前配置自定義指令碼的調用 {#configuring-invocation-of-custom-scripts-before-form-submit}

執行下列步驟以啟用功能：

1. 登入管理控制台。
1. 前往 **服務** > **表單**.
1. 將「輸出」類型指定為「表單主體」。
1. 儲存設定。
1. 在HTML程式碼的標題區段中宣告JavaScript變數__CUSTOM_SCRIPTS_VERSION，並將其值設為1。

   >[!NOTE]
   >
   >*若要停用功能，您可以移除JavaScript變數，或將其值設為0。*
