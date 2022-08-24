---
title: SharePoint連接器
seo-title: SharePoint Connector
description: 用於MicrosoftSharePoint2010和MicrosoftSharePoint2013的日JCR連接器，4.0版。
seo-description: Learn about the Sharepoint Connector in AEM.
uuid: df650476-4e2a-486f-a007-b5ac437ff99f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 907316d1-3d23-4c46-bccb-bad6fe1bd1bb
docset: aem65
exl-id: 10ea7d2e-6e44-4d5c-a2b2-63c73b18f172
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1562'
ht-degree: 2%

---

# SharePoint連接器{#sharepoint-connector}

本文包括有關MicrosoftSharePoint2010和MicrosoftSharePoint2013版JCR連接器的AdobeJCR連接器4.0的詳細資訊。

SharePoint連接器支援以下基本功能：

* 正在閱讀SharePoint的內容和元資料。
* 通過應用本機SharePoint身份驗證和授權來確認訪問內容的SharePoint安全設定
* 使用Content Finder進行內容整合
* 使用AEM元件（如外部資源）顯示SharePoint影像和視頻
* 使SharePoint與AEM Assets同步

所有功能都使用SharePoint本地網路服務作為SharePoint內容和服務的介面來實現。

>[!NOTE]
>
>SharePointConnector也受AEM6.1 Service Pack 2支援。 連接器不再支援虛擬儲存庫裝載，因此無法裝載。 如果要使用Java API訪問Sharepoint儲存庫，請在項目中使用Sharepoint連接器的JCR儲存庫實現。
>
>SharePoint伺服器和相關IT基礎架構的安裝、配置、管理和IT操作不在本文檔的範圍之內。 請參閱上的供應商文檔 [SharePoint](https://www.microsoft.com/sharepoint) 的子菜單。 連接器要求正確安裝、配置和操作基礎架構的這些部分。

## 入門 {#getting-started}

要開始使用連接器，請執行以下操作：

* 確保至少安裝了Java 7。
* 從「軟體分發」下載連接器包分發檔案。
* 複製有效 *license.properties* 檔案到包含 *cq-quickstart-6.4.0.jar* 的子菜單。

* 按兩下/點擊.jar檔案以啟AEM動，或從命令行啟動。
* 從包管理器安裝連接器包。
* 配置連接器選項。

## 安裝SharePoint連接器 {#installing-sharepoint-connector}

連接器是便於安裝的內容包。 使用包管理器安裝包，然後設定SharePoint伺服器URL和其他配置選項。 SharePoint內容可在儲存庫AEM中找到。

### 安裝要求 {#installation-requirements}

連接器需要以下條件：

* Java運行時環境1.7或更高版本
* SharePointWeb服務可通過網路提供
* SharePoint伺服器URL
* CRX和SharePoint儲存庫的用戶憑據和權限
* [支援的平台](#supported-platforms)

SharePoint連接器可從下載 [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-17673)。

### 支援的平台 {#supported-platforms}

連接器支援以下內容：

* AEM版本：

   * AEM 6.4, 6.3

* MicrosoftSharePoint版：

   * MicrosoftOfficeSharePoint伺服器(MOSS)2010
   * Microsoft辦公室SharePoint伺服器(MOSS)2013

* 如果您需要對連接器的自定義部署（OEM、特殊要求、自定義身份驗證方法）提供支援，請與您所在區域的Adobe辦公室聯繫。

>[!NOTE]
>
>連接器僅支援Microsoft正式支援的配置。 請參閱 [MOSS 2010](https://technet.microsoft.com/en-us/library/cc262485(office.14).aspx) 和 [MOSS 2013](https://technet.microsoft.com/en-us/library/cc262485.aspx) 系統要求。

### 標準安裝 {#standard-installation}

軟體分發用於分發產品功能、示例和熱修復。 有關詳細資訊，請參閱 [軟體分發文檔](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html#software-distribution)。


#### 與整合AEM {#integrating-with-aem}

安裝連接器內容包。

1. 開啟Adobe支援票證以請求連接器功能。
1. 在包可用時下載該包，然後開啟實例的包管AEM理器。
1. 點擊/按一下 **安裝** 的子菜單。
1. 從 **安裝包** 對話框，點擊/按一下 **安裝**。

   **注釋**:確保您以管理員身份登錄。

1. 安裝軟體包後，點擊/按一下 **關閉**。

## 配置SharePoint連接器 {#configuring-sharepoint-connector}

安裝SharePoint連接器後，請為連接器配置應用程式和SharePoint層。

設定SharePoint伺服器URL，使SharePoint資料庫JCR相容。 可以設定額外參數來配置與SharePoint伺服器的連接。 此外，使用SharePoint連接器配置身份驗證。

### 配置與SharePoint伺服器的連接 {#configuring-the-connection-with-the-sharepoint-server}

要設定SharePoint伺服器的URL和高級選項，請執行以下步驟：

1. 導航到OSGi管理控制台： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)。
1. 搜索 **Day JCR Connector forMicrosoftSharepoint** 捆綁。
1. 編輯配置值。
1. 將SharePoint伺服器URL設定為 **工作區**。
1. 點擊/按一下 **保存**。

![chlimage_1-62](assets/chlimage_1-62.png)

「工作區」和「預設工作區名稱」參數：

預設情況下，連接器顯示單個JCR工作區。 此工作區公開的SharePoint伺服器通過「Sharepoint Server URL」配置參數設定。

連接器也可配置為多個工作區。 在這種情況下，每個工作區都與通過工作區公開的各個SharePoint伺服器的URL相關聯。 要添加工作區，請向「工作區」參數添加工作區定義。 工作區定義具有以下格式：
`<name>`= `<url>` 何處
`<name>` 是JCR工作區的名稱，
`<url>` 是該工作區的SharePoint伺服器的URL。

在中AEM，執行除上述配置步驟之外的另一步。 允許列出「**com.day.cq.dam.cq-dam-jcr-connectors**&#39;捆綁。

要允許清單捆綁AEM，請執行以下步驟：

1. 導航到OSGi管理控制台：http://localhost:4502/system/console/configMgr。
1. 搜索「Apache Sling登錄管理白名單」服務。
1. 選擇 **繞過白名單**。
1. 添加 `com.day.cq.dam.cq-dam-jcr-connectors` 白名單包預設
1. 按一下「儲存」。

![chlimage_1-82](assets/chlimage_1-82a.png)

>[!NOTE]
>
>如果配置了多個工作區，請在「預設工作區名稱」(Default Workspace Name)參數中指定預設工作區的名稱。

有關與身份驗證相關的參數的其他資訊，請參見 [驗證](/help/sites-administering/sharepoint-connector.md#configuring-authentication)。

### 驗證Sharepoint設定 {#verifying-the-sharepoint-setup}

配置連接器後，驗證以下內容：

* SharePoint伺服器運行，連接器實例可以訪問Web服務
* SharePoint用戶憑據有效，並且用戶具有必要的SharePoint權限
* 連接器已正確安裝和配置

### 配置與SharePoint伺服器的DAM同步 {#configuring-dam-sync-with-the-sharepoint-server}

要將SharePoint資產與同AEM步，請執行以下步驟：

1. 導航到OSGi管理控制台： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)。
1. 搜索「Default DAMAssetSynchronization」服務。
1. 編輯配置值。
1. 設定有權訪問SharePoint站點的用戶的用戶名和相應密碼。
1. 按一下「儲存」。

啟用DAM同步服務，預設禁用：

1. 導航到OSGi Web控制台元件： [http://localhost:4502/system/console/components](http://localhost:4502/system/console/components)
1. 搜索「com.day.cq.dam.jcrconnectors.impl.AssetSynchronizationService」。
1. 按一下啟用。

（可選）可以配置不同同步週期之間的同步延遲：

1. 導航到OSGi管理控制台： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
1. 搜索「DAY CQ DAM JCR連接器資產同步服務」。
1. 編輯配置值。
1. 設定同步時段的值（秒）。
1. 按一下「儲存」。

### 配置身份驗證 {#configuring-authentication}

Sharepoint包括經典和基於聲明的身份驗證方法，這兩種方法都支援以下身份驗證類型：

* 基本
* Forms

具體而言，以下類型的身份驗證可用：

* 經典 — 基本
* 經典Forms
* 基本聲明
* 基於索賠的Forms

用於AEMMicrosoftSharePoint2010和MicrosoftSharePoint2013的JCR連接器，4.0版。支援基於聲明的身份驗證(Microsoft建議)，它以下列模式運行：

* **基本/NTLM身份驗證**:連接器首先嘗試使用基本身份驗證進行連接。 如果不可用，則切換到基於NTLM的身份驗證。
* **Forms認證**:Sharepoint基於用戶在登錄表單（通常是網頁）中鍵入的憑據來驗證用戶。 系統為經過驗證的請求發出令牌，該令牌包含用於為後續請求重新建立標識的密鑰。

**配置基於Forms的身份驗證**

轉到： [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)

1. 按一下OSGI ->配置
1. 搜索「Day JCR Connector forMicrosoftSharepoint」
1. 按一下「編輯配置值」
1. 將「Sharepoint連接工廠」的值設定為「com.day.crx.spi.sharepoint.security.FormsBasedAuthenticationConnectionFactory」
1. 按一下「**儲存**」。

**配置基本身份驗證(Windows)**

1. [禁用令牌身份驗證](#disable-token-authentication)。
1. 轉到 [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)。
1. 按一下「OSGI」>「配置」。
1. 搜索 **Day JCR Connector forMicrosoftSharepoint**。
1. 按一下 `Edit the configuration values`.
1. 將Sharepoint連接工廠的值設定為 `com.day.crx.spi.sharepoint.security.WindowsAuthenticationConnectionFactory`。
1. 按一下「**儲存**」。

只有在兩者上都經過身份驗證的AEM用戶才能通過連接器訪問SharePoint內容。

您還可以使用連接器擴展進行身份驗證以建立自定義身份驗證模組，例如，將用戶的訪問權映射AEM給特定的SharePoint用戶。 創AEM建與SharePoint用戶（用戶名和密碼應匹配）對應的用戶，以便能夠查看映射到連接器實例的SharePoint內容。

要在中建立用戶AEM:

1. 登錄到http://localhost:9502/with管理員用戶。
1. 按一下「Tools（工具）」。
1. 按一下「Security（安全性）」。
1. 按一下用戶。
1. 按一下 **建立用戶**。
1. 提供用戶ID(在SharePoint具有訪問權限的用戶名)。
1. 提供相應的密碼。
1. 按一下「綠色」(Green)刻度符號以建立用戶。

要在管理組中添加用戶：

1. 轉到組管理。
1. 按一下「a」節點。
1. 按一下「administrators」。
1. 在文本框中鍵入以上建立的用戶ID **瀏覽** 按鈕
1. 按一下綠色刻度符將用戶添加到管理組。

### 禁用令牌身份驗證 {#disable-token-authentication}

1. 下載並安裝包 `basic auth`。 `zip` 從軟體分發。

1. 關閉快速啟動。
1. 開啟檔案 *\crx-quickstart\repository\repository.xml*。
1. 查找標籤 `<LoginModule class="com.day.crx.core.CRXLoginModule"> ... </LoginModule>.`
1. 插入標籤 `<param name="disableTokenAuth" value="true"/>` 在步驟4中提到的標籤中。
1. 保存並關閉xml檔案。
1. 重新啟動QuickStart並使用憑據登錄。

#### 支援SharePoint伺服器的不同身份驗證方法 {#supporting-different-authentication-methods-of-the-sharepoint-server}

在其標準版本中，連接器支援標準IIS **窗口** 驗證（基本）和基於Forms的驗證（基於令牌）。 的 [其他驗證方法](https://technet.microsoft.com/en-us/library/cc262350.aspx#section2) 可以通過擴展機制來支援。

以下步驟提供了有關擴展標準身份驗證以支援SharePoint伺服器各種身份驗證方法的指導：

1. 實施 `com.day.crx.spi.sharepoint.security.SharepointConnectionFactory` 處理特定身份驗證過程的客戶端。
1. 安裝 `SharepointConnectionFactory` 作為帶有片段主機的片段包的實現 `com.day.crx.spi.crx2sharepoint-bundle`。

   使用Maven時，請調整以下配置 `maven-bundle-plugin` 項目要求：

   ```xml
              <plugin>
                  <groupId>org.apache.felix</groupId>
                  <artifactId>maven-bundle-plugin</artifactId>
                  <extensions>true</extensions>
                  <configuration>
                      <instructions>
                          <Export-Package />
                          <Private-Package>
                              <!-- your private package here -->
                          </Private-Package>
                          <Fragment-Host>
                              com.day.crx.spi.crx2sharepoint-bundle
                          </Fragment-Host>
                       </instructions>
                  </configuration>
              </plugin>
   ```

1. 註冊 `SharepointConnectionFactory` 在連接器配置中實現。 在連接器的配置窗口中，按一下 **高級選項**。 在中 **Sharepoint連接工廠** 欄位，指定實現的名稱 `com.day.crx.spi.sharepoint.auth.CustomConnectionFactory`。

1. 重新啟動連接器。
