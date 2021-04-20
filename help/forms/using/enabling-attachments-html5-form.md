---
title: 啟用HTML5表單的附件
seo-title: 啟用HTML5表單的附件
description: 依預設，HTML5表單的附件支援會停用。
seo-description: 依預設，HTML5表單的附件支援會停用。
uuid: 2c62ac3e-4b27-46c7-a61d-a805fb5d26fb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# 啟用HTML5表單{#enabling-attachments-for-an-html-form}的附件

您可以使用HTML5表單上傳、預覽和送出附件。 預設情況下，附件支援被禁用。 要啟用附件支援，請執行以下操作：

1. 使用多選字串屬性`mfAttachmentOptions`建立[自訂描述檔](/help/forms/using/custom-profile.md)。
1. 在自訂描述檔中，指定屬性`fileSizeLimit`、`multiSelect`和`buttonTex`t，以設定檔案附件介面工具集的選項。 您也可以視需要指定更多自訂屬性。

1. 在自訂描述檔中，請使用下列組態：

   * **multiSelect** -> true或false（預設為true）
   * **fileSizeLimit** -> value_in_mb(say 5)（預設為2 MB）
   * **buttonText** ->快顯視窗的按鈕文字（預設為「附加」）
   * **accept** ->檔案類型以接受（預設為&quot;audio/&amp;ast;, video/&amp;ast;, image/&amp;ast;, text/&amp;ast;, .pdf&quot;）

   >[!NOTE]
   >
   >在Microsoft Internet Explorer 9中，使用者可附加超過指定限制的檔案。 這是已知問題。

1. 使用[中繼資料編輯器](/help/forms/using/manage-form-metadata.md)來選擇您為HTML 5表單上方建立的自訂描述檔。
1. 使用自訂描述檔來轉換您的表單範本，附件圖示會顯示在表單工具列上。

   >[!NOTE]
   >
   >現成可用的表單入口網站提供自訂描述檔，並啟用草稿和附件功能。 如需&#x200B;**另存為草稿**&#x200B;描述檔的詳細資訊，請參閱[將HTML5表單儲存為草稿](/help/forms/using/saving-html5-form-draft.md)。

1. 按一下附件表徵圖，將出現附件選擇對話框。 瀏覽並選擇附件，然後按一下&#x200B;**Attach**。

   >[!NOTE]
   >
   >要預覽附件，請按一下附件名稱。

   >[!NOTE]
   >
   >匿名使用者無法使用檔案預覽選項。

## 附件提交格式{#attachment-submission-format}

啟用附件後，HTML5表單會提交多部件資料。 多部件提交資料具有兩個部件&#x200B;**dataXml**&#x200B;和&#x200B;**附件**。

>[!NOTE]
>
>為了向後相容性，如果`mfAllowAttachments`選項已關閉，則HTML5表格不會傳送多部分資料。 它以&#x200B;**application/xml**&#x200B;格式發送簡單資料xml。

如果mfAllowAttachments標幟已開啟，[submit service proxy service](/help/forms/using/service-proxy.md)也會以dataXml和附件發佈多部分資料。
