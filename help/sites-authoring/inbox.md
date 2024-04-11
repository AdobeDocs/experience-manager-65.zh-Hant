---
title: 管理任務的收件匣
description: 使用Adobe Experience Manager 6.5中的收件匣管理您的工作。
exl-id: 80b7f179-b011-4f90-b5ab-9ef8a669d271
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 8%

---

# 您的收件匣{#your-inbox}

您可以從AEM的各種區域接收通知，包括工作流程和專案；例如，關於：

* 任務：

   * 這些也可以在AEM UI中的不同位置建立，例如 **專案**，
   * 這些可以是工作流程的產物 **建立任務** 或 **建立專案任務** 步驟。

* 工作流程：

   * 代表您需要對頁面內容執行之動作的工作專案；

      * 這些是工作流程的產物 **參與者** 步驟

   * 失敗專案，讓管理員重試失敗的步驟。

您會在自己的收件匣中收到這些通知，您可以在其中檢視通知並採取行動。

>[!NOTE]
>
>現成可用的AEM會預先載入指派給管理員使用者群組的管理任務。 另請參閱 [現成可用的管理工作](#out-of-the-box-administrative-tasks) 以取得詳細資訊。

>[!NOTE]
>
>如需有關料號型態的進一步資訊，另請參閱：
>
>* [專案](/help/sites-authoring/touch-ui-managing-projects.md)
>* [專案 — 使用任務](/help/sites-authoring/task-content.md)
>* [工作流程](/help/sites-authoring/workflows.md)
>* [Forms](/help/forms/using/introduction-aem-forms.md)
>

## 標題中的收件匣 {#inbox-in-the-header}

在任一控制檯中，收件匣中目前的專案數量會顯示在標題中。 也可以開啟指示器，提供對需要動作的頁面的快速存取許可權或收件匣的存取許可權：

![wf-80](assets/wf-80.png)

>[!NOTE]
>
>某些動作也會顯示在 [適當資源的卡片檢視](/help/sites-authoring/basic-handling.md#card-view).

## 現成可用的管理工作  {#out-of-the-box-administrative-tasks}

現成可用的AEM預先載入了指派給管理員使用者群組的四個任務。

* [設定分析和定位](/help/sites-administering/opt-in.md)
* [套用 AEM 安全檢查清單](/help/sites-administering/security-checklist.md)
* 啟用彙總使用狀況統計資料的收集
* [設定 HTTPS](/help/sites-administering/ssl-by-default.md)

## 開啟收件匣 {#opening-the-inbox}

若要開啟AEM通知收件匣：

1. 按一下工具列中的指示器。

1. 選擇「 **全部查看**」。此 **AEM收件匣** 隨即開啟。 收件匣會顯示工作流程、專案和工作中的項目。
1. 預設視圖是「列 [表視圖](#inbox-list-view)」，但您也可以切換到「日 [歷視圖」](#inbox-calendar-view)。這是使用檢視選取器 (工具列，右上方) 完成。

   對於這兩個檢視，您也可以定義 [檢視設定](#inbox-view-settings)；可用的選項取決於目前檢視。

   ![wf-79](assets/inbox-list-view.png)

>[!NOTE]
>
>收件箱作為控制台運行，因此，在您完成 [後，使用全局導航](/help/sites-authoring/basic-handling.md#global-navigation)[](/help/sites-authoring/search.md) 或搜索導航到其他位置。

### 收件匣 — 清單檢視 {#inbox-list-view}

此檢視會列出所有專案，以及主要的相關資訊：

![wf-82](assets/wf-82.png)

### 收件匣 — 行事曆檢視 {#inbox-calendar-view}

此檢視會根據專案在行事曆中的位置以及您選取的精確檢視來顯示專案：

![wf-93](assets/wf-93.png)

您可以：

* 選取特定檢視； **時間表**， **欄**， **清單**

* 指定要根據以下條件顯示的任務： **排程**； **全部**， **計畫**， **進行中**， **即將到期**， **過期**

* 向下展開以取得專案的詳細資訊
* 選取日期範圍以聚焦檢視：

![wf-91](assets/wf-91.png)

### 收件匣 — 設定 {#inbox-view-settings}

對於這兩個檢視（「清單」和「行事曆」），您可以定義設定：

* **日曆檢視**

  的 **行事曆檢視** 您可以設定：

   * **分組依據**
   * **排程** 或無 ****
   * **卡片大小**

  ![wf-92](assets/wf-92.png)

* **清單檢視**

  的 **清單檢視** 您可以設定排序機制：

   * **排序欄位**
   * **排序順序**

  ![wf-83](assets/inbox-settings.png)

### 收件匣 — 管理員控制 {#inbox-admin-control}

管理員控制選項可讓管理員：

* 自訂AEM收件匣欄

* 自訂頁首文字和標誌

* 控制標題中可用導覽連結的顯示

「管理員控制」選項僅對成員可見。 `administrators` 或 `workflow-administrators` 群組。

* **欄自訂**：自訂AEM收件匣以變更欄的預設標題、重新排序欄的位置，以及根據工作流程的資料顯示其他欄。
   * **新增欄**：選取要新增至AEM收件匣的欄。
   * **編輯欄**：將滑鼠停留在欄標題上並選取 ![編輯](assets/edit.svg) 圖示以輸入欄顯示名稱。
   * **刪除欄**：選取 ![刪除](assets/delete_updated.svg) 圖示可從AEM收件匣中刪除欄。
   * **移動欄**：拖曳 ![移動](assets/move_updated.svg) 圖示將欄移至AEM收件匣中的新位置。

  ![admin-control](assets/admin-control-column-customize.png)

* **品牌自訂**

   * **自訂頁首文字：** 指定要在標題中顯示的文字以取代預設文字 **Adobe Experience Manager** 文字。

   * **自訂標誌：** 指定要在頁首中顯示的影像為標誌。 在數位資產管理(DAM)中上傳影像，並在欄位中參照該影像。

* **使用者導覽**
   * **隱藏導覽選項：** 選取此選項可隱藏標題中可用的導覽選項。 導覽選項包含其他解決方案的連結、說明連結，以及點選Adobe Experience Manager標誌或文字時可用的撰寫選項。
* **儲存：** 按一下此選項以儲存設定。

## 對專案執行動作 {#taking-action-on-an-item}

>[!NOTE]
>
>雖然可以選取多個專案，但一次只能對一個專案執行動作。


1. 若要對專案執行動作，請選取適當專案的縮圖。 適用於該專案的動作圖示會顯示在工具列中：

   ![wf-84](assets/wf-84.png)

   這些動作適用於該專案，包括：

   * **完成** 動作；例如，任務或工作流程專案。
   * **重新指派**/**委派** 一個專案。
   * **開啟** 專案；視專案型別而定，此動作可以：

      * 顯示專案屬性
      * 開啟適當的儀表板或精靈以進一步動作
      * 開啟相關檔案

   * **後退** 到上一步。
   * 檢視工作流程的裝載。
   * 從專案建立專案。

   >[!NOTE]
   >
   >如需進一步詳細資訊，請參閱：
   >
   >* 工作流程專案 —  [參與工作流程](/help/sites-authoring/workflows-participating.md)

1. 視選取的專案而定，將會啟動動作；例如：

   * 將會開啟適合此動作的對話方塊。
   * 將會啟動動作精靈。
   * 將會開啟檔案頁面。

   例如， **重新指派** 開啟對話方塊：

   ![wf-85](assets/wf-85.png)

   視是否已開啟對話方塊、精靈、檔案頁面而定，您可以：

   * 確認適當的動作；例如，重新指派。
   * 取消動作。
   * 後退箭頭；例如，如果動作精靈或檔案頁面已開啟，您可以返回「收件匣」。

## 建立任務 {#creating-a-task}

您可以從收件匣建立任務：

1. 選取 **建立**，然後 **任務**.
1. 填妥 **基本** 和 **進階** 標籤；僅限 **標題** 為必要專案，其他專案則為選用專案：

   * **基本**：

      * **標題**
      * **專案**
      * **被指定者**
      * **內容**；與「裝載」類似，這是從任務到存放庫中的位置的參照
      * **說明**
      * **任務優先順序**
      * **開始日期**
      * **到期日期**

   ![wf-86](assets/wf-86.png)

   * **進階**

      * **名稱**：這會用來組成URL；如果留空，則會根據 **標題**.

   ![wf-87](assets/wf-87.png)

1. 選取 **提交**.

## 建立專案 {#creating-a-project}

您可以針對特定工作建立 [專案](/help/sites-authoring/projects.md) 根據該任務：

1. 點選/按一下縮圖，選取適當的工作。

   >[!NOTE]
   >
   >僅限使用建立的任務 **建立** 的選項 **收件匣** 可用來建立專案。
   >
   >工作專案（來自工作流程）無法用於建立專案。

1. 從工 **具列選擇** 「建立專案」以開啟精靈。
1. 選取適當的範本，然後 **下一個**.
1. 指定必要的屬性：

   * **基本**

      * **標題**
      * **說明**
      * **開始日期**
      * **到期日期**
      * **使用者** 和角色

   * **進階**

      * **名稱**

   >[!NOTE]
   >
   >另請參閱 [建立專案](/help/sites-authoring/touch-ui-managing-projects.md#creating-a-project) 以取得完整資訊。

1. 選取 **建立** 以確認動作。

## 篩選AEM收件匣中的專案 {#filtering-items-in-the-aem-inbox}

您可以篩選列出的專案：

1. 開啟 **AEM收件匣**.

1. 開啟篩選選擇器：

   ![wf-88](assets/wf-88.png)

1. 您可以根據一系列條件篩選列出的專案，其中許多條件可以細化；例如：

   ![wf-89](assets/wf-89.png)

   >[!NOTE]
   >
   >替換為 [檢視設定](#inbox-view-settings) 您也可以在使用時設定排序順序 [清單檢視](#inbox-list-view).
