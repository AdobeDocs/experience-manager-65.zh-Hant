---
title: 代理伺服器工具(proxy.jar)
seo-title: 代理伺服器工具(proxy.jar)
description: 瞭解AEM中的Proxy Server Tool。
seo-description: 瞭解AEM中的Proxy Server Tool。
uuid: 2fc1df24-8d5a-4be7-83fa-238ae65591b0
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: ca98dc3c-7056-4cdc-b4d3-23e471da5730
docset: aem65
translation-type: tm+mt
source-git-commit: 4e5e6ef022dc9f083859e13ab9c86b622fc3d46e

---


# 代理伺服器工具(proxy.jar){#proxy-server-tool-proxy-jar}

代理伺服器充當在客戶機和伺服器之間中繼請求的中間伺服器。 代理伺服器跟蹤所有客戶機與伺服器的交互，並輸出整個TCP通信的日誌。 這樣，您就可以完全監視當前的情況，而無需訪問主伺服器。

您可以在適當的安裝資料夾中找到代理伺服器：

* &lt;cq_install_path>/opt/helpers/proxy.jar
* &lt;crx_install_path>/opt/helpers/proxy.jar

您可以使用代理伺服器來監視所有客戶端與伺服器的交互，而不管底層的通信協定如何。 例如，您可以監控下列通訊協定：

* 網頁的HTTP
* HTTPS用於安全網頁
* 電子郵件的SMTP
* 用於用戶管理的LDAP

例如，您可以將代理伺服器放在通過TCP/IP網路通信的任意兩個應用程式之間；例如網頁瀏覽器和AEM。 這可讓您監控當您請求AEM頁面時的實際情況。

## 啟動代理伺服器工具 {#starting-the-proxy-server-tool}

此工具可在AEM安裝的/opt/helpers檔案夾中找到。 要啟動它，請鍵入：

```xml
java -jar proxy.jar <host> <remoteport> <localport> [options]
```

### 選項 {#options}

* **q（安靜模式）** Does not write the requests to the console window. 如果您不想減慢連接速度，或者將輸出記錄到檔案（請參見-logfile選項），請使用此選項。
* **b（二進位模式）** ，如果您要尋找流量中的特定位元組組合，請啟用二進位模式。 然後，輸出將包含十六進位和字元輸出。
* **t（時間戳記記錄項目）** ，將時間戳記新增至每個記錄輸出。 時間戳記以秒為單位，因此可能不適合檢查單一請求。 如果您在較長的時段內使用代理伺服器，則可使用它來查找在特定時間發生的事件。
* **logfile &lt;filename>（寫入日誌檔案）** ，將客戶機——伺服器會話寫入日誌檔案。 此參數也可在安靜模式下運作。
* **i &lt;numIndentions>（新增縮進）** ，每個作用中的連線都會縮進以提高可讀性。 預設為16層。 （proxy.jar 1.16版中的新功能）。

## 代理伺服器工具的使用 {#uses-of-the-proxy-server-tool}

以下案例說明了Proxy Server Tool可用於的一些用途：

**檢查Cookie及其值**

以下日誌條目示例顯示自代理啟動以來第6個連接開啟時客戶端發送的所有Cookie及其值：

```xml
C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]
```

**檢查標題及其值** ：以下日誌條目示例顯示伺服器能夠建立保持活動連接，並且內容長度標題已正確設定：

```xml
S-7-#000017 -> [Connection: Keep-Alive ]
...
S-7-#000107 -> [Content-Length: 124 ]
```

**檢查Keep-Alive是否有效**

**Keep-Alive** 意指用戶端重新使用伺服器連線來傳輸多個檔案（頁面程式碼、圖片、樣式表等）。 若不保持連線，用戶端必須為每個請求建立新的連線。

要檢查keep-alive是否有效：

1. 啟動代理伺服器。
1. 請求頁面。

* 如果保持活動正常，則連接計數器不應超過5到10個連接。
* 如果「保持活動」不工作，則連接計數器會快速增加。

**查找丟失的請求**

如果您在複雜的伺服器設定中遺失請求（例如使用防火牆和分派程式），則可使用代理伺服器來找出遺失請求的位置。 在防火牆的情況下：

1. 在防火牆之前啟動代理
1. 在防火牆後啟動另一個代理
1. 使用這些來查看請求的進度。

**請求掛起**

如果您不時遇到掛斷請求：

1. 啟動proxy.jar。
1. 等待或將訪問日誌寫入檔案——每個條目都有時間戳記。
1. 當請求開始掛起時，您可以看到開啟了多少連線，以及哪個請求造成問題。

## 日誌消息的格式 {#the-format-of-log-messages}

proxy.jar產生的記錄項目都有下列格式：

```xml
[timestamp (optional)] [<b>C</b>lient|<b>S</b>erver]-[ConnectionNumber]-[BytePosition] ->[Character Stream]
```

例如，網頁請求的外觀如下：

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]
```

* C表示此項目來自用戶端（這是網頁的要求）
* 0是連接號（連接計數器從0開始）
* &#x200B;# 00000位元組串流中的偏移。 這是第一個條目，因此偏移為0。
* [GET &lt;?>] 是請求的內容，在範例中是其中一個HTTP標題(url)。

當連接關閉時，將記錄以下資訊：

```xml
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

這顯示第6個連接上以平均速度在客戶機和伺服器之間傳遞的位元組數。

## 日誌輸出示例 {#an-example-of-log-output}

我們將審查一個簡單的模板，該模板在要求時生成以下代碼：

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

如果AEM在localhost:4303上執行，請啟動Proxy伺服器，如下所示：

```xml
java -jar proxy.jar localhost 4303 4444 -logfile test.log
```

您可以在沒有代理服務`localhost:4303`器的情況下訪問伺服器()，但如果通過訪問該伺服器 `localhost:4444`，則代理伺服器將記錄通信。 開啟瀏覽器並存取使用上述範本建立的頁面。 之後，查看日誌檔案。

>[!NOTE]
>
>在proxy.jar 1.14版之前，一個連接的日誌項不會同步，這表示一個客戶機／伺服器連接的日誌項不需要按正確的順序。 代理伺服器的較新版本(>=1.14)不存在此問題。

啟動時，以下資訊將寫入日誌：

```xml
starting proxy for localhost:4303 on port 4444
using logfile: C:\CQUnify355default\opt\helpers\test.log
```

第一個連線(0)的開頭會列出下列標題欄位，要求主HTML頁面：

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

Proxy伺服器是確認Cookie是否已正確設定的好工具。 這裡，我們看到：

* AEM產生的cq3session Cookie
* 由CFC產生的顯示模式切換Cookie
* 名為JSESSIONID的Cookie;如果未使用&lt;%@ page session=&quot;false&quot; %>顯式關閉，則JSP會自動建立此選項：

```xml
C-0-#000393 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-0-#000514 -> [ ]
S-0-#000000 -> [HTTP/1.0 200 OK ]
```

伺服器將在請求後關閉連接0。 無法保持生命，因為請求有問號。 這表示伺服器無法傳回快取版本，因此無法判斷此時的內容長度，這是維持連線所需的長度。

```xml
S-0-#000017 -> [Connection: Close ]
S-0-#000036 -> [Server: Communique Servlet Engine/3.5.5 ]
S-0-#000077 -> [Content-Type: text/html;charset=iso-8859-1 ]
S-0-#000121 -> [Date: Tue, 14 Dec 2004 09:46:44 GMT ]
S-0-#000158 -> [Set-Cookie: JSESSIONID=4161a56b-f193-d8-88a5-e09c5ff7ef2a;Path=/author ]
S-0-#000232 -> [ ]
```

在這裡，伺服器開始在連接0上發送HTML代碼：

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

在HTML檔案提供後，連線0會立即關閉：

```xml
C-0-Finished: 516 bytes (0.0 kb/s)
S-0-Finished: 374 bytes (0.0 kb/s)
```

現在，輸出會從connection 1開始，此連線會下載HTML程式碼中包含的影像：

```xml
C-1-#000000 -> [GET /author/logo.gif HTTP/1.1 ]
C-1-#000031 -> [Accept: */* ]
C-1-#000044 -> [Referer: http://localhost:4444/author/prox.html?CFC_cK=1102936796533 ]
C-1-#000114 -> [Accept-Language: de-ch ]
C-1-#000138 -> [Accept-Encoding: gzip, deflate ]
C-1-#000170 -> [User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0) ]
C-1-#000234 -> [Host: localhost:4444 ]
```

同樣地，客戶端請求保持連接：

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

伺服器會傳回連線1上的影像內容長度：

```xml
S-1-#000107 -> [Content-Length: 124 ]
S-1-#000128 -> [Date: Tue, 14 Dec 2004 09:46:44 GMT ]
S-1-#000165 -> [ ]
```

現在已建立內容長度，伺服器會在連線1傳送影像資料：

```xml
S-1-#000167 -> [GIF87a..........................,.......
...I....0.A..8......YDA.W...1..`i.`..6...Z...$@.F..)`..f..A.....iu.........$..;]
```

到達keep-alive超時後，連接1也會關閉：

```xml
S-1-Finished: 291 bytes (0.0 kb/s)
C-1-Finished: 403 bytes (0.0 kb/s)
```

上述範例相對簡單，因為這兩個連線會依序進行：

* 首先，伺服器傳回HTML程式碼
* 然後瀏覽器會要求影像並開啟新的連線

實際上，頁面可能會產生許多對影像、樣式表、JavaScript檔案等的平行要求。 這表示日誌具有並行開放連接的重疊條目。 在這種情況下，我們建議使用選項-i來改善可讀性。
