---
title: 配置驗證消息
seo-title: 配置驗證消息
description: 瞭解如何指定驗證訊息的顯示方式及其相對於網頁瀏覽器中傳回表單的位置。
seo-description: 瞭解如何指定驗證訊息的顯示方式及其相對於網頁瀏覽器中傳回表單的位置。
uuid: f6bff4fa-f90f-4135-ae40-7ab3d3613122
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5f2f8129-e45e-4f3f-ae30-c09330d0e152
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 配置驗證消息 {#configuring-validation-messages}

對於呈現為HTML的表單，會為使用者顯示發生的表單驗證錯誤。 您可以自訂驗證訊息的顯示方式。 根據驗證消息的顯示位置，您還可以控制消息在表單中的位置以及框架邊框的大小。

## 指定驗證訊息的顯示方式 {#specify-how-validation-messages-are-displayed}

1. 在管理控制台中，按一下「服務>表格」。
1. 在「驗證輸出」下方的「報告」清單中，選取下列其中一個選項：

   **** 消息框：要在單獨的對話框中顯示驗證消息，請執行以下操作：

   **** 影格：顯示同一窗口框架內的驗證消息。

   **** 無框架：要在同一窗口中顯示驗證消息。 此值為預設值。

   **** 透過API（含資料）:若要透過API傳回驗證訊息（含資料）。 驗證訊息不會顯示在螢幕上。

   **** 透過API（含表單）:若要透過API傳回驗證訊息（使用表單）。 驗證訊息不會顯示在螢幕上。

   **** 無：不顯示驗證消息。

1. 按一下「儲存」。

## 指定驗證訊息相對於網頁瀏覽器中傳回的表單的位置 {#specify-the-location-of-validation-messages-relative-to-the-form-returned-in-the-web-browser}

當「報表」設為「影格」或「無影格」時，您可以指定驗證訊息的位置。

1. 在「驗證輸出」(Validation Output)的「位置」(Position)清單中，選擇以下選項之一：

   **** 左：在Web瀏覽器左側顯示驗證消息。

   **** 右：在Web瀏覽器的右側顯示驗證消息。

   **頂部**:若要在網頁瀏覽器頂端顯示驗證訊息。 此值為預設值。

   **底部**:若要在網頁瀏覽器底部顯示驗證訊息。

1. 按一下「儲存」。

## 指定影格邊框大小 {#specify-the-frame-border-size}

當「報表」設為「影格」時，您可以指定影格邊框大小。

1. 在「驗證輸出」的「邊框大小」方塊中，輸入影格邊框的大小（以像素為單位）。

   邊框大小必須等於或大於0。 預設值為1。

1. 按一下「儲存」。

