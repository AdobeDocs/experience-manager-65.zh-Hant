---
title: 代理伺服器工具(proxy.jar)
seo-title: Proxy Server Tool (proxy.jar)
description: 瞭解中的代理伺服器工AEM具。
seo-description: Learn about the Proxy Server Tool in AEM.
uuid: 2fc1df24-8d5a-4be7-83fa-238ae65591b0
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: ca98dc3c-7056-4cdc-b4d3-23e471da5730
docset: aem65
exl-id: 3df50303-5cdd-4df0-abec-80831d2ccef7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 0%

---

# 代理伺服器工具(proxy.jar){#proxy-server-tool-proxy-jar}

代理伺服器充當在客戶機和伺服器之間中繼請求的中間伺服器。 代理伺服器跟蹤所有客戶端與伺服器的交互，並輸出整個TCP通信的日誌。 這樣，您就可以準確監視正在進行的操作，而無需訪問主伺服器。

您可以在相應的安裝資料夾中找到代理伺服器：

* &lt;cq_install_path>/opt/helpers/proxy.jar
* &lt;crx_install_path>/opt/helpers/proxy.jar

您可以使用代理伺服器來監視所有客戶端與伺服器的交互，而不管底層通信協定如何。 例如，可以監視以下協定：

* 網頁的HTTP
* 用於安全網頁的HTTPS
* 電子郵件的SMTP
* 用於用戶管理的LDAP

例如，可以在通過TCP/IP網路通信的任何兩個應用程式之間放置代理伺服器；例如Web瀏覽器和AEM。 這允許您準確監視請求頁面時發生的AEM情況。

## 啟動代理伺服器工具 {#starting-the-proxy-server-tool}

該工具可在安裝的/opt/helpers資料夾中找AEM到。 要啟動它，請鍵入：

```xml
java -jar proxy.jar <host> <remoteport> <localport> [options]
```

### 選項 {#options}

* **q（安靜模式）** 不將請求寫入控制台窗口。 如果不想減慢連接速度，或者將輸出記錄到檔案（請參見 — logfile選項），則使用此選項。
* **b（二進位模式）** 如果要查找通信中的特定位元組組合，請啟用二進位模式。 輸出將包含十六進位和字元輸出。
* **t（時間戳日誌條目）** 為每個日誌輸出添加時間戳。 時間戳以秒為單位，因此可能不適合檢查單個請求。 如果在較長的時間段內使用代理伺服器，則使用它查找在特定時間發生的事件。
* **日誌檔案 &lt;filename> （寫入日誌檔案）** 將客戶端 — 伺服器對話寫入日誌檔案。 此參數也在安靜模式下工作。
* **我 &lt;numindentions> （添加縮進）** 每個活動連接都縮進，以便更好地讀取。 預設為16級。 （proxy.jar 1.16版中的新增功能）。

## 代理伺服器工具的使用 {#uses-of-the-proxy-server-tool}

以下情形說明了可以使用代理伺服器工具的幾種用途：

**檢查Cookie及其值**

以下日誌條目示例顯示自代理啟動以來第6個連接開啟時客戶端發送的所有cookie及其值：

```xml
C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]
```

**檢查標題及其值** 以下日誌條目示例說明伺服器能夠建立保持活動連接，並且內容長度標頭已正確設定：

```xml
S-7-#000017 -> [Connection: Keep-Alive ]
...
S-7-#000107 -> [Content-Length: 124 ]
```

**檢查Keep-Alive是否工作**

**保持活動** 表示客戶端重新使用與伺服器的連接來傳輸多個檔案（頁碼、圖片、樣式表等）。 如果沒有保持活動狀態，客戶端必須為每個請求建立新連接。

要檢查保持活動是否有效，請執行以下操作：

1. 啟動代理伺服器。
1. 請求頁面。

* 如果keep-alive正在工作，則連接計數器不應超過5到10個連接。
* 如果保持活動狀態不工作，則連接計數器會迅速增加。

**查找丟失的請求**

如果在複雜的伺服器設定中丟失請求，則可以使用代理伺服器查找請求丟失的位置。 在防火牆的情況下：

1. 在防火牆之前啟動代理
1. 在防火牆後啟動另一個代理
1. 使用這些可查看請求的距離。

**掛起請求**

如果您不時遇到掛起請求：

1. 啟動proxy.jar。
1. 等待訪問日誌或將其寫入檔案 — 每個條目都有時間戳。
1. 當請求開始掛起時，您可以看到開啟了多少個連接，以及哪個請求導致了問題。

## 日誌消息的格式 {#the-format-of-log-messages}

proxy.jar生成的日誌條目都具有以下格式：

```xml
[timestamp (optional)] [<b>C</b>lient|<b>S</b>erver]-[ConnectionNumber]-[BytePosition] ->[Character Stream]
```

例如，對Web頁的請求可能如下所示：

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]
```

* C表示此條目來自客戶端（它是對Web頁的請求）
* 0是連接號（連接計數器從0開始）
* #00000位元組流中的偏移。 這是第一個條目，因此偏移為0。
* [GET &lt;?>] 是請求的內容，在示例中，HTTP標頭之一(url)。

連接關閉時，將記錄以下資訊：

```xml
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

這顯示在第6個連接上以平均速度在客戶端和伺服器之間傳遞的位元組數。

## 日誌輸出示例 {#an-example-of-log-output}

我們將審閱一個簡單的模板，該模板在請求時生成以下代碼：

```xml
<html>
  <head>
    <title>Welcome</title>
  </head>
  <body>
    Welcome to Playground<br>
    <img src="/logo.gif">
  </body>
</html>
```

如AEM果在localhost:4303上運行，請按如下方式啟動代理伺服器：

```xml
java -jar proxy.jar localhost 4303 4444 -logfile test.log
```

您可以訪問伺服器(`localhost:4303`)，但如果通過 `localhost:4444`，代理伺服器將記錄通信。 開啟瀏覽器並訪問使用上述模板建立的頁面。 然後，查看日誌檔案。

>[!NOTE]
>
>在proxy.jar 1.14版之前，一個連接的日誌項不會同步，這意味著一個客戶端/伺服器連接的日誌項不必按正確的順序排列。 代理伺服器的較新版本(>=1.14)不存在此問題。

啟動時，以下資訊將寫入日誌：

```xml
starting proxy for localhost:4303 on port 4444
using logfile: C:\CQUnify355default\opt\helpers\test.log
```

在請求主HTML頁的第一個連接(0)開始處列出以下標題欄位：

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102936796533 HTTP/1.1 ]
C-0-#000053 -> [Accept: image/gif, image/x-xbitmap, image/jpeg, image/pjpeg, application/vnd.ms-powerpoint, application/vnd.ms-excel, application/msword, appl]
C-0-#000194 -> [ication/x-shockwave-flash, */* ]
C-0-#000227 -> [Accept-Language: de-ch ]
C-0-#000251 -> [Accept-Encoding: gzip, deflate ]
C-0-#000283 -> [User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0) ]
C-0-#000347 -> [Host: localhost:4444 ]
```

客戶端請求保持連接，以便伺服器可以通過同一連接發送多個檔案：

```xml
C-0-#000369 -> [Connection: Keep-Alive ]
```

代理伺服器是驗證Cookie是否正確設定的好工具。 這裡，我們看到：

* cq3session cookie生AEM成
* 由CFC生成的show mode開關cookie
* 名為JSESSIONID的cookie;如果未使用&lt;%@ page session=&quot;false&quot; %>顯式關閉，則JSP會自動建立此對話框：

```xml
C-0-#000393 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-0-#000514 -> [ ]
S-0-#000000 -> [HTTP/1.0 200 OK ]
```

伺服器將在請求後關閉連接0。 無法保持活動狀態，因為請求有問號。 這意味著伺服器無法返回快取版本，因此無法確定此時的內容長度，這是保持活動連接所需的長度。

```xml
S-0-#000017 -> [Connection: Close ]
S-0-#000036 -> [Server: Communique Servlet Engine/3.5.5 ]
S-0-#000077 -> [Content-Type: text/html;charset=iso-8859-1 ]
S-0-#000121 -> [Date: Tue, 14 Dec 2004 09:46:44 GMT ]
S-0-#000158 -> [Set-Cookie: JSESSIONID=4161a56b-f193-d8-88a5-e09c5ff7ef2a;Path=/author ]
S-0-#000232 -> [ ]
```

在此，伺服器開始在連接0上發送HTML代碼：

```xml
S-0-#000234 -> [<html> ]
S-0-#000242 -> [.<head> ]
S-0-#000251 -> [..<title>Welcome</title> ]
S-0-#000277 -> [.</head> ]
S-0-#000287 -> [.<body> ]
S-0-#000296 -> [..Welcome to Playground<br> ]
S-0-#000325 -> [..<img src="/author/logo.gif"> ]
S-0-#000357 -> [.</body> ]
S-0-#000367 -> [</html>]
```

在HTML檔案送達後，連接0立即關閉：

```xml
C-0-Finished: 516 bytes (0.0 kb/s)
S-0-Finished: 374 bytes (0.0 kb/s)
```

現在，連接1的輸出將開始，該連接將下載包含在HTML代碼中的映像：

```xml
C-1-#000000 -> [GET /author/logo.gif HTTP/1.1 ]
C-1-#000031 -> [Accept: */* ]
C-1-#000044 -> [Referer: http://localhost:4444/author/prox.html?CFC_cK=1102936796533 ]
C-1-#000114 -> [Accept-Language: de-ch ]
C-1-#000138 -> [Accept-Encoding: gzip, deflate ]
C-1-#000170 -> [User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0) ]
C-1-#000234 -> [Host: localhost:4444 ]
```

同樣，客戶端請求保持活動連接：

```xml
C-1-#000256 -> [Connection: Keep-Alive ]
C-1-#000280 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-1-#000401 -> [ ]
S-1-#000000 -> [HTTP/1.0 200 OK ]
```

對於連接1，伺服器可以提供保持活動，因為影像是靜態的，因此內容長度是已知的。

```xml
S-1-#000017 -> [Connection: Keep-Alive ]
S-1-#000041 -> [Server: Communique Servlet Engine/3.5.5 ]
S-1-#000082 -> [Content-Type: image/gif ]
```

伺服器返回連接1上映像的內容長度：

```xml
S-1-#000107 -> [Content-Length: 124 ]
S-1-#000128 -> [Date: Tue, 14 Dec 2004 09:46:44 GMT ]
S-1-#000165 -> [ ]
```

現在，內容長度已建立，伺服器將在連接1上發送影像資料：

```xml
S-1-#000167 -> [GIF87a..........................,.......
...I....0.A..8......YDA.W...1..`i.`..6...Z...$@.F..)`..f..A.....iu.........$..;]
```

在達到keep-alive超時後，連接1也將關閉：

```xml
S-1-Finished: 291 bytes (0.0 kb/s)
C-1-Finished: 403 bytes (0.0 kb/s)
```

上例相對簡單，因為兩個連接按順序發生：

* 首先，伺服器返回HTML代碼
* 然後瀏覽器請求影像並開啟新連接

實際上，頁面可能會生成許多對影像、樣式表、JavaScript檔案等的並行請求。 這意味著日誌具有並行開啟連接的重疊條目。 在這種情況下，我們建議使用選項 — i來提高可讀性。
