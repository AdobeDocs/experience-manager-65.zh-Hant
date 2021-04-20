---
title: AEM Forms 伺服器的效能調整
seo-title: AEM Forms 伺服器的效能調整
description: 若要讓AEM Forms發揮最佳效能，您可以微調快取設定和JVM參數。 此外，使用Web伺服器可以增強AEM Forms部署的效能。
seo-description: 若要讓AEM Forms發揮最佳效能，您可以微調快取設定和JVM參數。 此外，使用Web伺服器可以增強AEM Forms部署的效能。
uuid: bf23b62c-7559-4726-8f4e-cc8b1457e501
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 38c0ec46-5686-4656-bfb4-7125ec194673
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 2%

---


# AEM Forms 伺服器的效能調整{#performance-tuning-of-aem-forms-server}

本文討論您可以實施的策略和最佳實踐，以減少瓶頸並優化AEM Forms部署的效能。

## 快取設定{#cache-settings}

您可以使用Web配置控制台中的&#x200B;**移動Forms配置**&#x200B;元件來配置和控制AEM Forms的快取AEM策略：

* (AEM FormsOSGi)`https://'[server]:[port]'/system/console/configMgr`
* (AEM FormsJEE)`https://'[server]:[port]'/lc/system/console/configMgr`

快取的可用選項如下：

* **無**:強制不快取任何對象。實際上，這會降低效能，並且由於缺少快取而需要高記憶體可用性。
* **保守**:指定僅快取在呈現表單之前生成的中間對象，例如包含內嵌片段和影像的模板。
* **咄咄逼人**:強制快取幾乎所有可快取的項目，包括從「保守」快取層級轉換的HTML內容。它會產生最佳效能，但也會耗用更多記憶體來儲存快取的工件。 積極的快取策略意味著，當快取轉譯內容時，您在轉譯表格時，會獲得持續的時間效能。

AEM Forms的預設快取設定可能不足以達到最佳效能。 因此，建議使用下列設定：

* **快取策略**:攻擊性
* **快取大小** （以表格數量計）:視需要
* **最大物件大小**:視需要

![行動Forms組態](assets/snap.png)

>[!NOTE]
>
>如果您使AEM用Dispatcher來快取最適化表單，它也會快取包含預先填入資料之表單的最適化表單。 如果這些表單是從AEMDispatcher快取中提供的，則可能導致向用戶提供預填充或過時的資料。 因此，請使AEM用Dispatcher來快取不使用預先填入資料的最適化表單。 此外，調度器快取不會自動使快取的片段無效。 因此，請勿使用它來快取表單片段。 對於此類表單和片段，請使用[最適化表單快取](../../forms/using/configure-adaptive-forms-cache.md)。

## JVM參數{#jvm-parameters}

為獲得最佳效能，建議使用以下JVM `init`參數來配置`Java heap`和`PermGen`。

```shell
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xms8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -Xmx8192m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:PermSize=256m
set CQ_JVM_OPTS=%CQ_JVM_OPTS% -XX:MaxPermSize=1024m
```

>[!NOTE]
>
>建議的設定適用於Windows 2008 R2 8核心和Oracle式HotSpot 1.7（64位元）JDK，應根據您的系統配置放大或縮小。

## 使用Web伺服器{#using-a-web-server}

最適化表單和HTML5表單會以HTML5格式演算。 產生的輸出可能會大，視表單大小和影像等因素而定。 為了最佳化資料傳輸，建議的方法是使用提供要求的網頁伺服器來壓縮HTML回應。 此方法可減少回應大小、網路流量，以及在伺服器與用戶端機器之間串流資料所需的時間。

例如，執行以下步驟以對具有JBoss的Apache Web Server 2.0 32位啟用壓縮：

>[!NOTE]
>
>以下說明不適用於除Apache Web Server 2.0 32位元以外的任何伺服器。 如需其他伺服器的特定步驟，請參閱相應的產品檔案。

以下步驟演示了使用Apache Web Server啟用壓縮所需的更改

**取得適用於您作業系統的Apache網路伺服器軟體**

* Windows:從Apache HTTP Server項目站點下載Apache Web伺服器。
* Solaris 64位：從Sunfreeware for Solaris網站下載Apache Web伺服器。
* Linux:apache Web伺服器已預安裝在Linux系統上。

Apache可以使用HTTP通訊協定與CRX通訊。 這些配置是用於使用HTTP進行優化的。

1. 在`APACHE_HOME/conf/httpd.conf`檔案中取消對以下模組配置的注釋。

   ```shell
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >對於Linux，預設`APACHE_HOME`為`/etc/httpd/`。

1. 在crx的埠4502上配置代理。
在`APACHE_HOME/conf/httpd.conf`配置檔案中添加以下配置。

   ```shell
   ProxyPass / https://<server>:4502/
   ProxyPassReverse / https://<server>:4502/
   ```

1. 啟用壓縮。 在`APACHE_HOME/conf/httpd.conf`配置檔案中添加以下配置。

   **針對HTML5表格**

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

   **針對最適化表單**

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

   要訪問crx伺服器，請使用`https://'server':80` ，其中`server`是運行Apache伺服器的伺服器的名稱。

## 在運行AEM Forms{#using-an-antivirus-on-server-running-aem-forms}的伺服器上使用防病毒軟體

在運行防病毒軟體的伺服器上，您可能會遇到效能降低的問題。 一律開啟防病毒（按訪問掃描）軟體會掃描系統的所有檔案。 它會減緩伺服器的速度，並影響AEM Forms的效能。

要提高效能，您可以指導防病毒軟體將下列AEM Forms檔案和資料夾從永遠開啟（訪問）掃描中排除：

* 安AEM裝目錄。 如果無法排除完整目錄，請排除下列項目：

   * [安AEM裝目錄]\crx-repository\temp
   * [安AEM裝目錄]\crx-repository\repository
   * [安AEM裝目錄]\crx-repository\launchpad

* 應用程式伺服器臨時目錄。 預設位置為：

   * (Jboss)[AEM安裝目錄]\jboss\standalone\tmp
   * (Weblogic)\Oracle\Middleware\user_projects\domains\LCDomain\servers\LCServer1\tmp
   * (Websphere)\Program Files\IBM\WebSphere\AppServer\profiles\AppSrv01\temp

* **(AEM Forms僅限JEE)全** 域檔案儲存(GDS)目錄。預設位置為：

   * (JBoss)[appserver root]/server/&#39;server&#39;/svcnative/DocumentStorage
   * (WebLogic)[appserverdomain]/&#39;server&#39;/adobe/LiveCycleServer/DocumentStorage
   * (WebSphere)[appserver root]/installedApps/adobe/&#39;server&#39;/DocumentStorage

* **(僅AEM Forms在JEE上)** AEM Forms伺服器日誌和臨時目錄。預設位置為：

   * 伺服器日誌- [AEM Forms安裝目錄]\Adobe\AEM forms\[app-server]\server\all\logs
   * Temp目錄- [AEM Forms安裝目錄]\temp

>[!NOTE]
>
>* 如果您對GDS和臨時目錄使用不同位置，請在`https://'[server]:[port]'/adminui`開啟AdminUI，導覽至&#x200B;**首頁>設定>核心繫統設定>核心組態**&#x200B;以確認使用中的位置。

* 如果AEM Forms伺服器在排除建議的目錄後執行速度變慢，則也排除Java執行檔(java.exe)。



