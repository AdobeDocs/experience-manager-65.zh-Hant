---
title: 使用 Brand Portal 設定 AEM Assets
seo-title: 使用 Brand Portal 設定 AEM Assets
description: 瞭解如何使用品牌入口網站設定AEM資產，以便將資產和系列發佈至品牌入口網站。
seo-description: 瞭解如何使用品牌入口網站設定AEM資產，以便將資產和系列發佈至品牌入口網站。
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
translation-type: tm+mt
source-git-commit: fb59bd52be86894e93063f4b7c32aef0ed23250b
workflow-type: tm+mt
source-wordcount: '1748'
ht-degree: 42%

---


# 使用 Brand Portal 設定 AEM Assets {#configure-integration-65}

Adobe Experience Manager (AEM) Assets 是透過 Adobe I/O 以 Brand Portal 設定，這種方式會取得 IMS Token 來使 Brand Portal 租用戶獲得授權。

>[!NOTE]
>
>AEM 6.5.4.0及更新版本支援透過Adobe I/O以品牌入口網站設定AEM資產。
>
>之前，品牌入口網站是透過舊版OAuth閘道在傳統使用者介面中設定，該閘道使用JWT代號交換來取得IMS存取代號以進行授權。
>
>自2020年4月6日起，不再支援透過舊版OAuth進行的設定，並變更為透過Adobe I/O進行設定。


>[!TIP]
>
>***僅限現有客戶***
>
>建議您繼續使用現有的舊版OAuth閘道設定。 萬一您遇到舊版OAuth閘道設定的問題，請刪除現有的設定，並透過Adobe I/O建立新的設定。



本說明說明下列兩個使用案例：
* [新配置](#configure-new-integration-65): 如果您是新的品牌入口網站使用者，並想要使用品牌入口網站設定您的AEM Assets作者例項，則可以在Adobe I/O上建立新的設定。
* [升級配置](#upgrade-integration-65): 如果您是現有的品牌入口網站使用者，且AEM Assets作者實例在舊版OAuth閘道上設定了品牌入口網站，建議您刪除現有的設定並在Adobe I/O上建立新的設定。

提供的資訊基於以下假設：閱讀本「說明」的人熟悉下列技術：

* 安裝、設定和管理Adobe Experience Manager和AEM套件

* 使用Linux和Microsoft Windows作業系統

## 必備條件 {#prerequisites}

您需要下列項目才能使用 Brand Portal 設定 AEM Assets：

* 具有最新Service Pack的AEM Assets作者執行個體。
* Brand Portal 租用戶 URL。
* 在 Brand Portal 租用戶的 IMS 組織具有系統管理員權限的使用者。


[下載並安裝AEM 6.5](#aemquickstart)

[下載並安裝最新的AEM Service Pack](#servicepack)

### 下載並安裝AEM 6.5 {#aemquickstart}

建議您讓AEM 6.5來設定AEM作者例項。 如果您沒有啟動並執行AEM，請從下列位置下載：

* 如果您是現有的AEM客戶，請從 [Adobe授權網站下載AEM 6.5](http://licensing.adobe.com)。

* 如果您是Adobe合作夥伴，請使用 [Adobe合作夥伴培訓計畫](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) ，申請AEM 6.5。

下載AEM後，如需設定AEM作者例項的指示，請參閱「部署 [與維護」](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/deploy.html#defaultlocalinstall)。

### 下載並安裝AEM最新Service Pack {#servicepack}

如需詳細指示，請參閱

* [AEM 6.5 Service Pack發行說明](https://helpx.adobe.com/tw/experience-manager/6-5/release-notes/sp-release-notes.html)

**如果您找不到最新的AEM套件或Service Pack** ，請連絡客戶服務。

## 建立設定 {#configure-new-integration-65}

如果您是第一次使用品牌入口網站設定AEM資產，請在所列順序中執行下列步驟：
1. [取得公開憑證](#public-certificate)
1. [建立 Adobe I/O 整合項目](#createnewintegration)
1. [建立 IMS 帳戶設定](#create-ims-account-configuration)
1. [設定雲端服務](#configure-the-cloud-service)
1. [測試設定](#test-integration)

### 建立 IMS 設定 {#create-ims-configuration}

IMS 設定會以 AEM Assets 作者例項驗證您的 Brand Portal 租用戶。

IMS 設定包括兩個步驟：

* [取得公開憑證](#public-certificate)
* [建立 IMS 帳戶設定](#create-ims-account-configuration)

### 取得公開憑證 {#public-certificate}

公開憑證可讓您在 Adobe I/O 上驗證設定檔。

1. 登入您的AEM Assets author instance預設URL: http:// localhost:4502/aem/start.html
1. From **Tools** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Security]** >> **[!UICONTROL Adobe IMS Configurations]**.

   ![Adobe IMS 帳戶設定 UI](assets/ims-config1.png)

1. Adobe IMS 設定頁面隨即開啟。

   按一下&#x200B;**[!UICONTROL 建立]**。

   這個動作會帶您前往&#x200B;**[!UICONTROL Adobe IMS 技術帳戶設定]**&#x200B;頁面。

1. 依預設，**憑證**&#x200B;標籤會開啟。

   在&#x200B;**雲端解決方案**&#x200B;中，選取 **[!UICONTROL Adobe Brand Portal]**。

1. 勾選核取方塊&#x200B;**[!UICONTROL 建立新憑證]**&#x200B;並指定憑證的&#x200B;**別名**。別名的作用是對話方塊的名稱。

1. 按一下&#x200B;**[!UICONTROL 建立憑證]**。對話方塊隨即顯示。按一下&#x200B;**[!UICONTROL 確定]**&#x200B;即可產生公開憑證。

   ![建立憑證](assets/ims-config2.png)

1. 按一下&#x200B;**[!UICONTROL 下載公開金鑰]**，並將 *AEM-Adobe-IMS.crt* 憑證檔案儲存在電腦上。憑證檔案可用於[建立 Adobe I/O 整合項目](#createnewintegration)。

   ![下載憑證](assets/ims-config3.png)

1. 按一下&#x200B;**[!UICONTROL 下一步]**。

   您會在&#x200B;**帳戶**&#x200B;標籤中建立 Adobe IMS 帳戶，但需要整合詳細資訊才能完成。暫時保持此頁面開啟。

   開啟新標籤並[建立 Adobe I/O 整合項目](#createnewintegration)，以便取得 IMS 帳戶設定的整合詳細資訊。

### 建立 Adobe I/O 整合項目 {#createnewintegration}

Adobe I/O 整合項目會產生 API 金鑰、用戶端密碼，以及設定 IMS 帳戶設定所需的裝載 (JWT)。

1. 以 Brand Portal 租用戶在 IMS 組織的系統管理員權限登入 Adobe I/O 控制台。

   預設 URL：[https://console.adobe.io/](https://console.adobe.io/)

1. 按一下&#x200B;**[!UICONTROL 建立整合項目]**。

1. 選取&#x200B;**[!UICONTROL 存取 API]**，然後按一下&#x200B;**[!UICONTROL 繼續]**。

   ![建立新整合項目](assets/create-new-integration1.png)

1. 建立新整合項目的頁面隨即開啟。

   從下拉式清單中選取您的組織。

   在 **[!UICONTROL Experience Cloud]** 中選取 **[!UICONTROL AEM Brand Portal]**，然後按一下&#x200B;**[!UICONTROL 繼續]**。

   如果您已停用「Brand Portal」選項，請確認您已在 **[!UICONTROL Adobe 服務]**&#x200B;選項上方的下拉式方塊中選取正確的組織。如果您不清楚自己的組織為何，請聯絡您的管理員。

   ![建立整合項目](assets/create-new-integration2.png)

1. 指定整合項目的名稱和說明。按一下&#x200B;**[!UICONTROL 從電腦選取檔案]**，並上傳在[取得公開憑證](#public-certificate)區段中下載的 `AEM-Adobe-IMS.crt` 檔案 。

1. 選取組織的設定檔。

   或者，選取預設設定檔 **[!UICONTROL Assets Brand Portal]**，然後按一下&#x200B;**[!UICONTROL 建立整合項目]**。整合項目隨即建立。

1. 按一下&#x200B;**[!UICONTROL 繼續前往整合詳細資訊]**，以便檢視整合資訊。

   複製 **[!UICONTROL API 金鑰]**

   按一下&#x200B;**[!UICONTROL 擷取用戶端密碼]**&#x200B;並複製用戶端密碼金鑰。

   ![整合項目的 API 金鑰、用戶端密碼和裝載資訊](assets/create-new-integration3.png)

1. 導覽至 **[!UICONTROL JWT]** 標籤，並複製 **[!UICONTROL JWT 裝載]**。

   API 金鑰、用戶端密碼金鑰和 JWT 裝載資訊將用來建立 IMS 帳戶設定。

### 建立 IMS 帳戶設定 {#create-ims-account-configuration}

請確認您已執行下列步驟：

* [取得公開憑證](#public-certificate)
* [建立 Adobe I/O 整合項目](#createnewintegration)

**建立 IMS 帳戶設定的步驟：**

1. 開啟 IMS 設定頁面&#x200B;**[!UICONTROL 帳戶]**&#x200B;標籤。在[取得公開憑證](#public-certificate)這一節的結尾，您已保持此頁面開啟。

1. 指定 IMS 帳戶的&#x200B;**[!UICONTROL 標題]**。

   在&#x200B;**[!UICONTROL 授權伺服器]**，輸入 URL：[https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   貼上您在[建立 Adobe I/O 整合項目](#createnewintegration)結尾複製的 API 金鑰、用戶端密碼和 JWT 裝載。

   按一下&#x200B;**[!UICONTROL 建立]**。

   整合項目隨即建立。

   ![IMS 帳戶設定](assets/create-new-integration6.png)


1. 選取 IMS 設定，然後按一下&#x200B;**[!UICONTROL 檢查健康狀態]**。對話方塊隨即顯示。

   按一下&#x200B;**[!UICONTROL 檢查]**。成功連線時，*已成功擷取 Token* 訊息就會顯示。

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>您只能有一個IMS設定。 請勿建立多個 IMS 組態。
>
>確保IMS配置通過健康檢查。 如果配置未通過健康檢查，則無效。 您必須刪除它並建立新的有效設定。


### 設定雲端服務 {#configure-the-cloud-service}

執行下列步驟以建立 Brand Portal 雲端服務設定：

1. 登入您的AEM Assets作者實例

   預設URL: http:// localhost:4502/aem/start.html
1. From **Tools** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Cloud Services >> AEM Brand Portal]**.

   「Brand Portal 設定」頁面隨即開啟。

1. 按一下&#x200B;**[!UICONTROL 建立]**。

1. 指定設定的&#x200B;**[!UICONTROL 標題]**。

   選取您在[建立 IMS 帳戶設定](#create-ims-account-configuration)步驟中建立的 IMS 設定。

   在&#x200B;**[!UICONTROL 服務 URL]**&#x200B;中，輸入您的 Brand Portal 租用戶 URL。

   ![](assets/create-cloud-service.png)

1. 按一下&#x200B;**[!UICONTROL 儲存並關閉]**。雲端設定此時已建立。您的AEM Assets作者實例現在已與品牌入口網站租用戶整合。

### 測試設定 {#test-integration}

1. 登入您的AEM Assets作者實例

   預設URL: http:// localhost:4502/aem/start.html

1. From **Tools** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Deployment >> Replication]**.

   ![](assets/test-integration1.png)

1. 複製頁開啟。

   按一 **[!UICONTROL 下作者上的代理]**。

   ![](assets/test-integration2.png)

1. 為每個租用戶建立四個複製代理。

   找到您品牌門戶租用戶的複製代理。

   按一下複製代理URL。

   ![](assets/test-integration3.png)


   >[!NOTE]
   >
   >複製代理並行工作，共用作業分配，使發佈速度提高了原始速度的四倍。 在設定雲端服務後，不需要額外的設定，就可啟用依預設啟用的複製代理，以啟用多個資產的並行發佈。

   >[!NOTE]
   >
   >請避免禁用任何複製代理，因為這可能導致某些資產的複製失敗。


1. To verify the connection between AEM Assets author and Brand Portal, click **[!UICONTROL Test Connection]**.

   ![](assets/test-integration4.png)

1. 查看測試結果底部以驗證複製是否成功。

   ![](assets/test-integration5.png)

   >[!NOTE]
   >
   >複製代理並行工作，共用作業分配，使發佈速度提高了原始速度的四倍。 在設定雲端服務後，不需要額外的設定，就可啟用依預設啟用的複製代理，以啟用多個資產的並行發佈。

1. 對所有四個複製代理逐一驗證測試結果。


   >[!NOTE]
   >
   >請避免禁用任何複製代理，因為這可能導致某些資產的複製失敗。

您的AEM Assets作者實例已成功設定品牌入口網站。 您現在可以：

* [從 AEM Assets 發佈資產到 Brand Portal](../assets/brand-portal-publish-assets.md)
* [從 AEM Assets 發佈資料夾到 Brand Portal](../assets/brand-portal-publish-folder.md)
* [從 AEM Assets 發佈集合到 Brand Portal](../assets/brand-portal-publish-collection.md)
* [設定「資產來源補充](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) 」，讓品牌入口網站使用者將資產貢獻並發佈至AEM資產。

## 升級配置 {#upgrade-integration-65}

在所列順序中執行以下步驟以升級現有配置：
1. [驗證正在運行的作業](#verify-jobs)
1. [刪除現有配置](#delete-existing-configuration)
1. [建立設定](#configure-new-integration-65)

### 驗證正在運行的作業 {#verify-jobs}

在您進行任何修改之前，請確定您的AEM Assets作者實例上沒有執行任何發佈工作。 為此，您可以驗證所有四個複製代理，並確保隊列是理想／空的。

1. 登入您的AEM Assets作者實例

   預設URL: http:// localhost:4502/aem/start.html

1. From **Tools** ![Tools](assets/tools.png) panel, navigate to **[!UICONTROL Deployment >> Replication]**.

1. 複製頁開啟。

   按一 **[!UICONTROL 下作者上的代理]**。

   ![](assets/test-integration2.png)

1. 找到您品牌門戶租用戶的複製代理。

   確保所有復 **制代理的隊列都為Idle** ，則未激活任何發佈作業。

   ![](assets/test-integration3.png)

### 刪除現有配置 {#delete-existing-configuration}

刪除現有配置時，必須運行以下檢查清單。
* 刪除所有四個複製代理
* 刪除雲端服務
* 刪除MAC用戶

1. 登入您的AEM Assets作者例項，並以管理員身分開啟CRX Lite。

   預設URL: http:// localhost:4502/crx/de/index.jsp

1. 導覽至 `/etc/replications/agents.author` 並刪除您品牌入口網站租用戶的所有4個複製代理。

   ![](assets/delete-replication-agent.png)

1. 導覽至 `/etc/cloudservices/mediaportal` 並刪除雲 **端服務設定**。

   ![](assets/delete-cloud-service.png)

1. 導覽至 `/home/users/mac` 並刪除您 **品牌入口網站的** MAC使用者。

   ![](assets/delete-mac-user.png)


您現在可 [以在Adobe I/O的AEM](#configure-new-integration-65) 6.5作者實例上建立設定。



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->

複製成功後，您可以將資產、檔案夾和系列發佈至品牌入口網站。 如需詳細資訊，請參閱：

* [將資產發佈至 Brand Portal](/help/assets/brand-portal-publish-assets.md)
* [將資料夾發佈至 Brand Portal](/help/assets/brand-portal-publish-folder.md)
* [將系列發佈至品牌入口網站](/help/assets/brand-portal-publish-collection.md)
