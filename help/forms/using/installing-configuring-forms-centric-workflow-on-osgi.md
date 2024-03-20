---
title: 在OSGi上安裝和設定以Forms為中心的工作流程
description: 安裝並設定AEM Forms互動式通訊，以建立商務對應、檔案、對帳單、福利通知、行銷郵件、帳單和歡迎套件。
topic-tags: installing
docset: aem65
role: Admin
exl-id: 4b24a38a-c1f0-4c81-bb3a-39ce2c4892b1
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1624'
ht-degree: 3%

---

# 在OSGi上安裝和設定以Forms為中心的工作流程{#installing-and-configuring-forms-centric-workflow-on-osgi}

## 簡介 {#introduction}

企業收集和處理來自多個表單、後端系統和其他數據源的數據。 數據處理涉及審查和批准程序、重複性任務和資料封存。 例如，審閱表單並將其轉換為 PDF 檔。 手動完成時，重複性任務可能需要大量時間和大量資源。

您可以在 [OSGi](../../forms/using/aem-forms-workflow.md) 上使用以Forms為中心的工作流程來快速版本編號基於自適應表單的工作流程。 這些工作流程可以幫助您自動執行審查和批准工作流程、業務流程 工作流程和其他重複性任務。 這些工作流程還有助於處理檔（創建、彙編、分發和存檔 PDF 檔，添加數位簽名以限制對文件的訪問，解碼條碼表單等），以及將Adobe Sign簽名工作流程與表單和檔一起使用。

設置完成後，可以手動觸發這些工作流程以完成定義的流程，或者在使用者提交表單或互動式通信時以程式設計方式運行。 該功能包含在AEM Forms附加元件包中。

AEM Forms是功能強大的企業級平台。 OSGi上的Forms中心工作流程只是AEM Forms功能之一。 如需完整的功能清單，請參閱 [AEM Forms簡介](introduction-aem-forms.md).

>[!NOTE]
>
>透過OSGi上的Forms工作流程，您可以在OSGi棧疊上快速建置和部署各種工作的工作流程，而不需要在JEE棧疊上安裝完整的流程管理功能。 檢視 [比較](capabilities-osgi-jee-workflows.md) OSGi上的Forms中心AEM工作流程和JEE上的流程管理，以瞭解功能的差異和相似性。
>
>比較後，如果您選擇在JEE棧疊上安裝「程式管理」功能，請參閱 [在JEE上安裝或升級AEM Forms](/help/forms/using/introduction-aem-forms.md) 以取得關於安裝和設定JEE棧疊及「程式管理」功能的詳細資訊。

## 部署拓撲 {#deployment-topology}

AEM Forms附加元件套件是部署至AEM的應用程式。 您只需要至少一個AEM作者或處理執行個體（生產作者），就能在OSGi功能上執行Forms為中心的工作流程。 處理執行個體是 [強化的AEM Author](/help/forms/using/hardening-securing-aem-forms-environment.md) 執行個體。 請勿對生產作者執行任何實際製作，例如建立工作流程或調適型表單。

下列拓朴可作為OSGi功能上執行AEM Forms互動式通訊、通訊管理、AEM Forms資料擷取和Forms工作流程的指示性拓朴。 如需有關拓朴的詳細資訊，請參閱 [AEM Forms的架構和部署拓撲](/help/forms/using/aem-forms-architecture-deployment.md).

![建議的拓朴](assets/recommended-topology.png)

OSGi上的AEM Forms Forms中心工作流程會在AEM Forms的作者執行個體上執行AEM收件匣和AEM工作流程模型建立UI。

## 系統需求 {#system-requirements}

>[!NOTE]
>
>跳至 [後續步驟](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps) 一節(如果您已在OSGi上安裝AEM Forms)，如 [安裝及設定資料擷取功能](../../forms/using/installing-configuring-aem-forms-osgi.md) 文章。

開始在OSGi上安裝及設定以Forms為中心的工作流程前，請確定：

* 硬體與軟體基礎架構已準備就緒。 如需支援的硬體和軟體的詳細清單，請參閱 [技術需求](/help/sites-deploying/technical-requirements.md).

* AEM執行個體的安裝路徑未包含空格。
* AEM執行個體已啟動且執行中。 在AEM術語中，「例項」是在伺服器上以製作或發佈模式執行的AEM的副本。 您至少需要一個AEM執行個體（製作或處理），才能在OSGi上執行Forms為中心的工作流程：

   * **作者**：用來建立、上傳和編輯內容以及管理網站的AEM執行個體。 一旦內容準備好上線，就會將其復寫到發佈執行個體。
   * **處理中：** 處理執行個體是 [強化的AEM Author](/help/forms/using/hardening-securing-aem-forms-environment.md) 執行個體。 您可以設定Author例項，並在執行安裝後加以強化。

   * **發佈**：透過網際網路或內部網路向公眾提供已發佈內容的AEM執行個體。

* 符合記憶體需求。 AEM Forms附加元件套件需要：

   * Microsoft Windows安裝專用的15 GB暫存空間。
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

AEM Forms附加元件套件是部署至AEM的應用程式。 此套件包含有關OSGi和其他功能的Forms中心工作流程。 執行以下步驟來安裝附加套件：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 選取 **[!UICONTROL Adobe Experience Manager]** 在頁首功能表中提供。
1. 在 **[!UICONTROL 篩選器]** 區段：
   1. 選取 **[!UICONTROL Forms]** 從 **[!UICONTROL 解決方案]** 下拉式清單。
   2. 選取封裝的版本和型別。 您也可以使用 **[!UICONTROL 搜尋下載]** 篩選結果的選項。
1. 選取適用於您的作業系統的套件名稱，然後選取 **[!UICONTROL 接受EULA條款]**，並選取 **[!UICONTROL 下載]**.
1. 開啟 [封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  並按一下 **[!UICONTROL 上傳套裝]** 以上傳套件。
1. 選擇包，然後按兩下安裝&#x200B;****。

   還可以通過AEM Forms版本](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)一文中[列出的直接連結下載包。

1. 安裝包后，系統會提示您重新啟動AEM 執行個體。 **不要立即重新啟動伺服器。**&#x200B;在停止 AEM Forms 伺服器之前，請等待 ServiceEvent REGISTERED 和 ServiceEvent UNREGISTERED 消息停止出現在 AEM-Installation-Directory]/crx-quickstart/logs/error.記錄檔 中[，並且日誌穩定。

   >[!NOTE]
   >
   > 建議使用 『Ctrl + C&#39; 命令重新啟動 SDK。 使用替代方法（例如，停止 Java 進程）重新啟動 AEM SDK，銷售機會可能會導致AEM開發環境不一致。

1. 對所有Author和Publish執行個體重複步驟1至7。

## 安裝後設定 {#post-installation-configurations}

AEM Forms有一些必要和選用的設定。 強制設定包括設定BouncyCastle程式庫和序列化代理程式。 選擇性設定包括設定Dispatcher和Adobe Target。

### 強制安裝後設定 {#mandatory-post-installation-configurations}

#### 設定RSA和BouncyCastle資料庫  {#configure-rsa-and-bouncycastle-libraries}

在所有Author和Publish執行個體上執行下列步驟，以啟動並委派程式庫：

1. 停止基礎AEM執行個體。
1. 開啟 [AEM安裝目錄]\crx-quickstart\conf\sling.properties檔案進行編輯。

   如果您使用 [AEM安裝目錄]\crx-quickstart\bin\start.bat以啟動AEM，然後編輯位於的sling.properties [AEM_root]\crx-quickstart\。

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

#### 設定Dispatcher {#configure-dispatcher}

Dispatcher是適用於AEM的快取與負載平衡工具。 AEM Dispatcher也有助於保護AEM伺服器不受攻擊。 您可以搭配使用Dispatcher與企業級網頁伺服器，以提高AEM執行個體的安全性。 如果您使用 [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)，然後針對AEM Forms執行下列設定：

1. 設定AEM Forms的存取權：

   開啟dispatcher.any檔案進行編輯。 導覽至篩選區段，並將下列篩選新增至篩選區段：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   儲存並關閉檔案。 如需有關篩選器的詳細資訊，請參閱 [Dispatcher檔案](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. 設定反向連結篩選服務：

   以管理員身分登入Apache Felix設定管理員。 組態管理員的預設URL為https://&#39;server&#39;：[連線埠號碼]/system/console/configMgr。 在 **設定** 功能表，選取 **Apache Sling查閱者篩選器** 選項。 在允許主機欄位中，輸入Dispatcher的主機名稱，以允許其作為反向連結，然後按一下 **儲存**. 專案的格式為 `https://'[server]:[port]'`.

#### 設定快取 {#configure-cache}

快取是縮短資料存取時間、減少延遲，以及改善輸入/輸出(I/O)速度的機制。 調適型表單快取只會儲存調適型表單的HTML內容和JSON結構，不會儲存任何預先填入的資料。 這有助於減少轉譯最適化表單所需的時間。

* 使用自適應表單快取時，請使用 [AEM傳送器](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) 快取最適化表單的使用者端資料庫（CSS和JavaScript）。
* 開發自訂元件時，請停用用於開發的伺服器上的最適化表單快取。

執行以下步驟來設定調適型表單快取：

1. 請前往AEM網頁主控台設定管理員，位於 `https://'[server]:[port]'/system/console/configMgr`.
1. 按一下 **[!UICONTROL 最適化表單和互動式通訊Web頻道設定]** 以編輯其設定值。 在編輯設定值對話方塊中，指定AEM Forms伺服器執行個體可快取在 **最適化Forms的數量** 欄位。 預設值為 100。按一下「**儲存**」。

   >[!NOTE]
   >
   >若要停用快取，請將「最適化Forms數目」欄位中的值設為 **0**. 當您停用或變更快取設定時，快取會重設，所有表單和檔案都會從快取中移除。

#### 設定Adobe Sign {#configure-adobe-sign}

Adobe Sign可啟用最適化表單的電子簽章工作流程。 電子簽名有助於改善處理法律、銷售、薪資、人力資源管理及許多領域文件的工作流程。

在OSGi上的典型Adobe Sign和Forms中心工作流程中，使用者會填寫最適化表單來 **申請服務**. 例如，信用卡申請表和市民福利表單。當使用者填寫、提交和簽署申請表單時，核准/拒絕工作流程就會開始。 服務提供者會在AEM Inbox中檢閱應用程式，並使用Adobe Sign以電子方式簽署應用程式。 若要啟用類似的電子簽章工作流程，您可以整合Adobe Sign與AEM Forms。

若要搭配AEM Forms使用Adobe Sign， [將Adobe Sign與AEM Forms整合](../../forms/using/adobe-sign-integration-adaptive-forms.md).

## 後續步驟 {#next-steps}

您已將環境設定為在OSGi功能上使用以Forms為中心的工作流程。 現在，使用功能的步驟如下：

* [在OSGi上使用以Forms為中心的工作流程](../../forms/using/aem-forms-workflow.md)
* [工作流程步驟參考](/help/sites-developing/workflows-step-ref.md)
* [信函和互動式通訊的後處理](../../forms/using/submit-letter-topostprocess.md)
