---
title: Work Manager和限制
seo-title: Work Manager and throttling
description: 本文檔提供了有關Work Manager的背景資訊，並提供了有關配置Work Manager限制選項的說明。
seo-description: This document provides background information on Work Manager, and provides instructions on configuring Work Manager throttling options.
uuid: b90998bc-e3d4-493a-9371-55ccb44da20d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9a8b4e3a-f416-4dc6-a90a-9018df5c844e
exl-id: 1f765de2-1362-4318-9302-c5036e6fa7d6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 0%

---

# Work Manager和限制{#work-manager-and-throttling}

AEM表單（及舊版）使用JMS佇列，以非同步方式執行操作。 在AEM表單中，JMS隊列已被Work Manager替換。 本文檔提供了有關Work Manager的背景資訊，並提供了有關配置Work Manager限制選項的說明。

## 關於長期（非同步）操作 {#about-long-lived-asynchronous-operations}

在AEM表單中，由服務執行的操作可以是短期（同步）操作，也可以是長期（非同步）操作。 短期操作在調用它們的同一線程上同步完成。 這些操作會等待回應，然後繼續。

長期運營可能跨越系統，甚至延伸到組織之外，例如客戶必須完成並提交貸款申請表，作為整合多個自動化和人力任務的更大解決方案的一部分。 在等待回應時，此類行動必須繼續。 長期作業以非同步方式執行其基礎工作，允許在等待完成時以其他方式參與資源。 與短期操作不同，一旦調用了長期操作，Work Manager就不會將其視為長期操作完成。 必須發生外部觸發器，例如在同一服務上請求另一操作的系統或提交表單的用戶，才能完成操作。

## 關於工作管理員 {#about-work-manager}

AEM表單（及舊版）使用JMS佇列，以非同步方式執行操作。 AEM forms使用Work Manager來排程及執行透過受管理的執行緒的非同步操作。

非同步操作的處理方式如下：

1. 工作經理接收要執行的工作項。
1. Oracle Work Manager將工作項儲存在資料庫表中，並為工作項分配唯一標識符。 資料庫記錄包含執行工作項所需的所有資訊。
1. 當線程空閒時，Work Manager線程將拉入工作項。 在提取工作項之前，線程可以檢查所需的服務是否已啟動、是否有足夠的堆大小來提取下一個工作項，以及是否有足夠的CPU週期來處理工作項。 Work Manager在計畫工作項的執行時，也會評估工作項的屬性（如其優先順序）。

AEM Forms管理員可以使用運行狀況監視器來檢查Work Manager統計資訊，如隊列中的工作項數及其狀態。 您也可以使用「運行狀況監視器」來暫停、繼續、重試或刪除工作項。 (請參閱 [查看與Work Manager相關的統計資訊](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)

## 配置Work Manager調節選項 {#configuring-work-manager-throttling-options}

您可以為Work Manager配置限制，以便只在有足夠的記憶體資源可用時才計畫工作項。 通過在應用程式伺服器中設定以下JVM選項，可以配置節流。

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
   <td><p>指定Work Manager在其隊列中檢查新項目時使用的時間間隔（以毫秒為單位）。</p><p>此選項的值是整數。 預設值為 <code>1000</code> 毫秒（1秒）。 </p><p>如果非同步叫用的數量較少，您可以增加此值。 例如，您可將其增加至2000到5000（2到5秒）之間。 </p><p>如果非同步叫用的量很大，預設值應該足夠，但您可以視需要使用較低的值。 將此值減少太多（例如，低於50，導致輪詢頻率為每秒20次），會導致系統產生大量開銷。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.debug-mode-enabled</code></td>
   <td><p>將此選項設定為 <code>true</code> 啟用偵錯模式，或設為false以停用。 </p><p>在調試模式下，將記錄有關Work Manager策略違規和Work Manager暫停/恢復操作的消息。 只有在進行疑難排解時，才將此選項設為true。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.enabled</code></td>
   <td><p>將此選項設定為 <code>true</code> 根據下面所述的記憶體控制設定啟用限制，或 <code>false</code> 禁用限制。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.high-limit</code></td>
   <td><p>指定在Work Manager限制傳入的作業之前，可以使用的記憶體的最大百分比。</p><p>此選項的預設值為 <code>95</code>. 此值在大部分系統中都可用。 僅在您的系統需要達到最大容量時才增加它。 但請注意，隨著您增加此值，記憶體不足問題的風險也會增加。</p><p>如果您在群集環境中運行AEM表單，則可能希望在群集的不同節點上以不同方式設定記憶體控制限制設定。 例如，您可以對節點A和B設定較低的高限制，這些節點在您的負載平衡器中寫程式，以便進行互動式工作。 而且，節點C和D上設定的高限值可以更高，這些不被負載平衡器使用，而是保留用於非同步工作。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.low-limit</code></td>
   <td><p>指定在Work Manager停止限制傳入的作業之前，可使用的記憶體的最大百分比。</p><p>此選項的預設值為 <code>20</code>. 此值在大部分系統中都可用。</p></td>
  </tr>
  <tr>
   <td><code>Dadobe.workmanager.allocate.max-batch-size</code></td>
   <td><p>指定Workmanager的最大批大小。 預設批大小為10。</p><p>如果工作管理器中的進程狀態在任務完成後也未更新，則將批大小設定為1。</p></td>
  </tr>
 </tbody>
</table>

**將Java選項新增至JBoss**

1. 停止JBoss應用程式伺服器。
1. 開啟 *[appserver根]*/bin/run.bat(Windows)或run.sh（Linux或UNIX），並視需要以格式新增任何Java選項 `-Dproperty=value`.
1. 重新啟動伺服器。

**將Java選項新增至WebLogic**

1. 輸入 `https://[host name]:[port]/console` 在網頁瀏覽器中。
1. 鍵入您為WebLogic Server域建立的用戶名和密碼，然後按一下更改中心下的日誌，按一下鎖定和編輯。
1. 在「域結構」下，按一下「環境」>「伺服器」，然後在右窗格中按一下受控伺服器名稱。
1. 在下一個畫面中，按一下「設定」標籤>「伺服器開始」標籤。
1. 在「參數」框中，將所需的參數附加到當前內容的結尾。 例如，要禁用運行狀況監視器，請添加：

   `-Dadobe.healthmonitor.enabled=false` 禁用運行狀況監視器。

1. 按一下「儲存」，然後按一下「啟動變更」。
1. 重新啟動WebLogic托管伺服器。

**將Java選項添加到WebSphere**

1. 在WebSphere管理控制台導航樹中，按一下「伺服器」>「伺服器類型」>「WebSphere應用程式伺服器」。
1. 在右窗格中，按一下伺服器名稱。
1. 在「伺服器基礎架構」下，按一下「Java和表單工作流」>「流程定義」。
1. 在「其他屬性」下，按一下「Java虛擬機」。
1. 在「一般JVM參數」框中，鍵入所需參數。
1. 按一下「確定」或「應用」，然後按一下「直接保存到主配置」。
