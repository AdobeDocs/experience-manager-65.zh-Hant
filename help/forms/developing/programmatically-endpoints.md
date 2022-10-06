---
title: 以寫程式方式管理端點
seo-title: Programmatically Managing Endpoints
description: 使用Endpoint Registry服務添加EJB端點、添加SOAP端點、添加監視資料夾端點、添加電子郵件端點、添加遠程處理端點、添加Task Manager端點、修改端點、刪除端點以及檢索端點連接器資訊。
seo-description: Use the Endpoint Registry service to add EJB endpoints, add SOAP endpoint, add Watched Folder endpoints, add Email endpoints, add  Remoting endpoints, add Task Manager endpoints, modify endpoints, remove endpoints, and retrieve endpoint connector information.
uuid: 5dc50946-3323-4c5d-a43b-31c1c980bd04
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 076889a7-9c9f-4b6f-a45b-67a9b3923c36
role: Developer
exl-id: b94dcca2-136b-4b7d-b5ce-544804575876
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '10805'
ht-degree: 0%

---

# 以寫程式方式管理端點 {#programmatically-managing-endpoints}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於端點註冊表服務**

Endpoint Registry服務提供以寫程式方式管理端點的功能。 例如，您可以將下列類型的端點新增至服務：

* EJB
* SOAP
* 監看資料夾
* 電子郵件
* (AEM表單已淘汰)遠端
* 任務管理員

>[!NOTE]
>
>SOAP、EJB和(JEE上的AEM表單已棄用)會為每個已激活的服務自動建立遠程端點。 SOAP和EJB終結點為所有服務操作啟用SOAP和EJB。

遠端端點可讓Flex用戶端叫用端點已新增至之AEM Forms服務上的作業。 建立與端點同名的Flex目標，Flex客戶端可以建立指向此目標的RemoteObjects，以調用相關服務上的操作。

電子郵件、任務管理器和監視的資料夾端點僅顯示服務的特定操作。 添加這些端點需要第二個配置步驟來選擇調用方法、設定配置參數以及指定輸入和輸出參數映射。

您可以將TaskManager端點組織到名為 *類別*. 然後，這些類別將通過TaskManager公開到Workspace中，最終用戶將按分類查看TaskManager端點。 在工作區中，一般使用者會在導覽窗格中看到這些類別。 每個類別中的端點會在工作區的「啟動程式」頁面上顯示為程式卡。

您可以使用Endpoint Registry服務完成以下任務：

* 添加EJB終結點。 (請參閱 [添加EJB終結點](programmatically-endpoints.md#adding-ejb-endpoints).)
* 添加SOAP端點。 (請參閱 [添加SOAP端點](programmatically-endpoints.md#adding-soap-endpoints).)
* 添加監視的資料夾端點(請參閱 [添加監視的資料夾端點](programmatically-endpoints.md#adding-watched-folder-endpoints).)
* 新增電子郵件端點。 (請參閱 [新增電子郵件端點](programmatically-endpoints.md#adding-email-endpoints).)
* 新增遠端端點。 (請參閱 [新增遠端端點](programmatically-endpoints.md#adding-remoting-endpoints).)
* 添加TaskManager終結點(請參閱 [添加TaskManager端點](programmatically-endpoints.md#adding-taskmanager-endpoints).)
* 修改端點(請參閱 [修改端點](programmatically-endpoints.md#modifying-endpoints).)
* 移除端點(請參閱 [移除端點](programmatically-endpoints.md#removing-endpoints).)
* 檢索端點連接器資訊(請參閱 [檢索端點連接器資訊](programmatically-endpoints.md#retrieving-endpoint-connector-information).)

## 添加EJB終結點 {#adding-ejb-endpoints}

可以使用AEM Forms Java API以寫程式方式將EJB端點添加到服務中。 通過將EJB端點添加到服務中，可以使客戶端應用程式使用EJB模式調用該服務。 也就是說，在設定調用AEM Forms所需的連接屬性時，可以選擇EJB模式。 (請參閱 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>不能使用Web服務添加EJB終結點。

>[!NOTE]
>
>通常，EJB端點預設會添加到服務中。但是，EJB端點可以添加到以寫程式方式部署的進程中，或者在刪除EJB端點時添加到該進程中，並且必須重新添加。

### 步驟摘要 {#summary-of-steps}

要將EJB端點添加到服務，請執行以下任務：

1. 包含專案檔案。
1. 建立 `EndpointRegistry Client` 物件。
1. 設定EJB終結點屬性。
1. 建立EJB終結點。
1. 啟用端點。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss Application Server上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss Application Server上則為必要)

有關這些JAR檔案的位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立EndpointRegistry客戶端對象**

在以寫程式方式添加EJB端點之前，必須先建立 `EndpointRegistryClient` 物件。

**設定EJB終結點屬性**

要為服務建立EJB端點，請指定以下值：

* **連接器識別碼**:指定要建立的端點類型。 要建立EJB終結點，請指定 `EJB`.
* **說明**:指定端點說明。
* **名稱**:指定端點的名稱。
* **服務標識符**:指定端點所屬的服務。
* **操作名稱**:指定使用端點調用的操作的名稱。 建立EJB端點時，請指定通配符( `*`)。 但是，如果要指定特定操作而不是調用所有服務操作，請指定操作的名稱，而不是使用通配符( `*`)。

**建立EJB終結點**

設定EJB終結點屬性後，可以為服務建立EJB終結點。

**啟用端點**

建立新端點後，必須啟用它。 啟用端點後，即可用來叫用服務。 啟用端點後，您就可以在管理控制台中檢視它。

**另請參閱**

[使用Java API添加EJB端點](programmatically-endpoints.md#adding-an-ejb-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加EJB端點 {#adding-an-ejb-endpoint-using-the-java-api}

使用Java API添加EJB端點：

1. 包含專案檔案。

   在您Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-livecycle-client.jar。 (

1. 建立EndpointRegistry客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EndpointRegistryClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 設定EJB終結點屬性。

   * 建立 `CreateEndpointInfo` 物件，使用其建構子。
   * 叫用 `CreateEndpointInfo` 物件 `setConnectorId` 方法和傳遞字串值 `EJB`.
   * 叫用 `CreateEndpointInfo` 物件 `setDescription` 方法，並傳遞描述端點的字串值。
   * 叫用 `CreateEndpointInfo` 物件 `setName` 方法，並傳遞指定名稱的字串值。
   * 通過調用 `CreateEndpointInfo` 物件 `setServiceId` 方法，並傳遞指定服務名稱的字串值。
   * 指定通過調用 `CreateEndpointInfo` 物件 `setOperationName` 方法，並傳遞指定操作名稱的字串值。 對於SOAP和EJB端點，請指定通配符( `*`)，表示所有操作。

1. 建立EJB終結點。

   叫用 `EndpointRegistryClient` 物件 `createEndpoint` 方法和傳遞 `CreateEndpointInfo` 物件。 此方法會傳回 `Endpoint` 表示新EJB端點的對象。

1. 啟用端點。

   叫用 `EndpointRegistryClient` 對象的啟用方法和傳遞 `Endpoint` 由傳回的物件 `createEndpoint` 方法。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API添加EJB端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-ejb-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 添加SOAP端點 {#adding-soap-endpoints}

您可以使用AEM Forms Java API以程式設計方式將SOAP端點新增至服務。 通過添加SOAP端點，可以使客戶端應用程式能夠使用SOAP模式調用服務。 也就是說，在設定調用AEM Forms所需的連接屬性時，可以選擇SOAP模式。

>[!NOTE]
>
>不能使用Web服務添加SOAP端點。

>[!NOTE]
>
>通常，SOAP端點預設會添加到服務中。但是，SOAP端點可以添加到以寫程式方式部署的進程中，或者在刪除SOAP端點時添加，並且必須重新添加。

### 步驟摘要 {#summary_of_steps-1}

要向服務添加SOAP端點，請執行以下任務：

1. 包含專案檔案。
1. 建立 `EndpointRegistryClient` 物件。
1. 設定SOAP終結點屬性。
1. 建立SOAP端點。
1. 啟用端點。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss Application Server上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss Application Server上則為必要)

建立SOAP端點時需要這些JAR檔案。 但是，如果使用SOAP端點調用服務，則需要添加JAR檔案。 如需AEM Forms JAR檔案的相關資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立EndpointRegistry客戶端對象**

要以寫程式方式將SOAP端點添加到服務，必須建立 `EndpointRegistryClient` 物件。

**設定SOAP終結點屬性**

要向服務添加SOAP端點，請指定以下值：

* **連接器識別碼值**:指定要建立的端點類型。 要建立SOAP端點，請指定 `SOAP`.
* **說明**:指定端點說明。
* **名稱**:指定端點名稱。
* **服務標識符值**:指定端點所屬的服務。
* **操作名稱**:指定使用端點調用的操作的名稱。 建立SOAP端點時，請指定通配符( `*`)。 但是，如果要指定特定操作而不是調用所有服務操作，請指定操作的名稱，而不是使用通配符( `*`)。

**建立SOAP端點**

設定SOAP端點屬性後，可以建立SOAP端點。

**啟用端點**

建立新端點後，必須啟用它。 啟用端點時，可用來叫用服務。 啟用端點後，您就可以在管理控制台中查看它。

**另請參閱**

[使用Java API添加SOAP端點](programmatically-endpoints.md#add-a-soap-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加SOAP端點 {#add-a-soap-endpoint-using-the-java-api}

使用Java API將SOAP端點新增至服務：

1. 包含專案檔案。

   在您Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-livecycle-client.jar。

1. 建立EndpointRegistry客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EndpointRegistryClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 設定SOAP終結點屬性。

   * 建立 `CreateEndpointInfo` 物件，使用其建構子。
   * 叫用 `CreateEndpointInfo` 物件 `setConnectorId` 方法和傳遞字串值 `SOAP`.
   * 叫用 `CreateEndpointInfo` 物件 `setDescription` 方法，並傳遞描述端點的字串值。
   * 叫用 `CreateEndpointInfo` 物件 `setName` 方法，並傳遞指定名稱的字串值。
   * 通過調用 `CreateEndpointInfo` 物件 `setServiceId` 方法，並傳遞指定服務名稱的字串值。
   * 指定通過調用 `CreateEndpointInfo` 物件 `setOperationName` 方法，並傳遞指定操作名稱的字串值。 對於SOAP和EJB端點，請指定通配符( `*`)，表示所有操作。

1. 建立SOAP端點。

   叫用 `EndpointRegistryClient` 物件 `createEndpoint` 方法和傳遞 `CreateEndpointInfo` 物件。 此方法會傳回 `Endpoint` 表示新SOAP端點的對象。

1. 啟用端點。

   叫用 `EndpointRegistryClient` 物件的啟用方法，並傳遞 `Endpoint` 由傳回的物件 `createEndpoint` 方法。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API添加SOAP端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-soap-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 添加監視的資料夾端點 {#adding-watched-folder-endpoints}

您可以使用AEM Forms Java API以程式設計方式將「監看資料夾」端點新增至服務。 通過添加「監看資料夾」端點，可讓用戶將檔案(如PDF檔案)放在資料夾中。 將檔案放在資料夾中時，會叫用已設定的服務並處理檔案。 服務執行指定操作後，會將修改的檔案保存在指定的輸出資料夾中。 已設定以固定速率間隔或cron排程（例如每週一、週三和週五中午）掃描受監視的資料夾。

為了以程式設計方式將Watched Folder端點新增至服務，請考慮下列短期程式，名為 *EncryptDocument*. (請參閱 [了解AEM Forms程式](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).)

![aw_aw_encryptdocumentprocess](assets/aw_aw_encryptdocumentprocess.png)

此過程接受不安全的PDF文檔作為輸入值，然後將不安全的PDF文檔傳遞給加密服務的 `EncryptPDFUsingPassword` 操作。 PDF文檔使用密碼加密，而密碼加密的PDF文檔是此過程的輸出值。 輸入值的名稱(不安全的PDF文檔)為 `InDoc` 而資料類型是 `com.adobe.idp.Document`. 輸出值的名稱(密碼加密的PDF文檔)為 `SecuredDoc` 而資料類型是 `com.adobe.idp.Document`.

>[!NOTE]
>
>無法使用Web服務添加「監視的資料夾」端點。

### 步驟摘要 {#summary_of_steps-2}

要將「監看資料夾」端點添加到服務，請執行以下任務：

1. 包含專案檔案。
1. 建立 `EndpointRegistryClient` 物件。
1. 設定「監看資料夾」端點屬性。
1. 指定配置值。
1. 定義輸入參數值。
1. 定義輸出參數值。
1. 建立「監看資料夾」端點。
1. 啟用端點。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss Application Server上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss Application Server上則為必要)

有關這些JAR檔案的位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立EndpointRegistry客戶端對象**

若要以程式設計方式新增「監看資料夾」端點，您必須建立 `EndpointRegistryClient` 物件。

**設定「監看資料夾」端點屬性**

若要為服務建立「監看資料夾」端點，請指定以下值：

* **連接器識別碼**:指定所建立的端點類型。 若要建立「監看資料夾」端點，請指定 `WatchedFolder`.
* **說明**:指定端點的說明。
* **名稱**:指定端點的名稱。
* **服務標識符**:指定端點所屬的服務。 例如，要將「監看資料夾」端點新增至本區段引入的程式（使用Workbench啟動的程式會變成服務），請指定 `EncryptDocument`.
* **操作名稱**:指定使用端點調用的操作的名稱。 通常，為源自於Workbench中建立的程式的服務建立「監看資料夾」端點時，操作的名稱為 `invoke`.

**指定配置值**

以程式設計方式將「監看資料夾」端點新增至服務時，必須指定「監看資料夾」端點的設定值。 如果使用管理控制台添加了「監看資料夾」端點，管理員將指定這些配置值。

以下清單指定當以寫程式方式將Watched Folder端點添加到服務時設定的配置值：

* **url**:指定已監視的資料夾位置。 在群集環境中，此值必須指向可從群集中的每台電腦訪問的共用網路資料夾。
* **非同步**:將調用類型標識為非同步或同步。 只能同步調用瞬態和同步進程。 預設值為true。 建議使用非同步。
* **cronExpression**:由石英用於調度輸入目錄的輪詢。
* **purgeDuration**:這是必填屬性。 結果資料夾中的檔案和資料夾早於此值時將被清除。 此值以天計量。 此屬性有助於確保結果資料夾未滿。 值為–1天表示絕不刪除結果資料夾。 預設值為–1。
* **repeatInterval**:掃描「觀看」資料夾以進行輸入的間隔（秒）。 除非啟用限制，否則此值應比處理平均作業的時間長；否則，系統可能會變得過載。 預設值為 5。
* **repeatCount**:監視的資料夾掃描資料夾或目錄的次數。 值–1表示掃描不確定。 預設值為–1。
* **throttleOn**:限制可在任何指定時間處理的「已監看資料夾」作業數。 作業的最大數量由batchSize值確定。
* **userName**:從「觀看的資料夾」叫用目標服務時使用的使用者名稱。 此值是必填的。 預設值為SuperAdmin。
* **domainName**:使用者的網域。 此值是必填的。 預設值為DefaultDom。
* **batchSize**:每次掃描要提取的檔案或資料夾數。 使用此值來防止系統過載；一次掃描太多檔案可能會導致當機。 預設值為 2。
* **waitTime**:建立後掃描資料夾或檔案之前等待的時間（以毫秒為單位）。 例如，如果等待時間是36,000,000毫秒（一小時），而檔案是在一分鐘前建立的，則此檔案會在59分鐘或更久的時間過後擷取。 此屬性對於確保檔案或資料夾被完全複製到輸入資料夾非常有用。 例如，如果要處理大型檔案，而要下載該檔案需要10分鐘，請將等待時間設定為10&amp;ast;60&amp;ast;1000毫秒。 如果已等待10分鐘，此設定將阻止監視的資料夾掃描該檔案。 預設值為 0。
* **excludeFilePattern**:觀看的資料夾用於確定要掃描和拾取的檔案和資料夾的模式。 系統不會掃描任何具有此模式的檔案或資料夾以進行處理。 當輸入是包含多個檔案的資料夾時，此設定很實用。 資料夾的內容可複製到具有名稱的資料夾中，該名稱將被觀看的資料夾擷取。 此步驟可防止觀看的資料夾在資料夾完全複製到輸入資料夾之前，擷取資料夾以進行處理。 例如，如果excludeFilePattern值為 `data*`，所有符合 `data*` 沒有被接走。 這包括名為的檔案和資料夾 `data1`, `data2`等。 此外，該模式可以用通配符模式來補充，以指定檔案模式。 監看的資料夾會修改規則運算式以支援萬用字元模式，例如 `*.*` 和 `*.pdf`. 規則運算式不支援這些萬用字元模式。
* **includeFilePattern**:觀看的資料夾用來決定要掃描和擷取的資料夾和檔案的模式。 例如，如果此值為 `*`，所有符合 `input*` 被撿起。 這包括名為的檔案和資料夾 `input1`, `input2`等。 預設值為 `*`。此值表示所有檔案和資料夾。 此外，該模式可以用通配符模式來補充，以指定檔案模式。 監看的資料夾會修改規則運算式以支援萬用字元模式，例如 `*.*` 和 `*.pdf`. 規則運算式不支援這些萬用字元模式。 此值是必填的。
* **resultFolderName**:儲儲存存結果的資料夾。 此位置可以是絕對路徑或相對目錄路徑。 如果結果未出現在此資料夾中，請檢查失敗資料夾。 不會處理唯讀檔案，且會儲存在失敗資料夾中。 預設值為 `result/%Y/%M/%D/`。這是監看資料夾內的結果資料夾。
* **preserveFolderName**:成功掃描和拾取檔案後儲存檔案的位置。 此位置可以是絕對、相對或空目錄路徑。 預設值為 `preserve/%Y/%M/%D/`。
* **failureFolderName**:保存故障檔案的資料夾。 此位置一律與已觀看的資料夾相對。 不會處理唯讀檔案，且會儲存在失敗資料夾中。 預設值為 `failure/%Y/%M/%D/`。
* **preserveOnFailure**:如果無法對服務執行操作，則保留輸入檔案。 預設值為true。
* **overwriteDuplicateFilename**:設為true時，會覆寫結果資料夾和保留資料夾中的檔案。 設為false時，名稱會使用具有數值索引尾碼的檔案和資料夾。 預設值為false。

**定義輸入參數值**

建立「監看資料夾」端點時，必須定義輸入參數值。 也就是說，您必須說明傳遞至受監視資料夾叫用之操作的輸入值。 例如，請考量本主題中引入的程式。 它有一個輸入值，名為 `InDoc` 其資料類型 `com.adobe.idp.Document`. 為此程式建立「監看資料夾」端點時（啟動程式後，該端點會變成服務），您必須定義輸入參數值。

要定義「監看資料夾」端點所需的輸入參數值，請指定以下值：

**輸入參數名稱**:輸入參數的名稱。 輸入值的名稱是在Workbench中為流程指定的。 如果輸入值屬於服務操作（不是在Workbench中建立的進程的服務），則輸入名稱在component.xml檔案中指定。 例如，本部分引入的進程的輸入參數的名稱為 `InDoc`.

**對應類型**:用於配置調用服務操作所需的輸入值。 映射類型有兩種：

* `Literal`:「監看資料夾」端點會使用在顯示時輸入欄位的值。 支援所有基本Java類型。 例如，如果API使用String、long、int和Boolean等輸入，則會將字串轉換為適當的類型，並叫用服務。
* `Variable`:輸入的值是檔案模式，監看資料夾用於選擇輸入。 例如，如果為映射類型選擇「變數」，且輸入文檔必須是PDF檔案，則可以指定 `*.pdf`作為對應值。

**對應值**:指定映射類型的值。 例如，若您選取 `Variable` 映射類型，可以指定 `*.pdf` 作為檔案模式。

**資料類型**:指定輸入值的資料類型。 例如，本部分引入的進程輸入值的資料類型為 `com.adobe.idp.Document`.

**定義輸出參數值**

建立「監看資料夾」端點時，必須定義輸出參數值。 也就是說，您必須說明由Watched Folder端點叫用的服務傳回的輸出值。 例如，請考量本主題中引入的程式。 其輸出值名為 `SecuredDoc` 其資料類型 `com.adobe.idp.Document`. 為此程式建立「監看資料夾」端點時（啟動程式後，該端點會變成服務），您必須定義輸出參數值。

要定義「監看資料夾」端點所需的輸出參數值，請指定以下值：

**輸出參數名稱**:輸出參數的名稱。 流程輸出值的名稱在Workbench中指定。 如果輸出值屬於服務操作（不是在Workbench中建立的進程的服務），則輸出名稱在component.xml檔案中指定。 例如，本節中引入的進程的輸出參數的名稱為 `SecuredDoc`.

**對應類型**:用於配置服務和操作的輸出。 可使用下列選項：

* 如果服務返回單個對象（單個文檔），則模式為 `%F.pdf` 而來源目的地為sourcefilename.pdf。 例如，本節中引入的程式會傳回單一檔案。 因此，對應類型可定義為 `%F.pdf` ( `%F` 表示使用指定的檔案名稱)。 模式 `%E` 指定輸入文檔的擴展。
* 如果服務傳回清單，模式為 `Result\%F\`，而源目標為Result\sourcefilename\source1(output 1)和Result\sourcefilename\source2(output 2)。
* 如果服務傳回地圖，模式為 `Result\%F\`，源目標為Result\sourcefilename\file1和Result\sourcefilename\file2。 如果地圖有多個物件，則模式為 `Result\%F.pdf` 而源目標是Result\sourcefilename1.pdf(output 1)、Result\sourcefilenam2.pdf(output 2)等。

**資料類型**:指定傳回值的資料類型。 例如，本節中引入的進程返回值的資料類型為 `com.adobe.idp.Document`.

**建立「監看資料夾」端點**

設定端點的屬性、配置值，並定義輸入和輸出參數值後，必須建立「監看資料夾」端點。

**啟用端點**

建立「監看資料夾」端點後，必須啟用它。 啟用端點時，可用來叫用服務。 啟用端點後，您就可以在管理控制台中檢視它。

**另請參閱**

[使用Java API新增「監看資料夾」端點](programmatically-endpoints.md#add-a-watched-folder-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API新增「監看資料夾」端點 {#add-a-watched-folder-endpoint-using-the-java-api}

使用AEM Forms Java API新增「監看資料夾」端點：

1. 包含專案檔案。

   在您Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-livecycle-client.jar。

1. 建立EndpointRegistry客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EndpointRegistryClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 設定「監看資料夾」端點屬性。

   * 建立 `CreateEndpointInfo` 物件，使用其建構子。
   * 叫用 `CreateEndpointInfo` 物件 `setConnectorId` 方法和傳遞字串值 `WatchedFolder`.
   * 叫用 `CreateEndpointInfo` 物件 `setDescription` 方法，並傳遞描述端點的字串值。
   * 叫用 `CreateEndpointInfo` 物件 `setName` 方法，並傳遞指定名稱的字串值。
   * 通過調用 `CreateEndpointInfo` 物件 `setServiceId` 方法，並傳遞指定服務名稱的字串值。
   * 指定通過調用 `CreateEndpointInfo` 物件 `setOperationName` 方法，並傳遞指定操作名稱的字串值。 通常，為源自於Workbench中建立的程式的服務建立「監看資料夾」端點時，會叫用操作的名稱。

1. 指定配置值。

   對於要為「監看資料夾」端點設定的每個配置值，必須調用 `CreateEndpointInfo` 物件 `setConfigParameterAsText` 方法。 例如，若要設定 `url` 配置值，調用 `CreateEndpointInfo` 物件 `setConfigParameterAsText` 方法，並傳遞下列字串值：

   * 指定配置值名稱的字串值。 設定 `url` 配置值，指定 `url`.
   * 指定配置值的字串值。 設定 `url` 設定值，指定監看的資料夾位置。

   >[!NOTE]
   >
   >要查看為EncryptDocument服務設定的所有配置值，請參閱位於 [快速入門：使用Java API新增「監看資料夾」端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api).

1. 定義輸入參數值。

   叫用 `CreateEndpointInfo` 物件 `setInputParameterMapping` 方法，並傳遞下列值：

   * 指定輸入參數名稱的字串值。 例如，EncryptDocument服務的輸入參數的名稱為 `InDoc`.
   * 一個字串值，它指定輸入參數的資料類型。 例如， `InDoc` 輸入參數為 `com.adobe.idp.Document`.
   * 指定映射類型的字串值。 例如，您可以指定 `variable`.
   * 指定映射類型值的字串值。 例如，可以指定&amp;ast;.pdf作為檔案模式。

   >[!NOTE]
   >
   >叫用 `setInputParameterMapping` 方法來定義每個輸入參數值。 由於EncryptDocument進程只有一個輸入參數，因此您需要調用此方法一次。

1. 定義輸出參數值。

   叫用 `CreateEndpointInfo` 物件 `setOutputParameterMapping` 方法，並傳遞下列值：

   * 指定輸出參數名稱的字串值。 例如，EncryptDocument服務的輸出參數的名稱為 `SecuredDoc`.
   * 一個字串值，它指定輸出參數的資料類型。 例如， `SecuredDoc` 輸出參數為 `com.adobe.idp.Document`.
   * 指定映射類型的字串值。 例如，您可以指定 `%F.pdf`.

1. 建立「監看資料夾」端點。

   叫用 `EndpointRegistryClient` 物件 `createEndpoint` 方法和傳遞 `CreateEndpointInfo` 物件。 此方法會傳回 `Endpoint` 表示「監看資料夾」端點的對象。

1. 啟用端點。

   叫用 `EndpointRegistryClient` 物件 `enable` 方法和傳遞 `Endpoint` 由傳回的物件 `createEndpoint` 方法。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API新增「監看資料夾」端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 監看的資料夾配置值常數檔案 {#watched-folder-configuration-values-constant-file}

此 [快速入門：使用Java API新增「監看資料夾」端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api) 使用必須是Java項目一部分的常數檔案，以編譯快速啟動。 此常數檔案表示在添加「監看資料夾」端點時必須設定的配置值。 以下Java代碼表示常數檔案。

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

您可以使用AEM Forms Java API，以程式設計方式將電子郵件端點新增至服務。 通過添加電子郵件端點，用戶可以向指定的電子郵件帳戶發送包含一個或多個檔案附件的電子郵件。 然後叫用配置服務操作並處理這些檔案。 服務執行指定操作後，會向發送者發送一封電子郵件，其中修改的檔案作為檔案附件。

為了以程式設計方式將電子郵件端點新增至服務，請考慮下列短期程式，名為 *MyApplication\EncryptDocument*. 有關短期流程的資訊，請參見 [了解AEM Forms程式](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).

![ae_ae_encryptdocumentprocess](assets/ae_ae_encryptdocumentprocess.png)

此過程接受不安全的PDF文檔作為輸入值，然後將不安全的PDF文檔傳遞給加密服務的 `EncryptPDFUsingPassword` 操作。 此過程使用密碼加密PDF文檔，並將密碼加密的PDF文檔返回為輸出值。 輸入值的名稱(不安全的PDF文檔)為 `InDoc` 而資料類型是 `com.adobe.idp.Document`. 輸出值的名稱(密碼加密的PDF文檔)為 `SecuredDoc` 而資料類型是 `com.adobe.idp.Document`.

>[!NOTE]
>
>您無法使用Web服務來添加電子郵件端點。

### 步驟摘要 {#summary_of_steps-3}

要向服務添加電子郵件端點，請執行以下任務：

1. 包含專案檔案。
1. 建立 `EndpointRegistryClient` 物件。
1. 設定電子郵件端點屬性。
1. 指定配置值。
1. 定義輸入參數值。
1. 定義輸出參數值。
1. 建立電子郵件端點。
1. 啟用端點。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss Application Server上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss Application Server上則為必要)

有關這些JAR檔案的位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立EndpointRegistry客戶端對象**

您必須先建立 `EndpointRegistryClient` 物件。

**設定電子郵件端點屬性**

若要為服務建立電子郵件端點，請指定下列值：

* **連接器識別碼值**:指定所建立的端點類型。 若要建立電子郵件端點，請指定 `Email`.
* **說明**:指定端點的說明。
* **名稱**:指定端點的名稱。
* **服務標識符值**:指定端點所屬的服務。 例如，若要將「電子郵件」端點新增至本區段引入的程式（使用Workbench啟動的程式會變成服務），請指定 `EncryptDocument`.
* **操作名稱**:指定使用端點調用的操作的名稱。 通常，為源自於Workbench中建立之程式的服務建立電子郵件端點時，操作的名稱為 `invoke`.

**指定配置值**

以程式設計方式將電子郵件端點新增至服務時，您必須指定電子郵件端點的設定值。 如果使用管理控制台新增電子郵件端點，管理員會指定這些設定值。

>[!NOTE]
>
>受監控的電子郵件帳戶是僅用於電子郵件端點的特殊帳戶。 此帳戶不是一般使用者的電子郵件帳戶。 常規用戶的電子郵件帳戶不能配置為電子郵件提供程式使用的帳戶，因為電子郵件提供程式在郵件完成後會從收件箱中刪除電子郵件郵件。

以程式設計方式將電子郵件端點新增至服務時，會設定下列設定值：

* **cronExpression**:cron運算式（如果必須使用cron運算式排程電子郵件）。
* **repeatCount**:電子郵件端點掃描資料夾或目錄的次數。 值–1表示掃描不確定。 預設值為–1。
* **repeatInterval**:接收者用於檢查傳入郵件的掃描速率（以秒為單位）。 預設值為 10。
* **startDelay**:排程器啟動後等待掃描的時間。 預設時間為0。
* **batchSize**:接收者在每次掃描時處理的電子郵件訊息數量，以獲得最佳效能。 值–1表示所有電子郵件。 預設值為 2。
* **userName**:從電子郵件叫用目標服務時使用的使用者名稱。 預設值為 `SuperAdmin`。
* **domainName**:強制設定值。 預設值為 `DefaultDom`。
* **domainPattern**:指定提供程式接受的傳入電子郵件的域模式。 例如，若 `adobe.com` 時，只會處理adobe.com的電子郵件，忽略其他網域的電子郵件。
* **filePattern**:指定提供程式接受的傳入檔案附件模式。 這包括具有特定檔案名副檔名(&amp;ast;.dat、&amp;ast;.xml)的檔案、具有特定名稱（資料）的檔案，以及在名稱和副檔名(&amp;ast;)中具有複合運算式的檔案。[dD][aA]&#39;port&#39;)。 預設值為 `*`。
* **recipientSuccessfulJob**:傳送訊息以指出成功作業的電子郵件地址。 預設情況下，成功的作業消息始終發送給發件人。 如果您輸入 `sender`，則會將電子郵件結果傳送給寄件者。 最多支援100個收件者。 使用電子郵件地址指定其他收件者，每個收件者以逗號分隔。 若要關閉此選項，請將此值留空。 在某些情況下，您可能會想要觸發程式，而不想要結果的電子郵件通知。 預設值為 `sender`。
* **recipientFailedJob**:發送郵件以指示失敗作業的電子郵件地址。 預設情況下，將始終向發件人發送失敗的作業消息。 如果您輸入 `sender`，則會將電子郵件結果傳送給寄件者。 最多支援100個收件者。 使用電子郵件地址指定其他收件者，每個收件者以逗號分隔。 若要關閉此選項，請將此值留空。 預設值為 `sender`。
* **inboxHost**:要掃描的電子郵件提供程式的收件箱主機名或IP地址。
* **inboxPort**:電子郵件伺服器使用的埠。 POP3的預設值為110,IMAP的預設值為143。 如果啟用了SSL，則POP3的預設值為995，而IMAP的預設值為993。
* **inboxProtocol**:用於掃描收件箱的電子郵件端點的電子郵件協定。 選項包括 `IMAP` 或 `POP3`. 收件箱主機郵件伺服器必須支援這些協定。
* **inboxTimeOut**:電子郵件提供者等待收件匣回應的逾時（秒）。 預設值為 60。
* **inboxUser**:登入電子郵件帳戶所需的使用者名稱。 視電子郵件伺服器和設定而定，這可能只是電子郵件的使用者名稱部分，或可能是完整的電子郵件地址。
* **inboxPassword**:收件匣使用者的密碼。
* **inboxSSLEnabled**:設定此值可在傳送結果或錯誤的通知訊息時，強制電子郵件提供者使用SSL。 確保IMAP或POP3主機支援SSL。
* **smtpHost**:電子郵件提供程式向其發送結果和錯誤消息的郵件伺服器的主機名。
* **smtpPort**:SMTP埠的預設值為25。
* **smtpUser**:電子郵件提供者在傳送結果和錯誤的電子郵件通知時要使用的使用者帳戶。
* **smtpPassword**:SMTP帳戶的密碼。 某些郵件伺服器不需要SMTP密碼。
* **charSet**:電子郵件提供者使用的字元集。 預設值為 `UTF-8`。
* **smtpSSLEnabled**:設定此值可在傳送結果或錯誤的通知訊息時，強制電子郵件提供者使用SSL。 確保SMTP主機支援SSL。
* **failedJobFolder**:指定在SMTP郵件伺服器不運行時要儲存結果的目錄。
* **非同步**:設為同步時，會處理所有輸入檔案並傳回單一回應。 設為非同步時，會針對每個處理的輸入檔案傳送回應。 例如，會為本主題中引入的流程建立電子郵件端點，並向端點的收件匣發送電子郵件，該收件匣包含多個不安全的PDF檔案。 當所有PDF文檔都使用密碼加密，並且終結點配置為同步時，將發送一條響應電子郵件消息並附加所有安全PDF文檔。 如果將端點配置為非同步，則為每個安全PDF文檔發送單獨的響應電子郵件消息。 每則電子郵件包含作為附件的單一PDF檔案。 預設值為非同步。

**定義輸入參數值**

建立電子郵件端點時，您必須定義輸入參數值。 也就是說，您必須說明傳遞至由電子郵件端點叫用之操作的輸入值。 例如，請考量本主題中引入的程式。 它有一個輸入值，名為 `InDoc` 其資料類型 `com.adobe.idp.Document`. 為此流程建立電子郵件端點時（在啟動流程後，它會變成服務），您必須定義輸入參數值。

要定義「電子郵件」端點所需的輸入參數值，請指定以下值：

**輸入參數名稱**:輸入參數的名稱。 輸入值的名稱是在Workbench中為流程指定的。 如果輸入值屬於服務操作(不是在Workbench中建立的進程的Forms服務)，則輸入名稱在component.xml檔案中指定。 例如，本部分引入的進程的輸入參數的名稱為 `InDoc`.

**對應類型**:用於配置調用服務操作所需的輸入值。 兩種映射類型如下：

* `Literal`:電子郵件端點會使用在欄位中輸入的值，以顯示它。 支援所有基本Java類型。 例如，如果API使用String、long、int和Boolean等輸入，則字串會轉換為適當的類型，並叫用服務。
* `Variable`:輸入的值是電子郵件端點用於選擇輸入的檔案模式。 例如，如果為映射類型選擇「變數」，且輸入文檔必須是PDF檔案，則可以指定 `*.pdf` 作為對應值。

**對應值**:指定映射類型的值。 例如，若您選取「變數」對應類型，可指定 `*.pdf` 作為檔案模式。

**資料類型**:指定輸入值的資料類型。 例如，本節中引入之程式輸入值的資料類型為com.adobe.idp.Document。

**定義輸出參數值**

建立電子郵件端點時，您必須定義輸出參數值。 也就是說，您必須說明由電子郵件端點叫用的服務所傳回的輸出值。 例如，請考量本主題中引入的程式。 其輸出值名為 `SecuredDoc` 其資料類型 `com.adobe.idp.Document`. 為此流程建立電子郵件端點時（在啟動流程後，它會變成服務），您必須定義輸出參數值。

要定義「電子郵件」端點所需的輸出參數值，請指定以下值：

**輸出參數名稱**:輸出參數的名稱。 流程輸出值的名稱在Workbench中指定。 如果輸出值屬於服務操作（不是在Workbench中建立的進程的服務），則輸出名稱在component.xml檔案中指定。 例如，本節中引入的進程的輸出參數的名稱為 `SecuredDoc`.

**對應類型**:用於配置服務和操作的輸出。 可使用下列選項：

* 如果服務返回單個對象（單個文檔），則模式為 `%F.pdf` 而來源目的地為sourcefilename.pdf。 例如，本節中引入的程式會傳回單一檔案。 因此，對應類型可定義為 `%F.pdf` ( `%F` 表示使用指定的檔案名稱)。 模式 `%E` 指定輸入文檔的擴展。
* 如果服務傳回清單，模式為 `Result\%F\`，而源目標為Result\sourcefilename\source1(output 1)和Result\sourcefilename\source2(output 2)。
* 如果服務傳回地圖，模式為 `Result\%F\`，源目標為Result\sourcefilename\file1和Result\sourcefilename\file2。 如果地圖有多個物件，則模式為 `Result\%F.pdf` 而源目標是Result\sourcefilename1.pdf(output 1)、Result\sourcefilenam2.pdf(output 2)等。

**資料類型**:指定傳回值的資料類型。 例如，本節中引入的進程返回值的資料類型為 `com.adobe.idp.Document`.

**建立電子郵件端點**

設定電子郵件端點屬性和設定值，並定義輸入和輸出參數值後，您必須建立電子郵件端點。

**啟用端點**

建立電子郵件端點後，您必須啟用它。 啟用端點時，可用來叫用服務。 啟用端點後，您就可以在管理控制台中檢視它。

**另請參閱**

[使用Java API新增電子郵件端點](programmatically-endpoints.md#add-an-email-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API新增電子郵件端點 {#add-an-email-endpoint-using-the-java-api}

使用Java API新增電子郵件端點：

1. 包含專案檔案。

   在您Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-livecycle-client.jar。

1. 建立EndpointRegistry客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EndpointRegistryClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 設定電子郵件端點屬性。

   * 建立 `CreateEndpointInfo` 物件，使用其建構子。
   * 叫用 `CreateEndpointInfo` 物件 `setConnectorId` 方法和傳遞字串值 `Email`.
   * 叫用 `CreateEndpointInfo` 物件 `setDescription` 方法，並傳遞描述端點的字串值。
   * 叫用 `CreateEndpointInfo` 物件 `setName` 方法，並傳遞指定名稱的字串值。
   * 通過調用 `CreateEndpointInfo` 物件 `setServiceId` 方法，並傳遞指定服務名稱的字串值。
   * 指定通過調用 `CreateEndpointInfo` 物件 `setOperationName` 方法，並傳遞指定操作名稱的字串值。 通常，為源自於Workbench中建立之程式的服務建立電子郵件端點時，會叫用操作的名稱。

1. 指定配置值。

   對於要為電子郵件端點設定的每個配置值，必須調用 `CreateEndpointInfo` 物件 `setConfigParameterAsText` 方法。 例如，若要設定 `smtpHost` 配置值，調用 `CreateEndpointInfo` 物件 `setConfigParameterAsText` 方法，並傳遞下列值：

   * 指定配置值名稱的字串值。 設定 `smtpHost` 配置值，指定 `smtpHost`.
   * 指定配置值的字串值。 設定 `smtpHost` 配置值，指定指定SMTP伺服器名稱的字串值。

   >[!NOTE]
   >
   >若要查看本節中引入的EncryptDocument服務所設定的所有配置值，請參閱位於 [快速入門：使用Java API新增電子郵件端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api).

1. 定義輸入參數值。

   叫用 `CreateEndpointInfo` 物件 `setInputParameterMapping` 方法，並傳遞下列值：

   * 指定輸入參數名稱的字串值。 例如，EncryptDocument服務的輸入參數的名稱為 `InDoc`.
   * 一個字串值，它指定輸入參數的資料類型。 例如， `InDoc` 輸入參數為 `com.adobe.idp.Document`.
   * 指定映射類型的字串值。 例如，您可以指定 `variable`.
   * 指定映射類型值的字串值。 例如，可以指定&amp;ast;.pdf作為檔案模式。

   >[!NOTE]
   >
   >叫用 `setInputParameterMapping` 方法來定義每個輸入參數值。 由於EncryptDocument進程只有一個輸入參數，因此您需要調用此方法一次。

1. 定義輸出參數值。

   叫用 `CreateEndpointInfo` 物件 `setOutputParameterMapping` 方法並傳遞下列值：

   * 指定輸出參數名稱的字串值。 例如，EncryptDocument服務的輸出參數的名稱為 `SecuredDoc`.
   * 一個字串值，它指定輸出參數的資料類型。 例如， `SecuredDoc` 輸出參數為 `com.adobe.idp.Document`.
   * 指定映射類型的字串值。 例如，您可以指定 `%F.pdf`.

1. 建立電子郵件端點。

   叫用 `EndpointRegistryClient` 物件 `createEndpoint` 方法和傳遞 `CreateEndpointInfo` 物件。 此方法會傳回 `Endpoint` 代表電子郵件端點的物件。

1. 啟用端點。

   叫用 `EndpointRegistryClient` 物件 `enable` 方法和傳遞 `Endpoint` 由傳回的物件 `createEndpoint` 方法。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API新增「監看資料夾」端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 電子郵件配置值常數檔案 {#email-configuration-values-constant-file}

此 [快速入門：使用Java API新增電子郵件端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api) 使用必須是Java項目一部分的常數檔案，以編譯快速啟動。 此常數檔案代表新增電子郵件端點時必須設定的設定值。 以下Java代碼表示常數檔案。

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
>LiveCycle RemotingAPI已於JEE上淘汰的AEM表單。

您可以使用AEM Forms Java API，以程式設計方式將Remoting端點新增至服務。 通過添加Remoting端點，可使Flex應用程式通過使用Remoting調用服務。 (請參閱 [使用叫用AEM Forms(AEM表單已淘汰)AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

為了以寫程式方式將Remoting端點添加到服務中，請考慮以下短期進程，名為 *EncryptDocument*.

![ar_ar_encryptdocumentprocess](assets/ar_ar_encryptdocumentprocess.png)

此過程接受不安全的PDF文檔作為輸入值，然後將不安全的PDF文檔傳遞給加密服務的 `EncryptPDFUsingPassword` 操作。 PDF文檔使用密碼加密，而密碼加密的PDF文檔是此過程的輸出值。 輸入值的名稱(不安全的PDF文檔)為 `InDoc` 而資料類型是 `com.adobe.idp.Document`. 輸出值的名稱(密碼加密的PDF文檔)為 `SecuredDoc` 而資料類型是 `com.adobe.idp.Document`.

為了演示如何將Remoteing端點添加到服務，本節將Remoteing端點添加到名為EncryptDocument的服務。

>[!NOTE]
>
>不能使用Web服務添加Remoting端點。

### 步驟摘要 {#summary_of_steps-4}

要從服務中刪除端點，請執行以下任務：

1. 包含專案檔案。
1. 建立 `EndpointRegistryClient` 物件。
1. 設定Remoting端點屬性。
1. 建立遠程端點。
1. 啟用端點。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss Application Server上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss Application Server上則為必要)

有關這些JAR檔案的位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立EndpointRegistry客戶端對象**

要以寫程式方式添加Remoting端點，必須建立 `EndpointRegistryClient` 物件。

**設定遠程處理終結點屬性**

要為服務建立遠程端點，請指定以下值：

* **連接器識別碼值**:指定所建立的端點類型。 要建立遠程端點，請指定 `Remoting`.
* **說明**:指定端點的說明。
* **名稱**:指定端點的名稱。
* **服務標識符值**:指定端點所屬的服務。 例如，若要將遠端端點新增至本區段中引入的程式（在Workbench內啟動程式時，程式就會變成服務），請指定 `EncryptDocument`.
* **操作名稱**:指定使用端點調用的操作的名稱。 建立遠程終結點時，請指定通配符(&amp;ast;)。

**建立遠程端點**

設定Remoting端點屬性後，可以為服務建立Remoting端點。

**啟用端點**

建立新端點後，必須啟用它。 啟用Remoting端點時，會啟用Flex用戶端叫用服務。

**另請參閱**

[使用Java API新增遠端端點](programmatically-endpoints.md#add-a-remoting-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API新增遠端端點 {#add-a-remoting-endpoint-using-the-java-api}

使用Java API新增遠端端點：

1. 包含專案檔案。

   在您Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-livecycle-client.jar。

1. 建立EndpointRegistry客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EndpointRegistryClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 設定Remoting端點屬性。

   * 建立 `CreateEndpointInfo` 物件，使用其建構子。
   * 叫用 `CreateEndpointInfo` 物件 `setConnectorId` 方法和傳遞字串值 `Remoting`.
   * 叫用 `CreateEndpointInfo` 物件 `setDescription` 方法，並傳遞描述端點的字串值。
   * 叫用 `CreateEndpointInfo` 物件 `setName` 方法，並傳遞指定名稱的字串值。
   * 通過調用 `CreateEndpointInfo` 物件 `setServiceId` 方法，並傳遞指定服務名稱的字串值。
   * 指定由 `CreateEndpointInfo` 物件 `setOperationName` 方法，並傳遞指定操作名稱的字串值。 對於「遠程」端點，指定通配符(&amp;ast;)。

1. 建立遠程端點。

   叫用 `EndpointRegistryClient` 物件 `createEndpoint` 方法和傳遞 `CreateEndpointInfo` 物件。 此方法會傳回 `Endpoint` 表示新Remoting端點的對象。

1. 啟用端點。

   叫用 `EndpointRegistryClient` 物件 `enable` 方法和傳遞 `Endpoint` 由傳回的物件 `createEndpoint` 方法。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API新增遠端端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-remoting-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 添加TaskManager端點 {#adding-taskmanager-endpoints}

您可以使用AEM Forms Java API以程式設計方式將TaskManager端點新增至服務。 通過將TaskManager端點添加到服務，可使Workspace用戶調用該服務。 也就是說，在工作區中工作的用戶可以調用具有相應TaskManager終結點的進程。

>[!NOTE]
>
>不能使用Web服務添加TaskManager終結點。

### 步驟摘要 {#summary_of_steps-5}

要將TaskManager端點添加到服務，請執行以下任務：

1. 包含專案檔案。
1. 建立 `EndpointRegistryClient` 物件。
1. 為端點建立類別。
1. 設定TaskManager終結點屬性。
1. 建立TaskManager終結點。
1. 啟用端點。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss Application Server上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss Application Server上則為必要)

有關這些JAR檔案的位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立EndpointRegistry客戶端對象**

在以寫程式方式添加TaskManager端點之前，必須先建立 `EndpointRegistryClient` 物件。

**為端點建立類別**

類別可用來組織工作區中的服務。 也就是說，工作區用戶可以通過在工作區中選擇類別來調用具有TaskManager端點的服務。 建立TaskManager端點時，可以參照現有類別或以寫程式方式建立新類別。

>[!NOTE]
>
>此部分將建立新類別，作為向服務添加TaskManager終結點的一部分。

**設定TaskManager終結點屬性**

要為服務建立TaskManager端點，請指定以下值：

* **連接器識別碼**:指定所建立的端點類型。 要建立TaskManager端點，請指定 `TaskManagerConnector`.
* **說明**:指定端點的說明。
* **名稱**:指定端點的名稱。
* **服務標識符**:指定端點所屬的服務。
* **類別**:指定與TaskManager終結點關聯的類別標識符值。
* **操作名稱**:通常，在為源自於Workbench中建立的流程的服務建立TaskManager端點時，操作的名稱為 `invoke`.

**建立TaskManager終結點**

設定TaskManager終結點屬性後，可以為服務建立TaskManager終結點。

**啟用端點**

建立新端點後，必須啟用它。 啟用端點時，可用來從工作區內叫用服務。 啟用端點後，您就可以在管理控制台中檢視它。

**另請參閱**

[使用Java API添加TaskManager終結點](programmatically-endpoints.md#add-a-taskmanager-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加TaskManager終結點 {#add-a-taskmanager-endpoint-using-the-java-api}

使用Java API添加TaskManager終結點：

1. 包含專案檔案。

   在您Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-livecycle-client.jar。

1. 建立EndpointRegistry客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EndpointRegistryClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 為端點建立類別。

   * 建立 `CreateEndpointCategoryInfo` 物件，方法是使用其建構子並傳遞下列值：

      * 指定類別標識符值的字串值
      * 指定類別說明的字串值
   * 叫用 `EndpointRegistryClient` 物件 `createEndpointCategory` 方法和傳遞 `CreateEndpointCategoryInfo` 物件。 此方法會傳回 `EndpointCategory` 代表新類別的物件。


1. 設定TaskManager終結點屬性。

   * 建立 `CreateEndpointInfo` 物件，使用其建構子。
   * 叫用 `CreateEndpointInfo` 物件 `setConnectorId` 方法和傳遞字串值 `TaskManagerConnector`.
   * 叫用 `CreateEndpointInfo` 物件 `setDescription` 方法，並傳遞描述端點的字串值。
   * 叫用 `CreateEndpointInfo` 物件 `setName` 方法，並傳遞指定名稱的字串值。
   * 通過調用 `CreateEndpointInfo` 物件 `setServiceId` 方法，並傳遞指定服務名稱的字串值。
   * 通過調用 `CreateEndpointInfo` 物件 `setCategoryId` 方法，並傳遞指定類別識別碼值的字串值。 您可以叫用 `EndpointCategory` 物件 `getId` 方法來取得此類別的識別碼值。
   * 指定通過調用 `CreateEndpointInfo` 物件 `setOperationName` 方法，並傳遞指定操作名稱的字串值。 通常，在建立 `TaskManager` 源自於在Workbench中建立的程式的服務端點，操作的名稱為 `invoke`.

1. 建立TaskManager終結點。

   叫用 `EndpointRegistryClient` 物件 `createEndpoint` 方法和傳遞 `CreateEndpointInfo` 物件。 此方法會傳回 `Endpoint` 表示新TaskManager端點的對象。

1. 啟用端點。

   叫用 `EndpointRegistryClient` 物件 `enable` 方法和傳遞 `Endpoint` 由傳回的物件 `createEndpoint` 方法。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API添加TaskManager終結點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-taskmanager-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 修改端點 {#modifying-endpoints}

您可以使用AEM Forms Java API以程式設計方式修改現有端點。 通過修改端點，可以更改端點的行為。 例如，假設「監看資料夾」端點指定用作監看資料夾的資料夾。 您可以用程式設計方式修改屬於「監看資料夾」端點的設定值，使另一個資料夾可作為監看資料夾運作。 如需屬於「監看資料夾」端點之設定值的相關資訊，請參閱 [添加監視的資料夾端點](programmatically-endpoints.md#adding-watched-folder-endpoints).

為了演示如何修改端點，本節通過更改行為與監視資料夾相同的資料夾來修改監視資料夾端點。

>[!NOTE]
>
>不能使用Web服務修改端點。

### 步驟摘要 {#summary_of_steps-6}

要修改端點，請執行以下任務：

1. 包含專案檔案。
1. 建立 `EndpointRegistryClient` 物件。
1. 擷取端點。
1. 指定新的配置值。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss Application Server上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss Application Server上則為必要)

有關這些JAR檔案的位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立EndpointRegistry客戶端對象**

要以寫程式方式修改端點，必須建立 `EndpointRegistryClient` 物件。

**檢索要修改的端點**

必須先檢索終結點，才能修改它。 若要擷取端點，您必須以可存取端點的使用者身分連線。 建議您以管理員身分連線。 (請參閱 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties))。

通過檢索端點清單可以檢索端點。 然後，您可以逐一查看清單，搜尋要移除的特定端點。 例如，您可以判斷與端點對應的服務和端點類型，以找出端點。 找到端點時，可以修改它。

**指定新配置值**

修改端點時，請指定新的配置值。 例如，要修改「監看資料夾」端點，請重置所有「監看資料夾」端點配置值，而不只是要修改的值。 如需屬於「監看資料夾」端點之設定值的相關資訊，請參閱 [添加監視的資料夾端點](programmatically-endpoints.md#adding-watched-folder-endpoints).

>[!NOTE]
>
>如需屬於電子郵件端點之設定值的相關資訊，請參閱 [新增電子郵件端點](programmatically-endpoints.md#adding-email-endpoints).

>[!NOTE]
>
>您無法修改端點叫用的服務。 如果嘗試修改服務，則會引發異常。 要修改與給定端點關聯的服務，請刪除該端點並建立新端點。 (請參閱 [移除端點](programmatically-endpoints.md#removing-endpoints).)

**另請參閱**

[使用Java API修改端點](programmatically-endpoints.md#modifying-an-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API修改端點 {#modifying-an-endpoint-using-the-java-api}

使用Java API修改端點：

1. 包含專案檔案。

   在您Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-livecycle-client.jar。

1. 建立EndpointRegistry客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EndpointRegistryClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 檢索要修改的端點。

   * 通過調用 `EndpointRegistryClient` 物件 `getEndpoints` 方法和傳遞 `PagingFilter` 用作篩選器的對象。 您可以傳遞 `(PagingFilter)null` 值以傳回所有端點。 此方法會傳回 `java.util.List` 其中每個元素都是 `Endpoint` 物件。 如需 `PagingFilter` 對象，請參見 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * 重複 `java.util.List` 物件，以判斷其是否具有端點。 如果端點存在，則每個元素都是 `EndPoint` 例項。
   * 通過調用 `EndPoint` 物件 `getServiceId` 方法。 此方法會傳回指定服務名稱的字串值。
   * 叫用 `EndPoint` 物件 `getConnectorId` 方法。 此方法會傳回指定端點類型的字串值。 例如，如果端點是「監看資料夾」端點，則此方法會傳回 `WatchedFolder`.

1. 指定新的配置值。

   * 建立 `ModifyEndpointInfo` 對象，方法是調用其建構子。
   * 對於要設定的每個設定值，叫用 `ModifyEndpointInfo` 物件 `setConfigParameterAsText` 方法。 例如，若要設定url設定值，請叫用 `ModifyEndpointInfo` 物件 `setConfigParameterAsText` 方法，並傳遞下列值：

      * 指定配置值名稱的字串值。 例如，若要設定 `url` 配置值，指定 `url`.
      * 指定配置值的字串值。 若要定義 `url` 設定值，指定監看的資料夾位置。
   * 叫用 `EndpointRegistryClient` 物件 `modifyEndpoint` 方法並傳遞 `ModifyEndpointInfo` 物件。


**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API修改端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-modifying-an-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 移除端點 {#removing-endpoints}

您可以使用AEM Forms Java API以程式設計方式從服務中移除端點。 移除端點後，無法使用端點啟用的叫用方法叫用服務。 例如，如果從服務中刪除SOAP端點，則無法使用SOAP模式調用服務。

要演示如何從服務中刪除終結點，此部分將從名為的服務中刪除EJB終結點 *EncryptDocument*.

>[!NOTE]
>
>不能使用Web服務刪除終結點。

### 步驟摘要 {#summary_of_steps-7}

要從服務中刪除端點，請執行以下任務：

1. 包含專案檔案。
1. 建立 `EndpointRegistryClient` 物件。
1. 擷取端點。
1. 移除端點。

**包含項目檔案**

將必要的檔案納入您的開發專案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss Application Server上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss Application Server上則為必要)

有關這些JAR檔案的位置的資訊，請參見 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立EndpointRegistry客戶端對象**

要以寫程式方式刪除端點，必須建立 `EndpointRegistryClient` 物件。

**檢索要刪除的端點**

必須先檢索終結點，才能刪除它。 若要擷取端點，您必須以可存取端點的使用者身分連線。 建議您以管理員身分連線。 (請參閱 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties))。

通過檢索端點清單可以檢索端點。 然後，您可以逐一查看清單，搜尋要移除的特定端點。 例如，您可以判斷與端點對應的服務和端點類型，以找出端點。 找到端點後，可將其移除。

**移除端點**

建立新端點後，必須啟用它。 啟用端點時，可用來叫用服務。 啟用端點後，您就可以在管理控制台中檢視它。

**另請參閱**

[使用Java API移除端點](programmatically-endpoints.md#removing-an-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API移除端點 {#removing-an-endpoint-using-the-java-api}

使用Java API移除端點：

1. 包含專案檔案。

   在您Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-livecycle-client.jar。

1. 建立EndpointRegistry客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EndpointRegistryClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 檢索要刪除的端點。

   * 通過調用 `EndpointRegistryClient` 物件 `getEndpoints` 方法和傳遞 `PagingFilter` 用作篩選器的對象。 你可以通過 `(PagingFilter)null` 返回所有端點。 此方法會傳回 `java.util.List` 其中每個元素都是 `Endpoint` 物件。
   * 重複 `java.util.List` 物件，以判斷其是否具有端點。 如果端點存在，則每個元素都是 `EndPoint` 例項。
   * 通過調用 `EndPoint` 物件 `getServiceId` 方法。 此方法會傳回指定服務名稱的字串值。
   * 叫用 `EndPoint` 物件 `getConnectorId` 方法。 此方法會傳回指定端點類型的字串值。 例如，如果終結點是EJB終結點，則此方法將返回 `EJB`.

1. 移除端點。

   叫用 `EndpointRegistryClient` 物件 `remove` 方法和傳遞 `EndPoint` 代表要移除之端點的物件。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API移除端點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-removing-an-endpoint-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 檢索端點連接器資訊 {#retrieving-endpoint-connector-information}

您可以使用AEM Forms API以程式設計方式擷取端點連接器的相關資訊。 連接器使端點能夠使用各種調用方法調用服務。 例如，「觀看資料夾」連接器可讓端點使用觀看資料夾叫用服務。 通過以寫程式方式檢索關於端點連接器的資訊，您可以檢索與連接器關聯的配置值，如需要哪些配置值以及哪些配置值是可選的。

為了示範如何擷取端點連接器的相關資訊，本區段會擷取關於「已觀看資料夾」連接器的資訊。 (請參閱 [添加監視的資料夾端點](programmatically-endpoints.md#adding-watched-folder-endpoints).)

>[!NOTE]
>
>您無法使用Web服務檢索有關端點的資訊。

>[!NOTE]
>
>本主題使用 `ConnectorRegistryClient` API以擷取端點連接器的相關資訊。 (請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

### 步驟摘要 {#summary_of_steps-8}

要檢索端點連接器資訊，請執行以下任務：

1. 包含專案檔案。
1. 建立 `ConnectorRegistryClient` 物件。
1. 指定連接器類型。
1. 擷取設定值。

**包含項目檔案**

將必要的檔案納入您的開發專案。 如果您是使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請務必包含Proxy檔案。

必須將以下JAR檔案添加到項目的類路徑中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(若AEM Forms部署在JBoss Application Server上則為必要)
* jbossall-client.jar(若AEM Forms部署在JBoss Application Server上則為必要)

如果AEM Forms部署在非JBoss的支援J2EE應用程式伺服器上，則請以部署AEM Forms的J2EE應用程式伺服器專屬的JAR檔案取代adobe-utilities.jar和jbossall-client.jar。 如需所有AEM Forms JAR檔案位置的相關資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立ConnectorRegistry客戶端對象**

要以寫程式方式檢索端點連接器資訊，請建立 `ConnectorRegistryClient` 物件。

**指定連接器類型**

指定要從中檢索資訊的連接器類型。 連接器類型如下：

* **EJB**:使客戶端應用程式能夠使用EJB模式調用服務。
* **SOAP**:使客戶端應用程式能夠使用SOAP模式調用服務。
* **監看資料夾**:啟用受監視的資料夾以調用服務。
* **電子郵件**:啟用電子郵件以調用服務。
* **遠端**:啟用Flex用戶端應用程式以叫用服務。
* **TaskManagerConnector**:允許工作區使用者從工作區內叫用服務。

**擷取設定值**

指定連接器類型後，可以檢索有關連接器的資訊，如支援的配置值。 例如，對於任何連接器，您可以決定需要哪些配置值，以及哪些配置值是可選的。

**另請參閱**

[使用Java API擷取端點連接器資訊](programmatically-endpoints.md#retrieve-endpoint-connector-information-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API擷取端點連接器資訊 {#retrieve-endpoint-connector-information-using-the-java-api}

使用Java API檢索端點連接器資訊：

1. 包含專案檔案。.

   在您Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-livecycle-client.jar。

1. 建立ConnectorRegistry客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `ConnectorRegistryClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 指定連接器類型。

   叫用 `ConnectorRegistryClient` 物件 `getEndpointDefinition` 方法，並傳遞指定連接器類型的字串值。 例如，若要指定「監看資料夾」連接器類型，請傳遞字串值 `WatchedFolder`. 此方法會傳回 `Endpoint` 與連接器類型對應的物件。

1. 擷取設定值。

   * 通過調用 `Endpoint` 物件 `getConfigParameters` 方法。 此方法會傳回陣列 `ConfigParameter` 對象。
   * 擷取陣列內的每個元素，以擷取關於每個設定值的資訊。 每個元素都是 `ConfigParameter` 物件。 例如，您可以借由叫用 `ConfigParameter` 物件 `isRequired` 方法。 如果需要設定值，則此方法會傳回 `true`.

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速入門：使用Java API擷取端點連接器資訊](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-retrieving-endpoint-connector-information-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
