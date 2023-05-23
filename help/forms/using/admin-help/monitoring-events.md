---
title: 監視事件
seo-title: Monitoring events
description: 啟用審計功能後，文檔安全性使您能夠監視某些類型的事件。 您可以使用文檔安全性輕鬆搜索和排序事件清單。
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

# 監視事件 {#monitoring-events}

啟用審計功能後，文檔安全性使您能夠監視某些類型的事件。 您可以看到的事件取決於您的角色：

**用戶：** 可以查看其受策略保護的文檔及其接收和使用的任何受保護文檔的審計事件。

**策略集協調員：** 可以查看受策略保護的文檔（包括文檔和策略事件）的審計事件（從其策略集）。

**管理員：** 可以查看與所有受策略保護的文檔和用戶相關的已審核事件。 管理員還可以跟蹤其他類型的事件，包括用戶、文檔、策略和系統事件。

>[!NOTE]
>
>在策略保護文檔的副本上執行的事件也作為原始受保護文檔上的事件進行跟蹤。

(請參閱 [事件審計選項](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options)。)

如果未經授權的用戶嘗試查看文檔或嘗試使用不正確的用戶名或密碼登錄，則記錄失敗事件。

>[!NOTE]
>
>如果編輯策略以刪除匿名訪問，則可能會記錄文檔的匿名訪問事件。 當授權收件人嘗試訪問已編輯策略保護的文檔時，仍會嘗試匿名訪問，但將失敗。

如果策略允許匿名用戶訪問，但管理員稍後會關閉對文檔安全的匿名訪問，則對於受策略保護的文檔，匿名訪問將失敗，事件將不會記錄。

## 啟用事件審核 {#enable-event-auditing}

要進行事件審核，必須滿足以下設定要求：

* 系統或管理員必須啟用伺服器的審核功能。

   (請參閱 [配置事件審核和隱私設定](/help/forms/using/admin-help/configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings)。)

* 您用於保護文檔的策略必須已啟用審核。 (請參閱 [建立和編輯策略](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies)。)

## 搜索事件 {#search-for-an-event}

您可以搜索事件清單並查看有關事件的更詳細的說明。 詳細說明包括事件ID、說明、IP地址、組織、受影響的用戶、事件發生的日期和時間、拒絕的活動和離線事件（當用戶嘗試在未連接到文檔安全性時使用文檔時）等資訊。

您可以使用事件搜索標準和事件發生日期的組合來搜索「事件」頁上的事件。 您可以搜索的事件取決於您的角色：

**用戶：** 可以查看其受策略保護的文檔及其接收和使用的任何受保護文檔的審計事件。 這些搜索選項可用：

**與我有關的事件：** 用戶可以查找他們建立或接收的任何受策略保護的文檔的事件。 例如，如果用戶開啟、查看或打印受其他人保護的文檔，則用戶只能看到該文檔的這些事件。

**與我的文檔相關的事件：** 用戶可以找到與其自身受策略保護的文檔相關的所有事件。 用戶將看到每個處理其文檔的人生成的事件。

**策略集協調員：** 可以查看受策略保護的文檔（包括文檔和策略事件）的審計事件（從其策略集）。 這些選項可用：

**將我作為策略集協調員的事件記錄在案：** 具有查看事件權限的策略集協調員可以查找與策略集保護的文檔相關的事件。

**我是策略集協調員的策略事件：** 具有查看事件權限的策略集協調員可以從其策略集中查找與策略相關的事件。

**管理員：** 可以查看與所有受策略保護的文檔和用戶相關的已審核事件。 管理員還可以跟蹤其他類型。 此外，管理員可以根據用戶類型進一步細分事件搜索：

**已知用戶：** 用戶位於源目錄中或註冊為外部用戶。

**匿名用戶：** 訪問受允許匿名訪問的策略保護的文檔的未知用戶。

**系統用戶：** 伺服器啟動的事件，如目錄同步。

1. 在文檔安全頁面上，按一下事件。
1. 在「查找」(Find)清單中，選擇要使用的搜索條件。 根據您在「查找」清單中的選擇，將顯示第二個清單，提供附加的搜索條件。 如果適用，在文本框中鍵入搜索條件。

   有關特定事件類型的詳細資訊，請參閱 [事件審計選項](/help/forms/using/admin-help/configuring-client-server-options.md#event-auditing-options)。

1. 在「用戶」清單中，選擇執行該事件的用戶類型：

   * 如果選擇「已知用戶」，則顯示第二個搜索框，您必須在其中鍵入用戶的用戶名或電子郵件地址。
   * 如果您不知道這些值，請按一下通訊簿搜索表徵圖按用戶名或電子郵件地址搜索用戶。

1. 在「日期」清單中，選擇一個日期範圍選項。 如果選擇「自定義日期」，則會出現以yyyy/mm/dd格式鍵入日期的框，或者可以使用日期選擇器指定日期範圍：

   * 按一下日曆以開啟日期選取器。
   * 使用箭頭查找年和月。
   * 在日曆上按一下月份的某一天。
   * 按一下「確定」關閉日期選取器。

1. 在「顯示」清單中，選擇每頁要顯示的搜索結果數。
1. 按一下「查找」。

   所有失敗事件都以拒絕表徵圖在清單中突出顯示。

1. 要查看有關事件的詳細資訊，請按一下清單中事件的說明。

## 對事件清單排序 {#sort-the-event-list}

您可以按列標題對事件清單進行排序，以便更輕鬆地查找事件。 列標題旁邊的三角形表徵圖指示當前用於排序的列。 向上指向三角形表示升序，而向下指向三角形表示降序。

1. 按一下相應的列標題。
1. 要更改排序順序，請再次按一下列標題。
