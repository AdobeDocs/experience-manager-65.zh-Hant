---
title: 啟用HTML5表單的附件
seo-title: Enabling attachments for an HTML5 form
description: 依預設，會停用HTML5表單的附件支援。
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

# 啟用HTML5表單的附件 {#enabling-attachments-for-an-html-form}

您可以使用HTML5表單上傳、預覽和提交附件。 依預設，附件支援會停用。 要啟用附件支援，請執行以下操作：

1. 建立 [自訂設定檔](/help/forms/using/custom-profile.md) 帶 `mfAttachmentOptions` 多選字串屬性。 中的每個字串 `mfAttachmentOptions` 屬性必須具有 `property=value` 格式來配置檔案附件小工具集的選項。 此 `property` 和 `value` 可以有下列任一值：

   | 屬性 | 值 |
   |--- |---|
   | multiSelect | true或false（預設為true） |
   | fileSizeLimit | 以MB為單位的數字（預設為2 MB）。 例如5。 |
   | buttonText | 彈出式視窗的按鈕文字（預設為「附加」） |
   | 接受 | 要接受的檔案類型清單（預設為「audio/&amp;ast;, video/&amp;ast;, image/&amp;ast;, text/&amp;ast;, .pdf」） |

   例如：

   ![配置選項](assets/mfAttachmentOptions.png)

   您也可以視需要為 `mfAttachmentOptions` 屬性。

   >[!NOTE]
   >
   >在Microsoft Internet Explorer 9中，用戶可以附加大於指定限制的檔案。 這是已知問題。

1. 使用 [中繼資料編輯器](/help/forms/using/manage-form-metadata.md) 選取您為HTML5表單上建立的自訂設定檔。
1. 使用自訂設定檔呈現您的表單範本，附件圖示會出現在表單工具列上。

   >[!NOTE]
   >
   >表單入口網站會立即提供已啟用草稿和附件功能的自訂設定檔。 如需 **另存為草稿** 設定檔，請參閱 [將HTML5表單儲存為草稿](/help/forms/using/saving-html5-form-draft.md).

1. 按一下附件表徵圖，隨即出現附件選擇對話框。 瀏覽並選取附件，然後按一下 **附加**.

   >[!NOTE]
   >
   >若要預覽附件，請按一下附件名稱。

   >[!NOTE]
   >
   >匿名用戶無法使用檔案預覽選項。

## 附件提交格式 {#attachment-submission-format}

啟用附件時，HTML5表單會提交多部分資料。 多部分提交資料包含兩部分 **dataXml** 和 **附件**.

>[!NOTE]
>
>為了回溯相容性，如果 `mfAllowAttachments` 選項關閉，則HTML5表單不會傳送多部分資料。 它會在 **application/xml** 格式。

如果mfAllowAttachments標幟已開啟，則 [提交服務代理服務](/help/forms/using/service-proxy.md) 也會發佈包含dataXml和附件的多部分資料。
