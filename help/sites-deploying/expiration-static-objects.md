---
title: 靜態物件的到期日
description: 瞭解如何設定Adobe Experience Manager，讓靜態物件不會在合理的時間內過期。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: bfd5441c-19cc-4fa8-b597-b1221465f75d
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# 靜態物件的到期日{#expiration-of-static-objects}

靜態物件（例如圖示）不會變更。 因此，系統應設定為不會過期（在合理的時間範圍內），並減少不必要的流量。

這會造成下列影響：

* 從伺服器基礎結構解除安裝請求。
* 當瀏覽器快取瀏覽器快取中的物件時，提高頁面載入的效能。

到期日由HTTP標準所指定，與檔案的「到期日」有關（例如，請參閱[RFC 2616](https://www.ietf.org/rfc/rfc2616.txt)「超文字傳輸通訊協定 — HTTP 1.1」的第14.21章）。 此標準會使用標頭來允許使用者端快取物件，直到它們被視為過時；這些物件會快取指定的時間量，而不會對原始伺服器進行任何狀態檢查。

>[!NOTE]
>
>此設定與Dispatcher不同（且無法運作）。
>
>Dispatcher的目的是將資料快取到Adobe Experience Manager (AEM)前面。

所有非動態且不會隨時間變化的檔案都可以且應該快取。 Apache HTTPD伺服器的設定可能如以下任一項 — 取決於環境：

>[!CAUTION]
>
>定義將物件視為最新的時段時，請務必小心。 因為指定時段到期之前&#x200B;*沒有檢查*，所以使用者端最終可以從快取中呈現舊內容。

1. **對於作者執行個體：**

   ```xml
   LoadModule expires_module modules/mod_expires.so
   <Location /libs>
     ExpiresByType text/css "access plus 1 month"
     ExpiresByType text/javascript "access plus 1 month"
     ExpiresByType image/png "access plus 1 month"
     ExpiresByType image/gif "access plus 1 month"
   </Location>
   ```

   這可讓中繼快取（例如瀏覽器快取）將CSS、JavaScript、PNG和GIF檔案儲存長達一個月，直到檔案過期為止。 這表示不需要從AEM或Web伺服器要求這些篩選器，但可保留在瀏覽器快取中。

   不應在製作執行個體上快取網站的其他區段，因為這些區段隨時可能變更。

1. **適用於Publish執行個體：**

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

   這可讓中繼快取（例如瀏覽器快取）將CSS、JavaScript、PNG和GIF檔案儲存在使用者端快取中長達一天。 雖然此範例說明低於`/content`和`/etc/designs`的所有專案的全域設定，但您應該讓它更精細。

   根據網站更新頻率的不同，您也可以考慮快取HTML頁面。 合理的時段為一小時：

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

設定好靜態物件後，在選取存放此類物件的頁面時掃描`request.log`，以確認沒有對靜態物件發出任何（不必要的）要求。
