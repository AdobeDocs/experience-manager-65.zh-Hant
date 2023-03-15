---
title: 連線到 Microsoft Translator
seo-title: Connecting to Microsoft Translator
description: 了解如何將AEM連線至Microsoft Translator。
seo-description: Learn how to connect AEM to Microsoft Translator.
uuid: 5e3916ec-36a0-4d31-94ff-c340a462411a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: a7958411-b509-428e-bbe2-42efe8fd1add
feature: Language Copy
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 3%

---

# 連線到 Microsoft Translator{#connecting-to-microsoft-translator}

為Microsoft Translator雲端服務建立設定，以使用您的Microsoft翻譯帳戶來轉譯AEM頁面內容、社群內容或資產。

| 屬性 | 說明 |
|---|---|
| 翻譯標籤 | 翻譯服務的顯示名稱。 |
| 翻譯歸因 | （選用）針對使用者產生的內容，例如顯示在翻譯文字旁的歸因 `Translations by Microsoft`. |
| 工作區ID | （選用）要使用的自訂Microsoft轉譯器引擎ID。 |
| 訂閱金鑰 | 您的Microsoft TranslatorMicrosoft訂閱密鑰。 |

建立設定後，您需要 [啟動](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations).

下列程式使用觸控最佳化UI來建立Microsoft Translator設定。

1. 在導軌上，按一下或點選「工具>Cloud Services」。
1. 在「 Microsoft Translator 」區域中，按一下或點選「 Show Configurations 」。
1. 按一下「可用配置」旁的+連結。

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. 輸入您設定的標題。 標題會在「Cloud Services」主控台以及頁面屬性下拉式清單中識別設定。 預設名稱是以標題為基礎。 （可選）鍵入用於儲存配置的儲存庫節點的名稱。 您應使用父配置屬性（儲存庫節點的路徑）的預設值。
1. 按一下建立。
1. 在出現的對話框中，鍵入屬性的值，然後按一下確定。

## 範例Microsoft轉譯器Cloud Service設定 {#sample-microsoft-translator-cloud-service-configurations}

以下Microsoft Translator雲服務配置隨Geometrixx示例一起安裝。 某些設定範例使用試用的Microsoft翻譯帳戶，每月最多可允許2 000 000個免費翻譯字元。

### Microsoft Translator 試用版授權 {#microsoft-translator-trial-license}

Microsoft Translator試用許可證配置是隨Geometrixx Outdoors示例包一起安裝的示例配置。 此配置使用Microsoft Translator帳戶，該帳戶具有免費訂閱，每月允許2 000 000個翻譯字元。

### Microsoft翻譯試用授權 — Geometrixx戶外 {#microsoft-translator-trial-license-geometrixx-outdoors}

Microsoft Translator試用版授權 — Geometrixx — 戶外配置是隨Geometrixx Outdoors一起安裝的示例配置。 此配置使用與Microsoft Translator試用許可證配置相同的免費Microsoft Translator帳戶。 帳戶有免費訂閱，每月可允許2 000 000個翻譯字元。

此Microsoft轉譯器配置已優化，以便與Geometrixx Outdoors示例站點的內容類型一起使用。

### 升級Microsoft Translator試用版許可證配置 {#upgrading-the-microsoft-translator-trial-license-configuration}

Microsoft翻譯設定頁面提供Microsoft網站的便利連結，以取得適用於生產系統的帳戶訂閱。

1. 在導軌上，按一下或點選「工具>作業>雲端>Cloud Services」。
1. 在「Microsoft Translator 」區域中，按一下或點選「 Show Configurations 」，然後按一下或點選「 Microsoft Translator Trial License 」(「Microsoft Translation Configuration 」)。

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 在配置頁面上，按一下升級訂閱。 使用開啟的Microsoft網頁來設定您的帳戶。

   ![chlimage_1-384](assets/chlimage_1-384.png)

### 自訂您的Microsoft Translator引擎 {#customizing-your-microsoft-translator-engine}

Microsoft翻譯設定頁面提供Microsoft網站的便利連結，可自訂您的Microsoft翻譯引擎。 ([https://hub.microsofttranslator.com](https://hub.microsofttranslator.com/))

1. 在導軌上，按一下或點選「工具>作業>雲端>Cloud Services」。
1. 在「 Microsoft Translator 」區域中，按一下或點選「 Show Configurations 」，然後按一下或點選您要自訂的設定。
1. 在配置頁上，按一下「自定義轉換器」。 使用開啟的Microsoft網頁來自訂您的服務。

## 激活轉換器服務配置 {#activating-the-translator-service-configurations}

您需要啟動雲端服務設定，以支援複製到發佈執行個體的翻譯內容。 使用 [激活完整節（樹）](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree) 啟用儲存Microsoft Translator或協力廠商雲端服務設定的存放庫節點。 節點位於以下父節點下：

* Microsoft翻譯服務：/libs/settings/cloudconfigs/translation/msft-translation
* 第三方翻譯：/etc/cloudservices/machine-translation
