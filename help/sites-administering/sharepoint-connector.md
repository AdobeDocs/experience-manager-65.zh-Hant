---
title: SharePoint Connector
seo-title: SharePoint Connector
description: 適用於Microsoft SharePoint 2010和Microsoft SharePoint 2013的Day JCR Connector,4.0版。
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

# SharePoint Connector{#sharepoint-connector}

本文包含有關適用於Microsoft SharePoint 2010和Microsoft SharePoint 2013 4.0版的AdobeJCR Connector的詳細資訊。

SharePoint連接器支援下列基本功能：

* 從SharePoint讀取內容和中繼資料。
* 套用原生SharePoint驗證和授權，確認所存取內容的SharePoint安全性設定
* 使用內容尋找器進行內容整合
* 使用AEM元件（例如外部資源）來顯示SharePoint影像和視訊
* 同步SharePoint與AEM Assets

所有功能都是使用原生SharePoint網站服務來實作，作為SharePoint內容與服務的介面。

>[!NOTE]
>
>AEM 6.1 Service Pack 2也支援SharePoint Connector。 連接器不再支援虛擬存放庫裝載，因此無法裝載。 如果要使用Java API訪問Sharepoint儲存庫，請在項目中使用Sharepoint Connector的JCR儲存庫實施。
>
>SharePoint伺服器和相關IT基礎架構的安裝、配置、管理和IT操作不在本文檔的範圍之內。 請參閱以下的供應商文檔： [SharePoint](https://www.microsoft.com/sharepoint) 以取得這些主題的資訊。 連接器要求正確安裝、配置和操作基礎架構的這些部分。

## 快速入門 {#getting-started}

若要開始使用連接器，請執行下列動作：

* 請確定您至少已安裝Java 7。
* 從Software Distribution下載連接器封裝發佈檔案。
* 複製有效 *license.properties* 檔案至包含 *cq-quickstart-6.4.0.jar* 檔案。

* 按兩下/點選.jar檔案以啟動AEM，或從命令列啟動。
* 從「封裝管理器」安裝連接器封裝。
* 配置連接器選項。

## 安裝SharePoint連接器 {#installing-sharepoint-connector}

該連接器是便於安裝的內容封裝。 使用套件管理器安裝套件，然後設定SharePoint伺服器URL和其他設定選項。 AEM存放庫中提供SharePoint內容。

### 安裝需求 {#installation-requirements}

連接器需要下列項目：

* Java Runtime Environment 1.7或更新版本
* SharePoint網站服務可透過網路取得
* SharePoint伺服器URL
* CRX和SharePoint存放庫的使用者認證和權限
* [支援平台](#supported-platforms)

SharePoint連接器可從下載 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-17673).

### 支援平台 {#supported-platforms}

連接器支援下列功能：

* AEM版本：

   * AEM 6.4、6.3

* Microsoft SharePoint版本：

   * Microsoft Office SharePoint伺服器(MOSS)2010
   * Microsoft Office SharePoint伺服器(MOSS)2013

* 如果您需要支援連接器的自訂部署（OEM、特殊要求、自訂驗證方法），請與貴地區的Adobe辦公室聯繫。

>[!NOTE]
>
>連接器僅支援Microsoft正式支援的設定。 請參閱 [MOSS 2010](https://technet.microsoft.com/en-us/library/cc262485(office.14).aspx) 和 [MOSS 2013](https://technet.microsoft.com/en-us/library/cc262485.aspx) 系統需求。

### 標準安裝 {#standard-installation}

Software Distribution可用來發佈產品功能、範例和Hotfix。 如需詳細資訊，請參閱 [Software Distribution檔案](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html#software-distribution).


#### 與AEM整合 {#integrating-with-aem}

安裝連接器內容封裝。

1. 開啟「Adobe支援」票證以要求連接器功能。
1. 若有套件可用，請下載該套件，然後開啟AEM執行個體的套件管理器。
1. 點選/按一下 **安裝** 從包說明頁面。
1. 從 **安裝套件** 對話方塊，點選/按一下 **安裝**.

   **附註**:請確定您是以管理員身分登入。

1. 安裝套件時，點選/按一下 **關閉**.

## 配置SharePoint連接器 {#configuring-sharepoint-connector}

安裝SharePoint連接器後，請為連接器配置應用程式和SharePoint層。

設定SharePoint伺服器URL，使您的SharePoint存放庫JCR符合規範。 您可以設定額外的參數來設定與SharePoint伺服器的連線。 此外，請使用SharePoint連接器設定驗證。

### 設定與SharePoint伺服器的連線 {#configuring-the-connection-with-the-sharepoint-server}

若要設定SharePoint伺服器的URL和進階選項，請執行下列步驟：

1. 導覽至OSGi管理控制台： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. 搜尋 **Day JCR Connector for Microsoft Sharepoint** 捆綁。
1. 編輯設定值。
1. 將SharePoint伺服器URL設定為 **工作區**.
1. 點選/按一下 **儲存**.

![chlimage_1-62](assets/chlimage_1-62.png)

「工作區」和「預設工作區名稱」參數：

依預設，連接器會公開單一JCR工作區。 此工作區公開的SharePoint伺服器是通過「Sharepoint伺服器URL」配置參數設定的。

連接器也可針對多個工作區而設定。 在此情況下，每個工作區都會與透過工作區公開之個別SharePoint伺服器的URL相關聯。 若要新增工作區，請將工作區定義新增至工作區參數。 工作區定義的格式如下：
`<name>`= `<url>` where
`<name>` 是JCR工作區的名稱，且
`<url>` 是該工作區的SharePoint伺服器URL。

在AEM中，除了上述設定步驟以外，再執行一個步驟。 允許列出「**com.day.cq.dam.cq-dam-jcr-connectors**&#39;組合。

若要在AEM中允許清單套件組合，請執行下列步驟：

1. 導覽至OSGi管理控制台：http://localhost:4502/system/console/configMgr。
1. 搜尋「Apache Sling登入管理員白名單」服務。
1. 選擇 **略過白名單**.
1. 新增 `com.day.cq.dam.cq-dam-jcr-connectors` 白名單套件預設
1. 按一下「儲存」。

![chlimage_1-82](assets/chlimage_1-82a.png)

>[!NOTE]
>
>如果配置了多個工作區，請在「預設工作區名稱」(Default Workspace Name)參數中指定預設工作區的名稱。

如需與驗證相關的參數的其他資訊，請參閱 [驗證](/help/sites-administering/sharepoint-connector.md#configuring-authentication).

### 驗證Sharepoint設定 {#verifying-the-sharepoint-setup}

配置連接器後，請驗證以下內容：

* SharePoint伺服器會執行，而連接器執行個體可存取web服務
* SharePoint使用者憑證有效，且使用者擁有必要的SharePoint權限
* 已正確安裝並配置連接器

### 設定與SharePoint伺服器的DAM同步 {#configuring-dam-sync-with-the-sharepoint-server}

若要將SharePoint Assets與AEM同步，請執行下列步驟：

1. 導覽至OSGi管理控制台： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. 搜索「Default DAMAssetSynchronization」服務。
1. 編輯設定值。
1. 設定在SharePoint網站上具有存取權之使用者的使用者名稱和對應密碼。
1. 按一下「儲存」。

啟用DAM同步服務，預設會停用：

1. 導覽至OSGi Web主控台元件： [http://localhost:4502/system/console/components](http://localhost:4502/system/console/components)
1. 搜尋「com.day.cq.dam.jcrconnectors.impl.AssetSynchronizationService」。
1. 按一下「啟用」。

您可以根據需要配置不同同步週期之間的同步延遲：

1. 導覽至OSGi管理控制台： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
1. 搜尋「DAY CQ DAM JCR連接器資產同步服務」。
1. 編輯設定值。
1. 設定同步週期的值（以秒為單位）。
1. 按一下「儲存」。

### 配置驗證 {#configuring-authentication}

Sharepoint包括基於傳統和聲明的身份驗證方法，這兩種方法均支援以下身份驗證類型：

* 基本
* Forms

尤其是，下列驗證類型可供使用：

* Classic-Basic
* 傳統型Forms
* 基本索賠
* 基於索賠的Forms

適用於Microsoft SharePoint 2010和Microsoft SharePoint 2013的AEM JCR Connector 4.0版支援以聲明為基礎的驗證(由Microsoft建議)，其運作方式如下：

* **基本/NTLM身份驗證**:連接器會先嘗試使用基本驗證來連線。 如果不可用，則切換為基於NTLM的身份驗證。
* **Forms型驗證**:Sharepoint根據用戶在登錄表單中鍵入的憑據（通常為網頁）來驗證用戶。 系統為已驗證的請求發出令牌，該令牌包含用於為後續請求重新建立標識的密鑰。

**設定Forms式驗證**

前往： [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)

1. 按一下「OSGI ->設定」
1. 搜尋「Day JCR Connector for Microsoft Sharepoint」
1. 按一下「編輯配置值」
1. 將「Sharepoint連接工廠」的值設定為「com.day.crx.spi.sharepoint.security.FormsBasedAuthenticationConnectionFactory」
1. 按一下「**儲存**」。

**配置基本身份驗證(Windows)**

1. [禁用令牌驗證](#disable-token-authentication).
1. 前往 [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles).
1. 按一下「OSGI >設定」。
1. 搜尋 **Day JCR Connector for Microsoft Sharepoint**.
1. 按一下 `Edit the configuration values`.
1. 將Sharepoint連接工廠的值設定為 `com.day.crx.spi.sharepoint.security.WindowsAuthenticationConnectionFactory`.
1. 按一下「**儲存**」。

只有同時在AEM和SharePoint上驗證的使用者才能透過連接器存取SharePoint內容。

您也可以使用驗證的連接器擴充功能來建立自訂驗證模組，例如，將AEM使用者的存取權對應至特定SharePoint使用者。 建立與SharePoint使用者對應的AEM使用者（使用者名稱與密碼應相符），以便查看對應至連接器例項的SharePoint內容。

若要在AEM中建立使用者：

1. 登入http://localhost:9502/with管理員使用者。
1. 按一下「工具」。
1. 按一下「安全性」。
1. 按一下「使用者」。
1. 按一下 **建立使用者**.
1. 提供使用者ID(在SharePoint上具有存取權的使用者名稱)。
1. 提供對應的密碼。
1. 按一下綠色勾號以建立使用者。

若要在管理群組中新增使用者：

1. 前往「群組管理」。
1. 按一下「a」節點。
1. 按一下「管理員」。
1. 在前面的文字方塊中，輸入上方建立的使用者ID **瀏覽** 按鈕。
1. 按一下綠色勾號，將使用者新增至管理群組。

### 禁用令牌驗證 {#disable-token-authentication}

1. 下載並安裝套件 `basic auth`. `zip` 從Software Distribution.

1. 關閉快速入門。
1. 開啟檔案 *\crx-quickstart\repository\repository.xml*.
1. 尋找標籤 `<LoginModule class="com.day.crx.core.CRXLoginModule"> ... </LoginModule>.`
1. 插入標籤 `<param name="disableTokenAuth" value="true"/>` 在步驟4中提及的標籤內。
1. 保存並關閉xml檔案。
1. 重新啟動QuickStart並使用您的憑據登錄。

#### 支援SharePoint伺服器的不同驗證方法 {#supporting-different-authentication-methods-of-the-sharepoint-server}

在其標準版本中，連接器支援標準IIS **Windows** 驗證（基本）和Forms式驗證（以權杖為基礎）。 此 [其他驗證方法](https://technet.microsoft.com/en-us/library/cc262350.aspx#section2) 可透過擴充性機制來支援。

下列步驟提供延伸標準驗證的相關准則，以支援SharePoint伺服器的各種驗證方法：

1. 實作 `com.day.crx.spi.sharepoint.security.SharepointConnectionFactory` 來處理您特定驗證程式的用戶端。
1. 安裝 `SharepointConnectionFactory` 片段主機的片段套件組合實作 `com.day.crx.spi.crx2sharepoint-bundle`.

   使用Maven時，請調整 `maven-bundle-plugin` 符合您專案的需求：

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

1. 註冊 `SharepointConnectionFactory` 在連接器設定中實作。 在連接器的配置窗口中，按一下 **進階選項**. 在 **Sharepoint連接工廠** 欄位，指定實作的名稱 `com.day.crx.spi.sharepoint.auth.CustomConnectionFactory`.

1. 重新啟動連接器。
