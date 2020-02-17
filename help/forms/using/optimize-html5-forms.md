---
title: 最佳化HTML5表單
seo-title: 最佳化HTML5表單
description: 您可以最佳化HTML5表單的輸出大小。
seo-description: 您可以最佳化HTML5表單的輸出大小。
uuid: 959f0b6a-9e4d-478a-afa8-4c39011fdf7a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdb9edc2-6a37-4d3f-97d5-0fc5664316be
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 最佳化HTML5表單 {#optimizing-html-forms}

HTML5表格會以HTML5格式轉譯表格。 產生的輸出可能會大，視表單大小和影像等因素而定。 為了最佳化資料傳輸，建議的方法是使用提供請求的Web伺服器來壓縮HTML回應。 此方法可減少回應大小、網路流量，以及在伺服器與用戶端機器之間串流資料所需的時間。

本文介紹使用JBoss為Apache Web Server 2.0 32位啟用壓縮所需的步驟。

*注意：以下說明不適用於Apache Web Server 2.0 32位元以外的伺服器。*

取得適用於您作業系統的Apache網路伺服器軟體：

* 對於Windows，請從Apache HTTP Server項目站點下載Apache Web伺服器。
* 對於Solaris 64位，請從Sunfreeware for Solaris網站下載Apache Web伺服器。
* 對於Linux,Apache web伺服器已預安裝在Linux系統上。

Apache可以使用HTTP或AJP協定與JBoss通信。

1. 在APACHE_HOME/conf/httpd.conf檔案中取消對以下模組配 *置的注* 釋。

   ```java
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >對於Linux，預設的APACHE_HOME目錄為/etc/httpd/。

1. 在JBoss的埠8080上配置代理。

   將下列配置添加到 *APACHE_HOME/conf/httpd.conf* 配置檔案。

   ```java
   ProxyPass / https://<server_Name>:8080/
   ProxyPassReverse / https://<server_Name>:8080/
   ```

   >[!NOTE]
   >
   >使用Proxy時，需要進行下列組態變更：
   >
   >* 存取： *https://&lt;server>:&lt;port>/system/console/configMgr*
   * 編輯Apache Sling Referrer Filter的設定
   * 在「允許主機」中，添加代理伺服器的條目


1. 啟用壓縮。

   將下列配置添加到 *APACHE_HOME/conf/httpd.conf* 配置檔案。

   ```java
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

1. 若要存取AEM伺服器，請使用https://[Apache_server]:80。

**[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)**
