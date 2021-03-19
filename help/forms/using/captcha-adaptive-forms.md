---
title: 在最適化表單中使用CAPTCHA
seo-title: 在最適化表單中使用CAPTCHA
description: 瞭解如何以最適AEM化表單來設定CAPTCHA或Google reCAPTCHA服務。
seo-description: 瞭解如何以最適AEM化表單來設定CAPTCHA或Google reCAPTCHA服務。
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
feature: 適用性表單
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---


# 在最適化表單中使用CAPTCHA{#using-captcha-in-adaptive-forms}

CAPTCHA（完全自動化的公共圖靈測試，可區分電腦和人類）是線上交易常用的程式，用來區分人類和自動化程式或機器人。 它會帶來挑戰，並評估使用者回應，以判斷它是人還是機器人與網站互動。 它可防止使用者在測試失敗時繼續作業，並防止機器人張貼垃圾訊息或惡意目的，以確保線上交易的安全。

AEM Forms支援CAPTCHA的調適性表單。 您可以使用Google的reCAPTCHA服務來實作CAPTCHA。

>[!NOTE]
>
>* AEM Forms僅支援reCaptcha v2。 不支援任何其他版本。
>* AEM Forms應用程式的離線模式不支援最適化表單的CAPTCHA。

>



## Google {#google-recaptcha}設定ReCAPTCHA服務

表單作者可以使用Google的reCAPTCHA服務，在最適化表單中實作CAPTCHA。 它提供進階的CAPTCHA功能，以保護您的網站。 如需reCAPTCHA如何運作的詳細資訊，請參閱[Google reCAPTCHA](https://developers.google.com/recaptcha/)。

![Recaptcha](assets/recaptcha_new.png)

若要在AEM Forms實作reCAPTCHA服務：

1. 從Google取得[reCAPTCHA API金鑰對](https://www.google.com/recaptcha/admin)。 它包含網站金鑰和機密。
1. 建立雲端服務的設定容器。

   1. 前往&#x200B;**[!UICONTROL 工具>一般>組態瀏覽器]**。
      * 如需詳細資訊，請參閱[Configuration Browser](/help/sites-administering/configurations.md)檔案。
   1. 請執行下列動作，為雲端設定啟用全域資料夾，或略過此步驟，為雲端服務設定建立並設定另一個資料夾。

      1. 在「配置瀏覽器」中，選擇&#x200B;**[!UICONTROL global]**&#x200B;資料夾，然後點選&#x200B;**[!UICONTROL 屬性]**。

      1. 在「配置屬性」對話框中，啟用&#x200B;**[!UICONTROL 雲配置]**。
      1. 點選&#x200B;**[!UICONTROL 儲存並關閉]**&#x200B;以儲存設定並退出對話方塊。
   1. 在配置瀏覽器中，按一下&#x200B;**[!UICONTROL 建立]**。
   1. 在「建立配置」對話框中，指定資料夾的標題並啟用&#x200B;**[!UICONTROL 雲配置]**。
   1. 點選「**[!UICONTROL 建立]**」以建立可用於雲端服務組態的資料夾。


1. 為reCAPTCHA設定雲端服務。

   1. 在您AEM的作者例項中，前往![tools-1](assets/tools-1.png) > **Cloud Services**。
   1. 點選&#x200B;**[!UICONTROL reCAPTCHA]**。 將開啟「配置」頁。 選擇在上一步驟中建立的配置容器，然後按一下&#x200B;**[!UICONTROL 建立]**。
   1. 指定reCAPTCHA服務的名稱、網站金鑰和機密金鑰，並點選&#x200B;**[!UICONTROL Create]**&#x200B;以建立雲端服務設定。
   1. 在「編輯元件」對話方塊中，指定在步驟1中取得的網站和機密金鑰。 點選「**儲存設定**」，然後點選「**確定**」以完成設定。

   在設定reCAPTCHA服務後，就可在最適化表單中使用。 如需詳細資訊，請參閱[在最適化表單中使用CAPTCHA](#using-captcha)。

## 在最適化表單{#using-captcha}中使用CAPTCHA

若要在最適化表單中使用CAPTCHA:

1. 在編輯模式中開啟最適化表單。

   >[!NOTE]
   >
   >請確定建立最適化表單時選取的組態容器包含reCAPTCHA雲端服務。 您也可以編輯最適化表單屬性，以變更與表單關聯的組態容器。

1. 從元件瀏覽器，將&#x200B;**Captcha**&#x200B;元件拖放至最適化表單。

   >[!NOTE]
   >
   >不支援在最適化表單中使用多個Captcha元件。 此外，建議不要在標示為延遲載入的面板或片段中使用CAPTCHA。

   >[!NOTE]
   >
   >驗證碼是時間敏感的，約一分鐘後過期。 因此，建議將Captcha元件置於最適化表單中「提交」按鈕之前。

1. 選取您新增的Captcha元件，並點選![cmppr](assets/cmppr.png)以編輯其屬性。
1. 指定CAPTCHA介面工具集的標題。 預設值為&#x200B;**Captcha**。 如果您不想顯示標題，請選擇&#x200B;**隱藏標題**。
1. 從&#x200B;**Captcha服務**&#x200B;下拉式清單中，選擇&#x200B;**reCaptcha**&#x200B;以啟用reCAPTCHA服務（若您依[Google](#google-recaptcha)的ReCAPTCHA服務中所述設定）。 從「設定」下拉式清單中選取設定。 此外，請為reCAPTCHA Widget選擇大小為&#x200B;**Normal**&#x200B;或&#x200B;**Compact**。

   >[!NOTE]
   >
   >請勿從Captcha服務下拉式清單中選取&#x200B;**[!UICONTROL Default]**，因為預設的AEMCAPTCHA服務已過時。

1. 儲存屬性。

reCAPTCHA服務在最適化表單上啟用。 您可以預覽表單，並檢視CAPTCHA運作。
