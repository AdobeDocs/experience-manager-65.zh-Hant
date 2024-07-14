---
title: 透過電子郵件傳送表單提交通知
description: AEM Forms可讓您設定電子郵件提交動作，在提交表單時傳送通知給使用者。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: bca4044a-18a9-4b97-92de-eff1e9a840f9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---

# 透過電子郵件傳送表單提交通知 {#sending-a-form-submission-acknowledgement-via-email}

## 最適化表單資料提交 {#adaptive-form-data-submission}

最適化表單提供幾個現成的[提交動作](../../forms/using/configuring-submit-actions.md)工作流程，用於將表單資料提交至不同的端點。

例如，**[!UICONTROL 傳送電子郵件]**&#x200B;提交動作會在成功提交最適化表單時傳送電子郵件。 您也可以將其設定為在電子郵件中傳送表單資料和PDF。

本文詳細說明在最適化表單及其提供的不同設定上啟用電子郵件動作的步驟。

>[!NOTE]
>
>您也可以使用&#x200B;**[!UICONTROL 透過電子郵件傳送PDF]**&#x200B;選項，以電子郵件傳送完成的表單作為PDF附件。 此動作可用的組態選項與&#x200B;**[!UICONTROL 傳送電子郵件]**&#x200B;動作可用的選項相同。 電子郵件PDF動作僅適用於XFA型最適化表單

## 傳送電子郵件動作 {#email-action}

「傳送電子郵件」動作可讓作者在成功提交最適化表單時，自動傳送電子郵件給一或多個收件者。

>[!NOTE]
>
>若要使用[傳送電子郵件]動作，您必須依照[設定郵件服務](/help/sites-administering/notification.md#configuring-the-mail-service)中的說明設定AEM郵件服務。

### 在最適化表單上啟用「傳送電子郵件」動作 {#enabling-email-action-on-an-adaptive-form}

1. 以&#x200B;**[!UICONTROL 編輯]**&#x200B;模式開啟最適化表單。

1. 在&#x200B;**[!UICONTROL 內容]**&#x200B;索引標籤中，選取&#x200B;**[!UICONTROL 表單容器]**，然後選取![設定](assets/configure-icon.svg)以檢視最適化表單屬性。

1. 在&#x200B;**[!UICONTROL 提交]**&#x200B;區段中，從&#x200B;**[!UICONTROL 提交動作]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL 傳送電子郵件]**。

   ![提交動作](assets/submission-actions.png)

1. 在&#x200B;**[!UICONTROL 到]**、**[!UICONTROL 副本]**&#x200B;和&#x200B;**[!UICONTROL 密件副本]**&#x200B;欄位中指定有效的電子郵件識別碼。

   在&#x200B;**[!UICONTROL 主旨]**&#x200B;與&#x200B;**[!UICONTROL 電子郵件範本]**&#x200B;欄位中分別指定電子郵件的主旨與內文。

   您也可以在欄位中指定變數預留位置，在這種情況下，當一般使用者成功提交表單時會處理欄位的值。 如需詳細資訊，請參閱[使用最適化表單欄位名稱來動態建立電子郵件內容](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p)。

   如果表單包含檔案附件，而且您想要在電子郵件中附加這些檔案，請選取&#x200B;**[!UICONTROL 包含附件]**。

   >[!NOTE]
   >
   >如果您選擇&#x200B;**[!UICONTROL 透過電子郵件傳送PDF]**&#x200B;選項，則必須選取「包含附件」選項。

1. 按一下![儲存](assets/save_icon.svg)以儲存變更。

### 使用最適化表單欄位名稱來動態建立電子郵件內容 {#using-adaptive-form-field-names-to-dynamically-create-email-content}

調適型表單中的欄位名稱稱為預留位置，在使用者提交表單後會以該欄位的值取代。

在&#x200B;**[!UICONTROL 傳送電子郵件]**&#x200B;動作中，您可以使用執行動作時所處理的預留位置。 這表示使用者提交表單時會產生電子郵件的標頭（例如&#x200B;**[!UICONTROL To]**、**[!UICONTROL CC]**、**[!UICONTROL BCC]**、**[!UICONTROL Subject]**）。

若要定義預留位置，請在選取&#x200B;**[!UICONTROL 傳送電子郵件]**&#x200B;做為提交動作之後，在欄位中指定`${<field name>}`。

例如，如果表單包含名為`email_addr`的&#x200B;**[!UICONTROL 電子郵件地址]**&#x200B;欄位，用於擷取使用者的電子郵件識別碼，您可以在&#x200B;**[!UICONTROL 收件者]**、**[!UICONTROL 副本]**&#x200B;或&#x200B;**[!UICONTROL 密件副本]**&#x200B;欄位中指定下列專案。

`${email_addr}`

當使用者提交表單時，會傳送電子郵件給在表單的`email_addr`欄位中輸入的電子郵件識別碼。

>[!NOTE]
>
>您可以在欄位的&#x200B;**[!UICONTROL 編輯]**&#x200B;對話方塊中找到欄位名稱。

變數預留位置也可以在&#x200B;**[!UICONTROL 主旨]**&#x200B;和&#x200B;**[!UICONTROL 電子郵件範本]**&#x200B;欄位中使用。

例如：

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>可重複面板中的欄位無法當作變數預留位置使用。
