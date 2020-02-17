---
title: 複製故障排除
seo-title: 複製故障排除
description: 本文提供了有關如何排除複製問題的資訊。
seo-description: 本文提供了有關如何排除複製問題的資訊。
uuid: 1662bf60-b000-4eb2-8834-c6da607128fe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 0d055be7-7189-4587-8c7c-2ce34e22a6ad
docset: aem65
translation-type: tm+mt
source-git-commit: 38ef8fc8d80009c8ca79aca9e45cf10bd70e1f1e

---


# 複製故障排除{#troubleshooting-replication}

本頁提供了有關如何排除複製問題的資訊。

## 問題 {#problem}

複製（非反向複製）因某些原因而失敗。

## 解析度 {#resolution}

複製失敗有各種原因。 本文就這些問題的分析作了說明。

**按一下「激活」按鈕時，複製是否會觸發？ 如果NOT，請執行下列動作：**

1. 前往/crx/explorer並以管理員身分登入。
1. 開啟「內容總管」
1. 查看節點/bin/replicate或/bin/replicate.json是否存在。 如果節點存在，請刪除它並保存。

**複製是否在複製代理隊列中排隊？**

請前往/etc/replication/agents.author.html，然後按一下複製代理以檢查，以檢查此項。

**如果一個代理隊列或幾個代理隊列被卡住：**

1. 佇列是否顯示已 **封鎖** 狀態？ 如果是，則發佈執行個體是否未執行或完全沒有回應？ 檢查發佈實例以查看其中有什麼問題(例如，檢查日誌，並查看是否存在OutOfMemory錯誤或其他問題。 然後，如果執行緒轉儲通常很慢，請提取線程轉儲並分析它們。
1. 佇列狀態是否顯示「佇 **列為作用中- # pending**?」 基本上，復製作業可能會卡在套接字讀取中，等待pubilsh實例或調度程式作出響應。 這可能表示發佈實例或調度程式處於高負載狀態或卡在鎖中。 從作者處取出執行緒轉儲，並在此案例中發佈。

   * 線上程轉儲分析器中從author開啟線程轉儲，檢查它是否顯示複製代理的sling事件作業卡在套接字讀取中。
   * 線上程轉儲分析器中從發佈開啟線程轉儲，分析可能導致發佈實例不響應的原因。 您應看到名稱中包含POST /bin/receive的線程，即從作者處接收複製的線程。

**如果所有代理隊列都被卡住**

1. 由於儲存庫損壞或某些其他問題，某段內容可能無法在/var/replication/data下序列化。 檢查logs/error.log中是否有相關錯誤。 要清除錯誤的複製項，請執行以下操作：

   1. 前往https://&lt;host>:&lt;port>/crx/de，並以管理員使用者身分登入。
   1. 按一下頂端選單中的「工具」。
   1. 按一下放大鏡按鈕。
   1. 選擇「XPath」作為「類型」。
   1. 在「查詢」方塊中，輸入@slingevent:created的查詢/jcr:root/var/eventing/jobs//element(*,slingevent:Job)順序
   1. 按一下「搜尋」
   1. 在結果中，排名最前的項目是最新的sling事件工作。 按一下每個複製，查找與隊列頂部顯示的副本匹配的停滯複製。

1. sling事件架構工作佇列可能有問題。 嘗試在/system/console中重新啟動org.apache.sling.event套件。
1. 可能是工作處理完全關閉。 您可以在Felix Console的Sling Eventing tab下檢查此項目。 檢查是否顯示- Apache Sling Eventing(JOB PROCESSING IS DISABLED!)

   * 如果是，請在Felix Console的「設定」標籤下檢查Apache Sling Job Event Handler。 可能是未勾選「作業處理已啟用」核取方塊。 如果已勾選，但仍顯示「作業處理已停用」，則請檢查/apps/system/config下是否有任何覆蓋正在停用作業處理。 嘗試為jobmanager.enabled建立一個osgi:config節點，將布爾值設定為true，然後重新檢查啟動是否開始以及隊列中沒有更多作業。

1. DefaultJobManager配置也可能進入不一致狀態。 當某人透過OSGiconsole手動修改「Apache Sling Job Event Handler」設定時，就會發生這種情況（例如，停用並重新啟用「Job Processing Enabled」屬性，並儲存設定）。

   * 此時，儲存於crx-quickstart/launchpad/config/org/apache/sling/event/impl/jobs/DefaultJobManager.config的DefaultJobManager設定會進入不一致狀態。 即使「Apache Sling Job Event Handler」屬性顯示「Job Processing Enabled」為勾選狀態，當有人導覽至Sling Eventing標籤時，也會顯示訊息- JOB PROCESSING IS DISABLED，而複製不會運作。
   * 若要解決此問題，您必須導覽至OSGi主控台的「設定」頁面，並刪除「Apache Sling Job Event Handler」設定。 然後重新啟動群集的主節點，使配置恢復到一致狀態。 這應該會修正問題，複製將重新開始運作。

**建立replication.log**

有時，將所有複製記錄設定為在DEBUG級別的單獨日誌檔案中添加，會非常有用。 要執行此操作：

1. 前往https://host:port/system/console/configMgr，以管理員身分登入。
1. 尋找Apache Sling Logging Logger工廠，並按一下工廠組態右側的 **+** button建立例項。 This will create a new logging logger.
1. 將配置設定為如下：

   * 記錄層級：除錯
   * 日誌檔案路徑：logs/replication.log
   * 類別：com.day.cq.replication

1. 如果您懷疑問題與sling eventing/jobs有任何關聯，則您也可以將此java套件新增至categories:org.apache.sling.event

## 暫停複製代理隊列 {#pausing-replication-agent-queue}

有時，可以暫停複製隊列以減少作者系統上的負載，而不禁用它。 目前，只有通過臨時配置無效埠的攻擊才能做到這一點。 從5.4開始，您可以在複製代理隊列中看到暫停按鈕，它有一些限制

1. 狀態不會持續存在，這表示如果重新啟動伺服器或複製捆綁包被循環使用，它將返回運行狀態。
1. 暫停在較短的時間段（OOB在沒有其他線程複製的活動後1小時）內處於空閒狀態，而不是在較長的時間內。 因為吊具中有可避免閒置線程的功能。 基本上，檢查作業隊列線程是否已被使用較長時間，如果這樣，它將啟動清理週期。 由於清理週期，它會停止線程，因此暫停的設定將丟失。 由於作業是持續的，因此會啟動新線程來處理沒有暫停配置詳細資訊的隊列。 由於此隊列變為運行狀態。

## 使用者啟動時不會複製頁面權限 {#page-permissions-are-not-replicated-on-user-activation}

頁面權限不會複製，因為這些權限會儲存在授予存取權的節點下，而不是儲存在使用者下。

一般而言，頁面權限不應從作者複製以發佈，而且預設不會複製。 這是因為這兩種環境中的存取權限應該不同。 因此，建議在發佈時與作者分開配置ACL。

## 從「作者」複製命名空間資訊到「發佈」時，複製隊列被阻止 {#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}

在某些情況下，當嘗試將命名空間資訊從作者實例複製到發佈實例時，複製隊列會被阻止。 這是因為複製用戶沒有權 `jcr:namespaceManagement` 限。 若要避免此問題，請確定：

* 複製用戶(如「傳輸」頁籤>「用 [戶」下配置的](/help/sites-deploying/replication.md#replication-agents-configuration-parameters) )也存在於「發佈」實例上。
* 用戶在安裝內容的路徑上具有讀寫權限。
* 用戶在存 `jcr:namespaceManagement` 儲庫級別具有權限。 您可以按如下方式授予權限：

1. 以管理員身份登錄到CRX/DE( `https://localhost:4502/crx/de/index.jsp`)。
1. 按一下「存 **取控制** 」標籤。
1. 選擇 **儲存庫**。
1. 按一 **下「新增項目** 」（加號圖示）。
1. 輸入用戶的名稱。
1. 從權 `jcr:namespaceManagement` 限清單中選擇。
1. 按一下「確定」。

