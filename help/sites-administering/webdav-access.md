---
title: WebDAV訪問
seo-title: WebDAV Access
description: 瞭解中的WebDAV訪AEM問。
seo-description: Learn about WebDAV access in AEM.
uuid: b0ecaa5d-5454-42df-8453-404ece734c32
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
discoiquuid: 1eaf7afe-a181-45df-8766-bd564b1ad22a
exl-id: 891ee66c-e49c-4561-8fef-e6e448a8aa1c
source-git-commit: e05f6cd7cf17f4420176cf76f28cb469bcee4a0a
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 1%

---

# WebDAV訪問{#webdav-access}

要通過WebDAVAEM與KDE連接：

提AEM供WebDAV支援，允許您顯示和編輯儲存庫內容。 通過WebDAV連接，您可以直接通過案頭訪問內容儲存庫。 通過WebDAV連接添加到儲存庫的文本和PDF檔案將自動建立全文索引，並可通過標準搜索介面和標準Java™ API進行搜索。

## 一般 {#general}

[每個作業系統的詳細說明](/help/sites-administering/webdav-access.md#connecting-via-webdav) 包含在本文檔中，但實際上是使用WebDAV協定連接到儲存庫，您將WebDAV客戶端指向以下位置：

```xml
http://localhost:4502
```

![chlimage_1-111](assets/chlimage_1-111a.png)

當從作業系統級別連接時，此URL提供對預設工作區( `crx.default`)。 雖然對於用戶來說更簡單，但它不賦予他們指定工作區名稱的額外靈活性，這可以通過使用其他 [WebDAV URL](/help/sites-administering/webdav-access.md#webdav-urls)。

按如AEM下方式顯示儲存庫內容：

* 類型的節點 `nt:folder` 顯示為資料夾。 位於 `nt:folder` 資料夾內容。

* 類型的節點 `nt:file` 的子菜單。 位於 `nt:file` 不顯示節點，但會形成檔案的內容。

使用WebDAV建立和編輯資料夾和檔案時，AEM建立和編輯必需的 `nt:folder` 和 `nt:file` 節點。 如果計畫使用WebDAV導入和導出內容，請嘗試使用 `nt:file` 和 `nt:folder` 節點類型。

>[!NOTE]
>
>在設定WebDAV之前，請檢查 [技術要求](/help/sites-deploying/technical-requirements.md#webdav-clients)。

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
   <td>運行的主機和端AEM口</td>
   <td>儲存庫WebAEM應用的路徑</td>
   <td>WebDAV Servlet映射到的路徑</td>
   <td>工作區的名稱</td>
  </tr>
 </tbody>
</table>

通過更改路徑中的工作區元素，可以映射除預設值( `crx.default`)。 例如，映射名為 `staging`，使用以下URL:

```xml
http://localhost:4502/crx/repository/staging
```

## 通過WebDAV連接 {#connecting-via-webdav}

[如上所述](/help/sites-administering/webdav-access.md#general)，要使用WebDAV協定連接到儲存庫，請將WebDAV客戶端指向儲存庫位置。 但是，根據您的作業系統，連接客戶端所涉及的步驟不同，可能需要配置作業系統。

提供了有關如何連接以下作業系統的說明：

* [Windows](/help/sites-administering/webdav-access.md#windows)
* [macOS](/help/sites-administering/webdav-access.md#macos)
* [Linux](/help/sites-administering/webdav-access.md#linux)

### Windows {#windows}

要成功將Microsoft® Windows 7（及更高版本）系統連接到AEM未使用SSL保護的實例，必須在Windows中明確啟用通過不安全網路建立基本身份驗證的選項。 此功能要求更改WebClient的Windows註冊表。

一旦更新了註冊表，AEM則實例可以映射為驅動器。

#### Windows 7和更高版本的配置 {#windows-and-greater-configuration}

要更新註冊表以允許通過不安全的網路進行基本身份驗證，請：

1. 找到以下註冊表子項：

   ```xml
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters
   ```

1. 設定 `BasicAuthLevel` 註冊表項子項到的值 `2` 或更大。

   如果不存在，請添加子項。

1. 重新啟動系統，使註冊表更改生效。

>[!NOTE]
>
>Adobe建議您建立一個與儲存庫用戶具有相同憑據的Windows用戶，否則可能會遇到權限衝突。

#### Windows 8配置 {#windows-configuration}

對於Windows 8，更改註冊表項 [如Windows 7及更高版本中所述](/help/sites-administering/webdav-access.md#windows-and-greater-configuration)。 但是，在執行此任務之前，必須啟用「案頭體驗」才能查看註冊表項。

要啟用案頭體驗，請開啟 **伺服器管理器**，則 **功能**，則 **添加功能**，則 **台式機體驗**。

重新啟動後，Windows 7及更高版本的註冊表條目可用。 按照Windows 7及更高版本的說明修改它。

#### 在Windows中連接 {#connecting-in-windows}

要在WindowsAEM環境中通過WebDAV連接：

1. 開啟 **Windows資源管理器** 或 **檔案資源管理器** 按一下 **電腦** 或 **這台電腦**。

   ![chlimage_1-112](assets/chlimage_1-112a.png)

1. 要啟動嚮導，請按一下 **映射網路驅動器**。
1. 輸入映射詳細資訊：

   * **驅動器**:選擇任何可用信函
   * **資料夾**: `http://localhost:4502`
   * 檢查 **使用不同憑據連接**

   按一下「完成」

   ![chlimage_1-113](assets/chlimage_1-113a.png)

   >[!NOTE]
   >
   >如AEM果位於另一個埠上，請使用該埠號，而不是4502。 此外，如果您沒有在本地電腦上運行內容儲存庫，請替換 `localhost` 伺服器名或IP地址。

1. 輸入用戶名 `admin` 和密碼 `admin`。 Adobe建議您使用預配置的管理員帳戶進行測試。

   ![chlimage_1-114](assets/chlimage_1-114a.png)

1. 嚮導將關閉，並在Windows資源管理器或檔案資源管理器窗口中開啟新映射的驅動器。

   ![chlimage_1-115](assets/chlimage_1-115a.png)

Windows現在已通AEM過WebDAV映射為驅動器，您可以將其用作任何其他驅動器。

### macOS {#macos}

通過macOS的WebDAV連接不需要配置步驟。 可以連接到WebDAV伺服器。

1. 導航至任意 **查找器** 的 **開始** 和 **連接到伺服器**&#x200B;或 **命令+k**。
1. 在 **連接到伺服器** 輸入位AEM置：

   * `http://localhost:4502`
   >[!NOTE]
   >
   >如AEM果位於另一個埠上，請使用該埠號，而不是4502。 此外，如果您沒有在本地電腦上運行內容儲存庫，請替換 `localhost` 伺服器名或IP地址。

1. 當系統提示您進行身份驗證時，輸入用戶名 `admin` 和密碼 `admin`。 Adobe建議您使用預配置的管理員帳戶進行測試。

macOS現在已通AEM過WebDAV連接，您可以將其用作Mac上的任何其他資料夾。

### Linux® {#linux}

在Linux®上通過WebDAV進行連接不需要任何配置，但需要執行一些步驟來建立連接，這些步驟因您的案頭環境而異。

#### 尼奧梅 {#gnome}

要通過WebDAVAEM與GNOME連接：

1. 在Nautilus（檔案資源管理器）中，選擇 **位置** 選擇 **連接到伺服器**。
1. 在 **連接到伺服器** 窗口，在服務類型中選擇WebDAV(HTTP)。

1. 在 **伺服器**&#x200B;輸入 `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >如AEM果位於另一個埠上，請使用該埠號，而不是4502。 此外，如果您沒有在本地電腦上運行內容儲存庫，請替換 `localhost` 伺服器名或IP地址。

1. 在 **資料夾**&#x200B;輸入 `/dav`
1. 輸入用戶名 `admin`。 Adobe建議您使用預配置的管理員帳戶進行測試。
1. 將埠留空，並輸入連接的任何名稱。
1. 按一下 **連接**。 提示AEM您輸入密碼。
1. 輸入密碼 `admin` 按一下 **連接**。

GNOME現在已作AEM為卷裝載，您可以像其他卷一樣使用它。

#### 克德 {#kde}

1. 開啟「網路資料夾」嚮導。
1. 選擇 **Web資料夾**(webdav)，然後按一下「Next（下一步）」。
1. 在 **名稱**&#x200B;鍵入連接名稱。
1. 在 **用戶**&#x200B;輸入 `admin.` Adobe建議您使用預配置的管理員帳戶。
1. 在 **伺服器**&#x200B;輸入 `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >如AEM果位於另一個埠上，請使用該埠號，而不是4502。 此外，如果您沒有在本地電腦上運行內容儲存庫，請替換 `localhost` 具有相應的伺服器名或IP地址

1. 在 **資料夾**&#x200B;輸入 `dav`

1. 按一下 **保存並連接**。
1. 提示輸入密碼時，輸入密碼 `admin` 按一下 **連接**。

KDE現在已作AEM為卷裝載，您可以像其他卷一樣使用它。
