---
title: 適用於AEM Forms的架構和部署拓撲
seo-title: Architecture and deployment topologies for AEM Forms
description: AEM Forms的架構詳細資訊，以及新客戶和現有客戶從LiveCycleES4升級至AEM Forms的建議拓撲。
seo-description: Architecture details for AEM Forms and recommended topologies for new and existing AEM customers and customers upgrading from LiveCycle ES4 to AEM Forms.
uuid: 90baa57a-4785-4b49-844c-a44717d3c12d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 0156b5c3-3bef-4213-9ada-c7b6ae96ada4
role: Admin
exl-id: d4421d46-cfc9-424e-8a88-9d0a2994a5cf
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '2460'
ht-degree: 0%

---

# 適用於AEM Forms的架構和部署拓撲 {#architecture-and-deployment-topologies-for-aem-forms}

## 架構 {#architecture}

AEM Forms是部署至AEM as a AEM套件的應用程式。 套件稱為AEM Forms附加套件。 AEM Forms附加元件套件包含部署至AEM OSGi容器的服務（API提供者），以及由AEM Sling架構管理的servlet或JSP（同時提供前端和REST API功能）。 下圖描述了此設定：

![架構](assets/architecture.png)

AEM Forms的架構包含下列元件：

* **核心AEM服務：** AEM為部署的應用程式提供的基本服務。 這些服務包括符合JCR的內容存放庫、OSGI服務容器、工作流程引擎、信任存放區、金鑰存放區等。 這些服務適用於AEM Forms應用程式，但不由AEM Forms套件提供。 這些服務是整體AEM堆疊的必要部分，且各種AEM Forms元件都使用這些服務。
* **Forms服務：** 提供表單相關功能，例如建立、組合、分發和歸檔PDF文檔、添加數字簽名以限制對文檔的訪問，以及將條碼式表單解碼。 這些服務可公開供部署於AEM中的自訂程式碼使用。
* **Web層：** JSP或servlet，以通用和表單服務為基礎，提供下列功能：

   * **製作前端**:用於製作和管理表單的表單製作和表單管理用戶介面。
   * **表單轉譯和提交前端**:供AEM Forms一般使用者使用（例如公民存取政府網站）的一般使用者介面。 這可提供表單轉譯（在網頁瀏覽器中顯示表單）和提交功能。
   * **REST API**:JSP和servlet會匯出表單服務子集，供HTTP型用戶端（例如forms mobile SDK）遠端使用。

**AEM Forms on OSGi:** OSGi環境上的AEM Forms是部署在其上的標準AEM製作或AEM Publish搭配AEM Forms套件。 您可以在OSGi上執行AEM Forms, [單一伺服器環境、伺服器場和群集設定](/help/sites-deploying/recommended-deploys.md). 叢集設定僅適用於AEM Author執行個體。

**AEM Forms on JEE:** JEE上的AEM Forms是JEE堆疊上執行的AEM Forms伺服器。 它有AEM Author和AEM Forms附加元件套件，以及在應用程式伺服器上執行的單一JEE堆疊上共同部署的其他AEM Forms JEE功能。 您可以在JEE上以單一伺服器和叢集設定執行AEM Forms。 AEM Forms on JEE僅需執行檔案安全性、程式管理，以及LiveCycle客戶升級至AEM Forms。 以下是在JEE上使用AEM Forms的額外案例：

* **HTML工作區支援(適用於使用HTML工作區的客戶):** AEM Forms on JEE可啟用處理例項的單一登入、提供處理例項上轉譯的特定資產，以及處理HTML工作區中轉譯表單的提交作業。
* **高級附加表單/互動式通信資料處理**:在需要進階處理管理功能的複雜使用案例中，JEE上的AEM Forms可用來額外處理表單/互動式通訊資料（並將結果儲存至適當的資料存放區）。

AEM Forms on JEE也包含下列AEM元件支援服務：

* **整合的用戶管理：** 可讓JEE上的AEM Forms使用者在OSGi使用者上辨識為AEM表單，並協助OSGi和JEE使用者啟用SSO。 若是需要OSGi上的AEM表單與JEE上的AEM Forms表單之間的單一登入(例如HTML工作區)，則此為必要項目。
* **資產托管：** JEE上的AEM Forms可提供在OSGi上於AEM Forms上轉譯的資產(例如HTML5個表單)。

AEM Forms編寫使用者介面不支援建立記錄檔(DOR)、PDF forms和HTML5 Forms。 這類資產是使用獨立的Forms Designer應用程式設計，並個別上傳至AEM Forms Manager。 或者，若是JEE版的AEM Forms，表單可設計為應用程式(在AEM Forms Workbench中)資產，並部署至JEE伺服器上的AEM Forms。

OSGi上的AEM Forms和JEE上的AEM Forms都具備工作流程功能。 您可以在OSGi上的AEM表單上，快速建立並部署基本工作流程，而無須在JEE上安裝AEM Forms的完整程式管理功能。 在 [OSGi上的AEM Forms表單導向工作流程功能以及JEE上的AEM Forms流程管理功能](capabilities-osgi-jee-workflows.md). 在OSGi上開發及管理AEM Forms上以表單為中心的工作流程，使用熟悉的AEM工作流程和AEM收件匣功能。

## 術語 {#terminologies}

下圖顯示典型AEM Forms部署中使用的各種AEM表單伺服器設定及其元件：

![aem_forms_-recommended拓撲](assets/aem_forms_-_recommendedtopology.png)

**作者：** 製作例項是在標準製作執行模式中執行的AEM Forms伺服器。 可以是JEE上的AEM Forms或OSGi環境上的AEM Forms。 它適用於內部使用者、表單和互動式通訊設計人員和開發人員。 可啟用下列功能：

* **製作和管理表單和互動式通訊：** 設計人員和開發人員可以建立和編輯最適化表單和互動式通訊、上傳從外部建立的其他類型表單(例如在AdobeForms Designer中建立的表單)，以及使用Forms Manager主控台管理這些資產。
* **表單與互動式通訊發佈：** 托管於製作例項的資產可發佈至發佈例項，以執行執行階段作業。 資產發佈使用AEM復寫功能。 Adobe建議在所有製作執行個體上設定復寫代理，以手動將已發佈的表單推送至處理執行個體，並在具有的處理執行個體上設定另一個復寫代理 *接收時* 觸發器已啟用，可自動將收到的表單復寫至發佈執行個體。

**發佈：** 發佈執行個體是在標準發佈執行模式中執行的AEM Forms伺服器。 發佈例項的用途為表單式應用程式的一般使用者，例如存取公開網站和提交表單的使用者。 可啟用下列功能：

* 為使用者轉譯和提交Forms。
* 將原始提交的表單資料傳輸到處理實例，以便進一步處理和儲存在最終記錄系統中。 AEM Forms中提供的預設實作會使用AEM的反向復寫功能來達成此目的。 另外，也提供可直接將表單資料推送至處理伺服器，而非先將表單資料儲存在本機（後者是進行反向復寫以啟用的先決條件）。 若客戶對於在發佈執行個體上儲存可能敏感的資料有疑慮，可以加入 [替代性實施](/help/forms/using/configuring-draft-submission-storage.md)，因為處理例項通常位於更安全的區域。
* 轉譯和提交互動式通訊和信函：在發佈實例上呈現互動式通信和信函，並將相應資料提交到處理實例以用於儲存和後處理。 資料可在發佈執行個體上儲存，並在稍後反向複製至處理執行個體（預設選項），或直接推送至處理執行個體而不儲存於發佈執行個體。 後一種實施對於注重安全性的客戶非常有用。

**處理中：** 以製作執行模式執行的AEM Forms例項，未指派任何使用者給forms-manager群組。 您可以在JEE上部署AEM Forms，或在OSGi上部署AEM Forms，作為處理執行個體。 系統未指派使用者，以確保表單編寫和管理活動不會在處理執行個體上執行，且只會在製作執行個體上執行。 處理例項可啟用下列功能：

* **處理從發佈例項抵達的原始表單資料：** 這主要是透過AEM工作流程在資料到達時觸發的處理例項上達成。 工作流程可使用現成可用的「表單資料模型」步驟，將資料或檔案封存至適當的資料存放區。
* **表單資料的安全儲存**:處理程式為與使用者隔離的原始表單資料提供防火牆後的存放庫。 製作例項的表單設計人員和發佈例項的一般使用者都無法存取此存放庫。

   >[!NOTE]
   >
   > Adobe建議使用協力廠商資料存放區來儲存最終處理的資料，而非使用AEM存放庫。

* **儲存來自發佈例項之通信資料的後續處理：** AEM工作流程會對對應的信函定義執行選擇性的後置處理。 這些工作流程可將最終處理的資料儲存至適當的外部資料存放區。

* **HTML工作區托管**:處理例項會托管HTML工作區的前端。 HTML工作區提供UI，供審核和核准流程的相關任務/組分配。

處理例項設定為在製作執行模式中執行，因為：

* 它可從發佈執行個體反向復寫原始表單資料。 預設資料儲存處理程式需要反向復寫功能。
* AEM工作流程是處理從發佈例項抵達的原始表單資料的主要方式，建議您在製作樣式的系統上執行。

## JEE版AEM Forms的實體拓撲範例 {#sample-physical-topologies-for-aem-forms-on-jee}

以下建議使用JEE版AEM Forms拓撲，主要適用於從JEE版LiveCycle或舊版AEM Forms JEE版升級的客戶。 Adobe建議在OSGi上使用AEM Forms以執行全新安裝。 在JEE上全新安裝AEM Forms，僅建議使用檔案安全性和程式管理功能。

### 使用文檔服務或文檔安全功能的拓撲 {#topology-for-using-document-services-or-document-security-capabilities}

AEM Forms客戶計畫只使用文檔服務或文檔安全功能，其拓撲可以與下面顯示的拓撲類似。 此拓撲建議使用單個AEM Forms實例。 您也可以視需要建立AEM Forms伺服器的叢集或伺服器陣列。 當大多數用戶以寫程式方式訪問AEM Forms伺服器的功能，並且通過用戶介面的干預最小時，建議使用此拓撲。 該拓撲對於文檔服務的批處理操作很有幫助。 例如，使用輸出服務每天建立數百個不可編輯的PDF文檔。

雖然AEM Forms可讓您從單一伺服器設定和執行所有功能，但您應執行容量規劃、負載平衡，以及針對生產環境中的特定功能設定專用伺服器。 例如，對於使用PDF產生器服務每天轉換數千頁並新增數位簽名以限制檔案存取的環境，請針對PDF產生器服務和數位簽名功能設定個別的AEM Forms伺服器。 它有助於提供最佳效能，並可獨立擴展伺服器。

![基本功能](assets/basic-features.png)

### 使用AEM Forms進程管理的拓撲 {#topology-for-using-aem-forms-process-management}

AEM Forms客戶計畫使用AEM Forms流程管理功能，例如，HTML工作區的拓撲可能類似於下方顯示的拓撲。 JEE伺服器上的AEM Forms可以是單一伺服器或叢集設定。

如果您從LiveCycleES4升級，此拓撲會與您已有的LiveCycle緊密鏡像，除了在JEE上將AEM Author內建到AEM Forms之外。 此外，對於執行升級的客戶，群集需求沒有變化。 如果您在叢集環境中使用AEM Forms，則可在AEM 6.5 Forms中繼續使用。 若是全新安裝JEE AEM Forms以使用HTML工作區，則需額外執行內建至JEE環境的AEM製作例項。

表單資料存放區是第三方資料存放區，用於存放表單的最終處理資料和互動式通訊。 這是拓撲中的可選元素。 您也可以選擇設定處理例項，並視需要將其存放庫用作最終的記錄系統。

![topology_for_usinghtmlworkspaceandformsapp](assets/topology_for_usinghtmlworkspaceandformsapp.png)

如果客戶打算使用JEE伺服器上的AEM Forms來提供流程管理功能(HTML工作區)，則建議您使用此拓撲，而不需使用任何後處理、最適化表單、HTML5表單和互動式通訊功能。

### 使用最適化表單的拓撲、HTML5表單、互動式通信功能 {#topology-for-using-adaptive-forms-html-forms-interactive-communication-capabilities}

AEM Forms客戶計畫使用AEM Forms資料擷取功能，例如適用性表單、HTML5 Forms、PDF forms，其拓撲可能類似於下方顯示的拓撲。 此拓撲還建議使用AEM Forms的交互通信功能。

![topology-for-using-forms-osgi-modules](assets/topology-for-using-forms-osgi-modules.png)

您可以對上述拓撲進行以下更改/自定義：

* 使用HTML工作區和AEM Forms應用程式需要AEM製作或處理例項。 您可以在JEE伺服器上使用內建至AEM Forms的AEM製作例項，而非設定其他外部AEM製作伺服器。
* OSGi、最適化表單、表單入口網站和互動式通訊上以Forms為中心的工作流程，才需要AEM製作或處理例項。
* 互動式通訊代理UI通常在組織內執行。 因此，您可以將代理UI的發佈伺服器保留在專用網路中。
* OSGi例項上內建至JEE伺服器上AEM Forms的AEM表單，也可在OSGi和Watched資料夾上執行以Forms為中心的工作流程。

## 在OSGi上使用AEM Forms的物理拓撲示例 {#sample-physical-topologies-for-using-aem-forms-on-osgi}

### 用於資料捕獲的拓撲、互動式通信、OSGi功能上的以表單為中心的工作流 {#topology-for-data-capture-interactive-communication-form-centric-workflow-on-osgi-capabilities}

AEM Forms客戶計畫使用AEM Forms資料擷取功能，例如適用性表單、HTML5 Forms、PDF forms，其拓撲可能類似於下方顯示的拓撲。 對於在OSGi功能上使用互動式通信和以Forms為中心的工作流程(例如，對於將AEM收件匣和AEM Forms應用程式用於業務流程工作流程)，也建議使用此拓撲。

![interactive-use-cases-af-cm-osgi-workflow](assets/interactive-use-cases-af-cm-osgi-workflow.png)

### 用於離線批處理的使用監看資料夾功能的拓撲 {#topology-for-using-watched-folder-capabilities-for-offline-batch-processing}

AEM Forms客戶計畫使用「監看資料夾」進行批次處理，其拓撲可能類似於下方顯示的拓撲。 拓撲顯示群集環境，但您決定根據負載使用單個實例或AEM Forms伺服器群。 第三方資料來源是您自己的記錄系統。 它可作為「觀看的資料夾」的輸入來源。 拓撲還以打印檔案的形式顯示輸出。 您也可以將輸出內容儲存至檔案系統、透過電子郵件傳送，以及使用其他自訂方法來使用輸出。

![offline-batch-processing-via-watched-folders](assets/offline-batch-processing-via-watched-folders.png)

### 使用文檔服務功能進行基於API的離線處理的拓撲 {#topology-for-using-document-services-capabilities-for-offline-api-based-processing}

AEM Forms客戶計畫只使用文檔服務功能，其拓撲可以與下面顯示的拓撲類似。 此拓撲建議在OSGi伺服器上使用AEM Forms群集。 當大部分使用者以程式設計方式（使用API）存取AEM Forms伺服器的功能，且透過使用者介面的干預達到最低時，建議使用此拓撲。 該拓撲在多種軟體客戶端情況下非常有用。 例如，多個客戶端使用PDF生成器服務按需建立PDF文檔。

雖然AEM Forms可讓您從單一伺服器設定和執行所有功能，但您應執行容量規劃、負載平衡，以及針對生產環境中的特定功能設定專用伺服器。 例如，針對使用PDF產生器服務每天轉換數千頁和多個最適化表單來擷取資料的環境，請針對PDF產生器服務和最適化表單功能設定個別的AEM Forms伺服器。 它有助於提供最佳效能，並可獨立擴展伺服器。

![離線 — api型處理](assets/offline-api-based-processing.png)
