---
title: 在最適化表單中使用驗證碼
seo-title: Using CAPTCHA in adaptive forms
description: 瞭解如何在適用性表單中設定AEM CAPTCHA或Google reCAPTCHA服務。
seo-description: Learn how to configure AEM CAPTCHA or Google reCAPTCHA service in adaptive forms.
uuid: 0e11e98a-12ac-484c-b77f-88ebdf0f40e5
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: adaptive_forms, author
discoiquuid: 4c53dfc0-25ca-419d-abfe-cf31fc6ebf61
docset: aem65
feature: Adaptive Forms
exl-id: 9b4219b8-d5eb-4099-b205-d98d84e0c249
source-git-commit: 498fb5f6f923710a907e1cf525f56f49850e16b2
workflow-type: tm+mt
source-wordcount: '1995'
ht-degree: 0%

---

# 在最適化表單中使用驗證碼{#using-captcha-in-adaptive-forms}

|版本 |文章連結 | |-------- |---------------------------- | | AEMAS A CLOUD SERVICE |    [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-components-to-an-adaptive-form/captcha-adaptive-forms.html)                  | | AEM 6.5 |本文 |
=======
<span class="preview"> Adobe建議使用現代化且可擴充的資料擷取 [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) 的 [建立新的Adaptive Forms](/help/forms/using/create-an-adaptive-form-core-components.md) 或 [將最適化Forms新增至AEM Sites頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). 這些元件代表最適化Forms建立工作取得重大進展，可確保提供令人驚歎的使用者體驗。 本文說明使用基礎元件製作最適化Forms的舊方法。 </span>


CAPTCHA （完全自動化的公用圖靈測試，用於區分電腦和人類）是一種常用於線上交易的程式，用來區分人類和自動化程式或機器人。 這會帶來挑戰，並評估使用者回應，以判斷它是人類還是機器人與網站互動。 它可防止使用者在測試失敗時繼續進行，並透過防止機器人張貼垃圾郵件或惡意目的來確保線上交易的安全。

AEM Forms支援最適化表單中的驗證碼。 您可以使用Google的reCAPTCHA服務來實作CAPTCHA。

>[!NOTE]
>
>* AEM Forms支援reCAPTCHA v2和enterprise。 不支援任何其他版本。
>* AEM Forms應用程式上的離線模式不支援適用性表單中的驗證碼。

## 由Google為最適化Forms設定reCAPTCHA服務 {#google-reCAPTCHA}

AEM Forms使用者可以使用Google的reCAPTCHA服務，在最適化表單中實作CAPTCHA。 它提供進階的驗證碼功能，以保護您的網站。 如需reCAPTCHA運作方式的詳細資訊，請參閱 [Google reCAPTCHA](https://developers.google.com/recaptcha/). reCAPTCHA服務（包括reCAPTCHA v2和reCAPTCHA Enterprise）已整合至AEM Forms。 您可以視需要設定reCAPTCHA服務，以啟用：

* [AEM Forms中的reCAPTCHA Enterprise](#steps-to-implement-reCAPTCHA-enterprise-in-forms)
* [AEM Forms中的reCAPTCHA v2](#steps-to-implement-reCAPTCHA-v2-in-forms)

![reCAPTCHA](/help/forms/using/assets/recaptcha_new.png)

### 設定reCAPTCHA Enterprise  {#steps-to-implement-reCAPTCHA-enterprise-in-forms}

1. 建立 [reCAPTCHA企業專案](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#before-you-begin) 啟用方式 [reCAPTCHA Enterprise API](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#enable-the-recaptcha-enterprise-api).
1. [取得](https://support.google.com/googleapi/answer/7014113?hl=en#:~:text=To%20locate%20your%20project%20ID,a%20member%20of%20are%20displayed) 專案識別碼。
1. 建立 [API金鑰](https://cloud.google.com/recaptcha-enterprise/docs/set-up-non-google-cloud-environments-api-keys#create_an_api_key) 和 [網站的網站金鑰](https://cloud.google.com/recaptcha-enterprise/docs/create-key#create-key).
1. 建立雲端服務的設定容器。

   1. 前往 **[!UICONTROL 「工具」>「一般」>「設定瀏覽器」]**. 請參閱 [設定瀏覽器](/help/sites-administering/configurations.md) 說明檔案以取得詳細資訊。
   1. 請執行以下操作來啟用雲端設定的全域資料夾，或跳過此步驟來建立和設定雲端服務設定的另一個資料夾。
      1. 在設定瀏覽器中，選取 **[!UICONTROL 全域]** 資料夾並點選 **[!UICONTROL 屬性]**.
      1. 在「組態屬性」對話方塊中，啟用 **[!UICONTROL 雲端設定]**.
      1. 點選 **[!UICONTROL 儲存並關閉]** 以儲存設定並結束對話方塊。

   1. 在設定瀏覽器中，點選 **[!UICONTROL 建立]**.
   1. 在建立設定對話方塊中，指定資料夾的標題並啟用 **[!UICONTROL 雲端設定]**.
   1. 點選 **[!UICONTROL 建立]** 以建立為雲端服務設定啟用的資料夾。
1. 設定reCAPTCHA Enterprise的雲端服務。

   1. 在您的Experience Manager編寫執行個體上，前往 ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]**.
   1. 點選 **[!UICONTROL reCAPTCHA]**. 「組態」頁面隨即開啟。 選取在上一步建立的設定容器並點選 **[!UICONTROL 建立]**.
   1. 選取reCAPTCHA Enterprise版本並指定reCAPTCHA Enterprise服務的名稱；專案ID、網站金鑰和API金鑰（在步驟2和3中取得）。
   1. 選取金鑰型別，金鑰型別應與Google雲端專案中設定的網站金鑰相同，例如， **核取方塊網站索引鍵** 或 **以分數為基礎的網站金鑰**.
   1. 指定介於0到1之間的臨界值分數([按一下以進一步瞭解分數](https://cloud.google.com/recaptcha-enterprise/docs/interpret-assessment#interpret_scores))。 分數大於或等於臨界值分數會識別人類互動，否則會被視為機器人互動。

      > 注意：
      >
      > * 表單作者可以在適合不間斷表單提交的範圍中指定分數。

   1. 點選 **[!UICONTROL 建立]** 以建立雲端服務設定。

   1. 在「編輯元件」對話方塊中，指定名稱、專案ID、網站金鑰、API金鑰（在步驟2和3中取得）、選取金鑰型別，然後輸入臨界值分數。 點選 **[!UICONTROL 儲存設定]** 然後點選 **[!UICONTROL 確定]** 以完成設定。

reCAPTCHA Enterprise服務啟用後，就可在調適型表單中使用。 另請參閱 [在最適化表單中使用驗證碼](#using-reCAPTCHA).

![reCAPTCHA Enterprise](/help/forms/using/assets/recaptcha1-enterprise.png)


### 設定Google reCAPTCHA v2 {#steps-to-implement-reCAPTCHA-v2-in-forms}

1. 取得 [recaptcha API金鑰組](https://www.google.com/recaptcha/admin) 來自Google。 它包含 **網站金鑰** 和 **秘密金鑰**.
1. 建立雲端服務的設定容器。
   1. 前往 **[!UICONTROL 「工具」>「一般」>「設定瀏覽器」]**. 請參閱 [設定瀏覽器](/help/sites-administering/configurations.md) 說明檔案以取得詳細資訊。
   1. 請執行以下操作來啟用雲端設定的全域資料夾，或跳過此步驟來建立和設定雲端服務設定的另一個資料夾。

      1. 在設定瀏覽器中，選取 **[!UICONTROL 全域]** 資料夾並點選 **[!UICONTROL 屬性]**.

      1. 在「組態屬性」對話方塊中，啟用 **[!UICONTROL 雲端設定]**.
      1. 點選 **[!UICONTROL 儲存並關閉]** 以儲存設定並結束對話方塊。

   1. 在設定瀏覽器中，點選 **[!UICONTROL 建立]**.
   1. 在建立設定對話方塊中，指定資料夾的標題並啟用 **[!UICONTROL 雲端設定]**.
   1. 點選 **[!UICONTROL 建立]** 以建立為雲端服務設定啟用的資料夾。

1. 設定reCAPTCHA v2的雲端服務。

   1. 在您的AEM編寫執行個體上，前往 ![tools-1](assets/tools-1.png) > **Cloud Services**.
   1. 點選 **[!UICONTROL reCAPTCHA]**. 「組態」頁面隨即開啟。 選取在上一步建立的設定容器並點選 **[!UICONTROL 建立]**.
   1. 選取版本為reCAPTCHA v2，指定reCAPTCHA服務（在步驟1中取得）的名稱、網站金鑰和秘密金鑰，然後點選 **[!UICONTROL 建立]** 以建立雲端服務設定。
   1. 在「編輯元件」對話方塊中，指定在步驟1中取得的場地和秘密金鑰。 點選 **[!UICONTROL 儲存設定]** 然後點選 **確定** 以完成設定。

   設定reCAPTCHA服務後，就可在調適型表單中使用。 如需詳細資訊，請參閱 [在最適化表單中使用驗證碼](#using-captcha).

![reCAPTCHA v2](/help/forms/using/assets/recaptcha-v2.png)


## 在最適化表單中使用reCAPTCHA {#using-reCAPTCHA}

若要在最適化表單中使用reCAPTCHA：

1. 在編輯模式下開啟最適化表單。

   >[!NOTE]
   >
   >確定建立最適化表單時選取的設定容器包含reCAPTCHA雲端服務。 您也可以編輯最適化表單屬性，以變更與表單相關聯的設定容器。

1. 在元件瀏覽器中，拖放 **驗證碼** 元件至最適化表單。

   >[!NOTE]
   >
   >不支援在最適化表單中使用多個Captcha元件。 此外，不建議在標示為延遲載入的面板或片段中使用驗證碼。

   >[!NOTE]
   >
   >驗證碼會區分大小寫，且約一分鐘後過期。 因此，建議將驗證碼元件放在最適化表單中提交按鈕之前。

1. 選取您新增的Captcha元件並點選 ![cmppr](assets/cmppr.png) 以編輯其屬性。
1. 指定驗證碼介面工具集的標題。 預設值為 **驗證碼**. 選取 **隱藏標題** 如果您不想顯示標題。
1. 從 **驗證碼服務** 下拉式清單，選取 **reCAPTCHA** 啟用reCAPTCHA服務（若您已依照中的說明進行設定） [Google的reCAPTCHA服務](#google-reCAPTCHA).
1. 從「設定」下拉式清單中選取設定。
1. **如果選取的組態版本為reCAPTCHA Enterprise**：
   1. 您可以透過以下方式選取reCAPTCHA雲端設定 **金鑰型別** 作為 **核取方塊**. 在核取方塊索引鍵中，如果驗證碼驗證失敗，自訂的錯誤訊息會顯示為內嵌訊息。 您可以選取大小為 **[!UICONTROL 一般]** 和 **[!UICONTROL 壓縮]**.
   1. 您可以透過以下方式選取reCAPTCHA雲端設定 **金鑰型別** 作為 **以分數為基礎**. 在以分數為基礎的金鑰型別中，如果驗證碼驗證失敗，自訂的錯誤訊息會顯示為快顯訊息。
   1. 當您選取 **[!UICONTROL 繫結參考]** 提交的資料是已繫結的資料，否則就是未繫結的資料。 以下是提交表單時，未繫結資料和已繫結資料（以SSN為繫結參考）的XML範例。

      ```xml
          <?xml version="1.0" encoding="UTF-8" standalone="no"?>
          <afData>
          <afUnboundData>
              <data>
                  <captcha16820607953761>
                      <captchaType>reCAPTCHAEnterprise</captchaType>
                      <captchaScore>0.9</captchaScore>
                  </captcha16820607953761>
              </data>
          </afUnboundData>
          <afBoundData>
              <Root
                  xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                  <PersonalDetails>
                      <SSN>371237912</SSN>
                      <FirstName>Sarah </FirstName>
                      <LastName>Smith</LastName>
                  </PersonalDetails>
                  <OtherInfo>
                      <City>California</City>
                      <Address>54 Residency</Address>
                      <State>USA</State>
                      <Zip>123112</Zip>
                  </OtherInfo>
              </Root>
          </afBoundData>
          <afSubmissionInfo>
              <stateOverrides/>
              <signers/>
              <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
              <afSubmissionTime>20230608034928</afSubmissionTime>
          </afSubmissionInfo>
          </afData>
      ```


      ```xml
          <?xml version="1.0" encoding="UTF-8" standalone="no"?>
          <afData>
          <afUnboundData>
              <data/>
          </afUnboundData>
          <afBoundData>
              <Root
                  xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"
                  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                  <PersonalDetails>
                      <SSN>
                          <captchaType>reCAPTCHAEnterprise</captchaType>
                          <captchaScore>0.9</captchaScore>
                      </SSN>
                      <FirstName>Sarah</FirstName>
                      <LastName>Smith</LastName>
                  </PersonalDetails>
                  <OtherInfo>
                      <City>California</City>
                      <Address>54 Residency</Address>
                      <State>USA</State>
                      <Zip>123112</Zip>
                  </OtherInfo>
              </Root>
          </afBoundData>
          <afSubmissionInfo>
              <stateOverrides/>
              <signers/>
              <afPath>/content/dam/formsanddocuments/captcha-form</afPath>
              <afSubmissionTime>20230608035111</afSubmissionTime>
          </afSubmissionInfo>
          </afData>
      ```


   **如果選取的組態有版本reCAPTCHA v2**：
   1. 選取大小為 **[!UICONTROL 一般]** 或 **[!UICONTROL 壓縮]** 用於reCAPTCHA小工具。 您也可以選取 **[!UICONTROL 隱藏]** 選項，僅在可疑活動的情況下顯示CAPTCHA質詢。 此 **受reCAPTCHA保護** 徽章（如下所示）會顯示在受保護的表單上。

      ![受reCAPTCHA徽章保護的Google](/help/forms/using/assets/google-recaptcha-v2.png)


   已在最適化表單上啟用reCAPTCHA服務。 您可以預覽表單並檢視驗證碼運作中。

1. 儲存屬性。

>[!NOTE]
> 
> 不要選取 **[!UICONTROL 預設]** Captcha服務下拉式清單中，預設的AEM驗證碼服務已過時。

### 根據規則顯示或隱藏驗證碼元件 {#show-hide-captcha}

您可以根據在最適化表單中套用至元件的規則，選擇顯示或隱藏驗證碼元件。 點選元件，選取 ![編輯規則](assets/edit-rules-icon.svg)，然後點選 **[!UICONTROL 建立]** 以建立規則。 如需建立規則的詳細資訊，請參閱 [規則編輯器](rule-editor.md).

例如，只有在表單中的「貨幣值」欄位的值超過25000時，CAPTCHA元件才會顯示在調適型表單中。

點選 **[!UICONTROL 貨幣值]** 欄位並建立以下規則：

![顯示或隱藏規則](assets/rules-show-hide-captcha.png)

>[!NOTE]
>
> * 如果您選取reCAPTCHA v2設定，大小為 **[!UICONTROL 隱藏]** 或reCAPTCHA Enterprise分數型金鑰，則顯示/隱藏選項不適用。

### 進行驗證碼驗證 {#validate-captcha}

您可以在提交表單時驗證最適化表單中的驗證碼，或依據使用者動作和條件進行驗證碼驗證。

#### 在表單提交時驗證驗證碼 {#validation-form-submission}

若要在提交最適化表單時自動驗證碼：

1. 點選CAPTCHA元件並選取 ![cmppr](assets/configure-icon.svg) 以檢視元件屬性。
1. 在 **[!UICONTROL 驗證碼驗證]** 區段，選取 **[!UICONTROL 在表單提交時驗證驗證碼]**.
1. 點選 ![完成](assets/save_icon.svg) 以儲存元件屬性。

#### 驗證使用者動作和條件的驗證碼 {#validate-captcha-user-action}

若要根據條件和使用者動作來驗證驗證碼：

1. 點選CAPTCHA元件並選取 ![cmppr](assets/configure-icon.svg) 以檢視元件屬性。
1. 在 **[!UICONTROL 驗證碼驗證]** 區段，選取 **[!UICONTROL 使用者動作時驗證驗證碼]**.
1. 點選 ![完成](assets/save_icon.svg) 以儲存元件屬性。

   >[!NOTE]
   >
   >
   > 如果您選取reCAPTCHA v2設定，大小為 **[!UICONTROL 隱藏]** 或reCAPTCHA Enterprise分數型金鑰，則使用者動作上的有效Captcha不適用。

[!DNL Experience Manager Forms] 提供 `ValidateCAPTCHA` 使用預先定義的條件來驗證驗證碼的API。 您可以使用自訂提交動作或透過在調適型表單中定義元件規則來叫用API。

以下範例為 `ValidateCAPTCHA` 使用預先定義條件來驗證驗證碼的API：

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

此範例表示 `ValidateCAPTCHA` 只有在使用者在填寫表單時指定的數字方塊位數大於5時，API才會驗證表單中的驗證碼。

**選項1：使用 [!DNL Experience Manager Forms] ValidateCAPTCHA API可使用自訂提交動作來驗證CAPTCHA**

執行以下步驟以使用 `ValidateCAPTCHA` 使用自訂提交動作驗證驗證碼的API：

1. 新增包含 `ValidateCAPTCHA` 自訂提交動作的API。 如需自訂提交動作的詳細資訊，請參閱 [建立最適化Forms的自訂提交動作](custom-submit-action-form.md).
1. 從中選擇自訂提交動作的名稱 **[!UICONTROL 提交動作]** 中的下拉式清單 **[!UICONTROL 提交]** 最適化表單的屬性。
1. 點選 **[!UICONTROL 提交]**. 系統會根據中定義的條件來驗證驗證碼 `ValidateCAPTCHA` 自訂提交動作的API。

**選項2：使用 [!DNL Experience Manager Forms] ValidateCAPTCHA API可在提交表單前，依使用者動作驗證驗證碼**

您也可以叫用 `ValidateCAPTCHA` API的方式是對調適型表單中的元件套用規則。

例如，您新增 **[!UICONTROL 驗證碼驗證]** 最適化表單中的按鈕，並建立規則以在按一下按鈕時叫用服務。

下圖說明如何在 **[!UICONTROL 驗證碼驗證]** 按鈕：

![進行驗證碼驗證](assets/captcha-validation1.gif)

您可以叫用包含的自訂servlet `ValidateCAPTCHA` API使用規則編輯器，並根據驗證結果啟用或停用最適化表單的提交按鈕。

同樣地，您可以使用規則編輯器在適用性表單中包含驗證CAPTCHA的自訂方法。

### 新增自訂驗證碼服務 {#add-custom-captcha-service}

[!DNL Experience Manager Forms] 提供reCAPTCHA作為CAPTCHA服務。 不過，您可以新增自訂服務，以顯示於 **[!UICONTROL 驗證碼服務]** 下拉式清單。

以下是將其他CAPTCHA服務新增至最適化表單的介面實作範例：

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

`captchaPropertyNodePath` 參考Sling存放庫中驗證碼元件的資源路徑。 此屬性用於包含驗證碼元件的特定詳細資料。 例如， `captchaPropertyNodePath` 包含在CAPTCHA元件上設定的reCAPTCHA雲端設定資訊。 雲端設定資訊提供 **[!UICONTROL 網站金鑰]** 和 **[!UICONTROL 秘密金鑰]** 實作reCAPTCHA服務的設定。

`userResponseToken` 請參考 `g_reCAPTCHA_response` 在表單中解決驗證碼後產生的驗證碼。
