---
title: 連接到Microsoft&reg;翻譯
description: 了解如何將AEM連線至Microsoft&reg;翻譯。
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

# 連接到Microsoft® Translator{#connecting-to-microsoft-translator}

為Microsoft® Translator雲端服務建立設定，以使用您的Microsoft®翻譯帳戶來轉譯AEM頁面內容、社群內容或資產。

| 屬性 | 說明 |
|---|---|
| 翻譯標籤 | 翻譯服務的顯示名稱。 |
| 翻譯歸因 | （選用）針對使用者產生的內容，例如顯示在翻譯文字旁的歸因 `Translations by Microsoft`. |
| 工作區ID | （選用）您要使用的自訂Microsoft®轉譯器引擎ID。 |
| 訂閱金鑰 | 您的Microsoft®Microsoft®翻譯器訂閱密鑰。 |

建立設定後，您必須 [啟動](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations).

下列程式使用觸控最佳化的UI來建立Microsoft® Translator設定。

1. 在導軌上，按一下或點選「工具>Cloud Services」。
1. 在「Microsoft®轉換器」區域中，選擇「顯示配置」。
1. 按一下「可用配置」旁的+連結。

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. 輸入您設定的標題。 標題會在Cloud Services主控台和頁面屬性下拉式清單中識別設定。 預設名稱是以標題為基礎。 （可選）鍵入用於儲存配置的儲存庫節點的名稱。 使用父配置屬性的預設值，該屬性是儲存庫節點的路徑。
1. 按一下建立。
1. 在出現的對話框中，鍵入屬性的值，然後按一下確定。

## 範例Microsoft®轉譯器Cloud Service設定 {#sample-microsoft-translator-cloud-service-configurations}

以下Microsoft® Translator雲服務配置隨Geometrixx示例一起安裝。 某些設定範例使用試用的Microsoft®翻譯帳戶，每月最多可允許2 000 000個免費翻譯字元。

### Microsoft®翻譯試用版 {#microsoft-translator-trial-license}

Microsoft® Translator試用版許可證配置是隨Geometrixx Outdoors示例包一起安裝的示例配置。 此配置使用Microsoft® Translator帳戶，該帳戶具有免費訂閱，每月可允許2 000 000個翻譯字元。

### Microsoft®翻譯試用許可 — Geometrixx — 戶外 {#microsoft-translator-trial-license-geometrixx-outdoors}

Microsoft® Translator試用版授權 — Geometrixx — 戶外配置是隨Geometrixx Outdoors一起安裝的示例配置。 此配置使用與Microsoft® Translator試用許可證配置相同的免費Microsoft® Translator帳戶。 帳戶有免費訂閱，每月可允許2 000 000個翻譯字元。

此Microsoft® Translator配置已優化，以便與Geometrixx Outdoors示例站點的內容類型一起使用。

### 升級Microsoft® Translator試用版許可證配置 {#upgrading-the-microsoft-translator-trial-license-configuration}

Microsoft®翻譯設定頁面提供前往Microsoft®網站的便利連結，以取得適合生產系統的帳戶訂閱。

1. 在導軌上，按一下或點選「工具>作業>雲端>Cloud Services」。
1. 在「 Microsoft® Translator 」區域中，按一下或點選「 Show Configurations 」，然後按一下或點選「 Microsoft® Translator Trial License(Microsoft® Translation Configuration)」。

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 在配置頁面上，按一下升級訂閱。 使用開啟的Microsoft®網頁來設定您的帳戶。

   ![chlimage_1-384](assets/chlimage_1-384.png)

### 自訂您的Microsoft® Translator引擎 {#customizing-your-microsoft-translator-engine}

Microsoft®翻譯設定頁面提供Microsoft®網站的便利連結，可自訂您的Microsoft®翻譯器引擎。 ([https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/](https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/))

1. 在導軌上，按一下或點選「工具>作業>雲端>Cloud Services」。
1. 在「 Microsoft®轉譯器」區域中，按一下或點選「顯示組態」，然後按一下或點選您要自訂的組態。
1. 在配置頁上，按一下「自定義轉換器」。 使用開啟的Microsoft®網頁來自訂您的服務。

## 激活轉換器服務配置 {#activating-the-translator-service-configurations}

若要支援複製到發佈執行個體的翻譯內容，請啟動您的雲端服務設定。 要激活儲存Microsoft® Translator或第三方雲服務配置的儲存庫節點，請使用 [激活完整節（樹）](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree). 節點位於以下父節點下：

* Microsoft®翻譯服務：/libs/settings/cloudconfigs/translation/msft-translation
* 第三方翻譯：/etc/cloudservices/machine-translation
