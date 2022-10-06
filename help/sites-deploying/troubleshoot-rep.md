---
title: 疑難排解復寫
seo-title: Troubleshooting Replication
description: 本文提供如何疑難排解復寫問題的資訊。
seo-description: This article provides information on how to troubleshoot replication issues.
uuid: 1662bf60-b000-4eb2-8834-c6da607128fe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 0d055be7-7189-4587-8c7c-2ce34e22a6ad
docset: aem65
feature: Configuring
exl-id: cfa822c8-f9a9-4122-9eac-0293d525f6b5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1243'
ht-degree: 0%

---

# 疑難排解復寫{#troubleshooting-replication}

本頁面提供如何疑難排解復寫問題的資訊。

## 問題 {#problem}

復寫（非反向復寫）因某些原因而失敗。

## 解析度 {#resolution}

複製失敗有多種原因。 本文說明分析這些問題時可能採取的方法。

**按一下「激活」按鈕時，複製是否完全觸發？ 若非，則執行下列動作：**

1. 前往/crx/explorer並以管理員身分登入。
1. 開啟「Content Explorer」
1. 查看節點/bin/replicate或/bin/replicate.json是否存在。 如果節點存在，請刪除該節點並保存。

**複製是否在複製代理隊列中排隊？**

請前往/etc/replication/agents.author，然後按一下復寫代理以檢查，以檢查此項目。

**如果一個代理隊列或幾個代理隊列被卡住：**

1. 佇列是否顯示 **已阻止** 狀態？ 如果是，則發佈執行個體是否未執行或完全停止回應？ 檢查發佈執行個體以查看其有何錯誤（亦即檢查記錄，並查看是否有OutOfMemory錯誤或其他問題）。 如果速度通常很慢，請提取線程轉儲並分析它們。
1. 佇列狀態是否顯示 **隊列處於活動狀態 — 待處理數量**? 基本上，復寫工作可能卡在通訊端讀取中，等待發佈執行個體或調度程式回應。 這可能表示發佈執行個體或調度程式負載高或卡在鎖中。 從作者取用執行緒轉儲，並在此情況下發佈。

   * 在執行緒傾印分析器中，從作者開啟執行緒傾印，檢查是否顯示復寫代理的sling事件工作卡在socketRead中。
   * 在執行緒傾印分析器中從發佈開啟執行緒傾印，分析可能導致發佈執行個體未回應的因素。 您應該會看到名稱中包含/bin/receivePOST的執行緒，即接收來自作者之復寫的執行緒。

**如果所有代理隊列都卡住**

1. 由於存放庫損毀或其他問題，某個內容片段可能無法在/var/replication/data底下序列化。 檢查logs/error.log中是否有相關錯誤。 要清除錯誤的複製項，請執行以下操作：

   1. 前往https://&lt;host>:&lt;port>/crx/de ，並以管理員使用者身分登入。
   1. 按一下頂端功能表中的「工具」。
   1. 按一下放大鏡按鈕。
   1. 選擇「XPath」作為「類型」。
   1. 在「查詢」框中，輸入此查詢/jcr:root/var/eventing/jobs//element(&#42;,slingevent:Job)順序(@slingevent:created
   1. 按一下「搜尋」
   1. 在結果中，排名最前的項目是最新的Sling事件工作。 按一下每個，然後找到與隊列頂部顯示的內容相匹配的停滯複製。

1. Sling事件架構工作佇列可能有問題。 嘗試在/system/console中重新啟動org.apache.sling.event套件組合。
1. 可能是作業處理完全關閉。 您可以在Sling事件標籤的Felix Console底下查看。 檢查是否顯示 — Apache Sling事件（已停用作業處理！）

   * 如果是，請在Felix Console的「設定」標籤下檢查Apache Sling Job Event Handler。 「已啟用作業處理」核取方塊未勾選。 如果已勾選，但仍顯示「作業處理已停用」，則檢查/apps/system/config底下是否有任何覆蓋正在停用作業處理。 請嘗試為jobmanager.enabled建立一個osgi:config節點，將布爾值設為true，然後重新檢查啟動是否開始以及隊列中沒有其他作業。

1. DefaultJobManager配置也可能進入不一致狀態。 當有人透過OSGiconsole手動修改「Apache Sling Job Event Handler」設定（例如，停用並重新啟用「Job Processing Enabled」屬性並儲存設定）時，就會發生此情況。

   * 此時，儲存在crx-quickstart/launchpad/config/org/apache/sling/event/impl/jobs/DefaultJobManager.config的DefaultJobManager設定會進入不一致狀態。 即使「Apache Sling Job Event Handler」屬性顯示「已啟用作業處理」為已勾選狀態，當您導覽至Sling Eventing標籤時，仍會顯示訊息 — JOB PROCESSING IS DISABLED，且復寫無法運作。
   * 若要解決此問題，您必須導覽至OSGi主控台的「設定」頁面，並刪除「Apache Sling Job Event Handler」設定。 然後重新啟動群集的主節點，使配置恢復為一致狀態。 這應該會修正問題，復寫將會重新開始運作。

**建立replication.log**

有時，將所有復寫記錄設定為在DEBUG層級的個別記錄檔中新增，會很有幫助。 要執行此操作：

1. 前往https://host:port/system/console/configMgr並以管理員身分登入。
1. 尋找Apache Sling Logging Logger工廠，並按一下 **+** 按鈕（位於工廠配置右側）。 這將建立新的記錄器。
1. 以下列方式設定設定：

   * 記錄層級：除錯
   * 日誌檔案路徑：logs/replication.log
   * 類別：com.day.cq.replication

1. 如果您懷疑問題與sling事件/工作有任何關係，您也可以在categories:org.apache.sling.event下新增此java套件

## 暫停複製代理隊列  {#pausing-replication-agent-queue}

有時候，暫停復寫佇列以減少製作系統的負載，而不停用它可能比較合適。 目前，只有通過臨時配置無效埠的駭客攻擊才能做到這一點。 從5.4開始，您可以在復寫代理佇列中看到暫停按鈕，但有一些限制

1. 狀態不會持續，這表示如果重新啟動伺服器或復寫套件組合已循環，則會回復為執行狀態。
1. 暫停的空閒時間較短（在沒有其他線程進行複製的活動後1小時，OOB），而不是更長的時間。 因為Sling中有可避免閒置執行緒的功能。 基本上，檢查作業隊列線程是否已被長時間未使用，如果這樣，它將啟動清理週期。 由於清理週期，它會停止線程，因此暫停的設定會丟失。 由於作業持續存在，它會啟動一個新線程來處理隊列，該隊列沒有暫停配置的詳細資訊。 由於此佇列會變成執行狀態。

## 使用者啟動時不會複製頁面權限 {#page-permissions-are-not-replicated-on-user-activation}

不會複製頁面權限，因為這些權限儲存在授予存取權的節點下，而不是與使用者一起。

一般頁面權限不應從作者複製到發佈，且預設不會。 這是因為這兩個環境中的存取權限應該不同。 因此，建議您在發佈時與作者分開設定ACL。

## 將命名空間資訊從製作複製到發佈時，復寫佇列遭封鎖 {#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}

在某些情況下，嘗試將命名空間資訊從製作例項複製到發佈例項時，復寫佇列會遭到封鎖。 發生此情況是因為復寫使用者沒有 `jcr:namespaceManagement` 權限。 若要避免此問題，請確定：

* 復寫使用者(如 [運輸](/help/sites-deploying/replication.md#replication-agents-configuration-parameters) 標籤>使用者)也存在於發佈執行個體上。
* 用戶在安裝內容的路徑上具有讀寫權限。
* 使用者已 `jcr:namespaceManagement` 權限。 您可以依照下列方式授予權限：

1. 登入CRX/DE( `https://localhost:4502/crx/de/index.jsp`)為管理員。
1. 按一下 **存取控制** 標籤。
1. 選擇 **存放庫**.
1. 按一下 **添加條目** （加號圖示）。
1. 輸入使用者名稱。
1. 選擇 `jcr:namespaceManagement` 從權限清單中。
1. 按一下「確定」。
