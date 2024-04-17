---
title: WebDAV存取
description: 瞭解如何使用WebDAV存取Adobe Experience Manager。
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
exl-id: 891ee66c-e49c-4561-8fef-e6e448a8aa1c
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 1%

---

# WebDAV存取{#webdav-access}

透過WebDAV與KDE連線AEM：

AEM提供WebDAV支援，可讓您顯示和編輯存放庫內容。 透過WebDAV連線可讓您透過案頭直接存取內容存放庫。 透過WebDAV連線新增到存放庫中的文字和PDF檔案會自動建立全文檢索索引，並可透過標準搜尋介面及標準Java™ API進行搜尋。

## 一般 {#general}

[每個作業系統的詳細指示](/help/sites-administering/webdav-access.md#connecting-via-webdav) 本檔案已包含，但基本上為使用WebDAV通訊協定連線到您的存放庫，您可以將WebDAV使用者端指向下列位置：

```xml
http://localhost:4502
```

![chlimage_1-111](assets/chlimage_1-111a.png)

此URL從作業系統層級連線時，可提供WebDAV存取預設工作區( `crx.default`)。 雖然對使用者來說比較簡單，但是這並不會提供他們指定工作區名稱的額外靈活性，而指定工作區名稱可使用額外的 [WebDAV URL](/help/sites-administering/webdav-access.md#webdav-urls).

AEM會依照以下方式顯示存放庫內容：

* 型別的節點 `nt:folder` 會顯示為資料夾。 以下的節點 `nt:folder` 節點會顯示為資料夾內容。

* 型別的節點 `nt:file` 會顯示為檔案。 以下的節點 `nt:file` 節點不會顯示，但會構成檔案的內容。

當您使用WebDAV建立及編輯資料夾和檔案時，AEM會建立並編輯必要的 `nt:folder` 和 `nt:file` 節點。 如果您打算使用WebDAV來匯入和匯出內容，請嘗試使用 `nt:file` 和 `nt:folder` 節點型別越多越好。

>[!NOTE]
>
>設定WebDAV之前，請檢查 [技術需求](/help/sites-deploying/technical-requirements.md#webdav-clients).

## WebDAV URL {#webdav-urls}

WebDAV伺服器的URL結構如下：

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
   <td>AEM執行所在的主機和連線埠</td>
   <td>AEM存放庫Webapp的路徑</td>
   <td>WebDAV servlet對應到的路徑</td>
   <td>工作區的名稱</td>
  </tr>
 </tbody>
</table>

透過變更路徑中的工作區元素，您可以對應預設工作區以外的工作區( `crx.default`)。 例如，若要對映名為的工作區 `staging`，使用下列URL：

```xml
http://localhost:4502/crx/repository/staging
```

## 透過WebDAV連線 {#connecting-via-webdav}

[如上所述](/help/sites-administering/webdav-access.md#general)，若要使用WebDAV通訊協定連線到您的存放庫，請將WebDAV使用者端指向您的存放庫位置。 不過，視您的作業系統而定，連線使用者端的步驟會有所不同，因此可能需要設定作業系統。

提供如何連線下列作業系統的說明：

* [Windows](/help/sites-administering/webdav-access.md#windows)
* [macOS](/help/sites-administering/webdav-access.md#macos)
* [Linux](/help/sites-administering/webdav-access.md#linux)

### Windows {#windows}

若要成功將Microsoft® Windows 7 （及更新版本）系統連線至不使用SSL保護的AEM執行個體，必須在Windows中明確啟用透過不安全的網路建立基本驗證的選項。 這項功能需要在WebClient的Windows登入中進行變更。

更新登入之後，AEM執行個體就可以對應為磁碟機。

#### Windows 7和更新組態 {#windows-and-greater-configuration}

若要更新登入以允許透過不安全的網路進行基本驗證：

1. 找到下列登入子機碼：

   ```xml
   HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters
   ```

1. 設定 `BasicAuthLevel` 登入專案子機碼至值 `2` 或更高。

   如果不存在，請新增子索引鍵。

1. 重新啟動系統，讓登入變更生效。

>[!NOTE]
>
>Adobe建議您使用與存放庫使用者相同的認證來建立Windows使用者，否則可能會發生許可權衝突。

#### Windows 8設定 {#windows-configuration}

若是Windows 8，請變更登入專案 [如Windows 7及更新版本所述](/help/sites-administering/webdav-access.md#windows-and-greater-configuration). 但是，在執行此工作之前，必須啟用[案頭體驗]才能看到登入專案。

若要啟用案頭體驗，請開啟 **伺服器管理員**，然後 **功能**，然後 **新增功能**，然後 **案頭體驗**.

重新開機後，即可使用Windows 7及更新版本的登入專案。 請依照Windows 7和更新版本的說明修改它。

#### 在Windows中連線 {#connecting-in-windows}

若要在Windows環境中透過WebDAV連線至AEM：

1. 開啟 **Windows檔案總管** 或 **檔案總管** 並按一下 **電腦** 或 **這台電腦**.

   ![chlimage_1-112](assets/chlimage_1-112a.png)

1. 若要啟動精靈，請按一下 **對應網路磁碟機**.
1. 輸入對應明細：

   * **推動**：選擇任何可用的字母
   * **資料夾**： `http://localhost:4502`
   * 檢查 **使用不同的認證連線**

   按一下完成

   ![chlimage_1-113](assets/chlimage_1-113a.png)

   >[!NOTE]
   >
   >如果AEM在另一個連線埠上，請使用該連線埠號碼，而不是4502。 此外，如果您未在本機電腦上執行內容存放庫，請將 `localhost` ，並使用個別伺服器名稱或IP位址。

1. 輸入使用者名稱 `admin` 和密碼 `admin`. Adobe建議您使用預先設定的管理員帳戶進行測試。

   ![chlimage_1-114](assets/chlimage_1-114a.png)

1. 精靈會關閉，新對應的磁碟機會在Windows檔案總管或檔案總管視窗中開啟。

   ![chlimage_1-115](assets/chlimage_1-115a.png)

Windows現在已透過WebDAV將AEM對應為磁碟機，您可以像使用任何其他磁碟機一樣使用它。

### macOS {#macos}

在macOS上透過WebDAV連線不需要設定步驟。 您可以連線到WebDAV伺服器。

1. 導覽至任何 **搜尋器** 視窗並按一下 **前往** 和 **連線到伺服器**，或按下 **Command+k**.
1. 在 **連線到伺服器** 視窗，輸入AEM位置：

   * `http://localhost:4502`

   >[!NOTE]
   >
   >如果AEM在另一個連線埠上，請使用該連線埠號碼，而不是4502。 此外，如果您未在本機電腦上執行內容存放庫，請將 `localhost` ，並使用個別伺服器名稱或IP位址。

1. 當系統提示您進行驗證時，請輸入使用者名稱 `admin` 和密碼 `admin`. Adobe建議您使用預先設定的管理員帳戶進行測試。

macOS現在已透過WebDAV連線至AEM，您可以像使用Mac上的任何其他資料夾一樣使用此資料夾。

### Linux® {#linux}

在Linux®上透過WebDAV連線不需要任何設定，但需要執行幾個步驟來進行連線，因您的案頭環境而異。

#### 地名 {#gnome}

若要使用GNOME透過WebDAV連線至AEM：

1. 在Nautilus （檔案總管）中，選取 **地點** 並選取 **連線到伺服器**.
1. 在 **連線到伺服器** 視窗，選取「服務型別」中的WebDAV (HTTP)。

1. 在 **伺服器**，輸入 `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >如果AEM在另一個連線埠上，請使用該連線埠號碼，而不是4502。 此外，如果您未在本機電腦上執行內容存放庫，請將 `localhost` ，並使用個別伺服器名稱或IP位址。

1. 在 **資料夾**，輸入 `/dav`
1. 輸入使用者名稱 `admin`. Adobe建議您使用預先設定的管理員帳戶進行測試。
1. 將連線埠保留空白，並為您的連線輸入任何名稱。
1. 按一下「**連結**」。AEM會提示您輸入密碼。
1. 輸入密碼 `admin` 並按一下 **連線**.

GNOME現在已將AEM掛接為磁碟區，您可以像使用任何其他磁碟區一樣使用它。

#### KDE {#kde}

1. 開啟網路資料夾精靈。
1. 選取 **Web資料夾**(webdav)，然後按「下一步」。
1. 在 **名稱**，輸入連線名稱。
1. 在 **使用者**，輸入 `admin.` Adobe建議您使用預先設定的管理帳戶。
1. 在 **伺服器**，輸入 `http://localhost:4502/crx/repository/crx.default`

   >[!NOTE]
   >
   >如果AEM在另一個連線埠上，請使用該連線埠號碼，而不是4502。 此外，如果您未在本機電腦上執行內容存放庫，請將 `localhost` 和個別伺服器名稱或IP位址

1. 在 **資料夾**，輸入 `dav`

1. 按一下 **儲存並連線**.
1. 提示輸入密碼時，請輸入密碼 `admin` 並按一下 **連線**.

KDE現在已將AEM掛接為磁碟區，您可以像使用任何其他磁碟區一樣使用它。
