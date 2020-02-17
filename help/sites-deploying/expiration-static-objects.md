---
title: 靜態對象的過期
seo-title: 靜態對象的過期
description: 瞭解如何設定AEM，讓靜態物件不會過期（在合理的時段內）。
seo-description: 瞭解如何設定AEM，讓靜態物件不會過期（在合理的時段內）。
uuid: ee019a3d-4133-4d40-98ec-e0914b751fb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 73f37b3c-5dbe-4132-bb60-daa8de871884
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 靜態對象的過期{#expiration-of-static-objects}

靜態物件（例如圖示）不會變更。 因此，應將系統配置為不會過期（在合理的時間段內），從而減少不必要的通信。

其影響如下：

* 卸載伺服器基礎架構中的請求。
* 當瀏覽器在瀏覽器快取中快取物件時，可提高頁面載入的效能。

過期時間由HTTP標準指定，與檔案的「過期」有關(例如，請參閱 [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) &quot;超文本傳輸協定— HTTP 1.1&quot;的第14.21章)。 此標準使用標題來允許用戶端快取物件，直到物件被視為過時；這些對象被快取指定的時間長度，而不對源伺服器進行任何狀態檢查。

>[!NOTE]
>
>此配置與Dispatcher完全不同（且不適用於）。
>
>Dispatcher的用途是在AEM之前快取資料。

所有非動態且不會隨著時間而變更的檔案都可以且應該快取。 Apache HTTPD伺服器的配置可能類似於下列配置之一——取決於環境：

>[!CAUTION]
>
>在定義對象被視為最新的時間段時，必須小心。 由於在指 *定的時段到期之前沒有檢查*，所以客戶端最終可以從快取中呈現舊內容。

1. **對於「作者」實例：**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /libs>
     ExpiresByType text/css "access plus 1 month"
     ExpiresByType text/javascript "access plus 1 month"
     ExpiresByType image/png "access plus 1 month"
     ExpiresByType image/gif "access plus 1 month"
   </Location>
   ```

   這可讓中介快取（例如瀏覽器快取）儲存CSS、Javascript、PNG和GIF檔案最多一個月，直到過期為止。 這表示不需要從AEM或webserver要求這些檔案，但可以保留在瀏覽器快取中。

   網站的其他區段不應快取至作者例項，因為這些區段隨時可能會變更。

1. **對於「發佈」例項：**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /content>
     ExpiresByType text/css "access plus 1 day"
     ExpiresByType text/javascript "access plus 1 day"
     ExpiresByType image/png "access plus 1 day"
     ExpiresByType image/gif "access plus 1 day"
   </Location>
   <Location /etc/designs>
     ExpiresByType text/css "access plus 1 day"
     ExpiresByType text/javascript "access plus 1 day"
     ExpiresByType image/png "access plus 1 day"
     ExpiresByType image/gif "access plus 1 day"
   </Location>
   ```

   這允許中間快取（例如瀏覽器快取）在用戶端快取中儲存CSS、Javascript、PNG和GIF檔案，最多一天。 雖然此範例說明下列和項目的全域 `/content` 設定 `/etc/designs`，但您應更精細。

   您也可以考慮快取HTML頁面，視網站的更新頻率而定。 合理的時段為1小時：

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

配置靜態對象後，在選擇包含這些對象的頁 `request.log`面時，請掃描，以確認沒有對靜態對象發出（不必要）請求。
