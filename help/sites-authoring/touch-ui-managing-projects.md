---
title: 管理專案
seo-title: Managing Projects
description: 專案可讓您將資源分組為一個可在「專案」主控台中存取和管理的實體，借此組織專案
seo-description: Projects lets you organize your project by grouping resources into one entity which can be acessed and managed intheProjects console
uuid: ac937582-181f-429b-9404-3c71d1241495
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: fb354c72-debb-4fb6-9ccf-56ff5785c3ae
exl-id: 62586c8e-dab4-4be9-a44a-2c072effe3c0
source-git-commit: 200b47070b7ead54ee54eea504bd960d4e0731d9
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 1%

---


# 管理專案 {#managing-projects}

在 **專案** 主控台，您可以存取和管理您的專案。

![專案主控台](assets/projects-console.png)

使用控制台，您可以建立專案、將資源與專案建立關聯，以及刪除專案或資源連結。

## 存取需求 {#access-requirements}

專案標準AEM功能，不需要任何額外設定。

不過，若要讓專案中的使用者在使用專案時查看其他使用者/群組（例如建立專案、建立工作/工作流程或檢視和管理團隊時），這些使用者必須具有讀取存取權 `/home/users` 和 `/home/groups`.

最簡單的方法就是 **專案 — 使用者** 群組讀取存取權 `/home/users` 和 `/home/groups`.

## 建立專案 {#creating-a-project}

請依照下列步驟建立新專案。

1. 在 **專案** 主控台，點選或按一下 **建立** 開啟 **建立專案** 嚮導。
1. 選取範本，然後按一下 **下一個**. 您可以進一步了解標準專案範本 [這裡。](/help/sites-authoring/projects.md#project-templates)

   ![建立專案精靈](assets/create-project-wizard.png)

1. 定義 **標題** 和 **說明** 並新增 **縮圖** 影像（如果需要）。 您也可以新增或刪除使用者，以及使用者所屬的群組。

   ![嚮導的屬性步驟](assets/create-project-wizard-properties.png)

1. 點選/按一下 **建立**. 確認會詢問您是否要開啟新專案或返回主控台。

所有專案範本的建立程式都相同。 項目類型之間的差異與可用項目有關 [使用者角色](/help/sites-authoring/projects.md) 和 [工作流程。](/help/sites-authoring/projects-with-workflows.md)

### 將資源與您的專案關聯 {#associating-resources-with-your-project}

專案可讓您將資源分組為一個實體，以便將其整體管理。 因此，您需要將資源與專案建立關聯。 這些資源在專案中分組為 **圖磚**. 可新增的資源類型於 [專案圖磚](/help/sites-authoring/projects.md#project-tiles).

將資源與項目關聯：

1. 從 **專案** 控制台。
1. 點選/按一下 **添加磁貼** 並選取您要連結至專案的圖磚。 您可以選取多種圖磚類型。

   ![添加磁貼](assets/project-add-tile.png)

1. 點選/按一下 **建立**. 您的資源已連結至專案，從現在開始，您就可以從專案存取。

### 將項目新增至圖磚 {#adding-items-to-a-tile}

在某些圖磚中，您可能想要新增多個項目。 例如，您可能一次執行多個工作流程或執行多個體驗。

若要將項目新增至圖磚：

1. 在 **專案**，導覽至專案，然後按一下您要新增項目的圖磚右上角的向下>形圖示，並選取適當的選項。

   * 選項取決於圖磚的類型。 例如，它可能是 **建立任務** 針對 **工作** 拼貼或 **開始工作流程** 針對 **工作流程** 方塊。

   ![Tile雪佛龍](assets/project-tile-create-task.png)

1. 將項目新增至圖磚，如同建立新圖磚時一樣。 說明專案圖磚 [這裡。](/help/sites-authoring/projects.md#project-tiles)

## 查看項目資訊 {#viewing-project-info}

專案的主要用途是將相關資訊群組在一個地方，讓資訊更方便存取且易於操作。 您有許多存取此資訊的方法。

### 開啟磁貼 {#opening-a-tile}

您可能想要查看當前表徵圖中包含的項目，或修改或刪除表徵圖中的項目。

要開啟圖磚，以便查看或修改項目：

1. 點選或按一下圖磚右下方的點圖示。

   ![任務表徵圖](assets/project-tile-tasks.png)

1. AEM會開啟主控台，顯示與圖磚相關聯的項目類型，並根據選取的專案進行篩選。

   ![專案任務](assets/project-tasks.png)

### 檢視專案時間軸 {#viewing-a-project-timeline}

專案時間軸提供上次使用專案中資產的時間。 要查看項目時間表，請按照以下步驟操作。

1. 在 **專案** 主控台，按一下或點選 **時間表** 在主控台左上角的邊欄選取器中。
   ![選擇時間軸模式](assets/projects-timeline-rail.png)
2. 在主控台中，選取您要檢視其時間軸的專案。
   ![項目時間軸視圖](assets/project-timeline-view.png)

資產會顯示在邊欄中。 完成後，使用邊欄選取器返回一般檢視。

### 檢視非作用中專案 {#viewing-active-inactive-projects}

在使用中和之間切換 [非作用中專案，](#making-projects-inactive-or-active) 在 **專案** 主控台，按一下 **切換作用中的專案** 圖示。

![切換作用中的專案圖示](assets/projects-toggle-active.png)

依預設，主控台會顯示使用中的專案。 按一下 **切換作用中的專案** 圖示切換至檢視非使用中專案。 再按一下，以切換回使用中的專案。

## 組織專案 {#organizing-projects}

有數個選項可協助組織您的專案，以保留 **專案** 主控台可管理。

### 專案資料夾 {#project-folders}

您可以在 **專案** 控制台來分組和組織類似的專案。

1. 在 **專案** 主控台點選或按一下 **建立** 然後 **建立資料夾**.

   ![建立資料夾](assets/project-create-folder.png)

1. 為資料夾輸入標題，然後按一下 **建立**.

1. 資料夾會新增至主控台。

您現在可以在資料夾中建立專案。 您可以建立多個資料夾，也可以巢狀內嵌資料夾。

### 停用專案 {#making-projects-inactive-or-active}

如果項目已完成，您可能希望將該項目標籤為非活動項目，但仍希望保留有關該項目的資訊。 [非使用中專案現在會顯示](#viewing-active-inactive-projects) 依預設，在 **專案** 控制台。

若要讓專案停用，請依照下列步驟操作。

1. 開啟 **專案屬性** 的下限。
   * 您可以從主控台選取專案，或從專案內透過 **專案資訊** 方塊。
1. 在 **專案屬性** 窗口，更改 **專案狀態** 滑桿 **作用中** to **非作用中**.

   ![屬性窗口中的項目狀態選擇器](assets/project-status.png)

1. 點選或按一下 **儲存並關閉** 來儲存變更。

### 刪除專案 {#deleting-a-project}

請依照下列步驟刪除專案。

1. 導覽至 **專案** 控制台。
1. 在主控台中選取您的專案。
1. 點選或按一下 **刪除** 的下一頁。
1. AEM可在刪除專案時移除/修改相關的專案資料。 在 **刪除專案** 對話框。
   * 移除專案群組和角色
   * 刪除專案資產資料夾
   * 終止專案工作流程

   ![專案刪除選項](assets/project-delete-options.png)
1. 點選或按一下 **刪除** 刪除已選選項的項目。

若要深入了解專案自動建立的群組，請參閱 [自動建立群組](/help/sites-authoring/projects.md#auto-group-creation) 以取得詳細資訊。
