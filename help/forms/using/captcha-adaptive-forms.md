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
source-git-commit: 7a3f54d90769708344e6751756b2a12ac6c962d7
workflow-type: tm+mt
source-wordcount: '1291'
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

### 根據規則{#show-hide-captcha}顯示或隱藏CAPTCHA元件

您可以選擇根據在自適應表單中對元件應用的規則來顯示或隱藏CAPTCHA元件。 點選元件，選取![edit rules](assets/edit-rules-icon.svg)，然後點選&#x200B;**[!UICONTROL Create]**&#x200B;以建立規則。 有關建立規則的詳細資訊，請參閱[規則編輯器](rule-editor.md)。

例如，只有當表單中的「貨幣值」欄位的值超過25000時，CAPTCHA元件才必須顯示在最適化表單中。

點選表單中的&#x200B;**[!UICONTROL 貨幣值]**&#x200B;欄位並建立下列規則：

![顯示或隱藏規則](assets/rules-show-hide-captcha.png)

### 進行驗證碼驗證 {#validate-captcha}

當您提交表單或根據使用者動作與條件來驗證CAPTCHA時，您都可以在最適化表單中驗證CAPTCHA。

#### 在表單提交{#validation-form-submission}時驗證CAPTCHA

要在提交最適化表單時自動驗證CAPTCHA，請執行以下操作：

1. 點選CAPTCHA元件並選取![cmppr](assets/configure-icon.svg)以檢視元件屬性。
1. 在&#x200B;**[!UICONTROL 驗證CAPTCHA]**&#x200B;區段中，選擇&#x200B;**[!UICONTROL 在表單提交時驗證CAPTCHA]**。
1. 點選![Done](assets/save_icon.svg)以儲存元件屬性。

#### 驗證使用者動作與條件{#validate-captcha-user-action}的CAPTCHA

要根據條件和用戶操作驗證CAPTCHA，請執行以下操作：

1. 點選CAPTCHA元件並選取![cmppr](assets/configure-icon.svg)以檢視元件屬性。
1. 在&#x200B;**[!UICONTROL 驗證CAPTCHA]**&#x200B;區段中，選擇&#x200B;**[!UICONTROL 驗證使用者動作]**&#x200B;的CAPTCHA。
1. 點選![Done](assets/save_icon.svg)以儲存元件屬性。

[!DNL Experience Manager Forms] 提供 `ValidateCAPTCHA` API以使用預先定義的條件來驗證CAPTCHA。您可以使用自訂的「提交動作」或在最適化表單中定義元件規則來叫用API。

以下是`ValidateCAPTCHA` API的範例，以使用預先定義的條件來驗證CAPTCHA:

```javascript
if (slingRequest.getParameter("numericbox1614079614831").length() >= 5) {
    	GuideCaptchaValidatorProvider apiProvider = sling.getService(GuideCaptchaValidatorProvider.class);
        String formPath = slingRequest.getResource().getPath();
        String captchaData = slingRequest.getParameter(GuideConstants.GUIDE_CAPTCHA_DATA);
        if (!apiProvider.validateCAPTCHA(formPath, captchaData).isCaptchaValid()){
            response.setStatus(400);
            return;
        }
    }
```

範例表示，`ValidateCAPTCHA` API僅在使用者填寫表單時指定數值方塊中的位數大於5時，才會驗證表單中的CAPTCHA。

**選項1:使用 [!DNL Experience Manager Forms] ValidateCAPTCHA API來驗證使用自訂提交動作的CAPTCHA**

請執行下列步驟，以使用`ValidateCAPTCHA` API來驗證使用自訂提交動作的CAPTCHA:

1. 將包含`ValidateCAPTCHA` API的指令碼新增至自訂「提交動作」。 有關自定義提交操作的詳細資訊，請參閱[為最適化Forms建立自定義提交操作](custom-submit-action-form.md)。
1. 從最適化表單的&#x200B;**[!UICONTROL Submission]**&#x200B;屬性的&#x200B;**[!UICONTROL Submit Action]**&#x200B;下拉式清單中，選取自訂提交動作的名稱。
1. 點選&#x200B;**[!UICONTROL Submit]**。 CAPTCHA會根據自訂「提交動作」的`ValidateCAPTCHA` API中定義的條件進行驗證。

**選項2:在提 [!DNL Experience Manager Forms] 交表單之前，請使用ValidateCAPTCHA API來驗證使用者動作的CAPTCHA**

您也可以在最適化表單的元件上套用規則，以叫用`ValidateCAPTCHA` API。

例如，您在「最適化表單」中新增&#x200B;**[!UICONTROL 驗證CAPTCHA]**&#x200B;按鈕，並建立規則以在按一下按鈕時叫用服務。

下圖說明如何在按一下&#x200B;**[!UICONTROL 驗證CAPTCHA]**&#x200B;按鈕時叫用服務：

![進行驗證碼驗證](assets/captcha-validation1.gif)

您可以使用規則編輯器調用包含`ValidateCAPTCHA` API的自定義servlet，並根據驗證結果啟用或禁用最適化表單的提交按鈕。

同樣地，您也可以使用規則編輯器來包含自訂方法，以驗證最適化表單中的CAPTCHA。

### 新增自訂CAPTCHA服務{#add-custom-captcha-service}

[!DNL Experience Manager Forms] 提供reCAPTCHA做為CAPTCHA服務。不過，您可以新增自訂服務以顯示在&#x200B;**[!UICONTROL CAPTCHA服務]**&#x200B;下拉式清單中。

以下是介面的範例實作，可將額外的CAPTCHA服務新增至最適化表單：

```javascript
package com.adobe.aemds.guide.service;

import org.osgi.annotation.versioning.ConsumerType;

/**
 * An interface to provide captcha validation at server side in Adaptive Form
 * This interface can be used to provide custom implementation for different captcha services.
 */
@ConsumerType
public interface GuideCaptchaValidator {
    /**
     * This method should define the actual validation logic of the captcha
     * @param captchaPropertyNodePath path to the node with CAPTCHA configurations inside form container
     * @param userResponseToken  The user response token provided by the CAPTCHA from client-side
     *
     * @return  {@link GuideCaptchaValidationResult} validation result of the captcha
     */
     GuideCaptchaValidationResult validateCaptcha(String captchaPropertyNodePath, String userResponseToken);

    /**
     * Returns the name of the captcha validator. This should be unique among the different implementations
     * @return  name of the captcha validator
     */
     String getCaptchaValidatorName();
}
```

`captchaPropertyNodePath` 參照Sling存放庫中CAPTCHA元件的資源路徑。使用此屬性可包含CAPTCHA元件的特定詳細資訊。 例如，`captchaPropertyNodePath`包含在CAPTCHA元件上設定的reCAPTCHA雲端設定資訊。 雲端設定資訊提供&#x200B;**[!UICONTROL 網站金鑰]**&#x200B;和&#x200B;**[!UICONTROL 機密金鑰]**&#x200B;設定，以實作reCAPTCHA服務。

`userResponseToken` 是指在表 `g_recaptcha_response` 單中解決CAPTCHA後產生的。
