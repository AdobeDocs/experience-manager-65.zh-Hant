---
title: 建立內容片段的翻譯專案
description: 瞭解如何在Adobe Experience Manager中翻譯內容片段。
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
feature: Content Fragments
role: User, Admin
exl-id: 19bb58da-8220-404e-bddb-34be94a3a7d7
solution: Experience Manager, Experience Manager Assets
source-git-commit: 7bf70ba18603bfd17dec391ddcd623e9085fbd04
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 4%

---

# 建立內容片段的翻譯專案 {#creating-translation-projects-for-content-fragments}

除了資產之外，Adobe Experience Manager (AEM) Assets還支援[內容片段](/help/assets/content-fragments/content-fragments.md) （包括變數）的語言複製工作流程。 對內容片段執行語言複製工作流程不需要其他最佳化。 在每個工作流程中，會傳送整個內容片段以供翻譯。

您可以在內容片段上執行的工作流程型別與您為資產執行的工作流程型別完全類似。 此外，每個工作流程型別中可用的選項，都與資產之對應工作流程型別下可用的選項相符。

您可以對內容片段執行下列型別的語言複製工作流程：

**建立並翻譯**

在此工作流程中，要翻譯的內容片段會複製到您要翻譯之語言的語言根目錄。 此外，系統會根據您選擇的選項，在「專案」主控台中為內容片段建立翻譯專案。 根據設定，翻譯專案可以手動啟動，或允許在建立翻譯專案後立即自動執行。

**更新語言副本**

更新或修改來源內容片段時，對應的地區設定/語言特定內容片段需要重新翻譯。 更新語言副本工作流程會翻譯額外的內容片段群組，並將其包含在特定地區設定的語言副本中。 在這種情況下，翻譯的內容片段會新增到已經包含先前翻譯的內容片段的目標資料夾。

## 建立及翻譯工作流程 {#create-and-translate-workflow}

建立與翻譯工作流程包含下列選項。 與每個選項相關的程式步驟與資產相應選項相關的程式步驟類似。

* 僅建立結構：如需程式步驟，請參閱[僅建立資產的結構](translation-projects.md#create-structure-only)。
* 建立翻譯專案：如需程式步驟，請參閱[建立資產的翻譯專案](translation-projects.md#create-a-new-translation-project)。
* 新增至現有的翻譯專案：如需程式步驟，請參閱[新增至資產的現有翻譯專案](translation-projects.md#add-to-existing-translation-project)。

## 更新語言副本工作流程 {#update-language-copies-workflow}

更新語言副本工作流程包含以下選項。 與每個選項相關的程式步驟與資產相應選項相關的程式步驟類似。

* 建立翻譯專案：如需程式步驟，請參閱[建立資產的翻譯專案](translation-projects.md#create-a-new-translation-project) （更新工作流程）。
* 新增至現有翻譯專案：如需程式步驟，請參閱[新增至資產的現有翻譯專案](translation-projects.md#add-to-existing-translation-project) （更新工作流程）。

您也可以建立片段的臨時語言副本，其方式類似於建立資產的臨時副本。 如需詳細資訊，請參閱[建立資產的暫存語言復本](translation-projects.md#creating-temporary-language-copies)。

## 翻譯混合媒體片段 {#translating-mixed-media-fragments}

AEM可讓您翻譯包含各種媒體資產和集合型別的內容片段。 如果您翻譯包含內嵌資產的內容片段，這些資產的翻譯副本會儲存在目標語言根下。

如果內容片段包含集合，則集合中的資產會與內容片段一併翻譯。 資產的翻譯版本會儲存在適當的目標語言根目錄中，且位置與來源語言根目錄下來源資產的實體位置相符。

為了能夠翻譯包含混合媒體的內容片段，請先編輯預設翻譯框架以啟用與內容片段關聯的內嵌資產和集合的翻譯。

1. 按一下AEM標誌，並導覽至&#x200B;**[!UICONTROL 工具>部署>Cloud Service]**。
1. 在&#x200B;**[!UICONTROL Adobe Marketing Cloud]**&#x200B;下找到&#x200B;**[!UICONTROL 翻譯整合]**，然後按一下&#x200B;**[!UICONTROL 顯示設定]**。

   ![chlimage_1-444](assets/chlimage_1-444.png)

1. 從可用組態清單中，按一下&#x200B;**[!UICONTROL 預設組態（翻譯整合組態）]**&#x200B;以開啟&#x200B;**[!UICONTROL 預設組態]**&#x200B;頁面。

   ![chlimage_1-445](assets/chlimage_1-445.png)

1. 按一下工具列中的&#x200B;**[!UICONTROL 編輯]**&#x200B;以顯示&#x200B;**[!UICONTROL 翻譯設定]**&#x200B;對話方塊。

   ![chlimage_1-446](assets/chlimage_1-446.png)

1. 導覽至&#x200B;**[!UICONTROL Assets]**&#x200B;標籤，然後從&#x200B;**[!UICONTROL 翻譯內容片段Assets]**&#x200B;清單中選擇&#x200B;**[!UICONTROL 內嵌媒體Assets和相關集合]**。 按一下&#x200B;**[!UICONTROL 確定]**&#x200B;以儲存變更。

   ![chlimage_1-447](assets/chlimage_1-447.png)

1. 從英文根資料夾中，開啟內容片段。

   ![chlimage_1-448](assets/chlimage_1-448.png)

1. 按一下&#x200B;**[!UICONTROL 插入資產]**&#x200B;圖示。

   ![chlimage_1-449](assets/chlimage_1-449.png)

1. 將資產插入內容片段。

   ![將資產插入內容片段](assets/column-view.png)

1. 按一下&#x200B;**[!UICONTROL 關聯內容]**&#x200B;圖示。

   ![chlimage_1-451](assets/chlimage_1-451.png)

1. 按一下&#x200B;**[!UICONTROL 關聯內容]**。

   ![chlimage_1-452](assets/chlimage_1-452.png)

1. 選取收藏集並將其納入內容片段中。 按一下「**[!UICONTROL 儲存]**」。

   ![chlimage_1-453](assets/chlimage_1-453.png)

1. 選取內容片段，然後按一下&#x200B;**[!UICONTROL GlobalNav]**&#x200B;圖示。
1. 從功能表選取&#x200B;**[!UICONTROL 參考]**&#x200B;以顯示&#x200B;**[!UICONTROL 參考]**&#x200B;窗格。

   ![chlimage_1-454](assets/chlimage_1-454.png)

1. 按一下&#x200B;**[!UICONTROL 復本]**&#x200B;下的&#x200B;**[!UICONTROL 語言復本]**&#x200B;以顯示語言復本。

   ![chlimage_1-455](assets/chlimage_1-455.png)

1. 從面板底部按一下&#x200B;**[!UICONTROL 建立並翻譯]**&#x200B;以顯示&#x200B;**[!UICONTROL 建立並翻譯]**&#x200B;對話方塊。

   ![chlimage_1-456](assets/chlimage_1-456.png)

1. 從&#x200B;**[!UICONTROL 目標語言]**&#x200B;清單中選取目標語言。

   ![chlimage_1-457](assets/chlimage_1-457.png)

1. 從&#x200B;**[!UICONTROL 專案]**&#x200B;清單中選取翻譯專案型別。

   ![chlimage_1-458](assets/chlimage_1-458.png)

1. 在&#x200B;**[!UICONTROL 專案標題]**&#x200B;方塊中指定專案標題，然後按一下&#x200B;**建立**。

   ![chlimage_1-459](assets/chlimage_1-459.png)

1. 導覽至&#x200B;**[!UICONTROL 專案]**&#x200B;主控台，並開啟您建立之翻譯專案的專案資料夾。

   ![chlimage_1-460](assets/chlimage_1-460.png)

1. 按一下專案拼貼，開啟專案詳細資訊頁面。

   ![chlimage_1-461](assets/chlimage_1-461.png)

1. 在「翻譯工作」方塊中，驗證要翻譯的資產數量。
1. 從&#x200B;**[!UICONTROL 翻譯工作]**&#x200B;圖磚，開始翻譯工作。

   ![chlimage_1-462](assets/chlimage_1-462.png)

1. 按一下「翻譯工作」表徵圖底部的省略符號，以顯示翻譯工作的狀態。

   ![chlimage_1-463](assets/chlimage_1-463.png)

1. 按一下內容片段以檢查翻譯的相關資產的路徑。

   ![chlimage_1-464](assets/chlimage_1-464.png)

1. 在「系列」主控台中檢閱系列的語言副本。

   ![chlimage_1-465](assets/chlimage_1-465.png)

   請注意，只會翻譯集合的內容。 集合本身不會翻譯。

1. 導覽至轉譯的相關資產路徑。 請注意，翻譯的資產會儲存在目標語言根目錄下。

   ![chlimage_1-466](assets/chlimage_1-466.png)

1. 導覽至系列中隨內容片段翻譯的資產。 請注意，資產的翻譯副本會儲存在適當的目標語言根目錄中。

   ![chlimage_1-467](assets/chlimage_1-467.png)

   >[!NOTE]
   >
   >將內容片段新增到現有專案或執行更新工作流程的程式與資產的對應程式類似。 如需這些程式的指引，請參閱資產程式說明。
