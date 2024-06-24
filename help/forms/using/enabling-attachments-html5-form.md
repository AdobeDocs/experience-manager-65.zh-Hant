---
title: 啟用HTML5表單的附件
description: 依預設，會停用HTML5表單的附件支援。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
feature: HTML5 Forms,Mobile Forms
exl-id: 68912260-179a-4d1b-b944-0a1777c021ac
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 1%

---

# 啟用HTML5表單的附件 {#enabling-attachments-for-an-html-form}

您可以透過HTML5表單上傳、預覽及提交附件。 依預設，會停用附件支援。 若要啟用附件支援：

1. 建立 [自訂設定檔](/help/forms/using/custom-profile.md) 與 `mfAttachmentOptions` multiselect string屬性。 每個字串 `mfAttachmentOptions` 屬性必須有 `property=value` 格式，以設定檔案附件小工具的選項。 此 `property` 和 `value` 可以有下列任一值：

   | 屬性 | 值 |
   |--- |---|
   | multiSelect | true或false （預設為true） |
   | fileSizeLimit | 以MB為單位的編號（預設為2 MB）。 例如，5。 |
   | 按鈕文字 | 快顯視窗的按鈕文字（預設為「附加」） |
   | 接受 | 要接受的檔案型別清單（預設為&quot;audio/&amp;ast；， video/&amp;ast；， image/&amp;ast；， text/&amp;ast；， .pdf&quot;），以逗號分隔 |

   例如：

   ![設定選項](assets/mfAttachmentOptions.png)

   如有需要，您也可以為「 」指定更多自訂選項 `mfAttachmentOptions` 屬性。

   >[!NOTE]
   >
   >在Microsoft Internet Explorer 9中，使用者可以附加超過指定限制的檔案。 這是已知問題。

1. 使用 [中繼資料編輯器](/help/forms/using/manage-form-metadata.md) 以選取您在上面為HTML5表單建立的自訂設定檔。
1. 使用自訂設定檔轉譯您的表單範本，表單工具列上會顯示附件圖示。

   >[!NOTE]
   >
   >Forms Portal提供開箱即用的自訂設定檔，並啟用草稿和附件功能。 如需關於的詳細資訊 **另存為草稿** 設定檔，請參閱 [將HTML5表單儲存為草稿](/help/forms/using/saving-html5-form-draft.md).

1. 按一下附件圖示，附件選取對話方塊就會顯示。 瀏覽並選取附件，然後按一下 **附加**.

   >[!NOTE]
   >
   >若要預覽附件，請按一下附件名稱。

   >[!NOTE]
   >
   >檔案預覽選項不適用於匿名使用者。

## 附件提交格式 {#attachment-submission-format}

啟用附件時，HTML5表單會提交多部分資料。 多部分提交資料分為兩部分 **dataXml** 和 **附件**.

>[!NOTE]
>
>若為回溯相容性，若 `mfAllowAttachments` 選項關閉，則HTML5表單不會傳送多部分資料。 它會傳送簡單資料xml於 **application/xml** 格式。

如果開啟mfAllowAttachments旗標， [送出服務Proxy服務](/help/forms/using/service-proxy.md) 也會張貼含有dataXml和附件的多部分資料。
