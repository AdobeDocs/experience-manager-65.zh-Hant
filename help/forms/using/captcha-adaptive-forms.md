---
title: 在最適化表單中使用CAPTCHA
seo-title: Using CAPTCHA in adaptive forms
description: 了解如何在最適化表單中設定AEM CAPTCHA或Google reCAPTCHA服務。
seo-description: Learn how to configure AEM CAPTCHA or Google reCAPTCHA service in adaptive forms.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
feature: Adaptive Forms
exl-id: 9b4219b8-d5eb-4099-b205-d98d84e0c249
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1271'
ht-degree: 0%

---

# 在最適化表單中使用CAPTCHA{#using-captcha-in-adaptive-forms}

驗證碼（Captcha，完全自動化的公共圖靈測試，可區分電腦和人）是線上交易中常用的一種程式，用於區分人和自動程式或機器人。 這會帶來挑戰並評估使用者回應，以判斷其為與網站互動的人或機器人。 它可防止機器人張貼垃圾訊息或惡意用途，讓使用者在測試失敗時繼續執行，有助於確保線上交易的安全。

AEM Forms支援適用性表單中的驗證碼。 您可以使用Google的reCAPTCHA服務來實作CAPTCHA。

>[!NOTE]
>
>* AEM Forms僅支援reCaptcha v2。 不支援任何其他版本。
>* AEM Forms應用程式的離線模式不支援適用性表單中的驗證碼。
>


## 配置ReCAPTCHA服務(由Google提供) {#google-recaptcha}

表單作者可使用Google提供的reCAPTCHA服務，在最適化表單中實作CAPTCHA。 它提供進階驗證碼功能，可保護您的網站。 如需reCAPTCHA如何運作的詳細資訊，請參閱 [Google reCAPTCHA](https://developers.google.com/recaptcha/).

![Recaptcha](assets/recaptcha_new.png)

若要在AEM Forms中實作reCAPTCHA服務：

1. 取得 [reCAPTCHA API金鑰組](https://www.google.com/recaptcha/admin) 從Google。 其中包含網站金鑰和機密。
1. 為雲端服務建立設定容器。

   1. 前往 **[!UICONTROL 工具>一般>設定瀏覽器]**.
      * 請參閱 [配置瀏覽器](/help/sites-administering/configurations.md) 檔案以取得詳細資訊。
   1. 請執行下列操作以啟用雲配置的全局資料夾，或跳過此步驟以建立和配置雲服務配置的其他資料夾。

      1. 在設定瀏覽器中，選取 **[!UICONTROL 全球]** 資料夾和點選 **[!UICONTROL 屬性]**.

      1. 在「配置屬性」對話框中，啟用 **[!UICONTROL 雲端設定]**.
      1. 點選 **[!UICONTROL 儲存並關閉]** 以保存配置並退出對話框。
   1. 在「設定瀏覽器」中，點選 **[!UICONTROL 建立]**.
   1. 在「建立配置」對話框中，指定資料夾的標題並啟用 **[!UICONTROL 雲端設定]**.
   1. 點選 **[!UICONTROL 建立]** 建立雲端服務設定啟用的資料夾。


1. 為reCAPTCHA設定雲端服務。

   1. 在AEM Author例項上，前往 ![tools-1](assets/tools-1.png) > **Cloud Services**.
   1. 點選 **[!UICONTROL reCAPTCHA]**. 「設定」頁面隨即開啟。 選取在上一步驟中建立的設定容器，然後點選 **[!UICONTROL 建立]**.
   1. 為reCAPTCHA服務指定名稱、網站金鑰和密鑰，然後點選 **[!UICONTROL 建立]** 來建立雲端服務設定。
   1. 在「編輯元件」對話方塊中，指定在步驟1取得的網站和機密金鑰。 點選 **儲存設定** 然後點選 **確定** 以完成設定。

   設定reCAPTCHA服務後，即可在最適化表單中使用。 如需詳細資訊，請參閱 [在最適化表單中使用CAPTCHA](#using-captcha).

## 在最適化表單中使用CAPTCHA {#using-captcha}

若要在最適化表單中使用CAPTCHA:

1. 在編輯模式中開啟最適化表單。

   >[!NOTE]
   >
   >建立最適化表單時，請確定選取的設定容器包含reCAPTCHA雲端服務。 您也可以編輯最適化表單屬性，以變更與表單相關聯的設定容器。

1. 從元件瀏覽器中，拖放 **驗證碼** 元件至最適化表單。

   >[!NOTE]
   >
   >不支援在最適化表單中使用多個驗證碼元件。 此外，不建議在標示為延遲載入的面板或片段中使用CAPTCHA。

   >[!NOTE]
   >
   >驗證碼具有時效性，約一分鐘後過期。 因此，建議將驗證碼元件放置在最適化表單中的提交按鈕之前。

1. 選取您新增的驗證碼元件，然後點選 ![cppr](assets/cmppr.png) 來編輯其屬性。
1. 指定驗證碼介面工具集的標題。 預設值為 **驗證碼**. 選擇 **隱藏標題** 如果您不想顯示標題。
1. 從 **驗證碼服務** 下拉式清單，選取 **reCaptcha** 啟用reCAPTCHA服務(如果您已按照 [ReCAPTCHA服務，由Google提供](#google-recaptcha). 從「設定」下拉式清單中選取設定。 同時，選取大小為 **正常** 或 **緊湊** 用於reCAPTCHA介面工具集。

   >[!NOTE]
   >
   >不選擇 **[!UICONTROL 預設]** 從驗證碼服務下拉式清單中取消使用，因為預設的AEM CAPTCHA服務已遭取代。

1. 儲存屬性。

reCAPTCHA服務已在最適化表單上啟用。 您可以預覽表單，並查看驗證碼正常運作。

### 根據規則顯示或隱藏CAPTCHA元件 {#show-hide-captcha}

您可以選取根據套用至適用性表單中元件的規則，來顯示或隱藏CAPTCHA元件。 點選元件，選取 ![編輯規則](assets/edit-rules-icon.svg)，然後點選 **[!UICONTROL 建立]** 來建立規則。 如需建立規則的詳細資訊，請參閱 [規則編輯器](rule-editor.md).

例如，只有當表單中的「貨幣值」欄位值超過25000時，CAPTCHA元件才必須顯示在適用性表單中。

點選 **[!UICONTROL 貨幣值]** 欄位，並建立下列規則：

![顯示或隱藏規則](assets/rules-show-hide-captcha.png)

### 進行驗證碼驗證 {#validate-captcha}

提交表單時，或根據使用者動作和條件進行驗證驗證時，您都可以在適用性表單中驗證驗證驗證碼。

#### 在提交表單時驗證驗證碼 {#validation-form-submission}

在提交最適化表單時自動驗證驗證碼：

1. 點選驗證碼元件並選取 ![cppr](assets/configure-icon.svg) 查看元件屬性。
1. 在 **[!UICONTROL 驗證驗證碼]** 部分，選擇 **[!UICONTROL 在提交表單時驗證驗證碼]**.
1. 點選 ![完成](assets/save_icon.svg) 以保存元件屬性。

#### 驗證使用者動作和條件的驗證碼 {#validate-captcha-user-action}

若要根據條件和使用者動作驗證驗證驗證碼：

1. 點選驗證碼元件並選取 ![cppr](assets/configure-icon.svg) 查看元件屬性。
1. 在 **[!UICONTROL 驗證驗證碼]** 部分，選擇 **[!UICONTROL 驗證使用者動作的驗證碼]**.
1. 點選 ![完成](assets/save_icon.svg) 以保存元件屬性。

[!DNL Experience Manager Forms] proves `ValidateCAPTCHA` 使用預先定義的條件驗證驗證驗證碼的API。 您可以使用自訂提交動作或在適用性表單中定義元件規則，來叫用API。

以下是 `ValidateCAPTCHA` 使用預先定義的條件驗證驗證驗證碼的API:

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

此範例表示 `ValidateCAPTCHA` API僅會在使用者填寫表單時指定的數值方塊位數大於5時，才驗證表單中的驗證碼。

**選項1:使用 [!DNL Experience Manager Forms] 使用自訂提交動作驗證CAPTCHA API以驗證CAPTCHA**

執行下列步驟以使用 `ValidateCAPTCHA` 使用自訂提交動作驗證驗證驗證碼的API:

1. 新增包含 `ValidateCAPTCHA` 自訂提交動作的API。 如需自訂提交動作的詳細資訊，請參閱 [建立適用性Forms的自訂提交動作](custom-submit-action-form.md).
1. 從 **[!UICONTROL 提交動作]** 中的下拉式清單 **[!UICONTROL 提交]** 適用性表單的屬性。
1. 點選 **[!UICONTROL 提交]**. 驗證碼會根據 `ValidateCAPTCHA` 自訂提交動作的API。

**選項2:使用 [!DNL Experience Manager Forms] 提交表單前，驗證CAPTCHA API可先驗證使用者動作的CAPTCHA**

您也可以叫用 `ValidateCAPTCHA` 在適用性表單中對元件套用規則以取得API。

例如，您新增 **[!UICONTROL 驗證驗證碼]** 按鈕，並建立規則以在按一下按鈕時叫用服務。

下圖說明如何在點按 **[!UICONTROL 驗證驗證碼]** 按鈕：

![進行驗證碼驗證](assets/captcha-validation1.gif)

您可以叫用包含 `ValidateCAPTCHA` API使用規則編輯器，並根據驗證結果啟用或停用適用性表單的提交按鈕。

同樣地，您也可以使用規則編輯器加入自訂方法，以在適用性表單中驗證驗證碼字。

### 新增自訂驗證碼服務 {#add-custom-captcha-service}

[!DNL Experience Manager Forms] 提供reCAPTCHA作為CAPTCHA服務。 不過，您可以新增自訂服務以顯示在 **[!UICONTROL 驗證碼服務]** 下拉式清單。

以下是介面實作的範例，以新增其他CAPTCHA服務至您的適用性表單：

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

`captchaPropertyNodePath` 是指Sling存放庫中CAPTCHA元件的資源路徑。 使用此屬性來包含驗證碼元件的特定詳細資訊。 例如， `captchaPropertyNodePath` 包括在CAPTCHA元件上設定的reCAPTCHA雲端設定資訊。 雲配置資訊提供 **[!UICONTROL 網站金鑰]** 和 **[!UICONTROL 密鑰]** 實作reCAPTCHA服務的設定。

`userResponseToken` 是指 `g_recaptcha_response` 在解決表單中的驗證碼後產生。
