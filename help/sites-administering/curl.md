---
title: 搭配AEM使用cURL
seo-title: 搭配AEM使用cURL
description: 瞭解如何搭配AEM使用cURL。
seo-description: 瞭解如何搭配AEM使用cURL。
uuid: 771b9acc-ff3a-41c9-9fee-7e5d2183f311
contentOwner: Silviu Raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d4ceb82e-2889-4507-af22-b051af83be38
translation-type: tm+mt
source-git-commit: 7ee76afa11384aedc79b17e823c8dc9594662388

---


# 搭配AEM使用cURL{#using-curl-with-aem}

管理員通常需要自動化或簡化任何系統中的一般工作。 例如，在AEM中，管理使用者、安裝套件和管理OSGi搭售是通常必須完成的工作。

由於AEM所建立之Sling架構具有REST風格，因此大部分的工作都可簡化為URL呼叫。 cURL可用來執行此類URL呼叫，而且對AEM管理員而言也是有用的工具。

## 什麼是cURL {#what-is-curl}

cURL是用於執行URL操縱的開放原始碼命令列工具。 它支援多種網際網路通訊協定，包括HTTP、HTTPS、FTPS、SCP、SFTP、TFTP、LDAP、DAP、DICT、TELNET、FILE、IMAP、POP3、SMTP和RTSP。

cURL是使用URL語法取得或傳送資料的成熟且廣泛使用的工具，最初於1997年發行。 名稱cURL原意是「請參閱URL」。

由於建立AEM的Sling架構具有REST風格，因此大部分工作都可縮減為URL呼叫，而URL呼叫可以與cURL一起執行。 [使用cURL](/help/sites-administering/curl.md#common-content-manipulation-aem-curl-commands) ，可自動執行內容控制工作 [，例如啟動頁面、啟動工作流程](/help/sites-administering/curl.md#common-operational-aem-curl-commands) 以及操作工作，例如封裝管理和管理使用者。 此外，您也可 [](/help/sites-administering/curl.md#building-a-curl-ready-aem-command) 以針對AEM中的大部分工作建立自己的cURL指令。

>[!NOTE]
>
>透過cURL執行的任何AEM命令都必須像任何AEM使用者一樣獲得授權。 使用cURL執行AEM命令時，會考慮所有ACL和存取權限。

## 下載cURL {#downloading-curl}

cURL是macOS和部分Linux資料庫的標準部分。 但是，它適用於大多數的作業系統。 如需最新下載，請造訪 [https://curl.haxx.se/download.html](https://curl.haxx.se/download.html)。

cURL的來源儲存庫也可在GitHub上找到。

## 建立可立即使用cURL的AEM命令 {#building-a-curl-ready-aem-command}

cURL命令可針對AEM中的大部分作業建立，例如觸發工作流程、檢查OSGi組態、觸發JMX命令、建立複製代理等。

若要尋找您特定作業所需的確切命令，您必須使用瀏覽器中的開發人員工具，在您執行AEM命令時擷取對伺服器的POST呼叫。

以下步驟說明如何以在Chrome瀏覽器中建立新頁面為例。

1. 準備您要在AEM中叫用的動作。 在這種情況下，我們已進入「建立頁面」精靈的 **結尾** ，但尚未按一下「 **建立」**。

   ![chlimage_1-66](assets/chlimage_1-66a.png)

1. 啟動開發人員工具並選取「網 **路** 」標籤。 在清除控 **制台之前** ，按一下「保留日誌」選項。

   ![chlimage_1-67](assets/chlimage_1-67a.png)

1. 在「 **建立頁面** 」精靈中按 **一下「建立** 」，實際建立工作流程。
1. 按一下右鍵生成的POST操作，然後選擇「 **Copy** -> **Copy as cURL」（複製為cURL）**。

   ![chlimage_1-68](assets/chlimage_1-68a.png)

1. 將cURL命令複製到文字編輯器，並從命令中移除所有標題，其開頭為 `-H` （在下圖中以藍色標示），然後新增正確的驗證參數，例如 `-u admin:admin`。

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. 通過命令行執行cURL命令並查看響應。

   ![chlimage_1-70](assets/chlimage_1-70a.png)

## 常見作業AEM cURL命令 {#common-operational-aem-curl-commands}

以下是常見管理與作業工作的AEM cURL命令清單。

>[!NOTE]
>
>下列範例假設AEM在埠上執 `localhost` 行， `4502` 並使用使用者 `admin` 加上密碼 `admin`。 其他命令佔位符以方括弧設定。

### 套件管理 {#package-management}

#### 建立包 {#create-a-package}

```shell
curl -u admin:admin -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=create -d packageName=<name> -d groupName=<name>
```

#### 預覽套件 {#preview-a-package}

```shell
curl -u admin:admin -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=preview
```

#### 清單封裝內容 {#list-package-content}

```shell
curl -u admin:admin -X POST http://localhost:4502/crx/packmgr/service/console.html/etc/packages/mycontent.zip?cmd=contents
```

#### 建立套件 {#build-a-package}

```shell
curl -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=build
```

#### 重新包覆套件 {#rewrap-a-package}

```shell
curl -u admin:admin -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=rewrap
```

#### 更名包 {#rename-a-package}

```shell
curl -u admin:admin -X POST -Fname=<New Name> http://localhost:4502/etc/packages/<Group Name>/<Package Name>.zip/jcr:content/vlt:definition
```

#### 上傳套件 {#upload-a-package}

```shell
curl -u admin:admin -F cmd=upload -F force=true -F package=@test.zip http://localhost:4502/crx/packmgr/service/.json
```

#### 安裝軟體包 {#install-a-package}

```shell
curl -u admin:admin -F cmd=install http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### 卸載軟體包 {#uninstall-a-package}

```shell
curl -u admin:admin -F cmd=uninstall http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### 刪除包 {#delete-a-package}

```shell
curl -u admin:admin -F cmd=delete http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### 下載套件 {#download-a-package}

```shell
curl -u admin:admin http://localhost:4502/etc/packages/my_packages/test.zip
```

### 使用者管理 {#user-management}

#### Create a New User {#create-a-new-user}

```shell
curl -u admin:admin -FcreateUser= -FauthorizableId=hashim -Frep:password=hashim http://localhost:4502/libs/granite/security/post/authorizables
```

#### Create a New Group {#create-a-new-group}

```shell
curl -u admin:admin -FcreateGroup=group1 -FauthorizableId=testGroup1 http://localhost:4502/libs/granite/security/post/authorizables
```

#### 新增屬性至現有使用者 {#add-a-property-to-an-existing-user}

```shell
curl -u admin:admin -Fprofile/age=25 http://localhost:4502/home/users/h/hashim.rw.html
```

#### 使用描述檔建立使用者 {#create-a-user-with-a-profile}

```shell
curl -u admin:admin -FcreateUser=testuser -FauthorizableId=hashimkhan -Frep:password=hashimkhan -Fprofile/gender=male http://localhost:4502/libs/granite/security/post/authorizables
```

#### 建立新使用者作為群組成員 {#create-a-new-user-as-a-member-of-a-group}

```shell
curl -u admin:admin -FcreateUser=testuser -FauthorizableId=testuser -Frep:password=abc123 -Fmembership=contributor http://localhost:4502/libs/granite/security/post/authorizables
```

#### 新增使用者至群組 {#add-a-user-to-a-group}

```shell
curl -u admin:admin -FaddMembers=testuser1 http://localhost:4502/home/groups/t/testGroup.rw.html
```

#### 從群組移除使用者 {#remove-a-user-from-a-group}

```shell
curl -u admin:admin -FremoveMembers=testuser1 http://localhost:4502/home/groups/t/testGroup.rw.html
```

#### 設定使用者群組成員資格 {#set-a-user-s-group-membership}

```shell
curl -u admin:admin -Fmembership=contributor -Fmembership=testgroup http://localhost:4502/home/users/t/testuser.rw.html
```

#### 刪除用戶 {#delete-a-user}

```shell
curl -u admin:admin -FdeleteAuthorizable= http://localhost:4502/home/users/t/testuser 
```

#### 刪除群組 {#delete-a-group}

```shell
curl -u admin:admin -FdeleteAuthorizable= http://localhost:4502/home/groups/t/testGroup
```

### 備份 {#backup}

如需詳 [細資訊，請參閱備份](/help/sites-administering/backup-and-restore.md#automating-aem-online-backup) 和還原。

### OSGi {#osgi}

#### 啟動捆綁包 {#starting-a-bundle}

```shell
curl -u admin:admin -Faction=start http://localhost:4502/system/console/bundles/<bundle-name>
```

#### 停止捆綁包 {#stopping-a-bundle}

```shell
curl -u admin:admin -Faction=stop http://localhost:4502/system/console/bundles/<bundle-name>
```

### Dispatcher {#dispatcher}

#### 使快取失效 {#invalidate-the-cache}

```shell
curl -H "CQ-Action: Activate" -H "CQ-Handle: /content/test-site/" -H "CQ-Path: /content/test-site/" -H "Content-Length: 0" -H "Content-Type: application/octet-stream" http://localhost:4502/dispatcher/invalidate.cache
```

#### 驅逐快取 {#evict-the-cache}

```shell
curl -H "CQ-Action: Deactivate" -H "CQ-Handle: /content/test-site/" -H "CQ-Path: /content/test-site/" -H "Content-Length: 0" -H "Content-Type: application/octet-stream" http://localhost:4502/dispatcher/invalidate.cache
```

### 複寫代理 {#replication-agent}

#### 檢查座席狀態 {#check-the-status-of-an-agent}

```shell
curl -u admin:admin "http://localhost:4502/etc/replication/agents.author/publish/jcr:conten t.queue.json?agent=publish"
http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.js on?agent=publish
```

#### 刪除代理 {#delete-an-agent}

```shell
curl -X DELETE http://localhost:4502/etc/replication/agents.author/replication99 -u admin:admin
```

#### 建立代理 {#create-an-agent}

```shell
curl -u admin:admin -F "jcr:primaryType=cq:Page" -F "jcr:content/jcr:title=new-replication" -F "jcr:content/sling:resourceType=/libs/cq/replication/components/agent" -F "jcr:content/template=/libs/cq/replication/templates/agent" -F "jcr:content/transportUri=http://localhost:4503/bin/receive?sling:authRequestLogin=1" -F "jcr:content/transportUser=admin" -F "jcr:content/transportPassword={DES}8aadb625ced91ac483390ebc10640cdf"http://localhost:4502/etc/replication/agents.author/replication99
```

#### 暫停代理 {#pause-an-agent}

```shell
curl -u admin:admin -F "cmd=pause" -F "name=publish"  http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.js on
```

#### 清除代理隊列 {#clear-an-agent-queue}

```shell
curl -u admin:admin -F "cmd=clear" -F "name=publish"  http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.js on
```

### 社群 {#communities}

#### 指派和撤銷標章 {#assign-and-revoke-badges}

如需詳 [細資訊，請參閱社群評分](/help/communities/implementing-scoring.md#assign-and-revoke-badges) 和標章。

如需詳 [細資訊，請參閱Scoring and Badges Essentials](/help/communities/configure-scoring.md#example-setup) 。

#### MSRP重新索引 {#msrp-reindexing}

如需詳 [細資訊，請參閱MSRP - MongoDB儲存資源提供者](/help/communities/msrp.md#running-msrp-reindex-tool-using-curl-command) 。

### 安全性 {#security}

#### 啟用和禁用CRX DE Lite {#enabling-and-disabling-crx-de-lite}

如需詳 [細資訊，請參閱「在AEM中啟用CRXDE](/help/sites-administering/enabling-crxde-lite.md) Lite」。

### 資料存放庫廢棄項目收集 {#data-store-garbage-collection}

如需詳 [細資訊，請參閱資料存放區廢棄項目收集](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection) 。

### Analytics與Target整合 {#analytics-and-target-integration}

如需詳 [細資訊，請參閱「選擇加入Adobe Analytics和Adobe Target](/help/sites-administering/opt-in.md#configuring-the-setup-and-provisioning-via-script) 」。

### 單一登入 {#single-sign-on}

#### 傳送測試標題 {#send-test-header}

如需詳 [細資訊，請參閱單一登入](/help/sites-deploying/single-sign-on.md) 。

## 常見內容控制AEM cURL命令 {#common-content-manipulation-aem-curl-commands}

以下是AEM cURL指令的清單，以用於內容控制。

>[!NOTE]
>
>下列範例假設AEM在埠上執 `localhost` 行， `4502` 並使用使用者 `admin` 加上密碼 `admin`。 其他命令佔位符以方括弧設定。

### 頁面管理 {#page-management}

#### 頁面啟動 {#page-activation}

```shell
curl -u admin:admin -X POST -F path="/content/path/to/page" -F cmd="activate" http://localhost:4502/bin/replicate.json
```

#### 頁面停用 {#page-deactivation}

```shell
curl -u admin:admin -X POST -F path="/content/path/to/page" -F cmd="deactivate" http://localhost:4502/bin/replicate.json
```

#### 樹狀結構啟動 {#tree-activation}

```shell
curl -u admin:admin -F cmd=activate -F ignoredeactivated=true -F onlymodified=true -F path=/content/geometrixx http://localhost:4502/etc/replication/treeactivation.html
```

#### 鎖定頁面 {#lock-page}

```shell
curl -u admin:admin -X POST -F cmd="lockPage" -F path="/content/path/to/page" -F "_charset_"="utf-8" http://localhost:4502/bin/wcmcommand
```

#### 解鎖頁面 {#unlock-page}

```shell
curl -u admin:admin -X POST -F cmd="unlockPage" -F path="/content/path/to/page" -F "_charset_"="utf-8" http://localhost:4502/bin/wcmcommand
```

#### 複製頁面 {#copy-page}

```shell
curl -u admin:admin -F cmd=copyPage -F destParentPath=/path/to/destination/parent -F srcPath=/path/to/source/location http://localhost:4502/bin/wcmcommand
```

### 工作流程 {#workflows}

如需詳 [細資訊，請參閱「以程式設計方式](/help/sites-developing/workflows-program-interaction.md) 與工作流程互動」。

### Sling Content {#sling-content}

#### 建立資料夾 {#create-a-folder}

```shell
curl -u admin:admin -F jcr:primaryType=sling:Folder http://localhost:4502/etc/test
```

#### 刪除節點 {#delete-a-node}

```shell
curl -u admin:admin -F :operation=delete http://localhost:4502/etc/test/test.properties
```

#### 移動節點 {#move-a-node}

```shell
curl -u admin:admin -F":operation=move" -F":applyTo=/sourceurl"  -F":dest=/target/parenturl/" https://localhost:4502/content
```

#### 複製節點 {#copy-a-node}

```shell
curl -u admin:admin -F":operation=copy" -F":applyTo=/sourceurl"  -F":dest=/target/parenturl/" https://localhost:4502/content
```

#### 使用Sling PostServlet上傳檔案 {#upload-files-using-sling-postservlet}

```shell
curl -u admin:admin -F"*=@test.properties"  http://localhost:4502/etc/test
```

#### 使用Sling PostServlet和指定節點名稱上傳檔案 {#upload-files-using-sling-postservlet-and-specifying-node-name}

```shell
curl -u admin:admin -F"test2.properties=@test.properties"  http://localhost:4502/etc/test
```

#### 上傳指定內容類型的檔案 {#upload-files-specifying-a-content-type}

```shell
curl -u admin:admin -F "*=@test.properties;type=text/plain" http://localhost:4502/etc/test
```

### 資產操縱 {#asset-manipulation}

如需詳 [細資訊，請參閱Assets HTTP](/help/assets/mac-api-assets.md) API。
