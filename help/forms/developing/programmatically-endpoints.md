---
title: 以程式設計方式管理端點
seo-title: 以程式設計方式管理端點
description: 'null'
seo-description: 'null'
uuid: 5dc50946-3323-4c5d-a43b-31c1c980bd04
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 076889a7-9c9f-4b6f-a45b-67a9b3923c36
translation-type: tm+mt
source-git-commit: 8bc99ed3817398ae358d439a5c1fcc90bbd24327

---


# 以程式設計方式管理端點 {#programmatically-managing-endpoints}

**關於端點註冊服務**

端點註冊服務提供以程式設計方式管理端點的能力。 例如，您可以將下列類型的端點添加到服務中：

* EJB
* SOAP
* Watched資料夾
* 電子郵件
* （AEM表格已停用）遠端
* 任務管理器

   ***注意&#x200B;**:SOAP、EJB和（JEE上的AEM表單已過時）會針對每個已啟動的服務自動建立遠端端點。 SOAP和EJB端點可為所有服務操作啟用SOAP和EJB。*

   遠端端點可讓Flex用戶端叫用端點新增至之AEM Forms服務上的作業。 會建立與端點同名的Flex目標，而Flex用戶端可建立指向此目標的RemoteObjects，以叫用相關服務的作業。

   「電子郵件」、「任務管理員」和「監視資料夾」端點僅顯示服務的特定操作。 添加這些端點需要第二個配置步驟來選擇調用方法、設定配置參數以及指定輸入和輸出參數映射。

   您可以將TaskManager端點組織到稱為類別的 *組中*。 然後，這些類別會通過TaskManager向工作區公開，最終用戶將看到TaskManager端點按其分類。 在工作區中，使用者會在導覽窗格中看到這些類別。 每個類別中的端點都顯示為「工作區」的「啟動進程」頁上的進程卡。

   您可以使用端點註冊服務完成以下任務：

* 添加EJB端點。 (請參 [閱添加EJB端點](programmatically-endpoints.md#adding-ejb-endpoints)。)
* 添加SOAP端點。 (請參 [閱添加SOAP端點](programmatically-endpoints.md#adding-soap-endpoints)。)
* 添加監視資料夾端點(請參 [閱添加監視資料夾端點](programmatically-endpoints.md#adding-watched-folder-endpoints))。
* 新增電子郵件端點。 (請參閱 [新增電子郵件端點](programmatically-endpoints.md#adding-email-endpoints)。)
* 新增遠端端點。 (請參閱 [新增遠端端點](programmatically-endpoints.md#adding-remoting-endpoints)。)
* 添加TaskManager端點(請參 [閱添加TaskManager端點](programmatically-endpoints.md#adding-taskmanager-endpoints))。
* 修改端點(請參 [閱修改端點](programmatically-endpoints.md#modifying-endpoints))。
* 移除端點(請參 [閱移除端點](programmatically-endpoints.md#removing-endpoints))。
* 檢索端點連接器資訊(請參 [閱檢索端點連接器資訊](programmatically-endpoints.md#retrieving-endpoint-connector-information)。)

## 添加EJB端點 {#adding-ejb-endpoints}

您可以使用AEM Forms Java API，以程式設計方式將EJB端點新增至服務。 通過將EJB端點添加到服務中，可以使用EJB模式使客戶端應用程式調用服務。 也就是說，在設定呼叫AEM Forms所需的連線屬性時，您可以選取EJB模式。 (請參 [閱設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)

>[!NOTE]
>
>不能使用Web服務添加EJB端點。

>[!NOTE]
>
>通常，預設情況下會將EJB端點添加到服務中。但是，可以將EJB端點添加到以寫程式方式部署的進程中，或者刪除EJB端點後，必須重新添加。

### 步驟摘要 {#summary-of-steps}

要將EJB端點添加到服務，請執行以下任務：

1. 包含專案檔案。
1. 建立對 `EndpointRegistry Client` 像。
1. 設定EJB端點屬性。
1. 建立EJB端點。
1. 啟用端點。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（如果AEM Forms部署在JBoss Application server上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss Application server上，則為必需）

如需這些JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立EndpointRegistry客戶端對象**

在以寫程式方式添加EJB端點之前，必須先建立對 `EndpointRegistryClient` 像。

**設定EJB端點屬性**

要為服務建立EJB端點，請指定以下值：

* **連接器識別碼**:指定要建立的端點類型。 要建立EJB端點，請指定 `EJB`。
* **說明**:指定端點說明。
* **名稱**:指定端點的名稱。
* **服務識別碼**:指定端點所屬的服務。
* **操作名稱**:指定使用端點調用的操作的名稱。 建立EJB端點時，請指定通配符( `*`)。 但是，如果要指定與調用所有服務操作不同的特定操作，請指定操作的名稱，而不是使用通配符( `*`)。

**建立EJB端點**

設定EJB端點屬性後，可以為服務建立EJB端點。

**啟用端點**

建立新端點後，必須啟用該端點。 啟用端點後，可用來調用服務。 啟用端點後，可在管理控制台中查看該端點。

**另請參閱**

[使用Java API添加EJB端點](programmatically-endpoints.md#adding-an-ejb-endpoint-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加EJB端點 {#adding-an-ejb-endpoint-using-the-java-api}

使用Java API添加EJB端點：

1. 包含專案檔案。

   在您Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-livecycle-client.jar。 (

1. 建立EndpointRegistry客戶端對象。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `EndpointRegistryClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 設定EJB端點屬性。

   * 使用其 `CreateEndpointInfo` 建構函式建立物件。
   * 調用物件的方法並傳遞字串值， `CreateEndpointInfo` 以指定 `setConnectorId` 連接器識別碼值 `EJB`。
   * 調用物件的方法並傳遞描述 `CreateEndpointInfo` 端點的字 `setDescription` 串值，以指定端點的說明。
   * 調用物件的方法並傳遞指 `CreateEndpointInfo` 定名稱的字 `setName` 串值，以指定端點的名稱。
   * 通過調用對象的方法並傳遞指定服務名 `CreateEndpointInfo` 的字串值， `setServiceId` 指定端點所屬的服務。
   * 指定透過叫用物件的方法所 `CreateEndpointInfo` 呼叫的作 `setOperationName` 業，並傳遞指定作業名稱的字串值。 對於SOAP和EJB端點，請指定通配符( `*`)，表示所有操作。

1. 建立EJB端點。

   呼叫物件的方法並傳 `EndpointRegistryClient` 遞物件，以 `createEndpoint` 建立端點 `CreateEndpointInfo` 。 此方法返回 `Endpoint` 表示新EJB端點的對象。

1. 啟用端點。

   調用物件的啟用方 `EndpointRegistryClient` 法，並傳遞方法傳 `Endpoint` 回的物件，以啟用端 `createEndpoint` 點。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API添加EJB端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-ejb-endpoint-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 添加SOAP端點 {#adding-soap-endpoints}

您可以使用AEM Forms Java API，以程式設計方式將SOAP端點新增至服務。 通過添加SOAP端點，可使客戶端應用程式使用SOAP模式調用服務。 也就是說，當設定呼叫AEM Forms所需的連線屬性時，您可以選取SOAP模式。

>[!NOTE]
>
>您無法使用web services來新增SOAP端點。

>[!NOTE]
>
>通常，SOAP端點預設添加到服務中。但是，SOAP端點可以添加到以寫程式方式部署的進程中，或者在刪除SOAP端點後必須重新添加。

### 步驟摘要 {#summary_of_steps-1}

要向服務添加SOAP端點，請執行以下任務：

1. 包含專案檔案。
1. 建立對 `EndpointRegistryClient` 像。
1. 設定SOAP端點屬性。
1. 建立SOAP端點。
1. 啟用端點。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（如果AEM Forms部署在JBoss Application server上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss Application server上，則為必需）

建立SOAP端點時需要這些JAR檔案。 但是，如果使用SOAP端點調用服務，則需要添加JAR檔案。 如需AEM Forms JAR檔案的詳細資訊，請參 [閱「包含AEM Forms Java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立EndpointRegistry客戶端對象**

若要以程式設計方式將SOAP端點新增至服務，您必須建立 `EndpointRegistryClient` 物件。

**設定SOAP端點屬性**

要向服務添加SOAP端點，請指定以下值：

* **連接器標識符值**:指定要建立的端點類型。 要建立SOAP端點，請指定 `SOAP`。
* **說明**:指定端點說明。
* **名稱**:指定端點名稱。
* **服務標識符值**:指定端點所屬的服務。
* **操作名稱**:指定使用端點調用的操作的名稱。 建立SOAP端點時，請指定通配符( `*`)。 但是，如果要指定與調用所有服務操作不同的特定操作，請指定操作的名稱，而不是使用通配符( `*`)。

**建立SOAP端點**

設定SOAP端點屬性後，可以建立SOAP端點。

**啟用端點**

建立新端點後，必須啟用該端點。 啟用端點時，可用來調用服務。 啟用端點後，您可以在管理控制台中檢視它。

**另請參閱**

[使用Java API新增SOAP端點](programmatically-endpoints.md#add-a-soap-endpoint-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API新增SOAP端點 {#add-a-soap-endpoint-using-the-java-api}

使用Java API將SOAP端點新增至服務：

1. 包含專案檔案。

   在您Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-livecycle-client.jar。

1. 建立EndpointRegistry客戶端對象。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `EndpointRegistryClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 設定SOAP端點屬性。

   * 使用其 `CreateEndpointInfo` 建構函式建立物件。
   * 調用物件的方法並傳遞字串值， `CreateEndpointInfo` 以指定 `setConnectorId` 連接器識別碼值 `SOAP`。
   * 調用物件的方法並傳遞描述 `CreateEndpointInfo` 端點的字 `setDescription` 串值，以指定端點的說明。
   * 調用物件的方法並傳遞指 `CreateEndpointInfo` 定名稱的字 `setName` 串值，以指定端點的名稱。
   * 通過調用對象的方法並傳遞指定服務名 `CreateEndpointInfo` 的字串值， `setServiceId` 指定端點所屬的服務。
   * 指定透過叫用物件的方法並傳 `CreateEndpointInfo` 遞指定作 `setOperationName` 業名稱的字串值所呼叫的作業。 對於SOAP和EJB端點，請指定通配符( `*`)，表示所有操作。

1. 建立SOAP端點。

   呼叫物件的方法並傳 `EndpointRegistryClient` 遞物件，以 `createEndpoint` 建立端點 `CreateEndpointInfo` 。 此方法返回 `Endpoint` 表示新SOAP端點的對象。

1. 啟用端點。

   調用物件的enable方 `EndpointRegistryClient` 法以啟用端點，並傳遞 `Endpoint` 由方法傳回的物 `createEndpoint` 件。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API添加SOAP端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-soap-endpoint-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 添加監視資料夾端點 {#adding-watched-folder-endpoints}

您可以使用AEM Forms Java API，以程式設計方式將Watched資料夾端點新增至服務。 借由新增「監看資料夾」端點，您可讓使用者將檔案（例如PDF檔案）置入資料夾。 將檔案放在資料夾中時，將調用已配置的服務並操縱檔案。 服務執行指定操作後，會將修改的檔案保存到指定的輸出資料夾中。 已設定受監視的資料夾，以固定的速率間隔或cron排程進行掃描，例如每週一、週三和週五中午。

為了以程式設計方式將Watched資料夾端點新增至服務，請考慮下列名為 *EncryptDocument的簡短程式*。 (請參 [閱「瞭解AEM表單流程](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)」。)

![aw_aw_encryptdocumentprocess](assets/aw_aw_encryptdocumentprocess.png)

此程式會接受不安全的PDF檔案作為輸入值，然後將不安全的PDF檔案傳遞至加密服務的作 `EncryptPDFUsingPassword` 業。 PDF檔案會以密碼加密，而密碼加密的PDF檔案就是此程式的輸出值。 輸入值的名稱（不安全的PDF文檔） `InDoc` 和資料類型為 `com.adobe.idp.Document`。 輸出值的名稱（密碼加密的PDF檔案） `SecuredDoc` 和資料類型 `com.adobe.idp.Document`。

>[!NOTE]
>
>您無法使用Web服務來新增Watched資料夾端點。

### 步驟摘要 {#summary_of_steps-2}

要向服務添加Watched資料夾端點，請執行以下任務：

1. 包含專案檔案。
1. 建立對 `EndpointRegistryClient` 像。
1. 設定「監視資料夾」端點屬性。
1. 指定設定值。
1. 定義輸入參數值。
1. 定義輸出參數值。
1. 建立Watched資料夾端點。
1. 啟用端點。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（如果AEM Forms部署在JBoss Application server上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss Application server上，則為必需）

如需這些JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立EndpointRegistry客戶端對象**

若要以程式設計方式新增Watched資料夾端點，您必須建立 `EndpointRegistryClient` 物件。

**設定「監視資料夾」端點屬性**

要為服務建立「監視資料夾」端點，請指定以下值：

* **連接器識別碼**:指定所建立的端點類型。 要建立「監視資料夾」端點，請指定 `WatchedFolder`。
* **說明**:指定端點的說明。
* **名稱**:指定端點的名稱。
* **服務識別碼**:指定端點所屬的服務。 例如，若要將「監視資料夾」端點新增至本節中引入的程式（當使用Workbench啟動時，程式會變成服務），請指定 `EncryptDocument`。
* **操作名稱**:指定使用端點調用的操作的名稱。 通常，為源自在Workbench中建立的流程的服務建立「監視資料夾」端點時，操作的名稱為 `invoke`。

**指定配置值**

當以程式設計方式將Watched folder端點新增至服務時，您必須指定Watched folder端點的設定值。 如果使用管理控制台添加了「監視資料夾」端點，管理員將指定這些配置值。

以下清單指定在以寫程式方式將Watched資料夾端點添加到服務時設定的配置值：

* **url**:指定受監視的資料夾位置。 在叢集環境中，此值必須指向可從叢集中每台電腦存取的共用網路資料夾。
* **非同步**:將調用類型標識為非同步或同步。 瞬態和同步進程只能同步調用。 預設值為true。 建議使用非同步。
* **cronExpression**:Quartz用於調度輸入目錄的輪詢。 如需設定cron運算式的詳細資訊，請參閱 [https://quartz.sourceforge.net/javadoc/org/quartz/CronTrigger.html](https://quartz.sourceforge.net/javadoc/org/quartz/CronTrigger.html)。
* **purgeDuration**:這是必備屬性。 結果資料夾中的檔案和資料夾在其早於此值時被清除。 此值以天計。 此屬性對於確保結果資料夾未變為完整非常有用。 值為-1天表示從不刪除結果資料夾。 預設值為-1。
* **repeatInterval**:掃描「監視資料夾」進行輸入的間隔（秒）。 除非啟用調節，否則此值應比處理平均作業的時間長；否則，系統可能會超載。 預設值為5。
* **repeatCount**:「監視資料夾」掃描資料夾或目錄的次數。 值-1表示無限掃描。 預設值為-1。
* **throttleOn**:限制可在任何指定時間處理的「已監視資料夾」作業數。 作業的最大數量由batchSize值確定。
* **userName**:從「監視資料夾」叫用目標服務時使用的使用者名稱。 此值為強制值。 預設值為SuperAdmin。
* **domainName**:使用者的網域。 此值為強制值。 預設值為DefaultDom。
* **batchSize**:每次掃描要拾取的檔案或資料夾數。 使用此值可防止系統過載；一次掃描太多檔案可能會導致當機。 預設值為2。
* **waitTime**:建立資料夾或檔案後，在掃描資料夾或檔案之前等待的時間（以毫秒為單位）。 例如，如果等待時間是36,000,000毫秒（1小時），而檔案是在一分鐘前建立的，則此檔案會在59分鐘或更久之後擷取。 此屬性對於確保檔案或資料夾被完全複製到輸入資料夾非常有用。 例如，如果要處理大檔案，而要下載該檔案需要10分鐘，請將等待時間設定為10&amp;ast;60 &amp;ast;1000毫秒。 此設定會防止受監視的資料夾在檔案尚未等候10分鐘時進行掃描。 預設值為0。
* **excludeFilePattern**:受監視資料夾用於確定要掃描和拾取哪些檔案和資料夾的模式。 不會掃描任何具有此模式的檔案或資料夾以進行處理。 當輸入是包含多個檔案的檔案夾時，此設定很實用。 資料夾的內容可以複製到名稱由受監視資料夾挑選的資料夾中。 此步驟可防止被監視的資料夾在完全複製到輸入資料夾之前拾取要處理的資料夾。 例如，如果excludeFilePattern值為，則不 `data*`會擷取所有符合的檔 `data*` 案和檔案夾。 這包括名為、 `data1`等的 `data2`檔案和檔案夾。 此外，該模式可以用通配符模式補充以指定檔案模式。 監看的資料夾會修改規則運算式，以支援萬用字元模式，例如 `*.*` 和 `*.pdf`。 規則運算式不支援這些萬用字元模式。
* **includeFilePattern**:受監視資料夾用於確定要掃描和拾取哪些資料夾和檔案的模式。 例如，如果此值為，則 `*`會擷取所有符合的檔 `input*` 案和檔案夾。 這包括名為、 `input1`等的 `input2`檔案和檔案夾。 預設值為 `*`。 此值表示所有檔案和資料夾。 此外，該模式可以用通配符模式補充以指定檔案模式。 監看的資料夾會修改規則運算式，以支援萬用字元模式，例如 `*.*` 和 `*.pdf`。 規則運算式不支援這些萬用字元模式。 此值為必填值。
* **resultFolderName**:儲儲存存結果的資料夾。 此位置可以是絕對或相對目錄路徑。 如果結果未顯示在此資料夾中，請檢查失敗資料夾。 只讀檔案不會被處理，並將保存在失敗資料夾中。 預設值為 `result/%Y/%M/%D/`。 這是監視資料夾內的結果資料夾。
* **preserveFolderName**:成功掃描和拾取檔案後儲存檔案的位置。 此位置可以是絕對、相對或空目錄路徑。 預設值為 `preserve/%Y/%M/%D/`。
* **failureFolderName**:保存失敗檔案的資料夾。 此位置始終相對於監視的資料夾。 只讀檔案不會被處理，並將保存在失敗資料夾中。 預設值為 `failure/%Y/%M/%D/`。
* **preserveOnFailure**:在無法對服務執行操作時保留輸入檔案。 預設值為true。
* **overwriteDuplicateFilename**:設定為true時，將覆蓋結果資料夾和保留資料夾中的檔案。 設定為false時，名稱會使用具有數字索引尾碼的檔案和資料夾。 預設值為false。

**定義輸入參數值**

建立「監視資料夾」端點時，必須定義輸入參數值。 也就是說，您必須說明傳遞給受監視資料夾調用的操作的輸入值。 例如，請考慮本主題中介紹的過程。 它有一個輸入值， `InDoc` 名為，其資料類型為 `com.adobe.idp.Document`。 為此進程建立「監視資料夾」端點時（在激活進程後，該端點變為服務），必須定義輸入參數值。

要定義「監視資料夾」端點所需的輸入參數值，請指定以下值：

**輸入參數名稱**:輸入參數的名稱。 輸入值的名稱在流程的「工作台」中指定。 如果輸入值屬於服務操作（不是在Workbench中建立的進程的服務），則在component.xml檔案中指定輸入名稱。 例如，本節中引入的進程的輸入參數的名稱為 `InDoc`。

**對應類型**:用於配置調用服務操作所需的輸入值。 映射類型有兩種：

* `Literal`:「監視資料夾」端點使用在顯示時在欄位中輸入的值。 支援所有基本的Java類型。 例如，如果API使用輸入（例如String、long、int和Boolean），則字串將轉換為正確的類型並調用服務。
* `Variable`:輸入的值是受監視資料夾用於選擇輸入的檔案模式。 例如，如果為映射類型選擇「變數」，且輸入文檔必須是PDF檔案，則可以指 `*.pdf`定為映射值。

**對應值**:指定映射類型的值。 例如，如果選擇映射類 `Variable` 型，可以指定 `*.pdf` 為檔案模式。

**資料類型**:指定輸入值的資料類型。 例如，本節中介紹的進程輸入值的資料類型為 `com.adobe.idp.Document`。

**定義輸出參數值**

建立「監視資料夾」端點時，必須定義輸出參數值。 也就是說，您必須說明由「監視資料夾」端點調用的服務返回的輸出值。 例如，請考慮本主題中介紹的過程。 它的輸出值名為， `SecuredDoc` 其資料類型為 `com.adobe.idp.Document`。 為此進程建立「監視資料夾」端點時（在激活進程後，該端點變為服務），必須定義輸出參數值。

要定義「監視資料夾」端點所需的輸出參數值，請指定以下值：

**輸出參數名稱**:輸出參數的名稱。 流程輸出值的名稱在Workbench中指定。 如果輸出值屬於服務操作（不是在Workbench中建立的進程的服務），則輸出名稱在component.xml檔案中指定。 例如，本節中介紹的進程的輸出參數的名稱為 `SecuredDoc`。

**對應類型**:用於配置服務和操作的輸出。 可使用下列選項：

* 如果服務傳回單一物件（單一檔案），則模式為， `%F.pdf` 來源目的地為sourcefilename.pdf。 例如，本節中引入的程式會傳回單一檔案。 因此，映射類型可定義為 `%F.pdf` ( `%F` 表示使用給定檔案名)。 該模式 `%E` 指定輸入文檔的副檔名。
* 如果服務返回清單，則模式為 `Result\%F\`，源目標為Result\sourcefilename\source1 (output 1)和Result\sourcefilename\source2 (output 2)。
* 如果服務返回映射，則模式為 `Result\%F\`，源目標為Result\sourcefilename\file1 and Result\sourcefilename\file2。 如果映射有多個對象，則模式為 `Result\%F.pdf` ，源目標為Result\sourcefilename1.pdf（輸出1）、Result\sourcefilenam2.pdf（輸出2）等。

**資料類型**:指定返回值的資料類型。 例如，本節中介紹的進程返回值的資料類型為 `com.adobe.idp.Document`。

**建立Watched資料夾端點**

在您設定端點的屬性、設定值，並定義輸入和輸出參數值後，您必須建立「監看資料夾」端點。

**啟用端點**

建立「監視資料夾」端點後，必須啟用該端點。 啟用端點時，可用來調用服務。 啟用端點後，可在管理控制台中查看該端點。

**另請參閱**

[使用Java API新增「監視資料夾」端點](programmatically-endpoints.md#add-a-watched-folder-endpoint-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API新增「監視資料夾」端點 {#add-a-watched-folder-endpoint-using-the-java-api}

使用AEM Forms Java API新增「監看資料夾」端點：

1. 包含專案檔案。

   在您Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-livecycle-client.jar。

1. 建立EndpointRegistry客戶端對象。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `EndpointRegistryClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 設定「監視資料夾」端點屬性。

   * 使用其 `CreateEndpointInfo` 建構函式建立物件。
   * 調用物件的方法並傳遞字串值， `CreateEndpointInfo` 以指定 `setConnectorId` 連接器識別碼值 `WatchedFolder`。
   * 調用物件的方法並傳遞描述 `CreateEndpointInfo` 端點的字 `setDescription` 串值，以指定端點的說明。
   * 調用物件的方法並傳遞指 `CreateEndpointInfo` 定名稱的字 `setName` 串值，以指定端點的名稱。
   * 通過調用對象的方法並傳遞指定服務名 `CreateEndpointInfo` 的字串值， `setServiceId` 指定端點所屬的服務。
   * 指定透過叫用物件的方法並傳 `CreateEndpointInfo` 遞指定作 `setOperationName` 業名稱的字串值所呼叫的作業。 通常，為源自在Workbench中建立的流程的服務建立「監視資料夾」端點時，會調用操作的名稱。

1. 指定設定值。

   對於要為「監視資料夾」端點設定的每個配置值，必須調 `CreateEndpointInfo` 用對象的方 `setConfigParameterAsText` 法。 例如，若要設定 `url` 設定值，請叫用物件 `CreateEndpointInfo` 的方法並 `setConfigParameterAsText` 傳遞下列字串值：

   * 指定配置值名稱的字串值。 設定設定 `url` 值時，請指定 `url`。
   * 指定配置值值的字串值。 設定設定值 `url` 時，請指定監看的資料夾位置。
   >[!NOTE]
   >
   >要查看為EncryptDocument服務設定的所有配置值，請參閱 [QuickStart中的Java代碼示例：使用Java API新增「監看資料夾」端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)。

1. 定義輸入參數值。

   調用物件的方法以定義輸 `CreateEndpointInfo` 入參數值， `setInputParameterMapping` 並傳遞下列值：

   * 指定輸入參數名稱的字串值。 例如，EncryptDocument服務的輸入參數的名稱為 `InDoc`。
   * 指定輸入參數的資料類型的字串值。 例如，輸入參數的資料 `InDoc` 類型為 `com.adobe.idp.Document`。
   * 指定映射類型的字串值。 例如，您可以指定 `variable`。
   * 指定映射類型值的字串值。 例如，您可以指定&amp;ast;.pdf作為檔案模式。
   >[!NOTE]
   >
   >調用每 `setInputParameterMapping` 個輸入參數值的方法進行定義。 由於EncryptDocument進程只有一個輸入參數，因此您需要調用此方法一次。

1. 定義輸出參數值。

   調用物件的方法以定義輸 `CreateEndpointInfo` 出參數值， `setOutputParameterMapping` 並傳遞下列值：

   * 指定輸出參數名稱的字串值。 例如，EncryptDocument服務的輸出參數的名稱為 `SecuredDoc`。
   * 一個字串值，它指定輸出參數的資料類型。 例如，輸出參數的資料 `SecuredDoc` 類型為 `com.adobe.idp.Document`。
   * 指定映射類型的字串值。 例如，您可以指定 `%F.pdf`。

1. 建立Watched資料夾端點。

   呼叫物件的方法並傳 `EndpointRegistryClient` 遞物件，以 `createEndpoint` 建立端點 `CreateEndpointInfo` 。 此方法傳回代 `Endpoint` 表Watched資料夾端點的物件。

1. 啟用端點。

   調用物件的方 `EndpointRegistryClient` 法並傳 `enable` 遞方法傳 `Endpoint` 回的物件，以啟用端 `createEndpoint` 點。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API新增「監視資料夾」端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 監視資料夾配置值常數檔案 {#watched-folder-configuration-values-constant-file}

快速 [入門：使用Java API新增「監看資料夾」端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api) ，會使用必須屬於Java專案一部分的常數檔案，以編譯快速開始。 此常數檔案表示在添加「監視資料夾」端點時必須設定的配置值。 以下Java代碼表示常數檔案。

```as3
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

您可以使用AEM Forms Java API，以程式設計方式將電子郵件端點新增至服務。 通過添加電子郵件端點，用戶可以向指定的電子郵件帳戶發送包含一個或多個檔案附件的電子郵件。 然後調用配置服務操作並操作檔案。 在服務執行指定操作後，它會以檔案附件的形式將修改後的檔案發送給發件人，併發送電子郵件。

為了以程式設計方式將電子郵件端點新增至服務，請考慮下列名為 *MyApplication\EncryptDocument的簡短程式*。 如需短暫流程的詳細資訊，請參閱「了 [解AEM Forms流程」](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)。

![ae_ae_encryptdocumentprocess](assets/ae_ae_encryptdocumentprocess.png)

此程式會接受不安全的PDF檔案作為輸入值，然後將不安全的PDF檔案傳遞至加密服務的作 `EncryptPDFUsingPassword` 業。 此程式會使用密碼加密PDF檔案，並傳回密碼加密的PDF檔案作為輸出值。 輸入值的名稱（不安全的PDF文檔） `InDoc` 和資料類型為 `com.adobe.idp.Document`。 輸出值的名稱（密碼加密的PDF檔案） `SecuredDoc` 和資料類型為 `com.adobe.idp.Document`。

>[!NOTE]
>
>您無法使用web services新增電子郵件端點。

### 步驟摘要 {#summary_of_steps-3}

要向服務添加電子郵件端點，請執行以下任務：

1. 包含專案檔案。
1. 建立對 `EndpointRegistryClient` 像。
1. 設定電子郵件端點屬性。
1. 指定設定值。
1. 定義輸入參數值。
1. 定義輸出參數值。
1. 建立電子郵件端點。
1. 啟用端點。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（如果AEM Forms部署在JBoss Application server上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss Application server上，則為必需）

如需這些JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立EndpointRegistry客戶端對象**

您必須先建立物件，才能以程式設計方式新增電子郵件端點 `EndpointRegistryClient` 。

**設定電子郵件端點屬性**

要為服務建立電子郵件端點，請指定以下值：

* **連接器標識符值**:指定所建立的端點類型。 要建立電子郵件端點，請指定 `Email`。
* **說明**:指定端點的說明。
* **名稱**:指定端點的名稱。
* **服務標識符值**:指定端點所屬的服務。 例如，若要將電子郵件端點新增至本節中引入的程式（當使用Workbench啟動程式時，程式會變成服務），請指定 `EncryptDocument`。
* **操作名稱**:指定使用端點調用的操作的名稱。 通常，為源自在Workbench中建立的流程的服務建立電子郵件端點時，操作的名稱為 `invoke`。

**指定配置值**

在以程式設計方式將電子郵件端點新增至服務時，您必須指定電子郵件端點的設定值。 如果使用管理控制台新增電子郵件端點，管理員會指定這些設定值。

>[!NOTE]
>
>受監控的電子郵件帳戶是僅用於電子郵件端點的特殊帳戶。 此帳戶不是一般使用者的電子郵件帳戶。 一般使用者的電子郵件帳戶不得設定為「電子郵件提供者」使用的帳戶，因為「電子郵件提供者」在郵件完成後會從收件匣中刪除電子郵件。

在以寫程式方式將電子郵件端點添加到服務時設定以下配置值：

* **cronExpression**:cron運算式（如果電子郵件必須使用cron運算式來排程）。
* **repeatCount**:電子郵件端點掃描資料夾或目錄的次數。 值-1表示無限掃描。 預設值為-1。
* **repeatInterval**:接收方用於檢查傳入郵件的掃描速率（以秒為單位）。 預設值為10。
* **startDelay**:排程器啟動後等待掃描的時間。 預設時間為0。
* **batchSize**:接收方在每次掃描中處理的電子郵件消息數，以獲得最佳效能。 值-1表示所有電子郵件。 預設值為2。
* **userName**:從電子郵件中叫用目標服務時使用的用戶名。 預設值為 `SuperAdmin`。
* **domainName**:強制設定值。 預設值為 `DefaultDom`。
* **domainPattern**:指定提供者接受的傳入電子郵件的網域模式。 例如，若使用 `adobe.com` 此功能，則只會處理來自adobe.com的電子郵件，而忽略來自其他網域的電子郵件。
* **filePattern**:指定提供程式接受的傳入檔案附件模式。 這包括具有特定檔案名副檔名(&amp;ast;.dat、&amp;ast;.xml)的檔案、具有特定名稱（資料）的檔案，以及具有名稱和副檔名(&amp;ast;)中的複合表達式的檔案。[dD][aA][Tt])。 預設值為 `*`。
* **recipientSuccessfulJob**:傳送訊息以指出成功工作的電子郵件地址。 預設情況下，成功的作業消息始終發送給發送者。 如果您輸 `sender`入，電子郵件結果會傳送給寄件者。 支援最多100個收件者。 指定其他收件者，其電子郵件位址以逗號分隔。 若要關閉此選項，請將此值留空。 在某些情況下，您可能想要觸發程式，而不想收到結果的電子郵件通知。 預設值為 `sender`。
* **recipientFailedJob**:發送消息以指示失敗作業的電子郵件地址。 預設情況下，將始終向發件人發送失敗的作業消息。 如果您輸 `sender`入，電子郵件結果會傳送給寄件者。 支援最多100個收件者。 指定其他收件者，其電子郵件位址以逗號分隔。 若要關閉此選項，請將此值留空。 預設值為 `sender`。
* **inboxHost**:要掃描的電子郵件提供者的收件箱主機名或IP地址。
* **inboxPort**:電子郵件伺服器使用的埠。 POP3的預設值為110,IMAP的預設值為143。 如果啟用SSL，則POP3的預設值為995,IMAP的預設值為993。
* **inboxProtocol**:用於掃描收件箱的電子郵件端點的電子郵件協定。 選項為 `IMAP` 或 `POP3`。 收件箱主機郵件伺服器必須支援這些協定。
* **inboxTimeOut**:電子郵件提供者等待收件匣回應的逾時（秒）。 預設值為60。
* **inboxUser**:登入電子郵件帳戶所需的使用者名稱。 視電子郵件伺服器和設定而定，這可能只是電子郵件的使用者名稱部分，或可能是完整的電子郵件地址。
* **inboxPassword**:收件箱用戶的密碼。
* **inboxSSLEnabled**:設定此值，以在傳送結果或錯誤的通知訊息時強制電子郵件提供者使用SSL。 確保IMAP或POP3主機支援SSL。
* **smtp主機**:電子郵件提供程式發送結果和錯誤消息的郵件伺服器的主機名。
* **smtpPort**:SMTP埠的預設值為25。
* **smtpUser**:電子郵件提供者在傳送結果和錯誤的電子郵件通知時要使用的使用者帳戶。
* **smtpPassword**:SMTP帳戶的口令。 某些郵件伺服器不需要SMTP密碼。
* **charSet**:電子郵件提供者使用的字元集。 預設值為 `UTF-8`。
* **smtpSSLEnabled**:設定此值，以在傳送結果或錯誤的通知訊息時強制電子郵件提供者使用SSL。 確保SMTP主機支援SSL。
* **failedJobFolder**:指定在SMTP郵件伺服器不工作時儲存結果的目錄。
* **非同步**:設為同步時，會處理所有輸入檔案並傳回單一回應。 當設為非同步時，會針對每個已處理的輸入檔案傳送回應。 例如，會為本主題中介紹的程式建立電子郵件端點，並且會向端點的收件匣發送一封電子郵件，該收件匣包含多個不安全的PDF檔案。 當所有PDF檔案都使用密碼加密，且端點設定為同步時，會隨附所有安全的PDF檔案傳送單一回應電子郵件訊息。 如果端點設定為非同步，則會針對每個安全的PDF檔案傳送個別的回應電子郵件訊息。 每封電子郵件都包含一份PDF檔案作為附件。 預設值為非同步。

**定義輸入參數值**

建立電子郵件端點時，必須定義輸入參數值。 也就是說，您必須說明傳遞給電子郵件端點調用的操作的輸入值。 例如，請考慮本主題中介紹的過程。 它有一個輸入值， `InDoc` 名為，其資料類型為 `com.adobe.idp.Document`。 為此進程建立電子郵件端點時（在啟動進程後，該端點變為服務），必須定義輸入參數值。

要定義電子郵件端點所需的輸入參數值，請指定以下值：

**輸入參數名稱**:輸入參數的名稱。 輸入值的名稱在流程的「工作台」中指定。 如果輸入值屬於服務操作（不是在Workbench中建立的進程的Forms服務），則輸入名稱在component.xml檔案中指定。 例如，本節中引入的進程的輸入參數的名稱為 `InDoc`。

**對應類型**:用於配置調用服務操作所需的輸入值。 兩種映射類型如下：

* `Literal`:「電子郵件」端點會使用在顯示欄位中輸入的值。 支援所有基本的Java類型。 例如，如果API使用輸入（例如String、long、int和Boolean），則字串將轉換為正確的類型並調用服務。
* `Variable`:輸入的值是電子郵件端點用於選擇輸入的檔案模式。 例如，如果為映射類型選擇「變數」，且輸入文檔必須是PDF檔案，則可以指 `*.pdf` 定為映射值。

**對應值**:指定映射類型的值。 例如，如果選擇「變數」映射類型，可以指 `*.pdf` 定為檔案模式。

**資料類型**:指定輸入值的資料類型。 例如，本節中引入的程式輸入值的資料類型為com.adobe.idp.Document。

**定義輸出參數值**

建立電子郵件端點時，必須定義輸出參數值。 也就是說，您必須說明由電子郵件端點所呼叫的服務所傳回的輸出值。 例如，請考慮本主題中介紹的過程。 它的輸出值名為， `SecuredDoc` 其資料類型為 `com.adobe.idp.Document`。 為此進程建立電子郵件端點時（在激活進程後，該端點變為服務），必須定義輸出參數值。

要定義「電子郵件」端點所需的輸出參數值，請指定以下值：

**輸出參數名稱**:輸出參數的名稱。 流程輸出值的名稱在Workbench中指定。 如果輸出值屬於服務操作（不是在Workbench中建立的進程的服務），則輸出名稱在component.xml檔案中指定。 例如，本節中介紹的進程的輸出參數的名稱為 `SecuredDoc`。

**對應類型**:用於配置服務和操作的輸出。 可使用下列選項：

* 如果服務傳回單一物件（單一檔案），則模式為， `%F.pdf` 來源目的地為sourcefilename.pdf。 例如，本節中引入的程式會傳回單一檔案。 因此，映射類型可定義為 `%F.pdf` ( `%F` 表示使用給定檔案名)。 該模式 `%E` 指定輸入文檔的副檔名。
* 如果服務返回清單，則模式為 `Result\%F\`，源目標為Result\sourcefilename\source1 (output 1)和Result\sourcefilename\source2 (output 2)。
* 如果服務返回映射，則模式為 `Result\%F\`，源目標為Result\sourcefilename\file1 and Result\sourcefilename\file2。 如果映射有多個對象，則模式為 `Result\%F.pdf` ，源目標為Result\sourcefilename1.pdf（輸出1）、Result\sourcefilenam2.pdf（輸出2）等。

**資料類型**:指定返回值的資料類型。 例如，本節中介紹的進程返回值的資料類型為 `com.adobe.idp.Document`。

**建立電子郵件端點**

在您設定「電子郵件」端點屬性和配置值並定義輸入和輸出參數值後，必須建立「電子郵件」端點。

**啟用端點**

建立電子郵件端點後，必須啟用該端點。 啟用端點時，可用來調用服務。 啟用端點後，可在管理控制台中查看該端點。

**另請參閱**

[使用Java API新增電子郵件端點](programmatically-endpoints.md#add-an-email-endpoint-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API新增電子郵件端點 {#add-an-email-endpoint-using-the-java-api}

使用Java API新增電子郵件端點：

1. 包含專案檔案。

   在您Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-livecycle-client.jar。

1. 建立EndpointRegistry客戶端對象。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `EndpointRegistryClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 設定電子郵件端點屬性。

   * 使用其 `CreateEndpointInfo` 建構函式建立物件。
   * 調用物件的方法並傳遞字串值， `CreateEndpointInfo` 以指定 `setConnectorId` 連接器識別碼值 `Email`。
   * 調用物件的方法並傳遞描述 `CreateEndpointInfo` 端點的字 `setDescription` 串值，以指定端點的說明。
   * 調用物件的方法並傳遞指 `CreateEndpointInfo` 定名稱的字 `setName` 串值，以指定端點的名稱。
   * 通過調用對象的方法並傳遞指定服務名 `CreateEndpointInfo` 的字串值， `setServiceId` 指定端點所屬的服務。
   * 指定透過叫用物件的方法並傳 `CreateEndpointInfo` 遞指定作 `setOperationName` 業名稱的字串值所呼叫的作業。 通常，為源自在Workbench中建立的流程的服務建立電子郵件端點時，會調用操作的名稱。

1. 指定設定值。

   對於要為電子郵件端點設定的每個配置值，必須調 `CreateEndpointInfo` 用對象的方 `setConfigParameterAsText` 法。 例如，若要設定 `smtpHost` 設定值，請叫用物 `CreateEndpointInfo` 件的方 `setConfigParameterAsText` 法並傳遞下列值：

   * 指定配置值名稱的字串值。 設定設定 `smtpHost` 值時，請指定 `smtpHost`。
   * 指定配置值值的字串值。 設定配 `smtpHost` 置值時，請指定指定SMTP伺服器名稱的字串值。
   >[!NOTE]
   >
   >要查看本節中介紹的EncryptDocument服務的所有配置值集，請參見 [QuickStart上的Java代碼示例：使用Java API新增電子郵件端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api)。

1. 定義輸入參數值。

   調用物件的方法以定義輸 `CreateEndpointInfo` 入參數值， `setInputParameterMapping` 並傳遞下列值：

   * 指定輸入參數名稱的字串值。 例如，EncryptDocument服務的輸入參數的名稱為 `InDoc`。
   * 指定輸入參數的資料類型的字串值。 例如，輸入參數的資料 `InDoc` 類型為 `com.adobe.idp.Document`。
   * 指定映射類型的字串值。 例如，您可以指定 `variable`。
   * 指定映射類型值的字串值。 例如，您可以指定&amp;ast;.pdf作為檔案模式。
   >[!NOTE]
   >
   >調用每 `setInputParameterMapping` 個輸入參數值的方法進行定義。 由於EncryptDocument進程只有一個輸入參數，因此您需要調用此方法一次。

1. 定義輸出參數值。

   調用物件的方法並傳遞下 `CreateEndpointInfo` 列值，以 `setOutputParameterMapping` 定義輸出參數值：

   * 指定輸出參數名稱的字串值。 例如，EncryptDocument服務的輸出參數的名稱為 `SecuredDoc`。
   * 一個字串值，它指定輸出參數的資料類型。 例如，輸出參數的資料 `SecuredDoc` 類型為 `com.adobe.idp.Document`。
   * 指定映射類型的字串值。 例如，您可以指定 `%F.pdf`。

1. 建立電子郵件端點。

   呼叫物件的方法並傳 `EndpointRegistryClient` 遞物件，以 `createEndpoint` 建立端點 `CreateEndpointInfo` 。 此方法返回代 `Endpoint` 表電子郵件端點的對象。

1. 啟用端點。

   調用物件的方 `EndpointRegistryClient` 法並傳 `enable` 遞方法傳 `Endpoint` 回的物件，以啟用端 `createEndpoint` 點。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API新增「監視資料夾」端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 電子郵件組態值常數檔案 {#email-configuration-values-constant-file}

快速 [入門：使用Java API新增電子郵件端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api) ，會使用必須屬於Java專案一部分的常數檔案，以編譯快速入門。 此常數檔案表示添加電子郵件端點時必須設定的配置值。 以下Java代碼表示常數檔案。

```as3
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

## 添加遠程端點 {#adding-remoting-endpoints}

>[!NOTE]
>
>JEE上的AEM表單不建議使用LiveCycle Remoting API。

您可以使用AEM Forms Java API，以程式設計方式將遠端端點新增至服務。 借由新增Remoting端點，您就可讓Flex應用程式使用remoting來叫用服務。 (請參 [閱「使用（AEM表單已過時）AEM Forms Remoting叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)」)。

為了以程式設計方式將Remoting端點新增至服務，請考慮下列名為 *EncryptDocument的簡短程式*。

![ar_ar_encryptdocumentprocess](assets/ar_ar_encryptdocumentprocess.png)

此程式會接受不安全的PDF檔案作為輸入值，然後將不安全的PDF檔案傳遞至加密服務的作 `EncryptPDFUsingPassword` 業。 PDF檔案會以密碼加密，而密碼加密的PDF檔案就是此程式的輸出值。 輸入值的名稱（不安全的PDF文檔） `InDoc` 和資料類型為 `com.adobe.idp.Document`。 輸出值的名稱（密碼加密的PDF檔案） `SecuredDoc` 和資料類型為 `com.adobe.idp.Document`。

為演示如何向服務添加遠程端點，本節將遠程端點添加到名為EncryptDocument的服務。

>[!NOTE]
>
>您無法使用web services添加遠程端點。

### 步驟摘要 {#summary_of_steps-4}

要從服務中刪除端點，請執行以下任務：

1. 包含專案檔案。
1. 建立對 `EndpointRegistryClient` 像。
1. 設定「刪除」端點屬性。
1. 建立遠程端點。
1. 啟用端點。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（如果AEM Forms部署在JBoss Application server上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss Application server上，則為必需）

如需這些JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立EndpointRegistry客戶端對象**

要以寫程式方式添加遠程端點，必須建立對 `EndpointRegistryClient` 像。

**設定遠程端點屬性**

要為服務建立遠程端點，請指定以下值：

* **連接器標識符值**:指定所建立的端點類型。 要建立遠程端點，請指定 `Remoting`。
* **說明**:指定端點的說明。
* **名稱**:指定端點的名稱。
* **服務標識符值**:指定端點所屬的服務。 例如，要將遠程端點添加到本節中介紹的進程（進程在Workbench中激活後即變為服務），請指定 `EncryptDocument`。
* **操作名稱**:指定使用端點調用的操作的名稱。 建立遠程端點時，請指定通配符(&amp;ast;)。

**建立遠程端點**

設定Remoting端點屬性後，可以為服務建立Remoting端點。

**啟用端點**

建立新端點後，必須啟用該端點。 啟用Remoting端點時，Flex用戶端會呼叫服務。

**另請參閱**

[使用Java API新增遠端端點](programmatically-endpoints.md#add-a-remoting-endpoint-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API新增遠端端點 {#add-a-remoting-endpoint-using-the-java-api}

使用Java API新增遠端端點：

1. 包含專案檔案。

   在您Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-livecycle-client.jar。

1. 建立EndpointRegistry客戶端對象。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `EndpointRegistryClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 設定「刪除」端點屬性。

   * 使用其 `CreateEndpointInfo` 建構函式建立物件。
   * 調用物件的方法並傳遞字串值， `CreateEndpointInfo` 以指定 `setConnectorId` 連接器識別碼值 `Remoting`。
   * 調用物件的方法並傳遞描述 `CreateEndpointInfo` 端點的字 `setDescription` 串值，以指定端點的說明。
   * 調用物件的方法並傳遞指 `CreateEndpointInfo` 定名稱的字 `setName` 串值，以指定端點的名稱。
   * 通過調用對象的方法並傳遞指定服務名 `CreateEndpointInfo` 的字串值， `setServiceId` 指定端點所屬的服務。
   * 指定物件方法所呼叫的 `CreateEndpointInfo` 操作，並 `setOperationName` 傳遞指定操作名稱的字串值。 對於Remoting端點，請指定通配符(&amp;ast;)。

1. 建立遠程端點。

   呼叫物件的方法並傳 `EndpointRegistryClient` 遞物件，以 `createEndpoint` 建立端點 `CreateEndpointInfo` 。 此方法返回 `Endpoint` 表示新Remoting端點的對象。

1. 啟用端點。

   調用物件的方 `EndpointRegistryClient` 法並傳 `enable` 遞方法傳 `Endpoint` 回的物件，以啟用端 `createEndpoint` 點。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API新增遠端端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-remoting-endpoint-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 添加TaskManager端點 {#adding-taskmanager-endpoints}

您可以使用AEM Forms Java API，以程式設計方式將TaskManager端點新增至服務。 通過將TaskManager端點添加到服務中，可讓Workspace用戶調用服務。 即，在工作區中工作的用戶可以調用具有相應TaskManager端點的進程。

>[!NOTE]
>
>不能通過使用Web服務添加TaskManager端點。

### 步驟摘要 {#summary_of_steps-5}

要向服務添加TaskManager端點，請執行以下任務：

1. 包含專案檔案。
1. 建立對 `EndpointRegistryClient` 像。
1. 為端點建立類別。
1. 設定TaskManager端點屬性。
1. 建立TaskManager端點。
1. 啟用端點。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（如果AEM Forms部署在JBoss Application server上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss Application server上，則為必需）

如需這些JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立EndpointRegistry客戶端對象**

必須先建立對象，才能以寫程式方式添加TaskManager端 `EndpointRegistryClient` 點。

**為端點建立類別**

類別可用來組織工作區中的服務。 也就是說，工作區用戶可以通過在工作區中選擇類別來調用具有TaskManager端點的服務。 建立TaskManager端點時，可以引用現有類別或以寫程式方式建立新類別。

>[!NOTE]
>
>本節將建立新類別，作為向服務添加TaskManager端點的一部分。

**設定TaskManager端點屬性**

要為服務建立TaskManager端點，請指定以下值：

* **連接器識別碼**:指定所建立的端點類型。 要建立TaskManager端點，請指定 `TaskManagerConnector`。
* **說明**:指定端點的說明。
* **名稱**:指定端點的名稱。
* **服務識別碼**:指定端點所屬的服務。
* **類別**:指定與TaskManager端點關聯的類別標識符值。
* **操作名稱**:通常，為源自在Workbench中建立的進程的服務建立TaskManager端點時，操作的名稱為 `invoke`。

**建立TaskManager端點**

設定TaskManager端點屬性後，可以為服務建立TaskManager端點。

**啟用端點**

建立新端點後，必須啟用該端點。 啟用端點時，可用來從工作區中叫用服務。 啟用端點後，可在管理控制台中查看該端點。

**另請參閱**

[使用Java API添加TaskManager端點](programmatically-endpoints.md#add-a-taskmanager-endpoint-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加TaskManager端點 {#add-a-taskmanager-endpoint-using-the-java-api}

使用Java API添加TaskManager端點：

1. 包含專案檔案。

   在您Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-livecycle-client.jar。

1. 建立EndpointRegistry客戶端對象。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `EndpointRegistryClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 為端點建立類別。

   * 使用其 `CreateEndpointCategoryInfo` 建構函式並傳遞下列值來建立物件：

      * 指定類別識別碼值的字串值
      * 指定類別說明的字串值
   * 呼叫物件的方法並傳 `EndpointRegistryClient` 遞物件， `createEndpointCategory` 以建立類 `CreateEndpointCategoryInfo` 別。 此方法返回 `EndpointCategory` 表示新類別的對象。


1. 設定TaskManager端點屬性。

   * 使用其 `CreateEndpointInfo` 建構函式建立物件。
   * 調用物件的方法並傳遞字串值， `CreateEndpointInfo` 以指定 `setConnectorId` 連接器識別碼值 `TaskManagerConnector`。
   * 調用物件的方法並傳遞描述 `CreateEndpointInfo` 端點的字 `setDescription` 串值，以指定端點的說明。
   * 調用物件的方法並傳遞指 `CreateEndpointInfo` 定名稱的字 `setName` 串值，以指定端點的名稱。
   * 通過調用對象的方法並傳遞指定服務名 `CreateEndpointInfo` 的字串值， `setServiceId` 指定端點所屬的服務。
   * 調用物件的方法並傳遞指定類別識 `CreateEndpointInfo` 別碼值的字 `setCategoryId` 串值，以指定端點所屬的類別。 您可以叫用物 `EndpointCategory` 件的方 `getId` 法，以取得此類別的識別碼值。
   * 指定透過叫用物件的方法並傳 `CreateEndpointInfo` 遞指定作 `setOperationName` 業名稱的字串值所呼叫的作業。 通常，在為源自 `TaskManager` 於在Workbench中建立的進程的服務建立端點時，操作的名稱為 `invoke`。

1. 建立TaskManager端點。

   呼叫物件的方法並傳 `EndpointRegistryClient` 遞物件，以 `createEndpoint` 建立端點 `CreateEndpointInfo` 。 此方法返回一 `Endpoint` 個表示新TaskManager端點的對象。

1. 啟用端點。

   調用物件的方 `EndpointRegistryClient` 法並傳 `enable` 遞方法傳 `Endpoint` 回的物件，以啟用端 `createEndpoint` 點。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API添加TaskManager端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-taskmanager-endpoint-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 修改端點 {#modifying-endpoints}

您可以使用AEM Forms Java API，以程式設計方式修改現有端點。 通過修改端點，可以更改端點的行為。 例如，考慮指定用作監視資料夾的資料夾的「監視資料夾」端點。 您可以以程式設計方式修改屬於「Watched Folder」端點的設定值，使另一個資料夾可當成「Watched」資料夾運作。 有關屬於「監視資料夾」端點的配置值的資訊，請參 [閱添加監視資料夾端點](programmatically-endpoints.md#adding-watched-folder-endpoints)。

為示範如何修改端點，本節會變更動作為監視資料夾的資料夾，以修改「監視資料夾」端點。

>[!NOTE]
>
>您不能使用web services修改端點。

### 步驟摘要 {#summary_of_steps-6}

要修改端點，請執行以下任務：

1. 包含專案檔案。
1. 建立對 `EndpointRegistryClient` 像。
1. 檢索端點。
1. 指定新的設定值。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（如果AEM Forms部署在JBoss Application server上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss Application server上，則為必需）

如需這些JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立EndpointRegistry客戶端對象**

要以寫程式方式修改端點，必須建立對 `EndpointRegistryClient` 像。

**檢索要修改的端點**

在可以修改端點之前，必須先檢索端點。 要檢索端點，您必須以可訪問端點的用戶身份連接。 建議您以管理員身分連線。 (請參 [閱設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties))。

可通過檢索端點清單來檢索端點。 然後，您可以循環瀏覽清單，搜索要刪除的特定端點。 例如，可以通過確定與端點對應的服務和端點類型來定位端點。 找到端點後，可以對其進行修改。

**指定新的設定值**

修改端點時，請指定新的配置值。 例如，要修改Watched資料夾端點，請重設所有Watched資料夾端點配置值，而不只是要修改的值。 有關屬於「監視資料夾」端點的配置值的資訊，請參 [閱添加監視資料夾端點](programmatically-endpoints.md#adding-watched-folder-endpoints)。

>[!NOTE]
>
>有關屬於電子郵件端點的配置值的資訊，請參 [閱添加電子郵件端點](programmatically-endpoints.md#adding-email-endpoints)。

>[!NOTE]
>
>不能修改端點調用的服務。 如果您嘗試修改服務，則會拋出異常。 要修改與給定端點關聯的服務，請刪除該端點並建立新端點。 (請參閱 [移除端點](programmatically-endpoints.md#removing-endpoints)。)

**另請參閱**

[使用Java API修改端點](programmatically-endpoints.md#modifying-an-endpoint-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API修改端點 {#modifying-an-endpoint-using-the-java-api}

使用Java API修改端點：

1. 包含專案檔案。

   在您Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-livecycle-client.jar。

1. 建立EndpointRegistry客戶端對象。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `EndpointRegistryClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 檢索要修改的端點。

   * 擷取目前使用者（在連線屬性中指定）可存取的所有端點清單，方法是叫用 `EndpointRegistryClient` 物件的方 `getEndpoints` 法，並傳 `PagingFilter` 遞作為篩選的物件。 您可以傳遞 `(PagingFilter)null` 值以傳回所有端點。 此方法返回每個 `java.util.List` 元素都是對象的對 `Endpoint` 像。 如需物件的詳細 `PagingFilter` 資訊，請參 [閱「AEM Forms API參考」](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 逐步遍歷對 `java.util.List` 像以確定其是否具有端點。 如果端點存在，則每個元素都是實 `EndPoint` 例。
   * 調用物件的方法，以判斷對應於 `EndPoint` 端點的服 `getServiceId` 務。 此方法返回指定服務名的字串值。
   * 調用物件的方法，以 `EndPoint` 決定端點類 `getConnectorId` 型。 此方法返回指定端點類型的字串值。 例如，如果端點是Watched資料夾端點，則此方法會傳回 `WatchedFolder`。

1. 指定新的設定值。

   * 通過調用 `ModifyEndpointInfo` 其建構子建立對象。
   * 對於要設定的每個設定值，請叫 `ModifyEndpointInfo` 用物件的方 `setConfigParameterAsText` 法。 例如，若要設定URL設定值，請叫用物 `ModifyEndpointInfo` 件的方 `setConfigParameterAsText` 法並傳遞下列值：

      * 指定配置值名稱的字串值。 例如，要設定配 `url` 置值，請指定 `url`。
      * 指定配置值值的字串值。 要定義配置值的 `url` 值，請指定監視的資料夾位置。
   * 叫用物 `EndpointRegistryClient` 件的方 `modifyEndpoint` 法並傳遞物 `ModifyEndpointInfo` 件。


**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API修改端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-modifying-an-endpoint-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 移除端點 {#removing-endpoints}

您可以使用AEM Forms Java API，以程式設計方式從服務移除端點。 刪除端點後，無法使用啟用該端點的調用方法調用服務。 例如，如果從服務中刪除SOAP端點，則不能使用SOAP模式調用服務。

為演示如何從服務中刪除端點，本節將從名為 *EncryptDocument的服務中刪除EJB端點*。

>[!NOTE]
>
>您無法使用web services移除端點。

### 步驟摘要 {#summary_of_steps-7}

要從服務中刪除端點，請執行以下任務：

1. 包含專案檔案。
1. 建立對 `EndpointRegistryClient` 像。
1. 檢索端點。
1. 移除端點。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（如果AEM Forms部署在JBoss Application server上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss Application server上，則為必需）

如需這些JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立EndpointRegistry客戶端對象**

要以寫程式方式刪除端點，必須建立對 `EndpointRegistryClient` 像。

**檢索要刪除的端點**

必須先檢索端點，才能刪除端點。 要檢索端點，您必須以可訪問端點的用戶身份連接。 建議您以管理員身分連線。 (請參 [閱設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties))。

可通過檢索端點清單來檢索端點。 然後，您可以循環瀏覽清單，搜索要刪除的特定端點。 例如，可以通過確定與端點對應的服務和端點類型來定位端點。 找到端點後，可將其刪除。

**移除端點**

建立新端點後，必須啟用該端點。 啟用端點時，可用來調用服務。 啟用端點後，可在管理控制台中查看該端點。

**另請參閱**

[使用Java API移除端點](programmatically-endpoints.md#removing-an-endpoint-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API移除端點 {#removing-an-endpoint-using-the-java-api}

使用Java API移除端點：

1. 包含專案檔案。

   在您Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-livecycle-client.jar。

1. 建立EndpointRegistry客戶端對象。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `EndpointRegistryClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 檢索要刪除的端點。

   * 叫用物件的方法並傳遞作為篩選的物件，以擷取目前使用者（在連線屬性中指定）可存取的 `EndpointRegistryClient` 所 `getEndpoints` 有 `PagingFilter` 端點清單。 您可以傳遞 `(PagingFilter)null` 以傳回所有端點。 此方法返回每個 `java.util.List` 元素都是對象的對 `Endpoint` 像。
   * 逐步遍歷對 `java.util.List` 像以確定其是否具有端點。 如果端點存在，則每個元素都是實 `EndPoint` 例。
   * 調用物件的方法，以判斷對應於 `EndPoint` 端點的服 `getServiceId` 務。 此方法返回指定服務名的字串值。
   * 調用物件的方法，以 `EndPoint` 決定端點類 `getConnectorId` 型。 此方法返回指定端點類型的字串值。 例如，如果端點是EJB端點，則此方法返回 `EJB`。

1. 移除端點。

   叫用物件的方 `EndpointRegistryClient` 法並傳遞 `remove` 代表要移除 `EndPoint` 之端點的物件，以移除端點。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API移除端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-removing-an-endpoint-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 檢索端點連接器資訊 {#retrieving-endpoint-connector-information}

您可以使用AEM Forms API，以程式設計方式擷取端點連接器的相關資訊。 連接器使端點能夠使用各種調用方法調用服務。 例如，「監視資料夾」連接器使端點能夠使用監視資料夾調用服務。 通過以寫程式方式檢索端點連接器的資訊，可以檢索與連接器相關聯的配置值，例如需要哪些配置值以及哪些配置值是可選的。

為示範如何擷取端點連接器的相關資訊，本節會擷取有關Watched資料夾連接器的資訊。 (請參閱 [新增監看資料夾端點](programmatically-endpoints.md#adding-watched-folder-endpoints)。)

>[!NOTE]
>
>您無法使用web services擷取端點的相關資訊。

>[!NOTE]
>
>本主題使用 `ConnectorRegistryClient` API來擷取端點連接器的相關資訊。 (請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

### 步驟摘要 {#summary_of_steps-8}

要檢索端點連接器資訊，請執行以下任務：

1. 包含專案檔案。
1. 建立對 `ConnectorRegistryClient` 像。
1. 指定連接器類型。
1. 檢索配置值。

**包含專案檔案**

將必要的檔案加入您的開發專案中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請確定您包含proxy檔案。

必須將下列JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar（如果AEM Forms部署在JBoss Application server上，則為必要項）
* jbossall-client.jar（如果AEM Forms部署在JBoss Application server上，則為必需）

如果AEM Forms部署在非JBoss的受支援J2EE應用程式伺服器上，則請將adobe-utilities.jar和jbossall-client.jar取代為JAR檔案，此JAR檔案是部署AEM Forms的J2EE應用程式伺服器專用。 如需所有AEM Forms JAR檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立ConnectorRegistry客戶端對象**

要以寫程式方式檢索端點連接器資訊，請建立 `ConnectorRegistryClient` 對象。

**指定連接器類型**

指定要從中檢索資訊的連接器類型。 存在以下類型的連接器：

* **EJB**:使客戶端應用程式能夠使用EJB模式調用服務。
* **SOAP**:使客戶端應用程式能夠使用SOAP模式調用服務。
* **Watched Folder**:使受監視的資料夾能夠調用服務。
* **電子郵件**:啟用電子郵件訊息以叫用服務。
* **移除**:可讓Flex用戶端應用程式叫用服務。
* **TaskManagerConnector**:使工作區用戶能夠從工作區中調用服務。

**檢索配置值**

指定連接器類型後，可以檢索有關連接器的資訊，如支援的配置值。 例如，對於任何連接器，您可以確定需要哪些配置值以及哪些配置值是可選的。

**另請參閱**

[使用Java API擷取端點連接器資訊](programmatically-endpoints.md#retrieve-endpoint-connector-information-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API擷取端點連接器資訊 {#retrieve-endpoint-connector-information-using-the-java-api}

使用Java API擷取端點連接器資訊：

1. 包含專案檔案。.

   在您Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-livecycle-client.jar。

1. 建立ConnectorRegistry Client對象。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。
   * 使用其 `ConnectorRegistryClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 指定連接器類型。

   通過調用對象的方法並傳遞 `ConnectorRegistryClient` 指定連接器 `getEndpointDefinition` 類型的字串值來指定連接器類型。 例如，若要指定「Watched資料夾」連接器類型，請傳遞字串值 `WatchedFolder`。 此方法返回與 `Endpoint` 連接器類型對應的對象。

1. 檢索配置值。

   * 通過調用對象的方法來檢索在此端點中 `Endpoint` 關聯的配 `getConfigParameters` 置值。 此方法會傳回物件 `ConfigParameter` 陣列。
   * 通過檢索陣列中的每個元素來檢索有關每個配置值的資訊。 每個元素都是物 `ConfigParameter` 件。 例如，您可以叫用物件的方法，以決定設定值是必要 `ConfigParameter` 還是可 `isRequired` 選。 如果需要設定值，則此方法會傳回 `true`。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API檢索端點連接器資訊](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-retrieving-endpoint-connector-information-using-the-java-api)

[包含AEM Forms java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
