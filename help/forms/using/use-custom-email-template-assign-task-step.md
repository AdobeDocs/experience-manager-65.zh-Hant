---
title: 在「指派工作」步驟中使用自訂電子郵件範本
seo-title: 在「指派工作」步驟中使用自訂電子郵件範本
description: '表單工作流程電子郵件通知的自訂電子郵件範本 '
seo-description: '表單工作流程電子郵件通知的自訂電子郵件範本 '
uuid: ba453d54-813f-4a4f-a82e-1a6a28b6939c
topic-tags: publish
discoiquuid: 2ad4b7b5-2162-4599-af3f-9476f1256de6
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247

---


# 在「指派工作」步驟中使用自訂電子郵件範本{#use-custom-email-templates-in-an-assign-task-step}

您可以使用「指派任務」步驟來建立任務並指派給使用者或群組。 將任務指派給用戶或組時，會向已定義用戶或已定義組的每個成員發送電子郵件通知。 典型的電子郵件通知包含指派任務的連結和與任務相關的資訊。 下列影像顯示範例電子郵件通知：

![立即可用的電子郵件通知範本](do-not-localize/default_email_template_new.png)

您可以自訂外觀，並在電子郵件通知中使用自訂中繼資料。 AEM Forms為電子郵件通知提供現成可用的範本。 您可以自訂現成可用的範本，或從頭開始建立新範本。

電子郵件通知範本是以 [HTML電子郵件為基礎](https://en.wikipedia.org/wiki/HTML_email)。 這些電子郵件會根據不同的電子郵件客戶和螢幕大小進行調整。 此外，電子郵件的樣式是在範本中定義。

下列影像會顯示自訂的電子郵件通知：

![使用自訂範本的電子郵件通知](do-not-localize/customized-email.png)

## 自訂現有範本 {#customize-the-existing-template}

AEM Forms現成可用，提供電子郵件通知的範本。 此範本提供標題說明、到期日、優先順序、工作流程名稱，以及指派任務的連結。 您可以自訂範本以變更外觀。 執行下列步驟以自訂範本：

1. 使用管理員帳戶登入CRXDE。

1. 導覽至/libs/fd/dashboard/templates/email。

1. 開啟htmlEmailTemplate.txt檔案。 它包含預設範本。

1. 以自訂內容取代htmlEmailTemplate.txt檔案的內容。

   電子郵件通知範本是 [HTML電子郵件](https://en.wikipedia.org/wiki/HTML_email)。 您可以將現有的html程式碼取代為自訂程式碼，以變更範本的外觀。

1. 儲存檔案。 現在，自訂範本已可供使用。

## 建立電子郵件範本 {#create-an-email-template}

AEM Forms現成可用，提供電子郵件通知的範本。 此範本提供標題說明、到期日、優先順序、工作流程名稱，以及指派任務的連結。 您也可以為「指派」工作步驟新增自訂電子郵件範本（您自己的範本）。 執行下列步驟以新增自訂電子郵件範本：

1. 使用管理員帳戶登入CRXDE。

1. 導覽至/libs/fd/dashboard/templates/email。

1. 建立。txt檔案。 例如，EmailOnTaskAssign.txt。

1. 新增自訂HTML程式碼至檔案。

   電子郵件通知範本是 [HTML電子郵件](https://en.wikipedia.org/wiki/HTML_email)。 您可以將自訂HTML程式碼新增至檔案，以建立新範本。

1. 儲存檔案。 模板已準備好供「分配任務」步驟使用。

## 在「分配任務」步驟中使用電子郵件模板 {#use-an-email-template-in-an-assign-task-step}

現成可用的「指派任務」步驟已設定為使用預設範本htmlEmailTemplate.txt。 您可以選擇使用自訂範本。 要更改模板，請執行以下操作：

1. 開啟「指派任務」步驟。

1. 導覽至「受託人> HTML電子郵件範本」。

1. 選取新建立的HTML電子郵件範本。

1. 按一下「確定」。 範本已變更。

電子郵件通知也使用中 [繼資料](../../forms/using/use-metadata-in-email-notifications.md)。 例如，到期日、優先順序、工作流程名稱等。 您也可以設定範本以使用自訂 [中繼資料](../../forms/using/use-metadata-in-email-notifications.md#using-custom-metadata-in-an-email-notification)。
