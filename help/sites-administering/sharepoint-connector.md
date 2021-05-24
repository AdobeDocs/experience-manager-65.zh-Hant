---
title: SharePoint Connector
seo-title: SharePoint Connector
description: Day JCR Connector for Microsoft SharePoint 2010和Microsoft SharePoint 2013,4.0版。
seo-description: 了解AEM中的Sharepoint Connector。
uuid: df650476-4e2a-486f-a007-b5ac437ff99f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 907316d1-3d23-4c46-bccb-bad6fe1bd1bb
docset: aem65
exl-id: 10ea7d2e-6e44-4d5c-a2b2-63c73b18f172
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1571'
ht-degree: 0%

---

# SharePoint Connector{#sharepoint-connector}

本文包含有關AdobeJCR Connector for Microsoft SharePoint 2010和Microsoft SharePoint 2013 4.0版的詳細資訊。

SharePoint連接器支援以下基本功能：

* 從SharePoint讀取內容和元資料。
* 通過應用本機SharePoint身份驗證和授權來確認訪問內容的SharePoint安全設定
* 使用內容尋找器進行內容整合
* 使用AEM元件（例如外部資源）來顯示SharePoint影像和視訊
* 與SharePoint同步AEM Assets

所有功能都使用本機SharePoint Web服務作為SharePoint內容和服務的介面來實現。

>[!NOTE]
>
>AEM 6.1 Service Pack 2也支援SharePoint Connector。 連接器不再支援虛擬存放庫裝載，因此無法裝載。 如果要使用Java API訪問Sharepoint儲存庫，請在項目中使用Sharepoint Connector的JCR儲存庫實施。
>
>SharePoint伺服器和相關IT基礎架構的安裝、配置、管理和IT操作不在本文檔的範圍之內。 有關這些主題的資訊，請參閱[SharePoint](https://www.microsoft.com/sharepoint)上的供應商文檔。 連接器要求正確安裝、配置和操作基礎架構的這些部件。


## 入門{#getting-started}

若要開始使用連接器，請執行下列動作：

* 請確定您至少已安裝Java 7。
* 從Software Distribution下載連接器封裝發佈檔案。
* 將有效的&#x200B;*license.properties*&#x200B;檔案複製到包含&#x200B;*cq-quickstart-6.4.0.jar*&#x200B;檔案的目錄。

* 按兩下/點選.jar檔案以啟動AEM，或從命令列啟動。
* 從「封裝管理器」安裝連接器封裝。
* 配置連接器選項。

## 安裝SharePoint連接器{#installing-sharepoint-connector}

該連接器是便於安裝的內容封裝。 使用包管理器安裝包，然後設定SharePoint伺服器URL
和其他設定選項。 SharePoint內容可在AEM儲存庫中使用。

### 安裝要求{#installation-requirements}

連接器需要下列項目：

* Java Runtime Environment 1.7或更新版本
* 通過網路提供的SharePoint Web服務
* SharePoint伺服器URL
* CRX和SharePoint儲存庫的用戶憑據和權限
* [支援平台](#supported-platforms)

SharePoint連接器可從[軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-17673)下載。

### 支援的平台{#supported-platforms}

連接器支援下列功能：

* AEM版本：

   * AEM 6.4、6.3

* Microsoft SharePoint版本：

   * Microsoft Office SharePoint Server(MOSS)2010
   * Microsoft Office SharePoint Server(MOSS)2013

* 如果您需要支援連接器的自訂部署（OEM、特殊要求、自訂驗證方法），請與貴地區的Adobe辦公室聯繫。

>[!NOTE]
>
>連接器僅支援Microsoft正式支援的配置。 請參閱[MOSS 2010](https://technet.microsoft.com/en-us/library/cc262485(office.14).aspx)和[MOSS 2013](https://technet.microsoft.com/en-us/library/cc262485.aspx)系統要求。

### 標準安裝{#standard-installation}

Software Distribution可用來發佈產品功能、範例和Hotfix。 如需詳細資訊，請參閱[軟體發佈檔案](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html#software-distribution)。


#### 與AEM整合{#integrating-with-aem}

安裝連接器內容封裝。

1. 開啟「Adobe支援」票證以要求連接器功能。
1. 若有套件可用，請下載該套件，然後開啟AEM執行個體的套件管理器。
1. 從套件說明頁麵點選/按一下「**安裝**」。
1. 在&#x200B;**Install Package**&#x200B;對話方塊中，點選/按一下&#x200B;**Install**。

   **注意**:請確定您是以管理員身分登入。

1. 安裝套件時，點選/按一下「**關閉**」。

## 配置SharePoint連接器{#configuring-sharepoint-connector}

安裝SharePoint連接器後，請為連接器配置應用程式和SharePoint層。

設定SharePoint伺服器URL以使SharePoint儲存庫JCR相容。 您可以設定額外的參數來配置與SharePoint伺服器的連接。 此外，使用SharePoint連接器配置身份驗證。

### 配置與SharePoint伺服器{#configuring-the-connection-with-the-sharepoint-server}的連接

要設定SharePoint伺服器的URL和高級選項，請執行以下步驟：

1. 導覽至OSGi管理控制台：[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)。
1. 搜索Microsoft Sharepoint **套件組合的** Day JCR Connector。
1. 編輯設定值。
1. 將SharePoint伺服器URL設定為&#x200B;**Workspaces**&#x200B;的值。
1. 點選/按一下&#x200B;**儲存**。

![chlimage_1-62](assets/chlimage_1-62.png)

「工作區」和「預設工作區名稱」參數：

依預設，連接器會公開單一JCR工作區。 此工作區公開的SharePoint伺服器是通過「Sharepoint伺服器URL」配置參數設定的。

連接器也可針對多個工作區而設定。 在這種情況下，每個工作區都與通過工作區公開的各個SharePoint伺服器的URL相關聯。 若要新增工作區，請將工作區定義新增至工作區參數。 工作區定義的格式如下：
`<name>`= `<url>`，其中
`<name>`是JCR工作區的名稱，
`<url>`是該工作區的SharePoint伺服器的URL。

在AEM中，除了上述設定步驟以外，再執行一個步驟。 允許列出「**com.day.cq.dam.cq-dam-jcr-connectors**」套件組合。

若要在AEM中允許清單套件組合，請執行下列步驟：

1. 導覽至OSGi管理控制台：http://localhost:4502/system/console/configMgr。
1. 搜尋「Apache Sling登入管理員白名單」服務。
1. 選擇&#x200B;**繞過白名單**。
1. 在白名單套件組合預設中新增`com.day.cq.dam.cq-dam-jcr-connectors`
1. 按一下「儲存」。

![chlimage_1-82](assets/chlimage_1-82a.png)

>[!NOTE]
>
>如果配置了多個工作區，請在「預設工作區名稱」(Default Workspace Name)參數中指定預設工作區的名稱。

有關與身份驗證相關的參數的其他資訊，請參閱[Authentication](/help/sites-administering/sharepoint-connector.md#configuring-authentication)。

### 驗證Sharepoint設定{#verifying-the-sharepoint-setup}

配置連接器後，請驗證以下內容：

* SharePoint伺服器運行，連接器實例可以訪問Web服務
* SharePoint用戶憑據有效，並且用戶具有必要的SharePoint權限
* 已正確安裝並配置連接器

### 配置與SharePoint伺服器{#configuring-dam-sync-with-the-sharepoint-server}的DAM同步

要將SharePoint Assets與AEM同步，請執行以下步驟：

1. 導覽至OSGi管理控制台：[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)。
1. 搜索「Default DAMAssetSynchronization」服務。
1. 編輯設定值。
1. 設定在SharePoint站點上具有訪問權限的用戶的用戶名和相應的密碼。
1. 按一下「儲存」。

啟用DAM同步服務，預設會停用：

1. 導覽至OSGi Web主控台元件：[http://localhost:4502/system/console/components](http://localhost:4502/system/console/components)
1. 搜尋「com.day.cq.dam.jcrconnectors.impl.AssetSynchronizationService」。
1. 按一下「啟用」。

您可以根據需要配置不同同步週期之間的同步延遲：

1. 導覽至OSGi管理控制台：[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
1. 搜尋「DAY CQ DAM JCR連接器資產同步服務」。
1. 編輯設定值。
1. 設定同步週期的值（以秒為單位）。
1. 按一下「儲存」。

### 配置身份驗證{#configuring-authentication}

Sharepoint包括基於傳統和聲明的身份驗證方法，這兩種方法均支援以下身份驗證類型：

* 基本
* Forms

尤其是，下列驗證類型可供使用：

* Classic-Basic
* 傳統型Forms
* 基本索賠
* 基於索賠的Forms

AEM JCR Connector for Microsoft SharePoint 2010和Microsoft SharePoint 2013 4.0版。支援基於聲明的身份驗證（由Microsoft建議），它以下列模式運行：

* **基本/NTLM身份驗證**:連接器會先嘗試使用基本驗證來連線。如果不可用，則切換為基於NTLM的身份驗證。
* **Forms型驗證**:Sharepoint根據用戶在登錄表單中鍵入的憑據（通常為網頁）來驗證用戶。系統為已驗證的請求發出令牌，該令牌包含用於為後續請求重新建立標識的密鑰。

**設定Forms式驗證**

前往：[http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)

1. 按一下「OSGI ->設定」
1. 搜索「Day JCR Connector for Microsoft Sharepoint」
1. 按一下「編輯配置值」
1. 將「Sharepoint連接工廠」的值設定為「com.day.crx.spi.sharepoint.security.FormsBasedAuthenticationConnectionFactory」
1. 按一下「**儲存**」。

**配置基本身份驗證(Windows)**

1. [停用代號驗證](#disable-token-authentication)。
1. 前往[http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)。
1. 按一下「OSGI >設定」。
1. 搜索&#x200B;**Day JCR Connector for Microsoft Sharepoint**。
1. 按一下 `Edit the configuration values`.
1. 將Sharepoint連接工廠的值設定為`com.day.crx.spi.sharepoint.security.WindowsAuthenticationConnectionFactory`。
1. 按一下「**儲存**」。

只有在AEM和SharePoint上通過驗證的用戶才能通過連接器訪問SharePoint內容。

您也可以使用驗證的連接器擴充功能來建立自訂驗證模組，例如，將AEM使用者的存取權對應至特定的SharePoint使用者。 建立與SharePoint用戶對應的AEM用戶（用戶名和密碼應匹配），以便能夠查看映射到連接器實例的SharePoint內容。

若要在AEM中建立使用者：

1. 登入http://localhost:9502/with管理員使用者。
1. 按一下「工具」。
1. 按一下「安全性」。
1. 按一下「使用者」。
1. 按一下「**建立用戶**」。
1. 提供使用者ID（在SharePoint上具有存取權的使用者名稱）。
1. 提供對應的密碼。
1. 按一下綠色勾號以建立使用者。

若要在管理群組中新增使用者：

1. 前往「群組管理」。
1. 按一下「a」節點。
1. 按一下「管理員」。
1. 在&#x200B;**Browse**&#x200B;按鈕之前的文本框中鍵入上面建立的用戶ID。
1. 按一下綠色勾號，將使用者新增至管理群組。

### 禁用令牌身份驗證{#disable-token-authentication}

1. 下載並安裝包`basic auth`。 `zip` 從Software Distribution.

1. 關閉快速入門。
1. 開啟檔案&#x200B;*\crx-quickstart\repository\repository.xml*。
1. 查找標籤`<LoginModule class="com.day.crx.core.CRXLoginModule"> ... </LoginModule>.`
1. 將標籤`<param name="disableTokenAuth" value="true"/>`插入在步驟4提及的標籤內。
1. 保存並關閉xml檔案。
1. 重新啟動QuickStart並使用您的憑據登錄。

#### 支援SharePoint伺服器{#supporting-different-authentication-methods-of-the-sharepoint-server}的不同身份驗證方法

在其標準版本中，連接器支援標準IIS **Windows**&#x200B;驗證（基本）和Forms式驗證（基於令牌）。 可通過可擴充機制支援[其他驗證方法](https://technet.microsoft.com/en-us/library/cc262350.aspx#section2)。

以下步驟提供了擴展標準身份驗證以支援SharePoint伺服器的各種身份驗證方法的相關指南：

1. 實作`com.day.crx.spi.sharepoint.security.SharepointConnectionFactory`以處理特定驗證程式的用戶端。
1. 將`SharepointConnectionFactory`實作安裝為片段主機`com.day.crx.spi.crx2sharepoint-bundle`的片段套件組合。

   使用Maven時，請根據專案的需求調整下列`maven-bundle-plugin`組態：

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
