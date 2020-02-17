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
source-git-commit: 94472fad34fe97740e4711d2cb35beb884db52ce

---


# 透過電子郵件傳送表單提交確認{#sending-a-form-submission-acknowledgement-via-email}

## 最適化表單資料提交 {#adaptive-form-data-submission}

最適化表單提供數種立即可用的提交動 [作工作流程](../../forms/using/configuring-submit-actions.md) ，以將表單資料送出至不同的端點。

例如，「電子郵 **件」動作** 「提交」動作會在成功提交最適化表單時傳送電子郵件。 您也可以設定它來傳送表單資料和電子郵件中的PDF。

本文詳細說明如何在最適化表單及其提供的不同組態上啟用「電子郵件」動作。

>[!NOTE]
>
>您也可以使用「電子郵 **件PDF」動作** ，以電子郵件的方式傳送已完成的表單作為PDF附件。 此動作的可用設定選項與「電子郵件」動作的可用選項相同。 「電子郵件PDF」動作僅適用於XFA型調適性表單

## Email action {#email-action}

「電子郵件」動作可讓作者在成功提交調適性表單時，自動傳送電子郵件給一或多個收件者。

>[!NOTE]
>
>若要使用「電子郵件」動作，您必須依照 [Configuring the mail service](/help/sites-administering/notification.md#configuring the mail service)中所述，設定AEM郵件服務。

### 在最適化表單上啟用電子郵件動作 {#enabling-email-action-on-an-adaptive-form}

1. 在編輯模式中開啟最適化表單。

1. 按一下 **Adaptive Form** (最適化表 **單)工具欄的Start（開始）旁邊的Edit** （編輯）。

   「編輯元件」(Edit Component)對話框隨即開啟。

   ![最適化表單的編輯元件對話方塊](assets/start_of_adp_form.png)

1. 選擇「 **提交動作** 」標籤，並從「提 **交動作」下拉式清單中選擇「電子郵件動作** 」。

   該頁籤顯示為當前表單配置「電子郵件」操作的選項。

   ![「提交操作」頁籤](assets/dialog.png)

1. 在「郵件收件人」、「抄送」和「密件副本」欄位中指定有效的電子郵件ID。

   分別在「主旨」和「電子郵件」範本欄位中指定電子郵件的主旨和內文。

   您也可以在欄位中指定變數預留位置，此時，當使用者成功提交表單時，會處理欄位的值。 如需詳細資訊，請參 [閱「使用最適化表單欄位名稱動態建立電子郵件內容](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p)」。

   如果表單包含檔案附件，而您想在電子郵件中附加這些檔案，請選擇「包含附件」。

   >[!NOTE]
   >
   >如果您選擇「電子郵 **件PDF」動作**，則必須選取「包含附件」選項。

1. 按一下 **確定** ，保存更改。

### 使用可調式表單欄位名稱動態建立電子郵件內容 {#using-adaptive-form-field-names-to-dynamically-create-email-content}

最適化表單中的欄位名稱稱為預留位置，在使用者提交表單後，會以該欄位的值取代。

在「電子郵件」動作標籤中，您可以使用在執行動作時處理的預留位置。 這表示當使用者提交表單時，會產生電子郵件的標題（例如Mailto、CC、BCC、主旨）。

要定義佔位符，請在「提交 `${<field name>}` 操作」頁籤的欄位中指定。

例如，如果表單包含「電子郵件 **位址** 」欄位(名為 `email_addr`)，以擷取使用者的電子郵件ID，您可以在「郵件收件人」、「抄送」或「密件副本」欄位中指定下列項目。

`${email_addr}`

當使用者提交表格時，會傳送電子郵件至在表格欄位中輸入 `email_addr` 的電子郵件ID。

>[!NOTE]
>
>您可以在欄位的「編輯」對話方 **塊中** ，找到欄位名稱。

變數預留位置也可用於「主旨」 **和「電子郵件** 」 **範本欄位** 。

例如：

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>可重複面板中的欄位不能用作變數預留位置。

