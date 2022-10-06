---
title: 使用AEM Forms存放庫
seo-title: Working with AEM Forms Repository
description: 管理AEM Forms存放庫，以使用Java API和網站服務API建立資料夾、撰寫、列出、讀取、更新和搜尋資源。 此外，還了解如何建立資源關係、鎖定和刪除資源。
seo-description: Manage AEM Forms repository to create folders, write, list, read, update resources, and search resources using the Java API and Web Service API. In addition, learn how to create resource relationships, lock and delete resources.
uuid: 6ead49f9-ca0d-4ee4-86a6-0a9ced6ec4f8
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d2c95881-6c02-4e34-85af-84607df54287
role: Developer
exl-id: a07e51ca-fea0-4719-8071-1b7e805de2ae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '9117'
ht-degree: 0%

---

# 使用AEM Forms存放庫 {#working-with-aem-forms-repository}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於存放庫服務**

存放庫服務為AEM Forms提供資源儲存和管理服務。 開發人員建立 *AEM Forms* 應用程式中，使用者可將資產部署在存放庫中，而非檔案系統。 資產可以包括任何類型的宣傳品，包括XML表單、PDF forms(包括Acrobat表單)、表單片段、影像、配置檔案、策略、SWF檔案、DDX檔案、 XML結構、WSDL檔案和測試資料。

例如，請考量下列Forms應用程式名稱為 *應用程式/表單應用程式*:

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

請注意， FormsFolder中有一個名為Loan.xdp的檔案。 若要存取此表單設計，請指定完整路徑（包括版本）: `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.

>[!NOTE]
>
>如需使用Workbench建立Forms應用程式的相關資訊，請參閱 [Workbench說明](https://www.adobe.com/go/learn_aemforms_workbench_63).

位於AEM Forms存放庫中的資源路徑為：

`Applications/Application-name/Application-version/Folder.../Filename`

以下值顯示一些URI值的示例：

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>您可以使用網頁瀏覽器來瀏覽AEM Forms存放庫。 要瀏覽儲存庫，請在Web瀏覽器中輸入以下URL `https://[server name]:[server port]/repository`. 您可以使用網頁瀏覽器，驗證與使用AEM Forms存放庫區段相關聯的快速入門結果。 例如，如果將內容新增至AEM Forms存放庫，則可在網頁瀏覽器中查看內容。 (請參閱 [快速入門（SOAP模式）:使用Java API編寫資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api).)

存放庫API提供許多操作，可用來儲存和擷取存放庫中的資訊。 例如，您可以獲取資源清單，或在處理應用程式時需要資源時檢索儲存在儲存庫中的特定資源。

>[!NOTE]
>
>存放庫API無法用來與內容服務互動（已淘汰）。 若要與「內容服務」互動（已淘汰），請使用「檔案管理API」。

使用存放庫服務API，您可以完成下列工作：

* 建立檔案夾. 請參閱 [建立資料夾](aem-forms-repository.md#creating-folders).
* 編寫資源及其屬性。 請參閱 [編寫資源](aem-forms-repository.md#writing-resources).
* 列出指定集合中或與其他資源相關的資源。 請參閱 [列出資源](aem-forms-repository.md#listing-resources).
* 讀取資源及其屬性。 請參閱 [讀取資源](aem-forms-repository.md#reading-resources).
* 更新資源及其屬性。 請參閱 [更新資源](aem-forms-repository.md#updating-resources).
* 搜尋資源，包括其歷史記錄、相關資源和屬性。 請參閱 [搜尋資源](aem-forms-repository.md#searching-for-resources).
* 指定資源之間的關係。 請參閱 [建立資源關係](aem-forms-repository.md#creating-resource-relationships).
* 管理資源訪問控制，包括鎖定和解鎖資源，以及讀取和寫入訪問控制清單(ACL)。 請參閱 [鎖定資源](aem-forms-repository.md#locking-resources).
* 刪除資源及其屬性。 請參閱 [刪除資源](aem-forms-repository.md#deleting-resources).

>[!NOTE]
>
>使用儲存庫API時，無法使用ECM儲存庫管理資源訪問控制、搜索資源或指定資源關係。

>[!NOTE]
>
>加密的PDF寫入存放庫時，無法使用自動關係擷取功能。 否則，加密的PDF可儲存在儲存庫中，並稍後加以擷取。 從儲存庫中擷取PDF後，擷取器可以選擇將其解密。

>[!NOTE]
>
>如需存放庫服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 建立資料夾 {#creating-folders}

資料夾（資源集合）用於按有組織的分組儲存對象（檔案或資源）。 資料夾可以包含資源和其他資料夾，也稱為子資料夾。 資源一次只能儲存在一個資料夾中。

檔案從資料夾繼承訪問控制清單(ACL)，子資料夾從其父資料夾繼承ACL。 因此，必須存在父資料夾，然後才能建立子資料夾。 IDE僅允許您按資料夾進行交互，而不允許逐個檔案進行交互。 您無法對資料夾進行版本化，因此不需要這樣做；資料夾本身不包含資料。 相反地，它只是包含資料之資源的容器。 預設ACL是系統級權限，這意味著用戶必須具有系統級權限（讀取、寫入、遍歷、管理ACL），直到有人授予他們特定資料夾的權限。 ACL只能在IDE中工作。

>[!NOTE]
>
>如需存放庫服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

要建立資料夾，請執行以下步驟：

1. 包含專案檔案。
1. 建立服務客戶端。
1. 建立資料夾。
1. 將資料夾寫入儲存庫。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請包含代理檔案。

**建立服務客戶端**

在以寫程式方式建立資源集合之前，必須建立連接並提供憑據。 這可以通過建立服務客戶端來實現。

**建立資料夾**

調用Repository服務方法以建立資源集合，並使用標識資訊（包括其UUID、資料夾名稱和說明）填充資源集合。

**將資料夾寫入儲存庫**

調用Repository服務方法以編寫資源集合，指定目標資料夾的URI。

**另請參閱**

[使用Java API建立資料夾](aem-forms-repository.md#create-folders-using-the-java-api)

[使用網站服務API建立資料夾](aem-forms-repository.md#create-folders-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速入門](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API建立資料夾 {#create-folders-using-the-java-api}

使用儲存庫服務API(Java)建立資料夾：

1. 包含項目檔案

   在Java項目的類路徑中包含項目檔案。

1. 建立服務客戶端

   建立 `ResourceRepositoryClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 建立資料夾

   若要建立資源集合，您必須先建立 `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` 物件。

   叫用 `repositoryInfomodelFactoryBean` 物件 `newResourceCollection` 方法，並傳遞下列參數：

   * A `com.adobe.repository.infomodel.Id` 要指派給資源的UUID識別碼。
   * A `com.adobe.repository.infomodel.Lid` 要指派給資源的UUID識別碼。
   * A `java.lang.String` 包含資源集合的名稱。 例如， `FormsFolder`.

   方法會傳回 `com.adobe.repository.infomodel.bean.ResourceCollection` 代表新資料夾的物件。

   使用 `setDescription` 方法，並傳遞下列參數：

   * A `String` 說明資源集合。 在此範例中， `"test Folder"` 已使用 `.`


1. 將資料夾寫入儲存庫

   叫用 `ResourceRepositoryClient` 物件 `writeResource` 方法，並傳入資料夾和 `ResourceCollection` 物件。 例如，資料夾的URI可以是以下值 `/Applications/FormsApplication/1.0/`.

   方法會傳回新建立的例項 `com.adobe.repository.infomodel.bean.Resource` 物件。 例如，您可以借由叫用 `com.adobe.repository.infomodel.bean.Resource` 物件 `getId` 方法。

**另請參閱**

[建立資料夾](aem-forms-repository.md#creating-folders)

[快速入門（SOAP模式）:使用Java API建立資料夾](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API建立資料夾 {#create-folders-using-the-web-service-api}

使用存放庫服務API（Web服務）建立資料夾：

1. 包含項目檔案

   * 建立使用base64的儲存庫WSDL的Microsoft .NET客戶端程式集。
   * 參考Microsoft .NET客戶端程式集。

1. 建立服務客戶端

   使用Microsoft .NET客戶端程式集，建立 `RepositoryServiceService` 對象，方法是調用其預設建構子。 設定 `Credentials` 屬性使用 `System.Net.NetworkCredential` 包含用戶名和密碼的對象。

1. 建立資料夾

   使用 `ResourceCollection` 類別，並傳入下列參數：

   * 安 `Id` 對象，通過調用預設建構子來建立 `Id` 類並分配給 `Resource` 物件 `id` 欄位。
   * 安 `Lid` 對象，通過調用預設建構子來建立 `Lid` 類並分配給 `Resource` 物件 `lid` 欄位。
   * 包含資源集合名稱的字串，該名稱會指派給 `Resource` 物件 `name` 欄位。 此範例中使用的名稱為 `"testfolder"`.
   * 包含資源集合說明的字串，會指派給 `Resource` 物件 `description` 欄位。 此範例中使用的說明為 `"test folder"`.

1. 將資料夾寫入儲存庫

   叫用 `RepositoryServiceService` 物件 `writeResource` 方法，並傳遞下列參數：

   * 要建立資料夾的路徑。
   * 此 `ResourceCollection` 代表資料夾的物件。
   * 通過 `null` 的其他兩個參數。

**另請參閱**

[建立資料夾](aem-forms-repository.md#creating-folders)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 編寫資源 {#writing-resources}

您可以在存放庫的指定位置中建立資源。 自然檔案大小受資料庫限制和工作階段逾時限制。 對於預設配置，檔案限制為25 MB。 要提高或降低最大檔案大小，必須更改資料庫配置。

寫入資源等同於將資料儲存在儲存庫中。 將資源寫入儲存庫後，儲存庫生態系統中的所有客戶端都可以訪問該資源。 將資源（如XML架構、XDP檔案和XSD檔案）寫入儲存庫時，內容會根據MIME類型進行剖析。 如果支援MIME類型，則解析器確定是否與其他內容存在默示關係。 例如，如果階層式樣式表(CSS)有參考通用CSS的相對URL，您也應將通用CSS提交至存放庫。 兩個資源之間的關係被儲存為30天不可調整的待處理關係。 在30天內將通用CSS提交至存放庫時，會形成關係。

建立資源時，訪問控制清單(ACL)繼承自父資料夾。 根資料夾具有系統級權限，直到建立初始資源或資料夾為止，此時該資源或資料夾將獲得預設ACL權限。

您可以使用存放庫服務Java API或網站服務API，以程式設計方式撰寫資源。

>[!NOTE]
>
>如需存放庫服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-1}

要編寫資源，請執行以下步驟：

1. 包含專案檔案。
1. 建立儲存庫服務客戶端。
1. 指定要讀取的資源的URI。
1. 閱讀資源。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請包含代理檔案。

**建立服務客戶端**

在以寫程式方式讀取資源之前，您必須建立連接並提供憑據。 這可以通過建立服務客戶端來實現。

**指定資源的目標資料夾的URI**

建立包含要讀取之資源的URI的字串。 語法包含正斜線，如以下範例所示：&quot;/*路徑*/*資料夾*」。

**建立資源**

叫用存放庫服務方法以建立資源，並使用識別資訊（包括其UUID、資源名稱和說明）填入資源。

**指定資源內容**

調用Repository服務方法以建立資源內容，並將該內容儲存在資源中。

**將資源寫入目標資料夾**

調用Repository服務方法以寫入資源，指定目標資料夾的URI。

**另請參閱**

[使用Java API寫入資源](aem-forms-repository.md#write-resources-using-the-java-api)

[使用網站服務API寫入資源](aem-forms-repository.md#write-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速入門](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API寫入資源 {#write-resources-using-the-java-api}

使用存放庫服務API(Java)編寫資源：

1. 包含項目檔案

   在Java項目的類路徑中包含客戶端JAR檔案。

1. 建立服務客戶端

   建立 `ResourceRepositoryClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 指定資源的目標資料夾的URI

   指定資源的目標資料夾的URI。 在此情況下，因為資源名為 `testResource` 將儲存在名為的資料夾中 `testFolder`，資料夾的URI為 `"/testFolder"`. URI儲存為 `java.lang.String` 物件。

1. 建立資源

   若要建立資源，您必須先建立 `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` 物件。

   叫用 `RepositoryInfomodelFactoryBean` 物件 `newResource` 方法，它建立 `com.adobe.repository.infomodel.bean.Resource` 物件。 在此範例中，提供下列參數：

   * A `com.adobe.repository.infomodel.Id` 對象，通過調用預設建構子來建立 `Id` 類別。
   * A `com.adobe.repository.infomodel.Lid` 對象，通過調用預設建構子來建立 `Lid` 類別。
   * A `java.lang.String` 包含資源的檔案名。

   若要指定資源的說明，請叫用 `Resource` 物件 `setDescription` 方法，並傳遞包含說明的字串。 在此範例中，說明為 `"test resource"`.

1. 指定資源內容

   若要建立資源的內容，請叫用 `RepositoryInfomodelFactoryBean` 物件 `newResourceContent` 方法，返回 `com.adobe.repository.infomodel.bean.ResourceContent` 物件。 將內容新增至 `ResourceContent` 物件。 在此範例中，這是透過執行下列工作來完成：

   * 叫用 `ResourceContent` 物件 `setDataDocument` 方法 `com.adobe.idp.Document` 物件
   * 叫用 `ResourceContent` 物件 `setSize` 方法，並傳入 `Document` 物件

   叫用 `Resource` 物件 `setContent` 方法和傳遞 `ResourceContent` 物件。 如需詳細資訊，請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. 將資源寫入目標資料夾

   叫用 `ResourceRepositoryClient` 物件 `writeResource` 在資料夾的URI中傳遞的方法，以及 `Resource` 物件。

**另請參閱**

[編寫資源](aem-forms-repository.md#writing-resources)

[快速入門（SOAP模式）:使用Java API編寫資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API寫入資源 {#write-resources-using-the-web-service-api}

使用存放庫服務API（Web服務）編寫資源：

1. 包含項目檔案

   * 建立使用base64的儲存庫WSDL的Microsoft .NET客戶端程式集。
   * 參考Microsoft .NET客戶端程式集。

1. 建立服務客戶端

   使用Microsoft .NET客戶端程式集，建立 `RepositoryServiceService` 對象，方法是調用其預設建構子。 設定 `Credentials` 屬性使用 `System.Net.NetworkCredential` 包含用戶名和密碼的對象。

1. 指定資源的目標資料夾的URI

   指定資源的目標資料夾的URI。 在此情況下，因為資源名為 `testResource` 將儲存在名為的資料夾中 `testFolder`，資料夾的URI為 `"/testFolder"`. 使用與Microsoft .NET Framework（如C#）相容的語言時，請將URI儲存在 `System.String` 物件。

1. 建立資源

   要建立資源，請調用 `Resource` 類別。 在此範例中，下列資訊會儲存在 `Resource` 物件：

   * A `com.adobe.repository.infomodel.Id` 對象，通過調用預設建構子來建立 `Id` 類並分配給 `Resource` 物件 `id` 欄位。
   * A `com.adobe.repository.infomodel.Lid` 對象，通過調用預設建構子來建立 `Lid` 類並分配給 `Resource` 物件 `lid` 欄位。
   * 包含資源檔案名稱的字串，此名稱會指派給 `Resource` 物件 `name` 欄位。 此範例中使用的名稱為 `"testResource"`.
   * 包含資源說明的字串，會指派給 `Resource` 物件 `description` 欄位。 此範例中使用的說明為 `"test resource"`.

1. 指定資源內容

   要為資源建立內容，請調用 `ResourceContent` 類別。 然後將內容新增至 `ResourceContent` 物件。 在此範例中，這是透過執行下列工作來完成：

   * 指派 `BLOB` 包含文檔的對象 `ResourceContent` 物件 `dataDocument` 欄位。
   * 指派大小（以位元組為單位） `BLOB` 物件 `ResourceContent` 物件 `size` 欄位。

   指派 `ResourceContent` 物件 `Resource` 物件 `content` 欄位。

1. 將資源寫入目標資料夾

   叫用 `RepositoryServiceService` 物件 `writeResource` 在資料夾的URI中傳遞的方法，以及 `Resource` 物件。 通過 `null` 的其他兩個參數。

**另請參閱**

[編寫資源](aem-forms-repository.md#writing-resources)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 列出資源 {#listing-resources}

您可以列出資源，以探索資源。 系統會對儲存庫執行查詢，以尋找與指定資源集合相關的所有資源。

整理資源後，您就可以透過查看結構的特定分支來檢查您建立的結構，就像在作業系統中一樣。

上市資源按關係運作：資源是資料夾的成員。 成員由「成員」類型的關係表示。 在給定資料夾中列出資源時，將按「成員」關係查詢與給定資料夾相關的資源。 關係是方向的：關係的成員具有作為目標成員的源。 來源是資源；目標是父資料夾。

>[!NOTE]
>
>如需存放庫服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-2}

若要列出資源，請遵循下列步驟：

1. 包含專案檔案。
1. 建立服務客戶端。
1. 指定資料夾路徑。
1. 擷取資源清單。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請包含代理檔案。

**建立服務客戶端**

在以寫程式方式建立資源集合之前，必須建立連接並提供憑據。 這可以通過建立服務客戶端來實現。

**指定資料夾路徑**

建立包含資源之資料夾路徑的字串。 語法包含正斜線，如以下範例所示：&quot;/*路徑*/*資料夾*」。

**擷取資源清單**

調用Repository服務方法以檢索資源清單，指定目標資料夾的路徑。

**另請參閱**

[使用Java API列出資源](aem-forms-repository.md#list-resources-using-the-java-api)

[使用網站服務API列出資源](aem-forms-repository.md#list-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速入門](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API列出資源 {#list-resources-using-the-java-api}

使用儲存庫服務API(Java)列出資源：

1. 包含項目檔案

   在Java項目的類路徑中包含客戶端JAR檔案。

1. 建立服務客戶端

   建立 `ResourceRepositoryClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 指定資料夾路徑

   指定要查詢的資源集合的URI。 在此情況下，其URI為 `"/testFolder"`. URI儲存為 `java.lang.String` 物件。

1. 擷取資源清單

   叫用 `ResourceRepositoryClient` 物件 `listMembers` 方法，並傳遞資料夾的URI。

   方法會傳回 `java.util.List` of `com.adobe.repository.infomodel.bean.Resource` 作為 `com.adobe.repository.infomodel.bean.Relation` 類型 `Relation.TYPE_MEMBER_OF` 並將資源集合URI作為目標。 你可以反複一下 `List` 來擷取每個資源。 在此範例中，會顯示每個資源的名稱和說明。

**另請參閱**

[列出資源](aem-forms-repository.md#listing-resources).

[快速入門（SOAP模式）:使用Java API列出資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API列出資源 {#list-resources-using-the-web-service-api}

使用存放庫服務API（Web服務）列出資源：

1. 包含項目檔案

   * 建立會使用儲存庫WSDL的Microsoft .NET客戶端程式集。
   * 參考Microsoft .NET客戶端程式集。

1. 建立服務客戶端

   使用Microsoft .NET客戶端程式集，建立 `RepositoryServiceService` 對象，方法是調用其預設建構子。 設定 `Credentials` 屬性使用 `System.Net.NetworkCredential` 包含用戶名和密碼的對象。

1. 指定資料夾路徑

   指定包含要查詢的資料夾URI的字串。 在此情況下，其URI為 `"/testFolder"`. 使用與Microsoft .NET Framework（如C#）相容的語言時，請將URI儲存在 `System.String` 物件。

1. 擷取資源清單

   叫用 `RepositoryServiceService` 物件 `listMembers` 方法，並將資料夾的URI作為第一個參數傳遞。 通過 `null` 的其他兩個參數。

   方法會傳回物件陣列，可轉換為 `Resource` 對象。 您可以逐一查看物件陣列，以擷取每個相關資源。 在此範例中，會顯示每個資源的名稱和說明。

**另請參閱**

[列出資源](aem-forms-repository.md#listing-resources).

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 讀取資源 {#reading-resources}

您可以從存放庫中的指定位置擷取資源，以讀取其內容和中繼資料。 工作流程由初始化表單前端。 此程式具有讀取表單所需的所有權限。 系統會擷取資料表單，並從存放庫讀取內容。 存放庫會授予內容和中繼資料的存取權（即使知道資源存在的能力）。

存放庫有下列四種權限類型：

* **橫貫**:可讓您列出資源；即，讀取資源元資料，但不讀取資源內容
* **讀取**:可讓您讀取資源內容
* **寫入**:允許您寫入資源內容
* **管理訪問控制清單(ACL)**:允許您操作資源上的ACL

只有當用戶有權運行進程時，才能運行進程。 IDE用戶需要遍歷和讀取權限才能與儲存庫同步。 ACL僅在設計時應用，因為運行時發生在系統上下文中。

您可以使用存放庫服務Java API或網站服務API，以程式設計方式讀取資源。

>[!NOTE]
>
>如需存放庫服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-3}

若要讀取資源，請遵循下列步驟：

1. 包含專案檔案。
1. 建立儲存庫服務客戶端。
1. 指定要讀取的資源的URI。
1. 閱讀資源。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請包含代理檔案。

**建立服務客戶端**

在以寫程式方式讀取資源之前，您必須建立連接並提供憑據。 這可以通過建立服務客戶端來實現。

**指定要讀取的資源的URI**

建立包含要讀取之資源的URI的字串。 語法包含正斜線，如以下範例所示：&quot;/*路徑*/*資源*」。

**讀取資源**

調用儲存庫服務方法以讀取資源，指定URI。

**另請參閱**

[使用Java API讀取資源](aem-forms-repository.md#read-resources-using-the-java-api)

[使用網站服務API讀取資源](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速入門](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API讀取資源 {#read-resources-using-the-java-api}

使用存放庫服務API(Java)讀取資源：

1. 包含項目檔案

   在Java項目的類路徑中包含客戶端JAR檔案。

1. 建立服務客戶端

   建立 `ResourceRepositoryClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 指定要讀取的資源的URI

   指定表示要檢索的資源的URI的字串值。 例如，假設資源名為 *testResource* 位於名為 *testFolder*，指定 `/testFolder/testResource`.

1. 讀取資源

   叫用 `ResourceRepositoryClient` 物件 `readResource` 方法，並將資源的URI作為參數傳遞。 此方法會傳回 `Resource` 代表資源的例項。

**另請參閱**

[讀取資源](aem-forms-repository.md#reading-resources)

[快速入門（SOAP模式）:使用Java API讀取資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API讀取資源 {#reading-resources-using-the-web-service-api}

使用存放庫服務API（Web服務）讀取資源：

1. 包含項目檔案

   * 建立會使用儲存庫WSDL的Microsoft .NET客戶端程式集。 (請參閱 [建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)
   * 參考Microsoft .NET客戶端程式集。 (請參閱 [建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. 建立服務客戶端

   使用Microsoft .NET客戶端程式集，建立 `RepositoryServiceService` 對象，方法是調用其預設建構子。 設定 `Credentials` 屬性使用 `System.Net.NetworkCredential` 包含用戶名和密碼的對象。

1. 指定要讀取的資源的URI

   指定包含要檢索之資源URI的字串。 在此情況下，因為資源名為 `testResource` 位於名為的資料夾中 `testFolder`，其URI為 `"/testFolder/testResource"`. 使用與Microsoft .NET Framework（如C#）相容的語言時，請將URI儲存在 `System.String` 物件。

1. 讀取資源

   叫用 `RepositoryServiceService` 物件 `readResource` 方法，並將資源的URI作為第一個參數傳遞。 通過 `null` 的其他兩個參數。

**另請參閱**

[讀取資源](aem-forms-repository.md#reading-resources)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 更新資源 {#updating-resources}

您可以擷取和更新存放庫中的資源內容。 更新資源時，版本之間對這些資源的存取控制保持不變。 執行更新時，您可以選擇增加主要版本。 如果您不選擇增加主版本，則會自動更新次版本。

更新資源時，會根據指定的資源屬性建立新版本。 更新資源時，您需指定兩個重要參數：目標URI和包含所有更新元資料的資源實例。 請務必注意，如果您未變更指定屬性（例如名稱），在您傳入的例項中仍需要該屬性。 剖析內容時建立的關係會新增至特定版本，除非另有指定，否則不會轉送。

例如，如果您更新XDP檔案，且該檔案包含其他資源的參考，則這些額外的參考也會記錄下來。 假設form.xdp 1.0版有兩個外部參考：徽標和樣式表，然後您隨後更新form.xdp，因此它現在有三個引用：徽標、樣式表和方案檔案。 在更新期間，儲存庫會將第三個關係（到架構檔案）添加到其掛起關係表中。 一旦儲存庫中存在架構檔案，該關係就會自動形成。 不過，如果form.xdp 2.0版不再使用標誌，form.xdp 2.0版將不會與標誌有任何關係。

所有更新操作都是原子操作和事務操作。 例如，如果兩個用戶閱讀了相同的資源，並且兩個用戶都決定將1.0版更新為2.0版，則其中一個將成功，其中一個將失敗，則儲存庫的完整性將得到維護，並且兩個用戶都會收到確認成功或失敗的消息。 如果事務未提交，則在資料庫出現故障時將回滾，並且將根據應用程式伺服器超時或回滾。

您可以使用存放庫服務Java API或網站服務API，以程式設計方式更新資源。

>[!NOTE]
>
>如需存放庫服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-4}

若要更新資源，請執行下列步驟：

1. 包含專案檔案。
1. 建立儲存庫服務客戶端。
1. 擷取要更新的資源。
1. 更新資源。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請包含代理檔案。

**建立服務客戶端**

在以寫程式方式讀取資源之前，您必須建立連接並提供憑據。 這可以通過建立服務客戶端來實現。

**擷取要更新的資源**

閱讀資源。 如需詳細資訊，請參閱 [讀取資源](aem-forms-repository.md#reading-resources).

**更新資源**

在資源中設定新資訊並調用Repository服務方法以更新資源，指定URI、更新的資源以及如何更新版本資訊。

**另請參閱**

[使用Java API更新資源](aem-forms-repository.md#update-resources-using-the-java-api)

[使用網站服務API更新資源](aem-forms-repository.md#update-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速入門](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API更新資源 {#update-resources-using-the-java-api}

使用存放庫服務API(Java)更新資源：

1. 包含項目檔案

   在Java項目的類路徑中包含客戶端JAR檔案。

1. 建立服務客戶端

   建立 `ResourceRepositoryClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 擷取要更新的資源

   指定要檢索和讀取資源的資源的URI。 在此範例中，資源的URI為 `"/testFolder/testResource"`.

1. 更新資源

   更新 `Resource` 對象資訊。 在此範例中，若要更新說明，請叫用 `Resource` 物件 `setDescription` 方法，並將新說明字串作為參數傳遞。

   然後叫用 `ServiceClientFactory` 物件 `updateResource` 方法，並傳遞下列參數：

   * A `java.lang.String` 包含資源URI的對象。
   * 此 `Resource` 包含更新的資源資訊的對象。
   * A `boolean` 值指示是更新主版本還是次版本。 在此範例中，值為 `true` 會傳入，以指出主要版本將會增加。

**另請參閱**

[更新資源](aem-forms-repository.md#updating-resources)

[快速入門（SOAP模式）:使用Java API更新資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API更新資源 {#update-resources-using-the-web-service-api}

使用存放庫API（Web服務）更新資源：

1. 包含項目檔案

   * 建立會使用儲存庫WSDL的Microsoft .NET客戶端程式集。
   * 參考Microsoft .NET客戶端程式集。

1. 建立服務客戶端

   使用Microsoft .NET客戶端程式集，建立 `RepositoryServiceService` 對象，方法是調用其預設建構子。 設定 `Credentials` 屬性使用 `System.Net.NetworkCredential` 包含用戶名和密碼的對象。

1. 擷取要更新的資源

   指定要檢索的資源的URI並讀取資源。 在此範例中，資源的URI為 `"/testFolder/testResource"`. 如需詳細資訊，請參閱 [讀取資源](aem-forms-repository.md#reading-resources).

1. 更新資源

   更新 `Resource` 對象資訊。 在此範例中，若要更新說明，請為 `Resource` 物件 `description` 欄位。

1. 叫用 `RepositoryServiceService` 物件 `updateResource` 方法，並傳遞下列參數：

   * A `System.String` 包含資源URI的對象。
   * 此 `Resource` 包含更新的資源資訊的對象。
   * A `boolean` 值指示是更新主版本還是次版本。 在此範例中，值為 `true` 會傳入，以指出主要版本將會增加。
   * 通過 `null` ，取其餘兩個參數。

**另請參閱**

[更新資源](aem-forms-repository.md#updating-resources)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 搜尋資源 {#searching-for-resources}

您可以建構查詢，用於搜尋存放庫中的資源，包括歷史記錄、相關資源和屬性。

您可以擷取相關資源，以判斷表單及其片段之間的相依性。 例如，如果您有表單，便可判斷其使用的片段或外部資源。 如果您有影像，您也可以找出使用影像的表單。 您也可以使用根據屬性進行篩選來搜尋相關資源。 例如，您可以搜尋所有使用具有指定名稱的影像的表單，或尋找具有指定名稱的表單所使用的任何影像。 您也可以使用資源屬性進行搜尋。 例如，您可以執行查詢以尋找其名稱以指定字串開頭的所有表單或資源，該字串可能包含「%」和「_」萬用字元。 請記住，基於屬性的搜索不基於關係；這些搜尋是基於您對特定資源有特定知識的假設。

**查詢語句**

A *查詢* 包含一或多個以條件邏輯連結的陳述式。 A *語句* 由左操作數、運算子和右操作陣列成。 此外，還可以指定用於搜索結果的排序順序。 此 *排序順序* 包含與SQL等效的資訊 `ORDER BY` 子句和由元素組成，這些元素包含搜索所基於的屬性以及指示使用升序還是降序的值。

您可以使用Repository service Java API以程式設計方式搜尋資源。 目前無法使用網站服務API來搜尋資源。

**排序行為**

調用 `ResourceRepositoryClient` 物件 `searchProperties` 方法和指定排序順序。 例如，假設您建立了具有三個自訂屬性的資源，其中屬性名稱為 `name`, `secondName`，和 `asecondName`. 接下來，您在屬性名稱上建立排序順序元素，並設定 `ascending` 值 `true`.

然後您叫用 `ResourceRepositoryClient` 物件 `searchProperties` 方法，並以排序順序傳遞。 搜尋會傳回正確的資源，並包含三個屬性。 但是，屬性不會依屬性名稱排序。 系統會依新增順序傳回： `name`, `secondName`，和 `asecondName`.

>[!NOTE]
>
>如需存放庫服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-5}

若要搜尋資源，請依照下列步驟操作：

1. 包含專案檔案。
1. 建立儲存庫服務客戶端。
1. 指定搜索的目標資料夾。
1. 指定搜索中使用的屬性。
1. 建立搜索中使用的查詢。
1. 建立搜尋結果的排序順序。
1. 搜尋資源。
1. 從搜尋結果中擷取資源。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請包含代理檔案。

**建立服務客戶端**

在以寫程式方式讀取資源之前，您必須建立連接並提供憑據。 這可以通過建立服務客戶端來實現。

**指定搜索的目標資料夾**

建立一個字串，其中包含要從中執行搜索的基本路徑。 語法包含正斜線，如以下範例所示：&quot;/*路徑*/*資料夾*」。

**指定搜索中使用的屬性**

您可以根據資源中包含的屬性進行搜尋。 指定要對其執行搜索的屬性值。

**建立搜索中使用的查詢**

使用陳述式和條件來建構查詢。 每個語句將指定搜索的基礎屬性、要使用的條件以及要在搜索中使用的屬性值。

**建立搜索結果的排序順序**

排序順序由元素組成，每個元素都包含搜索中使用的一個屬性和一個值，該值指示是升序還是降序。

**搜尋資源**

使用資料夾、查詢和排序順序來搜尋資源。 此外，指示搜索的深度以及要返回的結果數的上限。

**從搜尋結果中擷取資源**

逐一查看返回的資源清單，並提取資訊以供進一步處理。

**另請參閱**

[使用Java API搜尋資源](aem-forms-repository.md#search-for-resources-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速入門](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API搜尋資源 {#search-for-resources-using-the-java-api}

使用Repository service API(Java)搜索資源：

1. 包含項目檔案

   在Java項目的類路徑中包含客戶端JAR檔案。

1. 建立服務客戶端

   建立 `ResourceRepositoryClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 指定搜索的目標資料夾

   指定要從中執行搜索的基本路徑的URI。 在此範例中，資源的URI為 `/testFolder`.

1. 指定搜索中使用的屬性

   指定要對其執行搜索的屬性的值。 屬性存在於 `com.adobe.repository.infomodel.bean.Resource` 物件。 在此範例中，將對name屬性進行搜尋；因此，a `java.lang.String` 包含 `Resource` 會使用物件的名稱，即 `testResource` 在這個情況下。

1. 建立搜索中使用的查詢

   若要建立查詢，請建立 `com.adobe.repository.query.Query` 對象，方法是調用 `Query` 類和向查詢添加語句。

   要建立語句，請調用 `com.adobe.repository.query.Query.Statement` 類別，並傳入下列參數：

   * 包含資源屬性常數的左操作數。 在此範例中，由於資源的名稱是作為搜尋的基礎，因此會使用靜態值 `Resource.ATTRIBUTE_NAME` 中所有規則的URL區段。
   * 包含用於搜尋屬性之條件的運算子。 運算子必須是 `Query.Statement` 類別。 在此範例中，靜態值 `Query.Statement.OPERATOR_BEGINS_WITH` 中所有規則的URL區段。
   * 包含要在其上執行搜索的屬性值的右操作數。 在此範例中，name屬性， `String` 包含值 `"testResource"`，則會使用。

   通過調用 `Query.Statement` 物件 `setNamespace` 方法，並傳遞 `com.adobe.repository.infomodel.bean.ResourceProperty` 類別。 在此範例中， `ResourceProperty.RESERVED_NAMESPACE_REPOSITORY` 中所有規則的URL區段。

   叫用 `Query` 物件 `addStatement` 方法和傳遞 `Query.Statement` 物件。

1. 建立搜索結果的排序順序

   若要指定搜尋結果中使用的排序順序，請建立 `com.adobe.repository.query.sort.SortOrder` 對象，方法是調用 `SortOrder` 類，並將元素添加到排序順序。

   要為排序順序建立元素，請為 `com.adobe.repository.query.sort.SortOrder.Element` 類別。 在此範例中，由於資源的名稱是作為搜尋的基礎，因此會使用靜態值 `Resource.ATTRIBUTE_NAME` 會作為第一個參數，且遞增順序( `boolean` 值 `true`)指定為第二個參數。

   叫用 `SortOrder` 物件 `addSortElement` 方法和傳遞 `SortOrder.Element` 物件。

1. 搜尋資源

   要搜索 `resources` 根據屬性屬性，調用 `ResourceRepositoryClient` 物件 `searchProperties` 方法，並傳遞下列參數：

   * A `String` 包含執行搜索的基路徑。 在這種情況下， `"/testFolder"` 中所有規則的URL區段。
   * 搜索中使用的查詢。
   * 搜尋的深度。 在這種情況下， `com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE` 用於指示要使用基本路徑及其所有資料夾。
   * 安 `int` 值指示要從中選擇未分頁結果集的第一行。 在此範例中， `0` 已指定。
   * 安 `int` 值表示要傳回的結果數上限。 在此範例中， `10` 已指定。
   * 搜索中使用的排序順序。

   方法會傳回 `java.util.List` of `Resource` 對象按指定的排序順序。

1. 從搜尋結果中擷取資源

   若要擷取搜尋結果中包含的資源，請逐一瀏覽 `List` 並將每個物件 `Resource` 以便提取其資訊。 在此範例中，會顯示每個資源的名稱。

**另請參閱**

[搜尋資源](aem-forms-repository.md#searching-for-resources)

[快速入門（SOAP模式）:使用Java API搜尋資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 建立資源關係 {#creating-resource-relationships}

您可以指定儲存庫中資源之間的關係。 有三種關係：

* **依賴**:資源依賴其他資源的關係，這表示儲存庫中需要所有相關資源。
* **成員資格（檔案系統）**:資源位於指定資料夾中的關係。
* **自訂**:您在資源之間指定的關係。 例如，如果某個資源已被取代，而另一個資源引入儲存庫中，則您可以指定自己的取代關係。

您可以建立自己的自訂關係。 例如，如果將HTML檔案儲存在儲存庫中，並且該檔案使用影像，則可以指定一個自定義關係，以將HTML檔案與影像相關（因為通常只有XML檔案與使用儲存庫定義的依賴關係的影像相關聯）。 自訂關係的另一個範例是，如果您想要以循環圖形結構（而非樹狀結構）建立存放庫的不同檢視。 您可以定義圓形圖和檢視器以周遊這些關係。 最後，您可以指出資源會取代另一個資源，即使這兩個資源完全不同。 在這種情況下，您可以在保留範圍之外定義關係類型，並在這兩個資源之間建立關係。 您的應用程式將是唯一能夠檢測和處理關係的客戶端，並且它可用於對該關係進行搜索。

您可以使用存放庫服務Java API或網站服務API，以程式設計方式指定資源之間的關係。

>[!NOTE]
>
>如需存放庫服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-6}

若要指定兩個資源之間的關係，請執行下列步驟：

1. 包含專案檔案。
1. 建立儲存庫服務客戶端。
1. 指定要關聯的資源的URI。
1. 建立關係。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請包含代理檔案。

**建立服務客戶端**

在以寫程式方式讀取資源之前，您必須建立連接並提供憑據。 這可以通過建立服務客戶端來實現。

**指定要關聯的資源的URI**

建立包含要相關資源的URI的字串。 語法包含正斜線，如以下範例所示：&quot;/*路徑*/*資源*」。

**建立關係**

調用儲存庫服務方法以建立並指定關係類型。

**另請參閱**

[使用Java API建立關係資源](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[使用Web服務API建立關係資源](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速入門](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API建立關係資源 {#create-relationship-resources-using-the-java-api}

使用Repository service Java API建立關係資源，執行下列任務：

1. 包含項目檔案

   在Java項目的類路徑中包含客戶端JAR檔案。

1. 建立服務客戶端

   建立 `ResourceRepositoryClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 指定要關聯的資源的URI

   指定要關聯的資源的URI。 在此案例中，因為資源已命名 `testResource1` 和 `testResource2` 和位於名為 `testFolder`，其URI為 `"/testFolder/testResource1"` 和 `"/testFolder/testResource2"`. URI儲存為 `java.lang.String` 對象。 在此示例中，資源首先寫入儲存庫，並且檢索其URI。 如需有關寫入資源的詳細資訊，請參閱 [編寫資源](aem-forms-repository.md#writing-resources).

1. 建立關係

   叫用 `ResourceRepositoryClient` 物件 `createRelationship` 方法，並傳遞下列參數：

   * 源資源的URI。
   * 目標資源的URI。
   * 關係的類型，此為 `com.adobe.repository.infomodel.bean.Relation` 類別。 在此示例中，通過指定值來建立依賴關係 `Relation.TYPE_DEPENDANT_OF`.
   * A `boolean` 指示目標資源是否自動更新到 `com.adobe.repository.infomodel.Id`基於新頭資源的標識符。 在此範例中，由於相依關係，因此值 `true` 已指定。

   您也可以叫用 `ResourceRepositoryClient` 物件 `getRelated` 方法，並傳遞下列參數：

   * 要為其檢索相關資源的資源的URI。 在此範例中，來源資源( `"/testFolder/testResource1"`)。
   * A `boolean` 值指示指定的資源是否為關係中的源資源。 在此範例中，值 `true` 已指定，因為此情況。
   * 關係類型，此為 `Relation` 類別。 在此示例中，通過使用先前使用的相同值來指定依賴關係： `Relation.TYPE_DEPENDANT_OF`.

   此 `getRelated` 方法傳回 `java.util.List` of `Resource` 可通過其迭代來檢索每個相關資源的對象，將包含在 `List` to `Resource` 就像你那樣。 在此範例中， `testResource2` 預計會位於傳回資源清單中。

**另請參閱**

[建立資源關係](aem-forms-repository.md#creating-resource-relationships)

[快速入門（SOAP模式）:使用Java API建立資源之間的關係](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API建立關係資源 {#create-relationship-resources-using-the-web-service-api}

使用存放庫API（Web服務）建立關係資源：

1. 包含項目檔案

   * 建立會使用儲存庫WSDL的Microsoft .NET客戶端程式集。
   * 參考Microsoft .NET客戶端程式集。

1. 建立服務客戶端

   使用Microsoft .NET客戶端程式集，建立 `RepositoryServiceService` 對象，方法是調用其預設建構子。 設定 `Credentials` 屬性使用 `System.Net.NetworkCredential` 包含用戶名和密碼的對象。

1. 指定要關聯的資源的URI

   指定要關聯的資源的URI。 在此案例中，因為資源已命名 `testResource1` 和 `testResource2` 和位於名為 `testFolder`，其URI為 `"/testFolder/testResource1"` 和 `"/testFolder/testResource2"`. 使用與Microsoft .NET Framework（如C#）相容的語言時，URI會儲存為 `System.String` 對象。 在此示例中，資源首先寫入儲存庫，並且檢索其URI。 如需有關寫入資源的詳細資訊，請參閱 [編寫資源](aem-forms-repository.md#writing-resources).

1. 建立關係

   叫用 `RepositoryServiceService` 物件 `createRelationship` 方法，並傳遞下列參數：

   * 源資源的URI。
   * 目標資源的URI。
   * 關係的類型。 在此示例中，通過指定值來建立依賴關係 `3`.
   * A `boolean` 值指示是否指定了關係類型。 在此範例中，值 `true` 已指定。
   * A `boolean` 指示目標資源是否自動更新到 `Id`基於新頭資源的標識符。 在此範例中，由於相依關係，因此值 `true` 已指定。
   * A `boolean` 值指示是否指定了目標頭。 在此範例中，值 `true` 已指定。
   * 通過 `null` ，以取得最後一個參數。

   您也可以叫用 `RepositoryServiceService` 物件 `getRelated` 方法，並傳遞下列參數：

   * 要為其檢索相關資源的資源的URI。 在此範例中，來源資源( `"/testFolder/testResource1"`)。
   * A `boolean` 值指示指定的資源是否為關係中的源資源。 在此範例中，值 `true` 已指定，因為此情況。
   * A `boolean` 值指示是否指定了源資源。 在此範例中，值 `true` 中所有規則的URL區段。
   * 包含關係類型的整數陣列。 在此示例中，通過在陣列中使用與先前使用相同的值來指定依賴關係： `3`.
   * 通過 `null` ，取其餘兩個參數。

   此 `getRelated` 方法會傳回可轉換為的物件陣列 `Resource` 物件，您可以透過物件反覆擷取每個相關資源。 在此範例中， `testResource2` 預計會位於傳回資源清單中。

**另請參閱**

[建立資源關係](aem-forms-repository.md#creating-resource-relationships)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 鎖定資源 {#locking-resources}

您可以鎖定資源或一組資源，供特定使用者專用或供多個使用者共用。 共用鎖定表示資源會發生什麼事，但不會阻止其他任何人對該資源採取行動。 共用鎖應視為信令機制。 專用鎖定表示鎖定資源的用戶將更改資源，而鎖定將確保在用戶不再需要訪問資源並釋放鎖定之前，其他人都不能更改。 如果儲存庫管理員解除了資源的鎖定，則該資源上的所有獨佔鎖定和共用鎖定將自動刪除。 此類型的動作適用於使用者不再可用且未解除鎖定資源的情況。

當資源鎖定時，當您檢視位於Workbench中的「資源」標籤時，會顯示鎖定圖示，如下圖所示。

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

您可以使用存放庫服務Java API或網站服務API，以程式設計方式控制對資源的存取。

>[!NOTE]
>
>如需存放庫服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-7}

若要鎖定和解除鎖定資源，請執行下列步驟：

1. 包含專案檔案。
1. 建立儲存庫服務客戶端。
1. 指定要鎖定的資源的URI。
1. 鎖定資源。
1. 檢索資源的鎖。
1. 解除鎖定資源

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請包含代理檔案。

**建立服務客戶端**

在以寫程式方式讀取資源之前，您必須建立連接並提供憑據。 這可以通過建立服務客戶端來實現。

**指定要鎖定的資源的URI**

建立包含要鎖定之資源URI的字串。 語法包含正斜線，如以下範例所示：&quot;/*路徑*/*資源*」。

**鎖定資源**

調用儲存庫服務方法以鎖定資源，指定URI、鎖定類型和鎖定深度。

**檢索資源的鎖**

調用Repository服務方法以檢索資源的鎖，指定URI。

**解除鎖定資源**

調用儲存庫服務方法以解鎖資源，指定URI。

**另請參閱**

[使用Java API鎖定資源](aem-forms-repository.md#lock-resources-using-the-java-api)

[使用Web服務API鎖定資源](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速入門](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API鎖定資源 {#lock-resources-using-the-java-api}

使用存放庫服務API(Java)鎖定資源：

1. 包含項目檔案

   在Java項目的類路徑中包含客戶端JAR檔案。

1. 建立服務客戶端

   建立 `ResourceRepositoryClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 指定要鎖定的資源的URI

   指定要鎖定的資源的URI。 在此情況下，因為資源名為 `testResource` 位於名為的資料夾中 `testFolder`，其URI為 `"/testFolder/testResource"`. URI儲存為 `java.lang.String` 物件。

1. 鎖定資源

   叫用 `ResourceRepositoryClient` 物件 `lockResource` 方法，並傳遞下列參數：

   * 資源的URI。
   * 鎖定範圍。 在此示例中，由於將鎖定資源以獨佔使用，因此將鎖定範圍指定為 `com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`.
   * 鎖定深度。 在此示例中，由於鎖定將僅應用於特定資源，且不適用其成員或子項，因此鎖定深度指定為 `Lock.DEPTH_ZERO`.

   >[!NOTE]
   >
   >的多載版本 `lockResource` 需要四個參數的方法會擲回例外狀況。 確保使用 `lockResource` 方法，需要三個參數，如本逐步說明所示。

1. 檢索資源的鎖

   叫用 `ResourceRepositoryClient` 物件 `getLocks` 方法，並將資源的URI作為參數傳遞。 該方法返回可迭代的鎖定對象清單。 在本示例中，通過調用每個鎖對象的 `getOwnerUserId`, `getDepth`，和 `getType` 方法。

1. 解除鎖定資源

   叫用 `ResourceRepositoryClient` 物件 `unlockResource` 方法，並將資源的URI作為參數傳遞。 如需詳細資訊，請參閱 [AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**另請參閱**

[鎖定資源](aem-forms-repository.md#locking-resources)

[快速入門（SOAP模式）:使用Java API鎖定資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API鎖定資源 {#lock-resources-using-the-web-service-api}

使用存放庫服務API（Web服務）鎖定資源：

1. 包含項目檔案

   * 建立使用Base64的儲存庫WSDL的Microsoft .NET客戶端程式集。
   * 參考Microsoft .NET客戶端程式集。

1. 建立服務客戶端

   使用Microsoft .NET客戶端程式集，建立 `RepositoryServiceService` 對象，方法是調用其預設建構子。 設定 `Credentials` 屬性使用 `System.Net.NetworkCredential` 包含用戶名和密碼的對象。

1. 指定要鎖定的資源的URI

   指定包含要鎖定之資源URI的字串。 在此情況下，因為資源名為 `testResource` 在資料夾中 `testFolder`，其URI為 `"/testFolder/testResource"`. 使用與Microsoft .NET Framework（如C#）相容的語言時，請將URI儲存在 `System.String` 物件。

1. 鎖定資源

   叫用 `RepositoryServiceService` 物件 `lockResource` 方法，並傳遞下列參數：

   * 資源的URI。
   * 鎖定範圍。 在此示例中，由於將鎖定資源以獨佔使用，因此將鎖定範圍指定為 `11`.
   * 鎖定深度。 在此示例中，由於鎖定將僅應用於特定資源，且不適用其成員或子項，因此鎖定深度指定為 `2`.
   * 安 `int` 值表示在鎖定過期之前的秒數。 在此範例中， `1000` 中所有規則的URL區段。
   * 通過 `null` ，以取得最後一個參數。

1. 檢索資源的鎖

   叫用 `RepositoryServiceService` 物件 `getLocks` 方法，並將資源的URI作為第一個參數傳遞，並 `null` 的第二個參數。 方法會傳回 `object` 包含陣列 `Lock` 可迭代的對象。 在本示例中，通過訪問每個對象來打印每個對象的鎖所有者、深度和範圍 `Lock` 物件 `ownerUserId`, `depth`，和 `type` 欄位。

1. 解除鎖定資源

   叫用 `RepositoryServiceService` 物件 `unlockResource` 方法，並將資源的URI作為第一個參數傳遞，並 `null` 的第二個參數。

**另請參閱**

[鎖定資源](aem-forms-repository.md#locking-resources)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 刪除資源 {#deleting-resources}

您可以使用存放庫服務Java API(SOAP)，以程式設計方式從存放庫中的指定位置刪除資源。

刪除資源時，刪除通常是永久的，但在某些情況下，ECM儲存庫可能會根據其歷史機制來儲存資源的版本。 因此，刪除資源時，務必確保您不再需要該資源。 刪除資源的常見原因包括需要增加資料庫中的可用空間。 您可以刪除資源的版本，但是，如果刪除，則必須指定資源標識符，而不是其邏輯標識符(LID)或路徑。 如果刪除資料夾，該資料夾中的所有內容（包括子資料夾和資源）都將自動刪除。

未刪除相關資源。 例如，如果您的表單使用logo.gif檔案，而您刪除logo.gif，則關係將儲存在掛起的關係表中。 另外，若要停用版本，請將最新版本的物件狀態設為停用。

刪除操作在ECM系統中不安全於事務。 例如，如果您嘗試刪除100個資源，而第50個資源的操作失敗，則前49個執行個體將被刪除，其餘的則不會刪除。 否則，預設行為為回退（非承諾）。

>[!NOTE]
>
>使用 `com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()` 方法與ECM儲存庫(EMC Documentum Content Server和IBM FileNet P8 Content Manager)一起使用時，如果某個指定資源的刪除失敗，則不會回退事務處理，這意味著無法刪除那些已刪除的檔案。

>[!NOTE]
>
>如需存放庫服務的詳細資訊，請參閱 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-8}

若要刪除資源，請執行下列步驟：

1. 包含專案檔案。
1. 建立儲存庫服務客戶端。
1. 指定要刪除的資源的URI。
1. 刪除資源。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用Web服務，請包含代理檔案。

**建立服務客戶端**

在以寫程式方式讀取資源之前，您必須建立連接並提供憑據。 這可以通過建立服務客戶端來實現。

**指定要刪除的資源的URI**

建立包含要刪除之資源的URI的字串。 語法包含正斜線，如以下範例所示：&quot;/*路徑*/*資源*」。 如果要刪除的資源是資料夾，刪除將是遞歸的。

**刪除資源**

調用Repository服務方法以刪除資源，指定URI。

**另請參閱**

[使用Java API刪除資源](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[使用網站服務API刪除資源](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速入門](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API(SOAP)刪除資源 {#delete-resources-using-the-java-api-soap}

使用存放庫API(Java)刪除資源：

1. 包含項目檔案

   在Java項目的類路徑中包含客戶端JAR檔案。

1. 建立服務客戶端

   建立 `ResourceRepositoryClient` 對象，使用其建構子並傳遞 `ServiceClientFactory` 包含連接屬性的對象。

1. 指定要刪除的資源的URI

   指定要檢索的資源的URI。 在此情況下，由於名為testResourceToBeDeleted的資源位於名為testFolder的資料夾中，因此其URI為 `/testFolder/testResourceToBeDeleted`. URI儲存為 `java.lang.String` 物件。 在此示例中，資源首先寫入儲存庫，並且檢索其URI。 如需有關寫入資源的詳細資訊，請參閱 [編寫資源](aem-forms-repository.md#writing-resources).

1. 刪除資源

   叫用 `ResourceRepositoryClient` 物件 `deleteResource` 方法，並將資源的URI作為參數傳遞。

**另請參閱**

[刪除資源](aem-forms-repository.md#deleting-resources)

[快速入門（SOAP模式）:使用Java API搜尋資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用網站服務API刪除資源 {#delete-resources-using-the-web-service-api}

使用存放庫API（Web服務）刪除資源：

1. 包含項目檔案

   * 建立使用Base64的儲存庫WSDL的Microsoft .NET客戶端程式集。
   * 參考Microsoft .NET客戶端程式集。

1. 建立服務客戶端

   使用Microsoft .NET客戶端程式集，建立 `RepositoryServiceService` 對象，方法是調用其預設建構子。 設定 `Credentials` 屬性使用 `System.Net.NetworkCredential` 包含用戶名和密碼的對象。

1. 指定要刪除的資源的URI

   指定要檢索的資源的URI。 在此情況下，因為資源名為 `testResourceToBeDeleted` 位於名為的資料夾中 `testFolder`，其URI為 `"/testFolder/testResourceToBeDeleted"`. 在此示例中，資源首先寫入儲存庫，並且檢索其URI。 如需有關寫入資源的詳細資訊，請參閱 [編寫資源](aem-forms-repository.md#writing-resources).

1. 刪除資源

   叫用 `RepositoryServiceService` 物件 `deleteResources` 方法和傳遞 `System.String` 包含資源URI作為第一個參數的陣列。 通過 `null` 的第二個參數。

**另請參閱**

[刪除資源](aem-forms-repository.md#deleting-resources)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
