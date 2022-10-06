---
title: 建立並指派啟用資源
seo-title: Create and Assign Enablement Resources
description: 新增啟用資源
seo-description: Add enablement resources
uuid: da940242-0c9b-4ad8-8880-61fd41461c3b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 8fe97181-600e-42ac-af25-d5d4db248740
exl-id: 78908a9c-a260-44ff-ad1e-baa6d78ae399
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 5%

---

# 建立並指派啟用資源 {#create-and-assign-enablement-resources}

## 新增啟用資源 {#add-an-enablement-resource}

若要將啟用資源新增至新社群網站：

* 以系統管理員身分登入製作執行個體：
   * 例如， [http://localhost:4502/](http://localhost:4503/)
* 在全局導航中，選擇 **[!UICONTROL 社群]** > **[!UICONTROL 資源]**

   ![資源](assets/resources.png)

   ![啟用資源](assets/enablement-resource.png)
* 選擇要向其添加啟用資源的社區站點：
   * 選擇 **[!UICONTROL 啟用教學課程]**.
* 從功能表選取 **[!UICONTROL 建立]**.
* 選擇 **[!UICONTROL 資源]**.

![create-resource](assets/create-enablement-resource.png)

### 基本資訊 {#basic-info}

填寫資源的基本資訊：

* **[!UICONTROL 網站名稱]**

   設定為所選社區站點的名稱：啟用教學課程

* **[!UICONTROL 資源名稱(&amp;A);]**

   滑雪課程1

* **[!UICONTROL 標記]**

   教學課程：運動/滑雪

* **[!UICONTROL 在目錄中顯示]**

   設為 **開啟**.

* **[!UICONTROL 說明]**

   在雪上滑行，初學者可以。

* **[!UICONTROL 新增影像]**

   添加影像以在其「分配」視圖中將資源表示給成員。

   ![基本資訊](assets/basic-info.png)

* 選擇 **[!UICONTROL 下一個]**

### 新增內容 {#add-content}

雖然看起來好像可以選取多個資源，但僅允許一個資源。

選取 `'+' icon`，以透過識別來源來開始選擇資源的程式。

![新增內容](assets/add-content.png)

![上傳資源](assets/upload-resource.png)

上傳資源。 如果視訊資源，請上傳自訂影像以在視訊開始播放前顯示，或允許從視訊產生縮圖（可能需要幾分鐘時間 — 不需要等候）。

![上傳 — 影片](assets/upload-video.png)

* 選擇 **[!UICONTROL 下一個]**.

### 設定 {#settings}

* **[!UICONTROL 社會化設定]**

   保留預設設定，讓使用者在體驗上留下註解並評分啟用資源。

* **[!UICONTROL 到期日期]**

   *（可選）* 可以選擇完成分配的日期。

* **[!UICONTROL 資原作者]**

   *（可選）* 留空。

* **[!UICONTROL 資源聯繫人(&amp;A);]**

   *（必要）* 使用下拉菜單選擇成員 `Quinn Harper`.

* **[!UICONTROL 資源專家]**

   *（可選）* 留空。

   **附註**:如果使用者或群組未顯示，請檢查是否已將其新增至 `Community Enable Members` 群組及 *已儲存* 在發佈例項上。

   ![啟用設定](assets/enablement-settings.png)

* 選擇 **[!UICONTROL 下一個]**

### 指定任務 {#assignments}

* **[!UICONTROL 新增被指定者]**

   保留未設定，因為此啟用資源將新增至學習路徑。 如果將學習者指派給個別輔助資源，以及包含輔助資源的學習路徑，則會將學習者指派給輔助資源兩次。

   ![新增指派](assets/add-assignments.png)

* 選擇 **[!UICONTROL 建立]**

   ![create-resource](assets/create-resource.png)

成功建立資源將返回到資源控制台，並選擇新建立的資源。 在此主控台中，可發佈、新增使用者及變更其他設定。

若要上傳新版本的啟用資源，建議您建立新資源，然後從舊版中取消註冊成員，並在新版本中註冊成員。

### 發佈資源 {#publish-the-resource}

登記者必須先發佈，才能看到已分配的資源：

* 選擇世界 `Publish` 圖示

已以成功訊息確認啟動：

![publish-resource](assets/publish-resource.png)

## 新增第二個啟用資源 {#add-a-second-enablement-resource}

重複上述步驟，建立並發佈第二個相關啟用資源，從中建立學習路徑。

![add-resource](assets/add-resource.png)

**發佈** 第二個資源。

返回「啟用教學課程」的「資源」清單。

*提示：如果兩個資源都不可見，請重新整理頁面。*

![重新整理資源](assets/refresh-resource.png)

## 添加學習路徑 {#add-a-learning-path}

學習路徑是培訓資源的邏輯分組，構成課程。

* 在資源控制台中，選擇 `+ Create`
* 選擇 **[!UICONTROL 學習路徑]**

![add-learning-path](assets/add-learning-path.png)

新增 **[!UICONTROL 基本資訊]**:

* **[!UICONTROL 學習路徑名稱]**

   滑雪課

* **[!UICONTROL 標記]**

   教學課程：滑雪

* **[!UICONTROL 在目錄中顯示]**

   不選中

* **[!UICONTROL 上傳影像]**

   在資源控制台中表示學習路徑。

   ![learningpath-basic](assets/learningpath-basic.png)

* 選擇 **[!UICONTROL 下一個]**.

跳過下一個面板，因為沒有要添加的先決條件學習路徑。

* 選擇 **[!UICONTROL 下一個]**

在「新增資源」面板上：

* 選擇 `+ Add Resources` 來選取2個滑雪課程資源，以新增至學習路徑。

   注意：僅 **已發佈** 資源可供選取。

>[!NOTE]
>
>您只能選擇與學習路徑位於同一級別的可用資源。 例如，對於在組中建立的學習路徑，只有組級別資源可用；對於在社區站點中建立的學習路徑，該站點中的資源可用於添加到學習路徑。

* 選擇 **[!UICONTROL 提交]**.

   ![學習路徑](assets/learningpath-add.png)

   ![建立學習路徑](assets/create-learningpath.png)

* 選擇 **[!UICONTROL 下一個]**

   ![學習路徑設定](assets/learningpath-settings.png)

* **[!UICONTROL 新增被指定者]**

   使用下拉式選單來選取 `Community Ski Class` 組，應包括成員 `Riley Taylor` 和 `Sidney Croft.`

* **[!UICONTROL 學習路徑聯繫人(&amp;A);]**

   *（必要）* 使用下拉菜單選擇成員 `Quinn Harper`.

* 選擇 **[!UICONTROL 建立]**。

   ![learningpath info](assets/learningpath-info.png)

成功建立學習路徑將返回資源控制台，並選擇新建立的學習路徑。 在此主控台中，可發佈、新增使用者及變更其他設定。

**發佈** 學習的路。
