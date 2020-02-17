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
translation-type: tm+mt
source-git-commit: 00e14be8a0775149b3ee7ce8cd781dd7f1e49e4f

---


# 啟用HTML5表單的附件 {#enabling-attachments-for-an-html-form}

您可以使用HTML5表單上傳、預覽和送出附件。 預設情況下，附件支援被禁用。 要啟用附件支援，請執行以下操作：

1. 使用多選 [字串屬性](/help/forms/using/custom-profile.md) ，建立自訂描述檔 `mfAttachmentOptions`。
1. 在自訂描述檔中，指定 `fileSizeLimit`屬性 `multiSelect`和 `buttonTex`t，以設定檔案附件介面工具集的選項。 您也可以視需要指定更多自訂屬性。

1. 在自訂描述檔中，請使用下列組態：

   * **multiSelect** -> true或false（預設為true）
   * **fileSizeLimit** -> value_in_mb(say 5)（預設為2 MB）
   * **buttonText** ->快顯視窗的按鈕文字（預設為「附加」）
   * **accept** -> file types to accept（&quot;audio/&amp;ast;, video/&amp;ast;, image/&amp;ast;, text/&amp;ast;, .pdf&quot;，預設）
   >[!NOTE]
   >
   >在Microsoft Internet Explorer 9中，使用者可附加超過指定限制的檔案。 這是已知問題。

1. 使用中 [繼資料編輯器](/help/forms/using/manage-form-metadata.md) ，選取您為HTML 5表格上建立的自訂描述檔。
1. 使用自訂描述檔來轉換您的表單範本，附件圖示會顯示在表單工具列上。

   >[!NOTE]
   >
   >現成可用的表單入口網站提供自訂描述檔，並啟用草稿和附件功能。 如需「另存為草稿」描述 **檔的詳細資訊** ，請參 [閱「將HTML5表單另存為草稿」](/help/forms/using/saving-html5-form-draft.md)。

1. 按一下附件表徵圖，將出現附件選擇對話框。 瀏覽並選擇附件，然後按一下「 **附加」**。

   >[!NOTE]
   >
   >要預覽附件，請按一下附件名稱。

   >[!NOTE]
   >
   >匿名使用者無法使用檔案預覽選項。

## 附件提交格式 {#attachment-submission-format}

啟用附件後，HTML5表單會提交多部件資料。 多部分提交資料包含兩部分 **dataXml** 和附 **件**。

>[!NOTE]
>
>為了向後相容性， `mfAllowAttachments` 如果關閉選項，HTML5表單就不會傳送多部分資料。 它以應用程式/xml格式傳 **送簡單的資料xml** 。

如果已開啟mfAllowAttachments標幟，送出服務 [proxy服務](/help/forms/using/service-proxy.md) ，也會使用dataXml和附件發佈多部分資料。
