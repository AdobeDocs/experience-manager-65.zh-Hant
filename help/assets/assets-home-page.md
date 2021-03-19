---
title: '[!DNL Assets] 首頁體驗'
description: '個人化首頁，提供多樣化的歡迎畫面體驗，包括資產最近活動的快照。 [!DNL Experience Manager Assets] '
contentOwner: AG
feature: 開發人員工具，資產管理
role: 管理員，商業從業人員
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# [!DNL Adobe Experience Manager Assets] 首頁體驗  {#aem-assets-home-page-experience}

個人化[!DNL Adobe Experience Manager Assets]首頁，提供多樣化的歡迎畫面體驗，包括資產最近活動的快照。

[!DNL Assets] 首頁提供多樣化的個人化歡迎畫面體驗，其中包含最近檢視或上傳的資產等活動的快照。

預設會停用[!DNL Assets]首頁。 要啟用它，請執行以下步驟：

1. 開啟[!DNL Experience Manager] Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`。
1. 開啟&#x200B;**[!UICONTROL Day CQ DAM Event Recorder]**&#x200B;服務。
1. 選擇&#x200B;**[!UICONTROL 啟用此服務]**&#x200B;以啟用活動記錄。

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. 從&#x200B;**[!UICONTROL 事件類型]**&#x200B;清單中，選擇要記錄的事件並保存更改。

   >[!CAUTION]
   >
   >啟用「已檢視的資產」、「已檢視的專案」和「已檢視的系列」選項，可大幅增加已記錄事件的數目。

1. 從Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`開啟&#x200B;**[!UICONTROL DAM資產首頁功能標誌]**&#x200B;服務。
1. 選擇`isEnabled.name`選項以啟用[!DNL Assets]首頁功能。 儲存變更。

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. 開啟&#x200B;**[!UICONTROL 使用者偏好設定]**&#x200B;對話方塊，並選取&#x200B;**[!UICONTROL 啟用資產首頁]**。 儲存變更。

   ![在「使用者偏好設定」對話方塊上啟用資產首頁](assets/Annotation-color.png)

啟用[!DNL Assets]首頁後，從「導覽」頁面導覽至[!DNL Assets]使用者介面，或直接從URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`存取。

![在資產使用者介面上設定體驗連結](assets/config-experience-link.png)

按一下&#x200B;**[!UICONTROL 按一下此處以設定您的體驗連結]**，以新增您的使用者名稱、背景影像和描述檔影像。

[!DNL Assets]首頁包含以下部分：

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

**活動**:在本節中，「我的 **** 活動」介面工具集會顯示登入使用者使用資產（包括無轉譯的資產）執行的最新活動，例如資產上傳、下載、資產建立、編輯、留言、註解和分享。

**最近**:此區 **[!UICONTROL 段下]** 的「最近檢視的介面工具集」會顯示登入使用者最近存取的實體，包括資料夾、系列和專案。

**Discover**:此區 **** 段下的新介面工具集會顯示最近上傳至部署的資產和 [!DNL Assets] 轉譯。

要啟用清除用戶活動資料，請從Configuration Manager中啟用&#x200B;**[!UICONTROL DAM事件清除服務]**。 啟用此服務後，系統將刪除超過指定數目的登入使用者活動。

「歡迎」畫面提供簡單的導覽協助，例如工具列上的圖示，可存取資料夾、系列和型錄。

>[!NOTE]
>
>啟用[!UICONTROL Day CQ DAM Event Recorder]和[!UICONTROL DAM Event Purge]服務可增加對JCR的寫操作和搜索索引，這顯著增加了[!DNL Experience Manager]伺服器上的負載。 [!DNL Experience Manager]伺服器上的額外負載可能會影響其效能。

>[!CAUTION]
>
>擷取、篩選和清除[!DNL Assets]首頁所需的使用者活動會對效能造成額外負擔。 因此，管理員應該為目標使用者有效配置首頁。
>
>Adobe建議執行大量作業的管理員和使用者避免使用「資產首頁」功能來防止使用者活動增加。 此外，管理員可以通過從[!UICONTROL 配置管理器]配置[!UICONTROL Day CQ DAM Event Recorder]來排除特定用戶的記錄活動。
>
>如果您使用此功能，Adobe建議您根據伺服器負載計劃清除頻率。
