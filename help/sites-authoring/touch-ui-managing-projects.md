---
title: 管理專案
description: 專案可讓您將資源分組到一個實體中以組織您的專案，該實體可在「專案」主控台中存取和管理
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
exl-id: 62586c8e-dab4-4be9-a44a-2c072effe3c0
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 2%

---


# 管理專案 {#managing-projects}

在&#x200B;**專案**&#x200B;主控台中，您可以存取和管理您的專案。

![專案主控台](assets/projects-console.png)

使用主控台，您可以建立專案、將資源與專案建立關聯，也可以刪除專案或資源連結。

## 存取需求 {#access-requirements}

專案標準AEM功能，不需要任何其他設定。

不過，若使用者在專案中使用專案（例如當建立專案、建立任務/工作流程或檢視及管理團隊時）時檢視其他使用者/群組，這些使用者需要擁有`/home/users`和`/home/groups`的讀取存取權。

最簡單的方法是授予&#x200B;**專案 — 使用者**&#x200B;群組對`/home/users`和`/home/groups`的讀取存取權。

## 建立專案 {#creating-a-project}

請依照下列步驟建立專案。

1. 在&#x200B;**專案**&#x200B;主控台中，按一下&#x200B;**建立**&#x200B;以開啟&#x200B;**建立專案**&#x200B;精靈。
1. 選取範本並按一下[下一步] ****。 您可以在[這裡](/help/sites-authoring/projects.md#project-templates)進一步瞭解標準專案範本。

   ![建立專案精靈](assets/create-project-wizard.png)

1. 定義&#x200B;**標題**&#x200B;和&#x200B;**描述**，並視需要新增&#x200B;**縮圖**&#x200B;影像。 您也可以新增或刪除使用者，以及使用者所屬的群組。

   精靈的![屬性步驟](assets/create-project-wizard-properties.png)

1. 按一下「**建立**」。確認會詢問您是要開啟新專案，還是返回主控台。

建立專案的程式與所有專案範本相同。 專案型別之間的差異與可用的[使用者角色](/help/sites-authoring/projects.md)和[工作流程有關。](/help/sites-authoring/projects-with-workflows.md)

### 將資源與專案建立關聯 {#associating-resources-with-your-project}

專案可讓您將資源分組到一個實體中，以便整體管理它們。 因此，您必須將資源與專案建立關聯。 這些資源在專案中群組為&#x200B;**圖磚**。 [專案拼貼](/help/sites-authoring/projects.md#project-tiles)中說明您可以新增的資源型別。

若要將資源與專案產生關聯，請執行下列動作：

1. 從&#x200B;**專案**&#x200B;主控台開啟您的專案。
1. 按一下&#x200B;**新增動態磚**，然後選取您要連結至專案的動態磚。 您可以選取多種型別的圖磚。

   ![新增圖磚](assets/project-add-tile.png)

1. 按一下「**建立**」。您的資源已連結至專案，從現在開始，您就可以從專案存取該資源。

### 將專案新增至圖磚 {#adding-items-to-a-tile}

在某些圖磚中，您可能想要新增多個專案。 例如，您可能會同時執行多個工作流程或多個體驗。

若要將專案新增至圖磚：

1. 在&#x200B;**專案**&#x200B;中，導覽至專案，然後按一下您要新增專案的圖磚右上方的向下>形圖示，並選取適當的選項。

   * 選項檢視磚型別而定。 例如，可能是&#x200B;**任務**&#x200B;拼貼的&#x200B;**建立任務**&#x200B;或&#x200B;**工作流程**&#x200B;拼貼的&#x200B;**開始工作流程**。

   ![平鋪V形](assets/project-tile-create-task.png)

1. 新增專案至圖磚，就像建立圖磚時一樣。 專案拼貼在[此處](/help/sites-authoring/projects.md#project-tiles)說明。

## 檢視專案資訊 {#viewing-project-info}

專案的主要用途是將相關資訊分組到一個位置，使其更易於存取及操作。 您有數種方式可以存取此資訊。

### 開啟拼貼 {#opening-a-tile}

您可能想要檢視目前圖磚中包含哪些專案，或修改或刪除圖磚中的專案。

若要開啟圖磚，以便檢視或修改專案：

1. 按一下圖磚右下方的省略符號圖示。

   ![任務拼貼](assets/project-tile-tasks.png)

1. AEM會開啟主控台，以顯示與圖磚關聯的專案型別，以及根據所選專案篩選專案。

   ![專案任務](assets/project-tasks.png)

### 檢視專案時間表 {#viewing-a-project-timeline}

專案時間表提供有關專案中資產上次使用時間的資訊。 若要檢視專案時間表，請按照下列步驟操作。

1. 在&#x200B;**專案**&#x200B;主控台中，按一下主控台左上角邊欄選擇器中的&#x200B;**時間表**。
   ![正在選取時間表模式](assets/projects-timeline-rail.png)
2. 在主控台中，選取您要檢視其時間軸的專案。
   ![專案時間表檢視](assets/project-timeline-view.png)

Assets會顯示在邊欄中。 完成後，使用邊欄選擇器返回正常檢視。

### 檢視非作用中專案 {#viewing-active-inactive-projects}

若要在作用中和[非作用中專案之間切換，請在&#x200B;**專案**&#x200B;主控台中按一下&#x200B;**切換作用中專案**&#x200B;圖示。](#making-projects-inactive-or-active)

![切換使用中的專案圖示](assets/projects-toggle-active.png)

根據預設，主控台會顯示作用中的專案。 按一下&#x200B;**切換作用中專案**&#x200B;圖示，切換至檢視非作用中專案。 再按一下以切換回使用中的專案。

## 組織專案 {#organizing-projects}

有數個選項可用來協助組織您的專案，以管理&#x200B;**專案**&#x200B;主控台。

### 專案資料夾 {#project-folders}

您可以在&#x200B;**專案**&#x200B;主控台中建立資料夾，以便群組及組織類似的專案。

1. 在&#x200B;**專案**&#x200B;主控台中，按一下&#x200B;**建立**，然後按&#x200B;**建立資料夾**。

   ![建立資料夾](assets/project-create-folder.png)

1. 提供資料夾標題，然後按一下[建立]。****

1. 資料夾會新增至主控台。

您現在可以在資料夾中建立專案。 您可以建立多個資料夾，也可以巢狀內嵌資料夾。

### 停用專案 {#making-projects-inactive-or-active}

如果專案已完成，您可能想要將其標示為非使用中，但仍要保留有關專案的資訊。 [非使用中的專案現在預設會在&#x200B;**專案**&#x200B;主控台中顯示](#viewing-active-inactive-projects)。

若要停用專案，請執行下列步驟。

1. 開啟專案的&#x200B;**專案屬性**&#x200B;視窗。
   * 您可以從主控台選取專案，或透過&#x200B;**專案資訊**&#x200B;圖磚從專案內進行選取。
1. 在&#x200B;**專案屬性**&#x200B;視窗中，將&#x200B;**專案狀態**&#x200B;滑桿從&#x200B;**作用中**&#x200B;變更為&#x200B;**非作用中**。

   ![屬性視窗中的專案狀態選擇器](assets/project-status.png)

1. 按一下&#x200B;**儲存並關閉**&#x200B;以儲存變更。

### 刪除專案 {#deleting-a-project}

請依照下列步驟刪除專案。

1. 導覽至&#x200B;**專案**&#x200B;主控台的最上層。
1. 在主控台中選取您的專案。
1. 按一下工具列中的&#x200B;**刪除**。
1. 刪除專案時，AEM可以移除/修改關聯的專案資料。 在&#x200B;**刪除專案**&#x200B;對話方塊中選取您需要的選項。
   * 移除專案群組和角色
   * 刪除專案Assets資料夾
   * 終止專案工作流程

   ![專案刪除選項](assets/project-delete-options.png)
1. 按一下&#x200B;**刪除**&#x200B;刪除選取選項的專案。

若要深入瞭解專案自動建立的群組，請參閱[自動建立群組](/help/sites-authoring/projects.md#auto-group-creation)以取得詳細資料。
