---
title: WebDAV訪問
seo-title: WebDAV訪問
description: 了解AEM中的WebDAV存取。
seo-description: 了解AEM中的WebDAV存取。
uuid: b0ecaa5d-5454-42df-8453-404ece734c32
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 1eaf7afe-a181-45df-8766-bd564b1ad22a
exl-id: 891ee66c-e49c-4561-8fef-e6e448a8aa1c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 0%

---

# WebDAV訪問{#webdav-access}

要通過WebDAV與KDE連接到AEM，請執行以下操作：

AEM提供WebDAV支援，讓您顯示及編輯存放庫內容。 通過WebDAV連接，您可以通過案頭直接訪問內容儲存庫。 通過WebDAV連接添加到儲存庫的文本和PDF檔案會自動建立全文索引，並可使用標準搜索介面和標準Java API進行搜索。

## 一般 {#general}

[本文檔中包含的](/help/sites-administering/webdav-access.md#connecting-via-webdav) 每個作業系統的詳細說明，但是，基本上是使用WebDAV協定連接到儲存庫的說明，將WebDAV客戶端指向以下位置：

```xml
http://localhost:4502
```

![chlimage_1-111](assets/chlimage_1-111a.png)

此URL從作業系統級別連接時，提供對預設工作區(`crx.default`)的WebDAV訪問。 雖然對使用者而言較簡單，但這並未賦予他們指定工作區名稱的額外彈性，這可透過其他[WebDAV URL](/help/sites-administering/webdav-access.md#webdav-urls)來完成。

AEM會依下列方式顯示存放庫內容：

* 類型`nt:folder`的節點顯示為資料夾。 `nt:folder`節點下的節點將顯示為資料夾內容。

* 類型`nt:file`的節點顯示為檔案。 `nt:file`節點下的節點不顯示，但會形成檔案的內容。

使用WebDAV建立和編輯資料夾和檔案時，AEM將建立和編輯必要的`nt:folder`和`nt:file`節點。 如果您打算使用WebDAV來匯入和匯出內容，請嘗試盡可能使用`nt:file`和`nt:folder`節點類型。

>[!NOTE]
>
>在設定WebDAV之前，請檢查[技術要求](/help/sites-deploying/technical-requirements.md#webdav-clients)。

## WebDAV URL {#webdav-urls}

WebDAV伺服器的URL具有以下結構：

<table>
 <colgroup>
  <col width="100" />
  <col width="100" />
  <col width="100" />
  <col width="100" />
  <col width="100" />
 </colgroup>
 <tbody>
  <tr>
   <td>
    <code>
     <strong>URL Component</strong>
    </code></td>
   <td><code>https://&lt;host&gt;:&lt;port&gt;</code></td>
   <td><code>/&lt;crx-webapp-path&gt;</code></td>
   <td><code>/repository</code></td>
   <td><code>/&lt;workspace&gt;</code></td>
  </tr>
  <tr>
   <td>
    <code>
     <strong>Example</strong>
    </code></td>
   <td><code>http://localhost:4502</code></td>
   <td><code>/crx</code></td>
   <td><code>/repository</code></td>
   <td><code>/crx.default</code></td>
  </tr>
  <tr>
   <td><strong>說明</strong></td>
   <td>AEM運行的主機和埠</td>
   <td>AEM存放庫網頁應用程式的路徑</td>
   <td>WebDAV servlet映射到的路徑</td>
   <td>工作區名稱</td>
  </tr>
 </tbody>
</table>

通過更改路徑中的工作區元素，可以映射預設值以外的工作區(`crx.default`)。 例如，要映射名為`staging`的工作區，請使用以下URL:

```xml
http://localhost:4502/crx/repository/staging
```

## 通過WebDAV {#connecting-via-webdav}連接

[如上所述](/help/sites-administering/webdav-access.md#general)，若要使用WebDAV通訊協定連線至您的存放庫，請將WebDAV用戶端指向您的存放庫位置。但是，根據您的作業系統，連接客戶端所涉及的步驟不同，可能需要配置作業系統。

提供了如何連接以下作業系統的說明：

* [Windows](/help/sites-administering/webdav-access.md#windows)
* [macOS](/help/sites-administering/webdav-access.md#macos)
* [Linux](/help/sites-administering/webdav-access.md#linux)

### Windows {#windows}

要成功將Microsoft Windows 7（及更高版本）系統連接到未通過SSL保護的AEM實例，必須在Windows中顯式啟用通過不安全網路建立基本身份驗證的選項。 這需要在WebClient的Windows註冊表中進行更改。

更新登錄表後，AEM執行個體即可對應為磁碟。

#### Windows 7和更高配置{#windows-and-greater-configuration}

要更新註冊表以允許通過不安全的網路進行基本身份驗證，請執行以下操作：

1. 找到以下註冊表子項：

   ```xml
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters
   ```

1. 將`BasicAuthLevel`註冊表項子項設定為`2`或更高的值。

   如果不存在，請新增子金鑰。

1. 必須重新啟動系統，註冊表更改才能生效。

有關此註冊表更改的詳細資訊，請參閱[Microsoft支援KB 841215](https://support.microsoft.com/default.aspx/kb/841215)。

有關在Windows下提高WebDav客戶端響應性的資訊，請參閱[Microsoft支援KB 2445570](https://support.microsoft.com/kb/2445570)。

>[!NOTE]
>
>Adobe建議您建立一個與儲存庫用戶具有相同憑據的Windows用戶，否則可能會遇到權限衝突。

#### Windows 8配置{#windows-configuration}

對於Windows 8，您還需要按Windows 7和更大版本](/help/sites-administering/webdav-access.md#windows-and-greater-configuration)的說明更改註冊表項[。 但是，您必須先啟用案頭體驗，才能查看登錄項。

若要啟用案頭體驗，請開啟&#x200B;**伺服器管理器**，然後開啟&#x200B;**功能**，然後開啟&#x200B;**新增功能**，然後開啟&#x200B;**案頭體驗**。

重新啟動Windows 7及更高版本描述的註冊表項後，可用。 按照Windows 7及更高版本的說明修改它。

#### 在Windows {#connecting-in-windows}中連接

要在Windows環境中通過WebDAV連接到AEM:

1. 開啟&#x200B;**Windows資源管理器**&#x200B;或&#x200B;**檔案資源管理器**，然後按一下&#x200B;**電腦**&#x200B;或&#x200B;**此電腦**。

   ![chlimage_1-112](assets/chlimage_1-112a.png)

1. 按一下&#x200B;**映射網路驅動器**&#x200B;以啟動嚮導。
1. 輸入映射詳細資訊：

   * **驅動器**:選擇任何可用的信函
   * **資料夾**:  `http://localhost:4502`
   * 檢查&#x200B;**使用不同憑據連接**

   按一下「完成」

   ![chlimage_1-113](assets/chlimage_1-113a.png)

   >[!NOTE]
   >
   >如果AEM位於其他埠，請使用該埠號，而不是4502。 此外，如果您未在本地電腦上運行內容儲存庫，請用相應的伺服器名或IP地址替換`localhost`。

1. 輸入用戶名`admin`和密碼`admin`。 Adobe建議您使用預先設定的管理員帳戶進行測試。

   ![chlimage_1-114](assets/chlimage_1-114a.png)

1. 嚮導將關閉，並在Windows資源管理器或檔案資源管理器窗口中開啟新映射的驅動器。

   ![chlimage_1-114](assets/chlimage_1-115a.png)

Windows現在已經通過WebDAV將AEM映射為驅動器，您可以將其用作任何其他驅動器。

### macOS {#macos}

在macOS上通過WebDAV連接無需配置步驟。 您只需連接到WebDAV伺服器。

1. 導航到任何&#x200B;**Finder**&#x200B;窗口，然後按一下&#x200B;**Go**&#x200B;和&#x200B;**連接到伺服器**，或按&#x200B;**Command+k**。
1. 在&#x200B;**連接到伺服器**&#x200B;窗口中，輸入AEM位置：

   * `http://localhost:4502`
   >[!NOTE]
   >
   >如果AEM位於其他埠，請使用該埠號，而不是4502。 此外，如果您未在本地電腦上運行內容儲存庫，請用相應的伺服器名或IP地址替換`localhost`。

1. 提示您進行身份驗證時，請輸入用戶名`admin`和密碼`admin`。 Adobe建議您使用預先設定的管理員帳戶進行測試。

macOS現在已透過WebDAV連線至AEM，而您可以將其作為Mac上的任何其他資料夾使用。

### Linux {#linux}

在Linux上通過WebDAV進行連接不需要任何配置，但需要執行一些步驟來建立連接，這些步驟會根據您的案頭環境而有所不同。

#### 格諾梅 {#gnome}

要通過WebDAV與GNOME連接到AEM:

1. 在Nautilus（檔案瀏覽器）中，選擇&#x200B;**Places**&#x200B;並選擇&#x200B;**Connect to Server**。
1. 在&#x200B;**連接到伺服器**&#x200B;窗口中，選擇服務類型中的WebDAV(HTTP)。

1. 在&#x200B;**伺服器**&#x200B;中，輸入`http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >如果AEM位於其他埠，請使用該埠號，而不是4502。 此外，如果您未在本地電腦上運行內容儲存庫，請用相應的伺服器名或IP地址替換`localhost`。

1. 在&#x200B;**資料夾**&#x200B;中，輸入`/dav`
1. 輸入用戶名`admin`。 Adobe建議您使用預先設定的管理員帳戶進行測試。
1. 將埠留空，然後為連接輸入任何名稱。
1. 按一下&#x200B;**Connect**。 AEM會提示您輸入密碼。
1. 輸入密碼`admin`，然後按一下&#x200B;**Connect**。

GNOME現在已將AEM裝入為卷，您可以像其他卷一樣使用它。

#### KDE {#kde}

1. 開啟「網路資料夾」嚮導。
1. 選擇&#x200B;**WebFolder**(webdav)，然後按一下「下一步」。
1. 在&#x200B;**Name**&#x200B;中，鍵入連接名稱。
1. 在&#x200B;**User**&#x200B;中，輸入`admin.`Adobe，建議您使用預先設定的管理員帳戶。
1. 在&#x200B;**伺服器**&#x200B;中，輸入`http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >如果AEM位於其他埠，請使用該埠號，而不是4502。 此外，如果您未在本地電腦上運行內容儲存庫，請用相應的伺服器名稱或IP地址替換`localhost`

1. 在&#x200B;**資料夾**&#x200B;中，輸入`dav`

1. 按一下&#x200B;**儲存並連線**。
1. 提示輸入密碼時，輸入密碼`admin`，然後按一下&#x200B;**Connect**。

KDE現在已將AEM裝入為卷，您可以像使用任何其他卷一樣使用它。
