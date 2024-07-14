---
title: 安裝及設定資料擷取功能
description: 安裝並設定最適化表單、PDF forms和HTML5 Forms。 設定最適化表單的Adobe Analytics和Adobe Target ，以分析表單的使用情況，並根據使用者的設定檔鎖定使用者。
topic-tags: installing
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
role: Admin, User, Developer
exl-id: 19b5765e-50bc-4fed-8af5-f6bb464516c8
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on OSGi
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1882'
ht-degree: 4%

---

# 安裝及設定資料擷取功能{#install-and-configure-data-capture-capabilities}

## 簡介 {#introduction}

AEM Forms提供一組表單，用於從一般使用者取得資料：調適型表單、HTML5 Forms和PDF forms。 它也提供工具，列出網頁上所有可用的表單、分析表單的使用情況，以及根據使用者的設定檔鎖定使用者。 這些功能包含在AEM Forms附加元件套件中。 附加元件套件部署在AEM的作者或Publish執行個體上。

**最適化表單：**&#x200B;這些表單會根據裝置的熒幕大小變更外觀、吸引人且本質上為互動式。 最適化Forms也可以整合Adobe Analytics、Adobe Sign和Adobe Target。 它可讓您根據使用者的人口統計和其他功能，提供個人化表單和程式導向的體驗給使用者。 您也可以將最適化表單與Adobe Sign整合。

**PDF forms**&#x200B;適用於PDF檔案中的畫素完美列印與數位資訊擷取。 在數位頭像中，您可以使用Adobe Acrobat或Acrobat Reader來填寫這些表單。 您可以在網站上託管這些表單，或使用表單入口網站在AEM網站上列出這些表單。 您也可以以電子郵件將這些表單作為附件傳送給其他人。 這些表單最適合案頭環境。

**HTML5 Forms**&#x200B;是瀏覽器易用的PDF forms版本。 HTML5 Forms適用於不支援PDF外掛程式的環境。 HTML5 Forms可在不支援XFAPDF的行動裝置和桌上型瀏覽器上，轉譯XFA型表單。 這些表格最適合平板電腦和桌上型電腦環境。

AEM Forms是功能強大的企業級平台，而資料擷取(調適型表單、PDF forms和HTML5 Forms)只是AEM Forms的其中一項功能。 如需完整的功能清單，請參閱[AEM Forms簡介](/help/forms/using/introduction-aem-forms.md)。

## 部署拓撲 {#deployment-topology}

AEM Forms附加元件套件是部署至AEM的應用程式。 您只需要至少一個AEM Author和AEM Publish執行個體，即可執行AEM Forms資料擷取功能。 建議使用下列拓撲來執行AEM Forms AEM Forms資料擷取功能。 如需拓撲的詳細資訊，請參閱[AEM Forms的架構和部署拓撲](/help/forms/using/aem-forms-architecture-deployment.md)。

![建議拓撲](assets/recommended-topology.png)

## 系統需求 {#system-requirements}

開始安裝及設定AEM Forms的資料擷取功能前，請確定：

* 硬體與軟體基礎架構已準備就緒。 如需支援的硬體和軟體詳細清單，請參閱[技術需求](/help/sites-deploying/technical-requirements.md)。

* AEM執行個體的安裝路徑未包含空格。
* AEM執行個體已啟動且執行中。 對於Windows使用者，請在提升許可權的模式下安裝AEM執行個體。 在AEM術語中，「例項」是在伺服器上以製作或發佈模式執行的AEM的副本。 您至少需要兩個[AEM執行個體(一個作者和一個Publish)](/help/sites-deploying/deploy.md)才能執行AEM Forms資料擷取功能：

   * **作者**：用來建立、上傳和編輯內容以及管理網站的AEM執行個體。 一旦內容準備好上線，就會將其復寫到發佈執行個體。
   * **Publish**：透過網際網路或內部網路，向公眾提供已發佈內容的AEM執行個體。

* 符合記憶體需求。 AEM Forms附加元件套件需要：

   * Microsoft Windows安裝專用的15 GB暫存空間。
   * UNIX安裝需要6 GB的暫存空間。

* 已設定作者和發佈執行個體的復寫和反向復寫。 如需詳細資訊，請參閱[復寫](/help/sites-deploying/replication.md)。
* 對於基於UNIX的系統：

   * 從安裝媒體安裝下列32位元套件：

<table>
 <tbody>
  <tr>
   <td>外派人員</td>
   <td>fontconfig</td>
   <td>自由文字</td>
   <td>glibc</td>
  </tr>
  <tr>
   <td>libcurl</td>
   <td>libICE</td>
   <td>利比庫</td>
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
>* 如果伺服器上已安裝OpenSSL，請將其升級至最新版本。
>* 分別建立指向最新版libcurl、libcrypto和libssl程式庫的libcurl.so、libcrypto.so和libssl.so symlink。
>

* 從安裝媒體安裝下列64位元套件：

   * 利比庫

* 安裝[Microsoft Visual Studio 2019 32位元可轉散發套件](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)。


## 安裝AEM Forms附加元件套件 {#install-aem-forms-add-on-package}

AEM Forms附加元件套件是部署至AEM的應用程式。 此套件包含AEM Forms資料擷取和其他功能。 執行以下步驟來安裝附加套件：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 選取標題功能表中可用的&#x200B;**[!UICONTROL Adobe Experience Manager]**。
1. 在&#x200B;**[!UICONTROL 篩選器]**&#x200B;區段中：
   1. 從&#x200B;**[!UICONTROL 解決方案]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Forms]**。
   2. 選取封裝的版本和型別。 您也可以使用&#x200B;**[!UICONTROL 搜尋下載]**&#x200B;選項來篩選結果。
1. 選取適用於您作業系統的封裝名稱，選取&#x200B;**[!UICONTROL 接受EULA條款]**，然後選取&#x200B;**[!UICONTROL 下載]**。
1. 開啟[封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 上傳封裝]**&#x200B;以上傳封裝。
1. 選取封裝並按一下&#x200B;**[!UICONTROL 安裝]**。

   您也可以透過[AEM Forms發行版本](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)文章中列出的直接連結來下載套件。
1. 安裝套件後，系統會提示您重新啟動AEM執行個體。 **不要立即重新啟動伺服器。**&#x200B;在停止AEM Forms伺服器之前，請等候直到ServiceEvent REGISTERED和ServiceEvent UNREGISTERED訊息停止出現在`[AEM-Installation-Directory]/crx-quickstart/logs/error.log`檔案中，而且記錄檔穩定。

   >[!NOTE]
   >
   > 建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK （例如停止Java程式）可能會導致AEM開發環境不一致。

1. 對所有Author和Publish執行個體重複步驟1至7。

### （僅限Windows）自動安裝Visual Studio可轉散發套件 {#automatic-installation-visual-studio-redistributables}

如果您以提升許可權模式安裝AEM執行個體，則在安裝AEM Forms附加元件套件期間，會自動安裝32位元Visual Studio可轉散發套件。

若要評估是否已自動安裝Visual Studio可轉散發套件，請開啟`/crx-repository/logs/`目錄中的`error.log`檔案。 記錄檔包含下列訊息：

`Redist <service name> already installed on system, will not attempt re-installation`

如果無法安裝可轉散發套件，記錄會包含下列訊息：

`Current user does not have elevated privileges, aborting installation of redist <service name>`

若要解決此問題，請重新啟動AEM伺服器，以提升許可權模式安裝AEM，然後安裝AEM Forms附加元件套件。

如果許可權檢查失敗，記錄會包含以下訊息：

`Privilege escalation check failed with error: <error message>`

## Post安裝設定 {#post-installation-configurations}

AEM Forms有一些必要和選用的設定。 強制設定包括設定BouncyCastle程式庫和序列化代理程式。 選擇性設定包括設定Dispatcher、Forms入口網站、Adobe Sign、Adobe Analytics和Adobe Target。

### 強制安裝後設定 {#mandatory-post-installation-configurations}

#### 設定RSA和BouncyCastle資料庫  {#configure-rsa-and-bouncycastle-libraries}

在所有Author和Publish執行個體上執行下列步驟，以啟動委派程式庫：

1. 停止基礎AEM執行個體。
1. 開啟 `[AEM installation directory]\crx-quickstart\conf\sling.properties` 檔案進行編輯。

   如果您使用`[AEM installation directory]\crx-quickstart\bin\start.bat`啟動AEM，請編輯位於`[AEM_root]\crx-quickstart\`的sling.properties。

1. 將以下屬性新增到sling.properties檔案：

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. 儲存並關閉檔案，然後啟動AEM執行個體。
1. 對所有Author和Publish執行個體重複步驟1至4。

#### 設定序列化代理程式 {#configure-the-serialization-agent}

在所有Author和Publish執行個體上執行以下步驟，將套件新增至允許清單：

1. 在瀏覽器視窗中開啟AEM Configuration Manager。 預設URL為`https://'[server]:[port]'/system/console/configMgr`。
1. 搜尋&#x200B;**com.adobe.cq.deserfw.impl.DeserializationFirewallImpl.name**&#x200B;並開啟設定。
1. 將&#x200B;**sun.util.calendar**&#x200B;封裝新增至&#x200B;**允許清單**&#x200B;欄位。 按一下「**儲存**」。
1. 對所有Author和Publish執行個體重複步驟1至3。

### 選用的安裝後設定 {#optional-post-installation-configurations}

#### 設定Dispatcher {#configure-dispatcher}

Dispatcher是Adobe Experience Manager的快取及/或負載平衡工具，可搭配企業級網頁伺服器使用。 如果您使用[Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)，請針對AEM Forms執行下列設定：

1. 設定AEM Forms的存取權：

   開啟dispatcher.any檔案進行編輯。 導覽至篩選區段，並將下列篩選新增至篩選區段：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   儲存並關閉檔案。 如需有關篩選器的詳細資訊，請參閱[Dispatcher檔案](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)。

1. 設定反向連結篩選服務：

   以管理員身分登入Apache Felix設定管理員。 組態管理員的預設URL為`https://[server]:[port_number]/system/console/configMgr`。 在&#x200B;**設定**&#x200B;功能表中，選取&#x200B;**Apache Sling反向連結篩選器**&#x200B;選項。 在允許主機欄位中，輸入Dispatcher的主機名稱，以允許其作為反向連結，然後按一下&#x200B;**儲存**。 專案的格式為`https://[server]:[port]`。

#### 設定快取 {#configure-cache}

快取是縮短資料存取時間、減少延遲，以及改善輸入/輸出(I/O)速度的機制。 調適型表單快取只會儲存調適型表單的HTML內容和JSON結構，不會儲存任何預先填入的資料。 這有助於減少轉譯最適化表單所需的時間。

* 在使用最適化表單快取時，請使用[AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)來快取最適化表單的使用者端資料庫(CSS和JavaScript)。
* 開發自訂元件時，請停用用於開發的伺服器上的最適化表單快取。

執行以下步驟來設定調適型表單快取：

1. 移至https://&#39;[伺服器]：[連線埠]&#39;/system/console/configMgr的AEM Web主控台組態管理員。
1. 按一下&#x200B;**最適化表單和互動式通訊Web Channel設定**&#x200B;以編輯其設定值。 在編輯設定值對話方塊中，指定AEM Forms伺服器執行個體可在&#x200B;**Number of Adaptive Forms**&#x200B;欄位中快取的表單或檔案數目上限。 預設值為 100。按一下「**儲存**」。

   >[!NOTE]
   >
   >若要停用快取，請將[最適化Forms數目]欄位中的值設定為&#x200B;**0**。 當您停用或變更快取設定時，快取會重設，所有表單和檔案都會從快取中移除。

#### 設定表單資料模型的SSL通訊 {#configure-ssl-communcation-for-form-data-model}

您可以為表單資料模型啟用SSL通訊。 若要為表單資料模型啟用SSL通訊，在啟動任何AEM Forms執行個體之前，請為所有執行個體的Java信任存放區新增憑證。 您可以執行以下命令來新增憑證： 」

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

#### 設定Adobe Sign {#configure-adobe-sign}

Adobe Sign可啟用最適化表單的電子簽章工作流程。 電子簽名有助於改善處理法律、銷售、薪資、人力資源管理及許多領域文件的工作流程。

在一般的Adobe Sign與最適化表單情境中，使用者會填寫最適化表單來&#x200B;**申請服務**。 例如，信用卡申請表和市民福利表單。用戶申請、提交和簽署申請表單時，此表單會被傳送給服務提供者，以進一步動作。服務提供者會稽核申請，並使用Adobe Sign將申請標籤為已核准。 若要啟用類似的電子簽章工作流程，您可以整合Adobe Sign與AEM Forms。

若要使用Adobe Sign與AEM Forms，[將Adobe Sign與AEM Forms整合](/help/forms/using/adobe-sign-integration-adaptive-forms.md)。

#### 設定 Adobe Analytics {#configure-adobe-analytics}

AEM Forms與Adobe Analytics整合，可讓您擷取及追蹤已發佈表單和檔案的績效量度。 分析這些量度背後的目的是，根據使表單或檔案更易於使用所需的變更相關資料，做出明智的決定。

若要搭配AEM Forms使用Adobe Analytics，請參閱[設定Analytics和報表](/help/forms/using/configure-analytics-forms-documents.md)。

#### 整合Adobe Target {#integrate-adobe-target}

如果表單提供的體驗不吸引人，您的客戶可能會捨棄表單。 雖然這會讓客戶感到挫折，但也可以提升貴組織的支援數量和成本。 識別並提供適當的客戶體驗以提高轉換率，這既重要又具有挑戰性。 AEM表單擁有此問題的關鍵所在。

AEM forms與Adobe Marketing Cloud解決方案Adobe Target整合，跨多個數位頻道提供個人化及吸引人的客戶體驗。 若要使用Adobe Target來A/B測試最適化表單，[將Adobe Target與AEM Forms整合](/help/forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms)。

## 後續步驟 {#next-steps}

您已將環境設定為使用AEM Forms資料擷取功能。 現在，使用功能的後續步驟為：

* [建立第一個最適化表單](/help/forms/using/create-your-first-adaptive-form.md)
* [建立您的第一個PDF表單](https://www.adobe.com/go/learn_aemforms_designer_quick_start_65)
* [HTML5 Forms簡介](/help/forms/using/introduction.md)
