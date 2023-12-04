---
title: 安裝和配置 互動式 通信
seo-title: Install and configure Interactive Communications
description: 安裝和配置 AEM Forms 互動式 通信以創建業務通信、檔、報表、福利通知、行銷郵件、帳單和歡迎工具組。
seo-description: Install and configure AEM Forms Interactive Communications to create business correspondences, documents, statements, benefit notices, marketing mails, bills, and welcome kits.
uuid: 8acb7f68-0b52-4acd-97e2-af31c9408e8d
topic-tags: installing
discoiquuid: 225f2bc1-6842-4c79-a66d-8024a29325c0
docset: aem65
role: Admin
exl-id: 37fcfad9-2f84-4f0c-aed8-e4a5a3303a06
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 1%

---

# 安裝和配置 互動式 通信{#install-and-configure-interactive-communications}

## 簡介 {#introduction}

AEM Form可集中建立、組裝、管理和傳送安全、互動式檔案，例如商務通訊、檔案、對帳單、福利通知、行銷郵件、帳單和歡迎套件。 此功能稱為互動式通訊。 此功能包含在AEM Forms附加元件套件中。 附加元件套件部署在AEM的製作或發佈執行個體上。

您可以使用互動式通訊功能，以多種格式產生通訊。 例如，Web和PDF。 您可以將互動式通訊與AEM Workflow整合，以透過客戶選擇的管道處理及傳遞組合通訊給客戶。 例如，透過電子郵件傳送通訊給一般使用者。

如果您要從舊版進行升級，而且已投資於通訊管理，則可以安裝 [相容性套件](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package) 以繼續使用通訊管理。 如需互動式通訊與通訊管理之間差異的相關資訊，請參閱 [互動式通訊概述](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management).

AEM Forms是功能強大的企業級平台。 互動式通訊只是AEM Forms的其中一項功能。 如需完整的功能清單，請參閱 [AEM Forms簡介](../../forms/using/introduction-aem-forms.md).

## 部署拓撲 {#deployment-topology}

AEM Forms附加元件套件是部署至AEM的應用程式。 您只需要至少一個AEM製作與處理執行個體，即可執行互動式通訊功能。 下列拓朴可作為OSGi功能上執行AEM Forms互動式通訊、通訊管理、AEM Forms資料擷取和Forms工作流程的指示性拓朴。 如需有關拓朴的詳細資訊，請參閱 [AEM Forms的架構和部署拓撲](/help/forms/using/aem-forms-architecture-deployment.md).

![建議的拓朴](assets/recommended-topology.png)

AEM Forms互動式通訊會在AEM Forms的製作例項上執行管理、製作和代理程式使用者介面。 發佈執行個體會託管互動式通訊的最終版本，以供一般使用者使用。

## 系統需求 {#system-requirements}

開始安裝及設定AEM Forms的互動式通訊與通訊管理功能之前，請確定：

* 硬體與軟體基礎架構已準備就緒。 如需支援的硬體和軟體的詳細清單，請參閱 [技術需求](/help/sites-deploying/technical-requirements.md).

* AEM執行個體的安裝路徑未包含空格。
* AEM執行個體已啟動且執行中。 在AEM術語中，「例項」是在伺服器上以製作或發佈模式執行的AEM的副本。 您至少需要一個AEM執行個體（製作或處理）才能執行AEM Forms互動式通訊和通訊管理功能：

   * **作者**：用來建立、上傳和編輯內容以及管理網站的AEM執行個體。 一旦內容準備好上線，就會將其復寫到發佈執行個體。
   * **處理中：** 處理執行個體是 [強化的AEM Author](/help/forms/using/hardening-securing-aem-forms-environment.md) 執行個體。 您可以設定Author例項，並在執行安裝後加以強化。

   * **發佈**：透過網際網路或內部網路向公眾提供已發佈內容的AEM執行個體。

* 滿足記憶體要求。 AEM Forms附加包需要：

   * 15 GB 的臨時空間，供基於 Microsoft® Windows 的安裝使用。
   * UNIX安裝需要6 GB的暫存空間。

* UNIX系統的額外需求：如果您使用的是UNIX作業系統，請從個別作業系統的安裝媒體安裝下列套件。

<table>
 <tbody>
  <tr>
   <td>外派人員</td>
   <td>libxcb</td>
   <td>自由文字</td>
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

AEM Forms附加元件套件是部署至AEM的應用程式。 此套件包含AEM Forms互動式通訊、通訊管理和其他功能。 執行以下步驟來安裝附加套件：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 選擇 **[!UICONTROL 標題功能表中的可用Adobe Experience Manager]** 。
1. 在「篩選器」 **** 部分中：
   1. 從解決方案 **** 下拉式清單中選擇 **[!UICONTROL Forms]** 。
   2. 選擇包的版本和類型。 您也可以使用「 **[!UICONTROL Search下載]** 」選項來篩選結果。
1. 選取適用於您的作業系統的套件名稱，然後選取 **[!UICONTROL 接受EULA條款]**，並選取 **[!UICONTROL 下載]**.
1. 打開 [ 封裝管理員 ](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  然後按一下上傳 **[!UICONTROL 包]** 以上傳包。
1. 選擇包，然後按一下安裝 **** 。

   還可以通過AEM Forms版本 ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en) 一文中 [ 列出的直接連結下載包。

1. 安裝包後，系統會提示您重新開機AEM 執行個體。 **不要立即重新開機伺服器。**&#x200B;在停止 AEM Forms 伺服器之前，請等待 ServiceEvent REGISTERED 和 ServiceEvent UNREGISTERED 消息停止出現在 AEM-Installation-Directory ] /crx-quickstart/logs/error.記錄檔 中 [ ，並且日誌穩定。
1. 對所有Author和Publish執行個體重複步驟1至7。

## 安裝後設定 {#post-installation-configurations}

AEM Forms有一些必要和選用的設定。 強制設定包括設定BouncyCastle程式庫和序列化代理程式。 選擇性設定包括設定Dispatcher和Adobe Target。

### 強制安裝後設定 {#mandatory-post-installation-configurations}

#### 設定RSA和BouncyCastle資料庫  {#configure-rsa-and-bouncycastle-libraries}

在所有Author和Publish執行個體上執行下列步驟，以啟動並委派程式庫：

1. 停止基礎AEM執行個體。
1. 開啟 [AEM安裝目錄]\crx-quickstart\conf\sling.properties檔案進行編輯。

   如果您使用 [AEM安裝目錄]\crx-quickstart\bin\start.bat以啟動AEM，然後編輯sling.properties於 [AEM_root]\crx-quickstart\。

1. 將以下屬性新增到sling.properties檔案：

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. 儲存並關閉檔案，然後啟動AEM執行個體。
1. 對所有Author和Publish執行個體重複步驟1至4。

#### 設定序列化代理程式 {#configure-the-serialization-agent}

對所有Author和Publish執行個體執行以下步驟，將套件新增到允許清單：

1. 在瀏覽器視窗中開啟AEM Configuration Manager。 預設URL為https://&#39;[伺服器]：[連線埠]&#39;/system/console/configMgr.
1. 搜尋並開啟 **還原序列化防火牆設定**.
1. 新增 **sun.util.calendar** 封裝到 **允許清單** 欄位。 按一下「儲存」。
1. 對所有Author和Publish執行個體重複步驟1至3。

### 選用的安裝後設定 {#optional-post-installation-configurations}

#### 安裝相容性套件 {#install-compatibility-package}

互動式通訊是在AEM 6.5 Forms中建立客戶通訊的預設和建議方法。 如果您已從舊版升級或移轉，並計畫繼續使用信件（通訊管理），請安裝 [AEMFD相容性套件](https://experienceleague.adobe.com/docs/experience-manager-65/forms/upgrade-aem-forms/aem-forms-osgi-upgrade/compatibility-package.html?lang=en).

AEMFD 相容性套件可讓您在 AEM 6.5 Forms AEM 6.4 Forms、AEM 6.3 Forms 和 AEM 6.2 Forms使用以下資產：

* 檔片段
* 字母
* 資料字典
* 最適化表單已棄用的範本和頁面

#### 設定Dispatcher {#configure-dispatcher}

Dispatcher是Adobe Experience Manager的快取和負載平衡工具，用於企業級網頁伺服器。 如果您使用 [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hant)，然後針對AEM Forms執行下列設定：

1. 設定AEM Forms的存取權：

   開啟dispatcher.any檔案進行編輯。 導覽至篩選區段，並將下列篩選新增至篩選區段：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   儲存並關閉檔案。 如需有關篩選器的詳細資訊，請參閱 [Dispatcher檔案](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hant).

1. 設定反向連結篩選服務：

   以管理員身分登入Apache Felix設定管理員。 組態管理員的預設URL為https://&#39;server&#39;：[連線埠號碼]/system/console/configMgr。 在 **設定** 功能表，選取 **Apache Sling查閱者篩選器** 選項。 在允許主機欄位中，輸入Dispatcher的主機名稱，以允許其作為反向連結，然後按一下 **儲存**. 專案的格式為https://&#39;[伺服器]：[連線埠]&#39;.

#### 整合Adobe Target {#integrate-adobe-target}

如果互動式通訊提供的體驗不吸引人，您的客戶可能會捨棄互動式通訊。 雖然這會讓客戶感到挫折，但也會提高貴組織的支援數量和成本。 識別並提供適當的客戶體驗以提高轉換率，這既重要又具有挑戰性。 AEM表單擁有此問題的關鍵所在。

AEM forms與Adobe Experience Cloud解決方案Adobe Target整合，跨多個數位頻道提供個人化及吸引人的客戶體驗。 若要使用Adobe Target來個人化互動式通訊， [將Adobe Target與AEM Forms整合](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

#### 設定表單資料模型的SSL通訊  {#configure-ssl-communcation-for-form-data-model}

您可以為表單資料模型啟用SSL通訊。 若要為表單資料模型啟用SSL通訊，在啟動任何AEM Forms執行個體之前，請將憑證新增到所有執行個體的Java™信任存放區。 您可以執行以下命令來新增憑證：

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## 後續步驟 {#next-steps}

您已將環境設定為使用互動式通訊和通訊管理功能。 現在，使用功能的步驟如下：

* [通信管理概述](/help/forms/using/interactive-communications-overview.md)

* [建立互動式通訊](../../forms/using/create-interactive-communication.md)

* [建立通信管理信函](../../forms/using/create-letter.md)
