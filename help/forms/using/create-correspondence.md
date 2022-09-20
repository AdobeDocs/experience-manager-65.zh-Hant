---
title: 建立通信
seo-title: Create Correspondence
description: 建立信函範本後，您就可以透過管理資料、內容及附件，使用該範本在AEM Forms中建立通信。
seo-description: After you have created a letter template, you can use it to create correspondence in AEM Forms by managing data, content, and attachments.
uuid: 48cf2b26-c9b4-4127-9ea0-1b36addbff60
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 87742cb2-357b-421f-b79d-e355887ddec0
docset: aem65
feature: Correspondence Management
exl-id: da966787-a3b9-420f-8b7c-f00d05c61d43
source-git-commit: 1a6881b29024799c44b2068ea82750c983a012e5
workflow-type: tm+mt
source-wordcount: '3867'
ht-degree: 0%

---

# 建立通信{#create-correspondence}

## 在建立通信用戶介面中建立通信 {#create-correspondence-in-the-create-correspondence-user-interface}

之後 [信函範本是在通信管理中建立](../../forms/using/create-letter.md)，最終用戶/代理/聲明調整器可以在「建立通信」用戶介面中開啟信函，並通過輸入資料、設定內容和管理附件來建立通信。 最後，聲明調整者或代理可以在預覽模式下管理內容並提交信函。

### 預覽通信 {#preview-a-correspondence}

使用下列步驟選擇要預覽的信函：

1. 在「信函」頁面上，點選 **選擇**.
1. 點選適當的字母。

   ![選擇信函](assets/1_selectletter.png)

   選擇信函

1. 若為以資料字典為基礎的信函，請選取 **預覽** > **預覽**. 或者，對於非資料字典型信函，請選取 **預覽**. 您也可以將滑鼠指標暫留在信函上（未選取），然後點選「信函預覽」圖示以預覽。

   >[!NOTE]
   >
   >如果資料字典未與信函相關聯，信函預覽隨即開啟。 否則，如果信函是以資料字典為基礎，則通信管理會在「預覽」功能表中顯示「預覽」和「自訂」選項，您可以選取這兩個選項之一。 您也可以將測試資料與資料字典建立關聯。 當 [資料字典具有關聯的測試資料](../../forms/using/data-dictionary.md#p-working-with-test-data-p)，然後選取預覽選項時，一般預覽隨即開啟，並填入測試資料。

1. 若要在預覽通信時轉譯通信，您應是管理員或下列其中一個群組的一員：

   * forms-users（在製作執行個體上預覽）
   * cm-agent-users（用於發佈實例上的轉譯）

   如果您不具備必要的權限，請向管理員要求適當的存取權。 如需建立使用者及將使用者新增至群組的詳細資訊，請參閱 [新增使用者或群組至群組](/help/sites-administering/security.md). 如果您嘗試在沒有適當權限的情況下轉譯通信，則會顯示404錯誤頁面。

1. 如果您已選取 **預覽** > **自訂**，則會開啟對話方塊。 在對話方塊中，選取與資料字典對應的資料檔案，以預覽信函，然後選取 **預覽**. 根據特定信函的資料字典來建立資料檔案。 如需資料檔案的詳細資訊，請參閱 [資料字典](../../forms/using/data-dictionary.md#p-working-with-test-data-p).

   ![預覽信函](assets/8_previewcustomdatafile.png)

1. 信函HTML預覽（行動表單預覽）會隨著「資料」索引標籤的焦點預設開啟。

   如需行動表單及其支援功能的詳細資訊，請參閱 [Mobile Forms和PDF forms的功能差異](https://helpx.adobe.com/livecycle/help/mobile-forms/feature-differentiation-mobile-forms-pdf.html).

   有三個索引標籤：資料、內容和附件。 如果沒有資料元素（預留位置變數和佈局欄位），則信函會直接在中開啟，並顯示「內容」索引標籤。 只有在附件存在或啟用庫訪問時，附件頁簽才可用。

   >[!NOTE]
   >
   >如需在信函預覽的HTML或PDF轉譯模式之間切換的詳細資訊，請參閱 [更改信函的轉譯模式](#changerenditionmode). 如需通信管理和AEM中PDF支援的詳細資訊，請參閱 [中止NPAPI瀏覽器外掛程式及其影響](https://helpx.adobe.com/aem-forms/kb/discontinuation-of-npapi-plugins-impact-on-aem-forms.html) 和 [PDF forms至HTML5 Forms](https://helpx.adobe.com/aem-forms/kb/pdf-forms-to-html5-forms.html).

### 輸入資料 {#enterdata}

在「資料」索引標籤中，填入可用的版面欄位和預留位置。

1. 視需要在欄位中輸入資料和內容變數。 填寫標有星號(&#42;)啟用 **提交** 按鈕。

   點選HTML信函預覽中的資料欄位值，以在「資料」標籤中反白顯示對應的資料欄位。

   ![在信函中輸入資料](assets/2_enterdata.png) ![2_1_enterdata](assets/2_1_enterdata.png)

### 管理內容 {#managecontent}

在內容索引標籤中，管理信函中的檔案片段和內容變數等內容。

1. 選擇 **內容**. 通信管理會顯示信函的內容索引標籤。

   ![內容標籤 — 在內容中反白標示模組](assets/3_content.png)

1. 視需要在「內容」索引標籤中編輯內容模組。 若要聚焦到內容階層中的相關內容模組，您可以點選信函預覽中的相關行或段落，或直接點選內容階層中的內容模組。

   例如，在下圖中選取了「我們已檢閱……」行，並在「內容」索引標籤中選取了相關內容模組。

   ![4_highlightmoduleincontent](assets/4_highlightmoduleincontent.png)

   在「內容」或「資料」索引標籤中，點選「反白標示選取的模組」( ![highlightselectedmodulesincontentccr](assets/highlightselectedmodulesincontentccr.png))，您可以在信函預覽中選取相關文字、段落或資料欄位時，停用或啟用前往內容/資料模組的功能。

   如需建立通信使用者介面中各種模組可用動作的詳細資訊，請參閱 [「建立通信」使用者介面中可用的動作和資訊](#actions-and-info-available-in-the-create-correspondence-content-tab).

1. 要查找內容模組，請使用「查找」欄位。 輸入內容模組的完整或部分名稱或標題，以在通信中搜索該名稱。
1. 點選「顯示」圖示( ![顯示](assets/display.png))，在清單、文字、條件或目標區域前顯示或隱藏信函。
1. 若要編輯內嵌或可編輯的文字模組，請點選相關 **編輯** 圖示( ![edittextmodule](assets/edittextmodule.png))或在信函預覽中連按兩下相關的文字模組。

   系統會顯示一個文本編輯器以編輯文本並設定其格式。

   瀏覽器中的預設拼字檢查程式會在文字編輯器中檢查拼字。 若要管理拼字和語法檢查，您可以編輯瀏覽器的拼字檢查程式設定，或安裝瀏覽器外掛程式/附加程式以檢查拼字和語法。

   您也可以使用文字編輯器中的各種鍵盤快速鍵來管理、編輯及格式化文字。 如需 [文字編輯器](/help/forms/using/keyboard-shortcuts.md#correspondence-management) 通信管理鍵盤快速鍵中的鍵盤快速鍵。

   ![5_edittextmodule](assets/5_edittextmodule.png)

   您可能希望重複使用文檔的另一個應用程式中存在的多個文本段落之一。 您可以直接複製和貼上文字，例如來自MS Word、HTML頁面或任何其他應用程式。

   您可以在可編輯的文字模組中複製並貼上一或多段文字。 例如，您可能有MS Word文檔，其中包含可接受居留校樣的項目符號清單，如下所示：

   ![巴斯德文字](assets/pastetextmsword.png)

   您可以直接將MS Word檔案中的文字複製並貼到可編輯的文字模組。 文本模組中將保留項目符號清單、字型和文本顏色等格式。

   ![pastetexteditablemodule](assets/pastetexteditablemodule.png)

   >[!NOTE]
   >
   >但貼上文字的格式有一些 [限制](https://helpx.adobe.com/aem-forms/kb/cm-copy-paste-text-limitations.html).

   您可以使用Tab鍵縮進信函中的文字和數字。 例如，您可以使用Tab鍵將清單中的多欄文字對齊為表格格式。

   ![tablespace](assets/tabspaces.png)

   範例：使用Tab鍵將多列文本對齊為表格格式

   >[!NOTE]
   >
   >有關為文本模組和字母設定頁簽間距的詳細資訊，請參閱 [有關使用頁簽間距排列文本的詳細資訊](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html).

1. 如果需要，請在通信中插入特殊字元。 例如，您可以使用「特殊字元」浮動視窗來插入：

   * 貨幣符號，如€、¥和£
   * 數學符號，如∑、√、∂和^
   * 標點符號，例如&quot;和&quot;

   ![特殊字元](assets/specialcharacters.png)

   通信管理內建支援210個特殊字元。 管理員可 [新增支援更多/自訂特殊字元，可依自訂](../../forms/using/custom-special-characters.md).

1. 要在可編輯的內嵌模組中突出顯示\強調部分文本，請選擇文本並點選「突出顯示顏色」。

   ![背景顏色](assets/letterbackgroundcolor.png)

   您可以直接點選基本顏色 `**[A]**` 顯示在「基本顏色」調色板中或點選 **選擇** 使用滑桿後 `**[B]**` 來選擇適當的顏色。

   （可選）您也可以轉到「高級」頁簽，以選擇適當的「色相」、「明度」和「飽和度」 `**[C]**` 要建立精確顏色，然後點選「選擇」 `**[D]**` ，以應用顏色來突出顯示文本。

   ![textbackgroundcolor](assets/textbackgroundcolor.png)

1. 進行適當的內容和格式變更，並點選 **儲存**. 點選( ![editnextmoduleccr](assets/editnextmoduleccr.png))來在可編輯的文字模組之間移動，或點選 **儲存和下一個** 以儲存變更並移至下一個可編輯的文字模組。
1. 系統也會顯示每個分支的未填充變數。 當沒有未填充的變數時，未填充的變數會顯示為0。 如果有未填充的變數，您可以點選分支以展開該分支，並找出未填入的變數。 使用內容工具欄來刪除內容、增加/減少內容的縮進，以及在內容之前/之後插入分頁符。

   您可以在資料模組的上方和下方插入分頁符，即使這些分頁符是清單和條件的一部分亦然。

1. 點選「開啟/關閉內容變數」( ![opencontentvariables](assets/opencontentvariables.png))以開啟內容變數並適當填入。
1. 正確填入未填入的變數後，未填入的變數的計數會設為0。

   在「建立通信」使用者介面中，未填入的變數計數會顯示在任何包含至少一個變數之模組階層的每個層級。 如果模組包含未填充的變數，則計數會顯示在變數、模組、目標區域和信函範本層級。

   未填入的變數計數包括：

   * 只有未受保護的資料字典和佔位符變數。 變數計數不包含配置或受保護的資料字典變數。
   * 必填欄位。
   * 版面欄位（若為必填欄位）並系結至使用者。
   * 僅限唯一變數例項。 如果模組、目標區域或信函範本包含相同變數的兩個或多個例項，則計數會顯示為1(1)。 不過，對於每個例項，計數會顯示為1。

   未填入的變數計數不包含取消選取的模組。 如果模組包含在信函範本中，但不在信函中，則不會顯示此模組中未填充變數的計數。

   對於目標區域、模組和變數，計數會顯示在信函範本中每個物件的右側。 不過，對於完整範本，計數會顯示在「建立通信」狀態列中。

   信函範本中的模組會顯示未填入的變數計數，如下所述：

   * **文字** 顯示文字模組中包含的不重複未填入預留位置變數和資料字典元素的總和。
   * **條件** 顯示條件中包含的唯一未填充條件變數和結果模組中包含的變數的總和。
   * **清單** 顯示指派給清單的模組中包含的所有不重複未填變數的總和。
   * **目標區域** 顯示指派給目標區域的模組中包含的所有唯一未填變數的總和。

   請留意下列關於具有預設值的變數：

   * 布林變數欄位預設為 *false*. 不過，變數仍被視為未填入。 這表示變數計數會包含所有具有值的布林變數欄位 *false*.

   * 數值變數欄位預設為 *0（零）*. 不過，變數仍被視為未填入。 這表示變數計數會包含所有具有值的數值變數欄位 *0（零）*.



#### 「建立通信內容」索引標籤中可用的動作和資訊 {#actions-and-info-available-in-the-create-correspondence-content-tab}

**目標區域**

* 插入空白行：插入新的空行。
* 插入內嵌文字：插入新文本模組。
* 訂購鎖（資訊）:表示無法變更內容的順序。
* 未填充的值（資訊）:指示目標區域中未填充的變數的數量。

**模組**

* 選擇（眼睛表徵圖）:在信函中包括\排除模組。
* 跳過項目符號（適用於清單模組及其子模組）:跳過特定模組中的子彈。
* 前分頁符（適用於目標區域的子模組）:在模組前插入分頁符。
* 後分頁符（適用於目標區域的子模組）:在模組前插入分頁符。
* 未填充的值（資訊）:指示目標區域中未填充的變數的數量。
* 編輯（僅限文字模組）:開啟RTF編輯器以編輯文字模組。
* 資料面板（文字和條件模組）:開啟模組的所有變數。

**清單模組**

* 插入空白行：插入新的空行。
* 內容庫：開啟內容庫以將模組添加到清單中。
* 清單設定（僅限巢狀清單）:
* 訂購鎖（資訊）:指出無法變更清單項目的順序。

### 管理附件 {#manage-attachments}

1. 選擇 **附件**. 「通信管理」會依照建立信函範本時的設定，顯示可用的附件。
1. 您可以點選檢視圖示，選擇不隨信函提交附件，並點選附件中的十字以從信函中刪除。 對於指定的附件，在建立信函模板時，視圖和刪除表徵圖為「強制」，將被禁用。
1. 點選程式庫存取( ![程式庫存取](assets/libraryaccess.png))圖示來存取「內容資料庫」 ，以插入DAM資產作為附件。

   >[!NOTE]
   >
   >「程式庫存取」圖示僅在編寫信函時啟用程式庫存取。

1. 如果建立通信時未鎖定附件的順序，則可以通過選擇附件並點選向下和向上箭頭來重新排序附件。

   如需詳細資訊，請參閱 [附件傳送](#attachmentdelivery).

### 在預覽中管理內容並提交信函 {#manage-content-in-preview-and-submit-the-letter}

您可以進行版面配置和內容相關變更，確保信函的外觀符合您的預期，並提交至各種貼文程式。

1. 若要反白顯示信函中所有可編輯的內容，請點選 **反白顯示可編輯的區段**.

   信函的可編輯內容會以灰色背景強調顯示。

   ![反白顯示可編輯的內容](assets/4_highlightmoduleincontent-1.png)

1. 視需要在「內容」索引標籤中編輯內容模組。 若要聚焦到內容階層中的相關內容模組，您可以點選信函預覽中的相關行或段落，或直接點選內容階層中的內容模組。

   例如，行「允許我們存取……」 在下圖中選取，並在「內容」索引標籤中選取對應的內容模組。

   點選「在內容中反白顯示選取的模組」( ![highlightselectedmodulesincontentccr](assets/highlightselectedmodulesincontentccr.png))，則在信函預覽中點選相關文字、段落或資料欄位時，您可以停用或啟用功能，以反白標示「內容」索引標籤中的內容模組。

   如需建立通信使用者介面中各種模組可用動作的詳細資訊，請參閱 [「建立通信」使用者介面中可用的動作和資訊](#actions-and-info-available-in-the-create-correspondence-content-tab).

1. 若要將分頁符新增至信函，請點選您要插入分頁符的位置，然後選取「分頁符之前」或「分頁符之後」( ![pagebreakbefore](assets/pagebreakbeforeafter.png))。

   信函中插入明確的分頁符預留位置。 若要檢視明確的分頁符對信函的影響，請參閱平面化PDF預覽。

   >[!NOTE]
   >
   >由於行動表單不支援分頁，因此頁首和頁尾只會顯示一次。 不過，您可以在版面（每頁）中明確設定頁首和頁尾，以便顯示在行動表單預覽中。 此外，信函中的空白頁面（如果有的話）不會顯示在行動表單預覽中。

   ![顯式分頁符](assets/8_pagebreak.png)

1. 若要將信函儲存為草稿，而稍後可繼續處理，請點選「另存為草稿」。 若要使用此選項，您的信函必須 [已發佈](../../forms/using/publishing-unpublishing-forms.md#publishanasset). 如需詳細資訊，請參閱下方的草稿例項 [保存草稿和提交信函實例](#savingdrafts).

   ![saveasdraft](assets/saveasdraft.png)

   出現「Draft Letter Name（繪製字母名稱）」對話框，其中包含字母實例ID。 您可以選擇編輯此ID。 記下字母Id，然後點選 **完成**. 您稍後可以將此ID用於 [重新載入草稿信](submit-letter-topostprocess.md#reloaddraft).

1. 若要以平面化PDF預覽信函，並具有確切的版面和將提交時的分頁符，請點選( ![預覽](assets/preview.png))預覽。

   信函會以平面化PDF顯示。 拼合PDF是信函的確切表示，因為它將以信函的正確字型、斷字和版面來提交。

   >[!NOTE]
   >
   >如果您使用Mozilla Firefox和HTML轉譯類型，若要將信函預覽為平面化PDF，請確定您使用原生瀏覽器外掛程式，而非Acrobat外掛程式。 若要選取原生瀏覽器外掛程式，請前往Mozilla Firefox的設定，並針對內容類型PDF，選取「在Firefox中預覽」。

1. 如果您覺得平面化PDF預覽滿意，請點選 **提交** 來提交信。 或者，若要對信函進行變更，請點選 **退出預覽** 返回信函的「建立通信UI」預覽，以變更信函。 當您點選「提交」時，如果在「發佈」執行個體上啟用「管理信函例項」設定，則會產生提交信函例項。

   如需詳細資訊，請參閱儲存草稿和提交信函例項下方的草稿例項。

   您也可以將信函儲存為草稿，以便稍後變更信函。

   進行所需的變更後，您可以從HTML5預覽提交信函，或再次點選「預覽」以檢閱平面化的PDF輸出。

   如需HTML5表單與PDF forms之間差異的詳細資訊，請參閱 [HTML5表單和PDF forms之間的功能差異](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

## 保存草稿和提交信函實例 {#savingdrafts}

在「建立通信」使用者介面中轉譯信函時，您可以將信函儲存為已檢視。

可儲存的信函例項有兩種類型：草稿例項和提交例項。

* **草稿例項**:草稿例項會擷取您正在預覽之信函的目前狀態。 若要儲存草稿例項，請先確定信函參照的字母和所有資產都處於「已發佈」狀態。 如需發佈信函的詳細資訊，請參閱 [發佈資產](../../forms/using/publishing-unpublishing-forms.md#publishanasset). 您需要先發佈信函，才能將其儲存為草稿，因為當您發佈信函時，會建立信函版本、其相依資產，以及該時間點的資料。 信函的已發佈版本無法由您或其他使用者編輯，且稍後可還原，而未發生任何已發佈版本的非預期差異。 您稍後可以返回此執行個體，並從您離開的位置繼續。

* **提交實例**:提交例項會在提交時擷取信函狀態。 提交執行個體會在信函執行個體經過後與使用者在建立通信使用者介面中輸入的資料一起處理後，儲存其PDF狀態。

只有在發佈執行個體上檢視信函時，才能儲存這類執行個體。 預設情況下，關閉執行個體的儲存。 要啟用信函實例的保存，請執行以下步驟。

1. 在AEM中，使用下列URL開啟您伺服器的Adobe Experience Manager Web Console設定：https://&lt;server>:&lt;port>/&lt;contextpath>/system/console/configMgr
1. 找出 **[!UICONTROL 通信管理配置]** 然後按一下。
1. 檢查 **[!UICONTROL 在發佈時管理信函例項]** 設定，然後按一下 **[!UICONTROL 儲存]**.

### 啟用保存草稿功能 {#enable-save-draft-feature}

在發佈信函或在發佈執行個體上儲存草稿之前，請對製作和發佈執行個體執行下列步驟，以啟用「另存為草稿」功能：

此 *cq:lastReplicationAction*, *cq:lastreaded* 和 *cq:lastReplicatedBy* 依預設，屬性不會傳遞至發佈執行個體。 為了繼續 *cq:lastReplicationAction*, *cq:lastreaded* 和 *cq:lastReplicatedBy* 要發佈實例的屬性，禁用 [!UICONTROL com.day.cq.replication.impl.ReplicationPropertiesFilterFactory] 元件。 若要停用元件：

1. 在製作執行個體上，開啟Adobe Experience Manager Web主控台元件主控台。 預設URL為 `http://author-server:port/system/console/components`

1. 搜尋 **[!UICONTROL com.day.cq.replication.impl.ReplicationPropertiesFilterFactory]** 元件。

1. 按一下 ![「禁用」按鈕](/help/forms/using/assets/enablebutton.png) 表徵圖禁用 [!UICONTROL com.day.cq.replication.impl.ReplicationPropertiesFilterFactory] 元件。

![製作例項](/help/forms/using/assets/replicationproperties.png)

若要啟用另存為草稿功能，請取代現有URL，位於 [!UICONTROL VersionRestoreManager作者URL] 搭配您製作例項的URL。 若要取代URL:

1. 在發佈例項上，開啟 [!UICONTROL Adode Manager Web控制台配置]. 預設URL為 `https://publish-server:port/system/console/configMgr`

1. 搜尋並開啟 **[!UICONTROL 通信管理 — 製作執行個體版本還原設定]** 元件。

1. 找出 **[!UICONTROL VersionRestoreManager作者URL]** 欄位，並指定製作例項的URL。

1. 按一下「儲存」。

![發佈例項](/help/forms/using/assets/correspondencemanagement.png)

開啟信函例項的儲存時，您可以選擇要儲存信函例項的位置。 儲存字母例項有兩個選項：本地保存或遠程保存。

### 本機儲存 {#local-save}

信函例項會儲存在發佈例項上，並會在製作例項上反向複製。

### 遠程保存 {#remote-save}

對於在發佈執行個體上儲存使用者資料有疑慮的人，通常在公司防火牆之外會有此選項。 開啟遠端儲存時，信函例項不會儲存在發佈例項上，但會透過LiveCycle用戶端SDK設定，在指定的處理製作上遠端儲存。

#### 啟用遠程保存 {#enable-remote-save}

1. 在AEM中，使用下列URL開啟您伺服器的Adobe Experience Manager Web Console設定： `https://<server>:<port>/<contextpath>/system/console/configMgr`
1. 搜尋 **[!UICONTROL 通信管理配置]** 然後按一下。
1. 找出 **[!UICONTROL 遠程保存]** 設定，檢查，然後按一下 **[!UICONTROL 儲存]**.

#### 指定處理製作設定 {#specify-processing-author-settings}

1. 在AEM中，使用下列URL開啟您伺服器的Adobe Experience Manager Web Console設定： `https://<server>:<port>/system/console/configMgr`

   ![Adobe Experience Manager Web主控台設定](assets/2configmanager.png)

1. 在此頁面上，找出「AdobeLiveCycle用戶端SDK設定」 ，然後按一下以展開它。

1. 在處理伺服器URL中，輸入LiveCycle伺服器的名稱，提供登入資訊，然後按一下 **儲存**.

   ![輸入LiveCycle伺服器的名稱和登錄資訊](assets/3configmanager.png)

1. 如有必要，請設定您要用來存取伺服器的使用者名稱和密碼。

#### 附件傳送 {#attachmentdelivery}

* 信函附件是PDF中可用的後續處理，此後會在提交信函後建立。
* 使用伺服器端API以互動式或非互動式PDF呈現信函時，呈現的PDF會以PDF附件的形式包含附件。
* 使用「建立通信」用戶介面載入與信函模板關聯的後置進程，作為「提交」或「完成通信」操作的一部分時，附件作為「清單」傳遞&lt;com.adobe.idp.document> （在AttachmentDocs參數中）。
* 現成可用的傳送機制（例如電子郵件和列印）也會傳送附件，並PDF產生的通信。

## 信函預覽的轉譯模式：行動表單預覽和PDF預覽 {#rendition-modes-of-letter-preview-mobile-forms-preview-and-pdf-preview}

AEM Forms通信管理會在「建立通信UI」中將信函顯示為HTML。 不過，「通信管理」仍支援還原為PDF預覽，而非HTML預覽。 如需在預覽HTML和PDF模式之間切換的詳細資訊，請參閱 [更改信函的轉譯模式](#changerenditionmode).

以下是HTML和PDF預覽中可用的優點和功能。

**行動表單/HTML預覽的優點**

* **點選資料欄位值以反白標示對應的資料欄位**:在「建立通信」使用者介面中，您可以點選信函中的資料欄位值，以在「資料」索引標籤中反白顯示對應的資料欄位。 如需詳細資訊，請參閱 [輸入資料](#enterdata).

* **瀏覽器支援**:瀏覽器會逐漸撤回對NPAPI的支援，這會影響信函的PDF預覽。 HTML/行動表單信函預覽不受此影響。
* **反白標示信函中可編輯的內容**:在「建立通信」使用者介面中，您可以點選「反白標示可編輯內容」，以灰色反白標示信函中所有可編輯的內容。 如需詳細資訊，請參閱 [管理內容](#managecontent).

`<li>` `<li>Benefits of HTML preview  <ul>   <li>Right to left</li>   <li>NPAPI</li>   <li>Highlight Editable Content</li>  </ul> </li>` `<li>Benefits of PDF preview  <ul>   <li>Page Break</li>   <li>Final Preview</li>  </ul> </li>`
`<li>` `<li>Benefits of HTML preview  <ul>   <li>Right to left</li>   <li>NPAPI</li>   <li>Highlight Editable Content</li>  </ul> </li>` `<li>Benefits of PDF preview  <ul>   <li>Page Break</li>   <li>Final Preview</li>  </ul> </li>`  **PDF預覽的優點**

* **分頁符**:在PDF預覽中，您可以精確檢視信函中的分頁如何影響其輸出。
* **最終預覽**:在PDF預覽中，您可以檢視信函的確切格式和外觀，因為信函會出現在其輸出中。

如需PDF forms中指令碼支援的詳細資訊，請參閱 [指令碼支援](https://help.adobe.com/en_US/livecycle/11.0/ScriptingSupport/index.html).

如需HTML5表單中指令碼支援的詳細資訊，請參閱 [支援HTML5表單的指令碼](/help/forms/using/scripting-support.md).

### 更改信函的轉譯模式 {#changerenditionmode}

依預設，「建立通信UI」會使用HTML或行動表單來轉譯信函預覽。 行動表單預覽在任何瀏覽器中皆無問題，因為使用瀏覽器的原生外掛程式，且不需要其他外掛程式。 您可以將信函預覽模式變更為PDF。 不過，瀏覽器限制可能會針對信函互動式PDF預覽的不同功能產生問題。

如需瀏覽器與信函預覽相容性的詳細資訊，請參閱 [中止NPAPI瀏覽器外掛程式及其影響](https://helpx.adobe.com/aem-forms/kb/discontinuation-of-npapi-plugins-impact-on-aem-forms.html).

要更改信函的預覽模式，請完成以下步驟：

1. 前往 `https://[system]:'port'/system/console/configMgr` 並視需要以管理員身分登入。
1. 前往 **[!UICONTROL 通信管理配置]** > **[!UICONTROL 轉譯類型]** 選取 **HTML轉譯** （預設）或 **PDF轉譯**.
1. 按一下「**[!UICONTROL 儲存]**」。
