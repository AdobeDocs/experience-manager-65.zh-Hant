---
title: 通過電子郵件發送表單提交確認
seo-title: Sending a form submission acknowledgement via email
description: AEM Forms允許您配置電子郵件提交操作，在提交表單時向用戶發送確認。
seo-description: AEM Forms allows you to configure the email submit action that sends an acknowledgement to a user on submitting the form.
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
exl-id: bca4044a-18a9-4b97-92de-eff1e9a840f9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# 通過電子郵件發送表單提交確認 {#sending-a-form-submission-acknowledgement-via-email}

## 自適應表單資料提交 {#adaptive-form-data-submission}

自適應表單提供多種現成功能 [提交操作](../../forms/using/configuring-submit-actions.md) 將表單資料提交到不同終結點的工作流。

例如， **[!UICONTROL 發送電子郵件]** 提交操作在成功提交自適應表單時發送電子郵件。 還可以配置它以發送電子郵件中的表單資料和PDF。

本文詳細介紹了在自適應表單上啟用電子郵件操作的步驟及其提供的不同配置。

>[!NOTE]
>
>您還可以使用 **[!UICONTROL 通過電子郵件發送PDF]** 按鈕，將選定控制項在Tab鍵次序中下移一個位置。 此操作可用的配置選項與 **[!UICONTROL 發送電子郵件]** 操作。 「電子郵件PDF」操作僅對基於XFA的自適應表單可用

## 發送電子郵件操作 {#email-action}

通過「發送電子郵件」(Send e-mail)操作，作者可以在成功提交自適應表單時自動向一個或多個收件人發送電子郵件。

>[!NOTE]
>
>要使用「發送電子郵件」操作，您需要按照中AEM所述配置郵件服務 [配置郵件服務](/help/sites-administering/notification.md#configuring-the-mail-service)。

### 在自適應窗體上啟用「發送電子郵件」操作 {#enabling-email-action-on-an-adaptive-form}

1. 在中開啟自適應窗體 **[!UICONTROL 編輯]** 的子菜單。

1. 在 **[!UICONTROL 內容]** 頁籤，點擊 **[!UICONTROL 窗體容器]** 點擊 ![配置](assets/configure-icon.svg) 的子菜單。

1. 在 **[!UICONTROL 提交]** 選擇 **[!UICONTROL 發送電子郵件]** 從 **[!UICONTROL 提交操作]** 的子菜單。

   ![提交操作](assets/submission-actions.png)

1. 在 **[!UICONTROL 至]**。 **[!UICONTROL 抄送]**, **[!UICONTROL 密件抄送]** 的子菜單。

   在中指定電子郵件的主題和正文 **[!UICONTROL 主題]** 和 **[!UICONTROL 電子郵件模板]** 的下界。

   也可以在欄位中指定變數佔位符，在這種情況下，當最終用戶成功提交表單時，將處理欄位的值。 有關詳細資訊，請參見 [使用自適應表單域名動態建立電子郵件內容](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p)。

   選擇 **[!UICONTROL 包括附件]** 如果表單包含檔案附件，並且您希望在電子郵件中附加這些檔案。

   >[!NOTE]
   >
   >如果選擇 **[!UICONTROL 通過電子郵件發送PDF]** 選項。

1. 按一下 ![保存](assets/save_icon.svg) 的子菜單。

### 使用自適應表單域名動態建立電子郵件內容 {#using-adaptive-form-field-names-to-dynamically-create-email-content}

自適應表單中的欄位名稱稱為佔位符，用戶提交表單後，這些佔位符將替換為該欄位的值。

在 **[!UICONTROL 發送電子郵件]** 操作中，可以使用執行操作時處理的佔位符。 它意味著電子郵件的標題(如 **[!UICONTROL 至]**。 **[!UICONTROL 抄送]**。 **[!UICONTROL 密件抄送]**。 **[!UICONTROL 主題]**)。

要定義佔位符，請指定 `${<field name>}` 在 **[!UICONTROL 發送電子郵件]** 作為「提交操作」。

例如，如果窗體包含 **[!UICONTROL 電子郵件地址]** 欄位，命名 `email_addr`，要捕獲用戶的電子郵件ID，可以在 **[!UICONTROL 至]**。 **[!UICONTROL 抄送]**&#x200B;或 **[!UICONTROL 密件抄送]** 的子菜單。

`${email_addr}`

當用戶提交表單時，會向在 `email_addr` 的子菜單。

>[!NOTE]
>
>您可以在 **[!UICONTROL 編輯]** 對話框。

變數佔位符也可用於 **[!UICONTROL 主題]** 和 **[!UICONTROL 電子郵件模板]** 的子菜單。

例如：

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>可重複面板中的欄位不能用作變數佔位符。
