---
title: 將cURL與
seo-title: Using cURL with AEM
description: 瞭解如何使用cURLAEM。
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

# 將cURL與{#using-curl-with-aem}

管理員通常需要自動化或簡化任何系統中的常見任務。 例AEM如，管理用戶、安裝軟體包和管理OSGi軟體包是通常必須完成的任務。

由於構建Sling框架的REST風格AEM，大多數任務都可以通過URL調用完成。 cURL可用於執行此類URL調用，並且可以是管理員的有用工AEM具。

## 什麼是cURL {#what-is-curl}

cURL是用於執行URL操作的開源命令行工具。 它支援多種網際網路協定，包括HTTP、HTTPS、FTP、FTPS、SCP、SFTP、TFTP、LDAP、DAP、DICT、TELNET、FILE、IMAP、POP3、SMTP和RTSP。

cURL是一種成熟且廣泛使用的工具，用於使用URL語法獲取或發送資料，最初於1997年發佈。 名稱cURL最初意為「查看URL」。

由於構建Sling框架的REST風格AEM，大多數任務都可以簡化為URL調用，可以用cURL執行。 [內容處理任務](/help/sites-administering/curl.md#common-content-manipulation-aem-curl-commands) 如激活頁面和啟動工作流以及 [操作任務](/help/sites-administering/curl.md#common-operational-aem-curl-commands) 如包管理和管理用戶，可以使用cURL自動執行。 此外，您還可以 [建立您自己的cURL](/help/sites-administering/curl.md#building-a-curl-ready-aem-command) 的子例AEM行。

>[!NOTE]
>
>通過AEMcURL執行的任何命令必須像任何用戶一樣獲得授AEM權。 使用cURL執行命令時，會尊重所有ACL和訪問AEM權限。

## 正在下載cURL {#downloading-curl}

cURL是macOS和一些Linux目錄的標準部分。 但是，它適用於大多數作業系統。 最新下載可在 [https://curl.haxx.se/download.html](https://curl.haxx.se/download.html)。

cURL的源儲存庫也可在GitHub上找到。

## 生成cURL就緒命AEM令 {#building-a-curl-ready-aem-command}

cURL命令可用於大多數操作，AEM如觸發工作流、檢查OSGi配置、觸發JMX命令、建立複製代理等。

要查找特定操作所需的確切命令，您需要使用瀏覽器中的開發人員工具來捕獲執行該命令時對伺服器的POST調AEM用。

以下步驟將以在Chrome瀏覽器中建立新頁面為例說明如何執行此操作。

1. 準備要在中調用的操AEM作。 在這個例子中，我們已經 **建立頁** 的 **建立**。

   ![chlimage_1-66](assets/chlimage_1-66a.png)

1. 啟動開發人員工具並選擇 **網路** 頁籤。 按一下 **保留日誌** 選項。

   ![chlimage_1-67](assets/chlimage_1-67a.png)

1. 按一下 **建立** 的 **建立頁** 的子菜單。
1. 按一下右鍵結果POST操作，然後選擇 **複製** -> **複製為cURL**。

   ![chlimage_1-68](assets/chlimage_1-68a.png)

1. 將cURL命令複製到文本編輯器並從命令中刪除所有標題，該命令以 `-H` （在下圖中以藍色突出顯示），並添加正確的驗證參數，如 `-u <user>:<password>`。

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. 通過命令行執行cURL命令並查看響應。

   ![chlimage_1-70](assets/chlimage_1-70a.png)

## 常用操作AEMcURL命令 {#common-operational-aem-curl-commands}

下面是常見管AEM理和操作任務的cURL命令清單。

>[!NOTE]
>
>以下示例假定AEM正在運行 `localhost` 埠 `4502` 並使用用戶 `admin` 帶密碼 `admin`。 附加命令佔位符設定在尖括弧中。

### 包管理 {#package-management}

#### 列出所有已安裝的包

```shell
curl -u <user>:<password> http://<host>:<port>/crx/packmgr/service.jsp?cmd=ls
```

#### 建立包 {#create-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=create -d packageName=<name> -d groupName=<name>
```

#### 預覽包 {#preview-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=preview
```

#### 列出包內容 {#list-package-content}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/console.html/etc/packages/mycontent.zip?cmd=contents
```

#### 生成包 {#build-a-package}

```shell
curl -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=build
```

#### 重新包裝包 {#rewrap-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=rewrap
```

#### 更名包 {#rename-a-package}

```shell
curl -u <user>:<password> -X POST -Fname=<New Name> http://localhost:4502/etc/packages/<Group Name>/<Package Name>.zip/jcr:content/vlt:definition
```

#### 上載包 {#upload-a-package}

```shell
curl -u <user>:<password> -F cmd=upload -F force=true -F package=@test.zip http://localhost:4502/crx/packmgr/service/.json
```

#### 安裝軟體包 {#install-a-package}

```shell
curl -u <user>:<password> -F cmd=install http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### 卸載包 {#uninstall-a-package}

```shell
curl -u <user>:<password> -F cmd=uninstall http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### 刪除包 {#delete-a-package}

```shell
curl -u <user>:<password> -F cmd=delete http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### 下載包 {#download-a-package}

```shell
curl -u <user>:<password> http://localhost:4502/etc/packages/my_packages/test.zip
```

#### 複製包 {#replicate-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip?cmd=replicate
```

### 使用者管理 {#user-management}

#### 建立新用戶 {#create-a-new-user}

```shell
curl -u <user>:<password> -FcreateUser= -FauthorizableId=hashim -Frep:password=hashim http://localhost:4502/libs/granite/security/post/authorizables
```

#### 建立新組 {#create-a-new-group}

```shell
curl -u <user>:<password> -FcreateGroup=group1 -FauthorizableId=testGroup1 http://localhost:4502/libs/granite/security/post/authorizables
```

#### 向現有用戶添加屬性 {#add-a-property-to-an-existing-user}

```shell
curl -u <user>:<password> -Fprofile/age=25 http://localhost:4502/home/users/h/hashim.rw.html
```

#### 使用配置檔案建立用戶 {#create-a-user-with-a-profile}

```shell
curl -u <user>:<password> -FcreateUser=testuser -FauthorizableId=hashimkhan -Frep:password=hashimkhan -Fprofile/gender=male http://localhost:4502/libs/granite/security/post/authorizables
```

#### 將新用戶建立為組成員 {#create-a-new-user-as-a-member-of-a-group}

```shell
curl -u <user>:<password> -FcreateUser=testuser -FauthorizableId=testuser -Frep:password=abc123 -Fmembership=contributor http://localhost:4502/libs/granite/security/post/authorizables
```

#### 將用戶添加到組 {#add-a-user-to-a-group}

```shell
curl -u <user>:<password> -FaddMembers=testuser1 http://localhost:4502/home/groups/t/testGroup.rw.html
```

#### 從組中刪除用戶 {#remove-a-user-from-a-group}

```shell
curl -u <user>:<password> -FremoveMembers=testuser1 http://localhost:4502/home/groups/t/testGroup.rw.html
```

#### 設定用戶組成員身份 {#set-a-user-s-group-membership}

```shell
curl -u <user>:<password> -Fmembership=contributor -Fmembership=testgroup http://localhost:4502/home/users/t/testuser.rw.html
```

#### 刪除用戶 {#delete-a-user}

```shell
curl -u <user>:<password> -FdeleteAuthorizable= http://localhost:4502/home/users/t/testuser
```

#### 刪除組 {#delete-a-group}

```shell
curl -u <user>:<password> -FdeleteAuthorizable= http://localhost:4502/home/groups/t/testGroup
```

### 備份 {#backup}

請參閱 [備份和恢復](/help/sites-administering/backup-and-restore.md#automating-aem-online-backup) 的雙曲餘切值。

### OSGi {#osgi}

#### 啟動捆綁包 {#starting-a-bundle}

```shell
curl -u <user>:<password> -Faction=start http://localhost:4502/system/console/bundles/<bundle-name>
```

#### 停止捆綁 {#stopping-a-bundle}

```shell
curl -u <user>:<password> -Faction=stop http://localhost:4502/system/console/bundles/<bundle-name>
```

### Dispatcher {#dispatcher}

#### 使快取無效 {#invalidate-the-cache}

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

#### 分配和撤消徽章 {#assign-and-revoke-badges}

請參閱 [社區評分和徽章](/help/communities/implementing-scoring.md#assign-and-revoke-badges) 的雙曲餘切值。

請參閱 [評分和徽章要點](/help/communities/configure-scoring.md#example-setup) 的雙曲餘切值。

#### MSRP重新索引 {#msrp-reindexing}

請參閱 [MSRP - MongoDB儲存資源提供程式](/help/communities/msrp.md#running-msrp-reindex-tool-using-curl-command) 的雙曲餘切值。

### 安全性 {#security}

#### 啟用和禁用CRX DE Lite {#enabling-and-disabling-crx-de-lite}

請參閱 [啟用CRXDE LiteAEM](/help/sites-administering/enabling-crxde-lite.md) 的雙曲餘切值。

### 資料存放庫廢棄項目收集 {#data-store-garbage-collection}

請參閱 [資料儲存垃圾收集](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection) 的雙曲餘切值。

### 分析和目標整合 {#analytics-and-target-integration}

請參閱 [跳進Adobe Analytics和Adobe Target](/help/sites-administering/opt-in.md#configuring-the-setup-and-provisioning-via-script) 的雙曲餘切值。

### 單一登錄 {#single-sign-on}

#### 發送Test標題 {#send-test-header}

請參閱 [單一登錄](/help/sites-deploying/single-sign-on.md) 的雙曲餘切值。

## 常用內容操AEM作cURL命令 {#common-content-manipulation-aem-curl-commands}

下面是用於內AEM容處理的cURL命令清單。

>[!NOTE]
>
>以下示例假定AEM正在運行 `localhost` 埠 `4502` 並使用用戶 `admin` 帶密碼 `admin`。 附加命令佔位符設定在尖括弧中。

### 頁面管理 {#page-management}

#### 頁面激活 {#page-activation}

```shell
curl -u <user>:<password> -X POST -F path="/content/path/to/page" -F cmd="activate" http://localhost:4502/bin/replicate.json
```

#### 頁面停用 {#page-deactivation}

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

請參閱 [以寫程式方式與工作流交互](/help/sites-developing/workflows-program-interaction.md) 的雙曲餘切值。

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

#### 使用Sling PostServlet上載檔案 {#upload-files-using-sling-postservlet}

```shell
curl -u <user>:<password> -F"*=@test.properties"  http://localhost:4502/etc/test
```

#### 使用Sling PostServlet和指定節點名稱上載檔案 {#upload-files-using-sling-postservlet-and-specifying-node-name}

```shell
curl -u <user>:<password> -F"test2.properties=@test.properties"  http://localhost:4502/etc/test
```

#### 上載指定內容類型的檔案 {#upload-files-specifying-a-content-type}

```shell
curl -u <user>:<password> -F "*=@test.properties;type=text/plain" http://localhost:4502/etc/test
```

### 資產操作 {#asset-manipulation}

請參閱 [資產HTTP API](/help/assets/mac-api-assets.md) 的雙曲餘切值。
