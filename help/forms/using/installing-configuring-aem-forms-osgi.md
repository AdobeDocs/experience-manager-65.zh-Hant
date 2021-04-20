---
title: 安裝和配置資料捕獲功能
seo-title: 安裝和配置資料捕獲功能
description: 安裝和設定最適化表單、PDF forms和HTML5Forms。 設定Adobe Analytics和Adobe Target的最適化表單，以分析表單的使用情形，並根據使用者的設定檔來定位使用者。
seo-description: 安裝和設定最適化表單、PDF forms和HTML5Forms。 設定Adobe Analytics和Adobe Target的最適化表單，以分析表單的使用情形，並根據使用者的設定檔來定位使用者。
uuid: 5d49032a-4dea-4f21-9dad-a7a30c5872ea
topic-tags: installing
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dfc473eb-6091-4f5d-a5a0-789972c513a9
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1911'
ht-degree: 3%

---


# 安裝和配置資料捕獲功能{#install-and-configure-data-capture-capabilities}

## 簡介 {#introduction}

AEM Forms提供一組表單，以從最終用戶獲取資料：最適化表單、HTML5Forms和PDF forms。 它還提供工具來列出網頁上所有可用的表單、分析表單的使用情況，並根據用戶的個人檔案來定位用戶。 這些功能已包含在AEM Forms附加套件中。 附加元件套件會部署在的「作者」或「發佈」例項AEM上。

**最適化表** 單：這些表單會根據裝置的螢幕大小改變外觀，而且具有吸引力，而且具互動性。適應性Forms也可以與Adobe Analytics、Adobe Sign和Adobe Target整合。 它可讓您根據使用者的人口結構和其他功能，為使用者提供個人化表單和流程導向的體驗。 您也可以將調適性表單與Adobe Sign整合。

**PDF表** 格適合在PDF檔案中列印精確像素及擷取數位資訊。在數位化身中，您可以使用Adobe Acrobat或Acrobat Reader填寫這些表格。 您可以將這些表單托管在您的網站上，或使用表單入口網站將這些表單列在網AEM站上。 您也可以將這些表格以電子郵件附件形式寄送給其他人。 這些表格最適合案頭環境。

**HTML5表** 格是適用於瀏覽器的PDF forms。HTML5Forms適用於不支援PDF外掛程式的環境。 HTML5Forms可讓行動裝置和案頭瀏覽器上轉換不支援XFA PDF的XFA表單。 這些表格最適合平板電腦和案頭環境。

AEM Forms是強大的企業級平台，資料擷取(調適性表單、PDF forms和HTML5Forms)只是AEM Forms的功能之一。 有關功能的完整清單，請參見[AEM Forms簡介](/help/forms/using/introduction-aem-forms.md)。

## 部署拓撲{#deployment-topology}

AEM Forms附加套件是部署在上的應用程AEM式。 您至少只需要一個AEM作者和AEM Publish執行個體，即可執行AEM Forms資料擷取功能。 建議使用以下拓撲來運行AEM FormsAEM Forms資料捕獲功能。 有關拓撲的詳細資訊，請參見[AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md)的體系結構和部署拓撲。

![推薦拓撲](assets/recommended-topology.png)

## 系統要求{#system-requirements}

在開始安裝和配置AEM Forms的資料捕獲功能之前，請確保：

* 硬體和軟體基礎架構已就緒。 有關支援的硬體和軟體的詳細清單，請參見[技術要求](/help/sites-deploying/technical-requirements.md)。

* 實例的安AEM裝路徑不包含空格。
* 實AEM例已啟動並運行。 對於Windows用戶，請以提升模AEM式安裝實例。 在術AEM語中，「例項」是在作者或發AEM布模式下在伺服器上執行的副本。 您至少需要兩個[例項AEM（一個作者和一個發佈）](/help/sites-deploying/deploy.md)來執行AEM Forms資料捕獲功能：

   * **作者**:用於AEM建立、上傳和編輯內容以及管理網站的例項。內容一旦準備好上線，就會複製到發佈實例。
   * **發佈**:透過AEM網際網路或內部網路為公眾提供發佈內容的例項。

* 符合記憶體需求。 AEM Forms附加套件需要：

   * 15 GB的臨時空間，用於基於Microsoft Windows的安裝。
   * 6 GB的臨時空間，用於基於UNIX的安裝。

* 為作者和發佈實例設定複製和反向複製。 有關詳細資訊，請參見[Replication](/help/sites-deploying/replication.md)。
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

## 安裝AEM Forms附加軟體包{#install-aem-forms-add-on-package}

AEM Forms附加套件是部署在上的應用程AEM式。 此套件包含AEM Forms資料擷取和其他功能。 執行下列步驟以安裝附加元件套件：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 點一下頁首功能表中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在&#x200B;**[!UICONTROL Filters]**&#x200B;區段中：
   1. 從&#x200B;**[!UICONTROL Solution]**&#x200B;下拉式清單中選擇&#x200B;**[!UICONTROL Forms]**。
   2. 選擇包的版本和類型。 您也可以使用&#x200B;**[!UICONTROL 搜尋下載]**&#x200B;選項來篩選結果。
1. 點選適用於您作業系統的套件名稱，選取「**[!UICONTROL 接受EULA條款]**」，然後點選「**[!UICONTROL 下載]**」。
1. 開啟[套件管理器](https://docs.adobe.com/content/help/zh-Hant/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。
1. 選擇軟體包並按一下&#x200B;**[!UICONTROL Install]**。

   您也可以透過[AEM Forms版本](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)文章中所列的直接連結下載套件。
1. 安裝軟體包後，系統會提示您重新啟動AEM實例。 **不要立即重新啟動伺服器。** 在停止AEM Forms伺服器之前，請等待ServiceEvent REGISTERED和ServiceEvent UNREGISTERED消息停止顯示在文 `[AEM-Installation-Directory]/crx-quickstart/logs/error.log` 件中，並且日誌穩定。
1. 對所有「作者」和「發佈」例項重複步驟1-7。

### （僅限Windows）自動安裝Visual Studio可轉發套件{#automatic-installation-visual-studio-redistributables}

如果以提升模AEM式安裝實例，則在安裝AEM Forms附加軟體包期間會自動安裝缺少的Visual Studio可轉發套件。

要評估是否自動安裝了Visual Studio可轉發套件，請開啟`/crx-repository/logs/`目錄下的`error.log`檔案。 日誌包含以下消息：

`Redist <service name> already installed on system, will not attempt re-installation`

如果無法安裝可轉發套件，記錄檔會包含下列訊息：

`Current user does not have elevated privileges, aborting installation of redist <service name>`

要解決此問題，請重新啟AEM動伺服器，以提AEM升模式安裝，然後安裝AEM Forms附加軟體包。

如果權限檢查失敗，日誌將包含以下消息：

`Privilege escalation check failed with error: <error message>`

## 安裝後配置{#post-installation-configurations}

AEM Forms有一些強制性和可選配置。 必備配置包括配置BuncyCastle庫和序列化代理。 可選配置包括配置調度程式、Forms門戶、Adobe Sign、Adobe Analytics和Adobe Target。

### 強制安裝後配置{#mandatory-post-installation-configurations}

#### 配置RSA和BuncyCastle庫{#configure-rsa-and-bouncycastle-libraries}

對所有「作者」(Author)和「發佈」(Publish)實例執行以下步驟以引導委派庫：

1. 停止基礎實AEM例。
1. 開啟`[AEM installation directory]\crx-quickstart\conf\sling.properties`檔案進行編輯。

   如果您使用`[AEM installation directory]\crx-quickstart\bin\start.bat`來啟動，AEM則請編輯位於`[AEM_root]\crx-quickstart\`的sling.properties。

1. 將下列屬性新增至sling.properties檔案：

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. 儲存並關閉檔案，然後啟AEM動執行個體。
1. 對所有「作者」和「發佈」例項重複步驟1-4。

#### 配置序列化代理{#configure-the-serialization-agent}

對所有「作者」(Author)和「發佈」(Publish)實例執行以下步驟，將包添加到allowlist:

1. 在瀏AEM覽器視窗中開啟「設定管理員」。 預設URL為`https://'[server]:[port]'/system/console/configMgr`。
1. 搜尋&#x200B;**com.adobe.cq.deserfw.impl.DeserializationFirewallImpl.name**&#x200B;並開啟設定。
1. 將&#x200B;**sun.util.calendar**&#x200B;軟體包添加到&#x200B;**allowlist**&#x200B;欄位。 按一下「**儲存**」。
1. 對所有「作者」和「發佈」例項重複步驟1-3。

### 可選安裝後配置{#optional-post-installation-configurations}

#### 配置Dispatcher {#configure-dispatcher}

Dispatcher是Adobe Experience Manager的快取和／或負載平衡工具，可與企業級Web伺服器一起使用。 如果使用[Dispatcher](https://helpx.adobe.com/tw/experience-manager/dispatcher/using/dispatcher-configuration.html)，則對AEM Forms執行以下配置：

1. 配置AEM Forms的訪問：

   開啟dispatcher.any檔案以進行編輯。 導覽至篩選區段，並將下列篩選新增至篩選區段：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   儲存並關閉檔案。 有關篩選器的詳細資訊，請參見[Dispatcher documentation](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)。

1. 設定反向連結篩選服務：

   以管理員身分登入Apache Felix組態管理員。 配置管理器的預設URL為`https://[server]:[port_number]/system/console/configMgr`。 在&#x200B;**Configurations**&#x200B;選單中，選取&#x200B;**Apache Sling Referrer Filter**&#x200B;選項。 在「允許主機」欄位中，輸入調度程式的主機名以允許它作為反向連接，然後按一下「保存」。 ****&#x200B;條目的格式為「https://[server]:[port]」。

#### 配置快取{#configure-cache}

快取是一種機制，可縮短資料存取時間、減少延遲，並改善輸入／輸出(I/O)速度。 最適化表單快取只儲存最適化表單的HTML內容和JSON結構，而不儲存任何預先填入的資料。 它有助於縮短轉換最適化表單所需的時間。

* 在使用最適化表單快取時，請使用AEM[ Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)來快取最適化表單的用戶端程式庫（CSS和JavaScript）。
* 在開發自訂元件時，請在用於開發的伺服器上停用最適化表單快取。

執行以下步驟以配置自適應表單快取：

1. 轉至AEMWeb控制台配置管理器，網址為https://&#39;[server]:[port]&#39;/system/console/configMgr。
1. 按一下&#x200B;**自適應表單和互動式通信Web通道配置**&#x200B;以編輯其配置值。 在編輯配置值對話框中，在&#x200B;**Number of AdaptiveForms**&#x200B;欄位中指定AEM Forms伺服器實例可以快取的表單或文檔的最大數量。 預設值為 100。按一下「**儲存**」。

   >[!NOTE]
   >
   >要禁用快取，請將「Number of AdaptiveForms」（自適應性資料）欄位中的值設定為&#x200B;**0**。 當禁用或更改快取配置時，將重置快取，並從快取中刪除所有表單和文檔。

#### 為表單資料模型{#configure-ssl-communcation-for-form-data-model}配置SSL通信

您可以為表單資料模型啟用SSL通訊。 若要啟用表單資料模型的SSL通訊，在啟動任何AEM Forms例項之前，請將憑證新增至所有例項的Java信任存放區。 您可以執行以下命令來添加證書：&quot;

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

#### 配置Adobe Sign{#configure-adobe-sign}

Adobe Sign為調適性表單提供電子簽名工作流程。 電子簽名可改善處理法律、銷售、薪資、人力資源管理等領域檔案的工作流程。

在典型的Adobe Sign和適應性表單場景中，用戶填充適應於&#x200B;**服務**&#x200B;的自適應表單。 例如，信用卡申請和公民福利表。 當使用者填寫、提交及簽署申請表格時，表格會傳送給服務提供者，以做進一步的動作。 服務提供商會審查應用程式，並使用Adobe Sign標籤批准的應用程式。 若要啟用類似的電子簽名工作流程，您可以將Adobe Sign與AEM Forms整合。

要將Adobe Sign與AEM Forms結合，[將Adobe Sign與AEM Forms整合。](/help/forms/using/adobe-sign-integration-adaptive-forms.md)

#### 配置Adobe Analytics{#configure-adobe-analytics}

AEM Forms與Adobe Analytics整合，可讓您擷取並追蹤已發佈表單和檔案的效能量度。 分析這些量度的目的，是根據使表單或檔案更有用所需變更的資料，做出明智的決策。

若要搭配使用Adobe Analytics與AEM Forms，請參閱[設定分析和報表](/help/forms/using/configure-analytics-forms-documents.md)。

#### 整合Adobe Target{#integrate-adobe-target}

如果您的客戶提供的體驗並不吸引人，他們可能會放棄表單。 雖然這令客戶感到挫折，但也可以提升組織的支援數量和成本。 識別並提供合適的客戶體驗以提高轉化率，既重要，也極具挑戰性。 表AEM單是問題的關鍵。

表AEM單與Adobe Marketing Cloud解決方案Adobe Target整合，跨多個數位通道提供個人化且吸引人的客戶體驗。 要使用Adobe Target對A/B測試適應性表單，[將Adobe Target與AEM Forms整合。](/help/forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms)

## 後續步驟{#next-steps}

您已配置環境以使用AEM Forms資料捕獲功能。 現在，使用此功能的後續步驟是：

* [建立您的第一個最適化表單](/help/forms/using/create-your-first-adaptive-form.md)
* [建立您的第一個PDF表格](http://www.adobe.com/go/learn_aemforms_designer_quick_start_65)
* [HTML5簡介Forms](/help/forms/using/introduction.md)

