---
title: 預設情況下為SSL/TLS
seo-title: SSL/TLS By Default
description: 瞭解如何在中預設使用SSLAEM。
seo-description: Learn how to use SSL by Default in AEM.
uuid: 2fbfd020-1d33-4b22-b963-c698e62f5bf6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
discoiquuid: 68077369-0549-4c0f-901b-952e323013ea
docset: aem65
exl-id: 574e2fc2-6ebf-49b6-9b65-928237a8a34d
source-git-commit: 9273282b26aeab5f65f0f05aa8ad754962dc59ec
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---

# 預設情況下為SSL/TLS{#ssl-tls-by-default}

為了不斷提高安全性，Adobe已AEM經引入了一種預設情況下稱為SSL的功能。 目的是鼓勵使用HTTPS連接到實AEM例。

## 預設情況下啟用SSL/TLS {#enabling-ssl-tls-by-default}

預設情況下，您可以通過按一下主螢幕中的相關收件箱消息開始配置SSL/AEMTLS。 要訪問收件箱，請按螢幕右上角的鈴表徵圖。 然後，按一下 **全部查看**。 這將顯示清單視圖中排序的所有警報的清單。

在清單中，選擇並開啟 **配置HTTPS** 警報：

![chlimage_1-103](assets/chlimage_1-103.png)

>[!NOTE]
>
>如果 **配置HTTPS** 「收件箱」中不存在警報，您可以通過轉到「HTTPS嚮導」直接導航到 *<http://serveraddress:serverport/libs/granite/security/content/sslConfig.html?item=configuration%2fconfiguressl&_charset_=utf-8>*

名為的服務用戶 **ssl服務** 已為此功能建立。 開啟警報後，將引導您執行以下配置嚮導：

1. 首先，設定「儲存憑據」。 這些是 **ssl服務** 將包含HTTPS偵聽器的私鑰和信任儲存的系統用戶密鑰儲存。

   ![chlimage_1-104](assets/chlimage_1-104.png)

1. 輸入憑據後，按一下 **下一個** 的子菜單。 然後，上載SSL/TLS連接的相關私鑰和證書。

   ![chlimage_1-105](assets/chlimage_1-105.png)

   >[!NOTE]
   >
   >有關如何生成私鑰和證書以便與嚮導一起使用的資訊，請參見 [本程式](/help/sites-administering/ssl-by-default.md#generating-a-private-key-certificate-pair-to-use-with-the-wizard) 下。

1. 最後，為HTTPS偵聽器指定HTTPS主機名和TCP埠。

   ![screen_shot_2018-07-25at31658pm](assets/screen_shot_2018-07-25at31658pm.png)

## 預設情況下自動執行SSL/TLS {#automating-ssl-tls-by-default}

預設情況下，有三種自動執行SSL/TLS的方法。

### 通過HTTPPOST {#via-http-post}

第一種方法涉及過帳到配置嚮導正在使用的SSLSetup伺服器：

```shell
POST /libs/granite/security/post/sslSetup.html
```

您可以在POST中使用以下負載來自動配置：

```xml
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="keystorePassword"

test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="keystorePasswordConfirm"
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="truststorePassword"
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="truststorePasswordConfirm"
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="privatekeyFile"; filename="server.der"
Content-Type: application/x-x509-ca-cert

------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="certificateFile"; filename="server.crt"
Content-Type: application/x-x509-ca-cert

------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="httpsPort"
8443
```

Servlet與任何slingPOSTServlet一樣，將響應200 OK（正常）或錯誤HTTP狀態代碼。 您可以在響應的HTML正文中查找有關狀態的詳細資訊。

下面是成功響應和錯誤的示例。

**成功示例** （狀態= 200）:

```xml
<!DOCTYPE html>
<html lang='en'>
<head>
<title>OK</title>
</head>
<body>
<h1>OK</h1>
<dl>
<dt class='foundation-form-response-status-code'>Status</dt>
<dd>200</dd>
<dt class='foundation-form-response-status-message'>Message</dt>
<dd>SSL successfully configured</dd>
<dt class='foundation-form-response-title'>Title</dt>
<dd>OK</dd>
<dt class='foundation-form-response-description'>Description</dt>
<dd>HTTPS has been configured on port 8443. The private key and
certificate were stored in the key store of the user ssl-service.
Please take note of the key store password you provided. You will need
it for any subsequent updating of the private key or certificate.</dd>
</dl>
<h2>Links</h2>
<ul class='foundation-form-response-links'>
<li><a class='foundation-form-response-redirect' href='/'>Done</a></li>
</ul>
</body>
</html>
```

**錯誤示例** （狀態= 500）:

```xml
<!DOCTYPE html>
<html lang='en'>
<head>
<title>Error</title>
</head>
<body>
<h1>Error</h1>
<dl>
<dt class='foundation-form-response-status-code'>Status</dt>
<dd>500</dd>
<dt class='foundation-form-response-status-message'>Message</dt>
<dd>The provided file is not a valid key, DER format expected</dd>
<dt class='foundation-form-response-title'>Title</dt>
<dd>Error</dd>
</dl>
</body>
</html>
```

### 通過包 {#via-package}

或者，可以通過上載已包含以下必需項的包來自動執行SSL/TLS設定：

* ssl服務用戶的密鑰庫。 位於 */home/users/system/security/ssl/service/keystore* 的下界。
* 的 `GraniteSslConnectorFactory` 配置

### 生成要與嚮導一起使用的私鑰/證書對 {#generating-a-private-key-certificate-pair-to-use-with-the-wizard}

在下面，您將找到一個示例，用於建立SSL/TLS嚮導可以使用的DER格式的自簽名證書。 根據作業系統安裝OpenSSL，開啟OpenSSL命令提示符，並將目錄更改為要生成私鑰/證書的資料夾。

>[!NOTE]
>
>例如，使用自簽名證書只是出於目的，不應在生產中使用。

1. 首先，建立私鑰：

   ```shell
   openssl genrsa -aes256 -out localhostprivate.key 4096
   openssl rsa -in localhostprivate.key -out localhostprivate.key
   ```

1. 然後，使用私鑰生成證書籤名請求(CSR):

   ```shell
   openssl req -sha256 -new -key localhostprivate.key -out localhost.csr -subj "/CN=localhost"
   ```

1. 生成SSL/TLS證書並使用私鑰對其進行簽名。 在本示例中，將從現在起過期一年：

   ```shell
   openssl x509 -req -days 365 -in localhost.csr -signkey localhostprivate.key -out localhost.crt
   ```

將私鑰轉換為DER格式。 這是因為SSL嚮導要求密鑰採用DER格式：

```shell
openssl pkcs8 -topk8 -inform PEM -outform DER -in localhostprivate.key -out localhostprivate.der -nocrypt
```

最後，上載 **localhostprivate.der** 和 **localhost.crt** 作為本頁開頭所述的圖形SSL/TLS嚮導步驟2中的SSL/TLS證書。

### 通過cURL更新SSL/TLS配置 {#updating-the-ssl-tls-configuration-via-curl}

>[!NOTE]
>
>請參閱 [將cURL與](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/curl.html) 中集中列出的有用cURL命令AEM。

您還可以使用cURL工具自動執行SSL/TLS配置。 可以通過將配置參數發佈到此URL來執行此操作：

*https://&lt;serveraddress>:&lt;serverport>/libs/granite/security/post/sslSetup.html*

以下是可用於更改配置嚮導中各種設定的參數：

* `-F "keystorePassword=password"`  — 密鑰庫密碼；

* `-F "keystorePasswordConfirm=password"`  — 確認密鑰庫密碼；

* `-F "truststorePassword=password"`  — 信任儲存密碼；

* `-F "truststorePasswordConfirm=password"`  — 確認信任商店密碼；

* `-F "privatekeyFile=@localhostprivate.der"`  — 指定私鑰；

* `-F "certificateFile=@localhost.crt"`  — 指定證書；

* `-F "httpsHostname=host.example.com"` — 指定主機名；
* `-F "httpsPort=8443"` - HTTPS偵聽器將使用的埠。

>[!NOTE]
>
>運行cURL以自動執行SSL/TLS配置的最快方式來自DER和CRT檔案所在的資料夾。 或者，可以在 `privatekeyFile` 和certificateFile參數。
>
>您還需要經過身份驗證才能執行更新，因此請確保在 `-u user:passeword` 的下界。
>
>正確的cURL帖子命令應如下所示：

```shell
curl -u user:password -F "keystorePassword=password" -F "keystorePasswordConfirm=password" -F "truststorePassword=password" -F "truststorePasswordConfirm=password" -F "privatekeyFile=@localhostprivate.der" -F "certificateFile=@localhost.crt" -F "httpsHostname=host.example.com" -F "httpsPort=8443" https://host:port/libs/granite/security/post/sslSetup.html
```

#### 使用cURL的多個證書 {#multiple-certificates-using-curl}

通過重複certificateFile參數，可以向servlet發送一串證書，如下所示：

`-F "certificateFile=@root.crt" -F "certificateFile=@localhost.crt"..`

執行該命令後，請驗證所有證書是否都已將其保存到密鑰庫。 從以下位置檢查密鑰庫：
[http://localhost:4502/libs/granite/security/content/userEditor.html/home/users/system/security/ssl-service](http://localhost:4502/libs/granite/security/content/userEditor.html/home/users/system/security/ssl-service)

### 啟用TLS 1.3連接 {#enabling-tls-connection}

1. 轉到Web控制台
1. 然後，導航到 **OSGi** - **配置** - **Adobe花崗岩SSL連接器工廠**
1. 轉到 **包括的密碼套件** 欄位，然後添加以下條目。 通過按「 」，可確認每個添加項&#x200B;**+**「 」按鈕，添加後：

   * `TLS_AES_256_GCM_SHA384`
   * `TLS_AES_128_GCM_SHA256`
   * `TLS_CHACHA20_POLY1305_SHA256`
   * `TLS_AES_128_CCM_SHA256`
   * `TLS_AES_128_CCM_8_SHA256`