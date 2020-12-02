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
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---


# 透過電子郵件{#sending-a-form-submission-acknowledgement-via-email}傳送表單提交確認

## 最適化表單資料提交{#adaptive-form-data-submission}

最適化表單提供數種現成可用的[提交動作](../../forms/using/configuring-submit-actions.md)工作流程，以將表單資料提交至不同的端點。

例如，**[!UICONTROL 傳送電子郵件]**&#x200B;提交動作會在成功提交最適化表單時傳送電子郵件。 您也可以設定它來傳送表單資料和電子郵件中的PDF。

本文詳細說明如何在最適化表單及其提供的不同組態上啟用「電子郵件」動作。

>[!NOTE]
>
>您也可以使用&#x200B;**[!UICONTROL 透過電子郵件傳送PDF]**&#x200B;選項，以電子郵件方式將填妥的表單傳送為PDF附件。 此動作的可用配置選項與&#x200B;**[!UICONTROL 發送電子郵件]**&#x200B;動作的可用選項相同。 「電子郵件PDF」動作僅適用於XFA型調適性表單

## 傳送電子郵件動作{#email-action}

「傳送電子郵件」動作可讓作者在成功提交調適性表單時，自動傳送電子郵件給一或多個收件者。

>[!NOTE]
>
>若要使用「傳送電子郵件」動作，您必須依照[設定郵件服務](/help/sites-administering/notification.md#configuring-the-mail-service)中所述，設定AEM郵件服務。

### 在最適化表單{#enabling-email-action-on-an-adaptive-form}上啟用「傳送電子郵件」動作

1. 在&#x200B;**[!UICONTROL edit]**&#x200B;模式中開啟自適應表單。

1. 在&#x200B;**[!UICONTROL Content]**&#x200B;標籤中，點選&#x200B;**[!UICONTROL Form Container]**&#x200B;並點選![configure](assets/configure-icon.svg)以檢視最適化表單屬性。

1. 在&#x200B;**[!UICONTROL Submission]**&#x200B;區段中，從&#x200B;**[!UICONTROL Submit Action]**&#x200B;下拉式清單中選擇&#x200B;**[!UICONTROL Send email]**。

   ![提交動作](assets/submission-actions.png)

1. 在&#x200B;**[!UICONTROL To]**、**[!UICONTROL CC]**&#x200B;和&#x200B;**[!UICONTROL BCC]**&#x200B;欄位中指定有效的電子郵件ID。

   在&#x200B;**[!UICONTROL Subject]**&#x200B;和&#x200B;**[!UICONTROL 電子郵件範本]**&#x200B;欄位中分別指定電子郵件的主旨和內文。

   您也可以在欄位中指定變數預留位置，此時，當使用者成功提交表單時，會處理欄位的值。 如需詳細資訊，請參閱[使用最適化表單欄位名稱動態建立電子郵件內容](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p)。

   如果表單包含檔案附件，並且您希望在電子郵件中附加這些檔案，請選擇&#x200B;**[!UICONTROL 「包括附件」]**。

   >[!NOTE]
   >
   >如果您選擇「透過電子郵件傳送PDF」選項，則必須選擇「包含附件」選項。****

1. 按一下![save](assets/save_icon.svg)保存更改。

### 使用可調式表單欄位名稱動態建立電子郵件內容{#using-adaptive-form-field-names-to-dynamically-create-email-content}

最適化表單中的欄位名稱稱為預留位置，在使用者提交表單後，會以該欄位的值取代。

在&#x200B;**[!UICONTROL 傳送電子郵件]**&#x200B;動作中，您可以使用在執行動作時處理的預留位置。 這意味著當用戶提交表單時，生成電子郵件的標題（例如&#x200B;**[!UICONTROL To]**、**[!UICONTROL CC]**、**[!UICONTROL BCC]**、**[!UICONTROL Subject]**）。

若要定義預留位置，請在選擇&#x200B;**[!UICONTROL 傳送電子郵件]**&#x200B;作為「提交動作」後，在欄位中指定`${<field name>}`。

例如，如果表單包含&#x200B;**[!UICONTROL 電子郵件地址]**&#x200B;欄位（名為`email_addr`），以擷取使用者的電子郵件ID，您可在&#x200B;**[!UICONTROL To]**、**[!UICONTROL CC]**&#x200B;或&#x200B;**[!UICONTROL BCC]**&#x200B;欄位中指定下列項目。

`${email_addr}`

當使用者提交表格時，會傳送電子郵件至在表格的`email_addr`欄位中輸入的電子郵件ID。

>[!NOTE]
>
>您可以在&#x200B;**[!UICONTROL 編輯]**&#x200B;對話框中找到欄位的名稱。

變數預留位置也可用於&#x200B;**[!UICONTROL Subject]**&#x200B;和&#x200B;**[!UICONTROL 電子郵件範本]**&#x200B;欄位。

例如：

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>可重複面板中的欄位不能用作變數預留位置。

