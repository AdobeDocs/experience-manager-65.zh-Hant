---
title: 排除複製故障
seo-title: Troubleshooting Replication
description: 本文提供了有關如何解決複製問題的資訊。
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

# 排除複製故障{#troubleshooting-replication}

此頁提供有關如何解決複製問題的資訊。

## 問題 {#problem}

複製（非反向複製）由於某種原因失敗。

## 解析度 {#resolution}

複製失敗有多種原因。 本文闡述了在分析這些問題時可能採取的方法。

**按一下「激活」按鈕時，複製是否已被觸發？ 如果NOT，則執行以下操作：**

1. 轉到/crx/explorer並以管理員身份登錄。
1. 開啟「內容瀏覽器」
1. 查看節點/bin/replicate或/bin/replicate.json是否存在。 如果節點存在，則刪除它並保存。

**複製是否正在在複製代理隊列中排隊？**

轉到/etc/replication/agents.author.html，然後按一下要檢查的複製代理，以檢查此項。

**如果一個代理隊列或幾個代理隊列被卡住：**

1. 隊列是否顯示 **阻止** 狀態？ 如果是，則發佈實例是否未運行或完全無響應？ 檢查發佈實例以查看它的問題(例如，檢查日誌，並查看是否存在OutOfMemory錯誤或其他問題。 然後，如果速度通常很慢，請提取線程轉儲並分析它們。
1. 隊列狀態是否顯示 **隊列處於活動狀態 — 掛起#**? 基本上，復製作業可能會卡在套接字讀取中，等待公開實例或調度程式作出響應。 這可能意味著發佈實例或調度程式負載較高或卡在鎖中。 從作者處獲取線程轉儲，並在此情況下發佈。

   * 線上程轉儲分析器中從作者開啟線程轉儲，檢查它是否顯示複製代理的sling事件作業卡在socketRead中。
   * 線上程轉儲分析器中從發佈中開啟線程轉儲，分析可能導致發佈實例不響應的原因。 您應看到名稱中包含POST/bin/receive的線程，該線程是從作者處接收複製的線程。

**如果所有代理隊列都被卡住**

1. 由於儲存庫損壞或其他問題，有可能無法在/var/replication/data下序列化某一內容。 查看logs/error.log中的相關錯誤。 要清除錯誤的複製項，請執行以下操作：

   1. 請訪問https://&lt;host>:&lt;port>/crx/de並以admin用戶身份登錄。
   1. 按一下頂部菜單中的「工具」。
   1. 按一下放大鏡按鈕。
   1. 選擇「XPath」作為「Type（類型）」。
   1. 在「查詢」框中，輸入此查詢/jcr:root/var/eventing/jobs//element(&#42;,slingevent:Job)順序(按@slingevent：已建立)
   1. 按一下「搜索」
   1. 在結果中，頂級項目是最新的懸索事件作業。 按一下每個副本，然後查找與隊列頂部顯示的匹配的停滯的複製。

1. 掛起事件框架作業隊列可能有問題。 嘗試在/system/console中重新啟動org.apache.sling.event包。
1. 可能是作業處理完全關閉。 您可以在「Sling Eventing（Sling事件）」頁籤的「Felix Console（Felix控制台）」下檢查。 檢查是否顯示 — Apache Sling事件(JOB PROCESSING IS DISABLED!)

   * 如果是，則在Felix控制台的「配置」頁籤下檢查Apache Sling作業事件處理程式。 可能是「已啟用作業處理」複選框未選中。 如果選中該選項，但仍顯示「作業處理已禁用」，則檢查/apps/system/config下是否存在正在禁用作業處理的覆蓋。 嘗試為jobmanager.enabled建立osgi:config節點，布爾值為true，然後重新檢查激活是否已啟動且隊列中沒有其他作業。

1. DefaultJobManager配置也可能處於不一致狀態。 當有人通過OSGiconsole手動修改「Apache Sling作業事件處理程式」配置（例如，禁用並重新啟用「Job Processing Enabled」屬性並保存配置）時，就會發生這種情況。

   * 此時，儲存在crx-quickstart/launchpad/config/org/apache/sling/event/impl/jobs/DefaultJobManager.config上的DefaultJobManager配置將進入不一致狀態。 即使「Apache Sling Job Event Handler」屬性顯示「已啟用作業處理」處於選中狀態，但當您導航到「Sling Eventing」頁籤時，該屬性仍顯示消息 — JOB PROCESSING IS DISABLED，且複製無效。
   * 要解決此問題，需要導航到OSGi控制台的「配置」頁並刪除「Apache Sling作業事件處理程式」配置。 然後重新啟動群集的主節點以使配置恢復為一致狀態。 這應該可以解決問題，複製將重新開始工作。

**建立replication.log**

有時，將所有複製日誌記錄都設定為在DEBUG級別的單獨日誌檔案中添加可能會非常有用。 要執行此操作：

1. 轉到https://host:port/system/console/configMgr並以管理員身份登錄。
1. 查找Apache Sling日誌記錄記錄器工廠，並通過按一下 **+** 按鈕。 這將建立新的日誌記錄記錄器。
1. 將配置設定為：

   * 日誌級別：調試
   * 日誌檔案路徑：logs/replication.log
   * 類別：com.day.cq.re複製

1. 如果您懷疑此問題與sling事件/作業有任何關係，則還可以在categories:org.apache.sling.event下添加此java包

## 暫停複製代理隊列  {#pausing-replication-agent-queue}

有時，可以暫停複製隊列以減少作者系統上的負載，而不禁用它。 目前，只有臨時配置無效埠的駭客攻擊才可能做到這一點。 從5.4開始，您可以看到複製代理隊列中的暫停按鈕，它有一些限制

1. 該狀態未永續，這意味著如果重新啟動伺服器或複製包被循環使用，它將恢復為運行狀態。
1. 暫停在較短的時間段內（OOB在沒有其他線程複製的活動後1小時）處於空閒狀態，而在較長的時間內處於空閒狀態。 因為吊具中有避免空閒線程的特徵。 基本上，檢查作業隊列線程是否已使用較長時間，如果這樣，則啟動清理週期。 由於清理週期，它會停止線程，因此暫停的設定將丟失。 由於作業被保留，因此啟動新線程以處理沒有暫停配置詳細資訊的隊列。 由於此隊列變為運行狀態。

## 未在用戶激活時複製頁面權限 {#page-permissions-are-not-replicated-on-user-activation}

不複製頁面權限，因為這些權限儲存在授予訪問權限的節點下，而不是與用戶一起。

一般情況下，不應將權限從作者複製到發佈，預設情況下不應複製。 這是因為訪問權限在這兩種環境中應該不同。 因此，建議在發佈時與作者分開配置ACL。

## 將命名空間資訊從「作者」複製到「發佈」時，複製隊列被阻止 {#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}

在某些情況下，當嘗試將命名空間資訊從作者實例複製到發佈實例時，複製隊列將被阻止。 這是因為複製用戶沒有 `jcr:namespaceManagement` 權限。 要避免此問題，請確保：

* 複製用戶(如在 [運輸](/help/sites-deploying/replication.md#replication-agents-configuration-parameters) 頁籤>用戶)也存在於發佈實例中。
* 用戶在安裝內容的路徑上具有讀寫權限。
* 用戶具有 `jcr:namespaceManagement` 權限。 您可以按如下方式授予權限：

1. 登錄CRX/DE( `https://localhost:4502/crx/de/index.jsp`)。
1. 按一下 **訪問控制** 頁籤。
1. 選擇 **儲存庫**。
1. 按一下 **添加條目** （加號）。
1. 輸入用戶名。
1. 選擇 `jcr:namespaceManagement` 從權限清單中。
1. 按一下「確定」。
