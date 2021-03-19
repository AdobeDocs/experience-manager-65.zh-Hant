---
title: 管理數位資產集合
description: 瞭解要管理資產集合的任務，例如建立、檢視、刪除、編輯和下載系列。
contentOwner: AG
mini-toc-levels: 1
role: 業務從業人員
translation-type: tm+mt
source-git-commit: ebe7042b931869c3b4b7204e3ce7afa52d56f0ef
workflow-type: tm+mt
source-wordcount: '2182'
ht-degree: 11%

---


# 管理集合 {#managing-collections}

系列是[!DNL Adobe Experience Manager Assets]內的一組資產。 使用系列在使用者之間共用資產。 該集可以是靜態集合或基於搜索結果的動態集合。

與資料夾不同，系列可以包含不同位置的資產。 您可以與指派不同權限層級的不同使用者共用系列，包括檢視、編輯等。

您可以與使用者共用多個系列。 每個系列都包含資產的參考。 資產的參考完整性會跨系列維持。

系列是以下類型，依據其收集資產的方式：

* 包含資產、檔案夾和其他系列之靜態參考清單的系列。

* 智慧型系列，根據搜尋准則動態包含資產。

## 存取系列主控台{#navigating-the-collections-console}

若要開啟&#x200B;**[!UICONTROL Collections]**，請在[!DNL Experience Manager]介面中，前往&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Collections]**。

## 建立系列{#creating-a-collection}

您可以使用[靜態參考](#creating-a-collection-with-static-references)或根據[搜尋准則型篩選器](#creating-a-smart-collection)建立系列。 您也可以從燈箱建立系列。

### 建立包含靜態參考{#creating-a-collection-with-static-references}的系列

您可以建立包含靜態參考的系列，例如具有資產、檔案夾、系列、回轉集和影像集參考的系列。

1. 導覽至&#x200B;**[!UICONTROL Collections]**&#x200B;主控台。
1. 在工具欄中，按一下&#x200B;**[!UICONTROL 建立]**。
1. 在&#x200B;**[!UICONTROL 建立系列]**&#x200B;頁面中，輸入系列的標題和選用說明。
1. 新增成員至系列並指派適當的權限。或者，選取「 **[!UICONTROL 公用系列]** 」，讓所有使用者都能存取系列。

   >[!NOTE]
   >
   >若要讓成員與其他使用者共用系列，請在路徑`home/users`提供`dam-users`群組讀取權限。 為位於`/content/dam/collections`位置的使用者提供權限，讓使用者在快顯清單中檢視「系列」。 或者，讓使用者成為`dam-users`群組的一部分。

1. （選用）新增系列的縮圖影像。
1. 按一下&#x200B;**[!UICONTROL 建立]** ，然後按一下&#x200B;**[!UICONTROL 確定]**&#x200B;關閉對話框。 具有指定標題和屬性的系列會在「系列」主控台中開啟。

   >[!NOTE]
   >
   >[!DNL Experience Manager Assets] 可讓您建立系列的審閱工作，類似為資產檔案夾建立審閱工作的方式。

   若要新增資產至系列，請導覽至[!DNL Assets]使用者介面。 如需詳細資訊，請參閱[將資產新增至系列](#adding-assets-to-a-collection)。

### 使用dropzone {#create-collections-using-dropzone}建立系列

您可以將資產從[!DNL Assets]使用者介面拖曳至系列。 您也可以建立系列的復本，並將資產拖曳至該處。

1. 從[!DNL Assets]使用者介面中，選取您要新增至系列的資產。
1. 將資產拖曳至&#x200B;**[!UICONTROL Drop in Collection]**&#x200B;區域。 或者，從工具列按一下「收藏」**[!UICONTROL 。]**

   ![drop_in_collection](assets/drop_in_collection.png)

1. 在&#x200B;**[!UICONTROL 新增至系列]**&#x200B;頁面中，從工具列按一下「建立系列&#x200B;**[!UICONTROL 」。]**

   如果您想要將資產新增至現有的系列，請從頁面中選取資產，然後按一下「新增&#x200B;****」。 依預設，會選取最近更新的系列。

1. 在「建 **[!UICONTROL 立新系列]** 」對話方塊中，指定系列的名稱。如果您希望系列可供所有使用者存取，請選取「公用 **[!UICONTROL 系列」]**。
1. 按一下&#x200B;**[!UICONTROL 繼續]**&#x200B;以建立系列。

### 建立智慧型系列{#creating-a-smart-collection}

智慧型收集會使用搜尋准則來動態填入資產。 您只能使用檔案（而不是資料夾或檔案和資料夾）建立Smart Collection。

若要建立智慧型系列，請依照下列步驟進行：

1. 導覽至[!DNL Assets]使用者介面，然後按一下搜尋。

1. 在Omnisearch方塊中輸入搜尋關鍵字，然後選取`Enter`。 開啟「篩選」面板並套用搜尋篩選。

1. 從&#x200B;**[!UICONTROL 檔案和資料夾]**&#x200B;清單中，選擇&#x200B;**[!UICONTROL 檔案]**。

   ![files_option](assets/files_option.png)

1. 按一下「儲存智慧型系列」。****

1. 指定系列的名稱。 選擇&#x200B;**[!UICONTROL Public]**&#x200B;將具有查看器角色的DAM用戶組添加到智慧系列。

   ![save_collection](assets/save_collection.png)

   >[!NOTE]
   >
   >如果您選擇&#x200B;**[!UICONTROL Public]**，則在建立智慧系列後，所有具有所有者角色的人都可以使用該智慧系列。 如果您取消&#x200B;**[!UICONTROL Public]**&#x200B;選項，DAM使用者群組將不再與智慧型系列相關聯。

1. 按一下&#x200B;**[!UICONTROL 保存]**&#x200B;建立智慧集合，然後關閉消息框以完成該過程。

   新的智慧型系列也會新增至「已儲存的搜尋」清單。****

   ![collection_listing](assets/collection_listing.png)

   **[!UICONTROL 建立智慧選擇]**&#x200B;選項的標籤將更改為&#x200B;**[!UICONTROL 編輯智慧選擇]**。 要編輯智慧系列的設定，請從「檔案和文 **[!UICONTROL 件夾]** 」列 **[!UICONTROL 表中選擇「檔案]** 」。按一下「編輯智慧選擇」**** ![編輯智慧集合](assets/do-not-localize/edit-smart-collection.png)選項。

## 將資產新增至系列{#adding-assets-to-a-collection}

您可以將資產新增至包含參考資產或檔案夾清單的系列。 智慧型系列使用搜尋查詢來填入資產。 因此，資產和檔案夾的靜態參考不適用。

1. 在[!DNL A]ssets使用者介面中，選取資產，然後從工具列按一下「至系列&#x200B;**** ![新增至系列](assets/do-not-localize/add-to-collection.png)」。
或者，您也可以將資產拖曳至介面上的「拖曳至系列」區域。 ****&#x200B;當區域的標籤變更為&#x200B;**[!UICONTROL 拖放至新增]**&#x200B;時新增資產。

1. 在&#x200B;**[!UICONTROL 新增至系列]**&#x200B;頁面中，選取您要新增資產的系列。

1. 按一下&#x200B;**[!UICONTROL 添加]** ，然後關閉確認消息。 資產會新增至系列。

## 編輯智慧型系列{#editing-a-smart-collection}

智慧型系列是透過儲存搜尋來建立的，因此您可以修改[已儲存搜尋](#saved-searches)的搜尋參數來變更其內容。

1. 在[!DNL Assets]使用者介面中，按一下工具列中的搜尋選項![搜尋選項](assets/do-not-localize/search_icon.png)。
1. 在「Omnisearch」（搜索）框中，選擇`Return`鍵。
1. 在[!DNL Experience Manager]介面中，開啟「篩選」面板。
1. 從「保 **[!UICONTROL 存的搜索]** 」清單中，選擇要修改的智慧系列。「搜尋」面板會顯示為儲存的搜尋設定的篩選器。

   ![select_smart_collection](assets/select_smart_collection.png)

1. 從&#x200B;**[!UICONTROL 檔案和資料夾]**&#x200B;清單中，選擇&#x200B;**[!UICONTROL 檔案]**。
1. 視需要修改一或多個篩選器。 按一下「編輯智慧型系列」。****

   您也可以編輯智慧型系列的名稱。

   ![edit_smart_collection對話框](assets/edit_smart_collectiondialog.png)

1. 按一下「**[!UICONTROL 儲存]**」。此時將顯示&#x200B;**[!UICONTROL 編輯智慧集合]**&#x200B;對話框。
1. 按一下「覆寫&#x200B;**[!UICONTROL 」，以編輯的系列取代原始的智慧型系列。]**&#x200B;或者，選擇「另存新檔」以個別儲存已編輯的系列。****
1. 在確認對話框中，按一下&#x200B;**[!UICONTROL 保存]**&#x200B;以完成該過程。

## 檢視並編輯系列中繼資料{#view-edit-collection-metadata}

系列中繼資料包含系列的相關資料，包括所新增的任何標籤。

1. 從[!UICONTROL Collections]控制台中，選擇一個系列，然後從工具欄中按一下「屬性」。****
1. 在「系列 **[!UICONTROL 中繼資料]** 」頁面中，從「基本」和「進階」標籤檢視系 **[!UICONTROL 列中繼資]** 料 **** 。
1. 視需要修改中繼資料。 要保存更改，請按一下工具欄中的&#x200B;**[!UICONTROL 保存並關閉]**。

## 大量編輯多個系列的中繼資料{#editing-collection-metadata-in-bulk}

您可以同時編輯多個系列的中繼資料。 這項功能可協助您快速複製多個系列中的常用中繼資料。

1. 在「系列」控制台中，選取兩或多個系列。
1. 在工具欄中，按一下&#x200B;**[!UICONTROL 屬性]**。
1. 在「系 **[!UICONTROL 列中繼資料]** 」頁面中，視需要編輯「基本」和「進階」標籤下的中繼資料 ******** 。
1. 若要檢視特定系列的中繼資料屬性，請取消在系列清單中選取剩餘的系列。 中繼資料編輯器欄位會填入特定系列的中繼資料。

   >[!NOTE]
   >
   >* 在[!UICONTROL 屬性]頁面中，您可以取消選擇，從系列清單中移除系列。 系列清單預設會選取所有系列。 [!DNL Experience Manager] 不會更新您移除之系列的中繼資料。
   >* 在清單頂端，選取&#x200B;**[!UICONTROL Title]**&#x200B;附近的核取方塊，在選取系列和清除清單之間切換。


1. 從工具列按一下「儲存並關閉」，然後關閉確認對話方塊。****
1. 要將新元資料與現有元資料一起附加，請選擇&#x200B;**[!UICONTROL 附加模式]**。 如果您未選取此選項，新的中繼資料會取代欄位中現有的中繼資料。按一下&#x200B;**[!UICONTROL 提交]**。

   >[!NOTE]
   >
   >您為所選系列新增的中繼資料會覆寫這些系列的先前中繼資料。 使用[!UICONTROL 附加模式]，在可包含多個值的欄位中，將新值新增至現有的中繼資料。 一律會覆寫單一值欄位。 您在[!UICONTROL Tags]欄位中新增的任何標籤，都會附加至中繼資料中現有的標籤清單。

要自定義元資料[!UICONTROL 屬性]頁，包括添加、修改、刪除元資料屬性，請使用模式編輯器。

>[!TIP]
>
>批量編輯方法適用於系列中的可用資產。 對於跨資料夾可用或符合一般准則的資產，可在搜尋](/help/assets/search-assets.md#metadataupdates)後，大量更新中繼資料。[

## 搜尋系列{#searching-collections}

您可以從「系列」主控台搜尋系列。 當您在Omnisearch方塊中搜尋關鍵字時，[!DNL Assets]會搜尋系列名稱、中繼資料和新增至系列的標籤。

如果您從頂層搜尋系列，搜尋結果中只會傳回個別的系列。 [!DNL Assets] 或系列中的檔案夾會排除。在所有其他情況下（例如，在個別系列或檔案夾階層中），會傳回所有相關資產、檔案夾和系列。

## 在系列中搜尋{#searching-within-collections}

在「系列」控制台中，按一下系列以開啟它。

在系列中，[!DNL Experience Manager]搜尋會限制在您檢視之系列中的資產（及其標籤和中繼資料）。 當您在資料夾內搜尋時，會傳回目前資料夾內所有相符的資產和子資料夾。 當您在系列中搜尋時，只會傳回符合的資產、檔案夾和其他系列，這些系列是系列的直接成員。

## 編輯系列設定{#editing-collection-settings}

您可以編輯系列設定，例如標題和說明，或新增成員至系列。

1. 選取系列，然後按一下工具列中的「設定」****。 或者，從系列縮圖使用&#x200B;**[!UICONTROL Settings]**&#x200B;快速動作。
1. 修改「系列設定」頁面中 **[!UICONTROL 的系列設定]** 。例如，修改系列標題、說明、成員和權限，如[新增系列](#creating-a-collection)中所述。

1. 要保存更改，請按一下「保存」。****

## 刪除系列{#deleting-a-collection}

1. 從「系列」控制台中，選取一或多個系列，然後從工具列按一下「刪除」。

1. 在對話框中，按一下&#x200B;**[!UICONTROL Delete]**&#x200B;確認刪除操作。

   >[!NOTE]
   >
   >您也可以透過[刪除已儲存的搜尋](#saved-searches)來刪除智慧型系列。

## 下載系列{#downloading-a-collection}

當您下載系列時，系列中資產的整個階層會下載，包括檔案夾和子系列。

1. 從「系列」主控台中，選取一或多個要下載的系列。
1. 從工具列按一下&#x200B;**[!UICONTROL 下載]**。
1. 在&#x200B;**[!UICONTROL 下載]**&#x200B;對話方塊中，按一下&#x200B;**[!UICONTROL 下載]**。 如果您想要下載系列中資產的轉譯，請選取「轉譯」**[!UICONTROL 「轉譯」]**。 選擇&#x200B;**[!UICONTROL Email]**&#x200B;選項，以傳送電子郵件通知給系列的擁有者。

   當您選取要下載的系列時，系列下方的完整檔案夾階層會下載。 若要將您下載的每個系列（包括父系列下巢狀的子系列中的資產）包含在個別檔案夾中，請選取&#x200B;**[!UICONTROL 為每個資產建立個別的檔案夾]**。

## 建立巢狀系列{#creating-nested-collections}

您可以新增系列至另一個系列，從而建立巢狀系列。

1. 從「系列」控制台中，選取所要的系列或系列群組，然後按一下工具列中的「至系列」**[!UICONTROL 。]**

1. 從&#x200B;**[!UICONTROL 新增至系列]**&#x200B;頁面中，選取要新增系列的系列。

   >[!NOTE]
   >
   >在&#x200B;**[!UICONTROL 新增至系列]**&#x200B;頁面中，預設會選取最近更新的系列。

1. 按一下&#x200B;**[!UICONTROL 「新增」]**。訊息會確認系列已新增至&#x200B;**[!UICONTROL 選擇目標]**&#x200B;頁面中的目標系列。 關閉訊息以完成程式。

>[!NOTE]
>
>智慧型系列無法巢狀化。 換言之，智慧型系列不能包含任何其他系列。

## 保存的搜索{#saved-searches}

在[!DNL Assets]使用者介面中，您可以根據特定規則、搜尋准則或自訂搜尋刻面來搜尋或篩選資產。 如果您將這些項目儲存為「 **[!UICONTROL 已儲存的搜尋]**」，您稍後可從「篩選」面板的「已儲存的搜尋 **** 」清單中存取。建立儲存的搜尋也會建立智慧型系列。

![saved_searches_list](assets/saved_searches_list.png)

儲存的搜尋會在您建立智慧型系列時建立。智慧型系列會自動新增至「已儲 **[!UICONTROL 存的搜尋]** 」清單。系列的[!UICONTROL Saved Searches]查詢會儲存在CRXDE的`dam:query`屬性中，位於相對位置`/content/dam/collections/`。 您可以儲存的搜尋和清單中顯示的已儲存搜尋沒有限制。

>[!NOTE]
>
>您可以以共用靜態系列的相同方式共用智慧型系列。

編輯已儲存的搜尋與編輯智慧型系列相同。 如需詳細資訊，請參閱[編輯智慧型系列](#editing-a-smart-collection)。

要刪除保存的搜索，請執行以下步驟：

1. 在[!DNL Assets]使用者介面中，按一下搜尋![搜尋選項](assets/do-not-localize/search_icon.png)。
1. 在「Omnisearch」（搜索）欄位中，選擇`Return`鍵。
1. 在[!DNL Experience Manager]介面中，開啟「篩選」面板。
1. 在&#x200B;**[!UICONTROL 儲存的搜尋]**&#x200B;清單中，按一下您要刪除的智慧型系列旁的&#x200B;**[!UICONTROL 刪除]**。

   ![select_smart_collection](assets/select_smart_collection.png)

1. 在對話框中，按一下&#x200B;**[!UICONTROL Delete]**&#x200B;刪除保存的搜索。

## 在系列{#running-a-workflow-on-a-collection}上執行工作流程

您可以為系列中的資產執行工作流程。 如果系列包含巢狀系列，工作流程也會在巢狀系列內的資產上執行。 不過，如果系列和巢狀系列包含重複的資產，此類資產的工作流程只會執行一次。

1. 開啟&#x200B;**[!UICONTROL 資產]** > **[!UICONTROL 系列]**。 若要在特定系列上執行工作流程，請選取它。
1. 開啟&#x200B;**[!UICONTROL 時間軸]**&#x200B;邊欄。 按一下![chevron up](assets/do-not-localize/chevron-up-icon.png) ，然後按一下&#x200B;**[!UICONTROL 啟動工作流]**。
1. 在「開 **[!UICONTROL 始工作流]** 」部分，從清單中選擇工作流模型。例如，選取「 **[!UICONTROL DAM更新資產」模型]** 。
1. 輸入工作流的標題，然後按一下&#x200B;**[!UICONTROL 開始]**。
1. 在對話框中，按一下&#x200B;**[!UICONTROL 繼續]**。 工作流程會處理所選集合中的所有資產。

>[!MORELIKETHIS]
>
>* [設定Experience Manager資產電子郵件通知](/help/sites-administering/notification.md#assetsconfig)
>* [建立系列的審閱工作](bulk-approval.md)

