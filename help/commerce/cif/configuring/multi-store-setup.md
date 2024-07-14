---
title: Commerce多商店設定
description: 瞭解如何將多個商店檢視從Adobe Commerce對應至AEM。 如此一來，專案便可支援多租使用者和多語言使用案例。
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
exl-id: 1d4e9b7b-848b-4007-b884-dd48682d62e8
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 2%

---

# Commerce多商店設定 {#multi-store}

AEM CIF核心元件可用於多個AEM網站結構，而基礎GraphQL使用者端實作可連線至不同的Adobe Commerce存放區/存放區檢視。 如此一來，專案便可實作複雜的多商店/多網站設定。

逐步解說影片，詳述將多個Adobe Commerce商店檢視與Adobe Experience Manager Sites整合的選項。

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

即時副本和語言副本的AEM多網站管理功能可與Commerce integration framework搭配使用，以全域方式管理跨地區和地區的網站。

建議的設定是使用AEM網站與Adobe Commerce商店檢視之間的1:1關係。

若要將AEM網站和AEM CIF核心元件也連線至專用的商店檢視，請遵循下列步驟：

## 設定 {#configuration}

1. 根據[Adobe Commerce網站、商店和檢視](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html)中所述的模式，設定多個商店和商店檢視

2. 請確定AEM與Adobe Commerce之間的連線正常運作。

3. 依照下列步驟建立CIFCloud Service設定的子設定：

   * 在AEM中，移至[工具] > [一般] > [設定瀏覽器] ](/help/sites-administering/configurations.md#using-configuration-browser)[
   * 選取您建立的基本組態
   * 使用上述第2點所述的步驟建立設定

   此新組態會建立為基底組態的子組態。 您現在可以前往「工具>一般>組態瀏覽器」並建立組態設定。

   >[!TIP]
   >
   >Commerce目錄可使用ID或UID來處理。 Adobe Commerce 2.4.2匯入了UID。只有在您的Commerce後端支援2.4.2版或更新版本的GraphQL結構描述時，才會啟用此功能。

4. 將子組態指派至AEM站台

   * 前往AEM Sites主控台
   * 導覽至您網站結構的區域或語言根目錄，例如，/content/venia/us _或_ /content/venia/us/en代表Venia範例頁面
   * 選取頁面並開啟頁面屬性
   * 選取「進階」標籤
   * 在`Configuration`區段中，選取您在步驟中建立的組態

## 其他資源

* [Adobe Commerce網站、商店和檢視](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html)
* [AEM CIF核心元件 — 多存放區/網站組態](https://github.com/adobe/aem-core-cif-components#multi-store--site-configuration)
* [使用多網站管理員](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [重複使用內容：多網站管理員和 Live Copy](/help/sites-administering/msm.md)
