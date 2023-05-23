---
title: 在OSGi上安裝和配置以Forms為中心的工作流
seo-title: Installing and Configuring Forms-centric workflow on OSGi
description: 安裝和配置AEM Forms互動通信，以建立業務通信、文檔、聲明、利益通知、營銷郵件、帳單和歡迎套件。
seo-description: Install and configure AEM Forms Interactive Communications to create business correspondences, documents, statements, benefit notices, marketing mails, bills, and welcome kits.
uuid: 1ceae822-215a-4b83-a562-4609a09c3a54
topic-tags: installing
discoiquuid: de292a19-07db-4ed3-b13a-7a2f1cd9e0dd
docset: aem65
role: Admin
exl-id: 4b24a38a-c1f0-4c81-bb3a-39ce2c4892b1
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1612'
ht-degree: 6%

---

# 在OSGi上安裝和配置以Forms為中心的工作流{#installing-and-configuring-forms-centric-workflow-on-osgi}

## 簡介 {#introduction}

企業從多個表單、後端系統和其他資料源收集和處理資料。 資料處理涉及審核和批准過程、重複性任務和資料歸檔。 例如，複查表單並將其轉換為PDF文檔。 手動完成時，重複性任務可能需要大量的時間和資源。

您可以使用 [基於OSGi的以Forms為中心的工作流](../../forms/using/aem-forms-workflow.md) 快速構建基於表單的自適應工作流。 這些工作流可幫助您自動執行審核和批准工作流、業務流程工作流和其他重複性任務。 這些工作流還幫助處理文檔(建立、匯編、分發和歸檔PDF文檔，添加數字簽名以限制對文檔的訪問，對條形碼表單進行解碼等)，並將Adobe Sign簽名工作流與表單和文檔一起使用。

一旦設定，用戶提交表單或互動式通信時，可以手動觸發這些工作流以完成定義的進程或以寫程式方式運行。 該功能包含在AEM Forms附加軟體包中。

AEM Forms是一個強大的企業級平台。 以Forms為中心的OSGi工作流只是AEM Forms的能力之一。 有關權能的完整清單，請參見 [AEM Forms簡介](introduction-aem-forms.md)。

>[!NOTE]
>
>在OSGi上，使用以Forms為中心的工作流，您可以快速構建和部署OSGi堆棧上各種任務的工作流，而無需在JEE堆棧上安裝完整的進程管理功能。 查看 [比較](capabilities-osgi-jee-workflows.md) 以Forms為AEM中心的OSGi工作流和JEE進程管理工作流，以瞭解功能的不同之處和相似性。
>
>比較後，如果選擇在JEE堆棧上安裝「進程管理」功能，請參閱 [在JEE上安裝或升級AEM Forms](/help/forms/home.md) 有關安裝和配置JEE堆棧和進程管理功能的詳細資訊。

## 部署拓撲 {#deployment-topology}

AEM Forms附加軟體包是部署到的應AEM用程式 您至少只需一個AEM作者或處理實例（生產作者）即可運行以Forms為中心的OSGi功能工作流。 處理實例是 [AEM作者](/help/forms/using/hardening-securing-aem-forms-environment.md) 實例。 不要在生產作者上執行任何實際創作，如建立工作流或自適應表單。

以下拓撲是指示性拓撲，用於運行AEM Forms互動式通信、通信管理、AEM Forms資料捕獲和以Forms為中心的OSGi功能工作流。 有關拓撲的詳細資訊，請參見 [用於AEM Forms的體系結構和部署拓撲](/help/forms/using/aem-forms-architecture-deployment.md)。

![推薦拓撲](assets/recommended-topology.png)

AEM Forms以Forms為中心的工作流在OSGi上AEM運行「收件箱」AEM和「工作流模型建立UI」，在AEM Forms的作者實例上運行。

## 系統要求 {#system-requirements}

>[!NOTE]
>
>跳至 [後續步驟](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps) 文檔的「 」部分，如中所述，如果您已在OSGi上安裝了AEM Forms [安裝和配置資料捕獲功能](../../forms/using/installing-configuring-aem-forms-osgi.md) 文章。

在OSGi上開始安裝和配置以Forms為中心的工作流之前，請確保：

* 硬體和軟體基礎架構已到位。 有關支援的硬體和軟體的詳細清單，請參見 [技術要求](/help/sites-deploying/technical-requirements.md)。

* 實例的安AEM裝路徑不包含空格。
* 實例AEM已啟動並正在運行。 在術AEM語中，「實例」是在作者或發AEM布模式下在伺服器上運行的副本。 您至少需要一個AEM實例（作者或處理）才能在OSGi上運行以Forms為中心的工作流：

   * **作者**:用於AEM建立、上載和編輯內容以及管理網站的實例。 一旦內容準備好投入使用，就會將其複製到發佈實例。
   * **處理：** 處理實例是 [AEM作者](/help/forms/using/hardening-securing-aem-forms-environment.md) 實例。 可以設定Author實例並在執行安裝後對其進行強化。

   * **發佈**:通過AEMInternet或內部網路向公眾提供已發佈內容的實例。

* 滿足記憶體要求。 AEM Forms附加軟體包要求：

   * 15 GB臨時空間，用於基於MicrosoftWindows的安裝。
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

AEM Forms附加軟體包是部署到的應AEM用程式 該軟體包包含以Forms為中心的OSGi工作流和其他功能。 執行以下步驟以安裝附加軟體包：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 點一下頁首功能表中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在 **[!UICONTROL 篩選器]** 部分：
   1. 選擇 **[!UICONTROL Forms]** 從 **[!UICONTROL 解決方案]** 的子菜單。
   2. 選擇包的版本和類型。 您還可以使用 **[!UICONTROL 搜索下載]** 選項。
1. 點擊適用於您的作業系統的包名稱，選擇 **[!UICONTROL 接受EULA條款]**，然後點擊 **[!UICONTROL 下載]**。
1. 開啟[套件管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。
1. 選擇包並按一下 **[!UICONTROL 安裝]**。

   您也可以通過中列出的直接連結下載軟體包 [AEM Forms釋放](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 文章。

1. 安裝軟體包後，系統會提示您重新啟動實AEM例。 **不要立即重新啟動伺服器。** 停止AEM Forms伺服器之前，請等待ServiceEvent REGISTERED和ServiceEvent UNREGISTERED消息停止出現在 [安AEM裝目錄]/crx-quickstart/logs/error.log檔案，日誌穩定。
1. 對所有「作者」和「發佈」實例重複步驟1-7。

## 安裝後配置 {#post-installation-configurations}

AEM Forms有一些強制性和可選配置。 強制配置包括配置BouncyCastle庫和序列化代理。 可選配置包括配置調度程式和Adobe Target。

### 強制安裝後配置 {#mandatory-post-installation-configurations}

#### 配置RSA和BouncyCastle庫  {#configure-rsa-and-bouncycastle-libraries}

對所有「作者」(Author)和「發佈」(Publish)實例執行以下步驟以引導委託庫：

1. 停止基礎實AEM例。
1. 開啟 [AEM安裝目錄]\crx-quickstart\conf\sling.properties檔案進行編輯。

   如果你用了 [AEM安裝目錄]\crx-quickstart\bin\start.bat啟動AEM，然後編輯位於 [AEM根]\crx-quickstart\。

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

#### 設定 Dispatcher {#configure-dispatcher}

Dispatcher正在為快取和負載平衡工具AEM。 AEM Dispatcher還有助於保護服AEM務器免受攻擊。 通過與企業級Web服AEM務器一起使用Dispatcher，可以提高實例的安全性。 如果您使用 [調度程式](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)，然後為AEM Forms執行以下配置：

1. 配置AEM Forms的訪問：

   開啟dispatcher.any檔案進行編輯。 導航到篩選器節，然後將以下篩選器添加到篩選器節：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   保存並關閉檔案。 有關篩選器的詳細資訊，請參見 [調度程式文檔](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)。

1. 配置引用程式篩選器服務：

   以管理員身份登錄到Apache Felix配置管理器。 配置管理器的預設URL為https://&#39;server&#39;:[埠號]/system/console/configMgr。 在 **配置** 的 **Apache Sling引用篩選器** 的雙曲餘切值。 在「允許主機」欄位中，輸入調度程式的主機名以允許它作為引用者，然後按一下 **保存**。 條目的格式為 `https://'[server]:[port]'`。

#### 配置快取 {#configure-cache}

快取是一種縮短資料存取時間、減少延遲和提高輸入/輸出(I/O)速度的機制。 自適應表單快取僅儲存自適應表單的HTML內容和JSON結構，而不保存任何預填資料。 它有助於減少渲染自適應表單所需的時間。

* 在使用自適應表單快取時，使用 [調度AEM程式](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) 快取自適應表單的客戶端庫（CSS和JavaScript）。
* 在開發自定義元件時，在用於開發的伺服器上禁用自適應表單快取。

執行以下步驟來配置自適應表單快取：

1. 轉到AEMWeb控制台配置管理器 `https://'[server]:[port]'/system/console/configMgr`。
1. 按一下 **[!UICONTROL 自適應形式與交互通信Web通道配置]** 編輯其配置值。 在「編輯配置值」對話框中，指定AEM Forms伺服器實例可以快取的最大表單或文檔數 **自適應Forms** 的子菜單。 預設值為 100。按一下「**儲存**」。

   >[!NOTE]
   >
   >要禁用快取，請將「自適應Forms數」欄位中的值設定為 **0**。 在禁用或更改快取配置時，將重置快取，並從快取中刪除所有表單和文檔。

#### 配置Adobe Sign {#configure-adobe-sign}

Adobe Sign支援自適應表單的電子簽名工作流。 電子簽名有助於改善處理法律、銷售、薪資、人力資源管理及許多領域文件的工作流程。

在典型的以Adobe Sign和Forms為中心的OSGi工作流中，用戶填充自適應表單， **申請服務**。 例如，信用卡申請表和市民福利表單。當用戶填寫、提交和簽署申請表時，將啟動批准/拒絕工作流。 服務提供商在收件箱中查看AEM應用程式，並使用Adobe Sign以電子方式對應用程式進行簽名。 要啟用類似的電子簽名工作流，您可以將Adobe Sign與AEM Forms整合。

用Adobe Sign和AEM Forms, [整合Adobe Sign與AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)。

## 後續步驟 {#next-steps}

您已將環境配置為在OSGi功能上使用以Forms為中心的工作流。 現在，使用該功能的步驟如下：

* [在OSGi上使用以Forms為中心的工作流](../../forms/using/aem-forms-workflow.md)
* [工作流程步驟參考](/help/sites-developing/workflows-step-ref.md)
* [信件和互動式通信的後處理](../../forms/using/submit-letter-topostprocess.md)
