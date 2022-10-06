---
title: 在OSGi上安裝和設定以Forms為中心的工作流程
seo-title: Installing and Configuring Forms-centric workflow on OSGi
description: 安裝及設定AEM Forms互動式通訊，以建立業務通訊、檔案、對帳單、利益通知、行銷郵件、帳單和歡迎套件。
seo-description: Install and configure AEM Forms Interactive Communications to create business correspondences, documents, statements, benefit notices, marketing mails, bills, and welcome kits.
uuid: 1ceae822-215a-4b83-a562-4609a09c3a54
topic-tags: installing
discoiquuid: de292a19-07db-4ed3-b13a-7a2f1cd9e0dd
docset: aem65
role: Admin
exl-id: 4b24a38a-c1f0-4c81-bb3a-39ce2c4892b1
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1614'
ht-degree: 6%

---

# 在OSGi上安裝和設定以Forms為中心的工作流程{#installing-and-configuring-forms-centric-workflow-on-osgi}

## 簡介 {#introduction}

企業從多個表單、後端系統和其他資料來源收集和處理資料。 資料處理涉及審核和批准過程、重複性任務和資料歸檔。 例如，檢閱表單並將其轉換為PDF檔案。 手動完成時，重複性任務可能需要大量的時間和資源。

您可以使用 [Forms以OSGi為中心的工作流程](../../forms/using/aem-forms-workflow.md) 快速建立最適化表單式工作流程。 這些工作流程可協助您自動執行審核和核准工作流程、業務流程工作流程和其他重複性工作。 這些工作流程還有助於處理檔案(建立、組合、分發和歸檔PDF檔案、添加數字簽名以限制對文檔的訪問、對條碼式表單進行解碼等)，以及將Adobe Sign簽名工作流程與表單和文檔一起使用。

設定後，即可手動觸發這些工作流程以完成定義的程式，或在使用者提交表單或互動式通訊時以程式設計方式執行。 此功能包含在AEM Forms附加元件套件中。

AEM Forms是功能強大的企業級平台。 以Forms為中心的OSGi工作流程只是AEM Forms的其中一項功能。 如需功能的完整清單，請參閱 [AEM Forms簡介](introduction-aem-forms.md).

>[!NOTE]
>
>透過OSGi上以Forms為中心的工作流程，您可以快速建立並部署OSGi堆疊上各種工作的工作流程，而無須在JEE堆疊上安裝完整的流程管理功能。 請參閱 [比較](capabilities-osgi-jee-workflows.md) OSGi和JEE上以Forms為中心的AEM工作流程，以了解功能的差異與相似之處。
>
>比較後，如果您選擇在JEE堆疊上安裝「程式管理」功能，請參閱 [在JEE安裝或升級AEM Forms](/help/forms/home.md) 以取得安裝和設定JEE堆疊與「程式管理」功能的詳細資訊。

## 部署拓撲 {#deployment-topology}

AEM Forms附加元件套件是部署至AEM的應用程式。 您至少需要一個AEM製作或處理執行個體（生產製作），才能針對OSGi功能執行以Forms為中心的工作流程。 處理例項是 [強化AEM作者](/help/forms/using/hardening-securing-aem-forms-environment.md) 例項。 請勿在生產作者上執行任何實際製作作業，例如建立工作流程或最適化表單。

以下拓撲是指示性拓撲，用於在OSGi功能上運行AEM Forms Interactive Communications、通信管理、AEM Forms資料捕獲和以Forms為中心的工作流。 有關拓撲的詳細資訊，請參見 [適用於AEM Forms的架構和部署拓撲](/help/forms/using/aem-forms-architecture-deployment.md).

![推薦拓撲](assets/recommended-topology.png)

AEM Forms Forms為中心的OSGi工作流程會在AEM Forms的製作執行個體上執行AEM收件匣和AEM工作流程模型建立UI。

## 系統需求 {#system-requirements}

>[!NOTE]
>
>跳到 [後續步驟](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps) 一節，若您已按照 [安裝和配置資料捕獲功能](../../forms/using/installing-configuring-aem-forms-osgi.md) 文章。

開始在OSGi上安裝和設定以Forms為中心的工作流程之前，請確定：

* 硬體和軟體基礎架構已就緒。 有關支援的硬體和軟體的詳細清單，請參見 [技術要求](/help/sites-deploying/technical-requirements.md).

* AEM例項的安裝路徑不包含空格。
* AEM例項已啟動並執行。 在AEM術語中，「例項」是在製作或發佈模式中，於伺服器上執行的AEM復本。 您至少需要一個AEM例項（製作或處理），才能在OSGi上執行以Forms為中心的工作流程：

   * **作者**:用於建立、上傳和編輯內容及管理網站的AEM例項。 內容準備好上線後，就會複製到發佈執行個體。
   * **處理中：** 處理例項是 [強化AEM作者](/help/forms/using/hardening-securing-aem-forms-environment.md) 例項。 您可以設定製作例項，並在執行安裝後加強執行。

   * **發佈**:透過網際網路或內部網路向公眾提供已發佈內容的AEM例項。

* 滿足記憶體要求。 AEM Forms附加元件套件需要：

   * 15 GB的暫存空間，適用於Microsoft Windows安裝。
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

AEM Forms附加元件套件是部署至AEM的應用程式。 此套件包含以Forms為中心的OSGi和其他功能工作流程。 執行下列步驟以安裝附加元件套件：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 點一下頁首功能表中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在 **[!UICONTROL 篩選器]** 小節：
   1. 選擇 **[!UICONTROL Forms]** 從 **[!UICONTROL 解決方案]** 下拉式清單。
   2. 選取套件的版本和類型。 您也可以使用 **[!UICONTROL 搜尋下載]** 選項來篩選結果。
1. 點選適用於您作業系統的套件名稱，然後選取 **[!UICONTROL 接受EULA條款]**，然後點選 **[!UICONTROL 下載]**.
1. 開啟[套件管理器](https://docs.adobe.com/content/help/zh-Hant/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。
1. 選取套件，然後按一下 **[!UICONTROL 安裝]**.

   您也可以透過 [AEM Forms版本](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 文章。

1. 安裝套件後，系統會提示您重新啟動AEM執行個體。 **不要立即重新啟動伺服器。** 停止AEM Forms伺服器之前，請等到ServiceEvent REGISTERED和ServiceEvent UNECROVERD訊息停止出現在 [AEM-Installation-Directory]/crx-quickstart/logs/error.log檔案和日誌穩定。
1. 在所有「製作」和「發佈」例項上重複步驟1至7。

## 安裝後配置 {#post-installation-configurations}

AEM Forms提供一些強制和選用設定。 強制設定包括設定BouncyCastle程式庫和序列化代理。 選用的設定包括設定Dispatcher和Adobe Target。

### 強制安裝後配置 {#mandatory-post-installation-configurations}

#### 配置RSA和BouncyCastle庫  {#configure-rsa-and-bouncycastle-libraries}

對所有製作和發佈執行個體執行下列步驟以引導委派程式庫：

1. 停止基礎AEM例項。
1. 開啟 [AEM安裝目錄]\crx-quickstart\conf\sling.properties檔案進行編輯。

   若您使用 [AEM安裝目錄]\crx-quickstart\bin\start.bat以啟動AEM，然後編輯位於的sling.properties [AEM_root]\crx-quickstart\。

1. 將下列屬性新增至sling.properties檔案：

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. 儲存並關閉檔案，然後啟動AEM例項。
1. 在所有「製作」和「發佈」例項上重複步驟1至4。

#### 配置序列化代理 {#configure-the-serialization-agent}

對所有製作和發佈執行個體執行下列步驟，將套件新增至允許清單：

1. 在瀏覽器視窗中開啟AEM Configuration Manager。 預設URL為https://&#39;[伺服器]:[埠]「/system/console/configMgr。
1. 搜尋並開啟 **反序列化防火牆配置**.
1. 新增 **sun.util.calendar** 封裝至 **允許清單** 欄位。 按一下「儲存」。
1. 在所有「製作」和「發佈」例項上重複步驟1至3。

### 可選安裝後配置 {#optional-post-installation-configurations}

#### 設定 Dispatcher {#configure-dispatcher}

Dispatcher是AEM的快取和負載平衡工具。 AEM Dispatcher也有助於保護AEM伺服器免受攻擊。 您可以搭配使用Dispatcher與企業級Web伺服器，以提高AEM例項的安全性。 如果您使用 [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)，然後對AEM Forms執行下列設定：

1. 設定AEM Forms的存取權：

   開啟dispatcher.any檔案以進行編輯。 導覽至篩選區段，並將下列篩選新增至篩選區段：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   儲存並關閉檔案。 如需篩選器的詳細資訊，請參閱 [Dispatcher檔案](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. 設定反向連結篩選服務：

   以管理員身分登入Apache Felix設定管理器。 配置管理器的預設URL為https://&#39;server&#39;:[port_number]/system/console/configMgr。 在 **配置** ，選擇 **Apache Sling反向連結篩選器** 選項。 在「允許主機」欄位中，輸入Dispatcher的主機名稱，以允許它作為反向連結，然後按一下 **儲存**. 輸入的格式為 `https://'[server]:[port]'`.

#### 配置快取 {#configure-cache}

快取是一種縮短資料存取時間、減少延遲並改善輸入/輸出(I/O)速度的機制。 適用性表單快取僅儲存適用性表單的HTML內容和JSON結構，而不儲存任何預先填入的資料。 有助於縮短演算最適化表單所需的時間。

* 使用最適化表單快取時，請使用 [AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) 快取最適化表單的用戶端程式庫（CSS和JavaScript）。
* 開發自訂元件時，請在用於開發的伺服器上停用最適化表單快取。

執行下列步驟以設定最適化表單快取：

1. 前往AEM Web主控台組態管理器，網址為 `https://'[server]:[port]'/system/console/configMgr`.
1. 按一下 **[!UICONTROL 最適化表單與互動式通訊Web通道設定]** 來編輯其配置值。 在「編輯設定值」對話方塊中，指定AEM Forms伺服器執行個體可在 **適用性Forms數** 欄位。 預設值為 100。按一下「**儲存**」。

   >[!NOTE]
   >
   >若要停用快取，請將「適用性Forms數」欄位中的值設為 **0**. 當禁用或更改快取配置時，將重置快取，並從快取中刪除所有表單和文檔。

#### 設定Adobe Sign {#configure-adobe-sign}

Adobe Sign可啟用最適化表單的電子簽名工作流程。 電子簽名有助於改善處理法律、銷售、薪資、人力資源管理及許多領域文件的工作流程。

在OSGi的典型Adobe Sign和Forms工作流程案例中，使用者會填入最適化表單以 **申請服務**. 例如，信用卡申請表和市民福利表單。當用戶填寫、提交和簽名申請表時，將啟動批准/拒絕工作流。 服務提供者會在AEM收件匣中檢閱應用程式，並使用Adobe Sign以電子方式簽署應用程式。 若要啟用類似的電子簽名工作流程，您可以整合Adobe Sign與AEM Forms。

若要搭配使用Adobe Sign和AEM Forms, [整合Adobe Sign與AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

## 後續步驟 {#next-steps}

您已設定環境，在OSGi功能上使用以Forms為中心的工作流程。 現在，使用功能的步驟如下：

* [在OSGi上使用以Forms為中心的工作流程](../../forms/using/aem-forms-workflow.md)
* [工作流程步驟參考](/help/sites-developing/workflows-step-ref.md)
* [信件和互動式通信的後處理](../../forms/using/submit-letter-topostprocess.md)
