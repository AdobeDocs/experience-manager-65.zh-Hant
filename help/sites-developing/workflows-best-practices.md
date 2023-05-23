---
title: 工作流最佳實踐
seo-title: Workflow Best Practices
description: 工作流最佳實踐
seo-description: null
uuid: 79be4055-c2ef-428e-9054-103c6cfde1d2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 0be8b88c-6f57-4dcc-ae11-77b378a2decd
exl-id: 14775476-6fe5-4583-8ab5-b55fef892174
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1920'
ht-degree: 1%

---

# 工作流最佳實踐{#workflow-best-practices}

工作流使您能夠自動執行Adobe Experience Manager(AEM)活動。

它們通常表示環境中發生的大量處理AEM，因此，當自定義工作流步驟未根據最佳做法編寫或出廠設定工作流未配置為盡可能高效地運行時，系統會因此受損。

因此，強烈建議仔細規劃您的工作流實施。

## 設定 {#configuration}

在配置工作流進程（自定義和/或開箱即用）時，應牢記以下幾點。

### 暫時性工作流程 {#transient-workflows}

要優化高吞吐載荷，可以定義 [工作流作為暫時](/help/sites-developing/workflows.md#transient-workflows)。

當工作流處於臨時狀態時，與中間工作步驟相關的運行時資料在運行時不會保留在JCR中（當然，輸出格式副本會保留）。

其優點包括：

* 減少工作流處理時間；高達10%。
* 顯著減少儲存庫增長。
* 不再需要CRUD工作流來清除。
* 另外，它還減少了TAR檔案的數量，使其緊湊。

>[!CAUTION]
>
>如果您的業務要求您保留/存檔工作流運行時資料以用於審核目的，請不要啟用此功能。

### 調整DAM工作流 {#tuning-dam-workflows}

有關DAM工作流的效能調整指南，請參見 [AEM Assets效能調整指南](/help/assets/performance-tuning-guidelines.md)。

### 配置最大併發工作流數 {#configure-the-maximum-number-of-concurrent-workflows}

允許AEM多個工作流線程併發運行。 預設情況下，線程數配置為系統上處理器內核數的一半。

如果正在執行的工作流要求系統資源，則這可能意味AEM著很少可用於其他任務，如呈現創作UI。 因此，在諸如批量影像上傳等活動期間，系統可能處於停滯狀態。

要解決此問題，Adobe建議配置 **最大並行作業數** 佔系統處理器內核數量的半至四分之三。 這應允許系統有足夠的容量在處理這些工作流時保持響應。

配置 **最大並行作業數**，您可以選擇：

* 配置 **[OSGi配置](/help/sites-deploying/configuring-osgi.md)** 從AEMWeb控制台；為 **隊列：花崗岩工作流隊列** (a) **Apache Sling作業隊列配置**)。

* 從 **斯林喬布斯** Web控制AEM台選項；為 **作業隊列配置：花崗岩工作流隊列**。 `http://localhost:4502/system/console/slingevent`。

此外，還有一個單獨的配置 **花崗岩工作流外部進程作業隊列**。 這用於啟動外部二進位檔案的工作流進程，如 **InDesign Server** 或 **影像馬吉克**。

### 配置單個作業隊列 {#configure-individual-job-queues}

在某些情況下，配置單個作業隊列以控制並行線程或其它隊列選項是非常有用的。 您可以通過Web控制台添加和配置單個隊列 **Apache Sling作業隊列配置** 工廠。 要查找要列出的相應主題，請執行工作流模型並在 **斯林喬布斯** 控制台；例如，在 `http://localhost:4502/system/console/slingevent`。

也可以為臨時工作流添加單個作業隊列。

### 配置工作流清除 {#configure-workflow-purging}

在標準安裝中，AEM提供了維護控制台，可安排和配置每日和每週的維護活動；例如，在：

`http://localhost:4502/libs/granite/operations/content/maintenance.html`

預設情況下， **每週維護窗口** 有 **工作流清除** 任務，但需要先配置此項，然後才能運行。 要配置工作流清除，請新建 **Adobe花崗岩工作流清除配置** 必須添加到Web控制台中。

有關中維護任務的詳細信AEM息，請參閱 [操作儀表板](/help/sites-administering/operations-dashboard.md)。

## 自定義 {#customization}

在編寫自定義工作流進程時，應牢記一些事項。

### 位置 {#locations}

工作流模型、啟動器、指令碼和通知的定義按類型保存在儲存庫中；例如，開箱即用、定制等。

>[!NOTE]
>
>另請參閱 [6.5中的AEM儲存庫重組](/help/sites-deploying/repository-restructuring.md)。

#### 位置 — 工作流模型 {#locations-workflow-models}

工作流模型根據類型儲存在儲存庫中：

* 現成工作流設計按以下路徑保存：

   `/libs/settings/workflow/models/`

   >[!CAUTION]
   >
   >不要：
   >
   >* 將您的任何自定義工作流模型放置在此資料夾中
   >* 編輯任何內容 `/libs`

   >
   >由於升級時或安裝熱修復程式時，任何更改都可能被覆蓋，因此累積的修復程式包或服務包會被覆蓋。

* 自定義工作流設計保留在：

   ```
   /conf/global/settings/workflow/models/...
   ```

* 運行時工作流設計（現成和自定義）都保存在以下路徑下：

   `/var/workflow/models/`

* 舊式工作流設計（設計時間和運行時）保留在以下路徑下：

   `/etc/workflow/models/`

   >[!NOTE]
   >
   >如果編輯了這些設計 *使用AEMUI*，然後將詳細資訊複製到新位置。

#### 位置 — 工作流啟動程式 {#locations-workflow-launchers}

工作流啟動程式定義也根據類型儲存在儲存庫中：

* 現成工作流啟動程式按以下路徑持有：

   `/libs/settings/workflow/launcher/`

   >[!CAUTION]
   >
   >不要：
   >
   >* 將您的任何自定義工作流啟動程式放置在此資料夾中
   >* 編輯任何內容 `/libs`

   >
   >由於升級時或安裝熱修復程式時，任何更改都可能被覆蓋，因此累積的修復程式包或服務包會被覆蓋。

* 自定義工作流啟動器位於：

   ```
   /conf/global/settings/workflow/launcher/...
   ```

* 舊式工作流啟動器按以下路徑持有：

   `/etc/workflow/launcher/`

   >[!NOTE]
   >
   >如果編輯了這些定義 *使用AEMUI*，然後將詳細資訊複製到新位置。

#### 位置 — 工作流指令碼 {#locations-workflow-scripts}

工作流指令碼還根據以下類型儲存在儲存庫中：

* 現成工作流指令碼保存在以下路徑下：

   `/libs/workflow/scripts/`

   >[!CAUTION]
   >
   >不要：
   >
   >* 將您的任何自定義工作流指令碼放在此資料夾中
   >* 編輯任何內容 `/libs`

   >
   >由於升級時或安裝熱修復程式時，任何更改都可能被覆蓋，因此累積的修復程式包或服務包會被覆蓋。

* 自定義工作流指令碼保存在：

   ```
   /apps/workflow/scripts/...
   ```

* 舊工作流指令碼保存在以下路徑下：

   `/etc/workflow/scripts/`

#### 位置 — 工作流通知 {#locations-workflow-notifications}

工作流通知還根據以下類型儲存在儲存庫中：

* 現成工作流通知定義保存在以下路徑下：

   `/libs/settings/workflow/notification/`

   >[!CAUTION]
   >
   >不要：
   >
   >* 將任何自定義工作流通知定義放在此資料夾中
   >* 編輯任何內容 `/libs`

   >
   >由於升級時或安裝熱修復程式時，任何更改都可能被覆蓋，因此累積的修復程式包或服務包會被覆蓋。

* 自定義工作流通知定義保存在：

   ```
   /conf/global/settings/workflow/notification/...
   ```

   >[!NOTE]
   >
   >如果要覆蓋工作流通知文本，請在以下位置建立重疊路徑：
   >
   >
   >`/conf/global/settings/workflow/notification/<path-under-libs>`

* 舊式工作流通知定義保存在以下路徑下：

   `/etc/workflow/notification/`

### 進程會話 {#process-sessions}

與任何自定義開發一樣，始終建議盡可能使用用戶的會話：

* 以最好地遵守安全准則
* 允許系統管理開啟和關閉會話

實施工作流進程時：

* 將提供工作流會話，並且應使用該會話，除非有令人信服的理由不使用。
* 不應根據工作流步驟建立新會話，因為這會導致狀態不一致以及工作流引擎中可能的併發問題。
* 您不應從工作流中的進程步驟中獲取新的JCR會話；您應將「進程步驟API」提供的工作流會話調整為jcr會話。 例如：

```
public void execute(WorkItem item, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
        // to obtain a jcr session:
        javax.jcr.Session jcrSession = workflowSession.adaptTo(javax.jcr.Session.class);

        // to obtain a sling resource resolver:
        org.apache.sling.api.resource.ResourceResolver slingResourceResolver = workflowSession.adaptTo(org.apache.sling.api.resource.ResourceResolver.class);
```

保存會話：

* 在工作流進程內，如果 `WorkflowSession` 正在用於修改儲存庫，然後不顯式保存會話 — 工作流將在會話完成後保存會話。
* `Session.Save` 不應從工作流步驟中調用：

   * 建議調整工作流jcr會話；然後 `save` 不需要，因為工作流引擎會在工作流完成執行後自動保存會話。
   * 不建議進程步驟建立自己的jcr會話。

* 通過消除不必要的儲存，您可以減少開銷，從而提高工作流的效率。

>[!CAUTION]
>
>如果您確實建立了自己的jcr會話，則需要保存它。

### 最大限度地減少發射器的數量/範圍 {#minimize-the-number-scope-of-launchers}

有一個監聽器負責 [工作流程啟動器](/help/sites-administering/workflows-starting.md#workflows-launchers) 已註冊：

* 它將偵聽其他啟動器的globbing屬性中指定的所有路徑的更改。
* 當調度事件時，工作流引擎將評估每個啟動程式以確定它是否應運行。

建立過多的啟動器將導致評估過程運行更慢。

在單個啟動器上儲存庫的根位置建立全局路徑將導致工作流引擎偵聽並評估建立/修改事件到儲存庫中的每個節點。 因此，建議只建立所需的啟動器，並盡可能使全域路徑具體化。

由於這些啟動程式對工作流行為的影響，禁用任何未使用的出廠設定啟動程式也會有所幫助。

### 啟動器的配置增強 {#configuration-enhancements-for-launchers}

自定義 [啟動程式配置](/help/sites-administering/workflows-starting.md#workflows-launchers) 已增強，以支援以下內容：

* 將多個條件「AND」連在一起。
* 在單個條件內具有OR條件。
* 根據功能標誌是啟用還是禁用，禁用/啟用啟動程式。
* 在啟動程式條件中支援regex。

### 不從其他工作流啟動工作流 {#do-not-start-workflows-from-other-workflows}

工作流可以帶來大量開銷，無論是在記憶體中建立的對象，還是在儲存庫中跟蹤的節點。 因此，最好讓工作流在其內部完成其處理，而不是啟動其他工作流。

一個示例是一個工作流，它在一組內容上實現業務流程，然後激活該內容。 最好建立一個自定義工作流進程來激活這些節點中的每個節點，而不是啟動 **激活內容** 每個需要發佈的內容節點的模型。 此方法需要額外的開發工作，但執行時比為每次激活啟動單獨的工作流實例更高效。

另一個示例是處理多個節點的工作流，建立工作流包，然後激活所述包。 您可以在建立包的步驟中更改工作流的負載，然後調用該步驟以在同一工作流模型內激活包，而不是建立包，然後以包作為負載啟動單獨的工作流。

### 處理常式前進 {#handler-advance}

在設計工作流模型時，您可以選擇在工作流步驟上啟用處理程式高級。 或者，您可以將代碼添加到工作流步驟中，以確定下一步應運行哪個步驟，然後執行該步驟。

建議使用處理程式高級，因為它提供了更好的效能。

### 工作流階段 {#workflow-stages}

您可以定義 [工作流階段](/help/sites-developing/workflows.md#workflow-stages)，然後將任務/步驟分配給特定的工作流階段。

此資訊用於在按一下 [**工作流資訊** 的子菜單。 **收件箱**](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions)。 可以編輯現有工作流模型以添加階段。

### 激活頁面處理步驟 {#activate-page-process-step}

的 **激活頁面進程** 步驟將為您激活頁面，但不會自動找到任何引用的DAM資產並激活這些資產。

如果您計畫將此步驟用作工作流模型的一部分，請記住這一點。

### 升級注意事項 {#upgrade-considerations}

升級實例時：

* 確保在升級實例之前備份所有自定義工作流模型。
* 確認您的自定義工作流未儲存在 [位置](#locations):

   * `/libs/settings/workflow/models/projects`

>[!NOTE]
>
>另請參閱 [6.5中的AEM儲存庫重組](/help/sites-deploying/repository-restructuring.md)。

## 系統工具 {#system-tools}

有許多系統工具可用於幫助監控、維護和排除工作流故障。 下面的所有示例URL都使用 `localhost:4502`，但任何作者實例( `<hostname>:<port>`)。

### Sling作業處理控制台 {#sling-job-handling-console}

`http://localhost:4502/system/console/slingevent`

Sling作業處理控制台將顯示：

* 自上次重新啟動以來系統中作業狀態的統計資訊。
* 它還將顯示所有作業隊列的配置，並提供在配置管理器中編輯這些隊列的快捷方式。

### 工作流報告工具 {#workflow-report-tool}

6.3中刪除了工作流報告工具，以防止效能下降。

### 工作流維護操作MBean {#workflow-maintenance-operations-mbean}

`http://localhost:4502/system/console/jmx/com.adobe.granite.workflow:type=Maintenance`

工作流維護MBean公開了一些有用的維護常式，如清除已完成的工作流和檢索工作流統計資訊。

## 更多資訊 {#further-information}

如需進一步詳細資訊，請參閱：

* [使用工作流程](/help/sites-authoring/workflows.md)
* [管理工作流程](/help/sites-administering/workflows.md)
* [開發和延伸工作流程](/help/sites-developing/workflows.md)
* [效能優化](/help/sites-deploying/configuring-performance.md)
