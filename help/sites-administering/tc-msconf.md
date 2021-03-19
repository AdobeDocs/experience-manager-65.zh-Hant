---
title: 連接到Microsoft Translator
seo-title: 連接到Microsoft Translator
description: 瞭解如何連AEM接Microsoft Translator。
seo-description: 瞭解如何連AEM接Microsoft Translator。
uuid: 5e3916ec-36a0-4d31-94ff-c340a462411a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: a7958411-b509-428e-bbe2-42efe8fd1add
feature: 語言副本
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 1%

---


# 連接到Microsoft Translator{#connecting-to-microsoft-translator}

為Microsoft Translator雲端服務建立組態，以使用您的Microsoft Translation帳戶AEM來轉換頁面內容、社群內容或資產。

| 屬性 | 說明 |
|---|---|
| 翻譯標籤 | 翻譯服務的顯示名稱。 |
| 翻譯歸因 | （選擇性）對於使用者產生的內容，顯示在翻譯文字旁的歸因，例如`Translations by Microsoft`。 |
| 工作區ID | （可選）您要使用的自訂Microsoft Translator引擎ID。 |
| 訂閱金鑰 | 您的Microsoft Translator訂閱金鑰。 |

建立配置後，需要[激活它](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations)。

以下過程使用最佳化觸控式UI來建立Microsoft Translator組態。

1. 在邊欄上，按一下或點選「工具>Cloud Services」。
1. 在「Microsoft Translator」區域中，按一下或點選「Show Configurations」（顯示配置）。
1. 按一下「Available Configurations（可用配置）」旁邊的+連結。

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. 輸入您設定的標題。 此標題可識別Cloud Services控制台和頁面屬性下拉式清單中的設定。 預設名稱是以標題為基礎。 （可選）鍵入用於儲存配置的儲存庫節點的名稱。 您應使用「父配置」屬性的預設值，該屬性是儲存庫節點的路徑。
1. 按一下建立。
1. 在出現的對話方塊中，輸入屬性值，然後按一下「確定」。

## Microsoft TranslatorCloud Service配置示例{#sample-microsoft-translator-cloud-service-configurations}

下列Microsoft Translator雲服務配置隨Geometrixx示例一起安裝。 某些配置示例使用試用版Microsoft Translation帳戶，該帳戶每月最多允許2 000 000個免費翻譯字元。

### Microsoft Translator 試用版授權 {#microsoft-translator-trial-license}

Microsoft Translator試用版許可證配置是隨Geometrixx Outdoors示例軟體包一起安裝的示例配置。 此配置使用Microsoft Translator帳戶，該帳戶有免費訂閱，允許每月2 000 000個翻譯字元。

### Microsoft Translator試用版授權-Geometrixx-戶外{#microsoft-translator-trial-license-geometrixx-outdoors}

Microsoft Translator試用版授權——戶外配置是與Geometrixx Outdoors一起安裝的示例配置。 此配置使用與Microsoft Translator試用版許可證配置相同的免費Microsoft Translator帳戶。 該帳戶有免費訂閱，每月允許2 000 000個翻譯字元。

此Microsoft Translator配置已優化，可用於Geometrixx Outdoors示例站點的內容類型。

### 升級Microsoft Translator試用版許可證配置{#upgrading-the-microsoft-translator-trial-license-configuration}

「Microsoft翻譯」配置頁提供了指向Microsoft網站的方便連結，以便獲得適合生產系統的帳戶訂閱。

1. 在邊欄上，按一下或點選「工具>作業>雲端>Cloud Services」。
1. 在「Microsoft Translator」區域，按一下或點選「Show Configurations」（顯示配置），然後按一下或點選「Microsoft Translator試用許可證」(Microsoft Translator Translation Configuration)。

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 在設定頁面上，按一下「升級訂閱」。 使用開啟的Microsoft網頁來設定您的帳戶。

   ![chlimage_1-384](assets/chlimage_1-384.png)

### 自定義Microsoft Translator引擎{#customizing-your-microsoft-translator-engine}

「Microsoft翻譯配置」頁提供了指向Microsoft網站的方便連結，用於自定義Microsoft Translator引擎。 ([https://hub.microsofttranslator.com](https://hub.microsofttranslator.com/))

1. 在邊欄上，按一下或點選「工具>作業>雲端>Cloud Services」。
1. 在「Microsoft Translator」區域，按一下或點選「Show Configurations」（顯示配置），然後按一下或點選要自定義的配置。
1. 在配置頁上，按一下「自定義轉換器」。 使用開啟的Microsoft網頁自訂您的服務。

## 激活Translator服務配置{#activating-the-translator-service-configurations}

您需要啟用雲端服務設定，以支援複製至發佈例項的翻譯內容。 使用[激活完整部分（樹）](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree)的方法激活儲存Microsoft Translator或第三方雲服務配置的儲存庫節點。 節點位於以下父節點下：

* Microsoft翻譯服務：/libs/settings/cloudconfigs/translation/msft-translation
* 第三方翻譯：/etc/cloudservices/machine-translation

