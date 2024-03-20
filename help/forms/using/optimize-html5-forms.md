---
title: 最佳化HTML5表單
description: 您可以最佳化HTML5表單的輸出大小。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdb9edc2-6a37-4d3f-97d5-0fc5664316be
feature: HTML5 Forms
exl-id: 14309ebd-8d00-4ca5-b4ab-44d80d97d066
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# 最佳化HTML5表單 {#optimizing-html-forms}

HTML5表單會以HTML5格式轉譯表單。 根據表單的表單大小和影像等因素，產生的輸出可能會很大。 為了最佳化資料傳輸，建議使用提供請求的Web伺服器來壓縮HTML回應。 此方法可減少回應大小、網路流量，以及在伺服器和使用者端電腦之間串流資料所需的時間。

本文說明使用JBoss為Apache Web Server 2.0 32位元啟用壓縮的必要步驟。

>[!NOTE]
>
>下列指示不適用於Apache Web Server 2.0 32位元以外的伺服器。

取得適用於您作業系統的Apache Web Server軟體：

* 若為Windows，請從Apache HTTP Server Project網站下載Apache Web Server。
* 若為Solaris 64位元，請從Sunfreeware for Solaris網站下載Apache Web Server。
* 在Linux系統中，Apache Web Server是預先安裝在Linux系統上。

Apache可以使用HTTP或AJP通訊協定與JBoss通訊。

1. 在中取消註解以下模組設定 *APACHE_HOME/conf/httpd.conf* 檔案。

   ```java
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >對於Linux，預設的APACHE_HOME目錄為/etc/httpd/。

1. 在JBoss的連線埠8080上設定Proxy。

   將下列設定新增至 *APACHE_HOME/conf/httpd.conf* 組態檔。

   ```java
   ProxyPass / https://<server_Name>:8080/
   ProxyPassReverse / https://<server_Name>:8080/
   ```

   >[!NOTE]
   >
   >使用Proxy時，需要變更下列設定：
   >
   >* 存取： *https://&lt;server>：&lt;port>/system/console/configMgr*
   * 編輯Apache Sling查閱者篩選器的設定
   * 在允許主機中，新增代理主機伺服器的專案

1. 啟用壓縮。

   將下列設定新增至 *APACHE_HOME/conf/httpd.conf* 組態檔。

   ```xml
   <Location /content/xfaforms>
     <IfModule mod_deflate.c>
        SetOutputFilter DEFLATE
        # Don’t compress
        SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
        SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
       #Dealing with proxy servers
   
        <IfModule mod_headers.c>
           Header append Vary User-Agent
        </IfModule>
     </IfModule>
   </Location>
   ```

1. 若要存取AEM伺服器，請使用https://[Apache_server]：80。
