---
title: 將草稿和提交元件與資料庫整合的示例
seo-title: Sample for integrating drafts & submissions component with database
description: 參考定制資料和元資料服務的實現，將草稿和提交元件與資料庫整合。
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

# 將草稿和提交元件與資料庫整合的示例 {#sample-for-integrating-drafts-submissions-component-with-database}

## 示例概述 {#sample-overview}

AEM Forms門戶草稿和提交元件允許用戶將其表單另存為草稿並稍後從任何設備提交。 此外，用戶可以在門戶上查看其提交的表單。 為啟用此功能，AEM Forms提供資料和元資料服務，將用戶填寫的表格資料以及與草稿和已提交表格相關聯的表格元資料儲存起來。 預設情況下，此資料儲存在CRX儲存庫中。 但是，當用戶通過發佈實例與表單進行交互時AEM，組織可能希望自定義資料儲存，以使其更加安全和可靠。

本文檔中討論的示例是定制資料和元資料服務的參考實現，用於將草稿和提交元件與資料庫整合。 示例實現中使用的資料庫是 **MySQL 5.6.24**。 但是，您可以將草稿和提交元件與您選擇的任何資料庫整合。

>[!NOTE]
>
>* 本文檔中介紹的示例和配置是根據MySQL 5.6.24進行的，您必須將它們相應地替換為資料庫系統。
>* 確保已安裝最新版本的AEM Forms附加軟體包。 有關可用包的清單，請參見 [AEM Forms釋放](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 文章。
>* 示例包僅與Adaptive Forms提交操作配合使用。


## 設定和配置示例 {#set-up-and-configure-the-sample}

對所有作者和發佈實例執行以下步驟以安裝和配置示例：

1. 下載以下內容 **aem-fp-db-integration-sample-pkg-6.1.2-zip** 檔案系統。

   用於資料庫整合的示例包

[取得檔案](assets/aem-fp-db-integration-sample-pkg-6.1.2.zip)

1. 請訪問AEMhttps://上的包管理器&#x200B;[*主機*]:[*埠*]/crx/packmgr/。
1. 按一下 **[!UICONTROL 上載包]**。

1. 瀏覽以選擇 **aem-fp-db-integration-sample-pkg-6.1.2-zip** 包，按一下 **[!UICONTROL 確定]**。
1. 按一下 **[!UICONTROL 安裝]** 的子菜單。
1. 轉到 **[!UICONTROL Web控AEM制台配置]**
https://[*主機*]:[*埠*]/system/console/configMgr。
1. 按一下以開啟 **[!UICONTROL Forms門戶草稿和提交配置]** 的子菜單。

1. 指定屬性的值，如下表所述：

   | **屬性** | **說明** | **值** |
   |---|---|---|
   | Forms門戶草稿資料服務 | 草稿資料服務的標識符 | formsportal.sampledataservice |
   | Forms門戶草稿元資料服務 | 草稿元資料服務的標識符 | formsportal.samplemetadataservice |
   | Forms門戶提交資料服務 | 提交資料服務的標識符 | formsportal.sampledataservice |
   | Forms門戶提交元資料服務 | 提交元資料服務的標識符 | formsportal.samplemetadataservice |
   | Forms門戶待簽資料服務 | 掛起簽名資料服務的標識符 | formsportal.sampledataservice |
   | Forms門戶掛起簽名元資料服務 | 掛起簽名元資料服務的標識符 | formsportal.samplemetadataservice |

   >[!NOTE]
   >
   >這些服務由其名稱解析，這些名稱是 `aem.formsportal.impl.prop` 鍵如下：

   ```java
   @Service(value = {SubmitDataService.class, DraftDataService.class})
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.sampledataservice")
   @Service(value = { SubmitMetadataService.class, DraftMetadataService.class })
   @Property(name = "aem.formsportal.impl.prop", value = "formsportal.samplemetadataservice")
   ```

   可以更改資料表和元資料表的名稱。

   要為元資料表提供其他名稱：

   * 在Web控制台配置中，查找並按一下Forms門戶元資料服務示例實施。 您可以更改資料源、元資料/其他元資料表名的值。

   要為資料表提供其他名稱：

   * 在Web控制台配置中，查找並按一下Forms門戶資料服務示例實施。 可以更改資料源和資料表名稱的值。
   >[!NOTE]
   >
   >如果更改表名，請在「表單門戶」配置中提供它們。

1. 保持其他配置原樣，然後按一下 **[!UICONTROL 保存]**。

1. 資料庫連接可通過Apache Sling連接池資料源完成。
1. 對於Apache Sling連接，查找並按一下以開啟 **[!UICONTROL Apache Sling連接池化資料源]** 在「Web Console Configuration（Web控制台配置）」中，在「編輯」模式下。 指定屬性的值，如下表所述：

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>值</strong></td>
  </tr>
  <tr>
   <td>資料源名稱</td>
   <td><p>用於從資料源池篩選驅動程式的資料源名稱</p> <p><strong>注： </strong><em>示例實現使用FormsPortal作為資料源名稱。</em></p> </td>
  </tr>
  <tr>
   <td>JDBC驅動程式類</td>
   <td>com.mysql.jdbc.Driver</td>
  </tr>
  <tr>
   <td>JDBC連接URI<br /> </td>
   <td>jdbc:mysql:/[<em>主機</em>]:[<em>埠</em>]/[<em>架構名稱</em>]</td>
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
   <td>已提交讀取</td>
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
   <td>最大等待時間</td>
   <td>100000</td>
  </tr>
  <tr>
   <td>Test借用</td>
   <td>已核取</td>
  </tr>
  <tr>
   <td>Test空閒時</td>
   <td>已核取</td>
  </tr>
  <tr>
   <td>驗證查詢</td>
   <td>示例值為SELECT 1(mysql)、從雙(oracle)中選擇1、SELECT 1(MS Sql Server)(validationQuery)</td>
  </tr>
  <tr>
   <td>驗證查詢超時</td>
   <td>10000</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* MySQL的JDBC驅動程式未隨示例提供。 確保已為其設定並提供配置JDBC連接池所需的資訊。
>* 指向作者並發佈實例以使用同一資料庫。 對於所有作者和發佈實例，JDBC連接URI欄位的值必須相同。


1. 保持其他配置原樣，然後按一下 **[!UICONTROL 保存]**。

1. 如果資料庫架構中已有表，請跳到下一步。

   否則，如果資料庫架構中尚未包含表，請執行以下SQL陳述式，為資料庫架構中的資料、元資料和其他元資料建立單獨的表：

   >[!NOTE]
   >
   >作者和發佈實例不需要不同的資料庫。 在所有作者和發佈實例上使用相同的資料庫。

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

   **SQL陳述式用於其他元資料表**

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

1. 如果資料庫架構中已有表（資料、元資料和其他元資料表），請執行以下變更表查詢：

   **用於變更資料表的SQL陳述式**

   ```sql
   ALTER TABLE `data` CHANGE `owner` `owner` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL;
   ```

   **用於更改元資料表的SQL陳述式**

   ```sql
   ALTER TABLE metadata add markedForDeletion varchar(45) DEFAULT NULL
   ```

   >[!NOTE]
   >
   >如果ALTER TABLE元資料添加查詢已運行且表中存在markedforDeletion列，則該查詢將失敗。

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

   **用於更改附加可表的SQL陳述式**

   ```sql
   ALTER TABLE `additionalmetadatatable` CHANGE `value` `value` TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL, CHANGE `key` `key` VARCHAR(255) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL;
   ```

現在配置了示例實現，您可以使用它在資料庫中儲存所有資料和元資料時列出草稿和提交。 現在，讓我們看一下示例中如何配置資料和元資料服務。

## 安裝mysql-connector-java-5.1.39-bin.jar檔案 {#install-mysql-connector-java-bin-jar-file}

對所有作者和發佈實例執行以下步驟以安裝mysql-connector-java-5.1.39-bin.jar檔案：

1. 導航到 `https://'[server]:[port]'/system/console/depfinder` 並搜索com.mysql.jdbc包。
1. 在「導出者」(Exported by)列中，檢查包是否由任何捆綁包導出。

   如果包未由任何包導出，則繼續。

1. 導航到 `https://'[server]:[port]'/system/console/bundles` 按一下 **[!UICONTROL 安裝/更新]**。
1. 按一下 **[!UICONTROL 選擇檔案]** 並瀏覽以選擇mysql-connector-java-5.1.39-bin.jar檔案。 另外，選擇 **[!UICONTROL 啟動包]** 和 **[!UICONTROL 刷新包]** 複選框。
1. 按一下 **[!UICONTROL 安裝或更新]**。 完成後，重新啟動伺服器。
1. (*僅Windows*)關閉作業系統的系統防火牆。

## 表單門戶資料和元資料服務的示例代碼 {#sample-code-for-forms-portal-data-and-metadata-service}

以下zip包含 `FormsPortalSampleDataServiceImpl` 和 `FormsPortalSampleMetadataServiceImpl` （實現類），用於資料和元資料服務介面。 此外，它包含編譯上述實現類所需的所有類。

[取得檔案](assets/sample_package.zip)

## 驗證檔案名的長度  {#verify-length-of-the-file-name}

Forms門戶的資料庫實現使用了其他元資料表。 表具有基於表的鍵和id列的複合主鍵。 MySQL允許主鍵長達255個字元。 可以使用以下客戶端驗證指令碼驗證附加到檔案構件的檔案名的長度。 在附加檔案時運行驗證。 以下過程中提供的指令碼在檔案名大於150（包括副檔名）時顯示一條消息。 您可以修改指令碼，以檢查其中是否包含不同數量的字元。

執行以下步驟以建立 [客戶端庫](/help/sites-developing/clientlibs.md) 並使用指令碼：

1. 登錄到CRXDE並導航到/etc/clientlibs/
1. 建立類型的節點 **cq:ClientLibraryFolder** 並提供節點名稱。 比如說， `validation`。

   按一下 **[!UICONTROL 全部保存]**。

1. 按一下右鍵節點，按一下 **[!UICONTROL 建立新檔案]**，並建立副檔名為.txt的檔案。 比如說， `js.txt`將以下代碼添加到新建立的.txt檔案中，然後按一下 **[!UICONTROL 全部保存]**。

   ```javascript
   #base=util
    util.js
   ```

   在上述代碼中， `util` 是資料夾的名稱， `util.js` 檔案的名稱 `util` 的子菜單。 的 `util` 資料夾和 `util.js` 檔案在後續步驟中建立。

1. 按一下右鍵 `cq:ClientLibraryFolder` 節點在步驟2中建立，選擇「建立」>「建立資料夾」。 建立名為 `util`。 按一下 **[!UICONTROL 全部保存]**。 按一下右鍵 `util` 資料夾，選擇「建立」>「建立檔案」。 建立名為 `util.js`。 按一下 **[!UICONTROL 全部保存]**。

1. 將以下代碼添加到util.js檔案，然後按一下 **[!UICONTROL 全部保存]**。 代碼驗證檔案名的長度。

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
   >該指令碼用於開箱即用(OOTB)附件小部件元件。 如果已自定義OOTB附件小部件，請更改上述指令碼以合併相應更改。

1. 將以下屬性添加到在步驟2中建立的資料夾，然後按一下 **[!UICONTROL 全部保存]**。

   * **[!UICONTROL 名稱：]** 類別

   * **[!UICONTROL 類型：]** 字串

   * **[!UICONTROL 值：]** fp.validation

   * **[!UICONTROL 多選項：]** 已啟用

1. 導航到 `/libs/fd/af/runtime/clientlibs/guideRuntime`並附加 `fp.validation` 值到embed屬性。

1. 導航到/libs/fd/af/runtime/clientlibs/guideRuntimeWithXFA並附加 `fp.validation` 嵌入屬性的值。

   >[!NOTE]
   >
   >如果使用的是自定義客戶端庫，而不是guideRuntime和guideRuntimeWithXfa客戶端庫，請使用類別名稱將在此過程中建立的客戶端庫嵌入到運行時載入的自定義庫中。

1. 按一下 **[!UICONTROL 全部保存。]** 現在，當檔案名大於150（包括副檔名）字元時，將顯示一條消息。
