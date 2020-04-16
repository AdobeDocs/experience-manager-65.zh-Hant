---
title: 透過電子郵件傳送表單提交確認
seo-title: 透過電子郵件傳送表單提交確認
description: AEM Forms可讓您設定電子郵件提交動作，在提交表單時傳送確認給使用者。
seo-description: AEM Forms可讓您設定電子郵件提交動作，在提交表單時傳送確認給使用者。
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
translation-type: tm+mt
source-git-commit: acc2a3977353386d7e1dfd1344a61d78812fe3fc

---


# 透過電子郵件傳送表單提交確認 {#sending-a-form-submission-acknowledgement-via-email}

## 最適化表單資料提交 {#adaptive-form-data-submission}

最適化表單提供數種立即可用的提交動 [作工作流程](../../forms/using/configuring-submit-actions.md) ，以將表單資料送出至不同的端點。

例如，「傳送電子 **[!UICONTROL 郵件]** 」提交動作會在成功提交最適化表單時傳送電子郵件。 您也可以設定它來傳送表單資料和電子郵件中的PDF。

本文詳細說明如何在最適化表單及其提供的不同組態上啟用「電子郵件」動作。

>[!NOTE]
>
>您也可以使用「透過電 **[!UICONTROL 子郵件傳送PDF]** 」選項，以電子郵件方式將填妥的表單傳送為PDF附件。 此動作的可用設定選項與「傳送電子郵件」動作的可用 **[!UICONTROL 選項]** 。 「電子郵件PDF」動作僅適用於XFA型調適性表單

## 傳送電子郵件動作 {#email-action}

「傳送電子郵件」動作可讓作者在成功提交調適性表單時，自動傳送電子郵件給一或多個收件者。

>[!NOTE]
>
>若要使用「傳送電子郵件」動作，您必須依照「設定郵件服務」中的說 [明設定AEM郵件服務](/help/sites-administering/notification.md#configuring-the-mail-service)。

### 在最適化表單上啟用「傳送電子郵件」動作 {#enabling-email-action-on-an-adaptive-form}

1. 在編輯模式中開啟最適 **[!UICONTROL 化表]** 格。

1. 在「內 **[!UICONTROL 容]** 」索引標籤中，點選「表單容器 **[!UICONTROL 」並點選]** 「設定 ![](assets/configure-icon.svg) 」以檢視最適化的表單屬性。

1. 在「提 **[!UICONTROL 交]** 」區段中，從「提交動作」下拉式清單中選取「傳送電子郵件 ******** 」。

   ![提交動作](assets/submission-actions.png)

1. 在「收件人」、「抄送」 **[!UICONTROL 和「密件抄送」欄位中]**，指定有效的電子郵件ID ******** 。

   分別在「主旨」和「電子郵件範本」欄位中 **[!UICONTROL 指定]****[!UICONTROL 電子郵件的主旨和內文]** 。

   您也可以在欄位中指定變數預留位置，此時，當使用者成功提交表單時，會處理欄位的值。 如需詳細資訊，請參 [閱「使用最適化表單欄位名稱動態建立電子郵件內容](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p)」。

   如果 **[!UICONTROL 表單包含檔案附件]** ，而您想在電子郵件中附加這些檔案，請選擇「包含附件」。

   >[!NOTE]
   >
   >如果您選擇「透過電 **[!UICONTROL 子郵件傳送PDF]** 」選項，則必須選取「包含附件」選項。

1. Click ![save](assets/save_icon.svg) to save the changes.

### 使用可調式表單欄位名稱動態建立電子郵件內容 {#using-adaptive-form-field-names-to-dynamically-create-email-content}

最適化表單中的欄位名稱稱為預留位置，在使用者提交表單後，會以該欄位的值取代。

在「傳 **[!UICONTROL 送電子郵件]** 」動作中，您可以使用在執行動作時處理的預留位置。 這表示當使用者提交表單時，會產生電子郵件的標題( **[!UICONTROL 例如To]**、 **[!UICONTROL CC]**、 **[!UICONTROL BCC]**、 **** SubjectSubject)。

若要定義預留位置，請在選 `${<field name>}` 取「傳送電子郵件」作 **[!UICONTROL 為「提交動作]** 」後，在欄位中指定。

例如，如果包含名為 **[!UICONTROL 「電子郵件地址]** 」的欄位，用於捕獲用戶的電子郵件ID，則可以在 `email_addr`To **[!UICONTROL 、]** CC ******** 、或BCC表單的JockT欄位中指定以下欄位。

`${email_addr}`

當使用者提交表格時，會傳送電子郵件至在表格欄位中輸入 `email_addr` 的電子郵件ID。

>[!NOTE]
>
>您可以在欄位的「編輯」對話方 **[!UICONTROL 塊中]** ，找到欄位名稱。

變數預留位置也可用於「主旨」 **[!UICONTROL 和「電子郵件]****[!UICONTROL 範本」欄位]** 。

例如：

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>可重複面板中的欄位不能用作變數預留位置。

