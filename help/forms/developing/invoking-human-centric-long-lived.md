---
title: 調用以人為中心的長壽命進程
seo-title: Invoking Human-Centric Long-Lived Processes
description: 以寫程式方式調用在Workbench中使用基於Java的客戶端應用程式（使用調用API）建立的以人為中心的長壽命進程、使用Web服務的ASP.NET應用程式以及使用遠程處理的Flex構建的客戶端應用程式。
seo-description: Programmatically invoke human-centric long-lived processes created in Workbench using a Java web-based client application that uses the Invocation API, an ASP.NET application that uses web services, and a client application built with Flex that uses Remoting.
uuid: 42269d41-a90f-4ea1-aeb9-d61337bcfa54
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 18a320b4-dce6-4c50-8864-644b0b2d6644
role: Developer
exl-id: c9ebad8b-b631-492d-99a3-094e892b2ddb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3699'
ht-degree: 0%

---

# 調用以人為中心的長壽命進程 {#invoking-human-centric-long-lived-processes}

您可以通過以下客戶端應用程式以寫程式方式調用在Workbench中建立的以人為中心的長期流程：

* 使用調用API的基於Java Web的客戶端應用程式。 (請參閱 [使用Java API調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md)(/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)。)
* 使用Web服務的ASP.NET應用程式。 (請參閱 [使用Web服務調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)。)
* 使用Flex構建的使用遠程處理的客戶端應用程式。 (請參閱 [調用AEM Forms使用(不建議AEM用於表單)AEM Forms遠程處理](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)。)

調用的長壽命進程名為 *FirstAppSolution/PreLoanProcess*。 您可以按照中指定的教程建立此過程 [建立第一個AEM Forms應用程式](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63)。

以人為中心的流程涉及用戶可以使用Workspace對其進行響應的任務。 例如，使用Workbench，您可以建立一個流程，讓銀行經理審批或拒絕貸款申請。 下圖顯示了該進程 *FirstAppSolution/PreLoanProcess*。

的 *FirstAppSolution/PreLoanProcess* 進程接受名為 *表單資料* 其資料類型為XML。 XML資料與名為 *PreLoanForm.xdp*。 下圖顯示了一個表單，它表示分配給用戶以批准或拒絕貸款申請的任務。 用戶使用Workspace批准或拒絕應用程式。 Workspace用戶可以通過按一下下圖中顯示的「批准」按鈕來批准貸款請求。 同樣，用戶可以通過按一下拒絕按鈕來拒絕貸款請求。

長壽命進程被非同步調用，由於以下因素，無法同步調用：

* 進程可以跨越大量時間。
* 流程可以跨越組織邊界。
* 進程需要外部輸入才能完成。 例如，請考慮將表單發送給不在辦公室的經理的情況。 在這種情況下，只有經理返回並填寫表單後，該過程才會完成。

調用長壽命進程時，AEM Forms會建立調用標識符值，作為建立記錄的一部分。 記錄跟蹤長期進程的狀態，並儲存在AEM Forms資料庫中。 使用調用標識符值，可以跟蹤長壽命進程的狀態。 此外，您可以使用進程調用標識符值來執行進程管理器操作，如終止正在運行的進程實例。

>[!NOTE]
>
>AEM Forms在調用短時間進程時不會建立調用標識符值或記錄。

的 `FirstAppSolution/PreLoanProcess` 當申請人提交以XML資料表示的申請時，將調用進程。 輸入進程變數的名稱為 `formData` 其資料類型為XML。 在本討論中，假定以下XML資料用作 `FirstAppSolution/PreLoanProcess` 處理。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <LoanApp>
 <Name>Sam White</Name>
 <LoanAmount>250000</LoanAmount>
 <PhoneOrEmail>(555)555-5555</PhoneOrEmail>
 <ApprovalStatus>PENDING APPROVAL</ApprovalStatus>
 </LoanApp>
```

傳遞給進程的XML資料必須與進程中使用的表單中的欄位匹配。 否則，資料不會顯示在表單中。 調用 `FirstAppSolution/PreLoanProcess` 進程必須傳遞此XML資料源。 在中建立的應用程式 *調用以人為中心的長壽命進程* 根據用戶輸入到Web客戶端的值動態建立XML資料源。

使用客戶端應用程式，可以 *FirstAppSolution/PreLoanProcess* 處理所需的XML資料。 長壽命進程返回調用標識符值作為其返回值。 下圖顯示了調用*FirstAppSolution/PreLoanProcess長期進程的客戶端應用程式。 客戶端應用程式發送XML資料並返回表示調用標識符值的字串值。

**另請參閱**

[建立調用以人為中心的長壽命進程的Java Web應用程式](invoking-human-centric-long-lived.md#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process)

[建立ASP.NET Web應用程式，該應用程式調用以人為中心的長壽命進程](invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

[建立使用Flex構建的客戶端應用程式，該應用程式調用以人為中心的長壽命流程](invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

## 建立調用以人為中心的長壽命進程的Java Web應用程式 {#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process}

您可以建立基於Web的應用程式，該應用程式使用Java Servlet來調用 `FirstAppSolution/PreLoanProcess` 處理。 要從Java Servlet調用此進程，請使用Java Servlet中的調用API。 (請參閱 [使用Java API調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)。)

下圖顯示了基於Web的客戶端應用程式，該應用程式會發佈名稱、電話（或電子郵件）和金額值。 當用戶按一下「提交應用程式」按鈕時，這些值將發送到Java servlet。

Java Servlet執行以下任務：

* 檢索從HTML頁發佈到Java Servlet的值。
* 動態建立要傳遞到 *FirstAppSolution/PreLoanProcess* 處理。 名稱、電話（或電子郵件）和金額值在XML資料源中指定。
* 調用 *FirstAppSolution/PreLoanProcess* 調用API。
* 將調用標識符值返回到客戶端Web瀏覽器。

### 步驟摘要 {#summary-of-steps}

建立調用Java Web的應用程式 `FirstAppSolution/PreLoanProcess` 執行以下步驟：

1. [建立Web項目](invoking-human-centric-long-lived.md#create-a-web-project)。
1. [為servlet建立Java應用程式邏輯](invoking-human-centric-long-lived.md#create-java-application-logic-for-the-servlet)。
1. [為Web應用程式建立網頁](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)
1. [將Web應用程式打包到WAR檔案](invoking-human-centric-long-lived.md#package-the-web-application-to-a-war-file)。
1. [將WAR檔案部署到托管AEM Forms的J2EE應用程式伺服器](invoking-human-centric-long-lived.md#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms)。
1. [TestWeb應用程式](invoking-human-centric-long-lived.md#test-your-web-application)。

>[!NOTE]
>
>其中一些步驟取決於部署了AEM Forms的J2EE應用程式。 例如，您用於部署WAR檔案的方法取決於您所使用的J2EE應用程式伺服器。 假定AEM Forms部署在JBoss®上。

### 建立Web項目 {#create-a-web-project}

建立Web應用程式的第一步是建立Web項目。 本文檔所基於的Java IDE是Eclipse 3.3。使用Eclipse IDE，建立Web項目，並將所需的JAR檔案添加到項目中。 添加名為的HTML頁 *索引.html*  和Java Servlet。

以下清單指定要包含在Web項目中的JAR檔案：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* J2EE.jar

有關這些JAR檔案的位置，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

>[!NOTE]
>
>J2EE.jar檔案定義Java Servlet使用的資料類型。 可以從部署了AEM Forms的J2EE應用程式伺服器獲取此JAR檔案。

**建立Web項目**

1. 啟動Eclipse並按一下 **檔案** >  **新建項目**。
1. 在 **新建項目** 對話框，選擇 **Web** > **動態Web項目**。
1. 類型 `InvokePreLoanProcess` ，然後按一下 **完成**。

**將所需的JAR檔案添加到項目**

1. 在「項目瀏覽器」窗口中，按一下右鍵 `InvokePreLoanProcess` 項目和選擇 **屬性**。
1. 按一下 **Java生成路徑** 然後按一下 **庫** 頁籤。
1. 按一下 **添加外部JAR** 按鈕並瀏覽到要包括的JAR檔案。

**將Java Servlet添加到項目**

1. 在「項目瀏覽器」窗口中，按一下右鍵 `InvokePreLoanProcess` 項目和選擇 **新建** >  **其他**。
1. 展開 **Web** 資料夾，選擇 **Servlet**，然後按一下 **下一個**。
1. 在「建立Servlet」對話框中，鍵入 `SubmitXML` ，然後按一下 **完成**。

**向項目添加HTML頁**

1. 在「項目瀏覽器」窗口中，按一下右鍵 `InvokePreLoanProcess` 項目和選擇 **新建** > **其他**。
1. 展開 **Web** 資料夾，選擇 **HTML**，然後按一下 **下一個**。
1. 在「新建HTML」對話框中，鍵入 `index.html` ，然後按一下 **完成**。

>[!NOTE]
>
>有關建立調用SubmitXML Java Servlet的HTML內容的資訊，請參見 [為Web應用程式建立網頁](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)。

### 為servlet建立Java應用程式邏輯 {#create-java-application-logic-for-the-servlet}

建立調用 `FirstAppSolution/PreLoanProcess` 從Java Servlet中進行處理。 以下代碼顯示 `SubmitXML` Java Servlet:

```java
     public class SubmitXML extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
         doPost(req,resp);
 
         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
             //Add code here to invoke the FirstAppSolution/PreLoanProcess process
             }
```

通常，不會將客戶端代碼放在Java Servlet中 `doGet` 或 `doPost` 的雙曲餘切值。 更好的寫程式實踐是將此代碼放在單獨的類中。 然後，在 `doPost` 方法 `doGet` 方法)，並調用相應的方法。 但是，對於代碼的簡短性，代碼示例將保持為最小值，並放置在 `doPost` 的雙曲餘切值。

調用 `FirstAppSolution/PreLoanProcess` 調用API的進程，執行以下任務：

1. 在Java項目的類路徑中包括客戶端JAR檔案，如adobe-liveccycle-client.jar。 有關這些檔案位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。
1. 檢索從HTML頁提交的名稱、電話和金額值。 使用這些值動態建立發送到 `FirstAppSolution/PreLoanProcess` 處理。 您可以使用 `org.w3c.dom` 類以建立XML資料源（以下代碼示例中顯示了此應用程式邏輯）。
1. 建立 `ServiceClientFactory` 包含連接屬性的對象。 (請參閱 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)
1. 建立 `ServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。 A `ServiceClient` object用於調用服務操作。 它處理諸如查找、調度和路由調用請求等任務。
1. 建立 `java.util.HashMap` 對象。
1. 調用 `java.util.HashMap` 對象 `put` 方法將每個輸入參數傳遞給長壽命過程。 確保指定進程的輸入參數的名稱。 因為 `FirstAppSolution/PreLoanProcess` 進程需要一個類型的輸入參數 `XML` （命名） `formData`)，您只需調用 `put` 方法。

   ```java
    //Get the XML to pass to the FirstAppSolution/PreLoanProcess process
    org.w3c.dom.Document inXML = GetDataSource(name,phone,amount);
    
    //Create a Map object to store the parameter value
    Map params = new HashMap();
    params.put("formData", inXML);
   ```

1. 建立 `InvocationRequest` 通過調用 `ServiceClientFactory` 對象 `createInvocationRequest` 方法並傳遞以下值：

   * 一個字串值，它指定要調用的長壽命進程的名稱。 調用 `FirstAppSolution/PreLoanProcess` 進程，指定 `FirstAppSolution/PreLoanProcess`。
   * 表示流程操作名稱的字串值。 長壽命流程操作的名稱為 `invoke`。
   * 的 `java.util.HashMap` 包含服務操作所需的參數值的對象。
   * 一個布爾值，它指定 `false`，建立非同步請求（此值適用於調用長壽命進程）。

   >[!NOTE]
   >
   >*通過將值true作為createInvocationRequest方法的第四個參數傳遞，可以調用短時間進程。 傳遞值true將建立同步請求。*

1. 通過調用 `ServiceClient` 對象 `invoke` 方法和傳遞 `InvocationRequest` 的雙曲餘切值。 的 `invoke` 方法返回 `InvocationReponse` 的雙曲餘切值。
1. 長壽命進程返回表示調用標識值的字串值。 通過調用 `InvocationReponse` 對象 `getInvocationId` 的雙曲餘切值。

   ```java
    //Send the invocation request to the long-lived process and
    //get back an invocation response object
    InvocationResponse lcResponse = myServiceClient.invoke(lcRequest);
    String invocationId = lcResponse.getInvocationId();
   ```

1. 將調用標識值寫入客戶端Web瀏覽器。 您可以使用 `java.io.PrintWriter` 將此值寫入客戶端web瀏覽器的實例。

### 快速啟動：使用調用API調用長壽命進程 {#quick-start-invoking-a-long-lived-process-using-the-invocation-api}

以下Java代碼示例表示調用 `FirstAppSolution/PreLoanProcess` 處理。

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-livecycle-client.jar
     * 2. adobe-usermanager-client.jar
     *
     * (Because this  quick start is implemented as a Java servlet, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     * */
 import java.io.ByteArrayOutputStream;
 import java.io.File;
 import java.io.IOException;
 import java.io.PrintWriter;
 
 import javax.servlet.ServletException;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import java.util.*;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import javax.xml.parsers.DocumentBuilder;
 import javax.xml.parsers.DocumentBuilderFactory;
 import javax.xml.transform.Transformer;
 import javax.xml.transform.TransformerFactory;
 import javax.xml.transform.dom.DOMSource;
 import javax.xml.transform.stream.StreamResult;
 
 import com.adobe.idp.dsc.InvocationRequest;
 import com.adobe.idp.dsc.InvocationResponse;
 import com.adobe.idp.dsc.clientsdk.ServiceClient;
 import org.w3c.dom.Element;
 
     public class SubmitXML extends javax.servlet.http.HttpServlet implements javax.servlet.Servlet {
       static final long serialVersionUID = 1L;
 
        public SubmitXML() {
         super();
     }
 
 
     protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
         // TODO Auto-generated method stub
         doPost(request,response);
     }
 
     protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a ServiceClient object
             ServiceClient myServiceClient = myFactory.getServiceClient();
 
             //Get the values that are passed from the Loan HTML page
             String name = (String)request.getParameter("name");
             String phone = (String)request.getParameter("phone");
             String amount = (String)request.getParameter("amount");
 
             //Create XML to pass to the FirstAppSolution/PreLoanProcess process
             org.w3c.dom.Document inXML = GetDataSource(name,phone,amount);
 
             //Create a Map object to store the XML input parameter value
             Map params = new HashMap();
             params.put("formData", inXML);
 
             //Create an InvocationRequest object
             InvocationRequest lcRequest =  myFactory.createInvocationRequest(
                 "FirstAppSolution/PreLoanProcess", //Specify the long-lived process name
                     "invoke",           //Specify the operation name
                     params,               //Specify input values
                     false);               //Create an asynchronous request
 
             //Send the invocation request to the long-lived process and
             //get back an invocation response object
             InvocationResponse lcResponse = myServiceClient.invoke(lcRequest);
             String invocationId = lcResponse.getInvocationId();
 
             //Create a PrintWriter instance
             PrintWriter pp = response.getWriter();
 
             //Write the invocation identifier value back to the client web browser
             pp.println("The job status identifier value is: " +invocationId);
 
         }catch (Exception e) {
              System.out.println("The following exception occurred: "+e.getMessage());
       }
     }
 
 
      //Create XML data to pass to the long-lived process
      private static org.w3c.dom.Document GetDataSource(String name, String phone, String amount)
      {
             org.w3c.dom.Document document = null;
 
             try
             {
                 //Create DocumentBuilderFactory and DocumentBuilder objects
                 DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
                 DocumentBuilder builder = factory.newDocumentBuilder();
 
                 //Create a new Document object
                 document = builder.newDocument();
 
                 //Create MortgageApp - the root element in the XML
                 Element root = (Element)document.createElement("LoanApp");
                 document.appendChild(root);
 
                 //Create an XML element for Name
                 Element nameElement = (Element)document.createElement("Name");
                 nameElement.appendChild(document.createTextNode(name));
                 root.appendChild(nameElement);
 
                 //Create an XML element for Phone
                 Element phoneElement = (Element)document.createElement("PhoneOrEmail");
                 phoneElement.appendChild(document.createTextNode(phone));
                 root.appendChild(phoneElement);
 
                 //Create an XML element for amount
                 Element loanElement = (Element)document.createElement("LoanAmount");
                 loanElement.appendChild(document.createTextNode(amount));
                 root.appendChild(loanElement);
 
                 //Create an XML element for ApprovalStatus
                 Element approveElement = (Element)document.createElement("ApprovalStatus");
                 approveElement.appendChild(document.createTextNode("PENDING APPROVAL"));
                 root.appendChild(approveElement);
 
               }
          catch (Exception e) {
                   System.out.println("The following exception occurred: "+e.getMessage());
                }
         return document;
          }
         }
```

### 為Web應用程式建立網頁 {#create-the-web-page-for-the-web-application}

的 *索引.html* 該網頁提供了一個指向調用Java Servlet的入口點 `FirstAppSolution/PreLoanProcess` 處理。 此網頁是一個基本HTML表單，包含HTML表單和提交按鈕。 當用戶按一下提交按鈕時，表單資料將發佈到 `SubmitXML` Java Servlet。

Java servlet使用以下Java代碼捕獲從HTML頁發佈的資料：

```java
 //Get the values that are passed from the Loan HTML page
 String name = request.getParameter("name");
 String phone = request.getParameter("phone");
 String amount = request.getParameter("amount");
```

以下HTML代碼表示在設定開發環境期間建立的index.html檔案。 (請參閱 [建立Web項目](invoking-human-centric-long-lived.md#create-a-web-project)。)

```xml
 <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "https://www.w3.org/TR/html4/loose.dtd">
 <html>
 <head>
 <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
 <title>Insert title here</title>
 </head>
 <body>
 <table>
     <TBODY>
         <TR>
             <td><img src="financeCorpLogo.jpg" width="172" height="62"></TD>
             <td><FONT size="+2"><strong>Java Loan Application Page</strong></FONT></TD>
             <td> </TD>
             <td> </TD>
         </TR>
 
     </TBODY>
 </TABLE>
     <FORM action="https://hiro-xp:8080/PreLoanProcess/SubmitXML" method="post">
        <table>
          <TBODY>
                <TR>
                      <td><LABEL for="name">Name: </LABEL></TD>
                  <td><INPUT type="text" name="name"></TD>
                  <td><input type="submit" value="Submit Application"></TD>
                  </TR>
            <TR>
                  <td> <LABEL for="phone">Phone/Email: </LABEL></TD>
              <td><INPUT type="text" name="phone"></TD>
                  <td></TD>
              </TR>
 
            <TR>
                  <td><LABEL for="amount">Amount: </LABEL></TD>
              <td><INPUT type="text" name="amount"></TD>
                 <td></TD>
             </TR>
          </TBODY>
 </TABLE>
       </FORM>
 </body>
 </html>
```

### 將Web應用程式打包到WAR檔案 {#package-the-web-application-to-a-war-file}

部署調用的Java Servlet `FirstAppSolution/PreLoanProcess` 進程，將Web應用程式打包到WAR檔案。 確保元件的業務邏輯所依賴的外部JAR檔案（如adobe-liveccycle-client.jar和adobe-usermanager-client.jar）也包含在WAR檔案中。

下圖顯示了Eclipse項目的內容，該內容已打包到WAR檔案中。

>[!NOTE]
>
>在上圖中，JPG檔案可以替換為任何JPG影像檔案。

**將Web應用程式打包到WAR檔案：**

1. 從 **項目瀏覽器** 窗口，按一下右鍵 `InvokePreLoanProcess` 項目和選擇 **導出** > **WAR檔案**。
1. 在 **Web模組** 文本框，類型 `InvokePreLoanProcess` 的子菜單。
1. 在 **目標** 文本框，類型 `PreLoanProcess.war`**為**&#x200B;檔案名，指定WAR檔案的位置，然後按一下「完成」。

### 將WAR檔案部署到托管AEM Forms的J2EE應用程式伺服器 {#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms}

將WAR檔案部署到部署了AEM Forms的J2EE應用程式伺服器。 要將WAR檔案部署到J2EE應用程式伺服器，請將WAR檔案從導出路徑複製到 `[AEM Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\lc_turnkey\deploy`。

>[!NOTE]
>
>如果AEM Forms未部署在JBoss上，則必須按照托管AEM Forms的J2EE應用程式伺服器部署WAR檔案。

### TestWeb應用程式 {#test-your-web-application}

部署Web應用程式後，可以使用Web瀏覽器test它。 假定您使用的是承載AEM Forms的同一台電腦，則可以指定以下URL:

* http://localhost:8080/PreLoanProcess/index.html

   在HTML表單欄位中輸入值，然後按一下「提交申請」按鈕。 如果出現問題，請參閱J2EE應用程式伺服器的日誌檔案。

>[!NOTE]
>
>要確認Java應用程式調用了該進程，請啟動Workspace並接受借出。

## 建立ASP.NET Web應用程式，該應用程式調用以人為中心的長壽命進程 {#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process}

您可以建立調用 `FirstAppSolution/PreLoanProcess` 處理。 要從ASP.NET應用程式調用此進程，請使用Web服務。 (請參閱 [使用Web服務調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)。)

下圖顯示了從最終用戶獲取資料的ASP.NET客戶端應用程式。 資料被放入XML資料源中併發送到 `FirstAppSolution/PreLoanProcess` 當用戶按一下「提交應用程式」按鈕時進行處理。

注意，在調用該進程後，將顯示調用標識符值。 建立調用標識符值作為跟蹤長壽命進程狀態的記錄的一部分。

ASP.NET應用程式執行以下任務：

* 檢索用戶在網頁中輸入的值。
* 動態建立傳遞到* FirstAppSolution/PreLoanProcess *進程的XML資料源。 這三個值在XML資料源中指定。
* 使用Web服務調用* FirstAppSolution/PreLoanProcess *進程。
* 將調用標識符值和長期操作的狀態返回到客戶端Web瀏覽器。

### 步驟摘要 {#summary_of_steps-1}

要建立能夠調用FirstAppSolution/PreLoanProcess進程的ASP.NET應用程式，請執行以下步驟：

1. [建立ASP.NET Web應用程式](invoking-human-centric-long-lived.md#create-an-asp-net-web-application)。
1. [建立調用FirstAppSolution/PreLoanProcess的ASP頁](invoking-human-centric-long-lived.md#create-an-asp-page-that-invokes-firstappsolution-preloanprocess)。
1. [運行ASP.NET應用程式](invoking-human-centric-long-lived.md#run-the-asp-net-application)。

### 建立ASP.NET Web應用程式 {#create-an-asp-net-web-application}

建立Microsoft.NET C# ASP.NET Web應用程式。 下圖顯示了名為ASP.NET的項目的內容 *InvokePreLoanProcess*。

注意，在「服務參考」(Service References)下，有兩個項目。 第一個項名為* JobManager*。 此引用使ASP.NET應用程式能夠調用作業管理器服務。 此服務返回有關長期進程狀態的資訊。 例如，如果進程當前正在運行，則此服務將返回一個指定進程當前正在運行的數值。 第二個引用的名稱為&#x200B;*貸前流程*。 此服務引用表示對* FirstAppSolution/PreLoanProcess *進程的引用。 建立服務引用後，與AEM Forms服務關聯的資料類型可在.NET項目中使用。

**建立ASP.NET項目：**

1. 啟動MicrosoftVisual Studio 2008。
1. 從 **檔案** 菜單，選擇 **新建**。 **網站**。
1. 在 **模板** 清單，選擇 **ASP.NET網站**。
1. 在 **位置** 框中，選擇項目的位置。 將項目命名為 *InvokePreLoanProcess*。
1. 在 **語言** 框中，選擇Visual C#
1. 按一下「確定」。

**添加服務引用：**

1. 在「項目」菜單中，選擇 **添加服務引用**。
1. 在 **地址** 對話框，指定作業管理器服務的WSDL。

   ```java
    https://hiro-xp:8080/soap/services/JobManager?WSDL&lc_version=9.0.1
   ```

1. 在「命名空間」欄位中，鍵入 `JobManager`。
1. 按一下 **開始**&#x200B;然後按一下&#x200B;**確定**。
1. 在 **項目** 菜單，選擇 **添加服務引用**。
1. 在 **地址** 對話框，指定FirstAppSolution/PreLoanProcess進程的WSDL。

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?WSDL&lc_version=9.0.1
   ```

1. 在「命名空間」欄位中，鍵入 `PreLoanProcess`。
1. 按一下 **開始**&#x200B;然後按一下&#x200B;**確定**。

>[!NOTE]
>
>替換 `hiro-xp` J2EE應用程式伺服器的IP地址托管AEM Forms。 的 `lc_version` 選項確保AEM Forms功能（如MTOM）可用。 不指定 `lc_version`選項，您不能使用MTOM調用AEM Forms。 (請參閱 [使用MTOM調用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)。)

### 建立調用FirstAppSolution/PreLoanProcess的ASP頁 {#create-an-asp-page-that-invokes-firstappsolution-preloanprocess}

在ASP.NET項目中，添加一個Web表單（ASPX檔案），該表單負責向貸款申請人顯示HTML頁。 Web表單基於派生自 `System.Web.UI.Page`。 調用的C#應用程式邏輯 `FirstAppSolution/PreLoanProcess` 位於 `Button1_Click` 方法（此按鈕表示「提交申請」按鈕）。

下圖顯示了ASP.NET應用程式

下表列出了屬於此ASP.NET應用程式的控制項。

<table>
 <thead>
  <tr>
   <th><p>控制項名稱</p></th>
   <th><p>說明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>文本框名稱</p></td>
   <td><p>指定客戶的姓和姓。 </p></td>
  </tr>
  <tr>
   <td><p>文本框電話</p></td>
   <td><p>指定客戶的電話或電子郵件地址。 </p></td>
  </tr>
  <tr>
   <td><p>文本框金額</p></td>
   <td><p>指定貸款金額。</p></td>
  </tr>
  <tr>
   <td><p>Button1</p></td>
   <td><p>表示「提交申請」按鈕。</p></td>
  </tr>
  <tr>
   <td><p>標籤作業ID</p></td>
   <td><p>一個標籤控制項，它指定調用標識符值的值。</p></td>
  </tr>
  <tr>
   <td><p>標籤狀態</p></td>
   <td><p>指定作業狀態值的標籤控制項。 通過調用作業管理器服務來檢索此值。 </p></td>
  </tr>
 </tbody>
</table>

作為ASP.NET應用程式一部分的應用程式邏輯必須動態建立XML資料源以傳遞到 `FirstAppSolution/PreLoanProcess` 處理。 申請人在HTML頁中輸入的值必須在XML資料源中指定。 在Workspace中查看表單時，這些資料值會合併到表單中。 位於 `System.Xml` 命名空間用於建立XML資料源。

當從ASP.NET應用程式調用需要XML資料的進程時，XML資料類型可供您使用。 就是，你不能通過 `System.Xml.XmlDocument` 實例。 要傳遞給進程的此XML實例的完全限定名稱為 `InvokePreLoanProcess.PreLoanProcess.XML`。 轉換 `System.Xml.XmlDocument` 實例 `InvokePreLoanProcess.PreLoanProcess.XML`。 可以使用以下代碼執行此任務。

```java
 //Create the XML to pass to the FirstAppSolution/PreLoanProcess process
 XmlDocument myXML = CreateXML(userName, phone, amount);
 
 //Convert the XML to a InvokePreLoanProcess.PreLoanProcess.XML instance
 StringWriter sw = new StringWriter();
 XmlTextWriter xw = new XmlTextWriter(sw);
 myXML.WriteTo(xw);
 
 InvokePreLoanProcess.PreLoanProcess.XML inXML = new XML();
 inXML.document = sw.ToString();
```

建立調用 `FirstAppSolution/PreLoanProcess` 處理，在 `Button1_Click` 方法：

1. 建立 `FirstAppSolution_PreLoanProcessClient` 對象。
1. 建立 `FirstAppSolution_PreLoanProcessClient.Endpoint.Address` 對象 `System.ServiceModel.EndpointAddress` 建構子。 將指定WSDL的字串值傳遞給AEM Forms服務和編碼類型：

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?blob=mtom
   ```

   你不需要 `lc_version` 屬性。 建立服務引用時使用此屬性。 但是，請確保指定 `?blob=mtom`。

   >[!NOTE]
   >
   >替換 `hiro-xp`*具有托管AEM Forms的J2EE應用伺服器的IP地址。*

1. 建立 `System.ServiceModel.BasicHttpBinding` 通過獲取 `FirstAppSolution_PreLoanProcessClient.Endpoint.Binding` 資料成員。 將返回值強制轉換為 `BasicHttpBinding`。
1. 設定 `System.ServiceModel.BasicHttpBinding` 對象 `MessageEncoding` 資料成員 `WSMessageEncoding.Mtom`。 此值確保使用MTOM。
1. 通過執行以下任務啟用基本HTTP身份驗證：

   * 為數AEM據成員分配表單用戶名 `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.UserName`。
   * 為資料成員分配相應的口令值 `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.Password`。
   * 分配常數值 `HttpClientCredentialType.Basic` 到資料成員 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 分配常數值 `BasicHttpSecurityMode.TransportCredentialOnly` 到資料成員 `BasicHttpBindingSecurity.Security.Mode`。

   以下代碼示例顯示了這些任務。

   ```as3
    //Enable BASIC HTTP authentication
    BasicHttpBinding b = (BasicHttpBinding)mortgageClient.Endpoint.Binding;
    b.MessageEncoding = WSMessageEncoding.Mtom;
    mortgageClient.ClientCredentials.UserName.UserName = "administrator";
    mortgageClient.ClientCredentials.UserName.Password = "password";
    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
    b.MaxReceivedMessageSize = 2000000;
    b.MaxBufferSize = 2000000;
    b.ReaderQuotas.MaxArrayLength = 2000000;
   ```

1. 檢索用戶在網頁中輸入的名稱、電話和金額值。 使用這些值動態建立發送到 `FirstAppSolution/PreLoanProcess` 處理。 建立 `System.Xml.XmlDocument` 表示要傳遞到進程的XML資料源（以下代碼示例中顯示了此應用程式邏輯）。
1. 轉換 `System.Xml.XmlDocument` 實例 `InvokePreLoanProcess.PreLoanProcess.XML` （以下代碼示例中顯示了此應用程式邏輯）。
1. 調用 `FirstAppSolution/PreLoanProcess` 通過調用 `FirstAppSolution_PreLoanProcessClient` 對象 `invoke_Async` 的雙曲餘切值。 此方法返回一個字串值，它表示長壽命進程的調用標識符值。
1. 建立 `JobManagerClient` 使用is建構子。 （確保已設定對作業管理器服務的服務引用。）
1. 重複步驟1-5。 為步驟2指定以下URL: `https://hiro-xp:8080/soap/services/JobManager?blob=mtom`。
1. 建立 `JobId` 對象。
1. 設定 `JobId` 對象 `id` 返回值為 `FirstAppSolution_PreLoanProcessClient` 對象 `invoke_Async` 的雙曲餘切值。
1. 分配 `value` 對 `JobId` 對象 `persistent` 資料成員。
1. 建立 `JobStatus` 通過調用 `JobManagerService` 對象s `getStatus` 方法和傳遞 `JobId` 的雙曲餘切值。
1. 通過檢索 `JobStatus` 對象 `statusCode` 資料成員。
1. 將調用標識符值分配給 `LabelJobID.Text` 的子菜單。
1. 將狀態值分配給 `LabelStatus.Text` 的子菜單。

### 快速啟動：使用Web服務API調用長期進程 {#quick-start-invoking-a-long-lived-process-using-the-web-service-api}

以下C#代碼示例調用 `FirstAppSolution/PreLoanProcess`處理。

```csharp
 ???/**
     * Ensure that you create a .NET project that uses
     * MS Visual Studio 2008 and version 3.5 of the .NET
     * framework. This is required to invoke a
     * AEM Forms service using MTOM.
 
 
 using System;
 using System.Collections;
 using System.Configuration;
 using System.Data;
 using System.Linq;
 using System.Web;
 using System.ServiceModel;
 using System.Web.Security;
 using System.Web.UI;
 using System.Web.UI.HtmlControls;
 using System.Web.UI.WebControls;
 using System.Web.UI.WebControls.WebParts;
 using System.Xml.Linq;
 using System.Xml;
 using System.IO;
 
 //A reference to FirstAppSolution/PreLoanProcess
 using InvokePreLoanProcess.PreLoanProcess;
 
 //A reference to JobManager service
 using InvokePreLoanProcess.JobManager;
 
 
 namespace InvokePreLoanProcess
 {
        public partial class _Default : System.Web.UI.Page
        {
            //This method is called when the Submit Application button is
            //Clicked
            protected void Button1_Click(object sender, EventArgs e)
            {
                //Create a FirstAppSolution_PreLoanProcessClient object
                FirstAppSolution_PreLoanProcessClient mortgageClient = new FirstAppSolution_PreLoanProcessClient();
                mortgageClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?blob=mtom");
 
                //Enable BASIC HTTP authentication
                BasicHttpBinding b = (BasicHttpBinding)mortgageClient.Endpoint.Binding;
                b.MessageEncoding = WSMessageEncoding.Mtom;
                mortgageClient.ClientCredentials.UserName.UserName = "administrator";
                mortgageClient.ClientCredentials.UserName.Password = "password";
                b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                b.MaxReceivedMessageSize = 2000000;
                b.MaxBufferSize = 2000000;
                b.ReaderQuotas.MaxArrayLength = 2000000;
 
                //Retrieve values that user entered into the web page
                String userName = TextBoxName.Text;
                String phone = TextBoxPhone.Text;
                String amount = TextBoxAmount.Text;
 
                //Create the XML to pass to the FirstAppSolution/PreLoanProcess process
                XmlDocument myXML = CreateXML(userName, phone, amount);
 
                StringWriter sw = new StringWriter();
                XmlTextWriter xw = new XmlTextWriter(sw);
                myXML.WriteTo(xw);
 
                InvokePreLoanProcess.PreLoanProcess.XML inXML = new XML();
                inXML.document = sw.ToString();
 
                //INvoke the FirstAppSolution/PreLoanProcess process
                String invocationID =  mortgageClient.invoke_Async(inXML);
 
                //Create a JobManagerClient object to obtain the status of the long-lived operation
                JobManagerClient jobManager = new JobManagerClient();
                jobManager.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/JobManager?blob=mtom");
 
                //Enable BASIC HTTP authentication
                BasicHttpBinding b1 = (BasicHttpBinding)jobManager.Endpoint.Binding;
                b1.MessageEncoding = WSMessageEncoding.Mtom;
                jobManager.ClientCredentials.UserName.UserName = "administrator";
                jobManager.ClientCredentials.UserName.Password = "password";
                b1.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                b1.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                b1.MaxReceivedMessageSize = 2000000;
                b1.MaxBufferSize = 2000000;
                b1.ReaderQuotas.MaxArrayLength = 2000000;
 
 
                //Create a JobID object that represents the status of the
                //long-lived operation
                JobId jobId = new JobId();
                jobId.id = invocationID;
                jobId.persistent = true;
                JobStatus jobStatus = jobManager.getStatus(jobId);
                System.Int16 val2 = jobStatus.statusCode;
                LabelJobID.Text = "The job status identifier value is " + invocationID;
                LabelStatus.Text = "The status of the long-lived operation is " + getJobDescription(val2);
 
            }
 
            private static XmlDocument CreateXML(String name, String phone, String amount)
            {
                //This method dynamically creates a DDX document
                //to pass to the FirstAppSolution/PreLoanProcess process
                XmlDocument xmlDoc = new XmlDocument();
 
                //Create the root element and append it to the XML DOM
                System.Xml.XmlElement root = xmlDoc.CreateElement("LoanApp");
                xmlDoc.AppendChild(root);
 
                //Create the Name element
                XmlElement nameElement = xmlDoc.CreateElement("Name");
                nameElement.AppendChild(xmlDoc.CreateTextNode(name));
                root.AppendChild(nameElement);
 
                //Create the LoanAmount element
                XmlElement LoanAmount = xmlDoc.CreateElement("LoanAmount");
                LoanAmount.AppendChild(xmlDoc.CreateTextNode(amount));
                root.AppendChild(LoanAmount);
 
                //Create the PhoneOrEmail element
                XmlElement PhoneOrEmail = xmlDoc.CreateElement("PhoneOrEmail");
                PhoneOrEmail.AppendChild(xmlDoc.CreateTextNode(phone));
                root.AppendChild(PhoneOrEmail);
 
                //Create the ApprovalStatus element
                XmlElement ApprovalStatus = xmlDoc.CreateElement("ApprovalStatus");
                ApprovalStatus.AppendChild(xmlDoc.CreateTextNode("PENDING APPROVAL"));
                root.AppendChild(ApprovalStatus);
 
                //Return the XmlElement instance
                return xmlDoc;
            }
 
 
            //Returns the String value of the Job Manager status code
            private String getJobDescription(int val)
            {
                switch(val)
                {
                    case 0:
                        return "JOB_STATUS_UNKNOWN";
 
                    case 1:
                        return "JOB_STATUS_QUEUED";
 
                    case 2:
                        return "JOB_STATUS_RUNNING";
 
                    case 3:
                        return "JOB_STATUS_COMPLETED";
 
                    case 4:
                        return "JOB_STATUS_FAILED";
 
                     case 5:
                        return "JOB_STATUS_COMPLETED";
 
                    case 6:
                        return "JOB_STATUS_SUSPENDED";
 
                    case 7:
                        return "JOB_STATUS_COMPLETE_REQUESTED";
 
                    case 8:
                        return "JOB_STATUS_TERMINATE_REQUESTED";
 
                     case 9:
                        return "JOB_STATUS_SUSPEND_REQUESTED";
 
                       case 10:
                        return "JOB_STATUS_RESUME_REQUESTED";
                }
 
                return "";
            }
       }
 }
 
```

>[!NOTE]
>
>getJobDescription用戶定義的方法中的值與作業管理器服務返回的值相對應。

### 運行ASP.NET應用程式 {#run-the-asp-net-application}

編譯和部署ASP.NET應用程式後，可以使用Web瀏覽器執行它。 假定ASP.NET項目的名稱為 *InvokePreLoanProcess*，在Web瀏覽器中指定以下URL:

*http://localhost:1629/InvokePreLoanProcess/*Default.aspx

其中localhost是承載ASP.NET項目的Web伺服器的名稱，1629是埠號。 編譯和構建ASP.NET應用程式時，MicrosoftVisual Studio會自動進行部署。

>[!NOTE]
>
>要確認ASP.NET應用程式調用了該流程，請啟動Workspace並接受貸款。

## 建立使用Flex構建的客戶端應用程式，該應用程式調用以人為中心的長壽命流程 {#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process}

您可以建立與Flex一起構建的客戶端應用程式以調用 *FirstAppSolution/PreLoanProcess* 處理。 此應用程式使用遠程處理來調用 *FirstAppSolution/PreLoanProcess* 處理。 (請參閱 [調用AEM Forms使用(不建議AEM用於表單)AEM Forms遠程處理](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)。)

下圖顯示了使用Flex從最終用戶收集資料構建的客戶端應用程式。 資料被放入XML資料源中，併發送到進程。

注意，在調用該進程後，將顯示調用標識符值。 建立調用標識符值作為跟蹤長壽命進程狀態的記錄的一部分。

使用Flex構建的客戶端應用程式執行以下任務：

* 檢索用戶在網頁中輸入的值。
* 動態建立傳遞到 *FirstAppSolution/PreLoanProcess* 處理。 這三個值在XML資料源中指定。
* 調用 *FirstAppSolution/PreLoanProcess* 處理。
* 返回長壽命進程的調用標識符值。

### 步驟摘要 {#summary_of_steps-2}

要建立使用Flex構建的能夠調用FirstAppSolution/PreLoanProcess流程的客戶端應用程式，請執行以下步驟：

1. 啟動新的Flex項目。
1. 在項目的類路徑中包括adobe-remotening-provider.swc檔案。 (請參閱 [包括AEM FormsFlex圖書館的檔案](/help/forms/developing/invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)。)
1. 建立 `mx:RemoteObject` 實例通過ActionScript或MXML。 (請參閱 [建立mx:RemoteObject實例](/help/forms/developing/invoking-aem-forms-using-remoting.md))
1. 設定 `ChannelSet` 實例與AEM Forms通信，並將其與 `mx:RemoteObject` 實例。 (請參閱 [建立通往AEM Forms的渠道](/help/forms/developing/invoking-aem-forms-using-remoting.md)。)
1. 調用ChannelSet `login` 方法或服務 `setCredentials` 方法，指定用戶標識符值和口令。 (請參閱 [使用單一登錄](/help/forms/developing/invoking-aem-forms-using-remoting.md#using-single-sign-on)。)
1. 建立要傳遞到的XML資料源 `FirstAppSolution/PreLoanProcess` 建立XML實例。 （以下代碼示例中顯示了此應用程式邏輯。）
1. 使用對象的建構子建立對象類型。 通過指定進程的輸入參數名稱為對象分配XML，如以下代碼所示：

   ```csharp
    //Get the XML data to pass to the AEM Forms process
    var xml:XML = createXML();
    var params:Object = new Object();
    params["formData"]=xml;
   ```

1. 調用 `FirstAppSolution/PreLoanProcess` 通過調用 `mx:RemoteObject` 實例 `invoke_Async` 的雙曲餘切值。 通過 `Object` 包含輸入參數。 (請參閱 [傳遞輸入值](/help/forms/developing/invoking-aem-forms-using-remoting.md)。)
1. 檢索從長期進程返回的調用標識值，如以下代碼所示：

   ```csharp
    // Handles async call that invokes the long-lived process
    private function resultHandler(event:ResultEvent):void
    {
    ji = event.result as JobId;
    jobStatusDisplay.text = "Job Status ID: " + ji.jobId as String;
    }
   ```

### 使用遠程處理調用長期進程 {#invoking-a-long-lived-process-using-remoting}

以下Flex代碼示例調用 `FirstAppSolution/PreLoanProcess` 處理。

```java
 <?xml version="1.0" encoding="utf-8"?>
 
 <mx:Application  xmlns="*" backgroundColor="#FFFFFF"
      creationComplete="initializeChannelSet();">
 
 <mx:Script>
          <![CDATA[
 
             import mx.controls.Alert;
             import mx.rpc.events.FaultEvent;
             import mx.rpc.events.ResultEvent;
             import flash.net.navigateToURL;
             import mx.messaging.ChannelSet;
             import mx.messaging.channels.AMFChannel;
             import mx.collections.ArrayCollection;
             import mx.rpc.livecycle.JobId;
             import mx.rpc.livecycle.JobStatus;
             import mx.rpc.livecycle.DocumentReference;
             import mx.formatters.NumberFormatter;
 
             // Holds the job ID returned by LC.JobManager
             private var ji:JobId;
 
             private function initializeChannelSet():void
              {
              var cs:ChannelSet= new ChannelSet();
         cs.addChannel(new AMFChannel("remoting-amf", "https://hiro-xp:8080/remoting/messagebroker/amf"));
         LC_MortgageApp.setCredentials("tblue", "password");
         LC_MortgageApp.channelSet = cs;
              }
 
            private function submitApplication():void
             {
             //Get the XML data to pass to the AEM Forms process
             var xml:XML = createXML();
             var params:Object = new Object();
             params["formData"]=xml;
             LC_MortgageApp.invoke_Async(params);
             }
 
             // Handles async call that invokes the long-lived process
             private function resultHandler(event:ResultEvent):void
             {
                ji = event.result as JobId;
                jobStatusDisplay.text = "Job Status ID: " + ji.jobId as String;
             }
 
             private function createXML():XML
             {
                //Calculate the Mortgage value to place in the XML data
                var propertyPrice:String = txtAmount.text ;
                var name:String = txtName.text ;
                var phone:String = txtPhone.text ;;
 
                var model:XML =
 
                  <LoanApp>
                           <Name>{name}</Name>
                           <LoanAmount>{propertyPrice}</LoanAmount>
                           <PhoneOrEmail>{phone}</PhoneOrEmail>
                           <ApprovalStatus>PENDING APPROVAL</ApprovalStatus>
                  </LoanApp>
 
              return model;
             }
 
 
          ]]>
       </mx:Script>
 
       <!-- Declare the RemoteObject and set its destination to the mortgage-app remoting endpoint defined in AEM Forms. -->
       <mx:RemoteObject id="LC_MortgageApp" destination="FirstAppSolution/PreLoanProcess" result="resultHandler(event);">
          <mx:method name="invoke_Async" result="resultHandler(event)"/>
      </mx:RemoteObject>
 
 
     <mx:Grid x="229" y="186">
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Image>
                     <mx:source>file:///D|/LiveCycle_9/FirstApp/financeCorpLogo.jpg</mx:source>
                 </mx:Image>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Flex Loan Application Page" fontSize="20"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Name:" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:TextInput id="txtName"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:Button label="Submit Application" click="submitApplication()"/>
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Phone/Email:" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:TextInput id="txtPhone"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Amount:" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:TextInput id="txtAmount"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Label" id="jobStatusDisplay" enabled="true" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
     </mx:Grid>
 
 </mx:Application>
 
```
