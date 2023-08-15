---
title: AEM 6.5的回溯相容性
seo-title: Backward Compatibility in AEM 6.5
description: 瞭解如何保持應用程式和設定與AEM 6.5相容
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
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# AEM 6.5的回溯相容性{#backward-compatibility-in-aem}

## 概觀 {#overview}

>[!NOTE]
>
>如需不在相容性套件範圍內的內容和設定變更清單，請參閱 [AEM中的存放庫重組](/help/sites-deploying/repository-restructuring.md).

在AEM 6.5中，開發所有功能時都考慮到回溯相容性。

在大多數情況下，執行AEM 6.3的客戶在升級時不必變更程式碼或自訂。 對於AEM 6.1和6.2客戶，升級至6.3期間不會面臨額外的重大變更。

若有例外狀況導致功能無法保持回溯相容，安裝6.4版的相容性套件可緩解套件和內容的回溯不相容問題（請參閱如何設定以取得下載位置的詳細資訊）。 在符合AEM 6.4規範的應用程式的大多數情況下，此相容性套件有助於還原相容性。

相容性套件可讓您以相容性模式執行AEM，並延遲針對新AEM功能的自訂開發：

>[!NOTE]
>
>請注意，相容性套件只是一個暫時性解決方案，可延遲相容於AEM 6.5所需的開發；如果您在升級後無法立即透過開發解決相容性問題，建議使用此套件作為最後選項。 強烈建議您切換到原生模式，並在您決定繼續進行6.5型自訂開發並取得完整的6.5功能後，解除安裝相容性套件。

![Sase](assets/sase.png)

相容性套件有兩種模式： **已啟用路由** 和 **已停用路由**.

如此可讓AEM 6.5以三種模式執行：

**原生模式：**

原生模式適用於想要使用AEM 6.5的所有新功能，並準備好進行一些開發以使其自訂功能與所有新功能的客戶。

這表示在升級後，您可能需要立即在應用程式中進行調整。

**相容性模式：相容性套件已安裝並啟用路由**

「相容性模式」適用於自訂介面的客戶，這些介面無法向下相容。 這可讓AEM在相容模式下執行，並延遲針對與某些自訂程式碼不相容的新AEM功能所需的自訂開發。

**舊版模式：安裝相容性套件，但已停用路由**

舊版模式適用於擁有自訂介面的客戶，這些介面是根據已移出相容性套件的AEM舊版或已棄用程式碼。

![格式](assets/sapte.png)

## 設定方法 {#how-to-set-up}

此 **AEM 6.4 Compatability Pack for 6.5** 可使用封裝管理員以封裝形式安裝。 您可以下載 [Software Distribution提供的6.5 AEM 6.4 Compatability Pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=compat*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=20&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fcompatpack%2Faem-compat-cq65-to-cq64) 網站。

安裝相容性套件後，即可使用OSGI組態中的交換器來啟用或停用路由，如下所示：

![電腦開關](assets/compat-switches.png)

安裝及設定相容性套件後，將根據所選的相容性模式使用功能。
