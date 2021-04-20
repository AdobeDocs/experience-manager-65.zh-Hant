---
title: 在OSGi上安裝和配置以Forms為中心的工作流
seo-title: 在OSGi上安裝和配置以Forms為中心的工作流
description: 安裝並設定AEM Forms互動式通訊，以建立商業通訊、檔案、陳述、利益通知、行銷郵件、帳單和歡迎套件。
seo-description: 安裝並設定AEM Forms互動式通訊，以建立商業通訊、檔案、陳述、利益通知、行銷郵件、帳單和歡迎套件。
uuid: 1ceae822-215a-4b83-a562-4609a09c3a54
topic-tags: installing
discoiquuid: de292a19-07db-4ed3-b13a-7a2f1cd9e0dd
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1643'
ht-degree: 4%

---


# 在OSGi{#installing-and-configuring-forms-centric-workflow-on-osgi}上安裝和配置以Forms為中心的工作流

## 簡介 {#introduction}

企業會收集和處理來自多個表單、後端系統和其他資料來源的資料。 資料處理包括審核和核准程式、重複性工作以及資料封存。 例如，檢閱表格並將其轉換為PDF檔案。 手動完成重複性任務時，可能需要大量的時間和資源。

您可以在OSGi](../../forms/using/aem-forms-workflow.md)上使用[以Forms為中心的工作流程，以快速建立以表單為基礎的調適性工作流程。 這些工作流程可協助您自動化審閱和核准工作流程、商業程式工作流程和其他重複性工作。 這些工作流程也有助於處理檔案（建立、組合、分發和封存PDF檔案、新增數位簽章以限制檔案存取、解碼條碼表格等），並搭配使用Adobe Sign簽章工作流程與表格和檔案。

設定後，這些工作流程可以手動觸發，以完成定義的程式，或在使用者提交表單或互動式通訊時以程式設計方式執行。 此功能包含在AEM Forms附加套件中。

AEM Forms是強大的企業級平台。 以Forms為中心的OSGi工作流程只是AEM Forms的功能之一。 有關功能的完整清單，請參見[AEM Forms簡介](introduction-aem-forms.md)。

>[!NOTE]
>
>有了以Forms為中心的OSGi工作流程，您就可以在OSGi堆疊上快速建立和部署各種工作的工作流程，而不需在JEE堆疊上安裝完整的流程管理功能。 請參閱OSGi和JEE流程管理Forms中心工作流程的[比較](capabilities-osgi-jee-workflows.md)，了AEM解各項功能的差異和相似性。
>
>比較後，如果您選擇在JEE堆棧上安裝「流程管理」功能，請參閱[在JEE上安裝或升級AEM Forms，以獲得有關安裝和配置JEE堆棧和「流程管理」功能的詳細資訊。](/help/forms/home.md)

## 部署拓撲{#deployment-topology}

AEM Forms附加套件是部署在上的應用程AEM式。 您至少只需要一個AEM作者或處理執行個體（生產作者），就可以針對OSGi功能執行以Forms為中心的工作流程。 處理例項是[硬化的AEM Author](/help/forms/using/hardening-securing-aem-forms-environment.md)例項。 請勿在生產作者上執行任何實際的製作，例如建立工作流程或調適性表單。

以下拓撲是指示性拓撲，用於運行AEM Forms互動式通信、通信管理、AEM Forms資料捕獲和Forms中心的OSGi功能工作流。 有關拓撲的詳細資訊，請參見[AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md)的體系結構和部署拓撲。

![推薦拓撲](assets/recommended-topology.png)

AEM Forms·Forms-以OSGi為中心的工作流AEM程在AEM Forms的「作者」例項AEM上執行「收件匣」和「工作流程模型建立UI」。

## 系統要求{#system-requirements}

>[!NOTE]
>
>如果您已按照[安裝和配置資料捕獲功能](../../forms/using/installing-configuring-aem-forms-osgi.md)文章中的說明，將AEM Forms安裝在OSGi上，請跳至文檔的[Next steps](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps)部分。

在OSGi上開始安裝和配置以Forms為中心的工作流程之前，請確保：

* 硬體和軟體基礎架構已就緒。 有關支援的硬體和軟體的詳細清單，請參見[技術要求](/help/sites-deploying/technical-requirements.md)。

* 實例的安AEM裝路徑不包含空格。
* 實AEM例已啟動並運行。 在術AEM語中，「例項」是在作者或發AEM布模式下在伺服器上執行的副本。 您至少需要一個例AEM項（作者或處理）才能在OSGi上執行以Forms為中心的工作流程：

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

AEM Forms附加套件是部署在上的應用程AEM式。 此套件包含以Forms為中心的OSGi和其他功能工作流程。 執行下列步驟以安裝附加元件套件：

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

#### 配置Dispatcher {#configure-dispatcher}

Dispatcher是適用於的快取和負載平衡工AEM具。 AEM Dispatcher還有助於保護服AEM務器免受攻擊。 您可以搭配使用Dispatcher和AEM企業級Web伺服器，以提高實例的安全性。 如果使用[Dispatcher](https://helpx.adobe.com/tw/experience-manager/dispatcher/using/dispatcher-configuration.html)，則對AEM Forms執行以下配置：

1. 配置AEM Forms的訪問：

   開啟dispatcher.any檔案以進行編輯。 導覽至篩選區段，並將下列篩選新增至篩選區段：

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   儲存並關閉檔案。 有關篩選器的詳細資訊，請參見[Dispatcher documentation](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)。

1. 設定反向連結篩選服務：

   以管理員身分登入Apache Felix組態管理員。 配置管理器的預設URL為https://&#39;server&#39;:[port_number]/system/console/configMgr。 在&#x200B;**Configurations**&#x200B;選單中，選取&#x200B;**Apache Sling Referrer Filter**&#x200B;選項。 在「允許主機」欄位中，輸入調度程式的主機名以允許它作為反向連接，然後按一下「保存」。 ****&#x200B;條目的格式為`https://'[server]:[port]'`。

#### 配置快取{#configure-cache}

快取是一種機制，可縮短資料存取時間、減少延遲，並改善輸入／輸出(I/O)速度。 最適化表單快取只儲存最適化表單的HTML內容和JSON結構，而不儲存任何預先填入的資料。 它有助於縮短轉換最適化表單所需的時間。

* 在使用最適化表單快取時，請使用AEM[ Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html)來快取最適化表單的用戶端程式庫（CSS和JavaScript）。
* 在開發自訂元件時，請在用於開發的伺服器上停用最適化表單快取。

執行以下步驟以配置自適應表單快取：

1. 轉至AEM`https://'[server]:[port]'/system/console/configMgr`的Web控制台配置管理器。
1. 按一下&#x200B;**[!UICONTROL 自適應表單和互動式通信Web通道配置]**&#x200B;以編輯其配置值。 在編輯配置值對話框中，在&#x200B;**Number of AdaptiveForms**&#x200B;欄位中指定AEM Forms伺服器實例可以快取的表單或文檔的最大數量。 預設值為 100。按一下「**儲存**」。

   >[!NOTE]
   >
   >要禁用快取，請將「Number of AdaptiveForms」（自適應性資料）欄位中的值設定為&#x200B;**0**。 當禁用或更改快取配置時，將重置快取，並從快取中刪除所有表單和文檔。

#### 配置Adobe Sign{#configure-adobe-sign}

Adobe Sign為調適性表單提供電子簽名工作流程。 電子簽名可改善處理法律、銷售、薪資、人力資源管理等領域檔案的工作流程。

在OSGi方案上以Adobe Sign和Forms為中心的典型工作流中，用戶填充適應於&#x200B;**服務**&#x200B;的表單。 例如，信用卡申請和公民福利表。 當使用者填寫、提交及簽署申請表格時，就會啟動核准／拒絕工作流程。 服務提供商會在「收件箱」中審AEM核應用程式，並使用Adobe Sign電子簽名應用程式。 若要啟用類似的電子簽名工作流程，您可以將Adobe Sign與AEM Forms整合。

要將Adobe Sign與AEM Forms結合，[將Adobe Sign與AEM Forms整合。](../../forms/using/adobe-sign-integration-adaptive-forms.md)

## 後續步驟{#next-steps}

您已經配置了在OSGi功能上使用以Forms為中心的工作流的環境。 現在，使用此功能的步驟如下：

* [在OSGi上使用以Forms為中心的工作流程](../../forms/using/aem-forms-workflow.md)
* [工作流程步驟參考](/help/sites-developing/workflows-step-ref.md)
* [信函的後處理和互動式通信](../../forms/using/submit-letter-topostprocess.md)

