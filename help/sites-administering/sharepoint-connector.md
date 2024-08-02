---
title: SharePoint聯結器
description: 適用於Microsoft SharePoint 2010和Microsoft SharePoint 2013的Day JCR Connector 4.0版。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 10ea7d2e-6e44-4d5c-a2b2-63c73b18f172
feature: Integration
role: Admin
source-git-commit: c4133584e9c2328b3a55042902c67770d78afcf7
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 1%

---

# SharePoint聯結器{#sharepoint-connector}

本文包含有關Microsoft SharePoint 2010和Microsoft SharePoint 2013,4.0版的JCR ConnectorAdobe的詳細資訊。

SharePoint聯結器支援下列基本功能：

* 從SharePoint讀取內容和中繼資料。
* 套用原生SharePoint驗證和授權，認可已存取內容的SharePoint安全性設定
* 使用內容尋找器整合內容
* 使用AEM元件（例如外部資源）來顯示SharePoint影像和影片
* 同步SharePoint與AEM Assets

所有功能都是使用原生SharePoint Web服務當作SharePoint內容和服務的介面來實作。

>[!NOTE]
>
>AEM 6.1 Service Pack 2也支援SharePoint聯結器。 聯結器不再支援虛擬存放庫掛載，因此無法掛載。 如果您想使用Java API存取Sharepoint存放庫，請在專案中使用Sharepoint聯結器的JCR存放庫實作。
>
>SharePoint伺服器和相關IT基礎結構的安裝、設定、管理和IT作業不在本檔案的涵蓋範圍內。 如需這些主題的資訊，請參閱[SharePoint](https://www.microsoft.com/sharepoint)上的廠商檔案。 聯結器需要正確安裝、設定和操作基礎結構的這些部分。
>

## 快速入門 {#getting-started}

若要開始使用聯結器，請執行下列動作：

* 確保您至少已安裝Java 7。
* 從Software Distribution下載聯結器套件散發檔案。
* 將有效的&#x200B;*license.properties*&#x200B;檔案複製到包含&#x200B;*cq-quickstart-6.4.0.jar*&#x200B;檔案的目錄。

* 連按兩下.jar檔案以啟動AEM，或從命令列啟動它。
* 從「封裝管理員」安裝聯結器封裝。
* 設定聯結器選項。

## 安裝SharePoint聯結器 {#installing-sharepoint-connector}

聯結器是一種內容封裝，可方便安裝。 使用封裝管理員安裝套件，然後設定SharePoint伺服器URL
和其他設定選項。 AEM存放庫中提供SharePoint內容。

### 安裝需求 {#installation-requirements}

聯結器需要下列專案：

* Java Runtime Environment 1.7或更新版本
* 可透過網路取得的SharePoint Web服務
* SharePoint伺服器URL
* CRX和SharePoint存放庫的使用者認證和許可權
* [支援平台](#supported-platforms)

SharePoint聯結器可從[軟體發佈](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-17673)下載。

### 支援平台 {#supported-platforms}

聯結器支援下列專案：

* AEM版本：

   * AEM 6.4、6.3

* Microsoft SharePoint版本：

   * Microsoft Office SharePoint Server (MOSS) 2010
   * Microsoft Office SharePoint Server (MOSS) 2013

* 如果您需要聯結器的自訂部署支援（OEM、特殊需求、自訂驗證方法），請連絡您所在地區的Adobe辦事處。

>[!NOTE]
>
>聯結器僅支援Microsoft正式支援的設定。 請參閱[MOSS 2010](https://technet.microsoft.com/en-us/library/cc262485(office.14).aspx)和[MOSS 2013](https://technet.microsoft.com/en-us/library/cc262485.aspx)系統需求。

### 標準安裝 {#standard-installation}

Software Distribution用於發佈產品功能、範例和Hot Fix。 如需詳細資訊，請參閱[軟體發佈檔案](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html#software-distribution)。


#### 與AEM整合 {#integrating-with-aem}

安裝聯結器內容封裝。

1. 開啟Adobe支援票證以請求聯結器功能套件。
1. 下載可用套件，然後開啟您AEM執行個體的套件管理器。
1. 從封裝說明頁面按一下&#x200B;**安裝**。
1. 在&#x200B;**安裝封裝**&#x200B;對話方塊中，按一下&#x200B;**安裝**。

   **注意**：請確定您是以管理員身分登入。

1. 安裝套件時，按一下&#x200B;**關閉**。

## 設定SharePoint聯結器 {#configuring-sharepoint-connector}

安裝SharePoint聯結器後，請設定聯結器的應用程式和SharePoint層。

設定SharePoint伺服器URL，使您的SharePoint存放庫符合JCR規範。 您可以設定額外的引數，以設定與SharePoint伺服器的連線。 此外，還可使用SharePoint聯結器設定驗證。

### 設定與SharePoint伺服器的連線 {#configuring-the-connection-with-the-sharepoint-server}

若要設定SharePoint伺服器的URL和進階選項，請執行下列步驟：

1. 導覽至OSGi管理主控台： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)。
1. 搜尋Microsoft Sharepoint **套件組合的**&#x200B;天JCR聯結器。
1. 編輯設定值。
1. 將SharePoint伺服器URL設定為&#x200B;**工作區**&#x200B;的值。
1. 按一下「**儲存**」。

![chlimage_1-62](assets/chlimage_1-62.png)

「工作區」和「預設Workspace名稱」引數：

依預設，聯結器會顯示單一JCR工作區。 此工作區公開的SharePoint伺服器是透過&#39;Sharepoint Server URL&#39;設定引數設定。

聯結器亦可針對多個工作區進行設定。 在此案例中，每個工作區都與透過工作區公開之個別SharePoint伺服器的URL相關聯。 若要新增工作區，請在「工作區」引數中新增工作區定義。 工作區定義的格式如下：
`<name>`= `<url>`，其中
`<name>`是JCR工作區的名稱和
`<url>`是該工作區之SharePoint伺服器的URL。

在AEM中，除了上述設定步驟外，另外執行一個步驟。 允許列出&#39;**com.day.cq.dam.cq-dam-jcr-connectors**&#39;組合。

若要允許AEM中的清單組合，請執行以下步驟：

1. 導覽至OSGi管理主控台： http://localhost:4502/system/console/configMgr。
1. 搜尋「Apache Sling登入管理員白名單」服務。
1. 選取&#x200B;**略過白名單**。
1. 在白名單套裝預設值中新增`com.day.cq.dam.cq-dam-jcr-connectors`
1. 按一下「儲存」。

![chlimage_1-82](assets/chlimage_1-82a.png)

>[!NOTE]
>
>如果您設定多個工作區，請在「預設Workspace名稱」引數中指定預設工作區的名稱。

如需有關驗證相關引數的詳細資訊，請參閱[驗證](/help/sites-administering/sharepoint-connector.md#configuring-authentication)。

### 驗證Sharepoint設定 {#verifying-the-sharepoint-setup}

設定聯結器後，請確認下列事項：

* SharePoint伺服器會執行，而聯結器執行個體可以存取web服務
* SharePoint使用者認證有效，且使用者擁有必要的SharePoint許可權
* 聯結器已安裝並正確設定

### 設定與SharePoint伺服器的DAM同步 {#configuring-dam-sync-with-the-sharepoint-server}

若要將SharePoint Assets與AEM同步，請執行以下步驟：

1. 導覽至OSGi管理主控台： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)。
1. 搜尋「預設DAMAsetSynchronization」服務。
1. 編輯設定值。
1. 設定在SharePoint網站上擁有存取許可權的使用者的使用者名稱和對應密碼。
1. 按一下「儲存」。

啟用DAM同步服務，此服務預設為停用：

1. 導覽至OSGi Web主控台元件： [http://localhost:4502/system/console/components](http://localhost:4502/system/console/components)
1. 搜尋「com.day.cq.dam.jcrconnectors.impl.AssetSynchronizationService」。
1. 按一下「啟用」。

或者，您可以設定不同同步化週期之間的同步化延遲：

1. 導覽至OSGi管理主控台： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
1. 搜尋「DAY CQ DAM JCR Connector Asset Synchronization Service」。
1. 編輯設定值。
1. 設定同步化期間的值（以秒為單位）。
1. 按一下「儲存」。

### 設定驗證 {#configuring-authentication}

Sharepoint包括「傳統」和「宣告式」驗證方法，兩者都支援下列驗證型別：

* 基本
* Forms型

特別是，可使用下列型別的驗證：

* 傳統 — 基本
* 基於Classic-Forms
* 索賠 — 基本
* 宣告型Forms

適用於Microsoft SharePoint 2010和Microsoft SharePoint 2013的AEM JCR Connector 4.0版支援宣告型驗證(由Microsoft建議)，其作業模式如下：

* **基本/NTLM驗證**：聯結器會先嘗試使用基本驗證進行連線。 如果無法使用，它會切換至NTLM式驗證。
* **以Forms為基礎的驗證**： Sharepoint會根據使用者在登入表單（通常是網頁）中輸入的認證，來驗證使用者。 系統會為已驗證請求發出權杖，其中包含為後續請求重新建立身分的金鑰。

**設定Forms驗證**

移至： [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)

1. 按一下「OSGI >設定」
1. 搜尋「Microsoft Sharepoint的Day JCR Connector」
1. 按一下「編輯設定值」
1. 將&#39;Sharepoint Connection Factory&#39;的值設為&#39;com.day.crx.spi.sharepoint.security.FormsBasedAuthenticationConnectionFactory&#39;
1. 按一下「**儲存**」。

**設定基本驗證(Windows)**

1. [停用Token驗證](#disable-token-authentication)。
1. 移至[http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)。
1. 按一下「OSGI >設定」 。
1. 搜尋Microsoft Sharepoint **的**&#x200B;天JCR聯結器。
1. 按一下「`Edit the configuration values`」。
1. 將Sharepoint Connection Factory的值設定為`com.day.crx.spi.sharepoint.security.WindowsAuthenticationConnectionFactory`。
1. 按一下「**儲存**」。

只有已在AEM和SharePoint上驗證的使用者才能透過聯結器存取SharePoint內容。

您也可以使用驗證的聯結器擴充功能來建立自訂驗證模組，例如，將AEM使用者的存取權對應至特定SharePoint使用者。 建立與SharePoint使用者（使用者名稱和密碼必須相符）相對應的AEM使用者，以便檢視對應至聯結器執行個體的SharePoint內容。

若要在AEM中建立使用者：

1. 以管理員使用者身分登入http://localhost:9502/with 。
1. 按一下「工具」。
1. 按一下「安全性」。
1. 按一下「使用者」。
1. 按一下&#x200B;**建立使用者**。
1. 提供使用者ID (可存取SharePoint的使用者名稱)。
1. 提供對應的密碼。
1. 按一下綠色勾號符號以建立使用者。

若要在管理員群組中新增使用者：

1. 前往群組管理。
1. 按一下「a」節點。
1. 按一下「管理員」。
1. 在&#x200B;**瀏覽**&#x200B;按鈕前的文字方塊中，輸入上面建立的使用者ID。
1. 按一下綠色勾號符號，將使用者新增至管理員群組。

### 停用權杖驗證 {#disable-token-authentication}

1. 下載並安裝封裝`basic auth`。 來自軟體散發的`zip`。

1. 關閉快速入門。
1. 開啟檔案&#x200B;*\crx-quickstart\repository\repository.xml*。
1. 尋找標籤`<LoginModule class="com.day.crx.core.CRXLoginModule"> ... </LoginModule>.`
1. 將標籤`<param name="disableTokenAuth" value="true"/>`插入步驟4提及的標籤中。
1. 儲存並關閉xml檔案。
1. 重新啟動QuickStart並使用您的憑證登入。

#### 支援SharePoint伺服器的不同驗證方法 {#supporting-different-authentication-methods-of-the-sharepoint-server}

在其標準版本中，聯結器支援標準IIS **Windows**&#x200B;驗證（基本）和Forms式驗證（權杖）。 可透過擴充性機制支援[其他驗證方法](https://technet.microsoft.com/en-us/library/cc262350.aspx#section2)。

下列步驟提供擴充標準驗證的指引，以支援SharePoint伺服器的各種驗證方法：

1. 實作`com.day.crx.spi.sharepoint.security.SharepointConnectionFactory`以處理您特定驗證程式的使用者端。
1. 將`SharepointConnectionFactory`實作安裝為片段主機`com.day.crx.spi.crx2sharepoint-bundle`的片段組合。

   使用Maven時，將`maven-bundle-plugin`的下列設定調整為您的專案需求：

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

1. 在聯結器設定中登入`SharepointConnectionFactory`實作。 在聯結器的設定視窗中，按一下&#x200B;**進階選項**。 在&#x200B;**Sharepoint Connection Factory**&#x200B;的欄位中，指定實作`com.day.crx.spi.sharepoint.auth.CustomConnectionFactory`的名稱。

1. 重新啟動聯結器。
