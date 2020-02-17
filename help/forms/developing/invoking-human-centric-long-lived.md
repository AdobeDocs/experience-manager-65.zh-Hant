---
title: 調用以人為中心的長壽命進程
seo-title: 調用以人為中心的長壽命進程
description: 'null'
seo-description: 'null'
uuid: 42269d41-a90f-4ea1-aeb9-d61337bcfa54
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 18a320b4-dce6-4c50-8864-644b0b2d6644
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# 調用以人為中心的長壽命進程 {#invoking-human-centric-long-lived-processes}

您可以使用下列用戶端應用程式，以程式設計方式叫用在Workbench中建立的以人為中心的長期流程：

* 使用調用API的Java基於Web的客戶端應用程式。 (請參 [閱「使用Java API叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md)」(/help/forms/developing/invoking-aem-forms-using-java.md#ucking-aem-forms-using-the-java-api))。
* 使用web services的ASP.NET應用程式。 (請參 [閱使用Web services叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services))。
* 使用Flex建立的用戶端應用程式，使用Remoting。 (請參 [閱使用（AEM表單已過時）AEM Forms Remoting叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting))。

調用的長期進程名為 *FirstAppSolution/PreLoanProcess*。 您可以遵循「建立您的第一個AEM Forms應用程式」中指 [定的教學課程，來建立此程式](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63)。

以人為中心的程式涉及使用者可使用工作區來回應的工作。 例如，您可以使用「工作台」建立流程，讓銀行經理核准或拒絕貸款申請。 下圖顯示流程 *FirstAppSolution/PreLoanProcess*。

FirstAppSolution/ *PreLoanProcess* 進程接受名為 *formData* 的輸入參數，其資料類型為XML。 XML資料會與名為 *PreLoanForm.xdp的表單設計合併*。 下圖顯示一個表單，它代表指派給用戶以批准或拒絕貸款申請的任務。 使用者使用「工作區」核准或拒絕應用程式。 「工作區」使用者可以按一下下圖所示的「核准」按鈕，以核准貸款要求。 同樣地，使用者也可以按一下拒絕按鈕來拒絕貸款要求。

由於以下因素，長壽命進程被非同步調用，且無法同步調用：

* 流程可以跨越大量時間。
* 流程可以跨越組織界限。
* 流程需要外部輸入才能完成。 例如，假設某個表單被傳送給不在辦公室的經理。 在這種情況下，在管理員返回並填寫表單之前，該過程不會完成。

當呼叫長期處理時，AEM Forms會建立呼叫識別碼值，做為建立記錄的一部分。 記錄會追蹤長期處理的狀態，並儲存在AEM Forms資料庫中。 使用調用標識符值，可以跟蹤長壽命進程的狀態。 此外，您可以使用進程調用標識符值來執行進程管理器操作，如終止正在運行的進程實例。

>[!NOTE]
>
>AEM Forms不會在呼叫短暫的程式時建立呼叫識別碼值或記錄。

當申 `FirstAppSolution/PreLoanProcess` 請人提交申請時，該程式被調用，該申請被表示為XML資料。 輸入進程變數的名稱為， `formData` 其資料類型為XML。 在本討論中，假設以下XML資料是用來輸入程式的 `FirstAppSolution/PreLoanProcess` 。

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <LoanApp>
 <Name>Sam White</Name>
 <LoanAmount>250000</LoanAmount>
 <PhoneOrEmail>(555)555-5555</PhoneOrEmail>
 <ApprovalStatus>PENDING APPROVAL</ApprovalStatus>
 </LoanApp>
```

傳遞至流程的XML資料必須與流程中使用的表單中的欄位相符。 否則，表單中不會顯示資料。 所有調用該進程的 `FirstAppSolution/PreLoanProcess` 應用程式都必須傳遞此XML資料源。 在「叫用以 *人為中心的長壽命流程* 」中建立的應用程式，會根據使用者輸入至網頁用戶端的值，動態建立XML資料來源。

使用用戶端應用程式，您可以傳送 *FirstAppSolution/PreLoanProcess* ，以處理所需的XML資料。 長期進程返回調用標識符值作為其返回值。 下圖顯示調用*FirstAppSolution/PreLoanProcess的客戶端應用程式。 用戶端應用程式會傳送XML資料，並回傳代表呼叫識別碼值的字串值。

**另請參閱**

[建立Java web應用程式，以叫用以人為中心的長壽命程式](invoking-human-centric-long-lived.md#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process)

[建立ASP.NET網路應用程式，以叫用以人為中心的長壽命程式](invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

[建立使用Flex建立的用戶端應用程式，以叫用以人為中心的長壽命程式](invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

## 建立Java web應用程式，以叫用以人為中心的長壽命程式 {#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process}

您可以建立使用Java servlet來叫用程式的基於Web的應用 `FirstAppSolution/PreLoanProcess` 程式。 要從Java servlet調用此進程，請使用Java servlet中的調用API。 (請參 [閱使用Java API叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api))。

下圖顯示以Web為基礎的用戶端應用程式，其中會發佈名稱、電話（或電子郵件）和金額值。 當使用者按一下「提交應用程式」按鈕時，這些值會傳送至Java servlet。

Java servlet將執行以下任務：

* 檢索從HTML頁張貼到Java servlet的值。
* 動態建立XML資料來源，以傳遞至 *FirstAppSolution/PreLoanProcess* 程式。 名稱、電話（或電子郵件）和金額值會在XML資料來源中指定。
* 使用 *AEM Forms Invocation API叫用FirstAppSolution/PreLoanProcess* 。
* 將調用標識符值返回到客戶端Web瀏覽器。

### 步驟摘要 {#summary-of-steps}

要建立調用該進程的基於Java的Web的應 `FirstAppSolution/PreLoanProcess` 用程式，請執行以下步驟：

1. [建立網頁專案](invoking-human-centric-long-lived.md#create-a-web-project)。
1. [為servlet建立Java應用程式邏輯](invoking-human-centric-long-lived.md#create-java-application-logic-for-the-servlet)。
1. [為Web應用程式建立網頁](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)
1. [將Web應用程式打包到WAR檔案](invoking-human-centric-long-lived.md#package-the-web-application-to-a-war-file)。
1. [將WAR檔案部署至代管AEM Forms的J2EE應用程式伺服器](invoking-human-centric-long-lived.md#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms)。
1. [測試您的Web應用程式](invoking-human-centric-long-lived.md#test-your-web-application)。

>[!NOTE]
>
>其中一些步驟取決於部署AEM Forms的J2EE應用程式。 例如，您用來部署WAR檔案的方法取決於您使用的J2EE應用程式伺服器。 假設AEM Forms已部署在JBoss®上。

### 建立網頁專案 {#create-a-web-project}

建立Web應用程式的第一步是建立Web專案。 本檔案所基於的Java IDE是Eclipse 3.3。使用Eclipse IDE，建立Web項目並將所需的JAR檔案添加到項目中。 將名為 *index.html* 和Java servlet的HTML頁面新增至專案。

以下清單指定要包含在Web項目中的JAR檔案：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* J2EE.jar

如需這些JAR檔案的位置，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

>[!NOTE]
>
>J2EE.jar檔案定義Java servlet使用的資料類型。 您可從部署AEM Forms的J2EE應用程式伺服器取得此JAR檔案。

**建立網頁專案**

1. 啟動Eclipse，然後按一 **下「檔案** >新 **增專案」**。
1. 在「新 **增專案** 」對話方塊中，選 **取「Web** > **動態網頁專案**」。
1. 輸 `InvokePreLoanProcess` 入專案名稱，然後按一下「完 **成」**。

**將所需的JAR檔案添加到項目中**

1. 在「項目瀏覽器」窗口中，按一下右鍵項目，然 `InvokePreLoanProcess` 後選擇「屬 **性」**。
1. 按一 **下「Java建置路徑** 」，然後按一下「 **資料庫** 」標籤。
1. 按一下「 **添加外部JAR** 」按鈕，並瀏覽至要包含的JAR檔案。

**將Java Servlet添加到項目**

1. 在「項目瀏覽器」窗口中，按一下右鍵項 `InvokePreLoanProcess` 目並選擇「 **新建** 」>「 **其他**」。
1. 展開「 **Web** 」資料夾，選 **擇「Servlet**」，然後按一下「 **Next**」。
1. 在「建立Servlet」對話框中，鍵 `SubmitXML` 入servlet的名稱，然後按一下「完 **成」**。

**新增HTML頁面至您的專案**

1. 在「項目瀏覽器」窗口中，按一下右鍵項 `InvokePreLoanProcess` 目並選擇「 **新建** 」>「 **其他**」。
1. 展開「 **Web** 」檔案夾，選 **取「HTML**」，然後按「 **下一步**」。
1. 在「新建HTML」對話方塊中，輸入檔 `index.html` 名，然後按一下「完 **成」**。

>[!NOTE]
>
>有關建立調用SubmitXML Java servlet的HTML內容的資訊，請參 [閱為Web應用程式建立網頁](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)。

### 為servlet建立Java應用程式邏輯 {#create-java-application-logic-for-the-servlet}

建立從Java servlet內調用 `FirstAppSolution/PreLoanProcess` 進程的Java應用程式邏輯。 下列程式碼顯示 `SubmitXML` Java servlet的語法：

```as3
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

通常，您不會將用戶端程式碼置於Java servlet或方 `doGet` 法 `doPost` 中。 更好的程式設計實務是將此程式碼放在個別類別中。 然後從方法（或方法）中 `doPost` 實例化類 `doGet` 別，並呼叫適當的方法。 不過，若是程式碼簡寫，程式碼範例會維持在最小值，並置於方 `doPost` 法中。

要使用調 `FirstAppSolution/PreLoanProcess` 用API調用進程，請執行以下任務：

1. 在您Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-livecycle-client.jar。 如需這些檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。
1. 擷取從HTML頁面提交的名稱、電話和金額值。 使用這些值動態建立傳送至程式的XML資料來源 `FirstAppSolution/PreLoanProcess` 。 您可以使用 `org.w3c.dom` 類別來建立XML資料來源（此應用程式邏輯如下列程式碼範例所示）。
1. 建立包 `ServiceClientFactory` 含連接屬性的對象。 (請參 [閱設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)
1. 使用其 `ServiceClient` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。 對 `ServiceClient` 像可讓您調用服務操作。 它可處理如定位、調度和路由調用請求等任務。
1. 使用其 `java.util.HashMap` 建構函式建立物件。
1. 針對每 `java.util.HashMap` 個輸入參 `put` 數叫用物件的方法，以傳遞至長期的程式。 請確定您指定流程輸入參數的名稱。 由於此 `FirstAppSolution/PreLoanProcess` 過程需要一個類型( `XML` 命名 `formData`)的輸入參數，因此您只需調用該方法一 `put` 次。

   ```as3
    //Get the XML to pass to the FirstAppSolution/PreLoanProcess process
    org.w3c.dom.Document inXML = GetDataSource(name,phone,amount);
    
    //Create a Map object to store the parameter value
    Map params = new HashMap();
    params.put("formData", inXML);
   ```

1. 調用物 `InvocationRequest` 件的方法並傳 `ServiceClientFactory` 遞下列值， `createInvocationRequest` 以建立物件：

   * 一個字串值，它指定要調用的長生命週期進程的名稱。 要調用該 `FirstAppSolution/PreLoanProcess` 進程，請指定 `FirstAppSolution/PreLoanProcess`。
   * 表示流程操作名稱的字串值。 長壽命流程操作的名稱為 `invoke`。
   * 包 `java.util.HashMap` 含服務操作所需參數值的對象。
   * 一個布爾值，它 `false`指定建立非同步請求（此值適用於調用長壽命進程）。
   >[!NOTE]
   >
   >*將值true傳入createInvocationRequest方法的第四個參數，即可叫用短暫的程式。 傳遞值true會建立同步請求。*

1. 呼叫物件的方法並傳遞物件，將呼叫 `ServiceClient` 請求傳 `invoke` 送至AEM Forms `InvocationRequest` 。 方法 `invoke` 返回對 `InvocationReponse` 像。
1. 長期進程返回一個字串值，該字串值表示調用標識值。 調用物件的方法 `InvocationReponse` 來擷取此 `getInvocationId` 值。

   ```as3
    //Send the invocation request to the long-lived process and
    //get back an invocation response object
    InvocationResponse lcResponse = myServiceClient.invoke(lcRequest);
    String invocationId = lcResponse.getInvocationId();
   ```

1. 將調用標識值寫入客戶端Web瀏覽器。 您可以使用例 `java.io.PrintWriter` 項將此值寫入用戶端網頁瀏覽器。

### 快速入門：使用調用API調用長壽命進程 {#quick-start-invoking-a-long-lived-process-using-the-invocation-api}

以下Java代碼示例表示調用進程的Java servlet `FirstAppSolution/PreLoanProcess` 。

```as3
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

此 *index.html* 網頁提供了調用該進程的Java servlet的入 `FirstAppSolution/PreLoanProcess` 口點。 此網頁是基本的HTML表單，包含HTML表單和送出按鈕。 當使用者按一下提交按鈕時，表單資料會張貼至 `SubmitXML` Java servlet。

Java servlet會使用下列Java程式碼，從HTML頁面擷取張貼的資料：

```as3
 //Get the values that are passed from the Loan HTML page
 String name = request.getParameter("name");
 String phone = request.getParameter("phone");
 String amount = request.getParameter("amount");
```

以下HTML程式碼代表在設定開發環境期間建立的index.html檔案。 (請參 [閱建立Web專案](invoking-human-centric-long-lived.md#create-a-web-project)。)

```as3
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

要部署調用該進程的Java servlet `FirstAppSolution/PreLoanProcess` ，請將Web應用程式打包到WAR檔案。 請確定WAR檔案中也包含元件商業邏輯所依賴的外部JAR檔案，例如adobe-livecycle-client.jar和adobe-usermanager-client.jar。

下圖顯示Eclipse專案的內容，此內容已封裝為WAR檔案。

>[!NOTE]
>
>在上圖中，JPG檔案可以由任何JPG影像檔案取代。

**將Web應用程式打包到WAR檔案：**

1. 在「項 **目瀏覽器** 」窗口中，按一下右鍵項 `InvokePreLoanProcess` 目並選擇「導 **出** 」>「 **WAR檔案」**。
1. 在「 **Web模組** 」文本框中， `InvokePreLoanProcess` 鍵入Java項目的名稱。
1. 在「目 **的地** 」文字方塊中， `PreLoanProcess.war`**輸&#x200B;**入檔案名稱，指定WAR檔案的位置，然後按一下「完成」。

### 將WAR檔案部署至代管AEM Forms的J2EE應用程式伺服器 {#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms}

將WAR檔案部署至部署AEM Forms的J2EE應用程式伺服器。 若要將WAR檔案部署至J2EE應用程式伺服器，請將WAR檔案從匯出路徑複製至 *[AEM Forms Install]*\Adobe\Adobe Experience Manager Forms\jboss\server\lc_turnkey\deploy。

>[!NOTE]
>
>如果AEM Forms未部署在JBoss上，則您必須依照代管AEM Forms的J2EE應用程式伺服器部署WAR檔案。

### 測試您的Web應用程式 {#test-your-web-application}

部署Web應用程式後，您可以使用Web瀏覽器來測試它。 假設您使用的是代管AEM Forms的相同電腦，您可以指定下列URL:

* http://localhost:8080/PreLoanProcess/index.html

   在HTML表單欄位中輸入值，然後按一下「提交申請」按鈕。 如果發生問題，請查看J2EE應用程式伺服器的記錄檔。

   ***注意&#x200B;**:要確認Java應用程式調用了該流程，請啟動Workspace並接受貸款。*

## 建立ASP.NET網路應用程式，以叫用以人為中心的長壽命程式 {#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process}

您可以建立調用該進程的ASP.NET應用 `FirstAppSolution/PreLoanProcess` 程式。 要從ASP.NET應用程式調用此過程，請使用web services。 (請參 [閱使用Web services叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services))。

下圖顯示ASP.NET客戶端應用程式從最終用戶獲取資料。 資料會放入XML資料來源中，當使用者按一下「提交應 `FirstAppSolution/PreLoanProcess` 用程式」按鈕時，就會傳送至程式。

注意，調用過程後，將顯示調用標識符值。 建立調用標識符值作為跟蹤長期進程狀態的記錄的一部分。

ASP.NET應用程式執行以下任務：

* 擷取使用者在網頁中輸入的值。
* 動態建立XML資料來源，並傳遞至* FirstAppSolution/PreLoanProcess *process。 這三個值在XML資料源中指定。
* 使用web services叫用* FirstAppSolution/PreLoanProcess *進程。
* 將調用標識符值和長期操作的狀態返回到客戶端Web瀏覽器。

### 步驟摘要 {#summary_of_steps-1}

要建立能夠調用FirstAppSolution/PreLoanProcess的ASP.NET應用程式，請執行以下步驟：

1. [建立ASP.NET網頁應用程式](invoking-human-centric-long-lived.md#create-an-asp-net-web-application)。
1. [建立叫用FirstAppSolution/PreLoanProcess的ASP頁面](invoking-human-centric-long-lived.md#create-an-asp-page-that-invokes-firstappsolution-preloanprocess)。
1. [運行ASP.NET應用程式](invoking-human-centric-long-lived.md#run-the-asp-net-application)。

### 建立ASP.NET網頁應用程式 {#create-an-asp-net-web-application}

建立Microsoft .NET C# ASP.NET web應用程式。 下圖顯示名為 *InvokePreLoanProcess的ASP.NET項目的內*&#x200B;容。

注意，在「服務參考」下，有兩個項目。 第一個項目名為* JobManager*。 此參考使ASP.NET應用程式能夠調用Job Manager服務。 此服務會傳回有關長期流程狀態的資訊。 例如，如果進程當前正在運行，則此服務將返回一個數值，該數值指定當前正在運行的進程。 第二個參考名&#x200B;*為PreLoanProcess*。 本服務參考代表對* FirstAppSolution/PreLoanProcess *進程的參考。 建立「服務參考」後，與AEM Forms服務關聯的資料類型即可用於您的。NET專案中。

**建立ASP.NET項目：**

1. 啟動Microsoft Visual Studio 2008。
1. 從「檔 **案** 」選單中，選 **擇「新增**, **網站**」。
1. 在「模 **板** 」清單中，選 **擇「ASP.NET網站」**。
1. 在「位 **置** 」方塊中，選取專案的位置。 將您的專案命 *名為InvokePreLoanProcess*。
1. 在「語 **言** 」框中，選擇「Visual C#」
1. 按一下「確定」。

**添加服務引用：**

1. 在「項目」菜單中，選擇「添 **加服務參考」**。
1. 在「地 **址** 」對話框中，為「作業管理器」服務指定WSDL。

   ```as3
    https://hiro-xp:8080/soap/services/JobManager?WSDL&lc_version=9.0.1
   ```

1. 在「命名空間」欄位中，輸入 `JobManager`。
1. 按一 **下「**&#x200B;執行」，然後按一下&#x200B;**「確定」**。
1. 在「項目 **」菜單中** ，選擇「 **添加服務參考」**。
1. 在「位 **址** 」對話方塊中，指定FirstAppSolution/PreLoanProcess程式的WSDL。

   ```as3
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?WSDL&lc_version=9.0.1
   ```

1. 在「命名空間」欄位中，輸入 `PreLoanProcess`。
1. 按一 **下「**&#x200B;執行」，然後按一下&#x200B;**「確定」**。

>[!NOTE]
>
>以 `hiro-xp` 代管AEM Forms的J2EE應用程式伺服器的IP位址取代。 此選 `lc_version` 項可確保AEM Forms功能（例如MTOM）可供使用。 若未指定 `lc_version`選項，就無法使用MTOM叫用AEM Forms。 (請參 [閱使用MTOM叫用AEM表格](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom))。

### 建立叫用FirstAppSolution/PreLoanProcess的ASP頁面 {#create-an-asp-page-that-invokes-firstappsolution-preloanprocess}

在ASP.NET專案中，新增負責向貸款申請人顯示HTML頁面的Web表單（ASPX檔案）。 Web表單以衍生自的類為基礎 `System.Web.UI.Page`。 叫用的C#應用程式邏輯位 `FirstAppSolution/PreLoanProcess` 於方法中(此按鈕 `Button1_Click` 代表「提交應用程式」按鈕)。

下圖顯示ASP.NET應用程式

下表列出屬於此ASP.NET應用程式的控制項。

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
   <td><p>一個標籤控制，它指定調用標識符值的值。</p></td>
  </tr>
  <tr>
   <td><p>LabelStatus</p></td>
   <td><p>指定作業狀態值的標籤控制。 通過調用作業管理器服務來檢索此值。 </p></td>
  </tr>
 </tbody>
</table>

作為ASP.NET應用程式一部分的應用程式邏輯必須動態建立XML資料來源，以傳遞至程 `FirstAppSolution/PreLoanProcess` 序。 必須在XML資料來源中指定申請人在HTML頁面中輸入的值。 當在工作區中檢視表單時，這些資料值會合併到表單中。 位於命名空間 `System.Xml` 中的類用於建立XML資料源。

當從ASP.NET應用程式叫用需要XML資料的程式時，您可使用XML資料類型。 也就是說，您無法將實 `System.Xml.XmlDocument` 例傳遞至流程。 要傳遞給該進程的此XML實例的完全限定名稱為 `InvokePreLoanProcess.PreLoanProcess.XML`。 將例項 `System.Xml.XmlDocument` 轉換為 `InvokePreLoanProcess.PreLoanProcess.XML`。 您可以使用下列程式碼來執行此工作。

```as3
 //Create the XML to pass to the FirstAppSolution/PreLoanProcess process
 XmlDocument myXML = CreateXML(userName, phone, amount);
 
 //Convert the XML to a InvokePreLoanProcess.PreLoanProcess.XML instance
 StringWriter sw = new StringWriter();
 XmlTextWriter xw = new XmlTextWriter(sw);
 myXML.WriteTo(xw);
 
 InvokePreLoanProcess.PreLoanProcess.XML inXML = new XML();
 inXML.document = sw.ToString();
```

要建立調用該流程的ASP `FirstAppSolution/PreLoanProcess` 頁，請在方法中執行以下 `Button1_Click` 任務：

1. 使用其 `FirstAppSolution_PreLoanProcessClient` 預設建構函式建立物件。
1. 使用建 `FirstAppSolution_PreLoanProcessClient.Endpoint.Address` 構函式建立物 `System.ServiceModel.EndpointAddress` 件。 將指定WSDL的字串值傳遞至AEM Forms服務和編碼類型：

   ```as3
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?blob=mtom
   ```

   您不需要使用屬 `lc_version` 性。 建立服務參考時，將使用此屬性。 不過，請確定您已指定 `?blob=mtom`。

   >[!NOTE]
   >
   >以 `hiro-xp`代管AEM Forms的J2EE應用程式伺服器的IP位址取代*。*

1. 通過獲 `System.ServiceModel.BasicHttpBinding` 取資料成員的值建立 `FirstAppSolution_PreLoanProcessClient.Endpoint.Binding` 對象。 將返回值轉換為 `BasicHttpBinding`。
1. 將物 `System.ServiceModel.BasicHttpBinding` 件的資料 `MessageEncoding` 成員設為 `WSMessageEncoding.Mtom`。 此值可確保使用MTOM。
1. 執行下列工作以啟用基本HTTP驗證：

   * 將AEM表單使用者名稱指派給資料成員 `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.UserName`。
   * 為資料成員分配相應的口令值 `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.Password`。
   * 為資料成員 `HttpClientCredentialType.Basic` 分配常數值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 為資料成員 `BasicHttpSecurityMode.TransportCredentialOnly` 分配常數值 `BasicHttpBindingSecurity.Security.Mode`。
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

1. 擷取使用者在網頁中輸入的名稱、電話和金額值。 使用這些值動態建立傳送至程式的XML資料來源 `FirstAppSolution/PreLoanProcess` 。 建立表 `System.Xml.XmlDocument` 示要傳遞至流程的XML資料源（此應用程式邏輯如下面的代碼示例所示）。
1. 將例項 `System.Xml.XmlDocument` 轉換為 `InvokePreLoanProcess.PreLoanProcess.XML` （此應用程式邏輯如下列程式碼範例所示）。
1. 叫用 `FirstAppSolution/PreLoanProcess` 物件的方 `FirstAppSolution_PreLoanProcessClient` 法以叫用 `invoke_Async` 程式。 此方法返回一個字串值，該字串值表示長壽命進程的調用標識符值。
1. 使用is建 `JobManagerClient` 構函式建立。 （請確定您已經為Job Manager服務設定了服務參考。）
1. 重複步驟1-5。 指定步驟2的下列URL: `https://hiro-xp:8080/soap/services/JobManager?blob=mtom`。
1. 使用其 `JobId` 建構函式建立物件。
1. 使用物 `JobId` 件方 `id` 法的傳回值設定物 `FirstAppSolution_PreLoanProcessClient` 件的資料成 `invoke_Async` 員。
1. 為對 `value` 像的資料 `JobId` 成員指 `persistent` 定true。
1. 通過調 `JobStatus` 用對象的方 `JobManagerService` 法並傳遞對 `getStatus` 像來建立對 `JobId` 像。
1. 通過檢索對象的資料成員的值 `JobStatus` 來獲取狀 `statusCode` 態值。
1. 將調用標識符值分配給 `LabelJobID.Text` 欄位。
1. 將狀態值指派給欄 `LabelStatus.Text` 位。

### 快速入門：使用web service API叫用長期的程式 {#quick-start-invoking-a-long-lived-process-using-the-web-service-api}

以下C#代碼示例調用該 `FirstAppSolution/PreLoanProcess`過程。

```as3
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
>getJobDescription用戶定義方法中的值對應於Job Manager服務返回的值。

### 運行ASP.NET應用程式 {#run-the-asp-net-application}

編譯和部署ASP.NET應用程式後，您可以使用Web瀏覽器執行它。 假設ASP.NET專案的名稱為 *InvokePreLoanProcess*，請在網頁瀏覽器中指定下列URL:

*http://localhost:1629/InvokePreLoanProcess/*Default.aspx

其中， localhost是代管ASP.NET項目的Web伺服器的名稱，1629是埠號。 編譯和構建ASP.NET應用程式時，Microsoft Visual studio會自動進行部署。

>[!NOTE]
>
>要確認ASP.NET應用程式調用了該流程，請啟動Workspace並接受貸款。

## 建立使用Flex建立的用戶端應用程式，以叫用以人為中心的長壽命程式 {#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process}

您可以建立使用Flex建立的用戶端應用程式，以叫用 *FirstAppSolution/PreLoanProcess* 程式。 此應用程式使用Remoting來叫 *用FirstAppSolution/PreLoanProcess* 程式。 (請參 [閱使用（AEM表單已過時）AEM Forms Remoting叫用AEM Forms](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting))。

下圖顯示以Flex建立的用戶端應用程式，可收集使用者的資料。 資料會放入XML資料來源中，並傳送至程式。

注意，調用過程後，將顯示調用標識符值。 建立調用標識符值作為跟蹤長期進程狀態的記錄的一部分。

使用Flex建立的用戶端應用程式會執行下列工作：

* 擷取使用者在網頁中輸入的值。
* 動態建立XML資料來源，並傳遞至 *FirstAppSolution/PreLoanProcess* 程式。 這三個值在XML資料源中指定。
* 使用 *Remoting叫用FirstAppSolution/PreLoanProcess* 進程。
* 返回長壽命進程的調用標識符值。

### 步驟摘要 {#summary_of_steps-2}

若要建立以Flex建立的用戶端應用程式，以叫用FirstAppSolution/PreLoanProcess程式，請執行下列步驟：

1. 開始新的Flex專案。
1. 在專案的類別路徑中加入adobe-remoting-provider.swc檔案。 (請參 [閱「包含AEM Forms flex程式庫檔案](/help/forms/developing/invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)」)。
1. 透過ActionScript `mx:RemoteObject` 或MXML建立例項。 (請參 [閱建立mx:RemoteObject例項](/help/forms/developing/invoking-aem-forms-using-remoting.md))
1. 設定要 `ChannelSet` 與AEM Forms通訊的例項，並將其與例項關 `mx:RemoteObject` 聯。 (請參 [閱「建立AEM表單的渠道](/help/forms/developing/invoking-aem-forms-using-remoting.md)」)。
1. 呼叫ChannelSet的方 `login` 法或服務的方法， `setCredentials` 以指定使用者識別碼值和密碼。 (請參 [閱使用單一登入](/help/forms/developing/invoking-aem-forms-using-remoting.md#using-single-sign-on)。)
1. 建立XML資料來源，以便透過建 `FirstAppSolution/PreLoanProcess` 立XML例項傳遞至程式。 （此應用程式邏輯如下列程式碼範例所示。）
1. 使用其建構子建立Object類型的對象。 指定程式輸入參數的名稱，將XML指派給物件，如下列程式碼所示：

   ```as3
    //Get the XML data to pass to the AEM Forms process
    var xml:XML = createXML();
    var params:Object = new Object();
    params["formData"]=xml;
   ```

1. 呼叫 `FirstAppSolution/PreLoanProcess` 例項的方 `mx:RemoteObject` 法以叫用 `invoke_Async` 程式。 傳遞包 `Object` 含輸入參數的參數。 (請參 [閱傳遞輸入值](/help/forms/developing/invoking-aem-forms-using-remoting.md)。)
1. 檢索從長壽命進程返回的調用標識值，如以下代碼所示：

   ```as3
    // Handles async call that invokes the long-lived process
    private function resultHandler(event:ResultEvent):void
    {
    ji = event.result as JobId;
    jobStatusDisplay.text = "Job Status ID: " + ji.jobId as String;
    }
   ```

### 使用Remoting調用長壽命進程 {#invoking-a-long-lived-process-using-remoting}

以下Flex程式碼範例會叫用此 `FirstAppSolution/PreLoanProcess` 程式。

```as3
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

