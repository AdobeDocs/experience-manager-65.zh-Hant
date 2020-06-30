---
title: 管理 [!DNL Adobe Stock] 資產 [!DNL Adobe Experience Manager Assets]。
description: 從內部搜尋、擷取、授 [!DNL Adobe Stock] 權及管理資產 [!DNL Adobe Experience Manager]。 將授權資產當做任何其他數位資產使用。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 97e17df1f79450b5aed5867633c129a1c21a17ac
workflow-type: tm+mt
source-wordcount: '1113'
ht-degree: 11%

---


# 使用 [!DNL Adobe Stock] 資產於 [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

組織可將其企 [!DNL Adobe Stock] 業計畫與 [!DNL Experience Manager Assets] 其強大的資產管理功能整合，以確保授權資產廣泛適用於其創意和行銷專案 [!DNL Experience Manager]。

[!DNL Adobe Stock] 服務可讓設計人員和企業針對其所有創意專案，取用數百萬個高品質、優質且免版稅的像片、向量、插圖、視訊、範本和3D資產。 [!DNL Experience Manager] 使用者可以快速尋找、預覽和授權儲 [!DNL Adobe Stock] 存在的資產，而 [!DNL Experience Manager]不需離開介 [!DNL Experience Manager] 面。

## 必備條件 {#prerequisites}

整合需要企 [業版Adobe Stock計畫](https://stockenterprise.adobe.com/)[!DNL Experience Manager] 和6.5或更新版本。 如需 [!DNL Experience Manager] 6.5 Service Pack的詳細資訊，請參閱這些 [發行說明](/help/release-notes/sp-release-notes.md)。

## 整合 [!DNL Experience Manager] 和 [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

若要允許與之 [!DNL Experience Manager] 間的 [!DNL Adobe Stock]通訊，請在中建立IMS組態和 [!DNL Adobe Stock] 組態 [!DNL Experience Manager]。

>[!NOTE]
>
>只有組 [!DNL Experience Manager] 織的管 [!DNL Admin Console] 理員和管理員才能執行整合，因為它需要管理員權限。

### Create an IMS configuration {#create-an-ims-configuration}

1. Click on [!DNL Experience Manager] logo. 導覽至「 **[!UICONTROL 工具]** >安 **[!UICONTROL 全]** > **[!UICONTROL Adobe IMS設定」]**。按一 **[!UICONTROL 下「建立]** 」，然後選 **[!UICONTROL 取「雲端解決方案]** > **[!UICONTROL Adobe Stock]**」。
1. 重複使用現有證書或選擇「 **[!UICONTROL 建立新證書」]**。
1. 按一下&#x200B;**[!UICONTROL 建立憑證]**。建立後，請下載公開金鑰。 按一下&#x200B;**[!UICONTROL 下一步]**。
1. 將下載的公開金鑰新增至您的服 [!DNL Adobe Developer Console] 務帳戶。 按一下&#x200B;**[!UICONTROL 下一步]**。讓「 [!UICONTROL Adobe IMS技術帳戶設定」畫面保持開啟] ，以便在不久後提供值。
1. 存取 [Adobe Developer Console](https://console.adobe.io)。 請確定您的帳戶擁有需要整合之組織的管理員權限。
1. 按一 **[!UICONTROL 下「建立新專案]** 」，然後按 **[!UICONTROL 一下「新增API」]**。 從 **[!UICONTROL 您可用的API清單]** 中選擇Adobe Stock 。 選 [!UICONTROL 擇OAUTH 2.0 Web]。 設定並複製顯示的各種值。
1. In [!DNL Experience Manager] provide the values in the fields titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. 有關這 [些值的詳細資訊](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md)，請參見JWT驗證快速入門。

<!-- TBD: Update the URL when the new URL is available. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

### 在中 [!DNL Adobe Stock] 建立配置 [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. 按一 **[!UICONTROL 下「建立]** 」以建立組態，並將它與您現有的IMS組態建立關聯。 選擇 `PROD` 作為環境參數。
1. 在「 **[!UICONTROL 授權資產路徑]** 」欄位中，保留原狀位置。 請勿變更資產的儲存位 [!DNL Adobe Stock] 置。
1. 新增所有必要屬性以完成建立。 Click **[!UICONTROL Save &amp; Close]**.
1. 新增 [!DNL Experience Manager] 可授權資產的使用者或群組。

>[!NOTE]
>
>如果有多個配 [!DNL Adobe Stock] 置，請在「用戶首選項」面板中選 [!UICONTROL 擇所需的配置] 。 按一 *下使用者* 介面右上角的 [!DNL Experience Manager] User標誌。

## 使用及管 [!DNL Adobe Stock] 理 [!DNL Experience Manager] {#usemanage}

使用這項功能，組織可以允許其使用者在中使用 [!DNL Adobe Stock] 資產 [!DNL Experience Manager Assets]。 使用者可在使 [!DNL Experience Manager] 用者介面中搜尋資產， [!DNL Adobe Stock] 並授權所需的資產。

在授權 [!DNL Adobe Stock] 資產後，就 [!DNL Experience Manager]可像一般資產一樣使用及管理資產。 用戶 [!DNL Experience Manager]可以搜索和預覽資產； 複製及發佈資產； 以股份形式分享資 [!DNL Brand Portal]產； 透過案頭應用程式存取及使 [!DNL Experience Manager] 用資產； 等等。

![搜尋Adobe Stock資產並篩選Adobe Experience Manager工作區的結果](assets/adobe-stock-search-results-workspace.png)

*圖： 從介面[!DNL Adobe Stock]搜尋資產並篩選結[!DNL Experience Manager]果。*

**A.**[!DNL Adobe Stock] 搜尋與已提供 ID 之資產的類似資產。**B.** 搜尋與您選取的型態或方向相符的資產。**C.** 搜尋一或多個支援的資產類型 **D.** 開啟或收合篩選器窗格 **E.** 在 中為選取的資產授權並加以儲存 [!DNL Experience Manager]**F.**[!DNL Experience Manager] 將資產儲存在 中並加上浮水印 **G.**[!DNL Adobe Stock] 在 網站上探索與選取的資產類似的資產 **H.**[!DNL Adobe Stock] 在 網站上檢視選取的資產 **I.** 搜尋結果中選取的資產數目 **J.** 在卡片檢視與清單檢視之間切換

### 尋找資產 {#find-assets}

您的 [!DNL Experience Manager] 使用者可以同時在和中搜尋 [!DNL Experience Manager] 資產 [!DNL Adobe Stock]。 當搜索位置不限於時， [!DNL Adobe Stock]將顯示來自和 [!DNL Experience Manager] 的搜 [!DNL Adobe Stock] 索結果。

* 若要搜尋資 [!DNL Adobe Stock] 產，請按一 **[!UICONTROL 下「導覽]** >資 **[!UICONTROL 產]** >搜 **[!UICONTROL 尋Adobe Stock]**」。

* 若要在和之間搜 [!DNL Adobe Stock] 尋資 [!DNL Experience Manager Assets]產，請按一 ![下search search_icon](assets/search_icon.png)。

或者，開始在搜 `Location: Adobe Stock` 尋列中輸入以選取 [!DNL Adobe Stock] 資產。 [!DNL Experience Manager] 提供已搜尋資產的進階篩選功能，讓使用者可使用篩選器（例如支援的資產類型、影像方向和授權狀態）快速將所需資產置入零位。

>[!NOTE]
>
>Assets searched from [!DNL Adobe Stock] are just displayed in [!DNL Experience Manager]. [!DNL Adobe Stock] 資產只有在使用者儲存資產 [!DNL Experience Manager] 或授權並儲存資產 [後](/help/assets/aem-assets-adobe-stock.md#saveassets) ，才會 [擷取並儲存在儲存庫中](/help/assets/aem-assets-adobe-stock.md#licenseassets)。 Assets that are already stored in [!DNL Experience Manager] are displayed and highlighted for ease of reference and access. Also, the [!DNL Stock] assets are saved with some additional metadata to indicate the source as [!DNL Stock].

![在Experience Manager中搜尋篩選器，並在搜尋結果中反白顯示Adobe Stock資產](assets/aem-search-filters2.jpg)

*圖： 在搜尋結果中[!DNL Experience Manager]搜尋篩選[!DNL Adobe Stock]素材並反白顯示。*

### 儲存並檢視所需資產 {#saveassets}

選取您要儲存的資產 [!DNL Experience Manager]。 按一 [!UICONTROL 下頂端] 工具列中的「儲存」，並提供資產的名稱和位置。 未授權資產會以浮水印儲存在本機。

下次您搜尋資產時，儲存的資產會以徽章反白顯示，以指出這些資產可在中使用 [!DNL Experience Manager Assets]。

>[!NOTE]
>
>最近新增的資產會顯示新徽章，而非授權徽章。

### 授權資產 {#licenseassets}

使用者可使 [!DNL Adobe Stock] 用其企業計畫的配額來授權 [!DNL Adobe Stock] 資產。 當您授權資產時，資產會儲存而無浮水印，並可供搜尋和使用 [!DNL Experience Manager Assets]。

![對話方塊可授權並儲存Experience Manager Assets中的Adobe Stock資產](assets/aem-stock_licenseandsave.jpg)

*圖： 對話方塊可授權並儲[!DNL Adobe Stock]存資產[!DNL Experience Manager Assets]。*

### 存取中繼資料和資產屬性 {#access-metadata-and-asset-properties}

使用者可以存取和預覽中繼資料，包括儲 [!DNL Adobe Stock] 存在中的資產的中繼資料屬性 [!DNL Experience Manager]，以及新增 **[!UICONTROL 資產的授權參考]** 。 不過，授權參考的更新不會在與網站之間 [!DNL Experience Manager] 同步 [!DNL Adobe Stock] 。

使用者可以同時檢視授權和未授權資產的屬性。

![檢視及存取已儲存資產的中繼資料和授權參考](assets/metadata_properties.jpg)

*圖： 檢視及存取已儲存資產的中繼資料和授權參考。*

## 已知限制 {#known-limitations}

* **未顯示編輯影像警告**: 授權影像時，使用者無法檢查影像是否為「僅供編輯使用」。 為防止可能的誤用，管理員可以關閉從管理控制台存取編輯資產的權限。

* **顯示的許可證類型錯誤**: 資產的授權類型可能顯示 [!DNL Experience Manager] 不正確。 使用者可登入網 [!DNL Adobe Stock] 站以檢視授權類型。

* **參考欄位和中繼資料不會同步**: 當使用者更新授權參考欄位時，授權參考資訊會在網站中更新， [!DNL Experience Manager] 但不會在網站上 [!DNL Adobe Stock] 更新。 同樣地，如果使用者更新網站上的參考欄 [!DNL Adobe Stock] 位，則更新不會同步 [!DNL Experience Manager]。

>[!MORELIKETHIS]
>
>* [有關搭配使用Adobe Stock資產與Experience Manager Assets的教學課程影片](https://helpx.adobe.com/experience-manager/kt/assets/using/stock-assets-feature-video-use.html)
>* [Adobe Stock企業計畫說明](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [Adobe Stock常見問答集](https://helpx.adobe.com/stock/faq.html)

