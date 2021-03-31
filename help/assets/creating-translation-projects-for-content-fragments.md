---
title: 建立內容片段的翻譯專案
seo-title: 建立內容片段的翻譯專案
description: 瞭解如何翻譯內容片段。
seo-description: 瞭解如何翻譯內容片段。
uuid: 23176e70-4003-453c-af25-6499a5ed3f6d
contentOwner: heimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
discoiquuid: d2decc31-a04b-4a8e-bb19-65f21cf7107e
feature: 內容片段
role: 業務從業人員、管理員
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---


# 為內容片段建立翻譯項目{#creating-translation-projects-for-content-fragments}

除了資產外，Adobe Experience Manager(AEM)資產還支援[內容片段](/help/assets/content-fragments/content-fragments.md)（包括變數）的語言複製工作流程。 在內容片段上執行語言複製工作流程不需要其他最佳化。 在每個工作流程中，都會傳送整個內容片段以供翻譯。

您可以在內容片段上執行的工作流程類型與您為資產執行的工作流程類型完全相同。 此外，每個工作流類型中可用的選項都與資產的相應工作流類型下可用的選項相匹配。

您可以針對內容片段執行下列語言複製工作流程類型：

**建立和翻譯**

在此工作流程中，要翻譯的內容片段會複製到您要翻譯的語言的語言根目錄。 此外，根據您選擇的選項，將為「項目」控制台中的內容片段建立一個翻譯項目。 根據設定，翻譯項目可以手動啟動，或者允許在建立翻譯項目後立即自動運行。

**更新語言副本**

當更新或修改源內容片段時，相應的地區／語言特定內容片段需要重新編譯。 更新語言副本工作流將翻譯另外一組內容片段並將其包含在特定地區的語言副本中。 在這種情況下，已翻譯的內容片段會新增至已包含先前已翻譯內容片段的目標資料夾。

## 建立並翻譯工作流{#create-and-translate-workflow}

「建立和翻譯」工作流程包含下列選項。 與每個選項相關聯的程式步驟類似於與資產的相應選項相關聯的步驟。

* 僅建立結構：如需程式步驟，請參閱[僅建立資產結構](translation-projects.md#create-structure-only)。
* 建立新的翻譯專案：有關過程步驟，請參閱[為資產](translation-projects.md#create-a-new-translation-project)建立新翻譯項目。
* 添加到現有翻譯項目：有關過程步驟，請參見[添加到資產](translation-projects.md#add-to-existing-translation-project)的現有翻譯項目。

## 更新語言副本工作流{#update-language-copies-workflow}

「更新語言副本」工作流程包含下列選項。 與每個選項相關聯的程式步驟類似於與資產的相應選項相關聯的步驟。

* 建立新的翻譯專案：有關過程步驟，請參閱[為資產](translation-projects.md#create-a-new-translation-project)建立新的翻譯項目（更新工作流）。
* 添加到現有翻譯項目：有關過程步驟，請參閱[將資產](translation-projects.md#add-to-existing-translation-project)（更新工作流）添加到現有翻譯項目。

您也可以建立片段的暫時語言復本，就像建立資產的暫時復本一樣。 如需詳細資訊，請參閱[建立資產的暫存語言副本。](translation-projects.md#creating-temporary-language-copies)

## 轉換混合媒體片段{#translating-mixed-media-fragments}

可讓AEM您翻譯包含各種類型媒體資產和系列的內容片段。 如果您翻譯包含內嵌資產的內容片段，則這些資產的翻譯副本會儲存在目標語言根目錄下。

如果內容片段包含系列，則系列中的資產會與內容片段一起翻譯。 資產的翻譯副本會儲存在適當的目標語言根目錄中，位於符合來源語言根目錄下之來源資產實體位置的位置。

若要能夠轉譯包含混合媒體的內容片段，請先編輯預設的轉譯架構，以便轉譯與內容片段關聯的內嵌資產和系列。

1. 按一下／點AEM選標誌，並導覽至「**[!UICONTROL 工具>部署>Cloud Services]**」。
1. 在&#x200B;**[!UICONTROL Adobe Marketing Cloud]**&#x200B;下找到&#x200B;**[!UICONTROL 翻譯整合]** ，然後按一下／點選&#x200B;**[!UICONTROL 顯示配置]**。

   ![chlimage_1-444](assets/chlimage_1-444.png)

1. 在可用配置清單中，按一下／點選&#x200B;**[!UICONTROL 預設配置（翻譯整合配置）]**&#x200B;以開啟&#x200B;**[!UICONTROL 預設配置]**&#x200B;頁。

   ![chlimage_1-445](assets/chlimage_1-445.png)

1. 按一下工具欄中的&#x200B;**[!UICONTROL 編輯]**&#x200B;以顯示&#x200B;**[!UICONTROL 翻譯配置]**&#x200B;對話框。

   ![chlimage_1-446](assets/chlimage_1-446.png)

1. 導覽至&#x200B;**[!UICONTROL Assets]**&#x200B;標籤，並從&#x200B;**[!UICONTROL Translate Content Fragment Assets]**&#x200B;清單中選擇&#x200B;**[!UICONTROL 內嵌媒體資產和關聯的系列]**。 按一下／點選&#x200B;**[!UICONTROL OK]**&#x200B;以保存更改。

   ![chlimage_1-447](assets/chlimage_1-447.png)

1. 從英文根資料夾中開啟內容片段。

   ![chlimage_1-448](assets/chlimage_1-448.png)

1. 按一下／點選&#x200B;**[!UICONTROL 插入資產]**&#x200B;圖示。

   ![chlimage_1-449](assets/chlimage_1-449.png)

1. 將資產插入內容片段。

   ![將資產插入內容片段](assets/column-view.png)

1. 按一下／點選&#x200B;**[!UICONTROL 關聯內容]**&#x200B;圖示。

   ![chlimage_1-451](assets/chlimage_1-451.png)

1. 按一下／點選&#x200B;**[!UICONTROL 關聯內容]**。

   ![chlimage_1-452](assets/chlimage_1-452.png)

1. 選取系列並將它加入內容片段中。 按一下／點選&#x200B;**[!UICONTROL Save]**。

   ![chlimage_1-453](assets/chlimage_1-453.png)

1. 選取內容片段，然後按一下／點選&#x200B;**[!UICONTROL GlobalNav]**&#x200B;圖示。
1. 從菜單中選擇&#x200B;**[!UICONTROL 引用]**&#x200B;以顯示&#x200B;**[!UICONTROL 引用]**&#x200B;窗格。

   ![chlimage_1-454](assets/chlimage_1-454.png)

1. 按一下／點選&#x200B;**[!UICONTROL **[!UICONTROL  Copys ]**下的「語言副本」，以顯示語言副本。]**

   ![chlimage_1-455](assets/chlimage_1-455.png)

1. 從面板底部按一下／點選「建立與轉譯」**[!UICONTROL ，以顯示「建立與轉譯」]**&#x200B;對話方塊。]****[!UICONTROL 

   ![chlimage_1-456](assets/chlimage_1-456.png)

1. 從&#x200B;**[!UICONTROL 目標語言]**&#x200B;清單中選擇目標語言。

   ![chlimage_1-457](assets/chlimage_1-457.png)

1. 從&#x200B;**[!UICONTROL Project]**&#x200B;清單中選擇翻譯項目類型。

   ![chlimage_1-458](assets/chlimage_1-458.png)

1. 在&#x200B;**[!UICONTROL 專案標題]**&#x200B;方塊中指定專案標題，然後按一下／點選&#x200B;**建立**。

   ![chlimage_1-459](assets/chlimage_1-459.png)

1. 導航到&#x200B;**[!UICONTROL Projects]**&#x200B;控制台，並開啟您建立的翻譯項目的項目資料夾。

   ![chlimage_1-460](assets/chlimage_1-460.png)

1. 按一下／點選專案圖格以開啟專案詳細資訊頁面。

   ![chlimage_1-461](assets/chlimage_1-461.png)

1. 從「翻譯工作」方塊中，確認要翻譯的資產數。
1. 從&#x200B;**[!UICONTROL 翻譯作業]**&#x200B;表徵圖中，啟動翻譯作業。

   ![chlimage_1-462](assets/chlimage_1-462.png)

1. 按一下「翻譯作業」表徵圖底部的橢圓以顯示翻譯作業的狀態。

   ![chlimage_1-463](assets/chlimage_1-463.png)

1. 按一下／點選內容片段，以檢查已轉譯的相關資產路徑。

   ![chlimage_1-464](assets/chlimage_1-464.png)

1. 在「系列」主控台中檢閱系列的語言復本。

   ![chlimage_1-465](assets/chlimage_1-465.png)

   請注意，只有系列的內容會翻譯。 系列本身不會翻譯。

1. 導覽至已轉譯之相關資產的路徑。 請注意，已翻譯的資產會儲存在目標語言根目錄下。

   ![chlimage_1-466](assets/chlimage_1-466.png)

1. 導覽至系列中與內容片段一起翻譯的資產。 請注意，資產的翻譯副本會儲存在適當的目標語言根目錄。

   ![chlimage_1-467](assets/chlimage_1-467.png)

   >[!NOTE]
   >
   >將內容片段新增至現有專案或執行更新工作流程的程式與資產的對應程式類似。 有關這些程式的指導，請參閱資產的程式。

