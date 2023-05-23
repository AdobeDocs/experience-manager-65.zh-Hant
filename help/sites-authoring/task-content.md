---
title: 使用任務
seo-title: Working with Tasks
description: 任務表示要針對內容完成的工作項，並用於項目以確定當前任務的完整程度
seo-description: Tasks represent items of work to be done on content and are used in projects to determine the level of completeness of current tasks
uuid: df4efb3f-8298-4159-acfe-305ba6b46791
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: 1b79d373-73f4-4228-b309-79e74d191f3e
exl-id: a0719745-8d67-44bc-92ba-9ab07f31f8d2
source-git-commit: 200b47070b7ead54ee54eea504bd960d4e0731d9
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 3%

---


# 使用任務 {#working-with-tasks}

任務指要針對內容執行的工作項。 分配任務後，該任務將顯示在工作流收件箱中。 任務項可以根據 **類型** 的雙曲餘切值。

項目中還使用任務來確定項目的完整性級別。

## 跟蹤項目進度 {#tracking-project-progress}

您可以通過查看由 **任務** 平鋪。 項目進度可由以下方式確定：

* **任務平鋪：** 項目的總體進度在任務磁貼中顯示，可在項目詳細資訊頁面上找到。

* **任務清單：** 按一下任務平鋪時，將顯示任務清單。 此清單包含與項目相關的所有任務的詳細資訊。

兩個選項都列出工作流任務以及您直接在任務磁貼中建立的任務。

### 任務平鋪 {#task-tile}

如果項目有任何相關任務，則項目內會顯示任務平鋪。 任務磁貼顯示項目的當前狀態。 這基於工作流內的現有任務，不包括將來隨著工作流繼續生成的任何任務。 在任務磁貼中可看到以下資訊：

* 已完成任務的百分比
* 活動任務的百分比
* 逾期任務的百分比

![任務平鋪](assets/project-tile-tasks.png)

### 查看或修改項目中的任務 {#viewing-or-modifying-the-tasks-in-a-project}

除了跟蹤進度外，您可能還希望查看有關項目的詳細資訊或修改項目。

#### 任務清單 {#task-list}

按一下任務磁貼右下角的省略號按鈕，顯示已篩選的與項目相關的任務的收件箱。 任務詳細資訊與元資料一起顯示，如到期日、受分配人、優先順序和狀態。

![項目任務收件箱](assets/project-tasks.png)

#### 任務詳細資料 {#task-details}

有關特定任務的詳細資訊，請在收件箱中點擊或按一下該任務以選擇它，然後點擊或按一下 **開啟** 的子菜單。

![任務詳細資訊](assets/project-task-detail.png)

您可以通過不同的頁籤查看、編輯或向任務添加詳細資訊。

* **任務**  — 一般任務資訊
* **項目資訊**  — 任務關聯的項目摘要
* **工作流到**  — 任務關聯的工作流摘要（如果適用）
* **注釋**  — 對任務本身的一般性評論

### 添加任務 {#adding-tasks}

可以向項目添加新任務。 然後，這些任務將顯示在任務磁貼中，並可在通知收件箱中使用，這樣您就能瞭解未完成的任務。

要添加任務：

1. 在項目中，找到 **任務** 瓦
1. 點擊或按一下拼貼右上角的向下字形並選擇 **建立任務**。
1. 在 **添加任務** 窗口，提供任務詳細資訊，如優先順序、受分配人和到期日期。

   ![添加任務](assets/project-add-task.png)

1. 點擊或按一下 **提交**。

## 在收件箱中處理任務 {#working-with-tasks-in-the-inbox}

您不能從項目本身訪問項目任務，而是可以直接從收件箱訪問它們。 收件箱將為您提供跨項目任務的概覽，以便您瞭解整個工作流。

在收件箱中，您可以開啟任務並設定任務狀態。 當將任務分配給您所屬的用戶組時，這些任務也會顯示在收件箱中。 在這種情況下，組的任何成員都可以執行工作並完成任務。

![收件匣](assets/project-inbox.png)

要完成任務，請選擇該任務，然後按一下 **完成** 的子菜單。 向任務中添加資訊，然後按一下 **完成**。 請參閱 [收件箱](/help/sites-authoring/inbox.md) 的子菜單。
