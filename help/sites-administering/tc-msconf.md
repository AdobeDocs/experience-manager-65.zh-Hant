---
title: 連接到Microsoft&reg;翻譯
description: 瞭解如何連AEM接到Microsoft&reg;翻譯。
uuid: 5e3916ec-36a0-4d31-94ff-c340a462411a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: a7958411-b509-428e-bbe2-42efe8fd1add
feature: Language Copy
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
source-git-commit: 95638b6dd9527c567b38d8cd9da14633bd4142b5
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 1%

---

# 連接到Microsoft®翻譯器{#connecting-to-microsoft-translator}

為Microsoft®翻譯器雲服務建立配置，以使用Microsoft®翻譯帳戶AEM翻譯頁面內容、社區內容或資產。

| 屬性 | 說明 |
|---|---|
| 翻譯標籤 | 翻譯服務的顯示名稱。 |
| 翻譯歸因 | （可選）對於用戶生成的內容，例如，在已翻譯文本旁邊顯示的屬性 `Translations by Microsoft`。 |
| 工作區ID | （可選）要使用的自定義Microsoft®翻譯器引擎的ID。 |
| 訂閱金鑰 | 您的Microsoft®Microsoft®翻譯器訂閱密鑰。 |

建立配置後，必須 [激活](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations)。

以下過程使用觸控優化的UI建立Microsoft®翻譯器配置。

1. 在滑軌上，按一下或點擊「工具」>「Cloud Services」。
1. 在「Microsoft®翻譯器」區域，選擇「顯示配置」。
1. 按一下「Available Configurations（可用配置）」旁邊的+連結。

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. 鍵入配置的標題。 標題標識Cloud Services控制台和頁屬性下拉清單中的配置。 預設名稱基於標題。 （可選）鍵入用於儲存配置的儲存庫節點的名稱。 使用「父配置」屬性（儲存庫節點的路徑）的預設值。
1. 按一下建立。
1. 在出現的對話框中，鍵入屬性的值，然後按一下「確定」。

## Microsoft®翻譯器Cloud Service配置示例 {#sample-microsoft-translator-cloud-service-configurations}

以下Microsoft®翻譯器雲服務配置隨Geometrixx示例一起安裝。 某些示例配置使用試用版Microsoft®翻譯帳戶，每月最多允許2 000 000個免費翻譯字元。

### Microsoft®翻譯員試用版 {#microsoft-translator-trial-license}

Microsoft®翻譯器試用許可證配置是隨Geometrixx Outdoors示例軟體包一起安裝的示例配置。 此配置使用一個Microsoft®翻譯器帳戶，該帳戶具有允許每月2 000 000個翻譯字元的免費訂閱。

### Microsoft®翻譯員試用許可證 — Geometrixx — 戶外 {#microsoft-translator-trial-license-geometrixx-outdoors}

Microsoft®翻譯器試用許可證 — Geometrixx — 室外配置是隨Geometrixx Outdoors安裝的示例配置。 此配置使用與Microsoft®翻譯器試用許可證配置相同的免費Microsoft®翻譯器帳戶。 該帳戶有免費訂閱，每月允許2 000 000個翻譯字元。

此Microsoft®翻譯器配置已優化，可與Geometrixx Outdoors示例站點的內容類型一起使用。

### 升級Microsoft®翻譯器試用版許可證配置 {#upgrading-the-microsoft-translator-trial-license-configuration}

Microsoft®翻譯配置頁提供指向Microsoft®網站的便捷連結，以獲得適用於生產系統的帳戶訂閱。

1. 在滑軌上，按一下或點擊「工具」>「操作」>「雲」>「Cloud Services」。
1. 在「Microsoft®翻譯器」區域，按一下或點擊「Show Configurations（顯示配置）」 ，然後按一下或點擊「Microsoft®翻譯器試用許可證(Microsoft®翻譯配置)」。

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 在配置頁上，按一下升級訂閱。 使用開啟的Microsoft®網頁配置您的帳戶。

   ![chlimage_1-384](assets/chlimage_1-384.png)

### 自定義您的Microsoft®翻譯器引擎 {#customizing-your-microsoft-translator-engine}

Microsoft®翻譯配置頁提供了到Microsoft®網站的便捷連結，可自定義您的Microsoft®翻譯器引擎。 ([https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/](https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/))

1. 在滑軌上，按一下或點擊「工具」>「操作」>「雲」>「Cloud Services」。
1. 在「Microsoft®翻譯器」區域，按一下或點擊「顯示配置」，然後按一下或點擊要自定義的配置。
1. 在配置頁上，按一下「自定義轉換器」。 使用開啟的Microsoft®網頁自定義您的服務。

## 激活轉換器服務配置 {#activating-the-translator-service-configurations}

要支援複製到發佈實例的已翻譯內容，請激活雲服務配置。 要激活儲存Microsoft®翻譯器或第三方雲服務配置的儲存庫節點，請使用 [激活完整節（樹）](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree)。 節點位於以下父節點下：

* Microsoft®翻譯服務：/libs/settings/cloudconfigs/translation/msft translation
* 第三方翻譯：/etc/cloudservices/機器翻譯
