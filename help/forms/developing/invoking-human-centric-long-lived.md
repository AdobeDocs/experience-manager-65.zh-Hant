---
title: 調用以人為中心的長壽命過程
seo-title: 調用以人為中心的長壽命過程
description: 以程式設計方式叫用在Workbench中建立的以人為中心的長期處理程式，此程式使用使用叫用API的Java Web型用戶端應用程式、使用Web服務的ASP.NET應用程式，以及使用Remoting的Flex所建置的用戶端應用程式。
seo-description: 以程式設計方式叫用在Workbench中建立的以人為中心的長期處理程式，此程式使用使用叫用API的Java Web型用戶端應用程式、使用Web服務的ASP.NET應用程式，以及使用Remoting的Flex所建置的用戶端應用程式。
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
source-wordcount: '3739'
ht-degree: 0%

---

# 調用以人為中心的長壽命過程{#invoking-human-centric-long-lived-processes}

您可以使用以下客戶端應用程式，以程式設計方式叫用在Workbench中建立的以人為中心的長期流程：

* 使用調用API的Java基於Web的客戶端應用程式。 (請參閱[使用Java API叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md)(/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)。)
* 使用Web服務的ASP.NET應用程式。 (請參閱[使用網站服務叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)。)
* 使用Flex建置的用戶端應用程式，使用Remoting。 (請參閱[使用叫用AEM Forms(AEM表單已淘汰)AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)。)

叫用的長期進程名為&#x200B;*FirstAppSolution/PreLoanProcess*。 您可以依照[建立您的第一個AEM Forms應用程式](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63)中指定的教學課程，建立此程式。

以人為中心的程式涉及使用者可使用工作區來回應的任務。 例如，使用Workbench，您可以建立流程，讓銀行經理核准或拒絕貸款申請。 下圖顯示進程&#x200B;*FirstAppSolution/PreLoanProcess*。

*FirstAppSolution/PreLoanProcess*&#x200B;進程接受名為&#x200B;*formData*&#x200B;的輸入參數，其資料類型為XML。 XML資料與名為&#x200B;*PreLoanForm.xdp*&#x200B;的表單設計合併。 下圖顯示的表單代表指派給使用者的任務，以核准或拒絕貸款申請。 使用者使用工作區來核准或拒絕應用程式。 工作區使用者可按一下下圖所示的「核准」按鈕，以核准貸款請求。 同樣地，使用者可以按一下拒絕按鈕來拒絕貸款請求。

非同步調用長期進程，且由於以下因素無法同步調用：

* 過程可能會跨越很長時間。
* 程式可跨越組織界限。
* 進程需要外部輸入才能完成。 例如，假設表單已傳送給不在辦公室的經理。 在這種情況下，在管理員返回並填寫表單之前，該過程不會完成。

當叫用長期處理程式時，AEM Forms會在建立記錄時建立叫用識別碼值。 記錄會追蹤長期處理程式的狀態，並儲存在AEM Forms資料庫中。 使用調用標識符值，可以跟蹤長期進程的狀態。 此外，您還可以使用進程調用標識符值來執行進程管理器操作，如終止正在運行的進程實例。

>[!NOTE]
>
>AEM Forms不會在叫用短期程式時建立叫用識別碼值或記錄。

當申請人提交申請時，將調用`FirstAppSolution/PreLoanProcess`過程，該申請以XML資料表示。 輸入進程變數的名稱為`formData`，其資料類型為XML。 在本討論中，假定以下XML資料用作`FirstAppSolution/PreLoanProcess`進程的輸入。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <LoanApp>
 <Name>Sam White</Name>
 <LoanAmount>250000</LoanAmount>
 <PhoneOrEmail>(555)555-5555</PhoneOrEmail>
 <ApprovalStatus>PENDING APPROVAL</ApprovalStatus>
 </LoanApp>
```

傳遞至流程的XML資料必須與流程中使用的表單中的欄位匹配。 否則，資料不會顯示在表單中。 調用`FirstAppSolution/PreLoanProcess`進程的所有應用程式都必須傳遞此XML資料源。 在&#x200B;*調用以人為中心的長期進程*&#x200B;中建立的應用程式從用戶輸入到Web客戶端的值動態建立XML資料源。

使用客戶端應用程式，可以發送&#x200B;*FirstAppSolution/PreLoanProcess*&#x200B;處理所需的XML資料。 長期進程返回調用標識符值作為其返回值。 下圖顯示調用*FirstAppSolution/PreLoanProcess的客戶端應用程式的長期進程。 客戶端應用程式發送XML資料，並返回表示調用標識符值的字串值。

**另請參閱**

[建立調用以人為中心的長生命週期過程的Java Web應用程式](invoking-human-centric-long-lived.md#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process)

[建立ASP.NET Web應用程式，該應用程式調用以人為中心的長生命週期過程](invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

[建立使用Flex構建的客戶端應用程式，該應用程式調用以人為中心的長期流程](invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

## 建立調用以人為中心的長期進程{#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process}的Java Web應用程式

您可以建立基於Web的應用程式，該應用程式使用Java servlet調用`FirstAppSolution/PreLoanProcess`進程。 要從Java servlet調用此進程，請使用Java servlet內的調用API。 (請參閱[使用Java API叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)。)

下圖顯示發佈名稱、電話（或電子郵件）和金額值的網頁型用戶端應用程式。 當使用者按一下「提交應用程式」按鈕時，這些值會傳送至Java servlet。

Java servlet執行下列任務：

* 擷取從HTML頁面張貼至Java servlet的值。
* 動態建立XML資料源以傳遞至&#x200B;*FirstAppSolution/PreLoanProcess*&#x200B;進程。 名稱、電話（或電子郵件）和金額值在XML資料源中指定。
* 使用AEM Forms叫用API叫用&#x200B;*FirstAppSolution/PreLoanProcess*&#x200B;程式。
* 將調用標識符值返回給客戶端Web瀏覽器。

### 步驟{#summary-of-steps}的摘要

要建立調用`FirstAppSolution/PreLoanProcess`進程的基於Java Web的應用程式，請執行以下步驟：

1. [建立Web專案](invoking-human-centric-long-lived.md#create-a-web-project)。
1. [為servlet建立Java應用程式邏輯](invoking-human-centric-long-lived.md#create-java-application-logic-for-the-servlet)。
1. [為Web應用程式建立網頁](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)
1. [將Web應用程式封裝為WAR檔案](invoking-human-centric-long-lived.md#package-the-web-application-to-a-war-file)。
1. [將WAR檔案部署至托管AEM Forms的J2EE應用程式伺服器](invoking-human-centric-long-lived.md#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms)。
1. [測試您的Web應用程式](invoking-human-centric-long-lived.md#test-your-web-application)。

>[!NOTE]
>
>其中有些步驟取決於部署了AEM Forms的J2EE應用程式。 例如，您用來部署WAR檔案的方法取決於您使用的J2EE應用程式伺服器。 假設已在JBoss®上部署AEM Forms。

### 建立Web項目{#create-a-web-project}

建立Web應用程式的第一步是建立Web項目。 本文檔所基於的Java IDE是Eclipse 3.3。使用Eclipse IDE，建立Web項目，並將所需的JAR檔案添加到項目中。 將名為&#x200B;*index.html*&#x200B;的HTML頁面和Java servlet新增至您的專案。

以下清單指定要包含在Web項目中的JAR檔案：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* J2EE.jar

有關這些JAR檔案的位置，請參閱[包括AEM Forms Java庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

>[!NOTE]
>
>J2EE.jar檔案定義Java servlet使用的資料類型。 您可以從部署了AEM Forms的J2EE應用程式伺服器中獲取此JAR檔案。

**建立Web專案**

1. 啟動Eclipse，然後按一下&#x200B;**File** > **New Project**。
1. 在&#x200B;**新建項目**&#x200B;對話框中，選擇&#x200B;**Web** > **動態Web項目**。
1. 鍵入`InvokePreLoanProcess`作為項目名稱，然後按一下&#x200B;**完成**。

**將所需的JAR檔案添加到項目中**

1. 在「項目資源管理器」窗口中，按一下右鍵`InvokePreLoanProcess`項目並選擇&#x200B;**屬性**。
1. 按一下&#x200B;**Java組建路徑**，然後按一下&#x200B;**Libraries**&#x200B;標籤。
1. 按一下&#x200B;**添加外部JAR**&#x200B;按鈕，然後瀏覽到要包含的JAR檔案。

**新增Java servlet至您的專案**

1. 在「項目資源管理器」窗口中，按一下右鍵`InvokePreLoanProcess`項目，然後選擇&#x200B;**New** > **Other**。
1. 展開&#x200B;**Web**&#x200B;資料夾，選擇&#x200B;**Servlet**，然後按一下&#x200B;**Next**。
1. 在「建立Servlet」對話框中，鍵入`SubmitXML`作為servlet的名稱，然後按一下&#x200B;**完成**。

**新增HTML頁面至您的專案**

1. 在「項目資源管理器」窗口中，按一下右鍵`InvokePreLoanProcess`項目，然後選擇&#x200B;**New** > **Other**。
1. 展開&#x200B;**Web**&#x200B;資料夾，選擇&#x200B;**HTML**，然後按一下&#x200B;**Next**。
1. 在「新建HTML」對話框中，鍵入檔案名`index.html`，然後按一下&#x200B;**完成**。

>[!NOTE]
>
>有關建立調用SubmitXML Java servlet的HTML內容的資訊，請參閱[為Web應用程式建立網頁](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)。

### 為servlet {#create-java-application-logic-for-the-servlet}建立Java應用程式邏輯

從Java servlet內建立調用`FirstAppSolution/PreLoanProcess`進程的Java應用程式邏輯。 以下代碼顯示`SubmitXML` Java Servlet的語法：

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

通常，您不會將用戶端代碼放在Java servlet的`doGet`或`doPost`方法中。 更好的程式設計實務是將此程式碼放在個別類別中。 然後從`doPost`方法（或`doGet`方法）內實例化類，並調用相應的方法。 但是，為了簡單起見，程式碼範例會保持在最小值，並放置在`doPost`方法中。

要使用調用API調用`FirstAppSolution/PreLoanProcess`進程，請執行以下任務：

1. 在您Java專案的類別路徑中加入用戶端JAR檔案，例如adobe-livecycle-client.jar。 有關這些檔案的位置資訊，請參閱[包含AEM Forms Java庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。
1. 從HTML頁面擷取提交的名稱、電話和金額值。 使用這些值動態建立發送到`FirstAppSolution/PreLoanProcess`進程的XML資料源。 可以使用`org.w3c.dom`類建立XML資料源（以下代碼示例中顯示了此應用程式邏輯）。
1. 建立包含連接屬性的`ServiceClientFactory`對象。 （請參閱[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）
1. 使用其建構子並傳遞`ServiceClientFactory`物件，以建立`ServiceClient`物件。 `ServiceClient`物件可讓您叫用服務操作。 它處理諸如查找、調度和路由調用請求等任務。
1. 使用其建構子建立`java.util.HashMap`物件。
1. 為每個輸入參數調用`java.util.HashMap`對象的`put`方法，以傳遞至長期進程。 確保指定進程輸入參數的名稱。 因為`FirstAppSolution/PreLoanProcess`進程需要一個類型`XML`（名為`formData`）的輸入參數，您只需調用`put`方法一次。

   ```java
    //Get the XML to pass to the FirstAppSolution/PreLoanProcess process
    org.w3c.dom.Document inXML = GetDataSource(name,phone,amount);
    
    //Create a Map object to store the parameter value
    Map params = new HashMap();
    params.put("formData", inXML);
   ```

1. 調用`ServiceClientFactory`對象的`createInvocationRequest`方法並傳遞以下值，建立`InvocationRequest`對象：

   * 一個字串值，它指定要調用的長期進程的名稱。 要調用`FirstAppSolution/PreLoanProcess`進程，請指定`FirstAppSolution/PreLoanProcess`。
   * 表示流程操作名稱的字串值。 長期進程操作的名稱為`invoke`。
   * `java.util.HashMap`物件，包含服務操作所需的參數值。
   * 指定`false`的布爾值，它建立非同步請求（此值適用於調用長期進程）。

   >[!NOTE]
   >
   >*可將值true傳遞為createInvocationRequest方法的第四個參數，以叫用短期進程。傳遞值true會建立同步請求。*

1. 叫用`ServiceClient`物件的`invoke`方法並傳遞`InvocationRequest`物件，將叫用請求傳送至AEM Forms。 `invoke`方法返回`InvocationReponse`對象。
1. 長期進程返回一個字串值，該字串值表示調用標識值。 調用`InvocationReponse`對象的`getInvocationId`方法來檢索此值。

   ```java
    //Send the invocation request to the long-lived process and
    //get back an invocation response object
    InvocationResponse lcResponse = myServiceClient.invoke(lcRequest);
    String invocationId = lcResponse.getInvocationId();
   ```

1. 將調用標識值寫入客戶端Web瀏覽器。 您可以使用`java.io.PrintWriter`實例將此值寫入客戶端Web瀏覽器。

### 快速入門：使用調用API {#quick-start-invoking-a-long-lived-process-using-the-invocation-api}調用長期進程

以下Java代碼示例表示調用`FirstAppSolution/PreLoanProcess`進程的Java servlet。

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

### 為Web應用程式{#create-the-web-page-for-the-web-application}建立網頁

*index.html*&#x200B;網頁提供了調用`FirstAppSolution/PreLoanProcess`進程的Java servlet的入口點。 此網頁是基本HTML表單，包含HTML表單和提交按鈕。 當用戶按一下提交按鈕時，表單資料將發佈到`SubmitXML` Java servlet。

Java servlet會使用下列Java代碼從HTML頁面擷取發佈的資料：

```java
 //Get the values that are passed from the Loan HTML page
 String name = request.getParameter("name");
 String phone = request.getParameter("phone");
 String amount = request.getParameter("amount");
```

下列HTML程式碼代表在設定開發環境期間建立的index.html檔案。 （請參閱[建立Web項目](invoking-human-centric-long-lived.md#create-a-web-project)。）

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

### 將Web應用程式打包到WAR檔案{#package-the-web-application-to-a-war-file}

要部署調用`FirstAppSolution/PreLoanProcess`進程的Java servlet，請將Web應用程式打包到WAR檔案。 確保元件的業務邏輯所依賴的外部JAR檔案（例如adobe-livecycle-client.jar和adobe-usermanager-client.jar）也包含在WAR檔案中。

下圖顯示Eclipse專案的內容，其封裝為WAR檔案。

>[!NOTE]
>
>在上圖中，JPG檔案可替換為任何JPG影像檔案。

**將Web應用程式打包為WAR檔案：**

1. 在&#x200B;**Project Explorer**&#x200B;窗口中，按一下右鍵`InvokePreLoanProcess`項目並選擇&#x200B;**Export** > **WAR檔案**。
1. 在&#x200B;**Web模組**&#x200B;文本框中，鍵入`InvokePreLoanProcess`作為Java項目的名稱。
1. 在&#x200B;**Destination**&#x200B;文本框中，為&#x200B;**檔案名鍵入`PreLoanProcess.war`**，指定WAR檔案的位置，然後按一下「完成」。

### 將WAR檔案部署到托管AEM Forms {#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms}的J2EE應用程式伺服器

將WAR檔案部署到部署了AEM Forms的J2EE應用程式伺服器。 要將WAR檔案部署到J2EE應用程式伺服器，請將WAR檔案從導出路徑複製到`[AEM Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\lc_turnkey\deploy`。

>[!NOTE]
>
>如果AEM Forms未部署在JBoss上，則您必須部署WAR檔案，以符合托管AEM Forms的J2EE應用程式伺服器。

### 測試Web應用程式{#test-your-web-application}

部署Web應用程式後，可以使用Web瀏覽器進行測試。 假設您使用的電腦與托管AEM Forms的電腦相同，您可以指定下列URL:

* http://localhost:8080/PreLoanProcess/index.html

   在HTML表單欄位中輸入值，然後按一下「提交應用程式」按鈕。 如果出現問題，請參閱J2EE應用程式伺服器的日誌檔案。

>[!NOTE]
>
>若要確認Java應用程式已叫用此程式，請啟動Workspace並接受貸款。

## 建立ASP.NET Web應用程式，該應用程式調用以人為中心的長期進程{#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process}

您可以建立調用`FirstAppSolution/PreLoanProcess`進程的ASP.NET應用程式。 要從ASP.NET應用程式調用此過程，請使用Web服務。 (請參閱[使用網站服務叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)。)

下圖顯示一個從最終用戶獲取資料的ASP.NET客戶端應用程式。 當用戶按一下「提交應用程式」按鈕時，資料將放入XML資料源中併發送到`FirstAppSolution/PreLoanProcess`進程。

調用該進程後，將顯示調用標識符值。 建立調用標識符值作為跟蹤長期進程狀態的記錄的一部分。

ASP.NET應用程式執行以下任務：

* 檢索用戶在網頁中輸入的值。
* 動態建立傳遞至* FirstAppSolution/PreLoanProcess *process的XML資料源。 這三個值在XML資料源中指定。
* 調用* FirstAppSolution/PreLoanProcess *進程，方法是使用Web服務。
* 將調用標識符值和長期操作的狀態返回給客戶端Web瀏覽器。

### 步驟{#summary_of_steps-1}的摘要

要建立能夠調用FirstAppSolution/PreLoanProcess進程的ASP.NET應用程式，請執行以下步驟：

1. [建立ASP.NET Web應用程式](invoking-human-centric-long-lived.md#create-an-asp-net-web-application)。
1. [建立調用FirstAppSolution/PreLoanProcess的ASP頁](invoking-human-centric-long-lived.md#create-an-asp-page-that-invokes-firstappsolution-preloanprocess)。
1. [運行ASP.NET應用程式](invoking-human-centric-long-lived.md#run-the-asp-net-application)。

### 建立ASP.NET Web應用程式{#create-an-asp-net-web-application}

建立Microsoft .NET C# ASP.NET Web應用程式。 下圖顯示名為&#x200B;*InvokePreLoanProcess*&#x200B;的ASP.NET項目的內容。

注意「服務參考」下有兩個項目。 第一項名為* JobManager*。 此引用使ASP.NET應用程式能夠調用作業管理器服務。 此服務會傳回有關長期進程狀態的資訊。 例如，如果進程當前正在運行，則此服務將返回一個數值，該數值指定當前正在運行的進程。 第二個引用名為&#x200B;*PreLoanProcess*。 此服務參考代表對* FirstAppSolution/PreLoanProcess *process的參考。 建立服務參考後，與AEM Forms服務相關聯的資料類型便可在您的.NET專案中使用。

**建立ASP.NET項目：**

1. 啟動Microsoft Visual Studio 2008。
1. 從&#x200B;**File**&#x200B;菜單中，選擇&#x200B;**New**、**Web站點**。
1. 在&#x200B;**模板**&#x200B;清單中，選擇&#x200B;**ASP.NET網站**。
1. 在&#x200B;**Location**&#x200B;方塊中，選取專案的位置。 為項目命名&#x200B;*InvokePreLoanProcess*。
1. 在&#x200B;**Language**&#x200B;框中，選擇Visual C#
1. 按一下「確定」。

**添加服務引用：**

1. 在「項目」菜單中，選擇&#x200B;**添加服務引用**。
1. 在&#x200B;**地址**&#x200B;對話框中，指定作業管理器服務的WSDL。

   ```java
    https://hiro-xp:8080/soap/services/JobManager?WSDL&lc_version=9.0.1
   ```

1. 在命名空間欄位中，鍵入`JobManager`。
1. 按一下「**Go**」，然後按一下「**確定**」。
1. 在&#x200B;**Project**&#x200B;菜單中，選擇&#x200B;**添加服務引用**。
1. 在&#x200B;**Address**&#x200B;對話框中，指定FirstAppSolution/PreLoanProcess進程的WSDL。

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?WSDL&lc_version=9.0.1
   ```

1. 在命名空間欄位中，鍵入`PreLoanProcess`。
1. 按一下「**Go**」，然後按一下「**確定**」。

>[!NOTE]
>
>將`hiro-xp`替換為托管AEM Forms之J2EE應用程式伺服器的IP位址。 `lc_version`選項可確保AEM Forms功能（例如MTOM）可供使用。 若未指定`lc_version`選項，則無法使用MTOM叫用AEM Forms。 (請參閱[使用MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)叫用AEM Forms。)

### 建立調用FirstAppSolution/PreLoanProcess {#create-an-asp-page-that-invokes-firstappsolution-preloanprocess}的ASP頁

在ASP.NET項目中，添加一個Web表單（ASPX檔案），該表單負責向貸款申請人顯示HTML頁。 Web表單基於從`System.Web.UI.Page`派生的類。 調用`FirstAppSolution/PreLoanProcess`的C#應用程式邏輯位於`Button1_Click`方法中（此按鈕表示「提交應用程式」按鈕）。

下圖顯示ASP.NET應用程式

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
   <td><p>TextBoxName</p></td>
   <td><p>指定客戶的名字和姓氏。 </p></td>
  </tr>
  <tr>
   <td><p>TextBoxPhone</p></td>
   <td><p>指定客戶的電話或電子郵件地址。 </p></td>
  </tr>
  <tr>
   <td><p>TextBoxAmount</p></td>
   <td><p>指定貸款金額。</p></td>
  </tr>
  <tr>
   <td><p>Button1</p></td>
   <td><p>表示「提交申請」按鈕。</p></td>
  </tr>
  <tr>
   <td><p>LabelJobID</p></td>
   <td><p>一個標籤控制項，它指定調用標識符值的值。</p></td>
  </tr>
  <tr>
   <td><p>LabelStatus</p></td>
   <td><p>指定作業狀態值的標籤控制項。 通過調用作業管理器服務來檢索此值。 </p></td>
  </tr>
 </tbody>
</table>

屬於ASP.NET應用程式的應用程式邏輯必須動態建立XML資料源以傳遞至`FirstAppSolution/PreLoanProcess`進程。 必須在XML資料源中指定申請人在HTML頁中輸入的值。 在工作區中檢視表單時，這些資料值會合併至表單。 位於`System.Xml`命名空間中的類用於建立XML資料源。

調用需要來自ASP.NET應用程式的XML資料的進程時，可以使用XML資料類型。 也就是說，您無法將`System.Xml.XmlDocument`例項傳遞至程式。 要傳遞到進程的此XML實例的完全限定名稱為`InvokePreLoanProcess.PreLoanProcess.XML`。 將`System.Xml.XmlDocument`實例轉換為`InvokePreLoanProcess.PreLoanProcess.XML`。 您可以使用下列程式碼來執行此工作。

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

要建立調用`FirstAppSolution/PreLoanProcess`進程的ASP頁，請在`Button1_Click`方法中執行以下任務：

1. 使用其預設建構子建立`FirstAppSolution_PreLoanProcessClient`物件。
1. 使用`System.ServiceModel.EndpointAddress`建構子建立`FirstAppSolution_PreLoanProcessClient.Endpoint.Address`物件。 將指定WSDL的字串值傳遞至AEM Forms服務和編碼類型：

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?blob=mtom
   ```

   您不需要使用`lc_version`屬性。 建立服務參考時，會使用此屬性。 但請務必指定`?blob=mtom`。

   >[!NOTE]
   >
   >將`hiro-xp`*替換為托管AEM Forms的J2EE應用程式伺服器的IP地址。*

1. 獲取`FirstAppSolution_PreLoanProcessClient.Endpoint.Binding`資料成員的值，建立`System.ServiceModel.BasicHttpBinding`對象。 將傳回值轉換為`BasicHttpBinding`。
1. 將`System.ServiceModel.BasicHttpBinding`對象的`MessageEncoding`資料成員設定為`WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
1. 通過執行以下任務來啟用基本HTTP身份驗證：

   * 將AEM表單用戶名分配給資料成員`FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.UserName`。
   * 為資料成員`FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.Password`分配相應的密碼值。
   * 將常數值`HttpClientCredentialType.Basic`分配給資料成員`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 將常數值`BasicHttpSecurityMode.TransportCredentialOnly`分配給資料成員`BasicHttpBindingSecurity.Security.Mode`。

   下列程式碼範例顯示這些工作。

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

1. 檢索用戶在網頁中輸入的名稱、電話和金額值。 使用這些值動態建立發送到`FirstAppSolution/PreLoanProcess`進程的XML資料源。 建立`System.Xml.XmlDocument`，該表示要傳遞到進程的XML資料源（以下代碼示例中顯示了此應用程式邏輯）。
1. 將`System.Xml.XmlDocument`實例轉換為`InvokePreLoanProcess.PreLoanProcess.XML`（以下代碼示例中顯示了此應用程式邏輯）。
1. 調用`FirstAppSolution_PreLoanProcessClient`對象的`invoke_Async`方法來調用`FirstAppSolution/PreLoanProcess`進程。 此方法會傳回字串值，該值代表長期處理程式的叫用識別碼值。
1. 使用is建構子建立`JobManagerClient`。 （請確定您已為作業管理員服務設定服務參考。）
1. 重複步驟1-5。 指定步驟2的下列URL:`https://hiro-xp:8080/soap/services/JobManager?blob=mtom`。
1. 使用其建構子建立`JobId`物件。
1. 使用`FirstAppSolution_PreLoanProcessClient`對象`invoke_Async`方法的返回值設定`JobId`對象的`id`資料成員。
1. 將`value` true指派給`JobId`物件的`persistent`資料成員。
1. 調用`JobManagerService`對象s `getStatus`方法並傳遞`JobId`對象，建立`JobStatus`對象。
1. 通過檢索`JobStatus`對象的`statusCode`資料成員的值來獲取狀態值。
1. 將調用標識符值分配給`LabelJobID.Text`欄位。
1. 將狀態值指派給`LabelStatus.Text`欄位。

### 快速入門：使用Web服務API {#quick-start-invoking-a-long-lived-process-using-the-web-service-api}調用長期進程

以下C#代碼示例調用`FirstAppSolution/PreLoanProcess`進程。

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
>getJobDescription用戶定義方法中的值與作業管理器服務返回的值對應。

### 運行ASP.NET應用程式{#run-the-asp-net-application}

編譯和部署ASP.NET應用程式後，您可以使用Web瀏覽器執行它。 假設ASP.NET項目的名稱為&#x200B;*InvokePreLoanProcess*，請在Web瀏覽器中指定以下URL:

*http://localhost:1629/InvokePreLoanProcess/*Default.aspx

其中localhost是承載ASP.NET項目的web伺服器的名稱，1629是埠號。 當您編譯和構建ASP.NET應用程式時，Microsoft Visual Studio會自動進行部署。

>[!NOTE]
>
>要確認ASP.NET應用程式調用了該過程，請啟動Workspace並接受貸款。

## 建立使用Flex構建的客戶端應用程式，該應用程式調用以人為中心的長期進程{#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process}

您可以建立使用Flex建置的用戶端應用程式，以叫用&#x200B;*FirstAppSolution/PreLoanProcess*&#x200B;程式。 此應用程式使用Remoting調用&#x200B;*FirstAppSolution/PreLoanProcess*&#x200B;進程。 (請參閱[使用叫用AEM Forms(AEM表單已淘汰)AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)。)

下圖顯示以Flex建置的用戶端應用程式，其會收集一般使用者的資料。 資料會放入XML資料來源中，並傳送至程式。

調用該進程後，將顯示調用標識符值。 建立調用標識符值作為跟蹤長期進程狀態的記錄的一部分。

以Flex建置的用戶端應用程式會執行下列工作：

* 檢索用戶在網頁中輸入的值。
* 動態建立傳遞至&#x200B;*FirstAppSolution/PreLoanProcess*&#x200B;進程的XML資料源。 這三個值在XML資料源中指定。
* 使用Remoting調用&#x200B;*FirstAppSolution/PreLoanProcess*&#x200B;進程。
* 返回長期進程的調用標識符值。

### 步驟{#summary_of_steps-2}的摘要

要建立使用Flex構建的能夠調用FirstAppSolution/PreLoanProcess進程的客戶端應用程式，請執行以下步驟：

1. 開始新的Flex專案。
1. 在專案的類別路徑中加入adobe-remoting-provider.swc檔案。 (請參閱[包含AEM Forms Flex程式庫檔案](/help/forms/developing/invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)。)
1. 透過ActionScript或MXML建立`mx:RemoteObject`例項。 （請參閱[建立mx:RemoteObject實例](/help/forms/developing/invoking-aem-forms-using-remoting.md)）
1. 設定`ChannelSet`例項以與AEM Forms通訊，並將其與`mx:RemoteObject`例項建立關聯。 (請參閱[建立通道至AEM Forms](/help/forms/developing/invoking-aem-forms-using-remoting.md)。)
1. 調用ChannelSet的`login`方法或服務的`setCredentials`方法以指定用戶標識符值和口令。 （請參閱[使用單一登入](/help/forms/developing/invoking-aem-forms-using-remoting.md#using-single-sign-on)。）
1. 建立XML資料源以通過建立XML實例傳遞至`FirstAppSolution/PreLoanProcess`進程。 （以下程式碼範例中顯示此應用程式邏輯。）
1. 使用物件的建構函式來建立物件類型。 通過指定進程輸入參數的名稱來為對象分配XML，如以下代碼所示：

   ```csharp
    //Get the XML data to pass to the AEM Forms process
    var xml:XML = createXML();
    var params:Object = new Object();
    params["formData"]=xml;
   ```

1. 呼叫`mx:RemoteObject`實例的`invoke_Async`方法，以調用`FirstAppSolution/PreLoanProcess`進程。 傳遞包含輸入參數的`Object`。 （請參閱[傳遞輸入值](/help/forms/developing/invoking-aem-forms-using-remoting.md)。）
1. 檢索從長期進程返回的調用標識值，如以下代碼所示：

   ```csharp
    // Handles async call that invokes the long-lived process
    private function resultHandler(event:ResultEvent):void
    {
    ji = event.result as JobId;
    jobStatusDisplay.text = "Job Status ID: " + ji.jobId as String;
    }
   ```

### 使用Remoting {#invoking-a-long-lived-process-using-remoting}調用長壽命進程

以下Flex代碼示例調用`FirstAppSolution/PreLoanProcess`進程。

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
