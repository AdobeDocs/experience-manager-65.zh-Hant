---
title: '[!DNL Assets] 首頁體驗'
description: 為豐富的歡迎畫面體驗個人化 [!DNL Experience Manager Assets] 首頁，包括資產相關最近活動的快照。
contentOwner: AG
feature: 開發人員工具，資產管理
role: Admin, User
exl-id: 042bd959-256a-4794-a34d-0848a6b8840d
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager Assets] 首頁體驗 {#aem-assets-home-page-experience}

個人化[!DNL Adobe Experience Manager Assets]首頁以提供豐富的歡迎畫面體驗，包括資產近期活動的快照。

[!DNL Assets] 首頁提供豐富且個人化的歡迎畫面體驗，包含最近活動（例如最近檢視或上傳的資產）的快照。

預設會停用[!DNL Assets]首頁。 要啟用它，請執行以下步驟：

1. 開啟[!DNL Experience Manager] Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`。
1. 開啟&#x200B;**[!UICONTROL Day CQ DAM Event Recorder]**&#x200B;服務。
1. 選擇&#x200B;**[!UICONTROL 啟用此服務]**&#x200B;以啟用活動記錄。

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. 從&#x200B;**[!UICONTROL 事件類型]**&#x200B;清單中，選擇要記錄的事件並保存更改。

   >[!CAUTION]
   >
   >啟用「已檢視資產」、「已檢視專案」和「已檢視集合」選項，可大幅增加記錄的事件數。

1. 從Configuration Manager `https://[aem_server]:[port]/system/console/configMgr`開啟&#x200B;**[!UICONTROL DAM資產首頁功能標幟]**&#x200B;服務。
1. 選擇`isEnabled.name`選項以啟用[!DNL Assets]首頁功能。 儲存變更。

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. 開啟&#x200B;**[!UICONTROL 使用者偏好設定]**&#x200B;對話方塊，然後選取&#x200B;**[!UICONTROL 啟用資產首頁]**。 儲存變更。

   ![在使用者偏好設定對話方塊上啟用資產首頁](assets/Annotation-color.png)

啟用[!DNL Assets]首頁後，從導航頁導航到[!DNL Assets]用戶介面或直接從URL `https://[aem_server]:[port]/aem/assetshome.html/content/dam`訪問該介面。

![在Assets使用者介面上設定體驗連結](assets/config-experience-link.png)

按一下&#x200B;**[!UICONTROL 按一下這裡以設定您的體驗連結]**&#x200B;以新增您的使用者名稱、背景影像和設定檔影像。

[!DNL Assets]首頁包含以下部分：

* 歡迎區段
* 介面工具集區段

**歡迎區段**

如果您的設定檔存在，歡迎區段會顯示寄送給您的歡迎訊息。 此外，它還會顯示您的個人資料圖片和歡迎影像（如果已設定）。

如果您的個人資料不完整，歡迎區段會顯示一般歡迎訊息和個人資料圖片的預留位置。

**介面工具集區段**

此部分顯示在「歡迎」部分下方，並在以下部分下顯示現成的Widget:

* 活動
* 最近
* 探索

**活動**:在此區段下，「我的 **[!UICONTROL 活動]** 介面工具集」會顯示登入使用者使用資產（包括不轉譯的資產）執行的最新活動，例如資產上傳、下載、資產建立、編輯、留言、註解和共用。

**最近**:本 **[!UICONTROL 節下]** 的「最近查看的介面工具集」顯示登錄用戶最近訪問的實體，包括資料夾、集合和項目。

**Discover**:此區 **** 段下的新介面工具集會顯示最近上傳至部署的資產和轉 [!DNL Assets] 譯。

若要啟用清除使用者活動資料，請從Configuration Manager啟用&#x200B;**[!UICONTROL DAM事件清除服務]**。 啟用此服務後，系統會刪除登入使用者超過指定數目的活動。

「歡迎」畫面提供簡單的導覽輔助工具，例如工具列上的圖示，可存取資料夾、收藏和目錄。

>[!NOTE]
>
>啟用[!UICONTROL Day CQ DAM Event Recorder]和[!UICONTROL  DAM Event Purge]服務會增加對JCR的寫入操作和搜索索引，這會顯著增加[!DNL Experience Manager]伺服器上的負載。 [!DNL Experience Manager]伺服器上的額外負載可能會影響其效能。

>[!CAUTION]
>
>擷取、篩選及清除[!DNL Assets]首頁所需的使用者活動會對效能造成額外負荷。 因此，管理員應該為目標使用者有效配置首頁。
>
>Adobe建議執行大量作業的管理員和使用者避免使用資產首頁功能，以防止使用者活動增加。 此外，管理員可以從[!UICONTROL Configuration Manager]配置[!UICONTROL Day CQ DAM Event Recorder] ，以排除特定使用者的記錄活動。
>
>如果您使用此功能，Adobe建議您根據伺服器負載排程清除頻率。
