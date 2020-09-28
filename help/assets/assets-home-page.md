---
title: '[!DNL資產]首頁體驗'
description: 個人 [!DNL Experience Manager Assets] 化首頁，提供多樣化的歡迎畫面體驗，包括資產相關活動的快照。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 1%

---


# [!DNL Adobe Experience Manager Assets] 首頁體驗 {#aem-assets-home-page-experience}

個人化 [!DNL Adobe Experience Manager Assets] 首頁，提供豐富的歡迎畫面體驗，包括資產相關活動的快照。

[!DNL Assets] 首頁提供多樣化的個人化歡迎畫面體驗，其中包含最近檢視或上傳的資產等活動的快照。

預設 [!DNL Assets] 會停用首頁。 要啟用它，請執行以下步驟：

1. 開啟 [!DNL Experience Manager] 配置管理 `https://[aem_server]:[port]/system/console/configMgr`器。
1. 開啟 **[!UICONTROL Day CQ DAM Event Recorder服務]** 。
1. 選擇「 **[!UICONTROL 啟用此服務]** 」以啟用活動記錄。

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. 從「事 **[!UICONTROL 件類型]** 」清單中，選取要記錄的事件並儲存變更。

   >[!CAUTION]
   >
   >啟用「已檢視的資產」、「已檢視的專案」和「已檢視的系列」選項，可大幅增加已記錄事件的數目。

1. 從Configuration Manager開 **[!UICONTROL 啟DAM Asset首頁功能標幟]** (DAM Asset Home Page Feature Flag `https://[aem_server]:[port]/system/console/configMgr`)服務。
1. 選取選 `isEnabled.name` 項以啟用「首 [!DNL Assets] 頁」功能。 儲存變更。

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. 開啟「使 **[!UICONTROL 用者偏好設定]** 」對話方塊，並選 **[!UICONTROL 取「啟用資產首頁」]**。 儲存變更。

   ![在「使用者偏好設定」對話方塊上啟用資產首頁](assets/Annotation-color.png)

啟用首頁 [!DNL Assets] 後，從「導覽」頁 [!DNL Assets] 面導覽至使用者介面，或直接從URL存取該介面 `https://[aem_server]:[port]/aem/assetshome.html/content/dam`。

![在資產使用者介面上設定體驗連結](assets/config-experience-link.png)

按一下 **[!UICONTROL 此處以設定體驗連結]** ，以新增您的使用者名稱、背景影像和描述檔影像。

「首 [!DNL Assets] 頁」包含以下部分：

* 歡迎區
* 介面工具集區段

**歡迎區**

如果您的個人檔案存在，歡迎區段會顯示歡迎訊息給您。 此外，它還會顯示您的個人檔案圖片和歡迎影像（如果已設定）。

如果您的描述檔不完整，「歡迎」區段會顯示一般歡迎訊息，以及描述檔圖片的預留位置。

**介面工具集區段**

此區段會顯示在「歡迎」區段下方，並在下列區段下顯示現成可用的Widget:

* 活動
* 最近
* 探索

**活動**:在本節中，「我的活動 **** 」介面工具集會顯示登入使用者使用資產（包括無轉譯的資產）執行的最新活動，例如資產上傳、下載、資產建立、編輯、留言、註解和分享。

**最近**:此區 **[!UICONTROL 段下的「最近檢視]** 」介面工具集會顯示登入使用者最近存取的實體，包括資料夾、系列和專案。

**Discover**:此區 **[!UICONTROL 段下的]** 「新增」介面工具集會顯示最近上傳至部署的資產和轉 [!DNL Assets] 譯。

要啟用清除用戶活動資料，請從配置管理 **[!UICONTROL 器啟用DAM事件清除服務]** 。 啟用此服務後，系統將刪除超過指定數目的登入使用者活動。

「歡迎」畫面提供簡單的導覽協助，例如工具列上的圖示，可存取資料夾、系列和型錄。

>[!NOTE]
>
>啟用 [!UICONTROL Day CQ DAM Event Recorder] and [!UICONTROL DAM Event Purge] services可增加對JCR的寫入操作和搜尋索引，這可大幅增加伺服器的負 [!DNL Experience Manager] 載。 伺服器的額外負載 [!DNL Experience Manager] 可能會影響其效能。

>[!CAUTION]
>
>擷取、篩選和清除首頁所需的使用者活 [!DNL Assets] 動會對效能造成額外負擔。 因此，管理員應該為目標使用者有效配置首頁。
>
>Adobe建議執行大量作業的管理員和使用者避免使用「資產首頁」功能來防止使用者活動增加。 此外，管理員可以從Configuration Manager中設定 [!UICONTROL Day CQ DAM Event Recorder] ，排除特定使用者的 [!UICONTROL 錄制活動]。
>
>如果您使用此功能，Adobe建議您根據伺服器負載來排程清除頻率。
