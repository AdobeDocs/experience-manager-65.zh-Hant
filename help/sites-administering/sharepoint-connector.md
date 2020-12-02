---
title: SharePoint Connector
seo-title: SharePoint Connector
description: Day JCR Connector for Microsoft SharePoint 2010和Microsoft SharePoint 2013,4.0版。
seo-description: 瞭解AEM中的Sharepoint Connector。
uuid: df650476-4e2a-486f-a007-b5ac437ff99f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 907316d1-3d23-4c46-bccb-bad6fe1bd1bb
docset: aem65
translation-type: tm+mt
source-git-commit: cc3a2ce7cb3dc020f5466a4b65cf5a9714e7a344
workflow-type: tm+mt
source-wordcount: '1571'
ht-degree: 0%

---


# SharePoint連接器{#sharepoint-connector}

本文包含有關Adobe JCR Connector for Microsoft SharePoint 2010和Microsoft SharePoint 2013 4.0版的詳細資訊。

SharePoint連接器支援下列基本功能：

* 從SharePoint讀取內容和中繼資料。
* 通過應用本機SharePoint身份驗證和授權，確認訪問內容的SharePoint安全設定
* 使用Content Finder進行內容整合
* 使用AEM元件（例如外部資源）來顯示SharePoint影像和視訊
* 將SharePoint與AEM資產同步化

所有功能都是使用原生SharePoint web services，做為SharePoint內容與服務的介面來實作。

>[!NOTE]
>
>AEM 6.1 Service Pack 2也支援SharePoint Connector。 連接器不再支援虛擬儲存庫裝載，因此無法裝載它。 如果要使用Java API訪問Sharepoint儲存庫，請在項目中使用Sharepoint連接器的JCR儲存庫實施。
>
>SharePoint伺服器和相關IT基礎架構的安裝、配置、管理和IT操作不在本文檔的範圍之內。 有關這些主題的資訊，請參見[SharePoint](https://www.microsoft.com/sharepoint)上的供應商文檔。 連接器要求正確安裝、配置和操作基礎架構的這些部分。


## 開始使用{#getting-started}

要開始使用連接器，請執行以下操作：

* 請確定您至少已安裝Java 7。
* 從「軟體分發」下載連接器軟體包分發檔案。
* 將有效的&#x200B;*license.properties*&#x200B;檔案複製到包含&#x200B;*cq-quickstart-6.4.0.jar*&#x200B;檔案的目錄。

* 按兩下／點選。jar檔案以啟動AEM，或從命令列啟動它。
* 從「包管理器」安裝連接器包。
* 配置連接器選項。

## 安裝SharePoint連接器{#installing-sharepoint-connector}

連接器是便於安裝的內容封裝。 使用Package Manager安裝套件，然後設定SharePoint伺服器URL
和其他配置選項。 SharePoint內容可在AEM儲存庫中使用。

### 安裝要求{#installation-requirements}

連接器需要：

* Java Runtime Environment 1.7或更新版本
* 透過網路提供SharePoint Web Services
* SharePoint伺服器URL
* CRX和SharePoint資料庫的使用者憑證和權限
* [支援的平台](#supported-platforms)

SharePoint連接器可從[軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-17673)下載。

### 支援的平台{#supported-platforms}

連接器支援以下功能：

* AEM版本：

   * AEM 6.4、6.3

* Microsoft SharePoint版本：

   * Microsoft Office SharePoint Server(MOSS)2010
   * Microsoft Office SharePoint Server(MOSS)2013

* 如果您需要支援連接器的自訂部署（OEM、特殊要求、自訂驗證方法），請洽詢您所在地區的Adobe辦公室。

>[!NOTE]
>
>此連接器僅支援Microsoft正式支援的配置。 請參閱[MOSS 2010](https://technet.microsoft.com/en-us/library/cc262485(office.14).aspx)和[MOSS 2013](https://technet.microsoft.com/en-us/library/cc262485.aspx)系統需求。

### 標準安裝{#standard-installation}

「軟體散發」是用來散發產品功能、範例和修補程式。 如需詳細資訊，請參閱[軟體散發檔案](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html#software-distribution)。


#### 與AEM {#integrating-with-aem}整合

安裝連接器內容包。

1. 開啟Adobe支援票證以要求連接器功能。
1. 當套件可供使用時，請下載它，然後開啟AEM例項的Package Manager。
1. 從軟體包描述頁點選／按一下&#x200B;**Install**。
1. 在&#x200B;**安裝軟體包**&#x200B;對話框中，按一下／按一下&#x200B;**安裝**。

   **注意**:請確定您是以管理員身分登入。

1. 安裝軟體包後，點選／按一下&#x200B;**Close**。

## 配置SharePoint連接器{#configuring-sharepoint-connector}

安裝SharePoint連接器後，請為連接器配置應用程式和SharePoint層。

設定SharePoint伺服器URL，讓您的SharePoint儲存庫JCR符合規範。 您可以設定額外參數來配置與SharePoint伺服器的連接。 此外，還可使用SharePoint連接器來設定驗證。

### 配置與SharePoint伺服器{#configuring-the-connection-with-the-sharepoint-server}的連接

要設定SharePoint伺服器的URL和高級選項，請執行以下步驟：

1. 導覽至OSGi Management Console:[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)。
1. 搜索&#x200B;**Day JCR Connector for Microsoft Sharepoint**&#x200B;捆綁包。
1. 編輯配置值。
1. 將SharePoint伺服器URL設為&#x200B;**Workspaces**&#x200B;的值。
1. 點選／按一下&#x200B;**儲存**。

![chlimage_1-62](assets/chlimage_1-62.png)

「工作區」和「預設工作區名稱」參數：

依預設，連接器會公開單一JCR工作區。 此工作區公開的SharePoint伺服器是透過「Sharepoint伺服器URL」設定參數來設定。

連接器也可以配置為多個工作區。 在這種情況下，每個工作區都與通過工作區公開的各個SharePoint伺服器的URL相關聯。 若要新增工作區，請新增工作區定義至「工作區」參數。 工作區定義具有以下格式：
`<name>`= `<url>`其中
`<name>`是JCR工作區的名稱，
`<url>`是該工作區的SharePoint伺服器URL。

在AEM中，請執行上述設定步驟以外的另一個步驟。 允許列出&#39;**com.day.cq.dam.cq-dam-jcr-connectors**&#39;組合。

若要允許AEM中的清單組合，請執行下列步驟：

1. 導覽至OSGi Management Console:http://localhost:4502/system/console/configMgr。
1. 搜尋「Apache Sling Login Admin Whitelist」服務。
1. 選擇&#x200B;**繞過白名單**。
1. 將`com.day.cq.dam.cq-dam-jcr-connectors`新增至白名單組合預設值
1. 按一下「儲存」。

![chlimage_1-82](assets/chlimage_1-82a.png)

>[!NOTE]
>
>如果您設定多個工作區，請在「預設工作區名稱」參數中指定預設工作區的名稱。

有關與身份驗證相關的參數的其他資訊，請參見[Authentication](/help/sites-administering/sharepoint-connector.md#configuring-authentication)。

### 驗證Sharepoint設定{#verifying-the-sharepoint-setup}

配置連接器後，請驗證以下內容：

* SharePoint伺服器會執行，而Web服務可供連接器例項存取
* SharePoint使用者憑證是有效的，而且使用者具有必要的SharePoint權限
* 連接器已正確安裝和配置

### 配置與SharePoint伺服器{#configuring-dam-sync-with-the-sharepoint-server}的DAM同步

若要將SharePoint Assets與AEM同步，請執行下列步驟：

1. 導覽至OSGi Management Console:[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)。
1. 搜索「預設DAMAssetSynchronization」服務。
1. 編輯配置值。
1. 設定有權在SharePoint網站上存取之使用者的使用者名稱和對應密碼。
1. 按一下「儲存」。

啟用DAM同步服務，預設禁用該服務：

1. 導覽至「OSGi Web Console元件」:[http://localhost:4502/system/console/components](http://localhost:4502/system/console/components)
1. 搜尋「com.day.cq.dam.jcrconnectors.impl.AssetSynchronizationService」。
1. 按一下「啟用」。

或者，您可以配置不同同步週期之間的同步延遲：

1. 導覽至OSGi Management Console:[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
1. 搜尋「DAY CQ DAM JCR Connector Asset Synchronization Service」。
1. 編輯配置值。
1. 設定同步時段的值（以秒為單位）。
1. 按一下「儲存」。

### 配置驗證{#configuring-authentication}

Sharepoint包含「經典」和「基於索賠的」驗證方法，這兩種方法都支援以下驗證類型：

* 基本
* 表單型

尤其是，下列驗證類型可用：

* Classic-Basic
* 傳統型表單
* 基本索賠
* 基於索賠表單

AEM JCR Connector for Microsoft SharePoint 2010和Microsoft SharePoint 2013,4.0版。支援基於索賠的驗證（由Microsoft建議），該驗證在以下模式下運行：

* **基本/NTLM身份驗證**:連接器首先嘗試使用基本驗證進行連接。如果不可用，則切換到基於NTLM的身份驗證。
* **表單式驗證**:Sharepoint會根據使用者在登入表單（通常是網頁）中輸入的認證來驗證使用者。該系統為已驗證的請求發出令牌，該令牌包含用於為後續請求重新建立標識的密鑰。

**配置基於表單的驗證**

前往：[http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)

1. 按一下OSGI ->配置
1. 搜尋「Day JCR Connector for Microsoft Sharepoint」
1. 按一下「編輯設定值」
1. 將「Sharepoint Connection Factory」的值設為「com.day.crx.spi.sharepoint.security.FormsBasedAuthenticationConnectionFactory」
1. 按一下&#x200B;**「儲存」**。

**配置基本身份驗證(Windows)**

1. [停用Token驗證](#disable-token-authentication)。
1. 前往[http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)。
1. 按一下「OSGI >設定」。
1. 搜索&#x200B;**Day JCR Connector for Microsoft Sharepoint**。
1. 按一下 `Edit the configuration values`.
1. 將「Sharepoint連接工廠」的值設定為`com.day.crx.spi.sharepoint.security.WindowsAuthenticationConnectionFactory`。
1. 按一下&#x200B;**「儲存」**。

只有在AEM和SharePoint上都經過驗證的使用者才能透過連接器存取SharePoint內容。

您也可以使用驗證的連接器擴充功能來建立自訂驗證模組，例如，將AEM使用者的存取權對應至特定SharePoint使用者。 建立與SharePoint使用者對應的AEM使用者（使用者名稱和密碼應相符），以便能夠查看對應至連接器例項的SharePoint內容。

若要在AEM中建立使用者：

1. 登入http://localhost:9502/with管理員使用者。
1. 按一下「工具」。
1. 按一下「安全性」。
1. 按一下「使用者」。
1. 按一下&#x200B;**建立用戶**。
1. 提供使用者ID（可存取SharePoint的使用者名稱）。
1. 提供對應的密碼。
1. 按一下「綠色勾號」(Green tick)符號以建立使用者。

若要在管理員群組中新增使用者：

1. 前往「群組管理」。
1. 按一下「a」節點。
1. 按一下「管理員」。
1. 在&#x200B;**Browse**&#x200B;按鈕之前的文字方塊中，輸入上述建立的使用者ID。
1. 按一下「綠色勾選」符號，將使用者新增至管理群組。

### 停用Token驗證{#disable-token-authentication}

1. 下載並安裝軟體包`basic auth`。 `zip` 從「軟體散發」。

1. 關閉快速入門。
1. 開啟檔案&#x200B;*\crx-quickstart\repository\repository.xml*。
1. 尋找標籤`<LoginModule class="com.day.crx.core.CRXLoginModule"> ... </LoginModule>.`
1. 將標籤`<param name="disableTokenAuth" value="true"/>`插入步驟4中提及的標籤內。
1. 儲存並關閉xml檔案。
1. 重新啟動QuickStart並使用您的認證登入。

#### 支援SharePoint伺服器{#supporting-different-authentication-methods-of-the-sharepoint-server}的不同驗證方法

在其標準版本中，連接器支援標準IIS **Windows**&#x200B;驗證（基本）和基於表單的驗證（基於令牌）。 可通過擴展性機制支援[其它驗證方法](https://technet.microsoft.com/en-us/library/cc262350.aspx#section2)。

以下步驟提供有關擴展標準身份驗證的指導，以支援SharePoint伺服器的各種身份驗證方法：

1. 實作`com.day.crx.spi.sharepoint.security.SharepointConnectionFactory`以處理您特定驗證程式的用戶端。
1. 將`SharepointConnectionFactory`實作安裝為帶有片段主機`com.day.crx.spi.crx2sharepoint-bundle`的片段包。

   使用Maven時，請根據項目要求調整`maven-bundle-plugin`的以下配置：

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

1. 在連接器配置中註冊`SharepointConnectionFactory`實施。 在連接器的配置窗口中，按一下&#x200B;**高級選項**。 在&#x200B;**Sharepoint連接工廠**&#x200B;欄位中，指定實施`com.day.crx.spi.sharepoint.auth.CustomConnectionFactory`的名稱。

1. 重新啟動連接器。

