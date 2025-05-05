---
title: AEM Forms的架構和部署拓撲
description: AEM Forms的架構詳細資料，以及建議新老的AEM客戶和從LiveCycleES4升級至AEM Forms的客戶使用的拓撲。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: d4421d46-cfc9-424e-8a88-9d0a2994a5cf
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2469'
ht-degree: 0%

---

# AEM Forms的架構和部署拓撲 {#architecture-and-deployment-topologies-for-aem-forms}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/aem-forms-cloud-service-architecture.html?lang=zh-Hant) |
| AEM 6.5 | 本文章 |

## 架構 {#architecture}

AEM Forms是部署至AEM的應用程式，做為AEM套件。 此套件稱為AEM Forms附加元件套件。 AEM Forms附加元件套件包含部署至AEM OSGi容器中的服務（API提供者），以及由AEM Sling架構管理的servlet或JSP （提供前端和REST API功能）。 下圖說明此設定：

![架構](assets/architecture.png)

AEM Forms的架構包括下列元件：

* **核心AEM服務：** AEM提供給已部署應用程式的基本服務。 這些服務包括符合JCR規範的內容存放庫、OSGI服務容器、工作流程引擎、信任存放區、金鑰存放區等。 AEM Forms應用程式可使用這些服務，但AEM Forms套件不提供這些服務。 這些服務是整體AEM棧疊不可或缺的一部分，各種AEM Forms元件都會使用這些服務。
* **Forms服務：**&#x200B;提供表單相關功能，例如建立、組合、散發及封存PDF檔案、新增數位簽章以限制對檔案的存取，以及解碼條碼式表單。 這些服務可公開供共同部署在AEM中的自訂程式碼使用。
* **網頁層：** JSP或servlet，建置在通用和表單服務之上，可提供下列功能：

   * **製作前端**：用於製作和管理表單的表單製作和表單管理使用者介面。
   * **表單轉譯與提交前端**：使用者對面的介面，可供AEM Forms的一般使用者（例如，存取政府網站的公民）使用。 此功能提供表單轉譯（在網頁瀏覽器中顯示表單）和提交功能。
   * **REST API**： JSP和servlet會匯出表單服務的子集，以供HTTP型使用者端（例如Forms行動SDK）遠端使用。

**OSGi上的AEM Forms：** OSGi環境上的AEM Forms是標準的AEM Author或AEM Publish，且已部署在AEM Forms套件上。 您可以在[單一伺服器環境、伺服器陣列和叢集設定](/help/sites-deploying/recommended-deploys.md)中的OSGi上執行AEM Forms。 叢集設定僅適用於AEM編寫執行個體。

JEE上的&#x200B;**AEM Forms：** JEE上的AEM Forms是在JEE棧疊上執行的AEM Forms伺服器。 它的AEM Author搭配AEM Forms附加元件套件，以及其他AEM Forms JEE功能，可共同部署於應用程式伺服器上執行的單一JEE棧疊上。 您可以在單一伺服器和叢集設定中在JEE上執行AEM Forms 。 只有執行Document Security、程式管理，以及升級至AEM Forms的LiveCycle客戶時，才需要JEE上的AEM Forms。 以下是一些在JEE上使用AEM Forms的其他案例：

* **HTML工作區支援(適用於使用HTML工作區的客戶)：** AEM Forms on JEE啟用單一登入與處理執行個體，提供處理執行個體上轉譯的特定資產，以及處理HTML工作區內轉譯的表單提交。
* **進階額外表單/互動式通訊資料處理**：在需要進階程式管理功能的複雜使用案例中，可以使用JEE上的AEM Forms來額外處理表單/互動式通訊資料（並將結果儲存到適當的資料存放區）。

JEE上的AEM Forms也包含對AEM元件提供的下列支援服務：

* **整合式使用者管理：**&#x200B;可讓JEE上的AEM Forms使用者在OSGi使用者上辨識為AEM表單，並協助為OSGi和JEE使用者啟用SSO。 若需要在OSGi上的AEM表單與JEE上的AEM Forms之間進行單一登入(例如HTML工作區)，則需要此專案。
* **資產託管：** JEE上的AEM Forms可以提供OSGi上在AEM Forms上轉譯的資產(例如HTML5表單)。

AEM Forms編寫使用者介面不支援建立記錄檔案(DOR)、PDF forms和HTML5 Forms。 這類資產是使用獨立的Forms Designer應用程式來設計，並個別上傳至AEM Forms Manager。 或者，對於JEE上的AEM Forms ，可將表單設計成應用程式(在AEM Forms Workbench中)資產，並部署至JEE伺服器上的AEM Forms 。

OSGi上的AEM Forms和JEE上的AEM Forms都有工作流程功能。 您可以在OSGi上的AEM表單上快速建立及部署各種工作流程的基本工作流程，而無須在JEE上安裝AEM Forms的完整程式管理功能。 OSGi上AEM Forms的表單中心工作流程[功能與JEE上AEM Forms的流程管理功能](capabilities-osgi-jee-workflows.md)有一些差異。 在OSGi上，使用AEM Workflow和AEM Inbox功能在AEM Forms上開發和管理表單中心工作流程。

## 術語 {#terminologies}

下圖顯示典型AEM Forms部署中使用的各種AEM表單伺服器設定及其元件：

![aem_forms_-_recommendedtopology](assets/aem_forms_-_recommendedtopology.png)

**作者：**&#x200B;作者執行個體是以標準作者執行模式執行的AEM Forms伺服器。 這可以是JEE上的AEM Forms或OSGi環境上的AEM Forms 。 此範本適用於內部使用者、表單和互動式通訊設計人員以及開發人員。 可啟用下列功能：

* **製作及管理表單與互動式通訊：**&#x200B;設計人員和開發人員可以建立和編輯最適化表單與互動式通訊、上傳外部建立的其他型別的表單(例如在AdobeForms Designer中建立的表單)，以及使用Forms Manager主控台管理這些資產。
* **表單與互動式通訊發佈：**&#x200B;裝載於製作執行個體的Assets可以發佈至發佈執行個體，以執行執行階段作業。 資產發佈會使用AEM的復寫功能。 Adobe建議在所有作者執行個體上設定復寫代理程式，以手動方式將發佈的表單推播到處理執行個體，並在處理執行個體上設定另一個復寫代理程式，且啟用&#x200B;*接收時*&#x200B;觸發程式，以自動將接收的表單復寫到發佈執行個體。

**Publish：**&#x200B;發佈執行個體是以標準AEM Forms執行模式執行的Publish伺服器。 Publish例項適用於表單式應用程式的一般使用者，例如存取公開網站及提交表單的使用者。 可啟用下列功能：

* 呈現及提交一般使用者的Forms。
* 將原始提交的表單資料傳輸至處理執行個體，以便在最終記錄系統中進一步處理和儲存。 AEM Forms中提供的預設實作可使用AEM的反向復寫功能來達成此目的。 您也可以使用替代實作，將表單資料直接推送至處理伺服器，而非先在本機儲存（後者是啟用反向復寫的先決條件）。 擔心發佈執行個體上儲存潛在敏感資料的客戶，可以加入此[替代實作](/help/forms/using/configuring-draft-submission-storage.md)，因為處理執行個體通常位於較安全的區域中。
* 呈現和提互動動式通訊和信件：互動式通訊和信件會呈現在發佈執行個體上，而對應的資料會提交至處理執行個體，以進行儲存和後處理。 資料可以儲存在發佈執行個體本機上，並在稍後反向複製到處理執行個體（預設選項），也可以直接推送至處理執行個體，而不儲存在發佈執行個體上。 後者實作對注重安全性的客戶很有用。

**處理中：** AEM Forms的執行個體以作者執行模式執行，未將使用者指派給表單管理員群組。 您可以在JEE上部署AEM Forms，或在OSGi上部署AEM Forms作為處理執行個體。 未指派使用者以確保表單製作和管理活動未在處理執行個體上執行並僅在製作執行個體上發生。 處理執行個體可啟用下列功能：

* **處理來自Publish執行個體的原始表單資料：**&#x200B;這主要是透過資料到達時觸發的AEM工作流程在處理執行個體上完成的。 工作流程可以使用現成可用的表單資料模型步驟，將資料或檔案封存至適當的資料存放區。
* **表單資料的安全儲存**：處理作業提供防火牆後存放庫，供與使用者隔離的原始表單資料使用。 無論是作者執行個體的表單設計人員還是Publish執行個體的一般使用者都無法存取此存放庫。

  >[!NOTE]
  >
  >Adobe建議使用協力廠商資料存放區來儲存最後處理的資料，而非使用AEM存放庫。

* **對來自Publish執行個體的通訊資料進行儲存和後置處理：** AEM工作流程會執行對應信件定義的選擇性後置處理。 這些工作流程可將最終處理的資料儲存至適當的外部資料存放區。

* **託管HTMLWorkspace**：處理執行個體會託管HTMLWorkspace的前端。 HTML工作區為稽核和核准流程提供相關任務/群組指派的UI。

處理執行個體設定為在作者執行模式中執行，因為：

* 這可讓您從Publish執行個體反向復寫原始表單資料。 預設的資料儲存處理常式需要反向復寫功能。
* AEM工作流程是處理來自Publish執行個體之原始表單資料的主要方法，建議在作者樣式系統上執行。

## JEE上AEM Forms的實體拓撲範例 {#sample-physical-topologies-for-aem-forms-on-jee}

以下建議的JEE版AEM Forms拓撲主要是供從JEE上的LiveCycle或舊版AEM Forms升級的客戶使用。 Adobe建議在OSGi上使用AEM Forms進行全新安裝。 只有使用「檔案安全性」和「程式管理」功能時，才建議在JEE上全新安裝AEM Forms。

### 用於使用Document Services或Document Security功能的拓撲 {#topology-for-using-document-services-or-document-security-capabilities}

計畫僅使用Document Services或Document Security功能的AEM Forms客戶可擁有類似於以下顯示的拓撲。 此拓撲建議使用單一AEM Forms例項。 如有需要，您也可以建立AEM Forms伺服器的叢集或陣列。 當大部分使用者以程式設計方式存取AEM Forms伺服器的功能時，且透過使用者介面的干預最小時，建議使用此拓撲。 拓撲有助於檔案服務的批次處理操作。 例如，每天使用輸出服務建立數百份不可編輯的PDF檔案。

雖然AEM Forms可讓您從單一伺服器設定並執行所有功能，但您仍應執行容量規劃、負載平衡，並為生產環境中的特定功能設定專用伺服器。 例如，在使用PDF Generator服務每天轉換數千頁並新增數位簽名以限制存取檔案的環境中，請為PDF Generator服務和數位簽名功能設定個別的AEM Forms伺服器。 它有助於提供最佳效能，並獨立擴充伺服器。

![基本功能](assets/basic-features.png)

### 使用AEM Forms流程管理的拓撲 {#topology-for-using-aem-forms-process-management}

例如，AEM Forms客戶計畫使用AEM Forms流程管理功能，HTMLWorkspace可擁有類似於以下顯示的拓撲。 JEE伺服器上的AEM Forms可以在單一伺服器或叢集設定中。

如果您從LiveCycleES4升級，此拓撲會密切反映您在LiveCycle中已有的內容，除了在JEE上的AEM Forms中新增AEM Author內建外。 此外，執行升級之客戶的叢集需求沒有改變。 如果您在叢集環境中使用AEM Forms，則可以在AEM 6.5 Forms中繼續使用相同功能。 若要使用HTMLWorkspace全新安裝JEE的AEM Forms，則需額外執行內建至JEE環境的AEM製作例項。

表單資料存放區是協力廠商資料存放區，用於儲存表單及互動式通訊的最終處理資料。 這是拓撲中的選用元素。 如有需要，您也可以選擇設定處理執行個體，並將其存放庫作為最終的記錄系統。

![topology_for_usinghtmlworkspaceandformsapp](assets/topology_for_usinghtmlworkspaceandformsapp.png)

此拓撲建議給打算使用JEE伺服器上的AEM Forms進行程式管理功能(HTMLWorkspace)的客戶，而不需使用任何後續處理、調適型表單、HTML5表單和互動式通訊功能。

### 使用自適應表單、HTML5表單、互動式通訊功能的拓撲 {#topology-for-using-adaptive-forms-html-forms-interactive-communication-capabilities}

計畫使用AEM Forms資料擷取功能(例如最適化表單、HTML5 Forms、PDF forms)的AEM Forms客戶，可擁有類似於以下顯示的拓撲。 在使用AEM Forms的互動式通訊功能時，也建議使用此拓撲。

![topology-for-using-forms-osgi-modules](assets/topology-for-using-forms-osgi-modules.png)

您可以對上述建議的拓撲進行下列變更/自訂：

* 使用HTMLWorkspace和AEM Forms應用程式需要AEM作者或處理例項。 您可以在JEE伺服器上使用AEM編寫執行個體內建至AEM Forms，而非設定額外的外部AEM編寫伺服器。
* 只有在OSGi、適用性表單、表單入口網站和互動式通訊中以Forms為中心的工作流程，才需要AEM製作或處理例項。
* 互動式通訊Agent UI通常在組織內執行。 因此，您可以在私人網路內保留代理程式UI的發佈伺服器。
* JEE伺服器上AEM Forms內建的OSGi執行個體上的AEM表單也可以在OSGi和Watched資料夾上執行Forms中心的工作流程。

## 在OSGi上使用AEM Forms的實體拓撲範例 {#sample-physical-topologies-for-using-aem-forms-on-osgi}

### 資料擷取、互動式通訊、OSGi功能表單導向工作流程的拓撲 {#topology-for-data-capture-interactive-communication-form-centric-workflow-on-osgi-capabilities}

計畫使用AEM Forms資料擷取功能(例如最適化表單、HTML5 Forms、PDF forms)的AEM Forms客戶，可擁有類似於以下顯示的拓撲。 在OSGi功能上使用互動式通訊和Forms中心工作流程時(例如，使用AEM收件匣和AEM Forms應用程式進行業務流程工作流程)，也建議使用此拓撲。

![interactive-use-cases-af-cm-osgi-workflow](assets/interactive-use-cases-af-cm-osgi-workflow.png)

### 使用watched資料夾功能進行離線批次處理的拓撲 {#topology-for-using-watched-folder-capabilities-for-offline-batch-processing}

計畫使用Watched資料夾進行批次處理的AEM Forms客戶可擁有類似於以下所示的拓撲。 拓撲會顯示叢集環境，但您會根據負載決定使用單一執行個體或AEM Forms伺服器陣列。 第三方資料來源是您自己的記錄系統。 它可作為Watched資料夾的輸入來源。 拓撲也會以列印檔案的形式顯示輸出。 您也可以將輸出內容儲存至檔案系統、透過電子郵件傳送，以及使用其他自訂方法來使用輸出。

![offline-batch-processing-via-watched-folders](assets/offline-batch-processing-via-watched-folders.png)

### 使用檔案服務功能進行離線API型處理的拓撲 {#topology-for-using-document-services-capabilities-for-offline-api-based-processing}

計畫僅使用檔案服務功能的AEM Forms客戶可擁有類似於以下所示的拓撲。 此拓撲建議在OSGi伺服器上使用AEM Forms叢集。 當大部分使用者以程式設計（使用API）存取AEM Forms伺服器的功能時，且透過使用者介面的干預最小時，建議使用此拓撲。 此拓撲在多個軟體使用者端案例中相當實用。 例如，多個客戶使用PDF Generator服務來隨選建立PDF檔案。

雖然AEM Forms可讓您從單一伺服器設定並執行所有功能，但您應執行容量規劃、負載平衡，並為生產環境中的特定功能設定專用伺服器。 例如，在使用PDF Generator服務每天轉換數千頁頁面及多個調適型表單來擷取資料的環境中，請為PDF Generator服務和調適型表單功能設定個別的AEM Forms伺服器。 它有助於提供最佳效能，並獨立擴充伺服器。

![離線api處理](assets/offline-api-based-processing.png)
