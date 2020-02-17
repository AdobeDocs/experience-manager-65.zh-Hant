---
title: 安裝和配置互動式通訊
seo-title: 安裝和配置互動式通訊
description: 安裝和設定AEM Forms互動式通訊，以建立商業通訊、檔案、陳述、權益通知、行銷郵件、帳單和歡迎套件。
seo-description: 安裝和設定AEM Forms互動式通訊，以建立商業通訊、檔案、陳述、權益通知、行銷郵件、帳單和歡迎套件。
uuid: 8acb7f68-0b52-4acd-97e2-af31c9408e8d
topic-tags: installing
discoiquuid: 225f2bc1-6842-4c79-a66d-8024a29325c0
docset: aem65
translation-type: tm+mt
source-git-commit: 94472fad34fe97740e4711d2cb35beb884db52ce

---


# 安裝和配置互動式通訊{#install-and-configure-interactive-communications}

## 簡介 {#introduction}

AEM Form可集中建立、匯整、管理和傳送安全且互動式檔案，例如商業通訊、檔案、陳述、權益通知、行銷郵件、帳單和歡迎套件。 此功能稱為互動式通訊。 此功能已包含在AEM Forms附加套件中。 附加元件套件已部署在AEM的「作者」或「發佈」例項上。

您可以使用互動式通訊功能，以多種格式產生通訊。 例如，網頁和PDF。 您可以將互動式通訊與AEM Workflow整合，以處理並透過客戶選擇的通道向客戶傳遞整合式通訊。 例如，透過電子郵件傳送通訊給使用者。

如果您從舊版升級並已投資於通信管理，則可以安裝相容 [性包](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package) ，以繼續使用通信管理。 如需互動式通訊與通訊管理之間差異的詳細資訊，請參閱互動式 [通訊概觀](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management)。

AEM Forms是功能強大的企業級平台。 互動式通訊只是AEM Forms的其中一項功能。 如需完整的功能清單，請參 [閱「AEM Forms簡介」](../../forms/using/introduction-aem-forms.md)。

## 部署拓撲 {#deployment-topology}

AEM Forms附加元件套件是部署在AEM上的應用程式。 您至少只需要一個AEM作者和處理執行個體，就能執行互動式通訊功能。 以下拓撲是指示性拓撲，可針對OSGi功能執行AEM Forms Interactive Communications、Conversence Management、AEM Forms資料擷取和Forms-Centric工作流程。 如需拓撲的詳細資訊，請參 [閱「AEM Forms的架構和部署拓撲」](/help/forms/using/aem-forms-architecture-deployment.md)。

![推薦拓撲](assets/recommended-topology.png)

AEM Forms Interactive Communications會在AEM Forms的「作者」例項上執行管理、編寫和代理使用者介面。 「發佈」執行個體代管最終版本的互動式通訊，可供使用者使用。

## 系統需求 {#system-requirements}

在您開始安裝和設定AEM Forms的互動式通訊和通訊管理功能之前，請確定：

* 硬體和軟體基礎架構已就緒。 如需支援硬體和軟體的詳細清單，請參閱 [技術需求](/help/sites-deploying/technical-requirements.md)。

* AEM例項的安裝路徑不包含空格。
* AEM例項已啟動並執行。 在AEM術語中，「例項」是在作者或發佈模式下伺服器上執行的AEM復本。 您至少需要一個AEM例項（作者或處理）才能執行AEM Forms互動式通訊和通訊管理功能：

   * **作者**:用於建立、上傳和編輯內容以及管理網站的AEM例項。 內容一旦準備好上線，就會複製到發佈實例。
   * **** 處理：處理例項是硬 [化的AEM Author例項](/help/forms/using/hardening-securing-aem-forms-environment.md) 。 您可以設定Author例項，並在執行安裝後加強它。

   * **發佈**:透過網際網路或內部網路為大眾提供已發佈內容的AEM例項。

* 符合記憶體需求。 AEM Forms附加元件套件需要：

   * 15 GB的臨時空間，用於基於Microsoft windows的安裝。
   * 6 GB的臨時空間，用於基於UNIX的安裝。

* 基於UNIX的系統的額外要求：如果您使用基於UNIX的作業系統，請從相應作業系統的安裝介質安裝以下軟體包。

<table>
 <tbody>
  <tr>
   <td>expat</td>
   <td>libxcb</td>
   <td>freetype</td>
   <td>libXau</td>
  </tr>
  <tr>
   <td>libSM</td>
   <td>zlib</td>
   <td>libICE</td>
   <td>libuuid</td>
  </tr>
  <tr>
   <td>glibc</td>
   <td>libXext</td>
   <td><p>nss-softokn-freebl</p> </td>
   <td>fontconfig</td>
  </tr>
  <tr>
   <td>libX11</td>
   <td>libXrender</td>
   <td>libXrandr</td>
   <td>libXinerama</td>
  </tr>
 </tbody>
</table>

## 安裝AEM Forms附加元件套件 {#install-aem-forms-add-on-package}

AEM Forms附加元件套件是部署在AEM上的應用程式。 此套件包含AEM Forms互動式通訊、通訊管理和其他功能。 執行下列步驟以安裝附加元件套件：

1. 以管理員身分登入 [AEM伺服器](https://localhost:4502) ，並開啟套 [件共用](https://localhost:4502/crx/packageshare)。 您需要Adobe ID才能登入套件共用。
1. 在 [AEM套件共用](https://localhost:4502/crx/packageshare/login.html)、搜尋 **AEM 6.5 Forms附加套件或最新** 服務套件中，按一下適用於您作業系統的套件，然後按一 ********&#x200B;下「下載」。 閱讀並接受授權合約，然後按一下「 **確定**」。 下載開始。 下載後，「已下 **載** 」一詞會出現在套件旁。

   您也可以使用版本號碼來搜尋附加元件套件。 如需最新套件的版本號碼，請參閱 [AEM Forms發行文章](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 。

1. 下載完成後，按一下「已 **下載**」。 您被重定向到包管理器。 在包管理器中，搜索下載的包，然後按一下安 **裝**。

   如果您透過 [AEM Forms發行文章中所列的直接連結手動下載套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) ，請登入套件管理員，按一下「 **Upload Package**」（上傳套件），選取已下載的套件，然後按一下「upload」（上傳）。 上載包後，按一下包名稱，然後按一下安 **裝。**

1. 安裝套件後，系統會提示您重新啟動AEM例項。 **不要立即重新啟動伺服器。** 在停止AEM Forms伺服器之前，請等到ServiceEvent REGISTERED和ServiceEvent UNREGISTERED訊息停止出現在 [AEM-Installation-Directory]/crx-quickstart/logs/error.log檔案中，且記錄檔是穩定的。
1. 對所有「作者」和「發佈」例項重複步驟1-4。

## 安裝後配置 {#post-installation-configurations}

AEM Forms有一些必備和選用的設定。 必備配置包括配置BuncyCastle庫和序列化代理。 可選配置包括配置調度程式和Adobe Target。

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

1. 在瀏覽器視窗中開啟AEM Configuration Manager。 預設URL為https://[server]:[port]/system/console/configMgr。
1. 搜尋並開啟還原 **序列化防火牆設定**。
1. 將 **sun.util.calendar** 包添加到白 **名單欄位** 。 按一下「儲存」。
1. 對所有「作者」和「發佈」例項重複步驟1-3。

### 可選安裝後配置 {#optional-post-installation-configurations}

#### 安裝相容性軟體包 {#install-compatibility-package}

在AEM 6.5 Forms中建立客戶通訊的預設和建議方式是互動式通訊。 如果您已升級或從舊版移轉，並計畫繼續使用字母(Correponsement Management)，請安裝 [AEMFD Compatibility套件](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/fd/AEM-FORMS-6.4-COMPAT)。

AEMFD相容性套件可讓您在AEM 6.5表單上使用AEM 6.4 Forms、AEM 6.3 Forms和AEM 6.2 Forms的下列資產：

* 檔案片段
* 字母
* 資料字典
* 不再支援的最適化表單範本和頁面

#### 配置Dispatcher {#configure-dispatcher}

Dispatcher是AEM的快取和負載平衡工具。 AEM Dispatcher也可協助保護AEM伺服器不受攻擊。 您可搭配使用Dispatcher與企業級Web伺服器，以提高AEM例項的安全性。 如果您使 [用Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)，請針對AEM Forms執行下列設定：

1. 設定AEM Forms的存取權：

   開啟dispatcher.any檔案以進行編輯。 導覽至篩選區段，並將下列篩選新增至篩選區段：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   儲存並關閉檔案。 有關篩選器的詳細資訊，請參 [閱Dispatcher文檔](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)。

1. 設定反向連結篩選服務：

   以管理員身分登入Apache Felix組態管理員。 配置管理器的預設URL是https://[server]:[port_number]/system/console/configMgr。 在「設 **定** 」選單中，選取 **Apache Sling Referrer Filter** 選項。 在「允許主機」欄位中，輸入調度程式的主機名以允許它作為反向連接，然後按一下「保 **存」**。 條目的格式為https://[server]:[port]。

#### 整合Adobe Target {#integrate-adobe-target}

如果您的客戶提供的體驗不吸引人，他們可能會放棄互動式通訊。 雖然這令客戶感到挫折，但也可以提升組織的支援數量和成本。 識別並提供適當的客戶體驗以提高轉化率，這既重要，也極具挑戰性。 AEM表格是此問題的關鍵。

AEM表單與Adobe Marketing cloud解決方案Adobe Target整合，跨多個數位通道提供個人化且吸引人的客戶體驗。 若要使用Adobe target個人化互動式通訊，請 [將Adobe Target與AEM Forms整合](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms)。

#### 為表單資料模型配置SSL通信 {#configure-ssl-communcation-for-form-data-model}

您可以為表單資料模型啟用SSL通訊。 若要啟用表單資料模型的SSL通訊，請在啟動任何AEM Forms例項之前，將憑證新增至所有例項的Java信任存放區。 您可以執行以下命令來添加證書：

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## 後續步驟 {#next-steps}

您已設定環境，以使用互動式通訊和通訊管理功能。 現在，使用此功能的步驟如下：

* [通信管理概述](/help/forms/using/interactive-communications-overview.md)

* [建立互動式通訊](../../forms/using/create-interactive-communication.md)

* [建立信件管理函件](../../forms/using/create-letter.md)

