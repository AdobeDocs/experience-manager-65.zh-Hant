---
title: 在OSGi上安裝和設定以表單為中心的工作流程
seo-title: 在OSGi上安裝和設定以表單為中心的工作流程
description: 安裝和設定AEM Forms互動式通訊，以建立商業通訊、檔案、陳述、權益通知、行銷郵件、帳單和歡迎套件。
seo-description: 安裝和設定AEM Forms互動式通訊，以建立商業通訊、檔案、陳述、權益通知、行銷郵件、帳單和歡迎套件。
uuid: 1ceae822-215a-4b83-a562-4609a09c3a54
topic-tags: installing
discoiquuid: de292a19-07db-4ed3-b13a-7a2f1cd9e0dd
docset: aem65
translation-type: tm+mt
source-git-commit: 3226edb575de3d9f8bff53f5ca81e2957f37c544

---


# 在OSGi上安裝和設定以表單為中心的工作流程{#installing-and-configuring-forms-centric-workflow-on-osgi}

## 簡介 {#introduction}

企業會收集和處理來自多個表單、後端系統和其他資料來源的資料。 資料處理包括審核和核准程式、重複性工作以及資料封存。 例如，檢閱表單並將其轉換為PDF檔案。 手動完成重複性任務時，可能需要大量的時間和資源。

您可以在OSGi上 [使用以表單為中心的工作流程](../../forms/using/aem-forms-workflow.md) ，快速建立以表單為主的調適性工作流程。 這些工作流程可協助您自動化審閱和核准工作流程、商業程式工作流程和其他重複性工作。 這些工作流程也有助於處理檔案（建立、組合、分發和封存PDF檔案、新增數位簽章以限制檔案存取、解碼條碼表格等），並搭配表格和檔案使用Adobe Sign簽章工作流程。

設定後，這些工作流程可以手動觸發，以完成定義的程式，或在使用者提交表單或互動式通訊時以程式設計方式執行。 此功能已包含在AEM Forms附加套件中。

AEM Forms是功能強大的企業級平台。 OSGi上的表單導向工作流程只是AEM Forms的功能之一。 如需完整的功能清單，請參 [閱「AEM Forms簡介」](../../forms/using/introduction-aem-forms.md)。

>[!NOTE]
>
>有了OSGi上以表單為中心的工作流程，您就可以在OSGi堆疊上快速建立和部署各種工作的工作流程，而不需在JEE堆疊上安裝完整的流程管理功能。 檢視OSGi [上的](../../forms/using/capabilities-osgi-jee-workflows.md) 「Forms-centric AEM Workflows」與JEE上的「Process Management」的比較，以瞭解功能的不同與相似之處。
>
>比較後，如果您選擇在JEE堆疊上安裝「流程管理」功能，請參閱在JEE上安裝或升級AEM Forms [](/help/forms/home.md) ，以取得有關安裝和設定JEE堆疊和「流程管理」功能的詳細資訊。

## 部署拓撲 {#deployment-topology}

AEM Forms附加元件套件是部署在AEM上的應用程式。 您至少只需要一個AEM作者或處理執行個體（生產作者），就可以在OSGi功能上執行以表單為中心的工作流程。 處理例項是硬 [化的AEM Author例項](/help/forms/using/hardening-securing-aem-forms-environment.md) 。 請勿在生產作者上執行任何實際的製作，例如建立工作流程或調適性表單。

以下拓撲是指示性拓撲，可針對OSGi功能執行AEM Forms Interactive Communications、Conversence Management、AEM Forms資料擷取和Forms-Centric工作流程。 如需拓撲的詳細資訊，請參 [閱「AEM Forms的架構和部署拓撲」](/help/forms/using/aem-forms-architecture-deployment.md)。

![推薦拓撲](assets/recommended-topology.png)

OSGi上的AEM Forms以表單為中心的工作流程會在AEM Forms的「作者」例項上執行AEM Inbox和AEM Workflow Model建立UI。

## 系統需求 {#system-requirements}

>[!NOTE]
>
>請跳至文 [件的](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps) 「後續步驟」區段，如果您已在OSGi上安裝AEM Forms，如安裝與設 [定資料擷取功能文章所述](../../forms/using/installing-configuring-aem-forms-osgi.md) 。

在OSGi上開始安裝和設定以表單為中心的工作流程之前，請確定：

* 硬體和軟體基礎架構已就緒。 如需支援硬體和軟體的詳細清單，請參閱 [技術需求](/help/sites-deploying/technical-requirements.md)。

* AEM例項的安裝路徑不包含空格。
* AEM例項已啟動並執行。 在AEM術語中，「例項」是在作者或發佈模式下伺服器上執行的AEM復本。 您至少需要一個AEM例項（作者或處理），才能在OSGi上執行以表單為中心的工作流程：

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

AEM Forms附加元件套件是部署在AEM上的應用程式。 此套件包含OSGi和其他功能的表單導向工作流程。 執行下列步驟以安裝附加元件套件：

1. 以管理員身分登入 [AEM伺服器](https://localhost:4502) ，並開啟套 [件共用](https://localhost:4502/crx/packageshare)。 您需要Adobe ID才能登入套件共用。
1. 在 [AEM套件共用](https://localhost:4502/crx/packageshare/login.html)、搜尋 **AEM 6.5 Forms附加套件**&#x200B;或最新服務套件中&#x200B;**，按一下適用於您作業系統的套件，然後按一下「下******&#x200B;載」。 閱讀並接受授權合約，然後按一下「 **確定**」。 下載開始。 下載後，「已下 **載** 」一詞會出現在套件旁。

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

#### 配置Dispatcher {#configure-dispatcher}

Dispatcher是AEM的快取和負載平衡工具。 AEM Dispatcher也可協助保護AEM伺服器不受攻擊。 您可搭配使用Dispatcher與企業級Web伺服器，以提高AEM例項的安全性。 如果您使 [用Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)，請針對AEM Forms執行下列設定：

1. 設定AEM Forms的存取權：

   開啟dispatcher.any檔案以進行編輯。 導覽至篩選區段，並將下列篩選新增至篩選區段：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   儲存並關閉檔案。 有關篩選器的詳細資訊，請參 [閱Dispatcher文檔](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)。

1. 設定反向連結篩選服務：

   以管理員身分登入Apache Felix組態管理員。 配置管理器的預設URL是https://[server]:[port_number]/system/console/configMgr。 在「設 **定** 」選單中，選取 **Apache Sling Referrer Filter** 選項。 在「允許主機」欄位中，輸入調度程式的主機名以允許它作為反向連接，然後按一下「保 **存」**。 條目的格式為 `https://[server]:[port]`。

#### 配置快取 {#configure-cache}

快取是一種機制，可縮短資料存取時間、減少延遲，並改善輸入／輸出(I/O)速度。 最適化表單快取只儲存最適化表單的HTML內容和JSON結構，而不儲存任何預先填入的資料。 它有助於縮短轉換最適化表單所需的時間。

* 在使用最適化表單快取時，請使用 [AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) ，快取最適化表單的用戶端程式庫（CSS和JavaScript）。
* 在開發自訂元件時，請在用於開發的伺服器上停用最適化表單快取。

執行以下步驟以配置自適應表單快取：

1. 請前往AEM網頁主控台組態管理器(網址 `https://[server]:[port]/system/console/configMgr`)。
1. 按一下 **Adaptive Form Configuration Service** （自適應表單配置服務）以編輯其配置值。 在「編輯設定值」對話方塊中，在「最適化表單數」欄位中指定AEM Forms伺服器執行個體可快取的表 **單或檔案數上限** 。 預設值為100。 按一下&#x200B;**「儲存」**。

   >[!NOTE]
   >
   >要禁用快取，請將「最適化表單數」欄位中的值設定為 **0**。 當禁用或更改快取配置時，將重置快取，並從快取中刪除所有表單和文檔。

#### 設定Adobe Sign {#configure-adobe-sign}

Adobe Sign可針對最適化表單啟用電子簽名工作流程。 電子簽名可改善處理法律、銷售、薪資、人力資源管理等領域檔案的工作流程。

在OSGi案例上典型的Adobe Sign和Forms導向工作流程中，使用者會填寫最適化表單以 **申請服務**。 例如，信用卡申請和公民福利表。 當使用者填寫、提交及簽署申請表格時，就會啟動核准／拒絕工作流程。 服務供應商會在AEM Inbox中審核應用程式，並使用Adobe Sign以電子方式簽署應用程式。 若要啟用類似的電子簽名工作流程，您可以將Adobe Sign與AEM Forms整合。

若要搭配使用Adobe Sign和AEM Forms，請 [將Adobe Sign與AEM Forms整合](../../forms/using/adobe-sign-integration-adaptive-forms.md)。

## 後續步驟 {#next-steps}

您已設定環境，以便在OSGi功能上使用以表單為中心的工作流程。 現在，使用此功能的步驟如下：

* [在OSGi上使用以表單為中心的工作流程](../../forms/using/aem-forms-workflow.md)
* [工作流程步驟參考](/help/sites-developing/workflows-step-ref.md)
* [信函的後處理和互動式通信](../../forms/using/submit-letter-topostprocess.md)

