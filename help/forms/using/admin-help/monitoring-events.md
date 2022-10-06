---
title: 監控事件
seo-title: Monitoring events
description: 啟用審核功能後，文檔安全性允許您監視某些類型的事件。 您可以使用檔案安全性輕鬆搜尋事件清單並加以排序。
seo-description: When the auditing capability is enabled, document security enables you to monitor certain types of events. You can easily search and sort the events list using the document security.
uuid: 22add6ff-536d-4cb9-8eac-b72cad5c3ecf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 379957bf-0634-4182-b269-1b010da4c90f
feature: Document Security
exl-id: 078b9ad1-16e2-40f4-92dc-e4093c0bb6ac
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---

# 監控事件 {#monitoring-events}

啟用審核功能後，文檔安全性允許您監視某些類型的事件。 您可以看到的事件取決於您的角色：

**用戶：** 可以查看其受策略保護的文檔以及接收和使用的任何受保護文檔的已審核事件。

**策略集協調員：** 可以查看受策略保護的文檔的審核事件，包括文檔和策略事件，使其不受其策略集的影響。

**管理員：** 可以查看與所有受策略保護的文檔和用戶相關的已審核事件。 管理員也可以追蹤其他類型的事件，包括使用者、檔案、原則和系統事件。

>[!NOTE]
>
>對受策略保護文檔的副本執行的事件也作為原始受保護文檔上的事件被跟蹤。

(請參閱 [事件審核選項](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options).)

如果未經授權的用戶嘗試查看文檔或嘗試使用不正確的用戶名或密碼登錄，則記錄失敗事件。

>[!NOTE]
>
>如果編輯了策略以刪除匿名訪問，則可能會記錄文檔的匿名訪問事件。 當被授權的收件人嘗試訪問編輯的策略所保護的文檔時，仍然嘗試匿名訪問，但將失敗。

如果策略允許匿名用戶訪問，但管理員稍後為文檔安全關閉匿名訪問，則對於受該策略保護的文檔，匿名訪問將失敗，且該事件將不會記錄。

## 啟用事件審核 {#enable-event-auditing}

事件審核必須符合以下設定要求：

* 系統或管理員必須啟用伺服器的審核功能。

   (請參閱 [配置事件審核和隱私設定](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings).)

* 用於保護文檔的策略必須啟用審核。 (請參閱 [建立和編輯原則](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).)

## 搜尋事件 {#search-for-an-event}

您可以搜尋事件清單，並檢視有關事件的更詳細說明。 詳細說明包括事件ID、說明、IP位址、組織、受影響的使用者、事件發生的日期和時間、拒絕的活動，以及離線事件（當使用者未連線至檔案安全性時嘗試使用檔案）等資訊。

您可以使用事件搜尋准則和事件發生日期的組合，在「事件」頁面上搜尋事件。 您可搜尋的事件取決於您的角色：

**用戶：** 可以查看其受策略保護的文檔以及接收和使用的任何受保護文檔的已審核事件。 可使用下列搜尋選項：

**與我相關的事件：** 用戶可以找到他們建立或接收的任何受策略保護文檔的事件。 例如，如果用戶開啟、查看或打印另一個人保護的文檔，則用戶只看到該文檔的這些事件。

**與我的文檔相關的事件：** 用戶可以找到與自己受策略保護的文檔相關的所有事件。 使用者會看見處理其檔案之每個人產生的事件。

**策略集協調員：** 可以查看受策略保護的文檔的審核事件，包括文檔和策略事件，使其不受其策略集的影響。 可使用下列選項：

**記錄我是策略集協調員的事件：** 具有查看事件權限的策略集協調員可以查找與策略集保護的文檔相關的事件。

**我擔任策略集協調員的策略事件：** 具有查看事件權限的策略集協調員可以從其策略集中查找與策略相關的事件。

**管理員：** 可以查看與所有受策略保護的文檔和用戶相關的已審核事件。 管理員也可以追蹤其他類型。 此外，管理員可以根據使用者類型進一步細分事件搜尋：

**已知用戶：** 用戶位於源目錄中或註冊為外部用戶。

**匿名用戶：** 訪問受允許匿名訪問的策略保護的文檔的未知用戶。

**系統用戶：** 伺服器啟動的事件，如目錄同步。

1. 在文檔安全頁上，按一下「事件」。
1. 在「查找」清單中，選擇要使用的搜索標準。 根據您在「查找」清單中的選擇，將顯示另一個清單，該清單提供其他搜索條件。 如果適用，在文字方塊中輸入搜尋條件。

   如需特定事件類型的詳細資訊，請參閱 [事件審核選項](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options).

1. 在「用戶」清單中，選擇執行該事件的用戶類型：

   * 如果選擇「已知用戶」，則會顯示第二個搜索框，您必須在其中鍵入用戶的用戶名或電子郵件地址。
   * 如果您不知道這些值，請按一下通訊簿搜索表徵圖，按用戶名或電子郵件地址搜索用戶。

1. 在「日期」清單中，選取日期範圍選項。 如果選擇「自訂日期」，則會出現方塊，您在其中輸入日期的格式為yyyy/mm/dd，或者您可以使用「日期選擇器」來指定日期範圍：

   * 按一下日曆以開啟「日期選擇器」。
   * 使用箭頭來查找年份和月份。
   * 按一下日曆上月份的某天。
   * 按一下「確定」以關閉日期選擇器。

1. 在「顯示」清單中，選取每頁要顯示的搜尋結果數量。
1. 按一下「查找」。

   清單中會以拒絕的圖示強調顯示任何失敗事件。

1. 若要檢視事件的詳細資訊，請按一下清單中事件的說明。

## 排序事件清單 {#sort-the-event-list}

您可以依欄標題來排序事件清單，以更輕鬆地尋找事件。 欄標題旁的三角形圖示表示目前要排序的欄。 向上指向的三角形表示升序，而向下指向的三角形表示降序。

1. 按一下適當的欄標題。
1. 要更改排序順序，請再次按一下列標題。
