---
title: 工作流程最佳實務
seo-title: 工作流程最佳實務
description: 工作流程最佳實務
seo-description: 'null'
uuid: 79be4055-c2ef-428e-9054-103c6cfde1d2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 0be8b88c-6f57-4dcc-ae11-77b378a2decd
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1924'
ht-degree: 1%

---


# 工作流程最佳實務{#workflow-best-practices}

工作流程可讓您將Adobe Experience Manager(AEM)活動自動化。

它們通常代表環境中發生的大量處理AEM，因此，當自訂工作流程步驟未根據最佳實務撰寫，或現成可用的工作流程未設定為盡可能有效地執行時，系統會因此受到影響。

因此，強烈建議您謹慎規劃您的工作流程實作。

## 設定 {#configuration}

在設定工作流程程式（自訂和／或現成可用）時，有些事情需要留意。

### 暫時性工作流程 {#transient-workflows}

若要最佳化高擷取負載，您可將[工作流程定義為transient](/help/sites-developing/workflows.md#transient-workflows)。

當工作流程為暫時性時，與中間工作步驟相關的執行階段資料在執行時不會保存在JCR中（當然會保留輸出轉譯）。

其優點包括：

* 縮短工作流處理時間；高達10%。
* 顯著減少儲存庫的增長。
* 您不再需要CRUD工作流程來清除。
* 此外，它還可將TAR檔案的數量減少至精簡。

>[!CAUTION]
>
>如果您的企業規定您為了審核目的而保留／封存工作流程執行階段資料，請勿啟用此功能。

### 調整DAM工作流程{#tuning-dam-workflows}

有關DAM工作流的效能調整指導，請參閱[AEM Assets效能調整指南](/help/assets/performance-tuning-guidelines.md)。

### 配置併發工作流的最大數{#configure-the-maximum-number-of-concurrent-workflows}

可允AEM許同時運行多個工作流線程。 預設情況下，線程數配置為系統上處理器內核數的一半。

當執行的工作流程需要系統資源時，這可能表示其他工作(AEM例如轉譯編寫UI)幾乎不需要使用。 因此，在大量影像上傳等活動期間，系統可能會變慢。

要解決此問題，Adobe建議將&#x200B;**最大並行作業數**&#x200B;配置為系統上處理器內核數的一半到四分之三之間。 這應允許系統有足夠的容量在處理這些工作流程時保持回應速度。

要配置&#x200B;**最大並行作業數**，您可以執行以下任一操作：

* 從Web控制台配置&#x200B;**[OSGi Configuration&lt;a1/AEM>;對於**&#x200B;隊列：Granite Workflow Queue **(an** Apache Sling Job Queue Configuration **)。](/help/sites-deploying/configuring-osgi.md)**

* 從Web主控台的&#x200B;**Sling Jobs**&#x200B;選項設定佇列AEM;對於&#x200B;**作業隊列配置：Granite Workflow Queue**, at `http://localhost:4502/system/console/slingevent`。

此外，**Granite工作流外部進程作業隊列**&#x200B;還有單獨的配置。 這適用於啟動外部二進位檔案的工作流程程式，例如&#x200B;**InDesign Server**&#x200B;或&#x200B;**影像快訊**。

### 配置單個作業隊列{#configure-individual-job-queues}

在某些情況下，配置單個作業隊列以控制單個作業的併發線程或其他隊列選項非常有用。 您可以透過&#x200B;**Apache Sling Job Queue Configuration**&#x200B;工廠，從Web主控台新增及設定個別佇列。 若要尋找要列出的適當主題，請執行您工作流程的模型，然後在&#x200B;**Sling Jobs**&#x200B;主控台中尋找它；例如，在`http://localhost:4502/system/console/slingevent`。

您也可以新增個別工作佇列，以進行暫時性工作流程。

### 配置工作流清除{#configure-workflow-purging}

在標準安裝中，AEM提供維護主控台，可安排和設定每日和每週的維護活動；例如，at:

`http://localhost:4502/libs/granite/operations/content/maintenance.html`

預設情況下，**每週維護窗口**&#x200B;具有&#x200B;**工作流清除**&#x200B;任務，但必須在運行前配置此任務。 要配置工作流清除，必須在Web控制台中添加新的&#x200B;**Adobe花崗岩工作流清除配置**。

有關中維護任務的詳細信AEM息，請參見[操作儀表板](/help/sites-administering/operations-dashboard.md)。

## 自訂{#customization}

在編寫自訂工作流程程式時，應牢記一些事項。

### 位置 {#locations}

工作流模型、啟動器、指令碼和通知的定義根據類型保存在儲存庫中；例如現成可用、自訂等。

>[!NOTE]
>
>另請參閱[6.5&lt;a1/AEM>中的儲存庫重組。](/help/sites-deploying/repository-restructuring.md)

#### 位置——工作流模型{#locations-workflow-models}

工作流模型根據類型儲存在儲存庫中：

* 現成可用的工作流程設計會保留在下列路徑下：

   `/libs/settings/workflow/models/`

   >[!CAUTION]
   >
   >不要：
   >
   >* 將任何自訂的工作流程模型置於此資料夾中
   >* 編輯`/libs`中的任何內容

   >
   >因為升級時或安裝修補程式、累積修補程式套件或服務套件時，可能會覆寫任何變更。

* 自訂工作流程設計保留於：

   ```
   /conf/global/settings/workflow/models/...
   ```

* 執行時期工作流程設計（現成可用和自訂）會保存在下列路徑下：

   `/var/workflow/models/`

* 舊式工作流程設計（包括設計時和執行時期）會保留在下列路徑下：

   `/etc/workflow/models/`

   >[!NOTE]
   >
   >如果這些設計是使用UI *編AEM輯的，則詳細資料會複製到新位置。*

#### 位置——工作流啟動器{#locations-workflow-launchers}

工作流啟動程式定義也根據類型儲存在儲存庫中：

* 現成可用的工作流程啟動器依下列路徑持有：

   `/libs/settings/workflow/launcher/`

   >[!CAUTION]
   >
   >不要：
   >
   >* 將任何自訂工作流程啟動器放在此資料夾中
   >* 編輯`/libs`中的任何內容

   >
   >因為升級時或安裝修補程式、累積修補程式套件或服務套件時，可能會覆寫任何變更。

* 自訂工作流程啟動程式存放於：

   ```
   /conf/global/settings/workflow/launcher/...
   ```

* 舊式工作流程啟動器依下列路徑持有：

   `/etc/workflow/launcher/`

   >[!NOTE]
   >
   >如果使用UI *編輯了這些定義AEM，則詳細資訊將複製到新位置。*

#### 位置——工作流指令碼{#locations-workflow-scripts}

工作流指令碼也根據類型儲存在儲存庫中：

* 現成可用的工作流程指令碼位於下列路徑下：

   `/libs/workflow/scripts/`

   >[!CAUTION]
   >
   >不要：
   >
   >* 將任何自訂工作流程指令碼置於此資料夾中
   >* 編輯`/libs`中的任何內容

   >
   >因為升級時或安裝修補程式、累積修補程式套件或服務套件時，可能會覆寫任何變更。

* 自訂工作流程指令碼保留於：

   ```
   /apps/workflow/scripts/...
   ```

* 舊式工作流程指令碼會保留在下列路徑下：

   `/etc/workflow/scripts/`

#### 位置——工作流通知{#locations-workflow-notifications}

工作流通知也根據類型儲存在儲存庫中：

* 現成可用的工作流程通知定義位於下列路徑下：

   `/libs/settings/workflow/notification/`

   >[!CAUTION]
   >
   >不要：
   >
   >* 將任何自訂工作流程通知定義放在此資料夾中
   >* 編輯`/libs`中的任何內容

   >
   >因為升級時或安裝修補程式、累積修補程式套件或服務套件時，可能會覆寫任何變更。

* 自訂工作流程通知定義位於：

   ```
   /conf/global/settings/workflow/notification/...
   ```

   >[!NOTE]
   >
   >如果要覆蓋工作流通知文本，請在以下位置建立一個覆蓋路徑：
   >
   >
   >`/conf/global/settings/workflow/notification/<path-under-libs>`

* 舊式工作流程通知定義位於下列路徑下：

   `/etc/workflow/notification/`

### 進程會話{#process-sessions}

和任何自訂開發一樣，建議您盡可能使用使用者的工作階段：

* 以最佳方式遵守安全准則
* 允許系統管理開啟和關閉會話

實作工作流程程式時：

* 將會提供工作流程工作階段，且應使用，除非有令人信服的理由不提供。
* 不應從工作流步驟建立新會話，因為這會導致狀態不一致以及工作流引擎中的可能併發問題。
* 您不應從工作流中的流程步驟中獲取新的JCR會話；您應將「流程步驟API」提供的工作流程工作階段調整為jcr工作階段。 例如：

```
public void execute(WorkItem item, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
        // to obtain a jcr session:
        javax.jcr.Session jcrSession = workflowSession.adaptTo(javax.jcr.Session.class);

        // to obtain a sling resource resolver:
        org.apache.sling.api.resource.ResourceResolver slingResourceResolver = workflowSession.adaptTo(org.apache.sling.api.resource.ResourceResolver.class);
```

保存會話：

* 在工作流進程內，如果`WorkflowSession`用於修改儲存庫，則不顯式保存會話——工作流將在會話完成時保存會話。
* `Session.Save` 不應從工作流程步驟中呼叫：

   * 建議對工作流jcr會話進行調整；然後，工作流引擎在工作流完成執行後自動保存會話，因此不需要`save`。
   * 不建議進程步驟建立自己的jcr會話。

* 借由消除不必要的省錢，您可以降低開銷，進而提高工作流程的效率。

>[!CAUTION]
>
>如果您確實建立自己的jcr作業，儘管此處有建議，但需要儲存它。

### 將發射器的數量／範圍減至最小{#minimize-the-number-scope-of-launchers}

有一個監聽器負責所有已註冊的[工作流啟動器](/help/sites-administering/workflows-starting.md#workflows-launchers):

* 它將監聽其他發射器的globbing屬性中指定的所有路徑的更改。
* 當傳送事件時，工作流程引擎會評估每個啟動程式，以判斷它是否應該執行。

建立過多的啟動器將導致評估程式運行更慢。

在單個啟動器上在儲存庫的根位置建立全域路徑將導致工作流引擎偵聽並評估建立／修改事件到儲存庫中的每個節點。 因此，建議僅建立所需的發射器，並盡可能使全域路徑具體。

由於這些啟動器對工作流行為的影響，禁用任何未使用的現成可用啟動器也很有幫助。

### 啟動器的配置增強功能{#configuration-enhancements-for-launchers}

自訂[啟動器組態](/help/sites-administering/workflows-starting.md#workflows-launchers)已增強，可支援下列功能：

* 將多個條件&quot;AND&quot;結合在一起。
* 在單一條件內具有OR條件。
* 根據功能標幟是啟用還是停用，停用／啟用啟動器。
* 在啟動器條件中支援regex。

### 不要從其他工作流程中啟動工作流{#do-not-start-workflows-from-other-workflows}

工作流在記憶體中建立的對象和儲存庫中跟蹤的節點方面，都會產生大量開銷。 因此，最好讓工作流程自行處理，而不是啟動其他工作流程。

例如，在一組內容上實作商業程式，然後啟動該內容的工作流程。 最好為每個需要發佈的內容節點建立可啟動這些節點的自訂工作流程程式，而不是啟動&#x200B;**啟動內容**&#x200B;模型。 此方法需要額外的開發工作，但執行時會比針對每次啟動啟動啟動個別工作流程執行個體更有效率。

另一個例子是處理多個節點的工作流，建立工作流包，然後激活所述包。 您可以在建立封裝的步驟中變更工作流程的裝載，然後呼叫步驟，以在相同的工作流程模型中啟動封裝，而不是先建立封裝，然後再以封裝為裝載來啟動個別的工作流程。

### 處理常式前進 {#handler-advance}

在設計工作流模型時，您可以選擇在工作流步驟上啟用處理程式。 或者，您也可以將程式碼新增至工作流程步驟，以決定下一步應執行哪個步驟，然後加以執行。

建議使用處理常式進階，以提供更佳的效能。

### 工作流程階段{#workflow-stages}

您可以定義[工作流階段](/help/sites-developing/workflows.md#workflow-stages)，然後將任務／步驟指派給特定的工作流階段。

當您從&#x200B;**收件箱**](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions)&#x200B;中按一下工作項目的&#x200B;[**工作流資訊**&#x200B;頁籤時，此資訊用於顯示工作流的進度。 可編輯現有的工作流程模型以新增階段。

### 啟動頁面處理步驟{#activate-page-process-step}

**啟動頁面程式**&#x200B;步驟會為您啟用頁面，但不會自動尋找任何參照的DAM資產並啟動這些資產。

如果您打算將此步驟用作工作流程模型的一部分，請務必留意。

### 升級注意事項{#upgrade-considerations}

升級實例時：

* 確保在升級實例之前備份任何自定義工作流模型。
* 確認您的自訂工作流程未儲存在[location](#locations)下方：

   * `/libs/settings/workflow/models/projects`

>[!NOTE]
>
>另請參閱[6.5&lt;a1/AEM>中的儲存庫重組。](/help/sites-deploying/repository-restructuring.md)

## 系統工具{#system-tools}

有許多系統工具可協助您監控、維護和疑難排解工作流程。 以下所有範例URL都使用`localhost:4502`，但應適用於任何作者例項(`<hostname>:<port>`)。

### Sling Job Handling Console {#sling-job-handling-console}

`http://localhost:4502/system/console/slingevent`

Sling Job Handling主控台將會顯示：

* 上次重新啟動後系統中作業狀態的統計資訊。
* 它還將顯示所有作業隊列的配置，並提供在配置管理器中編輯這些隊列的快捷方式。

### 工作流程報表工具{#workflow-report-tool}

6.3版中已移除工作流程報告工具，以防止效能降低。

### 工作流維護操作MBean {#workflow-maintenance-operations-mbean}

`http://localhost:4502/system/console/jmx/com.adobe.granite.workflow:type=Maintenance`

工作流維護MBean提供了一些有用的維護常式，如清除已完成的工作流和檢索工作流統計資訊。

## 更多資訊 {#further-information}

如需詳細資訊，請參閱：

* [使用工作流程](/help/sites-authoring/workflows.md)
* [管理工作流程](/help/sites-administering/workflows.md)
* [開發和延伸工作流程](/help/sites-developing/workflows.md)
* [效能最佳化](/help/sites-deploying/configuring-performance.md)