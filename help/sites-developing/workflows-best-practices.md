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
exl-id: 14775476-6fe5-4583-8ab5-b55fef892174
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1924'
ht-degree: 1%

---

# 工作流最佳實踐{#workflow-best-practices}

工作流程可讓您自動執行Adobe Experience Manager(AEM)活動。

它們通常代表發生在AEM環境中的大量處理，因此，當自訂工作流程步驟未根據最佳實務撰寫，或現成可用的工作流程未設定為盡可能有效率地執行時，系統可能會因此受到影響。

因此，強烈建議您謹慎規劃工作流程實作。

## 設定 {#configuration}

設定工作流程程式（自訂和/或現成可用）時，應謹記一些事項。

### 暫時性工作流程 {#transient-workflows}

若要最佳化高擷取載入，您可以將[工作流程定義為暫時](/help/sites-developing/workflows.md#transient-workflows)。

當工作流程為暫時性時，與中間工作步驟相關的執行階段資料在執行時不會保存在JCR中（當然會保存輸出轉譯）。

其優點包括：

* 縮短工作流程處理時間；高達10%。
* 顯著減少儲存庫增長。
* 清除不再需要CRUD工作流程。
* 此外，它還能減少TAR檔案的數量，使其更緊湊。

>[!CAUTION]
>
>如果您的業務指定您保留/封存工作流程執行階段資料以用於稽核用途，請勿啟用此功能。

### 調整DAM工作流程{#tuning-dam-workflows}

如需DAM工作流程的效能調整指南，請參閱[AEM Assets效能調整指南](/help/assets/performance-tuning-guidelines.md)。

### 配置併發工作流的最大數{#configure-the-maximum-number-of-concurrent-workflows}

AEM可允許同時執行多個工作流程執行緒。 預設情況下，線程數配置為系統上處理器核心數的一半。

在執行中的工作流程需要系統資源的情況下，這可能表示AEM沒有剩餘的時間用於其他工作，例如轉譯製作UI。 因此，在大量影像上傳等活動期間，系統可能會變得緩慢。

要解決此問題，Adobe建議將&#x200B;**最大並行作業數**&#x200B;配置為系統上處理器內核數的一半到四分之三之間。 這應該能讓系統有足夠的容量，在處理這些工作流程時能持續回應。

要配置&#x200B;**最大並行作業數**，可以執行以下操作：

* 從AEM Web控制台配置&#x200B;**[OSGi配置](/help/sites-deploying/configuring-osgi.md)**;對於&#x200B;**隊列：Granite工作流程佇列**（**Apache Sling作業佇列設定**）。

* 從AEM Web控制台的&#x200B;**Sling作業**&#x200B;選項設定佇列；對於&#x200B;**作業隊列配置：Granite工作流程佇列**，位於`http://localhost:4502/system/console/slingevent`。

此外，還為&#x200B;**Granite工作流外部進程作業隊列**&#x200B;提供單獨的配置。 這會用於啟動外部二進位檔的工作流程程式，例如&#x200B;**InDesign Server**&#x200B;或&#x200B;**影像摘要**。

### 配置單個作業隊列{#configure-individual-job-queues}

在某些情況下，配置單個作業隊列以根據單個作業控制併發線程或其他隊列選項非常有用。 您可以透過&#x200B;**Apache Sling Job Queue Configuration**&#x200B;工廠，從Web主控台新增和設定個別佇列。 若要尋找要列出的適當主題，請執行工作流程的模型，並在&#x200B;**Sling Jobs**&#x200B;主控台中尋找；例如，在`http://localhost:4502/system/console/slingevent`。

也可以為暫時性工作流程新增個別工作佇列。

### 配置工作流清除{#configure-workflow-purging}

在標準安裝AEM中，提供維護主控台，可安排和設定每日和每週的維護活動；例如：

`http://localhost:4502/libs/granite/operations/content/maintenance.html`

預設情況下，**每週維護窗口**&#x200B;具有&#x200B;**工作流清除**&#x200B;任務，但在運行前需要配置此任務。 若要設定工作流程清除，必須在Web主控台中新增新的&#x200B;**AdobeGranite工作流程清除設定**。

有關AEM中維護任務的詳細資訊，請參閱[操作儀表板](/help/sites-administering/operations-dashboard.md)。

## 自訂 {#customization}

撰寫自訂工作流程程式時，應謹記一些事項。

### 位置 {#locations}

工作流模型、啟動器、指令碼和通知的定義根據類型保存在儲存庫中；例如現成可用、自訂等。

>[!NOTE]
>
>另請參閱[AEM 6.5](/help/sites-deploying/repository-restructuring.md)中的存放庫重新調整。

#### 位置 — 工作流模型{#locations-workflow-models}

工作流模型會根據類型儲存在儲存庫中：

* 現成可用的工作流程設計會保留在下列路徑下：

   `/libs/settings/workflow/models/`

   >[!CAUTION]
   >
   >請勿：
   >
   >* 在此資料夾中放置任何自訂工作流程模型
   >* 編輯`/libs`中的任何內容

   >
   >任何變更可能會在升級時或安裝Hotfix、Cumulative Fix Pack或Service Pack時覆寫。

* 自訂工作流程設計保留在下列位置：

   ```
   /conf/global/settings/workflow/models/...
   ```

* 執行階段工作流程設計（現成和自訂）會保留在下列路徑下：

   `/var/workflow/models/`

* 舊式工作流程設計（包括設計時間和執行階段）會保留在下列路徑下：

   `/etc/workflow/models/`

   >[!NOTE]
   >
   >如果使用AEM UI *編輯了這些設計，則詳細資料將複製到新位置。*

#### 位置 — 工作流啟動器{#locations-workflow-launchers}

工作流程啟動器定義也會根據類型儲存在存放庫中：

* 現成可用的工作流程啟動器會存放在下列路徑中：

   `/libs/settings/workflow/launcher/`

   >[!CAUTION]
   >
   >請勿：
   >
   >* 將任何自訂工作流程啟動器置於此資料夾中
   >* 編輯`/libs`中的任何內容

   >
   >任何變更可能會在升級時或安裝Hotfix、Cumulative Fix Pack或Service Pack時覆寫。

* 自訂工作流程啟動器位於：

   ```
   /conf/global/settings/workflow/launcher/...
   ```

* 舊式工作流程啟動器依下列路徑持有：

   `/etc/workflow/launcher/`

   >[!NOTE]
   >
   >如果使用AEM UI *編輯了這些定義，則詳細資料將複製到新位置。*

#### 位置 — 工作流指令碼{#locations-workflow-scripts}

工作流程指令碼也會根據類型儲存在存放庫中：

* 現成可用的工作流程指令碼會保留在下列路徑下：

   `/libs/workflow/scripts/`

   >[!CAUTION]
   >
   >請勿：
   >
   >* 將任何自訂工作流程指令碼放在此資料夾中
   >* 編輯`/libs`中的任何內容

   >
   >任何變更可能會在升級時或安裝Hotfix、Cumulative Fix Pack或Service Pack時覆寫。

* 自訂工作流程指令碼保留在下：

   ```
   /apps/workflow/scripts/...
   ```

* 舊版工作流程指令碼保留在以下路徑下：

   `/etc/workflow/scripts/`

#### 位置 — 工作流通知{#locations-workflow-notifications}

工作流程通知也會根據類型儲存在存放庫中：

* 現成可用的工作流程通知定義會保留在下列路徑下：

   `/libs/settings/workflow/notification/`

   >[!CAUTION]
   >
   >請勿：
   >
   >* 將任何自訂工作流程通知定義放置在此資料夾中
   >* 編輯`/libs`中的任何內容

   >
   >任何變更可能會在升級時或安裝Hotfix、Cumulative Fix Pack或Service Pack時覆寫。

* 自訂工作流程通知定義保留在下：

   ```
   /conf/global/settings/workflow/notification/...
   ```

   >[!NOTE]
   >
   >如果要覆寫工作流程通知文字，請在下方建立重疊路徑：
   >
   >
   >`/conf/global/settings/workflow/notification/<path-under-libs>`

* 舊版工作流程通知定義會保留在下列路徑下：

   `/etc/workflow/notification/`

### 進程會話{#process-sessions}

如同任何自訂開發，建議一律使用使用者的工作階段：

* 以最佳方式遵守安全性准則
* 允許系統管理開啟和關閉會話

實作工作流程程式時：

* 將會提供工作流程工作階段，且應使用，除非有令人信服的理由不這麼做。
* 不應從工作流程步驟建立新工作階段，因為這會導致狀態不一致，以及工作流程引擎中可能發生的並行問題。
* 您不應從工作流程中的處理步驟內取得新的JCR工作階段；您應將「處理步驟API」提供的工作流程工作階段調整為jcr工作階段。 例如：

```
public void execute(WorkItem item, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
        // to obtain a jcr session:
        javax.jcr.Session jcrSession = workflowSession.adaptTo(javax.jcr.Session.class);

        // to obtain a sling resource resolver:
        org.apache.sling.api.resource.ResourceResolver slingResourceResolver = workflowSession.adaptTo(org.apache.sling.api.resource.ResourceResolver.class);
```

儲存工作階段：

* 在工作流程程式中，如果使用`WorkflowSession`來修改存放庫，則不明確儲存工作階段 — 工作流程會在工作階段完成時儲存該工作階段。
* `Session.Save` 不應從工作流程步驟中呼叫：

   * 建議調整工作流jcr會話；然後，不需要`save`，因為工作流引擎會在工作流完成執行後自動保存會話。
   * 不建議對進程步驟建立自己的jcr會話。

* 通過消除不必要的節省，您可以減少開銷，從而使工作流更加高效。

>[!CAUTION]
>
>儘管此處提供建議，但您確實已建立自己的jcr工作階段，則需要儲存該工作階段。

### 將啟動器數量/範圍最小化{#minimize-the-number-scope-of-launchers}

有一個偵聽器負責所有已註冊的[工作流啟動器](/help/sites-administering/workflows-starting.md#workflows-launchers):

* 它會監聽其他啟動器的全域屬性中指定的所有路徑的變更。
* 發送事件時，工作流引擎將評估每個啟動器以確定它是否應運行。

建立過多的啟動器將導致評估過程運行更慢。

在單一啟動器上位於存放庫根目錄建立全域路徑時，工作流程引擎會監聽並評估建立/修改事件至存放庫中的每個節點。 因此，建議僅建立所需的啟動器，並盡可能使全域路徑具體。

由於這些啟動器對工作流行為的影響，禁用任何未使用的現成啟動器也會有所幫助。

### 啟動器{#configuration-enhancements-for-launchers}的配置增強

已增強自訂[啟動器配置](/help/sites-administering/workflows-starting.md#workflows-launchers)，以支援下列功能：

* 將多個條件「AND」結合在一起。
* 在單一條件內有OR條件。
* 根據功能標誌是啟用還是禁用，禁用/啟用啟動器。
* 在啟動器條件中支援regex。

### 請勿從其他工作流程開始工作流程{#do-not-start-workflows-from-other-workflows}

工作流程可能會產生大量的額外負荷，無論是在記憶體中建立的物件，還是在存放庫中追蹤的節點皆然。 因此，最好讓工作流程自行處理，而非啟動其他工作流程。

例如，會對一組內容實作業務處理，然後啟用該內容的工作流程。 最好建立會啟用這些節點的自訂工作流程程式，而不是針對需要發佈的每個內容節點啟動&#x200B;**啟用內容**&#x200B;模型。 此方法需要額外的開發工作，但執行時比為每個啟動啟動個別的工作流程例項更有效率。

另一個例子是處理多個節點、建立工作流包、然後激活所述包的工作流。 您可以在建立套件的步驟中變更工作流程的裝載，然後呼叫步驟，以在相同的工作流程模型中啟用套件，而不是建立套件，然後以套件作為裝載啟動個別的工作流程。

### 處理常式前進 {#handler-advance}

在設計工作流模型時，您可以選擇啟用處理常式，使其在工作流步驟上前進。 或者，您可以將程式碼新增至工作流程步驟，以決定後續應執行哪個步驟，然後加以執行。

建議您使用處理常式進階，以提供更佳的效能。

### 工作流階段{#workflow-stages}

您可以定義[工作流階段](/help/sites-developing/workflows.md#workflow-stages)，然後將任務/步驟分配給特定工作流階段。

當您從&#x200B;**收件箱**](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions)&#x200B;中按一下工作項的&#x200B;[**工作流資訊**&#x200B;頁簽時，此資訊用於顯示工作流的進度。 可以編輯現有的工作流模型以添加階段。

### 啟動頁面處理步驟{#activate-page-process-step}

**啟動頁面程式**&#x200B;步驟將會為您啟動頁面，但不會自動尋找任何參考的DAM資產並啟動這些資產。

如果您打算將此步驟用於工作流程模型，請謹記這一點。

### 升級注意事項{#upgrade-considerations}

升級執行個體時：

* 確保在升級實例之前備份所有自定義工作流模型。
* 確認您的自訂工作流程皆未儲存在[location](#locations)下：

   * `/libs/settings/workflow/models/projects`

>[!NOTE]
>
>另請參閱[AEM 6.5](/help/sites-deploying/repository-restructuring.md)中的存放庫重新調整。

## 系統工具{#system-tools}

有許多系統工具可協助您監控、維護和疑難排解工作流程。 以下所有範例URL都使用`localhost:4502`，但應可用於任何製作例項(`<hostname>:<port>`)。

### Sling作業處理控制台{#sling-job-handling-console}

`http://localhost:4502/system/console/slingevent`

Sling作業處理主控台將顯示：

* 上次重新啟動後系統中作業狀態的統計資訊。
* 它還將顯示所有作業隊列的配置，並提供在配置管理器中編輯它們的快捷方式。

### 工作流報表工具{#workflow-report-tool}

6.3版中移除了工作流程報告工具，以防止效能下降。

### 工作流維護操作MBean {#workflow-maintenance-operations-mbean}

`http://localhost:4502/system/console/jmx/com.adobe.granite.workflow:type=Maintenance`

工作流維護MBean公開了幾個有用的維護常式，如清除已完成的工作流和檢索工作流統計資訊。

## 更多資訊 {#further-information}

如需詳細資訊，請參閱：

* [使用工作流程](/help/sites-authoring/workflows.md)
* [管理工作流程](/help/sites-administering/workflows.md)
* [開發和延伸工作流程](/help/sites-developing/workflows.md)
* [效能最佳化](/help/sites-deploying/configuring-performance.md)
