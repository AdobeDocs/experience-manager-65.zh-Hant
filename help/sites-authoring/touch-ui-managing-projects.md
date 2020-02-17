---
title: 管理專案
seo-title: 管理專案
description: 專案可讓您將資源分組為一個實體，以便在Projects主控台中存取和管理，以組織專案
seo-description: 專案可讓您將資源分組為一個實體，以便在Projects主控台中存取和管理，以組織專案
uuid: ac937582-181f-429b-9404-3c71d1241495
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: fb354c72-debb-4fb6-9ccf-56ff5785c3ae
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# 管理專案{#managing-projects}

專案可讓您將資源分組為一個實體，以組織專案。

在「專 **案** 」主控台中，您可以存取專案並採取下列動作：

![chlimage_1-255](assets/chlimage_1-255.png)

在「項目」中，您可以建立項目、將資源與項目關聯，以及刪除項目或資源連結。 您可能想要開啟圖格來檢視其內容，並新增項目至圖格。 本主題介紹這些過程。

>[!NOTE]
>
>6.2引進了將專案組織在資料夾中的功能。 在「專案」頁面上，您可以建立專案或資料夾。
>
>如果已建立資料夾，使用者就會被帶到該資料夾，以便建立其他資料夾或專案。 它可協助您根據產品促銷活動、位置、翻譯語言等類別，將專案組織在資料夾中。
>
>您可以在清單檢視中檢視專案和資料夾，也可以進行搜尋。

>[!CAUTION]
>
>如果專案中的使用者在使用專案功能（例如建立專案、建立工作／工作流程、查看和管理團隊）時要查看其他使用者／群組，這些使用者必須擁有 **/home** /users **和/home/groups的讀取存取權**。 實作此項目最簡單的方式是，讓專 **案使用者群組** (projects-users **)可讀取** /home/users **和**/home/groups。

## 建立專案 {#creating-a-project}

AEM現成可用，提供下列範本供您在建立專案時選擇：

* 簡單專案
* 媒體專案
* 產品像片拍攝專案
* 翻譯專案

從專案到專案，建立專案的程式都相同。 專案類型之間的差異包括可用的使 [用者角色](/help/sites-authoring/projects.md)[和工作流程](/help/sites-authoring/projects-with-workflows.md)。  要建立新項目，請執行以下操作：

1. 在「 **專案**」中，點選／按一 **下「建立** 」以開啟「 **** 建立專案」精靈：
1. 選取範本. 立即可用的Simple Project、Media Project、 [Translation Project](/help/sites-administering/tc-manage.md)[和Product Photo Shoot Product](/help/sites-authoring/managing-product-information.md) ，然後按一下 **Next**。

   ![chlimage_1-256](assets/chlimage_1-256.png)

1. 定義「 **標題** 」和「說 **明」** ，並視需要新 **增「縮圖** 」影像。 您也可以新增或刪除使用者及其所屬的群組。 此外，按一下「 **進階** 」，新增URL中使用的名稱。

   ![chlimage_1-257](assets/chlimage_1-257.png)

1. 點選／按一下「 **建立**」。 確認會詢問您是要開啟新專案，還是要返回主控台。

### 將資源與項目關聯 {#associating-resources-with-your-project}

由於項目使您能夠將資源分組到一個實體，因此您希望將資源與項目關聯。 這些資源稱為 **Tiles**。 可添加的資源類型在「項目表徵圖」中 [有說明](/help/sites-authoring/projects.md#project-tiles)。

要將資源與您的項目關聯，請執行以下操作：

1. 從「專案」主控台 **開啟您的專** 案。
1. 點選／按 **一下「新增圖格** 」，然後選取您要連結至專案的圖格。 您可以選取多種圖格類型。

   ![chlimage_1-258](assets/chlimage_1-258.png)

   >[!NOTE]
   >
   >可以與項目關聯的項目表徵圖在項目表徵圖中有詳細 [說明。](/help/sites-authoring/projects.md#project-tiles)

1. 點選／按一下「 **建立**」。 您的資源會連結至您的專案，從現在起，您就可以從專案存取它。

### 刪除項目或資源連結 {#deleting-a-project-or-resource-link}

從控制台刪除項目或從項目中刪除連結資源的方法相同：

1. 導覽至適當的位置：

   * 若要刪除專案，請移至「專案」主控台的 **頂層** 。
   * 若要刪除專案中的資源連結，請在「專案」主控台中開 **啟專案** 。

1. 通過按一下「選擇」( **Select** )並選擇項目或資源連結進入選擇模式。
1. 點選／按一下「 **刪除**」。

1. 您必須在對話方塊中確認刪除。 如果確認，項目或資源連結將被刪除。 點選／按一下「 **取消選取** 」以退出選取模式。

>[!NOTE]
>
>當您建立專案並將使用者新增至各種角色時，系統會自動建立與專案相關的群組，以管理相關的權限。 例如，名為Myproject的專案會有三個群組 **Myproject Owners**、 **Myproject Editors**、 **Myproject Obsertors**。 不過，如果刪除專案，這些群組不會自動刪除。 管理員需要手動刪除「工具 **>安全** 性 **>** 群組 ****」。

### 新增項目至圖格 {#adding-items-to-a-tile}

在某些圖格中，您可能想要新增多個項目。 例如，您可能同時執行多個工作流程或多個體驗。

若要新增項目至圖格：

1. 在「 **專案**」中，導覽至專案，然後按一下您要新增項目的方塊上的「新增+」圖示。

   ![chlimage_1-259](assets/chlimage_1-259.png)

1. 新增項目至圖格，就像建立新圖格時一樣。 此處描述了項 [目表徵圖](/help/sites-authoring/projects.md#project-tiles)。 在此範例中，新增了另一個工作流程。

   ![chlimage_1-260](assets/chlimage_1-260.png)

### 開啟圖格 {#opening-a-tile}

您可能想要查看目前圖格中包含哪些項目，或修改或刪除圖格中的項目。

若要開啟圖格，以便檢視或修改項目：

1. 在「專案」主控台中，點選／按一下省略號(...)

   ![chlimage_1-261](assets/chlimage_1-261.png)

1. AEM會列出該方塊中的項目。 您可以進入選擇模式來修改或刪除項目。

   ![chlimage_1-262](assets/chlimage_1-262.png)

## 查看項目統計資訊 {#viewing-project-statistics}

要查看項目統計資訊，請在「項目」控 **制台中** ，單 **擊顯示統計資訊視圖**。 會顯示每個專案的完成層級。 再次 **按一下「顯示統計資料檢視** 」，前往「專 **案** 」主控台。

![chlimage_1-263](assets/chlimage_1-263.png)

### 檢視專案時間軸 {#viewing-a-project-timeline}

專案時間軸提供上次使用專案中資產的資訊。 若要檢視專案時間軸，請按一下／點選 **時間軸**，然後進入選取模式並選取專案。 資產會顯示在左窗格中。 按一下／點選 **時間軸** ，返回 **Projects控制台** 。

![chlimage_1-264](assets/chlimage_1-264.png)

### 查看活動／非活動項目 {#viewing-active-inactive-projects}

若要在作用中和非作用中專案之間切換，請在「專案」控制 **台中** ，按一 **下「切換作用中專案」**。 如果圖示旁有複選標籤，則會顯示作用中的專案。

![chlimage_1-265](assets/chlimage_1-265.png)

如果圖示旁有x，則會顯示非作用中專案。

![chlimage_1-266](assets/chlimage_1-266.png)

## 將專案設為非作用中或作用中 {#making-projects-inactive-or-active}

如果您已完成項目，但仍想保留項目的資訊，則可能希望將其設定為非活動項目。

要將項目設定為非活動（或活動），請執行以下操作：

1. 在「專 **案** 」主控台中 **，開啟專案，然後尋找** 「專案」資訊。

   >[!NOTE]
   如果您的專案中尚未加入此圖格，您可能需要加入它。 請參 [閱添加表徵圖](#adding-items-to-a-tile)。

1. 點選／按一下「 **編輯**」。
1. 將選取器從「活 **動** 」變 **更為「非活動** 」（反之亦然）。

   ![chlimage_1-267](assets/chlimage_1-267.png)

1. 點選／按一 **下「完成** 」以儲存變更。

