---
title: 在「分配任務」步驟中使用自定義電子郵件模板
seo-title: Use custom email templates in an Assign Task step
description: 表單工作流電子郵件通知的自定義電子郵件模板
seo-description: Custom email templates for forms workflow email notifications
uuid: ba453d54-813f-4a4f-a82e-1a6a28b6939c
topic-tags: publish
discoiquuid: 2ad4b7b5-2162-4599-af3f-9476f1256de6
docset: aem65
exl-id: d4035c91-ee8d-4f12-bdac-e3912be732d7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 1%

---

# 在「分配任務」步驟中使用自定義電子郵件模板{#use-custom-email-templates-in-an-assign-task-step}

您可以使用分配任務步驟建立任務並將任務分配給用戶或組。 當將任務分配給用戶或組時，將向定義的用戶或定義的組的每個成員發送電子郵件通知。 典型的電子郵件通知包含已分配任務的連結和與任務相關的資訊。 下圖顯示示例電子郵件通知：

![帶開箱模板的電子郵件通知](do-not-localize/default_email_template_new.png)

您可以自定義外觀並在電子郵件通知中使用自定義元資料。 AEM Forms為電子郵件通知提供現成模板。 您可以自定義現成模板或從頭建立新模板。

電子郵件通知模板基於 [HTML電子郵件](https://en.wikipedia.org/wiki/HTML_email)。 這些電子郵件適用於不同的電子郵件客戶端和螢幕大小。 此外，電子郵件的樣式定義在模板中。

以下影像顯示自定義電子郵件通知：

![使用自定義模板發送電子郵件通知](do-not-localize/customized-email.png)

## 自定義現有模板 {#customize-the-existing-template}

現成，AEM Forms為電子郵件通知提供了模板。 模板提供了已分配任務的標題說明、到期日期、優先順序、工作流名稱和連結。 可以自定義模板以更改外觀。 執行以下步驟來自定義模板：

1. 使用管理員帳戶登錄到CRXDE。

1. 導航至/libs/fd/dashboard/templates/email。

1. 開啟htmlEmailTemplate.txt檔案。 它包含預設模板。

1. 將htmlEmailTemplate.txt檔案的內容替換為自定義內容。

   電子郵件通知模板是 [HTML電子郵件](https://en.wikipedia.org/wiki/HTML_email)。 可以用自定義代碼替換現有的html代碼以更改模板的外觀。

1. 儲存檔案。現在，自定義模板已準備就緒。

## 建立電子郵件模板 {#create-an-email-template}

現成，AEM Forms為電子郵件通知提供了模板。 模板提供了已分配任務的標題說明、到期日期、優先順序、工作流名稱和連結。 您還可以為「分配」任務步驟添加自定義電子郵件模板（您自己的模板）。 執行以下步驟以添加自定義電子郵件模板：

1. 使用管理員帳戶登錄到CRXDE。

1. 導航至/libs/fd/dashboard/templates/email。

1. 建立.txt檔案。 例如， EmailOnTaskAssign.txt。

1. 將自定義HTML代碼添加到檔案。

   電子郵件通知模板是 [HTML電子郵件](https://en.wikipedia.org/wiki/HTML_email)。 可以向檔案添加自定義HTML代碼以建立新模板。

1. 儲存檔案。該模板已準備好在「分配任務」步驟中使用。

## 在「分配任務」步驟中使用電子郵件模板 {#use-an-email-template-in-an-assign-task-step}

現在，「分配」任務步驟已配置為使用預設模板htmlEmailTemplate.txt。 您可以選擇使用自定義模板。 要更改模板：

1. 開啟「分配任務」步驟。

1. 定位至「工作負責人」>「HTML電子郵件模板」。

1. 選擇新建立的HTML電子郵件模板。

1. 按一下「確定」。模板已更改。

電子郵件通知還使用 [元資料](../../forms/using/use-metadata-in-email-notifications.md)。 例如，到期日、優先順序、工作流名稱等。 您還可以配置模板以使用 [自定義元資料](../../forms/using/use-metadata-in-email-notifications.md#using-custom-metadata-in-an-email-notification)。
