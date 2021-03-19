---
title: 6.5中的AEM向後相容性
seo-title: 6.5中的AEM向後相容性
description: 瞭解如何讓您的應用程式和設定與AEM6.5相容
seo-description: 瞭解如何讓您的應用程式和設定與AEM6.5相容
uuid: 81dc2771-f59b-4b24-8932-9e938cba05e0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: f3b4ec1d-9054-47d4-afcb-0a0121b94190
docset: aem65
feature: 升級
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---


# 6.5&lt;a0/AEM>中的向後相容性{#backward-compatibility-in-aem}

## 概覽 {#overview}

>[!NOTE]
>
>有關不在「相容性包」範圍內的內容和配置更改的清單，請參見](/help/sites-deploying/repository-restructuring.md)中的AEM[資源庫重構。

在AEM6.5中，所有功能都已在開發時考慮到向後相容性。

在大多數情況下，執AEM行6.3的客戶在進行升級時，不必變更程式碼或自訂設定。 對AEM6.1和6.2客戶而言，升級至6.3時所面臨的更改並不多。

如果功能無法保持向後相容，則可透過安裝6.4版相容性套件來緩解套件和內容的向後相容問題（請參閱以下如何設定，以取得下載位置的詳細資訊）。 在大多數情況下，此組合套件將有助於恢復符合6.4規範的應AEM用程式的相容性。

Compatibility Package允許您在相容性模AEM式下運行，並根據新功能推遲自定義AEM開發：

>[!NOTE]
>
>請注意，相容性套件只是暫時解決方案，可延遲6.5相容性所需的開發，如果您無法在升級後立即透過開發解決相容性問題，則建議將它當成最後一個選項。 強烈建議在您決定繼續以6.5為基礎的自訂開發並運用完整的6.5功能後，切換至原生模式並解除安裝相容性套件。

![sase](assets/sase.png)

Compatibility Package有兩種模式：**啟用路由**&#x200B;和&#x200B;**禁用路由**。

這可讓AEM6.5以三種模式執行：

**原生模式：**

原生模式適用於想要使用6.5所有新功能的客戶，並準備進行一些開發，讓其自訂功能可搭配所有新功能運作。

這表示在升級後，您可能需要立即對您的應用程式進行調整。

**相容模式：已安裝相容包並啟用了路由**

相容性模式適用於具有向後不相容介面的定製的客戶。 如此可AEM以在相容模式下執行，並針對與您的某些自訂程式碼不相容的AEM新功能，延遲所需的自訂開發。

**舊模式：已安裝相容包且禁用路由**

舊版模式是針對具有自訂介面的客戶，其介面是根據相容性套件中已移AEM出的舊版或淘汰的程式碼。

![sapte](assets/sapte.png)

## 設定方法 {#how-to-set-up}

6.AEM3 Compatibility Package可以使用Package Manager作為軟體包安裝。 您可以從軟體分發&lt;a1/AEM>站點下載[ 6.3 Compatibility Package。](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/compatpack/aem-compat-cq64-to-cq63)

在安裝Compatibility Package後，可以使用OSGI配置中的交換機啟用或禁用路由，如下所示：

![screen_shot_2017-11-27at122421pm](assets/screen_shot_2017-11-27at122421pm.png)

安裝並設定相容性軟體包後，將根據已選擇的相容性模式使用這些功能。
