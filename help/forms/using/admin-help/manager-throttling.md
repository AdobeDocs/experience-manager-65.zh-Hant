---
title: Work manager和調節
seo-title: Work manager和調節
description: 本文檔提供了有關Work manager的背景資訊，並提供了有關配置Work Manager調節選項的說明。
seo-description: 本文檔提供了有關Work manager的背景資訊，並提供了有關配置Work Manager調節選項的說明。
uuid: b90998bc-e3d4-493a-9371-55ccb44da20d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9a8b4e3a-f416-4dc6-a90a-9018df5c844e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Work manager和調節{#work-manager-and-throttling}

AEM表單（及舊版）使用JMS佇列以非同步方式執行作業。 在AEM表單中，JMS佇列已由Work Manager取代。 本文檔提供了有關Work manager的背景資訊，並提供了有關配置Work Manager調節選項的說明。

## 關於長壽命（非同步）操作 {#about-long-lived-asynchronous-operations}

在AEM表單中，由服務執行的作業可以是短期（同步）或長期（非同步）。 短時操作在調用它們的同一線程上同步完成。 這些操作在繼續之前等待響應。

長期運營可能跨系統，甚至延伸到組織之外，例如客戶必須填寫並提交貸款申請表，作為整合多項自動化和人力工作的大型解決方案的一部分。 在等待答復的同時，這些行動必須繼續。 長期業務以非同步方式執行其基礎工作，允許在等待完成時從事其他資源。 與短期操作不同，一旦調用長期操作，Oracle Work Manager不會認為該操作已完成。 必須出現外部觸發器，例如請求對同一服務執行另一操作的系統或提交表單的用戶，才能完成該操作。

## 關於Work Manager {#about-work-manager}

AEM表單（及舊版）使用JMS佇列以非同步方式執行作業。 AEM表單使用Work Manager透過受管理的執行緒來排程及執行非同步作業。

非同步操作以下列方式處理：

1. Work manager接收要執行的工作項目。
1. Work manager將工作項儲存在資料庫表中，並為工作項分配唯一標識符。 資料庫記錄包含執行工作項目所需的所有資訊。
1. 當線程空閒時，Work manager線程將拉入工作項。 在提取工作項目之前，線程可以檢查所需的服務是否已啟動、是否有足夠的堆大小來提取下一個工作項目，以及是否有足夠的CPU週期來處理工作項目。 Oracle Work manager還會在計畫執行時評估工作項目的屬性（如其優先順序）。

AEM Forms管理員可以使用Health Monitor來檢查Work Manager統計資料，例如佇列中的工作項目數及其狀態。 您也可以使用Health monitor暫停、繼續、重試或刪除工作項目。 (請參 [閱查看與Work manager相關的統計資訊](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager)。)

## 配置Work Manager調節選項 {#configuring-work-manager-throttling-options}

您可以為Work Manager配置頻寬限制，以便僅在有足夠的記憶體資源時才計畫工作項目。 您可在應用程式伺服器中設定下列JVM選項，以設定調節。

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
   <td><p>指定Work Manager在檢查其隊列中的新項目時使用的時間間隔（以毫秒為單位）。</p><p>此選項的值是整數。 預設值為毫 <code>1000</code> 秒（1秒）。 </p><p>如果非同步調用的卷很小，則可以增加此值。 例如，您可將其增加到2000到5000（2到5秒）之間。 </p><p>如果非同步調用的卷很大，則預設值應足夠，但可以根據需要使用較小的值。 將此值減得過多（例如，低於50，導致輪詢頻率為每秒20次）會給系統造成很大的開銷。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.debug-mode-enabled</code></td>
   <td><p>將此選項設 <code>true</code> 為啟用偵錯模式，或設為false則停用它。 </p><p>在調試模式下，將記錄有關Work Manager策略違規和Work Manager暫停／恢復操作的消息。 僅在疑難排解時，將此選項設為true。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.enabled</code></td>
   <td><p>將此選項設 <code>true</code> 置為根據下面所述的記憶體控制設定啟用頻寬限制，或 <code>false</code> 禁用頻寬限制。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.high-limit</code></td>
   <td><p>指定在Oracle Work manager調節傳入作業之前，可使用的記憶體的最大百分比。</p><p>此選項的預設值為 <code>95</code>。 此值對於大多數系統都適用。 只有在您的系統需要達到其最大容量時才需要增加容量。 但請注意，當您增加此值時，「記憶體不足」問題的風險也會隨之增加。</p><p>如果您在叢集環境中執行AEM表單，您可能想要在叢集的不同節點上，以不同的方式設定記憶體控制限制設定。 例如，您可以對節點A和B設定較低的上限，這些節點是在負載平衡器中設定，以用於互動式工作。 而且，節點C和D上可以設定較高的高限制，這些限制不被負載平衡器使用，但保留用於非同步工作。</p></td>
  </tr>
  <tr>
   <td><code> adobe.workmanager.memory-control.low-limit</code></td>
   <td><p>指定在Oracle Work manager停止調節傳入作業之前，可使用的記憶體的最大百分比。</p><p>此選項的預設值為 <code>20</code>。 此值對於大多數系統都適用。</p></td>
  </tr>
  <tr>
   <td><code>Dadobe.workmanager.allocate.max-batch-size</code></td>
   <td><p>指定Work manager的最大批處理大小。 預設批大小為10。</p><p>如果即使任務完成後，工作管理器中的進程狀態也未更新，則將批大小設定為1。</p></td>
  </tr>
 </tbody>
</table>

**將Java選項添加到JBoss**

1. 停止JBoss應用程式伺服器。
1. 在編輯 *[器中開啟]* appserver root `-Dproperty=value`/bin/run.bat(Windows)或run.sh（Linux或UNIX），並視需要以格式新增任何Java選項。
1. 重新啟動伺服器。

**將Java選項新增至WebLogic**

1. 在Web瀏覽器中輸入主機名 `https://`*[稱&#x200B;]*`:`*[埠]*`/console` ，啟動WebLogic管理控制台。
1. 鍵入您為WebLogic server域建立的用戶名和密碼，然後按一下「更改中心」下的「日誌」，按一下「鎖定和編輯」。
1. 在「域結構」下，按一下「環境」>「伺服器」，然後在右窗格中按一下受控伺服器名稱。
1. 在下一個畫面中，按一下「設定」標籤>「伺服器開始」標籤。
1. 在「參數」框中，將所需參數附加到當前內容的末尾。 例如，要禁用Health Monitor，請添加：

   `-Dadobe.healthmonitor.enabled=false` 禁用Health Monitor。

1. 按一下「儲存」，然後按一下「啟用變更」。
1. 重新啟動WebLogic受控伺服器。

**將Java選項新增至WebSphere**

1. 在WebSphere管理控制台導覽樹中，按一下「伺服器>伺服器類型> webSphere應用程式伺服器」。
1. 在右窗格中，按一下伺服器名稱。
1. 在「伺服器基礎架構」下，按一下「Java和表單工作流」>「流程定義」。
1. 在「其他屬性」下，按一下「Java虛擬機」。
1. 在「通用JVM參數」框中，鍵入所需參數。
1. 按一下「確定」或「應用」，然後按一下「直接保存到主配置」。

