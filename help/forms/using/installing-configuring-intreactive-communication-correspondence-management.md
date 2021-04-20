---
title: 安裝和配置互動式通訊
seo-title: 安裝和配置互動式通訊
description: 安裝並設定AEM Forms互動式通訊，以建立商業通訊、檔案、陳述、利益通知、行銷郵件、帳單和歡迎套件。
seo-description: 安裝並設定AEM Forms互動式通訊，以建立商業通訊、檔案、陳述、利益通知、行銷郵件、帳單和歡迎套件。
uuid: 8acb7f68-0b52-4acd-97e2-af31c9408e8d
topic-tags: installing
discoiquuid: 225f2bc1-6842-4c79-a66d-8024a29325c0
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1412'
ht-degree: 5%

---


# 安裝和配置互動式通信{#install-and-configure-interactive-communications}

## 簡介 {#introduction}

表AEM單可集中建立、匯整、管理和傳送安全且互動式檔案，例如商業通訊、檔案、報表、福利通知、行銷郵件、帳單和歡迎套件。 此功能稱為互動式通訊。 此功能包含在AEM Forms附加套件中。 附加元件套件會部署在的「作者」或「發佈」例項AEM上。

您可以使用互動式通訊功能，以多種格式產生通訊。 例如，網頁和PDF。 您可以將互動式通訊與AEMWorkflow整合，以透過客戶選擇的通道，處理並傳遞整合式通訊。 例如，透過電子郵件傳送通訊給使用者。

如果您從舊版升級並已投入通信管理，則可以安裝[相容包](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package)以繼續使用通信管理。 有關互動式通信和通信管理之間差異的資訊，請參閱[互動式通信概述](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management)。

AEM Forms是強大的企業級平台。 互動式通訊只是AEM Forms的一項功能。 有關功能的完整清單，請參見[AEM Forms簡介](../../forms/using/introduction-aem-forms.md)。

## 部署拓撲{#deployment-topology}

AEM Forms附加套件是部署在上的應用程AEM式。 您至少只需要一個AEM作者和處理執行個體，就能執行互動式通訊功能。 以下拓撲是指示性拓撲，用於運行AEM Forms互動式通信、通信管理、AEM Forms資料捕獲和Forms中心的OSGi功能工作流。 有關拓撲的詳細資訊，請參見[AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md)的體系結構和部署拓撲。

![推薦拓撲](assets/recommended-topology.png)

AEM Forms互動通訊在AEM Forms的「作者」執行個體上執行管理、製作和代理使用者介面。 「發佈」執行個體代管最終版本的互動式通訊，可供使用者使用。

## 系統要求{#system-requirements}

在您開始安裝和配置AEM Forms的互動式通訊和通訊管理功能之前，請確定：

* 硬體和軟體基礎架構已就緒。 有關支援的硬體和軟體的詳細清單，請參見[技術要求](/help/sites-deploying/technical-requirements.md)。

* 實例的安AEM裝路徑不包含空格。
* 實AEM例已啟動並運行。 在術AEM語中，「例項」是在作者或發AEM布模式下在伺服器上執行的副本。 您至少需要一個例AEM項（作者或處理）來執行AEM Forms互動式通訊和通訊管理功能：

   * **作者**:用於AEM建立、上傳和編輯內容以及管理網站的例項。內容一旦準備好上線，就會複製到發佈實例。
   * **處理：處** 理例項是硬化的 [AuthorAEM例](/help/forms/using/hardening-securing-aem-forms-environment.md) 項。您可以設定Author例項，並在執行安裝後加強它。

   * **發佈**:透過AEM網際網路或內部網路為公眾提供已發佈內容的例項。

* 符合記憶體需求。 AEM Forms附加套件需要：

   * 15 GB的臨時空間，用於基於Microsoft Windows的安裝。
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

## 安裝AEM Forms附加軟體包{#install-aem-forms-add-on-package}

AEM Forms附加套件是部署在上的應用程AEM式。 這套套件包含AEM Forms互動式通訊、通訊管理和其他功能。 執行下列步驟以安裝附加元件套件：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 點一下頁首功能表中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在&#x200B;**[!UICONTROL Filters]**&#x200B;區段中：
   1. 從&#x200B;**[!UICONTROL Solution]**&#x200B;下拉式清單中選擇&#x200B;**[!UICONTROL Forms]**。
   2. 選擇包的版本和類型。 您也可以使用&#x200B;**[!UICONTROL 搜尋下載]**&#x200B;選項來篩選結果。
1. 點選適用於您作業系統的套件名稱，選取「**[!UICONTROL 接受EULA條款]**」，然後點選「**[!UICONTROL 下載]**」。
1. 開啟[套件管理器](https://docs.adobe.com/content/help/zh-Hant/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。
1. 選擇軟體包並按一下&#x200B;**[!UICONTROL Install]**。

   您也可以透過[AEM Forms版本](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)文章中所列的直接連結下載套件。

1. 安裝軟體包後，系統會提示您重新啟動AEM實例。 **不要立即重新啟動伺服器。** 在停止AEM Forms伺服器之前，請等待ServiceEvent REGISTERED和ServiceEvent UNREGISTERED消息停止顯示在 [AEM-Installation-Directory] /crx-quickstart/logs/error.log檔案中，並且日誌是穩定的。
1. 對所有「作者」和「發佈」例項重複步驟1-7。

## 安裝後配置{#post-installation-configurations}

AEM Forms有一些強制性和可選配置。 必備配置包括配置BuncyCastle庫和序列化代理。 可選配置包括配置調度程式和Adobe Target。

### 強制安裝後配置{#mandatory-post-installation-configurations}

#### 配置RSA和BuncyCastle庫{#configure-rsa-and-bouncycastle-libraries}

對所有「作者」(Author)和「發佈」(Publish)實例執行以下步驟以引導委派庫：

1. 停止基礎實AEM例。
1. 開啟[安裝目AEM錄]\crx-quickstart\conf\sling.properties檔案進行編輯。

   如果您使用[AEM安裝目錄]\crx-quickstart\bin\start.bat來啟動AEM，則請編輯位於[AEM_root]\crx-quickstart\的sling.properties。

1. 將下列屬性新增至sling.properties檔案：

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. 儲存並關閉檔案，然後啟AEM動執行個體。
1. 對所有「作者」和「發佈」例項重複步驟1-4。

#### 配置序列化代理{#configure-the-serialization-agent}

對所有「作者」(Author)和「發佈」(Publish)實例執行以下步驟，將包添加到allowlist:

1. 在瀏AEM覽器視窗中開啟「設定管理員」。 預設URL為https://&#39;[server]:[port]&#39;/system/console/configMgr。
1. 搜索並開啟&#x200B;**還原序列化防火牆配置**。
1. 將&#x200B;**sun.util.calendar**&#x200B;軟體包添加到&#x200B;**allowlist**&#x200B;欄位。 按一下「儲存」。
1. 對所有「作者」和「發佈」例項重複步驟1-3。

### 可選安裝後配置{#optional-post-installation-configurations}

#### 安裝相容性軟體包{#install-compatibility-package}

在Forms6.5版中，互動式通訊是建立客戶通訊的預設AEM和建議方式。 如果您已升級或從舊版移轉，並計畫繼續使用字母（通信管理），請安裝[AEMFD相容性軟體包](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/fd/AEM-FORMS-6.4-COMPAT)。

AEMFD相容性軟體包允許您使用來自AEM6.4Forms、AEM 6.3Forms和AEM6.2Forms的以AEM下資產(在6.5Forms):

* 檔案片段
* 字母
* 資料字典
* 不再支援的最適化表單範本和頁面

#### 配置Dispatcher {#configure-dispatcher}

Dispatcher是Adobe Experience Manager的快取和／或負載平衡工具，可與企業級Web伺服器一起使用。 如果使用[Dispatcher](https://helpx.adobe.com/tw/experience-manager/dispatcher/using/dispatcher-configuration.html)，則對AEM Forms執行以下配置：

1. 配置AEM Forms的訪問：

   開啟dispatcher.any檔案以進行編輯。 導覽至篩選區段，並將下列篩選新增至篩選區段：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   儲存並關閉檔案。 有關篩選器的詳細資訊，請參見[Dispatcher documentation](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)。

1. 設定反向連結篩選服務：

   以管理員身分登入Apache Felix組態管理員。 配置管理器的預設URL為https://&#39;server&#39;:[port_number]/system/console/configMgr。 在&#x200B;**Configurations**&#x200B;選單中，選取&#x200B;**Apache Sling Referrer Filter**&#x200B;選項。 在「允許主機」欄位中，輸入調度程式的主機名以允許它作為反向連接，然後按一下「保存」。 ****&#x200B;條目的格式為https://&#39;[server]:[port]&#39;。

#### 整合Adobe Target{#integrate-adobe-target}

如果您的客戶提供的體驗不吸引人，他們可能會放棄互動式通訊。 雖然這令客戶感到挫折，但也可以提升組織的支援數量和成本。 識別並提供適當的客戶體驗以提高轉化率，這既重要，也極具挑戰性。 表AEM單是問題的關鍵。

表AEM單與Adobe Marketing Cloud解決方案Adobe Target整合，跨多個數位通道提供個人化且吸引人的客戶體驗。 要使用Adobe Target實現互動式通信的個性化，[將Adobe Target與AEM Forms整合。](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms)

#### 為表單資料模型{#configure-ssl-communcation-for-form-data-model}配置SSL通信

您可以為表單資料模型啟用SSL通訊。 若要啟用表單資料模型的SSL通訊，在啟動任何AEM Forms例項之前，請將憑證新增至所有例項的Java信任存放區。 您可以執行以下命令來添加證書：

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## 後續步驟{#next-steps}

您已設定環境，以使用互動式通訊和通訊管理功能。 現在，使用此功能的步驟如下：

* [通信管理概述](/help/forms/using/interactive-communications-overview.md)

* [建立互動式通訊](../../forms/using/create-interactive-communication.md)

* [建立信件管理函件](../../forms/using/create-letter.md)

