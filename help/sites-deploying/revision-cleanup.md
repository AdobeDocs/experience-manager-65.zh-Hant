---
title: 修訂清除
seo-title: Revision Cleanup
description: 瞭解如何在6.5中使用修訂版清AEM除功能。
seo-description: Learn how to use the Revision Cleanup functionality in AEM 6.5.
uuid: 321f5038-44b0-4f1e-a1aa-2d29074eed70
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: f03ebe60-88c0-4fc0-969f-949490a8e768
feature: Configuring
exl-id: e53c4c81-f62e-4b6d-929a-6649c8ced23c
source-git-commit: 24a64e603d460c659467c7679934bbdfd381aaa8
workflow-type: tm+mt
source-wordcount: '5903'
ht-degree: 0%

---

# 修訂清除{#revision-cleanup}

## 簡介 {#introduction}

每個對儲存庫的更新都建立一個新的內容修訂版本。 因此，每次更新後，儲存庫的大小都會增大。 舊版本需要清理，以釋放磁碟資源 — 這對於避免不受控制的儲存庫增長非常重要。 此維護功能稱為修訂版清除。 自6.0以來，它已作為脫AEM機常式可用。

在6AEM.3和更高版本中，引入了名為「線上修訂版清除」的線上版本。 與必須關閉實例的脫AEM機修訂版清理相比，在實例聯機時可以運AEM行聯機修訂版清理。 預設情況下，聯機修訂版清除已開啟，這是執行修訂版清除的推薦方式。

**注釋**: [查看視頻](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/revision-cleanup-technical-video-use.html) 以及如何使用「聯機修訂清除」。

修訂版清理過程包括三個階段： **估計**。 **壓實** 和 **清理**。 估計根據可能收集的垃圾量確定是否運行下一階段（壓縮）。 在壓縮階段段和tar檔案被重寫，而沒有任何未使用的內容。 清理階段隨後將舊段移除，包括它們可能包含的任何垃圾。 離線模式通常可以回收更多空間，因為聯機模式需要考慮工作AEM集，而工作集會保留不收集更多段。

有關修訂版清理的詳細資訊，請參閱以下連結：

* [如何運行聯機修訂版清除](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup)
* [線上修訂版清理常見問題](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions)
* [如何運行離線修訂版清除](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup)

此外，您還可以 [橡樹官方檔案。](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html)

### 何時使用「聯機修訂版清除」(Online Revision Cleanup)而不是「離線修訂版清除」(Offline Revision Cleanup)? {#when-to-use-online-revision-cleanup-as-opposed-to-offline-revision-cleanup}

**Online Revision Cleanup是執行修訂版清除的推薦方法。** 離線修訂版清理應僅在例外情況下使用 — 例如，在遷移到新儲存格式之前，或者如果Adobe客戶服務部門要求您這樣做的話。

## 如何運行聯機修訂版清除 {#how-to-run-online-revision-cleanup}

預設情況下，聯機修訂版清除配置為在AEM作者和發佈實例上每天自動運行一次。 您只需在用戶活動最少的期間內定義維護窗口即可。 您可以按如下方式配置「線上修訂版清除」任務：

1. 在主窗AEM口中，轉到 **工具 — 操作 — 儀表板 — 維護** 或將瀏覽器指向： `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. 懸停於 **每日維護窗口** 並按一下 **設定** 表徵圖

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. 輸入所需值（重複、開始時間、結束時間），然後按一下 **保存**。

   ![chlimage_1-92](assets/chlimage_1-92.png)

或者，如果要手動運行修訂版清除任務，可以：

1. 轉到 **工具 — 操作 — 儀表板 — 維護** 或直接瀏覽 `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`
1. 按一下 **每日維護窗口**。
1. 懸停在 **修訂版清除** 表徵圖
1. 按一下 **運行**。

   ![chlimage_1-93](assets/chlimage_1-93.png)

### 離線修訂版清除後運行聯機修訂版清除 {#running-online-revision-cleanup-after-offline-revision-cleanup}

修訂版清除過程按代重新收集舊修訂版。 這意味著每次運行修訂版清理時，都會在磁碟上建立並保留新一代。 但是，兩種版本清理類型之間存在差異：離線修訂版清理保留一代，而聯機修訂版清理保留兩代。 所以，當您運行線上修訂版清理 **後** 離線修訂版清除發生以下情況：

1. 在第一次聯機修訂版清除後，系統資訊庫的大小將翻倍。 這是因為現在有兩代儲存在磁碟上。
1. 在後續運行中，儲存庫將在建立新一代時臨時增長，然後穩定到第一次運行後的大小，因為線上修訂版清除過程將重新收集上一代。

另外，請記住，根據提交的類型和數量，每代的大小都可能與前一代不同，因此最終大小可能因一次運行而異。

因此，建議將磁碟的大小至少比最初估計的儲存庫大小大兩三倍。

## 全和尾擊實模式  {#full-and-tail-compaction-modes}

**AEM 6.5** 介紹 **兩種新模式** 為 **壓實** 聯機修訂清除過程的階段：

* 的 **全壓實** 模式將重寫整個儲存庫中的所有資料段和tar檔案。 因此，後續的清理階段可以刪除整個儲存庫的最大垃圾量。 由於完全壓縮會影響整個儲存庫，因此需要大量系統資源和時間來完成。 完全壓實與6.3的壓實相AEM對應。
* 的 **尾部壓實** 模式只重寫儲存庫中最近的段和tar檔案。 最近添加的段和tar檔案是自上次完全壓縮或尾部壓縮運行以來添加的段和tar檔案。 因此，後續的清理階段只能刪除儲存庫最近部分中包含的垃圾。 由於尾部壓縮只影響儲存庫的一部分，因此與完全壓縮相比，完成此操作所需的系統資源和時間要少得多。

這些壓縮模式構成了效率與資源消耗之間的權衡：尾部壓實效果較差，對系統正常運行影響較小。 而完全壓實則效果更好，但對系統正常運行影響更大。

AEM 6.5還引入了壓縮期間更高效的內容重複資料消除機制，這進一步減少了儲存庫的磁碟空間佔用。

下面兩張圖表顯示了內部實驗室測試的結果，這些測試表明與6.3相比，平均執行時間和磁碟AEM佔用空間平AEM均減少6.5:

![onrc持續時間–6_4vs63](assets/onrc-duration-6_4vs63.png) ![segmentstore-6_4vs63](assets/segmentstore-6_4vs63.png)

### 如何配置完整和尾部壓縮 {#how-to-configure-full-and-tail-compaction}

預設配置在周天運行尾部壓縮，在週日運行完全壓縮。 可以使用新配置值更改預設配置 `full.gc.days` 的 `RevisionCleanupTask` [維護任務](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup)。

配置 `full.gc.days` 請注意，完全壓縮將在值中定義的日期運行，而尾部壓縮將在未在值中定義的日期運行。 例如，如果將完全壓縮配置為在星期日運行，則尾部壓縮將在星期一到星期六運行。 例如，如果將完全壓縮配置為每週的每天運行，則完全壓縮將不運行。

另外，考慮到：

* **尾部壓實** 效率低，對正常系統操作影響小。 因此，計畫於營業日期間營運。
* **完全壓縮** 效果更好，但對正常系統運行影響更大。 因此，該筆款項擬於非營業日使用。
* 尾部壓縮和完全壓縮應安排在非高峰時段運行。

### 疑難排解 {#troubleshooting}

使用新壓縮模式時，請記住以下內容：

* 您可以監視輸入/輸出(I/O)活動，例如：I/O操作、等待IO的CPU、提交隊列大小。 這有助於確定系統是否正在綁定I/O，並且需要升級。
* 的 `RevisionCleanupTaskHealthCheck` 指示「Online Revision Cleanup（聯機修訂清除）」的整體運行狀況。 與6.3相同，AEM不區分全壓實和尾壓實。
* 日誌消息傳送有關壓縮模式的相關資訊。 例如，當「聯機修訂清除」啟動時，相應的日誌消息將指示壓縮模式。 此外，在某些拐角情況下，當計畫運行尾部壓縮時，系統將恢復為完全壓縮，而日誌消息將指示此更改。 測井樣品下表顯示壓實模式和從尾部到完全壓實的變化：

```
TarMK GC: running tail compaction
TarMK GC: no base state available, running full compaction instead
```

### 已知限制 {#known-limitations}

在某些情況下，尾部和完全壓縮模式之間的交替延遲了清理過程。 更準確地說，儲存庫在完整壓縮後將增長（其大小將翻倍）。 在後續的尾部壓縮中將回收額外空間，此時儲存庫將降至低於預完全壓縮大小。 應避免並行維護任務執行。

**建議將磁碟的大小至少比最初估計的儲存庫大小大兩三倍。**

## 線上修訂版清理常見問題 {#online-revision-cleanup-frequently-asked-questions}

### AEM 6.5升級注意事項 {#aem-upgrade-considerations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td>問題 </td>
   <td>答案</td>
  </tr>
  <tr>
   <td>升級到6.5時，我應AEM該知道什麼？</td>
   <td><p>TarMK的持久性格式將隨AEM6.5而改變。這些更改不需要主動遷移步驟。 現有儲存庫將經歷滾動遷移，這對用戶是透明的。 遷移過程在首次訪問存AEM儲庫6.5（或相關工具）時啟動。</p> <p><strong>一旦啟動到AEM6.5持久性格式的遷移，儲存庫將無法恢復為以前的AEM6.3持久性格式。</strong></p> </td>
  </tr>
 </tbody>
</table>

### 遷移到Oak Segment Tar {#migrating-to-oak-segment-tar}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>答案</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>為什麼需要遷移儲存庫？</strong></td>
   <td><p>在6AEM.3中，需要更改儲存格式，尤其是為了提高線上修訂版清理的效能和效果。 這些更改不向後相容，必須使用舊Oak Segment(AEM6.2和以前版本)建立的儲存庫必須遷移。</p> <p>更改儲存格式的其他好處：</p>
    <ul>
     <li>更好的可擴充性（優化的段大小）。</li>
     <li>更快 <a href="/help/sites-administering/data-store-garbage-collection.md" target="_blank">資料儲存垃圾收集</a>。<br /> </li>
     <li>地面工作，以便今後加強。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>是否仍支援以前的Tar格式？</strong></td>
   <td>只有新的Oak Segment Tar受6.AEM3或更高版本支援。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>內容遷移是否始終是強制的？</strong></td>
   <td>可以。除非您從新實例開始，否則您將始終必須遷移內容。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>我能否升級到6.3或更高版本並稍後進行遷移（例如，使用另一個維護窗口）?</strong></td>
   <td>否，如上所述，內容遷移是強制的。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>遷移時是否可避免停機？</strong></td>
   <td>否. 這是一次性工作，無法對正在運行的實例執行。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果無意中針對錯誤的儲存庫格式運行，會發生什麼情況？</strong></td>
   <td>如果您嘗試針對Oak-segment-tar儲存庫運行Oak-segment模組（反之亦然），啟動將失敗， <em>IllegalStateException</em> 消息為「無效段格式」。 不會發生資料損壞。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>是否需要重新索引搜索索引？</strong></td>
   <td>否. 從橡木段向橡木段焦油的遷移會導致容器格式的改變。 所包含的資料不受影響，不會被修改。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何最好地計算遷移期間和遷移後所需的預期磁碟空間？</strong></td>
   <td>遷移相當於以新格式重新建立段儲存。 這可用於估計遷移期間所需的額外磁碟空間。 遷移後，可刪除舊段儲存以回收空間。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何最好地估計遷移的持續時間？</strong></td>
   <td>如果能夠 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup">離線修訂清理</a> 在遷移之前執行。 建議所有客戶將其作為升級過程的先決條件執行。 通常，遷移的持續時間應與離線修訂版清除任務的持續時間類似，前提是在遷移之前已執行離線修訂版清除任務。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 運行聯機修訂版清除 {#running-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>答案</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>應執行「Online Revision Cleanup（聯機修訂清除）」的頻率是多少？</strong></td>
   <td>一天一次. 這是「操作儀表板」中的預設配置。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何配置聯機修訂清除維護任務的開始時間？</strong></td>
   <td>查看 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">如何運行聯機修訂版清除</a> 的子菜單。 </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>線上修訂版清除是否有不應超過的最大頻率？</strong></td>
   <td>建議按預設配置每天運行一次線上修訂版清除。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>哪些關鍵指示燈決定了聯機修訂清除的運行頻率？</strong></td>
   <td>無需確定「Online Revision Cleanup（聯機修訂版清除）」配置為維護任務的頻率，並且它每天都會自動運行。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>為什麼首次運行時，聯機修訂版清理不會回收任何空間？</strong></td>
   <td>線上修訂清除按代回收舊修訂。 每次運行修訂版清理時，都會生成新的層代。 只有至少兩代的內容才會被回收，這意味著在第一次運行中，沒有可回收的內容。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>為什麼第一個聯機修訂版清除在離線修訂版清除後運行時不會回收任何空間？</strong></td>
   <td><p>離線修訂版清除正在回收除最新一代之外的所有內容，而最近兩代用於線上修訂版清除。 對於新的儲存庫，在離線修訂版清除後首次執行聯機修訂版清除時，不會回收任何空間，因為沒有足夠舊的代可以回收。</p> <p>此外，請閱讀的「離線修訂版清除後運行線上修訂版清除」部分 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">本章</a>。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>「作者」和「發佈」通常是否具有不同的「線上修訂版清除」窗口？</strong></td>
   <td>這取決於辦公時間和客戶線上狀態的流量模式。 維護窗口應配置在主生產時間之外，以便獲得最佳的清理效果。 對於多個AEM發佈實例（TarMK場），應交錯顯示聯機修訂版清除的維護窗口。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>運行聯機修訂版清除之前是否有任何先決條件？</strong></td>
   <td><p>聯機版本清理僅在6.AEM3和更高版本中可用。 此外，如果您使用的是舊版本，AEM則需要遷移到新版本 <a href="/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar">橡樹木塔</a>。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>決定線上修訂版清除持續時間的因素有哪些？</strong></td>
   <td>這些因素包括：<br />
    <ul>
     <li>儲存庫大小</li>
     <li>在系統上載入（請求每分鐘，特別是寫操作）</li>
     <li>活動模式（讀取與寫入）</li>
     <li>硬體規格（CPU效能、記憶體、IOPS）</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>在聯機修訂版清理運行時，作者是否仍能工作？</strong></td>
   <td>是的，線上修訂版清除可以處理併發寫入。 但是，線上修訂版清除工作速度更快，效率更高，而無需併發寫入事務。 建議將「線上修訂清除」維護任務安排到相對安靜的時間，而不需要大量流量。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>運行聯機修訂清除時對磁碟空間和堆記憶體的最低要求是什麼？</strong></td>
   <td><p>在「Online Revision Cleanup（聯機修訂版清除）」期間，會持續監視磁碟空間。 如果可用磁碟空間降至關鍵值以下，將取消該進程。 關鍵值是儲存庫當前磁碟佔用量的25%，且無法配置。</p> <p><strong>建議將磁碟的大小至少比最初估計的儲存庫大小大兩三倍。</strong></p> <p>清除過程中會持續監視空閒堆空間。 如果可用堆空間降低到臨界值以下，則取消進程。 關鍵值是通過org.apache.jackrabbit.oak.segment.SegmentNodeStoreService#MEMORY_THRESHOLD配置的。 預設值為15%。</p> <p>Recommendations對於最小壓縮堆大小調整的建議與記憶體大小AEM調整建議不分開。 一般規則是： <strong>如果實例AEM的大小足夠大，足以處理使用情形和其上的預期負載，則清除過程將獲得足夠的記憶體。</strong></p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>運行線上修訂版清除時預期的效能影響是什麼？</strong></td>
   <td>聯機修訂清除是從儲存庫並行讀取和寫入到正常系統操作的後台進程。 特別是，它可能需要在很短的時間內獲得對儲存庫的獨佔訪問權限，從而防止其他線程寫入儲存庫。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>預期聯機修訂版清理將運行多久？</strong></td>
   <td>根據我們內部執行的最新效能test，執行該操作不應超過2小時。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果「線上修訂清除」需要更長時間，應該做什麼？</strong></td>
   <td>
    <ul>
     <li>確保每天執行。<br /> </li>
     <li>通過相應地在Operations Dashboard中配置維護窗口，確保在最少的儲存庫活動期間執行該操作。</li>
     <li>擴展系統資源（CPU、記憶體、I/O）。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果「線上修訂版清除」超出了配置的維護窗口，會發生什麼情況？</strong></td>
   <td>確保其他維護任務不會延遲其執行。 如果在同一維護窗口內執行的維護任務比聯機修訂清除要多，則可能會出現這種情況。 請注意，維護任務是按順序執行的，而不是可配置的訂單。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>為什麼跳過修訂垃圾收集？</strong></td>
   <td><p>修訂版清理依賴於評估階段來確定是否有足夠的垃圾要清理。 估計器將當前大小與上次壓縮後的儲存庫大小進行比較。 如果大小超出配置的增量，將運行清理。 大小增量設定為1 GB。 這實際上意味著，如果自上次清除運行以來儲存庫大小未增長1 GB，則將跳過新修訂版清除迭代。 </p> <p>以下是估計階段的相關日誌條目：</p>
    <ul>
     <li>版本GC將運行： <em>大小增量為N%或N/N（N/N位元組），因此運行壓縮</em></li>
     <li>修訂版GC將 <strong>不</strong> 運行： <em>大小增量為N%或N/N（N/N位元組），因此暫時跳過壓縮</em></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果效能影響太大，是否可以安全地中止自動壓縮？</strong></td>
   <td>可以。自AEM6.3起，可通過操作控制面板中的維護任務窗口或通過JMX安全停止。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果實AEM例在計劃清理任務期間關閉，進程是否安全中止，或者關閉是否在壓縮完成之前被阻止？</strong></td>
   <td>版本清理將被中斷，儲存庫將安全關閉。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>在聯機修訂版清除期間系統崩潰時會發生什麼情況？</strong></td>
   <td>在這類情況下，資料不會損壞。 垃圾剩菜將在隨後的跑步中清理。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>不運行線上修訂版清理會產生什麼影響？</strong></td>
   <td>效能隨時間的推移而下降。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>正在收集哪些修訂？</strong></td>
   <td>預設情況下，「線上修訂版清除」僅收集至少24小時的修訂。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果併發寫入儲存庫造成過多干擾，會發生什麼情況？</strong></td>
   <td><p>如果系統上存在寫併發，則聯機修訂版清除可能需要獨佔寫訪問才能在壓縮週期結束時提交更改。 系統將進入 <strong>forceCompact模式</strong>，如 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html" target="_blank">橡木文檔</a>。 在強制壓縮期間，獲取獨佔寫鎖定以便最終提交更改而不會干擾任何併發寫入。 要限制對響應時間的影響，可以定義超時值。 預設情況下，此值設定為1分鐘，這意味著如果強制壓縮在1分鐘內未完成，壓縮過程將中止，有利於併發提交。</p> <p>力緊縮的持續時間取決於以下因素：</p>
    <ul>
     <li>硬體：特別是IOPS。 持續時間隨IOPS的增加而減少。</li>
     <li>段儲存大小：持續時間隨段儲存的大小而增加。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>如何在備用實例上執行聯機修訂版清除？</strong></p> </td>
   <td><p>在冷備用安裝中，只需將主實例配置為運行線上修訂版清除。 在備用實例上，不需要專門安排線上修訂版清除。</p> <p>備用實例上的相應操作是「自動清理」(Automatic Cleanup) — 這對應於「聯機修訂版清理」(Online Revision Cleanup)的清理階段。 在主實例上執行「線上修訂版清除」後，將在備用實例上運行「自動清除」。</p> <p>估計階段和壓縮階段將不會在備用實例上運行。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>離線修訂版清除是否可釋放比聯機修訂版清除更多的磁碟空間？</strong></td>
   <td><p>離線修訂版清除可以立即刪除舊修訂，而聯機修訂版清除需要考慮應用程式堆棧仍引用的舊修訂。 因此，前者比後者更積極地去除垃圾，因為在幾個垃圾收集週期中，效果被攤銷。</p> <p>此外，請閱讀的「離線修訂版清除後運行線上修訂版清除」部分 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">本章</a>。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>有關記憶體映射檔案操作的注意事項嗎？</td>
   <td>
    <ul>
     <li><strong>在Windows環境中</strong>，始終強制執行常規檔案訪問，因此不使用記憶體映射訪問。 一般建議，應將所有可用RAM分配給堆，並增加segmentCache大小。 通過將segmentCache.size選項添加到org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config（例如，segmentCache.size=20480），可增加segmentCache。 切記為作業系統和其他進程留出一些記憶體。</li>
     <li><strong>在非Windows環境中</strong>，增加物理記憶體的大小以改進儲存庫的記憶體映射。</li>
    </ul> </td>
   <td>
    <ul>
     <li> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 監視線上修訂版清除 {#monitoring-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>線上修訂版清理期間需要監控哪些內容？</strong></td>
   <td>
    <ul>
     <li>啟用「Online Revision Cleanup（聯機修訂清除）」時，應監視磁碟空間。 清理將不會運行，或者在磁碟空間不足時將搶先終止。</li>
     <li>檢查日誌以瞭解聯機修訂版清除的完成時間。 不得超過2小時。</li>
     <li>檢查點數。 如果壓縮運行時有3個以上的檢查點，建議清除這些檢查點。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何檢查聯機修訂版清除是否已成功完成？</strong></td>
   <td><p>您可以通過檢查日誌來檢查聯機修訂版清除是否已成功完成。</p> <p>例如， "<code>TarMK GC #{}: compaction completed in {} ({} ms), after {} cycles</code>"表示壓縮步驟成功完成，除非出現消息"<code>TarMK GC #{}: compaction gave up compacting concurrent commits after {} cycles</code>"，也就是說同時載入過多。</p> <p>相應地，有消息"<code>TarMK GC #{}: cleanup completed in {} ({} ms</code>」，以成功完成清理步驟。</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><strong>在何處可以找到上次聯機修訂版清除執行的統計資訊？</strong></td>
   <td><p>通過JMX(<code>SegmentRevisionGarbageCollection</code> MBean)。 有關 <code>SegmentRevisionGarbageCollection</code> MBean，讀取 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">後段</a>。</p> <p>可以通過 <code>EstimatedRevisionGCCompletion</code> 屬性 <code>SegmentRevisionGarbageCollection MBean.</code></p> <p>可以使用 <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection"</code>。</p> <p>請注意，統計資訊僅自上次系統啟動後可用。 可以利用外部監控工具將資料保持在超出正常AEM運行時間。 請參閱 <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">將運行AEM狀況檢查連接到Nagios的文檔，作為外部監控工具的示例</a>。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>哪些相關日誌條目？</strong></td>
   <td>
    <ul>
     <li>聯機修訂版清理已啟動/已停止
      <ul>
       <li>線上修訂清除由三個階段組成：估計、壓縮和清理。 如果儲存庫中沒有足夠的垃圾，則估計可能會強制壓縮和清除。 在的最新版本AEM中，消息「<code>TarMK GC #{}: estimation started</code>"標籤估計的開始， "<code>TarMK GC #{}: compaction started, strategy={}</code>"標籤壓縮的開始和"T"<code>arMK GC #{}: cleanup started. Current repository size is {} ({} bytes</code>"標籤清理的開始。</li>
      </ul> </li>
     <li>修訂版清除獲取的磁碟空間
      <ul>
       <li>僅在清理階段完成時才回收空間。 清理階段的完成由日誌消息「T」標籤<code>arMK GC #{}: cleanup completed in {} ({} ms</code>。 後清理大小為{}（{}位元組），回收的空間為{}（{}位元組）。 壓縮映射重量/深度為{}/{}({} bytes/{})。"</li>
      </ul> </li>
     <li>修訂版清除期間出現問題
      <ul>
       <li>故障情況很多，所有故障都標有WARN或ERROR日誌消息，並顯示「TarMK GC」。</li>
      </ul> </li>
    </ul> <p>另請參見 <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">基於錯誤消息的故障排除</a> 的下界。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何檢查在「線上修訂版清理」完成後回收了多少空間？</strong></td>
   <td>清理週期結束時，日誌中有一條消息："<code>TarMK GC #3: cleanup completed</code>「包括儲存庫的大小和回收垃圾的數量。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何在「線上修訂版清除」完成後檢查儲存庫的完整性？</strong></td>
   <td><p>在「線上修訂版清除」之後，不需要進行儲存庫完整性檢查。 </p> <p>但是，您可以執行以下操作，以在清除後檢查儲存庫狀態：</p>
    <ul>
     <li>儲存庫 <a href="/help/sites-deploying/consistency-check.md" target="_blank">遍歷檢查</a></li>
     <li>清理過程完成後，使用oak-run工具檢查是否不一致。 有關如何執行此操作的詳細資訊，請檢查 <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Apache文檔。</a> 您不需要關閉AEM即可運行工具。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何檢測「Online Revision Cleanup（聯機修訂版清除）」是否失敗，以及要恢復的步驟是什麼？</strong></td>
   <td>故障條件由以「TarMK GC」開頭的WARN或ERROR日誌消息標籤。 另請參見 <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">基於錯誤消息的故障排除</a> 的下界。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>修訂版清理運行狀況檢查中公開了哪些資訊？ 它們如何以及何時對顏色編碼狀態級別做出貢獻？ </strong></td>
   <td><p>修訂版清理運行狀況檢查是 <a href="/help/sites-administering/operations-dashboard.md#health-reports" target="_blank">操作儀表板</a>。<br /> </p> <p>狀態為 <strong>綠色</strong> 如果上次執行聯機修訂清理維護任務已成功完成。</p> <p>會是 <strong>黃色</strong> 「聯機修訂版清理」維護任務取消一次。<br /> </p> <p>會是 <strong>紅色</strong> 在一行中取消了三次「線上修訂清除」維護任務。 <strong>在這種情況下，需要手動交互</strong> 或線上修訂清除可能再次失敗。 有關詳細資訊，請閱讀 <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-online-revision-cleanup">故障排除</a> 的下界。<br /> </p> <p>另請注意，系統重新啟動後將重置運行狀況檢查狀態。 因此，新重新啟動的實例在修訂版清理運行狀況檢查中顯示綠色狀態。 可以利用外部監控工具將資料保持在超出正常AEM運行時間。 請參閱 <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios">將運行AEM狀況檢查連接到Nagios的文檔，作為外部監控工具的示例</a>。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>如何監視備用實例上的自動清理？</strong></p> </td>
   <td><p>通過JMX，使用 <code>SegmentRevisionGarbageCollection</code> MBean。 另請參閱以下內容 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">橡木文檔</a>。 </p> <p>可以使用 <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection"</code>。</p> <p>請注意，統計資訊僅自上次系統啟動後才可用。 可以利用外部監控工具將資料保持在超出正常AEM運行時間。 另請參見 <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">將運行AEM狀況檢查連接到Nagios的文檔，作為外部監控工具的示例</a>。</p> <p>日誌檔案還可用於檢查自動清理的狀態、進度和統計資訊。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>在備用實例上的自動清理期間需要監視哪些內容？</strong></p> </td>
   <td>
    <ul>
     <li>運行「Automatic Cleanup（自動清理）」時，應監視磁碟空間。</li>
     <li>完成時間（通過日誌），以確保不超過2小時。</li>
     <li>Segmentstore大小在「自動清理」運行後。 備用實例上的段儲存大小應與主實例上的段儲存大小大致相同。</li>
    </ul> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 聯機修訂版清除疑難解答 {#troubleshooting-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>如果不運行「線上修訂版清除」，最壞的情況是什麼？</strong></td>
   <td>實AEM例將耗盡磁碟空間，導致生產中斷。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>在發佈實例上運行聯機修訂版清除時，用戶流量是否存在高問題？</strong></td>
   <td>高用戶流量會影響壓縮階段能否成功完成。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>根據運行狀況檢查和日誌條目，聯機修訂版清理未在一行中成功完成三次。 要成功完成線上修訂版清除，需要什麼？</strong></td>
   <td>您可以採取幾個步驟來查找和解決問題：<br />
    <ul>
     <li>首先，檢查日誌條目<br /> </li>
     <li>根據日誌中的資訊，採取相應的操作：
      <ul>
       <li>如果日誌顯示五個丟失的壓縮週期，並且 <code>forceCompact</code> 週期，將維護窗口安排到儲存庫寫入量低時的安靜時間。 您可以在位於的儲存庫度量監視工具中檢查儲存庫寫入 <em>https://serveraddress:serverport/libs/granite/operations/content/monitoring/page.html</em></li>
       <li>如果清理在維護窗口的末尾停止，請確保維護任務用戶介面中維護窗口的配置足夠大</li>
       <li>如果可用堆記憶體不足，請確保實例具有足夠的記憶體。</li>
       <li>如果出現延遲反應，則SegmentStore可能會增長太多，以致於線上修訂版清理無法在較長的維護窗口中完成。 例如，如果上週未成功完成線上修訂版清理，則建議計畫離線維護並執行離線修訂版清理，以便將段儲存恢復到可管理的大小。</li>
      </ul> </li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>開啟運行狀況檢查警報後需要執行什麼操作？</strong></td>
   <td>請參閱上一點。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果在計畫的維護窗口期間，「線上修訂版清除」超時，會發生什麼情況？</strong></td>
   <td>將取消線上修訂版清除，並刪除剩餘內容。 它將在下次計畫維護窗口時重新啟動。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>原因 <code>SegmentNotFoundException</code> 要登錄的實例 <code>error.log</code> 如何恢復？</strong></td>
   <td><p>A <code>SegmentNotFoundException</code> 當TarMK嘗試訪問它找不到的儲存單元（段）時，它將記錄該日誌。 有三種情況可能導致此問題：</p>
    <ol>
     <li>繞過建議的訪問機制（如Sling和JCR API）並使用較低級別的API/SPI訪問儲存庫，然後超過段的保留時間的應用程式。 也就是說，它會將對實體的引用保留的時間長於「線上修訂版清除」允許的保留時間（預設為24小時）。 此案件是暫時的，不會導致資料損壞。 要恢復，應使用oak-run工具來確認異常的瞬時性（oak-run檢查不應報告任何錯誤）。 為此，需要使實例離線，然後重新啟動。</li>
     <li>外部事件導致磁碟上的資料損壞。 這可能是磁碟故障、磁碟空間不足或意外修改所需資料檔案。 在這種情況下，實例需要離線並使用oak-run檢查進行修復。 有關如何執行橡樹運行檢查的詳細資訊，請閱讀以下內容 <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Apache文檔</a>。</li>
     <li>所有其他事件應通過 <a href="https://helpx.adobe.com/tw/marketing-cloud/contact-support.html" target="_blank">Adobe客戶關懷</a>。</li>
    </ol> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 基於錯誤消息的故障排除 {#troubleshooting-based-on-error-messages}

如果在聯機修訂版清除過程中發生意外事件，error.log將是冗餘的。 以下矩陣旨在解釋最常見的資訊並提供可能的解決方案：

<!---| **Phase** |**Log Messages** |**Explanation** |**Next Steps** |
|---|---|---|---|
|   |  |  |  |
| Estimation |TarMK GC #2: estimation skipped because compaction is paused |The estimation phase is skipped when compaction is disabled on the system by configuration. |Enable Online Revision Cleanup. |
|   |TarMK GC #2: estimation interrupted: ${REASON}. Skipping compaction. |The estimation phase terminated prematurely. Some examples of events that could interrupt the estimation phase: not enough memory or disk space on the host system. |Depends on the given reason. |
| Compaction |TarMK GC #2: compaction paused |As long as the compaction phase is paused by configuration, neither the estimation phase nor the compaction phase will be executed. |Enable online revision cleanup. |
|   |TarMK GC #2: compaction cancelled: ${REASON}. |The compaction phase terminated prematurely. Some examples of events that could interrupt the compaction phase: not enough memory or disk space on the host system. Moreover, compaction can also be cancelled by shutting down the system or by explicitly cancelling it via administrative interfaces such as the Maintenance Window within the Operations Dashobard. |Depends on the given reason. |
|   |TarMK GC #2: compaction failed in 32.902 min (1974140 ms), after 5 cycles |This message doesn’t mean that there was an unrecoverable error, but only that compaction was terminated after a certain amount of attempts. Also, read the [following paragraph](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes). |Read the following [Oak documentation](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes), and the last question of the [Running Online Revision Cleanup](/help/sites-deploying/revision-cleanup.md#running-online-revision-cleanup) section. |
| Cleanup |TarMK GC #2: cleanup interrupted |Cleanup has been cancelled by shutting down the repository. No impact on consistency is expected. Also, disk space is most likely not reclaimed to full extent. It will be reclaimed during next revision cleanup cycle. |Investigate why repository has been shut down and going forward try to avoid shutting down the repository during maintenance windows. |-->

<table style="table-layout:auto">
 <tbody>
  <tr>
    <th>階段</th>
    <th>日誌消息</th>
    <th>解釋</th>
    <th>後續步驟</th>
  </tr>  
  <tr>
    <td>估計</td>
    <td>TarMK GC #2:已跳過估計，因為壓縮已暫停。</td>
    <td>當按配置在系統上禁用壓縮時跳過估計階段。</td>
    <td>啟用聯機修訂版清除。</td>
  </td>
  </tr>
  <tr>
    <td>N/A</td>
    <td>TarMK GC #2:估計中斷：${REASON}。 跳過壓縮。</td>
    <td>估計階段提前終止。 可能中斷估計階段的事件的一些示例：主機系統上記憶體或磁碟空間不足。</td>
    <td>這要看給定的原因。</td>
  </td>
  </tr>
  <tr>
    <td>壓縮</td>
    <td>TarMK GC #2:壓縮暫停。</td>
    <td>只要壓縮階段被配置暫停，估計階段和壓縮階段都不會執行。</td>
    <td>啟用聯機修訂版清除。</td>
  </td>
  </tr>
   <tr>
    <td>N/A</td>
    <td>TarMK GC #2:壓縮已取消：${REASON}。</td>
    <td>壓縮階段提前終止。 可能中斷壓縮階段的事件的一些示例：主機系統上記憶體或磁碟空間不足。 此外，還可以通過關閉系統或通過管理介面（如操作控制板中的維護窗口）顯式取消壓縮來取消壓縮。</td>
    <td>這要看給定的原因。</td>
  </td>
  </tr>
  <tr>
    <td>N/A</td>
    <td>TarMK GC #2:壓縮在5次循環後32.902 min(1974140 ms)失效。</td>
    <td>此消息並不表示存在無法恢復的錯誤，但只表示在經過一定的嘗試後才終止壓縮。 另外，閱讀 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes">下段。</a></td>
    <td>閱讀以下內容 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes">橡木文檔</a>，以及「正在運行的聯機修訂版清除」部分的最後一個問題。</a></td>
  </td>
  </tr>
  <tr>
    <td>清理</td>
    <td>TarMK GC #2:清理中斷。</td>
    <td>已通過關閉儲存庫取消清理。 預期不會影響一致性。 另外，磁碟空間很可能不會完全回收。 將在下一個修訂版清除週期中回收。</td>
    <td>調查儲存庫關閉的原因，然後繼續嘗試避免在維護窗口期間關閉儲存庫。</td>
  </td>
  </tr>
  </tbody>
</table>

## 如何運行離線修訂版清除 {#how-to-run-offline-revision-cleanup}

>[!CAUTION]
>
>使用Oak運行的工具版本，該版本具有與安裝的Oak核心版本匹配的版本號(主要版本和次要版AEM本)。 例如，如果實AEM例的Oak核心版本為1.22.x，則應使用Oak運行工具的最新版本1.22.x。

Adobe提供一個名為 **橡樹** 執行修訂版清除。 可在以下位置下載：

[https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/)

該工具是可運行的罐，可手動運行以壓縮儲存庫。 該過程稱為離線修訂版清除，因為需要關閉儲存庫才能正確運行該工具。 確保根據維護窗口規劃清理。

有關如何提高清除過程效能的提示，請參見 [提高離線修訂版清除的效能](/help/sites-deploying/revision-cleanup.md#increasing-the-performance-of-offline-revision-cleanup)。

>[!NOTE]
>
>在進行維護之前，您還可以清除舊檢查點（下面步驟中的步驟2和3）。 僅對具有100個以上檢查點的實例建議使用此選項。

1. 請務必確保您最近備份了實AEM例。

   閉嘴AEM。

1. （可選）使用工具查找舊檢查點：

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore
   ```

1. （可選）然後，刪除未引用的檢查點：

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore rm-unreferenced
   ```

1. 運行壓縮並等待其完成：

   ```xml
   java -jar -Dsun.arch.data.model=32 oak-run.jar compact install-folder/crx-quickstart/repository/segmentstore
   ```

### 提高離線修訂版清除的效能 {#increasing-the-performance-of-offline-revision-cleanup}

這款自動運行工具引入了幾項功能，旨在提高修訂版清理過程的效能，並盡可能減少維護窗口。

該清單包括幾個命令行參數，如下所述：

* **-mmap。** 可以將其設定為true或false。 如果設定為true，則使用記憶體映射訪問。 如果設定為false，則使用檔案訪問。 如果未指定，則64位系統上使用記憶體映射訪問，32位系統上使用檔案訪問。 在Windows上，始終強制執行常規檔案訪問，並忽略此選項。 **此參數已替換 — Dtar.memoryMapped參數。**

* **-Dupdate.limit**。 定義臨時事務刷新到磁碟的閾值。 預設值為 10000。

* **— 壓縮間隔**。 壓縮當前映射之前要保留的壓縮映射條目數。 預設值為1000000。 如果有足夠的堆記憶體可用，則應將此值增加到更高的數量，以加快吞吐量。 **此參數已在Oak版本1.6中刪除，且無效。**

* **— 壓縮 — 進度 — 日誌**。 將記錄的壓縮節點數。 預設值為150000，這意味著在操作過程中將記錄前150000個壓縮節點。 將此參數與下面介紹的下一個參數一起使用。

* **-Dtar.PersistCompontMap。** 將此參數設定為true可使用磁碟空間而不是堆記憶體來壓縮映射持久性。 需要使用橡木制工具 **版本1.4** 更高。 有關更多詳情，請參閱 [離線修訂版清理常見問題](/help/sites-deploying/revision-cleanup.md#offline-revision-cleanup-frequently-asked-questions) 的子菜單。 **此參數已在Oak版本1.6中刪除，且無效。**

* **— 力。** 強制壓縮並忽略不匹配的段儲存版本。

>[!CAUTION]
>
>使用 `--force` 參數會將段儲存升級到與較舊的Oak版本不相容的最新版本。 另外，考慮到不可能降級。 通常，您應謹慎使用這些參數，並且只有在知道如何使用這些參數時才可使用。

使用中的參數示例：

```xml
java -Dupdate.limit=10000 -Dcompaction-progress-log=150000 -Dlogback.configurationFile=logback.xml -Xmx8g -jar oak-run-*.jar checkpoints <repository>
```

### 觸發修訂清除的其他方法 {#additional-methods-of-triggering-revision-cleanup}

除上面介紹的方法外，還可以使用JMX控制台觸發修訂版清除機制，如下所示：

1. 通過轉到 [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)
1. 按一下 **修訂垃圾收集** MBean。
1. 在下一個窗口中，按一下 **startRevisionGC()** 然後 **調用** 啟動修訂垃圾收集作業。

### 離線修訂版清理常見問題 {#offline-revision-cleanup-frequently-asked-questions}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>決定離線修訂版清除持續時間的因素有哪些？</strong></td>
   <td><p>儲存庫大小和需要清理的修訂量決定了清理的持續時間。</p> </td>
  </tr>
  <tr>
   <td><strong>修訂版和頁面版本有何區別？</strong></td>
   <td>
    <ul>
     <li><strong>橡樹版：</strong> Oak將所有內容組織在由節點和屬性組成的大樹層次結構中。 此內容樹的每個快照或修訂版本是不可變的，對該樹所做的更改將表示為新修訂的序列。 通常，每個內容修改都觸發新修訂。 另請參閱 <a href="https://jackrabbit.apache.org/dev/ngp.html" target="_blank"> 跟蹤連結</a>。</li>
     <li><strong>頁面版本：</strong> 版本控制在特定時間點建立頁面的「快照」。 通常，在激活頁面時會建立新版本。 有關詳細資訊，請參見 <a href="/help/sites-authoring/working-with-page-versions.md" target="_blank">使用頁面版本</a>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>如果離線修訂版清除任務在8小時內未完成，如何加快該任務的速度？</strong></td>
   <td>如果修訂任務在8小時內未完成， <a href="/help/sites-administering/operations-dashboard.md#diagnosis-tools" target="_blank">線程轉儲</a> 揭示了主要熱點是 <code>InMemoryCompactionMap.findEntry</code>，將以下參數與oak-run工具一起使用 <strong>版本1.4 </strong>或更高： <code>-Dtar.PersistCompactionMap=true</code>。 請注意 <code>-Dtar.PersistCompactionMap</code> 已在Oak版本1.6中刪除參數。</td>
  </tr>
 </tbody>
</table>
