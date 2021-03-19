---
title: 建立轉譯Forms的Web應用程式
seo-title: 建立轉譯Forms的Web應用程式
description: 建立使用Java servlet來叫用Forms服務和轉換表單的Web應用程式。 Java servlet用作返回表單的Forms服務與客戶端Web瀏覽器之間的連結。
seo-description: 建立使用Java servlet來叫用Forms服務和轉換表單的Web應用程式。 Java servlet用作返回表單的Forms服務與客戶端Web瀏覽器之間的連結。
uuid: 00de10c5-79bd-4d8a-ae18-32f1fd2623bf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f29b089e-8902-4744-81c5-15ee41ba8069
role: 開發人員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 0%

---


# 建立轉換Forms{#creating-web-applications-thatrenders-forms}的Web應用程式

**本文中的範例和範例僅適用於AEM Forms的JEE環境。**

## 建立轉換Forms{#creating-web-applications-that-renders-forms}的Web應用程式

您可以建立使用Java servlet來叫用Forms服務和轉換表單的Web應用程式。 使用Java™ servlet的好處是，您可以將進程的返回值寫入客戶端Web瀏覽器。 也就是說，Java servlet可用作傳回表單的Forms服務與用戶端網頁瀏覽器之間的連結。

>[!NOTE]
>
>本節介紹如何建立基於Web的應用程式，該應用程式使用調用Forms服務並基於片段呈現表單的Java servlet。 (請參閱[根據片段呈現Forms。)](/help/forms/developing/rendering-forms-based-fragments.md)

使用Java servlet，您可以將表單寫入客戶端Web瀏覽器，以便客戶可以查看表單並在表單中輸入資料。 在將資料填入表單後，Web使用者會按一下表單上的提交按鈕，將資訊傳回Java servlet，在Java servlet中可擷取和處理資料。 例如，資料可以傳送至另一個程式。

本節討論如何建立以Web為基礎的應用程式，讓使用者選擇以美國為基礎的表單資料或以加拿大為基礎的表單資料，如下圖所示。

![cw_cw_fragmentwebclient](assets/cw_cw_fragmentwebclient.png)

呈現的表單是以片段為基礎的表單。 也就是說，如果使用者選擇美國資料，則傳回的表格會根據美國資料使用片段。 例如，表單的頁尾包含美國地址，如下圖所示。

![cw_cw_fragementfooter](assets/cw_cw_fragementformfooter.png)

同樣地，如果使用者選擇加拿大資料，則傳回的表格會包含加拿大地址，如下圖所示。

![cw_cw_fragementformfootercnd](assets/cw_cw_fragementformfootercnd.png)

>[!NOTE]
>
>如需建立以片段為基礎的表單設計的詳細資訊，請參閱[Forms設計人員](https://www.adobe.com/go/learn_aemforms_designer_63)。

**範例檔案**

本節使用可位於以下位置的示例檔案：

&lt;>Forms設計人員安裝目錄&#x200B;*>/範例/Forms/採購單／表單片段*

其中， &lt;*install directory*>是安裝路徑。 就客戶端應用程式而言，Purchase Order Dynamic.xdp檔案從此安裝位置複製並部署到名為&#x200B;*Applications/FormsApplication*&#x200B;的Forms應用程式。 Purchase Order Dynamic.xdp檔案會放在名為FormsFolder的檔案夾中。 同樣地，這些片段會放在名為「片段」的檔案夾中，如下圖所示。

![cw_cw_fraguments儲存庫](assets/cw_cw_fragmentsrepository.png)

要訪問Purchase Order Dynamic.xdp表單設計，請指定`Applications/FormsApplication/1.0/FormsFolder/Purchase Order Dynamic.xdp`作為表單名稱（傳遞至`renderPDFForm`方法的第一個參數），並指定`repository:///`作為內容根URI值。

Web應用程式使用的XML資料檔案已從「資料」檔案夾移至`C:\Adobe`(屬於代管AEM Forms的J2EE應用程式伺服器的檔案系統)。 檔案名稱為採購單&#x200B;*Canada.xml*&#x200B;和採購單&#x200B;*US.xml*。

>[!NOTE]
>
>有關使用Workbench建立Forms應用程式的資訊，請參閱[workbench幫助](https://www.adobe.com/go/learn_aemforms_workbench_63)。

### 步驟{#summary-of-steps}摘要

若要建立以Web為基礎的應用程式，並根據片段轉譯表單，請執行下列步驟：

1. 建立新的網頁專案。
1. 建立代表Java servlet的Java應用程式邏輯。
1. 為Web應用程式建立網頁。
1. 將Web應用程式打包到WAR檔案。
1. 將WAR檔案部署至J2EE應用程式伺服器。
1. 測試您的Web應用程式。

>[!NOTE]
>
>其中有些步驟取決於部署AEM Forms的J2EE應用程式。 例如，您用來部署WAR檔案的方法取決於您使用的J2EE應用程式伺服器。 本節假設AEM Forms部署在JBoss®上。

### 建立Web項目{#creating-a-web-project}

建立包含Java servlet且可以叫用Forms服務的Web應用程式的第一步，就是建立新的Web專案。 本檔案所基於的Java IDE是Eclipse 3.3。使用Eclipse IDE，建立Web項目並將所需的JAR檔案添加到項目中。 最後，將名為&#x200B;*index.html*&#x200B;的HTML頁面和Java servlet新增至您的專案。

以下清單指定必須添加到Web項目的JAR檔案：

* adobe-forms-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar

有關這些JAR檔案的位置，請參見[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**若要建立Web專案：**

1. 啟動Eclipse，然後按一下「檔案&#x200B;**** > **新專案**」。
1. 在&#x200B;**新建項目**&#x200B;對話框中，選擇&#x200B;**Web** > **動態Web項目**。
1. 鍵入`FragmentsWebApplication`作為項目名稱，然後按一下&#x200B;**完成**。

**要將所需的JAR檔案添加到項目中，請執行以下操作：**

1. 在「項目瀏覽器」窗口中，按一下右鍵`FragmentsWebApplication`項目，然後選擇&#x200B;**屬性**。
1. 按一下&#x200B;**Java組建路徑** ，然後按一下&#x200B;**庫**&#x200B;頁籤。
1. 按一下&#x200B;**添加外部JAR**&#x200B;按鈕並瀏覽至要包含的JAR檔案。

**要將Java Servlet添加到項目中，請執行以下操作：**

1. 在「項目瀏覽器」窗口中，按一下右鍵`FragmentsWebApplication`項目，然後選擇「新建」**>**「其他」**。**
1. 展開&#x200B;**Web**&#x200B;資料夾，選擇&#x200B;**Servlet** ，然後按一下&#x200B;**Next**。
1. 在「建立Servlet」對話框中，鍵入`RenderFormFragment`作為servlet的名稱，然後按一下&#x200B;**完成**。

**若要新增HTML頁面至您的專案：**

1. 在「項目瀏覽器」窗口中，按一下右鍵`FragmentsWebApplication`項目，然後選擇「新建」**>**「其他」**。**
1. 展開&#x200B;**Web**&#x200B;資料夾，選擇&#x200B;**HTML** ，然後按一下&#x200B;**Next**。
1. 在「新建HTML」對話框中，鍵入`index.html`作為檔案名，然後按一下&#x200B;**完成**。

>[!NOTE]
>
>有關建立調用`RenderFormFragment` Java servlet的HTML頁的資訊，請參閱[建立網頁](/help/forms/developing/rendering-forms.md#creating-the-web-page)。

### 為servlet {#creating-java-application-logic-for-the-servlet}建立Java應用程式邏輯

您可以在Java servlet內建立調用Forms服務的Java應用程式邏輯。 以下代碼顯示`RenderFormFragment` Java Servlet的語法：

```java
     public class RenderFormFragment extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
         doPost(req,resp);
 
         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
             //Add code here to invoke the Forms service
             }
```

通常，您不會將用戶端程式碼置於Java servlet的`doGet`或`doPost`方法中。 更好的程式設計實務是將此程式碼放在個別的類別中、從`doPost`方法（或`doGet`方法）實例化類別，並呼叫適當的方法。 但是，對於代碼簡寫，本節中的代碼示例將保持在最小值，代碼示例將放在`doPost`方法中。

若要使用Forms服務API根據片段來呈現表單，請執行下列工作：

1. 在Java專案的類別路徑中包含用戶端JAR檔案，例如adobe-forms-client.jar。 有關這些檔案位置的資訊，請參見[包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。
1. 擷取從HTML表單提交的選項按鈕值，並指定使用美國或加拿大資料。 如果提交美國文，請建立`com.adobe.idp.Document`，以儲存位於&#x200B;*採購單US.xml*&#x200B;中的資料。 同樣地，如果是加拿大人，請建立一個`com.adobe.idp.Document`，儲存位於&#x200B;*Purchase Order Canada.xml*&#x200B;檔案中的資料。
1. 建立包含連接屬性的`ServiceClientFactory`對象。 （請參閱[設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）
1. 使用其建構子並傳遞`ServiceClientFactory`對象，建立`FormsServiceClient`對象。
1. 使用`URLSpec`的建構函式建立儲存URI值的物件。
1. 叫用`URLSpec`物件的`setApplicationWebRoot`方法，並傳遞代表應用程式Web根目錄的字串值。
1. 叫用`URLSpec`物件的`setContentRootURI`方法，並傳遞指定內容根URI值的字串值。 請確定表單設計和片段位於內容根URI中。 如果沒有，Forms服務會提出例外。 要引用AEM Forms儲存庫，請指定`repository://`。
1. 叫用`URLSpec`物件的`setTargetURL`方法，並傳遞字串值，指定表單資料張貼到的目標URL值。 如果您在表單設計中定義目標URL，則可以傳遞空字串。 您也可以指定表單傳送至的URL，以便執行計算。
1. 叫用`FormsServiceClient`物件的`renderPDFForm`方法並傳遞下列值：

   * 指定表單設計名稱的字串值，包括檔案副檔名。
   * `com.adobe.idp.Document`物件，包含要與表單合併的資料（在步驟2中建立）。
   * 儲存運行時選項的`PDFFormRenderSpec`對象。 如需詳細資訊，請參閱[AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * `URLSpec`物件，包含Forms服務根據片段來呈現表單所需的URI值。
   * 儲存檔案附件的`java.util.HashMap`對象。 此為可選參數，如果您不想將檔案附加到表單，可以指定`null`。

   `renderPDFForm`方法返回一個`FormsResult`對象，該對象包含必須寫入客戶端Web瀏覽器的表單資料流。

1. 通過調用`FormsResult`對象「s `getOutputContent`」方法建立`com.adobe.idp.Document`對象。
1. 通過調用`getContentType`方法獲取`com.adobe.idp.Document`對象的內容類型。
1. 調用`setContentType`方法並傳遞`com.adobe.idp.Document`物件的內容類型，以設定`javax.servlet.http.HttpServletResponse`物件的內容類型。
1. 呼叫`javax.servlet.http.HttpServletResponse`物件的`getOutputStream`方法，建立`javax.servlet.ServletOutputStream`物件，用來將表單資料串流寫入用戶端Web瀏覽器。
1. 調用`com.adobe.idp.Document`物件的`getInputStream`方法，以建立`java.io.InputStream`物件。
1. 通過調用`InputStream`對象的`read`方法並將位元組陣列作為引數傳遞，建立以表單資料流填充的位元組陣列。
1. 叫用`javax.servlet.ServletOutputStream`物件的`write`方法，將表單資料串流傳送至用戶端網頁瀏覽器。 將位元組陣列傳遞到`write`方法。

以下代碼示例表示調用Forms服務並基於片段呈現表單的Java servlet。

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.File;
 import java.io.FileInputStream;
 import java.io.IOException;
 import java.io.PrintWriter;
 
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 import java.net.URL;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderFormFragment extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
 
     }
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
     throws ServletException, IOException {
 
 
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Get the value of selected radio button
             String radioValue = req.getParameter("radio");
 
             //Create an Document object to store form data
             Document oInputData = null;
 
             //The value of the radio button determines the form data to use
             //which determines which fragments used in the form
             if (radioValue.compareTo("AMERICAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order US.xml");
                 oInputData = new Document(myData);
             }
             else if (radioValue.compareTo("CANADIAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order Canada.xml");
                 oInputData = new Document(myData);
             }
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Set the parameter values for the renderPDFForm method
             String formName = "Applications/FormsApplication/1.0/FormsFolder/Purchase Order Dynamic.xdp";
 
             //Cache the PDF form
             PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
             pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
 
             //Specify URI values that are required to render a form
             //design based on fragments
             URLSpec uriValues = new URLSpec();
             uriValues.setApplicationWebRoot("https://'[server]:[port]'/RenderFormFragment");
             uriValues.setContentRootURI("repository:///");
             uriValues.setTargetURL("https://'[server]:[port]'/FormsServiceClientApp/HandleData");
 
             //Invoke the renderPDFForm method and write the
             //results to a client web browser
             FormsResult formOut = formsClient.renderPDFForm(
                         formName,               //formQuery
                         oInputData,             //inDataDoc
                         pdfFormRenderSpec,      //PDFFormRenderSpec
                         uriValues,                //urlSpec
                         null                    //attachments
                         );
 
             //Create a Document object that stores form data
             Document myData = formOut.getOutputContent();
 
             //Get the content type of the response and
             //set the HttpServletResponse object’s content type
             String contentType = myData.getContentType();
             resp.setContentType(contentType);
 
             //Create a ServletOutputStream object
             ServletOutputStream oOutput = resp.getOutputStream();
 
             //Create an InputStream object
             InputStream inputStream = myData.getInputStream();
 
             //Write the data stream to the web browser
             byte[] data = new byte[4096];
             int bytesRead = 0;
             while ((bytesRead = inputStream.read(data)) > 0)
             {
                 oOutput.write(data, 0, bytesRead);
             }
 
         }catch (Exception e) {
              System.out.println("The following exception occurred: "+e.getMessage());
       }
     }
 }
```

### 建立網頁{#creating-the-web-page}

index.html網頁提供Java servlet的入口點，並調用Forms服務。 此網頁是基本的HTML表單，包含兩個選項按鈕和一個提交按鈕。 選項按鈕的名稱是單選按鈕。 當使用者按一下提交按鈕時，表單資料會張貼至`RenderFormFragment` Java servlet。

Java servlet會使用下列Java程式碼，從HTML頁面擷取張貼的資料：

```java
             Document oInputData = null;
 
             //Get the value of selected radio button
             String radioValue = req.getParameter("radio");
 
             //The value of the radio button determines the form data to use
             //which determines which fragments used in the form
             if (radioValue.compareTo("AMERICAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order US.xml");
                 oInputData = new Document(myData);
             }
             else if (radioValue.compareTo("CANADIAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order Canada.xml");
                 oInputData = new Document(myData);
             }
```

以下HTML程式碼位於在設定開發環境時建立的index.html檔案中。 （請參閱[建立Web項目](/help/forms/developing/rendering-forms.md#creating-a-web-project)。）

```xml
 <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
 <html xmlns="https://www.w3.org/1999/xhtml">
 <head>
 <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
 <title>Untitled Document</title>
 </head>
 
 <body>
 <form name="myform" action="https://'[server]:[port]'/FragmentsWebApplication/RenderFormFragment" method="post">
      <table>
      <tr>
        <th>Forms Fragment Web Client</th>
      </tr>
      <tr>
        <td>
          <label>
          <input type="radio" name="radio" id="radio_Data" value="CANADIAN" />
          Canadian data<br />
          </label>
          <p>
            <label>
            <input type="radio" name="radio" id="radio_Data" value="AMERICAN" checked/>
            American data</label>
          </p>
        </td>
      </tr>
      <tr>
      <td>
        <label>
          <input type="submit" name="button_Submit" id="button_Submit" value="Submit" />
            </label>
            </td>
         </tr>
        </table>
      </form>
 </body>
 </html>
```

### 打包Web應用程式{#packaging-the-web-application}

要部署調用Forms服務的Java Servlet，請將Web應用程式打包到WAR檔案。 請確定WAR檔案中也包含元件商業邏輯所依賴的外部JAR檔案，例如adobe-livecycle-client.jar和adobe-forms-client.jar。

**要將Web應用程式打包到WAR檔案：**

1. 在&#x200B;**項目瀏覽器**&#x200B;窗口中，按一下右鍵`FragmentsWebApplication`項目並選擇&#x200B;**導出** > **WAR檔案**。
1. 在&#x200B;**Web模組**&#x200B;文本框中，鍵入`FragmentsWebApplication`作為Java項目的名稱。
1. 在&#x200B;**Destination**&#x200B;文本框中，鍵入&#x200B;`FragmentsWebApplication.war`**作為**&#x200B;檔案名，指定WAR檔案的位置，然後按一下「Finish（完成）」。

### 將WAR檔案部署到J2EE應用程式伺服器{#deploying-the-war-file-to-the-j2ee-application-server}

您可將WAR檔案部署至部署了AEM Forms的J2EE應用程式伺服器。 部署WAR檔案後，您可以使用Web瀏覽器訪問HTML網頁。

**要將WAR檔案部署到J2EE應用程式伺服器，請執行以下操作：**

* 將WAR檔案從導出路徑複製到`[Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\all\deploy`。

### 測試您的Web應用程式{#testing-your-web-application}

部署Web應用程式後，您可以使用Web瀏覽器來測試它。 假設您使用的是裝載AEM Forms的同一部電腦，您可以指定下列URL:

* http://localhost:8080/FragmentsWebApplication/index.html

   選擇單選按鈕，然後按一下「提交」按鈕。 網頁瀏覽器中會顯示以片段為基礎的表單。 如果發生問題，請查看J2EE應用程式伺服器的記錄檔。

