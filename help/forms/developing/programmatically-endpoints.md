---
title: 以寫程式方式管理端點
seo-title: Programmatically Managing Endpoints
description: 使用終結點註冊表服務添加EJB終結點、添加SOAP終結點、添加監視資料夾終結點、添加電子郵件終結點、添加遠程處理終結點、添加任務管理器終結點、修改終結點、刪除終結點和檢索終結點連接器資訊。
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

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

**關於Endpoint Registry服務**

Endpoint Registry服務提供了以寫程式方式管理端點的功能。 例如，可以向服務添加以下類型的端點：

* EJB
* SOAP
* 監視資料夾
* 電子郵件
* (不建議AEM用於表單)遠程處理
* 任務管理器

>[!NOTE]
>
>SOAP、EJB和(JEE上的表AEM單已棄用)遠程處理終結點將自動為每個激活的服務建立。 SOAP和EJB終結點為所有服務操作啟用SOAP和EJB。

遠程處理終結點使Flex客戶端能夠調用該終結點添加到的AEM Forms服務上的操作。 建立與終結點同名的Flex目標，Flex客戶端可以建立指向此目標以調用相關服務上的操作的RemoteObjects。

電子郵件、任務管理器和監視資料夾終結點僅公開服務的特定操作。 添加這些端點需要第二個配置步驟來選擇要調用、設定配置參數以及指定輸入和輸出參數映射的方法。

可以將TaskManager端點組織成名為 *類別*。 然後，這些類別通過TaskManager公開給Workspace，最終用戶將按照TaskManager端點的分類查看它們。 在Workspace中，最終用戶可以在導航窗格中看到這些類別。 每個類別中的端點將作為進程卡顯示在Workspace的「啟動進程」(Start Processes)頁上。

可以使用端點註冊表服務完成以下任務：

* 添加EJB終結點。 (請參閱 [添加EJB終結點](programmatically-endpoints.md#adding-ejb-endpoints)。)
* 添加SOAP終結點。 (請參閱 [添加SOAP終結點](programmatically-endpoints.md#adding-soap-endpoints)。)
* 添加監視的資料夾終結點(請參閱 [添加監視的資料夾終結點](programmatically-endpoints.md#adding-watched-folder-endpoints)。)
* 添加電子郵件終結點。 (請參閱 [添加電子郵件終結點](programmatically-endpoints.md#adding-email-endpoints)。)
* 添加遠程處理終結點。 (請參閱 [添加遠程處理終結點](programmatically-endpoints.md#adding-remoting-endpoints)。)
* 添加TaskManager終結點(請參閱 [添加TaskManager終結點](programmatically-endpoints.md#adding-taskmanager-endpoints)。)
* 修改端點(請參閱 [修改端點](programmatically-endpoints.md#modifying-endpoints)。)
* 刪除端點(請參閱 [刪除端點](programmatically-endpoints.md#removing-endpoints)。)
* 檢索端點連接器資訊(請參閱 [檢索端點連接器資訊](programmatically-endpoints.md#retrieving-endpoint-connector-information)。)

## 添加EJB終結點 {#adding-ejb-endpoints}

可以使用AEM FormsJava API以寫程式方式將EJB端點添加到服務。 通過將EJB終結點添加到服務中，即使使用EJB模式，也使客戶端應用程式能夠調用服務。 即，在設定調用AEM Forms所需的連接屬性時，可以選擇EJB模式。 (請參閱 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)

>[!NOTE]
>
>不能使用Web服務添加EJB終結點。

>[!NOTE]
>
>通常，預設情況下會將EJB終結點添加到服務中，但是，可以將EJB終結點添加到以寫程式方式部署的進程中，或在刪除EJB終結點並必須再次添加時，可以將EJB終結點添加到該進程中。

### 步驟摘要 {#summary-of-steps}

要將EJB終結點添加到服務，請執行以下任務：

1. 包括項目檔案。
1. 建立 `EndpointRegistry Client` 的雙曲餘切值。
1. 設定EJB終結點屬性。
1. 建立EJB終結點。
1. 啟用終結點。

**包括項目檔案**

在開發項目中包括必要的檔案。 必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)

有關這些JAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立EndpointRegistry客戶端對象**

在以寫程式方式添加EJB端點之前，必須先建立 `EndpointRegistryClient` 的雙曲餘切值。

**設定EJB終結點屬性**

要為服務建立EJB終結點，請指定以下值：

* **連接器標識符**:指定要建立的終結點的類型。 要建立EJB終結點，請指定 `EJB`。
* **說明**:指定終結點說明。
* **名稱**:指定終結點的名稱。
* **服務標識符**:指定終結點所屬的服務。
* **操作名稱**:指定使用終結點調用的操作的名稱。 建立EJB終結點時，請指定通配符( `*`)。 但是，如果要指定特定操作而不是調用所有服務操作，請指定該操作的名稱，而不是使用通配符( `*`)。

**建立EJB終結點**

設定EJB終結點屬性後，可以為服務建立EJB終結點。

**啟用終結點**

建立新端點後，必須啟用它。 啟用終結點後，它可用於調用服務。 啟用終結點後，可以在管理控制台中查看它。

**另請參閱**

[使用Java API添加EJB終結點](programmatically-endpoints.md#adding-an-ejb-endpoint-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加EJB終結點 {#adding-an-ejb-endpoint-using-the-java-api}

使用Java API添加EJB終結點：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-liveccycle-client.jar。 (

1. 建立EndpointRegistry客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EndpointRegistryClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 設定EJB終結點屬性。

   * 建立 `CreateEndpointInfo` 對象。
   * 通過調用 `CreateEndpointInfo` 對象 `setConnectorId` 方法和傳遞字串值 `EJB`。
   * 通過調用 `CreateEndpointInfo` 對象 `setDescription` 和傳遞描述終結點的字串值。
   * 通過調用 `CreateEndpointInfo` 對象 `setName` 方法並傳遞指定名稱的字串值。
   * 通過調用 `CreateEndpointInfo` 對象 `setServiceId` 方法並傳遞指定服務名的字串值。
   * 指定通過調用 `CreateEndpointInfo` 對象 `setOperationName` 方法並傳遞一個指定操作名稱的字串值。 對於SOAP和EJB終結點，指定通配符( `*`)，這意味著所有操作。

1. 建立EJB終結點。

   通過調用 `EndpointRegistryClient` 對象 `createEndpoint` 方法和傳遞 `CreateEndpointInfo` 的雙曲餘切值。 此方法返回 `Endpoint` 表示新EJB終結點的對象。

1. 啟用終結點。

   通過調用 `EndpointRegistryClient` 對象的enable方法和傳遞 `Endpoint` 返回的對象 `createEndpoint` 的雙曲餘切值。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速啟動：使用Java API添加EJB終結點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-ejb-endpoint-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 添加SOAP終結點 {#adding-soap-endpoints}

可以使用AEM FormsJava API以寫程式方式將SOAP端點添加到服務。 通過添加SOAP終結點，您可以啟用客戶端應用程式通過使用SOAP模式來調用服務。 即，在設定調用AEM Forms所需的連接屬性時，可以選擇SOAP模式。

>[!NOTE]
>
>無法使用Web服務添加SOAP終結點。

>[!NOTE]
>
>通常，預設情況下會將SOAP終結點添加到服務中，但是，可以將SOAP終結點添加到以寫程式方式部署的進程中，或在刪除SOAP終結點並且必須再次添加時添加SOAP終結點。

### 步驟摘要 {#summary_of_steps-1}

要向服務添加SOAP終結點，請執行以下任務：

1. 包括項目檔案。
1. 建立 `EndpointRegistryClient` 的雙曲餘切值。
1. 設定SOAP終結點屬性。
1. 建立SOAP終結點。
1. 啟用終結點。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)

建立SOAP終結點需要這些JAR檔案。 但是，如果使用SOAP終結點調用服務，則需要添加JAR檔案。 有關AEM FormsJAR檔案的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立EndpointRegistry客戶端對象**

要以寫程式方式將SOAP終結點添加到服務，必須建立 `EndpointRegistryClient` 的雙曲餘切值。

**設定SOAP終結點屬性**

要向服務添加SOAP終結點，請指定以下值：

* **連接器標識符值**:指定要建立的終結點的類型。 要建立SOAP終結點，請指定 `SOAP`。
* **說明**:指定終結點說明。
* **名稱**:指定終結點名稱。
* **服務標識符值**:指定終結點所屬的服務。
* **操作名稱**:指定使用終結點調用的操作的名稱。 建立SOAP終結點時，請指定通配符( `*`)。 但是，如果要指定特定操作而不是調用所有服務操作，請指定該操作的名稱，而不是使用通配符( `*`)。

**建立SOAP終結點**

設定SOAP終結點屬性後，可以建立SOAP終結點。

**啟用終結點**

建立新端點後，必須啟用它。 啟用終結點後，它可用於調用服務。 啟用終結點後，可以在管理控制台中查看它。

**另請參閱**

[使用Java API添加SOAP終結點](programmatically-endpoints.md#add-a-soap-endpoint-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加SOAP終結點 {#add-a-soap-endpoint-using-the-java-api}

使用Java API將SOAP終結點添加到服務：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-liveccycle-client.jar。

1. 建立EndpointRegistry客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EndpointRegistryClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 設定SOAP終結點屬性。

   * 建立 `CreateEndpointInfo` 對象。
   * 通過調用 `CreateEndpointInfo` 對象 `setConnectorId` 方法和傳遞字串值 `SOAP`。
   * 通過調用 `CreateEndpointInfo` 對象 `setDescription` 和傳遞描述終結點的字串值。
   * 通過調用 `CreateEndpointInfo` 對象 `setName` 方法並傳遞指定名稱的字串值。
   * 通過調用 `CreateEndpointInfo` 對象 `setServiceId` 方法並傳遞指定服務名的字串值。
   * 指定通過調用 `CreateEndpointInfo` 對象 `setOperationName` 方法並傳遞指定操作名的字串值。 對於SOAP和EJB終結點，指定通配符( `*`)，這意味著所有操作。

1. 建立SOAP終結點。

   通過調用 `EndpointRegistryClient` 對象 `createEndpoint` 方法和傳遞 `CreateEndpointInfo` 的雙曲餘切值。 此方法返回 `Endpoint` 表示新SOAP終結點的對象。

1. 啟用終結點。

   通過調用 `EndpointRegistryClient` 對象的啟用方法和傳遞 `Endpoint` 返回的對象 `createEndpoint` 的雙曲餘切值。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速啟動：使用Java API添加SOAP終結點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-soap-endpoint-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 添加監視的資料夾終結點 {#adding-watched-folder-endpoints}

可以使用AEM FormsJava API以寫程式方式將監視資料夾終結點添加到服務。 通過添加「監視資料夾」終結點，用戶可以將檔案(如PDF檔案)放在資料夾中。 將檔案放在資料夾中時，將調用所配置的服務並處理該檔案。 服務執行指定操作後，會將修改的檔案保存到指定的輸出資料夾中。 已將受監視資料夾配置為以固定速率間隔或按cron計畫進行掃描，例如每週一、週三和週五的中午。

為以寫程式方式將「監視資料夾」終結點添加到服務，請考慮以下名為的短時進程 *加密文檔*。 (請參閱 [瞭解AEM Forms進程](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)。)

![aw_aw_encryptdocument進程](assets/aw_aw_encryptdocumentprocess.png)

此過程接受一個不安全的PDF文檔作為輸入值，然後將該不安全的PDF文檔傳遞給加密服務 `EncryptPDFUsingPassword` 的下界。 PDF文檔用密碼加密，而密碼加密的PDF文檔是此過程的輸出值。 輸入值(不安全的PDF文檔)的名稱為 `InDoc` 資料類型是 `com.adobe.idp.Document`。 輸出值(密碼加密的PDF文檔)的名稱為 `SecuredDoc` 資料類型是 `com.adobe.idp.Document`。

>[!NOTE]
>
>無法使用Web服務添加「監視資料夾」終結點。

### 步驟摘要 {#summary_of_steps-2}

要向服務添加監視資料夾終結點，請執行以下任務：

1. 包括項目檔案。
1. 建立 `EndpointRegistryClient` 的雙曲餘切值。
1. 設定「監視資料夾」終結點屬性。
1. 指定配置值。
1. 定義輸入參數值。
1. 定義輸出參數值。
1. 建立「監視資料夾」終結點。
1. 啟用終結點。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)

有關這些JAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立EndpointRegistry客戶端對象**

要以寫程式方式添加「監視資料夾」終結點，必須建立 `EndpointRegistryClient` 的雙曲餘切值。

**設定監視資料夾終結點屬性**

要為服務建立「監視資料夾」終結點，請指定以下值：

* **連接器標識符**:指定所建立的終結點的類型。 要建立監視資料夾終結點，請指定 `WatchedFolder`。
* **說明**:指定終結點的說明。
* **名稱**:指定終結點的名稱。
* **服務標識符**:指定終結點所屬的服務。 例如，要將「受監視資料夾」終結點添加到本節中引入的流程（當使用Workbench激活時，流程將變為服務），請指定 `EncryptDocument`。
* **操作名稱**:指定使用終結點調用的操作的名稱。 通常，在為源自在Workbench中建立的進程的服務建立「監視資料夾」終結點時，操作的名稱為 `invoke`。

**指定配置值**

以寫程式方式將監視資料夾終結點添加到服務時，必須為監視資料夾終結點指定配置值。 如果使用管理控制台添加了「監視資料夾」終結點，則管理員會指定這些配置值。

以下清單指定在以寫程式方式將監視資料夾終結點添加到服務時設定的配置值：

* **url**:指定監視的資料夾位置。 在群集環境中，此值必須指向可從群集中每台電腦訪問的共用網路資料夾。
* **非同步**:將調用類型標識為非同步或同步。 只能同步調用瞬態和同步進程。 預設值為true。 建議使用非同步。
* **cron表達式**:由石英用於調度輸入目錄的輪詢。
* **清除持續時間**:這是一個必需屬性。 結果資料夾中的檔案和資料夾在早於此值時被清除。 此值以天計。 此屬性在確保結果資料夾未滿時非常有用。 值為–1天表示從不刪除結果資料夾。 預設值為–1。
* **重複間隔**:掃描監視資料夾以進行輸入的間隔（秒）。 除非啟用限制，否則此值應比處理平均作業的時間長；否則，系統可能會過載。 預設值為 5。
* **重複計數**:監視資料夾掃描資料夾或目錄的次數。 值為–1表示無限掃描。 預設值為–1。
* **節流開啟**:限制可在任何給定時間處理的「監視資料夾」作業的數量。 作業的最大數量由batchSize值確定。
* **用戶名**:從監視資料夾調用目標服務時使用的用戶名。 此值是必需的。 預設值為SuperAdmin。
* **域名**:用戶的域。 此值是必需的。 預設值為DefaultDom。
* **批大小**:每次掃描要拾取的檔案或資料夾數。 使用此值可防止系統過載；一次掃描過多檔案可能會導致崩潰。 預設值為 2。
* **等待時間**:建立後掃描資料夾或檔案之前等待的時間（以毫秒為單位）。 例如，如果等待時間為36,000,000毫秒（一小時），並且檔案是在一分鐘前建立的，則此檔案在經過59分鐘或更長時間後被拾取。 此屬性對於確保將檔案或資料夾完全複製到輸入資料夾非常有用。 例如，如果要處理一個大檔案，並且該檔案下載需要10分鐘，請將等待時間設定為10&amp;ast;60 &amp;ast;1000毫秒。 此設定可阻止監視資料夾在等待10分鐘後掃描檔案。 預設值為 0。
* **排除檔案模式**:被監視資料夾用於確定要掃描和拾取的檔案和資料夾的模式。 不會掃描任何具有此模式的檔案或資料夾進行處理。 當輸入是包含多個檔案的資料夾時，此設定非常有用。 可以將資料夾的內容複製到一個資料夾中，該資料夾的名稱將由監視的資料夾拾取。 此步驟防止監視資料夾在將資料夾完全複製到輸入資料夾之前提取要處理的資料夾。 例如，如果excludeFilePattern值為 `data*`，所有與 `data*` 不被接走。 這包括名為 `data1`。 `data2`等等。 此外，可以用通配符模式來補充該模式以指定檔案模式。 監視資料夾修改規則運算式以支援通配符模式，如 `*.*` 和 `*.pdf`。 規則運算式不支援這些通配符模式。
* **包括檔案模式**:被監視資料夾用於確定掃描和拾取哪些資料夾和檔案的模式。 例如，如果此值 `*`，所有與 `input*` 被選中。 這包括名為 `input1`。 `input2`等等。 預設值為 `*`。此值表示所有檔案和資料夾。 此外，可以用通配符模式來補充該模式以指定檔案模式。 監視資料夾修改規則運算式以支援通配符模式，如 `*.*` 和 `*.pdf`。 規則運算式不支援這些通配符模式。 此值是必需的。
* **結果資料夾名**:儲存保存結果的資料夾。 此位置可以是絕對路徑或相對目錄路徑。 如果結果未顯示在此資料夾中，請檢查失敗資料夾。 不處理只讀檔案，將保存在故障資料夾中。 預設值為 `result/%Y/%M/%D/`。這是監視資料夾內的結果資料夾。
* **preserveFolderName**:成功掃描和拾取檔案後儲存檔案的位置。 此位置可以是絕對、相對或空目錄路徑。 預設值為 `preserve/%Y/%M/%D/`。
* **failureFolderName**:保存故障檔案的資料夾。 此位置始終相對於監視的資料夾。 不處理只讀檔案，將保存在故障資料夾中。 預設值為 `failure/%Y/%M/%D/`。
* **preserveOnFailure**:在無法對服務執行操作時保留輸入檔案。 預設值為true。
* **overwriteDuplicateFilename**:如果設定為true，結果資料夾和保留資料夾中的檔案將被覆蓋。 如果設定為false，則具有數字索引尾碼的檔案和資料夾將用於名稱。 預設值為false。

**定義輸入參數值**

建立「監視資料夾」終結點時，必須定義輸入參數值。 即，必須描述傳遞給受監視資料夾調用的操作的輸入值。 例如，請考慮本主題中介紹的過程。 它有一個名為 `InDoc` 其資料類型為 `com.adobe.idp.Document`。 為此進程建立「監視資料夾」終結點時（在某個進程被激活後，它將變為服務），必須定義輸入參數值。

要定義監視資料夾終結點所需的輸入參數值，請指定以下值：

**輸入參數名稱**:輸入參數的名稱。 在Workbench中為流程指定輸入值的名稱。 如果輸入值屬於服務操作（不是在Workbench中建立的進程的服務），則在component.xml檔案中指定輸入名稱。 例如，本節中介紹的進程的輸入參數名稱為 `InDoc`。

**映射類型**:用於配置調用服務操作所需的輸入值。 映射類型有兩種：

* `Literal`:監視資料夾終結點在顯示時使用在欄位中輸入的值。 支援所有基本Java類型。 例如，如果API使用String、long、int和Boolean等輸入，則字串將轉換為正確的類型並調用服務。
* `Variable`:輸入的值是被監視資料夾用於選擇輸入的檔案模式。 例如，如果為映射類型選擇「變數」，且輸入文檔必須是PDF檔案，則可以指定 `*.pdf`值。

**映射值**:指定映射類型的值。 例如，如果您選擇 `Variable` 映射類型，可以指定 `*.pdf` 檔案模式。

**資料類型**:指定輸入值的資料類型。 例如，本節中介紹的進程輸入值的資料類型為 `com.adobe.idp.Document`。

**定義輸出參數值**

建立「監視資料夾」終結點時，必須定義輸出參數值。 也就是說，必須描述由「監視資料夾」終結點調用的服務返回的輸出值。 例如，請考慮本主題中介紹的過程。 它的輸出值名為 `SecuredDoc` 其資料類型為 `com.adobe.idp.Document`。 為此進程建立「監視資料夾」終結點時（在某個進程被激活後，它將變為服務），必須定義輸出參數值。

要定義監視資料夾終結點所需的輸出參數值，請指定以下值：

**輸出參數名稱**:輸出參數的名稱。 流程輸出值的名稱在Workbench中指定。 如果輸出值屬於服務操作（不是在Workbench中建立的進程的服務），則輸出名稱在component.xml檔案中指定。 例如，本節中介紹的進程的輸出參數的名稱是 `SecuredDoc`。

**映射類型**:用於配置服務和操作的輸出。 以下選項可用：

* 如果服務返回單個對象（單個文檔），則模式為 `%F.pdf` 源目標為sourcefilename.pdf。 例如，本節中引入的進程返回單個文檔。 因此，可以將映射類型定義為 `%F.pdf` ( `%F` 表示使用給定的檔案名)。 圖案 `%E` 指定輸入文檔的副檔名。
* 如果服務返回清單，則模式為 `Result\%F\`，並且源目標為Result\sourcefilename\source1（輸出1）和Result\sourcefilename\source2（輸出2）。
* 如果服務返回映射，則模式為 `Result\%F\`，並且源目標為Result\sourcefilename\file1和Result\sourcefilename\file2。 如果映射具有多個對象，則模式為 `Result\%F.pdf` 而源目標為Result\sourcefilename1.pdf（輸出1）、Result\sourcefilenam2.pdf（輸出2）等。

**資料類型**:指定返回值的資料類型。 例如，本節中介紹的進程返回值的資料類型為 `com.adobe.idp.Document`。

**建立監視資料夾終結點**

設定終結點的屬性、配置值並定義輸入和輸出參數值後，必須建立「監視資料夾」終結點。

**啟用終結點**

建立「監視資料夾」終結點後，必須啟用它。 啟用終結點後，它可用於調用服務。 啟用終結點後，可以在管理控制台中查看它。

**另請參閱**

[使用Java API添加監視資料夾終結點](programmatically-endpoints.md#add-a-watched-folder-endpoint-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加監視資料夾終結點 {#add-a-watched-folder-endpoint-using-the-java-api}

使用AEM FormsJava API添加監視資料夾終結點：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-liveccycle-client.jar。

1. 建立EndpointRegistry客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EndpointRegistryClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 設定「監視資料夾」終結點屬性。

   * 建立 `CreateEndpointInfo` 對象。
   * 通過調用 `CreateEndpointInfo` 對象 `setConnectorId` 方法和傳遞字串值 `WatchedFolder`。
   * 通過調用 `CreateEndpointInfo` 對象 `setDescription` 和傳遞描述終結點的字串值。
   * 通過調用 `CreateEndpointInfo` 對象 `setName` 方法並傳遞指定名稱的字串值。
   * 通過調用 `CreateEndpointInfo` 對象 `setServiceId` 方法並傳遞指定服務名的字串值。
   * 指定通過調用 `CreateEndpointInfo` 對象 `setOperationName` 方法並傳遞指定操作名的字串值。 通常，在為源自在Workbench中建立的進程的服務建立「監視資料夾」終結點時，將調用操作的名稱。

1. 指定配置值。

   對於要為「監視資料夾」終結點設定的每個配置值，必須調用 `CreateEndpointInfo` 對象 `setConfigParameterAsText` 的雙曲餘切值。 例如，要設定 `url` 配置值，調用 `CreateEndpointInfo` 對象 `setConfigParameterAsText` 方法並傳遞以下字串值：

   * 一個字串值，它指定配置值的名稱。 設定 `url` 配置值，指定 `url`。
   * 一個字串值，它指定配置值的值。 設定 `url` 配置值，指定監視的資料夾位置。

   >[!NOTE]
   >
   >要查看為EncryptDocument服務設定的所有配置值，請參閱位於 [快速啟動：使用Java API添加監視資料夾終結點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)。

1. 定義輸入參數值。

   通過調用 `CreateEndpointInfo` 對象 `setInputParameterMapping` 方法並傳遞以下值：

   * 指定輸入參數名稱的字串值。 例如，EncryptDocument服務的輸入參數的名稱為 `InDoc`。
   * 一個字串值，它指定輸入參數的資料類型。 例如， `InDoc` 輸入參數為 `com.adobe.idp.Document`。
   * 指定映射類型的字串值。 例如，可以指定 `variable`。
   * 指定映射類型值的字串值。 例如，可以將&amp;ast;.pdf指定為檔案模式。

   >[!NOTE]
   >
   >調用 `setInputParameterMapping` 定義每個輸入參數值的方法。 由於EncryptDocument進程只有一個輸入參數，因此需要調用此方法一次。

1. 定義輸出參數值。

   通過調用 `CreateEndpointInfo` 對象 `setOutputParameterMapping` 方法並傳遞以下值：

   * 指定輸出參數名稱的字串值。 例如，EncryptDocument服務的輸出參數的名稱為 `SecuredDoc`。
   * 一個字串值，它指定輸出參數的資料類型。 例如， `SecuredDoc` 輸出參數為 `com.adobe.idp.Document`。
   * 指定映射類型的字串值。 例如，可以指定 `%F.pdf`。

1. 建立「監視資料夾」終結點。

   通過調用 `EndpointRegistryClient` 對象 `createEndpoint` 方法和傳遞 `CreateEndpointInfo` 的雙曲餘切值。 此方法返回 `Endpoint` 表示「監視資料夾」終結點的對象。

1. 啟用終結點。

   通過調用 `EndpointRegistryClient` 對象 `enable` 方法和傳遞 `Endpoint` 返回的對象 `createEndpoint` 的雙曲餘切值。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速啟動：使用Java API添加監視資料夾終結點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 監視的資料夾配置值常數檔案 {#watched-folder-configuration-values-constant-file}

的 [快速啟動：使用Java API添加監視資料夾終結點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api) 使用一個常數檔案，該檔案必須是Java項目的一部分，才能編譯快速啟動。 此常數檔案表示添加監視資料夾終結點時必須設定的配置值。 以下Java代碼表示常數檔案。

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

## 添加電子郵件終結點 {#adding-email-endpoints}

可以使用AEM FormsJava API以寫程式方式將電子郵件終結點添加到服務。 通過添加電子郵件終結點，用戶可以將包含一個或多個檔案附件的電子郵件發送到指定的電子郵件帳戶。 然後調用配置服務操作並操縱檔案。 在服務執行指定操作後，它會向發送者發送一封電子郵件，其中將修改的檔案作為檔案附件。

為了以寫程式方式將電子郵件終結點添加到服務中，請考慮以下名為的短時間進程 *MyApplication\EncryptDocument*。 有關短期進程的資訊，請參見 [瞭解AEM Forms進程](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)。

![ae_ae_encryptdocument進程](assets/ae_ae_encryptdocumentprocess.png)

此過程接受一個不安全的PDF文檔作為輸入值，然後將該不安全的PDF文檔傳遞給加密服務 `EncryptPDFUsingPassword` 的下界。 此過程使用密碼對PDF文檔進行加密，並將密碼加密的PDF文檔返回為輸出值。 輸入值(不安全的PDF文檔)的名稱為 `InDoc` 資料類型是 `com.adobe.idp.Document`。 輸出值(密碼加密的PDF文檔)的名稱為 `SecuredDoc` 資料類型是 `com.adobe.idp.Document`。

>[!NOTE]
>
>無法使用Web服務添加電子郵件終結點。

### 步驟摘要 {#summary_of_steps-3}

要將電子郵件終結點添加到服務，請執行以下任務：

1. 包括項目檔案。
1. 建立 `EndpointRegistryClient` 的雙曲餘切值。
1. 設定電子郵件終結點屬性。
1. 指定配置值。
1. 定義輸入參數值。
1. 定義輸出參數值。
1. 建立電子郵件終結點。
1. 啟用終結點。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)

有關這些JAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立EndpointRegistry客戶端對象**

在以寫程式方式添加電子郵件終結點之前，必須建立 `EndpointRegistryClient` 的雙曲餘切值。

**設定電子郵件終結點屬性**

要為服務建立電子郵件終結點，請指定以下值：

* **連接器標識符值**:指定所建立的終結點的類型。 要建立電子郵件終結點，請指定 `Email`。
* **說明**:指定終結點的說明。
* **名稱**:指定終結點的名稱。
* **服務標識符值**:指定終結點所屬的服務。 例如，要將電子郵件終結點添加到本節中介紹的流程（使用Workbench激活時，流程將成為服務），請指定 `EncryptDocument`。
* **操作名稱**:指定使用終結點調用的操作的名稱。 通常，在為源自在Workbench中建立的流程的服務建立電子郵件終結點時，操作的名稱為 `invoke`。

**指定配置值**

以寫程式方式將電子郵件終結點添加到服務時，必須為電子郵件終結點指定配置值。 如果使用管理控制台添加電子郵件終結點，則管理員會指定這些配置值。

>[!NOTE]
>
>受監視的電子郵件帳戶是僅用於電子郵件終結點的特殊帳戶。 此帳戶不是普通用戶的電子郵件帳戶。 常規用戶的電子郵件帳戶不能配置為電子郵件提供程式使用的帳戶，因為電子郵件提供程式在郵件完成後會從收件箱中刪除電子郵件。

以寫程式方式將電子郵件終結點添加到服務時，將設定以下配置值：

* **cron表達式**:如果必須使用cron表達式來調度電子郵件，則為cron表達式。
* **重複計數**:電子郵件終結點掃描資料夾或目錄的次數。 值為–1表示無限掃描。 預設值為–1。
* **重複間隔**:接收方用於檢查傳入郵件的掃描速率（秒）。 預設值為 10。
* **啟動延遲**:計畫程式啟動後等待掃描的時間。 預設時間為0。
* **批大小**:每次掃描接收方處理的電子郵件數以獲得最佳效能。 值–1表示所有電子郵件。 預設值為 2。
* **用戶名**:從電子郵件調用目標服務時使用的用戶名。 預設值為 `SuperAdmin`。
* **域名**:必需的配置值。 預設值為 `DefaultDom`。
* **域模式**:指定提供程式接受的傳入電子郵件的域模式。 例如，如果 `adobe.com` 只處理adobe.com的電子郵件，忽略其他域的電子郵件。
* **檔案模式**:指定提供程式接受的傳入檔案附件模式。 這包括具有特定檔案名副檔名(&amp;ast;.dat、&amp;ast;.xml)的檔案、具有特定名稱（資料）的檔案，以及在名稱和副檔名中具有複合表達式的檔案(&amp;ast;)。[dD][aA]「port」)。 預設值為 `*`。
* **收件人成功作業**:發送郵件以指示成功作業的電子郵件地址。 預設情況下，成功的作業消息始終發送給發件人。 如果鍵入 `sender`，電子郵件結果將發送給發件人。 最多支援100個收件人。 使用電子郵件地址指定其他收件人，每個收件人用逗號分隔。 要關閉此選項，請將此值留空。 在某些情況下，您可能希望觸發進程，而不希望收到結果的電子郵件通知。 預設值為 `sender`。
* **收件人失敗作業**:發送郵件以指示失敗作業的電子郵件地址。 預設情況下，失敗的作業消息始終發送給發件人。 如果鍵入 `sender`，電子郵件結果將發送給發件人。 最多支援100個收件人。 使用電子郵件地址指定其他收件人，每個收件人用逗號分隔。 要關閉此選項，請將此值留空。 預設值為 `sender`。
* **收件箱主機**:要掃描的電子郵件提供程式的收件箱主機名或IP地址。
* **收件箱埠**:電子郵件伺服器使用的埠。 POP3的預設值為110,IMAP的預設值為143。 如果啟用了SSL，則POP3的預設值為995,IMAP的預設值為993。
* **收件箱協定**:用於掃描收件箱的電子郵件終結點的電子郵件協定。 選項包括 `IMAP` 或 `POP3`。 收件箱主機郵件伺服器必須支援這些協定。
* **收件箱超時**:電子郵件提供程式等待收件箱響應的超時（秒）。 預設值為 60。
* **收件箱用戶**:登錄到電子郵件帳戶所需的用戶名。 根據電子郵件伺服器和配置的不同，這可能只是電子郵件的用戶名部分，也可能是完整的電子郵件地址。
* **收件箱密碼**:收件箱用戶的密碼。
* **收件箱已啟用**:將此值設定為在發送結果或錯誤通知消息時強制電子郵件提供程式使用SSL。 確保IMAP或POP3主機支援SSL。
* **smtp主機**:電子郵件提供程式向其發送結果和錯誤消息的郵件伺服器的主機名。
* **smtp埠**:SMTP埠的預設值為25。
* **smtp用戶**:電子郵件提供程式在發送結果和錯誤的電子郵件通知時要使用的用戶帳戶。
* **smtp密碼**:SMTP帳戶的密碼。 某些郵件伺服器不需要SMTP密碼。
* **字元集**:電子郵件提供程式使用的字元集。 預設值為 `UTF-8`。
* **smtpSSLEnabled**:將此值設定為在發送結果或錯誤通知消息時強制電子郵件提供程式使用SSL。 確保SMTP主機支援SSL。
* **失敗的作業資料夾**:指定當SMTP郵件伺服器不工作時要在其中儲存結果的目錄。
* **非同步**:設定為同步時，將處理所有輸入文檔並返回單個響應。 當設定為非同步時，會為每個被處理的輸入文檔發送響應。 例如，會為本主題中引入的進程建立一個電子郵件終結點，並且會向終結點的收件箱發送一封電子郵件，其中包含多個不安全的PDF文檔。 當所有PDF文檔都使用密碼進行加密，並且如果終結點配置為同步，則會發送單個響應電子郵件，並附加所有安全PDF文檔。 如果端點配置為非同步，則為每個安全PDF文檔發送單獨的響應電子郵件。 每封電子郵件都包含一個作為附件的PDF文檔。 預設值為非同步。

**定義輸入參數值**

建立電子郵件端點時，必須定義輸入參數值。 即，必須描述傳遞給電子郵件終結點調用的操作的輸入值。 例如，請考慮本主題中介紹的過程。 它有一個名為 `InDoc` 其資料類型為 `com.adobe.idp.Document`。 為此進程建立電子郵件終結點時（在某個進程被激活後，它將變為服務），必須定義輸入參數值。

要定義電子郵件終結點所需的輸入參數值，請指定以下值：

**輸入參數名稱**:輸入參數的名稱。 在Workbench中為流程指定輸入值的名稱。 如果輸入值屬於服務操作(不是在Workbench中建立的進程的Forms服務)，則在component.xml檔案中指定輸入名稱。 例如，本節中介紹的進程的輸入參數名稱為 `InDoc`。

**映射類型**:用於配置調用服務操作所需的輸入值。 映射類型有兩種：

* `Literal`:「電子郵件」端點在顯示時使用在欄位中輸入的值。 支援所有基本Java類型。 例如，如果API使用String、long、int和Boolean等輸入，則字串將轉換為正確的類型並調用服務。
* `Variable`:輸入的值是電子郵件終結點用於選擇輸入的檔案模式。 例如，如果為映射類型選擇「變數」，且輸入文檔必須是PDF檔案，則可以指定 `*.pdf` 值。

**映射值**:指定映射類型的值。 例如，如果選擇了「變數」映射類型，則可以指定 `*.pdf` 檔案模式。

**資料類型**:指定輸入值的資料類型。 例如，本節中介紹的進程輸入值的資料類型是com.adobe.idp.Document。

**定義輸出參數值**

建立電子郵件端點時，必須定義輸出參數值。 即，必須描述由電子郵件終結點調用的服務返回的輸出值。 例如，請考慮本主題中介紹的過程。 它的輸出值名為 `SecuredDoc` 其資料類型為 `com.adobe.idp.Document`。 為此進程建立電子郵件終結點時（在某個進程被激活後，它將變為服務），必須定義輸出參數值。

要定義電子郵件終結點所需的輸出參數值，請指定以下值：

**輸出參數名稱**:輸出參數的名稱。 流程輸出值的名稱在Workbench中指定。 如果輸出值屬於服務操作（不是在Workbench中建立的進程的服務），則輸出名稱在component.xml檔案中指定。 例如，本節中介紹的進程的輸出參數的名稱是 `SecuredDoc`。

**映射類型**:用於配置服務和操作的輸出。 以下選項可用：

* 如果服務返回單個對象（單個文檔），則模式為 `%F.pdf` 源目標為sourcefilename.pdf。 例如，本節中引入的進程返回單個文檔。 因此，可以將映射類型定義為 `%F.pdf` ( `%F` 表示使用給定的檔案名)。 圖案 `%E` 指定輸入文檔的副檔名。
* 如果服務返回清單，則模式為 `Result\%F\`，並且源目標為Result\sourcefilename\source1（輸出1）和Result\sourcefilename\source2（輸出2）。
* 如果服務返回映射，則模式為 `Result\%F\`，並且源目標為Result\sourcefilename\file1和Result\sourcefilename\file2。 如果映射具有多個對象，則模式為 `Result\%F.pdf` 而源目標為Result\sourcefilename1.pdf（輸出1）、Result\sourcefilenam2.pdf（輸出2）等。

**資料類型**:指定返回值的資料類型。 例如，本節中介紹的進程返回值的資料類型為 `com.adobe.idp.Document`。

**建立電子郵件終結點**

在設定電子郵件端點屬性和配置值並定義輸入和輸出參數值後，必須建立電子郵件端點。

**啟用終結點**

建立電子郵件終結點後，必須啟用它。 啟用終結點後，它可用於調用服務。 啟用終結點後，可以在管理控制台中查看它。

**另請參閱**

[使用Java API添加電子郵件終結點](programmatically-endpoints.md#add-an-email-endpoint-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加電子郵件終結點 {#add-an-email-endpoint-using-the-java-api}

使用Java API添加電子郵件終結點：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-liveccycle-client.jar。

1. 建立EndpointRegistry客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EndpointRegistryClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 設定電子郵件終結點屬性。

   * 建立 `CreateEndpointInfo` 對象。
   * 通過調用 `CreateEndpointInfo` 對象 `setConnectorId` 方法和傳遞字串值 `Email`。
   * 通過調用 `CreateEndpointInfo` 對象 `setDescription` 和傳遞描述終結點的字串值。
   * 通過調用 `CreateEndpointInfo` 對象 `setName` 方法並傳遞指定名稱的字串值。
   * 通過調用 `CreateEndpointInfo` 對象 `setServiceId` 方法並傳遞指定服務名的字串值。
   * 指定通過調用 `CreateEndpointInfo` 對象 `setOperationName` 方法並傳遞指定操作名的字串值。 通常，在為源自在Workbench中建立的進程的服務建立電子郵件終結點時，會調用該操作的名稱。

1. 指定配置值。

   對於要為電子郵件終結點設定的每個配置值，必須調用 `CreateEndpointInfo` 對象 `setConfigParameterAsText` 的雙曲餘切值。 例如，要設定 `smtpHost` 配置值，調用 `CreateEndpointInfo` 對象 `setConfigParameterAsText` 方法並傳遞以下值：

   * 一個字串值，它指定配置值的名稱。 設定 `smtpHost` 配置值，指定 `smtpHost`。
   * 一個字串值，它指定配置值的值。 設定 `smtpHost` 配置值，指定指定SMTP伺服器名稱的字串值。

   >[!NOTE]
   >
   >要查看本節中介紹的EncryptDocument服務的所有配置值集，請參閱位於 [快速啟動：使用Java API添加電子郵件終結點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api)。

1. 定義輸入參數值。

   通過調用 `CreateEndpointInfo` 對象 `setInputParameterMapping` 方法並傳遞以下值：

   * 指定輸入參數名稱的字串值。 例如，EncryptDocument服務的輸入參數的名稱為 `InDoc`。
   * 一個字串值，它指定輸入參數的資料類型。 例如， `InDoc` 輸入參數為 `com.adobe.idp.Document`。
   * 指定映射類型的字串值。 例如，可以指定 `variable`。
   * 指定映射類型值的字串值。 例如，可以將&amp;ast;.pdf指定為檔案模式。

   >[!NOTE]
   >
   >調用 `setInputParameterMapping` 定義每個輸入參數值的方法。 由於EncryptDocument進程只有一個輸入參數，因此需要調用此方法一次。

1. 定義輸出參數值。

   通過調用 `CreateEndpointInfo` 對象 `setOutputParameterMapping` 方法並傳遞以下值：

   * 指定輸出參數名稱的字串值。 例如，EncryptDocument服務的輸出參數的名稱為 `SecuredDoc`。
   * 一個字串值，它指定輸出參數的資料類型。 例如， `SecuredDoc` 輸出參數為 `com.adobe.idp.Document`。
   * 指定映射類型的字串值。 例如，可以指定 `%F.pdf`。

1. 建立電子郵件終結點。

   通過調用 `EndpointRegistryClient` 對象 `createEndpoint` 方法和傳遞 `CreateEndpointInfo` 的雙曲餘切值。 此方法返回 `Endpoint` 表示電子郵件終結點的對象。

1. 啟用終結點。

   通過調用 `EndpointRegistryClient` 對象 `enable` 方法和傳遞 `Endpoint` 返回的對象 `createEndpoint` 的雙曲餘切值。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速啟動：使用Java API添加監視資料夾終結點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 電子郵件配置值常數檔案 {#email-configuration-values-constant-file}

的 [快速啟動：使用Java API添加電子郵件終結點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api) 使用一個常數檔案，該檔案必須是Java項目的一部分，才能編譯快速啟動。 此常數檔案表示添加電子郵件終結點時必須設定的配置值。 以下Java代碼表示常數檔案。

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

## 添加遠程處理終結點 {#adding-remoting-endpoints}

>[!NOTE]
>
>LiveCycle RemotingAPI已棄AEM用於JEE上的表單。

可以使用AEM FormsJava API以寫程式方式將遠程處理終結點添加到服務。 通過添加遠程處理終結點，您正在啟用Flex應用程式通過使用遠程處理來調用服務。 (請參閱 [調用AEM Forms使用(不建議AEM用於表單)AEM Forms遠程處理](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)。)

為了以寫程式方式將遠程處理終結點添加到服務中，請考慮以下名為的短期進程 *加密文檔*。

![ar_ar_encryptdocumentprocess](assets/ar_ar_encryptdocumentprocess.png)

此過程接受一個不安全的PDF文檔作為輸入值，然後將該不安全的PDF文檔傳遞給加密服務 `EncryptPDFUsingPassword` 的下界。 PDF文檔用密碼加密，而密碼加密的PDF文檔是此過程的輸出值。 輸入值(不安全的PDF文檔)的名稱為 `InDoc` 資料類型是 `com.adobe.idp.Document`。 輸出值(密碼加密的PDF文檔)的名稱為 `SecuredDoc` 資料類型是 `com.adobe.idp.Document`。

要演示如何向服務添加遠程處理終結點，本節將遠程處理終結點添加到名為EncryptDocument的服務。

>[!NOTE]
>
>無法使用Web服務添加遠程處理終結點。

### 步驟摘要 {#summary_of_steps-4}

要從服務中刪除終結點，請執行以下任務：

1. 包括項目檔案。
1. 建立 `EndpointRegistryClient` 的雙曲餘切值。
1. 設定遠程處理終結點屬性。
1. 建立遠程處理終結點。
1. 啟用終結點。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)

有關這些JAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立EndpointRegistry客戶端對象**

要以寫程式方式添加遠程處理端點，必須建立 `EndpointRegistryClient` 的雙曲餘切值。

**設定遠程處理終結點屬性**

要為服務建立遠程處理終結點，請指定以下值：

* **連接器標識符值**:指定所建立的終結點的類型。 要建立遠程處理終結點，請指定 `Remoting`。
* **說明**:指定終結點的說明。
* **名稱**:指定終結點的名稱。
* **服務標識符值**:指定終結點所屬的服務。 例如，要將遠程處理終結點添加到此部分中引入的流程（當在Workbench中激活該流程時，該流程將成為服務），請指定 `EncryptDocument`。
* **操作名稱**:指定使用終結點調用的操作的名稱。 建立遠程處理終結點時，請指定通配符(&amp;ast;)。

**建立遠程處理終結點**

設定遠程處理終結點屬性後，可以為服務建立遠程處理終結點。

**啟用終結點**

建立新端點後，必須啟用它。 啟用遠程處理終結點後，它使Flex客戶端能夠調用該服務。

**另請參閱**

[使用Java API添加遠程處理終結點](programmatically-endpoints.md#add-a-remoting-endpoint-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加遠程處理終結點 {#add-a-remoting-endpoint-using-the-java-api}

使用Java API添加遠程處理終結點：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-liveccycle-client.jar。

1. 建立EndpointRegistry客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EndpointRegistryClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 設定遠程處理終結點屬性。

   * 建立 `CreateEndpointInfo` 對象。
   * 通過調用 `CreateEndpointInfo` 對象 `setConnectorId` 方法和傳遞字串值 `Remoting`。
   * 通過調用 `CreateEndpointInfo` 對象 `setDescription` 和傳遞描述終結點的字串值。
   * 通過調用 `CreateEndpointInfo` 對象 `setName` 方法並傳遞指定名稱的字串值。
   * 通過調用 `CreateEndpointInfo` 對象 `setServiceId` 方法並傳遞指定服務名的字串值。
   * 指定由 `CreateEndpointInfo` 對象 `setOperationName` 方法並傳遞指定操作名的字串值。 對於遠程處理終結點，指定通配符(&amp;ast;)。

1. 建立遠程處理終結點。

   通過調用 `EndpointRegistryClient` 對象 `createEndpoint` 方法和傳遞 `CreateEndpointInfo` 的雙曲餘切值。 此方法返回 `Endpoint` 表示新遠程處理終結點的對象。

1. 啟用終結點。

   通過調用 `EndpointRegistryClient` 對象 `enable` 方法和傳遞 `Endpoint` 返回的對象 `createEndpoint` 的雙曲餘切值。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速啟動：使用Java API添加遠程處理終結點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-remoting-endpoint-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 添加TaskManager終結點 {#adding-taskmanager-endpoints}

可以通過使用AEM FormsJava API以寫程式方式將TaskManager終結點添加到服務。 通過將TaskManager終結點添加到服務，可使Workspace用戶調用該服務。 即，在Workspace中工作的用戶可以調用具有相應TaskManager終結點的進程。

>[!NOTE]
>
>不能使用Web服務添加TaskManager終結點。

### 步驟摘要 {#summary_of_steps-5}

要將TaskManager終結點添加到服務，請執行以下任務：

1. 包括項目檔案。
1. 建立 `EndpointRegistryClient` 的雙曲餘切值。
1. 為終結點建立類別。
1. 設定TaskManager終結點屬性。
1. 建立TaskManager終結點。
1. 啟用終結點。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)

有關這些JAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立EndpointRegistry客戶端對象**

在以寫程式方式添加TaskManager終結點之前，必須建立 `EndpointRegistryClient` 的雙曲餘切值。

**為終結點建立類別**

類別用於組織工作區中的服務。 即，Workspace用戶可以通過在Workspace中選擇類別來調用具有TaskManager終結點的服務。 建立TaskManager端點時，可以引用現有類別或以寫程式方式建立新類別。

>[!NOTE]
>
>此部分將建立新類別，作為向服務添加TaskManager終結點的一部分。

**設定TaskManager終結點屬性**

要為服務建立TaskManager終結點，請指定以下值：

* **連接器標識符**:指定所建立的終結點的類型。 要建立TaskManager終結點，請指定 `TaskManagerConnector`。
* **說明**:指定終結點的說明。
* **名稱**:指定終結點的名稱。
* **服務標識符**:指定終結點所屬的服務。
* **類別**:指定與TaskManager終結點關聯的類別標識符值。
* **操作名稱**:通常，在為源自在Workbench中建立的進程的服務建立TaskManager終結點時，操作的名稱為 `invoke`。

**建立TaskManager終結點**

設定TaskManager終結點屬性後，可以為服務建立TaskManager終結點。

**啟用終結點**

建立新端點後，必須啟用它。 啟用端點後，它可用於從工作區中調用服務。 啟用終結點後，可以在管理控制台中查看它。

**另請參閱**

[使用Java API添加TaskManager終結點](programmatically-endpoints.md#add-a-taskmanager-endpoint-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加TaskManager終結點 {#add-a-taskmanager-endpoint-using-the-java-api}

使用Java API添加TaskManager終結點：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-liveccycle-client.jar。

1. 建立EndpointRegistry客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EndpointRegistryClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 為終結點建立類別。

   * 建立 `CreateEndpointCategoryInfo` 對象，並傳遞以下值：

      * 指定類別標識符值的字串值
      * 指定類別描述的字串值
   * 通過調用 `EndpointRegistryClient` 對象 `createEndpointCategory` 方法和傳遞 `CreateEndpointCategoryInfo` 的雙曲餘切值。 此方法返回 `EndpointCategory` 表示新類別的對象。


1. 設定TaskManager終結點屬性。

   * 建立 `CreateEndpointInfo` 對象。
   * 通過調用 `CreateEndpointInfo` 對象 `setConnectorId` 方法和傳遞字串值 `TaskManagerConnector`。
   * 通過調用 `CreateEndpointInfo` 對象 `setDescription` 和傳遞描述終結點的字串值。
   * 通過調用 `CreateEndpointInfo` 對象 `setName` 方法並傳遞指定名稱的字串值。
   * 通過調用 `CreateEndpointInfo` 對象 `setServiceId` 方法並傳遞指定服務名的字串值。
   * 通過調用 `CreateEndpointInfo` 對象 `setCategoryId` 方法，並傳遞指定類別標識符值的字串值。 您可以調用 `EndpointCategory` 對象 `getId` 方法，獲取此類別的標識符值。
   * 指定通過調用 `CreateEndpointInfo` 對象 `setOperationName` 方法並傳遞指定操作名的字串值。 通常，在建立 `TaskManager` 源於在Workbench中建立的進程的服務的終結點，該操作的名稱為 `invoke`。

1. 建立TaskManager終結點。

   通過調用 `EndpointRegistryClient` 對象 `createEndpoint` 方法和傳遞 `CreateEndpointInfo` 的雙曲餘切值。 此方法返回 `Endpoint` 表示新TaskManager終結點的對象。

1. 啟用終結點。

   通過調用 `EndpointRegistryClient` 對象 `enable` 方法和傳遞 `Endpoint` 返回的對象 `createEndpoint` 的雙曲餘切值。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速啟動：使用Java API添加TaskManager終結點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-taskmanager-endpoint-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 修改端點 {#modifying-endpoints}

可以使用AEM FormsJava API以寫程式方式修改現有端點。 通過修改端點，可以更改端點的行為。 例如，考慮一個「監視資料夾」終結點，它指定用作監視資料夾的資料夾。 您可以以寫程式方式修改屬於「監視資料夾」終結點的配置值，從而導致另一個資料夾作為監視資料夾工作。 有關屬於監視資料夾終結點的配置值的資訊，請參見 [添加監視的資料夾終結點](programmatically-endpoints.md#adding-watched-folder-endpoints)。

為了演示如何修改終結點，本節通過更改行為為監視資料夾的資料夾來修改監視資料夾終結點。

>[!NOTE]
>
>不能使用Web服務修改終結點。

### 步驟摘要 {#summary_of_steps-6}

要修改端點，請執行以下任務：

1. 包括項目檔案。
1. 建立 `EndpointRegistryClient` 的雙曲餘切值。
1. 檢索終結點。
1. 指定新配置值。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)

有關這些JAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立EndpointRegistry客戶端對象**

要以寫程式方式修改端點，必須建立 `EndpointRegistryClient` 的雙曲餘切值。

**檢索要修改的端點**

在修改端點之前，必須檢索它。 要檢索終結點，必須以可以訪問終結點的用戶身份連接。 建議您以管理員身份連接。 (請參閱 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties))。

可通過檢索端點清單來檢索端點。 然後，可以循環訪問清單，搜索要刪除的特定端點。 例如，可以通過確定與端點對應的服務和端點的類型來定位端點。 找到端點時，可以修改它。

**指定新配置值**

修改端點時，請指定新的配置值。 例如，要修改監視資料夾終結點，請重置所有監視資料夾終結點配置值，而不僅是要修改的值。 有關屬於監視資料夾終結點的配置值的資訊，請參見 [添加監視的資料夾終結點](programmatically-endpoints.md#adding-watched-folder-endpoints)。

>[!NOTE]
>
>有關屬於電子郵件終結點的配置值的資訊，請參見 [添加電子郵件終結點](programmatically-endpoints.md#adding-email-endpoints)。

>[!NOTE]
>
>無法修改終結點調用的服務。 如果嘗試修改服務，則會引發異常。 要修改與給定端點關聯的服務，請刪除該端點並建立一個新端點。 (請參閱 [刪除端點](programmatically-endpoints.md#removing-endpoints)。)

**另請參閱**

[使用Java API修改終結點](programmatically-endpoints.md#modifying-an-endpoint-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API修改終結點 {#modifying-an-endpoint-using-the-java-api}

使用Java API修改終結點：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-liveccycle-client.jar。

1. 建立EndpointRegistry客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EndpointRegistryClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 檢索要修改的端點。

   * 通過調用 `EndpointRegistryClient` 對象 `getEndpoints` 方法和通過 `PagingFilter` 用作篩選器的對象。 你可以通過 `(PagingFilter)null` 值以返回所有端點。 此方法返回 `java.util.List` 其中每個元素為 `Endpoint` 的雙曲餘切值。 有關 `PagingFilter` 對象，請參閱 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 迭代 `java.util.List` 確定它是否具有端點的對象。 如果存在端點，則每個元素都是 `EndPoint` 實例。
   * 通過調用 `EndPoint` 對象 `getServiceId` 的雙曲餘切值。 此方法返回一個指定服務名稱的字串值。
   * 通過調用 `EndPoint` 對象 `getConnectorId` 的雙曲餘切值。 此方法返回一個字串值，它指定端點的類型。 例如，如果終結點是「監視資料夾」終結點，則此方法返回 `WatchedFolder`。

1. 指定新配置值。

   * 建立 `ModifyEndpointInfo` 調用其建構子。
   * 對於要設定的每個配置值，調用 `ModifyEndpointInfo` 對象 `setConfigParameterAsText` 的雙曲餘切值。 例如，要設定url配置值，請調用 `ModifyEndpointInfo` 對象 `setConfigParameterAsText` 方法並傳遞以下值：

      * 一個字串值，它指定配置值的名稱。 例如，要設定 `url` 配置值，指定 `url`。
      * 一個字串值，它指定配置值的值。 要為 `url` 配置值，指定監視的資料夾位置。
   * 調用 `EndpointRegistryClient` 對象 `modifyEndpoint` 方法和通過 `ModifyEndpointInfo` 的雙曲餘切值。


**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速啟動：使用Java API修改終結點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-modifying-an-endpoint-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 刪除端點 {#removing-endpoints}

可以通過使用AEM FormsJava API以寫程式方式從服務中刪除端點。 刪除終結點後，無法使用啟用該終結點的調用方法調用該服務。 例如，如果從服務中刪除SOAP終結點，則不能使用SOAP模式調用服務。

要演示如何從服務中刪除終結點，本節將從名為EJB的服務中刪除EJB終結點 *加密文檔*。

>[!NOTE]
>
>不能使用Web服務刪除終結點。

### 步驟摘要 {#summary_of_steps-7}

要從服務中刪除終結點，請執行以下任務：

1. 包括項目檔案。
1. 建立 `EndpointRegistryClient` 的雙曲餘切值。
1. 檢索終結點。
1. 刪除終結點。

**包括項目檔案**

將必要的檔案包括到您的開發項目中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)

有關這些JAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立EndpointRegistry客戶端對象**

要以寫程式方式刪除端點，必須建立 `EndpointRegistryClient` 的雙曲餘切值。

**檢索要刪除的終結點**

必須先檢索終結點，然後才能刪除它。 要檢索終結點，必須以可以訪問終結點的用戶身份連接。 建議您以管理員身份連接。 (請參閱 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties))。

可通過檢索端點清單來檢索端點。 然後，可以循環訪問清單，搜索要刪除的特定端點。 例如，可以通過確定與端點對應的服務和端點的類型來定位端點。 找到端點後，可將其刪除。

**刪除終結點**

建立新端點後，必須啟用它。 啟用終結點後，它可用於調用服務。 啟用終結點後，可以在管理控制台中查看它。

**另請參閱**

[使用Java API刪除終結點](programmatically-endpoints.md#removing-an-endpoint-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API刪除終結點 {#removing-an-endpoint-using-the-java-api}

使用Java API刪除終結點：

1. 包括項目檔案。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-liveccycle-client.jar。

1. 建立EndpointRegistry客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `EndpointRegistryClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 檢索要刪除的終結點。

   * 通過調用 `EndpointRegistryClient` 對象 `getEndpoints` 方法和通過 `PagingFilter` 用作篩選器的對象。 你可以通過 `(PagingFilter)null` 返回所有終結點。 此方法返回 `java.util.List` 其中每個元素為 `Endpoint` 的雙曲餘切值。
   * 迭代 `java.util.List` 確定它是否具有端點的對象。 如果存在端點，則每個元素都是 `EndPoint` 實例。
   * 通過調用 `EndPoint` 對象 `getServiceId` 的雙曲餘切值。 此方法返回一個指定服務名稱的字串值。
   * 通過調用 `EndPoint` 對象 `getConnectorId` 的雙曲餘切值。 此方法返回一個字串值，它指定端點的類型。 例如，如果終結點是EJB終結點，則此方法返回 `EJB`。

1. 刪除終結點。

   通過調用 `EndpointRegistryClient` 對象 `remove` 方法和傳遞 `EndPoint` 表示要刪除的終結點的對象。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速啟動：使用Java API刪除終結點](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-removing-an-endpoint-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 檢索端點連接器資訊 {#retrieving-endpoint-connector-information}

可以使用AEM FormsAPI以寫程式方式檢索有關端點連接器的資訊。 連接器使端點能夠使用各種調用方法調用服務。 例如，「監視資料夾」連接器使終結點能夠使用監視資料夾調用服務。 通過以寫程式方式檢索有關端點連接器的資訊，可以檢索與連接器關聯的配置值，例如需要哪些配置值以及哪些配置值是可選的。

要演示如何檢索有關端點連接器的資訊，本節將檢索有關受監視資料夾連接器的資訊。 (請參閱 [添加監視的資料夾終結點](programmatically-endpoints.md#adding-watched-folder-endpoints)。)

>[!NOTE]
>
>無法使用Web服務檢索有關端點的資訊。

>[!NOTE]
>
>此主題使用 `ConnectorRegistryClient` API，用於檢索有關終結點連接器的資訊。 (請參閱 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。)

### 步驟摘要 {#summary_of_steps-8}

要檢索端點連接器資訊，請執行以下任務：

1. 包括項目檔案。
1. 建立 `ConnectorRegistryClient` 的雙曲餘切值。
1. 指定連接器類型。
1. 檢索配置值。

**包括項目檔案**

將必要的檔案包括到您的開發項目中。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請確保包含代理檔案。

必須將以下JAR檔案添加到項目的類路徑：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)

如果AEM Forms部署在非JBoss的受支援的J2EE應用程式伺服器上，則用特定於部署了AEM Forms的J2EE應用程式伺服器的JAR檔案替換adobe-utilities.jar和jbossall-client.jar。 有關所有AEM FormsJAR檔案的位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立ConnectorRegistry客戶端對象**

要以寫程式方式檢索端點連接器資訊，請建立 `ConnectorRegistryClient` 的雙曲餘切值。

**指定連接器類型**

指定要從中檢索資訊的連接器的類型。 存在以下類型的連接器：

* **EJB**:允許客戶端應用程式使用EJB模式調用服務。
* **SOAP**:使客戶端應用程式能夠使用SOAP模式調用服務。
* **監視資料夾**:允許受監視資料夾調用服務。
* **電子郵件**:允許電子郵件調用服務。
* **遠程處理**:使Flex客戶端應用程式能夠調用服務。
* **任務管理器連接器**:使Workspace用戶能夠從Workspace中調用服務。

**檢索配置值**

指定連接器類型後，可以檢索有關連接器的資訊，如支援的配置值。 例如，對於任何連接器，可確定需要哪些配置值以及哪些配置值是可選的。

**另請參閱**

[使用Java API檢索端點連接器資訊](programmatically-endpoints.md#retrieve-endpoint-connector-information-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API檢索端點連接器資訊 {#retrieve-endpoint-connector-information-using-the-java-api}

使用Java API檢索端點連接器資訊：

1. 包括項目檔案。。

   在Java項目的類路徑中包括客戶端JAR檔案，如adobe-liveccycle-client.jar。

1. 建立ConnectorRegistry客戶端對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。
   * 建立 `ConnectorRegistryClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 指定連接器類型。

   通過調用 `ConnectorRegistryClient` 對象 `getEndpointDefinition` 方法並傳遞指定連接器類型的字串值。 例如，要指定「監視資料夾」連接器類型，請傳遞字串值 `WatchedFolder`。 此方法返回 `Endpoint` 與連接器類型對應的對象。

1. 檢索配置值。

   * 通過調用 `Endpoint` 對象 `getConfigParameters` 的雙曲餘切值。 此方法返回 `ConfigParameter` 對象。
   * 通過檢索陣列中的每個元素來檢索有關每個配置值的資訊。 每個元素都是 `ConfigParameter` 的雙曲餘切值。 例如，通過調用 `ConfigParameter` 對象 `isRequired` 的雙曲餘切值。 如果需要配置值，則此方法將返回 `true`。

**另請參閱**

[步驟摘要](programmatically-endpoints.md#summary-of-steps)

[快速啟動：使用Java API檢索端點連接器資訊](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-retrieving-endpoint-connector-information-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
