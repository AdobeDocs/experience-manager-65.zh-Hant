---
title: AEM Forms 伺服器的效能調整
seo-title: Performance tuning of AEM Forms server
description: 若要讓AEM Forms以最佳方式執行，您可以微調快取設定和JVM參數。 此外，使用Web伺服器可提升AEM Forms部署的效能。
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

本文探討您可實作的策略和最佳實務，以減少瓶頸並最佳化AEM Forms部署的效能。

## 快取設定 {#cache-settings}

您可以使用 **行動Forms設定** 元件(位於：

* (AEM Forms on OSGi) `https://'[server]:[port]'/system/console/configMgr`
* (JEE版AEM Forms) `https://'[server]:[port]'/lc/system/console/configMgr`

快取的可用選項如下：

* **無**:強制不快取任何對象。 實際上，這會降低效能，而且由於缺少快取，需要高記憶體可用性。
* **保守**:指定僅快取在呈現表單之前產生的那些中間工件，例如包含內嵌片段和影像的範本。
* **攻擊性**:強制快取幾乎可快取的所有內容，包括保守快取層級中除所有成品外，呈現的HTML內容。 它會產生最佳效能，但也會耗用更多記憶體來儲存快取成品。 積極的快取策略意味著快取呈現的內容時，表單呈現會持續提供時間效能。

AEM Forms的預設快取設定可能不足以達到最佳效能。 因此，建議使用下列設定：

* **快取策略**:攻擊性
* **快取大小** （表格數）:視需要
* **最大對象大小**:視需要

![行動Forms設定](assets/snap.png)

>[!NOTE]
>
>如果您使用AEM Dispatcher來快取最適化表單，也會快取包含已預填資料表單的最適化表單。 如果從AEM Dispatcher快取提供這類表單，可能會導致為使用者提供預先填入或過時的資料。 因此，請使用AEM Dispatcher來快取不使用預填資料的最適化表單。 此外，Dispatcher快取不會自動使快取片段無效。 因此，請勿將其用於快取表單片段。 對於這類表單和片段，請使用 [適用性表單快取](../../forms/using/configure-adaptive-forms-cache.md).

## JVM參數 {#jvm-parameters}

為獲得最佳效能，建議使用以下JVM `init` 要配置的參數 `Java heap` 和 `PermGen`.

```shell
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xms8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xmx8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:PermSize=256m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:MaxPermSize=1024m
```

>[!NOTE]
>
>建議的設定用於Windows 2008 R2 8 Core和OracleHotSpot 1.7（64位）JDK，應根據您的系統配置進行放大或縮小。

## 使用Web伺服器 {#using-a-web-server}

適用性表單和HTML5表單會以HTML5格式呈現。 結果的輸出可能會很大，具體取決於表單大小和表單中的影像等因素。 若要最佳化資料傳輸，建議的方法是使用要求提供來源的Web伺服器來壓縮HTML回應。 此方法可減少回應大小、網路流量，以及在伺服器與用戶端電腦之間串流資料所需的時間。

例如，執行下列步驟，使用JBoss在Apache Web Server 2.0 32位元上啟用壓縮：

>[!NOTE]
>
>下列說明不適用於Apache Web Server 2.0 32位元以外的任何伺服器。 如需任何其他伺服器的特定步驟，請參閱對應的產品檔案。

以下步驟演示了使用Apache Web Server啟用壓縮所需的更改

**獲取適用於您的作業系統的Apache Web伺服器軟體**

* 窗口：從Apache HTTP Server Project站點下載Apache Web伺服器。
* Solaris 64位：從Sunfreeware for Solaris網站下載Apache web伺服器。
* Linux:Linux系統上已預裝了Apache Web伺服器。

Apache可以使用HTTP通訊協定與CRX通訊。 這些設定是用於使用HTTP進行最佳化。

1. 取消註解下列模組配置： `APACHE_HOME/conf/httpd.conf` 檔案。

   ```shell
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >對於Linux，預設 `APACHE_HOME` is `/etc/httpd/`.

1. 在crx的埠4502上配置代理。
在中新增下列設定 `APACHE_HOME/conf/httpd.conf` 設定檔。

   ```shell
   ProxyPass / https://<server>:4502/
   ProxyPassReverse / https://<server>:4502/
   ```

1. 啟用壓縮。 在中新增下列設定 `APACHE_HOME/conf/httpd.conf` 設定檔。

   **HTML5表單**

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

   **適用於最適化表單**

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

   若要存取crx伺服器，請使用 `https://'server':80`，其中 `server` 是運行Apache伺服器的伺服器的名稱。

## 在執行AEM Forms的伺服器上使用防病毒 {#using-an-antivirus-on-server-running-aem-forms}

運行防病毒軟體的伺服器上的效能可能會下降。 始終開啟防病毒（訪問掃描）軟體掃描系統的所有檔案。 這可能會減緩伺服器速度，並影響AEM Forms的效能。

要提高效能，可以指導防病毒軟體從始終開啟（訪問）掃描中排除以下AEM Forms檔案和資料夾：

* AEM安裝目錄。 如果無法排除完整目錄，請排除下列項目：

   * [AEM安裝目錄]\crx-repository\temp
   * [AEM安裝目錄]\crx-repository\repository
   * [AEM安裝目錄]\crx-repository\launchpad

* 應用程式伺服器臨時目錄。 預設位置為：

   * (Jboss) [AEM安裝目錄]\jboss\standalone\tmp
   * (Weblogic)\Oracle\Middleware\user_projects\domains\LCDomain\servers\LCServer1\tmp
   * (Websphere)\計畫Files\IBM\WebSphere\AppServer\profiles\AppSrv01\temp

* **(僅限JEE版AEM Forms)** 全局文檔儲存(GDS)目錄。 預設位置為：

   * (JBoss) [appserver根]/server/&#39;server&#39;/svcnative/DocumentStorage
   * (WebLogic) [appserverdomain]/&#39;server&#39;/adobe/LiveCycleServer/DocumentStorage
   * (WebSphere) [appserver根]/installedApps/adobe/&#39;server&#39;/DocumentStorage

* **(僅限JEE版AEM Forms)** AEM Forms伺服器記錄檔和臨時目錄。 預設位置為：

   * 伺服器日誌 —  [AEM Forms安裝目錄]\Adobe\AEM forms\[app-server]\server\all\logs
   * 臨時目錄 —  [AEM Forms安裝目錄]\temp

>[!NOTE]
>
>* 如果您對GDS和臨時目錄使用不同位置，請在 `https://'[server]:[port]'/adminui`，導覽至 **首頁>設定>核心繫統設定>核心配置** 確認使用中的位置。
* 如果AEM Forms伺服器在排除建議的目錄後執行速度緩慢，則也排除Java執行檔(java.exe)。
>

