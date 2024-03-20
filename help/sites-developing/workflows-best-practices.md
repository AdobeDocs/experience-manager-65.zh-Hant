---
title: 工作流程最佳實務
description: 瞭解在Adobe Experience Manager中使用工作流程的最佳實務。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 14775476-6fe5-4583-8ab5-b55fef892174
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1925'
ht-degree: 1%

---

# 工作流程最佳實務{#workflow-best-practices}

工作流程可讓您自動化Adobe Experience Manager (AEM)活動。

這些錯誤通常代表AEM環境中發生的大量處理，因此，當自訂工作流程步驟未根據最佳實務編寫時，或現成的工作流程未設定為儘可能有效率地執行時，系統可能會受損。

因此，強烈建議您仔細規劃工作流程實作。

## 設定 {#configuration}

在設定工作流程程式（自訂和/或現成可用）時，有一些需要牢記的事項。

### 暫時性工作流程 {#transient-workflows}

若要最佳化高擷取負載，您可以定義 [暫時性工作流程](/help/sites-developing/workflows.md#transient-workflows).

當工作流程為暫時性時，與中間工作步驟相關的執行階段資料在執行時不會儲存在JCR中（會儲存輸出轉譯）。

優點包括：

* 工作流程處理時間減少；最多10%。
* 大幅減少存放庫的成長。
* 清除時不再需要執行CRUD工作流程。
* 此外，它還減少了要壓縮的TAR檔案數量。

>[!CAUTION]
>
>如果您的企業要求您保留/封存工作流程執行階段資料以進行稽核，請勿啟用此功能。

### 調整DAM工作流程 {#tuning-dam-workflows}

如需DAM工作流程的效能調整指南，請參閱 [AEM Assets效能調整指南](/help/assets/performance-tuning-guidelines.md).

### 設定並行工作流程的最大數量 {#configure-the-maximum-number-of-concurrent-workflows}

AEM可允許同時執行多個工作流程執行緒。 根據預設，執行緒的數目設定為系統處理器核心數目的一半。

如果正在執行的工作流程需要系統資源，這可能意味著AEM幾乎無法再用於其他工作，例如呈現編寫UI。 因此，系統在大量影像上傳等活動期間可能會變得緩慢。

若要解決此問題，Adobe建議將 **最大平行作業數** 介於系統處理器核心數量的一半至四分之三之間。 這應該有足夠的容量讓系統在處理這些工作流程時保持回應。

進行設定 **最大平行作業數**，您可以：

* 設定 **[OSGi設定](/help/sites-deploying/configuring-osgi.md)** 從AEM Web主控台； **佇列： Granite工作流程佇列** (一 **Apache Sling工作佇列設定**)。

* 設定佇列可從以下位置： **Sling工作** 的AEM Web主控台選項； **工作佇列設定： Granite工作流程佇列**，在 `http://localhost:4502/system/console/slingevent`.

此外，「 」還有單獨的設定 **Granite工作流程外部程式作業佇列**. 這用於啟動外部二進位檔的工作流程程式，例如 **InDesign Server** 或 **影像Magick**.

### 設定個別工作佇列 {#configure-individual-job-queues}

在某些情況下，根據個別工作來設定個別工作佇列以控制並行執行緒或其他佇列選項會很有用。 您可以透過以下方式從Web主控台新增及設定個別佇列 **Apache Sling工作佇列設定** 工廠。 若要尋找要列出的適當主題，請執行工作流程的模型，並在 **Sling工作** 主控台；例如，在 `http://localhost:4502/system/console/slingevent`.

您也可以為暫時性工作流程新增個別工作佇列。

### 設定工作流程清除 {#configure-workflow-purging}

在標準安裝中，AEM提供維護主控台，可從中排程及設定每日和每週的維護活動；例如：

`http://localhost:4502/libs/granite/operations/content/maintenance.html`

根據預設， **每週維護期間** 具有 **工作流程清除** 工作，但是這必須在執行前進行設定。 若要設定工作流程清除，請使用 **AdobeGranite工作流程清除設定** 必須新增至Web主控台。

如需AEM中維護任務的詳細資訊，請參閱 [操作控制面板](/help/sites-administering/operations-dashboard.md).

## 自訂 {#customization}

在撰寫自訂工作流程時，有些事情應牢記在心。

### 位置 {#locations}

工作流程模型、啟動器、指令碼和通知的定義會根據型別儲存在存放庫中；也就是現成可用的自訂等。

>[!NOTE]
>
>另請參閱 [AEM 6.5中的存放庫重組](/help/sites-deploying/repository-restructuring.md).

#### 位置 — 工作流程模型 {#locations-workflow-models}

工作流程模型會根據型別儲存在存放庫中：

* 現成的工作流程設計儲存在以下路徑下：

  `/libs/settings/workflow/models/`

  >[!CAUTION]
  >
  >請勿：
  >
  >* 將任何自訂工作流程模型放置在此資料夾中
  >* 編輯任何內容 `/libs`
  >
  >因為任何變更在升級或安裝修補程式、累積修補程式套件或Service Pack時都可能被覆寫。

* 自訂工作流程設計位於下：

  ```
  /conf/global/settings/workflow/models/...
  ```

* 執行階段工作流程設計（現成和自訂）儲存在以下路徑下：

  `/var/workflow/models/`

* 舊版工作流程設計（設計階段和執行階段）儲存在以下路徑下：

  `/etc/workflow/models/`

  >[!NOTE]
  >
  >如果編輯這些設計 *使用AEM UI*，則會將詳細資料複製到新位置。

#### 位置 — 工作流程啟動器 {#locations-workflow-launchers}

工作流程啟動器定義也會根據型別儲存在存放庫中：

* 現成的工作流程啟動器位於以下路徑下：

  `/libs/settings/workflow/launcher/`

  >[!CAUTION]
  >
  >請勿：
  >
  >* 將您的任何自訂工作流程啟動器放置在此資料夾中
  >* 編輯任何內容 `/libs`
  >
  >因為任何變更在升級或安裝修補程式、累積修補程式套件或Service Pack時都可能被覆寫。

* 自訂工作流程啟動器位於下：

  ```
  /conf/global/settings/workflow/launcher/...
  ```

* 舊版工作流程啟動器位於以下路徑下：

  `/etc/workflow/launcher/`

  >[!NOTE]
  >
  >如果已編輯這些定義 *使用AEM UI*，則會將詳細資料複製到新位置。

#### 位置 — 工作流程指令碼 {#locations-workflow-scripts}

工作流程指令碼也會根據型別儲存在存放庫中：

* 現成的工作流程指令碼會儲存在以下路徑中：

  `/libs/workflow/scripts/`

  >[!CAUTION]
  >
  >請勿：
  >
  >* 將您的任何自訂工作流程指令碼放在此資料夾中
  >* 編輯任何內容 `/libs`
  >
  >因為任何變更在升級或安裝修補程式、累積修補程式套件或Service Pack時都可能被覆寫。

* 自訂工作流程指令碼儲存在下：

  ```
  /apps/workflow/scripts/...
  ```

* 舊版工作流程指令碼會保留在下列路徑下：

  `/etc/workflow/scripts/`

#### 位置 — 工作流程通知 {#locations-workflow-notifications}

工作流程通知也根據型別儲存在存放庫中：

* 現成的工作流程通知定義位於以下路徑下：

  `/libs/settings/workflow/notification/`

  >[!CAUTION]
  >
  >請勿：
  >
  >* 將任何自訂工作流程通知定義放置在此資料夾中
  >* 編輯任何內容 `/libs`
  >
  >因為任何變更在升級或安裝修補程式、累積修補程式套件或Service Pack時都可能被覆寫。

* 自訂工作流程通知定義位於下：

  ```
  /conf/global/settings/workflow/notification/...
  ```

  >[!NOTE]
  >
  >如果您想要覆寫工作流程通知文字，請在下方建立覆蓋的路徑：
  >
  >
  >`/conf/global/settings/workflow/notification/<path-under-libs>`

* 舊版工作流程通知定義會保留在下列路徑下：

  `/etc/workflow/notification/`

### 處理工作階段 {#process-sessions}

如同任何自訂開發作業，建議您儘可能使用使用者的工作階段：

* 以最佳方式遵守安全性方針
* 允許系統管理工作階段的開啟和關閉

實作工作流程處理時：

* 我們將提供工作流程工作階段，除非有令人信服的理由不提供，否則應使用此工作流程工作階段。
* 不應從工作流程步驟建立新的工作階段，因為這會造成狀態不一致，且工作流程引擎可能發生並行問題。
* 您不應從工作流程的處理步驟中取得新的JCR工作階段；您應將「處理步驟API」提供的工作流程工作階段調整為JCR工作階段。 例如：

```
public void execute(WorkItem item, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
        // to obtain a jcr session:
        javax.jcr.Session jcrSession = workflowSession.adaptTo(javax.jcr.Session.class);

        // to obtain a sling resource resolver:
        org.apache.sling.api.resource.ResourceResolver slingResourceResolver = workflowSession.adaptTo(org.apache.sling.api.resource.ResourceResolver.class);
```

儲存工作階段：

* 在工作流程內，如果 `WorkflowSession` 用來修改存放庫，然後不要明確儲存工作階段 — 工作流程完成時會儲存工作階段。
* `Session.Save` 不應從工作流程步驟中呼叫：

   * 建議調整工作流程jcr工作階段； `save` 不需要使用，因為工作流程引擎會在工作流程執行完畢後自動儲存工作階段。
   * 不建議流程步驟建立自己的jcr工作階段。

* 透過消除不必要的節省，您可以減少額外負荷，進而讓工作流程更有效率。

>[!CAUTION]
>
>儘管有此處提供的建議，但如果您確實建立了自己的jcr工作階段，則必須將其儲存。

### 將啟動器的數量/範圍最小化 {#minimize-the-number-scope-of-launchers}

有一個監聽器負責所有 [工作流程啟動器](/help/sites-administering/workflows-starting.md#workflows-launchers) 已註冊的：

* 它會接聽其他啟動器萬用字元屬性中指定的所有路徑變更。
* 傳送事件時，工作流程引擎會評估每個啟動器，以決定是否應執行。

建立太多啟動器會導致評估程式執行速度變慢。

在單一啟動器上的存放庫根目錄下建立萬用字元路徑，會導致工作流程引擎監聽並評估存放庫內每個節點的建立/修改事件。 因此，建議僅建立所需的啟動器，並儘可能指定萬用路徑。

由於這些啟動器對工作流程行為的影響，停用任何未使用的現成啟動器也會有幫助。

### 啟動器的設定增強功能 {#configuration-enhancements-for-launchers}

自訂 [啟動器設定](/help/sites-administering/workflows-starting.md#workflows-launchers) 已增強以支援下列專案：

* 將多個條件「AND」放在一起。
* 在單一條件中具有OR條件。
* 根據功能標幟啟用或停用，停用/啟用啟動器。
* 在啟動器條件中支援Regex。

### 不要從其他工作流程開始工作流程 {#do-not-start-workflows-from-other-workflows}

工作流程可能會產生大量額外負荷，例如在記憶體中建立的物件和存放庫中追蹤的節點兩方面都是如此。 因此，與其啟動其他工作流程，不如讓工作流程在內部進行其處理。

此情況的範例是在一組內容上實作業務流程，然後啟用該內容的工作流程。 最好建立自訂工作流程流程來啟動每個節點，而不是啟動 **啟用內容** 需要發佈的每個內容節點的模型。 此方法需要額外的開發工作，但在執行時比為每個啟用啟動個別的工作流程例項更有效率。

另一個範例是處理數個節點的工作流程，建立工作流程封裝，然後啟動所述封裝。 與其建立封裝，然後以封裝作為裝載啟動單獨的工作流程，您可以在建立封裝的步驟中變更工作流程的裝載，然後呼叫步驟以在相同工作流程模型中啟動封裝。

### 處理常式推進 {#handler-advance}

設計工作流程模型時，您可以選擇啟用工作流程步驟上的處理常式。 或者，您可以將程式碼新增至工作流程步驟，以決定下一個要執行的步驟，然後再執行它。

建議使用處理常式進階，因為它可提供較出色的效能。

### 工作流程階段 {#workflow-stages}

您可以定義 [工作流程階段](/help/sites-developing/workflows.md#workflow-stages)，然後將任務/步驟指派至特定工作流程階段。

當您按一下 [**工作流程資訊** 工作專案的索引標籤 **收件匣**](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions). 可以編輯現有的工作流程模型以新增階段。

### 啟動頁面處理步驟 {#activate-page-process-step}

此 **啟動頁面程式** 步驟將為您啟用頁面，但不會自動找到任何參照的DAM資產並啟用它們。

如果您打算將此步驟作為工作流程模型的一部分，請記得這一點。

### 升級注意事項 {#upgrade-considerations}

升級執行個體時：

* 在升級執行個體之前，請確定已備份任何自訂工作流程模型。
* 確認您的自訂工作流程未儲存在 [位置](#locations)：

   * `/libs/settings/workflow/models/projects`

>[!NOTE]
>
>另請參閱 [AEM 6.5中的存放庫重組](/help/sites-deploying/repository-restructuring.md).

## 系統工具 {#system-tools}

有許多系統工具可協助監控、維護和疑難排解工作流程。 以下所有範例URL都使用 `localhost:4502`，但應該可以在任何作者執行個體上使用( `<hostname>:<port>`)。

### Sling工作處理主控台 {#sling-job-handling-console}

`http://localhost:4502/system/console/slingevent`

「Sling作業處理」控制檯將顯示：

* 自上次重新啟動後，系統中工作狀態的統計資料。
* 它也會顯示所有工作佇列的設定，並提供在Configuration Manager中編輯它們的捷徑。

### 工作流程報告工具 {#workflow-report-tool}

6.3版中移除了工作流程報告工具，以防止效能降低。

### 工作流程維護操作MBean {#workflow-maintenance-operations-mbean}

`http://localhost:4502/system/console/jmx/com.adobe.granite.workflow:type=Maintenance`

工作流程維護MBean會顯示數個實用的維護常式，例如清除已完成的工作流程及擷取工作流程統計資料。

## 更多資訊 {#further-information}

如需進一步詳細資訊，請參閱：

* [使用工作流程](/help/sites-authoring/workflows.md)
* [管理工作流程](/help/sites-administering/workflows.md)
* [開發和延伸工作流程](/help/sites-developing/workflows.md)
* [效能最佳化](/help/sites-deploying/configuring-performance.md)
