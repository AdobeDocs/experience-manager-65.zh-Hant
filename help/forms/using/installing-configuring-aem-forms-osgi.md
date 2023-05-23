---
title: 安裝和配置資料捕獲功能
seo-title: Install and configure data capture capabilities
description: 安裝和配置自適應表單、PDF forms和HTML5Forms。 配置Adobe Analytics和Adobe Target，以便根據表單和目標用戶的配置檔案分析其使用情況。
seo-description: Install and configure adaptive forms, PDF Forms, and HTML5 Forms. Configure Adobe Analytics and Adobe Target for adaptive forms to analyze usage of forms and target users based on their profile.
uuid: 5d49032a-4dea-4f21-9dad-a7a30c5872ea
topic-tags: installing
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dfc473eb-6091-4f5d-a5a0-789972c513a9
docset: aem65
role: Admin
exl-id: 19b5765e-50bc-4fed-8af5-f6bb464516c8
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1882'
ht-degree: 8%

---

# 安裝和配置資料捕獲功能{#install-and-configure-data-capture-capabilities}

## 簡介 {#introduction}

AEM Forms提供一組表單以從最終用戶獲取資料：適應表格、HTML5Forms和PDF forms。 它還提供了工具，用於列出網頁上所有可用的表單，分析表單的使用情況，並根據其配置檔案來確定目標用戶。 這些功能包含在AEM Forms附加軟體包中。 載入項包部署在的Author或Publish實例AEM上。

**自適應表單：** 這些形式根據設備的螢幕大小改變外觀，在本質上是接合的，並且是交互的。 適應性Forms也可以與Adobe Analytics、Adobe Sign和Adobe Target相融合。 它使您能夠根據用戶的人口結構和其他功能向用戶提供個性化表單和面向流程的體驗。 您還可以將自適應形式與Adobe Sign整合。

**PDF forms** 適用於像素完美打印和PDF文檔中的數字資訊捕獲。 在數字化虛擬形象中，你可以使用Adobe Acrobat或Acrobat Reader填寫這些表格。 您可以將這些表單托管在您的網站上，或使用表單門戶在站點上列出AEM這些表單。 您還可以將這些表單作為附件通過電子郵件發送給其他人。 這些表格最適合案頭環境。

**HTML5Forms** 是瀏覽器友好版的PDF forms。 HTML5Forms適用於不支援PDF插件的環境。 HTML5Forms允許在不支援基於XFA的PDF的移動設備和案頭瀏覽器上呈現基於XFA的表單。 這些表格最適合平板電腦和台式機環境。

AEM Forms是一個功能強大的企業級平台，資料捕獲(自適應表單、PDF forms和HTML5Forms)只是AEM Forms的能力之一。 有關權能的完整清單，請參見 [AEM Forms簡介](/help/forms/using/introduction-aem-forms.md)。

## 部署拓撲 {#deployment-topology}

AEM Forms附加軟體包是部署到的應AEM用程式 運行AEM Forms資料捕獲功能至少只需一個AEM作者和AEM發佈實例。 建議使用以下拓撲來運行AEM FormsAEM Forms資料捕獲功能。 有關拓撲的詳細資訊，請參見 [用於AEM Forms的體系結構和部署拓撲](/help/forms/using/aem-forms-architecture-deployment.md)。

![推薦拓撲](assets/recommended-topology.png)

## 系統要求 {#system-requirements}

在開始安裝和配置AEM Forms的資料捕獲功能之前，請確保：

* 硬體和軟體基礎架構已到位。 有關支援的硬體和軟體的詳細清單，請參見 [技術要求](/help/sites-deploying/technical-requirements.md)。

* 實例的安AEM裝路徑不包含空格。
* 實例AEM已啟動並正在運行。 對於Windows用戶，以提升AEM模式安裝實例。 在術AEM語中，「實例」是在作者或發AEM布模式下在伺服器上運行的副本。 你至少需要兩個 [實AEM例（一個作者和一個發佈）](/help/sites-deploying/deploy.md) 運行AEM Forms資料捕獲功能：

   * **作者**:用於AEM建立、上載和編輯內容以及管理網站的實例。 一旦內容準備好投入使用，就會將其複製到發佈實例。
   * **發佈**:通過AEMInternet或內部網路向公眾提供已發佈內容的實例。

* 滿足記憶體要求。 AEM Forms附加軟體包要求：

   * 15 GB臨時空間，用於基於MicrosoftWindows的安裝。
   * 6 GB的臨時空間，用於基於UNIX的安裝。

* 為作者和發佈實例設定複製和反向複製。 有關詳細資訊，請參閱 [複製](/help/sites-deploying/replication.md)。
* 對於基於UNIX的系統：

   * 從安裝介質安裝以下32位軟體包：

<table>
 <tbody>
  <tr>
   <td>外</td>
   <td>方配</td>
   <td>自由型</td>
   <td>格列布</td>
  </tr>
  <tr>
   <td>自旋</td>
   <td>libICE</td>
   <td>利比庫</td>
   <td>libSM</td>
  </tr>
  <tr>
   <td>液體</td>
   <td>libX11</td>
   <td><p>庫</p> </td>
   <td>libxcb</td>
  </tr>
  <tr>
   <td>libXext</td>
   <td>利布希內拉馬</td>
   <td>libXrandr</td>
   <td>libXrender</td>
  </tr>
  <tr>
   <td>nss-softokn-freebl</td>
   <td>OpenSSL</td>
   <td>茲利布</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* 如果伺服器上已安裝OpenSSL，請將其升級到最新版本。
>* 建立libcurl.so、libcrypto.so和libssl.so符號連結，分別指向libcurl、libcrypto和libssl庫的最新版本。
>


* 從安裝介質安裝以下64位軟體包：

   * 利比庫

* 安裝 [MicrosoftVisual Studio 2019 32位可再發行](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)。


## 安裝AEM Forms載入項軟體包 {#install-aem-forms-add-on-package}

AEM Forms附加軟體包是部署到的應AEM用程式 該包包含AEM Forms資料捕獲和其他功能。 執行以下步驟以安裝附加軟體包：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 點一下頁首功能表中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在 **[!UICONTROL 篩選器]** 部分：
   1. 選擇 **[!UICONTROL Forms]** 從 **[!UICONTROL 解決方案]** 的子菜單。
   2. 選擇包的版本和類型。 您還可以使用 **[!UICONTROL 搜索下載]** 選項。
1. 點擊適用於您的作業系統的包名稱，選擇 **[!UICONTROL 接受EULA條款]**，然後點擊 **[!UICONTROL 下載]**。
1. 開啟[套件管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。
1. 選擇包並按一下 **[!UICONTROL 安裝]**。

   您也可以通過中列出的直接連結下載軟體包 [AEM Forms釋放](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 文章。
1. 安裝軟體包後，系統會提示您重新啟動實AEM例。 **不要立即重新啟動伺服器。** 停止AEM Forms伺服器之前，請等待ServiceEvent REGISTERED和ServiceEvent UNREGISTERED消息停止出現在 `[AEM-Installation-Directory]/crx-quickstart/logs/error.log` 檔案和日誌穩定。
1. 對所有「作者」和「發佈」實例重複步驟1-7。

### （僅限Windows）自動安裝Visual Studio可再分發表 {#automatic-installation-visual-studio-redistributables}

如果以提升模AEM式安裝實例，則在安裝AEM Forms附加軟體包期間會自動安裝32位Visual Studio可再分發版。

要評估是否自動安裝了Visual Studio可再分發表，請開啟 `error.log` 檔案在 `/crx-repository/logs/` 的子菜單。 日誌包含以下消息：

`Redist <service name> already installed on system, will not attempt re-installation`

如果重新分發表無法安裝，日誌將包含以下消息：

`Current user does not have elevated privileges, aborting installation of redist <service name>`

要解決此問題，請重新啟AEM動伺服器，AEM以提升模式安裝，然後安裝AEM Forms附加軟體包。

如果權限檢查失敗，日誌將包含以下消息：

`Privilege escalation check failed with error: <error message>`

## 安裝後配置 {#post-installation-configurations}

AEM Forms有一些強制性和可選配置。 強制配置包括配置BouncyCastle庫和序列化代理。 可選配置包括配置調度程式、Forms門戶、Adobe Sign、Adobe Analytics和Adobe Target。

### 強制安裝後配置 {#mandatory-post-installation-configurations}

#### 配置RSA和BouncyCastle庫  {#configure-rsa-and-bouncycastle-libraries}

對所有「作者」(Author)和「發佈」(Publish)實例執行以下步驟以引導委託庫：

1. 停止基礎實AEM例。
1. 開啟 `[AEM installation directory]\crx-quickstart\conf\sling.properties` 檔案。

   如果你用了 `[AEM installation directory]\crx-quickstart\bin\start.bat` 啟AEM動，然後編輯位於 `[AEM_root]\crx-quickstart\`。

1. 將以下屬性添加到sling.properties檔案：

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. 保存並關閉檔案並啟AEM動實例。
1. 對所有「作者」和「發佈」實例重複步驟1-4。

#### 配置序列化代理 {#configure-the-serialization-agent}

對所有「作者」(Author)和「發佈」(Publish)實例執行以下步驟，將包添加到允許清單：

1. 在瀏覽AEM器窗口中開啟Configuration Manager。 預設URL為 `https://'[server]:[port]'/system/console/configMgr`。
1. 搜索 **com.adobe.cq.deserfw.impl.反序列化FirewallImpl.name** 開啟配置。
1. 添加 **sun.util.calendar** 包到 **允許清單** 的子菜單。 按一下「**儲存**」。
1. 對所有「作者」和「發佈」實例重複步驟1-3。

### 可選安裝後配置 {#optional-post-installation-configurations}

#### 設定 Dispatcher {#configure-dispatcher}

Dispatcher 是 Adobe Experience Manager 的快取及/或負載平衡工具，可搭配企業級網頁伺服器使用。如果您使用 [調度程式](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)，然後為AEM Forms執行以下配置：

1. 配置AEM Forms的訪問：

   開啟dispatcher.any檔案進行編輯。 導航到篩選器節，然後將以下篩選器添加到篩選器節：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   保存並關閉檔案。 有關篩選器的詳細資訊，請參見 [調度程式文檔](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)。

1. 配置引用程式篩選器服務：

   以管理員身份登錄到Apache Felix配置管理器。 配置管理器的預設URL為 `https://[server]:[port_number]/system/console/configMgr`。 在 **配置** 的 **Apache Sling引用篩選器** 的雙曲餘切值。 在「允許主機」欄位中，輸入調度程式的主機名以允許它作為引用者，然後按一下 **保存**。 條目的格式為 `https://[server]:[port]`。

#### 配置快取 {#configure-cache}

快取是一種縮短資料存取時間、減少延遲和提高輸入/輸出(I/O)速度的機制。 自適應表單快取僅儲存自適應表單的HTML內容和JSON結構，而不保存任何預填資料。 它有助於減少渲染自適應表單所需的時間。

* 在使用自適應表單快取時，使用 [調度AEM程式](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) 快取自適應表單的客戶端庫（CSS和JavaScript）。
* 在開發自定義元件時，在用於開發的伺服器上禁用自適應表單快取。

執行以下步驟來配置自適應表單快取：

1. 轉到AEMhttps://&#39;上的Web控制台配置管理器[伺服器]:[埠]「/system/console/configMgr。
1. 按一下 **自適應形式與交互通信Web通道配置** 編輯其配置值。 在「編輯配置值」對話框中，指定AEM Forms伺服器實例可以快取的最大表單或文檔數 **自適應Forms** 的子菜單。 預設值為 100。按一下「**儲存**」。

   >[!NOTE]
   >
   >要禁用快取，請將「自適應Forms數」欄位中的值設定為 **0**。 在禁用或更改快取配置時，將重置快取，並從快取中刪除所有表單和文檔。

#### 為表單資料模型配置SSL通信 {#configure-ssl-communcation-for-form-data-model}

可以為表單資料模型啟用SSL通信。 要為表單資料模型啟用SSL通信，請在啟動任何AEM Forms實例之前，將證書添加到所有實例的Java信任儲存中。 您可以運行以下命令來添加證書：&quot;

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

#### 配置Adobe Sign {#configure-adobe-sign}

Adobe Sign支援自適應表單的電子簽名工作流。 電子簽名有助於改善處理法律、銷售、薪資、人力資源管理及許多領域文件的工作流程。

在典型的Adobe Sign和自適應表單場景中，用戶填充自適應表單以 **申請服務**。 例如，信用卡申請表和市民福利表單。用戶申請、提交和簽署申請表單時，此表單會被傳送給服務提供者，以進一步動作。服務提供商審閱應用程式，並使用Adobe Sign標籤批准的應用程式。 要啟用類似的電子簽名工作流，您可以將Adobe Sign與AEM Forms整合。

用Adobe Sign和AEM Forms, [整合Adobe Sign與AEM Forms](/help/forms/using/adobe-sign-integration-adaptive-forms.md)。

#### 配置Adobe Analytics {#configure-adobe-analytics}

AEM Forms與Adobe Analytics整合，使您能夠捕獲和跟蹤已發佈表單和文檔的效能指標。 分析這些指標背後的目標是根據有關使表單或文件更有用所需的變更資料做出明智的決策。

要將Adobe Analytics與AEM Forms一起使用，請參閱 [配置分析和報告](/help/forms/using/configure-analytics-forms-documents.md)。

#### 整合Adobe Target {#integrate-adobe-target}

如果您的客戶提供的體驗不吸引人，他們可能會放棄表單。 雖然這讓客戶感到沮喪，但也會增加您組織的支援量和成本。 確定並提供適當的客戶體驗，提高轉換率，這既是關鍵，也是挑戰。 表AEM單是此問題的關鍵。

表AEM單與Adobe Marketing Cloud解決方案Adobe Target整合，跨多個數字渠道提供個性化且引人入勝的客戶體驗。 要使用Adobe Target到A/Btest適應形式， [整合Adobe Target與AEM Forms](/help/forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms)。

## 後續步驟 {#next-steps}

您已將環境配置為使用AEM Forms資料捕獲功能。 現在，使用該功能的後續步驟是：

* [建立第一個自適應窗體](/help/forms/using/create-your-first-adaptive-form.md)
* [建立第一個PDF窗體](https://www.adobe.com/go/learn_aemforms_designer_quick_start_65)
* [HTML5Forms](/help/forms/using/introduction.md)
