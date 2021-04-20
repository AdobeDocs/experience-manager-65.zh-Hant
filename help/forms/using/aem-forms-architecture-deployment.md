---
title: 適用於AEM Forms的體系結構和部署拓撲
seo-title: 適用於AEM Forms的體系結構和部署拓撲
description: 針對AEM Forms的體系結構詳細資訊，以及針對從LiveCycleES4升級到AEM Forms的新客AEM戶和現有客戶的建議拓撲。
seo-description: 針對AEM Forms的體系結構詳細資訊，以及針對從LiveCycleES4升級到AEM Forms的新客AEM戶和現有客戶的建議拓撲。
uuid: 90baa57a-4785-4b49-844c-a44717d3c12d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 0156b5c3-3bef-4213-9ada-c7b6ae96ada4
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2491'
ht-degree: 0%

---


# AEM Forms{#architecture-and-deployment-topologies-for-aem-forms}的體系結構和部署拓撲

## 架構 {#architecture}

AEM Forms是以套件的形AEM式部署到AEM的應用程式。 此套件稱為AEM Forms附加套件。 AEM Forms附加套件包含部署在AEMOSGi容器中的服務（API提供者），以及由AEMSling Framework管理的servlet或JSP（提供前端和REST API功能）。 下圖描述了此設定：

![架構](assets/architecture.png)

AEM Forms的架構包括下列元件：

* **核心AEM服務：提** 供給已部署應AEM用程式的基本服務。這些服務包括JCR相容內容儲存庫、OSGI服務容器、工作流程引擎、信任存放區、金鑰存放區等。 這些服務可用於AEM Forms應用程式，但不由AEM Forms軟體包提供。 這些服務是整個堆棧的一個組成部分，而AEM且AEM Forms的各種元件都使用這些服務。
* **Forms服務：** 提供表單相關功能，例如建立、組合、分發和封存PDF檔案、新增數位簽章以限制檔案存取，以及解碼條碼表單。這些服務可公開供部署於的自訂程式碼使用AEM。
* **Web層：** JSP或servlet，以常見和表單服務為基礎，提供下列功能：

   * **前端製作**:表單製作和表單管理使用者介面，以製作和管理表單。
   * **表單轉譯和提交前端**:一種最終用戶面向介面，供AEM Forms最終用戶（例如，公民訪問政府網站）使用。這提供表單轉譯（在網頁瀏覽器中顯示表單）和提交功能。
   * **REST API**:JSP和servlet會匯出表單服務子集，供HTTP型用戶端（例如表單mobile SDK）遠端使用。

**AEM Formson OSGi:** AEM Formson OSGi環境是標準AEM作者或AEM Publish，並部署在其上的AEM Forms套件。您可以在[單一伺服器環境、農場和叢集設定](/help/sites-deploying/recommended-deploys.md)中，在OSGi上執行AEM Forms。 叢集設定僅適用於AEM Author例項。

**AEM Forms在JEE:** AEM Forms在JEE上是AEM Forms伺服器在JEE堆棧上運行。它有AEM Author與AEM Forms附加套件，以及其他AEM FormsJEE功能，可共同部署在應用程式伺服器上執行的單一JEE堆疊上。 您可以在JEE上在單伺服器和叢集設定中執行AEM Forms。 AEM Forms的JEE要求僅運行文檔安全性、流程管理，以及LiveCycle客戶升級到AEM Forms。 以下是在JEE上使用AEM Forms的另外幾種情況：

* **HTML工作區支援（適用於使用HTML工作區的客戶）:** JEE上的AEM Forms啟用具有處理例項的單一登入、支援處理例項上呈現的特定資產，以及處理在HTML工作區中呈現的表單提交。
* **進階的其他表單／互動式通訊資料處理**:AEM FormsJEE上的JEE可用於在需要高級流程管理功能的複雜使用情況中另外處理表單／互動式通信資料（並將結果保存到合適的資料儲存）。

AEM Forms的JEE還包括向各組成部分提供以下支AEM持服務：

* **整合的使用者管** 理：讓JEE上的AEM Forms使用者可辨識為AEMOSGi使用者的表單，並協助OSGi和JEE使用者啟用SSO。在需要OSGi和JEE上AEM Forms表AEM單之間單一登入（例如HTML工作區）的情況下，這是必要項。
* **資產代管：** JEE上的AEM Forms可以支援OSGi上AEM Forms呈現的資產（例如HTML5表格）。

AEM Forms製作使用者介面不支援建立記錄檔案(DOR)、PDF forms和HTML5Forms。 這些資產是使用獨立的Forms設計人員應用程式設計，並個別上傳至AEM Forms經理。 或者，對於JEE上的AEM Forms，表單可設計為應用程式(在AEM Forms工作台中)資產，並部署在JEE伺服器上的AEM Forms。

AEM Forms的OSGi和AEM Forms的JEE都具有工作流程功能。 您可以在OSGi的表單上快速建立和部署各種工作AEM的基本工作流程，而不需在JEE上安裝AEM Forms的完整流程管理功能。 在AEM Forms的OSGi表單導向工作流的[功能和AEM Forms的JEE](capabilities-osgi-jee-workflows.md)流程管理功能之間有一些不同。 AEM FormsOSGi表單導向工作流程的開發與管理使用熟悉的工作AEM流程和收件AEM匣功能。

## 術語{#terminologies}

下面的映像顯示AEM典型AEM Forms部署中使用的各種表單伺服器配置及其元件：

![aem_forms_--建議的拓撲](assets/aem_forms_-_recommendedtopology.png)

**作者：** 作者實例是在標準「作者」運行模式下運行的AEM Forms伺服器。JEE上的AEM Forms,OSGi環境上的AEM Forms。 它適用於內部使用者、表單和互動式通訊設計人員和開發人員。 它提供下列功能：

* **製作和管理表單和互動式通訊：設計人員和開發人員可以建立和編輯最適化表單和互動式通訊，上傳其他外部建立的表單類型，例如在AdobeForms設計人員中建立的表單，並使用Forms管理主控台管理這些資產。** 
* **表單與互動式通訊發佈：** 在作者例項上代管的資產可發佈至發佈例項，以執行執行時期作業。資產發佈使AEM用複製功能。 Adobe建議在所有作者實例上配置複製代理，以手動將已發佈的表單推送到處理實例，並在處理實例上配置另一個複製代理，並啟用&#x200B;*On Receive*&#x200B;觸發器以自動複製已接收的表單以發佈實例。

**發佈：發** 布實例是在標準發佈運行模式下運行的AEM Forms伺服器。發佈例項適用於表單型應用程式的使用者，例如存取公開網站和送出表單的使用者。 它提供下列功能：

* 轉譯並送出Forms供使用者使用。
* 將原始提交的表單資料傳輸到處理實例，以便在最終記錄系統中進一步處理和儲存。 在AEM Forms提供的預設實施使用的反向複製功能來實現此目AEM的。 另外，還提供另一種實施方式，可將表單資料直接推送至處理伺服器，而非先將表單資料儲存在本機（後者是進行反向複製以啟動的先決條件）。 擔心在發佈例項上儲存可能敏感資料的客戶可以進入此[替代實作](/help/forms/using/configuring-draft-submission-storage.md)，因為處理例項通常位於更安全的區域。
* 轉譯和送出互動式通訊和信件：在發佈實例上呈現互動式通信和信函，並將相應資料提交到處理實例以用於儲存和後處理。 資料可以儲存在本機發佈例項上，稍後再反向複製至處理例項（預設選項），或直接推送至處理例項，而不需儲存在發佈例項上。 後一種實施對注重安全性的客戶非常有用。

**處理：在「** 作者」執行模式中執行的AEM Forms例項，未指派任何使用者至表單管理員群組。您可將AEM Forms部署在JEE上，或將AEM Forms部署在OSGi上，做為處理例項。 不會指派使用者來確保表單製作和管理活動不會在「處理」例項上執行，而且只會在「作者」例項上執行。 處理實例啟用以下功能：

* **處理來自發佈例項的原始表單資料：這** 主要是透過在資料送達時觸發的AEM工作流程在處理例項上實現。工作流程可使用現成可用的「表單資料模型」步驟，將資料或檔案封存至適當的資料儲存。
* **表單資料的安全儲存**:處理提供防火牆後的原始表單資料存放庫，與使用者隔離。作者實例和發佈實例的最終用戶都不能訪問此儲存庫。

   >[!NOTE]
   >
   > Adobe建議使用第三方資料儲存區來儲存最終處理的資料，而非使用儲AEM存庫。

* **儲存和後處理來自發佈例項的對應資料：** AEM工作流程會對對應的信件定義執行選擇性後處理。這些工作流程可將最終處理的資料儲存至適當的外部資料儲存區。

* **HTML工作區代管**:處理例項會代管HTML工作區的前端。HTML工作區為相關的任務／群組指派提供UI，以供審核和核准程式使用。

處理實例配置為在「作者」運行模式下運行，因為：

* 它允許從發佈實例中反向複製原始表單資料。 預設資料儲存處理程式需要反向複製功能。
* 建AEM議在作者式系統上執行工作流程，工作流程是處理來自發佈例項的原始表單資料的主要方式。

## JEE上AEM Forms的物理拓撲示例{#sample-physical-topologies-for-aem-forms-on-jee}

以下推薦的AEM FormsJEE拓撲主要適用於從JEE上的LiveCycle或舊版AEM Forms升級的客戶。 Adobe建議在OSGi上使用AEM Forms進行新安裝。 在JEE上新安裝的AEM Forms僅建議使用Document Security和Process Management功能。

### 使用文檔服務或文檔安全功能{#topology-for-using-document-services-or-document-security-capabilities}的拓撲

AEM Forms客戶計畫只使用檔案服務或檔案安全性功能，其拓撲可能與下面顯示的拓撲類似。 此拓撲建議使用單個AEM Forms實例。 如有必要，您也可以建立一個群集或群集的AEM Forms伺服器。 當大多數用戶以寫程式方式訪問AEM Forms伺服器的功能並且通過用戶介面進行干預時，建議使用此拓撲。 該拓撲結構有助於文檔服務的批處理操作。 例如，使用輸出服務每天建立數百份不可編輯的PDF檔案。

雖然AEM Forms允許您從單一伺服器設定和運行所有功能，但是，您應該執行容量規劃、負載平衡，並針對生產環境中的特定功能設定專用伺服器。 例如，對於使用PDF Generator服務的環境，每天轉換數千頁並新增數位簽章以限制檔案存取權，請針對PDF Generator服務和數位簽章功能設定個別的AEM Forms伺服器。 它有助於提供最佳效能，並可獨立擴展伺服器。

![基本功能](assets/basic-features.png)

### 使用AEM Forms進程管理的拓撲{#topology-for-using-aem-forms-process-management}

AEM Forms客戶計畫使用AEM Forms流程管理功能，例如，HTML工作區的拓撲可能與下面顯示的拓撲類似。 JEE上的AEM Forms伺服器可以是單個伺服器或群集配置。

如果您從LiveCycleES4升級，此拓撲與您在LiveCycle中已有的拓撲緊密相映，除了在JEE上將AEM Author內置到AEM Forms之外。 此外，執行升級的客戶的叢集需求並無改變。 如果您在叢集環境中使用AEM Forms，則可在AEM6.5Forms中繼續使用。 若要新安裝JEE的AEM Forms以使用HTML Workspace,AEM則需執行內建至JEE環境的作者執行個體。

表單資料儲存是第三方資料儲存，用於儲存表單的最終處理資料和互動式通訊。 這是拓撲中的可選元素。 您也可以選擇設定處理實例，並視需要將其儲存庫用作最終的記錄系統。

![topology_for_usinghtmlworkspace和formsapp](assets/topology_for_usinghtmlworkspaceandformsapp.png)

建議客戶使用拓撲，以便在JEE伺服器上使用AEM Forms的流程管理功能（HTML工作區），而不使用任何後處理、自適應表單、HTML5表單和互動式通信功能。

### 使用自適應表單、HTML5表單、互動式通訊功能{#topology-for-using-adaptive-forms-html-forms-interactive-communication-capabilities}的拓撲

AEM Forms客戶計畫使用AEM Forms資料捕獲功能，例如，自適應表單、HTML5Forms、PDF forms，其拓撲可能與下面顯示的拓撲類似。 此拓撲也建議使用AEM Forms的互動式通信功能。

![topology-forms-osgi-modules](assets/topology-for-using-forms-osgi-modules.png)

您可以對上述建議的拓撲進行以下更改／自定義：

* 使用HTML工作區和AEM Forms應用程式需要AEM作者或處理例項。 您可以在JEEAEM伺服器上使用內建至AEM Forms的作者例項，而不需設定額外的外部作AEM者伺服器。
* AEM Author或Processing例項僅適用於以Forms為中心的OSGi、最適化表單、表單入口網站和互動式通訊工作流程。
* 互動式通訊代理UI通常在組織內執行。 因此，您可以在專用網路中保留代理UI的發佈伺服器。
* OSGiAEM實例上的表單內置於JEE伺服器上的AEM Forms，還可以在OSGi和Watched資料夾上運行以Forms為中心的工作流。

## 在OSGi {#sample-physical-topologies-for-using-aem-forms-on-osgi}上使用AEM Forms的物理拓撲示例

### 用於資料捕獲、互動式通信、OSGi功能{#topology-for-data-capture-interactive-communication-form-centric-workflow-on-osgi-capabilities}的表單導向工作流的拓撲

AEM Forms客戶計畫使用AEM Forms資料捕獲功能，例如，自適應表單、HTML5Forms、PDF forms，其拓撲可能與下面顯示的拓撲類似。 此拓撲還建議在OSGi功能上使用互動式通訊和Forms中心工作流程，例如，在業務流程工作流程中使AEM用收件箱和AEM Forms應用程式。

![interactive-use-cases-af-cm-osgi-workflow](assets/interactive-use-cases-af-cm-osgi-workflow.png)

### 用於使用監視資料夾功能進行離線批處理{#topology-for-using-watched-folder-capabilities-for-offline-batch-processing}的拓撲

AEM Forms客戶計畫使用「監視資料夾」進行批處理，其拓撲可能與下面顯示的拓撲類似。 拓撲顯示一個群集環境，但您決定使用單個實例或一個群組的AEM Forms伺服器，具體取決於負載。 第三方資料來源是您自己的記錄系統。 它用作「監視的資料夾」的輸入源。 拓撲還以打印檔案的形式顯示輸出。 您也可以將輸出內容儲存至檔案系統、透過電子郵件傳送，以及使用其他自訂方法來使用輸出。

![offline-batch-processing-via-watched-folders](assets/offline-batch-processing-via-watched-folders.png)

### 用於使用文檔服務功能進行基於API的離線處理{#topology-for-using-document-services-capabilities-for-offline-api-based-processing}的拓撲

AEM Forms計畫僅使用文檔服務功能的客戶可以具有類似於下面顯示的拓撲。 此拓撲建議在OSGi伺服器上使用AEM Forms群集。 當大多數用戶以寫程式方式（使用API）訪問AEM Forms伺服器的功能和通過用戶介面的干預最小時，建議使用此拓撲。 該拓撲在多種軟體客戶端場景中非常有用。 例如，多位客戶使用PDF Generator服務，隨選建立PDF檔案。

雖然AEM Forms允許您從單一伺服器設定和運行所有功能，但您應執行容量規劃、負載平衡，並為生產環境中的特定功能設定專用伺服器。 例如，對於使用PDF Generator服務每天轉換數千頁的環境，以及擷取資料的多個最適化表單，請針對PDF Generator服務和最適化表單功能設定個別的AEM Forms伺服器。 它有助於提供最佳效能，並可獨立擴展伺服器。

![離線-api-based-processing](assets/offline-api-based-processing.png)

