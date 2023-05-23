---
title: Commerce多商店設定
description: 瞭解如何將多個商店視圖從Adobe Commerce映射到AEM。 這允許項目支援多租戶和多語言使用案例。
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 3046
thumbnail: 28952.jpg
exl-id: 1d4e9b7b-848b-4007-b884-dd48682d62e8
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 2%

---

# Commerce多商店設定 {#multi-store}

CIF核AEM心元件可用於多個站點結AEM構，而基礎的GraphQL客戶端實現可連接到不同的Adobe Commerce商店/商店視圖。 這允許項目實施複雜的多儲存/多站點設定。

一個視頻漫遊，詳細介紹了將多個Adobe Commerce商店視圖與Adobe Experience Manager Sites整合的選項。

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

Live Copy和AEM Language Copy的多站點管理功能與Commerce Integration Framework結合使用，以全局管理跨區域和區域設定的站點。

建議的設定是使用站點和Adobe Commerce商店AEM視圖之間的1:1關係。

要將站點AEM和AEMCIF核心元件連接到專用商店視圖，請執行以下步驟：

## 設定 {#configuration}

1. 根據中所述的模式配置多個儲存和儲存視圖 [Adobe Commerce網站、商店和視圖](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)

2. 確保與Adobe Commerce之AEM間的連接正在工作。

3. 按照以下步驟建立CIFCloud Service配置的子配置：

   * 轉AEM到工具 — >常規 — > [配置瀏覽器](/help/sites-administering/configurations.md#using-configuration-browser)
   * 選擇您建立的基本配置
   * 使用上面第2點所述的步驟建立新配置

   此新配置將作為基本配置的子配置建立。 現在，您可以轉到「工具」 — >「常規」 — >「配置瀏覽器」並建立配置設定。

   >[!TIP]
   >
   >商業目錄可以使用ID或UID來定址。 UID在Adobe Commerce2.4.2。僅當您的商業後端支援2.4.2版或更高版本的GraphQL架構時才啟用此功能。

4. 將子配置分配給站AEM點

   * 轉到AEM Sites控制台
   * 導航到站點結構的區域或語言根，例如/content/venia/us _或_ /content/venia/us/en（用於Venia示例頁）
   * 選擇頁面並開啟頁面屬性
   * 選擇「高級」頁籤
   * 在 `Configuration` 部分選擇在步驟中建立的配置

## 其他資源

* [Adobe Commerce網站、商店和視圖](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)
* [CIFAEM核心元件 — 多儲存/站點配置](https://github.com/adobe/aem-core-cif-components/wiki/configuration#multi-store--site-configuration)
* [使用多站點管理器](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [重複使用內容：多網站管理員和 Live Copy](/help/sites-administering/msm.md)
