---
title: 升級AEM至6.5
seo-title: 升級AEM至6.5
description: 瞭解將舊版安裝升級至AEMAEM6.5的基本概念。
seo-description: 瞭解將舊版安裝升級至AEMAEM6.5的基本概念。
uuid: 45368056-273c-4f1a-9da6-e7ba5c2bbc0d
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: ebd99cc4-8762-4c28-a177-d62dac276afe
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 4%

---


# 升級AEM至6.5 {#upgrading-to-aem}

在本節中，我們將介紹將安AEM裝升級AEM至6.5:

* [規劃升級](/help/sites-deploying/upgrade-planning.md)
* [用模式檢測器評估升級複雜度](/help/sites-deploying/pattern-detector.md)
* [6.5中的AEM向後相容性](/help/sites-deploying/backward-compatibility.md)

<!--* [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->
* [升級程式](/help/sites-deploying/upgrade-procedure.md)
* [升級程式碼和自訂](/help/sites-deploying/upgrading-code-and-customizations.md)
* [升級前維護任務](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [執行就地升級](/help/sites-deploying/in-place-upgrade.md)
* [升級後檢查和疑難排解](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [可持續升級](/help/sites-deploying/sustainable-upgrades.md)
* [延遲內容移轉](/help/sites-deploying/lazy-content-migration.md)
* [6.5中的AEM儲存庫重組](/help/sites-deploying/repository-restructuring.md)

為了更方便地參AEM考這些程式中的例項，本文中會使用下列詞語：

* *source*&#x200B;實例是您從中升AEM級的實例。
* *target*&#x200B;實例是您要升級到的實例。

>[!NOTE]
>
>作為提高昇級可靠性的努力的一部分，已經進AEM行了全面的儲存庫重組。 有關如何與新結構對齊的詳細資訊，請參見[中的AEM儲存庫重構。](/help/sites-deploying/repository-restructuring.md)

## 有什麼改變？{#what-has-changed}

以下是過去數個版本的注意事項的主要變更AEM:

AEM6.0推出了新的Jackrabbit Oak資料庫。 持久性管理器由[微內核](/help/sites-deploying/platform.md#contentbody_title_4)替換。 從6.1版開始，不再支援CRX2。 需要執行稱為crx2oak的移轉工具，才能從5.6.1例項移轉CRX2儲存庫。 如需詳細資訊，請參閱[使用CRX2OAK移轉工具](/help/sites-deploying/using-crx2oak.md)。

如果要使用Asset Insights，而您正從6.2以AEM前的版本升級，則必須移轉資產，並透過JMX Bean產生ID。 在我們的內部測試中，TarMK環境上的125K資產在一小時內就會移轉，但結果可能會有所不同。

6.3為`SegmentNodeStore`引進了新格式，這是TarMK實施的基礎。 如果從6.3以前的版本進行升級，AEM則需要在升級過程中進行資料庫遷移，涉及系統停機。

Adobe工程公司估計這大約是20分鐘。 請注意，不需要重新建立索引。 此外，新版crx2oak工具已發行，可搭配新的儲存庫格式運作。

**如果從6.3升級至AEM6.5，則不需AEM要此移轉。**

升級前維護工作已最佳化，可支援自動化。

crx2oak工具命令列使用選項已變更為適合自動化的選項，並支援更多升級途徑。

升級後檢查功能也變得易於自動化。

修訂的定期廢棄項目收集和資料儲存廢棄項目收集現在是需要定期執行的例行維護工作。 隨著6.3的推AEM出，Adobe支援並建議「線上修訂清除」。 有關如何配置這些任務的資訊，請參見[修訂清理](/help/sites-deploying/revision-cleanup.md)。

最AEM近推出[Pattern Detector](/help/sites-deploying/pattern-detector.md)，以評估您開始規劃升級時的複雜性。 6.5還強調[功能的向後相容性](/help/sites-deploying/backward-compatibility.md)。 最後，還添加了[可持續升級的最佳做法。](/help/sites-deploying/sustainable-upgrades.md)

如需最新版本中其他變更的詳細資訊，請參AEM閱完整的發行說明：

* [https://helpx.adobe.com/tw/experience-manager/6-2/release-notes.html](https://helpx.adobe.com/tw/experience-manager/6-2/release-notes.html)
* [https://helpx.adobe.com/tw/experience-manager/6-3/release-notes.html](https://helpx.adobe.com/tw/experience-manager/6-3/release-notes.html)
* [https://helpx.adobe.com/tw/experience-manager/6-4/release-notes.html](https://helpx.adobe.com/tw/experience-manager/6-4/release-notes.html)
* [https://helpx.adobe.com/tw/experience-manager/6-5/release-notes.html](https://helpx.adobe.com/tw/experience-manager/6-5/release-notes.html)

## 升級概述{#upgrade-overview}

升級AEM是多步驟、有時是多月的程式。 以下概要概述了升級項目中包含的內容以及本文檔中包含的內容：

![screen_shot_2018-03-30at80708am](assets/screen_shot_2018-03-30at80708am.png)

## 升級流{#upgrade-overview-1}

下圖顯示了建議的整體流程，重點說明了升級方法。 請注意我們所引進新功能的參考。 升級應從模式偵測器開始（請參閱[評估使用模式偵測器的升級複雜度](/help/sites-deploying/pattern-detector.md)），讓您根據產生的報表中的模式，決定要採取與AEM6.4相容的路徑。

在6.5中，我們著重討論如何讓所有新功能都向後相容，但是在您仍然看到某些向後相容性問題時，相容性模式可讓您暫時延遲開發，以維持自訂程式碼與6.5相容。此方法可協助您避免在升級後立即進行開發工作(請參閱AEM6.5](/help/sites-deploying/backward-compatibility.md)中的[向後相容性)。

最後，在6.5開發週期中，「可持續升級」（請參閱[「可持續升級」](/help/sites-deploying/sustainable-upgrades.md)）中引進的功能可協助您遵循最佳實務，讓未來的升級更有效率、更順暢。

![6_4_upgrade_overviewforthbat-newpage3](assets/6_4_upgrade_overviewflowchart-newpage3.png)

