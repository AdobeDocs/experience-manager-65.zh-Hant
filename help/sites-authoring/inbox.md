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

您可以從各個領域接收通知AEM，包括工作流和項目；例如，關於：

* 任務:

   * 也可在UI內的各個點建立AEM這些，例如，在 **項目**。
   * 這些可以是工作流的產品 **建立任務** 或 **建立項目任務** 的子菜單。

* 工作流程:

   * 表示您需要在頁面內容上執行的操作的工作項目；

      * 這些是工作流的產品 **參與者** 步驟
   * 失敗項，允許管理員重試失敗的步驟。


您可以在自己的收件箱中接收這些通知，您可以在此查看這些通知並採取行動。

>[!NOTE]
>
>現成版本預裝AEM有分配給管理員用戶組的管理任務。 請參閱 [現成管理任務](#out-of-the-box-administrative-tasks) 的雙曲餘切值。

>[!NOTE]
>
>有關項目類型的詳細資訊，另請參閱：
>
>* [專案](/help/sites-authoring/touch-ui-managing-projects.md)
>* [項目 — 使用任務](/help/sites-authoring/task-content.md)
>* [工作流程](/help/sites-authoring/workflows.md)
>* [Forms](/help/forms/home.md)
>


## 標題中的收件箱 {#inbox-in-the-header}

在任何控制台中，收件箱中的當前項目數都顯示在標題中。 還可以開啟指示器，以便快速訪問需要操作的頁面或訪問收件箱：

![wf-80](assets/wf-80.png)

>[!NOTE]
>
>某些操作也將顯示在 [相應資源的卡視圖](/help/sites-authoring/basic-handling.md#card-view)。

## 現成管理任務  {#out-of-the-box-administrative-tasks}

現成版本預裝了AEM分配給管理員用戶組的四項任務。

* [設定分析和定位](/help/sites-administering/opt-in.md)
* [套用 AEM 安全檢查清單](/help/sites-administering/security-checklist.md)
* 啟用彙總使用狀況統計資料的收集
* [設定 HTTPS](/help/sites-administering/ssl-by-default.md)

## 開啟收件箱 {#opening-the-inbox}

要開啟通知收AEM件箱：

1. 按一下/點擊工具欄中的指示器。

1. 選擇「 **全部查看**」。「 **AEM收件匣** 」將會開啟。收件匣會顯示工作流程、專案和工作中的項目。
1. 預設視圖是「列 [表視圖](#inbox-list-view)」，但您也可以切換到「日 [歷視圖」](#inbox-calendar-view)。這是使用檢視選取器 (工具列，右上方) 完成。

   對於這兩個視圖，您還可以定義 [查看設定](#inbox-view-settings);可用選項取決於當前視圖。

   ![wf-79](assets/inbox-list-view.png)

>[!NOTE]
>
>收件箱作為控制台運行，因此，在您完成 [後，使用全局導航](/help/sites-authoring/basic-handling.md#global-navigation)[](/help/sites-authoring/search.md) 或搜索導航到其他位置。

### 收件箱 — 清單視圖 {#inbox-list-view}

此視圖列出所有項目以及關鍵相關資訊：

![wf-82](assets/wf-82.png)

### 收件箱 — 日曆視圖 {#inbox-calendar-view}

此視圖根據項目在日曆中的位置和您選擇的精確視圖顯示項目：

![wf-93](assets/wf-93.png)

您可以：

* 選擇特定視圖； **時間軸**。 **列**。 **清單**

* 指定根據 **計畫**; **全部**。 **計畫**。 **正在進行**。 **即將到期**。 **過期**

* 向下鑽取以獲取有關物料的詳細資訊
* 選擇日期範圍以集中查看：

![wf-91](assets/wf-91.png)

### 收件箱 — 設定 {#inbox-view-settings}

對於兩個視圖（「清單」和「日曆」），可以定義設定：

* **日曆檢視**

   對於 **日曆視圖** 您可以配置：

   * **分組依據**
   * **排程** 或無 ****
   * **卡大小**

   ![wf-92](assets/wf-92.png)

* **清單檢視**

   對於 **清單視圖** 可以配置排序機制：

   * **排序欄位**
   * **排序順序**

   ![wf-83](assets/inbox-settings.png)

### 收件箱 — 管理控制 {#inbox-admin-control}

管理控制選項使管理員能夠：

* 自定義收AEM件箱列

* 自定義標題文本和徽標

* 控制標題中可用導航連結的顯示

「管理控制」選項僅對的成員可見 `administrators` 或 `workflow-administrators` 組。

* **列自定義**:自定義收AEM件箱以更改列的預設標題、重新排序列的位置，並根據工作流的資料顯示附加列。
   * **添加列**:選擇要添加到收件箱的AEM列。
   * **編輯列**:將滑鼠懸停在列標題上，然後點擊 ![編輯](assets/edit.svg) 表徵圖，輸入列顯示名稱。
   * **刪除列**:點擊 ![刪除](assets/delete_updated.svg) 表徵圖，從收件箱中刪AEM除列。
   * **移動列**:拖動 ![移動](assets/move_updated.svg) 表徵圖將列移到收件箱中的新AEM位置。

   ![管理控制](assets/admin-control-column-customize.png)

* **品牌自訂**

   * **自定義標題文本：** 指定要在標題中顯示的文本以替換預設 **Adobe Experience Manager** 的子菜單。

   * **自定義徽標：** 指定要在標題中顯示為徽標的影像。 在數字資產管理(DAM)中上載影像，並參考現場中的該影像。

* **使用者導覽**
   * **隱藏導航選項：** 選擇此選項可隱藏標題中可用的導航選項。 導航選項包括指向其他解決方案的連結、幫助連結以及點擊Adobe Experience Manager徽標或文本時可用的創作選項。
* **保存：** 點擊/按一下此選項以保存設定。

## 對物料執行操作 {#taking-action-on-an-item}

>[!NOTE]
>
>雖然可以選擇多個項，但一次只能對一個項執行操作。


1. 要對項目執行操作，請為相應項目選擇縮略圖。 適用於該項目的操作的表徵圖將顯示在工具欄中：

   ![wf-84](assets/wf-84.png)

   這些操作適用於項目，包括：

   * **完成** 行動；例如，任務或工作流項。
   * **重新分配**/**委託** 項目。
   * **開啟** 物品；根據項類型，此操作可以：

      * 顯示項屬性
      * 開啟適當的儀表板或嚮導以執行進一步操作
      * 開啟相關文檔
   * **後退** 上一步。
   * 查看工作流的負載。
   * 從項建立項目。

   >[!NOTE]
   >
   >如需進一步詳細資訊，請參閱：
   >
   >* 工作流項 —  [參與工作流](/help/sites-authoring/workflows-participating.md)


1. 根據選定的項目，將啟動操作；例如：

   * 將開啟與操作相適應的對話框。
   * 將啟動操作嚮導。
   * 將開啟文檔頁面。

   比如說， **重新分配** 將開啟對話框：

   ![wf-85](assets/wf-85.png)

   根據是否開啟了對話框、嚮導和文檔頁，您可以：

   * 確認相應的操作；例如重新分配。
   * 取消操作。
   * 後箭頭；例如，如果操作嚮導或文檔頁面已開啟，則可以返回「收件箱」。


## 建立任務 {#creating-a-task}

在收件箱中，您可以建立任務：

1. 選擇 **建立**，則 **任務**。
1. 完成 **基本** 和 **高級** 頁籤；只有 **標題** 是必填項，其他所有項都是可選項：

   * **基本**:

      * **標題**
      * **專案**
      * **被指派者**
      * **內容**;與負載類似，這是從任務到儲存庫中某個位置的引用
      * **說明**
      * **任務優先順序**
      * **開始日期**
      * **到期日期**

   ![wf-86](assets/wf-86.png)

   * **進階**

      * **名稱**:將用於形成URL;如果為空，則基於 **標題**。

   ![wf-87](assets/wf-87.png)

1. 選擇 **提交**。

## 建立項目 {#creating-a-project}

對於某些任務，您可以建立 [項目](/help/sites-authoring/projects.md) 基於該任務：

1. 按一下/按一下縮略圖，選擇相應的任務。

   >[!NOTE]
   >
   >僅使用 **建立** 選項 **收件箱** 可用於建立項目。
   >
   >無法使用工作流中的工作項建立項目。

1. 從工 **具列選擇** 「建立專案」以開啟精靈。
1. 選擇相應模板，然後 **下一個**。
1. 指定所需的屬性：

   * **基本**

      * **標題**
      * **說明**
      * **開始日期**
      * **到期日期**
      * **用戶** 角色
   * **進階**

      * **名稱**
   >[!NOTE]
   >
   >請參閱 [建立項目](/help/sites-authoring/touch-ui-managing-projects.md#creating-a-project) 的雙曲餘切值。

1. 選擇 **建立** 確認操作。

## 篩選收件箱中的AEM項 {#filtering-items-in-the-aem-inbox}

您可以篩選列出的項：

1. 開啟 **收件箱AEM**。

1. 開啟篩選器選擇器：

   ![wf-88](assets/wf-88.png)

1. 您可以根據一系列標準篩選列出的項目，其中許多可以細化；例如：

   ![wf-89](assets/wf-89.png)

   >[!NOTE]
   >
   >與 [查看設定](#inbox-view-settings) 也可以在使用 [清單視圖](#inbox-list-view)。
