---
title: 以程式管理端點
description: 使用「端點登入」服務來新增EJB端點、新增SOAP端點、新增Watched資料夾端點、新增電子郵件端點、新增遠端端點、新增工作管理員端點、修改端點、移除端點，以及擷取端點聯結器資訊。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: b94dcca2-136b-4b7d-b5ce-544804575876
source-git-commit: 7d46ba0eaa73d9f7a67034ba81d7fa379aa0112c
workflow-type: tm+mt
source-wordcount: '10791'
ht-degree: 0%

---

# 以程式管理端點 {#programmatically-managing-endpoints}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms 。**

**關於端點登入服務**

端點登入服務提供以程式設計方式管理端點的功能。 例如，您可以將下列型別的端點新增至服務：

* EJB
* SOAP
* Watched資料夾
* 電子郵件
* (AEM表單已棄用)遠端
* 任務管理員

>[!NOTE]
>
>SOAP、EJB和(JEE上的AEM Forms已棄用)遠端端點會自動為每個啟用的服務建立。 SOAP和EJB端點會為所有服務作業啟用SOAP和EJB。

遠端端點可讓Flex使用者端叫用新增端點的AEM Forms服務上的操作。 會建立與端點同名的Flex目的地，且Flex使用者端可建立指向此目的地的RemoteObjects，以叫用相關服務的作業。

電子郵件、工作管理員和Watched資料夾端點只會公開服務的特定作業。 新增這些端點需要第二個組態步驟來選取要呼叫的方法、設定組態引數，以及指定輸入和輸出引數對應。

您可以將TaskManager端點組織成群組，稱為 *類別*. 然後這些類別會透過TaskManager向工作區公開，一般使用者會在分類時看到TaskManager端點。 在Workspace中，一般使用者可在導覽窗格中看到這些類別。 每個類別中的端點會在Workspace的「開始程式」頁面上顯示為程式卡。

您可以使用Endpoint Registry服務完成這些工作：

* 新增EJB端點。 (請參閱 [新增EJB端點](programmatically-endpoints.md#adding-ejb-endpoints).)
* 新增SOAP端點。 (請參閱 [新增SOAP端點](programmatically-endpoints.md#adding-soap-endpoints).)
* 新增Watched資料夾端點(請參閱 [新增Watched資料夾端點](programmatically-endpoints.md#adding-watched-folder-endpoints).)
* 新增電子郵件端點。 (請參閱 [新增電子郵件端點](programmatically-endpoints.md#adding-email-endpoints).)
* 新增遠端端點。 (請參閱 [新增遠端端點](programmatically-endpoints.md#adding-remoting-endpoints).)
* 新增TaskManager端點(請參閱 [新增TaskManager端點](programmatically-endpoints.md#adding-taskmanager-endpoints).)
* 修改端點(請參閱 [修改端點](programmatically-endpoints.md#modifying-endpoints).)
* 移除端點(請參閱 [移除端點](programmatically-endpoints.md#removing-endpoints).)
* 擷取端點聯結器資訊(請參閱 [正在擷取端點聯結器資訊](programmatically-endpoints.md#retrieving-endpoint-connector-information).)

## 新增EJB端點 {#adding-ejb-endpoints}

您可以使用AEM Forms Java API，以程式設計方式將EJB端點新增至服務。 藉由將EJB端點加入服務，即可讓從屬端應用程式使用EJB模式來呼叫服務。 也就是說，在設定呼叫AEM Forms所需的連線屬性時，您可以選取EJB模式。 (請參閱 [設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>您無法使用Web服務來新增EJB端點。

>[!NOTE]
>
>一般而言，EJB端點預設會新增至服務。不過，EJB端點可以新增至以程式設計方式建置的處理，或是移除EJB端點而必須再次新增的處理作業。

### 步驟摘要 {#summary-of-steps}

若要將EJB端點新增至服務，請執行下列工作：

1. 包含專案檔案。
1. 建立 `EndpointRegistry Client` 物件。
1. 設定EJB端點屬性。
1. 建立EJB端點。
1. 啟用端點。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (如果將AEM Forms部署在JBoss Application Server上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss Application Server上，則為必要)

有關這些JAR檔案位置的資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立EndpointRegistry使用者端物件**

您必須先建立EJB端點，才能以程式設計方式加入 `EndpointRegistryClient` 物件。

**設定EJB端點屬性**

若要建立服務的EJB端點，請指定下列值：

* **聯結器識別碼**：指定要建立的端點型別。 若要建立EJB端點，請指定 `EJB`.
* **說明**：指定端點說明。
* **名稱**：指定端點的名稱。
* **服務識別碼**：指定端點所屬的服務。
* **作業名稱**：指定使用端點叫用的作業名稱。 建立EJB端點時，請指定萬用字元( `*`)。 不過，如果您要指定特定作業，而不是叫用所有服務作業，請指定作業的名稱，而不是使用萬用字元( `*`)。

**建立EJB端點**

設定EJB端點屬性之後，即可建立服務的EJB端點。

**啟用端點**

建立端點後，您必須啟用它。 啟用端點後，便可用來叫用服務。 啟用端點後，即可在管理主控台中檢視它。

**另請參閱**

[使用Java API新增EJB端點](programmatically-endpoints.md#adding-an-ejb-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API新增EJB端點 {#adding-an-ejb-endpoint-using-the-java-api}

使用Java API新增EJB端點：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-livecycle-client.jar。 (

1. 建立EndpointRegistry使用者端物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `EndpointRegistryClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 設定EJB端點屬性。

   * 建立 `CreateEndpointInfo` 物件（使用其建構函式）。
   * 透過叫用「 」指定聯結器識別碼值 `CreateEndpointInfo` 物件的 `setConnectorId` 方法和傳遞字串值 `EJB`.
   * 透過叫用端點來指定端點的說明 `CreateEndpointInfo` 物件的 `setDescription` 方法和傳遞描述端點的字串值。
   * 透過叫用端點來指定名稱 `CreateEndpointInfo` 物件的 `setName` 方法並傳遞指定名稱的字串值。
   * 透過叫用「 」，指定端點所屬的服務 `CreateEndpointInfo` 物件的 `setServiceId` 方法並傳遞指定服務名稱的字串值。
   * 指定透過叫用呼叫的作業 `CreateEndpointInfo` 物件的 `setOperationName` 方法，並傳遞指定作業名稱的字串值。 對於SOAP和EJB端點，請指定萬用字元( `*`)，這表示所有作業。

1. 建立EJB端點。

   透過叫用 `EndpointRegistryClient` 物件的 `createEndpoint` 方法並傳遞 `CreateEndpointInfo` 物件。 此方法會傳回 `Endpoint` 代表新EJB端點的物件。

1. 啟用端點。

   透過叫用啟用端點 `EndpointRegistryClient` 物件的enable方法並傳遞 `Endpoint` 物件，由 `createEndpoint` 方法。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API新增EJB端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-ejb-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 新增SOAP端點 {#adding-soap-endpoints}

您可以使用AEM Forms Java API，以程式設計方式將SOAP端點新增至服務。 透過新增SOAP端點，您可以讓使用者端應用程式使用SOAP模式來叫用服務。 也就是說，在設定呼叫AEM Forms所需的連線屬性時，您可以選取SOAP模式。

>[!NOTE]
>
>您無法使用Web服務新增SOAP端點。

>[!NOTE]
>
>通常，SOAP端點會依預設新增至服務。不過，SOAP端點可以新增至以程式設計方式部署的流程，或是在移除SOAP端點且必須再次新增時。

### 步驟摘要 {#summary_of_steps-1}

若要將SOAP端點新增至服務，請執行下列工作：

1. 包含專案檔案。
1. 建立 `EndpointRegistryClient` 物件。
1. 設定SOAP端點屬性。
1. 建立SOAP端點。
1. 啟用端點。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (如果將AEM Forms部署在JBoss Application Server上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss Application Server上，則為必要)

需要這些JAR檔案才能建立SOAP端點。 不過，如果您使用SOAP端點來叫用服務，則需要額外的JAR檔案。 如需AEM Forms JAR檔案的相關資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立EndpointRegistry使用者端物件**

若要以程式設計方式將SOAP端點新增至服務，您必須建立 `EndpointRegistryClient` 物件。

**設定SOAP端點屬性**

若要將SOAP端點新增至服務，請指定下列值：

* **聯結器識別碼值**：指定要建立的端點型別。 若要建立SOAP端點，請指定 `SOAP`.
* **說明**：指定端點說明。
* **名稱**：指定端點名稱。
* **服務識別碼值**：指定端點所屬的服務。
* **作業名稱**：指定使用端點叫用的作業名稱。 建立SOAP端點時，請指定萬用字元( `*`)。 不過，如果您要指定特定作業，而不是叫用所有服務作業，請指定作業的名稱，而不是使用萬用字元( `*`)。

**建立SOAP端點**

設定SOAP端點屬性之後，您可以建立SOAP端點。

**啟用端點**

建立端點後，您必須啟用它。 端點啟用時，可用來叫用服務。 啟用端點後，即可在管理主控台中檢視端點。

**另請參閱**

[使用Java API新增SOAP端點](programmatically-endpoints.md#add-a-soap-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API新增SOAP端點 {#add-a-soap-endpoint-using-the-java-api}

使用Java API新增SOAP端點至服務：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-livecycle-client.jar。

1. 建立EndpointRegistry使用者端物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `EndpointRegistryClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 設定SOAP端點屬性。

   * 建立 `CreateEndpointInfo` 物件（使用其建構函式）。
   * 透過叫用「 」指定聯結器識別碼值 `CreateEndpointInfo` 物件的 `setConnectorId` 方法和傳遞字串值 `SOAP`.
   * 透過叫用端點來指定端點的說明 `CreateEndpointInfo` 物件的 `setDescription` 方法和傳遞描述端點的字串值。
   * 透過叫用端點來指定名稱 `CreateEndpointInfo` 物件的 `setName` 方法並傳遞指定名稱的字串值。
   * 透過叫用「 」，指定端點所屬的服務 `CreateEndpointInfo` 物件的 `setServiceId` 方法並傳遞指定服務名稱的字串值。
   * 指定透過叫用呼叫的作業 `CreateEndpointInfo` 物件的 `setOperationName` 方法並傳遞指定作業名稱的字串值。 對於SOAP和EJB端點，請指定萬用字元( `*`)，這表示所有作業。

1. 建立SOAP端點。

   透過叫用 `EndpointRegistryClient` 物件的 `createEndpoint` 方法並傳遞 `CreateEndpointInfo` 物件。 此方法會傳回 `Endpoint` 代表新SOAP端點的物件。

1. 啟用端點。

   透過叫用啟用端點 `EndpointRegistryClient` 物件的enable方法並傳遞 `Endpoint` 物件，由 `createEndpoint` 方法。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API新增SOAP端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-soap-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 新增Watched資料夾端點 {#adding-watched-folder-endpoints}

您可以使用AEM Forms Java API，以程式設計方式將Watched資料夾端點新增至服務。 透過新增Watched資料夾端點，您可以讓使用者將檔案(例如PDF檔案)放在資料夾中。 將檔案放在資料夾中時，會叫用已設定的服務並操作檔案。 服務執行指定的作業後，會將修改的檔案儲存在指定的輸出資料夾中。 觀察資料夾已設定為以固定速率間隔或以cron排程掃描，例如每個星期一、星期三和星期五中午。

為了以程式設計方式將Watched資料夾端點新增至服務，請考慮以下名為的短期程式 *Encryptdocument*. (請參閱 [瞭解AEM Forms流程](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).)

![aw_aw_encryptdocumentprocess](assets/aw_aw_encryptdocumentprocess.png)

此程式接受不安全的PDF檔案作為輸入值，然後將不安全的PDF檔案傳遞至加密服務的 `EncryptPDFUsingPassword` 作業。 PDF檔案使用密碼加密，而密碼加密的PDF檔案是此程式的輸出值。 輸入值的名稱(無保護PDF檔案)為 `InDoc` 而且資料型別為 `com.adobe.idp.Document`. 輸出值的名稱(密碼加密的PDF檔案)為 `SecuredDoc` 而且資料型別為 `com.adobe.idp.Document`.

>[!NOTE]
>
>您無法使用Web服務新增Watched資料夾端點。

### 步驟摘要 {#summary_of_steps-2}

若要將Watched資料夾端點新增至服務，請執行下列工作：

1. 包含專案檔案。
1. 建立 `EndpointRegistryClient` 物件。
1. 設定Watched資料夾端點屬性。
1. 指定設定值。
1. 定義輸入引數值。
1. 定義輸出引數值。
1. 建立Watched資料夾端點。
1. 啟用端點。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (如果將AEM Forms部署在JBoss Application Server上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss Application Server上，則為必要)

有關這些JAR檔案位置的資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立EndpointRegistry使用者端物件**

若要以程式設計方式新增Watched資料夾端點，您必須建立 `EndpointRegistryClient` 物件。

**設定Watched資料夾端點屬性**

若要為服務建立Watched資料夾端點，請指定下列值：

* **聯結器識別碼**：指定已建立的端點型別。 若要建立Watched資料夾端點，請指定 `WatchedFolder`.
* **說明**：指定端點的說明。
* **名稱**：指定端點的名稱。
* **服務識別碼**：指定端點所屬的服務。 例如，若要將Watched資料夾端點新增至本節中介紹的流程（使用Workbench啟動時流程會變成服務），請指定 `EncryptDocument`.
* **作業名稱**：指定使用端點叫用的作業名稱。 通常，在為源自於Workbench中建立的程式之服務建立Watched資料夾端點時，操作的名稱為 `invoke`.

**指定設定值**

以程式設計方式將Watched資料夾端點新增至服務時，請指定Watched資料夾端點的設定值。 如果使用管理主控台新增Watched資料夾端點，則由管理員指定這些設定值。

下列清單指定以程式設計方式將Watched資料夾端點新增至服務時所設定的設定值：

* **url**：指定watched資料夾位置。 在叢集環境中，此值必須指向可從叢集中的每台電腦存取的共用網路資料夾。
* **非同步**：識別非同步或同步叫用型別。 暫時和同步處理程式只能同步叫用。 預設值為true。 建議使用非同步。
* **cronExpression**：由Quartz用來排程輸入目錄的輪詢。
* **purgeDuration**：此為強制屬性。 當結果資料夾中的檔案和資料夾早於此值時，就會清除這些檔案和資料夾。 此值以天為單位測量。 此屬性有助於確保結果資料夾不會填滿。 值為–1天表示絕不刪除結果資料夾。 預設值為–1。
* **repeateinterval**：掃描Watched資料夾以進行輸入的間隔，以秒為單位。 除非啟用節流功能，否則此值應超過處理平均作業的時間；否則，系統可能會變得超載。 預設值為 5。
* **repeatcount**：觀察資料夾掃描資料夾或目錄的次數。 值–1表示無限掃描。 預設值為–1。
* **throttingOn**：限制可在任何指定時間處理的Watched資料夾工作數目。 最大作業數由batchSize值決定。
* **userName**：從Watched資料夾叫用目標服務時使用的使用者名稱。 此值為必填。 預設值為SuperAdmin。
* **domainName**：使用者的網域。 此值為必填。 預設值為DefaultDom。
* **batchSize**：每次掃描要擷取的檔案或資料夾數目。 使用此值可防止系統過載；一次掃描太多檔案可能會導致當機。 預設值為 2。
* **waittime**：建立資料夾或檔案後，等待掃描資料夾或檔案的時間（毫秒）。 例如，如果等待時間為36,000,000毫秒（一小時），且檔案是在一分鐘前建立的，則系統會在59分鐘或更長時間後擷取此檔案。 此屬性對於確保檔案或資料夾完全複製到輸入資料夾非常有用。 例如，如果您有大型檔案要處理，且檔案下載需要10分鐘，請將等待時間設定為10&amp;ast；60 &amp;ast；1000毫秒。 此設定可防止watched資料夾在等待十分鐘後掃描檔案。 預設值為 0。
* **excludeFilePattern**：watched資料夾用來判斷要掃描和擷取哪些檔案和資料夾的模式。 任何具有此模式的檔案或資料夾都不會掃描以進行處理。 當輸入是包含多個檔案的資料夾時，此設定非常有用。 資料夾的內容可以複製到一個資料夾中，該資料夾的名稱將由watched資料夾擷取。 此步驟可防止watched資料夾在資料夾完全複製到輸入資料夾之前擷取資料夾進行處理。 例如，如果excludeFilePattern值為 `data*`，所有符合的檔案和資料夾 `data*` 不會提取。 這包括名為的檔案和資料夾 `data1`， `data2`、等等。 此外，模式可附加萬用字元模式，以指定檔案模式。 watched資料夾會修改規則運算式，以支援萬用字元模式，例如 `*.*` 和 `*.pdf`. 規則運算式不支援這些萬用字元模式。
* **includefilePattern**：watched資料夾用來判斷要掃描和擷取哪些資料夾和檔案的模式。 例如，如果此值為 `*`，所有符合的檔案和資料夾 `input*` 已選取。 這包括名為的檔案和資料夾 `input1`， `input2`、等等。 預設值為 `*`。此值表示所有檔案和資料夾。 此外，模式可附加萬用字元模式，以指定檔案模式。 watched資料夾會修改規則運算式，以支援萬用字元模式，例如 `*.*` 和 `*.pdf`. 規則運算式不支援這些萬用字元模式。 此值為必填。
* **resultFolderName**：儲儲存存結果的資料夾。 此位置可以是絕對或相對目錄路徑。 如果結果未出現在此資料夾中，請檢查失敗資料夾。 唯讀檔案不會處理，且會儲存在失敗資料夾中。 預設值為 `result/%Y/%M/%D/`。這是watched資料夾內的結果資料夾。
* **preserveFolderName**：成功掃描和擷取後，檔案的儲存位置。 此位置可以是絕對、相對或Null目錄路徑。 預設值為 `preserve/%Y/%M/%D/`。
* **failureFolderName**：儲存失敗檔案的資料夾。 此位置永遠是相對於watched資料夾。 唯讀檔案不會處理，且會儲存在失敗資料夾中。 預設值為 `failure/%Y/%M/%D/`。
* **preserveOnFailure**：如果對服務執行作業失敗，則保留輸入檔案。 預設值為true。
* **overwriteDuplicateFilename**：設為true時，會覆寫結果資料夾和保留資料夾中的檔案。 設定為false時，名稱會使用具有數值索引尾碼的檔案和資料夾。 預設值為false。

**定義輸入引數值**

建立Watched資料夾端點時，您必須定義輸入引數值。 也就是說，您必須說明傳遞至watched資料夾所叫用之作業的輸入值。 例如，請考量本主題中介紹的程式。 它有一個輸入值，名為 `InDoc` 且其資料型別為 `com.adobe.idp.Document`. 當為此處理序建立Watched資料夾端點時（在處理序啟動後，它會變成服務），您必須定義輸入引數值。

若要定義Watched資料夾端點所需的輸入引數值，請指定下列值：

**輸入引數名稱**：輸入引數的名稱。 在Workbench中為處理指定輸入值的名稱。 如果輸入值屬於服務作業（不是在Workbench中建立的處理序的服務），則在component.xml檔案中指定輸入名稱。 例如，本節介紹之程式的輸入引數名稱為 `InDoc`.

**對應型別**：用於設定呼叫服務作業所需的輸入值。 對應型別有兩種：

* `Literal`： Watched資料夾端點使用顯示的欄位中輸入的值。 支援所有基本Java型別。 例如，如果API使用字串、long、int和Boolean等輸入，則字串會轉換為正確型別並叫用服務。
* `Variable`：輸入的值是watched資料夾用來挑選輸入的檔案模式。 例如，如果您為對應型別選取「變數」，且輸入檔案必須是PDF檔案，則可以指定 `*.pdf`做為對應值。

**對應值**：指定對應型別的值。 例如，如果您選取 `Variable` 對應型別，您可以指定 `*.pdf` 作為檔案模式。

**資料型別**：指定輸入值的資料型別。 例如，本節介紹之程式的輸入值的資料型別為 `com.adobe.idp.Document`.

**定義輸出引數值**

建立Watched資料夾端點時，您必須定義輸出引數值。 也就是說，您必須說明由Watched資料夾端點叫用的服務所傳回的輸出值。 例如，請考量本主題中介紹的程式。 它有一個輸出值，名為 `SecuredDoc` 且其資料型別為 `com.adobe.idp.Document`. 當為此處理序建立Watched資料夾端點時（在處理序啟動後，它會變成服務），您必須定義輸出引數值。

若要定義Watched資料夾端點所需的輸出引數值，請指定下列值：

**輸出引數名稱**：輸出引數的名稱。 在Workbench中指定處理輸出值的名稱。 如果輸出值屬於服務作業（不是在Workbench中建立的處理作業）時，會在component.xml檔案中指定輸出名稱。 例如，本節介紹的流程之輸出引數的名稱為 `SecuredDoc`.

**對應型別**：用於設定服務和操作的輸出。 下列選項可供使用：

* 如果服務傳回單一物件（單一檔案），則模式為 `%F.pdf` 而來源目的地是sourcefilename.pdf。 例如，本節介紹的程式會傳回單一檔案。 因此，可將對應型別定義為 `%F.pdf` ( `%F` 表示使用指定的檔案名稱)。 模式 `%E` 指定輸入檔案的副檔名。
* 如果服務傳回清單，則模式為 `Result\%F\`，而來源目的地為Result\sourcefilename\source1 （輸出1）和Result\sourcefilename\source2 （輸出2）。
* 如果服務傳回地圖，模式為 `Result\%F\`，而來源目的地為Result\sourcefilename\file1和Result\sourcefilename\file2。 如果地圖有多個物件，則模式為 `Result\%F.pdf` 來源目的地為Result\sourcefilename1.pdf （輸出1）、Result\sourcefilenam2.pdf （輸出2）等等。

**資料型別**：指定傳回值的資料型別。 例如，本節介紹之程式的傳回值資料型別為 `com.adobe.idp.Document`.

**建立Watched資料夾端點**

在您設定端點的屬性、組態值以及定義輸入和輸出引數值之後，您必須建立Watched資料夾端點。

**啟用端點**

建立Watched資料夾端點之後，您必須啟用它。 端點啟用時，可用來叫用服務。 啟用端點後，即可在管理主控台中檢視它。

**另請參閱**

[使用Java API新增Watched資料夾端點](programmatically-endpoints.md#add-a-watched-folder-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API新增Watched資料夾端點 {#add-a-watched-folder-endpoint-using-the-java-api}

使用AEM Forms Java API新增Watched資料夾端點：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-livecycle-client.jar。

1. 建立EndpointRegistry使用者端物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `EndpointRegistryClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 設定Watched資料夾端點屬性。

   * 建立 `CreateEndpointInfo` 物件（使用其建構函式）。
   * 透過叫用「 」指定聯結器識別碼值 `CreateEndpointInfo` 物件的 `setConnectorId` 方法和傳遞字串值 `WatchedFolder`.
   * 透過叫用端點來指定端點的說明 `CreateEndpointInfo` 物件的 `setDescription` 方法和傳遞描述端點的字串值。
   * 透過叫用端點來指定名稱 `CreateEndpointInfo` 物件的 `setName` 方法並傳遞指定名稱的字串值。
   * 透過叫用「 」，指定端點所屬的服務 `CreateEndpointInfo` 物件的 `setServiceId` 方法並傳遞指定服務名稱的字串值。
   * 指定透過叫用呼叫的作業 `CreateEndpointInfo` 物件的 `setOperationName` 方法並傳遞指定作業名稱的字串值。 通常，在為源自於Workbench中建立的程式之服務建立Watched資料夾端點時，會叫用操作的名稱。

1. 指定設定值。

   對於要為Watched資料夾端點設定的每個設定值，您必須叫用 `CreateEndpointInfo` 物件的 `setConfigParameterAsText` 方法。 例如，若要設定 `url` 設定值，叫用 `CreateEndpointInfo` 物件的 `setConfigParameterAsText` 方法並傳遞下列字串值：

   * 字串值，指定組態值的名稱。 設定時 `url` 設定值，指定 `url`.
   * 字串值，指定設定值的值。 設定時 `url` 設定值，指定watched資料夾位置。

   >[!NOTE]
   >
   >若要檢視為EncryptDocument服務設定的所有設定值，請參閱位於以下位置的Java程式碼範例： [快速入門：使用Java API新增Watched資料夾端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api).

1. 定義輸入引數值。

   透過叫用 `CreateEndpointInfo` 物件的 `setInputParameterMapping` 方法並傳遞下列值：

   * 字串值，指定輸入引數的名稱。 例如，EncryptDocument服務的輸入引數名稱是 `InDoc`.
   * 字串值，指定輸入引數的資料型別。 例如，資料型別 `InDoc` 輸入引數為 `com.adobe.idp.Document`.
   * 字串值，指定對應型別。 例如，您可以指定 `variable`.
   * 字串值，指定對應型別值。 例如，您可以指定&amp;ast；.pdf作為檔案模式。

   >[!NOTE]
   >
   >叫用 `setInputParameterMapping` 定義每個輸入引數值的方法。 由於EncryptDocument程式只有一個輸入引數，因此您需要叫用此方法一次。

1. 定義輸出引數值。

   透過叫用 `CreateEndpointInfo` 物件的 `setOutputParameterMapping` 方法並傳遞下列值：

   * 字串值，指定輸出引數的名稱。 例如，EncryptDocument服務的輸出引數名稱是 `SecuredDoc`.
   * 字串值，指定輸出引數的資料型別。 例如，資料型別 `SecuredDoc` 輸出引數為 `com.adobe.idp.Document`.
   * 字串值，指定對應型別。 例如，您可以指定 `%F.pdf`.

1. 建立Watched資料夾端點。

   透過叫用 `EndpointRegistryClient` 物件的 `createEndpoint` 方法並傳遞 `CreateEndpointInfo` 物件。 此方法會傳回 `Endpoint` 代表Watched資料夾端點的物件。

1. 啟用端點。

   透過叫用啟用端點 `EndpointRegistryClient` 物件的 `enable` 方法並傳遞 `Endpoint` 物件，由 `createEndpoint` 方法。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API新增Watched資料夾端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Watched資料夾組態值常數檔案 {#watched-folder-configuration-values-constant-file}

此 [快速入門：使用Java API新增Watched資料夾端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api) 使用必須屬於Java專案一部分的常數檔案來編譯快速入門。 此常數檔案代表新增Watched資料夾端點時必須設定的組態值。 下列Java程式碼代表常數檔案。

```java
 /**
     * This class contains constants that can be used when setting Watched Folder
     * configuration values
     */

 public final class WatchedFolderEndpointConfigConstants {

         public static final String PROPERTY_FILEPROVIDER_URL = "url";
         public static final String PROPERTY_PROPERTY_ASYNCHRONOUS = "asynchronous";
         public static final String PROPERTY_CRON_EXPRESSION = "cronExpression";
         public static final String PROPERTY_PURGE_DURATION = "purgeDuration";
         public static final String PROPERTY_REPEAT_INTERVAL = "repeatInterval";
         public static final String PROPERTY_REPEAT_COUNT = "repeatCount";
         public static final String PROPERTY_THROTTLE = "throttleOn";
         public static final String PROPERTY_USERNAMER = "userName";
         public static final String PROPERTY_DOMAINNAME = "domainName";
         public static final String PROPERTY_FILEPROVIDER_BATCH_SIZE = "batchSize";
         public static final String PROPERTY_FILEPROVIDER_WAIT_TIME = "waitTime";
         public static final String PROPERTY_EXCLUDE_FILE_PATTERN = "excludeFilePattern";
         public static final String PROPERTY_INCLUDE_FILE_PATTERN = "excludeFilePattern";
         public static final String PROPERTY_FILEPROVIDER_RESULT_FOLDER_NAME =  "resultFolderName";
         public static final String PROPERTY_FILEPROVIDER_PRESERVE_FOLDER_NAME = "preserveFolderName";
         public static final String PROPERTY_FILEPROVIDER_FAILURE_FOLDER_NAME = "failureFolderName";
         public static final String PROPERTY_FILEPROVIDER_PRESERVE_ON_FAILURE = "preserveOnFailure";
         public static final String PROPERTY_FILEPROVIDER_OVERWRITE_DUPLICATE_FILENAME = "overwriteDuplicateFilename";
        }
```

## 新增電子郵件端點 {#adding-email-endpoints}

您可以使用AEM Forms Java API，以程式設計方式將電子郵件端點新增至服務。 透過新增電子郵件端點，您可以讓使用者將包含一或多個檔案附件的電子郵件訊息傳送至指定的電子郵件帳戶。 然後會叫用設定服務操作並操作檔案。 服務執行指定的作業後，會傳送電子郵件訊息給寄件者，其中包含已修改的檔案作為檔案附件。

為了以程式設計方式將電子郵件端點新增至服務，請考慮以下名為的短期程式 *MyApplication\EncryptDocument*. 如需有關短期程式的資訊，請參閱 [瞭解AEM Forms流程](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).

![ae_ae_encryptdocumentprocess](assets/ae_ae_encryptdocumentprocess.png)

此程式接受不安全的PDF檔案作為輸入值，然後將不安全的PDF檔案傳遞至加密服務的 `EncryptPDFUsingPassword` 作業。 此程式會使用密碼加密PDF檔案，並傳回密碼加密的PDF檔案作為輸出值。 輸入值的名稱(無保護PDF檔案)為 `InDoc` 而且資料型別為 `com.adobe.idp.Document`. 輸出值的名稱(密碼加密的PDF檔案)為 `SecuredDoc` 而且資料型別為 `com.adobe.idp.Document`.

>[!NOTE]
>
>您無法使用網站服務來新增電子郵件端點。

### 步驟摘要 {#summary_of_steps-3}

若要將電子郵件端點新增至服務，請執行下列工作：

1. 包含專案檔案。
1. 建立 `EndpointRegistryClient` 物件。
1. 設定電子郵件端點屬性。
1. 指定設定值。
1. 定義輸入引數值。
1. 定義輸出引數值。
1. 建立電子郵件端點。
1. 啟用端點。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (如果將AEM Forms部署在JBoss Application Server上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss Application Server上，則為必要)

有關這些JAR檔案位置的資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立EndpointRegistry使用者端物件**

您必須先建立「 」，才能以程式設計方式新增電子郵件端點 `EndpointRegistryClient` 物件。

**設定電子郵件端點屬性**

若要建立服務的電子郵件端點，請指定下列值：

* **聯結器識別碼值**：指定已建立的端點型別。 若要建立電子郵件端點，請指定 `Email`.
* **說明**：指定端點的說明。
* **名稱**：指定端點的名稱。
* **服務識別碼值**：指定端點所屬的服務。 例如，若要將電子郵件端點新增至本節中介紹的流程（使用Workbench啟動時流程會變成服務），請指定 `EncryptDocument`.
* **作業名稱**：指定使用端點叫用的作業名稱。 一般而言，針對源自於Workbench中建立之程式的服務建立電子郵件端點時，操作的名稱為 `invoke`.

**指定設定值**

以程式設計方式將電子郵件端點新增至服務時，指定電子郵件端點的設定值。 如果使用管理主控台新增電子郵件端點，則管理員會指定這些設定值。

>[!NOTE]
>
>受監控的電子郵件帳戶是僅用於電子郵件端點的特殊帳戶。 此帳戶不是一般使用者的電子郵件帳戶。 一般使用者的電子郵件帳戶不可設定為電子郵件提供者使用的帳戶，因為電子郵件提供者在完成郵件處理之後，會從收件匣中刪除電子郵件訊息。

以程式設計方式將電子郵件端點新增至服務時，會設定下列設定值：

* **cronExpression**：Cron運算式，如果電子郵件必須使用cron運算式排程。
* **repeatcount**：電子郵件端點掃描資料夾或目錄的次數。 值–1表示無限掃描。 預設值為–1。
* **repeateinterval**：接收者用於檢查傳入郵件的掃描速率（以秒為單位）。 預設值為 10。
* **startDelay**：排程器啟動後等待掃描的時間。 預設時間為0。
* **batchSize**：接收者為了最佳效能而每次掃描處理的電子郵件訊息數。 值–1表示所有電子郵件。 預設值為 2。
* **userName**：從電子郵件叫用目標服務時使用的使用者名稱。 預設值為 `SuperAdmin`。
* **domainName**：強制設定值。 預設值為 `DefaultDom`。
* **domainPattern**：指定提供者接受的傳入電子郵件的網域模式。 例如，如果 `adobe.com` 會使用，僅處理來自adobe.com的電子郵件，而忽略來自其他網域的電子郵件。
* **filePattern**：指定提供者接受的傳入檔案附件模式。 這包括具有特定副檔名(&amp;ast；.dat、&amp;ast；.xml)的檔案、具有特定名稱（資料）的檔案，以及具有名稱與副檔名複合運算式的檔案(&amp;ast；)。[dD][aA]&#39;連線埠&#39;)。 預設值為 `*`。
* **recipientSuccessfulJob**：傳送訊息以指出成功作業的電子郵件地址。 依預設，成功的工作訊息一律會傳送給寄件者。 如果您輸入 `sender`，會將電子郵件結果傳送給寄件者。 最多可支援100個收件者。 使用電子郵件地址指定其他收件者，每個收件者之間以逗號分隔。 若要關閉此選項，請將此值留空。 某些情況下，您可能想要觸發程式，而不想收到結果的電子郵件通知。 預設值為 `sender`。
* **recipientFailedJob**：傳送訊息以指出作業失敗的電子郵件地址。 依預設，失敗的工作訊息一律會傳送給寄件者。 如果您輸入 `sender`，會將電子郵件結果傳送給寄件者。 最多可支援100個收件者。 使用電子郵件地址指定其他收件者，每個收件者之間以逗號分隔。 若要關閉此選項，請將此值留空。 預設值為 `sender`。
* **inboxHost**：要掃描的電子郵件提供者的收件匣主機名稱或IP位址。
* **inboxPort**：電子郵件伺服器使用的連線埠。 POP3的預設值為110，IMAP的預設值為143。 如果啟用SSL，POP3的預設值為995，IMAP的預設值為993。
* **inboxProtocol**：用於掃描收件匣之電子郵件端點的電子郵件通訊協定。 選項包括 `IMAP` 或 `POP3`. 收件匣主機郵件伺服器必須支援這些通訊協定。
* **收件匣逾時**：電子郵件提供者等候收件匣回應的逾時秒數。 預設值為 60。
* **inboxUser**：登入電子郵件帳戶所需的使用者名稱。 視電子郵件伺服器和設定而定，這可能只是電子郵件的使用者名稱部分，也可能是完整的電子郵件地址。
* **inboxPassword**：收件匣使用者的密碼。
* **inboxSSLEnabled**：設定此值，以強制電子郵件提供者在傳送結果或錯誤的通知訊息時使用SSL。 請確定IMAP或POP3主機支援SSL。
* **smtpHost**：電子郵件提供者傳送結果和錯誤訊息的目標郵件伺服器的主機名稱。
* **smtpPort**：SMTP連線埠的預設值為25。
* **smtpUser**：電子郵件提供者在傳送結果和錯誤的電子郵件通知時要使用的使用者帳戶。
* **smtpPassword**：SMTP帳戶的密碼。 有些郵件伺服器不需要SMTP密碼。
* **charSet**：電子郵件提供者使用的字元集。 預設值為 `UTF-8`。
* **smtpSSLEnabled**：設定此值，以強制電子郵件提供者在傳送結果或錯誤的通知訊息時使用SSL。 請確定SMTP主機支援SSL。
* **failedJobFolder**：指定當SMTP郵件伺服器無法運作時，要儲存結果的目錄。
* **非同步**：設為同步時，會處理所有輸入檔案並傳回單一回應。 設為非同步時，系統會針對每個已處理的輸入檔案傳送回應。 例如，會針對本主題中介紹的流程建立電子郵件端點，並傳送電子郵件訊息至端點的收件匣，其中包含多個不安全的PDF檔案。 當所有PDF檔案都使用密碼加密時，如果端點設定為同步，則會傳送單一回應電子郵件訊息並附加所有安全PDF檔案。 如果端點設定為非同步，則會為每個安全PDF檔案傳送個別的回應電子郵件訊息。 每封電子郵件都包含單一PDF檔案作為附件。 預設值為非同步。

**定義輸入引數值**

建立電子郵件端點時，您必須定義輸入引數值。 也就是說，您必須說明傳遞至電子郵件端點所叫用之作業的輸入值。 例如，請考量本主題中介紹的程式。 它有一個輸入值，名為 `InDoc` 且其資料型別為 `com.adobe.idp.Document`. 為此流程建立電子郵件端點時（流程啟動後，就會變成服務），您必須定義輸入引數值。

若要定義電子郵件端點所需的輸入引數值，請指定下列值：

**輸入引數名稱**：輸入引數的名稱。 在Workbench中為處理指定輸入值的名稱。 如果輸入值屬於服務操作(不是在Workbench中建立之程式的Forms服務)，則輸入名稱會在component.xml檔案中指定。 例如，本節介紹之程式的輸入引數名稱為 `InDoc`.

**對應型別**：用於設定呼叫服務作業所需的輸入值。 兩種對應型別如下：

* `Literal`：電子郵件端點使用在顯示的欄位中輸入的值。 支援所有基本Java型別。 例如，如果API使用字串、long、int和Boolean等輸入，則字串會轉換為正確型別並叫用服務。
* `Variable`：輸入的值是電子郵件端點用來挑選輸入的檔案模式。 例如，如果您為對應型別選取「變數」，且輸入檔案必須是PDF檔案，則可以指定 `*.pdf` 做為對應值。

**對應值**：指定對應型別的值。 例如，如果您選取「變數」對應型別，則可指定 `*.pdf` 作為檔案模式。

**資料型別**：指定輸入值的資料型別。 例如，本節介紹之程式的輸入值的資料型別為com.adobe.idp.Document。

**定義輸出引數值**

建立電子郵件端點時，您必須定義輸出引數值。 也就是說，您必須說明由電子郵件端點叫用的服務傳回的輸出值。 例如，請考量本主題中介紹的程式。 它有一個輸出值，名為 `SecuredDoc` 且其資料型別為 `com.adobe.idp.Document`. 為此流程建立電子郵件端點時（流程啟動後，就會變成服務），您必須定義輸出引數值。

若要定義電子郵件端點所需的輸出引數值，請指定下列值：

**輸出引數名稱**：輸出引數的名稱。 在Workbench中指定處理輸出值的名稱。 如果輸出值屬於服務作業（不是在Workbench中建立的處理作業）時，會在component.xml檔案中指定輸出名稱。 例如，本節介紹的流程之輸出引數的名稱為 `SecuredDoc`.

**對應型別**：用於設定服務和操作的輸出。 下列選項可供使用：

* 如果服務傳回單一物件（單一檔案），則模式為 `%F.pdf` 而來源目的地是sourcefilename.pdf。 例如，本節介紹的程式會傳回單一檔案。 因此，可將對應型別定義為 `%F.pdf` ( `%F` 表示使用指定的檔案名稱)。 模式 `%E` 指定輸入檔案的副檔名。
* 如果服務傳回清單，則模式為 `Result\%F\`，而來源目的地為Result\sourcefilename\source1 （輸出1）和Result\sourcefilename\source2 （輸出2）。
* 如果服務傳回地圖，模式為 `Result\%F\`，而來源目的地為Result\sourcefilename\file1和Result\sourcefilename\file2。 如果地圖有多個物件，則模式為 `Result\%F.pdf` 來源目的地為Result\sourcefilename1.pdf （輸出1）、Result\sourcefilenam2.pdf （輸出2）等等。

**資料型別**：指定傳回值的資料型別。 例如，本節介紹之程式的傳回值資料型別為 `com.adobe.idp.Document`.

**建立電子郵件端點**

設定電子郵件端點屬性和設定值，並定義輸入和輸出引數值後，您必須建立電子郵件端點。

**啟用端點**

建立電子郵件端點後，您必須啟用它。 端點啟用時，可用來叫用服務。 啟用端點後，即可在管理主控台中檢視它。

**另請參閱**

[使用Java API新增電子郵件端點](programmatically-endpoints.md#add-an-email-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API新增電子郵件端點 {#add-an-email-endpoint-using-the-java-api}

使用Java API新增電子郵件端點：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-livecycle-client.jar。

1. 建立EndpointRegistry使用者端物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `EndpointRegistryClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 設定電子郵件端點屬性。

   * 建立 `CreateEndpointInfo` 物件（使用其建構函式）。
   * 透過叫用「 」指定聯結器識別碼值 `CreateEndpointInfo` 物件的 `setConnectorId` 方法和傳遞字串值 `Email`.
   * 透過叫用端點來指定端點的說明 `CreateEndpointInfo` 物件的 `setDescription` 方法和傳遞描述端點的字串值。
   * 透過叫用端點來指定名稱 `CreateEndpointInfo` 物件的 `setName` 方法並傳遞指定名稱的字串值。
   * 透過叫用「 」，指定端點所屬的服務 `CreateEndpointInfo` 物件的 `setServiceId` 方法並傳遞指定服務名稱的字串值。
   * 指定透過叫用呼叫的作業 `CreateEndpointInfo` 物件的 `setOperationName` 方法並傳遞指定作業名稱的字串值。 一般而言，在為源自於Workbench中建立之程式的服務建立電子郵件端點時，會叫用操作的名稱。

1. 指定設定值。

   您必須針對要針對電子郵件端點設定的每個設定值，叫用 `CreateEndpointInfo` 物件的 `setConfigParameterAsText` 方法。 例如，若要設定 `smtpHost` 設定值，叫用 `CreateEndpointInfo` 物件的 `setConfigParameterAsText` 方法並傳遞下列值：

   * 字串值，指定組態值的名稱。 設定時 `smtpHost` 設定值，指定 `smtpHost`.
   * 字串值，指定設定值的值。 設定時 `smtpHost` 組態值，指定字串值，以指定SMTP伺服器的名稱。

   >[!NOTE]
   >
   >若要檢視本節介紹的EncryptDocument服務設定的所有設定值，請參閱位於以下位置的Java程式碼範例： [快速入門：使用Java API新增電子郵件端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api).

1. 定義輸入引數值。

   透過叫用 `CreateEndpointInfo` 物件的 `setInputParameterMapping` 方法並傳遞下列值：

   * 字串值，指定輸入引數的名稱。 例如，EncryptDocument服務的輸入引數名稱是 `InDoc`.
   * 字串值，指定輸入引數的資料型別。 例如，資料型別 `InDoc` 輸入引數為 `com.adobe.idp.Document`.
   * 字串值，指定對應型別。 例如，您可以指定 `variable`.
   * 字串值，指定對應型別值。 例如，您可以指定&amp;ast；.pdf作為檔案模式。

   >[!NOTE]
   >
   >叫用 `setInputParameterMapping` 定義每個輸入引數值的方法。 由於EncryptDocument程式只有一個輸入引數，因此您需要叫用此方法一次。

1. 定義輸出引數值。

   透過叫用 `CreateEndpointInfo` 物件的 `setOutputParameterMapping` 方法並傳遞下列值：

   * 字串值，指定輸出引數的名稱。 例如，EncryptDocument服務的輸出引數名稱是 `SecuredDoc`.
   * 字串值，指定輸出引數的資料型別。 例如，資料型別 `SecuredDoc` 輸出引數為 `com.adobe.idp.Document`.
   * 字串值，指定對應型別。 例如，您可以指定 `%F.pdf`.

1. 建立電子郵件端點。

   透過叫用 `EndpointRegistryClient` 物件的 `createEndpoint` 方法並傳遞 `CreateEndpointInfo` 物件。 此方法會傳回 `Endpoint` 代表電子郵件端點的物件。

1. 啟用端點。

   透過叫用啟用端點 `EndpointRegistryClient` 物件的 `enable` 方法並傳遞 `Endpoint` 物件，由 `createEndpoint` 方法。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API新增Watched資料夾端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 電子郵件設定值常數檔案 {#email-configuration-values-constant-file}

此 [快速入門：使用Java API新增電子郵件端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api) 使用必須屬於Java專案一部分的常數檔案來編譯快速入門。 此常數檔案代表新增電子郵件端點時必須設定的設定值。 下列Java程式碼代表常數檔案。

```java
 /**
     * This class contains constants that can be used when setting email endpoint
     * configuration values
     */
 public class EmailEndpointConfigConstants {

     public static final String PROPERTY_EMAILPROVIDER_CRON_EXPRESSION = "cronExpression";
     public static final String PROPERTY_EMAILPROVIDER_REPREAT_COUNT = "repeatCount";
     public static final String PROPERTY_EMAILPROVIDER_REPREAT_INTERVAL = "repeatInterval";
     public static final String PROPERTY_EMAILPROVIDER_START_DELAY = "startDelay";
     public static final String PROPERTY_EMAILPROVIDER_BATCH_SIZE = "batchSize";
     public static final String PROPERTY_EMAILPROVIDER_USERNAME = "userName";
     public static final String PROPERTY_EMAILPROVIDER_DOMAINNAME = "domainName";
     public static final String PROPERTY_EMAILPROVIDER_DOMAINPATTERN = "domainPattern";
     public static final String PROPERTY_EMAILPROVIDER_FILEPATTERN = "filePattern";
     public static final String PROPERTY_EMAILPROVIDER_RECIPIENT_SUCCESSFUL_JOB = "recipientSuccessfulJob";
     public static final String PROPERTY_EMAILPROVIDER_RECIPIENT_FAILED_JOB = "recipientFailedJob";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_HOST = "inboxHost";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_PORT = "inboxPort";
     public static final String PROPERTY_EMAILPROVIDER_PROTOCOL = "inboxProtocol";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_TIMEOUT = "inboxTimeOut";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_USER = "inboxUser";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_PASSWORD = "inboxPassword";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_SSL = "inboxSSLEnabled";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_HOST = "smtpHost";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_PORT = "smtpPort";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_USER = "smtpUser";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_PASSWORD = "smtpPassword";
     public static final String PROPERTY_EMAILPROVIDER_CHARSET = "charSet";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_SSL = "smtpSSLEnabled";
     public static final String PROPERTY_EMAILPROVIDER_FAILED_FOLDER = "failedJobFolder";
     public static final String PROPERTY_EMAILPROVIDER_ASYNCHRONOUS = "asynchronous";
 }
```

## 新增遠端端點 {#adding-remoting-endpoints}

>[!NOTE]
>
>JEE版的AEM表單已棄用LiveCycle Remoting API。

您可以使用AEM Forms Java API，以程式設計方式將遠端端點新增至服務。 透過新增遠端端點，您可以啟用Flex應用程式以使用遠端來叫用服務。 (請參閱 [叫用AEM Forms (AEM表單已棄用) AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

為了以程式設計方式將遠端端點新增至服務，請考慮以下名為的短期程式 *Encryptdocument*.

![ar_ar_encryptdocumentprocess](assets/ar_ar_encryptdocumentprocess.png)

此程式接受不安全的PDF檔案作為輸入值，然後將不安全的PDF檔案傳遞至加密服務的 `EncryptPDFUsingPassword` 作業。 PDF檔案使用密碼加密，而密碼加密的PDF檔案是此程式的輸出值。 輸入值的名稱(無保護PDF檔案)為 `InDoc` 而且資料型別為 `com.adobe.idp.Document`. 輸出值的名稱(密碼加密的PDF檔案)為 `SecuredDoc` 而且資料型別為 `com.adobe.idp.Document`.

為了示範如何將Remoting端點新增至服務，本節將Remoting端點新增至名為EncryptDocument的服務。

>[!NOTE]
>
>您無法使用Web服務來新增遠端端點。

### 步驟摘要 {#summary_of_steps-4}

若要從服務移除端點，請執行下列工作：

1. 包含專案檔案。
1. 建立 `EndpointRegistryClient` 物件。
1. 設定遠端端點屬性。
1. 建立遠端端點。
1. 啟用端點。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (如果將AEM Forms部署在JBoss Application Server上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss Application Server上，則為必要)

有關這些JAR檔案位置的資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立EndpointRegistry使用者端物件**

若要以程式設計方式新增遠端端點，您必須建立 `EndpointRegistryClient` 物件。

**設定遠端端點屬性**

若要建立服務的Remoting端點，請指定下列值：

* **聯結器識別碼值**：指定已建立的端點型別。 若要建立遠端端點，請指定 `Remoting`.
* **說明**：指定端點的說明。
* **名稱**：指定端點的名稱。
* **服務識別碼值**：指定端點所屬的服務。 例如，若要將Remoting端點新增至本節中介紹的流程（流程在Workbench中啟動時會成為服務），請指定 `EncryptDocument`.
* **作業名稱**：指定使用端點叫用的作業名稱。 建立遠端端點時，請指定萬用字元(&amp;ast；)。

**建立遠端端點**

設定Remoting端點屬性之後，您就可以為服務建立Remoting端點。

**啟用端點**

建立端點後，您必須啟用它。 遠端端點啟用時，可讓Flex使用者端叫用服務。

**另請參閱**

[使用Java API新增遠端端點](programmatically-endpoints.md#add-a-remoting-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API新增遠端端點 {#add-a-remoting-endpoint-using-the-java-api}

使用Java API新增Remoting端點：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-livecycle-client.jar。

1. 建立EndpointRegistry使用者端物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `EndpointRegistryClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 設定遠端端點屬性。

   * 建立 `CreateEndpointInfo` 物件（使用其建構函式）。
   * 透過叫用「 」指定聯結器識別碼值 `CreateEndpointInfo` 物件的 `setConnectorId` 方法和傳遞字串值 `Remoting`.
   * 透過叫用端點來指定端點的說明 `CreateEndpointInfo` 物件的 `setDescription` 方法和傳遞描述端點的字串值。
   * 透過叫用端點來指定名稱 `CreateEndpointInfo` 物件的 `setName` 方法並傳遞指定名稱的字串值。
   * 透過叫用「 」，指定端點所屬的服務 `CreateEndpointInfo` 物件的 `setServiceId` 方法並傳遞指定服務名稱的字串值。
   * 指定呼叫的作業 `CreateEndpointInfo` 物件的 `setOperationName` 方法並傳遞指定作業名稱的字串值。 對於遠端端點，請指定萬用字元(&amp;ast；)。

1. 建立遠端端點。

   透過叫用 `EndpointRegistryClient` 物件的 `createEndpoint` 方法並傳遞 `CreateEndpointInfo` 物件。 此方法會傳回 `Endpoint` 代表新遠端端點的物件。

1. 啟用端點。

   透過叫用啟用端點 `EndpointRegistryClient` 物件的 `enable` 方法並傳遞 `Endpoint` 物件，由 `createEndpoint` 方法。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API新增遠端端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-remoting-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 新增TaskManager端點 {#adding-taskmanager-endpoints}

您可以使用AEM Forms Java API，以程式設計方式將TaskManager端點新增至服務。 透過將TaskManager端點新增至服務，您可以讓Workspace使用者叫用服務。 也就是說，在Workspace中工作的使用者可以叫用具有對應TaskManager端點的程式。

>[!NOTE]
>
>您無法使用Web服務新增TaskManager端點。

### 步驟摘要 {#summary_of_steps-5}

若要將TaskManager端點新增至服務，請執行下列工作：

1. 包含專案檔案。
1. 建立 `EndpointRegistryClient` 物件。
1. 為端點建立類別。
1. 設定TaskManager端點屬性。
1. 建立TaskManager端點。
1. 啟用端點。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (如果將AEM Forms部署在JBoss Application Server上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss Application Server上，則為必要)

有關這些JAR檔案位置的資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立EndpointRegistry使用者端物件**

您必須先建立TaskManager端點，才能以程式設計方式新增 `EndpointRegistryClient` 物件。

**為端點建立類別**

類別是用來在工作區中組織服務。 也就是說，Workspace使用者可以透過在Workspace中選取類別來叫用具有TaskManager端點的服務。 建立TaskManager端點時，您可以參照現有類別或以程式設計方式建立類別。

>[!NOTE]
>
>本節會建立TaskManager端點新增至服務的新類別。

**設定TaskManager端點屬性**

若要建立服務的TaskManager端點，請指定下列值：

* **聯結器識別碼**：指定已建立的端點型別。 若要建立TaskManager端點，請指定 `TaskManagerConnector`.
* **說明**：指定端點的說明。
* **名稱**：指定端點的名稱。
* **服務識別碼**：指定端點所屬的服務。
* **類別**：指定與TaskManager端點相關聯的類別識別碼值。
* **作業名稱**：一般而言，在為源自於Workbench中建立之程式的服務建立TaskManager端點時，操作的名稱為 `invoke`.

**建立TaskManager端點**

設定TaskManager端點屬性之後，就可以為服務建立TaskManager端點。

**啟用端點**

建立端點後，您必須啟用它。 端點啟用時，可用來從工作區內叫用服務。 啟用端點後，即可在管理主控台中檢視它。

**另請參閱**

[使用Java API新增TaskManager端點](programmatically-endpoints.md#add-a-taskmanager-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API新增TaskManager端點 {#add-a-taskmanager-endpoint-using-the-java-api}

使用Java API新增TaskManager端點：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-livecycle-client.jar。

1. 建立EndpointRegistry使用者端物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `EndpointRegistryClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 為端點建立類別。

   * 建立 `CreateEndpointCategoryInfo` 物件，使用它的建構函式並傳遞下列值：

      * 字串值，指定類別的識別碼值
      * 字串值，指定類別的說明

   * 透過叫用類別來建立 `EndpointRegistryClient` 物件的 `createEndpointCategory` 方法並傳遞 `CreateEndpointCategoryInfo` 物件。 此方法會傳回 `EndpointCategory` 代表新類別的物件。

1. 設定TaskManager端點屬性。

   * 建立 `CreateEndpointInfo` 物件（使用其建構函式）。
   * 透過叫用「 」指定聯結器識別碼值 `CreateEndpointInfo` 物件的 `setConnectorId` 方法和傳遞字串值 `TaskManagerConnector`.
   * 透過叫用端點來指定端點的說明 `CreateEndpointInfo` 物件的 `setDescription` 方法和傳遞描述端點的字串值。
   * 透過叫用端點來指定名稱 `CreateEndpointInfo` 物件的 `setName` 方法並傳遞指定名稱的字串值。
   * 透過叫用「 」，指定端點所屬的服務 `CreateEndpointInfo` 物件的 `setServiceId` 方法並傳遞指定服務名稱的字串值。
   * 叫用「 」，指定端點所屬的類別 `CreateEndpointInfo` 物件的 `setCategoryId` 方法並傳遞字串值，該值會指定類別識別碼值。 您可以叫用 `EndpointCategory` 物件的 `getId` 取得此類別識別碼值的方法。
   * 指定透過叫用呼叫的作業 `CreateEndpointInfo` 物件的 `setOperationName` 方法並傳遞指定作業名稱的字串值。 通常當建立 `TaskManager` 源自於Workbench中建立之處理序的服務端點，作業名稱為 `invoke`.

1. 建立TaskManager端點。

   透過叫用 `EndpointRegistryClient` 物件的 `createEndpoint` 方法並傳遞 `CreateEndpointInfo` 物件。 此方法會傳回 `Endpoint` 代表新TaskManager端點的物件。

1. 啟用端點。

   透過叫用啟用端點 `EndpointRegistryClient` 物件的 `enable` 方法並傳遞 `Endpoint` 物件，由 `createEndpoint` 方法。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API新增TaskManager端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-taskmanager-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 修改端點 {#modifying-endpoints}

您可以使用AEM Forms Java API以程式設計方式修改現有端點。 透過修改端點，您可以變更端點的行為。 例如，假設一個Watched資料夾端點指定了一個資料夾作為watched資料夾使用。 您可以以程式設計方式修改屬於Watched資料夾端點的設定值，導致另一個資料夾充當watched資料夾。 如需屬於Watched資料夾端點的設定值相關資訊，請參閱 [新增Watched資料夾端點](programmatically-endpoints.md#adding-watched-folder-endpoints).

為了示範如何修改端點，本節會透過變更作為watched資料夾的資料夾來修改Watched資料夾端點。

>[!NOTE]
>
>您不能使用Web服務來修改端點。

### 步驟摘要 {#summary_of_steps-6}

若要修改端點，請執行下列工作：

1. 包含專案檔案。
1. 建立 `EndpointRegistryClient` 物件。
1. 擷取端點。
1. 指定新的設定值。

**包含專案檔案**

在您的開發專案中包含必要的檔案。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (如果將AEM Forms部署在JBoss Application Server上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss Application Server上，則為必要)

有關這些JAR檔案位置的資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立EndpointRegistry使用者端物件**

若要以程式設計方式修改端點，您必須建立 `EndpointRegistryClient` 物件。

**擷取端點以修改**

您必須先擷取端點，然後才能修改端點。 若要擷取端點，您必須以可存取端點的使用者身分連線。 建議您以管理員身分連線。 (請參閱 [設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties))。

您可以透過擷取端點清單來擷取端點。 然後，您可以逐一檢視清單，搜尋要移除的特定端點。 例如，您可以判斷與端點對應的服務以及端點的型別，以找出端點。 當您找到端點時，可以修改它。

**指定新的設定值**

修改端點時，請指定新的設定值。 例如，若要修改Watched資料夾端點，請重設所有Watched資料夾端點設定值，而不僅僅是您要修改的設定值。 如需屬於Watched資料夾端點的設定值相關資訊，請參閱 [新增Watched資料夾端點](programmatically-endpoints.md#adding-watched-folder-endpoints).

>[!NOTE]
>
>如需屬於電子郵件端點的設定值相關資訊，請參閱 [新增電子郵件端點](programmatically-endpoints.md#adding-email-endpoints).

>[!NOTE]
>
>您無法修改端點叫用的服務。 如果您嘗試修改服務，則會擲回例外狀況。 若要修改與指定端點關聯的服務，請移除端點並建立一個。 (請參閱 [移除端點](programmatically-endpoints.md#removing-endpoints).)

**另請參閱**

[使用Java API修改端點](programmatically-endpoints.md#modifying-an-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API修改端點 {#modifying-an-endpoint-using-the-java-api}

使用Java API修改端點：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-livecycle-client.jar。

1. 建立EndpointRegistry使用者端物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `EndpointRegistryClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 擷取要修改的端點。

   * 擷取目前使用者（在連線屬性中指定）可以存取的所有端點清單，方法是叫用 `EndpointRegistryClient` 物件的 `getEndpoints` 方法和傳遞 `PagingFilter` 做為濾鏡的物件。 您可以傳遞 `(PagingFilter)null` 值以傳回所有端點。 此方法會傳回 `java.util.List` 每個元素為的物件 `Endpoint` 物件。 關於的資訊 `PagingFilter` 物件，請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * 逐一檢視 `java.util.List` 物件以判斷它是否有端點。 如果端點存在，則每個元素為 `EndPoint` 執行個體。
   * 透過叫用 `EndPoint` 物件的 `getServiceId` 方法。 此方法會傳回指定服務名稱的字串值。
   * 透過叫用 `EndPoint` 物件的 `getConnectorId` 方法。 此方法會傳回指定端點型別的字串值。 例如，如果端點是Watched資料夾端點，則此方法會傳回 `WatchedFolder`.

1. 指定新的設定值。

   * 建立 `ModifyEndpointInfo` 物件，透過叫用它的建構函式。
   * 對於每個要設定的組態值，叫用 `ModifyEndpointInfo` 物件的 `setConfigParameterAsText` 方法。 例如，若要設定url設定值，請叫用 `ModifyEndpointInfo` 物件的 `setConfigParameterAsText` 方法並傳遞下列值：

      * 字串值，指定組態值的名稱。 例如，若要設定 `url` 設定值，指定 `url`.
      * 字串值，指定設定值的值。 若要定義 `url` 設定值，指定watched資料夾位置。

   * 叫用 `EndpointRegistryClient` 物件的 `modifyEndpoint` 方法並傳遞 `ModifyEndpointInfo` 物件。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API修改端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-modifying-an-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 移除端點 {#removing-endpoints}

您可以使用AEM Forms Java API，以程式設計方式從服務中移除端點。 移除端點後，無法使用啟用端點的叫用方法來叫用服務。 例如，如果您從服務中移除SOAP端點，就無法使用SOAP模式來叫用服務。

若要示範如何從服務移除端點，此段落會從名為的服務移除EJB端點 *Encryptdocument*.

>[!NOTE]
>
>您無法使用網站服務移除端點。

### 步驟摘要 {#summary_of_steps-7}

若要從服務移除端點，請執行下列工作：

1. 包含專案檔案。
1. 建立 `EndpointRegistryClient` 物件。
1. 擷取端點。
1. 移除端點。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (如果將AEM Forms部署在JBoss Application Server上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss Application Server上，則為必要)

有關這些JAR檔案位置的資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立EndpointRegistry使用者端物件**

若要以程式設計方式移除端點，您必須建立 `EndpointRegistryClient` 物件。

**擷取要移除的端點**

您必須先擷取端點，才能移除端點。 若要擷取端點，您必須以可存取端點的使用者身分連線。 建議您以管理員身分連線。 (請參閱 [設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties))。

您可以透過擷取端點清單來擷取端點。 然後，您可以逐一檢視清單，搜尋要移除的特定端點。 例如，您可以判斷與端點對應的服務以及端點的型別，以找出端點。 當您找到端點時，可以將其移除。

**移除端點**

建立端點後，您必須啟用它。 端點啟用時，可用來叫用服務。 啟用端點後，即可在管理主控台中檢視它。

**另請參閱**

[使用Java API移除端點](programmatically-endpoints.md#removing-an-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API移除端點 {#removing-an-endpoint-using-the-java-api}

使用Java API移除端點：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-livecycle-client.jar。

1. 建立EndpointRegistry使用者端物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `EndpointRegistryClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 擷取端點以移除。

   * 擷取目前使用者（在連線屬性中指定）有權存取的所有端點清單，方法是叫用 `EndpointRegistryClient` 物件的 `getEndpoints` 方法和傳遞 `PagingFilter` 做為濾鏡的物件。 您可以傳遞 `(PagingFilter)null` 以傳回所有端點。 此方法會傳回 `java.util.List` 每個元素為的物件 `Endpoint` 物件。
   * 逐一檢視 `java.util.List` 物件以判斷它是否有端點。 如果端點存在，則每個元素為 `EndPoint` 執行個體。
   * 透過叫用 `EndPoint` 物件的 `getServiceId` 方法。 此方法會傳回指定服務名稱的字串值。
   * 透過叫用 `EndPoint` 物件的 `getConnectorId` 方法。 此方法會傳回指定端點型別的字串值。 例如，如果端點是EJB端點，則此方法會傳回 `EJB`.

1. 移除端點。

   透過叫用來移除端點 `EndpointRegistryClient` 物件的 `remove` 方法並傳遞 `EndPoint` 代表要移除之端點的物件。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API移除端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-removing-an-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 正在擷取端點聯結器資訊 {#retrieving-endpoint-connector-information}

您可以使用AEM Forms API以程式設計方式擷取有關端點聯結器的資訊。 聯結器可讓端點使用各種叫用方法來叫用服務。 例如，Watched資料夾聯結器可讓端點使用watched資料夾叫用服務。 透過以程式擷取端點聯結器的相關資訊，您可以擷取與聯結器相關的組態值，例如需要哪些組態值以及哪些是選用值。

為了示範如何擷取端點聯結器的相關資訊，本節會擷取Watched資料夾聯結器的相關資訊。 (請參閱 [新增Watched資料夾端點](programmatically-endpoints.md#adding-watched-folder-endpoints).)

>[!NOTE]
>
>您無法使用Web服務擷取有關端點的資訊。

>[!NOTE]
>
>本主題使用 `ConnectorRegistryClient` 用於擷取端點聯結器相關資訊的API。 (請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

### 步驟摘要 {#summary_of_steps-8}

若要擷取端點聯結器資訊，請執行下列工作：

1. 包含專案檔案。
1. 建立 `ConnectorRegistryClient` 物件。
1. 指定聯結器型別。
1. 擷取設定值。

**包含專案檔案**

將必要的檔案納入您的開發專案中。 如果您使用Java建立使用者端應用程式，請包含必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將下列JAR檔案新增至專案的類別路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (如果將AEM Forms部署在JBoss Application Server上，則為必要)
* jbossall-client.jar (如果AEM Forms部署在JBoss Application Server上，則為必要)

如果將AEM Forms部署在支援的J2EE應用程式伺服器（不是JBoss）上，請將adobe-utilities.jar和jbossall-client.jar取代為特定於已部署AEM Forms之J2EE應用程式伺服器的JAR檔案。 如需有關所有AEM Forms JAR檔案位置的資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立ConnectorRegistry使用者端物件**

若要以程式擷取端點聯結器資訊，請建立 `ConnectorRegistryClient` 物件。

**指定聯結器型別**

指定要從中擷取資訊的聯結器型別。 存在下列型別的聯結器：

* **EJB**：讓使用者端應用程式能夠使用EJB模式叫用服務。
* **SOAP**：讓使用者端應用程式能夠使用SOAP模式叫用服務。
* **Watched資料夾**：啟用watched資料夾以叫用服務。
* **電子郵件**：啟用電子郵件訊息以叫用服務。
* **遠端**：讓Flex使用者端應用程式能夠叫用服務。
* **TaskmanagerConnector**：可讓Workspace使用者從Workspace內叫用服務。

**擷取設定值**

指定聯結器型別後，即可擷取有關聯結器的資訊，例如支援的組態值。 例如，對於任何聯結器，您可以決定哪些組態值是必要值，哪些是選用值。

**另請參閱**

[使用Java API擷取端點聯結器資訊](programmatically-endpoints.md#retrieve-endpoint-connector-information-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API擷取端點聯結器資訊 {#retrieve-endpoint-connector-information-using-the-java-api}

使用Java API擷取端點聯結器資訊：

1. 包含專案檔案。

   在您的Java專案的類別路徑中包含使用者端JAR檔案，例如adobe-livecycle-client.jar。

1. 建立ConnectorRegistry使用者端物件。

   * 建立 `ServiceClientFactory` 包含連線屬性的物件。
   * 建立 `ConnectorRegistryClient` 物件，使用它的建構函式並傳遞 `ServiceClientFactory` 物件。

1. 指定聯結器型別。

   透過叫用 `ConnectorRegistryClient` 物件的 `getEndpointDefinition` 方法並傳遞指定聯結器型別的字串值。 例如，若要指定Watched資料夾聯結器型別，請傳遞字串值 `WatchedFolder`. 此方法會傳回 `Endpoint` 與聯結器型別相對應的物件。

1. 擷取設定值。

   * 透過叫用「 」，擷取與此端點相關聯的設定值 `Endpoint` 物件的 `getConfigParameters` 方法。 此方法傳回陣列 `ConfigParameter` 物件。
   * 擷取陣列中的每個元素，以擷取有關每個設定值的資訊。 每個元素都是 `ConfigParameter` 物件。 例如，您可以透過叫用 `ConfigParameter` 物件的 `isRequired` 方法。 如果需要設定值，則此方法會傳回 `true`.

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API擷取端點聯結器資訊](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-retrieving-endpoint-connector-information-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連線屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
