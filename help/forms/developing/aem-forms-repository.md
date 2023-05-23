---
title: 使用AEM Forms儲存庫
seo-title: Working with AEM Forms Repository
description: 管理AEM Forms儲存庫，以使用Java API和Web服務API建立資料夾、寫入、清單、讀取、更新和搜索資源。 此外，瞭解如何建立資源關係、鎖定和刪除資源。
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

# 使用AEM Forms儲存庫 {#working-with-aem-forms-repository}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

**關於儲存庫服務**

儲存庫服務向AEM Forms提供資源儲存和管理服務。 當開發人員建立 *AEM Forms* 應用程式，他們可以在儲存庫中而不是檔案系統中部署資產。 資產可以包括任何類型的宣傳品，包括XML表單、PDF forms(包括Acrobat表單)、表單片段、影像、配置檔案、策略、SWF檔案、DDX檔案、XML架構、WSDL檔案和test資料。

例如，請考慮以下名為的Forms應用程式 *應用程式/表單應用程式*:

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

請注意，FormsFolder中有一個名為Loan.xdp的檔案。 要訪問此表單設計，請指定完整路徑（包括版本）: `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。

>[!NOTE]
>
>有關使用Workbench建立Forms應用程式的資訊，請參閱 [工作台幫助](https://www.adobe.com/go/learn_aemforms_workbench_63)。

位於AEM Forms儲存庫中的資源的路徑是：

`Applications/Application-name/Application-version/Folder.../Filename`

以下值顯示URI值的一些示例：

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>您可以使用Web瀏覽器瀏覽AEM Forms儲存庫。 要瀏覽儲存庫，請在Web瀏覽器中輸入以下URL `https://[server name]:[server port]/repository`。 您可以使用Web瀏覽器驗證與「使用AEM Forms儲存庫」部分關聯的快速啟動結果。 例如，如果向AEM Forms儲存庫添加內容，則可以在Web瀏覽器中查看內容。 (請參閱 [快速啟動（SOAP模式）:使用Java API編寫資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)。)

儲存庫API提供了許多操作，您可以使用這些操作來儲存和檢索儲存庫中的資訊。 例如，當處理應用程式時需要資源時，您可以獲取資源清單或檢索儲存在儲存庫中的特定資源。

>[!NOTE]
>
>儲存庫API不能用於與Content Services交互（不建議使用）。 要與Content Services交互（不建議使用），請使用Document Management API。

使用Repository服務API，可以完成以下任務：

* 建立檔案夾. 請參閱 [建立資料夾](aem-forms-repository.md#creating-folders)。
* 寫入資源及其屬性。 請參閱 [編寫資源](aem-forms-repository.md#writing-resources)。
* 列出給定集合中或與其他資源相關的資源。 請參閱 [列出資源](aem-forms-repository.md#listing-resources)。
* 讀取資源及其屬性。 請參閱 [讀取資源](aem-forms-repository.md#reading-resources)。
* 更新資源及其屬性。 請參閱 [更新資源](aem-forms-repository.md#updating-resources)。
* 搜索資源，包括其歷史記錄、相關資源和屬性。 請參閱 [搜索資源](aem-forms-repository.md#searching-for-resources)。
* 指定資源之間的關係。 請參閱 [建立資源關係](aem-forms-repository.md#creating-resource-relationships)。
* 管理資源訪問控制，包括鎖定和解鎖資源以及讀取和寫入訪問控制清單(ACL)。 請參閱 [鎖定資源](aem-forms-repository.md#locking-resources)。
* 刪除資源及其屬性。 請參閱 [刪除資源](aem-forms-repository.md#deleting-resources)。

>[!NOTE]
>
>使用儲存庫API，您無法使用ECM儲存庫管理資源訪問控制、搜索資源或指定資源關係。

>[!NOTE]
>
>當加密PDF寫入儲存庫時，無法使用自動關係提取功能。 否則，加密的PDF可以儲存在儲存庫中並稍後檢索。 檢索器可以選擇在從儲存庫檢索到PDF後對其解密。

>[!NOTE]
>
>有關儲存庫服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

## 建立資料夾 {#creating-folders}

資料夾（資源集合）用於在有組織的分組中儲存對象（檔案或資源）。 資料夾可以包含資源和其他資料夾，也稱為子資料夾。 資源一次只能儲存在一個資料夾中。

檔案從資料夾繼承訪問控制清單(ACL)，子資料夾從其父資料夾繼承ACL。 因此，在建立子資料夾之前，父資料夾必須存在。 IDE允許您僅按資料夾進行交互，而不按檔案進行交互。 您不能對資料夾進行版本化，也無需這樣做；資料夾不包含資料本身。 相反，它只是包含資料的資源的容器。 預設ACL是系統級權限，這意味著用戶必須具有系統級權限（讀、寫、遍歷、管理ACL），直到有人授予他們特定資料夾的權限。 ACL僅在IDE中工作。

>[!NOTE]
>
>有關儲存庫服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

要建立資料夾，請執行以下步驟：

1. 包括項目檔案。
1. 建立服務客戶端。
1. 建立資料夾。
1. 將資料夾寫入儲存庫。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請包括代理檔案。

**建立服務客戶端**

在以寫程式方式建立資源集合之前，必須建立連接並提供憑據。 這是通過建立服務客戶端來實現的。

**建立資料夾**

調用儲存庫服務方法以建立資源集合，並使用標識資訊填充資源集合，包括其UUID、資料夾名稱和說明。

**將資料夾寫入儲存庫**

調用儲存庫服務方法來寫入資源集合，並指定目標資料夾的URI。

**另請參閱**

[使用Java API建立資料夾](aem-forms-repository.md#create-folders-using-the-java-api)

[使用Web服務API建立資料夾](aem-forms-repository.md#create-folders-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API建立資料夾 {#create-folders-using-the-java-api}

使用Repository服務API(Java)建立資料夾：

1. 包括項目檔案

   在Java項目的類路徑中包括項目檔案。

1. 建立服務客戶端

   建立 `ResourceRepositoryClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 建立資料夾

   要建立資源集合，必須先建立 `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` 的雙曲餘切值。

   調用 `repositoryInfomodelFactoryBean` 對象 `newResourceCollection` 方法，並傳遞以下參數：

   * A `com.adobe.repository.infomodel.Id` 要分配給資源的UUID標識符。
   * A `com.adobe.repository.infomodel.Lid` 要分配給資源的UUID標識符。
   * A `java.lang.String` 包含資源集合的名稱。 比如說， `FormsFolder`。

   該方法返回 `com.adobe.repository.infomodel.bean.ResourceCollection` 表示新資料夾的對象。

   使用 `setDescription` 方法和傳遞的參數如下：

   * A `String` 描述資源集合。 在本例中， `"test Folder"` 已使用 `.`


1. 將資料夾寫入儲存庫

   調用 `ResourceRepositoryClient` 對象 `writeResource` 在資料夾的URI中傳遞 `ResourceCollection` 的雙曲餘切值。 例如，資料夾的URI可以是以下值 `/Applications/FormsApplication/1.0/`。

   該方法返回新建立的實例 `com.adobe.repository.infomodel.bean.Resource` 的雙曲餘切值。 例如，可以通過調用 `com.adobe.repository.infomodel.bean.Resource` 對象 `getId` 的雙曲餘切值。

**另請參閱**

[建立資料夾](aem-forms-repository.md#creating-folders)

[快速啟動（SOAP模式）:使用Java API建立資料夾](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API建立資料夾 {#create-folders-using-the-web-service-api}

使用儲存庫服務API（Web服務）建立資料夾：

1. 包括項目檔案

   * 使用base64建立使用儲存庫WSDL的Microsoft.NET客戶端程式集。
   * 引用Microsoft.NET客戶端程式集。

1. 建立服務客戶端

   使用Microsoft.NET客戶端程式集，建立 `RepositoryServiceService` 調用其預設建構子。 設定 `Credentials` 屬性使用 `System.Net.NetworkCredential` 包含用戶名和密碼的對象。

1. 建立資料夾

   使用資料夾的預設建構子 `ResourceCollection` 類和傳遞的參數如下：

   * 安 `Id` 對象，通過為 `Id` 類並分配給 `Resource` 對象 `id` 的子菜單。
   * 安 `Lid` 對象，通過為 `Lid` 類並分配給 `Resource` 對象 `lid` 的子菜單。
   * 包含資源集合名稱的字串，該名稱分配給 `Resource` 對象 `name` 的子菜單。 此示例中使用的名稱是 `"testfolder"`。
   * 一個字串，它包含資源集合的說明，它已分配給 `Resource` 對象 `description` 的子菜單。 本示例中使用的說明是 `"test folder"`。

1. 將資料夾寫入儲存庫

   調用 `RepositoryServiceService` 對象 `writeResource` 方法和傳遞以下參數：

   * 要建立資料夾的路徑。
   * 的 `ResourceCollection` 表示資料夾的對象。
   * 通過 `null` 來確定。

**另請參閱**

[建立資料夾](aem-forms-repository.md#creating-folders)

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 編寫資源 {#writing-resources}

您可以在儲存庫中的給定位置建立資源。 自然檔案大小受資料庫限制和會話超時的限制。 對於預設配置，檔案限制為25 MB。 要提高或降低最大檔案大小，必須更改資料庫配置。

寫入資源相當於將資料儲存在儲存庫中。 將資源寫入儲存庫後，儲存庫生態系統中的所有客戶端都可以訪問它。 將資源（如XML架構、XDP檔案和XSD檔案）寫入儲存庫時，將根據MIME類型分析內容。 如果支援MIME類型，則解析器確定是否與其他內容存在隱含關係。 例如，如果級聯樣式表(CSS)的相對URL引用了公用CSS，則您也應將公用CSS提交到儲存庫中。 兩個資源之間的關係被儲存為30天不可調節的掛起關係。 在30天內將公用CSS提交到儲存庫時，將形成關係。

建立資源時，訪問控制清單(ACL)將繼承自父資料夾。 根資料夾具有系統級權限，直到建立初始資源或資料夾，此時該資源或資料夾將獲得預設ACL權限。

可以使用Repository服務Java API或Web服務API以寫程式方式編寫資源。

>[!NOTE]
>
>有關儲存庫服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

要編寫資源，請執行以下步驟：

1. 包括項目檔案。
1. 建立儲存庫服務客戶端。
1. 指定要讀取的資源的URI。
1. 閱讀資源。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請包括代理檔案。

**建立服務客戶端**

在以寫程式方式讀取資源之前，必須建立連接並提供憑據。 這是通過建立服務客戶端來實現的。

**指定資源的目標資料夾的URI**

建立包含要讀取的資源的URI的字串。 語法包括正斜槓，如本示例所示：&quot;/*路徑*/*資料夾*。

**建立資源**

調用儲存庫服務方法以建立資源，並使用標識資訊填充資源，包括其UUID、資源名稱和說明。

**指定資源內容**

調用儲存庫服務方法以建立資源內容，並將該內容儲存在資源中。

**將資源寫入目標資料夾**

調用儲存庫服務方法來寫入資源，指定目標資料夾的URI。

**另請參閱**

[使用Java API寫入資源](aem-forms-repository.md#write-resources-using-the-java-api)

[使用Web服務API寫入資源](aem-forms-repository.md#write-resources-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API寫入資源 {#write-resources-using-the-java-api}

使用Repository服務API(Java)編寫資源：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案。

1. 建立服務客戶端

   建立 `ResourceRepositoryClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 指定資源的目標資料夾的URI

   指定資源的目標資料夾的URI。 在本例中，因為名為 `testResource` 將儲存在名為 `testFolder`，資料夾的URI為 `"/testFolder"`。 URI儲存為 `java.lang.String` 的雙曲餘切值。

1. 建立資源

   要建立資源，必須先建立 `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` 的雙曲餘切值。

   調用 `RepositoryInfomodelFactoryBean` 對象 `newResource` 方法，建立 `com.adobe.repository.infomodel.bean.Resource` 的雙曲餘切值。 在本示例中，提供了以下參數：

   * A `com.adobe.repository.infomodel.Id` 對象，通過為 `Id` 類。
   * A `com.adobe.repository.infomodel.Lid` 對象，通過為 `Lid` 類。
   * A `java.lang.String` 包含資源的檔案名。

   要指定資源的說明，請調用 `Resource` 對象 `setDescription` 方法並傳遞包含說明的字串。 在本示例中，說明為 `"test resource"`。

1. 指定資源內容

   要為資源建立內容，請調用 `RepositoryInfomodelFactoryBean` 對象 `newResourceContent` 方法，它返回 `com.adobe.repository.infomodel.bean.ResourceContent` 的雙曲餘切值。 將內容添加到 `ResourceContent` 的雙曲餘切值。 在本示例中，通過執行以下任務來完成此操作：

   * 調用 `ResourceContent` 對象 `setDataDocument` 方法和傳遞 `com.adobe.idp.Document` 對象
   * 調用 `ResourceContent` 對象 `setSize` 方法和傳入的大小（以位元組為單位） `Document` 對象

   通過調用 `Resource` 對象 `setContent` 方法和傳遞 `ResourceContent` 的雙曲餘切值。 有關詳細資訊，請參見 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

1. 將資源寫入目標資料夾

   調用 `ResourceRepositoryClient` 對象 `writeResource` 在資料夾的URI中傳遞，以及 `Resource` 的雙曲餘切值。

**另請參閱**

[編寫資源](aem-forms-repository.md#writing-resources)

[快速啟動（SOAP模式）:使用Java API編寫資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API寫入資源 {#write-resources-using-the-web-service-api}

使用儲存庫服務API（Web服務）編寫資源：

1. 包括項目檔案

   * 使用base64建立使用儲存庫WSDL的Microsoft.NET客戶端程式集。
   * 引用Microsoft.NET客戶端程式集。

1. 建立服務客戶端

   使用Microsoft.NET客戶端程式集，建立 `RepositoryServiceService` 調用其預設建構子。 設定 `Credentials` 屬性使用 `System.Net.NetworkCredential` 包含用戶名和密碼的對象。

1. 指定資源的目標資料夾的URI

   指定資源的目標資料夾的URI。 在本例中，因為名為 `testResource` 將儲存在名為 `testFolder`，資料夾的URI為 `"/testFolder"`。 使用與Microsoft.NET Framework（例如C#）相容的語言時，將URI儲存在 `System.String` 的雙曲餘切值。

1. 建立資源

   要建立資源，請為 `Resource` 類。 在本示例中，以下資訊儲存在 `Resource` 對象：

   * A `com.adobe.repository.infomodel.Id` 對象，通過為 `Id` 類並分配給 `Resource` 對象 `id` 的子菜單。
   * A `com.adobe.repository.infomodel.Lid` 對象，通過為 `Lid` 類並分配給 `Resource` 對象 `lid` 的子菜單。
   * 一個字串，它包含分配給 `Resource` 對象 `name` 的子菜單。 此示例中使用的名稱是 `"testResource"`。
   * 包含資源說明的字串，已分配給 `Resource` 對象 `description` 的子菜單。 本示例中使用的說明是 `"test resource"`。

1. 指定資源內容

   要為資源建立內容，請為 `ResourceContent` 類。 然後將內容添加到 `ResourceContent` 的雙曲餘切值。 在本示例中，通過執行以下任務來完成此操作：

   * 分配 `BLOB` 包含文檔的對象 `ResourceContent` 對象 `dataDocument` 的子菜單。
   * 分配大小（以位元組為單位） `BLOB` 對象 `ResourceContent` 對象 `size` 的子菜單。

   通過分配 `ResourceContent` 對象 `Resource` 對象 `content` 的子菜單。

1. 將資源寫入目標資料夾

   調用 `RepositoryServiceService` 對象 `writeResource` 在資料夾的URI中傳遞，以及 `Resource` 的雙曲餘切值。 通過 `null` 來確定。

**另請參閱**

[編寫資源](aem-forms-repository.md#writing-resources)

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 列出資源 {#listing-resources}

您可以通過列出資源來發現資源。 對儲存庫執行查詢以查找與給定資源集合相關的所有資源。

組織資源後，您可以檢查通過查看結構的特定分支所建立的結構，就像在作業系統中所做的那樣。

列出按關係運行的資源：資源是資料夾的成員。 成員身份由「成員」類型的關係表示。 在給定資料夾中列出資源時，您正在查詢與給定資料夾相關的資源，這些資源由關係「成員」進行。 關係是方向性的：關係的成員具有作為目標成員的源。 源是資源；目標是父資料夾。

>[!NOTE]
>
>有關儲存庫服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-2}

要列出資源，請執行以下步驟：

1. 包括項目檔案。
1. 建立服務客戶端。
1. 指定資料夾路徑。
1. 檢索資源清單。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請包括代理檔案。

**建立服務客戶端**

在以寫程式方式建立資源集合之前，必須建立連接並提供憑據。 這是通過建立服務客戶端來實現的。

**指定資料夾路徑**

建立包含包含資源的資料夾路徑的字串。 語法包括正斜槓，如本示例所示：&quot;/*路徑*/*資料夾*。

**檢索資源清單**

調用儲存庫服務方法以檢索資源清單，並指定目標資料夾的路徑。

**另請參閱**

[使用Java API列出資源](aem-forms-repository.md#list-resources-using-the-java-api)

[使用Web服務API列出資源](aem-forms-repository.md#list-resources-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API列出資源 {#list-resources-using-the-java-api}

使用Repository服務API(Java)列出資源：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案。

1. 建立服務客戶端

   建立 `ResourceRepositoryClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 指定資料夾路徑

   指定要查詢的資源集合的URI。 在這種情況下，其URI為 `"/testFolder"`。 URI儲存為 `java.lang.String` 的雙曲餘切值。

1. 檢索資源清單

   調用 `ResourceRepositoryClient` 對象 `listMembers` 方法並傳遞到資料夾的URI。

   該方法返回 `java.util.List` 共 `com.adobe.repository.infomodel.bean.Resource` 作為源的對象 `com.adobe.repository.infomodel.bean.Relation` 類型 `Relation.TYPE_MEMBER_OF` 將資源集合URI作為目標。 你可以反複 `List` 檢索每個資源。 在此示例中，將顯示每個資源的名稱和說明。

**另請參閱**

[列出資源](aem-forms-repository.md#listing-resources)。

[快速啟動（SOAP模式）:使用Java API列出資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API列出資源 {#list-resources-using-the-web-service-api}

使用儲存庫服務API（Web服務）列出資源：

1. 包括項目檔案

   * 建立使用儲存庫WSDL的Microsoft.NET客戶端程式集。
   * 引用Microsoft.NET客戶端程式集。

1. 建立服務客戶端

   使用Microsoft.NET客戶端程式集，建立 `RepositoryServiceService` 調用其預設建構子。 設定 `Credentials` 屬性使用 `System.Net.NetworkCredential` 包含用戶名和密碼的對象。

1. 指定資料夾路徑

   指定包含要查詢的資料夾的URI的字串。 在這種情況下，其URI為 `"/testFolder"`。 使用符合Microsoft.NET Framework（例如C#）的語言時，將URI儲存在 `System.String` 的雙曲餘切值。

1. 檢索資源清單

   調用 `RepositoryServiceService` 對象 `listMembers` 方法並作為第一個參數傳遞到資料夾的URI。 通過 `null` 來確定。

   該方法返回可轉換到 `Resource` 對象。 可以循環訪問對象陣列以檢索每個相關資源。 在此示例中，將顯示每個資源的名稱和說明。

**另請參閱**

[列出資源](aem-forms-repository.md#listing-resources)。

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 讀取資源 {#reading-resources}

您可以從儲存庫中的給定位置檢索資源，以便讀取其內容和元資料。 該工作流由初始化表單前端。 該進程具有讀取表單所需的所有權限。 系統檢索資料表單並從儲存庫讀取內容。 儲存庫授予對內容和元資料的訪問權限（甚至能夠知道資源存在）。

儲存庫具有以下四種權限類型：

* **橫**:允許您列出資源；即，讀取資源元資料，但不讀取資源內容
* **讀**:允許您讀取資源內容
* **寫**:允許您寫入資源內容
* **管理訪問控制清單(ACL)**:允許您在資源上操作ACL

用戶只有在有權運行進程時才能運行進程。 IDE用戶需要遍歷和讀取權限才能與儲存庫同步。 ACL僅在設計時應用，因為運行時出現在系統上下文中。

可以使用Repository服務Java API或Web服務API以寫程式方式讀取資源。

>[!NOTE]
>
>有關儲存庫服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-3}

要讀取資源，請執行以下步驟：

1. 包括項目檔案。
1. 建立儲存庫服務客戶端。
1. 指定要讀取的資源的URI。
1. 閱讀資源。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請包括代理檔案。

**建立服務客戶端**

在以寫程式方式讀取資源之前，必須建立連接並提供憑據。 這是通過建立服務客戶端來實現的。

**指定要讀取的資源的URI**

建立包含要讀取的資源的URI的字串。 語法包括正斜槓，如本示例所示：&quot;/*路徑*/*資源*。

**讀取資源**

調用Repository服務方法以讀取資源，並指定URI。

**另請參閱**

[使用Java API讀取資源](aem-forms-repository.md#read-resources-using-the-java-api)

[使用Web服務API讀取資源](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API讀取資源 {#read-resources-using-the-java-api}

使用Repository服務API(Java)讀取資源：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案。

1. 建立服務客戶端

   建立 `ResourceRepositoryClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 指定要讀取的資源的URI

   指定表示要檢索的資源的URI的字串值。 例如，假定資源名為 *測試資源* 位於名為 *測試資料夾*&#x200B;指定 `/testFolder/testResource`。

1. 讀取資源

   調用 `ResourceRepositoryClient` 對象 `readResource` 方法，並將資源的URI作為參數傳遞。 此方法返回 `Resource` 表示資源的實例。

**另請參閱**

[讀取資源](aem-forms-repository.md#reading-resources)

[快速啟動（SOAP模式）:使用Java API讀取資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API讀取資源 {#reading-resources-using-the-web-service-api}

使用Repository服務API（Web服務）讀取資源：

1. 包括項目檔案

   * 建立使用儲存庫WSDL的Microsoft.NET客戶端程式集。 (請參閱 [建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)。)
   * 引用Microsoft.NET客戶端程式集。 (請參閱 [建立使用Base64編碼的.NET客戶端程式集](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)。)

1. 建立服務客戶端

   使用Microsoft.NET客戶端程式集，建立 `RepositoryServiceService` 調用其預設建構子。 設定 `Credentials` 屬性使用 `System.Net.NetworkCredential` 包含用戶名和密碼的對象。

1. 指定要讀取的資源的URI

   指定包含要檢索的資源的URI的字串。 在本例中，因為名為 `testResource` 位於名為 `testFolder`，其URI為 `"/testFolder/testResource"`。 使用與Microsoft.NET Framework（例如C#）相容的語言時，將URI儲存在 `System.String` 的雙曲餘切值。

1. 讀取資源

   調用 `RepositoryServiceService` 對象 `readResource` 將資源的URI作為第一個參數傳遞。 通過 `null` 來確定。

**另請參閱**

[讀取資源](aem-forms-repository.md#reading-resources)

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 更新資源 {#updating-resources}

您可以檢索和更新儲存庫中的資源內容。 更新資源時，對這些資源的訪問控制在版本之間保持不變。 執行更新時，您可以選擇增加主版本。 如果不選擇增量主版本，則會自動更新次版本。

更新資源時，將根據指定的資源屬性建立新版本。 在更新資源時，您指定兩個重要參數：目標URI和包含所有更新元資料的資源實例。 請注意，如果不更改給定屬性（例如，名稱），則在傳入的實例中仍需要該屬性。 分析內容時建立的關係將添加到特定版本，除非指定，否則不會提前。

例如，如果更新XDP檔案並且該檔案包含對其他資源的引用，則還會記錄這些附加引用。 假設form.xdp 1.0版有兩個外部引用：徽標和樣式表，隨後您將更新form.xdp，以便它現在有三個引用：徽標、樣式表和架構檔案。 在更新期間，儲存庫會將第三個關係（到架構檔案）添加到其掛起關係表中。 一旦模式檔案存在於儲存庫中，將自動形成關係。 但是，如果form.xdp 2.0版不再使用徽標，則form.xdp 2.0版將與徽標無關。

所有更新操作都是原子操作和事務操作。 例如，如果兩個用戶讀取了同一資源，並且都決定將版本1.0更新到版本2.0，則其中一個將成功，而其中一個將失敗，則會維護儲存庫的完整性，並且兩個用戶都將收到消息，確認成功或失敗。 如果事務未提交，則在資料庫出現故障時將回退，並根據應用程式伺服器超時或回退。

可以使用Repository服務Java API或Web服務API以寫程式方式更新資源。

>[!NOTE]
>
>有關儲存庫服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-4}

要更新資源，請執行以下步驟：

1. 包括項目檔案。
1. 建立儲存庫服務客戶端。
1. 檢索要更新的資源。
1. 更新資源。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請包括代理檔案。

**建立服務客戶端**

在以寫程式方式讀取資源之前，必須建立連接並提供憑據。 這是通過建立服務客戶端來實現的。

**檢索要更新的資源**

閱讀資源。 有關詳細資訊，請參見 [讀取資源](aem-forms-repository.md#reading-resources)。

**更新資源**

在資源中設定新資訊並調用儲存庫服務方法來更新資源，指定URI、更新的資源以及如何更新版本資訊。

**另請參閱**

[使用Java API更新資源](aem-forms-repository.md#update-resources-using-the-java-api)

[使用Web服務API更新資源](aem-forms-repository.md#update-resources-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API更新資源 {#update-resources-using-the-java-api}

使用Repository服務API(Java)更新資源：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案。

1. 建立服務客戶端

   建立 `ResourceRepositoryClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 檢索要更新的資源

   指定要檢索和讀取資源的資源的URI。 在此示例中，資源的URI為 `"/testFolder/testResource"`。

1. 更新資源

   更新 `Resource` 對象資訊。 在此示例中，要更新說明，請調用 `Resource` 對象 `setDescription` 方法，並將新的描述字串作為參數傳遞。

   然後調用 `ServiceClientFactory` 對象 `updateResource` 方法，並傳遞以下參數：

   * A `java.lang.String` 包含資源URI的對象。
   * 的 `Resource` 包含更新的資源資訊的對象。
   * A `boolean` 指示是更新主版本還是次版本的值。 在此示例中， `true` 傳遞以指示將遞增主版本。

**另請參閱**

[更新資源](aem-forms-repository.md#updating-resources)

[快速啟動（SOAP模式）:使用Java API更新資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API更新資源 {#update-resources-using-the-web-service-api}

使用Repository API（Web服務）更新資源：

1. 包括項目檔案

   * 建立使用儲存庫WSDL的Microsoft.NET客戶端程式集。
   * 引用Microsoft.NET客戶端程式集。

1. 建立服務客戶端

   使用Microsoft.NET客戶端程式集，建立 `RepositoryServiceService` 調用其預設建構子。 設定 `Credentials` 屬性使用 `System.Net.NetworkCredential` 包含用戶名和密碼的對象。

1. 檢索要更新的資源

   指定要檢索並讀取資源的資源的URI。 在此示例中，資源的URI為 `"/testFolder/testResource"`。 有關詳細資訊，請參見 [讀取資源](aem-forms-repository.md#reading-resources)。

1. 更新資源

   更新 `Resource` 對象資訊。 在此示例中，要更新說明，請為 `Resource` 對象 `description` 的子菜單。

1. 調用 `RepositoryServiceService` 對象 `updateResource` 方法，並傳遞以下參數：

   * A `System.String` 包含資源URI的對象。
   * 的 `Resource` 包含更新的資源資訊的對象。
   * A `boolean` 指示是更新主版本還是次版本的值。 在此示例中， `true` 傳遞以指示將遞增主版本。
   * 通過 `null` 的下界。

**另請參閱**

[更新資源](aem-forms-repository.md#updating-resources)

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 搜索資源 {#searching-for-resources}

您可以構造用於搜索儲存庫中資源的查詢，包括歷史記錄、相關資源和屬性。

可以檢索相關資源以確定表單及其片段之間的依賴關係。 例如，如果您有表單，則可以確定它使用的片段或外部資源。 如果您有影像，您還可以查找使用影像的表單。 您還可以使用基於屬性的篩選來搜索相關資源。 例如，您可以搜索使用具有指定名稱的影像的所有表單，或查找具有指定名稱的表單使用的任何影像。 您也可以使用資源屬性進行搜索。 例如，您可以執行查詢以查找其名稱以給定字串開頭的所有表單或資源，該字串可能包括「%」和「_」通配符。 請記住，基於屬性的搜索不是基於關係的；此類搜索基於您對給定資源具有特定知識的假設。

**查詢語句**

A *查詢* 包含一個或多個與條件邏輯連接的語句。 A *語句* 由左操作數、運算子和右操作陣列成。 此外，還可以指定用於搜索結果的排序順序。 的 *排序順序* 包含與SQL等效的資訊 `ORDER BY` 子句，由包含搜索所基於的屬性的元素以及指示將使用升序還是降序的值組成。

可以使用Repository服務Java API以寫程式方式搜索資源。 此時，無法使用Web服務API來搜索資源。

**排序行為**

調用時不遵守排序順序 `ResourceRepositoryClient` 對象 `searchProperties` 方法和指定排序順序。 例如，假定您建立了具有三個自定義屬性的資源，其中屬性名稱為 `name`。 `secondName`, `asecondName`。 然後，在屬性名稱上建立排序順序元素並設定 `ascending` 值 `true`。

然後調用 `ResourceRepositoryClient` 對象 `searchProperties` 按排序順序傳遞。 搜索返回具有三個屬性的正確資源。 但是，屬性不按屬性名稱排序。 按添加順序返回： `name`。 `secondName`, `asecondName`。

>[!NOTE]
>
>有關儲存庫服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-5}

要搜索資源，請執行以下步驟：

1. 包括項目檔案。
1. 建立儲存庫服務客戶端。
1. 指定搜索的目標資料夾。
1. 指定搜索中使用的屬性。
1. 建立搜索中使用的查詢。
1. 建立搜索結果的排序順序。
1. 搜索資源。
1. 從搜索結果中檢索資源。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請包括代理檔案。

**建立服務客戶端**

在以寫程式方式讀取資源之前，必須建立連接並提供憑據。 這是通過建立服務客戶端來實現的。

**指定搜索的目標資料夾**

建立包含用於執行搜索的基本路徑的字串。 語法包括正斜槓，如本示例所示：&quot;/*路徑*/*資料夾*。

**指定搜索中使用的屬性**

您可以根據資源中包含的屬性進行搜索。 指定要在其上執行搜索的屬性的值。

**建立搜索中使用的查詢**

使用語句和條件構造查詢。 每個語句都將指定搜索所基於的屬性、要使用的條件以及要在搜索中使用的屬性值。

**建立搜索結果的排序順序**

排序順序由元素組成，每個元素都包含搜索中使用的屬性之一以及指示將使用升序還是降序的值。

**搜索資源**

使用資料夾、查詢和排序順序搜索資源。 此外，還指明搜索深度和要返回結果數的上限。

**從搜索結果中檢索資源**

循環訪問返回的資源清單並提取資訊以供進一步處理。

**另請參閱**

[使用Java API搜索資源](aem-forms-repository.md#search-for-resources-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API搜索資源 {#search-for-resources-using-the-java-api}

使用Repository服務API(Java)搜索資源：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案。

1. 建立服務客戶端

   建立 `ResourceRepositoryClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 指定搜索的目標資料夾

   指定要從中執行搜索的基本路徑的URI。 在此示例中，資源的URI為 `/testFolder`。

1. 指定搜索中使用的屬性

   指定要在其上執行搜索的屬性的值。 屬性存在於 `com.adobe.repository.infomodel.bean.Resource` 的雙曲餘切值。 在本示例中，將對name屬性進行搜索；因此， `java.lang.String` 包含 `Resource` 使用對象的名稱，即 `testResource` 在這個例子中。

1. 建立搜索中使用的查詢

   要建立查詢，請建立 `com.adobe.repository.query.Query` 對象，方法是為 `Query` 類和向查詢添加語句。

   要建立語句，請調用 `com.adobe.repository.query.Query.Statement` 類和傳遞的參數如下：

   * 包含資源屬性常數的左操作數。 在本示例中，由於資源的名稱用作搜索的基礎，因此靜態值 `Resource.ATTRIBUTE_NAME` 的子菜單。
   * 包含搜索屬性時使用的條件的運算子。 運算子必須是 `Query.Statement` 類。 在本示例中，靜態值 `Query.Statement.OPERATOR_BEGINS_WITH` 的子菜單。
   * 右操作數，包含要在其上執行搜索的屬性值。 在此示例中， name屬性， `String` 包含值 `"testResource"`的子菜單。

   通過調用 `Query.Statement` 對象 `setNamespace` 方法並傳遞包含在 `com.adobe.repository.infomodel.bean.ResourceProperty` 類。 在本例中， `ResourceProperty.RESERVED_NAMESPACE_REPOSITORY` 的子菜單。

   通過調用 `Query` 對象 `addStatement` 方法和傳遞 `Query.Statement` 的雙曲餘切值。

1. 建立搜索結果的排序順序

   要指定搜索結果中使用的排序順序，請建立 `com.adobe.repository.query.sort.SortOrder` 對象，方法是為 `SortOrder` 類，並將元素添加到排序順序。

   要為排序順序建立元素，請為 `com.adobe.repository.query.sort.SortOrder.Element` 類。 在本示例中，由於資源的名稱用作搜索的基礎，因此靜態值 `Resource.ATTRIBUTE_NAME` 用作第一個參數，並按升序(a `boolean` 值 `true`)指定為第二個參數。

   通過調用 `SortOrder` 對象 `addSortElement` 方法和傳遞 `SortOrder.Element` 的雙曲餘切值。

1. 搜索資源

   搜索 `resources` 基於屬性，調用 `ResourceRepositoryClient` 對象 `searchProperties` 方法和傳遞以下參數：

   * A `String` 包含要從中執行搜索的基本路徑。 在這個例子中， `"/testFolder"` 的子菜單。
   * 搜索中使用的查詢。
   * 搜索深度。 在這個例子中， `com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE` 用於指示要使用基本路徑及其所有資料夾。
   * 安 `int` 值，指示要從中選擇未分頁結果集的第一行。 在本例中， `0` 。
   * 安 `int` 值，指示要返回的結果的最大數量。 在本例中， `10` 。
   * 搜索中使用的排序順序。

   該方法返回 `java.util.List` 共 `Resource` 按指定的排序順序排列對象。

1. 從搜索結果中檢索資源

   要檢索搜索結果中包含的資源，請循環訪問 `List` 將每個對象 `Resource` 以便提取其資訊。 在此示例中，將顯示每個資源的名稱。

**另請參閱**

[搜索資源](aem-forms-repository.md#searching-for-resources)

[快速啟動（SOAP模式）:使用Java API搜索資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 建立資源關係 {#creating-resource-relationships}

您可以指定儲存庫中資源之間的關係。 有三種關係：

* **依賴**:資源依賴於其他資源的關係，這意味著儲存庫中需要所有相關資源。
* **成員資格（檔案系統）**:資源位於給定資料夾中的關係。
* **自定義**:您在資源之間指定的關係。 例如，如果一個資源已被棄用，而另一個資源被引入儲存庫，則可以指定您自己的替換關係。

您可以建立自己的自定義關係。 例如，如果將HTML檔案儲存在儲存庫中，並且它使用了映像，則可以指定將HTML檔案與映像關聯的自定義關係（因為通常只有XML檔案與使用儲存庫定義的依賴關係的影像關聯）。 自定義關係的另一個示例是，如果您希望使用循環圖結構而不是樹結構構建儲存庫的不同視圖。 可以定義圓形圖形和查看器來遍歷這些關係。 最後，您可以指示資源替代了另一個資源，即使這兩個資源完全不同。 在這種情況下，您可以定義保留範圍之外的關係類型，並在這兩個資源之間建立關係。 您的應用程式將是唯一能夠檢測和處理該關係的客戶端，並且它可用於對該關係執行搜索。

可以使用Repository服務Java API或Web服務API以寫程式方式指定資源之間的關係。

>[!NOTE]
>
>有關儲存庫服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-6}

要指定兩個資源之間的關係，請執行以下步驟：

1. 包括項目檔案。
1. 建立儲存庫服務客戶端。
1. 指定要關聯的資源的URI。
1. 建立關係。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請包括代理檔案。

**建立服務客戶端**

在以寫程式方式讀取資源之前，必須建立連接並提供憑據。 這是通過建立服務客戶端來實現的。

**指定要相關的資源的URI**

建立包含要相關的資源的URI的字串。 語法包括正斜槓，如本示例所示：&quot;/*路徑*/*資源*。

**建立關係**

調用儲存庫服務方法以建立和指定關係類型。

**另請參閱**

[使用Java API建立關係資源](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[使用Web服務API建立關係資源](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API建立關係資源 {#create-relationship-resources-using-the-java-api}

使用Repository服務Java API建立關係資源，執行以下任務：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案。

1. 建立服務客戶端

   建立 `ResourceRepositoryClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 指定要相關的資源的URI

   指定要關聯的資源的URI。 在本例中，因為資源被命名 `testResource1` 和 `testResource2` 位於名為 `testFolder`，其URI為 `"/testFolder/testResource1"` 和 `"/testFolder/testResource2"`。 URI儲存為 `java.lang.String` 對象。 在此示例中，資源首先寫入儲存庫，並檢索其URI。 有關編寫資源的詳細資訊，請參見 [編寫資源](aem-forms-repository.md#writing-resources)。

1. 建立關係

   調用 `ResourceRepositoryClient` 對象 `createRelationship` 方法和傳遞以下參數：

   * 源資源的URI。
   * 目標資源的URI。
   * 關係類型，它是 `com.adobe.repository.infomodel.bean.Relation` 類。 在本示例中，通過指定值來建立依賴關係 `Relation.TYPE_DEPENDANT_OF`。
   * A `boolean` 值指示是否將目標資源自動更新為 `com.adobe.repository.infomodel.Id`基於新頭資源的標識符。 在此示例中，由於依賴關係， `true` 。

   也可以通過調用 `ResourceRepositoryClient` 對象 `getRelated` 方法並傳遞以下參數：

   * 要為其檢索相關資源的資源的URI。 在本示例中，源資源( `"/testFolder/testResource1"`)。
   * A `boolean` 值，指示指定的資源是否是關係中的源資源。 在此示例中， `true` 已指定，因為此情況。
   * 關係類型，是 `Relation` 類。 在本示例中，使用先前使用的相同值指定依賴關係： `Relation.TYPE_DEPENDANT_OF`。

   的 `getRelated` 方法返回 `java.util.List` 共 `Resource` 可通過其迭代以檢索每個相關資源的對象，並轉換包含在 `List` 至 `Resource` 就像你一樣。 在本例中， `testResource2` 預計將在返回的資源清單中。

**另請參閱**

[建立資源關係](aem-forms-repository.md#creating-resource-relationships)

[快速啟動（SOAP模式）:使用Java API建立資源之間的關係](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API建立關係資源 {#create-relationship-resources-using-the-web-service-api}

使用Repository API（Web服務）建立關係資源：

1. 包括項目檔案

   * 建立使用儲存庫WSDL的Microsoft.NET客戶端程式集。
   * 引用Microsoft.NET客戶端程式集。

1. 建立服務客戶端

   使用Microsoft.NET客戶端程式集，建立 `RepositoryServiceService` 調用其預設建構子。 設定 `Credentials` 屬性使用 `System.Net.NetworkCredential` 包含用戶名和密碼的對象。

1. 指定要相關的資源的URI

   指定要關聯的資源的URI。 在本例中，因為資源被命名 `testResource1` 和 `testResource2` 位於名為 `testFolder`，其URI為 `"/testFolder/testResource1"` 和 `"/testFolder/testResource2"`。 使用與Microsoft.NET Framework（例如C#）相容的語言時，URI將儲存為 `System.String` 對象。 在此示例中，資源首先寫入儲存庫，並檢索其URI。 有關編寫資源的詳細資訊，請參見 [編寫資源](aem-forms-repository.md#writing-resources)。

1. 建立關係

   調用 `RepositoryServiceService` 對象 `createRelationship` 方法和傳遞以下參數：

   * 源資源的URI。
   * 目標資源的URI。
   * 關係類型。 在本示例中，通過指定值來建立依賴關係 `3`。
   * A `boolean` 值，指示是否指定了關係類型。 在此示例中， `true` 。
   * A `boolean` 值指示是否將目標資源自動更新為 `Id`基於新頭資源的標識符。 在此示例中，由於依賴關係， `true` 。
   * A `boolean` 指示是否指定了目標頭的值。 在此示例中， `true` 。
   * 通過 `null` 的雙曲餘切值。

   也可以通過調用 `RepositoryServiceService` 對象 `getRelated` 方法並傳遞以下參數：

   * 要為其檢索相關資源的資源的URI。 在本示例中，源資源( `"/testFolder/testResource1"`)。
   * A `boolean` 值，指示指定的資源是否是關係中的源資源。 在此示例中， `true` 已指定，因為此情況。
   * A `boolean` 值，指示是否指定了源資源。 在此示例中， `true` 的下界。
   * 包含關係類型的整數陣列。 在本示例中，依賴關係是通過在陣列中使用與前面使用的值相同的值來指定的： `3`。
   * 通過 `null` 的下界。

   的 `getRelated` 方法返回可轉換到的對象陣列 `Resource` 可通過對象進行迭代以檢索每個相關資源。 在本例中， `testResource2` 預計將在返回的資源清單中。

**另請參閱**

[建立資源關係](aem-forms-repository.md#creating-resource-relationships)

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 鎖定資源 {#locking-resources}

您可以鎖定資源或一組資源以供特定用戶獨佔使用或在多個用戶之間共用使用。 共用鎖表示資源將發生某種情況，但不會阻止其他任何人對該資源執行操作。 共用鎖應視為信令機制。 獨佔鎖表示鎖定資源的用戶將更改資源，而鎖則確保在用戶不再需要訪問該資源並已釋放該鎖之前，其他人不能更改。 如果儲存庫管理員解鎖某個資源，則該資源上的所有獨佔和共用鎖將自動刪除。 此類操作針對用戶不再可用且未解鎖資源的情況。

鎖定資源時，在查看位於Workbench中的「資源」標籤時，會出現鎖定表徵圖，如下圖所示。

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

可以使用Repository服務Java API或Web服務API以寫程式方式控制對資源的訪問。

>[!NOTE]
>
>有關儲存庫服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-7}

要鎖定和解鎖資源，請執行以下步驟：

1. 包括項目檔案。
1. 建立儲存庫服務客戶端。
1. 指定要鎖定的資源的URI。
1. 鎖定資源。
1. 檢索資源的鎖。
1. 解除鎖定資源

**包括項目檔案**

在開發項目中包括必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請包括代理檔案。

**建立服務客戶端**

在以寫程式方式讀取資源之前，必須建立連接並提供憑據。 這是通過建立服務客戶端來實現的。

**指定要鎖定的資源的URI**

建立包含要鎖定的資源的URI的字串。 語法包括正斜槓，如本示例所示：&quot;/*路徑*/*資源*。

**鎖定資源**

調用儲存庫服務方法以鎖定資源，指定URI、鎖定類型和鎖定深度。

**檢索資源的鎖**

調用Repository服務方法以檢索資源的鎖，並指定URI。

**解除鎖定資源**

調用儲存庫服務方法來解鎖資源，指定URI。

**另請參閱**

[使用Java API鎖定資源](aem-forms-repository.md#lock-resources-using-the-java-api)

[使用Web服務API鎖定資源](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API鎖定資源 {#lock-resources-using-the-java-api}

使用Repository服務API(Java)鎖定資源：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案。

1. 建立服務客戶端

   建立 `ResourceRepositoryClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 指定要鎖定的資源的URI

   指定要鎖定的資源的URI。 在本例中，因為名為 `testResource` 位於名為 `testFolder`，其URI為 `"/testFolder/testResource"`。 URI儲存為 `java.lang.String` 的雙曲餘切值。

1. 鎖定資源

   調用 `ResourceRepositoryClient` 對象 `lockResource` 方法和傳遞以下參數：

   * 資源的URI。
   * 鎖定範圍。 在本示例中，由於將鎖定資源以供獨佔使用，因此將鎖定範圍指定為 `com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`。
   * 鎖的深度。 在本示例中，由於鎖定將僅應用於特定資源且不應用其任何成員或子項，因此鎖定深度將指定為 `Lock.DEPTH_ZERO`。

   >[!NOTE]
   >
   >的重載版本 `lockResource` 需要四個參數的方法會引發異常。 確保使用 `lockResource` 方法，該方法需要三個參數，如本步驟所示。

1. 檢索資源的鎖

   調用 `ResourceRepositoryClient` 對象 `getLocks` 方法，並將資源的URI作為參數傳遞。 該方法返回可通過其迭代的鎖對象清單。 在本示例中，通過調用每個Lock對象的 `getOwnerUserId`。 `getDepth`, `getType` 方法。

1. 解除鎖定資源

   調用 `ResourceRepositoryClient` 對象 `unlockResource` 方法，並將資源的URI作為參數傳遞。 有關詳細資訊，請參見 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**另請參閱**

[鎖定資源](aem-forms-repository.md#locking-resources)

[快速啟動（SOAP模式）:使用Java API鎖定資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API鎖定資源 {#lock-resources-using-the-web-service-api}

使用Repository服務API（Web服務）鎖定資源：

1. 包括項目檔案

   * 使用Base64建立使用儲存庫WSDL的Microsoft.NET客戶端程式集。
   * 引用Microsoft.NET客戶端程式集。

1. 建立服務客戶端

   使用Microsoft.NET客戶端程式集，建立 `RepositoryServiceService` 調用其預設建構子。 設定 `Credentials` 屬性使用 `System.Net.NetworkCredential` 包含用戶名和密碼的對象。

1. 指定要鎖定的資源的URI

   指定包含要鎖定的資源的URI的字串。 在本例中，因為名為 `testResource` 在資料夾中 `testFolder`，其URI為 `"/testFolder/testResource"`。 使用與Microsoft.NET Framework（例如C#）相容的語言時，將URI儲存在 `System.String` 的雙曲餘切值。

1. 鎖定資源

   調用 `RepositoryServiceService` 對象 `lockResource` 方法和傳遞以下參數：

   * 資源的URI。
   * 鎖定範圍。 在本示例中，由於將鎖定資源以供獨佔使用，因此將鎖定範圍指定為 `11`。
   * 鎖的深度。 在本示例中，由於鎖定將僅應用於特定資源且不應用其任何成員或子項，因此鎖定深度將指定為 `2`。
   * 安 `int` 值，指示鎖定到期前的秒數。 在此示例中， `1000` 的子菜單。
   * 通過 `null` 的雙曲餘切值。

1. 檢索資源的鎖

   調用 `RepositoryServiceService` 對象 `getLocks` 將資源的URI作為第一個參數和 `null` 的雙曲餘切值。 該方法返回 `object` 陣列 `Lock` 可通過其迭代的對象。 在本示例中，通過訪問每個對象，為每個對象打印鎖所有者、深度和範圍 `Lock` 對象 `ownerUserId`。 `depth`, `type` 的下界。

1. 解除鎖定資源

   調用 `RepositoryServiceService` 對象 `unlockResource` 將資源的URI作為第一個參數和 `null` 的雙曲餘切值。

**另請參閱**

[鎖定資源](aem-forms-repository.md#locking-resources)

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 刪除資源 {#deleting-resources}

可以使用儲存庫服務Java API(SOAP)從儲存庫中的給定位置以寫程式方式刪除資源。

刪除資源時，刪除通常是永久的，但在某些情況下， ECM儲存庫可能會根據資源的歷史機制儲存資源的版本。 因此，刪除資源時，必須確保不再需要該資源。 刪除資源的常見原因包括需要增加資料庫中的可用空間。 您可以刪除資源的版本，但是如果刪除，則必須指定資源標識符，而不是其邏輯標識符(LID)或路徑。 如果刪除資料夾，則該資料夾中的所有內容（包括子資料夾和資源）將自動刪除。

未刪除相關資源。 例如，如果您的表單使用logo.gif檔案，而您刪除logo.gif，則關係將儲存在掛起的關係表中。 作為替代方法，對於版本棄用，請將最新版本的對象狀態設定為不建議使用。

刪除操作在ECM系統中不是事務安全的。 例如，如果嘗試刪除100個資源，並且第50個資源上的操作失敗，則前49個實例將被刪除，但其餘實例將不會刪除。 否則，預設行為為回退（非承諾）。

>[!NOTE]
>
>使用 `com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()` 方法(EMC Documentum Content Server和IBMFileNet P8 Content Manager)，如果某個指定資源的刪除失敗，則不會回滾事務，這意味著無法刪除那些已刪除的檔案。

>[!NOTE]
>
>有關儲存庫服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-8}

要刪除資源，請執行以下步驟：

1. 包括項目檔案。
1. 建立儲存庫服務客戶端。
1. 指定要刪除的資源的URI。
1. 刪除資源。

**包括項目檔案**

在開發項目中包括必要的檔案。 如果使用Java建立客戶端應用程式，請包括必要的JAR檔案。 如果使用Web服務，請包括代理檔案。

**建立服務客戶端**

在以寫程式方式讀取資源之前，必須建立連接並提供憑據。 這是通過建立服務客戶端來實現的。

**指定要刪除的資源的URI**

建立包含要刪除的資源的URI的字串。 語法包括正斜槓，如本示例所示：&quot;/*路徑*/*資源*。 如果要刪除的資源是資料夾，則刪除將是遞歸的。

**刪除資源**

調用Repository服務方法以刪除資源，並指定URI。

**另請參閱**

[使用Java API刪除資源](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[使用Web服務API刪除資源](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[儲存庫服務API快速啟動](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### 使用Java API(SOAP)刪除資源 {#delete-resources-using-the-java-api-soap}

使用Repository API(Java)刪除資源：

1. 包括項目檔案

   在Java項目的類路徑中包括客戶端JAR檔案。

1. 建立服務客戶端

   建立 `ResourceRepositoryClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 包含連接屬性的對象。

1. 指定要刪除的資源的URI

   指定要檢索的資源的URI。 在這種情況下，由於名為testResourceToBeDeleted的資源位於名為testFolder的資料夾中，因此其URI為 `/testFolder/testResourceToBeDeleted`。 URI儲存為 `java.lang.String` 的雙曲餘切值。 在此示例中，資源首先寫入儲存庫，並檢索其URI。 有關編寫資源的詳細資訊，請參見 [編寫資源](aem-forms-repository.md#writing-resources)。

1. 刪除資源

   調用 `ResourceRepositoryClient` 對象 `deleteResource` 方法，並將資源的URI作為參數傳遞。

**另請參閱**

[刪除資源](aem-forms-repository.md#deleting-resources)

[快速啟動（SOAP模式）:使用Java API搜索資源](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服務API刪除資源 {#delete-resources-using-the-web-service-api}

使用Repository API（Web服務）刪除資源：

1. 包括項目檔案

   * 使用Base64建立使用儲存庫WSDL的Microsoft.NET客戶端程式集。
   * 引用Microsoft.NET客戶端程式集。

1. 建立服務客戶端

   使用Microsoft.NET客戶端程式集，建立 `RepositoryServiceService` 調用其預設建構子。 設定 `Credentials` 屬性使用 `System.Net.NetworkCredential` 包含用戶名和密碼的對象。

1. 指定要刪除的資源的URI

   指定要檢索的資源的URI。 在本例中，因為名為 `testResourceToBeDeleted` 位於名為 `testFolder`，其URI為 `"/testFolder/testResourceToBeDeleted"`。 在此示例中，資源首先寫入儲存庫，並檢索其URI。 有關編寫資源的詳細資訊，請參見 [編寫資源](aem-forms-repository.md#writing-resources)。

1. 刪除資源

   調用 `RepositoryServiceService` 對象 `deleteResources` 方法和通過 `System.String` 包含資源的URI作為第一個參數的陣列。 通過 `null` 的雙曲餘切值。

**另請參閱**

[刪除資源](aem-forms-repository.md#deleting-resources)

[使用Base64編碼調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
