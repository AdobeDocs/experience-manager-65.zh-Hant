---
title: 安裝和配置互動式通信
seo-title: Install and configure Interactive Communications
description: 安裝和配置AEM Forms互動通信，以建立業務通信、文檔、聲明、利益通知、營銷郵件、帳單和歡迎套件。
seo-description: Install and configure AEM Forms Interactive Communications to create business correspondences, documents, statements, benefit notices, marketing mails, bills, and welcome kits.
uuid: 8acb7f68-0b52-4acd-97e2-af31c9408e8d
topic-tags: installing
discoiquuid: 225f2bc1-6842-4c79-a66d-8024a29325c0
docset: aem65
role: Admin
exl-id: 37fcfad9-2f84-4f0c-aed8-e4a5a3303a06
source-git-commit: 18cfefb794382b5314b18a62645f1fba28d314a2
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 6%

---

# 安裝和配置互動式通信{#install-and-configure-interactive-communications}

## 簡介 {#introduction}

AEM表單能夠集中建立、匯編、管理和交付安全的互動式文檔，如業務往來、文檔、報表、利益通知、營銷郵件、帳單和歡迎套件。 此功能稱為交互通信。 該功能包含在AEM Forms附加軟體包中。 載入項包部署在的Author或Publish實例AEM上。

您可以使用互動式通信功能以多種格式生成通信。 例如，Web和PDF。 您可以將互動式通信與AEMWorkflow整合，以處理並將裝配好的通信通過客戶選擇的渠道發送給客戶。 例如，通過電子郵件向最終用戶發送通信。

如果您正在從以前的版本升級並且已投資於通信管理，則可以安裝 [相容性包](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package) 繼續使用函件管理。 有關互動式通信和通信管理之間差異的資訊，請參見 [互動式通信概述](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management)。

AEM Forms是一個強大的企業級平台。 互動交流只是AEM Forms的能力之一。 有關權能的完整清單，請參見 [AEM Forms簡介](../../forms/using/introduction-aem-forms.md)。

## 部署拓撲 {#deployment-topology}

AEM Forms附加軟體包是部署到的應AEM用程式 運行互動式通信功能至少需要一個AEM作者和處理實例。 以下拓撲是指示性拓撲，用於運行AEM Forms互動式通信、通信管理、AEM Forms資料捕獲和以Forms為中心的OSGi功能工作流。 有關拓撲的詳細資訊，請參見 [用於AEM Forms的體系結構和部署拓撲](/help/forms/using/aem-forms-architecture-deployment.md)。

![推薦拓撲](assets/recommended-topology.png)

AEM Forms互動式通信在AEM Forms的「作者」實例上運行管理、創作和代理用戶介面。 「發佈」實例承載最終版本的互動式通信，可供最終用戶使用。

## 系統要求 {#system-requirements}

在開始安裝和配置AEM Forms的互動式通信和通信管理功能之前，請確保：

* 硬體和軟體基礎架構已到位。 有關支援的硬體和軟體的詳細清單，請參見 [技術要求](/help/sites-deploying/technical-requirements.md)。

* 實例的安AEM裝路徑不包含空格。
* 實例AEM已啟動並正在運行。 在術AEM語中，「實例」是在作者或發AEM布模式下在伺服器上運行的副本。 您至少需要一個AEM實例（作者或處理）來運行AEM Forms互動式通信和通信管理功能：

   * **作者**:用於AEM建立、上載和編輯內容以及管理網站的實例。 一旦內容準備好投入使用，就會將其複製到發佈實例。
   * **處理：** 處理實例是 [AEM作者](/help/forms/using/hardening-securing-aem-forms-environment.md) 實例。 可以設定Author實例並在執行安裝後對其進行強化。

   * **發佈**:通過AEMInternet或內部網路向公眾提供已發佈內容的實例。

* 滿足記憶體要求。 AEM Forms附加軟體包要求：

   * 15 GB臨時空間，用於基於Microsoft® Windows的安裝。
   * 6 GB的臨時空間，用於基於UNIX的安裝。

* 基於UNIX的系統的額外要求：如果使用基於UNIX的作業系統，請從相應作業系統的安裝介質安裝以下軟體包。

<table>
 <tbody>
  <tr>
   <td>外</td>
   <td>libxcb</td>
   <td>自由型</td>
   <td>庫</td>
  </tr>
  <tr>
   <td>libSM</td>
   <td>茲利布</td>
   <td>libICE</td>
   <td>液體</td>
  </tr>
  <tr>
   <td>格列布</td>
   <td>libXext</td>
   <td><p>nss-softokn-freebl</p> </td>
   <td>方配</td>
  </tr>
  <tr>
   <td>libX11</td>
   <td>libXrender</td>
   <td>libXrandr</td>
   <td>利布希內拉馬</td>
  </tr>
 </tbody>
</table>

## 安裝AEM Forms載入項軟體包 {#install-aem-forms-add-on-package}

AEM Forms附加軟體包是部署到的應AEM用程式 該包包含AEM Forms互動通信、通信管理和其他功能。 執行以下步驟以安裝附加軟體包：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 點一下頁首功能表中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在 **[!UICONTROL 篩選器]** 部分：
   1. 選擇 **[!UICONTROL Forms]** 從 **[!UICONTROL 解決方案]** 的子菜單。
   2. 選擇包的版本和類型。 您還可以使用 **[!UICONTROL 搜索下載]** 選項。
1. 點擊適用於您的作業系統的包名稱，選擇 **[!UICONTROL 接受EULA條款]**，然後點擊 **[!UICONTROL 下載]**。
1. 開啟[套件管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。
1. 選擇包並按一下 **[!UICONTROL 安裝]**。

   您也可以通過中列出的直接連結下載軟體包 [AEM Forms釋放](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hant) 文章。

1. 安裝軟體包後，系統會提示您重新啟動實AEM例。 **不要立即重新啟動伺服器。** 停止AEM Forms伺服器之前，請等待ServiceEvent REGISTERED和ServiceEvent UNREGISTERED消息停止出現在 [安AEM裝目錄]/crx-quickstart/logs/error.log檔案，日誌穩定。
1. 對所有「作者」和「發佈」實例重複步驟1-7。

## 安裝後配置 {#post-installation-configurations}

AEM Forms有一些強制性和可選配置。 強制配置包括配置BouncyCastle庫和序列化代理。 可選配置包括配置Dispatcher和Adobe Target。

### 強制安裝後配置 {#mandatory-post-installation-configurations}

#### 配置RSA和BouncyCastle庫  {#configure-rsa-and-bouncycastle-libraries}

對所有「作者」(Author)和「發佈」(Publish)實例執行以下步驟以引導委託庫：

1. 停止基礎實AEM例。
1. 開啟 [AEM安裝目錄]\crx-quickstart\conf\sling.properties檔案進行編輯。

   如果你用了 [AEM安裝目錄]\crx-quickstart\bin\start.bat啟動AEM，然後編輯sling.properties，地址為 [AEM根]\crx-quickstart\。

1. 將以下屬性添加到sling.properties檔案：

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. 保存並關閉檔案並啟AEM動實例。
1. 對所有「作者」和「發佈」實例重複步驟1-4。

#### 配置序列化代理 {#configure-the-serialization-agent}

對所有「作者」(Author)和「發佈」(Publish)實例執行以下步驟，將包添加到允許清單：

1. 在瀏覽AEM器窗口中開啟Configuration Manager。 預設URL為https://&#39;[伺服器]:[埠]「/system/console/configMgr。
1. 搜索並開啟 **反序列化防火牆配置**。
1. 添加 **sun.util.calendar** 包到 **允許清單** 的子菜單。 按一下「儲存」。
1. 對所有「作者」和「發佈」實例重複步驟1-3。

### 可選安裝後配置 {#optional-post-installation-configurations}

#### 安裝相容性包 {#install-compatibility-package}

在Forms6.5中，互動式通信是建立客戶通信的預設和AEM推薦方法。 如果您已升級或從以前版本遷移，並計畫繼續使用信函（通信管理），請安裝 [AEMFD相容性包](https://experienceleague.adobe.com/docs/experience-manager-65/forms/upgrade-aem-forms/aem-forms-osgi-upgrade/compatibility-package.html?lang=en)。

AEMFD相容性軟體包允許您在AEM6.5Forms上使用來自6.4Forms、AEM6.3Forms和AEM6.2Forms的AEM以下資產：

* 文檔片段
* 字母
* 資料字典
* 不建議使用的自適應表單模板和頁面

#### 設定 Dispatcher {#configure-dispatcher}

Dispatcher 是 Adobe Experience Manager 的快取及負載平衡工具，搭配企業級網頁伺服器使用。如果您使用 [調度程式](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hant)，然後為AEM Forms執行以下配置：

1. 配置AEM Forms的訪問：

   開啟dispatcher.any檔案進行編輯。 導航到篩選器節，然後將以下篩選器添加到篩選器節：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   保存並關閉檔案。 有關篩選器的詳細資訊，請參見 [調度程式文檔](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hant)。

1. 配置引用程式篩選器服務：

   以管理員身份登錄到Apache Felix配置管理器。 配置管理器的預設URL為https://&#39;server&#39;:[埠號]/system/console/configMgr。 在 **配置** 的 **Apache Sling引用篩選器** 的雙曲餘切值。 在「允許主機」欄位中，輸入Dispatcher的主機名以允許其作為引用者，然後按一下 **保存**。 條目的格式為https://&#39;[伺服器]:[埠]「 」。

#### 整合Adobe Target {#integrate-adobe-target}

如果您的客戶所提供的體驗不吸引人，則他們可能會放棄互動式通信。 雖然這讓客戶感到沮喪，但也會增加您組織的支援量和成本。 確定並提供適當的客戶體驗以提高轉換率，這一點非常關鍵，也極具挑戰性。 表AEM單是此問題的關鍵。

表AEM單與Adobe Experience Cloud解決方案Adobe Target整合，跨多個數字渠道提供個性化且引人入勝的客戶體驗。 用Adobe Target來個性化互動交流， [整合Adobe Target與AEM Forms](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms)。

#### 為表單資料模型配置SSL通信  {#configure-ssl-communcation-for-form-data-model}

可以為表單資料模型啟用SSL通信。 要為表單資料模型啟用SSL通信，請在啟動任何AEM Forms實例之前，將證書添加到所有實例的Java™信任儲存中。 您可以運行以下命令來添加證書：

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## 後續步驟 {#next-steps}

您已將環境配置為使用互動式通信和通信管理功能。 現在，使用該功能的步驟如下：

* [通信管理概述](/help/forms/using/interactive-communications-overview.md)

* [建立互動式通信](../../forms/using/create-interactive-communication.md)

* [建立信件管理信函](../../forms/using/create-letter.md)
