---
title: 工作管理員和節流
description: 本檔案提供Work Manager的背景資訊，以及設定Work Manager節流選項的說明。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1f765de2-1362-4318-9302-c5036e6fa7d6
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 0%

---

# 工作管理員和節流{#work-manager-and-throttling}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

AEM forms （及舊版）使用JMS佇列來非同步執行操作。 在AEM表單中，JMS佇列已由工作管理員取代。 本檔案提供Work Manager的背景資訊，以及設定Work Manager節流選項的說明。

## 關於長期（非同步）操作 {#about-long-lived-asynchronous-operations}

在AEM Forms中，服務執行的作業可能是短期（同步）或長期（非同步）。 短期作業會在從中叫用的相同執行緒上同步完成。 這些作業會等待回應再繼續。

長期作業可能橫跨系統，甚至可能延伸到組織之外，例如，客戶必須完成並提交貸款申請表，作為整合多項自動化和人為作業的較大解決方案的一部分。 在等待回應的同時，這類作業必須繼續。 長期作業以非同步方式執行其基礎工作，允許資源在等待完成時以其他方式參與。 不同於短期作業，「工作管理員」在叫用長期作業時，不會將其視為已完成。 必須發生外部觸發程式（例如要求相同服務上進行其他作業的系統或提交表單的使用者）才能完成作業。

## 關於工作管理員 {#about-work-manager}

AEM forms （及舊版）使用JMS佇列來非同步執行操作。 AEM Forms會使用工作管理器，透過受管理的執行緒來排程及執行非同步作業。

非同步操作的處理方式如下：

1. 工作管理員接收要執行的工作專案。
1. Work Manager會將工作專案儲存在資料庫表格中，並將唯一識別碼指派給工作專案。 資料庫記錄包含執行工作專案所需的所有資訊。
1. 當執行緒變成可用狀態時，工作管理員執行緒會拉入工作專案。 提取工作專案之前，執行緒可以檢查所需的服務是否已啟動、是否有足夠的棧積大小可提取下一個工作專案，以及是否有足夠的CPU週期可處理工作專案。 Work Manager也會在排程其執行時評估工作專案的屬性（例如其優先順序）。

AEM Forms管理員可以使用「健康情況監視」來檢查Work Manager統計資料，例如佇列中的工作專案數量及其狀態。 您也可以使用「健全狀態監視器」來暫停、繼續、重試或刪除工作專案。 （請參閱[檢視與工作管理員相關的統計資料](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager)。）

## 設定Work Manager節流選項 {#configuring-work-manager-throttling-options}

您可以為工作管理員設定節流，以便只有在有足夠的可用記憶體資源時才會排程工作專案。 若要設定節流，請在應用程式伺服器中設定下列JVM選項。

<table>
 <thead>
  <tr>
   <th><p>屬性</p></th>
   <th><p>說明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code> adobe.work-manager.queue-refill-interval</code></td>
   <td><p>指定Work Manager檢查其佇列中新專案時使用的時間間隔（毫秒）。</p><p>此選項的值是整數。 預設值為<code>1000</code>毫秒（1秒）。 </p><p>如果非同步叫用的數量很低，您可以增加此值。 例如，您可以將其增加到2000到5000 （2-5秒）之間的某個值。 </p><p>如果非同步叫用的數量很高，預設值應該就足夠了，但您可以視需要使用較低的值。 過多地減少這個值（例如，低於50，會導致輪詢頻率為每秒20次）會導致系統產生大量的額外負荷。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.debug-mode-enabled</code></td>
   <td><p>將此選項設為<code>true</code>以啟用偵錯模式，或設為false以停用它。 </p><p>在偵錯模式中，會記錄關於Work Manager原則違規和Work Manager暫停/恢復動作的訊息。 只有在疑難排解時才會將此選項設定為true。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.enabled</code></td>
   <td><p>將此選項設為<code>true</code>以根據下列所述的記憶體控制設定啟用節流，或設為<code>false</code>以停用節流。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.high-limit</code></td>
   <td><p>指定工作管理員限制內送工作之前，可以使用的最大記憶體百分比。</p><p>此選項的預設值為<code>95</code>。 這個值在大部分的系統上應該都可以。 只有在您的系統需要推進到其最大容量時才增加它。 但請注意，隨著您增加此值，記憶體不足問題的風險也會增加。</p><p>如果您在叢集環境中執行AEM表單，您可能想要在叢集的不同節點上以不同方式設定記憶體控制限制設定。 例如，節點A和B的上限可能較低，這些節點會在您的負載平衡器中程式設計以用於互動式工作。 而且，您可以在節點C和D上設定較高的上限，負載平衡器不會使用這些上限，但會將其保留給非同步工作。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.low-limit</code></td>
   <td><p>指定工作管理員停止限制內送工作之前，可以使用的最大記憶體百分比。</p><p>此選項的預設值為<code>20</code>。 這個值在大部分的系統上應該都可以。</p></td>
  </tr>
  <tr>
   <td><code>Dadobe.workmanager.allocate.max-batch-size</code></td>
   <td><p>指定Workmanager的批次大小上限。 預設批次大小為10。</p><p>如果即使在任務完成後，Workmanager中的流程狀態也未更新，則將批次大小設定為1。</p></td>
  </tr>
 </tbody>
</table>

**新增Java選項至JBoss**

1. 停止JBoss應用程式伺服器。
1. 在編輯器中開啟&#x200B;*[appserver root]*/bin/run.bat (Windows)或run.sh （Linux或UNIX），並視需要新增任何Java選項，格式為`-Dproperty=value`。
1. 重新啟動伺服器。

**新增Java選項至WebLogic**

1. 在網頁瀏覽器中輸入`https://[host name]:[port]/console`，啟動WebLogic管理主控台。
1. 輸入您為WebLogic Server網域建立的使用者名稱和密碼，然後按一下「變更中心」下的「記錄」，再按一下「鎖定與編輯」。
1. 在「網域結構」下，按一下「環境>伺服器」，然後在右窗格中按一下Managed伺服器名稱。
1. 在下一個畫面中，按一下「組態」標籤>「伺服器啟動」標籤。
1. 在「引數」方塊中，將所需的引數附加至目前內容的結尾。 例如，若要停用健康情況監視，請新增：

   `-Dadobe.healthmonitor.enabled=false`停用健康狀態監視。

1. 按一下儲存，然後按一下啟動變更。
1. 重新啟動WebLogic管理的伺服器。

**新增Java選項至WebSphere**

1. 在「WebSphere管理主控台」導覽樹狀結構中，按一下「伺服器」>「伺服器型別」>「WebSphere應用程式伺服器」。
1. 在右窗格中，按一下伺服器名稱。
1. 在「伺服器基礎結構」下，按一下「Java和表單工作流程>程式定義」。
1. 在「其他屬性」下，按一下「Java虛擬機器器」。
1. 在「一般JVM引數」方塊中，輸入所需的引數。
1. 按一下「確定」或「套用」，然後按一下「直接儲存至主組態」。
