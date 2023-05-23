---
title: 優化HTML5窗體
seo-title: Optimizing HTML5 forms
description: 可以優化HTML5窗體的輸出大小。
seo-description: You can optimize the output size of the HTML5 forms.
uuid: 959f0b6a-9e4d-478a-afa8-4c39011fdf7a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdb9edc2-6a37-4d3f-97d5-0fc5664316be
feature: Mobile Forms
exl-id: 14309ebd-8d00-4ca5-b4ab-44d80d97d066
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# 優化HTML5窗體 {#optimizing-html-forms}

HTML5窗體以HTML5格式呈現窗體。 結果輸出可能會很大，具體取決於窗體大小和窗體中的影像等因素。 為了優化資料傳輸，建議的方法是使用從中提供請求的Web伺服器壓縮HTML響應。 此方法可減少響應大小、網路流量，以及在伺服器和客戶機之間傳輸資料所需的時間。

本文介紹使用JBoss為Apache Web Server 2.0 32位啟用壓縮所需的步驟。

>[!NOTE]
>
>以下說明不適用於除Apache Web Server 2.0 32位以外的伺服器。

獲取適用於您的作業系統的Apache Web伺服器軟體：

* 對於Windows，從Apache HTTP Server項目站點下載Apache Web伺服器。
* 對於Solaris 64位，請從Sunfreeware for Solaris網站下載Apache Web伺服器。
* 對於Linux,Apache Web伺服器預安裝在Linux系統上。

Apache可以使用HTTP或AJP協定與JBoss通信。

1. 取消注釋中的以下模組配置 *APACHE_HOME/conf/httpd.conf* 的子菜單。

   ```java
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >對於Linux，預設的APACHE_HOME目錄為/etc/httpd/。

1. 在JBoss的埠8080上配置代理。

   將以下配置添加到 *APACHE_HOME/conf/httpd.conf* 配置檔案。

   ```java
   ProxyPass / https://<server_Name>:8080/
   ProxyPassReverse / https://<server_Name>:8080/
   ```

   >[!NOTE]
   >
   >使用代理時，需要更改以下配置：
   >
   >* 訪問： *https://&lt;server>:&lt;port>/system/console/configMgr*
   * 編輯Apache Sling引用過濾器的配置
   * 在允許主機中，添加代理伺服器的項


1. 啟用壓縮。

   將以下配置添加到 *APACHE_HOME/conf/httpd.conf* 配置檔案。

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

1. 要訪問服AEM務器，請使用https://[Apache伺服器]:80。
