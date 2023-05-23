---
title: 工作經理和限制
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

# 工作經理和限制{#work-manager-and-throttling}

表AEM單（和早期版本）使用JMS隊列非同步執行操作。 在表AEM單中，JMS隊列已被Work Manager替換。 本文檔提供了有關Work Manager的背景資訊，並提供了有關配置Work Manager限制選項的說明。

## 關於長期（非同步）操作 {#about-long-lived-asynchronous-operations}

在形AEM式中，由服務執行的操作可以是短期（同步）或長期（非同步）。 短期操作在調用它們的同一線程上同步完成。 這些操作在繼續之前等待響應。

長期運營可能會跨越系統，甚至延伸到組織之外，例如，客戶必須完成並提交貸款申請表，作為整合多個自動化和人工任務的較大解決方案的一部分。 這些行動必須在等待答復時繼續。 長期業務非同步執行其基礎工作，允許資源在等待完成時以其他方式參與。 與短期操作不同，一旦調用長期操作，Oracle Work Manager就不會認為長期操作已完成。 必須出現外部觸發器，例如請求對同一服務進行其他操作的系統或提交表單的用戶，才能完成該操作。

## 關於工作經理 {#about-work-manager}

表AEM單（和早期版本）使用JMS隊列非同步執行操作。 表AEM單使用Work Manager通過托管線程計畫和執行非同步操作。

非同步操作以下方式處理：

1. 工作管理器接收要執行的工作項。
1. Work Manager將工作項儲存在資料庫表中，並為工作項分配唯一標識符。 資料庫記錄包含執行工作項所需的所有資訊。
1. 當線程空閒時，Work Manager線程將導入工作項。 在拉入工作項之前，線程可以檢查是否啟動了所需的服務、是否有足夠的堆大小以拉入下一個工作項，以及是否有足夠的CPU週期來處理該工作項。 Oracle Work Manager在計畫工作項的執行時還會評估工作項的屬性（如其優先順序）。

表AEM單管理員可以使用運行狀況監視器來檢查Work Manager統計資訊，如隊列中的工作項數及其狀態。 您還可以使用運行狀況監視器暫停、恢復、重試或刪除工作項。 (請參閱 [查看與Work Manager相關的統計資訊](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager)。)

## 配置Work Manager限制選項 {#configuring-work-manager-throttling-options}

您可以為Work Manager配置限制，以便只有在有足夠記憶體資源可用時才計畫工作項。 通過在應用程式伺服器中設定以下JVM選項來配置限制。

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
   <td><p>指定Work Manager在其隊列中檢查新項目時使用的時間間隔（毫秒）。</p><p>此選項的值為整數。 預設值為 <code>1000</code> 毫秒（1秒）。 </p><p>如果非同步調用的數量較少，則可以增加此值。 例如，您可以將其增加到2000到5000（2到5秒）之間。 </p><p>如果非同步調用的卷數較高，則預設值應足夠，但是，如有必要，您可以使用較低的值。 將此值減少太多（例如，低於50，導致輪詢頻率為每秒20次），會在系統上造成大量開銷。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.debug-mode-enabled</code></td>
   <td><p>將此選項設定為 <code>true</code> 啟用調試模式，或禁用為false。 </p><p>在調試模式下，將記錄有關Work Manager策略違規和Work Manager暫停/恢復操作的消息。 僅當進行故障排除時，才將此選項設定為true。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.enabled</code></td>
   <td><p>將此選項設定為 <code>true</code> 根據下面所述的記憶體控制設定啟用限制，或 <code>false</code> 禁用限制。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.high-limit</code></td>
   <td><p>指定在Work Manager限制傳入的作業之前可以使用的記憶體的最大百分比。</p><p>此選項的預設值為 <code>95</code>。 對於大多數系統，此值應是合適的。 僅當您的系統需要將其推入到最大容量時才增加它。 但請注意，隨著此值的增加，記憶體不足問題的風險也會增加。</p><p>如果您在群集AEM環境中運行表單，您可能希望在群集的不同節點上以不同方式設定記憶體控制限制設定。 例如，節點A和B的上限可以較低，這些節點在負載平衡器中寫程式以用於互動式工作。 您可以對節點C和D設定更高的高限制，這些不由負載平衡器使用，而是保留用於非同步工作。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.low-limit</code></td>
   <td><p>指定在Work Manager停止限制傳入作業之前可以使用的記憶體的最大百分比。</p><p>此選項的預設值為 <code>20</code>。 對於大多數系統，此值應是合適的。</p></td>
  </tr>
  <tr>
   <td><code>Dadobe.workmanager.allocate.max-batch-size</code></td>
   <td><p>指定workmanager的最大批大小。 預設批大小為10。</p><p>如果即使任務完成後仍未更新工作管理器中某個進程的狀態，則將批大小設定為1。</p></td>
  </tr>
 </tbody>
</table>

**將Java選項添加到JBoss**

1. 停止JBoss應用程式伺服器。
1. 開啟 *[appserver根]*/bin/run.bat(Windows)或run.sh（Linux或UNIX），並根據需要以格式添加任何Java選項 `-Dproperty=value`。
1. 重新啟動伺服器。

**將Java選項添加到WebLogic**

1. 通過鍵入以啟動WebLogic管理控制台 `https://[host name]:[port]/console` 的子菜單。
1. 鍵入您為WebLogic Server域建立的用戶名和密碼，然後按一下「更改中心」下的「日誌」，然後按一下「鎖定和編輯」。
1. 在「域結構」下，按一下「環境」>「伺服器」，然後在右窗格中按一下受控伺服器名稱。
1. 在下一螢幕中，按一下「配置」頁籤>「伺服器啟動」頁籤。
1. 在「參數」框中，將所需參數追加到當前內容的末尾。 例如，要禁用運行狀況監視器，請添加：

   `-Dadobe.healthmonitor.enabled=false` 禁用運行狀況監視器。

1. 按一下「保存」，然後按一下「激活更改」。
1. 重新啟動WebLogic托管伺服器。

**將Java選項添加到WebSphere**

1. 在WebSphere管理控制台導航樹中，按一下「伺服器」>「伺服器類型」>「WebSphere應用程式伺服器」。
1. 在右窗格中，按一下伺服器名稱。
1. 在「伺服器基礎架構」下，按一下「Java」和「表單」工作流>「進程定義」。
1. 在「其他屬性」下，按一下「Java虛擬機」。
1. 在「一般JVM參數」框中，鍵入所需的參數。
1. 按一下「確定」或「應用」，然後直接按一下「保存」到主配置。
