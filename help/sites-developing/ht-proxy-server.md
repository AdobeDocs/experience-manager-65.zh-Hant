---
title: 如何使用Proxy伺服器工具
seo-title: 如何使用Proxy伺服器工具
description: 代理伺服器充當在客戶機和伺服器之間中繼請求的中間伺服器
seo-description: 代理伺服器充當在客戶機和伺服器之間中繼請求的中間伺服器
uuid: 30f4f46d-839e-4d23-a511-12f29b3cc8aa
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: dfbc1d2f-80c1-4564-a01c-a5028b7257d7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 如何使用Proxy伺服器工具{#how-to-use-the-proxy-server-tool}

代理伺服器充當在客戶機和伺服器之間中繼請求的中間伺服器。 代理伺服器跟蹤所有客戶機與伺服器的交互，並輸出整個TCP通信的日誌。 這樣，您就可以完全監視當前的情況，而無需訪問主伺服器。

您可在以下網址找到AEM安裝中的Proxy伺服器：

`crx-quickstart/opt/helpers/proxy-2.1.jar`

您可以使用代理伺服器來監視所有客戶端與伺服器的交互，而不管底層的通信協定如何。 例如，您可以監控下列通訊協定：

* 網頁的HTTP
* HTTPS用於安全網頁
* 電子郵件的SMTP
* 用於用戶管理的LDAP

例如，您可以將代理伺服器放在通過TCP/IP網路通信的任意兩個應用程式之間；例如網頁瀏覽器和AEM。 這可讓您監控您請求CQ頁面時的實際情況。

## 啟動代理伺服器工具 {#starting-the-proxy-server-tool}

在命令行上啟動伺服器：

`java -jar proxy-2.1.jar <host> <remoteport> <localport> [options]`

**參數**

`<host>`

這是您要連接到的CRX實例的主機地址。 如果實例位於您的本地電腦上，則此為 `localhost`。

`<remoteport>`

這是目標CRX實例的主機埠。 例如，新安裝的AEM安裝的預設值為， **`4502`** 而新安裝的AEM作者例項的預設值為 `4502`。

`<localport>`

這是您本地電腦上要連接到的埠，以便通過代理訪問CRX實例。

**選項**

`-q` （安靜模式）

不將輸出寫入控制台窗口。 如果您不想減慢連接速度，或者將輸出記錄到檔案（請參見-logfile選項），請使用此選項。

`-b`（二進位模式）

如果您要尋找流量中的特定位元組組合，請啟用二進位模式。 然後，輸出將包含十六進位和字元輸出。

`-t` （時間戳記記錄項目）

為每個日誌輸出添加時間戳。 時間戳記以秒為單位，因此可能不適合檢查單一請求。 如果您在較長的時段內使用代理伺服器，則可使用它來查找在特定時間發生的事件。

`-logfile <filename>`（寫入日誌檔案）

將客戶機——伺服器對話寫入日誌檔案。 此參數也可在安靜模式下運作。

**`-i <numIndentions>`**（新增縮進）

每個作用中的連線都會縮排，以提高可讀性。 預設為16層。 此功能是隨附的 `proxy.jar version 1.16`。

### 日誌格式 {#log-format}

proxy-2.1.jar產生的記錄項目都有下列格式：

`[timestamp (optional)] [Client|Server]-[ConnectionNumber]-[BytePosition] ->[Character Stream]`

例如，網頁請求的外觀如下：

`C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]`

* C表示此項目來自用戶端（這是網頁的要求）
* 0是連接號（連接計數器從0開始）
* # 00000位元組串流中的偏移。 這是第一個條目，因此偏移為0。
* `[GET <?>]` 是請求的內容，在其中一個HTTP標題(url)範例中。

當連接關閉時，將記錄以下資訊：

```
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

這顯示第6個連接上以平均速度在客戶端( `C`)和伺服器( `S`)之間傳遞的位元組數。

**日誌輸出示例**

例如，請考慮在要求時產生下列程式碼的頁面：

### 例如 {#example}

例如，假設儲存庫中有一個非常簡單的html檔案，位於

`/content/test.html`

與位於

`/content/test.jpg`

其內容 `test.html` 為：

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

假設AEM例項正在執行， `localhost:4502` 我們會像這樣啟動Proxy:

`java -jar proxy.jar localhost 4502 4444 -logfile test.log`

CQ/CRX實例現在可以通過proxy `localhost:4444` at訪問，通過此埠的所有通信都記錄到 `test.log`。

如果我們現在檢視proxy的輸出，我們將會看到瀏覽器與AEM例項之間的互動。

在啟動時，Proxy會輸出下列內容：

```xml
starting proxy for localhost:4502 on port 4444
using logfile: <some-dir>/crx-quickstart/opt/helpers/test.log
```

接著，我們開啟瀏覽器並存取測試頁面：

`http://localhost:4444/content/test.html`

我們看到瀏覽器對頁 `GET` 面提出請求：

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

AEM例項會以檔案內容回應 `test.html`:

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

以下情況說明了可以使用代理伺服器的一些用途：

**檢查Cookie及其值**

以下日誌條目示例顯示自代理啟動以來客戶端在第六個連接上開啟的所有Cookie及其值：

`C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]`

**檢查標題及其值**

以下日誌條目示例說明伺服器能夠建立保持活動連接，並且內容長度標題已正確設定：

```
S-7-#000017 -> [Connection: Keep-Alive ]
 ...
 S-7-#000107 -> [Content-Length: 124 ]
```

**檢查Keep-Alive是否有效**

Keep-alive是HTTP的一項功能，可讓用戶端重新使用與伺服器的TCP連線，以發出多個要求（針對頁面程式碼、圖片、樣式表等）。 若不保持連線，用戶端必須為每個請求建立新的連線。

要檢查keep-alive是否有效：

* 啟動代理伺服器。
* 請求頁面。
* 如果保持活動正常，則連接計數器不應超過5到10個連接。
* 如果「保持活動」不工作，則連接計數器會快速增加。

**查找丟失的請求**

如果您在複雜的伺服器設定中遺失請求（例如使用防火牆和分派程式），則可使用代理伺服器來找出遺失請求的位置。 在防火牆的情況下：

* 在防火牆之前啟動代理
* 在防火牆後啟動另一個代理
* 使用這些來查看請求的進度。

**請求掛起**

如果您不時遇到掛斷請求：

* 啟動代理。
* 等待或將訪問日誌寫入每個條目具有時間戳的檔案。
* 當請求開始掛起時，您可以看到開啟了多少連線，以及哪個請求造成問題。

