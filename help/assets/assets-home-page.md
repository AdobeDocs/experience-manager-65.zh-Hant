---
title: '"[!DNL Assets] 首頁體驗」'
description: 個性化 [!DNL Experience Manager Assets] 歡迎使用的豐富螢幕體驗首頁，包括有關資產最近活動的快照。
contentOwner: AG
feature: Developer Tools, Asset Management
role: Admin, User
exl-id: 042bd959-256a-4794-a34d-0848a6b8840d
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager Assets] 首頁體驗 {#aem-assets-home-page-experience}

個性化 [!DNL Adobe Experience Manager Assets] 首頁，提供豐富的歡迎螢幕體驗，包括資產最近活動的快照。

[!DNL Assets] 首頁提供了豐富且個性化的歡迎螢幕體驗，其中包括最近活動的快照，如最近查看或上載的資產。

的 [!DNL Assets] 預設情況下禁用首頁。 要啟用它，請執行以下步驟：

1. 開啟 [!DNL Experience Manager] 配置管理器 `https://[aem_server]:[port]/system/console/configMgr`。
1. 開啟 **[!UICONTROL 第CQ天大壩事件記錄器]** 服務。
1. 選擇 **[!UICONTROL 啟用此服務]** 啟用活動錄制。

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. 從 **[!UICONTROL 事件類型]** 清單中，選擇要記錄的事件並保存更改。

   >[!CAUTION]
   >
   >啟用「已查看資產」、「已查看項目」和「已查看收集」選項，可顯著增加記錄的事件數。

1. 開啟 **[!UICONTROL DAM資產首頁功能標誌]** 從Configuration Manager提供服務 `https://[aem_server]:[port]/system/console/configMgr`。
1. 選擇 `isEnabled.name` 選項啟用 [!DNL Assets] 首頁功能。 儲存變更。

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. 開啟 **[!UICONTROL 用戶首選項]** 對話框，然後選擇 **[!UICONTROL 啟用資產首頁]**。 儲存變更。

   ![在「用戶首選項」對話框上啟用資產首頁](assets/Annotation-color.png)

啟用 [!DNL Assets] 首頁，導航到 [!DNL Assets] 用戶介面（從導航頁）或直接從URL訪問 `https://[aem_server]:[port]/aem/assetshome.html/content/dam`。

![在資產用戶介面上配置體驗連結](assets/config-experience-link.png)

按一下 **[!UICONTROL 按一下這裡配置您的體驗連結]** 添加用戶名、背景影像和配置檔案影像。

的 [!DNL Assets] 首頁包含以下部分：

* 歡迎節
* 小部件部分

**歡迎節**

如果您的配置檔案存在，則「歡迎」部分將顯示一條歡迎消息。 此外，它還顯示您的配置檔案圖片和歡迎影像（如果已配置）。

如果您的配置檔案不完整，則「歡迎」部分將顯示一般歡迎消息和配置檔案圖片的佔位符。

**小部件部分**

此部分顯示在「歡迎」部分下方，並在以下部分下顯示現成小部件：

* 活動
* 最近
* 探索

**活動**:在本節中， **[!UICONTROL 我的活動]** 構件顯示登錄用戶使用資產（包括不帶格式副本的資產）執行的最新活動，例如資產上載、下載、資產建立、編輯、注釋、注釋和共用。

**最近**:的 **[!UICONTROL 最近查看]** 此部分下的小部件顯示登錄用戶最近訪問的實體，包括資料夾、集合和項目。

**發現**:的 **[!UICONTROL 新建]** 此部分下的小部件顯示最近上載到 [!DNL Assets] 部署。

要啟用清除用戶活動資料，請啟用 **[!UICONTROL DAM事件清除服務]** 從Configuration Manager中。 啟用此服務後，系統將刪除已登錄用戶超過指定數目的活動。

「歡迎」螢幕提供了簡單的導航幫助，例如工具欄上的表徵圖可訪問資料夾、收藏和目錄。

>[!NOTE]
>
>啟用 [!UICONTROL 第CQ天大壩事件記錄器] 和 [!UICONTROL DAM事件清除] 服務增加了對JCR的寫操作和搜索索引，這大大增加了對 [!DNL Experience Manager] 伺服器。 上的附加負載 [!DNL Experience Manager] 伺服器會影響其效能。

>[!CAUTION]
>
>捕獲、篩選和清除用戶活動 [!DNL Assets] 首頁對效能造成了開銷。 因此，管理員應為目標用戶有效配置首頁。
>
>Adobe建議執行批量操作的管理員和用戶避免使用資產首頁功能來防止用戶活動增加。 此外，管理員可以通過配置來排除特定用戶的錄制活動 [!UICONTROL 第CQ天大壩事件記錄器] 從 [!UICONTROL 配置管理器]。
>
>如果使用該功能，Adobe建議根據伺服器負載計劃清除頻率。
