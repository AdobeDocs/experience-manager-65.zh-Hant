---
title: 使用代理UI準備和傳送互動式通訊
seo-title: 使用代理UI準備和傳送互動式通訊
description: 代理UI允許代理準備併發送互動式通信到後置進程。 代理程式會視需要進行修改，並將互動式通訊提交至後置程式，例如電子郵件或列印。
seo-description: 使用代理UI準備和傳送互動式通訊
uuid: d1a19b83-f630-4648-9ad2-a22374e31aa9
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 110c86ea-9bd8-4018-bfcc-ca33e6b3f3ba
feature: Interactive Communication
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2062'
ht-degree: 0%

---


# 使用代理UI {#prepare-and-send-interactive-communication-using-the-agent-ui}準備和發送互動式通信

代理UI允許代理準備併發送互動式通信到後置進程。 代理程式會視需要進行修改，並將互動式通訊提交至後置程式，例如電子郵件或列印。

## 概覽 {#overview}

建立互動式通信後，代理可以在代理UI中開啟互動式通信，並通過輸入資料和管理內容和附件來準備特定於收件人的副本。 最後，代理可將互動式通訊提交至後置程式。

使用代理UI準備互動式通訊時，代理會先在代理UI中管理互動式通訊的下列方面，再將它送出至後置程式：

* **資料**:Agent UI的「資料」頁籤顯示「交互通信」中任何可代理編輯的變數和解鎖表單資料模型屬性。這些變數／屬性是在編輯或建立包含在互動式通訊中的檔案片段時建立。 「資料」標籤也包含XDP/列印頻道範本中建立的任何欄位。 僅當代理可編輯「互動式通信」中的任何變數、表單資料模型屬性或欄位時，才會顯示「資料」頁籤。
* **內容**:在「內容」索引標籤中，「代理」管理「互動式通訊」中的檔案片段和內容變數等內容。在這些文檔片段的屬性中建立交互通信時，代理可以按照允許的方式在文檔片段中進行更改。 如果允許，代理還可以重新排序、添加／刪除文檔片段和添加分頁符。
* **附件**:只有當Interactive Communication具有任何附件或Agent具有庫訪問權限時，「附件」頁籤才會出現在Agent UI。工程師可以或不允許更改或編輯附件。

## 使用代理UI {#prepare-interactive-communication-using-the-agent-ui}準備互動式通信

1. 選擇&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms和文檔]**。
1. 選擇適當的「Interactive Communication（互動式通信）」 ，然後按一下「Open Agent UI（開啟代理UI）」。****

   >[!NOTE]
   >
   >代理UI僅在選定的互動式通信具有打印通道時才起作用。

   ![openagentiui](assets/openagentiui.png)

   根據Interactive Communication的內容和屬性，代理UI將顯示為以下三個頁籤：資料、內容和附件。

   ![agentitabs](assets/agentuitabs.png)

   繼續輸入資料、管理內容以及管理附件。

### 輸入資料 {#enter-data}

1. 在「資料」索引標籤中，視需要輸入變數、表單資料模型屬性和列印範本(XDP)欄位的資料。 填寫所有標有星號(&amp;ast;)的必填欄位，以啟用&#x200B;**Submit**&#x200B;按鈕。

   在「互動式通訊」預覽中點選資料欄位值，以在「資料」索引標籤中反白顯示對應的資料欄位，反之亦然。

### 管理內容 {#manage-content}

在「內容」索引標籤中，管理「互動式通訊」中的檔案片段和內容變數等內容。

1. 選擇&#x200B;**[!UICONTROL 內容]**。 此時將顯示「互動式通信」的內容頁籤。

   ![agentuicontentab](assets/agentuicontenttab.png)

1. 視需要在「內容」索引標籤中編輯檔案片段。 若要將焦點放在內容階層中的相關片段上，您可以在「互動式通訊」預覽中點選相關行或段落，或直接在「內容」階層中點選片段。

   例如，檔案片段的行為是「立即線上付款……」」在下圖的預覽中選取，而「內容」索引標籤中也選取了相同的檔案片段。

   ![contentmodulefocus](assets/contentmodulefocus.png)

   在「內容」或「資料」索引標籤中，點選預覽左上角的「反白標示內容中選取的模組」（![反白標示選取的模組incontentccr](assets/highlightselectedmodulesincontentccr.png)），可停用或啟用在預覽中點選／選取相關文字、段落或資料欄位時移至檔案片段的功能。

   建立交互通信時允許由代理編輯的片段具有編輯選定內容(![iconedited content](assets/iconeditselectedcontent.png))表徵圖。 點選「編輯選取的內容」圖示，以編輯模式啟動片段並在其中進行變更。 使用下列選項來格式化和管理文字：

   * [格式選項](#formattingtext)

      * [從其他應用程式複製貼上格式的文字](#pasteformattedtext)
      * [反白顯示部分文字](#highlightemphasize)
   * [特殊字元](#specialcharacters)
   * [鍵盤快速鍵](/help/forms/using/keyboard-shortcuts.md)

   有關Agent用戶介面中各種文檔片段的可用操作的詳細資訊，請參閱[Agent用戶介面中的可用操作和資訊。](#actionsagentui)

1. 要將分頁符添加到互動式通信的打印輸出中，請將游標置於要插入分頁符的位置，然後選擇「分頁前」或「分頁後」(![pagebreakafter](assets/pagebreakbeforeafter.png))。

   在「互動式通訊」中插入明確的分頁符預留位置。 若要檢視明確的分頁符號如何影響互動式通訊，請參閱列印預覽。

   ![explicitionpagebreak](assets/explicitpagebreak.png)

   繼續管理互動式通訊的附件。

### 管理附件{#manage-attachments}

1. 選擇&#x200B;**[!UICONTROL 附件]**。 Agent UI顯示建立交互通信時設定的可用附件。

   您可以點選檢視圖示，選擇不隨附件一起提交「互動式通訊」，也可以點選附件中的交叉點以從「互動式通訊」中刪除附件（如果允許代理刪除或隱藏附件）。 對於在建立互動式通信時指定為必備附件的附件，將禁用「查看」和「刪除」表徵圖。

   ![附件Agentui](assets/attachmentsagentui.png)

1. 點選「資料庫存取」（![資料庫存取](assets/libraryaccess.png)）圖示，以存取「內容庫」，將DAM資產插入為附件。

   >[!NOTE]
   >
   >只有在建立互動式通訊時（在列印頻道的「檔案容器」屬性中）啟用資料庫存取時，才可使用「資料庫存取」圖示。

1. 如果在建立「交互通信」時未鎖定附件順序，則可以通過選擇附件並點選向下和向上箭頭來重新排序附件。
1. 使用「網頁預覽和列印預覽」，查看這兩個輸出是否符合您的需求。

   如果您發現預覽結果令人滿意，請點選&#x200B;**[!UICONTROL Submit]**&#x200B;以提交／傳送互動式通訊至貼文程式。 或者，若要進行變更，請退出預覽，返回進行變更。

## 格式化文本{#formattingtext}

在代理UI中編輯文字片段時，工具列會依您選擇進行的編輯類型而變更：字型、段落或清單：

![文字](assets/typeofformattingtoolbar.png) ![格式工具列字型工具列](do-not-localize/fonttoolbar.png)

字型工具列

![段落工具列](do-not-localize/paragraphtoolbar.png)

段落工具列

![清單工具列](do-not-localize/listtoolbar.png)

清單工具列

### 突出顯示／強調部分文本{#highlightemphasize}

若要反白\強調可編輯片段中的部分文字，請選取文字並點選「反白顯示顏色」。

![highlighttextagentui](assets/highlighttextagentui.png)

### 貼上格式化文字{#pasteformattedtext}

![pastedtext](assets/pastedtext.png)

### 在文字{#specialcharacters}中插入特殊字元

Agent UI已內建支援210個特殊字元。 管理員可以透過自訂](/help/forms/using/custom-special-characters.md)新增對更多／自訂特殊字元的支援。[

#### 附件遞送{#attachmentdelivery}

* 當使用伺服器端API將互動式通訊轉譯為互動式或非互動式PDF時，轉譯的PDF會將附件包含為PDF附件。
* 當與互動式通訊相關聯的貼文程式載入為使用代理程式UI提交的一部分時，附件會以List&lt;com.adobe.idp.Document> inAttachmentDocs參數的形式傳遞。
* 傳送機制工作流程（例如電子郵件和列印）也會傳送附件以及互動式通訊的PDF版本。

## 代理用戶介面{#actionsagentui}中可用的操作和資訊

### 檔案片段{#document-fragments}

![](do-not-localize/contentoptionsdocfragments.png)

* **向上／向下箭頭**:在互動式通訊中向上或向下移動檔案片段的箭頭。
* **刪除**:如果允許，請從「互動式通訊」中刪除檔案片段。
* **分頁前** （適用於目標區域的子片段）:在文檔片段前插入分頁符。
* **縮進**:增加或減少文檔片段的縮進。
* **Page Break After** （適用於目標區域的子片段）:在文檔片段後面插入分頁符。

![docfragoptions](assets/docfragoptions.png)

* 編輯（僅限文字片段）:開啟豐富式文字編輯器，以編輯文字檔案片段。 如需詳細資訊，請參閱[格式化文字](#formattingtext)。

* 選取範圍（眼睛圖示）:包含\排除「互動式通訊」中的檔案片段。
* 未填充的值（資訊）:指出檔案片段中未填入的變數數。

### 列出文檔片段{#list-document-fragments}

![清單選項](assets/listoptions.png)

* 插入空白行：插入新的空行。
* 選取範圍（眼睛圖示）:包含\排除「互動式通訊」中的檔案片段。
* 跳過項目符號／編號：啟用以跳過清單文檔片段中的項目符號／編號。
* 未填充的值（資訊）:指出檔案片段中未填入的變數數。

## 將互動式通訊儲存為草稿{#save-as-draft}

您可以使用Agent UI為每個「互動式通訊」儲存一或多個草稿，並稍後擷取草稿以繼續處理。 您可以為每個草稿指定不同的名稱以加以識別。

Adobe建議依序執行這些指示，以成功將互動式通訊儲存為草稿。

### 啟用「另存為草稿」功能{#before-save-as-draft}

預設情況下，「另存為拔模」(Save as a Draft)特徵不啟用。 執行下列步驟以啟用功能：

1. 實施[ccrDocumentInstance](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/ccr/ccrDocumentInstance/api/services/CCRDocumentInstanceService.html)服務提供商介面(SPI)。

   SPI可讓您將互動式通信的草稿版本以草稿ID作為唯一標識符保存到資料庫。 這些指示假設您先前已具備使用Maven專案建立OSGi套件的相關知識。

   有關SPI實施示例，請參見[Sample ccrDocumentInstance SPI實施](#sample-ccrDocumentInstance-spi)。
1. 開啟`http://<hostname>:<port>/ system/console/bundles`並點選&#x200B;**[!UICONTROL 安裝／更新]**&#x200B;以上傳OSGi套件。 驗證已上載包的狀態是否顯示為&#x200B;**活動**。 如果軟體包的狀態未顯示為&#x200B;**活動**，請重新啟動伺服器。
1. 前往 `https://'[server]:[port]'/system/console/configMgr`.
1. 點選&#x200B;**[!UICONTROL 建立對應設定]**。
1. 選擇「使用CCRDocumentInstanceService ]**啟用儲存」，然後點選「儲存」。**[!UICONTROL ****

### 將互動式通訊儲存為草稿{#save-as-draft-agent-ui}

執行以下步驟將互動式通信另存為草稿：

1. 在「Forms管理器」中選擇「互動式通信」，然後按一下「開啟代理UI」。****

1. 在代理UI中進行適當的更改，然後點選「另存為草稿」。****

1. 在&#x200B;**[!UICONTROL Name]**&#x200B;欄位中指定草稿名稱，然後點選&#x200B;**[!UICONTROL Done]**。

將「互動式通訊」儲存為草稿後，請點選「儲存變更&#x200B;**[!UICONTROL 」以儲存對草稿的任何進一步變更。]**

### 檢索互動式通信的草稿{#retrieve-draft}

將互動式通訊儲存為草稿後，您可以擷取它以繼續處理它。 使用下列方法檢索互動式通信：

`https://server:port/aem/forms/createcorrespondence.hmtl?draftid=[draftid]`

[將] 互動式通訊儲存為草稿後產生之草稿版本的唯一識別碼。

>[!NOTE]
>
>如果您在將「互動式通訊」儲存為草稿後對它進行任何變更，則草稿版本無法開啟。

### ccrDocumentInstance SPI實現示例{#sample-ccrDocumentInstance-spi}

實作`ccrDocumentInstance` SPI，將互動式通訊儲存為草稿。 以下是`ccrDocumentInstance` SPI的示例實現。

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

`save`、`update`、`get`和`getAll`操作調用資料庫服務，以將互動式通信另存為草稿、更新互動式通信、從資料庫檢索資料，以及檢索資料庫中所有可用互動式通信的資料。 此示例使用`mySQLDataBaseServiceCRUD`作為資料庫服務的名稱。

下表說明了示例`ccrDocumentInstance` SPI實現。 它演示了`save`、`update`、`get`和`getAll`操作在示例實施中如何調用資料庫服務。

<table> 
 <tbody>
 <tr>
  <td><p><strong>操作</strong></p></td>
  <td><p><strong>資料庫服務示例</strong></p></td> 
   </tr>
  <tr>
   <td><p>您可以建立互動式通訊的草稿，或直接送出。 儲存作業的API會檢查「互動式通訊」是否以草稿形式提交，並包含草稿名稱。 然後，API會以「儲存為輸入法」呼叫mySQLDataBaseServiceCRUD服務。</p></br><img src="assets/save-as-draft-save-operation.png"/></br>[#$sd1_sf1_dp9]</td>
   <td><p>mySQLDataBaseServiceCRUD服務驗證「另存為」輸入方法，並生成自動生成的草稿ID並將其返回AEM。 產生草稿ID的邏輯會因資料庫而異。</p></br><img src="assets/save-operation-service.png"/></br>[#$sd1_sf1_dp13]</td>
   </tr>
  <tr>
   <td><p>更新操作的API會擷取互動式通訊草稿的狀態，並檢查互動式通訊是否包含草稿名稱。 API會呼叫mySQLDataBaseServiceCRUD服務，以在資料庫中更新該狀態。</p></br><img src="assets/save-as-draft-update-operation.png"/></br>[#$sd1_sf1_dp17]</td>
   <td><p>mySQLDataBaseServiceCRUD服務將「更新」驗證為輸入方法，並將「交互通信」草稿的狀態保存在資料庫中。</br></p><img src="assets/update-operation-service.png"/></td>
   </tr>
   <tr>
   <td><p>取得作業的API會檢查互動式通訊是否包含草稿ID。 然後，API會以Get作為輸入方法呼叫mySQLDataBaseServiceCRUD服務，以擷取互動式通訊的資料。</br></p><img src="assets/save-as-draft-get-operation.png"/></td>
   <td><p>mySQLDataBaseServiceCRUD服務驗證Get作為輸入方法，並基於草稿ID檢索互動式通信的資料。</p></br><img src="assets/get-operation-service.png"/></br>[#$sd1_sf1_dp29]</td>
   </tr>
   <tr>
   <td><p>getAll操作的API調用mySQLGetALLData服務，以檢索資料庫中保存的所有互動式通信的資料。</br></p><img src="assets/save-as-draft-getall-operation.png"/></td>
   <td><p>mySQLGetALLData服務檢索資料庫中保存的所有互動式通信的資料。</p></br><img src="assets/getall-operation-service.png"/></br>[#$sd1_sf1_dp37]</td>
   </tr>
  </tbody>
</table>

以下是實施中`pom.xml`檔案的範例：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
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
>確保將`pom.xml`檔案中的`aemfd-client-sdk`相關性更新為6.0.160。
