---
title: AEM Forms 伺服器的效能調整
seo-title: Performance tuning of AEM Forms server
description: 要使AEM Forms以最佳方式運行，您可以微調快取設定和JVM參數。 另外，使用Web伺服器可以增強AEM Forms部署的效能。
seo-description: For AEM Forms to perform optimally, you can fine-tune the cache settings and JVM parameters. Also, using a web server can enhance the performance of AEM Forms deployment.
uuid: bf23b62c-7559-4726-8f4e-cc8b1457e501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 38c0ec46-5686-4656-bfb4-7125ec194673
docset: aem65
role: Admin
exl-id: 22926757-9cdb-4f8a-9bd9-16ddbc3f954a
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 1%

---

# AEM Forms 伺服器的效能調整{#performance-tuning-of-aem-forms-server}

本文討論您可以實施的策略和最佳做法，以減少瓶頸並優化您的AEM Forms部署的效能。

## 快取設定 {#cache-settings}

您可以使用 **移動Forms配置** Web配置控AEM制台中的元件：

* (AEM FormsOSGi) `https://'[server]:[port]'/system/console/configMgr`
* (AEM FormsJEE) `https://'[server]:[port]'/lc/system/console/configMgr`

快取的可用選項如下：

* **無**:強制不快取任何對象。 實際上，這會降低效能，並且由於缺少快取而需要高記憶體可用性。
* **保守**:指示僅快取在呈現表單之前生成的那些中間對象，例如包含內聯片段和影像的模板。
* **攻擊性**:強制對幾乎所有可快取的內容進行快取，包括呈現的HTML內容，而不包括來自Conservative快取級別的所有對象。 它會產生最佳效能，但也會消耗更多記憶體來儲存快取的偽像。 主動快取策略意味著在快取已呈現內容時，在呈現表單時將獲得恆定的時間效能。

AEM Forms的預設快取設定可能不足以實現最佳效能。 因此，建議使用以下設定：

* **快取策略**:攻擊性
* **快取大小** （形式）:根據需要
* **最大對象大小**:根據需要

![移動Forms配置](assets/snap.png)

>[!NOTE]
>
>如果使用AEMDispatcher快取自適應表單，它還會快取包含預填充資料的表單的自適應表單。 如果從AEMDispatcher快取提供此類表單，則可能導致向用戶提供預填充或陳舊的資料。 因此，使用AEMDispatcher快取不使用預填充資料的自適應表單。 此外，調度器快取不會自動使快取的片段無效。 所以，不要用它來快取表單片段。 對於這種形式和片段，使用 [自適應表單快取](../../forms/using/configure-adaptive-forms-cache.md)。

## JVM參數 {#jvm-parameters}

為獲得最佳效能，建議使用以下JVM `init` 要配置的參數 `Java heap` 和 `PermGen`。

```shell
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xms8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xmx8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:PermSize=256m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:MaxPermSize=1024m
```

>[!NOTE]
>
>建議的設定是用於Windows 2008 R2 8核心和OracleHotSpot 1.7（64位）JDK，應根據系統配置進行放大或縮小。

## 使用Web伺服器 {#using-a-web-server}

自適應表單和HTML5表單以HTML5格式呈現。 結果輸出可能會很大，具體取決於窗體大小和窗體中的影像等因素。 為了優化資料傳輸，建議的方法是使用從中提供請求的Web伺服器壓縮HTML響應。 此方法可減少響應大小、網路流量，以及在伺服器和客戶機之間傳輸資料所需的時間。

例如，執行以下步驟以在具有JBoss的Apache Web Server 2.0 32位上啟用壓縮：

>[!NOTE]
>
>以下說明不適用於除Apache Web Server 2.0 32位以外的任何伺服器。 有關特定於任何其他伺服器的步驟，請參閱相應的產品文檔。

以下步驟演示了使用Apache Web Server啟用壓縮所需的更改

**獲取適用於您的作業系統的Apache Web伺服器軟體**

* 窗口：從Apache HTTP Server Project網站下載Apache Web伺服器。
* Solaris 64位：從Sunfreeware for Solaris網站下載Apache Web伺服器。
* Linux:Linux系統上預裝了Apache Web伺服器。

Apache可以使用HTTP協定與CRX通信。 配置用於使用HTTP進行優化。

1. 取消注釋中的以下模組配置 `APACHE_HOME/conf/httpd.conf` 的子菜單。

   ```shell
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >對於Linux，預設 `APACHE_HOME` 是 `/etc/httpd/`。

1. 在crx的埠4502上配置代理。
在中添加以下配置 `APACHE_HOME/conf/httpd.conf` 配置檔案。

   ```shell
   ProxyPass / https://<server>:4502/
   ProxyPassReverse / https://<server>:4502/
   ```

1. 啟用壓縮。 在中添加以下配置 `APACHE_HOME/conf/httpd.conf` 配置檔案。

   **對於HTML5窗體**

   ```xml
   <Location /content/xfaforms>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Don’t compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   **對於自適應表單**

   ```xml
   <Location /content/forms/af>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Don’t compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   要訪問crx伺服器，請使用 `https://'server':80`，也請參見Wiki頁。 `server` 是運行Apache伺服器的伺服器的名稱。

## 在運行AEM Forms的伺服器上使用防病毒 {#using-an-antivirus-on-server-running-aem-forms}

在運行防病毒軟體的伺服器上，您可能會遇到效能下降。 Always on antivirus（訪問時掃描）軟體會掃描系統的所有檔案。 它會降低伺服器速度，並影響AEM Forms的效能。

要提高效能，您可以指示防病毒軟體將以下AEM Forms檔案和資料夾從始終開啟（訪問）掃描中排除：

* 安裝AEM目錄。 如果無法排除完整目錄，請排除以下內容：

   * [AEM安裝目錄]\crx-repository\temp
   * [AEM安裝目錄]\crx-repository\repository
   * [AEM安裝目錄]\crx-repository\launchpad

* 應用程式伺服器臨時目錄。 預設位置為：

   * （傑博斯） [AEM安裝目錄]\jboss\standalone\tmp
   * (Weblogic)\Oracle\Middleware\user_projects\domains\LCDomain\servers\LCServer1\tmp
   * (Websphere)\程式Files\IBM\WebSphere\AppServer\profiles\AppSrv01\temp

* **(僅AEM FormsJEE)** 全局文檔儲存(GDS)目錄。 預設位置為：

   * (JBoss) [appserver根]/server/&#39;server&#39;/svcnative/DocumentStorage
   * (WebLogic) [appserverdomain]/&#39;server&#39;/adobe/LiveCycleServer/DocumentStorage
   * (WebSphere) [appserver根]/installedApps/adobe/&#39;server&#39;/DocumentStorage

* **(僅AEM FormsJEE)** AEM Forms伺服器日誌和臨時目錄。 預設位置為：

   * 伺服器日誌 —  [AEM Forms安裝目錄]\Adobe\AEM表單\[app-server]\server\all\logs
   * 臨時目錄 —  [AEM Forms安裝目錄]\temp

>[!NOTE]
>
>* 如果GDS和臨時目錄使用的位置不同，請在 `https://'[server]:[port]'/adminui`，導航 **首頁>設定>核心繫統設定>核心配置** 確認使用中的位置。
* 如果AEM Forms伺服器在排除建議的目錄後執行速度較慢，則也排除Java執行檔(java.exe)。
>

