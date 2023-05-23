---
title: 建立呈現Forms的Web應用程式
seo-title: Creating Web Applications thatRenders Forms
description: 建立基於Web的應用程式，該應用程式使用Java Servlet調用Forms服務和呈現表單。 Java Servlet用作返回表單的Forms服務與客戶端Web瀏覽器之間的連結。
seo-description: Create a web-based application that uses Java servlets to invoke the Forms service and render forms. The Java servlet serves as the link between the Forms service that returns a form and a client web browser.
uuid: 00de10c5-79bd-4d8a-ae18-32f1fd2623bf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f29b089e-8902-4744-81c5-15ee41ba8069
role: Developer
exl-id: 85e00003-8c8b-463a-b728-66af174be295
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 0%

---

# 建立呈現Forms的Web應用程式 {#creating-web-applications-thatrenders-forms}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

## 建立呈現Forms的Web應用程式 {#creating-web-applications-that-renders-forms}

您可以建立基於Web的應用程式，該應用程式使用Java Servlet調用Forms服務和呈現表單。 使用Java™ Servlet的一個優點是，您可以將進程的返回值寫入客戶端Web瀏覽器。 也就是說，Java Servlet可以用作返回表單的Forms服務與客戶端Web瀏覽器之間的連結。

>[!NOTE]
>
>本節介紹如何建立基於Web的應用程式，該應用程式使用調用Forms服務並基於片段呈現表單的Java Servlet。 (請參閱 [基於片段呈現Forms](/help/forms/developing/rendering-forms-based-fragments.md)。)

使用Java Servlet，您可以將表單寫入客戶端Web瀏覽器，以便客戶可以查看表單並將資料輸入到表單中。 在用資料填充表單後，Web用戶按一下表單上的提交按鈕，將資訊發回到Java Servlet，在該Java Servlet中可以檢索和處理資料。 例如，資料可以發送到另一個進程。

本節討論如何建立基於Web的應用程式，使用戶能夠選擇基於美國的表單資料或基於加拿大的表單資料，如下圖所示。

![cw_cw_fragmentwebclient](assets/cw_cw_fragmentwebclient.png)

呈現的表單是基於片段的表單。 即，如果用戶選擇美國資料，則返回的表單使用基於美國資料的片段。 例如，表單的頁腳包含美國地址，如下圖所示。

![cw_cw_fragefooter](assets/cw_cw_fragementformfooter.png)

同樣，如果用戶選擇加拿大資料，則返回的表單包含加拿大地址，如下圖所示。

![cw_cw_fragementformfootcnd](assets/cw_cw_fragementformfootercnd.png)

>[!NOTE]
>
>有關基於片段建立表單設計的資訊，請參見 [Forms設計師](https://www.adobe.com/go/learn_aemforms_designer_63_tw)。

**示例檔案**

本節使用可位於以下位置的示例檔案：

&lt;*Forms設計器安裝目錄*>/樣品/Forms/採購訂單/表單碎片

&lt;*安裝目錄*>是安裝路徑。 為客戶端應用程式的目的，已從此安裝位置複製Purchase Order Dynamic.xdp檔案，並將其部署到名為「DeS」的Forms應用程式 *應用程式/表單應用程式*。 Purchase Order Dynamic.xdp檔案放置在名為FormsFolder的資料夾中。 同樣，這些片段被放在名為Fragments的資料夾中，如下圖所示。

![cw_cw_fragments儲存庫](assets/cw_cw_fragmentsrepository.png)

要訪問Oracle Purchase Order Dynamic.xdp表單設計，請指定 `Applications/FormsApplication/1.0/FormsFolder/Purchase Order Dynamic.xdp` 表單名稱(傳遞給 `renderPDFForm` 方法)和 `repository:///` 作為內容根URI值。

Web應用程式使用的XML資料檔案已從「資料」資料夾移到 `C:\Adobe`(屬於承載AEM Forms的J2EE應用程式伺服器的檔案系統)。 檔案名為採購訂單 *加拿大.xml* 和採購訂單 *US.xml*。

>[!NOTE]
>
>有關使用Workbench建立Forms應用程式的資訊，請參閱 [工作台幫助](https://www.adobe.com/go/learn_aemforms_workbench_63)。

### 步驟摘要 {#summary-of-steps}

要建立基於Web的應用程式，以基於片段呈現表單，請執行以下步驟：

1. 建立新Web項目。
1. 建立表示Java Servlet的Java應用程式邏輯。
1. 為Web應用程式建立網頁。
1. 將Web應用程式打包到WAR檔案。
1. 將WAR檔案部署到J2EE應用程式伺服器。
1. TestWeb應用程式。

>[!NOTE]
>
>其中一些步驟取決於部署了AEM Forms的J2EE應用程式。 例如，您用於部署WAR檔案的方法取決於您所使用的J2EE應用程式伺服器。 本節假定AEM Forms部署在JBoss®上。

### 建立Web項目 {#creating-a-web-project}

建立包含可調用Forms服務的Java Servlet的Web應用程式的第一步是建立新的Web項目。 本文檔所基於的Java IDE是Eclipse 3.3。使用Eclipse IDE，建立Web項目，並將所需的JAR檔案添加到項目中。 最後，添加名為的HTML頁 *索引.html* 和Java Servlet。

以下清單指定必須添加到Web項目的JAR檔案：

* adobe-forms-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar

有關這些JAR檔案的位置，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**要建立Web項目：**

1. 啟動Eclipse並按一下 **檔案** >  **新建項目**。
1. 在 **新建項目** 對話框，選擇 **Web** > **動態Web項目**。
1. 類型 `FragmentsWebApplication` ，然後按一下 **完成**。

**要將所需的JAR檔案添加到項目中，請執行以下操作：**

1. 在「項目瀏覽器」窗口中，按一下右鍵 `FragmentsWebApplication` 項目和選擇 **屬性**。
1. 按一下 **Java生成路徑** 然後按一下 **庫** 頁籤。
1. 按一下 **添加外部JAR** 按鈕並瀏覽到要包括的JAR檔案。

**要將Java Servlet添加到項目中：**

1. 在「項目瀏覽器」窗口中，按一下右鍵 `FragmentsWebApplication` 項目和選擇 **新建** >  **其他**。
1. 展開 **Web** 資料夾，選擇 **Servlet**，然後按一下 **下一個**。
1. 在「建立Servlet」對話框中，鍵入 `RenderFormFragment` ，然後按一下 **完成**。

**向項目添加HTML頁：**

1. 在「項目瀏覽器」窗口中，按一下右鍵 `FragmentsWebApplication` 項目和選擇 **新建** > **其他**。
1. 展開 **Web** 資料夾，選擇 **HTML**，然後按一下 **下一個**。
1. 在「新建HTML」對話框中，鍵入 `index.html` ，然後按一下 **完成**。

>[!NOTE]
>
>有關建立調用HTML頁的資訊 `RenderFormFragment` Java Servlet，請參見 [建立網頁](/help/forms/developing/rendering-forms.md#creating-the-web-page)。

### 為servlet建立Java應用程式邏輯 {#creating-java-application-logic-for-the-servlet}

您可以從Java Servlet內建立調用Forms服務的Java應用程式邏輯。 以下代碼顯示 `RenderFormFragment` Java Servlet:

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

通常，不會將客戶端代碼放在Java Servlet中 `doGet` 或 `doPost` 的雙曲餘切值。 更好的寫程式方法是將此代碼放在單獨的類中，從中實例化類 `doPost` 方法 `doGet` 方法)，並調用相應的方法。 但是，對於代碼簡化，本節中的代碼示例將保持為最小值，代碼示例將放在 `doPost` 的雙曲餘切值。

要使用Forms服務API基於片段呈現表單，請執行以下任務：

1. 在Java項目的類路徑中包括客戶端JAR檔案，如adobe-forms-client.jar。 有關這些檔案位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。
1. 檢索從HTML表單提交的單選按鈕的值，並指定是使用美國資料還是加拿大資料。 如果提交American，請建立 `com.adobe.idp.Document` 儲存位於 *採購訂單US.xml*。 同樣，如果是加拿大人，則建立 `com.adobe.idp.Document` 儲存位於 *採購訂單Canada.xml* 的子菜單。
1. 建立 `ServiceClientFactory` 包含連接屬性的對象。 (請參閱 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)
1. 建立 `FormsServiceClient` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。
1. 建立 `URLSpec` 使用其建構子儲存URI值的對象。
1. 調用 `URLSpec` 對象 `setApplicationWebRoot` 方法，並傳遞一個表示應用程式web根的字串值。
1. 調用 `URLSpec` 對象 `setContentRootURI` 方法並傳遞一個字串值，該字串值指定內容根URI值。 確保表單設計和片段位於內容根URI中。 否則，Forms服務會引發異常。 要引用AEM Forms儲存庫，請指定 `repository://`。
1. 調用 `URLSpec` 對象 `setTargetURL` 方法並傳遞一個字串值，該字串值指定將表單資料發佈到的目標URL值。 如果在表單設計中定義目標URL，則可以傳遞空字串。 您還可以指定表單發送到的URL以執行計算。
1. 調用 `FormsServiceClient` 對象 `renderPDFForm` 方法並傳遞以下值：

   * 一個字串值，它指定表單設計名稱，包括檔案副檔名。
   * A `com.adobe.idp.Document` 包含要與窗體合併的資料的對象（在步驟2中建立）。
   * A `PDFFormRenderSpec` 儲存運行時選項的對象。 有關詳細資訊，請參見 [AEM FormsAPI參考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * A `URLSpec` 包含Forms服務基於片段呈現表單所需的URI值的對象。
   * A `java.util.HashMap` 儲存檔案附件的對象。 這是可選參數，您可以指定 `null` 的子菜單。

   的 `renderPDFForm` 方法返回 `FormsResult` 包含必須寫入客戶端web瀏覽器的表單資料流的對象。

1. 建立 `com.adobe.idp.Document` 通過調用 `FormsResult` 對象s `getOutputContent` 的雙曲餘切值。
1. 獲取的內容類型 `com.adobe.idp.Document` 通過調用對象 `getContentType` 的雙曲餘切值。
1. 設定 `javax.servlet.http.HttpServletResponse` 通過調用對象的內容類型 `setContentType` 方法和傳遞 `com.adobe.idp.Document` 的雙曲餘切值。
1. 建立 `javax.servlet.ServletOutputStream` 用於通過調用 `javax.servlet.http.HttpServletResponse` 對象 `getOutputStream` 的雙曲餘切值。
1. 建立 `java.io.InputStream` 通過調用 `com.adobe.idp.Document` 對象 `getInputStream` 的雙曲餘切值。
1. 通過調用 `InputStream` 對象 `read`方法，並將位元組陣列作為參數傳遞。
1. 調用 `javax.servlet.ServletOutputStream` 對象 `write` 一種將表單資料流發送到客戶端web瀏覽器的方法。 將位元組陣列傳遞到 `write` 的雙曲餘切值。

以下代碼示例表示調用Forms服務並基於片段呈現表單的Java Servlet。

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

### 建立網頁 {#creating-the-web-page}

index.html網頁提供Java servlet的入口點並調用Forms服務。 此網頁是一個基本HTML表單，包含兩個單選按鈕和一個提交按鈕。 單選按鈕的名稱是單選按鈕。 當用戶按一下提交按鈕時，表單資料將發佈到 `RenderFormFragment` Java Servlet。

Java servlet使用以下Java代碼捕獲從HTML頁發佈的資料：

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

以下HTML代碼位於在設定開發環境期間建立的index.html檔案中。 (請參閱 [建立Web項目](/help/forms/developing/rendering-forms.md#creating-a-web-project)。)

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

### 打包Web應用程式 {#packaging-the-web-application}

要部署調用Forms服務的Java Servlet，請將Web應用程式打包到WAR檔案。 確保元件的業務邏輯所依賴的外部JAR檔案（如adobe-liveccycle-client.jar和adobe-forms-client.jar）也包含在WAR檔案中。

**要將Web應用程式打包到WAR檔案：**

1. 從 **項目瀏覽器** 窗口，按一下右鍵 `FragmentsWebApplication` 項目和選擇 **導出** > **WAR檔案**。
1. 在 **Web模組** 文本框，類型 `FragmentsWebApplication` 的子菜單。
1. 在 **目標** 文本框，類型 `FragmentsWebApplication.war`**為**&#x200B;檔案名，指定WAR檔案的位置，然後按一下「完成」。

### 將WAR檔案部署到J2EE應用程式伺服器 {#deploying-the-war-file-to-the-j2ee-application-server}

您可以將WAR檔案部署到部署了AEM Forms的J2EE應用程式伺服器。 部署WAR檔案後，您可以使用Web瀏覽器訪問HTML網頁。

**要將WAR檔案部署到J2EE應用程式伺服器，請執行以下操作：**

* 將WAR檔案從導出路徑複製到 `[Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\all\deploy`。

### 測試Web應用程式 {#testing-your-web-application}

部署Web應用程式後，可以使用Web瀏覽器test它。 假定您使用的是承載AEM Forms的同一台電腦，則可以指定以下URL:

* http://localhost:8080/FragmentsWebApplication/index.html

   選擇一個單選按鈕，然後按一下「提交」按鈕。 基於片段的表單將出現在Web瀏覽器中。 如果出現問題，請參閱J2EE應用程式伺服器的日誌檔案。
