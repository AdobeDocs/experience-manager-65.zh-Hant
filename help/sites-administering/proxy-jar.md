---
title: 代理伺服器工具(proxy.jar)
seo-title: Proxy Server Tool (proxy.jar)
description: 了解AEM中的Proxy伺服器工具。
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

代理伺服器充當在客戶機和伺服器之間中繼請求的中間伺服器。 代理伺服器跟蹤所有客戶端與伺服器的交互，並輸出整個TCP通信的日誌。 這可讓您不需存取主伺服器，即可精確監視目前的情況。

您可以在適當的安裝資料夾中找到代理伺服器：

* &lt;cq_install_path>/opt/helpers/proxy.jar
* &lt;crx_install_path>/opt/helpers/proxy.jar

您可以使用代理伺服器來監視所有客戶端與伺服器的交互，而不管基礎的通信協定如何。 例如，您可以監視下列通訊協定：

* 網頁的HTTP
* HTTPS用於安全網頁
* 電子郵件的SMTP
* 用於用戶管理的LDAP

例如，您可以在通過TCP/IP網路通信的任何兩個應用程式之間定位代理伺服器；例如網頁瀏覽器和AEM。 這可讓您監控要求AEM頁面時的確切情況。

## 啟動代理伺服器工具 {#starting-the-proxy-server-tool}

此工具可在AEM安裝程式的/opt/helpers資料夾中找到。 要啟動它，請鍵入：

```xml
java -jar proxy.jar <host> <remoteport> <localport> [options]
```

### 選項 {#options}

* **q（靜默模式）** 不會將請求寫入主控台視窗。 如果您不想減緩連線速度，或將輸出記錄到檔案（請參閱 — logfile選項），請使用此選項。
* **b（二進位模式）** 如果要在流量中查找特定的位元組組合，請啟用二進位模式。 輸出將包含十六進位和字元輸出。
* **t（時間戳記記錄項）** 將時間戳添加到每個日誌輸出。 時間戳記以秒為單位，因此可能不適合檢查單一請求。 如果您使用代理伺服器的時間較長，則可使用它查找在特定時間發生的事件。
* **記錄檔 &lt;filename> （寫入日誌檔案）** 將客戶端 — 伺服器對話寫入日誌檔案。 此參數也可在安靜模式下運作。
* **i &lt;numindentions> （添加縮進）** 每個作用中的連線都會縮排，以提高可讀性。 預設為16個層級。 （proxy.jar 1.16版中的新功能）。

## 使用代理伺服器工具 {#uses-of-the-proxy-server-tool}

下列案例說明了可以使用代理伺服器工具的一些用途：

**檢查Cookie及其值**

下列記錄項目範例顯示自代理啟動以來第6個連線上開啟之用戶端傳送的所有Cookie及其值：

```xml
C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]
```

**檢查標題及其值** 以下日誌條目示例說明伺服器能夠建立保持活動連接，並且內容長度標頭已正確設定：

```xml
S-7-#000017 -> [Connection: Keep-Alive ]
...
S-7-#000107 -> [Content-Length: 124 ]
```

**檢查「保留」是否有效**

**保存** 表示用戶端會重新使用與伺服器的連線來傳輸多個檔案（頁面程式碼、圖片、樣式表等）。 若不保持運作，用戶端必須為每個請求建立新連線。

檢查保持活動是否有效：

1. 啟動代理伺服器。
1. 要求頁面。

* 如果保持活動正常運作，連線計數器的連線數不應超過5到10個。
* 如果「保活」不起作用，則連接計數器會迅速增加。

**查找丟失的請求**

如果您在複雜的伺服器設定（例如防火牆和Dispatcher）中遺失請求，可以使用Proxy伺服器來找出請求遺失的位置。 如果是防火牆：

1. 在防火牆之前啟動代理
1. 在防火牆後啟動另一個代理
1. 使用這些項目可了解請求的深入程度。

**請求掛起**

如果您不時遇到掛起的請求：

1. 啟動proxy.jar。
1. 等待或將訪問日誌寫入檔案 — 每個條目都有時間戳。
1. 當請求開始掛起時，您可以查看已開啟的連接數，以及哪個請求導致了問題。

## 記錄訊息的格式 {#the-format-of-log-messages}

proxy.jar產生的記錄項目皆具有下列格式：

```xml
[timestamp (optional)] [<b>C</b>lient|<b>S</b>erver]-[ConnectionNumber]-[BytePosition] ->[Character Stream]
```

例如，網頁的請求可能如下所示：

```xml
C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]
```

* C表示此項目來自用戶端（這是網頁的要求）
* 0是連接號（連接計數器從0開始）
* # 00000位元組資料流中的偏移。 這是第一個條目，因此偏移為0。
* [GET &lt;?>] 是要求的內容，在其中一個HTTP標題(url)的範例中。

當連線關閉時，會記錄下列資訊：

```xml
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

這顯示在第6個連接上以平均速度在客戶端和伺服器之間傳遞的位元組數。

## 記錄輸出的範例 {#an-example-of-log-output}

我們將審核一個簡單模板，該模板在請求時生成以下代碼：

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

如果AEM在localhost:4303上運行，請按如下方式啟動代理伺服器：

```xml
java -jar proxy.jar localhost 4303 4444 -logfile test.log
```

您可以存取伺服器(`localhost:4303`)，但若您透過 `localhost:4444`，代理伺服器將記錄通訊。 開啟瀏覽器並存取使用上述範本建立的頁面。 之後，查看記錄檔。

>[!NOTE]
>
>在proxy.jar 1.14版之前，一個連接的日誌項不會同步，這意味著一個客戶端/伺服器連接的日誌項不必按正確的順序進行。 代理伺服器的較新版本(>=1.14)不存在此問題。

開始時，會將下列資訊寫入記錄檔：

```xml
starting proxy for localhost:4303 on port 4444
using logfile: C:\CQUnify355default\opt\helpers\test.log
```

第一個連接(0)的開頭列出了以下標題欄位，它請求主HTML頁：

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

代理伺服器是驗證Cookie是否已正確設定的好工具。 在此，我們看到：

* cq3session cookie由AEM產生
* 顯示模式切換CFC生成的cookie
* 名為JSESSIONID的cookie;如果未使用&lt;%@ page session=&quot;false&quot; %>顯式關閉，則JSP會自動建立此選項：

```xml
C-0-#000393 -> [Cookie: Show=ShowMode; cq3session=3bce15cf-1575-1b4e-8ea6-0d1a0c64738e; JSESSIONID=4161a56b-f193-d748-88a5-e09c5ff7ef2a ]
C-0-#000514 -> [ ]
S-0-#000000 -> [HTTP/1.0 200 OK ]
```

伺服器會在請求後關閉連線0。 無法保持生命，因為請求帶有問號。 這表示伺服器無法傳回快取版本，因此無法判斷此時的內容長度，這是保持連線所需的長度。

```xml
S-0-#000017 -> [Connection: Close ]
S-0-#000036 -> [Server: Communique Servlet Engine/3.5.5 ]
S-0-#000077 -> [Content-Type: text/html;charset=iso-8859-1 ]
S-0-#000121 -> [Date: Tue, 14 Dec 2004 09:46:44 GMT ]
S-0-#000158 -> [Set-Cookie: JSESSIONID=4161a56b-f193-d8-88a5-e09c5ff7ef2a;Path=/author ]
S-0-#000232 -> [ ]
```

在此，伺服器會開始在連線0上傳送HTML代碼：

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

提供HTML檔案後，連接0立即關閉：

```xml
C-0-Finished: 516 bytes (0.0 kb/s)
S-0-Finished: 374 bytes (0.0 kb/s)
```

現在，連線1的輸出會開始，而連線1會下載HTML程式碼中包含的影像：

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

對於連接1，伺服器可提供保持活動，因為影像是靜態的，因此是已知的內容長度。

```xml
S-1-#000017 -> [Connection: Keep-Alive ]
S-1-#000041 -> [Server: Communique Servlet Engine/3.5.5 ]
S-1-#000082 -> [Content-Type: image/gif ]
```

伺服器在連接1上返回影像的內容長度：

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

達到保持活動逾時後，連接1也會關閉：

```xml
S-1-Finished: 291 bytes (0.0 kb/s)
C-1-Finished: 403 bytes (0.0 kb/s)
```

上述範例相對簡單，因為兩個連線會依序發生：

* 首先，伺服器返回HTML代碼
* 接著瀏覽器會要求影像並開啟新連線

實際上，頁面可能會針對影像、樣式表、JavaScript檔案等產生許多平行請求。 這表示記錄檔具有重疊的並行開啟連線項目。 在此情況下，我們建議使用選項 — i來改善可讀性。
