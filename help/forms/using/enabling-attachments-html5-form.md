---
title: 啟用HTML5窗體的附件
seo-title: Enabling attachments for an HTML5 form
description: 預設情況下，HTML5表單的附件支援被禁用。
seo-description: By default, the attachment support for HTML5 forms is disabled.
uuid: 2c62ac3e-4b27-46c7-a61d-a805fb5d26fb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
feature: Mobile Forms
exl-id: 68912260-179a-4d1b-b944-0a1777c021ac
source-git-commit: 6e2a0f053a1f6989524e9ae2b1dcb001b0397ac6
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 1%

---

# 啟用HTML5窗體的附件 {#enabling-attachments-for-an-html-form}

您可以使用HTML5表單上載、預覽和提交附件。 預設情況下，附件支援處於禁用狀態。 要啟用附件支援，請執行以下操作：

1. 建立 [自定義配置檔案](/help/forms/using/custom-profile.md) 帶 `mfAttachmentOptions` multiselect字串屬性。 中的每個字串 `mfAttachmentOptions` 屬性必須具有 `property=value` 格式，以配置檔案附件小部件的選項。 的 `property` 和 `value` 可以具有以下任何值：

   | 屬性 | 值 |
   |--- |---|
   | 多選擇 | true或false（預設為true） |
   | 檔案大小限制 | 以MB為單位（預設為2 MB）。 例如，5。 |
   | 按鈕文本 | 彈出窗口的按鈕文本（預設為「附加」） |
   | 接受 | 要接受的檔案類型的逗號分隔清單（預設情況下為「audio/&amp;ast;、video/&amp;ast;、image/&amp;ast;、text/&amp;ast;、.pdf」） |

   例如：

   ![配置選項](assets/mfAttachmentOptions.png)

   根據需要，還可以為 `mfAttachmentOptions` 屬性。

   >[!NOTE]
   >
   >在MicrosoftInternet Explorer 9中，用戶可以附加大於指定限制的檔案。 這是一個眾所周知的問題。

1. 使用 [元資料編輯器](/help/forms/using/manage-form-metadata.md) 選擇您為HTML5窗體建立的自定義配置檔案。
1. 使用自定義配置檔案呈現您的表單模板，附件表徵圖將顯示在表單工具欄上。

   >[!NOTE]
   >
   >開箱後，表單門戶將提供一個自定義配置檔案，並啟用了草稿和附件功能。 有關 **另存為草稿** 配置檔案，請參閱 [將HTML5窗體另存為草稿](/help/forms/using/saving-html5-form-draft.md)。

1. 按一下附件表徵圖，將出現附件選擇對話框。 瀏覽並選擇附件，然後按一下 **附加**。

   >[!NOTE]
   >
   >要預覽附件，請按一下附件名稱。

   >[!NOTE]
   >
   >檔案預覽選項對匿名用戶不可用。

## 附件提交格式 {#attachment-submission-format}

啟用附件後，HTML5表單將提交多部件資料。 多部分提交資料分為兩部分 **資料Xml** 和 **附件**。

>[!NOTE]
>
>為了向後相容，如果 `mfAllowAttachments` 選項，則HTML5窗體不會發送多部分資料。 它將簡單的資料xml **應用程式/xml** 的子菜單。

如果啟用了mfAllowAttachments標誌， [提交服務代理服務](/help/forms/using/service-proxy.md) 還會發佈包含dataXml和附件的多部件資料。
