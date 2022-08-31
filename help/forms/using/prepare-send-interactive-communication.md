---
title: 使用Agent UI準備和發送互動式通信
seo-title: Prepare and send Interactive Communication using the Agent UI
description: 代理UI允許代理準備並將互動式通信發送到後續進程。 代理程式會根據允許進行所需的修改，並將互動式通訊提交至後置程式，例如電子郵件或列印。
seo-description: Prepare and send Interactive Communication using the Agent UI
uuid: d1a19b83-f630-4648-9ad2-a22374e31aa9
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 110c86ea-9bd8-4018-bfcc-ca33e6b3f3ba
feature: Interactive Communication
exl-id: 4fb82e9b-f870-47db-ac92-2d7510acace8
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '2021'
ht-degree: 0%

---

# 使用Agent UI準備和發送互動式通信 {#prepare-and-send-interactive-communication-using-the-agent-ui}

代理UI允許代理準備並將互動式通信發送到後續進程。 代理程式會根據允許進行所需的修改，並將互動式通訊提交至後置程式，例如電子郵件或列印。

## 總覽 {#overview}

建立互動式通信後，代理可以在代理UI中開啟互動式通信，並通過輸入資料和管理內容和附件準備特定於收件人的副本。 最後，代理可將互動式通訊提交至後續程式。

使用代理UI準備互動式通訊時，代理在將互動式通訊提交至後續程式之前，會先在代理UI中管理互動式通訊的下列方面：

* **資料**:代理UI的「資料」頁簽顯示「交互通信」中任何可代理編輯的變數和未鎖定表單資料模型屬性。 這些變數/屬性是在編輯或建立互動式通訊中包含的檔案片段時建立。 「資料」標籤也包含XDP/列印通道範本中建置的任何欄位。 只有當Interactive Communication中存在代理可編輯的任何變數、表單資料模型屬性或欄位時，才會顯示「資料」頁簽。
* **內容**:在「內容」頁簽中，代理管理互動式通信中的文檔片段和內容變數等內容。 在這些文檔片段的屬性中建立交互通信時，代理可以按照允許的方式在文檔片段中進行更改。 如果允許，代理還可以重新排序、添加/刪除文檔片段以及添加分頁符。
* **附件**:僅當Interactive Communication具有任何附件或Agent具有庫訪問權時，Attachments頁簽才會顯示在代理UI中。 代理可以更改或不能編輯附件。

## 使用代理UI準備互動式通訊 {#prepare-interactive-communication-using-the-agent-ui}

1. 選擇 **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 選擇適當的「互動式通信」並點選 **[!UICONTROL 開啟代理UI]**.

   >[!NOTE]
   >
   >只有選定的交互通信具有打印通道時，代理UI才工作。

   ![openagentiui](assets/openagentiui.png)

   根據互動式通訊的內容和屬性，代理程式UI會顯示以下三個標籤：資料、內容和附件。

   ![代理](assets/agentuitabs.png)

   繼續輸入資料、管理內容及管理附件。

### 輸入資料 {#enter-data}

1. 在「資料」頁簽中，根據需要輸入變數的資料、表單資料模型屬性和打印模板(XDP)欄位。 填寫所有標有星號(&amp;ast;)的必填欄位，以啟用 **提交** 按鈕。

   在「互動式通訊」預覽中點選資料欄位值，以在「資料」標籤中反白顯示對應的資料欄位，反之亦然。

### 管理內容 {#manage-content}

在「內容」標籤中，管理互動式通訊中的內容，例如檔案片段和內容變數。

1. 選擇 **[!UICONTROL 內容]**. 「互動式通訊」的內容標籤隨即出現。

   ![agentuicontentab](assets/agentuicontenttab.png)

1. 視需要在「內容」索引標籤中編輯檔案片段。 若要聚焦在內容階層中的相關片段，您可以在「互動式通訊」預覽中點選相關行或段落，或直接在「內容」階層中點選片段。

   例如，在下圖的預覽中選擇了行為「立即進行線上付款……」的單據片段，並在「內容」頁簽中選擇了相同的單據片段。

   ![contentmodulefocus](assets/contentmodulefocus.png)

   在「內容」或「資料」索引標籤中，點選「在內容中反白顯示選取的模組」( ![highlightselectedmodulesincontentccr](assets/highlightselectedmodulesincontentccr.png))，您可以在預覽中點選/選取相關文字、段落或資料欄位時，停用或啟用功能以前往檔案片段。

   建立互動式通訊時允許由代理編輯的片段具有編輯選取的內容( ![iconeditselectedcontent](assets/iconeditselectedcontent.png))圖示。 點選「編輯選取的內容」圖示，以在編輯模式中啟動片段，並在其中進行變更。 使用下列選項來格式化和管理文本：

   * [格式選項](#formattingtext)

      * [從其他應用程式複製貼上格式化文本](#pasteformattedtext)
      * [突出顯示部分文本](#highlightemphasize)
   * [特殊字元](#specialcharacters)
   * [鍵盤快速鍵](/help/forms/using/keyboard-shortcuts.md)

   有關代理用戶介面中各種文檔片段可用操作的詳細資訊，請參見 [代理用戶介面中可用的操作和資訊](#actionsagentui).

1. 要將分頁符添加到互動式通信的打印輸出中，請將游標放在要插入分頁符的位置，並選擇「分頁前」或「分頁後」( ![pagebreakbefore](assets/pagebreakbeforeafter.png))。

   在互動式通訊中插入明確的分頁符預留位置。 要查看顯式分頁符對互動式通信的影響，請參閱打印預覽。

   ![explocipagebreak](assets/explicitpagebreak.png)

   繼續管理互動式通信的附件。

### 管理附件 {#manage-attachments}

1. 選擇 **[!UICONTROL 附件]**. Agent UI將按建立互動式通信時設定的方式顯示可用附件。

   通過點選視圖表徵圖，您可以選擇不連同互動式通信一起提交附件，並且可以點選附件中的十字以從互動式通信中刪除附件（如果允許代理刪除或隱藏附件）。 對於在建立互動式通信時指定為強制的附件，將禁用「查看」和「刪除」表徵圖。

   ![附件代理](assets/attachmentsagentui.png)

1. 點選程式庫存取( ![程式庫存取](assets/libraryaccess.png))圖示來存取「內容資料庫」 ，以插入DAM資產作為附件。

   >[!NOTE]
   >
   >只有在建立互動式通訊時已啟用程式庫存取（位於列印管道的「檔案容器」屬性中）時，才可使用「程式庫存取」圖示。

1. 如果建立「互動式通信」時未鎖定附件的順序，則可以通過選擇附件並點選向下和向上箭頭來重新排序附件。
1. 使用「Web預覽」和「打印預覽」，查看兩個輸出是否符合您的要求。

   如果您發現預覽結果令人滿意，請點選 **[!UICONTROL 提交]** 提交/將互動式通訊傳送至貼文程式。 或者，若要進行變更，請退出預覽，返回進行變更。

## 格式化文字 {#formattingtext}

在代理UI中編輯文字片段時，工具列會根據您選擇進行的編輯類型而變更：字型、段落或清單：

![typeofformatting工具欄](assets/typeofformattingtoolbar.png) ![字型工具列](do-not-localize/fonttoolbar.png)

字型工具列

![段落工具欄](do-not-localize/paragraphtoolbar.png)

段落工具欄

![清單工具列](do-not-localize/listtoolbar.png)

清單工具列

### 加亮/強調部分文本 {#highlightemphasize}

要突出顯示/強調可編輯片段中的部分文本，請選擇文本並點選「突出顯示顏色」。

![highlighttextagentui](assets/highlighttextagentui.png)

### 貼上格式化文字 {#pasteformattedtext}

![貼文文字](assets/pastedtext.png)

### 在文本中插入特殊字元 {#specialcharacters}

代理UI內建支援210個特殊字元。 管理員可 [新增支援更多/自訂特殊字元，可依自訂](/help/forms/using/custom-special-characters.md).

#### 附件傳送 {#attachmentdelivery}

* 使用伺服器端API呈現互動式或非互動式PDF時，呈現的PDF會包含附件作為PDF附件。
* 使用代理UI將與互動式通訊相關聯的後置程式載入為提交的一部分時，附件會以清單的形式傳遞&lt;com.adobe.idp.document> inAttachmentDocs參數。
* 傳遞機制工作流程（例如電子郵件和列印）也會傳送附件以及互動式通訊的PDF版本。

## 代理用戶介面中可用的操作和資訊 {#actionsagentui}

### 檔案片段 {#document-fragments}

![](do-not-localize/contentoptionsdocfragments.png)

* **向上/向下箭頭**:在互動式通訊中向上或向下移動檔案片段的箭頭。
* **刪除**:如果允許，請從「交互通信」中刪除文檔片段。
* **分頁前** （適用於目標區域的子片段）:在文檔片段前插入分頁符。
* **縮進**:增加或減少文檔片段的縮進。
* **後斷頁** （適用於目標區域的子片段）:在文檔片段後插入分頁符。

![docfragoptions](assets/docfragoptions.png)

* 編輯（僅限文字片段）:開啟RTF編輯器以編輯文字檔案片段。 如需詳細資訊，請參閱 [格式化文字](#formattingtext).

* 選擇（眼睛表徵圖）:包括\排除互動式通信中的文檔片段。
* 未填充的值（資訊）:指示文檔片段中未填充的變數的數量。

### 列出文檔片段 {#list-document-fragments}

![listoptions](assets/listoptions.png)

* 插入空白行：插入新的空行。
* 選擇（眼睛表徵圖）:包括\排除互動式通信中的文檔片段。
* 跳過項目符號/編號：啟用以跳過清單文檔片段中的項目符號/編號。
* 未填充的值（資訊）:指示文檔片段中未填充的變數的數量。

## 將互動式通訊儲存為草稿 {#save-as-draft}

您可以使用代理UI為每個互動式通訊儲存一或多個草稿，並稍後擷取草稿以繼續處理。 您可以為每個草稿指定不同的名稱以加以識別。

Adobe建議依序執行這些指示，以成功將互動式通訊儲存為草稿。

### 啟用另存為草稿功能 {#before-save-as-draft}

預設情況下，「另存為草稿」(Save as a Draft)功能未啟用。 執行下列步驟以啟用功能：

1. 實作 [ccrDocumentInstance](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/ccr/ccrDocumentInstance/api/services/CCRDocumentInstanceService.html) 服務提供商介面(SPI)。

   SPI可讓您將互動式通訊的草稿版本以草稿ID作為唯一識別碼，儲存至資料庫。 這些指示假設您先前已了解如何使用Maven專案建立OSGi套件組合。

   如需範例SPI實作，請參閱 [示例ccrDocumentInstance SPI實施](#sample-ccrDocumentInstance-spi).
1. 開啟 `http://<hostname>:<port>/ system/console/bundles` 點選 **[!UICONTROL 安裝/更新]** 上傳OSGi套件組合。 確認上傳套件的狀態顯示為 **作用中**. 如果包的狀態未顯示為 **作用中**.
1. 前往 `https://'[server]:[port]'/system/console/configMgr`.
1. 點選 **[!UICONTROL 建立通信配置]**.
1. 選擇 **[!UICONTROL 使用CCRDocumentInstanceService啟用儲存]** 點選 **[!UICONTROL 儲存]**.

### 將互動式通訊儲存為草稿 {#save-as-draft-agent-ui}

執行下列步驟將互動式通訊儲存為草稿：

1. 在Forms Manager中選取互動式通訊，然後點選 **[!UICONTROL 開啟代理UI]**.

1. 在代理程式UI中進行適當的變更，然後點選 **[!UICONTROL 另存為草稿]**.

1. 指定 **[!UICONTROL 名稱]** 欄位和點選 **[!UICONTROL 完成]**.

將「互動式通訊」儲存為草稿後，請點選 **[!UICONTROL 儲存變更]** 以保存對草稿的任何進一步更改。

### 檢索互動式通信的草稿 {#retrieve-draft}

將互動式通訊儲存為草稿後，您可以擷取它以繼續處理。 使用以下內容檢索互動式通信：

`https://server:port/aem/forms/createcorrespondence.hmtl?draftid=[draftid]`

[draftid] 是指將互動式通訊儲存為草稿後產生的草稿版本唯一識別碼。

### 示例ccrDocumentInstance SPI實施 {#sample-ccrDocumentInstance-spi}

實作 `ccrDocumentInstance` SPI將互動式通訊儲存為草稿。 以下是的範例實作 `ccrDocumentInstance` SPI。

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

此 `save`, `update`, `get`，和 `getAll` 操作調用資料庫服務以將互動式通信另存為草稿、更新互動式通信、從資料庫中檢索資料以及檢索資料庫中所有可用互動式通信的資料。 此範例使用 `mySQLDataBaseServiceCRUD` 作為資料庫服務的名稱。

下表說明範例 `ccrDocumentInstance` SPI實作。 這說明 `save`, `update`, `get`，和 `getAll` 操作調用示例實施中的資料庫服務。

<table> 
 <tbody>
 <tr>
  <td><p><strong>作業</strong></p></td>
  <td><p><strong>資料庫服務示例</strong></p></td> 
   </tr>
  <tr>
   <td><p>您可以建立互動式通訊的草稿，或直接提交。 儲存操作的API會檢查互動式通訊是否以草稿形式提交，且包含草稿名稱。 然後，API會以「儲存」作為輸入方法來呼叫mySQLDataBaseServiceCRUD服務。</p></br><img src="assets/save-as-draft-save-operation.png"/></br>[#$sd1_sf1_dp9]</td>
   <td><p>mySQLDataBaseServiceCRUD服務驗證「另存為」作為輸入方法，並生成自動生成的草稿ID並將其返回到AEM。 產生草稿ID的邏輯可能因資料庫而異。</p></br><img src="assets/save-operation-service.png"/></br>[#$sd1_sf1_dp13]</td>
   </tr>
  <tr>
   <td><p>更新操作的API將檢索互動式通信草稿的狀態，並檢查互動式通信是否包含草稿名稱。 API調用mySQLDataBaseServiceCRUD服務以更新資料庫中的該狀態。</p></br><img src="assets/save-as-draft-update-operation.png"/></br>[#$sd1_sf1_dp17]</td>
   <td><p>mySQLDataBaseServiceCRUD服務驗證Update作為輸入方法，並將Interactive Communication草稿的狀態保存在資料庫中。</br></p><img src="assets/update-operation-service.png"/></td>
   </tr>
   <tr>
   <td><p>get操作的API會檢查互動式通訊是否包含草稿ID。 然後，API調用mySQLDataBaseServiceCRUD服務，使用Get作為輸入方法來檢索互動式通信的資料。</br></p><img src="assets/save-as-draft-get-operation.png"/></td>
   <td><p>mySQLDataBaseServiceCRUD服務驗證Get作為輸入方法，並基於草稿ID檢索互動式通信的資料。</p></br><img src="assets/get-operation-service.png"/></br>[#$sd1_sf1_dp29]</td>
   </tr>
   <tr>
   <td><p>getAll操作的API調用mySQLGetALLData服務，以檢索儲存在資料庫中的所有互動式通信的資料。</br></p><img src="assets/save-as-draft-getall-operation.png"/></td>
   <td><p>mySQLGetALLData服務檢索儲存在資料庫中的所有互動式通信的資料。</p></br><img src="assets/getall-operation-service.png"/></br>[#$sd1_sf1_dp37]</td>
   </tr>
  </tbody>
</table>

以下是 `pom.xml` 屬於實作的檔案：

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
>請確定您更新 `aemfd-client-sdk` 依存於6.0.160 `pom.xml` 檔案。
