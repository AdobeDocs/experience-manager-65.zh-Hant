---
title: 將草稿和提交元件與資料庫整合的範例
description: 參考自訂資料和中繼資料服務的實作，以將草稿和提交元件與資料庫整合。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
exl-id: 2e4f8f51-df02-4bbb-99bb-30181facd1e0
solution: Experience Manager, Experience Manager Forms
feature: Forms Portal
role: Admin, User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1502'
ht-degree: 1%

---

# 將草稿和提交元件與資料庫整合的範例 {#sample-for-integrating-drafts-submissions-component-with-database}

## 範例概述 {#sample-overview}

AEM Forms入口網站草稿和提交元件可讓使用者將其表單儲存為草稿，並於稍後從任何裝置提交。 此外，使用者還可以在入口網站上檢視他們提交的表單。 為了啟用此功能，AEM Forms提供資料和中繼資料服務，以儲存使用者在表單中填入的資料，以及與草稿和已提交表單關聯的表單中繼資料。 依預設，此資料會儲存在CRX存放庫中。 不過，當使用者透過AEM發佈執行個體（通常位於企業防火牆之外）與表單互動時，組織可能會想要自訂資料儲存，使其更安全可靠。

本檔案中討論的範例是自訂資料和中繼資料服務的參考實作，以將草稿和提交元件與資料庫整合。 範例實作中使用的資料庫是&#x200B;**MySQL 5.6.24**。 不過，您可以將草稿和提交元件與所選的任何資料庫整合。

>[!NOTE]
>
>* 本檔案中說明的範例和設定是根據MySQL 5.6.24，您必須適當地取代它們來取代資料庫系統。
>* 確保您已安裝最新版的AEM Forms附加元件套件。 如需可用封裝的清單，請參閱[AEM Forms發行版本](https://helpx.adobe.com/tw/aem-forms/kb/aem-forms-releases.html)文章。
>* 範例套件僅適用於Adaptive Forms提交動作。

## 設定範例 {#set-up-and-configure-the-sample}

在所有作者和發佈執行個體上執行以下步驟，以安裝和設定範例：

1. 將下列&#x200B;**aem-fp-db-integration-sample-pkg-6.1.2.zip**&#x200B;封裝下載至您的檔案系統。

   資料庫整合的範例套件

[取得檔案](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. 移至https://[*host*]：[*連線埠*]/crx/packmgr/的AEM封裝管理員。
1. 按一下&#x200B;**[!UICONTROL 上傳封裝]**。

1. 瀏覽以選取&#x200B;**aem-fp-db-integration-sample-pkg-6.1.2.zip**&#x200B;封裝，然後按一下&#x200B;**[!UICONTROL 確定]**。
1. 按一下封裝旁的&#x200B;**[!UICONTROL 安裝]**&#x200B;以安裝封裝。
1. 移至&#x200B;**[!UICONTROL AEM Web主控台組態]**
頁面位於https://[*host*]：[*連線埠*]/system/console/configMgr。
1. 按一下以在編輯模式中開啟&#x200B;**[!UICONTROL Forms入口網站草稿和提交設定]**。

1. 指定特性值，如下表所述：

   | **屬性** | **說明** | **值** |
   |---|---|---|
   | Forms入口網站草稿資料服務 | 草稿資料服務的識別碼 | formsportal.sampledataservice |
   | Forms入口網站草稿中繼資料服務 | 草稿中繼資料服務的識別碼 | formsportal.samplemetadataservice |
   | Forms入口網站提交資料服務 | 用於提交資料服務的識別碼 | formsportal.sampledataservice |
   | Forms入口網站提交中繼資料服務 | 用於提交中繼資料服務的識別碼 | formsportal.samplemetadataservice |
   | Forms入口網站等待簽署的資料服務 | 擱置簽署資料服務的識別碼 | formsportal.sampledataservice |
   | Forms入口網站等待簽署中繼資料服務 | 擱置簽署中繼資料服務的識別碼 | formsportal.samplemetadataservice |

   >[!NOTE]
   >
   >服務的名稱會解析為`aem.formsportal.impl.prop`索引鍵的值，如下所示：

   ```java
   @Service(value = {SubmitDataService.class, DraftDataService.class})
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.sampledataservice")
   @Service(value = { SubmitMetadataService.class, DraftMetadataService.class })
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.samplemetadataservice")
   ```

   您可以變更資料和中繼資料表的名稱。

   為中繼資料表格提供不同的名稱：

   * 在Web主控台設定中，尋找並按一下Forms Portal中繼資料服務實作範例。 您可以變更資料來源、中繼資料/其他中繼資料表格名稱的值。

   為資料表格提供不同的名稱：

   * 在Web主控台設定中，尋找並按一下Forms Portal Data Service實作範例。 您可以變更資料來源和資料表格名稱的值。

   >[!NOTE]
   >
   >如果您變更表格名稱，請在Form Portal設定中提供它們。

1. 將其他組態維持原狀，然後按一下[儲存]。**&#x200B;**

1. 資料庫連線可透過Apache Sling Connection Pooled Data Source完成。
1. 若為Apache Sling連線，請在Web主控台設定中尋找並按一下，以編輯模式開啟&#x200B;**[!UICONTROL Apache Sling Connection Pooled DataSource]**。 指定特性值，如下表所述：

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>值</strong></td>
  </tr>
  <tr>
   <td>資料來源名稱</td>
   <td><p>從資料來源集區篩選驅動程式的資料來源名稱</p> <p><strong>注意： </strong><em>範例實作使用FormsPortal做為資料來源名稱。</em></p> </td>
  </tr>
  <tr>
   <td>JDBC驅動程式類別</td>
   <td>com.mysql.jdbc.Driver</td>
  </tr>
  <tr>
   <td>JDBC連線URI<br /> </td>
   <td>jdbc:mysql://[<em>主機</em>]：[<em>連線埠</em>]/[<em>結構描述名稱</em>]</td>
  </tr>
  <tr>
   <td>使用者名稱</td>
   <td>用於驗證資料庫表格並執行動作的使用者名稱</td>
  </tr>
  <tr>
   <td>密碼</td>
   <td>與使用者名稱關聯的密碼</td>
  </tr>
  <tr>
   <td>交易隔離</td>
   <td>READ_COMMITTED</td>
  </tr>
  <tr>
   <td>最大使用中連線</td>
   <td>1000</td>
  </tr>
  <tr>
   <td>最大閒置連線</td>
   <td>100</td>
  </tr>
  <tr>
   <td>最小閒置連線</td>
   <td>10</td>
  </tr>
  <tr>
   <td>初始大小</td>
   <td>10</td>
  </tr>
  <tr>
   <td>等待上限</td>
   <td>100000</td>
  </tr>
  <tr>
   <td>借入時測試</td>
   <td>已核取</td>
  </tr>
  <tr>
   <td>閒置時測試</td>
   <td>已核取</td>
  </tr>
  <tr>
   <td>驗證查詢</td>
   <td>範例值為SELECT 1(mysql)、select 1 from dual(oracle)、SELECT 1(MS Sql Server) (validationQuery)</td>
  </tr>
  <tr>
   <td>驗證查詢逾時</td>
   <td>10000</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* 範例未提供適用於MySQL的JDBC驅動程式。 請確定您已布建此資料庫，並提供設定JDBC連線集區所需的資訊。
>* 將您的作者和發佈執行個體指向使用相同的資料庫。 所有製作和發佈執行個體的JDBC連線URI欄位值必須相同。

1. 將其他組態維持原狀，然後按一下[儲存]。**&#x200B;**

1. 如果資料庫綱要中已經有表格，請跳至下一個步驟。

   否則，如果資料庫綱要中還沒有表格，請執行下列SQL敘述句，為資料庫綱要中的資料、中繼資料和其他中繼資料建立個別的表格：

   >[!NOTE]
   >
   >製作和發佈執行個體不需要不同的資料庫。 在所有作者和發佈執行個體上使用相同的資料庫。

   資料表&#x200B;**的** SQL陳述式

   ```sql
   CREATE TABLE `data` (
   `owner` varchar(255) DEFAULT NULL,
   `data` longblob,
   `metadataId` varchar(45) DEFAULT NULL,
   `id` varchar(45) NOT NULL,
   PRIMARY KEY (`id`)
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   中繼資料資料表&#x200B;**的** SQL陳述式

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

   適用於additionalmetadatatable **的** SQL陳述式

   ```sql
   CREATE TABLE `additionalmetadatatable` (
   `value` text,
   `key` varchar(255) NOT NULL,
   `id` varchar(60) NOT NULL,
   PRIMARY KEY (`id`,`key`),
   CONSTRAINT 'additionalmetadatatable_fk' FOREIGN KEY (`id`) REFERENCES `metadata` (`id`) ON DELETE CASCADE
   ) ENGINE=InnoDB DEFAULT CHARSET=utf8;
   ```

   註解資料表的&#x200B;**SQL陳述式**

   ```sql
   CREATE TABLE `commenttable` (
   `commentId` varchar(255) DEFAULT NULL,
   `comment` text DEFAULT NULL,
   `ID` varchar(255) DEFAULT NULL,
   `commentowner` varchar(255) DEFAULT NULL,
   `time` varchar(255) DEFAULT NULL);
   ```

1. 如果您在資料庫綱要中已經有表格（資料、中繼資料和additionalmetadatable），請執行以下變更表格查詢：

   變更資料表的&#x200B;**SQL陳述式**

   ```sql
   ALTER TABLE `data` CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   變更中繼資料資料表的&#x200B;**SQL陳述式**

   ```sql
   ALTER TABLE metadata add markedForDeletion varchar(45) DEFAULT NULL
   ```

   >[!NOTE]
   >
   >如果您已執行ALTER TABLE中繼資料新增查詢，且表格中有marketforDeletion欄，則該查詢會失敗。

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

   用於變更additionalmetadatable資料表的&#x200B;**SQL陳述式**

   ```sql
   ALTER TABLE `additionalmetadatatable` CHANGE `value` `value` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL, CHANGE `key` `key` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL;
   ```

範例實作現在已設定，您可以在資料庫中儲存所有資料和中繼資料時，使用範例實作來列出草稿和提交內容。 現在來看看範例中資料和中繼資料服務的設定方式。

## 安裝mysql-connector-java-5.1.39-bin.jar檔案 {#install-mysql-connector-java-bin-jar-file}

在所有作者和發佈執行個體上執行以下步驟，以安裝mysql-connector-java-5.1.39-bin.jar檔案：

1. 瀏覽至`https://'[server]:[port]'/system/console/depfinder`並搜尋com.mysql.jdbc套件。
1. 在「匯出者」欄中，檢查封裝是否由任何束匯出。

   如果套件未由任何套件組合匯出，請繼續。

1. 瀏覽至`https://'[server]:[port]'/system/console/bundles`並按一下&#x200B;**[!UICONTROL 安裝/更新]**。
1. 按一下&#x200B;**[!UICONTROL 選擇檔案]**&#x200B;並瀏覽以選取mysql-connector-java-5.1.39-bin.jar檔案。 此外，選取&#x200B;**[!UICONTROL 開始套件]**&#x200B;和&#x200B;**[!UICONTROL 重新整理套件]**&#x200B;核取方塊。
1. 按一下&#x200B;**[!UICONTROL 安裝或更新]**。 完成後，請重新啟動伺服器。
1. （*僅限Windows*）關閉作業系統的系統防火牆。

>[!NOTE]
>
> 建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式）可能會導致AEM開發環境不一致。

## 表單入口網站資料和中繼資料服務的範常式式碼 {#sample-code-for-forms-portal-data-and-metadata-service}

下列zip包含資料和中繼資料服務介面的`FormsPortalSampleDataServiceImpl`和`FormsPortalSampleMetadataServiceImpl` （實作類別）。 此外，它包含編譯上述實作類別所需的所有類別。

[取得檔案](assets/sample_package.zip)

## 驗證檔案名稱的長度  {#verify-length-of-the-file-name}

Forms Portal的資料庫實作會使用其他中繼資料表格。 表格具有以表格的「索引鍵」和ID欄為基礎的複合主索引鍵。 MySQL允許主鍵長度不超過255個字元。 您可以使用以下使用者端驗證指令碼來驗證附加至檔案Widget的檔案名稱長度。 驗證會在附加檔案時執行。 當檔案名稱大於150 （包括副檔名）時，下列程式中提供的指令碼會顯示訊息。 您可以修改指令碼以檢查是否有不同的字元數。

執行以下步驟來建立[使用者端程式庫](/help/sites-developing/clientlibs.md)並使用指令碼：

1. 登入CRXDE並導覽至/etc/clientlibs/
1. 建立&#x200B;**cq：ClientLibraryFolder**&#x200B;型別的節點，並提供節點的名稱。 例如，`validation`。

   按一下&#x200B;**[!UICONTROL 「儲存全部」]**。

1. 以滑鼠右鍵按一下節點，按一下&#x200B;**[!UICONTROL 建立新檔案]**，然後建立副檔名為.txt的檔案。 例如，`js.txt`將下列程式碼新增至新建立的.txt檔案，然後按一下&#x200B;**[!UICONTROL 全部儲存]**。

   ```javascript
   #base=util
    util.js
   ```

   在上述程式碼中，`util`是資料夾的名稱和`util`資料夾中檔案的`util.js`名稱。 `util`資料夾和`util.js`檔案是在後續步驟中建立的。

1. 以滑鼠右鍵按一下在步驟2中建立的`cq:ClientLibraryFolder`節點，選取建立>建立資料夾。 建立名為`util`的資料夾。 按一下&#x200B;**[!UICONTROL 全部儲存]**。 在`util`資料夾上按一下滑鼠右鍵，選取「建立>建立檔案」。 建立名為`util.js`的檔案。 按一下&#x200B;**[!UICONTROL 「儲存全部」]**。

1. 將下列程式碼新增至util.js檔案，然後按一下[儲存全部]。**&#x200B;** 程式碼會驗證檔案名稱的長度。

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
   >此指令碼適用於現成可用的附件Widget元件。 如果您已自訂立即可用的附件Widget，請變更上述指令碼以納入個別變更。

1. 將下列屬性新增至步驟2中建立的資料夾，然後按一下[儲存全部]。**&#x200B;**

   * **[!UICONTROL 名稱：]**&#x200B;類別

   * **[!UICONTROL 型別：]**&#x200B;字串

   * **[!UICONTROL 值：]** fp.validation

   * **[!UICONTROL 多重選項：]**&#x200B;已啟用

1. 導覽至`/libs/fd/af/runtime/clientlibs/guideRuntime`並將`fp.validation`值附加至內嵌屬性。

1. 導覽至/libs/fd/af/runtime/clientlibs/guideRuntimeWithXFA並將`fp.validation`值附加至內嵌屬性。

   >[!NOTE]
   >
   >如果您使用自訂使用者端程式庫，而不是guideRuntime和guideRuntimeWithXfa使用者端程式庫，請使用類別名稱，將在此程式中建立的使用者端程式庫內嵌到在執行階段載入的自訂程式庫中。

1. 按一下「**[!UICONTROL 儲存全部」。]**&#x200B;現在，當檔案名稱大於150 （包括副檔名）字元時，會顯示訊息。
