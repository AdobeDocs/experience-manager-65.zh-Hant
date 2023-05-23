---
title: 靜態對象的到期
seo-title: Expiration of Static Objects
description: 瞭解如何配AEM置以使靜態對象不會過期（在合理的時間段內）。
seo-description: Learn how to configure AEM so that static objects do not expire (for a reasonable period of time).
uuid: ee019a3d-4133-4d40-98ec-e0914b751fb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 73f37b3c-5dbe-4132-bb60-daa8de871884
feature: Configuring
exl-id: bfd5441c-19cc-4fa8-b597-b1221465f75d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# 靜態對象的到期{#expiration-of-static-objects}

靜態對象（例如，表徵圖）不會更改。 因此，應配置系統，使其不會過期（在合理的時間段內），從而減少不必要的通信量。

這具有以下影響：

* 卸載來自伺服器基礎架構的請求。
* 當瀏覽器在瀏覽器快取中快取對象時，提高頁面載入的效能。

過期由HTTP標準指定，涉及檔案的「過期」(例如，請參閱的第14.21章 [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) &quot;超文本傳輸協定 — HTTP 1.1&quot;)。 此標準使用標題，允許客戶端在對象被視為過時之前快取對象；這些對象被快取指定的時間量，而不對始發伺服器進行任何狀態檢查。

>[!NOTE]
>
>此配置與Dispatcher完全分離（並且不適用於）。
>
>Dispatcher的目的是在前面快取數AEM據。

所有檔案（不是動態的，並且不隨時間而改變）都可以且應該進行快取。 Apache HTTPD伺服器的配置可能類似於以下配置之一 — 取決於環境：

>[!CAUTION]
>
>在定義對象被視為最新的時間段時，必須小心。 因為 *在指定的時間段過期之前不檢查*，客戶端最終可以從快取中呈現舊內容。

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

   這允許中間快取（例如瀏覽器快取）最多儲存一個月的CSS、Javascript、PNG和GIF檔案，直到它們過期。 這意味著不需要從或Web伺服器請求AEM它們，但可以保留在瀏覽器快取中。

   站點的其他部分不應快取在作者實例上，因為它們隨時可能更改。

1. **對於發佈實例：**

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

   這允許中間快取（例如瀏覽器快取）在客戶端快取中儲存一天的CSS、Javascript、PNG和GIF檔案。 儘管此示例說明了下面所有內容的全局設定 `/content` 和 `/etc/designs`你應該讓它更細緻。

   根據站點更新的頻率，您還可以考慮快取HTML頁。 合理的時間段為1小時：

   ```xml
   <Location /content>
     ExpiresByType text/html "access plus 1 hour"
   </Location>
   ```

配置靜態對象後，掃描 `request.log`，在選擇保存此類對象的頁面時，確認沒有為靜態對象發出（不必要）請求。
