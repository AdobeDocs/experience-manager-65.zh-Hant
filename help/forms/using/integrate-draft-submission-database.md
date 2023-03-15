---
title: 將草稿和提交元件與資料庫整合的範例
seo-title: Sample for integrating drafts & submissions component with database
description: 參考自訂資料和中繼資料服務的實作，以整合草稿和提交元件與資料庫。
seo-description: Reference implementation of customized data and metadata services to integrate drafts and submissions component with a database.
uuid: ccdb900e-2c2e-4ed3-8a88-5c97aa0092a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: da96d3d8-a338-470a-8d20-55ea39bd15bf
exl-id: 2e4f8f51-df02-4bbb-99bb-30181facd1e0
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '1467'
ht-degree: 1%

---

# 將草稿和提交元件與資料庫整合的範例 {#sample-for-integrating-drafts-submissions-component-with-database}

## 範例概觀 {#sample-overview}

AEM Forms portal草稿和提交元件可讓使用者將表單儲存為草稿，並稍後從任何裝置提交。 此外，使用者也可以在入口網站上檢視其提交的表單。 為了啟用此功能，AEM Forms提供資料和中繼資料服務，將使用者填入的資料儲存在表單中，以及與草稿和已提交表單相關聯的表單中繼資料。 預設情況下，此資料會儲存在CRX存放庫中。 不過，當使用者透過AEM發佈例項與表單互動時（通常不在企業防火牆之外），組織可能會想要自訂資料儲存，以提高安全性和可靠性。

本檔案中討論的範例是自訂資料和中繼資料服務的參考實作，以將草稿和提交元件與資料庫整合。 範例實作中使用的資料庫為 **MySQL 5.6.24**. 不過，您可以將草稿和提交元件與您選擇的任何資料庫整合。

>[!NOTE]
>
>* 本文檔中解釋的示例和配置是根據MySQL 5.6.24進行的，您必須將它們適當替換為資料庫系統。
>* 請確定您已安裝最新版的AEM Forms附加元件套件。 如需可用套件的清單，請參閱 [AEM Forms版本](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 文章。
>* 範例套件僅適用於適用性Forms提交動作。


## 設定範例 {#set-up-and-configure-the-sample}

在所有製作和發佈執行個體上執行下列步驟，以安裝和設定範例：

1. 下載下列 **aem-fp-db-integration-sample-pkg-6.1.2.zip** 封裝至您的檔案系統。

   資料庫整合的示例包

[取得檔案](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. 前往AEM套件管理器，網址為https://[*主機*]:[*埠*]/crx/packmgr/。
1. 按一下 **[!UICONTROL 上傳套件]**.

1. 瀏覽以選取 **aem-fp-db-integration-sample-pkg-6.1.2.zip** 封裝，按一下 **[!UICONTROL 確定]**.
1. 按一下 **[!UICONTROL 安裝]** ，即可安裝套件。
1. 前往 **[!UICONTROL AEM Web主控台設定]**
https://[*主機*]:[*埠*]/system/console/configMgr。
1. 按一下以開啟 **[!UICONTROL Forms入口網站草稿和提交設定]** 在編輯模式中。

1. 指定屬性的值，如下表所述：

   | **屬性** | **說明** | **值** |
   |---|---|---|
   | Forms入口網站草稿資料服務 | 草稿資料服務的識別碼 | formsportal.sampledataservice |
   | Forms入口網站草稿中繼資料服務 | 草稿元資料服務的識別碼 | formsportal.samplemetadataservice |
   | Forms Portal提交資料服務 | 提交資料服務的標識符 | formsportal.sampledataservice |
   | Forms Portal提交中繼資料服務 | 提交元資料服務的標識符 | formsportal.samplemetadataservice |
   | Forms Portal待簽署資料服務 | 掛起簽名資料服務的標識符 | formsportal.sampledataservice |
   | Forms Portal擱置中的簽署中繼資料服務 | 待定簽名元資料服務的標識符 | formsportal.samplemetadataservice |

   >[!NOTE]
   >
   >這些服務會由其名稱解析，其名稱提及為 `aem.formsportal.impl.prop` 索引鍵如下：

   ```java
   @Service(value = {SubmitDataService.class, DraftDataService.class})
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.sampledataservice")
   @Service(value = { SubmitMetadataService.class, DraftMetadataService.class })
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.samplemetadataservice")
   ```

   您可以變更資料和中繼資料表格的名稱。

   要為元資料表提供不同的名稱：

   * 在「Web主控台設定」中，尋找並按一下「Forms入口網站中繼資料服務實作範例」。 您可以變更資料來源、中繼資料/其他中繼資料表格名稱的值。

   要為資料表提供不同的名稱：

   * 在Web主控台設定中，尋找並按一下Forms Portal資料服務實作範例。 您可以變更資料來源和資料表格名稱的值。
   >[!NOTE]
   >
   >如果您變更表格名稱，請在「表單入口網站」設定中提供這些名稱。

1. 保留其他設定原樣，然後按一下 **[!UICONTROL 儲存]**.

1. 資料庫連線可透過Apache Sling Connection Pooled Data Source完成。
1. 若為Apache Sling連線，請尋找並按一下以開啟 **[!UICONTROL Apache Sling Connection Pooled DataSource]** 在「Web控制台配置」的編輯模式下。 指定屬性的值，如下表所述：

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>值</strong></td>
  </tr>
  <tr>
   <td>資料源名稱</td>
   <td><p>用於從資料源池中篩選驅動程式的資料源名稱</p> <p><strong>注意： </strong><em>實作範例使用FormsPortal做為資料來源名稱。</em></p> </td>
  </tr>
  <tr>
   <td>JDBC驅動程式類</td>
   <td>com.mysql.jdbc.Driver</td>
  </tr>
  <tr>
   <td>JDBC連接URI<br /> </td>
   <td>jdbc:mysql://[<em>主機</em>]:[<em>埠</em>]/[<em>schema_name</em>]</td>
  </tr>
  <tr>
   <td>使用者名稱</td>
   <td>對資料庫表進行身份驗證和執行操作的用戶名</td>
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
   <td>最小空閒連接</td>
   <td>10</td>
  </tr>
  <tr>
   <td>初始大小</td>
   <td>10</td>
  </tr>
  <tr>
   <td>等待次數上限</td>
   <td>100000</td>
  </tr>
  <tr>
   <td>借閱時測試</td>
   <td>已核取</td>
  </tr>
  <tr>
   <td>空閒時測試</td>
   <td>已核取</td>
  </tr>
  <tr>
   <td>驗證查詢</td>
   <td>示例值為SELECT 1(mysql)、從dual(oracle)中選擇1、SELECT 1(MS Sql Server)(validationQuery)</td>
  </tr>
  <tr>
   <td>驗證查詢超時</td>
   <td>10000</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* 示例中未提供MySQL的JDBC驅動程式。 請確保已為其進行了配置，並提供配置JDBC連接池所需的資訊。
>* 指向您的製作和發佈執行個體以使用相同的資料庫。 所有製作和發佈實例的JDBC連接URI欄位值必須相同。


1. 保留其他設定原樣，然後按一下 **[!UICONTROL 儲存]**.

1. 如果資料庫架構中已有表，請跳到下一步。

   否則，如果資料庫架構中沒有表，請執行以下SQL陳述式，為資料、元資料和資料庫架構中的其他元資料建立單獨的表：

   >[!NOTE]
   >
   >製作和發佈例項不需要不同的資料庫。 在所有製作和發佈執行個體上使用相同的資料庫。

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

   **其他元資料表的SQL陳述式**

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

1. 如果資料庫架構中已有表（資料、元資料和其他元資料表），請執行以下更改表查詢：

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
   >如果您已執行ALTER TABLE中繼資料新增查詢，且表格中存在marketdforDeletion欄，則該查詢會失敗。

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

   **用於更改additionalmetadatatable表的SQL陳述式**

   ```sql
   ALTER TABLE `additionalmetadatatable` CHANGE `value` `value` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL, CHANGE `key` `key` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL;
   ```

現在已設定範例實作，您可以用來列出草稿和提交，同時將所有資料和中繼資料儲存在資料庫中。 現在來查看範例中資料和中繼資料服務的設定方式。

## 安裝mysql-connector-java-5.1.39-bin.jar檔案 {#install-mysql-connector-java-bin-jar-file}

在所有製作執行個體和發佈執行個體上執行下列步驟，以安裝mysql-connector-java-5.1.39-bin.jar檔案：

1. 導覽至 `https://'[server]:[port]'/system/console/depfinder` 並搜索com.mysql.jdbc包。
1. 在「匯出依據」欄中，檢查套件是否由任何套件匯出。

   如果包未由任何包導出，請繼續。

1. 導覽至 `https://'[server]:[port]'/system/console/bundles` 按一下 **[!UICONTROL 安裝/更新]**.
1. 按一下 **[!UICONTROL 選擇檔案]** 並瀏覽以選擇mysql-connector-java-5.1.39-bin.jar檔案。 此外，請選取 **[!UICONTROL 開始套件組合]** 和 **[!UICONTROL 刷新包]** 複選框。
1. 按一下 **[!UICONTROL 安裝或更新]**. 完成後，重新啟動伺服器。
1. (*僅限Windows*)關閉作業系統的系統防火牆。

## 表單入口網站資料和中繼資料服務的范常式式碼 {#sample-code-for-forms-portal-data-and-metadata-service}

下列zip包含 `FormsPortalSampleDataServiceImpl` 和 `FormsPortalSampleMetadataServiceImpl` （實作類別），用於資料和中繼資料服務介面。 此外，它包含編譯上述實施類所需的所有類。

[取得檔案](assets/sample_package.zip)

## 驗證檔案名的長度  {#verify-length-of-the-file-name}

Forms Portal的資料庫實作使用其他中繼資料表格。 該表具有基於表的「鍵」和「id」列的複合主鍵。 MySQL允許主鍵長達255個字元。 您可以使用下列用戶端驗證指令碼來驗證附加至檔案介面工具集的檔案名稱長度。 附加檔案時會執行驗證。 下列程式中提供的指令碼會在檔案名稱大於150（包括副檔名）時顯示訊息。 您可以修改指令碼，以檢查其是否有不同數量的字元。

執行下列步驟以建立 [客戶端庫](/help/sites-developing/clientlibs.md) 並使用指令碼：

1. 登入CRXDE並導覽至/etc/clientlibs/
1. 建立類型的節點 **cq:ClientLibraryFolder** 和提供節點的名稱。 例如, `validation`.

   按一下 **[!UICONTROL 全部儲存]**.

1. 以滑鼠右鍵按一下節點，按一下 **[!UICONTROL 建立新檔案]**，並建立副檔名為.txt的檔案。 例如， `js.txt`將下列程式碼新增至新建立的.txt檔案，然後按一下 **[!UICONTROL 全部儲存]**.

   ```javascript
   #base=util
    util.js
   ```

   在上述程式碼中， `util` 是資料夾的名稱， `util.js` 檔案名稱 `util` 檔案夾。 此 `util` 資料夾和 `util.js` 檔案是在遵循步驟中建立。

1. 以滑鼠右鍵按一下 `cq:ClientLibraryFolder` 在步驟2中建立的節點，選擇「建立」>「建立資料夾」。 建立名為 `util`. 按一下 **[!UICONTROL 全部儲存]**. 以滑鼠右鍵按一下 `util` 資料夾，選擇「建立」>「建立檔案」。 建立名為 `util.js`. 按一下 **[!UICONTROL 全部儲存]**.

1. 將下列程式碼新增至util.js檔案，然後按一下 **[!UICONTROL 全部儲存]**. 程式碼會驗證檔案名稱的長度。

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
   >指令碼適用於現成(OOTB)附件Widget元件。 如果您已自訂OOTB附件Widget，請變更上述指令碼以併入個別變更。

1. 將下列屬性新增至步驟2中建立的資料夾，然後按一下 **[!UICONTROL 全部儲存]**.

   * **[!UICONTROL 名稱：]** 類別

   * **[!UICONTROL 類型：]** 字串

   * **[!UICONTROL 值：]** fp.validation

   * **[!UICONTROL 多選項：]** 已啟用

1. 導覽至 `/libs/fd/af/runtime/clientlibs/guideRuntime`並附加 `fp.validation` 值。

1. 導覽至/libs/fd/af/runtime/clientlibs/guideRuntimeWithXFA並附加 `fp.validation` 要內嵌屬性的值。

   >[!NOTE]
   >
   >如果您使用自訂用戶端程式庫，而非guideRuntime和guideRuntimeWithXfa用戶端程式庫，請使用類別名稱，將此程式中建立的用戶端程式庫內嵌至執行階段載入的自訂程式庫。

1. 按一下 **[!UICONTROL 全部儲存。]** 現在，當檔案名稱大於150（包括副檔名）字元時，就會顯示訊息。
