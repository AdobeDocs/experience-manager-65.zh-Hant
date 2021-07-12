---
title: 安裝和配置互動式通信
seo-title: 安裝和配置互動式通信
description: 安裝及設定AEM Forms互動式通訊，以建立業務通訊、檔案、對帳單、利益通知、行銷郵件、帳單和歡迎套件。
seo-description: 安裝及設定AEM Forms互動式通訊，以建立業務通訊、檔案、對帳單、利益通知、行銷郵件、帳單和歡迎套件。
uuid: 8acb7f68-0b52-4acd-97e2-af31c9408e8d
topic-tags: installing
discoiquuid: 225f2bc1-6842-4c79-a66d-8024a29325c0
docset: aem65
role: Admin
exl-id: 37fcfad9-2f84-4f0c-aed8-e4a5a3303a06
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1411'
ht-degree: 5%

---

# 安裝和配置互動式通信{#install-and-configure-interactive-communications}

## 簡介 {#introduction}

AEM Form能夠集中建立、匯編、管理和傳送安全且互動式的檔案，如業務往來函件、檔案、對帳單、利益通知、行銷郵件、帳單和歡迎套件。 此功能稱為互動式通訊。 此功能包含在AEM Forms附加元件套件中。 附加套件部署在AEM的製作或發佈例項上。

您可以使用互動式通訊功能來產生多種格式的通訊。 例如Web和PDF。 您可以將互動式通訊與AEM Workflow整合，以處理並傳送已組合的通訊給客戶所選擇的通道。 例如，透過電子郵件傳送通訊給使用者。

如果您從舊版升級並已投資通信管理，則可以安裝[相容性包](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package)以繼續使用通信管理。 有關互動式通信和通信管理之間差異的資訊，請參閱[互動式通信概述](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management)。

AEM Forms是功能強大的企業級平台。 互動式通訊只是AEM Forms的其中一項功能。 如需功能的完整清單，請參閱[AEM Forms簡介](../../forms/using/introduction-aem-forms.md)。

## 部署拓撲 {#deployment-topology}

AEM Forms附加元件套件是部署至AEM的應用程式。 您至少需要一個AEM製作與處理執行個體，才能執行互動式通訊功能。 以下拓撲是指示性拓撲，用於在OSGi功能上運行AEM Forms Interactive Communications、通信管理、AEM Forms資料捕獲和以Forms為中心的工作流。 有關拓撲的詳細資訊，請參閱[AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md)的體系結構和部署拓撲。

![推薦拓撲](assets/recommended-topology.png)

AEM Forms互動式通訊會在AEM Forms的Author例項上執行管理、製作和代理使用者介面。 發佈執行個體會托管最終版本的互動式通訊，供使用者使用。

## 系統需求 {#system-requirements}

開始安裝及設定AEM Forms的互動式通訊和通信管理功能之前，請確定：

* 硬體和軟體基礎架構已就緒。 有關支援的硬體和軟體的詳細清單，請參見[技術要求](/help/sites-deploying/technical-requirements.md)。

* AEM例項的安裝路徑不包含空格。
* AEM例項已啟動並執行。 在AEM術語中，「例項」是在製作或發佈模式中，於伺服器上執行的AEM復本。 您至少需要一個AEM例項（製作或處理）才能執行AEM Forms互動式通訊和通信管理功能：

   * **作者**:用於建立、上傳和編輯內容及管理網站的AEM例項。內容準備好上線後，就會複製到發佈執行個體。
   * **處理：** 處理例項是強化的 [AEM](/help/forms/using/hardening-securing-aem-forms-environment.md)  Authorinstance。您可以設定製作例項，並在執行安裝後加強執行。

   * **發佈**:透過網際網路或內部網路向公眾提供已發佈內容的AEM例項。

* 滿足記憶體要求。 AEM Forms附加元件套件需要：

   * 15 GB的臨時空間，用於基於Microsoft Windows的安裝。
   * 6 GB的臨時空間，用於基於UNIX的安裝。

* 基於UNIX的系統的額外要求：如果使用基於UNIX的作業系統，請從相應作業系統的安裝介質安裝以下軟體包。

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

AEM Forms附加元件套件是部署至AEM的應用程式。 此套件包含AEM Forms互動式通訊、通信管理和其他功能。 執行下列步驟以安裝附加元件套件：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 點一下頁首功能表中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在&#x200B;**[!UICONTROL Filters]**&#x200B;部分：
   1. 從&#x200B;**[!UICONTROL Solution]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Forms]**。
   2. 選取套件的版本和類型。 您也可以使用&#x200B;**[!UICONTROL 搜尋下載]**&#x200B;選項來篩選結果。
1. 點選適用於您作業系統的套件名稱，選取「**[!UICONTROL 接受EULA條款]**」，然後點選「**[!UICONTROL 下載]**」。
1. 開啟[套件管理器](https://docs.adobe.com/content/help/zh-Hant/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。
1. 選擇包，然後按一下&#x200B;**[!UICONTROL Install]**。

   您也可以透過[AEM Forms發行](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)文章中列出的直接連結下載套件。

1. 安裝套件後，系統會提示您重新啟動AEM執行個體。 **不要立即重新啟動伺服器。** 停止AEM Forms伺服器之前，請等到AEM-Installation-Directory []/crx-quickstart/logs/error.log檔案中出現ServiceEvent REGISTERED和ServiceEvent UNEGRESTED訊息，且記錄穩定。
1. 在所有「製作」和「發佈」例項上重複步驟1至7。

## 安裝後配置 {#post-installation-configurations}

AEM Forms提供一些強制和選用設定。 強制設定包括設定BouncyCastle程式庫和序列化代理。 選用的設定包括設定Dispatcher和Adobe Target。

### 強制安裝後配置 {#mandatory-post-installation-configurations}

#### 配置RSA和BouncyCastle庫  {#configure-rsa-and-bouncycastle-libraries}

對所有製作和發佈執行個體執行下列步驟以引導委派程式庫：

1. 停止基礎AEM例項。
1. 開啟[AEM安裝目錄]\crx-quickstart\conf\sling.properties檔案進行編輯。

   如果您使用[AEM安裝目錄]\crx-quickstart\bin\start.bat來啟動AEM，請編輯位於[AEM_root]\crx-quickstart\的sling.properties。

1. 將下列屬性新增至sling.properties檔案：

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. 儲存並關閉檔案，然後啟動AEM例項。
1. 在所有「製作」和「發佈」例項上重複步驟1至4。

#### 配置序列化代理 {#configure-the-serialization-agent}

對所有製作和發佈執行個體執行下列步驟，將套件新增至允許清單：

1. 在瀏覽器視窗中開啟AEM Configuration Manager。 預設URL為https://&#39;[server]:[port]&#39;/system/console/configMgr。
1. 搜索並開啟&#x200B;**反序列化防火牆配置**。
1. 將&#x200B;**sun.util.calendar**&#x200B;套件新增至&#x200B;**allowlist**&#x200B;欄位。 按一下「儲存」。
1. 在所有「製作」和「發佈」例項上重複步驟1至3。

### 可選安裝後配置 {#optional-post-installation-configurations}

#### 安裝相容性包 {#install-compatibility-package}

互動式通訊是在AEM 6.5 Forms中建立客戶通訊的預設且建議方法。 如果您已從舊版升級或移轉，並計畫繼續使用信函（通信管理），請安裝[AEMFD相容性套件](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/fd/AEM-FORMS-6.4-COMPAT)。

AEMFD相容性套件可讓您在AEM 6.5 Forms上使用來自AEM 6.4 Forms、AEM 6.3 Forms和AEM 6.2 Forms的下列資產：

* 檔案片段
* 字母
* 資料字典
* 適用性表單已棄用的範本和頁面

#### 設定Dispatcher {#configure-dispatcher}

Dispatcher是Adobe Experience Manager的快取和/或負載平衡工具，可與企業級Web伺服器搭配使用。 如果您使用[Dispatcher](https://helpx.adobe.com/tw/experience-manager/dispatcher/using/dispatcher-configuration.html)，請對AEM Forms執行下列設定：

1. 設定AEM Forms的存取權：

   開啟dispatcher.any檔案以進行編輯。 導覽至篩選區段，並將下列篩選新增至篩選區段：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   儲存並關閉檔案。 如需篩選器的詳細資訊，請參閱[Dispatcher檔案](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)。

1. 設定反向連結篩選服務：

   以管理員身分登入Apache Felix設定管理器。 配置管理器的預設URL為https://&#39;server&#39;:[port_number]/system/console/configMgr。 在&#x200B;**Configurations**&#x200B;功能表中，選取&#x200B;**Apache Sling Referrer Filter**&#x200B;選項。 在「允許主機」欄位中，輸入Dispatcher的主機名稱，以允許它作為反向連結，然後按一下「**儲存**」。 條目的格式為https://&#39;[server]:[port]&#39;。

#### 整合Adobe Target {#integrate-adobe-target}

如果您的客戶提供的體驗不吸引人，就可能會放棄互動式通訊。 雖然讓客戶感到沮喪，但它還可以提高貴組織的支援量和成本。 識別並提供適當的客戶體驗以提高轉換率，既重要又具挑戰性。 AEM表單是此問題的關鍵。

AEM forms與Adobe Marketing Cloud解決方案Adobe Target整合，可跨多個數位頻道提供個人化且吸引人的客戶體驗。 若要使用Adobe Target來個人化互動式通訊，請[將Adobe Target與AEM Forms整合](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms)。

#### 為表單資料模型配置SSL通訊  {#configure-ssl-communcation-for-form-data-model}

您可以為表單資料模型啟用SSL通訊。 若要為表單資料模型啟用SSL通訊，請在啟動任何AEM Forms例項前，將憑證新增至所有例項的Java信任存放區。 您可以執行以下命令來新增憑證：

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## 後續步驟 {#next-steps}

您已設定環境，以使用互動式通訊和通信管理功能。 現在，使用功能的步驟如下：

* [通信管理概觀](/help/forms/using/interactive-communications-overview.md)

* [建立互動式通訊](../../forms/using/create-interactive-communication.md)

* [建立通信管理信函](../../forms/using/create-letter.md)
