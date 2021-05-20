---
title: 啟用HTML5表單的附件
seo-title: 啟用HTML5表單的附件
description: 依預設，HTML5表單的附件支援已停用。
seo-description: 依預設，HTML5表單的附件支援已停用。
uuid: 2c62ac3e-4b27-46c7-a61d-a805fb5d26fb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
feature: 行動表單
exl-id: 68912260-179a-4d1b-b944-0a1777c021ac
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# 啟用HTML5表單{#enabling-attachments-for-an-html-form}的附件

您可以使用HTML5表單上傳、預覽和提交附件。 依預設，附件支援會停用。 要啟用附件支援，請執行以下操作：

1. 使用多選字串屬性`mfAttachmentOptions`建立[自訂設定檔](/help/forms/using/custom-profile.md)。
1. 在自訂設定檔中，指定屬性`fileSizeLimit`、`multiSelect`和`buttonTex`t ，以配置檔案附件小工具集的選項。 您也可以視需要指定更多自訂屬性。

1. 在自訂設定檔中，使用下列設定：

   * **multiSelect**  -> true或false（預設為true）
   * **fileSizeLimit**  -> value_in_mb（例如5）（預設為2 MB）
   * **buttonText**  ->快顯視窗的按鈕文字（預設為「Attach」）
   * **接受**  ->檔案類型以接受（預設為「audio/&amp;ast;, video/&amp;ast;, image/&amp;ast;, text/&amp;ast;, .pdf」）

   >[!NOTE]
   >
   >在Microsoft Internet Explorer 9中，用戶可以附加大於指定限制的檔案。 這是已知問題。

1. 使用[中繼資料編輯器](/help/forms/using/manage-form-metadata.md)來選取您已針對HTML 5表單在上述建立的自訂設定檔。
1. 使用自訂設定檔呈現您的表單範本，附件圖示會出現在表單工具列上。

   >[!NOTE]
   >
   >表單入口網站會立即提供已啟用草稿和附件功能的自訂設定檔。 如需&#x200B;**另存為草稿**&#x200B;設定檔的詳細資訊，請參閱[將HTML5表單儲存為草稿](/help/forms/using/saving-html5-form-draft.md)。

1. 按一下附件表徵圖，隨即出現附件選擇對話框。 瀏覽並選擇附件，然後按一下&#x200B;**Attach**。

   >[!NOTE]
   >
   >若要預覽附件，請按一下附件名稱。

   >[!NOTE]
   >
   >匿名用戶無法使用檔案預覽選項。

## 附件提交格式{#attachment-submission-format}

啟用附件時，HTML5表單會提交多部分資料。 多部分提交資料包含兩部分&#x200B;**dataXml**&#x200B;和&#x200B;**附件**。

>[!NOTE]
>
>為了向後相容性，如果`mfAllowAttachments`選項關閉，則HTML5表單不會傳送多部分資料。 它以&#x200B;**application/xml**&#x200B;格式發送簡單資料xml。

如果mfAllowAttachments標幟已開啟， [submit service proxy service](/help/forms/using/service-proxy.md)還會發佈包含dataXml和附件的多部分資料。
