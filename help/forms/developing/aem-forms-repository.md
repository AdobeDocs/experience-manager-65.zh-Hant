---
title: 使用AEM Forms Repository
seo-title: 使用AEM Forms Repository
description: 管理AEM Forms儲存庫，以使用Java API和Web Service API建立資料夾、寫入、列出、讀取、更新和搜尋資源。 此外，還要瞭解如何建立資源關係、鎖定和刪除資源。
seo-description: 管理AEM Forms儲存庫，以使用Java API和Web Service API建立資料夾、寫入、清單、讀取、更新資源及搜尋資源。 此外，還要瞭解如何建立資源關係、鎖定和刪除資源。
uuid: 6ead49f9-ca0d-4ee4-86a6-0a9ced6ec4f8
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d2c95881-6c02-4e34-85af-84607df54287
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '9157'
ht-degree: 0%

---


# 使用AEM Forms Repository {#working-with-aem-forms-repository}

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

**關於儲存庫服務**

Repository服務為AEM Forms提供資源儲存和管理服務。 當開發人員建立&#x200B;*AEM Forms*&#x200B;應用程式時，他們可以將資產部署在儲存庫中，而非檔案系統。 這些資產可以包含任何類型的文宣，包括XML表單、PDF表單（包括Acrobat表單）、表單片段、影像、描述檔、原則、SWF檔案、DDX檔案、XML架構、WSDL檔案和測試資料。

例如，請考慮以下名為&#x200B;*Applications/FormsApplication*&#x200B;的Forms應用程式：

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

請注意，FormsFolder中有一個名為Loan.xdp的檔案。 若要存取此表單設計，請指定完整路徑（包括版本）:`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。

>[!NOTE]
>
>有關使用Workbench建立Forms應用程式的資訊，請參閱[Workbench幫助](https://www.adobe.com/go/learn_aemforms_workbench_63)。

位於AEM Forms儲存庫中的資源路徑為：

`Applications/Application-name/Application-version/Folder.../Filename`

以下值顯示一些URI值的示例：

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>您可以使用網頁瀏覽器來瀏覽AEM Forms Repository。 要瀏覽儲存庫，請在Web瀏覽器中輸入以下URL `https://[server name]:[server port]/repository`。 您可以使用網頁瀏覽器來驗證與「使用AEM Forms Repository」（使用AEM Forms資料庫）區段關聯的快速啟動結果。 例如，如果您新增內容至AEM Forms Repository，您就可以在網頁瀏覽器中看到內容。 (請參閱[快速入門（SOAP模式）:使用Java API](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)編寫資源。)

儲存庫API提供了一些操作，可用來儲存和檢索儲存庫中的資訊。 例如，當處理應用程式時需要資源時，可以獲取資源清單或檢索儲存在儲存庫中的特定資源。

>[!NOTE]
>
>儲存庫API不能用於與Content Services交互（已過時）。 若要與Content Services互動（已過時），請使用「檔案管理API」。

使用儲存庫服務API，您可以完成以下任務：

* 建立資料夾。 請參閱[建立資料夾](aem-forms-repository.md#creating-folders)。
* 編寫資源及其屬性。 請參閱[編寫資源](aem-forms-repository.md#writing-resources)。
* 列出指定系列中的資源或與其他資源相關的資源。 請參閱[列出資源](aem-forms-repository.md#listing-resources)。
* 閱讀資源及其屬性。 請參閱[閱讀資源](aem-forms-repository.md#reading-resources)。
* 更新資源及其屬性。 請參閱[更新資源](aem-forms-repository.md#updating-resources)。
* 搜尋資源，包括其歷史記錄、相關資源和屬性。 請參閱[搜索資源](aem-forms-repository.md#searching-for-resources)。
* 指定資源之間的關係。 請參閱[建立資源關係](aem-forms-repository.md#creating-resource-relationships)。
* 管理資源訪問控制，包括鎖定和解鎖資源，以及讀取和寫入訪問控制清單(ACL)。 請參閱[鎖定資源](aem-forms-repository.md#locking-resources)。
* 刪除資源及其屬性。 請參閱[刪除資源](aem-forms-repository.md#deleting-resources)。

>[!NOTE]
>
>使用儲存庫API，您無法使用ECM儲存庫管理資源訪問控制、搜索資源或指定資源關係。

>[!NOTE]
>
>將加密的PDF寫入儲存庫時，無法使用自動關係提取功能。 否則，加密的PDF可以儲存在儲存庫中，稍後再擷取。 檢索器可以選擇在從儲存庫檢索PDF後對其進行解密。

>[!NOTE]
>
>有關Repository服務的詳細資訊，請參閱[ Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

## 建立資料夾{#creating-folders}

資料夾（資源集合）用於按有組織的組儲存對象（檔案或資源）。 資料夾可以包含資源和其他資料夾，也稱為子資料夾。 資源一次只能儲存在一個資料夾中。

檔案從資料夾繼承訪問控制清單(ACL)，子資料夾從其父資料夾繼承ACL。 因此，在建立子資料夾之前，父資料夾必須存在。 IDE僅允許您逐個資料夾進行交互，而不允許逐個檔案進行交互。 您無法對資料夾進行版本化，也無需這樣做；資料夾本身不包含資料。 相反，它只是包含資料之資源的容器。 預設ACL是系統級權限，這意味著用戶必須擁有系統級權限（讀取、寫入、遍歷、管理ACL），直到有人授予他們特定資料夾的權限。 ACL僅在IDE中工作。

>[!NOTE]
>
>有關Repository服務的詳細資訊，請參閱[ Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary-of-steps}摘要

要建立資料夾，請執行以下步驟：

1. 包含專案檔案。
1. 建立服務客戶端。
1. 建立資料夾。
1. 將資料夾寫入儲存庫。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請加入proxy檔案。

**建立服務客戶端**

在以寫程式方式建立資源集合之前，必須建立連接並提供憑據。 這是通過建立服務客戶端來實現的。

**建立資料夾**

調用Repository服務方法以建立資源收集，並使用標識資訊（包括其UUID、資料夾名稱和說明）填充資源收集。

**將資料夾寫入儲存庫**

調用Repository服務方法來寫入資源集合，指定目標資料夾的URI。

**另請參閱**

[使用Java API建立資料夾](aem-forms-repository.md#create-folders-using-the-java-api)

[使用web service API建立資料夾](aem-forms-repository.md#create-folders-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API {#create-folders-using-the-java-api}建立資料夾

使用儲存庫服務API(Java)建立資料夾：

1. 包含專案檔案

   將專案檔案加入Java專案的類別路徑中。

1. 建立服務客戶端

   使用其建構子並傳遞包含連接屬性的`ServiceClientFactory`對象，建立`ResourceRepositoryClient`對象。

1. 建立資料夾

   要建立資源集合，必須首先建立`com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`對象。

   叫用`repositoryInfomodelFactoryBean`物件的`newResourceCollection`方法，並傳入下列參數：

   * 要分配給資源的`com.adobe.repository.infomodel.Id` UUID標識符。
   * 要分配給資源的`com.adobe.repository.infomodel.Lid` UUID標識符。
   * 包含資源集合名稱的`java.lang.String`。 例如，`FormsFolder`。

   該方法返回表示新資料夾的`com.adobe.repository.infomodel.bean.ResourceCollection`對象。

   使用`setDescription`方法設定資料夾的說明，並傳入下列參數：

   * 描述資源集合的`String`。 在此範例中，`"test Folder"`是使用`.`


1. 將資料夾寫入儲存庫

   叫用`ResourceRepositoryClient`物件的`writeResource`方法，並傳入資料夾的URI和`ResourceCollection`物件。 例如，資料夾的URI可以是以下值`/Applications/FormsApplication/1.0/`。

   該方法返回新建立的`com.adobe.repository.infomodel.bean.Resource`對象的實例。 例如，您可以叫用`com.adobe.repository.infomodel.bean.Resource`物件的`getId`方法，以擷取新資源的識別碼值。

**另請參閱**

[建立資料夾](aem-forms-repository.md#creating-folders)

[快速入門（SOAP模式）:使用Java API建立資料夾](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#create-folders-using-the-web-service-api}建立資料夾

使用儲存庫服務API(web service)建立資料夾：

1. 包含專案檔案

   * 建立使用base64的儲存庫WSDL的Microsoft .NET客戶端元件。
   * 參考Microsoft .NET客戶端元件。

1. 建立服務客戶端

   使用Microsoft .NET客戶端元件，通過調用其預設建構子建立`RepositoryServiceService`對象。 使用包含用戶名和口令的`System.Net.NetworkCredential`對象設定其`Credentials`屬性。

1. 建立資料夾

   使用`ResourceCollection`類的預設建構子建立資料夾，並傳遞以下參數：

   * `Id`物件，此物件是透過為`Id`類別叫用預設建構函式並指派給`Resource`物件的`id`欄位來建立。
   * `Lid`物件，此物件是透過為`Lid`類別叫用預設建構函式並指派給`Resource`物件的`lid`欄位來建立。
   * 包含資源集合名稱的字串，此名稱會指派給`Resource`物件的`name`欄位。 此示例中使用的名稱為`"testfolder"`。
   * 包含資源集合說明的字串，該說明已分配給`Resource`對象的`description`欄位。 此示例中使用的說明為`"test folder"`。

1. 將資料夾寫入儲存庫

   叫用`RepositoryServiceService`物件的`writeResource`方法並傳入下列參數：

   * 要建立資料夾的路徑。
   * 代表資料夾的`ResourceCollection`對象。
   * 傳遞`null`作為其他兩個參數。

**另請參閱**

[建立資料夾](aem-forms-repository.md#creating-folders)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 編寫資源{#writing-resources}

您可以在儲存庫中的給定位置建立資源。 自然檔案大小受資料庫限制和作業逾時的限制。 在預設組態中，檔案限制為25 MB。 要提高或降低最大檔案大小，必須更改資料庫配置。

寫入資源等同於將資料儲存在儲存庫中。 將資源寫入儲存庫後，儲存庫生態系統中的所有客戶端都可以訪問該資源。 將資源（如XML架構、XDP檔案和XSD檔案）寫入儲存庫時，將根據MIME類型對內容進行解析。 如果支援MIME類型，解析器確定是否與其他內容存在默示關係。 例如，如果階層式樣式表(CSS)有參照通用CSS的相對URL，您也會將通用CSS送出至儲存庫。 兩個資源之間的關係被儲存為不可調整的30天期間的待處理關係。 在30天內將公用CSS提交到儲存庫時，將形成關係。

建立資源時，訪問控制清單(ACL)會從父資料夾繼承。 根資料夾具有系統級權限，直到建立初始資源或資料夾，此時該資源或資料夾將獲得預設ACL權限。

您可以使用Repository服務Java API或web service API以程式設計方式編寫資源。

>[!NOTE]
>
>有關Repository服務的詳細資訊，請參閱[ Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-1}摘要

要編寫資源，請執行以下步驟：

1. 包含專案檔案。
1. 建立儲存庫服務客戶端。
1. 指定要讀取的資源的URI。
1. 閱讀資源。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請加入proxy檔案。

**建立服務客戶端**

在以寫程式方式讀取資源之前，必須建立連接並提供憑據。 這是通過建立服務客戶端來實現的。

**為資源指定目標資料夾的URI**

建立包含要讀取的資源URI的字串。 語法包含正斜線，如本例所示：&quot;/*path*/*folder*&quot;。

**建立資源**

調用Repository服務方法建立資源，並使用標識資訊（包括其UUID、資源名稱和說明）填充資源。

**指定資源內容**

調用儲存庫服務方法以建立資源內容，並將該內容儲存在資源中。

**將資源寫入目標資料夾**

調用Repository服務方法來寫入資源，指定目標資料夾的URI。

**另請參閱**

[使用Java API寫入資源](aem-forms-repository.md#write-resources-using-the-java-api)

[使用web service API編寫資源](aem-forms-repository.md#write-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API {#write-resources-using-the-java-api}寫入資源

使用Repository服務API(Java)編寫資源：

1. 包含專案檔案

   在Java專案的類別路徑中加入用戶端JAR檔案。

1. 建立服務客戶端

   使用其建構子並傳遞包含連接屬性的`ServiceClientFactory`對象，建立`ResourceRepositoryClient`對象。

1. 為資源指定目標資料夾的URI

   為資源指定目標資料夾的URI。 在這種情況下，由於名為`testResource`的資源將儲存在名為`testFolder`的資料夾中，因此該資料夾的URI為`"/testFolder"`。 URI儲存為`java.lang.String`對象。

1. 建立資源

   要建立資源，必須首先建立`com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean`對象。

   叫用`RepositoryInfomodelFactoryBean`物件的`newResource`方法，此方法會建立`com.adobe.repository.infomodel.bean.Resource`物件。 在本範例中，提供下列參數：

   * `com.adobe.repository.infomodel.Id`對象，通過調用`Id`類的預設建構子建立。
   * `com.adobe.repository.infomodel.Lid`對象，通過調用`Lid`類的預設建構子建立。
   * 包含資源檔案名的`java.lang.String`。

   若要指定資源的說明，請叫用`Resource`物件的`setDescription`方法，並傳遞包含說明的字串。 在此示例中，說明為`"test resource"`。

1. 指定資源內容

   要為資源建立內容，請調用`RepositoryInfomodelFactoryBean`對象的`newResourceContent`方法，該方法返回`com.adobe.repository.infomodel.bean.ResourceContent`對象。 將內容新增至`ResourceContent`物件。 在此示例中，通過執行以下任務來完成此操作：

   * 調用`ResourceContent`物件的`setDataDocument`方法並傳入`com.adobe.idp.Document`物件
   * 調用`ResourceContent`物件的`setSize`方法，並傳入`Document`物件的大小（位元組）

   調用`Resource`物件的`setContent`方法並傳入`ResourceContent`物件，將內容新增至資源。 如需詳細資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

1. 將資源寫入目標資料夾

   叫用`ResourceRepositoryClient`物件的`writeResource`方法，並傳入資料夾的URI以及`Resource`物件。

**另請參閱**

[編寫資源](aem-forms-repository.md#writing-resources)

[快速入門（SOAP模式）:使用Java API編寫資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#write-resources-using-the-web-service-api}寫入資源

使用Repository服務API(web service)編寫資源：

1. 包含專案檔案

   * 建立使用base64的儲存庫WSDL的Microsoft .NET客戶端元件。
   * 參考Microsoft .NET客戶端元件。

1. 建立服務客戶端

   使用Microsoft .NET客戶端元件，通過調用其預設建構子建立`RepositoryServiceService`對象。 使用包含用戶名和口令的`System.Net.NetworkCredential`對象設定其`Credentials`屬性。

1. 為資源指定目標資料夾的URI

   為資源指定目標資料夾的URI。 在這種情況下，由於名為`testResource`的資源將儲存在名為`testFolder`的資料夾中，因此該資料夾的URI為`"/testFolder"`。 使用與Microsoft .NET Framework（例如C#）相容的語言時，將URI儲存在`System.String`對象中。

1. 建立資源

   要建立資源，請調用`Resource`類的預設建構子。 在此示例中，以下資訊儲存在`Resource`對象中：

   * `com.adobe.repository.infomodel.Id`物件，此物件是透過為`Id`類別叫用預設建構函式並指派給`Resource`物件的`id`欄位來建立。
   * `com.adobe.repository.infomodel.Lid`物件，此物件是透過為`Lid`類別叫用預設建構函式並指派給`Resource`物件的`lid`欄位來建立。
   * 包含資源檔案名的字串，該字串被分配給`Resource`對象的`name`欄位。 此示例中使用的名稱為`"testResource"`。
   * 包含資源說明的字串，此說明會指派給`Resource`物件的`description`欄位。 此示例中使用的說明為`"test resource"`。

1. 指定資源內容

   要為資源建立內容，請調用`ResourceContent`類的預設建構子。 然後，將內容新增至`ResourceContent`物件。 在此示例中，通過執行以下任務來完成此操作：

   * 將包含文檔的`BLOB`對象分配給`ResourceContent`對象的`dataDocument`欄位。
   * 為`ResourceContent`對象的`size`欄位分配`BLOB`對象的大小（以位元組為單位）。

   將`ResourceContent`物件指派至`Resource`物件的`content`欄位，將內容新增至資源。

1. 將資源寫入目標資料夾

   叫用`RepositoryServiceService`物件的`writeResource`方法，並傳入資料夾的URI以及`Resource`物件。 傳遞`null`作為其他兩個參數。

**另請參閱**

[編寫資源](aem-forms-repository.md#writing-resources)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 列出資源{#listing-resources}

您可以列出資源來發現資源。 對儲存庫執行查詢，以查找與給定資源集合相關的所有資源。

組織資源後，您就可以檢視結構的特定分支來檢查您建立的結構，就像在作業系統中一樣。

上市資源按關係經營：資源是資料夾的成員。 會籍由「會員」類型的關係所代表。 在指定資料夾中列出資源時，您正在按關係「成員」查詢與指定資料夾相關的資源。 關係是方向性的：關係的成員具有作為目標成員的源。 源頭是資源；目標是父資料夾。

>[!NOTE]
>
>有關Repository服務的詳細資訊，請參閱[ Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-2}摘要

要列出資源，請執行以下步驟：

1. 包含專案檔案。
1. 建立服務客戶端。
1. 指定資料夾路徑。
1. 檢索資源清單。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請加入proxy檔案。

**建立服務客戶端**

在以寫程式方式建立資源集合之前，必須建立連接並提供憑據。 這是通過建立服務客戶端來實現的。

**指定資料夾路徑**

建立包含資源資料夾路徑的字串。 語法包含正斜線，如本例所示：&quot;/*path*/*folder*&quot;。

**檢索資源清單**

調用儲存庫服務方法以檢索資源清單，指定目標資料夾的路徑。

**另請參閱**

[使用Java API列出資源](aem-forms-repository.md#list-resources-using-the-java-api)

[使用web service API列出資源](aem-forms-repository.md#list-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API {#list-resources-using-the-java-api}列出資源

使用Repository服務API(Java)列出資源：

1. 包含專案檔案

   在Java專案的類別路徑中加入用戶端JAR檔案。

1. 建立服務客戶端

   使用其建構子並傳遞包含連接屬性的`ServiceClientFactory`對象，建立`ResourceRepositoryClient`對象。

1. 指定資料夾路徑

   指定要查詢的資源集合的URI。 在這種情況下，其URI為`"/testFolder"`。 URI儲存為`java.lang.String`對象。

1. 檢索資源清單

   叫用`ResourceRepositoryClient`物件的`listMembers`方法並傳入資料夾的URI。

   該方法返回`com.adobe.repository.infomodel.bean.Resource`對象的`java.util.List`，該對象是`Relation.TYPE_MEMBER_OF`類型`com.adobe.repository.infomodel.bean.Relation`的源，並以資源收集URI為目標。 您可重複此`List`以檢索每個資源。 在此示例中，將顯示每個資源的名稱和說明。

**另請參閱**

[列出資源](aem-forms-repository.md#listing-resources)。

[快速入門（SOAP模式）:使用Java API列出資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#list-resources-using-the-web-service-api}列出資源

使用儲存庫服務API（web服務）列出資源：

1. 包含專案檔案

   * 建立一個使用儲存庫WSDL的Microsoft .NET客戶端元件。
   * 參考Microsoft .NET客戶端元件。

1. 建立服務客戶端

   使用Microsoft .NET客戶端元件，通過調用其預設建構子建立`RepositoryServiceService`對象。 使用包含用戶名和口令的`System.Net.NetworkCredential`對象設定其`Credentials`屬性。

1. 指定資料夾路徑

   指定包含要查詢的資料夾URI的字串。 在這種情況下，其URI為`"/testFolder"`。 使用與Microsoft .NET Framework（例如，C#）相容的語言時，將URI儲存在`System.String`對象中。

1. 檢索資源清單

   叫用`RepositoryServiceService`物件的`listMembers`方法，並將資料夾的URI傳入為第一個參數。 傳遞`null`作為其他兩個參數。

   該方法返回可以轉換到`Resource`對象的對象陣列。 您可以循環瀏覽對象陣列以檢索每個相關資源。 在此示例中，將顯示每個資源的名稱和說明。

**另請參閱**

[列出資源](aem-forms-repository.md#listing-resources)。

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 讀取資源{#reading-resources}

您可以從儲存庫中的給定位置檢索資源，以讀取其內容和元資料。 工作流由初始化表單作為前端。 此程式具有讀取表單所需的所有權限。 系統檢索資料表單並從儲存庫讀取內容。 儲存庫授予對內容和元資料的訪問權（甚至能夠知道資源存在）。

儲存庫具有以下四種權限類型：

* **traverse**:允許您列出資源；即，讀取資源元資料，但不讀取資源內容
* **閱讀**:允許您讀取資源內容
* **寫入**:允許您編寫資源內容
* **管理訪問控制清單(ACL)**:允許您操縱資源上的ACL

用戶只能在擁有運行進程的權限時運行進程。 IDE用戶需要遍歷和讀取權限才能與儲存庫同步。 ACL僅在設計時才適用，因為運行時是在系統上下文中進行的。

您可以使用Repository服務Java API或web service API以程式設計方式讀取資源。

>[!NOTE]
>
>有關Repository服務的詳細資訊，請參閱[ Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-3}摘要

要讀取資源，請執行以下步驟：

1. 包含專案檔案。
1. 建立儲存庫服務客戶端。
1. 指定要讀取的資源的URI。
1. 閱讀資源。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請加入proxy檔案。

**建立服務客戶端**

在以寫程式方式讀取資源之前，必須建立連接並提供憑據。 這是通過建立服務客戶端來實現的。

**指定要讀取的資源的URI**

建立包含要讀取的資源URI的字串。 語法包含正斜線，如本例所示：&quot;/*path*/*resource*&quot;。

**閱讀資源**

調用Repository服務方法讀取資源，指定URI。

**另請參閱**

[使用Java API讀取資源](aem-forms-repository.md#read-resources-using-the-java-api)

[使用web service API讀取資源](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API {#read-resources-using-the-java-api}讀取資源

使用Repository服務API(Java)讀取資源：

1. 包含專案檔案

   在Java專案的類別路徑中加入用戶端JAR檔案。

1. 建立服務客戶端

   使用其建構子並傳遞包含連接屬性的`ServiceClientFactory`對象，建立`ResourceRepositoryClient`對象。

1. 指定要讀取的資源的URI

   指定代表要檢索的資源URI的字串值。 例如，假設資源名為&#x200B;*testResource*（位於名為&#x200B;*testFolder*&#x200B;的資料夾中），請指定`/testFolder/testResource`。

1. 閱讀資源

   調用`ResourceRepositoryClient`物件的`readResource`方法，並將資源的URI作為參數傳遞。 此方法返回表示資源的`Resource`實例。

**另請參閱**

[閱讀資源](aem-forms-repository.md#reading-resources)

[快速入門（SOAP模式）:使用Java API讀取資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#reading-resources-using-the-web-service-api}讀取資源

使用Repository服務API(web service)讀取資源：

1. 包含專案檔案

   * 建立一個使用儲存庫WSDL的Microsoft .NET客戶端元件。 （請參閱[建立使用Base64編碼的。NET客戶端元件。）](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
   * 參考Microsoft .NET客戶端元件。 （請參閱[建立使用Base64編碼的。NET客戶端元件。）](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

1. 建立服務客戶端

   使用Microsoft .NET客戶端元件，通過調用其預設建構子建立`RepositoryServiceService`對象。 使用包含用戶名和口令的`System.Net.NetworkCredential`對象設定其`Credentials`屬性。

1. 指定要讀取的資源的URI

   指定包含要檢索的資源URI的字串。 在這種情況下，由於名為`testResource`的資源位於名為`testFolder`的資料夾中，因此其URI為`"/testFolder/testResource"`。 使用與Microsoft .NET Framework（例如C#）相容的語言時，將URI儲存在`System.String`對象中。

1. 閱讀資源

   叫用`RepositoryServiceService`物件的`readResource`方法，並將資源的URI傳遞為第一個參數。 傳遞`null`作為其他兩個參數。

**另請參閱**

[閱讀資源](aem-forms-repository.md#reading-resources)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 更新資源{#updating-resources}

您可以檢索和更新儲存庫中的資源內容。 更新資源時，這些資源的訪問控制在版本之間保持不變。 執行更新時，您可以選擇增加主要版本。 如果您不選擇增加主要版本，次要版本會自動更新。

更新資源時，將根據指定的資源屬性建立新版本。 在更新資源時，可以指定兩個重要參數：目標URI和包含所有更新元資料的資源實例。 請務必注意，如果您未變更指定屬性（例如，名稱），則在您傳入的例項中仍需要該屬性。 解析內容時建立的關係會新增至特定版本，除非指定，否則不會前移。

例如，如果您更新XDP檔案，且其中包含其他資源的參考，則也會記錄這些額外的參考。 假設form.xdp 1.0版有兩個外部參照：標誌和樣式表，您隨後會更新form.xdp，以便現在有三個參照：標誌、樣式表和架構檔案。 在更新期間，儲存庫將將第三個關係（到架構檔案）添加到其暫掛關係表。 當架構檔案存在於儲存庫中時，將自動形成關係。 不過，如果form.xdp 2.0版不再使用標誌，form.xdp 2.0版將不會與標誌有任何關係。

所有更新操作都是原子操作和事務操作。 例如，如果兩個用戶讀取了相同的資源，並決定將1.0版更新為2.0版，則其中一個將成功，而另一個將失敗，則儲存庫的完整性將得到維護，並且兩個用戶都將收到確認成功或失敗的消息。 如果事務未提交，則在資料庫出現故障時將回退，並根據應用程式伺服器超時或回退。

您可以使用Repository服務Java API或web service API，以程式設計方式更新資源。

>[!NOTE]
>
>有關Repository服務的詳細資訊，請參閱[ Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-4}摘要

要更新資源，請執行以下步驟：

1. 包含專案檔案。
1. 建立儲存庫服務客戶端。
1. 檢索要更新的資源。
1. 更新資源。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請加入proxy檔案。

**建立服務客戶端**

在以寫程式方式讀取資源之前，必須建立連接並提供憑據。 這是通過建立服務客戶端來實現的。

**檢索要更新的資源**

閱讀資源。 如需詳細資訊，請參閱[閱讀資源](aem-forms-repository.md#reading-resources)。

**更新資源**

在資源中設定新資訊並調用儲存庫服務方法以更新資源，指定URI、更新的資源以及版本資訊的更新方式。

**另請參閱**

[使用Java API更新資源](aem-forms-repository.md#update-resources-using-the-java-api)

[使用web service API更新資源](aem-forms-repository.md#update-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API {#update-resources-using-the-java-api}更新資源

使用Repository服務API(Java)更新資源：

1. 包含專案檔案

   在Java專案的類別路徑中加入用戶端JAR檔案。

1. 建立服務客戶端

   使用其建構子並傳遞包含連接屬性的`ServiceClientFactory`對象，建立`ResourceRepositoryClient`對象。

1. 檢索要更新的資源

   指定要檢索和讀取資源的資源的URI。 在此示例中，資源的URI為`"/testFolder/testResource"`。

1. 更新資源

   更新`Resource`物件的資訊。 在此範例中，若要更新說明，請叫用`Resource`物件的`setDescription`方法，並將新的說明字串傳遞為參數。

   然後叫用`ServiceClientFactory`物件的`updateResource`方法，並傳入下列參數：

   * 包含資源URI的`java.lang.String`物件。
   * `Resource`對象包含更新的資源資訊。
   * 一個`boolean`值，指示要更新主版還是次版。 在此範例中，會傳入`true`值，以指出主要版本將會增加。

**另請參閱**

[更新資源](aem-forms-repository.md#updating-resources)

[快速入門（SOAP模式）:使用Java API更新資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#update-resources-using-the-web-service-api}更新資源

使用Repository API(web service)更新資源：

1. 包含專案檔案

   * 建立一個使用儲存庫WSDL的Microsoft .NET客戶端元件。
   * 參考Microsoft .NET客戶端元件。

1. 建立服務客戶端

   使用Microsoft .NET客戶端元件，通過調用其預設建構子建立`RepositoryServiceService`對象。 使用包含用戶名和口令的`System.Net.NetworkCredential`對象設定其`Credentials`屬性。

1. 檢索要更新的資源

   指定要檢索並讀取資源的資源的URI。 在此示例中，資源的URI為`"/testFolder/testResource"`。 如需詳細資訊，請參閱[閱讀資源](aem-forms-repository.md#reading-resources)。

1. 更新資源

   更新`Resource`物件的資訊。 在此範例中，若要更新說明，請為`Resource`物件的`description`欄位指派新值。

1. 叫用`RepositoryServiceService`物件的`updateResource`方法，並傳入下列參數：

   * 包含資源URI的`System.String`物件。
   * `Resource`對象包含更新的資源資訊。
   * 一個`boolean`值，指示要更新主版還是次版。 在此範例中，會傳入`true`值，以指出主要版本將會增加。
   * 傳遞`null`以取得其餘兩個參數。

**另請參閱**

[更新資源](aem-forms-repository.md#updating-resources)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 搜索資源{#searching-for-resources}

您可以構建用於搜索儲存庫中資源的查詢，包括歷史記錄、相關資源和屬性。

您可以檢索相關資源以確定表單及其片段之間的相關性。 例如，如果您有表單，您可以決定它使用的片段或外部資源。 如果您有影像，您也可以瞭解哪些表格使用影像。 您也可以使用根據屬性的篩選來搜尋相關資源。 例如，您可以搜尋使用指定名稱之影像的所有表單，或尋找具有指定名稱之表單使用的任何影像。 您也可以使用資源屬性進行搜索。 例如，您可以執行查詢，以查找其名稱以指定字串開頭的所有表單或資源，該字串可能包括「%」和「_」通配符。 請記住，基於屬性的搜索並非基於關係；此類搜索基於您對給定資源有特定知識的假設。

**查詢語句**

*query*&#x200B;包含一或多個與條件邏輯連接的語句。 *語句*&#x200B;由左操作數、運算子和右操作陣列成。 此外，您還可以指定用於搜尋結果的排序順序。 *排序順序*&#x200B;包含與SQL `ORDER BY`子句等效的資訊，並由包含搜索所基於屬性的元素以及指示使用升序或降序的值組成。

您可以使用Repository服務Java API，以程式設計方式搜索資源。 目前，無法使用web service API來搜尋資源。

**排序行為**

調用`ResourceRepositoryClient`物件的`searchProperties`方法並指定排序順序時，排序順序不受尊重。 例如，假設您建立了具有三個自定義屬性的資源，其中屬性名為`name`、`secondName`和`asecondName`。 接著，您在屬性名稱上建立排序順序元素，並將`ascending`值設定為`true`。

然後，您會叫用`ResourceRepositoryClient`物件的`searchProperties`方法，並依排序順序傳遞。 搜索返回具有三個屬性的正確資源。 但是，屬性不按屬性名稱排序。 它們會依新增順序傳回：`name`、`secondName`和`asecondName`。

>[!NOTE]
>
>有關Repository服務的詳細資訊，請參閱[ Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-5}摘要

要搜索資源，請執行以下步驟：

1. 包含專案檔案。
1. 建立儲存庫服務客戶端。
1. 指定搜尋的目標資料夾。
1. 指定搜尋中使用的屬性。
1. 建立搜索中使用的查詢。
1. 建立搜尋結果的排序順序。
1. 搜尋資源。
1. 從搜索結果中檢索資源。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請加入proxy檔案。

**建立服務客戶端**

在以寫程式方式讀取資源之前，必須建立連接並提供憑據。 這是通過建立服務客戶端來實現的。

**指定搜尋的目標資料夾**

建立包含執行搜索的基本路徑的字串。 語法包含正斜線，如本例所示：&quot;/*path*/*folder*&quot;。

**指定搜尋中使用的屬性**

您可以根據資源中包含的屬性進行搜索。 指定要對其執行搜索的屬性值。

**建立搜索中使用的查詢**

使用語句和條件構建查詢。 每個語句將指定搜索的基礎屬性、要使用的條件以及要在搜索中使用的屬性值。

**建立搜尋結果的排序順序**

排序順序由元素組成，每個元素包含搜索中使用的屬性之一和指示使用遞增或遞減順序的值。

**搜尋資源**

使用資料夾、查詢和排序順序搜尋資源。 此外，請指出搜尋的深度以及要傳回結果數的上限。

**從搜索結果中檢索資源**

重複返回的資源清單並提取資訊以供進一步處理。

**另請參閱**

[使用Java API搜尋資源](aem-forms-repository.md#search-for-resources-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API {#search-for-resources-using-the-java-api}搜尋資源

使用儲存庫服務API(Java)搜索資源：

1. 包含專案檔案

   在Java專案的類別路徑中加入用戶端JAR檔案。

1. 建立服務客戶端

   使用其建構子並傳遞包含連接屬性的`ServiceClientFactory`對象，建立`ResourceRepositoryClient`對象。

1. 指定搜尋的目標資料夾

   指定要執行搜索的基本路徑的URI。 在此示例中，資源的URI為`/testFolder`。

1. 指定搜尋中使用的屬性

   指定要對其執行搜索的屬性的值。 屬性存在於`com.adobe.repository.infomodel.bean.Resource`對象中。 在本例中，將對name屬性進行搜索；因此，會使用包含`Resource`物件名稱的`java.lang.String`，在本例中為`testResource`。

1. 建立搜索中使用的查詢

   要建立查詢，請通過調用`Query`類的預設建構子建立`com.adobe.repository.query.Query`對象，並向查詢添加語句。

   要建立語句，請調用`com.adobe.repository.query.Query.Statement`類的建構子並傳遞以下參數：

   * 包含資源屬性常數的左操作數。 在此範例中，由於資源的名稱是搜尋的基礎，因此會使用靜態值`Resource.ATTRIBUTE_NAME`。
   * 包含用於搜索屬性的條件的運算子。 運算子必須是`Query.Statement`類中的靜態常數之一。 在此示例中，使用靜態值`Query.Statement.OPERATOR_BEGINS_WITH`。
   * 包含用於執行搜索的屬性值的右操作數。 在此示例中，使用名稱屬性`String`，該屬性包含值`"testResource"`。

   調用`Query.Statement`物件的`setNamespace`方法並傳入`com.adobe.repository.infomodel.bean.ResourceProperty`類別中包含的其中一個靜態值，以指定左側運算元的命名空間。 在此範例中，使用`ResourceProperty.RESERVED_NAMESPACE_REPOSITORY`。

   調用`Query`物件的`addStatement`方法並傳入`Query.Statement`物件，將每個陳述式新增至查詢。

1. 建立搜尋結果的排序順序

   要指定搜索結果中使用的排序順序，請通過調用`SortOrder`類的預設建構子建立`com.adobe.repository.query.sort.SortOrder`對象，並將元素添加到排序順序。

   要為排序順序建立元素，請調用`com.adobe.repository.query.sort.SortOrder.Element`類的一個建構子。 在此範例中，由於資源的名稱是搜尋的基礎，因此靜態值`Resource.ATTRIBUTE_NAME`是第一個參數，而遞增順序（`boolean`值`true`）是指定為第二個參數。

   調用`SortOrder`物件的`addSortElement`方法並傳入`SortOrder.Element`物件，將每個元素新增至排序順序。

1. 搜尋資源

   若要根據屬性屬性搜尋`resources`，請叫用`ResourceRepositoryClient`物件的`searchProperties`方法並傳入下列參數：

   * `String`包含執行搜索的基本路徑。 在這種情況下，使用`"/testFolder"`。
   * 搜索中使用的查詢。
   * 搜尋深度。 在這種情況下，`com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE`用於指示將使用基本路徑及其所有資料夾。
   * `int`值，指示要從中選擇未分頁結果集的第一行。 在此示例中，指定了`0`。
   * 一個`int`值，指示要返回的最大結果數。 在此示例中，指定了`10`。
   * 搜索中使用的排序順序。

   該方法以指定的排序順序返回`Resource`對象的`java.util.List`。

1. 從搜索結果中檢索資源

   要檢索搜索結果中包含的資源，請循環瀏覽`List`並將每個對象轉換到`Resource`以提取其資訊。 在此示例中，將顯示每個資源的名稱。

**另請參閱**

[搜索資源](aem-forms-repository.md#searching-for-resources)

[快速入門（SOAP模式）:使用Java API搜尋資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 建立資源關係{#creating-resource-relationships}

您可以指定儲存庫中資源之間的關係。 有三種關係：

* **依賴**:資源依賴於其他資源的關係，這意味著儲存庫中需要所有相關資源。
* **會籍（檔案系統）**:資源位於給定資料夾中的關係。
* **自訂**:您在資源之間指定的關係。例如，如果一個資源已過時，而另一個資源已引入儲存庫，則可以指定您自己的替換關係。

您可以建立自己的自訂關係。 例如，如果將HTML檔案儲存在儲存庫中，並且它使用影像，則可以指定將HTML檔案與影像關聯的自定義關係（因為通常只有XML檔案與使用儲存庫定義的依賴關係的影像關聯）。 自定義關係的另一個示例是，如果希望使用循環圖結構而不是樹結構來構建儲存庫的不同視圖。 您可以定義圓形圖和檢視器來遍歷這些關係。 最後，您可以指出資源會取代另一個資源，即使兩個資源完全不同。 在這種情況下，您可以定義保留範圍以外的關係類型，並在這兩個資源之間建立關係。 您的應用程式將是唯一可偵測和處理關係的用戶端，而且可用來搜尋該關係。

您可以使用Repository服務Java API或web service API，以程式設計方式指定資源之間的關係。

>[!NOTE]
>
>有關Repository服務的詳細資訊，請參閱[ Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-6}摘要

要指定兩個資源之間的關係，請執行以下步驟：

1. 包含專案檔案。
1. 建立儲存庫服務客戶端。
1. 指定要關聯的資源的URI。
1. 建立關係。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請加入proxy檔案。

**建立服務客戶端**

在以寫程式方式讀取資源之前，必須建立連接並提供憑據。 這是通過建立服務客戶端來實現的。

**指定要關聯的資源的URI**

建立包含要關聯的資源的URI的字串。 語法包含正斜線，如本例所示：&quot;/*path*/*resource*&quot;。

**建立關係**

調用儲存庫服務方法以建立並指定關係類型。

**另請參閱**

[使用Java API建立關係資源](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[使用web service API建立關係資源](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API {#create-relationship-resources-using-the-java-api}建立關係資源

使用Repository服務Java API建立關係資源，執行以下任務：

1. 包含專案檔案

   在Java專案的類別路徑中加入用戶端JAR檔案。

1. 建立服務客戶端

   使用其建構子並傳遞包含連接屬性的`ServiceClientFactory`對象，建立`ResourceRepositoryClient`對象。

1. 指定要關聯的資源的URI

   指定要關聯的資源的URI。 在這種情況下，由於資源名為`testResource1`和`testResource2`，並位於名為`testFolder`的資料夾中，因此其URI為`"/testFolder/testResource1"`和`"/testFolder/testResource2"`。 URI儲存為`java.lang.String`對象。 在此示例中，資源首先寫入儲存庫，並檢索其URI。 有關編寫資源的詳細資訊，請參閱[編寫資源](aem-forms-repository.md#writing-resources)。

1. 建立關係

   叫用`ResourceRepositoryClient`物件的`createRelationship`方法並傳入下列參數：

   * 源資源的URI。
   * 目標資源的URI。
   * 關係類型，它是`com.adobe.repository.infomodel.bean.Relation`類中的靜態常數之一。 在此示例中，通過指定值`Relation.TYPE_DEPENDANT_OF`來建立依賴關係。
   * 一個`boolean`值，指示是否將目標資源自動更新為新頭資源的基於`com.adobe.repository.infomodel.Id`的標識符。 在此示例中，由於依賴關係，指定值`true`。

   您也可以叫用`ResourceRepositoryClient`物件的`getRelated`方法並傳入下列參數，以擷取特定資源的相關資源清單：

   * 要為其檢索相關資源的資源的URI。 在此示例中，指定了源資源(`"/testFolder/testResource1"`)。
   * `boolean`值，指示指定的資源是否是關係中的源資源。 在此示例中，指定值`true`，因為此情況。
   * 關係類型，它是`Relation`類中的靜態常數之一。 在此示例中，通過使用先前使用的相同值來指定從屬關係：`Relation.TYPE_DEPENDANT_OF`。

   `getRelated`方法返回`Resource`對象的`java.util.List`，通過對象可循環檢索每個相關資源，並將`List`中包含的對象按順序傳送到`Resource`。 在此示例中，`testResource2`應該位於返回的資源清單中。

**另請參閱**

[建立資源關係](aem-forms-repository.md#creating-resource-relationships)

[快速入門（SOAP模式）:使用Java API建立資源之間的關係](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#create-relationship-resources-using-the-web-service-api}建立關係資源

使用Repository API(web service)建立關係資源：

1. 包含專案檔案

   * 建立一個使用儲存庫WSDL的Microsoft .NET客戶端元件。
   * 參考Microsoft .NET客戶端元件。

1. 建立服務客戶端

   使用Microsoft .NET客戶端元件，通過調用其預設建構子建立`RepositoryServiceService`對象。 使用包含用戶名和口令的`System.Net.NetworkCredential`對象設定其`Credentials`屬性。

1. 指定要關聯的資源的URI

   指定要關聯的資源的URI。 在這種情況下，由於資源名為`testResource1`和`testResource2`，並位於名為`testFolder`的資料夾中，因此其URI為`"/testFolder/testResource1"`和`"/testFolder/testResource2"`。 使用與Microsoft .NET Framework（例如，C#）相容的語言時，URI將儲存為`System.String`對象。 在此示例中，資源首先寫入儲存庫，並檢索其URI。 有關編寫資源的詳細資訊，請參閱[編寫資源](aem-forms-repository.md#writing-resources)。

1. 建立關係

   叫用`RepositoryServiceService`物件的`createRelationship`方法並傳入下列參數：

   * 源資源的URI。
   * 目標資源的URI。
   * 關係類型。 在此示例中，通過指定值`3`來建立依賴關係。
   * 一個`boolean`值，指示是否已指定關係類型。 在此示例中，指定了值`true`。
   * 一個`boolean`值，指示是否將目標資源自動更新為新頭資源的基於`Id`的標識符。 在此示例中，由於依賴關係，指定值`true`。
   * 一個`boolean`值，指示是否指定了目標頭。 在此示例中，指定了值`true`。
   * 傳遞`null`作為最後一個參數。

   您也可以叫用`RepositoryServiceService`物件的`getRelated`方法並傳入下列參數，以擷取特定資源的相關資源清單：

   * 要為其檢索相關資源的資源的URI。 在此示例中，指定了源資源(`"/testFolder/testResource1"`)。
   * `boolean`值，指示指定的資源是否是關係中的源資源。 在此示例中，指定值`true`，因為此情況。
   * 一個`boolean`值，指示是否指定了源資源。 在此示例中，提供了值`true`。
   * 包含關係類型的整數陣列。 在此示例中，通過在陣列中使用與先前使用的相同值來指定依賴關係：`3`。
   * 傳遞`null`以取得其餘兩個參數。

   `getRelated`方法返回可以轉換到`Resource`對象的對象陣列，您可以通過這些對象進行迭代以檢索每個相關資源。 在此示例中，`testResource2`應該位於返回的資源清單中。

**另請參閱**

[建立資源關係](aem-forms-repository.md#creating-resource-relationships)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 鎖定資源{#locking-resources}

您可以鎖定資源或一組資源供特定使用者獨佔使用或在多個使用者間共用使用。 共用鎖表示資源將發生某些情況，但並不阻止其他人對該資源執行操作。 應將共用鎖視為信令機制。 獨佔鎖定表示鎖定資源的用戶將更改資源，而鎖定確保在用戶不再需要訪問資源並釋放鎖定之前，其他任何用戶都不能更改。 如果儲存庫管理員解除了資源的鎖定，則該資源上的所有獨佔鎖定和共用鎖定都將自動刪除。 此類操作適用於用戶不再可用且未解鎖資源的情況。

鎖定資源時，當您查看「工作台」中的「資源」頁籤時，將顯示鎖定表徵圖，如下圖所示。

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

您可以使用Repository服務Java API或web服務API，以程式設計方式控制對資源的存取。

>[!NOTE]
>
>有關Repository服務的詳細資訊，請參閱[ Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-7}摘要

要鎖定和解除鎖定資源，請執行以下步驟：

1. 包含專案檔案。
1. 建立儲存庫服務客戶端。
1. 指定要鎖定的資源的URI。
1. 鎖定資源。
1. 檢索資源的鎖。
1. 解除鎖定資源

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請加入proxy檔案。

**建立服務客戶端**

在以寫程式方式讀取資源之前，必須建立連接並提供憑據。 這是通過建立服務客戶端來實現的。

**指定要鎖定的資源的URI**

建立包含要鎖定的資源的URI的字串。 語法包含正斜線，如本例所示：&quot;/*path*/*resource*&quot;。

**鎖定資源**

調用儲存庫服務方法以鎖定資源，指定URI、鎖定類型和鎖定深度。

**檢索資源的鎖**

調用Repository服務方法以檢索資源的鎖，指定URI。

**解除鎖定資源**

調用儲存庫服務方法以解鎖資源，指定URI。

**另請參閱**

[使用Java API鎖定資源](aem-forms-repository.md#lock-resources-using-the-java-api)

[使用web service API鎖定資源](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API {#lock-resources-using-the-java-api}鎖定資源

使用Repository服務API(Java)鎖定資源：

1. 包含專案檔案

   在Java專案的類別路徑中加入用戶端JAR檔案。

1. 建立服務客戶端

   使用其建構子並傳遞包含連接屬性的`ServiceClientFactory`對象，建立`ResourceRepositoryClient`對象。

1. 指定要鎖定的資源的URI

   指定要鎖定的資源的URI。 在這種情況下，由於名為`testResource`的資源位於名為`testFolder`的資料夾中，因此其URI為`"/testFolder/testResource"`。 URI儲存為`java.lang.String`對象。

1. 鎖定資源

   叫用`ResourceRepositoryClient`物件的`lockResource`方法並傳入下列參數：

   * 資源的URI。
   * 鎖定範圍。 在此示例中，由於資源將被鎖定以供獨佔使用，因此鎖定範圍被指定為`com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`。
   * 鎖定深度。 在此示例中，由於鎖定僅適用於特定資源，且不適用於其成員或子代，因此將鎖定深度指定為`Lock.DEPTH_ZERO`。

   >[!NOTE]
   >
   >需要四個參數的`lockResource`方法的過載版本會引發異常。 請確定使用`lockResource`方法，該方法需要三個參數，如本逐步說明所示。

1. 檢索資源的鎖

   調用`ResourceRepositoryClient`物件的`getLocks`方法，並將資源的URI作為參數傳遞。 該方法返回可循環使用的鎖定對象清單。 在此範例中，會針對每個物件分別呼叫每個Lock物件的`getOwnerUserId`、`getDepth`和`getType`方法，以列印鎖定擁有者、深度和範圍。

1. 解除鎖定資源

   調用`ResourceRepositoryClient`物件的`unlockResource`方法，並將資源的URI作為參數傳遞。 如需詳細資訊，請參閱[AEM Forms API參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**另請參閱**

[鎖定資源](aem-forms-repository.md#locking-resources)

[快速入門（SOAP模式）:使用Java API鎖定資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#lock-resources-using-the-web-service-api}鎖定資源

使用Repository服務API(web service)鎖定資源：

1. 包含專案檔案

   * 建立使用Base64的儲存庫WSDL的Microsoft .NET客戶端元件。
   * 參考Microsoft .NET客戶端元件。

1. 建立服務客戶端

   使用Microsoft .NET客戶端元件，通過調用其預設建構子建立`RepositoryServiceService`對象。 使用包含用戶名和口令的`System.Net.NetworkCredential`對象設定其`Credentials`屬性。

1. 指定要鎖定的資源的URI

   指定包含要鎖定的資源URI的字串。 在這種情況下，由於名為`testResource`的資源位於`testFolder`資料夾中，其URI為`"/testFolder/testResource"`。 使用與Microsoft .NET Framework（例如C#）相容的語言時，將URI儲存在`System.String`對象中。

1. 鎖定資源

   叫用`RepositoryServiceService`物件的`lockResource`方法並傳入下列參數：

   * 資源的URI。
   * 鎖定範圍。 在此示例中，由於資源將被鎖定以供獨佔使用，因此鎖定範圍被指定為`11`。
   * 鎖定深度。 在此示例中，由於鎖定僅適用於特定資源，且不適用於其成員或子代，因此將鎖定深度指定為`2`。
   * 一個`int`值，指示鎖過期前的秒數。 在此示例中，使用`1000`的值。
   * 傳遞`null`作為最後一個參數。

1. 檢索資源的鎖

   調用`RepositoryServiceService`物件的`getLocks`方法，並將資源的URI傳遞為第一個參數，而將`null`傳遞為第二個參數。 該方法返回包含`Lock`對象的`object`陣列，可通過該陣列進行迭代。 在此示例中，通過分別訪問每個`Lock`對象的`ownerUserId`、`depth`和`type`欄位，可打印每個對象的鎖所有者、深度和範圍。

1. 解除鎖定資源

   調用`RepositoryServiceService`物件的`unlockResource`方法，並將資源的URI傳遞為第一個參數，而將`null`傳遞為第二個參數。

**另請參閱**

[鎖定資源](aem-forms-repository.md#locking-resources)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 刪除資源{#deleting-resources}

可以使用Repository服務Java API(SOAP)從儲存庫中的給定位置以寫程式方式刪除資源。

刪除資源時，刪除通常是永久的，但在某些情況下，ECM儲存庫可能會根據其歷史記錄機制儲存資源的版本。 因此，刪除資源時，務必確保您不再需要該資源。 刪除資源的常見原因包括需要增加資料庫中的可用空間。 您可以刪除資源的版本，但是，如果這樣做，則必須指定資源標識符，而不是其邏輯標識符(LID)或路徑。 如果您刪除資料夾，該資料夾中的所有項目（包括子資料夾和資源）都會自動刪除。

相關資源不會刪除。 例如，如果您有使用logo.gif檔案的表單，而您刪除logo.gif，則關係會儲存在待定關係表格中。 另外，若要取代版本，請將最新版本的物件狀態設定為不再提倡。

刪除操作在ECM系統中不是事務安全的。 例如，如果您嘗試刪除100個資源，而第50個資源上的操作失敗，則前49個實例將被刪除，但其餘實例將不刪除。 否則，預設行為是回滾（非承諾）。

>[!NOTE]
>
>將`com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()`方法與ECM儲存庫（EMC Documentum Content Server和IBM FileNet P8 Content Manager）一起使用時，如果某個指定資源的刪除失敗，則不會回退事務，這意味著無法刪除那些已刪除的檔案。

>[!NOTE]
>
>有關Repository服務的詳細資訊，請參閱[ Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟{#summary_of_steps-8}摘要

要刪除資源，請執行以下步驟：

1. 包含專案檔案。
1. 建立儲存庫服務客戶端。
1. 指定要刪除的資源的URI。
1. 刪除資源。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 如果要使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果您使用web services，請加入proxy檔案。

**建立服務客戶端**

在以寫程式方式讀取資源之前，必須建立連接並提供憑據。 這是通過建立服務客戶端來實現的。

**指定要刪除的資源的URI**

建立包含要刪除的資源的URI的字串。 語法包含正斜線，如本例所示：&quot;/*path*/*resource*&quot;。 如果要刪除的資源是資料夾，則刪除將是遞歸的。

**刪除資源**

調用Repository服務方法以刪除資源，指定URI。

**另請參閱**

[使用Java API刪除資源](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[使用web service API刪除資源](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API(SOAP){#delete-resources-using-the-java-api-soap}刪除資源

使用儲存庫API(Java)刪除資源：

1. 包含專案檔案

   在Java專案的類別路徑中加入用戶端JAR檔案。

1. 建立服務客戶端

   使用其建構子並傳遞包含連接屬性的`ServiceClientFactory`對象，建立`ResourceRepositoryClient`對象。

1. 指定要刪除的資源的URI

   指定要檢索的資源的URI。 在這種情況下，由於名為testResourceToBeDeleted的資源位於名為testFolder的資料夾中，因此其URI為`/testFolder/testResourceToBeDeleted`。 URI儲存為`java.lang.String`對象。 在此示例中，資源首先寫入儲存庫，並檢索其URI。 有關編寫資源的詳細資訊，請參閱[編寫資源](aem-forms-repository.md#writing-resources)。

1. 刪除資源

   調用`ResourceRepositoryClient`物件的`deleteResource`方法，並將資源的URI作為參數傳遞。

**另請參閱**

[刪除資源](aem-forms-repository.md#deleting-resources)

[快速入門（SOAP模式）:使用Java API搜尋資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用web service API {#delete-resources-using-the-web-service-api}刪除資源

使用儲存庫API（web服務）刪除資源：

1. 包含專案檔案

   * 建立使用Base64的儲存庫WSDL的Microsoft .NET客戶端元件。
   * 參考Microsoft .NET客戶端元件。

1. 建立服務客戶端

   使用Microsoft .NET客戶端元件，通過調用其預設建構子建立`RepositoryServiceService`對象。 使用包含用戶名和口令的`System.Net.NetworkCredential`對象設定其`Credentials`屬性。

1. 指定要刪除的資源的URI

   指定要檢索的資源的URI。 在這種情況下，由於名為`testResourceToBeDeleted`的資源位於名為`testFolder`的資料夾中，因此其URI為`"/testFolder/testResourceToBeDeleted"`。 在此示例中，資源首先寫入儲存庫，並檢索其URI。 有關編寫資源的詳細資訊，請參閱[編寫資源](aem-forms-repository.md#writing-resources)。

1. 刪除資源

   調用`RepositoryServiceService`物件的`deleteResources`方法，並傳遞包含資源URI作為第一個參數的`System.String`陣列。 傳遞`null`作為第二個參數。

**另請參閱**

[刪除資源](aem-forms-repository.md#deleting-resources)

[使用Base64編碼叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
