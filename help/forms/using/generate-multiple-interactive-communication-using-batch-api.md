---
title: 使用Batch API生成多個交互通信
description: 使用Batch API生成多個交互通信
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communication
feature: Interactive Communication
exl-id: f65d8eb9-4d2c-4a6e-825f-45bcfaa7ca75
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '2207'
ht-degree: 1%

---

# 使用Batch API生成多個交互通信 {#use-batch-api-to-generate-multiple-ic}

可以使用批處理API從模板生成多個交互通信。 該模板是沒有任何資料的互動式通信。 批處理API將資料與模板組合以生成互動式通信。 該API在互動式通信的批量生產中是有用的。 例如，電話帳單、多個客戶的信用卡對帳單。

批處理API接受JSON格式和表單資料模型中的記錄（資料）。 生成的互動式通信的數量等於配置的表單資料模型中輸入JSON檔案中指定的記錄。 可以使用API生成打印和Web輸出。 PRINT選項會生成PDF文檔，而WEB選項會為每個單獨記錄生成JSON格式的資料。

## 使用批處理API {#using-the-batch-api}

您可以將批處理API與「監視資料夾」結合使用，或作為獨立的Rest API。 您可以為生成的互動式通信配置模板、輸出類型(HTML、打印或兩者)、區域設定、預填充服務和名稱，以使用批處理API。

將記錄與互動式通信模板組合以生成互動式通信。 批處理API可以直接從JSON檔案或通過表單資料模型訪問的外部資料源讀取記錄（交互通信模板的資料）。 您可以將每個記錄保留在單獨的JSON檔案中，或建立JSON陣列以將所有記錄保留在單個檔案中。

**JSON檔案中的單個記錄**

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

**JSON檔案中的多個記錄**

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

### 將批處理API與受監視資料夾一起使用 {#using-the-batch-api-watched-folders}

為了方便地體驗API,AEM Forms提供了一個已配置為使用批處理API的監視資料夾服務。 您可以通過AEM FormsUI訪問服務，以生成多個交互通信。 您還可以根據自己的要求建立自定義服務。 您可以使用下面列出的方法將批處理API與「監視」資料夾一起使用：

* 指定JSON檔案格式的輸入資料（記錄）以生成互動式通信
* 使用保存在外部資料源中並通過表單資料模型訪問的輸入資料（記錄）來產生互動式通信

#### 指定JSON檔案格式的輸入資料記錄以生成互動式通信 {#specify-input-data-in-JSON-file-format}

將記錄與互動式通信模板組合以生成互動式通信。 您可以為每個記錄建立單獨的JSON檔案，或建立JSON陣列以將所有記錄保留在單個檔案中：

要從JSON檔案中保存的記錄建立互動式通信，請：

1. 建立 [監視資料夾](/help/forms/using/creating-configure-watched-folder.md) 並將其配置為使用Batch API:
   1. 登錄到AEM Forms作者實例。
   1. 導航到 **[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 配置監視資料夾]**。 點擊 **[!UICONTROL 新建]**。
   1. 指定 **[!UICONTROL 名稱]** 和物理 **[!UICONTROL 路徑]** 的子菜單。 比如說， `c:\batchprocessing`。
   1. 選擇 **[!UICONTROL 服務]** 的上界 **[!UICONTROL 進程檔案使用]** 的子菜單。
   1. 選擇 **[!UICONTROL com.adobe.fd.ccm.machnawer.batch.impl.service.InteractiveCommunicationBatchServiceImpl]** 服務 **[!UICONTROL 服務名稱]** 的子菜單。
   1. 指定 **[!UICONTROL 輸出檔案模式]**。 例如，%F/ [圖案](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns) 指定「監視資料夾」可以在「監視資料夾」\input資料夾的子資料夾中查找輸入檔案。
1. 配置高級參數：
   1. 開啟 **[!UICONTROL 高級]** 頁籤，然後添加以下自定義屬性：

      | 屬性 | 類型 | 說明 |
      |--- |--- |--- |
      | 模板路徑 | 字串 | 指定要使用的交互通信模板的路徑。 例如，/content/dam/formsanddocuments/testsample/mediumic。 這是強制屬性。 |
      | 記錄路徑 | 字串 | recordPath欄位的值有助於設定交互通信的名稱。 可以將記錄欄位的路徑設定為recordPath欄位的值。 例如，如果指定/employee/Id，則id欄位的值將成為相應交互通信的名稱。 預設值是隨機 [隨機UUID](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID())。 |
      | usePrefillService | 布林值 | 將值設定為False。 可以使用usePrefillService參數預填充互動式通信，該參數使用從為相應交互通信配置的預填充服務獲取的資料。 如果usePrefillService設定為true，則輸入JSON資料（對於每個記錄）將被視為FDM參數。 預設值為false。 |
      | batchType | 字串 | 將值設定為PRINT、WEB或WEB_AND_PRINT。 預設值為WEB_AND_PRINT。 |
      | 地區設定 | 字串 | 指定輸出互動式通信的區域設定。 現成服務不使用區域設定選項，但您可以建立定制服務以生成本地化的互動式通信。 預設值為en_US |

   1. 點擊 **[!UICONTROL 建立]** 已建立監視資料夾。
1. 使用監視資料夾生成互動式通信：
   1. 開啟「監視」資料夾。 導航到輸入資料夾。
   1. 在輸入資料夾中建立資料夾，並將JSON檔案放在新建立的資料夾中。
   1. 等待「監視資料夾」處理該檔案。 當處理開始時，包含該檔案的輸入檔案和子資料夾將移到暫存資料夾。
   1. 開啟輸出資料夾以查看輸出：
      * 在「監視資料夾配置」中指定PRINT選項時，將生成互動式通信的PDF輸出。
      * 在「監視資料夾配置」中指定WEB選項時，將生成每個記錄的JSON檔案。 可以使用JSON檔案 [預填充Web模板](#web-template)。
      * 指定PRINT和WEB選項時，將同時生成PDF文檔和每個記錄的JSON檔案。

#### 使用保存在外部資料源中並通過表單資料模型訪問的輸入資料來產生互動式通信 {#use-fdm-as-data-source}

將保存在外部資料源中的資料（記錄）與互動式通信模板組合以生成互動式通信。 建立互動式通信時，可通過表單資料模型(FDM)將其連接到外部資料源以訪問資料。 您可以配置「監視資料夾」批處理服務，以便使用同一表單資料模型從外部資料源獲取資料。 至 [從外部資料源中保存的記錄建立互動式通信](/help/forms/using/work-with-form-data-model.md):

1. 配置模板的表單資料模型：
   1. 開啟與交互通信模板關聯的表單資料模型。
   1. 選擇頂級模型對象，然後按一下「編輯屬性」(Edit Properties)。
   1. 從「編輯屬性」窗格下的「讀取服務」欄位中選擇獲取或獲取服務。
   1. 按一下讀取服務參數的鉛筆表徵圖，將參數綁定到請求屬性並指定綁定值。 它將服務參數綁定到指定的綁定屬性或文本值，該屬性或文本值作為參數傳遞給服務，以從資料源獲取與指定值關聯的詳細資訊。

      <br>
        在本示例中， id參數採用用戶配置檔案的id屬性的值並將其作為參數傳遞給讀取服務。 它將從指定ID的僱員資料模型對象讀取並返回關聯屬性的值。 因此，如果您在表單的id欄位中指定00250，則讀取服務將讀取具有00250employee id的員工的詳細資訊。
        <br>

      ![配置請求屬性](assets/request-attribute.png)

   1. 保存屬性和表單資料模型。
1. 配置請求屬性的值：
   1. 在檔案系統上建立.json檔案，然後將其開啟以進行編輯。
   1. 建立JSON陣列並指定從表單資料模型提取資料的主要屬性。 例如，以下JSON請求FDM發送id為27126或27127的記錄資料：

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

   1. 保存並關閉檔案。

1. 建立 [監視資料夾](/help/forms/using/creating-configure-watched-folder.md) 並將其配置為使用Batch API服務：
   1. 登錄到AEM Forms作者實例。
   1. 導航到 **[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 配置監視資料夾]**。 點擊 **[!UICONTROL 新建]**。
   1. 指定 **[!UICONTROL 名稱]** 和物理 **[!UICONTROL 路徑]** 的子菜單。 比如說， `c:\batchprocessing`。
   1. 選擇 **[!UICONTROL 服務]** 的上界 **[!UICONTROL 進程檔案使用]** 的子菜單。
   1. 選擇 **[!UICONTROL com.adobe.fd.ccm.machnawer.batch.impl.service.InteractiveCommunicationBatchServiceImpl]** 服務 **[!UICONTROL 服務名稱]** 的子菜單。
   1. 指定 **[!UICONTROL 輸出檔案模式]**。 例如，%F/ [圖案](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns) 指定「監視資料夾」可以在「監視資料夾」\input資料夾的子資料夾中查找輸入檔案。
1. 配置高級參數：
   1. 開啟 **[!UICONTROL 高級]** 頁籤，然後添加以下自定義屬性：

      | 屬性 | 類型 | 說明 |
      |--- |--- |--- |
      | 模板路徑 | 字串 | 指定要使用的交互通信模板的路徑。 例如，/content/dam/formsanddocuments/testsample/mediumic。 這是強制屬性。 |
      | 記錄路徑 | 字串 | recordPath欄位的值有助於設定交互通信的名稱。 可以將記錄欄位的路徑設定為recordPath欄位的值。 例如，如果指定/employee/Id，則id欄位的值將成為相應交互通信的名稱。 預設值是隨機 [隨機UUID](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID())。 |  |
      | usePrefillService | 布林值 | 將值設定為True。 預設值為false。  當值設定為true時，Batch API將從配置的表單資料模型讀取資料，並將其填充到交互通信中。 如果usePrefillService設定為true，則輸入JSON資料（對於每個記錄）將被視為FDM參數。 |
      | batchType | 字串 | 將值設定為PRINT、WEB或WEB_AND_PRINT。 預設值為WEB_AND_PRINT。 |
      | 地區設定 | 字串 | 指定輸出互動式通信的區域設定。 現成服務不使用區域設定選項，但您可以建立定制服務以生成本地化的互動式通信。 預設值為en_US。 |

   1. 點擊 **[!UICONTROL 建立]** 已建立監視資料夾。
1. 使用監視資料夾生成互動式通信：
   1. 開啟「監視」資料夾。 導航到輸入資料夾。
   1. 在輸入資料夾中建立資料夾。 將在步驟2中建立的JSON檔案放在新建立的資料夾中。
   1. 等待「監視資料夾」處理該檔案。 當處理開始時，包含該檔案的輸入檔案和子資料夾將移到暫存資料夾。
   1. 開啟輸出資料夾以查看輸出：
      * 在「監視資料夾配置」中指定PRINT選項時，將生成互動式通信的PDF輸出。
      * 在「監視資料夾配置」中指定WEB選項時，將生成每個記錄的JSON檔案。 可以使用JSON檔案 [預填充Web模板](#web-template)。
      * 指定PRINT和WEB選項時，將同時生成PDF文檔和每個記錄的JSON檔案。

## 使用REST請求調用批API

可以調用 [批處理API](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/index.html) 通過代表狀態轉移(REST)請求。 它允許您向其他用戶提供REST終結點以訪問API，並配置您自己的方法以處理、儲存和自定義互動式通信。 您可以開發自己的自定義Java Servlet，以在實例上部AEM署API。

在部署Java Servlet之前，請確保您有互動式通信，並且相應的資料檔案已準備好。 執行以下步驟以建立和部署Java Servlet:

1. 登錄到實例AEM並建立交互通信。 要使用下面給出的示例代碼中提到的互動式通信， [按一下這裡](assets/SimpleMediumIC.zip)。
1. [使用Apache Maven生成AEM和部署項目](https://helpx.adobe.com/experience-manager/using/maven_arch13.html) 你的案AEM子。
1. 添加 [AEM Forms客戶端SDK 6.0.12版](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 或在項目的POM檔案的依賴項清單中AEM更新。 例如，

   ```xml
       <dependency>
           <groupId>com.adobe.aemfd</groupId>
           <artifactId>aemfd-client-sdk</artifactId>
           <version>6.0.122</version>
       </dependency>
   ```

1. 開啟Java項目，建立.java檔案，例如CCMBatchServlet.java。 將下列程式碼新增至檔案中：

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

1. 在上述代碼中，將模板路徑(setTemplatePath)替換為模板路徑和setBatchType API的set值：
   * 指定互動式通信的PRINT選項PDF輸出時，將生成。
   * 指定WEB選項時，將生成每個記錄的JSON檔案。 可以使用JSON檔案 [預填充Web模板](#web-template)。
   * 指定PRINT和WEB選項時，將同時生成PDF文檔和每個記錄的JSON檔案。

1. [使用maven將更新的代碼部署到實AEM例](https://helpx.adobe.com/experience-manager/using/maven_arch13.html#BuildtheOSGibundleusingMaven)。
1. 調用批處理API以生成交互通信。 批處理API打印會根據記錄數返回PDF和.json檔案流。 可以使用JSON檔案 [預填充Web模板](#web-template)。 如果使用上述代碼，則API將部署在 `http://localhost:4502/bin/batchServlet`。 代碼將打印並返回PDF和JSON檔案的流。

### 預填充Web模板 {#web-template}

將batchType設定為呈現Web通道時，API將為每個資料記錄生成JSON檔案。 可以使用以下語法將JSON檔案與相應的Web通道合併，以生成互動式通信：

**語法**
`http://host:port/<template-path>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=<guide-merged-json-path>`

**示例**
如果JSON檔案位於 `C:\batch\mergedJsonPath.json` 並使用以下互動式通信模板： `http://host:port/content/dam/formsanddocuments/testsample/mediumic/jcr:content?channel=web`

然後，發佈節點上的以下URL將顯示互動式通信的Web通道
`http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/batch/mergedJsonData.json`

除了在檔案系統上保存資料外，您還將JSON檔案儲存在CRX-repository、檔案系統、Web伺服器中，或者可以通過OSGI預填充服務訪問資料。 使用各種協定合併資料的語法有：

* **CRX協定**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=crx:///tmp/fd/af/mergedJsonData.json`

* **檔案協定**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/Users/af/mergedJsonData.json`

* **預填充服務協定**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=service://[SERVICE_NAME]/[IDENTIFIER]`

   SERVICE_NAME指OSGI預填充服務的名稱。 請參閱建立並運行預填服務。

   IDENTIFIER指OSGI預填充服務獲取預填充資料所需的任何元資料。 登錄用戶的標識符是可以使用的元資料的示例。

* **HTTP協定**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=http://localhost:8000/somesamplexmlfile.xml`

>[!NOTE]
>
>預設情況下只啟用CRX協定。 要啟用其他支援的協定，請參見 [使用Configuration Manager配置預填充服務](https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#ConfiguringprefillserviceusingConfigurationManager)。
