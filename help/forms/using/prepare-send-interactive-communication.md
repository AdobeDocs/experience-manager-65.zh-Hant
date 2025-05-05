---
title: 使用Agent UI準備和傳送互動式通訊
description: 代理程式UI可讓代理程式準備互動式通訊，並將其傳送到發佈程式。 代理程式會視需要進行必要的修改，並將互動式通訊提交至發佈程式，例如電子郵件或列印。
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Interactive Communication
exl-id: 4fb82e9b-f870-47db-ac92-2d7510acace8
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '2010'
ht-degree: 0%

---

# 使用Agent UI準備和傳送互動式通訊 {#prepare-and-send-interactive-communication-using-the-agent-ui}

代理程式UI可讓代理程式準備互動式通訊，並將其傳送到發佈程式。 代理程式會視需要進行必要的修改，並將互動式通訊提交至發佈程式，例如電子郵件或列印。

## 概觀 {#overview}

建立互動式通訊後，代理程式便可在代理程式UI中開啟互動式通訊，並透過輸入資料及管理內容與附件來準備收件者特定的復本。 最後，代理程式可將互動式通訊提交至後續程式。

使用代理程式UI準備互動式通訊時，代理程式會先在代理程式UI中管理互動式通訊的下列方面，然後再將其提交至後續程式：

* **資料**：代理程式UI的「資料」索引標籤會在互動式通訊中顯示任何可編輯代理程式的變數以及解除鎖定的表單資料模型屬性。 這些變數/屬性是在編輯或建立包含在互動式通訊中的檔案片段時建立的。 資料標籤也包含在XDP/列印管道範本中建置的任何欄位。 只有當互動式通訊中有代理程式可編輯的任何變數、表單資料模型屬性或欄位時，資料標籤才會顯示。
* **內容**：在「內容」標籤中，代理程式會管理互動式通訊中的內容，例如檔案片段和內容變數。 代理程式可以在檔案片段的屬性中建立互動式通訊時，在這些檔案片段中進行允許的變更。 如果允許，代理程式也可以重新排序、新增/移除檔案片段以及新增分頁符號。
* **附件**：只有互動式通訊具有任何附件，或代理程式具有程式庫存取權時，「附件」索引標籤才會顯示在「代理程式」UI中。 代理程式可能可以變更或編輯附件，也可能不允許。

## 使用Agent UI準備互動式通訊 {#prepare-interactive-communication-using-the-agent-ui}

1. 選取&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**。
1. 選取適當的互動式通訊，並選取&#x200B;**[!UICONTROL 開啟代理程式UI]**。

   >[!NOTE]
   >
   >代理程式UI只有在選取的互動式通訊具有列印管道時才有效。

   ![openagentiui](assets/openagentiui.png)

   根據互動式通訊的內容和屬性，代理程式UI會出現以下三個索引標籤：資料、內容和附件。

   ![agentuitabs](assets/agentuitabs.png)

   繼續輸入資料、管理內容及管理附件。

### 輸入資料 {#enter-data}

1. 在「資料」標籤中，視需要輸入變數、表單資料模型屬性和列印範本(XDP)欄位的資料。 填寫標示星號(&amp;amp；ast；)的所有必要欄位，以啟用&#x200B;**提交**&#x200B;按鈕。

   在互動式通訊預覽中選取資料欄位值，以反白顯示「資料」標籤中對應的資料欄位，反之亦然。

### 管理內容 {#manage-content}

在「內容」標籤中，管理互動式通訊中的內容，例如檔案片段和內容變數。

1. 選取&#x200B;**[!UICONTROL 內容]**。 互動式通訊的內容標籤隨即顯示。

   ![agentuicontenttab](assets/agentuicontenttab.png)

1. 視需要在「內容」標籤中編輯檔案片段。 若要將焦點置於內容階層中的相關片段，您可以在互動式通訊預覽中選取相關行或段落，或直接在內容階層中選取片段。

   例如，在下圖中的預覽中選取了行為「立即線上上付款……」的檔案片段，並在「內容」標籤中選取了相同的檔案片段。

   ![contentmodulefocus](assets/contentmodulefocus.png)

   在「內容」或「資料」標籤中，點選預覽左上角的「內容中反白選取的模組」 (![highlightselectedmodulesincontentccr](assets/highlightselectedmodulesincontentccr.png))，即可停用或啟用在預覽中點選/選取相關文字、段落或資料欄位時移至檔案片段的功能。

   代理程式在建立互動式通訊時可以編輯的片段具有編輯選取的內容( ![iconeditselectedcontent](assets/iconeditselectedcontent.png))圖示。 選取「編輯選取的內容」圖示，在編輯模式中啟動片段並進行變更。 使用下列選項來格式化及管理文字：

   * [格式化選項](#formattingtext)

      * [從其他應用程式複製貼上格式化文字](#pasteformattedtext)
      * [反白部分文字](#highlightemphasize)

   * [特殊字元](#specialcharacters)
   * [鍵盤快速鍵](/help/forms/using/keyboard-shortcuts.md)

   如需代理程式使用者介面中各種檔案片段可用動作的詳細資訊，請參閱[代理程式使用者介面中可用的動作和資訊](#actionsagentui)。

1. 若要在互動式通訊的列印輸出中新增分頁符號，請將游標置於您要插入分頁符號的位置，並選取「在之前分頁符號」或「在之後分頁符號」 (![pagebreakbeforeafter](assets/pagebreakbeforeafter.png))。

   在互動式通訊中插入明確的分頁符號預留位置。 若要檢視明確的分頁符號如何影響互動式通訊，請參閱列印預覽。

   ![explicitpagebreak](assets/explicitpagebreak.png)

   繼續管理互動式通訊的附件。

### 管理附件 {#manage-attachments}

1. 選取&#x200B;**[!UICONTROL 附件]**。 建立互動式通訊時，代理程式UI會依設定顯示可用的附件。

   您可以點選檢檢視示，選擇不隨互動式通訊提交附件，也可以選取附件中的十字形將其從互動式通訊中刪除（如果允許代理程式刪除或隱藏附件）。 對於建立互動式通訊時指定為必要專案的附件，「檢視」和「刪除」圖示會停用。

   ![附件sagentui](assets/attachmentsagentui.png)

1. 選取「資料庫存取」 (![libraryaccess](assets/libraryaccess.png))圖示可存取「內容資料庫」，將DAM資產插入為附件。

   >[!NOTE]
   >
   >只有在建立互動式通訊時（在「列印」管道的「檔案容器」屬性中）已啟用資料庫存取，才可使用「資料庫存取」圖示。

1. 如果在建立互動式通訊時未鎖定附件的順序，您可以選取附件並點選向下和向上箭頭，以重新排序附件。
1. 使用「Web預覽」和「列印預覽」，檢視這兩個輸出是否符合您的要求。

   如果您覺得預覽滿意，請選取&#x200B;**[!UICONTROL 提交]**&#x200B;以提交/傳送互動式通訊至發佈程式。 或者，若要進行變更，請退出預覽以返回進行變更。

## 格式化文字 {#formattingtext}

在代理程式UI中編輯文字片段時，工具列會隨著您選擇進行的編輯型別而改變：「字型」、「段落」或「清單」：

![typeofformattingtoolbar](assets/typeofformattingtoolbar.png) ![字型工具列](do-not-localize/fonttoolbar.png)

字型工具列

![段落工具列](do-not-localize/paragraphtoolbar.png)

段落工具列

![清單工具列](do-not-localize/listtoolbar.png)

清單工具列

### 醒目提示/強調文字部分 {#highlightemphasize}

若要醒目提示\強調可編輯片段中的部分文字，請選取文字並選取「醒目提示顏色」。

![highlighttextagentui](assets/highlighttextagentui.png)

### 貼上格式化文字 {#pasteformattedtext}

![貼上文字](assets/pastedtext.png)

### 在文字中插入特殊字元 {#specialcharacters}

Agent UI已內建對210個特殊字元的支援。 管理員可以透過自訂[&#128279;](/help/forms/using/custom-special-characters.md) 新增更多/自訂特殊字元的支援。

#### 附件傳遞 {#attachmentdelivery}

* 使用伺服器端API以互動或非互動式PDF呈現互動式通訊時，呈現的PDF會包含附件作為PDF附件。
* 當使用代理程式UI將與互動式通訊相關聯的貼文程式載入為提交的一部分時，附件會傳遞為List&lt;com.adobe.idp.Document> inAttachmentDocs引數。
* 傳遞機制工作流程（例如電子郵件和列印）也會連同互動式通訊的PDF版本一起傳遞附件。

## 代理程式使用者介面中可用的動作和資訊 {#actionsagentui}

### 檔案片段 {#document-fragments}

![ ](do-not-localize/contentoptionsdocfragments.png)

* **向上/向下箭號**：在互動式通訊中向上或向下移動檔案片段的箭號。
* **刪除**：如果允許，請從互動式通訊中刪除檔案片段。
* **在**&#x200B;之前分頁（適用於目標區域的子片段）：在檔案片段之前插入分頁。
* **縮排**：增加或減少檔案片段的縮排。
* **在**&#x200B;之後分頁（適用於目標區域的子片段）：在檔案片段之後插入分頁。

![docfragoptions](assets/docfragoptions.png)

* 編輯（僅限文字片段）：開啟RTF編輯器以編輯文字檔案片段。 如需詳細資訊，請參閱[格式化文字](#formattingtext)。

* 選擇（眼睛圖示）：包含\排除互動式通訊的檔案片段。
* 未填入的值（資訊）：表示檔案片段中未填入的變數數量。

### 列出檔案片段 {#list-document-fragments}

![listoptions](assets/listoptions.png)

* 插入空白行：插入新的空白行。
* 選擇（眼睛圖示）：包含\排除互動式通訊的檔案片段。
* 略過專案符號/編號：若要略過清單檔案片段中的專案符號/編號，請啟用此選項。
* 未填入的值（資訊）：表示檔案片段中未填入的變數數量。

## 將互動式通訊儲存為草稿 {#save-as-draft}

您可以使用代理程式UI來儲存每個互動式通訊的一或多個草稿，並稍後擷取草稿以繼續處理。 您可以為每個草稿指定不同的名稱來識別它。

Adobe建議依序執行這些指示，以成功將互動式通訊儲存為草稿。

### 啟用另存為草稿功能 {#before-save-as-draft}

預設不會啟用「另存為草稿」功能。 執行以下步驟來啟用此功能：

1. 實作[ccrDocumentInstance](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/ccr/ccrDocumentInstance/api/services/CCRDocumentInstanceService.html)服務提供者介面(SPI)。

   SPI可讓您將互動式通訊的草稿版本儲存到資料庫，並將草稿ID儲存為唯一識別碼。 這些指示假設您擁有有關如何使用Maven專案建置OSGi套件的先前知識。

   如需範例SPI實作，請參閱[範例ccrDocumentInstance SPI實作](#sample-ccrDocumentInstance-spi)。
1. 開啟`http://<hostname>:<port>/ system/console/bundles`並選取&#x200B;**[!UICONTROL 安裝/更新]**&#x200B;以上傳OSGi套件。 確認上傳之封裝的狀態顯示為&#x200B;**作用中**。 如果封裝的狀態未顯示為&#x200B;**Active**，請重新啟動伺服器。
1. 前往 `https://'[server]:[port]'/system/console/configMgr`。
1. 選取&#x200B;**[!UICONTROL 建立通訊設定]**。
1. 選取&#x200B;**[!UICONTROL 使用CCRDocumentInstanceService啟用儲存]**，然後選取&#x200B;**[!UICONTROL 儲存]**。

### 將互動式通訊儲存為草稿 {#save-as-draft-agent-ui}

執行以下步驟，將互動式通訊儲存為草稿：

1. 在Forms Manager中選取互動式通訊，並選取&#x200B;**[!UICONTROL 開啟代理程式UI]**。

1. 在代理程式UI中進行適當的變更，並選取&#x200B;**[!UICONTROL 另存為草稿]**。

1. 在&#x200B;**[!UICONTROL 名稱]**&#x200B;欄位中指定草稿的名稱，並選取&#x200B;**[!UICONTROL 完成]**。

將互動式通訊儲存為草稿後，請選取&#x200B;**[!UICONTROL 儲存變更]**&#x200B;以儲存對草稿所做的任何進一步變更。

### 擷取互動式通訊的草稿 {#retrieve-draft}

將互動式通訊儲存為草稿後，您可以擷取該通訊以繼續處理。 擷取互動式通訊，使用：

`https://server:port/aem/forms/createcorrespondence.hmtl?draftid=[draftid]`

[draftid]參考將互動式通訊儲存為草稿後所產生之草稿版本的唯一識別碼。

### ccrDocumentInstance SPI實作範例 {#sample-ccrDocumentInstance-spi}

實作`ccrDocumentInstance` SPI以將互動式通訊儲存為草稿。 以下是`ccrDocumentInstance` SPI的範例實作。

```javascript
package Implementation;

import com.adobe.fd.ccm.ccr.ccrDocumentInstance.api.exception.CCRDocumentException;
import com.adobe.fd.ccm.ccr.ccrDocumentInstance.api.model.CCRDocumentInstance;
import com.adobe.fd.ccm.ccr.ccrDocumentInstance.api.services.CCRDocumentInstanceService;
import org.apache.commons.lang3.StringUtils;
import org.osgi.service.component.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.util.*;


@Component(service = CCRDocumentInstanceService.class, immediate = true)
public class CCRDraftService implements CCRDocumentInstanceService {

    private static final Logger logger = LoggerFactory.getLogger(CCRDraftService.class);

    private HashMap<String, Object> draftDataMap = new HashMap<>();

    @Override
    public String save(CCRDocumentInstance ccrDocumentInstance) throws CCRDocumentException {
        String documentInstanceName = ccrDocumentInstance.getName();
        if (StringUtils.isNotEmpty(documentInstanceName)) {
            logger.info("Saving ccrData with name : {}", ccrDocumentInstance.getName());
            if (!CCRDocumentInstance.Status.SUBMIT.equals(ccrDocumentInstance.getStatus())) {
                ccrDocumentInstance = mySQLDataBaseServiceCRUD(ccrDocumentInstance,null, "SAVE");
            }
        } else {
            logger.error("Could not save data as draft name is empty");
        }
        return ccrDocumentInstance.getId();
    }

    @Override
    public void update(CCRDocumentInstance ccrDocumentInstance) throws CCRDocumentException {
        String documentInstanceName = ccrDocumentInstance.getName();
        if (StringUtils.isNotEmpty(documentInstanceName)) {
            logger.info("Saving ccrData with name : {}", documentInstanceName);
            mySQLDataBaseServiceCRUD(ccrDocumentInstance, ccrDocumentInstance.getId(), "UPDATE");
        } else {
            logger.error("Could not save data as draft Name is empty");
        }
    }

    @Override
    public CCRDocumentInstance get(String id) throws CCRDocumentException {
        CCRDocumentInstance cCRDocumentInstance;
        if (StringUtils.isEmpty(id)) {
            logger.error("Could not retrieve data as draftId is empty");
            cCRDocumentInstance = null;
        } else {
            cCRDocumentInstance = mySQLDataBaseServiceCRUD(null, id,"GET");
        }
        return cCRDocumentInstance;
    }

    @Override
    public List<CCRDocumentInstance> getAll(String userId, Date creationTime, Date updateTime,
                                            Map<String, Object> optionsParams) throws CCRDocumentException {
        List<CCRDocumentInstance> ccrDocumentInstancesList = new ArrayList<>();

        HashMap<String, Object> allSavedDraft = mySQLGetALLData();
        for (String key : allSavedDraft.keySet()) {
            ccrDocumentInstancesList.add((CCRDocumentInstance) allSavedDraft.get(key));
        }
        return ccrDocumentInstancesList;
    }

    //The APIs call the service in the database using the following section.
    private CCRDocumentInstance mySQLDataBaseServiceCRUD(CCRDocumentInstance ccrDocumentInstance,String draftId, String method){
        if(method.equals("SAVE")){

            String autoGenerateId = draftDataMap.size() + 1 +"";
            ccrDocumentInstance.setId(autoGenerateId);
            draftDataMap.put(autoGenerateId, ccrDocumentInstance);
            return ccrDocumentInstance;

        }else if (method.equals("UPDATE")){

            draftDataMap.put(ccrDocumentInstance.getId(), ccrDocumentInstance);
            return ccrDocumentInstance;

        }else if(method.equals("GET")){

            return (CCRDocumentInstance) draftDataMap.get(draftId);

        }
        return null;
    }

    private HashMap<String, Object> mySQLGetALLData(){
        return draftDataMap;
    }
}
```

`save`、`update`、`get`和`getAll`作業會呼叫資料庫服務，以將互動式通訊儲存為草稿、更新互動式通訊、從資料庫擷取資料，以及擷取資料庫中所有可用互動式通訊的資料。 此範例使用`mySQLDataBaseServiceCRUD`作為資料庫服務的名稱。

下表說明範例`ccrDocumentInstance` SPI實作。 它示範`save`、`update`、`get`和`getAll`作業如何在範例實作中呼叫資料庫服務。

<table> 
 <tbody>
 <tr>
  <td><p><strong>操作</strong></p></td>
  <td><p><strong>資料庫服務範例</strong></p></td> 
   </tr>
  <tr>
   <td><p>您可以建立互動式通訊的草稿，或直接提交。 儲存作業的API會檢查互動式通訊是否以草稿形式提交，並包含草稿名稱。 然後，API會呼叫mySQLDataBaseServiceCRUD服務，並將Save儲存為輸入方法。</p></br><img src="assets/save-as-draft-save-operation.png"/></td>
   <td><p>mySQLDataBaseServiceCRUD服務會驗證Save作為輸入方法，並產生自動產生的草稿ID並將其傳回AEM。 產生草稿ID的邏輯可能會因資料庫而異。</p></br><img src="assets/save-operation-service.png"/></td>
   </tr>
  <tr>
   <td><p>更新作業的API會擷取互動式通訊草稿的狀態，並檢查互動式通訊是否包含草稿名稱。 API會呼叫mySQLDataBaseServiceCRUD服務來更新資料庫中的狀態。</p></br><img src="assets/save-as-draft-update-operation.png"/></td>
   <td><p>mySQLDataBaseServiceCRUD服務會驗證Update作為輸入方法，並將互動式通訊草稿的狀態儲存在資料庫中。</br></p><img src="assets/update-operation-service.png"/></td>
   </tr>
   <tr>
   <td><p>取得作業的API會檢查互動式通訊是否包含草稿ID。 然後API會呼叫mySQLDataBaseServiceCRUD服務（使用Get作為輸入方法），以擷取互動式通訊的資料。</br></p><img src="assets/save-as-draft-get-operation.png"/></td>
   <td><p>mySQLDataBaseServiceCRUD服務會驗證Get作為輸入方法，並根據草稿ID擷取互動式通訊的資料。</p></br><img src="assets/get-operation-service.png"/></td>
   </tr>
   <tr>
   <td><p>getAll作業的API會呼叫mySQLGetALLData服務，以擷取儲存在資料庫中所有互動式通訊的資料。</br></p><img src="assets/save-as-draft-getall-operation.png"/></td>
   <td><p>mySQLGetALLData服務會擷取儲存在資料庫中所有互動式通訊的資料。</p></br><img src="assets/getall-operation-service.png"/></td>
   </tr>
  </tbody>
</table>

以下是屬於實作一部分的`pom.xml`檔案的範例：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0"
         xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.adobe.livecycle</groupId>
    <artifactId>draft-sample</artifactId>
    <version>2.0.0-SNAPSHOT</version>

    <name>Interact</name>
    <packaging>bundle</packaging>

    <dependencies>
        <dependency>
            <groupId>com.adobe.aemfd</groupId>
            <artifactId>aemfd-client-sdk</artifactId>
            <version>6.0.160</version>
        </dependency>
    </dependencies>


    <!-- ====================================================================== -->
    <!-- B U I L D D E F I N I T I O N -->
    <!-- ====================================================================== -->
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.felix</groupId>
                <artifactId>maven-bundle-plugin</artifactId>
                <version>3.3.0</version>
                <extensions>true</extensions>
                <executions>
                    <!--Configure extra execution of 'manifest' in process-classes phase to make sure SCR metadata is generated before unit test runs-->
                    <execution>
                        <id>scr-metadata</id>
                        <goals>
                            <goal>manifest</goal>
                        </goals>
                    </execution>
                </executions>
                <configuration>
                    <exportScr>true</exportScr>
                    <instructions>
                        <!-- Enable processing of OSGI DS component annotations -->
                        <_dsannotations>*</_dsannotations>
                        <!-- Enable processing of OSGI metatype annotations -->
                        <_metatypeannotations>*</_metatypeannotations>
                        <Bundle-SymbolicName>${project.groupId}-${project.artifactId}</Bundle-SymbolicName>
                    </instructions>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>8</source>
                    <target>8</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
    <profiles>
        <profile>
            <id>autoInstall</id>
            <build>
                <plugins>
                    <plugin>
                        <groupId>org.apache.sling</groupId>
                        <artifactId>maven-sling-plugin</artifactId>
                        <executions>
                            <execution>
                                <id>install-bundle</id>
                                <phase>install</phase>
                                <goals>
                                    <goal>install</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
    </profiles>

</project>
```

>[!NOTE]
>
>請確定您在`pom.xml`檔案中將`aemfd-client-sdk`相依性更新為6.0.160。
