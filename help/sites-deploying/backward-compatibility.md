---
title: 6.5中的AEM向後相容性
seo-title: Backward Compatibility in AEM 6.5
description: 瞭解如何使您的應用和配置與AEM6.5相容
seo-description: Learn how to keep your apps and configurations compatible with AEM 6.5
uuid: 81dc2771-f59b-4b24-8932-9e938cba05e0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: f3b4ec1d-9054-47d4-afcb-0a0121b94190
docset: aem65
feature: Upgrading
exl-id: c432a014-2dab-4c49-a25b-e4f461d13f9b
source-git-commit: 50a11e30ccd720065962e8dd03cbcc71ec9f715a
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---

# 6.5中的AEM向後相容性{#backward-compatibility-in-aem}

## 概觀 {#overview}

>[!NOTE]
>
>有關不在相容性包範圍內的內容和配置更改的清單，請參見 [中的儲存庫重AEM組](/help/sites-deploying/repository-restructuring.md)。

在AEM6.5中，所有功能都是在考慮到向後相容性的基礎上開發的。

在大多數情況下，AEM運行6.3的客戶在進行升級時不必更改代碼或自定義。 對於AEM6.1和6.2客戶，沒有比升級到6.3時面臨的更多突破性更改。

對於無法使功能向後相容的異常，可以通過安裝6.4版相容性包來緩解捆綁包和內容的向後不相容問題（有關下載位置的詳細資訊，請參閱下面的設定）。 在大多數情況下，此相容軟體包將幫助恢復符合6.4AEM的應用程式的相容性。

相容性包允許您在相容AEM性模式下運行，並根據新功能推遲自AEM定義開發：

>[!NOTE]
>
>請注意，相容性軟體包只是一個臨時解決方案，可推遲相容AEM6.5所需的開發，建議只有在升級後無法立即通過開發解決相容性問題時才將其作為最後一個選項。 強烈建議在您決定繼續基於6.5的自定義開發並使用完整的6.5功能後，切換到本機模式並卸載相容性軟體包。

![酶](assets/sase.png)

相容性包有兩種模式： **已啟用路由** 和 **路由已禁用**。

這允AEM許6.5以三種模式運行：

**本機模式：**

本機模式適用於希望使用AEM6.5的所有新功能並準備進行一些開發以使其定制適用於所有新功能的客戶。

這意味著您可能需要在升級後立即對應用程式進行調整。

**相容模式：已安裝並啟用了路由的相容性包**

相容性模式適用於具有向後不相容介面的自定義的客戶。 這允許AEM在相容模式下運行，並針對與某些自定義代碼不相容AEM的新功能推遲所需的自定義開發。

**舊模式：安裝相容性包且已禁用路由**

舊模式適用於具有基於相容性包中已移出的舊代碼或AEM不建議使用的代碼的自定義介面的客戶。

![抽空](assets/sapte.png)

## 設定方法 {#how-to-set-up}

的 **6AEM.4適用於6.5的相容性包** 可以使用包管理器作為包安裝。 您可以下載 [6AEM.4軟體分發中6.5的相容性包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=compat*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=20&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fcompatpack%2Faem-compat-cq65-to-cq64) 的子菜單。

安裝相容性軟體包後，可以使用OSGI配置中的交換機啟用或禁用路由，如下所示：

![複合交換機](assets/compat-switches.png)

安裝和設定相容性軟體包後，將根據已選擇的相容模式使用這些功能。
