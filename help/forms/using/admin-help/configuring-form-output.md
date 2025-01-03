---
title: 設定表單輸出
description: 瞭解如何設定表單輸出。 若要設定表單輸出及啟用功能，請在表單提交前使用自訂指令碼。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d739806c-ce72-40fd-b304-3262a0988d96
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 1%

---

# 設定表單輸出{#configuring-form-output}

## 指定傳回網頁瀏覽器的HTML輸出型別 {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. 在Administration Console中，按一下「服務」 > 「表單」。
1. 在「表單輸出」下的「輸出型別」清單中，選取下列選項之一：

   **完整HTML：**&#x200B;若要在完整HTML標籤內轉譯表單(完整的HTML頁面)。 此值為預設值。

   **表單內文：**&#x200B;若要在`<BODY>`標籤內轉譯表單(不是完整的HTML頁面)。

1. 按一下「儲存」。

## 指定PDF內容的呈現位置 {#specify-the-location-where-pdf-content-is-rendered}

1. 在「表單輸出」下的「彩現於」清單中，選取下列其中一個選項：

   **使用者端：**&#x200B;在Adobe Acrobat或Adobe Reader中轉譯PDF forms。 使用者端轉譯可改善AEM表單的效能，且僅適用於PDF表單轉換。

   **伺服器：**&#x200B;在應用程式伺服器上轉譯PDF forms。

   **自動：**&#x200B;若要在XDP檔案的`dynamicRender`組態值所指定的位置轉譯PDF表單。 此值為預設值。

1. 按一下「儲存」。

## 在表單提交前設定自訂指令碼的引動過程 {#configuring-invocation-of-custom-scripts-before-form-submit}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

執行以下步驟來啟用此功能：

1. 登入管理主控台。
1. 移至&#x200B;**服務** > **表單**。
1. 將「輸出」型別指定為「表單主體」。
1. 儲存設定。
1. 在HTML程式碼的head區段中宣告JavaScript變數__CUSTOM_SCRIPTS_VERSION)，並將其值設為1。

   >[!NOTE]
   >
   >*若要停用此功能，您可以移除JavaScript變數或將其值設為0。*
