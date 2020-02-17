---
title: 在AEM Assets中管理Adobe Stock資產
description: 在AEM中搜尋、擷取、授權及管理Adobe Stock資產。 將授權資產當做任何其他數位資產使用。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 70a88085a0fd6e949974aa7f1f92fdc3def3d98e

---


# 在AEM資產中使用Adobe Stock資產 {#use-adobe-stock-assets-in-aem-assets}

組織可將其Adobe Stock企業計畫與AEM Assets整合，以確保授權資產可廣泛用於其創意和行銷專案，以及AEM的強大資產管理功能。

Adobe Stock服務可讓設計人員和企業針對其所有創意專案，取用數百萬個高品質、優質且免版稅的像片、向量、插圖、視訊、範本和3D資產。 AEM使用者可以快速尋找、預覽和授權儲存在AEM中的Adobe Stock資產，而不需離開AEM工作區。

## 必備條件 {#prerequisites}

整合需要企 [業版Adobe Stock計畫](https://landing.adobe.com/en/na/products/creative-cloud/ctir-4625-stock-for-enterprise/index.html) 和AEM 6.5或更新版本。 如需AEM 6.5 Service Pack詳細資訊，請參閱這些版 [本注意事項](/help/release-notes/sp-release-notes.md)。

## 整合AEM和Adobe Stock {#integrate-aem-and-adobe-stock}

若要允許AEM與Adobe Stock之間通訊，請在AEM中建立IMS設定和Adobe Stock設定。

>[!NOTE]
>
>只有組織的AEM管理員和Admin Console管理員才能執行整合，因為它需要管理員權限。

### 建立IMS設定 {#create-an-ims-configuration}

1. 按一下「AEM logo」。 導覽至「 **[!UICONTROL 工具]** >安 **[!UICONTROL 全]** > **[!UICONTROL Adobe IMS設定」]**。 按一 **[!UICONTROL 下「建立]** 」，然後選 **[!UICONTROL 取「雲端解決方案]** > **[!UICONTROL Adobe Stock]**」。
1. 重複使用現有證書或選擇「 **[!UICONTROL 建立新證書」]**。
1. 按一 **[!UICONTROL 下建立憑證]**。 建立後，請下載公開金鑰。 按一 **[!UICONTROL 下「下一步]**」。
1. 在標題為 **[!UICONTROL Title]**、 **[!UICONTROL Authorization Server]**、 **[!UICONTROL API Secret]**、Client Secret ******** PayloadKey、Client PayloadKey的欄位中提供適當的值。 如需 [從Adobe I/O擷取這些值的詳細資訊](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md)，請參閱JWT驗證快速入門。
1. 將下載的公開金鑰新增至您的Adobe I/O服務帳戶。

### 在AEM中建立Adobe Stock設定 {#create-adobe-stock-configuration-in-aem}

1. 在AEM使用者介面中，導覽至「工 **[!UICONTROL 具]** > **[!UICONTROL Cloud服務]** > **[!UICONTROL Adobe Stock]**」。
1. 按一 **[!UICONTROL 下「建立]** 」以建立組態，並將它與您現有的IMS組態建立關聯。 選擇 `PROD` 作為環境參數。
1. 在「 **[!UICONTROL 授權資產路徑]** 」欄位中，保留原狀位置。 請勿變更您要儲存Adobe Stock資產的位置。
1. 新增所有必要屬性以完成建立。 按一 **[!UICONTROL 下儲存並關閉]**。
1. 新增AEM使用者或群組，讓其授權資產。

>[!NOTE]
>
>如果有多個Adobe Stock設定，請在「使用者偏好設定」面板中按一下AEM使用者介面中的  AEM標誌，以選取所需的設定。

## 在AEM中使用及管理Adobe Stock資產 {#usemanage}

使用這項功能，組織可讓其使用者在AEM Assets中使用Adobe Stock資產。 在AEM使用者介面中，使用者可以搜尋Adobe Stock資產並授權所需的資產。

在AEM中授權Adobe Stock資產後，就可像一般資產一樣使用和管理。 在AEM中，使用者可以搜尋和預覽資產；複製及發佈資產；在品牌入口網站分享資產；透過AEM案頭應用程式存取及使用資產；等等。

![搜尋Adobe Stock資產並篩選AEM工作區的結果](assets/adobe-stock-search-results-workspace.png)*圖：搜尋Adobe Stock資產並篩選AEM工作區的結果*

**** 答：搜尋資產，類似於提供Adobe Stock ID的資產。 **** B.搜尋符合您選取形狀或方向的資產。 **************** C.**Search one of more supported asset types** D.開啟或收合篩選器窗格 **E。在AEM** F中授權並儲存選取的資產。將資產儲存在AEM中並加上浮水印 **G。在Adobe Stock網站上探索與所選資產** H類似的資產。在Adobe Stock網站 **I上檢視選取的資產。搜尋結果** J中選取的資產數。在卡片檢視和清單檢視之間切換

### 尋找資產 {#find-assets}

您的AEM使用者可以在AEM和Adobe Stock中搜尋資產。 當搜尋位置不限於Adobe Stock時，會顯示來自AEM和Adobe Stock的搜尋結果。

* 若要搜尋Adobe Stock資產，請按一 **[!UICONTROL 下「導覽]** > **[!UICONTROL 資產]** >搜 **[!UICONTROL 尋Adobe Stock]**」。

* 若要在Adobe Stock和AEM Assets中搜尋資產，請按一下搜尋圖示 ![search_icon](assets/search_icon.png)。

或者，開始在搜 `Location: Adobe Stock` 尋列中輸入以選取Adobe Stock資產。  AEM針對搜尋的資產提供進階篩選功能，讓使用者可使用篩選器，例如支援的資產類型、影像方向和授權狀態，快速將所需資產置於零。

>[!NOTE]
>
>從Adobe Stock搜尋的資產會顯示在AEM中。 Adobe Stock資產只有在使用者儲存資產或授權資產後，才會擷 [取並儲存在AEM](/help/assets/aem-assets-adobe-stock.md#saveassets)[儲存庫中](/help/assets/aem-assets-adobe-stock.md#licenseassets)。 已儲存在AEM中的資產會顯示並反白顯示，以方便參考和存取。 此外，這些資產會與一些額外的中繼資料一起儲存，以指出來源為Adobe Stock。

![AEM中的搜尋篩選器，並在搜尋結果中反白顯示Adobe Stock資](assets/aem-search-filters2.jpg)*產圖：AEM中的搜尋篩選器，並在搜尋結果中反白顯示Adobe Stock資產*

### 儲存並檢視所需資產 {#saveassets}

選取您要在AEM中儲存的資產。 按一下頂端工具列中的「儲存」，並提供資產的名稱和位置。 未授權資產會以浮水印儲存在本機。

下次您搜尋資產時，儲存的資產會以徽章反白顯示，以指出此類資產可在AEM Assets中使用。

>[!NOTE]
>
>最近新增的資產會顯示新徽章，而非授權徽章。

### 授權資產 {#licenseassets}

使用者可使用其Adobe Stock Enterprise計畫的配額來授權Adobe Stock資產。 當您授權資產時，資產會儲存而無浮水印，而且可供在AEM Assets中搜尋和使用。

![在AEM Assets中授權及儲存Adobe Stock資產的對話方塊](assets/aem-stock_licenseandsave.jpg)*圖：對話方塊可授權並儲存AEM Assets中的Adobe Stock資產*

### 存取中繼資料和資產屬性 {#access-metadata-and-asset-properties}

使用者可以存取和預覽中繼資料，包括儲存在AEM中之資產的Adobe Stock中繼資料屬性，以及新增資產的 **[!UICONTROL 授權參考]** 。 不過，AEM和Adobe Stock網站之間不會同步授權參考的更新。

使用者可以同時檢視授權和未授權資產的屬性。

![檢視及存取已儲存資產的中繼資料和授權參考](assets/metadata_properties.jpg)*圖：檢視及存取已儲存資產的中繼資料和授權參考*

## 已知限制 {#known-limitations}

### 未顯示編輯影像警告

授權影像時，使用者無法檢查影像是否為「僅供編輯使用」。 為防止可能的誤用，管理員可以關閉從管理控制台存取編輯資產的權限。

### 顯示的許可證類型錯誤

資產的AEM中可能會顯示不正確的授權類型。 使用者可登入Adobe Stock網站以檢視授權類型。

### 參考欄位和中繼資料不會同步

當使用者更新授權參考欄位時，授權參考資訊會在AEM中更新，但不會在Adobe Stock網站上更新。 同樣地，如果使用者更新Adobe Stock網站上的參考欄位，則AEM中的更新不會同步。

## Related resources {#related-resources}

[有關搭配使用Adobe Stock資產和AEM資產的教學影片](https://helpx.adobe.com/experience-manager/kt/assets/using/stock-assets-feature-video-use.html)

[Adobe Stock企業計畫說明](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)

[Adobe Stock常見問答集](https://helpx.adobe.com/stock/faq.html)
