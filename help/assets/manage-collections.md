---
title: 管理數位資產集合
description: 了解管理資產集合的工作，例如建立、檢視、刪除、編輯和下載集合。
contentOwner: AG
mini-toc-levels: 1
role: User
feature: Collections,Asset Management
exl-id: 2117b2de-8024-4aa8-9ce0-68a156928356
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '2203'
ht-degree: 14%

---

# 管理收藏集 {#managing-collections}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-collections.html?lang=en) |
| AEM 6.5 | 本文 |

集合是 [!DNL Adobe Experience Manager Assets]. 使用收藏集在使用者之間共用資產。此集可以是靜態集合或以搜尋結果為基礎的動態集合。

和檔案夾不同，收藏集可包含來自不同位置的資產。您可以與被指派不同權限層級的各種使用者共用集合，包括檢視、編輯等。

您可以和使用者共用多個收藏集。每個收藏集都包含資產的參考資料。資產的參考完整性會跨越收藏集來維護。

集合的收集方式會根據資產的收集方式，分為下列類型：

* 包含資產、資料夾和其他集合之靜態參考清單的集合。

* 智慧型集合，根據搜尋條件以動態方式包含資產。

## 存取集合主控台 {#navigating-the-collections-console}

若要開啟 **[!UICONTROL 集合]**，在 [!DNL Experience Manager] 介面，轉到 **[!UICONTROL 資產]** > **[!UICONTROL 集合]**.

## 建立收藏集 {#creating-a-collection}

您可以使用 [靜態參考](#creating-a-collection-with-static-references) 或根據 [搜尋條件型篩選](#creating-a-smart-collection). 您也可以從燈箱建立集合。

### 使用靜態參考建立集合 {#creating-a-collection-with-static-references}

您可以建立包含靜態參照的集合，例如包含資產、資料夾、集合、回轉集和影像集參考的集合。

1. 導覽至 **[!UICONTROL 集合]** 控制台。
1. 在工具列中，按一下 **[!UICONTROL 建立]**.
1. 在 **[!UICONTROL 建立集合]** 頁面，輸入集合的標題和可選說明。
1. 新增成員至系列並指派適當的權限。或者，選取「 **[!UICONTROL 公用系列]** 」，讓所有使用者都能存取系列。

   >[!NOTE]
   >
   >若要讓成員可與其他使用者共用集合，請提供 `dam-users` 群組在路徑上讀取權限 `home/users`. 授予使用者權限(位於 `/content/dam/collections` 位置，讓使用者在快顯清單中檢視集合。 或者，讓使用者成為 `dam-users` 群組。

1. （選用）為系列新增縮圖影像。
1. 按一下 **[!UICONTROL 建立]**，然後按一下 **[!UICONTROL 確定]** 以關閉對話方塊。 具有指定標題和屬性的系列會在「系列」主控台中開啟。

   >[!NOTE]
   >
   >[!DNL Experience Manager Assets] 可讓您建立集合的審核任務，類似於為資產資料夾建立審核任務的方式。

   若要新增資產至集合，請導覽至 [!DNL Assets] 使用者介面。 如需詳細資訊，請參閱 [新增資產至集合](#adding-assets-to-a-collection).

### 使用放置區建立集合 {#create-collections-using-dropzone}

您可以從 [!DNL Assets] 集合的使用者介面。 您也可以建立集合的復本，並將資產拖曳至該處。

1. 從 [!DNL Assets] 使用者介面，選取您要新增至集合的資產。
1. 將資產拖曳至 **[!UICONTROL 拖放集合]** 區域。 或者，按一下 **[!UICONTROL 收集]** 的上界。

   ![drop_in_collection](assets/drop_in_collection.png)

1. 在 **[!UICONTROL 新增至集合]** 頁面，按一下 **[!UICONTROL 建立集合]** 的上界。

   如果您想要將資產新增至現有集合，請從頁面中選取資產，然後按一下 **[!UICONTROL 新增]**. 依預設，會選取最近更新的系列。

1. 在「建 **[!UICONTROL 立新系列]** 」對話方塊中，指定系列的名稱。如果您希望系列可供所有使用者存取，請選取「公用 **[!UICONTROL 系列」]**。
1. 按一下 **[!UICONTROL 繼續]** 來建立集合。

### 建立智慧型集合 {#creating-a-smart-collection}

智慧型集合會使用搜尋條件來動態填入資產。 您可以僅使用檔案而不使用資料夾或檔案和資料夾來建立智慧集合。

若要建立智慧型系列，請遵循下列步驟：

1. 導覽至 [!DNL Assets] 使用者介面，然後按一下「搜尋」。

1. 在Omnisearch方塊中輸入搜尋關鍵字，然後選取 `Enter`. 開啟「篩選」面板並套用搜尋篩選。

1. 從 **[!UICONTROL 檔案和資料夾]** 清單，選擇 **[!UICONTROL 檔案]**.

   ![files_option](assets/files_option.png)

1. 按一下 **[!UICONTROL 儲存智慧型集合]**.

1. 指定集合的名稱。 選擇 **[!UICONTROL 公開]** 若要將具有檢視器角色的DAM使用者群組新增至智慧型集合。

   ![save_collection](assets/save_collection.png)

   >[!NOTE]
   >
   >如果您選取 **[!UICONTROL 公開]**，建立後，具有擁有者角色的每個人都能使用智慧型集合。 如果您取消 **[!UICONTROL 公開]** 選項中， DAM使用者群組將不再與智慧型集合相關聯。

1. 按一下 **[!UICONTROL 儲存]** 建立智慧型集合，然後關閉訊息方塊以完成程式。

   新的智慧型系列也會新增至 **[!UICONTROL 已儲存的搜尋]** 清單。

   ![collection_listing](assets/collection_listing.png)

   標籤 **[!UICONTROL 建立智慧選取]** 選項變更為 **[!UICONTROL 編輯智慧選擇]**. 要編輯智慧系列的設定，請從「檔案和文 **[!UICONTROL 件夾]** 」列 **[!UICONTROL 表中選擇「檔案]** 」。按一下 **[!UICONTROL 編輯智慧選擇]** ![編輯智慧集合](assets/do-not-localize/edit-smart-collection.png) 選項。

## 將資產新增至收藏集 {#adding-assets-to-a-collection}

您可以新增資產至包含參考資產或資料夾清單的集合。 智慧型集合會使用搜尋查詢來填入資產。 因此，資產和資料夾的靜態參考不適用。

1. 在 [!DNL A]設定使用者介面，選取資產並按一下 **[!UICONTROL 收集]** ![新增至集合](assets/do-not-localize/add-to-collection.png) 的上界。
或者，您也可以將資產拖曳至 **[!UICONTROL 拖放集合]** 區域。 當地區的標籤變更為 **[!UICONTROL 拖放以添加]**.

1. 在 **[!UICONTROL 新增至集合]** 頁面，選取您要新增資產的集合。

1. 按一下 **[!UICONTROL 新增]**，然後關閉確認訊息。 資產會新增至集合。

## 編輯智慧型集合 {#editing-a-smart-collection}

智慧型集合是透過儲存搜尋來建立，因此您可以修改 [儲存的搜尋](#saved-searches).

1. 在 [!DNL Assets] 使用者介面，按一下搜尋選項 ![搜尋選項](assets/do-not-localize/search_icon.png) 的上界。
1. 將游標置於Omnisearch方塊中，選取 `Return` 鍵。
1. 在 [!DNL Experience Manager] 介面，開啟「篩選器」面板。
1. 從「保 **[!UICONTROL 存的搜索]** 」清單中，選擇要修改的智慧系列。「搜尋」面板會顯示為儲存的搜尋設定的篩選器。

   ![select_smart_collection](assets/select_smart_collection.png)

1. 從 **[!UICONTROL 檔案和資料夾]** 清單，選擇 **[!UICONTROL 檔案]**.
1. 視需要修改一或多個篩選器。 按一下&#x200B;**[!UICONTROL 編輯智慧型集合]**。

   您也可以編輯智慧型系列的名稱。

   ![edit_smart_collectiondialog](assets/edit_smart_collectiondialog.png)

1. 按一下「**[!UICONTROL 儲存]**」。此 **[!UICONTROL 編輯智慧型集合]** 對話框。
1. 按一下 **[!UICONTROL 覆寫]** 將原始智慧系列替換為編輯的系列。 或者，選取 **[!UICONTROL 另存新檔]** 以單獨儲存已編輯的集合。
1. 在確認對話方塊中，按一下 **[!UICONTROL 儲存]** 來完成此程式。

## 檢視和編輯收藏集中繼資料 {#view-edit-collection-metadata}

集合中繼資料包含關於集合的資料，包括所新增的任何標籤。

1. 從 [!UICONTROL 集合] 主控台，選取集合併按一下 **[!UICONTROL 屬性]** 的上界。
1. 在「系列 **[!UICONTROL 中繼資料]** 」頁面中，從「基本」和「進階」標籤檢視系 **[!UICONTROL 列中繼資]** 料 **** 。
1. 視需要修改中繼資料。 若要儲存變更，請按一下 **[!UICONTROL 儲存並關閉]** 的上界。

## 大量編輯多個集合的中繼資料 {#editing-collection-metadata-in-bulk}

您可以同時編輯多個集合的中繼資料。 此功能可協助您快速復寫多個集合中的通用中繼資料。

1. 在「集合」控制台中，選取兩個或多個集合。
1. 在工具列中，按一下 **[!UICONTROL 屬性]**.
1. 在「系 **[!UICONTROL 列中繼資料]** 」頁面中，視需要編輯「基本」和「進階」標籤下的中繼資料 ******** 。
1. 若要檢視特定系列的中繼資料屬性，請取消在系列清單中選取剩餘的系列。 中繼資料編輯器欄位會填入特定集合的中繼資料。

   >[!NOTE]
   >
   >* 在 [!UICONTROL 屬性] 頁面，您可以取消選取項目，從集合清單中移除集合。 集合清單預設會選取所有集合。 [!DNL Experience Manager] 不會更新您移除之集合的中繼資料。
   >* 在清單頂端，選取附近的核取方塊 **[!UICONTROL 標題]** 切換選取集合和清除清單。


1. 按一下 **[!UICONTROL 儲存並關閉]** ，然後關閉確認對話框。
1. 若要將新中繼資料附加至現有的中繼資料，請選取 **[!UICONTROL 附加模式]**. 如果您未選取此選項，新的中繼資料會取代欄位中現有的中繼資料。按一下 **[!UICONTROL 提交]**.

   >[!NOTE]
   >
   >您為所選集合新增的中繼資料會覆寫這些集合的先前中繼資料。 使用 [!UICONTROL 附加模式] 若要在可包含多個值的欄位中，將新值新增至現有中繼資料。 一律會覆寫單一值欄位。 您在中新增的任何標籤 [!UICONTROL 標籤] 欄位，會附加至中繼資料中的現有標籤清單。

自訂中繼資料 [!UICONTROL 屬性] 頁面，包括添加、修改、刪除元資料屬性，請使用架構編輯器。

>[!TIP]
>
>大量編輯方法適用於集合中的可用資產。 對於可跨資料夾使用或符合通用條件的資產，您可以 [搜尋後大量更新中繼資料](/help/assets/search-assets.md#metadataupdates).

## 搜尋集合 {#searching-collections}

您可以從集合控制台搜尋集合。 在Omnisearch方塊中搜尋關鍵字時， [!DNL Assets] 搜尋系列名稱、中繼資料和新增至系列的標籤。

如果您從頂層搜尋集合，則搜尋結果中只會傳回個別的集合。 [!DNL Assets] 或集合內的資料夾會遭排除。 在所有其他情況下（例如在個別集合或資料夾階層中），會傳回所有相關資產、資料夾和集合。

## 在集合內搜尋 {#searching-within-collections}

在「集合」控制台中，按一下集合以開啟它。

在集合中， [!DNL Experience Manager] 搜尋僅限於您檢視之系列中的資產（及其標籤和中繼資料）。 在資料夾內搜尋時，會傳回目前資料夾內所有相符的資產和子資料夾。 在集合內搜尋時，系統只會傳回相符的資產、資料夾和其他集合，這些集合是集合的直接成員。

## 編輯集合設定 {#editing-collection-settings}

您可以編輯系列設定，例如標題和說明，或將成員新增至系列。

1. 選取集合，然後按一下 **[!UICONTROL 設定]** 的下一頁。 或者，使用 **[!UICONTROL 設定]** 從集合縮圖快速動作。
1. 修改「系列設定」頁面中 **[!UICONTROL 的系列設定]** 。例如，修改系列標題、說明、成員和權限，如 [新增集合](#creating-a-collection).

1. 若要儲存變更，請按一下 **[!UICONTROL 儲存]**.

## 刪除收藏集 {#deleting-a-collection}

1. 從「系列」控制台中，選擇一個或多個系列，然後按一下工具欄中的「刪除」。

1. 在對話方塊中，按一下 **[!UICONTROL 刪除]** 確認刪除動作。

   >[!NOTE]
   >
   >您也可以刪除智慧型集合，依 [刪除已保存的搜索](#saved-searches).

## 下載收藏集 {#downloading-a-collection}

下載集合時，會下載集合內的整個資產階層，包括資料夾和子集合。

1. 從「系列」控制台中，選擇要下載的一個或多個系列。
1. 在工具列中，按一下 **[!UICONTROL 下載]**.
1. 在 **[!UICONTROL 下載]** 對話框，按一下 **[!UICONTROL 下載]**. 如果您想要下載系列內資產的轉譯，請選取 **[!UICONTROL 轉譯]**. 選取 **[!UICONTROL 電子郵件]** 選項，將電子郵件通知傳送至集合的擁有者。

   當您選取要下載的集合時，會下載集合下的完整資料夾階層。 若要將您下載的每個系列（包括父系列下巢狀的子系列中的資產）納入個別資料夾，請選取 **[!UICONTROL 為每個資產建立個別資料夾]**.

## 建立巢狀集合 {#creating-nested-collections}

您可以將集合新增至其他集合，借此建立巢狀集合。

1. 從「集合」控制台，選擇所需的集合或集合組，然後按一下 **[!UICONTROL 收集]** 的下一頁。

1. 從 **[!UICONTROL 新增至集合]** 頁面，選擇要在其中添加集合的集合。

   >[!NOTE]
   >
   >依預設，會選取最近更新的集合，位於 **[!UICONTROL 新增至集合]** 頁面。

1. 按一下 **[!UICONTROL 新增]**. 訊息會確認集合已新增至 **[!UICONTROL 選擇目標]** 頁面。 關閉訊息以完成程式。

>[!NOTE]
>
>智慧型集合無法巢狀。 換言之，智慧型集合不能包含任何其他集合。

## 已儲存搜尋 {#saved-searches}

在 [!DNL Assets] 使用者介面，您可以根據特定規則、搜尋條件或自訂搜尋刻面來搜尋或篩選資產。 如果您將這些項目儲存為「 **[!UICONTROL 已儲存的搜尋]**」，您稍後可從「篩選」面板的「已儲存的搜尋 **** 」清單中存取。建立儲存的搜尋也會建立智慧型系列。

![saved_searches_list](assets/saved_searches_list.png)

儲存的搜尋會在您建立智慧型系列時建立。智慧型系列會自動新增至「已儲 **[!UICONTROL 存的搜尋]** 」清單。此 [!UICONTROL 已儲存的搜尋] 集合的查詢會儲存在 `dam:query` 屬性（位於相對位置） `/content/dam/collections/`. 您可以儲存的搜尋沒有限制，而清單中顯示的已儲存搜尋也沒有限制。

>[!NOTE]
>
>您可以以共用靜態集合的相同方式共用智慧型集合。

編輯已儲存的搜尋與編輯智慧型集合相同。 如需詳細資訊，請參閱 [編輯智慧型系列](#editing-a-smart-collection).

要刪除已保存的搜索，請執行以下步驟：

1. 在 [!DNL Assets] 使用者介面，按一下搜尋 ![搜尋選項](assets/do-not-localize/search_icon.png).
1. 在Omnisearch欄位中使用游標，選取 `Return` 鍵。
1. 在 [!DNL Experience Manager] 介面，開啟「篩選器」面板。
1. 從 **[!UICONTROL 已儲存的搜尋]** 清單，按一下 **[!UICONTROL 刪除]** 在您要刪除的智慧型集合旁。

   ![select_smart_collection](assets/select_smart_collection.png)

1. 在對話方塊中，按一下 **[!UICONTROL 刪除]** 刪除保存的搜索。

## 對集合執行工作流程 {#running-a-workflow-on-a-collection}

您可以為集合內的資產執行工作流程。 如果集合包含巢狀集合，工作流程也會在巢狀集合內的資產上執行。 不過，如果集合和巢狀集合包含重複資產，工作流程只會針對這些資產執行一次。

1. 開啟 **[!UICONTROL 資產]** > **[!UICONTROL 集合]**. 若要對特定集合執行工作流程，請選取該工作流程。
1. 開啟 **[!UICONTROL 時間表]** 欄。 按一下 ![雪佛龍](assets/do-not-localize/chevron-up-icon.png) 按一下 **[!UICONTROL 開始工作流程]**.
1. 在「開 **[!UICONTROL 始工作流]** 」部分，從清單中選擇工作流模型。例如，選取「 **[!UICONTROL DAM更新資產」模型]** 。
1. 輸入工作流程的標題，然後按一下 **[!UICONTROL 開始]**.
1. 在對話方塊中，按一下 **[!UICONTROL 繼續]**. 工作流程會處理所選集合中的所有資產。

>[!MORELIKETHIS]
>
>* [設定Experience Manager Assets電子郵件通知](/help/sites-administering/notification.md#assetsconfig)
>* [為集合建立審核任務](bulk-approval.md)

