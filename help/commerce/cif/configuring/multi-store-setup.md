---
title: 商務多商店設定
description: 瞭解如何將多個商店檢視從Magento對應至AEM。 這可讓專案支援多租用戶和多語言使用案例。
sub-product: 商務
doc-type: technical-video
activity: setup
audience: administrator
feature: 商務整合框架
kt: 3046
thumbnail: 28952.jpg
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 1%

---

# 商務多商店設定{#multi-store}

CIF核心AEM元件可用於多個站點結AEM構，基礎GraphQL客戶端實現可以連接到不同的Magento儲存／儲存視圖。 這可讓專案建置複雜的多商店／多網站設定。

視訊逐步說明整合多種Magento商店檢視與Adobe Experience Manager Sites的選項。

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

Live Copy和AEM Language Copy的多網站管理功能與Commerce Integration Framework搭配使用，以跨地區和地區全面管理網站。

建議的設定是在網站與Magento商店檢視之間使AEM用1:1關係。

要將站點AEM和AEMCIF核心元件連接到專用的商店視圖，請執行以下步驟：

## 設定 {#configuration}

1. 根據[Magento網站、商店與檢視](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)中所述的模式，設定多個商店與商店檢視

2. 請確定與Magento之AEM間的連接正常工作。

3. 按照以下步驟建立CIFCloud Service配置的子配置：

   * 轉AEM至「工具」->「常規」->「配置瀏覽器」](/help/sites-administering/configurations.md#using-configuration-browser)[
   * 選擇您建立的基本配置
   * 使用上述第2點所述的步驟建立新組態

   此新配置將建立為基本配置的子配置。 您現在可以前往「工具」->「一般」->「設定瀏覽器」並建立設定設定。

   >[!TIP]
   >
   > 商務型錄可透過使用ID或UID來解決。 UID在2.4.2Magento中引入。只有在您的商務後端支援2.4.2版或更新版本的GraphQL架構時，才能啟用此功能。

4. 將子配置分配給站AEM點

   * 前往AEM Sites主控台
   * 導覽至網站結構的地區或語言根目錄，例如/content/venia/us _或_ /content/venia/us/en，以取得Venia範例頁面
   * 選擇頁面並開啟頁面屬性
   * 選擇「高級」頁籤
   * 在`Configuration`部分中，選擇您在步驟中建立的配置

## 其他資源

* [Magento網站、商店和檢視](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)
* [AEM CIF核心元件——多商店／站點配置](https://github.com/adobe/aem-core-cif-components/wiki/configuration#multi-store--site-configuration)
* [使用多網站管理員](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [重複使用內容：多網站管理員和即時副本](/help/sites-administering/msm.md)
