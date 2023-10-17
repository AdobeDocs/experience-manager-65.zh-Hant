---
title: 正在連線到Microsoft&Reg； Translator
description: 瞭解如何將Adobe Experience Manager連結至Microsoft&reg； Translator。
contentOwner: Guillaume Carlino
feature: Language Copy
exl-id: ca575a30-fc3e-4f38-9aa7-dbecbc089f87
source-git-commit: eaffc71c23c18d26ec5cbb2bbb7524790c4826fe
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 1%

---

# 正在連線到Microsoft® Translator{#connecting-to-microsoft-translator}

建立Microsoft® Translator雲端服務的設定，以使用您的Microsoft® Translation帳戶來翻譯AEM頁面內容、社群內容或資產。

| 屬性 | 說明 |
|---|---|
| 翻譯標籤 | 翻譯服務的顯示名稱。 |
| 翻譯歸因 | （選用）對於使用者產生的內容，為已翻譯文字旁邊顯示的屬性，例如 `Translations by Microsoft`. |
| 工作區ID | （選用）要使用的自訂Microsoft® Translator引擎ID。 |
| 訂閱金鑰 | 您的Microsoft® Translator Microsoft®訂閱金鑰。 |

建立設定後，您必須 [啟用它](/help/sites-administering/tc-msconf.md#activating-the-translator-service-configurations).

下列程式使用觸控最佳化UI來建立Microsoft® Translator設定。

1. 在邊欄上，按一下或點選「工具>Cloud Service」。
1. 在Microsoft® Translator區域中，選取「顯示組態」。
1. 按一下「可用設定」旁的+連結。

   ![chlimage_1-382](assets/chlimage_1-382.png)

1. 輸入設定的標題。 標題可識別Cloud Service控制檯和頁面屬性下拉式清單中的設定。 預設名稱是根據標題。 選擇性地輸入儲存組態之儲存庫節點的名稱。 使用存放庫節點路徑的Parent Configuration屬性的預設值。
1. 按一下「建立」。
1. 在出現的對話方塊中，輸入屬性的值，然後按一下「確定」。

## Microsoft® TranslatorCloud Service設定範例 {#sample-microsoft-translator-cloud-service-configurations}

下列Microsoft® Translator雲端服務設定會與Geometrixx範例一起安裝。 有些設定範例使用試用的Microsoft®翻譯帳戶，每月最多允許200萬個免費翻譯的字元。

### Microsoft® Translator試用授權 {#microsoft-translator-trial-license}

Microsoft® Translator試用版授權設定是隨Geometrixx Outdoors範例套件一起安裝的範例設定。 此設定使用Microsoft® Translator帳戶，該帳戶具有每月允許2,000,000個已翻譯字元的免費訂閱。

### Microsoft® Translator試用版授權 — Geometrixx-outdoors {#microsoft-translator-trial-license-geometrixx-outdoors}

Microsoft® Translator試用版授權 — Geometrixx-outdoors設定是隨Geometrixx Outdoors一起安裝的設定範例。 此設定使用與Microsoft® Translator試用授權設定相同的免費Microsoft® Translator帳戶。 此帳戶提供免費訂閱，每月可允許2,000,000個已翻譯字元。

此Microsoft® Translator設定已針對與Geometrixx Outdoors範例網站的內容型別搭配使用而最佳化。

### 升級Microsoft® Translator試用授權設定 {#upgrading-the-microsoft-translator-trial-license-configuration}

Microsoft®翻譯設定頁面提供指向Microsoft®網站的便利連結，以取得足以用於生產系統的帳戶訂閱。

1. 在導軌上，按一下或點選「工具>作業>雲端>Cloud Service」。
1. 在Microsoft® Translator區域中，按一下或點選「顯示設定」，然後按一下或點選「Microsoft® Translator試用版授權(Microsoft® Translation Configuration)」。

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. 在設定頁面上，按一下升級訂閱。 使用開啟的Microsoft®網頁來設定您的帳戶。

   ![chlimage_1-384](assets/chlimage_1-384.png)

### 自訂Microsoft® Translator引擎 {#customizing-your-microsoft-translator-engine}

Microsoft®翻譯設定頁面提供指向Microsoft®網站的便利連結，以便自訂Microsoft® Translator引擎。 ([https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/](https://www.microsoft.com/en-us/research/project/microsoft-translator-hub/))

1. 在導軌上，按一下或點選「工具>作業>雲端>Cloud Service」。
1. 在Microsoft® Translator區域中，按一下或點選「顯示設定」，然後按一下或點選您要自訂的設定。
1. 在設定頁面上，按一下「自訂Translator」。 使用開啟的Microsoft®網頁來自訂您的服務。

## 啟用Translator服務設定 {#activating-the-translator-service-configurations}

若要支援復寫至發佈執行個體的翻譯內容，請啟用您的雲端服務設定。 若要啟用儲存Microsoft® Translator或協力廠商雲端服務設定的存放庫節點，請使用以下方法 [啟動完整截面（樹狀結構）](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree). 這些節點位於下列父節點的下方：

* Microsoft®翻譯服務： /libs/settings/cloudconfigs/translation/msft-translation
* 協力廠商翻譯： /etc/cloudservices/machine-translation
