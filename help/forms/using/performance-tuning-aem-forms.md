---
title: AEM Forms 伺服器的效能調整
description: 若要讓AEM Forms以最佳方式執行，您可以微調快取設定和JVM引數。 此外，使用網頁伺服器可增強AEM Forms部署的效能。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin,User
exl-id: 22926757-9cdb-4f8a-9bd9-16ddbc3f954a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# AEM Forms伺服器的效能調整{#performance-tuning-of-aem-forms-server}

本文會討論您可以實作的策略與最佳實務，以減少瓶頸並最佳化AEM Forms部署的效能。

## 快取設定 {#cache-settings}

您可以使用AEM Web Configuration Console中的&#x200B;**Mobile Forms Configurations**&#x200B;元件來設定和控制AEM Forms的快取策略：

* (OSGi上的AEM Forms) `https://'[server]:[port]'/system/console/configMgr`
* (JEE上的AEM Forms) `https://'[server]:[port]'/lc/system/console/configMgr`

可用的快取選項如下：

* **無**：強制不快取任何成品。 實際上，這會降低效能，而且因為沒有快取記憶體，所以需要較高的記憶體可用性。
* **保守**：指定僅快取在轉譯表單之前產生的那些中間成品，例如包含內嵌片段和影像的範本。
* **積極進取**：強制快取幾乎所有可以快取的專案，包括演算後的HTML內容，以及保守快取層級的所有成品。 這樣不僅可產生最佳效能，而且會消耗更多記憶體來儲存快取的成品。 積極快取策略表示您可以在快取呈現的內容時，在呈現表單時獲得持續的時間效能。

AEM Forms的預設快取設定可能不足以達到最佳效能。 因此，建議使用以下設定：

* **快取策略**：積極
* **快取大小** （以表單數計）：視需要
* **物件大小上限**：視需要

![行動Forms設定](assets/snap.png)

>[!NOTE]
>
>如果您使用AEM Dispatcher來快取最適化表單，它也會快取最適化表單，該表單包含具有預填資料的表單。 如果從AEM Dispatcher快取中提供這類表單，可能會導致為使用者提供預先填入或過時的資料。 因此，請使用AEM Dispatcher來快取不使用預先填入資料的最適化表單。 此外，Dispatcher快取不會自動讓快取片段失效。 因此，請勿將其用於快取表單片段。 對於這類表單和片段，請使用[最適化表單快取](../../forms/using/configure-adaptive-forms-cache.md)。

## JVM引數 {#jvm-parameters}

為獲得最佳效能，建議使用下列JVM `init`引數來設定`Java heap`和`PermGen`。

```shell
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xms8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xmx8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:PermSize=256m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:MaxPermSize=1024m
```

>[!NOTE]
>
>建議的設定適用於Windows 2008 R2 8 Core和OracleHotSpot 1.7 （64位元） JDK，應根據您的系統組態進行擴充或縮減。

## 使用網頁伺服器 {#using-a-web-server}

調適型表單和HTML5表單轉譯為HTML5格式。 根據表單的表單大小和影像等因素，產生的輸出可能會很大。 為了最佳化資料傳輸，建議使用提供請求的Web伺服器來壓縮HTML回應。 此方法可減少回應大小、網路流量，以及在伺服器和使用者端電腦之間串流資料所需的時間。

例如，執行以下步驟，透過JBoss®在Apache Web Server 2.0 32位元上啟用壓縮：

>[!NOTE]
>
>下列指示不適用於Apache Web Server 2.0 32位元以外的任何伺服器。 如需任何其他伺服器的特定步驟，請參閱相應的產品檔案。

下列步驟示範使用Apache Web Server啟用壓縮所需的變更

**取得適用於您作業系統的Apache網頁伺服器軟體**

* Windows：從Apache HTTP Server專案網站下載Apache Web Server。
* Solaris™ 64位元：從適用於Solaris™網站的Sunfreeware下載Apache網頁伺服器。
* Linux®： Apache Web Server已預先安裝在Linux®系統上。

Apache可以使用HTTP通訊協定與CRX通訊。 這些設定是使用HTTP進行最佳化。

1. 取消註解`APACHE_HOME/conf/httpd.conf`檔案中的下列模組設定。

   ```shell
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >Linux®的預設`APACHE_HOME`為`/etc/httpd/`。

1. 在crx的連線埠4502上設定Proxy。
在`APACHE_HOME/conf/httpd.conf`組態檔中新增下列組態。

   ```shell
   ProxyPass / https://<server>:4502/
   ProxyPassReverse / https://<server>:4502/
   ```

1. 啟用壓縮。 在`APACHE_HOME/conf/httpd.conf`組態檔中新增下列組態。

   HTML5表單的&#x200B;****

   ```xml
   <Location /content/xfaforms>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Do not compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   **適用性表單**

   ```xml
   <Location /content/forms/af>
       <IfModule mod_deflate.c>
           SetOutputFilter DEFLATE
           #Do not compress
           SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
           SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
           #Dealing with proxy servers
               <IfModule mod_headers.c>
                   Header append Vary User-Agent
               </IfModule>
       </IfModule>
   </Location>
   ```

   若要存取crx伺服器，請使用`https://'server':80`，其中`server`是執行Apache伺服器的伺服器名稱。

## 在執行AEM Forms的伺服器上使用防毒程式 {#using-an-antivirus-on-server-running-aem-forms}

執行防毒軟體的伺服器可能會發生效能變慢的情況。 永遠開啟的防毒（即時掃描）軟體會掃描系統的所有檔案。 可能會導致伺服器速度變慢，且AEM Forms的效能會受到影響。

若要改善效能，您可以直接使用防毒軟體，將下列AEM Forms檔案和資料夾排除在永遠開啟（隨選）掃描之外：

* AEM安裝目錄。 如果無法排除完整的目錄，請排除下列專案：

   * [AEM安裝目錄]\crx-repository\temp
   * [AEM安裝目錄]\crx-repository\repository
   * [AEM安裝目錄]\crx-repository\launchpad

* 應用程式伺服器暫存目錄。 預設位置為：

   * (JBoss®) [AEM安裝目錄]\jboss\standalone\tmp
   * (WebLogic) \Oracle\Middleware\user_projects\domains\LCDomain\servers\LCServer1\tmp
   * (WebSphere®) \程式Files\IBM\WebSphere\AppServer\profiles\AppSrv01\temp

* **(僅限JEE上的AEM Forms)**&#x200B;全域檔案儲存(GDS)目錄。 預設位置為：

   * (JBoss®) [appserver root]/server/&#39;server&#39;/svcnative/DocumentStorage
   * (WebLogic) [appserverdomain]/&#39;server&#39;/adobe/LiveCycleServer/DocumentStorage
   * (WebSphere®) [appserver root]/installedApps/adobe/&#39;server&#39;/DocumentStorage

* **(僅限JEE上的AEM Forms)** AEM Forms伺服器記錄檔和暫存目錄。 預設位置為：

   * 伺服器記錄檔 — [AEM Forms安裝目錄]\Adobe\AEM forms\[app-server]\server\all\logs
   * 暫存目錄 — [AEM Forms安裝目錄]\temp

>[!NOTE]
>
>* 如果您使用不同的GDS和暫存目錄位置，請開啟`https://'[server]:[port]'/adminui`的AdminUI，瀏覽至&#x200B;**首頁>設定>核心系統設定>核心設定**&#x200B;以確認使用中的位置。
>
* 如果排除建議的目錄後AEM Forms伺服器執行速度會很慢，則同時排除Java™可執行檔(java.exe)。
>
