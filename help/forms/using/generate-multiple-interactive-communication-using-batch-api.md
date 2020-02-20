---
title: 使用Batch API產生多種互動式通訊
description: 使用Batch API產生多種互動式通訊
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communication
translation-type: tm+mt
source-git-commit: 1b664d082f090814903b2802d8accd80eb6b9e5e

---


# 使用Batch API產生多種互動式通訊 {#use-batch-api-to-generate-multiple-ic}

您可以使用Batch API，從範本產生多種互動式通訊。 範本是互動式通訊，不含任何資料。 批次API將資料與範本結合，以產生互動式通訊。 API在大量製作互動式通訊時很實用。 例如，電話帳單、多名客戶的信用卡帳單。

批次API接受JSON格式和表單資料模型中的記錄（資料）。 產生的互動式通訊次數等於設定表單資料模型中輸入JSON檔案中所指定的記錄。 您可以使用API來產生列印和網頁輸出。 PRINT選項會產生PDF檔案，而WEB選項則會針對每個個別記錄產生JSON格式的資料。

## 使用批次API {#using-the-batch-api}

您可以搭配使用「批次API」和「監看的檔案夾」，或當做獨立的「余料API」。 您可以設定範本、輸出類型（HTML、PRINT或Both）、地區設定、預填服務，以及所產生互動式通訊的名稱，以使用「批次API」。

您可將記錄與互動式通訊範本結合，以產生互動式通訊。 批次API可直接從JSON檔案或透過表單資料模型存取的外部資料來源讀取記錄（互動式通訊範本的資料）。 您可以將每個記錄保留在個別的JSON檔案中，或建立JSON陣列，將所有記錄保留在單一檔案中。

**JSON檔案中的單一記錄**

```JSON
{
   "employee": {
       "name": "Sara",
       "id": 3,
       "mobileNo": 9871996463,
       "age": 37
   }
}
```

**JSON檔案中的多個記錄**

```JSON
[{
   "employee": {
       "name": "John",
       "id": 1,
       "mobileNo": 9871996461,
       "age": 39
   }
},{
   "employee": {
       "name": "Jacob",
       "id": 2,
       "mobileNo": 9871996462,
       "age": 38
   }
},{
   "employee": {
       "name": "Sara",
       "id": 3,
       "mobileNo": 9871996463,
       "age": 37
   }
}]
```

### 搭配使用批次API與Watched資料夾 {#using-the-batch-api-watched-folders}

為了讓您輕鬆體驗API,AEM Forms提供「Watched Folder」服務，設定為立即可用的「批次API」。 您可以透過AEM Forms UI存取服務，以產生多種互動式通訊。 您也可以根據需求建立自訂服務。 您可以使用下列方法，將Batch API與Watched資料夾搭配使用：

* 指定JSON檔案格式的輸入資料（記錄），以產生互動式通訊
* 使用儲存於外部資料來源並透過表單資料模型存取的輸入資料（記錄）來產生互動式通訊

#### 指定JSON檔案格式的輸入資料記錄，以產生互動式通訊 {#specify-input-data-in-JSON-file-format}

您可將記錄與互動式通訊範本結合，以產生互動式通訊。 您可以為每個記錄建立個別的JSON檔案，或建立JSON陣列，將所有記錄保存在單一檔案中：

若要從儲存在JSON檔案中的記錄建立互動式通訊：

1. 建立「 [Watched」資料夾](https://docs.adobe.com/content/help/en/experience-manager-64/forms/publish-process-aem-forms/creating-configure-watched-folder.html) ，並設定它以使用「批次API」:
   1. 登入AEM Forms作者例項。
   1. 導覽至「 **[!UICONTROL 工具]** >表單 **[!UICONTROL >設]** 定監看資料夾 ****」。 點選 **[!UICONTROL 新]**。
   1. 指定 **[!UICONTROL 資料夾]** 的名 **[!UICONTROL 稱和]** 物理路徑。 例如， `c:\batchprocessing`。
   1. 在「使用 **[!UICONTROL 流程檔案]** 」欄位中 **[!UICONTROL 選擇「服務]** 」選項。
   1. 在「服 **[!UICONTROL 務名稱」欄位中選取com.adobe.fd.ccm.multichannel.batch.impl.service.InteractiveCommunicationBatchServiceImpl]****[!UICONTROL 服務]** 。
   1. 指定「輸 **[!UICONTROL 出檔案模式」]**。 例如，%F/模 [式指定](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns) 「監視資料夾」可在「監視資料夾」\input資料夾的子資料夾中查找輸入檔案。
1. 設定進階參數：
   1. 開啟「進 **[!UICONTROL 階]** 」索引標籤並新增下列自訂屬性：

      | 屬性 | 類型 | 說明 |
      |--- |--- |--- |
      | templatePath | 字串 | 指定要使用的互動式通訊範本的路徑。 例如，/content/dam/formsanddocuments/testsample/mediamic。 這是強制屬性。 |
      | recordPath | 字串 | recordPath欄位的值有助於設定互動式通信的名稱。 您可以將記錄欄位的路徑設定為recordPath欄位的值。 例如，如果您指定/employee/Id,id欄位的值就會變成對應互動式通訊的名稱。 預設值為隨機隨 [機UUID](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID())。 |
      | usePrefillService | 布林值 (Boolean) | 將值設為False。 您可以使用usePrefillService參數，以預先填入從預先填入服務擷取的資料來預先填入互動式通訊，並設定對應的互動式通訊。 當usePrefillService設為true時，輸入的JSON資料（針對每個記錄）會被視為FDM引數。 預設值為false。 |
      | batchType | 字串 | 將值設定為PRINT、WEB或WEB_AND_PRINT。 預設值為WEB_AND_PRINT。 |
      | 地區設定 | 字串 | 指定輸出互動式通訊的地區。 現成可用的服務不使用地區設定選項，但您可以建立自訂服務，以產生本地化的互動式通訊。 預設值為en_US |

   1. 點選「 **[!UICONTROL 建立]** 」即會建立監看的資料夾。
1. 使用監看資料夾產生互動式通訊：
   1. 開啟「Watched」資料夾。 導覽至輸入資料夾。
   1. 在輸入檔案夾中建立檔案夾，並將JSON檔案置於新建立的檔案夾中。
   1. 等待「監視資料夾」處理檔案。 當處理開始時，包含檔案的輸入檔案和子檔案夾會移至預備檔案夾。
   1. 開啟輸出資料夾以查看輸出：
      * 當您在「Watched Folder Configuration」（監看資料夾設定）中指定「PRINT」（列印）選項時，會產生互動式通訊的PDF輸出。
      * 當您在「Watched Folder Configuration」（監看資料夾設定）中指定WEB選項時，會產生每個記錄的JSON檔案。 您可以使用JSON檔案 [預先填寫網頁範本](#web-template)。
      * 當您同時指定「列印」和「網頁」選項時，會產生PDF檔案和每個記錄的JSON檔案。

#### 使用儲存於外部資料來源並透過表單資料模型存取的輸入資料，產生互動式通訊 {#use-fdm-as-data-source}

您可將儲存在外部資料來源中的資料（記錄）與互動式通訊範本結合，以產生互動式通訊。 建立互動式通信時，可通過表單資料模型(FDM)將其連接到外部資料源以訪問資料。 您可以設定「監視資料夾」批次處理服務，從外部資料來源使用相同的表單資料模型擷取資料。 要從 [外部資料源中保存的記錄建立互動式通信](https://docs.adobe.com/content/help/en/experience-manager-64/forms/form-data-model/work-with-form-data-model.html):

1. 設定範本的表單資料模型：
   1. 開啟與互動式通訊範本關聯的表單資料模型。
   1. 選取頂層模型物件，並點選「編輯屬性」。
   1. 從「編輯屬性」窗格下的「讀取服務」欄位選擇您的讀取或獲取服務。
   1. 點選讀取服務引數的鉛筆圖示，將引數系結至「請求屬性」並指定系結值。 它將服務引數綁定到指定的綁定屬性或常值，該值作為參數傳遞給服務，以從資料源中獲取與指定值相關聯的詳細資訊。

      <br>
        在此示例中，id引數採用用戶配置檔案的id屬性值，並將其作為參數傳遞給讀取服務。 它將從指定ID的員工資料模型對象讀取並返回相關屬性的值。 因此，如果您在表單的id欄位中指定00250，讀取服務會讀取擁有00250名員工id的員工詳細資訊。
        <br>

      ![設定請求屬性](assets/request-attribute.png)

   1. 儲存屬性和表單資料模型。
1. 設定請求屬性的值：
   1. 在您的檔案系統上建立。json檔案，並開啟它以進行編輯。
   1. 建立JSON陣列，並指定要從表單資料模型擷取資料的主要屬性。 例如，下列JSON要求FDM傳送ID為27126或27127的記錄資料：

      ```json
          [
              {
                  "id": 27126
              },
              {
                  "id": 27127
              }
          ]
      ```

   1. 儲存並關閉檔案。

1. 建立「 [Watched」資料夾](https://docs.adobe.com/content/help/en/experience-manager-64/forms/publish-process-aem-forms/creating-configure-watched-folder.html) ，並設定它以使用「Batch API」服務：
   1. 登入AEM Forms作者例項。
   1. 導覽至「 **[!UICONTROL 工具]** >表單 **[!UICONTROL >設]** 定監看資料夾 ****」。 點選 **[!UICONTROL 新]**。
   1. 指定 **[!UICONTROL 資料夾]** 的名 **[!UICONTROL 稱和]** 物理路徑。 例如， `c:\batchprocessing`。
   1. 在「使用 **[!UICONTROL 流程檔案]** 」欄位中 **[!UICONTROL 選擇「服務]** 」選項。
   1. 在「服 **[!UICONTROL 務名稱」欄位中選取com.adobe.fd.ccm.multichannel.batch.impl.service.InteractiveCommunicationBatchServiceImpl]****[!UICONTROL 服務]** 。
   1. 指定「輸 **[!UICONTROL 出檔案模式」]**。 例如，%F/模 [式指定](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns) 「監視資料夾」可在「監視資料夾」\input資料夾的子資料夾中查找輸入檔案。
1. 設定進階參數：
   1. 開啟「進 **[!UICONTROL 階]** 」索引標籤並新增下列自訂屬性：

      | 屬性 | 類型 | 說明 |
      |--- |--- |--- |
      | templatePath | 字串 | 指定要使用的互動式通訊範本的路徑。 例如，/content/dam/formsanddocuments/testsample/mediamic。 這是強制屬性。 |
      | recordPath | 字串 | recordPath欄位的值有助於設定互動式通信的名稱。 您可以將記錄欄位的路徑設定為recordPath欄位的值。 例如，如果您指定/employee/Id,id欄位的值就會變成對應互動式通訊的名稱。 預設值為隨機隨 [機UUID](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID())。 |  |
      | usePrefillService | 布林值 (Boolean) | 將值設為True。 預設值為false。  當值設為true時，批次API會從已設定的表單資料模型讀取資料，並將其填入互動式通訊。 當usePrefillService設為true時，輸入的JSON資料（針對每個記錄）會被視為FDM引數。 |
      | batchType | 字串 | 將值設定為PRINT、WEB或WEB_AND_PRINT。 預設值為WEB_AND_PRINT。 |
      | 地區設定 | 字串 | 指定輸出互動式通訊的地區。 現成可用的服務不使用地區設定選項，但您可以建立自訂服務，以產生本地化的互動式通訊。 預設值為en_US。 |

   1. 點選「 **[!UICONTROL 建立]** 」即會建立監看的資料夾。
1. 使用監看資料夾產生互動式通訊：
   1. 開啟「Watched」資料夾。 導覽至輸入資料夾。
   1. 在輸入資料夾中建立資料夾。 將在步驟2中建立的JSON檔案置入新建立的檔案夾。
   1. 等待「監視資料夾」處理檔案。 當處理開始時，包含檔案的輸入檔案和子檔案夾會移至預備檔案夾。
   1. 開啟輸出資料夾以查看輸出：
      * 當您在「Watched Folder Configuration」（監看資料夾設定）中指定「PRINT」（列印）選項時，會產生互動式通訊的PDF輸出。
      * 當您在「Watched Folder Configuration」（監看資料夾設定）中指定WEB選項時，會產生每個記錄的JSON檔案。 您可以使用JSON檔案 [預先填寫網頁範本](#web-template)。
      * 當您同時指定「列印」和「網頁」選項時，會產生PDF檔案和每個記錄的JSON檔案。

## 使用REST請求叫用批次API

您可以透 [過「代表性狀態轉移](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/index.html) (REST)」請求叫用批次API。 它可讓您提供REST端點給其他使用者以存取API，並設定您自己的處理、儲存和自訂互動式通訊方法。 您可以開發自己的自訂Java servlet，以在AEM例項上部署API。

在部署Java servlet之前，請確定您有互動式通訊，並有對應的資料檔案可供使用。 執行以下步驟以建立和部署Java servlet:

1. 登入您的AEM例項並建立互動式通訊。 若要使用下列范常式式碼中提及的互動式通訊，請按 [一下這裡](assets/SimpleMediumIC.zip)。
1. [在您的AEM例項上使用Apache Maven](https://helpx.adobe.com/experience-manager/using/maven_arch13.html) ，建立和部署AEM專案。
1. 將 [AEM Forms Client SDK 6.0.12版或更新版本](https://repo.adobe.com/nexus/content/repositories/public/com/adobe/aemfd/aemfd-client-sdk/) ，以及最新的 [](https://docs.adobe.com/content/help/en/experience-manager-65/release-notes/service-pack/sp-release-notes.html#uber-jar) AEM Uber Jar新增至AEM專案的POm檔案相依性清單中。 例如，

   ```XML
       <dependency>
           <groupId>com.adobe.aemfd</groupId>
           <artifactId>aemfd-client-sdk</artifactId>
           <version>6.0.122</version>
       </dependency>
       <dependency>
          <groupId>com.adobe.aem</groupId>
          <artifactId>uber-jar</artifactId>
          <version>6.5.0</version>
          <classifier>apis</classifier>
          <scope>provided</scope>
       </dependency>
   ```

1. 開啟Java專案，建立。java檔案，例如CCMBatchServlet.java。 將下列程式碼新增至檔案：

   ```java
           package com.adobe.fd.ccm.multichannel.batch.integration;
   
           import java.io.File;
           import java.io.FileInputStream;
           import java.io.FileOutputStream;
           import java.io.IOException;
           import java.io.InputStream;
           import java.io.OutputStream;
           import java.io.PrintWriter;
           import java.util.List;
           import java.util.logging.FileHandler;
           import java.util.logging.Logger;
           import java.util.logging.SimpleFormatter;
   
           import javax.servlet.Servlet;
           import javax.servlet.ServletContext;
   
           import com.adobe.aemfd.watchfolder.service.api.ContentProcessor;
   
           import org.apache.commons.io.IOUtils;
           import org.apache.sling.api.SlingHttpServletRequest;
           import org.apache.sling.api.SlingHttpServletResponse;
           import org.apache.sling.api.servlets.SlingAllMethodsServlet;
           import org.json.JSONArray;
           import org.json.JSONObject;
           import org.osgi.service.component.annotations.Component;
           import org.osgi.service.component.annotations.Reference;
   
           import com.adobe.aemfd.docmanager.Document;
           import com.adobe.aemfd.docmanager.passivation.DocumentPassivationHandler;
           import com.adobe.fd.ccm.multichannel.batch.api.factory.BatchComponentBuilderFactory;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchConfig;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchInput;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchResult;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchType;
           import com.adobe.fd.ccm.multichannel.batch.api.model.RecordResult;
           import com.adobe.fd.ccm.multichannel.batch.api.model.RenditionResult;
           import com.adobe.fd.ccm.multichannel.batch.api.service.BatchGeneratorService;
           import com.adobe.fd.ccm.multichannel.batch.util.BatchConstants;
           import com.adobe.icc.render.obj.Content;
   
           import javax.annotation.PostConstruct;
           import javax.inject.Inject;
           import javax.inject.Named;
   
           import org.apache.sling.api.resource.Resource;
           import org.apache.sling.models.annotations.Default;
           import org.apache.sling.models.annotations.Model;
           import org.apache.sling.settings.SlingSettingsService;
           import org.apache.sling.api.resource.ResourceUtil;
   
   
           import org.slf4j.*;
           import java.util.Date;
   
           @Component(service=Servlet.class,
           property={
                   "sling.servlet.methods=GET",
                   "sling.servlet.paths="+ "/bin/batchServlet"
           })
           public class CCMBatchServlet extends SlingAllMethodsServlet {
   
               @Reference
               private BatchGeneratorService batchGeneratorService;
               @Reference
               private BatchComponentBuilderFactory batchBuilderFactory;
               public void doGet(SlingHttpServletRequest req, SlingHttpServletResponse resp) {
                   try {
                       executeBatch(req,resp);
                   } catch (Exception e) {
                       e.printStackTrace();
                   }
               }
               private void executeBatch(SlingHttpServletRequest req, SlingHttpServletResponse resp) throws Exception {
                   int count = 0;
                   JSONArray inputJSONArray = new JSONArray();
                   String filePath = req.getParameter("filePath");
                   InputStream is = new FileInputStream(filePath);
                   String data = IOUtils.toString(is);
                   try {
                       // If input file is json object, then create json object and add in json array, if not then try for json array
                       JSONObject inputJSON = new JSONObject(data);
                       inputJSONArray.put(inputJSON);
                   } catch (Exception e) {
                       try {
                           // If input file is json array, then iterate and add all objects into inputJsonArray otherwise throw exception
                           JSONArray inputArray = new JSONArray(data);
                           for(int i=0;i<inputArray.length();i++) {
                               inputJSONArray.put(inputArray.getJSONObject(i));
                           }
                       } catch (Exception ex) {
                           throw new Exception("Invalid JSON Data. File name : " + filePath, ex);
                       }
                   }
                   BatchInput batchInput = batchBuilderFactory.getBatchInputBuilder().setData(inputJSONArray).setTemplatePath("/content/dam/formsanddocuments/[path of the interactive communcation]").build();
                   BatchConfig batchConfig = batchBuilderFactory.getBatchConfigBuilder().setBatchType(BatchType.WEB_AND_PRINT).build();
                   BatchResult batchResult = batchGeneratorService.generateBatch(batchInput, batchConfig);
                   List<RecordResult> recordList = batchResult.getRecordResults();
                   JSONObject result = new JSONObject();
                   for (RecordResult recordResult : recordList) {
                       String recordId = recordResult.getRecordID();
                       for (RenditionResult renditionResult : recordResult.getRenditionResults()) {
                           if (renditionResult.isRecordPassed()) {
                               InputStream output = renditionResult.getDocumentStream().getInputStream();
                               result.put(recordId +"_"+renditionResult.getContentType(), output);
   
                               Date date= new Date();
                               long time = date.getTime();
   
                               // Print output
                               if(getFileExtension(renditionResult.getContentType()).equalsIgnoreCase(".json")) {
                                   File file = new File(time + getFileExtension(renditionResult.getContentType()));
                                   copyInputStreamToFile(output, file);
                               } else
                               {
                                   File file = new File(time + getFileExtension(renditionResult.getContentType()));
                                   copyInputStreamToFile(output, file);
                               }
                           }
                       }
                   }
                   PrintWriter writer = resp.getWriter();
                   JSONObject resultObj = new JSONObject();
                   resultObj.put("result", result);
                   writer.write(resultObj.toString());
               }
   
   
               private static void copyInputStreamToFile(InputStream inputStream, File file)
                       throws IOException {
   
                       try (FileOutputStream outputStream = new FileOutputStream(file)) {
   
                           int read;
                           byte[] bytes = new byte[1024];
   
                           while ((read = inputStream.read(bytes)) != -1) {
                               outputStream.write(bytes, 0, read);
                           }
   
                       }
   
                   }
   
   
               private String getFileExtension(String contentType) {
                   if (contentType.endsWith(BatchConstants.JSON)) {
                       return ".json";
                   } else return ".pdf";
               }
   
   
           }
   ```

1. 在上述程式碼中，將範本路徑(setTemplatePath)取代為範本的路徑，並設定setBatchType API的值：
   * 當您指定互動式通訊的PRINT選項時，就會產生PDF輸出。
   * 當您指定WEB選項時，會產生每個記錄的JSON檔案。 您可以使用JSON檔案 [預先填寫網頁範本](#web-template)。
   * 當您同時指定「列印」和「網頁」選項時，會產生PDF檔案和每個記錄的JSON檔案。

1. [使用maven將更新的程式碼部署至您的AEM例項](https://helpx.adobe.com/experience-manager/using/maven_arch13.html#BuildtheOSGibundleusingMaven)。
1. 叫用批次API以產生互動式通訊。 批次API會根據記錄數傳回PDF和。json檔案串流。 您可以使用JSON檔案 [預先填寫網頁範本](#web-template)。 如果您使用上述程式碼，API會部署於 `http://localhost:4502/bin/batchServlet`。 程式碼會列印並傳回PDF和JSON檔案的串流。

### 預先填寫網頁範本 {#web-template}

當您將batchType設定為轉譯網頁頻道時，API會為每個資料記錄產生JSON檔案。 您可以使用下列語法，將JSON檔案與對應的「網頁頻道」合併，以產生互動式通訊：

**語法**`http://host:port/<template-path>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=<guide-merged-json-path>`

**範例**&#x200B;如果您的JSON檔案位於，而您 `C:\batch\mergedJsonPath.json` 使用下列互動式通訊範本： `http://host:port/content/dam/formsanddocuments/testsample/mediumic/jcr:content?channel=web`

然後，發佈節點上的下列URL會顯示互動式通訊的Web頻道`http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/batch/mergedJsonData.json`

除了將資料儲存在檔案系統外，您還可將JSON檔案儲存在CRX-repository、檔案系統、Web伺服器，或可透過OSGI預填服務存取資料。 使用各種通訊協定來合併資料的語法為：

* **CRX協定**
   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=crx:///tmp/fd/af/mergedJsonData.json`

* **檔案協定**
   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/Users/af/mergedJsonData.json`

* **預填充服務協定**
   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=service://[SERVICE_NAME]/[IDENTIFIER]`

   SERVICE_NAME是指OSGI預填充服務的名稱。 請參閱「建立並執行預填服務」。

   識別碼是指OSGI預填服務擷取預填資料所需的任何中繼資料。 登入使用者的識別碼是可使用的中繼資料範例。

* **HTTP通訊協定**
   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=http://localhost:8000/somesamplexmlfile.xml`

>[!NOTE]
> 預設情況下，僅啟用CRX協定。 若要啟用其他支援的通訊協定，請參 [閱使用Configuration Manager設定預填服務](https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#ConfiguringprefillserviceusingConfigurationManager)。
