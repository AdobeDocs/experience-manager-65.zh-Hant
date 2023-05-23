---
title: 用於AEM Forms的體系結構和部署拓撲
seo-title: Architecture and deployment topologies for AEM Forms
description: 針對AEM Forms的體系結構詳細資訊，以及針對新客戶和現AEM有客戶和客戶從LiveCycleES4升級到AEM Forms的推薦拓撲。
seo-description: Architecture details for AEM Forms and recommended topologies for new and existing AEM customers and customers upgrading from LiveCycle ES4 to AEM Forms.
uuid: 90baa57a-4785-4b49-844c-a44717d3c12d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 0156b5c3-3bef-4213-9ada-c7b6ae96ada4
role: Admin
exl-id: d4421d46-cfc9-424e-8a88-9d0a2994a5cf
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '2460'
ht-degree: 0%

---

# 用於AEM Forms的體系結構和部署拓撲 {#architecture-and-deployment-topologies-for-aem-forms}

## 架構 {#architecture}

AEM Forms是作為包部署AEM到的應AEM用程式。 該包稱為AEM Forms附加包。 AEM Forms附加軟體包包含部署到AEMOSGi容器中的服務（API提供程式）和由AEMSling框架管理的Servlet或JSP（提供前端和REST API功能）。 下圖描述了此設定：

![架構](assets/architecture.png)

AEM Forms的體系結構包括以下元件：

* **核心AEM服務：** 為已部署的AEM應用程式提供的基本服務。 這些服務包括符合JCR的內容儲存庫、OSGI服務容器、工作流引擎、信任儲存、密鑰儲存等。 這些服務可供AEM Forms應用程式使用，但不由AEM Forms包提供。 這些服務是整個堆棧的一個組成部分AEM,AEM Forms各部門使用這些服務。
* **Forms服務：** 提供與表單相關的功能，如建立、匯編、分發和歸檔PDF文檔，添加數字簽名以限制對文檔的訪問，以及對條形碼表單進行解碼。 這些服務可通過在中共同部署的自定義代碼公開AEM使用。
* **Web層：** JSP或Servlet，構建於常用和表單服務之上，提供以下功能：

   * **創作前端**:用於創作和管理表單的表單創作和表單管理用戶介面。
   * **表單格式副本和提交前端**:面向最終用戶的介面，供AEM Forms最終用戶使用（例如，公民訪問政府網站）。 這提供了表單格式副本（在Web瀏覽器中顯示表單）和提交功能。
   * **REST API**:JSP和Servlet導出表單服務的子集，以供基於HTTP的客戶端（如表單移動SDK）遠程使用。

**AEM Forms:** OSGi環境上的AEM Forms是標準AEM作者或AEM發佈，並部署了AEM Forms包。 你可以用OSGi運行AEM Forms [單伺服器環境、場和群集設定](/help/sites-deploying/recommended-deploys.md)。 群集設定僅適用於AEM Author實例。

**AEM Forms:** JEE上的AEM Forms是JEE堆棧上運行的AEM Forms伺服器。 它將AEM Author與AEM Forms附加軟體包和其他AEM FormsJEE功能共同部署在運行於應用程式伺服器上的單個JEE堆棧上。 您可以在單伺服器和群集設定中在JEE上運行AEM Forms。 AEM FormsJEE只需要運行文檔安全、流程管理以及LiveCycle客戶升級到AEM Forms。 以下是在JEE上使用AEM Forms的幾個附加方案：

* **HTML工作區支援(對於使用HTML工作區的客戶):** AEM FormsJEE啟用處理實例的單一登錄，為處理實例上呈現的某些資產提供服務，並處理在HTML工作區中呈現的表單的提交。
* **高級附加表單/互動式通信資料處理**:AEM FormsJEE論壇可用於在需要高級流程管理功能的複雜使用情形中另外處理表單/互動式通信資料（並將結果保存到合適的資料儲存）。

AEM Forms的JEE還包括向這些構成部分提供以下支AEM持服務：

* **整合用戶管理：** 允許JEE上的AEM Forms用戶被識別為OSGiAEM用戶上的表單，並幫助為OSGi和JEE用戶啟用SSO。 對於OSGi上的表單和JEE上的AEMAEM Forms之間需要單一登錄(例如HTML工作區)的情況，此選項是必需的。
* **資產托管：** AEM Forms在JEE上可為AEM Forms在OSGi上提供的資產(例如，HTML5份表格)提供服務。

AEM Forms創作用戶介面不支援建立記錄文檔(DOR)、PDF forms和HTML5Forms。 此類資產使用獨立的Forms設計器應用程式設計，並單獨上載到AEM Forms經理。 或者，對於JEE上的AEM Forms，表單可以設計為應用程式(在AEM Forms工作台中)資產並部署到JEE伺服器上的AEM Forms。

AEM Forms在OSGi上和AEM Forms在JEE上都具有工作流功能。 您可以在OSGi上的表單上快速構建和部署各種任務的AEM基本工作流，而無需在JEE上安裝AEM Forms的完整流程管理功能。 在 [AEM FormsOSGi上以表單為中心的工作流的特點及AEM FormsJEE上的流程管理能力](capabilities-osgi-jee-workflows.md)。 在OSGi上開發和管理AEM Forms上以表單為中心的工作流使用了熟悉的AEM工作流和AEM收件箱功能。

## 術語 {#terminologies}

以下映像顯示AEM典型AEM Forms部署中使用的各種表單伺服器配置及其元件：

![aem_forms_ — 推薦拓撲](assets/aem_forms_-_recommendedtopology.png)

**作者：** 作者實例是以標準作者運行模式運行的AEM Forms伺服器。 它可以是JEE上的AEM Forms或OSGi環境上的AEM Forms。 它適用於內部用戶、表單和互動式通信設計者和開發人員。 它啟用以下功能：

* **創作和管理表單和互動式通信：** 設計人員和開發人員可以建立和編輯自適應表單和互動式通信，上載在外部建立的其他類型表單，例如在AdobeForms設計器中建立的表單，並使用Forms管理器控制台管理這些資產。
* **表單和互動式通信發佈：** 在作者實例上托管的資產可以發佈到發佈實例以執行運行時操作。 資產發佈使AEM用複製功能。 Adobe建議在所有作者實例上配置複製代理，以手動將發佈的表單推送到處理實例，並在使用 *接收時* 觸發器已啟用，可自動將收到的表單複製到發佈實例。

**發佈：** 發佈實例是在標準發佈運行模式下運行的AEM Forms伺服器。 發佈實例旨在為基於表單的應用程式的最終用戶提供，例如訪問公共網站和提交表單的用戶。 它啟用以下功能：

* 為最終用戶呈現和提交Forms。
* 將原始提交的表單資料傳輸到處理實例，以便進一步處理和儲存在最終記錄系統中。 AEM Forms提供的預設實現使用的反向複製功能實現AEM了此。 還提供了另一種實現方法，用於直接將表單資料推送到處理伺服器，而不是先將其保存在本地（後者是進行反向複製以激活的先決條件）。 對發佈實例上可能敏感資料的儲存有顧慮的客戶可以為此服務 [替代性](/help/forms/using/configuring-draft-submission-storage.md)，因為處理實例通常位於更安全的區域中。
* 呈現和提交互動式通信和信函：在發佈實例上呈現互動式通信和信函，並將相應的資料提交到處理實例以用於儲存和後處理。 資料可以本地保存在發佈實例上，然後反向複製到處理實例（預設選項），也可以直接推送到處理實例而不保存在發佈實例上。 後一種實施對注重安全的客戶非常有用。

**處理：** 以「作者」運行模式運行的AEM Forms的實例，沒有為表單管理器組分配用戶。 您可以將JEE上的AEM Forms或OSGi上的AEM Forms作為處理實例部署。 未為用戶分配這些權限以確保表單創作和管理活動不會在「處理」實例上執行，並且只發生在「作者」實例上。 處理實例啟用以下功能：

* **處理從發佈實例到達的原始表單資料：** 這主要通過工作流在處理實例AEM上實現，當資料到達時會觸發工作流。 工作流可以使用現成的表單資料模型步驟將資料或文檔存檔到適當的資料儲存。
* **表單資料的安全儲存**:處理為與用戶隔離的原始表單資料提供防火牆後儲存庫。 「作者」實例上的表單設計者和「發佈」實例上的最終用戶都無法訪問此儲存庫。

   >[!NOTE]
   >
   >Adobe建議使用第三方資料儲存來保存最終處理的資料，而不是使用存AEM儲庫。

* **儲存和後處理從發佈實例到達的對應資料：** 工AEM作流執行相應字母定義的可選後處理。 這些工作流可以將最終處理的資料保存到合適的外部資料儲存中。

* **HTML工作區宿主**:處理實例承載HTML工作區的前端。 HTML工作區為關聯的任務/組分配提供UI，以用於審核和審批流程。

處理實例配置為在「作者」運行模式下運行，因為：

* 它允許從發佈實例反向複製原始表單資料。 預設資料儲存處理程式需要反向複製功能。
* 工AEM作流是處理從發佈實例到達的原始表單資料的主要方法，建議在作者風格的系統上運行。

## JEE上AEM Forms的物理拓撲示例 {#sample-physical-topologies-for-aem-forms-on-jee}

下面建議的JEE拓撲上的AEM Forms主要用於從JEE上的LiveCycle或舊版AEM Forms升級的客戶。 Adobe建議在OSGi上使用AEM Forms進行新安裝。 在JEE上新安裝AEM Forms僅建議使用文檔安全和流程管理功能。

### 用於使用文檔服務或文檔安全功能的拓撲 {#topology-for-using-document-services-or-document-security-capabilities}

AEM Forms客戶計畫只使用文檔服務或文檔安全功能，其拓撲結構與下面顯示的拓撲結構類似。 此拓撲建議使用單個AEM Forms實例。 如有必要，您還可以建立AEM Forms伺服器的群集或伺服器場。 當大多數用戶以寫程式方式訪問AEM Forms伺服器的功能和通過用戶介面進行的干預最小時，建議使用此拓撲。 該拓撲結構有助於文檔服務的批量處理操作。 例如，使用輸出服務每天建立數百個不可編輯的PDF文檔。

儘管AEM Forms允許您從單個伺服器設定和運行所有功能，但您應該執行容量規劃、負載平衡，並針對生產環境中的特定功能設定專用伺服器。 例如，對於使用PDF生成器服務每天轉換數千頁並添加數字簽名以限制對文檔的訪問的環境，請為PDF生成器服務和數字簽名功能設定單獨的AEM Forms伺服器。 它有助於提供最佳效能並獨立擴展伺服器。

![基本功能](assets/basic-features.png)

### 使用AEM Forms進程管理的拓撲 {#topology-for-using-aem-forms-process-management}

AEM Forms客戶計畫使用AEM Forms流程管理功能，例如，HTML工作區的拓撲與下面顯示的拓撲類似。 JEE伺服器上的AEM Forms可以是單個伺服器或群集配置。

如果您從LiveCycleES4升級，則此拓撲與您已有的LiveCycle緊密相映射，除了在JEE上將AEM Author內置到AEM Forms。 此外，對執行升級的客戶的群集要求沒有變化。 如果您在群集環境中使用AEM Forms，則可以在AEM6.5Forms中繼續使用。 對於使用HTML工作區的JEE的AEM Forms的新安裝，AEM運行內置於JEE環境的作者實例是一項附加要求。

表單資料儲存是用於儲存表單最終處理資料和交互通信的第三方資料儲存。 這是拓撲中的可選元素。 如有必要，您也可以選擇設定處理實例並將其儲存庫用作最終的記錄系統。

![拓撲_for_usingmlworkspace和formapp](assets/topology_for_usinghtmlworkspaceandformsapp.png)

建議計畫在JEE伺服器上使用AEM Forms進行流程管理功能(HTML工作區)的客戶不使用任何後處理、自適應表單、HTML5表單和交互通信功能。

### 用於使用自適應表單的拓撲、HTML5表單、交互通信功能 {#topology-for-using-adaptive-forms-html-forms-interactive-communication-capabilities}

AEM Forms客戶計畫使用AEM Forms資料捕獲功能，例如，自適應表單、HTML5Forms、PDF forms，可以具有與下面顯示的拓撲類似的拓撲。 此拓撲還建議使用AEM Forms的交互通信功能。

![用於使用的拓撲形式osgi模](assets/topology-for-using-forms-osgi-modules.png)

您可以對上述建議的拓撲進行以下更改/自定義：

* 使用HTML工作區和AEM Forms應用AEM需要作者或處理實例。 可以在JEE服AEM務器上使用內置於AEM Forms的作者實例，而不是設定額外的外部作者AEM伺服器。
* AEM作者或處理實例僅對於OSGi上以Forms為中心的工作流、自適應表單、表單門戶和互動式通信才需要。
* 交互通信代理UI通常在組織內運行。 因此，您可以將代理UI的發佈伺服器保留在專用網路中。
* 在JEE服AEM務器上內置到AEM Forms的OSGi實例上的表單還可以在OSGi和「監視資料夾」上運行以Forms為中心的工作流。

## 在OSGi上使用AEM Forms的物理拓撲示例 {#sample-physical-topologies-for-using-aem-forms-on-osgi}

### 用於資料捕獲的拓撲、互動式通信、基於OSGi功能的以表單為中心的工作流 {#topology-for-data-capture-interactive-communication-form-centric-workflow-on-osgi-capabilities}

AEM Forms客戶計畫使用AEM Forms資料捕獲功能，例如，自適應表單、HTML5Forms、PDF forms，可以具有與下面顯示的拓撲類似的拓撲。 此拓撲還建議在OSGi功能上使用互動式通信和以Forms為中心的工作流，例如，將收件箱和AEMAEM Forms應用用於業務流程工作流。

![交互用例 — af-cm-osgi-workflow](assets/interactive-use-cases-af-cm-osgi-workflow.png)

### 用於使用監視資料夾功能進行離線批處理的拓撲 {#topology-for-using-watched-folder-capabilities-for-offline-batch-processing}

AEM Forms客戶計畫使用「監視資料夾」進行批處理，其拓撲可能與下面顯示的拓撲類似。 拓撲顯示群集環境，但您決定根據負載使用單個實例或AEM Forms伺服器群。 第三方資料源是您自己的記錄系統。 它用作「監視資料夾」的輸入源。 拓撲還以打印檔案的形式顯示輸出。 您還可以將輸出內容儲存到檔案系統，通過電子郵件發送，以及使用其他自定義方法使用輸出。

![離線批處理 — 通過監視資料夾](assets/offline-batch-processing-via-watched-folders.png)

### 用於使用文檔服務功能進行基於API的離線處理的拓撲 {#topology-for-using-document-services-capabilities-for-offline-api-based-processing}

AEM Forms計畫只使用文檔服務功能的客戶可以具有與下面顯示的拓撲類似的拓撲。 此拓撲建議在OSGi伺服器上使用AEM Forms群集。 當大多數用戶以寫程式方式（使用API）訪問AEM Forms伺服器的功能和通過用戶介面的干預最小時，建議使用此拓撲。 該拓撲在多種軟體客戶端情形中非常有用。 例如，多個客戶端使用PDF生成器服務按需建立PDF文檔。

儘管AEM Forms允許您從單個伺服器設定和運行所有功能，但您應該執行容量規劃、負載平衡，並針對生產環境中的特定功能設定專用伺服器。 例如，對於使用PDF生成器服務每天轉換數千頁和多個自適應表單以捕獲資料的環境，請為PDF生成器服務和自適應表單功能設定單獨的AEM Forms伺服器。 它有助於提供最佳效能並獨立擴展伺服器。

![基於離線API的處理](assets/offline-api-based-processing.png)
