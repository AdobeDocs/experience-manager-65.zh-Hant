---
title: 啟動進程
seo-title: Starting processes
description: 如何使用LiveCycleAEM Forms工作區 — 選擇進程、添加註釋和附件、保存草稿副本和添加到收藏夾。
seo-description: How to use LiveCycle AEM Forms workspace--select processes, add notes and attachments, save draft copies, and add to favorites.
uuid: a61da785-25b4-4482-bd72-02e250d35dc7
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c9d3f369-3744-41d5-b340-390ab7e03f36
exl-id: b2a6ba3a-0f4c-44b1-8f9a-c15c6fb8c305
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 0%

---

# 啟動進程 {#starting-processes}

AEM Forms工作區按管理員或流程設計器設定的類別組織流程。 您還可以將經常使用的進程放入收藏夾類別，以便快速找到它們。

啟動流程時，可能需要填寫表單以啟動AEM Forms工作流控制的業務流程。 如果表單使用「準備資料流程」，則在啟動新流程時，可以將某些資訊預填充為空白表單。

例如，您想購買新的電腦監視器，因此啟動名為 *採購訂單*。 啟動流程時，會開啟一個表單，提示您輸入要訂購的物料的詳細資訊。 您的姓名、員工編號和經理的姓名可能已在表單上預先填充。 在您提交請求時，系統將起動業務流程。 根據進程定義，伺服器自動將請求路由到您的管理器。 該任務開始出現在您經理的待辦事項清單中。 經理批准該請求後，表單工作流會將該請求路由到採購部門，並向您發送電子郵件通知。

## 選擇要啟動的進程 {#selecting-processes-to-start}

您可以選擇要啟動該進程或查看有關該進程的詳細資訊。

選擇要啟動的進程時，可能需要填寫與該進程關聯的表單。 提交表單將啟動流程。

支援各種檔案格式的Forms，包括Adobe PDF、HTML和SWF檔案。 表單可能看起來像傳統的可打印或基於Web的表單，也可以引導您通過一系列嚮導式面板來收集資訊。

如果表單和流程允許，您還可以離線保存表單，填寫它，然後提交它以完成任務。 提交表單時，如果配置了電子郵件端點，則使用相應的伺服器電子郵件地址啟動電子郵件客戶端。 然後，您可以通過電子郵件將填寫好的表單發送到伺服器。

選擇流程時，將顯示「表單」頁籤和「詳細資訊」頁籤。 如果流程允許您添加附註或附件，則還會顯示「附件」標籤和「附註」標籤。 如果您還使用進程配置了摘要URL，則還會顯示「摘要」頁籤。 「Forms」頁籤顯示關聯的表單，「詳細資訊」頁籤顯示有關當前任務及其所屬流程的資訊。

### 啟動業務流程 {#start-a-business-process}

1. 在「開始流程」頁的左側清單中，選擇一個類別。 在類別中您有權訪問的所有進程都顯示在右側。

   >[!NOTE]
   >
   >如果「類別」窗格折疊，請按一下AEM Forms工作區左上角的「開啟類別」以開啟該窗格。

1. 通過按一下任務選擇進程。 與流程關聯的表單將在「表單」(Form)頁籤上開啟。

   進程中的每個表單都有一個唯一的URL。 可以使用唯一URL直接啟動具有特定流程和表單的HTML工作區。 URL的格式為https://&lt;server>:&lt;port>/lc/libs/ws/index.html#/startprocess/&lt;applicationname>%2F&lt;processname>。 的 &lt;applicationname>%2F&lt;processname> 字串始終是URL編碼的。 示例URL為http://localhost:8080/lc/libs/ws/index.html#/startprocess/MyApplication%2FNewProcess。 示例中的ApplicationName%2FProcessName字串是URL編碼的。

1. 根據隨附的說明填寫表單。 如有必要，按一下 **最大化** 的子菜單。
1. 如果「附件」(Attachments)頁籤可用，請根據需要添加附件。
1. 如果「附註」標籤可用，請根據需要提供任何附註。
1. 執行以下步驟之一：

   * 如果表單具有「提交」按鈕，則按一下表單上的「提交」按鈕。
   * 如果表單沒有「提交」按鈕，請按一下表單下面的「完成」。

   Oracle Process Management將啟動流程，並將表單路由至需要完成流程中下一個任務的相應人員的待辦事項清單。

   如果在提交表單之前必須關閉表單，而且不丟失您輸入的資料，則保存草稿並稍後完成（如果流程允許）。 如果表單和進程允許，也可以按一下 **離線** 然後從Adobe®Reader®或Adobe®Acrobat®專業或Acrobat Standard提交。

   >[!NOTE]
   >
   >離線選項僅可用於PDF forms。

## 添加附註和附件 {#adding-notes-and-attachments}

如果流程允許，您可以向流程添加附註和檔案附件。 您可以為參與流程的其他用戶提供查看、更新和刪除附註或附件的權限。

### 添加附註 {#add-a-note}

您可以添加多個注釋、編輯已寫入的注釋並刪除它們。 每個注釋都具有與其關聯的標題、描述和訪問權限。 可以在注釋上設定下列訪問權限之一：

* 只讀（預設權限）
* 讀取/編輯/刪除
* 讀取/編輯
* 讀取/刪除
* 無訪問權限

1. 開啟任務，然後按一下 **注釋** 頁籤。
1. 鍵入中注釋的標題 **標題** 框，並在 **注釋** 框。
1. 選擇 **權限** 級別，用於參與流程的其他用戶的注釋。
1. 按一下&#x200B;**「確定」**。包含注釋的文本檔案將附加到表單。 可通過按一下注釋並直接修改文本來更新注釋。 通過按一下 **刪除** 按鈕 ![垃圾桶的影像](assets/icondelete.png) 的下界。

### 添加附件 {#add-an-attachment}

您也可以添加有關附件的注釋。 可以對附件設定下列訪問權限之一：

* 只讀（預設權限）
* 讀取/編輯/刪除
* 讀取/編輯
* 讀取/刪除
* 無訪問權限

1. 按一下 **附件** 頁籤 **附件**。
1. 按一下 **瀏覽** 的子菜單。
1. 選擇 **權限** 其他參與流程的用戶的附件級別。 如果選擇 **閱讀**，其他用戶可以將檔案保存到本地。 如果選擇了編輯權限之一，其他用戶也可以上載新檔案以替換附件。
1. 按一下&#x200B;**「確定」**。檔案附加到窗體。 通過按一下 **刪除** 按鈕 ![垃圾桶的影像](assets/icondelete.png) 的子菜單。

## 保存表單的草稿副本 {#saving-draft-copies-of-forms}

如果您必須稍後完成並提交表單，則可以保存表單的草稿副本，以免丟失現有工作。 草稿副本將添加到「待辦事項」頁面的「草稿」類別中。

重新開啟並提交草稿表單後，草稿將從「草稿」類別中刪除。

此外，您還可以配置工作區，將用戶輸入的資訊自動保存為草稿。 有關詳細資訊，請參見 [管理首選項](/help/forms/using/getting-started-livecycle-html-workspace.md)。

>[!NOTE]
>
>「保存」按鈕對於某些表單不可用，具體取決於它所關聯的進程。

### 保存草稿副本 {#save-a-draft-copy}

1. 按一下 **保存** 的上界。 表單將添加到「待辦事項」頁面的「草稿」類別中。 您對表單所做的所有更改都將保存。

### 重新開啟草稿副本 {#reopen-a-draft-copy}

1. 在待辦事項頁面上，選擇 **草稿** 排隊，然後按一下表單的草稿副本。

   如果窗體包含一系列面板，則可能需要轉到結束上次會話的面板。

## 將進程添加到收藏夾類別 {#adding-processes-to-the-favorites-category}

您可以將任何進程添加到收藏夾類別。 通過設定收藏夾，您可以將您經常啟動的所有進程分組到一個類別中，以便您能夠快速找到它們。

>[!NOTE]
>
>如果通常在使用AEM Forms工作區時啟動進程，則可以設定「啟動位置」首選項，以便在啟動AEM Forms工作區時自動顯示「收藏夾」類別。 有關詳細資訊，請參閱中的「管理首選項」 [AEM Forms工作區入門](/help/forms/using/getting-started-livecycle-html-workspace.md)。

要將進程標籤為收藏夾，請在其類別中選擇任務，然後按一下空心星形。 那顆星星變黃了。 要取消將進程標籤為收藏夾，請再次按一下「金星」。
