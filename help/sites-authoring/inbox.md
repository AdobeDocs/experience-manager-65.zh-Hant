---
title: 管理任務的收件箱
description: 使用收件箱管理任務。
uuid: ddd48019-ce69-4a47-be2b-5b66ae2fe3c8
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 8b607b55-2412-469f-856b-0a3dea4b0efb
exl-id: 80b7f179-b011-4f90-b5ab-9ef8a669d271
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 11%

---

# 您的收件匣{#your-inbox}

您可以從AEM的各個區域收到通知，包括工作流程和專案；例如，關於：

* 任務:

   * 這些也可以在AEM UI內的各個時間點建立，例如在 **專案**,
   * 這些可以是工作流程的產品 **建立任務** 或 **建立項目任務** 步驟。

* 工作流程:

   * 代表您需要對頁面內容執行之動作的工作項目；

      * 這些是工作流程的產品 **參與者** 步驟
   * 失敗項目，以允許管理員重試失敗的步驟。


您會在自己的收件匣中收到這些通知，您可在此檢視並採取行動。

>[!NOTE]
>
>現成可用的AEM會預先載入指派給管理員使用者群組的管理工作。 請參閱 [現成可用的管理任務](#out-of-the-box-administrative-tasks) 以取得詳細資訊。

>[!NOTE]
>
>有關項目類型的詳細資訊，另請參閱：
>
>* [專案](/help/sites-authoring/touch-ui-managing-projects.md)
>* [項目 — 使用任務](/help/sites-authoring/task-content.md)
>* [工作流程](/help/sites-authoring/workflows.md)
>* [Forms](/help/forms/home.md)
>


## 標題中的收件匣 {#inbox-in-the-header}

從任何主控台中，收件匣中目前的項目數會顯示在標題中。 也可以開啟指示器以提供對需要操作的頁面的快速訪問，或訪問收件箱：

![wf-80](assets/wf-80.png)

>[!NOTE]
>
>某些動作也會顯示在 [適當資源的卡片檢視](/help/sites-authoring/basic-handling.md#card-view).

## 現成可用的管理任務  {#out-of-the-box-administrative-tasks}

現成可用的AEM會預先載入指派給管理員使用者群組的四個工作。

* [設定分析和定位](/help/sites-administering/opt-in.md)
* [套用 AEM 安全檢查清單](/help/sites-administering/security-checklist.md)
* 啟用彙總使用狀況統計資料的收集
* [設定 HTTPS](/help/sites-administering/ssl-by-default.md)

## 開啟收件匣 {#opening-the-inbox}

若要開啟AEM通知收件匣：

1. 按一下/點選工具列中的指示器。

1. 選擇「 **全部查看**」。「 **AEM收件匣** 」將會開啟。收件匣會顯示工作流程、專案和工作中的項目。
1. 預設視圖是「列 [表視圖](#inbox-list-view)」，但您也可以切換到「日 [歷視圖」](#inbox-calendar-view)。這是使用檢視選取器 (工具列，右上方) 完成。

   對於這兩個檢視，您也可以定義 [檢視設定](#inbox-view-settings);可用的選項取決於當前視圖。

   ![wf-79](assets/inbox-list-view.png)

>[!NOTE]
>
>收件箱作為控制台運行，因此，在您完成 [後，使用全局導航](/help/sites-authoring/basic-handling.md#global-navigation)[](/help/sites-authoring/search.md) 或搜索導航到其他位置。

### 收件箱 — 清單視圖 {#inbox-list-view}

此檢視會列出所有項目，以及主要相關資訊：

![wf-82](assets/wf-82.png)

### 收件箱 — 日曆視圖 {#inbox-calendar-view}

此視圖會根據項目在日曆中的位置和您選擇的精確視圖顯示項目：

![wf-93](assets/wf-93.png)

您可以：

* 選擇特定視圖； **時間表**, **欄**, **清單**

* 指定要根據 **排程**; **全部**, **已規劃**, **進行中**, **即將到期**, **過期**

* 深入查看有關物料的詳細資訊
* 選取要聚焦檢視的日期範圍：

![wf-91](assets/wf-91.png)

### 收件匣 — 設定 {#inbox-view-settings}

對於兩個檢視（清單和日曆），您可以定義設定：

* **日曆檢視**

   針對 **日曆檢視** 您可以設定：

   * **分組依據**
   * **排程** 或無 ****
   * **卡片大小**

   ![wf-92](assets/wf-92.png)

* **清單檢視**

   針對 **清單檢視** 您可以配置排序機制：

   * **排序欄位**
   * **排序順序**

   ![wf-83](assets/inbox-settings.png)

### 收件匣 — 管理控制 {#inbox-admin-control}

「管理控制」選項可讓管理員：

* 自訂AEM收件匣欄

* 自訂標題文字和標誌

* 控制頁首中可用導航連結的顯示

「管理控制」選項只對 `administrators` 或 `workflow-administrators` 群組。

* **欄自訂**:自訂AEM收件匣以變更欄的預設標題、重新排序欄的位置，以及根據工作流程的資料顯示其他欄。
   * **添加列**:選取要新增至AEM收件匣的欄。
   * **編輯欄**:將滑鼠暫留在欄標題上，然後點選 ![編輯](assets/edit.svg) 表徵圖，輸入列顯示名稱。
   * **刪除列**:點選 ![刪除](assets/delete_updated.svg) 圖示以從AEM收件匣中刪除欄。
   * **移動列**:拖曳 ![移動](assets/move_updated.svg) 圖示將欄移至AEM收件匣中的新位置。

   ![admin-control](assets/admin-control-column-customize.png)

* **品牌自訂**

   * **自訂標題文字：** 指定要在標題中顯示的文字以取代預設 **Adobe Experience Manager** 文字。

   * **自定義徽標：** 指定要在標題中顯示為標誌的影像。 在數位資產管理(DAM)中上傳影像，並在欄位中參照該影像。

* **使用者導覽**
   * **隱藏導航選項：** 選擇此選項可隱藏頁首中可用的導航選項。 導覽選項包括其他解決方案的連結、說明連結，以及點選Adobe Experience Manager標誌或文字時可用的製作選項。
* **儲存：** 點選/按一下此選項以儲存設定。

## 對項目採取操作 {#taking-action-on-an-item}

>[!NOTE]
>
>雖然可以選取多個項目，但一次只能對一個項目執行動作。


1. 要對項目執行操作，請為相應項目選擇縮圖。 適用於該項目的動作圖示會顯示在工具列中：

   ![wf-84](assets/wf-84.png)

   這些動作適合項目，包括：

   * **完成** 行動；例如，任務或工作流項。
   * **重新指派**/**委派** 項目。
   * **開啟** 物品；根據項目類型，此動作可以：

      * 顯示項目屬性
      * 開啟適當的控制面板或精靈以執行進一步動作
      * 開啟相關檔案
   * **後退** 改為上一步。
   * 檢視工作流程的裝載。
   * 從項目建立專案。

   >[!NOTE]
   >
   >如需進一步詳細資訊，請參閱：
   >
   >* 工作流程項目 —  [參與工作流程](/help/sites-authoring/workflows-participating.md)


1. 根據所選項目，將啟動操作；例如：

   * 將開啟與動作相適合的對話方塊。
   * 將啟動操作嚮導。
   * 檔案頁面將會開啟。

   例如， **重新指派** 將開啟對話方塊：

   ![wf-85](assets/wf-85.png)

   根據是否開啟了對話框、嚮導和文檔頁，您可以：

   * 確認適當的動作；例如重新指派。
   * 取消動作。
   * 後箭；例如，如果操作嚮導或文檔頁面已開啟，則可以返回「收件箱」。


## 建立任務 {#creating-a-task}

從收件箱中，您可以建立任務：

1. 選擇 **建立**，然後 **任務**.
1. 填妥 **基本** 和 **進階** 標籤；只有 **標題** 為必填項目，其他所有項目則為選用項目：

   * **基本**:

      * **標題**
      * **專案**
      * **被指派者**
      * **內容**;與裝載類似，這是從任務到儲存庫中某個位置的參考
      * **說明**
      * **任務優先順序**
      * **開始日期**
      * **到期日期**

   ![wf-86](assets/wf-86.png)

   * **進階**

      * **名稱**:這將用來形成URL;若空白，則會以 **標題**.

   ![wf-87](assets/wf-87.png)

1. 選擇 **提交**.

## 建立專案 {#creating-a-project}

對於某些任務，您可以建立 [專案](/help/sites-authoring/projects.md) 基於該任務：

1. 點選/按一下縮圖，以選取適當的任務。

   >[!NOTE]
   >
   >僅使用 **建立** 選項 **收件匣** 可用來建立專案。
   >
   >無法使用工作項目（來自工作流程）來建立專案。

1. 從工 **具列選擇** 「建立專案」以開啟精靈。
1. 選取適當的範本，然後 **下一個**.
1. 指定所需的屬性：

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
   >請參閱 [建立專案](/help/sites-authoring/touch-ui-managing-projects.md#creating-a-project) 以取得完整資訊。

1. 選擇 **建立** 以確認動作。

## 篩選AEM收件匣中的項目 {#filtering-items-in-the-aem-inbox}

您可以篩選列出的項目：

1. 開啟 **AEM收件匣**.

1. 開啟篩選選擇器：

   ![wf-88](assets/wf-88.png)

1. 您可以根據一系列條件來篩選列出的項目，其中許多條件可以細化；例如：

   ![wf-89](assets/wf-89.png)

   >[!NOTE]
   >
   >使用 [檢視設定](#inbox-view-settings) 您也可以在使用 [清單檢視](#inbox-list-view).
