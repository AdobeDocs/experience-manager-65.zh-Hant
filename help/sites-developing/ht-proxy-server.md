---
title: 如何使用代理伺服器工具
seo-title: How to use the Proxy Server Tool
description: 代理伺服器充當在客戶機和伺服器之間中繼請求的中間伺服器
seo-description: The proxy server acts as an intermediate server that relays requests between a client and a server
uuid: 30f4f46d-839e-4d23-a511-12f29b3cc8aa
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: dfbc1d2f-80c1-4564-a01c-a5028b7257d7
exl-id: 7222a0c3-cdb9-4c73-9d53-26f00792e439
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 0%

---

# 如何使用代理伺服器工具{#how-to-use-the-proxy-server-tool}

代理伺服器充當在客戶機和伺服器之間中繼請求的中間伺服器。 代理伺服器跟蹤所有客戶端與伺服器的交互，並輸出整個TCP通信的日誌。 這樣，您就可以準確監視正在進行的操作，而無需訪問主伺服器。

您可以在以下位置找到安裝中的代AEM理伺服器：

`crx-quickstart/opt/helpers/proxy-2.1.jar`

您可以使用代理伺服器來監視所有客戶端與伺服器的交互，而不管底層通信協定如何。 例如，可以監視以下協定：

* 網頁的HTTP
* 用於安全網頁的HTTPS
* 電子郵件的SMTP
* 用於用戶管理的LDAP

例如，可以在通過TCP/IP網路通信的任何兩個應用程式之間放置代理伺服器；例如Web瀏覽器和AEM。 這允許您準確監視請求CQ頁時發生的情況。

## 啟動代理伺服器工具 {#starting-the-proxy-server-tool}

在命令行上啟動伺服器：

`java -jar proxy-2.1.jar <host> <remoteport> <localport> [options]`

**參數**

`<host>`

這是要連接的CRX實例的主機地址。 如果實例在您的本地電腦上，則 `localhost`。

`<remoteport>`

這是目標CRX實例的主機埠。 例如，新安裝的安裝的默AEM認值為 **`4502`** 而新安裝的作者實AEM例的預設值是 `4502`。

`<localport>`

這是您本地電腦上要連接到的埠，通過代理訪問CRX實例。

**選項**

`-q` （安靜模式）

不將輸出寫入控制台窗口。 如果不想減慢連接速度，或者將輸出記錄到檔案（請參見 — logfile選項），則使用此選項。

`-b`（二進位模式）

如果要查找通信中的特定位元組組合，請啟用二進位模式。 輸出將包含十六進位和字元輸出。

`-t` （時間戳日誌條目）

為每個日誌輸出添加時間戳。 時間戳以秒為單位，因此可能不適合檢查單個請求。 如果在較長的時間段內使用代理伺服器，則使用它查找在特定時間發生的事件。

`-logfile <filename>`（寫入日誌檔案）

將客戶端 — 伺服器對話寫入日誌檔案。 此參數也在安靜模式下工作。

**`-i <numIndentions>`**（添加縮進）

每個活動連接都縮進，以便更好地讀取。 預設為16級。 此功能是 `proxy.jar version 1.16`。

### 日誌格式 {#log-format}

由proxy-2.1.jar生成的日誌條目都具有以下格式：

`[timestamp (optional)] [Client|Server]-[ConnectionNumber]-[BytePosition] ->[Character Stream]`

例如，對Web頁的請求可能如下所示：

`C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]`

* C表示此條目來自客戶端（它是對Web頁的請求）
* 0是連接號（連接計數器從0開始）
* #00000位元組流中的偏移。 這是第一個條目，因此偏移為0。
* `[GET <?>]` 是請求的內容，在示例中，HTTP標頭之一(url)。

連接關閉時，將記錄以下資訊：

```
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

這顯示在客戶端( `C`)和伺服器( `S`)，並以平均速度。

**日誌輸出示例**

例如，請考慮在請求時生成以下代碼的頁：

### 範例 {#example}

例如，請考慮位於儲存庫中的非常簡單的html文檔

`/content/test.html`

位於

`/content/test.jpg`

內容 `test.html` 為：

```xml
<html>
<head>
    <title>Test</title>
</head>
<body>
    Test<br>
    <img src="test.jpg">
</body>
</html>
```

假設實AEM例正在運行 `localhost:4502` 這樣啟動代理：

`java -jar proxy.jar localhost 4502 4444 -logfile test.log`

現在，可以通過以下位置的代理訪問CQ/CRX實例： `localhost:4444` 所有通過此埠的通信都記錄到 `test.log`。

如果現在觀看代理的輸出，我們將看到瀏覽器與實例之間的交AEM互。

啟動時，代理將輸出以下內容：

```xml
starting proxy for localhost:4502 on port 4444
using logfile: <some-dir>/crx-quickstart/opt/helpers/test.log
```

然後開啟瀏覽器並訪問test頁：

`http://localhost:4444/content/test.html`

我們看到瀏覽器 `GET` 頁面請求：

```shell
C-0-#000000 -> [GET /content/test.html HTTP/1.1 ]
C-0-#000033 -> [Host: localhost:4444 ]
C-0-#000055 -> [Connection: keep-alive ]
C-0-#000079 -> [User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_4) AppleWebKit/536.11 (KHTML, like Gecko) Chrome/20.0.1132.57 Safari/536.11 ]
C-0-#000212 -> [Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8 ]
C-0-#000285 -> [Accept-Encoding: gzip,deflate,sdch ]
C-0-#000321 -> [Accept-Language: en-US,en;q=0.8 ]
C-0-#000354 -> [Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.3 ]
C-0-#000402 -> [Cookie: login-token=179ba6bd-e0a7-4909-a965-e11c7f2bc2fc%3a618bd8a8-fbaf-43c5-827d-c84c62248c5e_22ee860cc9036fee%3acrx.default%3b21148fb0-eb6c]
C-0-#000543 -> [-43c9-a2b9-c8d40618d8ae%3ad87a3d1a-5e9a-4d5a-bab1-0ee60ad6d8df_d0e4ddce0fcd84b6%3acrx.default%3b5cb95227-ea51-47bf-850b-68ad1dfd7297%3af3bbb6]
C-0-#000684 -> [59-7913-4285-8857-832c087bafd5_c484727d3b3665ad%3acrx.default; ys-cq-siteadmin-tree=o%3Awidth%3Dn%253A240%5EselectedPath%3Ds%253A/content ]
C-0-#000824 -> [ ]
```

實AEM例用檔案內容作出響應 `test.html`:

```shell
S-0-#000000 -> [HTTP/1.1 200 OK ]
S-0-#000017 -> [Connection: Keep-Alive ]
S-0-#000041 -> [Server: Day-Servlet-Engine/4.1.24  ]
S-0-#000077 -> [Content-Type: text/html;charset=utf-8 ]
S-0-#000116 -> [Content-Length: 104 ]
S-0-#000137 -> [Date: Mon, 16 Jul 2012 11:23:38 GMT ]
S-0-#000174 -> [Last-Modified: Mon, 16 Jul 2012 11:19:27 GMT ]
S-0-#000220 -> [ ]
S-0-#000222 -> [<html>]
S-0-#000229 -> [<head>]
S-0-#000236 -> [    <title>Test</title>]
S-0-#000260 -> [</head> ]
S-0-#000269 -> [<body>]
S-0-#000276 -> [ Test<br>]
S-0-#000286 -> [    <img src="test.jpg">]
S-0-#000311 -> [</body>]
S-0-#000319 -> [</html>]
```

### 代理伺服器的使用 {#uses-of-the-proxy-server}

以下情形說明了可以使用代理伺服器的幾種用途：

**檢查Cookie及其值**

以下日誌條目示例顯示自代理啟動以來客戶端在開啟的第六個連接上發送的所有Cookie及其值：

`C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]`

**檢查標題及其值**

以下日誌條目示例說明伺服器能夠建立保持活動連接，並且內容長度標頭已正確設定：

```
S-7-#000017 -> [Connection: Keep-Alive ]
 ...
 S-7-#000107 -> [Content-Length: 124 ]
```

**檢查Keep-Alive是否工作**

Keep-alive是HTTP的一項功能，它允許客戶端重新使用與伺服器的TCP連接來發出多個請求（頁碼、圖片、樣式表等）。 如果沒有保持活動狀態，客戶端必須為每個請求建立新連接。

要檢查保持活動是否有效，請執行以下操作：

* 啟動代理伺服器。
* 請求頁面。
* 如果keep-alive正在工作，則連接計數器不應超過5到10個連接。
* 如果保持活動狀態不工作，則連接計數器會迅速增加。

**查找丟失的請求**

如果在複雜的伺服器設定中丟失請求，則可以使用代理伺服器查找請求丟失的位置。 在防火牆的情況下：

* 在防火牆之前啟動代理
* 在防火牆後啟動另一個代理
* 使用這些可查看請求的距離。

**掛起請求**

如果您不時遇到掛起請求：

* 啟動代理。
* 等待訪問日誌或將其寫入檔案，每個條目都具有時間戳。
* 當請求開始掛起時，您可以看到開啟了多少個連接，以及哪個請求導致了問題。
