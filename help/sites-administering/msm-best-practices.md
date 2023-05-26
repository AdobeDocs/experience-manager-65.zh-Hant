---
title: MSM 最佳做法
description: 尋找由Adobe工程和諮詢團隊編譯的最佳實務，以協助啟動並執行AEM多網站管理員。
topic-tags: site-features, best-practices
feature: Multi Site Manager
exl-id: 3fedc1ba-64f5-4fbe-9ee5-9b96b75dda58
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '1616'
ht-degree: 2%

---

# MSM 最佳做法{#msm-best-practices}

## 一般 {#general}

MSM是可設定的架構，用於自動化內容部署。 實作通常涉及網站的主要部分，且橫跨多個組織和地區。 因此，強烈建議您在規劃MSM實作時，如同規劃網站一樣謹慎：

* 小心 **計畫結構和內容流程** 開始實作之前。
* **將即時副本的數量維持在最小。** 處理即時副本是一項耗用大量資源的工作。 您的系統中存在的即時副本越多，會影響效能的程度就越高：從處理內部即時副本索引、透過即時副本作業（例如轉出）到UI作業（例如在「網站管理員參考」邊欄中顯示即時副本關係）。 最佳實務是建立網站或網站分支的即時副本，其中即時副本關係會繼承至網站或分支中的頁面。 當整個結構可成為即時副本時，請避免為網站或分支中的頁面建立個別即時副本。
* **儘可能多地自訂，但越少越好。** 雖然MSM支援高度自訂（例如轉出設定），但網站在效能、可靠性和可升級性方面的最佳作法通常是儘可能減少自訂。
* 建立 **治理** 及早建立模型，並據此訓練使用者，以確保成功。 從治理的角度來看，最佳實務是 **將本機內容製作者擁有的許可權降至最低** 來配置/連線內容給其他本機使用者及其各自的即時副本。 這是因為不受控管、鏈結的繼承會大幅增加MSM結構的複雜性，並損害其效能和可靠性。

* 在針對您的結構、內容流程、自動化和控管制定計畫後 —  **建立原型並徹底測試您的系統**，然後再開始即時實作。
* 請記住 **Adobe諮詢與領先的系統整合業者** 擁有透過MSM規劃和實作內容自動化的豐富經驗，因此他們可以協助您開始使用MSM專案並完成整個實作。

>[!NOTE]
>
>有關使用MSM的更多資訊，請參閱知識庫文章：
>
>* [疑難排解MSM問題和常見問題](troubleshoot-msm.md)
>


>[!NOTE]
>
>您也可以使用 [參照元件](/help/sites-authoring/default-components-foundation.md#reference) 重複使用單一頁面或段落。 但請記住：
>
>* MSM更為靈活，可讓您對同步的內容和時間進行細微控制。
>* [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 現在建議使用，而不使用基礎元件。
>


## 即時副本來源和Blueprint設定 {#live-copy-sources-and-blueprint-configurations}

請記住，可使用以下任一方式建立即時副本 [一般頁面](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) 或 [Blueprint設定](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). 兩者都是有效的使用案例。

使用Blueprint設定的其他優點包括：

* 允許作者使用 **轉出** blueprint上的選項 — 以（明確）推送修改至繼承自此blueprint的即時副本。
* 允許作者使用 **建立網站**；這可讓使用者輕鬆選取語言並設定即時副本的結構。
* 為與Blueprint有關聯的即時副本定義預設轉出設定。

如果未參考Blueprint設定，則轉出只能從即時副本本身啟動，基本上是從來源提取內容。

使用即時副本建立新網站時，建立Blueprint設定以確保完整MSM功能集的可用性是有利的。

>[!NOTE]
>
>請注意，許可權標籤中的CUG無法從Blueprint轉出至即時副本。 請在設定即時副本時對此進行規劃。

## 元件和容器同步 {#components-and-container-synchronization}

一般而言，MSM中有關元件同步的轉出規則是：

* 元件會同步處理Blueprint中包含的任何資源轉出。
* 容器僅同步目前資源。

這表示會將元件視為彙總，在轉出時，元件本身及其所有子項都會取代為Blueprint中的元件。 這表示如果在本機將資源新增至這類元件，轉出時它會遺失至Blueprint的內容。

若要支援巢狀元件，以便在轉出中維護本機新增的元件，必須將元件宣告為容器。 例如，預設parsys會宣告為容器，以便支援本機新增的內容。

>[!NOTE]
>
>新增屬性 `cq:isContainer` 至元件，以將其指定為容器。

## 建立網站 {#create-site}

請注意，AEM有兩個主要方法可建立即時副本：

* 時間 [建立即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   這可視為較通用的方法，可讓您從任何頁面建立即時副本。 即時副本的內容結構與來源完全相符。

* 時間 [建立網站](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

   這是一種更專業的方法，主要用於建立具有多語言結構的網站。

建立網站時，請謹記以下一些考量事項：

* 若要建立新網站，您需要 [Blueprint設定](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations).
* 若要允許選取要在新網站中建立的語言路徑，對應的語言根必須存在於Blueprint （來源）中。
* 一次a [新網站已建立為即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (使用 **建立**，則 **網站**)，此即時副本的前兩個層級為 *淺*. 頁面的子系不屬於即時關係，但如果找到符合觸發器的即時關係，轉出仍會下降。

   這有助於避免：

   * 在Blueprint中手動新增語言（第一個層級以下）
   * 手動將內容直接新增至語言根下，
   * 不會導致在轉出時自動將此新內容傳送至即時副本。

## MSM和多語言網站 {#msm-and-multilingual-websites}

MSM可透過兩種方式協助建立多語言網站：

* 建立語言主版時。

   * 而MSM本身 **不提供內容翻譯**，可與第三方翻譯聯結器整合。 請注意：

      * MSM可讓您在頁面和/或元件層級取消繼承。 這有助於防止在下一次轉出時覆寫已翻譯內容（來自即時副本，以及來自Blueprint的尚未翻譯內容）。
      * 某些協力廠商翻譯聯結器會自動管理MSM繼承。

         如需詳細資訊，請洽詢您的翻譯服務供應商。

      * 建立及翻譯語言母版的另一種方法是將語言副本與AEM現成的翻譯整合架構搭配使用。

* 從語言主版轉出內容時。

   * 例如，從法語主版到國家/地區特定網站，例如法國/法語、加拿大/法語、瑞士/法語。

如需詳細資訊，請參閱 [翻譯多語言網站的內容](/help/sites-administering/translation.md) 和 [翻譯最佳實務](/help/sites-administering/tc-bp.md).

## 結構變更和轉出 {#structure-changes-and-rollouts}

對Blueprint/來源樹狀結構中內容結構的修改會以不同方式反映在即時副本中。 這取決於修改型別：

* **建立** Blueprint中的新頁面將導致在使用標準轉出設定轉出後，在即時副本中建立對應的頁面。

* **正在刪除** 使用標準轉出設定進行轉出後，Blueprint中的頁面將導致對應的頁面從即時副本中刪除。

* **移動** Blueprint中的頁面將 **not** 使用標準轉出設定進行轉出後，會在即時副本中移動對應的頁面：

   * 此行為的原因是頁面移動隱含包含頁面刪除。 這可能會導致發佈時出現非預期的行為，因為刪除作者上的頁面會自動停用發佈上的對應內容。 這也可能對相關專案（例如連結、書籤等）產生連鎖效應。
   * 個別即時副本頁面中的內容繼承會更新，以反映其來源在Blueprint中的新位置。
   * 若要完全實現從Blueprint到即時副本的頁面移動，請考慮以下最佳實務：

>[!NOTE]
>
>這僅適用於 [在轉出觸發時](/help/sites-administering/msm-sync.md#rollout-triggers).

* 建立自訂轉出設定：

   * 此新設定必須包含動作：

      `PageMoveAction`

      請勿將其他動作新增至此設定。

* 定位新設定：

   * 若要完全轉出頁面移動，同時在即時副本中的舊位置刪除個別頁面：

      * 將新建立的設定放置在標準轉出設定之前。

         標準轉出設定會負責刪除舊位置的頁面。
   * 若要轉出頁面移動，同時將個別頁面保留在即時副本中的舊位置（基本上是重複內容）：

      * 將新建立的設定放置在標準轉出設定之後。

         這將確保即時副本中不會刪除內容或從發佈中停用。


## 自訂轉出 {#customizing-rollouts}

MSM轉出設定可高度自訂。 您應注意，自動化轉出可能會產生深遠的影響。 最佳做法是規劃 *非常* 之前請務必小心，例如：

* 自動化轉出；例如，使用 [onModify觸發程式](#onmodify)，
* 自訂 [節點型別/屬性](#node-types-properties)，
* 開始後續工作流程，
* 和/或啟用轉出中的內容。

### onModify {#onmodify}

使用時 [轉出觸發器](/help/sites-administering/msm-sync.md#rollout-triggers) `onModify` 您應考慮：

* 使用自動化轉出 `onModify` 觸發器可能會在觸發轉出後對編寫效能造成負面影響 *每* 頁面修改。

* 轉出結果可能與預期結果不同：

   * 您無法指定產生修改事件的順序。
   * 事件型架構無法保證傳遞至轉出管理器的事件順序。

* 如果同時更新相同的資源，使用這類轉出設定可能會導致認可衝突。

因此，建議您 *僅限* use `onModify` 如果自動轉出啟動的好處多於任何潛在的效能問題，則會觸發。

### 節點型別/屬性 {#node-types-properties}

請記住：

* 除了自訂轉出動作之外，MSM也可讓您自訂正在轉出的節點屬性。 此 [MSM OSGi設定可讓您排除節點型別](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization) 從來源複製到即時副本。

## 更多資訊 {#further-information}

本頁及以下頁面涵蓋相關問題：

* [建立和同步 Live Copy](/help/sites-administering/msm-livecopy.md)
* [Live Copy 概觀主控台](/help/sites-administering/msm-livecopy-overview.md)
* [設定 Live Copy 同步](/help/sites-administering/msm-sync.md)
* [MSM 推出衝突](/help/sites-administering/msm-rollout-conflicts.md)
