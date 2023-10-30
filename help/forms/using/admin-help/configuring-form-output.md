---
title: 設定表單輸出
description: 瞭解如何設定表單輸出。 若要設定表單輸出及啟用功能，請在表單提交前使用自訂指令碼。
uuid: 70aad14e-c845-4ef3-a751-ad8860d5d505
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 17c9b69a-3c6f-47e3-a828-841bb90eba8b
exl-id: d739806c-ce72-40fd-b304-3262a0988d96
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 1%

---

# 設定表單輸出{#configuring-form-output}

## 指定傳回網頁瀏覽器的HTML輸出型別 {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. 在Administration Console中，按一下「服務」 > 「表單」。
1. 在「表單輸出」下的「輸出型別」清單中，選取下列選項之一：

   **完整HTML：** 呈現完整HTML標籤內的表單(完整的HTML頁面)。 此值為預設值。

   **表單內文：** 若要在內呈現表單 `<BODY>` 標籤(非完整的HTML頁面)。

1. 按一下「儲存」。

## 指定PDF內容的呈現位置 {#specify-the-location-where-pdf-content-is-rendered}

1. 在「表單輸出」下的「彩現於」清單中，選取下列其中一個選項：

   **使用者端：** 若要在Adobe Acrobat或Adobe Reader中呈現PDF forms。 使用者端轉譯可改善AEM表單的效能，且僅適用於PDF表單轉換。

   **伺服器：** 在應用程式伺服器上呈現PDF forms。

   **自動：** 若要在指定的位置呈現PDF表單 `dynamicRender` xdp檔案的設定值。 此值為預設值。

1. 按一下「儲存」。

## 在表單提交前設定自訂指令碼的引動過程 {#configuring-invocation-of-custom-scripts-before-form-submit}

執行以下步驟來啟用此功能：

1. 登入管理主控台。
1. 前往 **服務** > **表單**.
1. 將「輸出」型別指定為「表單主體」。
1. 儲存設定。
1. 在HTML程式碼的head區段中宣告JavaScript變數__CUSTOM_SCRIPTS_VERSION)，並將其值設為1。

   >[!NOTE]
   >
   >*若要停用此功能，您可以移除JavaScript變數或將其值設為0。*
