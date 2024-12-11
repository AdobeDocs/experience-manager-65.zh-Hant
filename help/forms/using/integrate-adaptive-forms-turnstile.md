---
title: 如何在AEM最適化表單6.5中使用Turnstile？
description: 透過Turnstile服務輕鬆增強表單安全性。 內的逐步指南！
feature: Adaptive Forms, Foundation Components
role: User, Developer
exl-id: bed93ce3-89db-477a-8316-7598275e4bca
source-git-commit: 94a9f4087e36bfe5701ad9aafd4e8446ca643ddf
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 2%

---

# 使用Turnstile連線您的AEM Forms環境 {#connect-your-forms-environment-with-turnstile-service}

<!--
<span class="preview">This feature is based on Feature Toggle id `FT_FORMS-12407`. To enable the feature, follow the steps given in the [Enable Feature Toggle](/help/forms/using/enable-feature-toggle.md) article. </span>
-->

<span class="preview">預設不會啟用此功能。 您可以從您的官方地址寫信到aem-forms-ea@adobe.com，以要求存取此功能。</span>

CAPTCHA （完全自動化公用圖靈測試來區分電腦和人之間的差異）是一種常用於線上交易的程式，以區分人和自動化程式或機器人。 這會帶來挑戰，並評估使用者的回應，以判斷其是否為人類或機器人與網站互動。 它可防止使用者在測試失敗時繼續進行，並透過防止機器人張貼垃圾郵件或惡意目的來確保線上交易的安全。

AEM Forms 6.5支援下列驗證碼解決方案：

* [Turnstile驗證碼](/help/forms/using/integrate-adaptive-forms-turnstile.md)
* [Google reCAPTCHA](/help/forms/using/captcha-adaptive-forms.md)
* [驗證碼](/help/forms/using/integrate-adaptive-forms-hcaptcha.md)


<!-- ![Turnstile](assets/Turnstile-challenge.png)-->

## 將AEM Forms環境與Turnstile驗證碼整合

Cloudflare的Turnstile驗證碼是一種安全性措施，旨在保護表單和網站免受自動化機器人、惡意攻擊、垃圾郵件和不需要的自動化流量的傷害。 在允許提交表單前，它會在表單提交上顯示核取方塊，以驗證使用者是否為人類。

>[!VIDEO](https://video.tv.adobe.com/v/3440940/)

### 整合AEM Forms環境與Turnstile驗證碼的必要條件 {#prerequisite}

若要設定AEM Forms的Turnstile，您必須從Turnstile網站取得[Turnstile網站金鑰與秘密金鑰](https://developers.cloudflare.com/turnstile/get-started/)。

### 設定Turnstile {#steps-to-configure-hcaptcha}

若要將AEM Forms與Turnstile服務整合，請執行下列步驟：

1. 在您的AEM Forms環境中建立設定容器。 設定容器內含用來將AEM Forms連線至外部服務的雲端設定。 若要建立組態容器：
   1. 開啟您的AEM Forms環境。
   1. 前往&#x200B;**[!UICONTROL 工具 > 一般 > 設定瀏覽器]**。
   1. 在「組態瀏覽器」中，選取現有資料夾或建立新資料夾：
      * 若要建立&#x200B;**新資料夾**&#x200B;並啟用雲端設定：
         1. 在組態瀏覽器中，按一下&#x200B;**[!UICONTROL 建立]**。
         1. 在[建立設定]對話方塊中，指定名稱、標題，並檢查&#x200B;**[!UICONTROL 雲端設定]**。
         1. 按一下&#x200B;**[!UICONTROL 建立]**。
      * 若要啟用&#x200B;**現有資料夾**&#x200B;的雲端設定：
         1. 在組態瀏覽器中，選取資料夾並按一下&#x200B;**[!UICONTROL 內容]**。
         1. 在[組態內容]對話方塊中，啟用&#x200B;**[!UICONTROL 雲端組態]**。
         1. 按一下&#x200B;**[!UICONTROL 儲存並關閉]**&#x200B;以儲存組態。

1. 設定您的Cloud Service：
   1. 在您的AEM作者執行個體上，前往![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]**，然後按一下&#x200B;**[!UICONTROL Turnstile]**。
      在Cloud Service中![旋轉門](assets/turnstile-in-ui.png)
   1. 選取已建立或已更新的設定容器，如上一節所述。 按一下&#x200B;**[!UICONTROL 建立]**。
      ![組態旋轉門](assets/config-hcaptcha.png)
   1. 將&#x200B;**[!UICONTROL Widget Type]**&#x200B;指定為Managed、非互動式或隱藏式。
   1. 提供其他詳細資料，例如&#x200B;**[!UICONTROL 標題]**、**[!UICONTROL 名稱]**。
   1. 針對在先決條件](#prerequisite)中取得的Turnstile服務[，指定&#x200B;**[!UICONTROL 網站金鑰]**&#x200B;和&#x200B;**[!UICONTROL 秘密金鑰]**。
   1. 按一下&#x200B;**[!UICONTROL 建立]**。

      ![設定Cloud Service以連線您的AEM Forms環境與Turnstile](assets/config-turntstile.png)

   >[!NOTE]
   > 使用者不需要修改使用者端JavaScript驗證URL和伺服器端驗證URL，因為已預先填入Turnstile驗證。

   設定Turnstile Captcha服務後，就可在最適化表單中使用。

## 在最適化表單{#using-turnstile-aem-6.5}中使用Turnstile

1. 開啟您的AEM Forms環境。
1. 移至&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms和檔案]**。
1. 選取最適化表單，然後按一下&#x200B;**[!UICONTROL 屬性]**。 在&#x200B;**[!UICONTROL 設定容器]**&#x200B;中，選取包含連線AEM Forms與Turnstile的雲端設定的設定容器。
1. 按一下「**[!UICONTROL 儲存並關閉]**」。

   如果您沒有組態容器可設定Captcha服務，請參閱[設定Turnstile](#configure-turnstile-steps-to-configure-hcaptcha)一節，以瞭解如何建立組態容器。

   ![選取設定容器](assets/captcha-properties.png)

1. 選取最適化表單，然後按一下&#x200B;**[!UICONTROL 編輯]**，在編輯器中開啟最適化表單。
1. 從元件瀏覽器中，將&#x200B;**[!UICONTROL 驗證碼]**&#x200B;元件拖放至最適化表單上。
1. 選取&#x200B;**[!UICONTROL 驗證碼]**&#x200B;元件，然後按一下屬性![屬性圖示](assets/configure-icon.svg)圖示。 它會開啟屬性對話方塊。 指定下列屬性：

   <!--![Turnstile v2](assets/turnstile-settings-v2.png)-->
   ![Cloudfare Turnstile v1](assets/turnstile-setting-v1.png)

   * **[!UICONTROL 標題]：**&#x200B;指定驗證碼元件的標題。 您可以在表單和規則編輯器中以表單元件的唯一標題輕鬆識別表單元件。
   * **[!UICONTROL 組態設定]：**&#x200B;選取為Turnstile設定的雲端組態。
   * **[!UICONTROL 驗證訊息]：**&#x200B;提供驗證訊息，以便在表單提交或使用者動作時驗證驗證碼。
   * **[!UICONTROL 驗證碼服務]：**&#x200B;選取表單提交的驗證碼服務，這裡選取Turnstile®。
   * **[!UICONTROL 組態設定]：**&#x200B;選取您為Turnstile®設定的雲端組態。
     >[!NOTE]
     >基於類似目的，您的環境中可以有多個雲端設定。 因此，請謹慎選擇服務。 如果未列出任何服務，請參閱[將您的AEM Forms環境與Turnstile連線](#connect-your-forms-environment-with-turnstile-service)，以瞭解如何建立將AEM Forms環境與Turnstile服務連結的Cloud Service。

   * **[!UICONTROL 錯誤訊息]：**&#x200B;提供驗證碼提交失敗時向使用者顯示的錯誤訊息。
   * **驗證碼大小：**&#x200B;您可以選取hCaptcha®挑戰對話方塊的顯示大小。 使用&#x200B;**[!UICONTROL Compact]**&#x200B;選項可顯示小尺寸，使用&#x200B;**[!UICONTROL Normal]**&#x200B;可顯示相對大尺寸的hCaptcha®挑戰對話方塊。

1. 選取「**[!UICONTROL 完成]**」。


現在，只有合法的表單，表單填寫者才能成功清除Turnstile服務帶來的挑戰，才能提交表單。

![Turnstile挑戰賽](assets/turnstile-challenge.png)


## 常見問題

* **問：我可以在最適化表單中使用多個驗證碼元件嗎？**
* **Ans：**&#x200B;不支援在最適化表單中使用一個以上的Captcha元件。 此外，不建議在片段或標示為延遲載入的面板中使用驗證碼元件。

## 另請參閱 {#see-also}

* [在最適化表單中使用驗證碼](/help/forms/using/captcha-adaptive-forms.md)
* [在最適化表單中使用驗證碼](/help/forms/using/integrate-adaptive-forms-hcaptcha.md)
