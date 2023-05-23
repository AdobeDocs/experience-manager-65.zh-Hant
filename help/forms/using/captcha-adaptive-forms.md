---
title: 在自適應形式中使用驗證碼
seo-title: Using CAPTCHA in adaptive forms
description: 瞭解如何以自適AEM應形式配置CAPTCHA或GooglereCAPTCHA服務。
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

# 在自適應形式中使用驗證碼{#using-captcha-in-adaptive-forms}

CAPTCHA(完全自動化公共圖靈test，將電腦和人區分開)是線上交易中常用的程式，用於區分人類和自動程式或機器人。 它提出了一個挑戰，並評估用戶響應，以確定它是人還是機器人與站點交互。 它防止用戶在test失敗時繼續操作，並通過防止bot發佈垃圾郵件或惡意目的，幫助確保線上交易的安全。

AEM Forms支援自適應驗證碼。 您可以使用Google的reCAPTCHA服務來實施CAPTCHA。

>[!NOTE]
>
>* AEM Forms僅支援reCaptcha v2。 不支援任何其他版本。
>* 在AEM Forms應用的離線模式下，不支援自適應表單中的驗證碼。
>


## 配置由Google提供的ReCAPTCHA服務 {#google-recaptcha}

表單作者可以使用Google提供的reCAPTCHA服務以自適應形式實現CAPTCHA。 它提供高級驗證碼功能以保護您的站點。 有關reCAPTCHA工作原理的詳細資訊，請參見 [GoogleRE CAPTCHA](https://developers.google.com/recaptcha/)。

![重新捕獲](assets/recaptcha_new.png)

在AEM Forms實施reCAPTCHA服務：

1. 獲取 [reCAPTCHA API密鑰對](https://www.google.com/recaptcha/admin) Google。 它包括一個站點密鑰和一個秘密。
1. 為雲服務建立配置容器。

   1. 轉到 **[!UICONTROL 工具>常規>配置瀏覽器]**。
      * 查看 [配置瀏覽器](/help/sites-administering/configurations.md) 的子菜單。
   1. 執行以下操作以啟用雲配置的全局資料夾，或跳過此步驟為雲服務配置建立和配置另一個資料夾。

      1. 在配置瀏覽器中，選擇 **[!UICONTROL 全球]** 資料夾和點擊 **[!UICONTROL 屬性]**。

      1. 在「配置屬性」對話框中，啟用 **[!UICONTROL 雲配置]**。
      1. 點擊 **[!UICONTROL 保存並關閉]** 以保存配置並退出對話框。
   1. 在配置瀏覽器中，按一下 **[!UICONTROL 建立]**。
   1. 在「建立配置」對話框中，指定資料夾的標題並啟用 **[!UICONTROL 雲配置]**。
   1. 點擊 **[!UICONTROL 建立]** 建立為雲服務配置啟用的資料夾。


1. 為reCAPTCHA配置雲服務。

   1. 在您的AEM作者實例上，轉到 ![工具–1](assets/tools-1.png) > **Cloud Services**。
   1. 點擊 **[!UICONTROL reCAPTCHA]**。 將開啟「配置」頁。 選擇在上一步中建立的配置容器，然後點擊 **[!UICONTROL 建立]**。
   1. 為reCAPTCHA服務指定名稱、站點密鑰和密鑰並點擊 **[!UICONTROL 建立]** 建立雲服務配置。
   1. 在「編輯元件」對話框中，指定在步驟1中獲取的站點和密鑰。 點擊 **保存設定** 然後點擊 **確定** 完成配置。

   配置reCAPTCHA服務後，它可以在自適應表單中使用。 有關詳細資訊，請參見 [在自適應形式中使用驗證碼](#using-captcha)。

## 在自適應形式中使用CAPTCHA {#using-captcha}

要在自適應格式中使用驗證碼驗證碼：

1. 在編輯模式下開啟自適應窗體。

   >[!NOTE]
   >
   >確保在建立自適應表單時選擇的配置容器包含reCAPTCHA雲服務。 還可以編輯自適應表單屬性以更改與表單關聯的配置容器。

1. 在元件瀏覽器中，拖放 **驗證碼** 到自適應窗體。

   >[!NOTE]
   >
   >不支援在自適應表單中使用多個驗證碼元件。 此外，建議不要在標籤為延遲載入的面板或片段中使用驗證碼。

   >[!NOTE]
   >
   >驗證碼是時間敏感型的，大約一分鐘後過期。 因此，建議將驗證碼元件放在自適應表單中「提交」按鈕之前。

1. 選擇您添加的驗證碼元件並點擊 ![招商](assets/cmppr.png) 編輯其屬性。
1. 指定驗證碼構件的標題。 預設值為 **驗證碼**。 選擇 **隱藏標題** 的子菜單。
1. 從 **驗證碼服務** 下拉，選擇 **雷卡普查** 啟用reCAPTCHA服務（如所述） [ReCAPTCHA服務，Google](#google-recaptcha)。 從「設定」(Settings)下拉菜單中選擇配置。 另外，選擇大小為 **正常** 或 **緊湊** 用於reCAPTCHA小部件。

   >[!NOTE]
   >
   >不選擇 **[!UICONTROL 預設]** 不建議使用預設CAPTCHA服務時，從「驗證AEM碼服務」下拉清單中。

1. 保存屬性。

reCAPTCHA服務在自適應窗體上啟用。 您可以預覽表單並查看驗證碼正在工作。

### 根據規則顯示或隱藏驗證碼元件 {#show-hide-captcha}

您可以根據在自適應表單中的元件上應用的規則選擇顯示或隱藏CAPTCHA元件。 按一下元件，選擇 ![編輯規則](assets/edit-rules-icon.svg)，然後點擊 **[!UICONTROL 建立]** 的子菜單。 有關建立規則的詳細資訊，請參閱 [規則編輯器](rule-editor.md)。

例如，僅當表單中的「貨幣值」欄位的值大於25000時，CAPTCHA元件才必須顯示在自適應表單中。

點擊 **[!UICONTROL 貨幣值]** 的子例行程式，並建立以下規則：

![顯示或隱藏規則](assets/rules-show-hide-captcha.png)

### 進行驗證碼驗證 {#validate-captcha}

在提交表單或根據用戶操作和條件對驗證碼驗證進行基礎時，您都可以在自適應表單中驗證驗證碼。

#### 在提交表單時驗證驗證碼 {#validation-form-submission}

要在提交自適應表單時自動驗證驗證驗證碼，請執行以下操作：

1. 點擊驗證碼元件並選擇 ![招商](assets/configure-icon.svg) 的子菜單。
1. 在 **[!UICONTROL 驗證驗證驗證碼]** 選擇 **[!UICONTROL 在提交表單時驗證驗證碼]**。
1. 點擊 ![完成](assets/save_icon.svg) 的子菜單。

#### 驗證用戶操作和條件驗證驗證碼 {#validate-captcha-user-action}

要基於條件和用戶操作驗證驗證碼，請執行以下操作：

1. 點擊驗證碼元件並選擇 ![招商](assets/configure-icon.svg) 的子菜單。
1. 在 **[!UICONTROL 驗證驗證驗證碼]** 選擇 **[!UICONTROL 對用戶操作驗證驗證碼]**。
1. 點擊 ![完成](assets/save_icon.svg) 的子菜單。

[!DNL Experience Manager Forms] 提供 `ValidateCAPTCHA` 使用預定義條件驗證CAPTCHA的API。 您可以使用自定義提交操作或在自適應表單中定義元件規則來調用API。

以下是 `ValidateCAPTCHA` 使用預定義條件驗證CAPTCHA的API:

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

該示例表示 `ValidateCAPTCHA` API僅在填寫表單時用戶指定的數字框中的位數大於5時驗證表單中的驗證碼。

**選項1:使用 [!DNL Experience Manager Forms] 使用自定義提交操作驗證驗證查詢API**

執行以下步驟以使用 `ValidateCAPTCHA` 使用自定義提交操作驗證驗證碼的API:

1. 添加包含 `ValidateCAPTCHA` 自定義提交操作的API。 有關自定義提交操作的詳細資訊，請參閱 [為自適應Forms建立自定義提交操作](custom-submit-action-form.md)。
1. 從中選擇自定義提交操作的名稱 **[!UICONTROL 提交操作]** 下拉清單 **[!UICONTROL 提交]** 自適應窗體的屬性。
1. 點擊 **[!UICONTROL 提交]**。 根據中定義的條件驗證驗證驗證碼 `ValidateCAPTCHA` 自定義提交操作的API。

**選項2:使用 [!DNL Experience Manager Forms] 在提交表單之前驗證CAPTCHA API以驗證用戶操作上的CAPTCHA**

您還可以調用 `ValidateCAPTCHA` API，方法是對自適應表單中的元件應用規則。

例如，添加 **[!UICONTROL 驗證驗證驗證碼]** 的子菜單。

下圖說明了如何在按一下時調用服務 **[!UICONTROL 驗證驗證驗證碼]** 按鈕：

![進行驗證碼驗證](assets/captcha-validation1.gif)

可以調用包含的自定義Servlet `ValidateCAPTCHA` 使用規則編輯器的API，並根據驗證結果啟用或禁用自適應表單的提交按鈕。

同樣，您可以使用規則編輯器在自適應表單中包含驗證驗證碼查詢的自定義方法。

### 添加自定義驗證碼服務 {#add-custom-captcha-service}

[!DNL Experience Manager Forms] 提供reCAPTCHA作為驗證碼服務。 但是，您可以添加要在 **[!UICONTROL 驗證碼服務]** 的子菜單。

下面是向自適應表單添加附加CAPTCHA服務的介面的示例實現：

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

`captchaPropertyNodePath` 引用Sling儲存庫中CAPTCHA元件的資源路徑。 使用此屬性可包括特定於驗證碼元件的詳細資訊。 比如說， `captchaPropertyNodePath` 包括在CAPTCHA元件上配置的reCAPTCHA雲配置的資訊。 雲配置資訊提供 **[!UICONTROL 站點密鑰]** 和 **[!UICONTROL 密鑰]** 用於實施reCAPTCHA服務的設定。

`userResponseToken` 指 `g_recaptcha_response` 在解決一個形式的驗證碼後產生的。
