---
title: 將草稿和提交元件與資料庫整合的示例
seo-title: 將草稿和提交元件與資料庫整合的示例
description: 參考自訂資料和中繼資料服務的實作，將草稿和提交元件與資料庫整合。
seo-description: 參考自訂資料和中繼資料服務的實作，將草稿和提交元件與資料庫整合。
uuid: ccdb900e-2c2e-4ed3-8a88-5c97aa0092a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: da96d3d8-a338-470a-8d20-55ea39bd15bf
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 1%

---


# 將草稿和提交元件與資料庫{#sample-for-integrating-drafts-submissions-component-with-database}整合的示例

## 範例概述{#sample-overview}

AEM Forms Portal草稿和提交元件可讓使用者將表單儲存為草稿，並稍後從任何裝置提交。 此外，使用者也可以在入口網站上檢視其提交的表單。 為啟用此功能，AEM Forms提供資料和中繼資料服務，以儲存使用者填入的表單資料，以及與草稿和提交表單相關的表單中繼資料。 預設情況下，此資料儲存在CRX儲存庫中。 不過，當使用者透過AEM發佈例項與表單互動時（通常位於企業防火牆外），企業組織可能會想要自訂資料儲存，以提高其安全性和可靠性。

本檔案討論的範例是自訂資料和中繼資料服務的參考實作，以整合草稿和提交元件與資料庫。 示例實施中使用的資料庫為&#x200B;**MySQL 5.6.24**。 不過，您可以將草稿和提交元件整合到您選擇的任何資料庫。

>[!NOTE]
>
>* 本文檔中說明的示例和配置是根據MySQL 5.6.24進行的，您必須將它們適當地替代到資料庫系統。
>* 請確定您已安裝最新版的AEM Forms附加元件套件。 如需可用套件的清單，請參閱[AEM Forms releases](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)文章。
>* 範例套件僅能與Adaptive Forms提交動作搭配使用。


## 設定並配置示例{#set-up-and-configure-the-sample}

對所有作者和發佈實例執行以下步驟以安裝和配置示例：

1. 將下列&#x200B;**aem-fp-db-integration-sample-pkg-6.1.2.zip**&#x200B;套件下載至您的檔案系統。

   資料庫整合示例包

   [取得檔案](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. 前往https://[*host*]&#x200B;的AEM封裝管理器：[*port*]/crx/packmgr/。
1. 按一下&#x200B;**[!UICONTROL Upload Package]**。

1. 瀏覽以選擇&#x200B;**aem-fp-db-integration-sample-pkg-6.1.2.zip**&#x200B;套件，然後按一下&#x200B;**[!UICONTROL OK]**。
1. 按一下軟體包旁的&#x200B;**[!UICONTROL Install]**&#x200B;以安裝軟體包。
1. 前往&#x200B;**[!UICONTROL AEM Web Console Configuration]**
https://[*host*]:[*port*]/system/console/configMgr的頁面。
1. 按一下以編輯模式開啟&#x200B;**[!UICONTROL Forms Portal Draft and Submission Configuration]**。

1. 指定屬性的值，如下表所述：

   | **屬性** | **說明** | **值** |
   |---|---|---|
   | Forms Portal草稿資料服務 | 草稿資料服務的識別碼 | formsportal.sampledataservice |
   | Forms Portal草稿中繼資料服務 | 草稿中繼資料服務的識別碼 | formsportal.samplemetadataservice |
   | Forms Portal提交資料服務 | 用於提交資料服務的標識符 | formsportal.sampledataservice |
   | Forms Portal提交中繼資料服務 | 用於提交元資料服務的標識符 | formsportal.samplemetadataservice |
   | Forms Portal擱置中的Sign Data Service | 待定Sign資料服務的識別碼 | formsportal.sampledataservice |
   | Forms Portal擱置中的Sign中繼資料服務 | 待審Sign中繼資料服務的識別碼 | formsportal.samplemetadataservice |

   >[!NOTE]
   >
   >這些服務通過其名稱解析，這些名稱被提及為`aem.formsportal.impl.prop`鍵的值，如下所示：

   ```java
   @Service(value = {SubmitDataService.class, DraftDataService.class})
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.sampledataservice")
   @Service(value = { SubmitMetadataService.class, DraftMetadataService.class })
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.samplemetadataservice")
   ```

   您可以變更資料和中繼資料表格的名稱。

   要為元資料表提供不同的名稱：

   * 在「Web控制台配置」中，尋找並按一下「表單入口網站中繼資料服務範例實作」。 您可以變更資料來源、中繼資料／其他中繼資料表格名稱的值。

   要為資料表提供不同的名稱：

   * 在Web控制台配置中，查找並按一下表單門戶資料服務示例實施。 您可以變更資料來源和資料表格名稱的值。
   >[!NOTE]
   >
   >如果您變更表格名稱，請在表單入口網站設定中提供表格名稱。

1. 保持其他配置不變，然後按一下&#x200B;**[!UICONTROL 保存]**。

1. 資料庫連線可透過Apache Sling Connection Pooled Data Sources完成。
1. 若是Apache Sling連線，請尋找並按一下以編輯模式在Web Console設定中開啟&#x200B;**[!UICONTROL Apache Sling Connection Pooled DataSource]**。 指定屬性的值，如下表所述：

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>值</strong></td>
  </tr>
  <tr>
   <td>資料來源名稱</td>
   <td><p>用於從資料源池過濾驅動程式的資料源名稱</p> <p><strong>注意： </strong><em>範例實作使用FormsPortal作為資料來源名稱。</em></p> </td>
  </tr>
  <tr>
   <td>JDBC驅動程式類</td>
   <td>com.mysql.jdbc.Driver</td>
  </tr>
  <tr>
   <td>JDBC連接URI<br /> </td>
   <td>jdbc:mysql://[<em>host</em>]:[<em>port</em>]/[<em>schema_name</em>]</td>
  </tr>
  <tr>
   <td>使用者名稱</td>
   <td>對資料庫表進行驗證和執行操作的用戶名</td>
  </tr>
  <tr>
   <td>密碼</td>
   <td>與用戶名關聯的密碼</td>
  </tr>
  <tr>
   <td>事務隔離</td>
   <td>READ_COMMITTED</td>
  </tr>
  <tr>
   <td>最大活動連接數</td>
   <td>1000</td>
  </tr>
  <tr>
   <td>最大空閒連接數</td>
   <td>100</td>
  </tr>
  <tr>
   <td>最小空閒連接數</td>
   <td>10</td>
  </tr>
  <tr>
   <td>初始大小</td>
   <td>10</td>
  </tr>
  <tr>
   <td>最大等待</td>
   <td>100000</td>
  </tr>
  <tr>
   <td>借閱測試</td>
   <td>已核取</td>
  </tr>
  <tr>
   <td>空閒時測試</td>
   <td>已核取</td>
  </tr>
  <tr>
   <td>驗證查詢</td>
   <td>示例值包括SELECT 1(mysql)、從dual(oracle)中選擇1、SELECT 1(MS Sql Server)(validationQuery)</td>
  </tr>
  <tr>
   <td>驗證查詢超時</td>
   <td>10000</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
> * 示例中未提供MySQL的JDBC驅動程式。 確保已為其設定並提供配置JDBC連接池所需的資訊。
> * 指向您的作者和發佈例項，以使用相同的資料庫。 對於所有作者和發佈實例，JDBC連接URI欄位的值必須相同。

>



1. 保持其他配置不變，然後按一下&#x200B;**[!UICONTROL 保存]**。

1. 如果資料庫模式中已有表，請跳至下一步。

   否則，如果資料庫架構中沒有表，請執行以下SQL陳述式，以為資料、元資料和資料庫架構中的其他元資料建立單獨的表：

   >[!NOTE]
   >
   >作者和發佈例項不需要不同的資料庫。 在所有作者和發佈例項上使用相同的資料庫。

   **資料表的SQL陳述式**

   ```sql
   CREATE TABLE `data` (
   `owner` varchar(255) DEFAULT NULL,
   `data` longblob,
   `metadataId` varchar(45) DEFAULT NULL,
   `id` varchar(45) NOT NULL,
   PRIMARY KEY (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **元資料表的SQL陳述式**

   ```sql
   CREATE TABLE `metadata` (
   `formPath` varchar(1000) DEFAULT NULL,
   `formType` varchar(100) DEFAULT NULL,
   `description` text,
   `formName` varchar(255) DEFAULT NULL,
   `owner` varchar(255) DEFAULT NULL,
   `enableAnonymousSave` varchar(45) DEFAULT NULL,
   `renderPath` varchar(1000) DEFAULT NULL,
   `nodeType` varchar(45) DEFAULT NULL,
   `charset` varchar(45) DEFAULT NULL,
   `userdataID` varchar(45) DEFAULT NULL,
   `status` varchar(45) DEFAULT NULL,
   `formmodel` varchar(45) DEFAULT NULL,
   `markedForDeletion` varchar(45) DEFAULT NULL,
   `showDorClass` varchar(255) DEFAULT NULL,
   `sling:resourceType` varchar(1000) DEFAULT NULL,
   `attachmentList` longtext,
   `draftID` varchar(45) DEFAULT NULL,
   `submitID` varchar(45) DEFAULT NULL,
   `id` varchar(60) NOT NULL,
   `profile` varchar(255) DEFAULT NULL,
   `submitUrl` varchar(1000) DEFAULT NULL,
   `xdpRef` varchar(1000) DEFAULT NULL,
   `agreementId` varchar(255) DEFAULT NULL,
   `nextSigners` varchar(255) DEFAULT NULL,
   `eSignStatus` varchar(45) DEFAULT NULL,
   `pendingSignID` varchar(45) DEFAULT NULL,
   `agreementDataId` varchar(255) DEFAULT NULL,
   `enablePortalSubmit` varchar(45) DEFAULT NULL,
   `submitType` varchar(45) DEFAULT NULL,
   `dataType` varchar(45) DEFAULT NULL,
   `jcr:lastModified` varchar(45) DEFAULT NULL,
   PRIMARY KEY (`id`),
   UNIQUE KEY `ID_UNIQUE` (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **SQL陳述式for additionalmetadatatable**

   ```sql
   CREATE TABLE `additionalmetadatatable` (
   `value` text,
   `key` varchar(255) NOT NULL,
   `id` varchar(60) NOT NULL,
   PRIMARY KEY (`id`,`key`),
   CONSTRAINT ‘additionalmetadatatable_fk’ FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   **注釋表的SQL陳述式**

   ```sql
   CREATE TABLE `commenttable` (
   `commentId` varchar(255) DEFAULT NULL,
   `comment` text DEFAULT NULL,
   `ID` varchar(255) DEFAULT NULL,
   `commentowner` varchar(255) DEFAULT NULL,
   `time` varchar(255) DEFAULT NULL);
   ```

1. 如果資料庫模式中已經有表（資料、元資料和其他元資料表），請執行以下更改表查詢：

   **用於更改資料表的SQL陳述式**

   ```sql
   ALTER TABLE `data` CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   **用於更改元資料表的SQL陳述式**

   ```sql
   ALTER TABLE metadata add markedForDeletion varchar(45) DEFAULT NULL
   ```

   >[!NOTE]
   >
   >如果您已經運行ALTER TABLE元資料添加查詢，並且表中存在markedforDeletion列，則該查詢將失敗。

   ```sql
   ALTER TABLE metadata add agreementId varchar(255) DEFAULT NULL,
   add nextSigners varchar(255) DEFAULT NULL,
   add eSignStatus varchar(45) DEFAULT NULL,
   add pendingSignID varchar(45) DEFAULT NULL,
   add agreementDataId varchar(255) DEFAULT NULL,
   add enablePortalSubmit varchar(45) DEFAULT NULL,
   add submitType varchar(45) DEFAULT NULL,
   add dataType varchar(45) DEFAULT NULL;
   ```

   ```sql
   ALTER TABLE `metadata` CHANGE `formPath` `formPath` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `formType` `formType` VARCHAR(100) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `description` `description` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `formName` `formName` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `renderPath` `renderPath` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `showDorClass` `showDorClass` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `sling:resourceType` `sling:resourceType` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `profile` `profile` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `submitUrl` `submitUrl` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
   CHANGE `xdpRef` `xdpRef` VARCHAR(1000) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   **用於更改附加的additionalmetadatatable表的SQL陳述式**

   ```sql
   ALTER TABLE `additionalmetadatatable` CHANGE `value` `value` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL, CHANGE `key` `key` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL;
   ```

現在已設定範例實作，您可使用此範例來列出草稿和提交，同時將所有資料和中繼資料儲存在資料庫中。 現在，讓我們來看看資料和中繼資料服務在範例中的設定方式。

## 安裝mysql-connector-java-5.1.39-bin.jar檔案{#install-mysql-connector-java-bin-jar-file}

對所有作者和發佈實例執行以下步驟以安裝mysql-connector-java-5.1.39-bin.jar檔案：

1. 導覽至`https://'[server]:[port]'/system/console/depfinder`並搜尋com.mysql.jdbc套件。
1. 在「導出者」(Exported by)列中，檢查軟體包是否由任何包導出。

   如果軟體包未由任何包導出，請繼續。

1. 導覽至`https://'[server]:[port]'/system/console/bundles`，然後按一下&#x200B;**[!UICONTROL 安裝／更新]**。
1. 按一下&#x200B;**[!UICONTROL 選擇檔案]**&#x200B;並瀏覽以選擇mysql-connector-java-5.1.39-bin.jar檔案。 此外，選擇「啟動Bundle ]**」和「刷新包]**」複選框。**[!UICONTROL **[!UICONTROL 
1. 按一下&#x200B;**[!UICONTROL 安裝或更新]**。 完成後，重新啟動伺服器。
1. （*僅限Windows*）關閉作業系統的系統防火牆。

## 表單入口資料和中繼資料服務的范常式式碼{#sample-code-for-forms-portal-data-and-metadata-service}

以下zip包含`FormsPortalSampleDataServiceImpl`和`FormsPortalSampleMetadataServiceImpl`（實作類別），用於資料和中繼資料服務介面。 此外，它包含編譯上述實作類所需的所有類。

[取得檔案](assets/sample_package.zip)

## 驗證檔案名{#verify-length-of-the-file-name}的長度

Forms Portal的資料庫實作會使用其他中繼資料表格。 該表具有基於表的Key和id列的複合主鍵。 MySQL允許主鍵長度高達255個字元。 您可以使用下列用戶端驗證指令碼來驗證檔案介面工具集所附加的檔案名稱長度。 驗證會在附加檔案時執行。 以下過程中提供的指令碼在檔案名大於150（包括副檔名）時顯示一條消息。 您可以修改指令碼以檢查其中是否有不同數量的字元。

執行以下步驟以建立[客戶端庫](/help/sites-developing/clientlibs.md)並使用指令碼：

1. 登入CRXDE並導覽至/etc/clientlibs/
1. 建立類型&#x200B;**cq:ClientLibraryFolder**&#x200B;的節點，並提供該節點的名稱。 例如，`validation`。

   按一下&#x200B;**[!UICONTROL 保存全部]**。

1. 按一下右鍵該節點，按一下&#x200B;**[!UICONTROL 建立新檔案]**，然後建立副檔名為。txt的檔案。 例如，`js.txt`將下列程式碼新增至新建立的。txt檔案，然後按一下「全部儲存」。]****[!UICONTROL 

   ```javascript
   #base=util
    util.js
   ```

   在上述代碼中，`util`是資料夾的名稱，`util.js`是`util`資料夾中檔案的名稱。 `util`資料夾和`util.js`檔案是按照以下步驟建立的。

1. 按一下右鍵在步驟2中建立的`cq:ClientLibraryFolder`節點，選擇「建立」>「建立資料夾」。 建立名為`util`的資料夾。 按一下&#x200B;**[!UICONTROL 保存全部]**。 按一下右鍵`util`資料夾，選擇「建立」>「建立檔案」。 建立名為`util.js`的檔案。 按一下&#x200B;**[!UICONTROL 保存全部]**。

1. 將下列代碼添加到util.js檔案中，然後按一下&#x200B;**[!UICONTROL 保存所有]**。 代碼驗證檔案名的長度。

   ```javascript
   /*
    * ADOBE CONFIDENTIAL
    * ___________________
    *
    * Copyright 2016 Adobe Systems Incorporated
    * All Rights Reserved.
    *
    * NOTICE:  All information contained herein is, and remains
    * the property of Adobe Systems Incorporated and its suppliers,
    * if any.  The intellectual and technical concepts contained
    * herein are proprietary to Adobe Systems Incorporated and its
    * suppliers and may be covered by U.S. and Foreign Patents,
    * patents in process, and are protected by trade secret or copyright law.
    * Dissemination of this information or reproduction of this material
    * is strictly forbidden unless prior written permission is obtained
    * from Adobe Systems Incorporated.
    *
    */
   (function () {
       var connectWithGuideBridge = function (gb) {
           gb.connect(function () {
               //For first time load
               window.guideBridge.on("elementValueChanged" , function(event, payload) {
           var component = payload.target; // Field whose value has changed
                   if(component.name == 'fileAttachment' && component.parent) {
                       var fileItems = $('#'+payload.target.parent.id).find(".guide-fu-fileItem");
                       for (i = 0;i<fileItems.length;i++) {
                           var filename = $(fileItems[i]).find(".guide-fu-fileName").text();
                           //check whether it is previously attached file or a newly  attached one
                           if(filename.length > 150 && filename.indexOf("fp.attach.jsp") < 0) {
                               window.alert("filename is larger than 150 : "+filename);
                                $(fileItems[i]).find(".guide-fu-fileClose.close").click();
                           }
                       }
                   }
   
      });
           });
       };
   
       if (window.guideBridge) {
           connectWithGuideBridge(window.guideBridge);
       } else {
           window.addEventListener("bridgeInitializeStart", function (event) {
               connectWithGuideBridge(event.detail.guideBridge);
           });
       }
   })();
   ```

   >[!NOTE]
   >
   >此指令碼是開箱即用(OOTB)附件Widget元件。 如果您已自訂OOTB附件介面工具集，請變更上述指令碼以合併個別變更。

1. 將下列屬性新增至步驟2中建立的資料夾，然後按一下「全部儲存」。****

   * **[!UICONTROL 名稱：類]** 別

   * **[!UICONTROL 類型：字]** 串

   * **[!UICONTROL 值：]** fp.validation

   * **[!UICONTROL 多選項：啟]** 用

1. 導覽至`/libs/fd/af/runtime/clientlibs/guideRuntime`，並將`fp.validation`值附加至embed屬性。

1. 導覽至/libs/fd/af/runtime/clientlibs/guideRuntimeWithXFA，並將`fp.validation`值附加至embed屬性。

   >[!NOTE]
   >
   >如果您使用自訂用戶端程式庫，而非guideRuntime和guideRuntimeWithXfa用戶端程式庫，請使用類別名稱，將在此程式中建立的用戶端程式庫內嵌至您在執行時期載入的自訂程式庫。

1. 按一下「全部儲存」。**** 現在，當檔案名稱大於150（包括副檔名）字元時，會顯示訊息。

