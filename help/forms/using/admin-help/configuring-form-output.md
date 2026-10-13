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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 1%
---
# 設定表單輸出{#configuring-form-output}

## 指定傳回至網頁瀏覽器的HTML輸出型別 {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. 在Administration Console中，按一下「服務」 > 「表單」。
1. 在「表單輸出」下的「輸出型別」清單中，選取下列選項之一：

   **完整HTML：**&#x200B;若要在完整HTML標籤（完整的HTML頁面）中轉譯表單。 此值為預設值。

   **表單內文：**&#x200B;若要在`<BODY>`標籤內轉譯表單（不是完整的HTML頁面）。

1. 按一下「儲存」。

## 指定PDF內容的呈現位置 {#specify-the-location-where-pdf-content-is-rendered}

1. 在「表單輸出」下的「彩現於」清單中，選取下列其中一個選項：

   **使用者端：**&#x200B;在Adobe Acrobat或Adobe Reader中轉譯PDF forms。 使用者端轉譯可改善AEM表單的效能，且僅適用於PDF表單轉換。

   **伺服器：**&#x200B;若要在應用程式伺服器上呈現PDF forms。

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
1. 在JavaScript程式碼的head區段中宣告HTML變數__CUSTOM_SCRIPTS_VERSION)，並將其值設為1。

   >[!NOTE]
   >
   >*若要停用此功能，您可以移除JavaScript變數或將其值設為0。*
