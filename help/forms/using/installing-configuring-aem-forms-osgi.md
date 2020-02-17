---
title: 安裝和配置資料捕獲功能
seo-title: 安裝和配置資料捕獲功能
description: 安裝和設定最適化表單、PDF表單和HTML5表單。 設定Adobe Analytics和Adobe Target以調整表單，以根據使用者的個人檔案分析表單的使用情況並鎖定使用者。
seo-description: 安裝和設定最適化表單、PDF表單和HTML5表單。 設定Adobe Analytics和Adobe Target以調整表單，以根據使用者的個人檔案分析表單的使用情況並鎖定使用者。
uuid: 5d49032a-4dea-4f21-9dad-a7a30c5872ea
topic-tags: installing
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dfc473eb-6091-4f5d-a5a0-789972c513a9
docset: aem65
translation-type: tm+mt
source-git-commit: 5831c173114a5a6f741e0721b55d85a583e52f78

---


# 安裝和配置資料捕獲功能{#install-and-configure-data-capture-capabilities}

## 簡介 {#introduction}

AEM Forms提供一組表單，以從使用者取得資料：最適化表單、HTML5表單和PDF表單。 它還提供工具來列出網頁上所有可用的表單、分析表單的使用情況，並根據用戶的個人檔案來定位用戶。 這些功能已包含在AEM Forms附加套件中。 附加元件套件已部署在AEM的「作者」或「發佈」例項上。

**** 最適化表單：這些表格會根據裝置的螢幕大小改變外觀，而且具有吸引力，而且具互動性。 Adaptive Forms也可以與Adobe Analytics、Adobe Sign和Adobe Target整合。 它可讓您根據使用者的人口結構和其他功能，為使用者提供個人化表單和流程導向的體驗。 您也可以將最適化表單與Adobe Sign整合。

**PDF Forms** 適用於PDF檔案中像素精確的列印和數位資訊擷取。 在數位頭像中，您可以使用Adobe Acrobat或Acrobat Reader填寫這些表格。 您可以將這些表單托管在您的網站上，或使用表單入口網站，在AEM網站上列出這些表單。 您也可以將這些表格以電子郵件附件形式寄送給其他人。 這些表格最適合案頭環境。

**HTML5 Forms** 是PDF Forms的瀏覽器友好版本。 HTML5 Forms適用於不支援PDF外掛程式的環境。 HTML5 Forms可讓您在不支援XFA PDF的行動裝置和案頭瀏覽器上轉換以XFA為基礎的表格。 這些表格最適合平板電腦和案頭環境。

AEM Forms是功能強大的企業級平台，資料擷取（最適化表單、PDF表單和HTML5表單）只是AEM Forms的功能之一。 如需完整的功能清單，請參 [閱「AEM Forms簡介」](/help/forms/using/introduction-aem-forms.md)。

## 部署拓撲 {#deployment-topology}

AEM Forms附加元件套件是部署在AEM上的應用程式。 您至少只需要一個AEM Author和AEM Publish執行個體，即可執行AEM Forms資料擷取功能。 建議使用下列拓撲來執行AEM Forms AEM Forms資料擷取功能。 如需拓撲的詳細資訊，請參 [閱「AEM Forms的架構和部署拓撲」](/help/forms/using/aem-forms-architecture-deployment.md)。

![推薦拓撲](assets/recommended-topology.png)

## 系統需求 {#system-requirements}

在您開始安裝和設定AEM Forms的資料擷取功能之前，請確定：

* 硬體和軟體基礎架構已就緒。 如需支援硬體和軟體的詳細清單，請參閱 [技術需求](/help/sites-deploying/technical-requirements.md)。

* AEM例項的安裝路徑不包含空格。
* AEM例項已啟動並執行。 在AEM術語中，「例項」是在作者或發佈模式下伺服器上執行的AEM復本。 您至少需要兩個 [AEM例項（一個作者和一個發佈）](/help/sites-deploying/deploy.md) ，才能執行AEM Forms資料擷取功能：

   * **作者**:用於建立、上傳和編輯內容以及管理網站的AEM例項。 內容一旦準備好上線，就會複製到發佈實例。
   * **發佈**:透過網際網路或內部網路為大眾提供已發佈內容的AEM例項。

* 符合記憶體需求。 AEM Forms附加元件套件需要：

   * 15 GB的臨時空間，用於基於Microsoft windows的安裝。
   * 6 GB的臨時空間，用於基於UNIX的安裝。

* 為作者和發佈實例設定複製和反向複製。 有關詳細資訊，請參 [閱複製](/help/sites-deploying/replication.md)。
* 對於基於UNIX的系統：

   * 從安裝介質安裝以下32位軟體包：

<table>
 <tbody>
  <tr>
   <td>expat</td>
   <td>fontconfig</td>
   <td>freetype</td>
   <td>glibc</td>
  </tr>
  <tr>
   <td>libcurl</td>
   <td>libICE</td>
   <td>libicu</td>
   <td>libSM</td>
  </tr>
  <tr>
   <td>libuuid</td>
   <td>libX11</td>
   <td><p>libXau</p> </td>
   <td>libxcb</td>
  </tr>
  <tr>
   <td>libXext</td>
   <td>libXinerama</td>
   <td>libXrandr</td>
   <td>libXrender</td>
  </tr>
  <tr>
   <td>nss-softokn-freebl</td>
   <td>OpenSSL</td>
   <td>zlib</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* 如果伺服器上已安裝OpenSSL，請將它升級至最新版本。
>* 分別建立指向libcurl、libcrypto.so和libssl.so庫最新版本的libcurl.so、libcrypto.so和libssl.so符號連結。
>



* 從安裝媒體安裝下列64位元套件：

   * libicu

## 安裝AEM Forms附加元件套件 {#install-aem-forms-add-on-package}

AEM Forms附加元件套件是部署在AEM上的應用程式。 套件包含AEM Forms資料擷取和其他功能。 執行下列步驟以安裝附加元件套件：

1. 以管理員身分登入 [AEM伺服器](https://localhost:4502) ，並開啟套 [件共用](https://localhost:4502/crx/packageshare)。 您需要Adobe ID才能登入套件共用。
1. 在 [AEM套件共用中](https://localhost:4502/crx/packageshare/login.html)，搜尋 **AEM 6.5 Forms附加元件套件**，按一下適用於您作業系統的套件，然後按一下「 **下載」**。 閱讀並接受授權合約，然後按一下「 **確定**」。 下載開始。 下載後，「已下 **載** 」一詞會出現在套件旁。

   您也可以使用版本號碼來搜尋附加元件套件。 如需最新套件的版本號碼，請參閱 [AEM Forms發行文章](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 。

1. 下載完成後，按一下「已 **下載**」。 您被重定向到包管理器。 在包管理器中，搜索下載的包，然後按一下安 **裝**。

   如果您透過 [AEM Forms發行文章中所列的直接連結手動下載套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) ，請登入套件管理員，按一下「 **Upload Package**」（上傳套件），選取已下載的套件，然後按一下「upload」（上傳）。 上載包後，按一下包名稱，然後按一下安 **裝。**

1. 安裝套件後，系統會提示您重新啟動AEM例項。 **不要立即重新啟動伺服器。** 在停止AEM Forms伺服器之前，請等到ServiceEvent REGISTERED和ServiceEvent UNREGISTERED訊息停止出現在檔案中，而 `[AEM-Installation-Directory]/crx-quickstart/logs/error.log` 且記錄檔是穩定的。
1. 對所有「作者」和「發佈」例項重複步驟1-4。

## 安裝後配置 {#post-installation-configurations}

AEM Forms有一些必備和選用的設定。 必備配置包括配置BuncyCastle庫和序列化代理。 選用的組態包括設定Dispatcher、Forms入口網站、Adobe Sign、Adobe Analytics和Adobe Target。

### 強制安裝後配置 {#mandatory-post-installation-configurations}

#### 配置RSA和BuncyCastle庫 {#configure-rsa-and-bouncycastle-libraries}

對所有「作者」(Author)和「發佈」(Publish)實例執行以下步驟以引導委派庫：

1. 停止基礎AEM例項。
1. 開啟 [AEM安裝目錄]\crx-quickstart\conf\sling.properties檔案以進行編輯。

   如果您使 [用AEM安裝目錄]\crx-quickstart\bin\start.bat來啟動AEM，請編輯位於 [AEM_root]\crx-quickstart\的sling.properties。

1. 將下列屬性新增至sling.properties檔案：

   ```
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. 儲存並關閉檔案，然後啟動AEM例項。
1. 對所有「作者」和「發佈」例項重複步驟1-4。

#### 設定序列化代理 {#configure-the-serialization-agent}

對所有「作者」和「發佈」實例執行以下步驟，以將軟體包列入白名單：

1. 在瀏覽器視窗中開啟AEM Configuration Manager。 預設URL為 `https://[server]:[port]/system/console/configMgr`。
1. 搜尋 **com.adobe.cq.deserfw.impl.DeserializationFirewallImpl.name** ，並開啟設定。
1. 將 **sun.util.calendar** 包添加到白 **名單欄位** 。 按一下&#x200B;**「儲存」**。
1. 對所有「作者」和「發佈」例項重複步驟1-3。

### 可選安裝後配置 {#optional-post-installation-configurations}

#### 配置Dispatcher {#configure-dispatcher}

Dispatcher是AEM的快取和負載平衡工具。 AEM Dispatcher也可協助保護AEM伺服器不受攻擊。 您可搭配使用Dispatcher與企業級Web伺服器，以提高AEM例項的安全性。 如果您使 [用Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)，請針對AEM Forms執行下列設定：

1. 設定AEM Forms的存取權：

   開啟dispatcher.any檔案以進行編輯。 導覽至篩選區段，並將下列篩選新增至篩選區段：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   儲存並關閉檔案。 有關篩選器的詳細資訊，請參 [閱Dispatcher文檔](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)。

1. 設定反向連結篩選服務：

   以管理員身分登入Apache Felix組態管理員。 配置管理器的預設URL是https://[server]:[port_number]/system/console/configMgr。 在**Configurations **功能表中，選取 **Apache Sling Referrer Filter** （Apache Sling反向連結篩選）選項。 在「允許主機」欄位中，輸入調度程式的主機名以允許它作為反向連接，然後按一下「保 **存」**。 條目的格式為https://[server]:[port]。

#### 配置快取 {#configure-cache}

快取是一種機制，可縮短資料存取時間、減少延遲，並改善輸入／輸出(I/O)速度。 最適化表單快取只儲存最適化表單的HTML內容和JSON結構，而不儲存任何預先填入的資料。 它有助於縮短轉換最適化表單所需的時間。

* 在使用最適化表單快取時，請使用 [AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) ，快取最適化表單的用戶端程式庫（CSS和JavaScript）。
* 在開發自訂元件時，請在用於開發的伺服器上停用最適化表單快取。

執行以下步驟以配置自適應表單快取：

1. 前往https:// Server:[port]/system[]/console/configMgr的AEM web主控台組態管理器。
1. 按一 **下「最適化表單與互動式通訊Web頻道設定」** ，以編輯其設定值。 在「編輯設定值」對話方塊中，在「最適化表單數」欄位中指定AEM Forms伺服器執行個體可快取的表 **單或檔案數上限** 。 預設值為100。 按一下&#x200B;**「儲存」**。

   >[!NOTE]
   >
   >要禁用快取，請將「最適化表單數」欄位中的值設定為 **0**。 當禁用或更改快取配置時，將重置快取，並從快取中刪除所有表單和文檔。

#### 為表單資料模型配置SSL通信 {#configure-ssl-communcation-for-form-data-model}

您可以為表單資料模型啟用SSL通訊。 若要啟用表單資料模型的SSL通訊，請在啟動任何AEM Forms例項之前，將憑證新增至所有例項的Java信任存放區。 您可以執行以下命令來添加證書：&quot;

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

#### 設定Adobe Sign {#configure-adobe-sign}

Adobe Sign可針對最適化表單啟用電子簽名工作流程。 電子簽名可改善處理法律、銷售、薪資、人力資源管理等領域檔案的工作流程。

在典型的Adobe sign和最適化表單案例中，使用者會填入最適化表單以 **申請服務**。 例如，信用卡申請和公民福利表。 當使用者填寫、提交及簽署申請表格時，表格會傳送給服務提供者，以做進一步的動作。 服務供應商會審核應用程式，並使用Adobe Sign來標示已核准的應用程式。 若要啟用類似的電子簽名工作流程，您可以將Adobe Sign與AEM Forms整合。

若要搭配使用Adobe Sign和AEM Forms，請 [將Adobe Sign與AEM Forms整合](/help/forms/using/adobe-sign-integration-adaptive-forms.md)。

#### 設定Adobe Analytics {#configure-adobe-analytics}

AEM Forms與Adobe Analytics整合，可讓您擷取並追蹤已發佈表單和檔案的效能量度。 分析這些量度的目的，是根據使表單或檔案更有用所需變更的資料，做出明智的決策。

若要搭配AEM Forms使用Adobe Analytics，請參閱「 [設定分析與報表」](/help/forms/using/configure-analytics-forms-documents.md)。

#### 整合Adobe Target {#integrate-adobe-target}

如果您的客戶提供的體驗並不吸引人，他們可能會放棄表單。 雖然這令客戶感到挫折，但也可以提升組織的支援數量和成本。 識別並提供合適的客戶體驗以提高轉化率，既重要，也極具挑戰性。 AEM表格是此問題的關鍵。

AEM表單與Adobe Marketing cloud解決方案Adobe Target整合，跨多個數位通道提供個人化且吸引人的客戶體驗。 若要使用Adobe Target來A/B測試調適性表單，請 [將Adobe Target與AEM Forms整合](/help/forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms)。

## 後續步驟 {#next-steps}

您已設定環境以使用AEM Forms資料擷取功能。 現在，使用此功能的後續步驟是：

* [建立您的第一個最適化表單](/help/forms/using/create-your-first-adaptive-form.md)
* [建立您的第一個PDF表格](http://www.adobe.com/go/learn_aemforms_designer_quick_start_65)
* [HTML5 Forms簡介](/help/forms/using/introduction.md)

