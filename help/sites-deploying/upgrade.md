---
title: 升級AEM到6.5
seo-title: Upgrading to AEM 6.5
description: 瞭解將舊安裝升級到AEMAEM6.5的基本知識。
seo-description: Learn about the basics of upgrading an older AEM installation to AEM 6.5.
contentOwner: sarchiz
topic-tags: upgrading
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: 722d544c-c342-4c1c-80e5-d0a1244f4d36
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 0%

---

# 升級AEM到6.5 {#upgrading-to-aem}

在本節中，我們將介紹將安AEM裝升級AEM到6.5:

* [計畫升級](/help/sites-deploying/upgrade-planning.md)
* [用模式檢測器評估升級複雜度](/help/sites-deploying/pattern-detector.md)
* [6.5中的AEM向後相容性](/help/sites-deploying/backward-compatibility.md)

   <!--* [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->
* [升級過程](/help/sites-deploying/upgrade-procedure.md)
* [升級代碼和自定義](/help/sites-deploying/upgrading-code-and-customizations.md)
* [升級前維護任務](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [執行就地升級](/help/sites-deploying/in-place-upgrade.md)
* [升級後檢查和故障排除](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [永續升級](/help/sites-deploying/sustainable-upgrades.md)
* [懶惰內容遷移](/help/sites-deploying/lazy-content-migration.md)
* [6.5中的AEM儲存庫重組](/help/sites-deploying/repository-restructuring.md)

為了更方便地參AEM考這些程式中涉及的實例，在這些條款中使用了以下術語：

* 的 *源* instance是AEM要升級的實例。
* 的 *目標* 實例是要升級到的實例。

>[!NOTE]
>
>作為提高昇級可靠性努力的一部分，已進AEM行了全面的儲存庫重組。 有關如何與新結構對齊的詳細資訊，請參見 [中的儲存庫重AEM組。](/help/sites-deploying/repository-restructuring.md)

## 什麼變了？ {#what-has-changed}

以下是注釋在最近幾個版本的主要變AEM化：

6AEM.0推出了新的Jackrabbit橡樹資料庫。 持久性管理器已替換為 [微核](/help/sites-deploying/platform.md#contentbody_title_4)。 從6.1版開始，不再支援CRX2。 需要運行名為crx2oak的遷移工具，才能從5.6.1實例遷移CRX2儲存庫。 有關詳細資訊，請參見 [使用CRX2OAK遷移工具](/help/sites-deploying/using-crx2oak.md)。

如果要使用Assets Insights，並且您要從6.2以前的版本升級AEM，則必須遷移資產，並使用通過JMX Bean生成的ID。 在我們的內部test中，TarMK環境中的125K資產在一小時內就遷移了，但結果可能會有所不同。

6.3引入了一種 `SegmentNodeStore`是TarMK實現的基礎。 如果從6.3以前的版本進行升級，AEM則在升級過程中將需要進行儲存庫遷移，這涉及系統停機。

Adobe工程公司估計這大約是20分鐘。 請注意，無需重新編製索引。 此外，還發佈了新的crx2oak工具版本，以使用新的儲存庫格式。

**如果從6.3升級到AEM6.5，則不需AEM要此遷移。**

升級前維護任務已優化以支援自動化。

crx2oak工具命令行使用選項已更改為對自動化友好，並支援更多升級路徑。

升級後的檢查也使自動化變得友好。

修訂的定期垃圾收集和資料儲存垃圾收集現在是需要定期執行的例行維護任務。 隨著6.3的AEM引入，Adobe支援並建議「線上修訂版清除」。 請參閱 [修訂版清除](/help/sites-deploying/revision-cleanup.md) 以獲取有關如何配置這些任務的資訊。

最AEM近介紹 [圖案檢測器](/help/sites-deploying/pattern-detector.md) 以評估升級的複雜性，開始規劃升級。 6.5亦著重於 [向後相容](/help/sites-deploying/backward-compatibility.md) 的子菜單。 最後， [可持續升級](/help/sites-deploying/sustainable-upgrades.md) 的上界。

有關最新版本中其他更改內容的詳細信AEM息，請參閱完整的發行說明：

* [Adobe Experience Manager6.5最新Service Pack發行說明](/help/release-notes/release-notes.md)

## 升級概述 {#upgrade-overview}

升AEM級是一個多步驟、有時是多月的過程。 以下概要概述了升級項目中包括的內容和本文檔中包含的內容：

![screen_shot_2018-03-30at80708am](assets/screen_shot_2018-03-30at80708am.png)

## 升級流 {#upgrade-overview-1}

下圖顯示了總體建議的流程，突出了升級方法。 請注意我們介紹的新功能的參考。 升級應從模式檢測器開始(請參閱 [用模式檢測器評估升級複雜度](/help/sites-deploying/pattern-detector.md))，它應允許您根據生成的報告中的模式AEM確定要與6.4相容的路徑。

在6.5中，重點是要使所有新功能向後相容，但在您仍然看到某些向後相容問題時，相容模式允許您暫時推遲開發，以使自定義代碼與6.5保持相容。此方法可幫助您在升級後立即避免開發工作(請參見 [6.5中的AEM向後相容性](/help/sites-deploying/backward-compatibility.md))。

最後，在您的6.5開發週期中，可持續升級(請參閱： [可持續升級](/help/sites-deploying/sustainable-upgrades.md))幫助您遵循最佳實踐，使未來的升級更加高效和無縫。

![6_4_upgrade_overviewflowchart-newpage3](assets/6_4_upgrade_overviewflowchart-newpage3.png)
