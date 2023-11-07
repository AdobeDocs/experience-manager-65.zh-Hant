---
title: 管理數位資產集合
description: 瞭解管理資產集合的任務，例如建立、檢視、刪除、編輯和下載集合。
contentOwner: AG
mini-toc-levels: 1
role: User
feature: Collections,Asset Management
exl-id: 2117b2de-8024-4aa8-9ce0-68a156928356
hide: true
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2203'
ht-degree: 14%

---

# 管理收藏集 {#managing-collections}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-collections.html?lang=en) |
| AEM 6.5 | 本文章 |

集合是內的一組資產 [!DNL Adobe Experience Manager Assets]. 使用收藏集在使用者之間共用資產。集合可以是靜態集合或基於搜尋結果的動態集合。

和檔案夾不同，收藏集可包含來自不同位置的資產。您可以與獲指派不同許可權層級（包括檢視、編輯等）的各種使用者共用集合。

您可以和使用者共用多個收藏集。每個收藏集都包含資產的參考資料。資產的參考完整性會跨越收藏集來維護。

根據集合整理資產的方式，集合有下列型別：

* 包含資產、資料夾和其他集合之靜態參考清單的集合。

* 根據搜尋條件動態包含資產的智慧型集合。

## 存取集合主控台 {#navigating-the-collections-console}

若要開啟 **[!UICONTROL 集合]**，在 [!DNL Experience Manager] 介面，前往 **[!UICONTROL 資產]** > **[!UICONTROL 集合]**.

## 建立收藏集 {#creating-a-collection}

您可以使用以下任一專案建立集合： [靜態參考](#creating-a-collection-with-static-references) 或根據 [搜尋條件型篩選器](#creating-a-smart-collection). 您也可以從Lightbox建立集合。

### 使用靜態參考建立集合 {#creating-a-collection-with-static-references}

您可以建立具有靜態參照的集合，例如，具有資產、資料夾、集合、迴轉集及影像集參照的集合。

1. 導覽至 **[!UICONTROL 集合]** 主控台。
1. 在工具列中按一下 **[!UICONTROL 建立]**.
1. 在 **[!UICONTROL 建立集合]** 頁面，輸入收藏集的標題和說明（選用）。
1. 新增成員至系列並指派適當的權限。或者，選取「 **[!UICONTROL 公用系列]** 」，讓所有使用者都能存取系列。

   >[!NOTE]
   >
   >若要讓成員與其他使用者共用集合，請提供 `dam-users` 路徑上的群組讀取許可權 `home/users`. 將許可權授與以下位置的使用者： `/content/dam/collections` 可讓使用者在快顯清單中檢視集合的位置。 或者，讓使用者成為 `dam-users` 群組。

1. （選用）為集合新增縮圖影像。
1. 按一下 **[!UICONTROL 建立]**，然後按一下 **[!UICONTROL 確定]** 以關閉對話方塊。 具有指定標題和屬性的系列會在「系列」主控台中開啟。

   >[!NOTE]
   >
   >[!DNL Experience Manager Assets] 可讓您為集合建立稽核任務，其方式與為資產資料夾建立稽核任務類似。

   若要將資產新增至收藏集，請導覽至 [!DNL Assets] 使用者介面。 如需詳細資訊，請參閱 [將資產新增至收藏集](#adding-assets-to-a-collection).

### 使用dropzone建立集合 {#create-collections-using-dropzone}

您可以從以下位置拖曳資產： [!DNL Assets] 集合的使用者介面。 您也可以建立收藏集的副本，並將資產拖曳至該處。

1. 從 [!DNL Assets] 使用者介面，選取您要新增至集合的資產。
1. 將資產拖曳至 **[!UICONTROL 放入集合]** 區域。 或者，按一下 **[!UICONTROL 至集合]** 工具列中的。

   ![drop_in_collection](assets/drop_in_collection.png)

1. 在 **[!UICONTROL 新增至集合]** 頁面，按一下 **[!UICONTROL 建立集合]** 工具列中的。

   如果您想要將資產新增至現有的系列，請從頁面中選取資產，然後按一下 **[!UICONTROL 新增]**. 依預設，會選取最近更新的系列。

1. 在「建 **[!UICONTROL 立新系列]** 」對話方塊中，指定系列的名稱。如果您希望系列可供所有使用者存取，請選取「公用 **[!UICONTROL 系列」]**。
1. 按一下 **[!UICONTROL 繼續]** 以建立集合。

### 建立智慧型集合 {#creating-a-smart-collection}

智慧型集合會使用搜尋條件來動態填入資產。 您可以只使用檔案來建立Smart Collection，而不使用資料夾或檔案與資料夾。

若要建立智慧型集合，請遵循下列步驟：

1. 導覽至 [!DNL Assets] 使用者介面，然後按一下「搜尋」。

1. 在Omnisearch方塊中輸入搜尋關鍵字，然後選取 `Enter`. 開啟「篩選器」面板並套用搜尋篩選器。

1. 從 **[!UICONTROL 檔案與資料夾]** 清單，選取 **[!UICONTROL 檔案]**.

   ![files_option](assets/files_option.png)

1. 按一下 **[!UICONTROL 儲存智慧型集合]**.

1. 指定集合的名稱。 選取 **[!UICONTROL 公共]** 將具有檢視器角色的DAM Users群組新增至智慧型集合。

   ![save_collection](assets/save_collection.png)

   >[!NOTE]
   >
   >如果您選取 **[!UICONTROL 公共]**，在您建立智慧型集合後，便能供擁有擁有擁有者角色的所有人使用。 如果您取消 **[!UICONTROL 公共]** 選項，DAM使用者群組不再與智慧型集合建立關聯。

1. 按一下 **[!UICONTROL 儲存]** 以建立智慧型集合，然後關閉訊息方塊以完成程式。

   新的智慧型系列也會新增至 **[!UICONTROL 已儲存的搜尋]** 清單。

   ![collection_listing](assets/collection_listing.png)

   的標籤 **[!UICONTROL 建立智慧型選取範圍]** 選項變更為 **[!UICONTROL 編輯智慧型選取範圍]**. 要編輯智慧系列的設定，請從「檔案和文 **[!UICONTROL 件夾]** 」列 **[!UICONTROL 表中選擇「檔案]** 」。按一下 **[!UICONTROL 編輯智慧型選取範圍]** ![編輯智慧型集合](assets/do-not-localize/edit-smart-collection.png) 選項。

## 將資產新增至收藏集 {#adding-assets-to-a-collection}

您可以將資產新增至包含參照資產或資料夾清單的集合。 智慧型集合會使用搜尋查詢來填入資產。 因此，資產和資料夾的靜態參考不適用於它們。

1. 在 [!DNL A]資產使用者介面，選取資產並按一下 **[!UICONTROL 至集合]** ![新增至集合](assets/do-not-localize/add-to-collection.png) 工具列中的。
或者，您可以將資產拖曳至 **[!UICONTROL 放入集合]** 區域。 當區域的標籤變更為時，新增資產 **[!UICONTROL 放置以新增]**.

1. 在 **[!UICONTROL 新增至集合]** 頁面上，選取您要新增資產的集合。

1. 按一下 **[!UICONTROL 新增]**，然後關閉確認訊息。 資產會新增至集合中。

## 編輯智慧型集合 {#editing-a-smart-collection}

智慧型集合是透過儲存搜尋來建置，因此您可以修改搜尋的搜尋引數來變更其內容。 [已儲存搜尋](#saved-searches).

1. 在 [!DNL Assets] 使用者介面，按一下搜尋選項 ![搜尋選項](assets/do-not-localize/search_icon.png) 工具列中的。
1. 將游標置於Omnisearch方塊中，選取 `Return` 機碼。
1. 在 [!DNL Experience Manager] 介面，開啟「篩選器」面板。
1. 從「保 **[!UICONTROL 存的搜索]** 」清單中，選擇要修改的智慧系列。「搜尋」面板會顯示為儲存的搜尋設定的篩選器。

   ![select_smart_collection](assets/select_smart_collection.png)

1. 從 **[!UICONTROL 檔案與資料夾]** 清單，選取 **[!UICONTROL 檔案]**.
1. 視需要修改一或多個篩選器。 按一下&#x200B;**[!UICONTROL 編輯智慧型集合]**。

   您也可以編輯智慧型集合的名稱。

   ![edit_smart_collectiondialog](assets/edit_smart_collectiondialog.png)

1. 按一下「**[!UICONTROL 儲存]**」。此 **[!UICONTROL 編輯智慧型集合]** 對話方塊隨即顯示。
1. 按一下 **[!UICONTROL 覆寫]** 以已編輯的集合取代原始的智慧型集合。 或者，選取 **[!UICONTROL 另存為]** 以分別儲存已編輯的集合。
1. 在確認對話方塊中，按一下 **[!UICONTROL 儲存]** 以完成程式。

## 檢視和編輯收藏集中繼資料 {#view-edit-collection-metadata}

收藏集中繼資料包含有關收藏集的資料，包括新增的任何標籤。

1. 從 [!UICONTROL 集合] 主控台，選取收藏集並按一下 **[!UICONTROL 屬性]** 工具列中的。
1. 在「系列 **[!UICONTROL 中繼資料]** 」頁面中，從「基本」和「進階」標籤檢視系 **[!UICONTROL 列中繼資]** 料 **** 。
1. 視需要修改中繼資料。 若要儲存變更，請按一下 **[!UICONTROL 儲存並關閉]** 工具列中的。

## 大量編輯多個集合的中繼資料 {#editing-collection-metadata-in-bulk}

您可以同時編輯多個集合的中繼資料。 此功能可協助您在多個集合中快速復寫常見的中繼資料。

1. 在「集合」控制檯中，選取兩個或多個集合。
1. 在工具列中按一下 **[!UICONTROL 屬性]**.
1. 在「系 **[!UICONTROL 列中繼資料]** 」頁面中，視需要編輯「基本」和「進階」標籤下的中繼資料 ******** 。
1. 若要檢視特定集合的中繼資料屬性，請取消選取集合清單中剩餘的集合。 中繼資料編輯器欄位會填入特定集合的中繼資料。

   >[!NOTE]
   >
   >* 在 [!UICONTROL 屬性] 頁面中，您可以取消選取專案，從集合清單中移除集合。 集合清單預設會選取所有集合。 [!DNL Experience Manager] 不會更新您移除之集合的中繼資料。
   >* 在清單頂端，選取附近的核取方塊 **[!UICONTROL 標題]** 在選取收藏集和清除清單之間切換。

1. 按一下 **[!UICONTROL 儲存並關閉]** ，然後關閉確認對話方塊。
1. 若要將新中繼資料附加至現有的中繼資料，請選取「 」 **[!UICONTROL 附加模式]**. 如果您未選取此選項，新的中繼資料會取代欄位中現有的中繼資料。按一下「**[!UICONTROL 提交]**」。

   >[!NOTE]
   >
   >您為所選集合新增的中繼資料會覆寫這些集合先前的中繼資料。 使用 [!UICONTROL 附加模式] 在可包含多個值的欄位中，將新值新增至現有的中繼資料。 一律會覆寫單值欄位。 您在中新增的任何標籤 [!UICONTROL 標籤] 欄位附加至中繼資料中的現有標籤清單。

自訂中繼資料 [!UICONTROL 屬性] 頁面，包括新增、修改、刪除中繼資料屬性，請使用「結構」編輯器。

>[!TIP]
>
>大量編輯方法適用於集合中可用的資產。 對於跨資料夾可用的資產或符合共同條件的資產，可以 [搜尋後大量更新中繼資料](/help/assets/search-assets.md#metadataupdates).

## 搜尋集合 {#searching-collections}

您可以從「集合」控制檯搜尋集合。 當您在Omnisearch方塊中使用關鍵字進行搜尋時， [!DNL Assets] 搜尋系列名稱、中繼資料和新增至系列的標籤。

如果您從最上層搜尋集合，搜尋結果中只會傳回個別集合。 [!DNL Assets] 會排除集合中的或資料夾。 在所有其他情況下（例如，在個別集合或資料夾階層中），所有相關的資產、資料夾和集合都會傳回。

## 在集合中搜尋 {#searching-within-collections}

在「系列」控制檯中，按一下某個系列以開啟它。

在集合中， [!DNL Experience Manager] 搜尋僅限於您檢視之收藏集中的資產（及其標籤和中繼資料）。 在資料夾中搜尋時，系統將會傳回目前資料夾中所有相符的資產和子資料夾。 在集合中搜尋時，系統只會傳回符合的資產、資料夾及屬於集合直接成員的其他集合。

## 編輯集合設定 {#editing-collection-settings}

您可以編輯收藏集設定（例如標題和說明），或將成員新增至收藏集。

1. 選取收藏集，然後按一下 **[!UICONTROL 設定]** （在工具列中）。 或者，使用 **[!UICONTROL 設定]** 集合縮圖中的快速動作。
1. 修改「系列設定」頁面中 **[!UICONTROL 的系列設定]** 。例如，修改系列標題、說明、成員和許可權，如中所述 [新增集合](#creating-a-collection).

1. 若要儲存變更，請按一下 **[!UICONTROL 儲存]**.

## 刪除收藏集 {#deleting-a-collection}

1. 在「系列」控制檯中，選取一或多個系列，然後在工具列按一下「刪除」 。

1. 在對話方塊中，按一下 **[!UICONTROL 刪除]** 以確認刪除動作。

   >[!NOTE]
   >
   >您也可以刪除智慧型集合，方法是 [刪除已儲存的搜尋](#saved-searches).

## 下載收藏集 {#downloading-a-collection}

下載收藏集時，會下載收藏集中資產的整個階層，包括資料夾和子收藏集。

1. 從「系列」控制檯中，選取要下載的一或多個系列。
1. 在工具列中按一下 **[!UICONTROL 下載]**.
1. 在 **[!UICONTROL 下載]** 對話方塊，按一下 **[!UICONTROL 下載]**. 如果您想要下載收藏集中資產的轉譯，請選取「 」 **[!UICONTROL 轉譯]**. 選取 **[!UICONTROL 電子郵件]** 傳送電子郵件通知給集合擁有者的選項。

   當您選取要下載的收藏集時，將會下載收藏集下的完整資料夾階層。 若要將您下載的每個收藏集（包括父收藏集巢狀下之子收藏集中的資產）納入個別資料夾中，請選取 **[!UICONTROL 為每個資產建立個別的資料夾]**.

## 建立巢狀集合 {#creating-nested-collections}

您可以將集合新增至另一個集合，藉此建立巢狀集合。

1. 從集合控制檯中，選取所需的集合或集合群組，然後按一下 **[!UICONTROL 至集合]** （在工具列中）。

1. 從 **[!UICONTROL 新增至集合]** 頁面上，選取要新增集合的集合。

   >[!NOTE]
   >
   >根據預設，系統會選取最近更新的集合，位於 **[!UICONTROL 新增至集合]** 頁面。

1. 按一下&#x200B;**[!UICONTROL 「新增」]**。訊息會確認此集合已新增至中的目標集合 **[!UICONTROL 選取目的地]** 頁面。 關閉訊息以完成程式。

>[!NOTE]
>
>智慧型集合無法巢狀化。 換言之，智慧型集合不能包含任何其他集合。

## 已儲存搜尋 {#saved-searches}

在 [!DNL Assets] 使用者介面，您可以根據特定規則、搜尋准則或自訂搜尋刻面來搜尋或篩選資產。 如果您將這些項目儲存為「 **[!UICONTROL 已儲存的搜尋]**」，您稍後可從「篩選」面板的「已儲存的搜尋 **** 」清單中存取。建立儲存的搜尋也會建立智慧型系列。

![saved_searches_list](assets/saved_searches_list.png)

儲存的搜尋會在您建立智慧型系列時建立。智慧型系列會自動新增至「已儲 **[!UICONTROL 存的搜尋]** 」清單。此 [!UICONTROL 已儲存的搜尋] 集合的查詢儲存在 `dam:query` CRXDE中相對位置的屬性 `/content/dam/collections/`. 您可以儲存的搜尋以及清單中顯示的已儲存搜尋沒有限制。

>[!NOTE]
>
>您可以使用與共用靜態集合相同的方式來共用智慧型集合。

編輯已儲存的搜尋與編輯智慧型集合相同。 如需詳細資訊，請參閱 [編輯智慧型集合](#editing-a-smart-collection).

若要刪除已儲存的搜尋，請執行下列步驟：

1. 在 [!DNL Assets] 使用者介面，按一下搜尋 ![搜尋選項](assets/do-not-localize/search_icon.png).
1. 將游標放在Omnisearch欄位中，選取 `Return` 機碼。
1. 在 [!DNL Experience Manager] 介面，開啟「篩選器」面板。
1. 從 **[!UICONTROL 已儲存的搜尋]** 清單，按一下 **[!UICONTROL 刪除]** ，位於您要刪除的智慧型集合旁。

   ![select_smart_collection](assets/select_smart_collection.png)

1. 在對話方塊中，按一下 **[!UICONTROL 刪除]** 以刪除儲存的搜尋。

## 對集合執行工作流程 {#running-a-workflow-on-a-collection}

您可以為集合中的資產執行工作流程。 如果集合包含巢狀集合，工作流程也會在巢狀集合內的資產上執行。 不過，如果收藏集和巢狀收藏集包含重複資產，工作流程僅會針對此類資產執行一次。

1. 開啟 **[!UICONTROL 資產]** > **[!UICONTROL 集合]**. 若要在特定集合上執行工作流程，請選取該工作流程。
1. 開啟 **[!UICONTROL 時間表]** 邊欄。 按一下 ![V形箭號](assets/do-not-localize/chevron-up-icon.png) 並按一下 **[!UICONTROL 開始工作流程]**.
1. 在「開 **[!UICONTROL 始工作流]** 」部分，從清單中選擇工作流模型。例如，選取「 **[!UICONTROL DAM更新資產」模型]** 。
1. 輸入工作流程的標題，然後按一下 **[!UICONTROL 開始]**.
1. 在對話方塊中，按一下 **[!UICONTROL 繼續]**. 工作流程會處理所選集合中的所有資產。

>[!MORELIKETHIS]
>
>* [設定Experience Manager Assets電子郵件通知](/help/sites-administering/notification.md#assetsconfig)
>* [建立集合的稽核任務](bulk-approval.md)
