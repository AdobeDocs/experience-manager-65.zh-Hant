---
title: 使用批次API產生多種互動式通訊
description: 使用批次API產生多種互動式通訊
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communication
feature: Interactive Communication
exl-id: f65d8eb9-4d2c-4a6e-825f-45bcfaa7ca75
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '2234'
ht-degree: 1%

---

# 使用批次API產生多種互動式通訊 {#use-batch-api-to-generate-multiple-ic}

您可以使用批次API從範本產生多個互動式通訊。 範本是互動式通訊，不含任何資料。 批次API將資料與範本結合，以產生互動式通訊。 API在大量生產互動式通訊中很有用。 例如，電話單、多個客戶的信用卡對帳單。

批次API接受JSON格式和表單資料模型中的記錄（資料）。 產生的互動式通訊數量等於設定的「表單資料模型」中輸入JSON檔案中指定的記錄。 您可以使用API來產生「列印」和「網頁」輸出。 「打印」選項將生成PDF文檔，而「WEB」選項將生成每個單獨記錄的JSON格式資料。

## 使用批次API {#using-the-batch-api}

您可以將批次API與「監看資料夾」搭配使用，或作為獨立Rest API。 您可以配置模板、輸出類型(HTML、打印或兩者)、區域設定、預填服務，以及生成的互動式通信的名稱，以便使用批處理API。

您將記錄與互動式通訊範本結合，以產生互動式通訊。 批次API可直接從JSON檔案或透過表單資料模型存取的外部資料來源讀取記錄（互動式通訊範本的資料）。 您可以將每個記錄保留在個別的JSON檔案中，或建立JSON陣列，將所有記錄保留在單一檔案中。

**JSON檔案中的單一記錄**

```json
{
   "employee": {
       "name": "Sara",
       "id": 3,
       "mobileNo": 9871996463,
       "age": 37
   }
}
```

**JSON檔案中有多筆記錄**

```json
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

### 搭配監看資料夾使用批次API {#using-the-batch-api-watched-folders}

為了方便您體驗API,AEM Forms提供設定為立即使用批次API的Watched資料夾服務。 您可以透過AEM Forms UI存取服務，以產生多個互動式通訊。 您也可以根據需求建立自訂服務。 您可以使用下列方法，將批次API與「已觀看」資料夾搭配使用：

* 以JSON檔案格式指定輸入資料（記錄），以產生互動式通訊
* 使用儲存在外部資料源中並通過表單資料模型訪問的輸入資料（記錄）來產生互動式通信

#### 指定JSON檔案格式的輸入資料記錄，以產生互動式通訊 {#specify-input-data-in-JSON-file-format}

您將記錄與互動式通訊範本結合，以產生互動式通訊。 您可以為每個記錄建立個別的JSON檔案，或建立JSON陣列，將所有記錄保留在單一檔案中：

若要從JSON檔案中儲存的記錄建立互動式通訊：

1. 建立 [監看資料夾](https://docs.adobe.com/content/help/en/experience-manager-64/forms/publish-process-aem-forms/creating-configure-watched-folder.html) 並加以設定以使用批次API:
   1. 登入AEM Forms製作例項。
   1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 配置監視資料夾]**. 點選 **[!UICONTROL 新增]**.
   1. 指定 **[!UICONTROL 名稱]** 物理 **[!UICONTROL 路徑]** 的下限。 例如， `c:\batchprocessing`.
   1. 選取 **[!UICONTROL 服務]** 選項 **[!UICONTROL 處理檔案使用]** 欄位。
   1. 選取 **[!UICONTROL com.adobe.fd.ccm.m多頻道.batch.impl.service.InteractiveCommunicationBatchServiceImpl]** 服務 **[!UICONTROL 服務名稱]** 欄位。
   1. 指定 **[!UICONTROL 輸出檔案模式]**. 例如，%F/ [圖樣](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns) 指定「監看資料夾」可在「監看資料夾」的子資料夾\input資料夾中找到輸入檔案。
1. 設定進階參數：
   1. 開啟 **[!UICONTROL 進階]** 標籤，然後新增下列自訂屬性：

      | 屬性 | 類型 | 說明 |
      |--- |--- |--- |
      | templatePath | 字串 | 指定要使用的互動式通訊範本的路徑。 例如/content/dam/formsanddocuments/testsample/mediamic。 這是強制屬性。 |
      | recordPath | 字串 | recordPath欄位的值有助於設定互動式通訊的名稱。 您可以將記錄欄位的路徑設定為recordPath欄位的值。 例如，如果指定/employee/Id,id欄位的值就會變成對應互動式通訊的名稱。 預設值為隨機 [隨機UUID](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID()). |
      | usePrefillService | 布林值 | 將值設為False。 您可以使用usePrefillService參數，使用從針對對應互動式通訊設定的預填服務擷取的資料來預填互動式通訊。 將usePrefillService設為true時，輸入的JSON資料（對於每個記錄）會被視為FDM引數。 預設值為false。 |
      | batchType | 字串 | 將值設定為PRINT、WEB或WEB_AND_PRINT。 預設值為WEB_AND_PRINT。 |
      | 地區設定 | 字串 | 指定輸出互動式通訊的地區。 現成服務不使用地區設定選項，但您可以建立自訂服務來產生本地化的互動式通訊。 預設值為en_US |

   1. 點選 **[!UICONTROL 建立]** 已建立監看資料夾。
1. 使用觀看的資料夾來產生互動式通訊：
   1. 開啟「已觀看」資料夾。 導覽至輸入資料夾。
   1. 在輸入資料夾中建立資料夾，並將JSON檔案置於新建立的資料夾中。
   1. 等待「監看資料夾」處理檔案。 處理開始時，包含檔案的輸入檔案和子資料夾會移至中繼資料夾。
   1. 開啟輸出資料夾以檢視輸出：
      * 當您在「觀看的資料夾設定」中指定「列印」選項時，會產生互動式通訊的PDF輸出。
      * 當您在「監看資料夾設定」中指定WEB選項時，系統會根據每個記錄產生JSON檔案。 您可以使用JSON檔案 [預填網頁範本](#web-template).
      * 當您同時指定「列印」和「網頁」選項時，系統會產生PDF檔案和每個記錄的JSON檔案。

#### 使用儲存在外部資料源中、通過表單資料模型訪問的輸入資料來產生互動式通信 {#use-fdm-as-data-source}

將保存在外部資料源中的資料（記錄）與交互通信模板組合，以生成交互通信。 建立互動式通訊時，可透過表單資料模型(FDM)將其連線至外部資料來源，以存取資料。 您可以設定「監看資料夾」批次處理服務，以使用相同的表單資料模型從外部資料來源擷取資料。 結束日期 [從儲存在外部資料來源中的記錄建立互動式通訊](https://docs.adobe.com/content/help/en/experience-manager-64/forms/form-data-model/work-with-form-data-model.html):

1. 設定範本的表單資料模型：
   1. 開啟與互動式通訊範本相關聯的「表單資料模型」。
   1. 選擇頂級模型對象，然後點選「編輯屬性」(Edit Properties)。
   1. 從「編輯屬性」窗格下的「讀取服務」欄位中選擇獲取或獲取服務。
   1. 點選讀取服務引數的鉛筆圖示，將引數系結至「請求屬性」並指定系結值。 它將服務參數綁定到指定的綁定屬性或常值，該值作為參數傳遞給服務，以從資料源獲取與指定值關聯的詳細資訊。

      <br>
        在此範例中，id引數會採用使用者設定檔之id屬性的值，並將其作為引數傳給讀取服務。 它會從員工資料模型物件中讀取並傳回指定ID的相關屬性值。 因此，如果您在表單的id欄位中指定00250，則讀取服務將讀取具有00250員工id的員工的詳細資訊。
        <br>

      ![設定請求屬性](assets/request-attribute.png)

   1. 儲存屬性和表單資料模型。
1. 設定請求屬性的值：
   1. 在檔案系統上建立.json檔案，並開啟它進行編輯。
   1. 建立JSON陣列，並指定從「表單資料模型」擷取資料的主要屬性。 例如，下列JSON要求FDM傳送ID為27126或27127的記錄資料：

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

1. 建立 [監看資料夾](https://docs.adobe.com/content/help/en/experience-manager-64/forms/publish-process-aem-forms/creating-configure-watched-folder.html) 並加以設定，以使用批次API服務：
   1. 登入AEM Forms製作例項。
   1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 配置監視資料夾]**. 點選 **[!UICONTROL 新增]**.
   1. 指定 **[!UICONTROL 名稱]** 物理 **[!UICONTROL 路徑]** 的下限。 例如， `c:\batchprocessing`.
   1. 選取 **[!UICONTROL 服務]** 選項 **[!UICONTROL 處理檔案使用]** 欄位。
   1. 選取 **[!UICONTROL com.adobe.fd.ccm.m多頻道.batch.impl.service.InteractiveCommunicationBatchServiceImpl]** 服務 **[!UICONTROL 服務名稱]** 欄位。
   1. 指定 **[!UICONTROL 輸出檔案模式]**. 例如，%F/ [圖樣](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns) 指定「監看資料夾」可在「監看資料夾」的子資料夾\input資料夾中找到輸入檔案。
1. 設定進階參數：
   1. 開啟 **[!UICONTROL 進階]** 標籤，然後新增下列自訂屬性：

      | 屬性 | 類型 | 說明 |
      |--- |--- |--- |
      | templatePath | 字串 | 指定要使用的互動式通訊範本的路徑。 例如/content/dam/formsanddocuments/testsample/mediamic。 這是強制屬性。 |
      | recordPath | 字串 | recordPath欄位的值有助於設定互動式通訊的名稱。 您可以將記錄欄位的路徑設定為recordPath欄位的值。 例如，如果指定/employee/Id,id欄位的值就會變成對應互動式通訊的名稱。 預設值為隨機 [隨機UUID](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID()). |  |
      | usePrefillService | 布林值 | 將值設為True。 預設值為false。  當值設為true時，批次API會從設定的表單資料模型讀取資料，並填入互動式通訊。 將usePrefillService設為true時，輸入的JSON資料（對於每個記錄）會被視為FDM引數。 |
      | batchType | 字串 | 將值設定為PRINT、WEB或WEB_AND_PRINT。 預設值為WEB_AND_PRINT。 |
      | 地區設定 | 字串 | 指定輸出互動式通訊的地區。 現成服務不使用地區設定選項，但您可以建立自訂服務來產生本地化的互動式通訊。 預設值為en_US。 |

   1. 點選 **[!UICONTROL 建立]** 已建立監看資料夾。
1. 使用觀看的資料夾來產生互動式通訊：
   1. 開啟「已觀看」資料夾。 導覽至輸入資料夾。
   1. 在輸入資料夾中建立資料夾。 將在步驟2中建立的JSON檔案放置在新建立的資料夾中。
   1. 等待「監看資料夾」處理檔案。 處理開始時，包含檔案的輸入檔案和子資料夾會移至中繼資料夾。
   1. 開啟輸出資料夾以檢視輸出：
      * 當您在「觀看的資料夾設定」中指定「列印」選項時，會產生互動式通訊的PDF輸出。
      * 當您在「監看資料夾設定」中指定WEB選項時，系統會根據每個記錄產生JSON檔案。 您可以使用JSON檔案 [預填網頁範本](#web-template).
      * 當您同時指定「列印」和「網頁」選項時，系統會產生PDF檔案和每個記錄的JSON檔案。

## 使用REST請求叫用批次API

您可以叫用 [批次API](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/index.html) 通過代表性狀態轉移(REST)請求。 它可讓您向其他使用者提供REST端點，以存取API並設定您自己的處理、儲存和自訂互動式通訊的方法。 您可以開發自己的自訂Java servlet，以在AEM例項上部署API。

部署Java servlet之前，請確定您具備互動式通訊，且對應的資料檔案已就緒。 執行下列步驟以建立和部署Java servlet:

1. 登入您的AEM例項並建立互動式通訊。 若要使用下列范常式式碼中提及的互動式通訊， [按一下這裡](assets/SimpleMediumIC.zip).
1. [使用Apache Maven建立和部署AEM專案](https://helpx.adobe.com/experience-manager/using/maven_arch13.html) 在AEM例項上。
1. 新增 [AEM Forms用戶端SDK版本6.0.12](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 或更新版本，位於AEM專案的POM檔案的相依性清單中。 例如，

   ```xml
       <dependency>
           <groupId>com.adobe.aemfd</groupId>
           <artifactId>aemfd-client-sdk</artifactId>
           <version>6.0.122</version>
       </dependency>
   ```

1. 開啟Java專案，建立.java檔案，例如CCMBatchServlet.java。 將下列程式碼新增至檔案中：

   ```java
           package com.adobe.fd.ccm.multichannel.batch.integration;
   
           import java.io.File;
           import java.io.FileInputStream;
           import java.io.FileOutputStream;
           import java.io.IOException;
           import java.io.InputStream;
           import java.io.PrintWriter;
           import java.util.List;
           import javax.servlet.Servlet;
           import org.apache.commons.io.IOUtils;
           import org.apache.sling.api.SlingHttpServletRequest;
           import org.apache.sling.api.SlingHttpServletResponse;
           import org.apache.sling.api.servlets.SlingAllMethodsServlet;
           import org.json.JSONArray;
           import org.json.JSONObject;
           import org.osgi.service.component.annotations.Component;
           import org.osgi.service.component.annotations.Reference;
   
           import com.adobe.fd.ccm.multichannel.batch.api.builder.BatchConfigBuilder;
           import com.adobe.fd.ccm.multichannel.batch.api.factory.BatchComponentBuilderFactory;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchConfig;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchInput;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchResult;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchType;
           import com.adobe.fd.ccm.multichannel.batch.api.model.RecordResult;
           import com.adobe.fd.ccm.multichannel.batch.api.model.RenditionResult;
           import com.adobe.fd.ccm.multichannel.batch.api.service.BatchGeneratorService;
           import com.adobe.fd.ccm.multichannel.batch.util.BatchConstants;
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
   * 當為交互通信指定PRINT選項PDF輸出時，將生成該輸出。
   * 當您指定WEB選項時，系統會根據每個記錄產生JSON檔案。 您可以使用JSON檔案 [預填網頁範本](#web-template).
   * 當您同時指定「列印」和「網頁」選項時，系統會產生PDF檔案和每個記錄的JSON檔案。

1. [使用maven將更新的程式碼部署至您的AEM執行個體](https://helpx.adobe.com/experience-manager/using/maven_arch13.html#BuildtheOSGibundleusingMaven).
1. 叫用批次API以產生互動式通訊。 批次API會根據記錄數，列印傳回PDF和.json檔案資料流。 您可以使用JSON檔案 [預填網頁範本](#web-template). 如果您使用上述程式碼，API會部署在 `http://localhost:4502/bin/batchServlet`. 程式碼會列印並傳回PDF和JSON檔案的資料流。

### 預填網頁範本 {#web-template}

當您設定batchType來轉譯Web管道時，API會為每個資料記錄產生JSON檔案。 您可以使用下列語法來合併JSON檔案與對應的Web頻道，以產生互動式通訊：

**語法**
`http://host:port/<template-path>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=<guide-merged-json-path>`

**範例**
如果您的JSON檔案位於 `C:\batch\mergedJsonPath.json` 並使用以下互動式通信模板： `http://host:port/content/dam/formsanddocuments/testsample/mediumic/jcr:content?channel=web`

接著，發佈節點上的下列URL會顯示互動式通訊的Web通道
`http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/batch/mergedJsonData.json`

除了在檔案系統上儲存資料外，您還可以將JSON檔案儲存在CRX-repository、檔案系統、Web伺服器中，或透過OSGI預填服務存取資料。 使用各種通訊協定來合併資料的語法為：

* **CRX通訊協定**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=crx:///tmp/fd/af/mergedJsonData.json`

* **檔案通訊協定**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/Users/af/mergedJsonData.json`

* **預填服務協定**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=service://[SERVICE_NAME]/[IDENTIFIER]`

   SERVICE_NAME表示OSGI預填服務的名稱。 請參閱建立並執行預填服務。

   IDENTIFIER是指OSGI預填服務擷取預填資料所需的任何中繼資料。 登入使用者的識別碼是可使用的中繼資料範例。

* **HTTP通訊協定**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=http://localhost:8000/somesamplexmlfile.xml`

>[!NOTE]
>
>預設僅啟用CRX通訊協定。 若要啟用其他支援的通訊協定，請參閱 [使用Configuration Manager配置預填服務](https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#ConfiguringprefillserviceusingConfigurationManager).
