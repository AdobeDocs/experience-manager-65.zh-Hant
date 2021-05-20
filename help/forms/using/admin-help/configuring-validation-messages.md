---
title: 設定驗證訊息
seo-title: 設定驗證訊息
description: 了解如何指定驗證訊息的顯示方式及其相對於網頁瀏覽器中傳回的表單的位置。
seo-description: 了解如何指定驗證訊息的顯示方式及其相對於網頁瀏覽器中傳回的表單的位置。
uuid: f6bff4fa-f90f-4135-ae40-7ab3d3613122
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5f2f8129-e45e-4f3f-ae30-c09330d0e152
exl-id: 14314383-5228-4904-98c1-586f48a1142c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 2%

---

# 配置驗證消息{#configuring-validation-messages}

對於以HTML呈現的表單，會為使用者顯示發生的表單驗證錯誤。 您可以自訂驗證訊息的顯示方式。 根據驗證消息的顯示位置，您還可以控制窗體中消息的位置和框架邊框的大小。

## 指定驗證消息的顯示方式{#specify-how-validation-messages-are-displayed}

1. 在管理控制台中，按一下「服務>表單」。
1. 在「驗證輸出」下，在「報告」清單中，選擇以下選項之一：

   **訊息方塊：** 在個別對話方塊中顯示驗證訊息。

   **框架：** 在同一窗口的框架內顯示驗證消息。

   **無框架：** 在同一窗口中顯示驗證消息。此值為預設值。

   **透過API（含資料）:** 透過API（含資料）傳回驗證訊息。驗證訊息不會顯示在畫面上。

   **透過API（含表單）:** 透過API（含表單）傳回驗證訊息。驗證訊息不會顯示在畫面上。

   **無：** 不顯示驗證訊息。

1. 按一下「儲存」。

## 指定與在Web瀏覽器{#specify-the-location-of-validation-messages-relative-to-the-form-returned-in-the-web-browser}中返回的表單相對的驗證消息的位置

當「報告」設定為「幀」或「無幀」時，可以指定驗證消息的位置。

1. 在「驗證輸出」(Validation Output)下，在「位置」(Position)清單中，選擇以下選項之一：

   **左側：** 在Web瀏覽器左側顯示驗證訊息。

   **右：** 在Web瀏覽器的右側顯示驗證訊息。

   **排名**:在Web瀏覽器頂部顯示驗證消息。此值為預設值。

   **底部**:在Web瀏覽器底部顯示驗證消息。

1. 按一下「儲存」。

## 指定幀邊框大小{#specify-the-frame-border-size}

當「報告」設定為「框架」時，可以指定框架邊框大小。

1. 在「驗證輸出」下的「邊框大小」框中，以像素為單位鍵入邊框的大小。

   邊框大小必須等於或大於0。 預設值為 1。

1. 按一下「儲存」。
