---
title: 修訂清除
seo-title: Revision Cleanup
description: 了解如何使用AEM 6.5中的修訂清除功能。
seo-description: Learn how to use the Revision Cleanup functionality in AEM 6.5.
uuid: 321f5038-44b0-4f1e-a1aa-2d29074eed70
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: f03ebe60-88c0-4fc0-969f-949490a8e768
feature: Configuring
exl-id: e53c4c81-f62e-4b6d-929a-6649c8ced23c
source-git-commit: 28046104e75a833736f53b0e9d1edf4c8fbe6249
workflow-type: tm+mt
source-wordcount: '5898'
ht-degree: 0%

---

# 修訂清除{#revision-cleanup}

## 簡介 {#introduction}

每個對儲存庫的更新都會建立新的內容修訂。 因此，每次更新時，存放庫的大小都會增加。 為避免儲存庫增長失控，需要清理舊修訂版本以釋放磁碟資源。 此維護功能稱為修訂清除。 自AEM 6.0起，已可作為離線常式使用。

在AEM 6.3及更新版本中，引入了名為「線上修訂清除」的線上版本功能。 與必須關閉AEM例項的離線修訂清除相比，當AEM例項上線時，可執行線上修訂清除。 「線上修訂清除」預設為開啟，這是執行修訂清除的建議方式。

**附註**: [請參閱影片](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/revision-cleanup-technical-video-use.html) 以了解簡介及如何使用「線上修訂清除」。

修訂清除程式包含三個階段： **估計**, **壓實** 和 **清理**. 估計會根據可收集的垃圾量，決定是否要執行下一階段（壓縮）。 壓縮階段期間，會重寫區段和tar檔案，留下任何未使用的內容。 清理階段隨後移除了舊段，包括它們可能包含的任何垃圾。 離線模式通常可節省更多空間，因為線上模式需要考慮AEM工作集，而這會保留其他區段無法收集。

如需「修訂清除」的詳細資訊，請參閱下列連結：

* [如何執行線上修訂清除](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup)
* [線上修訂清除常見問題](/help/sites-deploying/revision-cleanup.md#online-revision-cleanup-frequently-asked-questions)
* [如何執行離線修訂清除](/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup)

此外，您也可以閱讀 [官方Oak檔案。](https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html)

### 何時使用「線上修訂清除」而非「離線修訂清除」？ {#when-to-use-online-revision-cleanup-as-opposed-to-offline-revision-cleanup}

**執行修訂清除的建議方式是「線上修訂清除」。** 離線修訂清除應僅在例外情況下使用，例如，在遷移至新儲存格式之前，或如果Adobe客戶服務要求您執行此操作，則應先使用。

## 如何執行線上修訂清除 {#how-to-run-online-revision-cleanup}

依預設，「線上修訂清除」會設定為在AEM製作和發佈執行個體上每天自動執行一次。 您只需在使用者活動最少的期間內定義維護期間即可。 您可以依照下列方式設定「線上修訂清除」任務：

1. 在主AEM視窗中，前往 **工具 — 操作 — 儀表板 — 維護** 或將瀏覽器指向： `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. 暫留在 **每日維護窗口** 並按一下 **設定** 表徵圖。

   ![chlimage_1-91](assets/chlimage_1-91.png)

1. 輸入所需值（重複、開始時間、結束時間），然後按一下 **儲存**.

   ![chlimage_1-92](assets/chlimage_1-92.png)

或者，如果要手動運行修訂清除任務，可以：

1. 前往 **工具 — 操作 — 儀表板 — 維護** 或直接瀏覽至 `https://serveraddress:serverport/libs/granite/operations/content/maintenance.html`
1. 按一下 **每日維護窗口**.
1. 暫留在 **修訂清除** 表徵圖。
1. 按一下 **執行**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

### 離線修訂清除後執行線上修訂清除 {#running-online-revision-cleanup-after-offline-revision-cleanup}

修訂清除程式會逐代回收舊修訂。 這表示每次執行修訂清除時，都會建立新的一代並保留在磁碟上。 不過，兩種修訂清除類型之間有差異：離線修訂清除會保留一代，而線上修訂清除會保留兩代。 所以，當您執行線上修訂清除時 **after** 離線修訂清除會發生下列情況：

1. 執行第一個線上修訂清除後，存放庫的大小會加倍。 之所以會發生這種情況，是因為現在有兩代人保留在磁碟上。
1. 在後續運行中，儲存庫將在建立新一代時臨時增長，然後穩定到首次運行後的大小，因為線上修訂清理過程將重新整理上一代。

另外，請記住，根據提交的類型和數量，每代的大小都可能與前一代不同，因此最終大小可能因一次運行而異。

因此，建議將磁碟的大小至少比最初估計的儲存庫大小大兩三倍。

## 完整和尾部壓實模式  {#full-and-tail-compaction-modes}

**AEM 6.5** 簡介 **兩種新模式** 針對 **壓實** 「線上修訂清除」過程的階段：

* 此 **全壓實** 模式會重寫整個存放庫中的所有區段和tar檔案。 因此，後續的清理階段可以在整個儲存庫中刪除最大的垃圾量。 由於完全壓縮會影響整個儲存庫，因此需要大量的系統資源和時間才能完成。 完全壓實與AEM 6.3中的壓實階段相對應。
* 此 **尾部壓實** 模式只會重寫存放庫中最新的區段和tar檔案。 最近的區段和tar檔案是自上次完全或尾部壓縮執行後新增的區段和tar檔案。 因此，後續的清理階段只能移除存放庫最近部分所包含的垃圾。 由於尾部壓縮只影響儲存庫的一部分，因此完成所需的系統資源和時間比完全壓縮要少得多。

這些壓縮模式構成了效率和資源消耗之間的權衡：尾部壓實效果差，對系統正常運行影響小。 相比之下，全壓實效果更好，但對系統正常運行影響較大。

AEM 6.5也導入了壓縮期間更有效的內容重複資料刪除機制，進一步減少存放庫的磁碟空間。

下面的兩張圖表呈現了內部實驗室測試的結果，這些測試說明與AEM 6.3相比，AEM 6.5中磁碟的平均執行時間和平均佔用空間減少了：

![onrc-duration-6_4vs63](assets/onrc-duration-6_4vs63.png) ![segmentstore-6_4vs63](assets/segmentstore-6_4vs63.png)

### 如何配置完整和尾部壓縮 {#how-to-configure-full-and-tail-compaction}

預設設定會在周天執行尾部壓縮，並在週日執行完全壓縮。 使用新配置值可以更改預設配置 `full.gc.days` 的 `RevisionCleanupTask` [維護任務](/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup).

當您設定 `full.gc.days` 值請注意，完全壓縮會在值中定義的日期期間執行，而尾部壓縮則會在值中未定義的日期期間執行。 例如，如果您設定完全壓縮以在星期日執行，則尾部壓縮將在星期一至星期六執行。 例如，如果您設定完全壓縮以每週的每天執行，則尾部壓縮完全不會執行。

此外，請考量：

* **尾部壓實** 效率較低，對正常系統操作的影響較小。 因此，它打算在工作日期間運行。
* **完全壓縮** 更有效，但對正常系統操作的影響也更大。 因此，本計畫在工作日使用。
* 尾部壓實和完全壓實都應安排在非高峰時段運行。

### 疑難排解 {#troubleshooting}

使用新的壓縮模式時，請記住以下事項：

* 您可以監控輸入/輸出(I/O)活動，例如：I/O操作、等待IO的CPU、提交隊列大小。 這有助於確定系統是否正在綁定I/O，並需要更新大小。
* 此 `RevisionCleanupTaskHealthCheck` 指示「線上修訂清除」的總體運行狀況。 其運作方式與AEM 6.3相同，不區分完整壓實與尾部壓實。
* 記錄訊息包含關於壓縮模式的相關資訊。 例如，當「線上修訂清除」啟動時，對應的記錄訊息會指出壓縮模式。 此外，在某些角落情況下，當計畫運行尾部壓縮時，系統將恢復為完全壓縮，日誌消息將指示此更改。 以下的日誌樣本指示壓實模式以及從尾部到完全壓實的變化：

```
TarMK GC: running tail compaction
TarMK GC: no base state available, running full compaction instead
```

### 已知限制 {#known-limitations}

在某些情況下，尾部和完全壓實模式之間的交替會延遲清理過程。 更準確地說，完整壓縮後，存放庫將會增加（其大小會翻倍）。 當存放庫將降至預先完全壓縮大小以下時，額外的空間將會在後續的尾部壓縮中回收。 還應避免並行維護任務執行。

**建議將磁碟的大小至少比最初估計的儲存庫大小大兩三倍。**

## 線上修訂清除常見問題 {#online-revision-cleanup-frequently-asked-questions}

### AEM 6.5升級考量事項 {#aem-upgrade-considerations}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td>問題 </td>
   <td>答案</td>
  </tr>
  <tr>
   <td>升級至AEM 6.5時，應注意什麼？</td>
   <td><p>AEM 6.5會變更TarMK的持續性格式。這些變更不需要主動移轉步驟。 現有存放庫會執行滾動式移轉，對使用者而言是透明的。 AEM 6.5（或相關工具）首次存取存放庫時，就會啟動移轉程式。</p> <p><strong>一旦開始移轉至AEM 6.5永續性格式，存放庫就無法還原回先前的AEM 6.3永續性格式。</strong></p> </td>
  </tr>
 </tbody>
</table>

### 移轉至Oak Segment Tar {#migrating-to-oak-segment-tar}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>答案</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>為何需要遷移儲存庫？</strong></td>
   <td><p>在AEM 6.3中，需要更改儲存格式，特別是為了改進線上修訂清理的效能和效果。 這些變更不向後相容，且以舊Oak區段(AEM 6.2和舊版)建立的存放庫必須移轉。</p> <p>更改儲存格式的其他好處：</p>
    <ul>
     <li>更佳的可擴充性（最佳化區段大小）。</li>
     <li>更快 <a href="/help/sites-administering/data-store-garbage-collection.md" target="_blank">資料儲存垃圾收集</a>.<br /> </li>
     <li>未來增強功能的基礎工作。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>仍支援舊版Tar格式嗎？</strong></td>
   <td>AEM 6.3或更新版本僅支援新的Oak Segment Tar。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>內容移轉一律為強制項目嗎？</strong></td>
   <td>可以。除非您從最新的例項開始，否則您永遠必須移轉內容。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>我是否可升級至6.3或更新版本，稍後再進行移轉（例如，使用其他維護視窗）?</strong></td>
   <td>否，如上所述，內容移轉是強制性的。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>遷移時可以避免停機嗎？</strong></td>
   <td>否. 這是一次性作業，無法在執行中的執行個體上完成。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果不小心執行錯誤的存放庫格式，會發生什麼事？</strong></td>
   <td>如果您嘗試對oak-segment-tar存放庫執行oak-segment模組（或反之），啟動會因 <em>IllegalStateException</em> 顯示訊息「區段格式無效」。 不會發生資料損壞。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>是否需要重新索引搜索索引？</strong></td>
   <td>否. 從oak-segment移轉至oak-segment-tar會導致容器格式的變更。 包含的資料不受影響，不會修改。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何最佳地計算遷移期間和遷移後所需的預期磁碟空間？</strong></td>
   <td>移轉等同於以新格式重新建立區段存放區。 這可用於估計遷移期間所需的額外磁碟空間。 遷移後，可以刪除舊的段儲存以回收空間。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何最佳估計移轉的持續時間？</strong></td>
   <td>如果 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-offline-revision-cleanup">離線修訂清除</a> 會在移轉前執行。 建議所有客戶在升級程式前先執行此作業。 一般而言，移轉的持續時間應與離線修訂清除任務的持續時間類似，假設離線修訂清除任務已在移轉前執行。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 執行線上修訂清除 {#running-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>問題</strong></td>
   <td><strong>答案</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>執行「線上修訂清除」的頻率為何？</strong></td>
   <td>一天一次. 這是「操作控制面板」中的預設配置。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何配置線上修訂清除維護任務的開始時間？</strong></td>
   <td>請參閱 <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">如何執行線上修訂清除</a> 區段。 </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>線上修訂清除是否有不應超過的最大頻率？</strong></td>
   <td>建議您依預設設定，每天執行一次線上修訂清除。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>決定線上修訂清除執行頻率的關鍵指標為何？</strong></td>
   <td>無需確定頻率，因為「線上修訂清除」已設定為維護任務，且每天會自動執行。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>為什麼「線上修訂清除」第一次運行時沒有回收任何空間？</strong></td>
   <td>線上修訂清除會按代回收舊修訂。 每次執行修訂清除時，都會產生新的層代。 只有至少兩代的內容才會被回收，這意味著在第一次運行中，沒有什麼可回收的。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>在離線修訂清除後執行時，第一個線上修訂清除為何不會回收任何空間？</strong></td>
   <td><p>離線修訂清除將回收除最新一代之外的所有內容，而線上修訂清除則需回收最新兩代。 若是新的存放庫，線上修訂清除在離線修訂清除後首次執行時，不會回收任何空間，因為沒有足夠可回收的代數。</p> <p>此外，請參閱以下的「離線修訂清除後執行線上修訂清除」一節： <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">本章</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>製作和發佈通常會有不同的「線上修訂清除」視窗嗎？</strong></td>
   <td>這取決於客戶的上班時間和線上狀態的流量模式。 維護窗口應配置在主生產時間之外，以獲得最佳的清理效果。 若為多個AEM發佈執行個體（TarMK伺服器陣列），「線上修訂清除」的維護視窗應交錯開來。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>執行線上修訂清除之前是否有任何先決條件？</strong></td>
   <td><p>「線上修訂清除」僅適用於AEM 6.3及更新版本。 此外，如果您使用舊版AEM，則需要移轉至新 <a href="/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar">Oak Segment Tar</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>決定線上修訂清除持續時間的因素有哪些？</strong></td>
   <td>因素包括：<br />
    <ul>
     <li>存放庫大小</li>
     <li>在系統上載入（每分鐘請求數，特別是寫入操作）</li>
     <li>活動模式（讀取與寫入）</li>
     <li>硬體規格（CPU效能、記憶體、IOPS）</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>執行線上修訂清除時，作者仍可工作嗎？</strong></td>
   <td>是的，線上修訂清除可以處理併發寫入。 但是，「線上修訂清除」可以更快、更高效地運行，而無需同時執行寫入事務。 建議將「線上修訂清除」維護任務安排到相對安靜的時間，而不需要大量流量。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>運行「聯機修訂清除」時，磁碟空間和堆記憶體的最低要求是什麼？</strong></td>
   <td><p>線上修訂清除期間會持續監控磁碟空間。 如果可用磁碟空間降至關鍵值以下，該過程將被取消。 關鍵值是儲存庫當前磁碟佔用量的25%，且不可配置。</p> <p><strong>建議將磁碟的大小至少比最初估計的儲存庫大小大兩三倍。</strong></p> <p>清除過程中會持續監視空閒堆空間。 如果空閒堆空間降至關鍵值以下，則取消該進程。 關鍵值是透過org.apache.jackrabbit.oak.segment.SegmentNodeStoreService#MEMORY_THRESHOLD設定。 預設值為15%。</p> <p>Recommendations的最小壓縮堆大小調整不會與AEM記憶體大小調整建議分開。 一般規則是： <strong>如果AEM例項的大小足以應付使用案例和其上預期的裝載，清理程式將會取得足夠的記憶體。</strong></p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>運行線上修訂清除時預期的效能影響是什麼？</strong></td>
   <td>「線上修訂清除」是一個後台進程，它從儲存庫中讀取資料，並將資料寫入正常的系統操作。 尤其是，它可能需要在短時間內獲得對儲存庫的獨佔訪問權，從而阻止其他線程寫入儲存庫。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>線上修訂清除預計會執行多久？</strong></td>
   <td>根據我們內部執行的最新效能測試，執行時間不應超過2小時。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果「線上修訂清除」需要更長時間，該怎麼辦？</strong></td>
   <td>
    <ul>
     <li>確保每日執行。<br /> </li>
     <li>請在Operations Dashboard中相應地配置維護窗口，以確保它在最少的儲存庫活動期間執行。</li>
     <li>擴展系統資源（CPU、記憶體、I/O）。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果「線上修訂清除」超過配置的維護窗口，會發生什麼情況？</strong></td>
   <td>確保其他維護任務不會延遲其執行。 如果在同一維護窗口中執行的維護任務比「線上修訂清除」更多，則可能會是這種情況。 請注意，維護任務是按順序執行的，不具有可配置的順序。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>為什麼跳過修訂垃圾收集？</strong></td>
   <td><p>「修訂清理」依賴於估計階段來確定是否有足夠的垃圾可清理。 估算程式會比較目前的大小與上次壓縮後存放庫的大小。 如果大小超過設定的增量，則清除將運行。 大小增量設定為1 GB。 這實際上表示，如果儲存庫大小自上次清除執行以來未增加1 GB，則會略過新的修訂清除迭代。 </p> <p>以下是估計階段的相關日誌條目：</p>
    <ul>
     <li>修訂GC將運行： <em>大小增量為N%或N/N（N/N位元組），因此運行壓縮</em></li>
     <li>修訂GC將 <strong>not</strong> 執行： <em>大小增量為N%或N/N（N/N位元組），因此暫時跳過壓縮</em></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果效能影響太大，是否可以安全地中止自動壓縮？</strong></td>
   <td>可以。自AEM 6.3起，它可通過Operations Dashboard中的Maintenance Task Window或JMX安全地停止。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果AEM執行個體在排程的清除任務期間關閉，程式是否會安全中止，或是在壓縮完成前關閉會遭到封鎖？</strong></td>
   <td>修訂清除將中斷，存放庫將安全關閉。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>線上修訂清除期間系統當機時會發生什麼事？</strong></td>
   <td>在此類情況下，資料不會損壞。 垃圾剩料將被後續運行清理。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>未運行線上修訂清除會產生什麼影響？</strong></td>
   <td>效能隨時間而降低。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>正在收集哪些修訂版本？</strong></td>
   <td>依預設，「線上修訂清除」只會收集至少24小時以前的修訂。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果同時寫入存放庫時受到的干擾過多，會發生什麼情況？</strong></td>
   <td><p>如果系統上存在寫併發，線上修訂清除可能需要獨佔的寫訪問權才能在壓縮週期結束時提交更改。 系統會進入 <strong>forceCompact模式</strong>，如 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html" target="_blank">oak檔案</a>. 在強制緊縮期間，獲取獨佔寫鎖，以便最終提交更改而不會任何併發寫入干擾。 若要限制對回應時間的影響，可以定義逾時值。 此值預設為1分鐘，這表示如果強制壓縮未在1分鐘內完成，壓縮過程將中止，以支援併發提交。</p> <p>力緊的持續時間取決於以下因素：</p>
    <ul>
     <li>硬體：特別是IOPS。 持續時間會隨著IOPS的增加而減少。</li>
     <li>區段存放區大小：持續時間會隨著區段存放區的大小而增加。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>如何在備用執行個體上執行線上修訂清除？</strong></p> </td>
   <td><p>在冷備用設定中，只需將主實例配置為運行聯機修訂清除。 在備用執行個體上，不需要特別排程線上修訂清除。</p> <p>備用執行個體上的對應操作是「自動清除」 ，這對應於「線上修訂清除」的清除階段。 在主實例上執行「線上修訂清除」後，在備用實例上運行「自動清除」。</p> <p>估計階段和壓縮階段不會在備用執行個體上執行。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>離線修訂清除是否能釋放比線上修訂清除更多的磁碟空間？</strong></td>
   <td><p>離線修訂清除可以立即移除舊修訂，而線上修訂清除需要考慮應用程式堆疊仍在參照的舊修訂。 因此，前者比後者更積極地去除垃圾，在幾個垃圾收集週期中，效果被攤銷。</p> <p>此外，請參閱以下的「離線修訂清除後執行線上修訂清除」一節： <a href="/help/sites-deploying/revision-cleanup.md#how-to-run-online-revision-cleanup">本章</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>有關記憶體映射檔案操作的注意事項嗎？</td>
   <td>
    <ul>
     <li><strong>在Windows環境上</strong>，則一律會強制執行一般檔案存取，因此不會使用記憶體對應存取。 作為一般建議，應將所有可用RAM分配給堆，並增加segmentCache大小。 將segmentCache.size選項新增至org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config(例如segmentCache.size=20480)，以增加segmentCache。 切記為作業系統和其他進程保留一些RAM。</li>
     <li><strong>在非Windows環境上</strong>，增加物理記憶體的大小，以改進儲存庫的記憶體映射。</li>
    </ul> </td>
   <td>
    <ul>
     <li> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 監控線上修訂清除 {#monitoring-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>線上修訂清除期間需要監控哪些項目？</strong></td>
   <td>
    <ul>
     <li>啟用「線上修訂清除」時，應監視磁碟空間。 清理將不運行，或在磁碟空間不足時搶先終止。</li>
     <li>檢查記錄檔中的線上修訂清除完成時間。 不應超過2小時。</li>
     <li>查核點數。 如果壓縮執行時有超過3個查核點，建議清除查核點。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何檢查線上修訂清除是否成功完成？</strong></td>
   <td><p>您可以檢查記錄檔，以檢查「線上修訂清除」是否已成功完成。</p> <p>例如，「<code>TarMK GC #{}: compaction completed in {} ({} ms), after {} cycles</code>"表示壓縮步驟成功完成，除非前面有消息"<code>TarMK GC #{}: compaction gave up compacting concurrent commits after {} cycles</code>「，這表示同時負載過多。</p> <p>相應地，會出現消息「<code>TarMK GC #{}: cleanup completed in {} ({} ms</code>」，以順利完成清除步驟。</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><strong>我們可以在哪裡找到上次線上修訂清除執行的統計資料？</strong></td>
   <td><p>狀態、進度和統計資訊會透過JMX公開(<code>SegmentRevisionGarbageCollection</code> MBean)。 如需 <code>SegmentRevisionGarbageCollection</code> MBean，請閱讀 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">後段</a>.</p> <p>進度可透過 <code>EstimatedRevisionGCCompletion</code> 屬性 <code>SegmentRevisionGarbageCollection MBean.</code></p> <p>您可以使用 <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection"</code>.</p> <p>請注意，統計資料僅自上次系統啟動後可用。 可運用外部監控工具，讓資料超出AEM正常運作時間。 請參閱 <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">將健康狀態檢查附加至Nagios的AEM檔案，作為外部監控工具的範例</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>相關記錄項目為何？</strong></td>
   <td>
    <ul>
     <li>已開始/停止線上修訂清除
      <ul>
       <li>「線上修訂清除」由三個階段組成：估計、壓縮和清理。 如果存放庫未包含足夠的垃圾，估計可能會強制壓縮和清除，以略過。 在最新版AEM中，訊息為「<code>TarMK GC #{}: estimation started</code>"標籤估計的開始， "<code>TarMK GC #{}: compaction started, strategy={}</code>"標籤壓縮的開頭和"T"<code>arMK GC #{}: cleanup started. Current repository size is {} ({} bytes</code>」會標示清理的開始。</li>
      </ul> </li>
     <li>修訂清除獲取的磁碟空間
      <ul>
       <li>只有在清理階段完成時，才會回收空間。 清理階段的完成由日誌消息「T」標籤<code>arMK GC #{}: cleanup completed in {} ({} ms</code>」。 清理後大小為{}（{}位元組），空間回收了{}（{}位元組）。 壓縮映射權重/深度為{}/{}({} bytes/{})。」</li>
      </ul> </li>
     <li>修訂清除期間發生問題
      <ul>
       <li>故障情況很多，所有情況都標籤有「TarMK GC」開頭的「WARN」或「ERROR」日誌消息。</li>
      </ul> </li>
    </ul> <p>另請參閱 <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">根據錯誤訊息進行疑難排解</a> 一節。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何檢查線上修訂清除完成後回收了多少空間？</strong></td>
   <td>清理週期結束時，日誌中會顯示一條消息："<code>TarMK GC #3: cleanup completed</code>「包括儲存庫的大小和回收的垃圾量。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>線上修訂清除完成後，如何檢查存放庫的完整性？</strong></td>
   <td><p>線上修訂清除後，不需要存放庫完整性檢查。 </p> <p>不過，您可以執行下列動作，在清除後檢查存放庫狀態：</p>
    <ul>
     <li>存放庫 <a href="/help/sites-deploying/consistency-check.md" target="_blank">遍歷檢查</a></li>
     <li>清理程式完成後，請使用oak-run工具來檢查不一致之處。 如需如何執行此動作的詳細資訊，請檢查 <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Apache檔案。</a> 您不需要關閉AEM即可執行工具。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如何檢測聯機修訂清除是否失敗，以及要恢復的步驟是什麼？</strong></td>
   <td>失敗條件會以「TarMK GC」開頭的「WARN」或「ERROR」記錄訊息標示。 另請參閱 <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-based-on-error-messages">根據錯誤訊息進行疑難排解</a> 一節。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>修訂清除運行狀況檢查中公開了哪些資訊？ 它們對色彩編碼狀態層級有何貢獻？ </strong></td>
   <td><p>修訂清理運行狀況檢查是 <a href="/help/sites-administering/operations-dashboard.md#health-reports" target="_blank">操作儀表板</a>.<br /> </p> <p>狀態將為 <strong>綠色</strong> 如果「線上修訂清理」維護任務的上次執行已成功完成。</p> <p>會是 <strong>黃色</strong> 如果「線上修訂清除」維護任務取消一次。<br /> </p> <p>會是 <strong>紅色</strong> 如果「線上修訂清理」維護任務已連續取消三次。 <strong>在此情況下，需要手動互動</strong> 或「線上修訂清除」可能再次失敗。 如需詳細資訊，請閱讀 <a href="/help/sites-deploying/revision-cleanup.md#troubleshooting-online-revision-cleanup">疑難排解</a> 一節。<br /> </p> <p>另請注意，系統重新啟動後，運行狀況檢查狀態將重置。 因此，新重新啟動的執行個體在修訂清除健康檢查中會顯示綠色狀態。 可運用外部監控工具，讓資料超出AEM正常運作時間。 請參閱 <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios">將健康狀態檢查附加至Nagios的AEM檔案，作為外部監控工具的範例</a>.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>如何監視待機實例的自動清除？</strong></p> </td>
   <td><p>狀態、進度和統計資訊會透過JMX公開，方法是使用 <code>SegmentRevisionGarbageCollection</code> MBean。 另請參閱下列內容 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#monitoring-via-jmx" target="_blank">Oak檔案</a>. </p> <p>您可以使用 <code>ObjectName org.apache.jackrabbit.oak:name="Segment node store revision garbage collection",type="SegmentRevisionGarbageCollection"</code>.</p> <p>請注意，統計資料僅自上次系統啟動後才可用。 可運用外部監控工具，讓資料超出AEM正常運作時間。 另請參閱 <a href="/help/sites-administering/operations-dashboard.md#monitoring-with-nagios" target="_blank">將健康狀態檢查附加至Nagios的AEM檔案，作為外部監控工具的範例</a>.</p> <p>日誌檔案還可用於檢查「自動清理」的狀態、進度和統計資訊。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p><strong>在備用實例的自動清理期間需要監控哪些內容？</strong></p> </td>
   <td>
    <ul>
     <li>運行「自動清理」時應監視磁碟空間。</li>
     <li>完成時間（透過記錄檔），以確保不會超過2小時。</li>
     <li>執行「自動清除」後，Segmentstore大小。 備用執行個體上的segmentstore大小應與主執行個體上的大小大致相同。</li>
    </ul> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 疑難排解線上修訂清除 {#troubleshooting-online-revision-cleanup}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>如果不運行「線上修訂清除」，最糟糕的情況是什麼？</strong></td>
   <td>AEM執行個體將耗盡磁碟空間，導致生產中斷。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>在發佈執行個體上執行線上修訂清除會造成高使用者流量問題嗎？</strong></td>
   <td>高使用者流量會影響壓縮階段是否能成功完成。<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>根據運行狀況檢查和日誌條目，聯機修訂清除未連續成功完成三次。 成功完成線上修訂清除需要什麼？</strong></td>
   <td>您可以執行數個步驟來尋找並修正問題：<br />
    <ul>
     <li>首先，檢查日誌條目<br /> </li>
     <li>視記錄檔中的資訊而定，採取適當動作：
      <ul>
       <li>如果記錄檔顯示5個遺漏的緊密週期，且逾時 <code>forceCompact</code> 週期，當儲存庫寫入量低時，將維護窗口安排到安靜時間。 您可以在位於的存放庫量度監控工具中檢查存放庫寫入作業 <em>https://serveraddress:serverport/libs/granite/operations/content/monitoring/page.html</em></li>
       <li>如果清理在維護窗口的末尾停止，請確保維護任務用戶介面中維護窗口的配置足夠大</li>
       <li>如果可用的堆記憶體不足，請確保實例具有足夠的記憶體。</li>
       <li>如果出現延遲反應，區段存放區可能會成長得太多，以致「線上修訂清除」無法在較長的維護期間內完成。 例如，如果上週未完成成功的線上修訂清除，則建議您規劃離線維護並執行離線修訂清除，以便將區段存放區恢復為可管理的大小。</li>
      </ul> </li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>開啟健康檢查警報後需要執行什麼？</strong></td>
   <td>請參閱前一點。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>如果「線上修訂清除」在排程的維護期間逾時，會發生什麼事？</strong></td>
   <td>將取消線上修訂清除，並刪除剩餘內容。 它將在下次計畫維護窗口時重新啟動。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>原因 <code>SegmentNotFoundException</code> 要登入的例項 <code>error.log</code> 如何恢復？</strong></td>
   <td><p>A <code>SegmentNotFoundException</code> 當TarMK嘗試存取找不到的儲存單元（區段）時，就會記錄。 有三種情況可能會導致此問題：</p>
    <ol>
     <li>規避建議存取機制（例如Sling和JCR API），並使用較低層級API/SPI存取存放庫，然後超過區段保留時間的應用程式。 也就是說，它會保留對實體的引用時間超過「線上修訂清除」允許的保留時間（預設為24小時）。 此案例為暫時性，不會導致資料損毀。 若要復原，應使用oak-run工具來確認例外狀況的暫時性質（oak-run檢查不應回報任何錯誤）。 為此，執行個體必須離線，然後重新啟動。</li>
     <li>外部事件導致磁碟上的資料損壞。 這可能是磁碟故障、磁碟空間不足或意外修改所需資料檔案。 在此情況下，執行個體需要離線，並使用oak-run檢查進行修復。 如需如何執行oak-run檢查的詳細資訊，請參閱下列內容 <a href="https://github.com/apache/jackrabbit-oak/blob/trunk/oak-doc/src/site/markdown/nodestore/segment/overview.md#check" target="_blank">Apache檔案</a>.</li>
     <li>所有其他發生次數皆應透過 <a href="https://helpx.adobe.com/tw/marketing-cloud/contact-support.html" target="_blank">Adobe客戶服務</a>.</li>
    </ol> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 根據錯誤訊息進行疑難排解 {#troubleshooting-based-on-error-messages}

如果線上修訂清除過程中發生事件，error.log將是詳細的。 下列矩陣旨在說明最常見的訊息並提供可能的解決方案：

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
    <th>記錄訊息</th>
    <th>解釋</th>
    <th>後續步驟</th>
  </tr>  
  <tr>
    <td>估計</td>
    <td>TarMK GC #2:因為壓縮已暫停，所以跳過估計。</td>
    <td>當通過配置在系統上禁用壓縮時，將跳過估計階段。</td>
    <td>啟用「線上修訂清除」。</td>
  </td>
  </tr>
  <tr>
    <td>N/A</td>
    <td>TarMK GC #2:估計中斷：${REASON}。 略過壓縮。</td>
    <td>估計階段提前終止。 可能會中斷估計階段的一些事件範例：主機系統上的記憶體或磁碟空間不足。</td>
    <td>這取決於特定原因。</td>
  </td>
  </tr>
  <tr>
    <td>壓實</td>
    <td>TarMK GC #2:壓縮已暫停。</td>
    <td>只要壓縮階段被配置暫停，則估計階段和壓縮階段都不會被執行。</td>
    <td>啟用線上修訂清除。</td>
  </td>
  </tr>
   <tr>
    <td>N/A</td>
    <td>TarMK GC #2:壓縮已取消：${REASON}。</td>
    <td>壓縮階段提前終止。 可能會中斷壓縮階段的事件範例：主機系統上的記憶體或磁碟空間不足。 此外，還可以通過關閉系統或通過管理介面（如操作儀表板中的維護窗口）顯式取消壓縮來取消壓縮。</td>
    <td>這取決於特定原因。</td>
  </td>
  </tr>
  <tr>
    <td>N/A</td>
    <td>TarMK GC #2:壓縮在5次循環後32.902分鐘(1974140毫秒)內失敗。</td>
    <td>此訊息不表示有無法復原的錯誤，但只有壓縮在經過特定嘗試後才會終止。 此外，請閱讀 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes">後面的段落。</a></td>
    <td>請閱讀以下內容 <a href="https://jackrabbit.apache.org/oak/docs/nodestore/segment/overview.html#how-does-compaction-works-with-concurrent-writes">Oak檔案</a>，以及執行線上修訂清除區段的最後一個問題。</a></td>
  </td>
  </tr>
  <tr>
    <td>清理</td>
    <td>TarMK GC #2:清理中斷。</td>
    <td>已通過關閉儲存庫取消清理。 預期不會影響一致性。 此外，磁碟空間很可能不會完全回收。 將在下一個修訂清除週期中回收。</td>
    <td>調查為何已關閉儲存庫，並在以後嘗試避免在維護窗口期間關閉儲存庫。</td>
  </td>
  </tr>
  </tbody>
</table>

## 如何執行離線修訂清除 {#how-to-run-offline-revision-cleanup}

>[!CAUTION]
>
>使用Oak執行工具版本，其版本號碼（主要和次要）符合AEM安裝的Oak核心版本。 例如，若您的AEM執行個體有Oak core 1.22.x版，則您應使用Oak-run工具1.22.x版。

Adobe提供以下工具： **Oak-run** 執行修訂清除。 可在下列位置下載：

[https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/](https://repo1.maven.org/maven2/org/apache/jackrabbit/oak-run/)

此工具是可執行的Jar，可手動執行以壓縮存放庫。 此程式稱為離線修訂清除，因為必須關閉存放庫才能正確執行工具。 請務必根據您的維護時段規劃清理。

有關如何提高清理過程效能的提示，請參閱 [提高離線修訂清除的效能](/help/sites-deploying/revision-cleanup.md#increasing-the-performance-of-offline-revision-cleanup).

>[!NOTE]
>
>您也可以在進行維護前清除舊查核點（以下程式中的步驟2和3）。 僅建議具有超過100個查核點的例項使用。

1. 請務必確認您最近有AEM例項的備份。

   關閉AEM。

1. （選用）使用工具尋找舊查核點：

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore
   ```

1. （選用）然後，刪除未參考的查核點：

   ```xml
   java -jar oak-run.jar checkpoints install-folder/crx-quickstart/repository/segmentstore rm-unreferenced
   ```

1. 執行壓縮並等待它完成：

   ```xml
   java -jar -Dsun.arch.data.model=32 oak-run.jar compact install-folder/crx-quickstart/repository/segmentstore
   ```

### 提高離線修訂清除的效能 {#increasing-the-performance-of-offline-revision-cleanup}

oak-run工具引入多項功能，旨在提升修訂清除程式的效能，並盡可能降低維護期間。

此清單包含數個命令列參數，如下所述：

* **-mmap。** 您可以將此值設為true或false。 如果設為true，則使用記憶體映射訪問。 若設為false，則會使用檔案存取。 如果未指定，則64位系統上將使用記憶體映射訪問，32位系統上使用檔案訪問。 在Windows上，一律會強制執行一般檔案存取，並忽略此選項。 **此參數已取代 — Dtar.memoryMapped參數。**

* **-Dupdate.limit**. 定義臨時事務到磁碟的刷新閾值。 預設值為 10000。

* **-Dcompress-interval**. 要保留直到壓縮當前映射為止的壓縮映射條目數。 預設為1000000。 如果有足夠的堆記憶體可用，則應將此值增加到更高的數字，以加快吞吐量。 **此參數已在Oak 1.6版中移除，且無效。**

* **-Dcompaction-progress-log**. 要記錄的壓縮節點數。 預設值為150000，這表示在操作期間將記錄150000個壓縮的節點。 請結合下列說明的下一個參數使用。

* **-Dtar.PersistCompactionMap。** 將此參數設為true ，以使用磁碟空間而非堆記憶體來保存壓縮映射。 需要oak-run工具 **版本1.4** 更高。 欲知更多詳情，請參閱 [離線修訂清除常見問題](/help/sites-deploying/revision-cleanup.md#offline-revision-cleanup-frequently-asked-questions) 區段。 **此參數已在Oak 1.6版中移除，且無效。**

* **— 力。** 強制壓縮並忽略非相符區段存放區版本。

>[!CAUTION]
>
>使用 `--force` 參數會將區段存放區升級至最新版本，與舊版Oak不相容。 此外，考慮到不可能降級。 一般來說，您應該小心使用這些參數，而且只有在您對如何使用這些參數有知識時才使用。

使用中參數的範例：

```xml
java -Dupdate.limit=10000 -Dcompaction-progress-log=150000 -Dlogback.configurationFile=logback.xml -Xmx8g -jar oak-run-*.jar checkpoints <repository>
```

### 觸發修訂清除的其他方法 {#additional-methods-of-triggering-revision-cleanup}

除了上述方法，您也可以使用JMX控制台觸發修訂清除機制，如下所示：

1. 開啟JMX控制台，請前往 [http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)
1. 按一下 **RevisionGarbageCollection** MBean。
1. 在下一個視窗中，按一下 **startRevisionGC()** 然後 **叫用** 以啟動修訂垃圾收集作業。

### 離線修訂清除常見問題 {#offline-revision-cleanup-frequently-asked-questions}

<table style="table-layout:auto">
 <tbody>
  <tr>
   <td><strong>決定離線修訂清除持續時間的因素有哪些？</strong></td>
   <td><p>需要清理的儲存庫大小和修訂的數量決定了清理的持續時間。</p> </td>
  </tr>
  <tr>
   <td><strong>修訂版本和頁面版本之間有何差異？</strong></td>
   <td>
    <ul>
     <li><strong>Oak修訂版：</strong> Oak以由節點和屬性組成的大型樹狀結構階層來組織所有內容。 此內容樹的每個快照或修訂都不可修改，對樹的更改將以新修訂的序清單示。 通常，每個內容修改都會觸發新修訂。 另請參閱 <a href="https://jackrabbit.apache.org/dev/ngp.html" target="_blank"> 追蹤連結</a>.</li>
     <li><strong>頁面版本：</strong> 版本設定會在特定時間點建立頁面的「快照」。 通常，頁面啟動時會建立新版本。 如需詳細資訊，請參閱 <a href="/help/sites-authoring/working-with-page-versions.md" target="_blank">使用頁面版本</a>.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>如果離線修訂清除任務在8小時內未完成，該如何加速？</strong></td>
   <td>如果修訂任務在8小時內未完成，且 <a href="/help/sites-administering/operations-dashboard.md#diagnosis-tools" target="_blank">線程轉儲</a> 主要熱點是 <code>InMemoryCompactionMap.findEntry</code>，搭配oak-run工具使用下列參數 <strong>版本1.4 </strong>或更高版本： <code>-Dtar.PersistCompactionMap=true</code>. 請注意， <code>-Dtar.PersistCompactionMap</code> 參數已在Oak 1.6版中移除。</td>
  </tr>
 </tbody>
</table>
