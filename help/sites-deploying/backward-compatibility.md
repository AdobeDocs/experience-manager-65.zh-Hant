---
title: AEM 6.5的向後相容性
seo-title: Backward Compatibility in AEM 6.5
description: 了解如何讓您的應用程式和設定與AEM 6.5相容
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

# AEM 6.5的向後相容性{#backward-compatibility-in-aem}

## 概觀 {#overview}

>[!NOTE]
>
>有關不在相容性包範圍內的內容和配置更改的清單，請參見 [AEM中的存放庫重新調整](/help/sites-deploying/repository-restructuring.md).

在AEM 6.5中，開發所有功能時都考量回溯相容性。

在大多數情況下，執行AEM 6.3的客戶在執行升級時，不應變更程式碼或自訂。 對於AEM 6.1和6.2客戶，升級至6.3期間不會遇到其他重大變更。

對於無法保持功能向後相容的例外情況，安裝6.4版的相容性套件可緩解套件和內容的向後不相容問題（有關下載位置的詳細資訊，請參閱下面的設定）。 此複合套件在大多數情況下都有助於恢復與AEM 6.4相容的應用程式的相容性。

相容性套件可讓您以相容模式執行AEM，並根據新的AEM功能推遲自訂開發：

>[!NOTE]
>
>請注意，相容性套件僅是暫時性解決方案，可延遲AEM 6.5相容所需的開發，只有在升級後立即透過開發解決相容性問題時，才建議使用此套件作為最後選項。 強烈建議您切換至原生模式，並在您決定繼續進行6.5型自訂開發並使用完整的6.5功能時解除安裝相容性套件。

![sase](assets/sase.png)

相容性包有兩種模式： **已啟用路由** 和 **已禁用路由**.

這可讓AEM 6.5以三種模式執行：

**本機模式：**

原生模式適用於想使用AEM 6.5所有新功能，且已準備好執行一些開發，讓其自訂功能可搭配所有新功能運作的客戶。

這表示升級後，您可能需要立即對應用程式進行調整。

**相容性模式：安裝相容性包並啟用路由**

相容性模式適用於具有自訂介面且無法回溯相容的客戶。 這可讓AEM以相容模式執行，並針對與您某些自訂程式碼不相容的新AEM功能，延後所需的自訂開發。

**舊模式：安裝的相容性包禁用路由**

舊版模式適用於具有自訂介面的客戶，這些介面是根據相容性套件中已移出之AEM的舊版或已棄用的程式碼。

![薩普特](assets/sapte.png)

## 設定方法 {#how-to-set-up}

此 **AEM 6.4適用於6.5的Compatability Pack** 可使用套件管理器以套件形式安裝。 您可以下載 [AEM 6.4 Software Distribution適用的6.5 Compatability Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=compat*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=20&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fcompatpack%2Faem-compat-cq65-to-cq64) 頁簽。

安裝相容性套件後，即可使用OSGI配置中的交換機來啟用或禁用路由，如下所示：

![比較交換機](assets/compat-switches.png)

安裝並設定相容性軟體包後，將根據已選擇的相容性模式使用功能。
