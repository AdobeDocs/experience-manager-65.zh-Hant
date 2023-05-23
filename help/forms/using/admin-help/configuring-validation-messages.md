---
title: 配置驗證消息
seo-title: Configuring validation messages
description: 瞭解如何指定驗證消息的顯示方式及其相對於在Web瀏覽器中返回的表單的位置。
seo-description: Learn how to specify how validation messages are displayed and their location relative to the form returned in the web browser.
uuid: f6bff4fa-f90f-4135-ae40-7ab3d3613122
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5f2f8129-e45e-4f3f-ae30-c09330d0e152
exl-id: 14314383-5228-4904-98c1-586f48a1142c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 2%

---

# 配置驗證消息 {#configuring-validation-messages}

對於呈現為HTML的表單，將為用戶顯示發生的表單驗證錯誤。 您可以自定義驗證消息的顯示方式。 根據驗證消息的顯示位置，您還可以控制表單中消息的位置以及框架邊框的大小。

## 指定驗證消息的顯示方式 {#specify-how-validation-messages-are-displayed}

1. 在管理控制台中，按一下「服務」>「表單」。
1. 在「驗證輸出」下，在「報告」清單中，選擇以下選項之一：

   **消息框：** 在單獨的對話框中顯示驗證消息。

   **框架：** 在同一窗口的幀內顯示驗證消息。

   **無幀：** 在同一窗口中顯示驗證消息。 此值為預設值。

   **通過API（含資料）:** 通過API（含資料）返回驗證消息。 驗證消息不顯示在螢幕上。

   **通過API（帶表單）:** 通過API返回驗證消息（使用表單）。 驗證消息不顯示在螢幕上。

   **無：** 不顯示驗證消息。

1. 按一下「儲存」。

## 指定驗證消息相對於在Web瀏覽器中返回的表單的位置 {#specify-the-location-of-validation-messages-relative-to-the-form-returned-in-the-web-browser}

將「報告」設定為「框架」或「無框架」時，可以指定驗證消息的位置。

1. 在「驗證輸出」(Validation Output)下，在「位置」(Position)清單中，選擇以下選項之一：

   **左：** 在Web瀏覽器左側顯示驗證消息。

   **對：** 在Web瀏覽器右側顯示驗證消息。

   **頂部**:在Web瀏覽器頂部顯示驗證消息。 此值為預設值。

   **底部**:在Web瀏覽器底部顯示驗證消息。

1. 按一下「儲存」。

## 指定框架邊框大小 {#specify-the-frame-border-size}

將「報告」設定為「幀」時，可以指定幀邊框大小。

1. 在「驗證輸出」下，在「邊框大小」框中，鍵入框邊框的大小（以像素為單位）。

   邊框大小必須等於或大於0。 預設值為 1。

1. 按一下「儲存」。
