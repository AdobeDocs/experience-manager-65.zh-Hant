---
title: 搭配使用cURL與AEM
seo-title: Using cURL with AEM
description: 了解如何搭配AEM使用cURL。
seo-description: Learn how to use cURL with AEM.
uuid: 771b9acc-ff3a-41c9-9fee-7e5d2183f311
contentOwner: Silviu Raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d4ceb82e-2889-4507-af22-b051af83be38
exl-id: e3f018e6-563e-456f-99d5-d232f1a4aa55
source-git-commit: fafcf5f9ec64f147447300b02afbc0590d0c5e22
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 2%

---

# 搭配使用cURL與AEM{#using-curl-with-aem}

管理員通常需要自動化或簡化任何系統內的常見任務。 例如，在AEM中，管理使用者、安裝套件和管理OSGi套件組合是通常必須完成的工作。

由於建置AEM的Sling架構具有RESTful性質，因此大部分工作都可以透過URL呼叫完成。 cURL可用來執行此類URL呼叫，且對AEM管理員來說也是很實用的工具。

## 什麼是cURL {#what-is-curl}

cURL是用於執行URL操作的開放原始碼命令列工具。 它支援多種網際網路協定，包括HTTP、HTTPS、FTPS、SCP、SFTP、TFTP、LDAP、DAP、DICT、TELNET、FILE、IMAP、POP3、SMTP和RTSP。

cURL是使用URL語法取得或傳送資料的成熟且廣泛使用的工具，最初於1997年發行。 名稱cURL原本意指「請參閱URL」。

由於建置AEM的Sling架構具有RESTful性質，因此大部分工作都可簡化為URL呼叫，而此呼叫可以使用cURL執行。 [內容操作任務](/help/sites-administering/curl.md#common-content-manipulation-aem-curl-commands) 例如啟動頁面、啟動工作流程以及 [操作任務](/help/sites-administering/curl.md#common-operational-aem-curl-commands) 例如，可使用cURL自動管理套件和管理使用者。 此外，您 [建立您自己的cURL](/help/sites-administering/curl.md#building-a-curl-ready-aem-command) 命令執行AEM中的大多數任務。

>[!NOTE]
>
>任何透過cURL執行的AEM命令，都必須像任何使用者一樣獲得AEM的授權。 使用cURL執行AEM命令時，會考量所有ACL和存取權限。

## 下載cURL {#downloading-curl}

cURL是macOS和部分Linux程式庫的標準部分。 但是，它適用於大多數作業系統。 您可在以下網址找到最新的下載內容： [https://curl.haxx.se/download.html](https://curl.haxx.se/download.html).

您也可以在GitHub上找到cURL的來源存放庫。

## 建立可用cURL的AEM命令 {#building-a-curl-ready-aem-command}

cURL命令可針對AEM中的大部分操作而建置，例如觸發工作流程、檢查OSGi設定、觸發JMX命令、建立復寫代理等。

若要尋找您特定作業所需的確切命令，您必須在瀏覽器中使用開發人員工具，以在執行AEM命令時擷取對伺服器的POST呼叫。

下列步驟以在Chrome瀏覽器中建立新頁面為例說明如何執行此操作。

1. 準備要在AEM中叫用的動作。 在這種情況下，我們已將 **建立頁面** 嚮導，但尚未按一下 **建立**.

   ![chlimage_1-66](assets/chlimage_1-66a.png)

1. 啟動開發人員工具並選取 **網路** 標籤。 按一下 **保留日誌** 選項。

   ![chlimage_1-67](assets/chlimage_1-67a.png)

1. 按一下 **建立** 在 **建立頁面** 精靈，以實際建立工作流程。
1. 以滑鼠右鍵按一下產生的POST動作，然後選取 **複製** -> **複製為cURL**.

   ![chlimage_1-68](assets/chlimage_1-68a.png)

1. 將cURL命令複製到文字編輯器，並從命令中移除所有標題（以開頭） `-H` （在下圖中以藍色顯示）並新增正確的驗證參數，例如 `-u <user>:<password>`.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. 通過命令行執行cURL命令並查看響應。

   ![chlimage_1-70](assets/chlimage_1-70a.png)

## 常見操作AEM cURL命令 {#common-operational-aem-curl-commands}

以下是常見管理和操作任務的AEM cURL命令清單。

>[!NOTE]
>
>下列範例假設AEM正在執行 `localhost` 埠 `4502` 和使用使用者 `admin` 使用密碼 `admin`. 其他命令佔位符設定在角括弧中。

### 套件管理 {#package-management}

#### 列出所有已安裝的軟體包

```shell
curl -u <user>:<password> http://<host>:<port>/crx/packmgr/service.jsp?cmd=ls
```

#### 建立套件 {#create-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=create -d packageName=<name> -d groupName=<name>
```

#### 預覽套件 {#preview-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=preview
```

#### 清單包內容 {#list-package-content}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/console.html/etc/packages/mycontent.zip?cmd=contents
```

#### 建立套件 {#build-a-package}

```shell
curl -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=build
```

#### 重新包裝套件 {#rewrap-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=rewrap
```

#### 更名包 {#rename-a-package}

```shell
curl -u <user>:<password> -X POST -Fname=<New Name> http://localhost:4502/etc/packages/<Group Name>/<Package Name>.zip/jcr:content/vlt:definition
```

#### 上傳套件 {#upload-a-package}

```shell
curl -u <user>:<password> -F cmd=upload -F force=true -F package=@test.zip http://localhost:4502/crx/packmgr/service/.json
```

#### 安裝套件 {#install-a-package}

```shell
curl -u <user>:<password> -F cmd=install http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### 解除安裝套件 {#uninstall-a-package}

```shell
curl -u <user>:<password> -F cmd=uninstall http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### 刪除套件 {#delete-a-package}

```shell
curl -u <user>:<password> -F cmd=delete http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### 下載套件 {#download-a-package}

```shell
curl -u <user>:<password> http://localhost:4502/etc/packages/my_packages/test.zip
```

#### 複製包 {#replicate-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip?cmd=replicate
```

### 使用者管理 {#user-management}

#### 建立新使用者 {#create-a-new-user}

```shell
curl -u <user>:<password> -FcreateUser= -FauthorizableId=hashim -Frep:password=hashim http://localhost:4502/libs/granite/security/post/authorizables
```

#### 建立新群組 {#create-a-new-group}

```shell
curl -u <user>:<password> -FcreateGroup=group1 -FauthorizableId=testGroup1 http://localhost:4502/libs/granite/security/post/authorizables
```

#### 新增屬性至現有使用者 {#add-a-property-to-an-existing-user}

```shell
curl -u <user>:<password> -Fprofile/age=25 http://localhost:4502/home/users/h/hashim.rw.html
```

#### 使用設定檔建立使用者 {#create-a-user-with-a-profile}

```shell
curl -u <user>:<password> -FcreateUser=testuser -FauthorizableId=hashimkhan -Frep:password=hashimkhan -Fprofile/gender=male http://localhost:4502/libs/granite/security/post/authorizables
```

#### 建立新使用者作為群組的成員 {#create-a-new-user-as-a-member-of-a-group}

```shell
curl -u <user>:<password> -FcreateUser=testuser -FauthorizableId=testuser -Frep:password=abc123 -Fmembership=contributor http://localhost:4502/libs/granite/security/post/authorizables
```

#### 新增使用者至群組 {#add-a-user-to-a-group}

```shell
curl -u <user>:<password> -FaddMembers=testuser1 http://localhost:4502/home/groups/t/testGroup.rw.html
```

#### 從群組中移除使用者 {#remove-a-user-from-a-group}

```shell
curl -u <user>:<password> -FremoveMembers=testuser1 http://localhost:4502/home/groups/t/testGroup.rw.html
```

#### 設定使用者的群組成員資格 {#set-a-user-s-group-membership}

```shell
curl -u <user>:<password> -Fmembership=contributor -Fmembership=testgroup http://localhost:4502/home/users/t/testuser.rw.html
```

#### 刪除使用者 {#delete-a-user}

```shell
curl -u <user>:<password> -FdeleteAuthorizable= http://localhost:4502/home/users/t/testuser
```

#### 刪除群組 {#delete-a-group}

```shell
curl -u <user>:<password> -FdeleteAuthorizable= http://localhost:4502/home/groups/t/testGroup
```

### 備份 {#backup}

請參閱 [備份和還原](/help/sites-administering/backup-and-restore.md#automating-aem-online-backup) 以取得詳細資訊。

### OSGi {#osgi}

#### 啟動套件組合 {#starting-a-bundle}

```shell
curl -u <user>:<password> -Faction=start http://localhost:4502/system/console/bundles/<bundle-name>
```

#### 停止捆綁 {#stopping-a-bundle}

```shell
curl -u <user>:<password> -Faction=stop http://localhost:4502/system/console/bundles/<bundle-name>
```

### Dispatcher {#dispatcher}

#### 使快取失效 {#invalidate-the-cache}

```shell
curl -H "CQ-Action: Activate" -H "CQ-Handle: /content/test-site/" -H "CQ-Path: /content/test-site/" -H "Content-Length: 0" -H "Content-Type: application/octet-stream" http://localhost:4502/dispatcher/invalidate.cache
```

#### 逐出快取 {#evict-the-cache}

```shell
curl -H "CQ-Action: Deactivate" -H "CQ-Handle: /content/test-site/" -H "CQ-Path: /content/test-site/" -H "Content-Length: 0" -H "Content-Type: application/octet-stream" http://localhost:4502/dispatcher/invalidate.cache
```

### 複寫代理 {#replication-agent}

#### 檢查代理的狀態 {#check-the-status-of-an-agent}

```shell
curl -u <user>:<password> "http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json?agent=publish"
http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json?agent=publish
```

#### 刪除代理 {#delete-an-agent}

```shell
curl -X DELETE http://localhost:4502/etc/replication/agents.author/replication99 -u <user>:<password>
```

#### 建立代理 {#create-an-agent}

```shell
curl -u <user>:<password> -F "jcr:primaryType=cq:Page" -F "jcr:content/jcr:title=new-replication" -F "jcr:content/sling:resourceType=/libs/cq/replication/components/agent" -F "jcr:content/template=/libs/cq/replication/templates/agent" -F "jcr:content/transportUri=http://localhost:4503/bin/receive?sling:authRequestLogin=1" -F "jcr:content/transportUser=admin" -F "jcr:content/transportPassword={DES}8aadb625ced91ac483390ebc10640cdf"http://localhost:4502/etc/replication/agents.author/replication99
```

#### 暫停代理 {#pause-an-agent}

```shell
curl -u <user>:<password> -F "cmd=pause" -F "name=publish"  http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json
```

#### 清除代理隊列 {#clear-an-agent-queue}

```shell
curl -u <user>:<password> -F "cmd=clear" -F "name=publish"  http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json
```

### 社群 {#communities}

#### 指派和撤銷徽章 {#assign-and-revoke-badges}

請參閱 [社群計分和徽章](/help/communities/implementing-scoring.md#assign-and-revoke-badges) 以取得詳細資訊。

請參閱 [計分和徽章要點](/help/communities/configure-scoring.md#example-setup) 以取得詳細資訊。

#### MSRP重新索引 {#msrp-reindexing}

請參閱 [MSRP - MongoDB儲存資源提供程式](/help/communities/msrp.md#running-msrp-reindex-tool-using-curl-command) 以取得詳細資訊。

### 安全性 {#security}

#### 啟用和禁用CRX DE Lite {#enabling-and-disabling-crx-de-lite}

請參閱 [在AEM中啟用CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md) 以取得詳細資訊。

### 資料存放庫廢棄項目收集 {#data-store-garbage-collection}

請參閱 [資料儲存垃圾收集](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection) 以取得詳細資訊。

### Analytics與Target整合 {#analytics-and-target-integration}

請參閱 [選擇加入Adobe Analytics和Adobe Target](/help/sites-administering/opt-in.md#configuring-the-setup-and-provisioning-via-script) 以取得詳細資訊。

### 單一登入 {#single-sign-on}

#### 傳送測試標題 {#send-test-header}

請參閱 [單一登入](/help/sites-deploying/single-sign-on.md) 以取得詳細資訊。

## 常見內容操作AEM cURL命令 {#common-content-manipulation-aem-curl-commands}

以下是用於內容操控的AEM cURL命令清單。

>[!NOTE]
>
>下列範例假設AEM正在執行 `localhost` 埠 `4502` 和使用使用者 `admin` 使用密碼 `admin`. 其他命令佔位符設定在角括弧中。

### 頁面管理 {#page-management}

#### 頁面啟動 {#page-activation}

```shell
curl -u <user>:<password> -X POST -F path="/content/path/to/page" -F cmd="activate" http://localhost:4502/bin/replicate.json
```

#### 停用頁面 {#page-deactivation}

```shell
curl -u <user>:<password> -X POST -F path="/content/path/to/page" -F cmd="deactivate" http://localhost:4502/bin/replicate.json
```

#### 樹激活 {#tree-activation}

```shell
curl -u <user>:<password> -F cmd=activate -F ignoredeactivated=true -F onlymodified=true -F path=/content/geometrixx http://localhost:4502/etc/replication/treeactivation.html
```

#### 鎖定頁面 {#lock-page}

```shell
curl -u <user>:<password> -X POST -F cmd="lockPage" -F path="/content/path/to/page" -F "_charset_"="utf-8" http://localhost:4502/bin/wcmcommand
```

#### 解鎖頁面 {#unlock-page}

```shell
curl -u <user>:<password> -X POST -F cmd="unlockPage" -F path="/content/path/to/page" -F "_charset_"="utf-8" http://localhost:4502/bin/wcmcommand
```

#### 複製頁面 {#copy-page}

```shell
curl -u <user>:<password> -F cmd=copyPage -F destParentPath=/path/to/destination/parent -F srcPath=/path/to/source/location http://localhost:4502/bin/wcmcommand
```

### 工作流程 {#workflows}

請參閱 [以程式設計方式與工作流程互動](/help/sites-developing/workflows-program-interaction.md) 以取得詳細資訊。

### Sling內容 {#sling-content}

#### 建立資料夾 {#create-a-folder}

```shell
curl -u <user>:<password> -F jcr:primaryType=sling:Folder http://localhost:4502/etc/test
```

#### 刪除節點 {#delete-a-node}

```shell
curl -u <user>:<password> -F :operation=delete http://localhost:4502/etc/test/test.properties
```

#### 移動節點 {#move-a-node}

```shell
curl -u <user>:<password> -F":operation=move" -F":applyTo=/sourceurl"  -F":dest=/target/parenturl/" https://localhost:4502/content
```

#### 複製節點 {#copy-a-node}

```shell
curl -u <user>:<password> -F":operation=copy" -F":applyTo=/sourceurl"  -F":dest=/target/parenturl/" https://localhost:4502/content
```

#### 使用Sling PostServlet上傳檔案 {#upload-files-using-sling-postservlet}

```shell
curl -u <user>:<password> -F"*=@test.properties"  http://localhost:4502/etc/test
```

#### 使用Sling PostServlet上傳檔案並指定節點名稱 {#upload-files-using-sling-postservlet-and-specifying-node-name}

```shell
curl -u <user>:<password> -F"test2.properties=@test.properties"  http://localhost:4502/etc/test
```

#### 上傳指定內容類型的檔案 {#upload-files-specifying-a-content-type}

```shell
curl -u <user>:<password> -F "*=@test.properties;type=text/plain" http://localhost:4502/etc/test
```

### 資產操作 {#asset-manipulation}

請參閱 [Assets HTTP API](/help/assets/mac-api-assets.md) 以取得詳細資訊。
