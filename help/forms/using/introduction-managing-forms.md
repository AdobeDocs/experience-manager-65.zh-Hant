---
title: 管理表單簡介
seo-title: 管理表單簡介
description: AEM Forms提供管理適用性Forms和相關資產的工具。 本文會介紹重要的表單管理功能和使用者介面元素。
seo-description: AEM Forms提供管理適用性Forms和相關資產的工具。 本文會介紹重要的表單管理功能和使用者介面元素。
uuid: 2275a0b6-b31e-4d8e-8154-ccdfff3705aa
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager, introduction
discoiquuid: c0e4c9bb-e12a-4f9a-a8fa-1a8ad41d3995
docset: aem65
exl-id: 3e063456-7f96-483d-86a3-6a414746db8a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1593'
ht-degree: 1%

---

# 管理表單簡介{#introduction-to-managing-forms}

AEM [!DNL Forms]提供簡化而功能強大的使用者介面，可建立及管理表單、檔案、主題、信函、檔案片段、資料字典和相關資產。 它有助於管理表單、檔案和相關資產的完整生命週期 — 從開發人員的案頭到產品
在入口伺服器上為最終用戶提供。 您可以使用AEM [!DNL Forms]使用者介面來執行下列動作：

* 存取AEM [!DNL Forms]元件
* 訪問AEM [!DNL Forms]配置

>[!NOTE]
>
>如需其他AEM工具和選項的詳細資訊，請參閱[Authoring](/help/sites-authoring/author.md)。

## 存取AEM Forms元件{#access-aem-forms-components}

除了建立表單、檔案和相關資產的選項之外，AEM還提供建立網站、資產、管理AEM例項等選項。 您可以按一下![adobeexperiencemanager](assets/adobeexperiencemanager.png)Experience Manager標誌，導覽至所有可用的工具。 此外，它還包含AEM [!DNL Forms]的連結，以及其他元件控制台的連結。 若要導覽至AEM [!DNL Forms]，請按一下Experience Manager標誌![adobeexperiencemanager](assets/adobeexperiencemanager.png) >導覽![compass](assets/compass.png) > **[!UICONTROL Forms]**。 畫面上會顯示下列主控台的連結：

* 表單與文件
* 主題
* 字母
* 文件片段
* 資料字典

   ![AEM Forms Console](assets/aem_forms_console_new.png)

### 表單與文件  {#forms-documents}

Forms與檔案提供建立互動式通訊、最適化表單、最適化表單片段和表單集的選項。 僅適用於JEE上的AEM [!DNL Forms],Forms與檔案提供從本機儲存匯入檔案，以及使用Workbench同步AEM [!DNL Forms]資產的選項。

「建立」按鈕是建立或上傳AEM [!DNL Forms]資產的程式起點。 它提供建立的選項：

* **互動式通訊**:互動式通訊是個人化、互動式且適合裝置的HTML數位通信、陳述或檔案。互動式通訊具有回應性，且會根據使用者裝置和設定自動變更版面和設計。 有關詳細資訊，請參閱[互動式通信概述](/help/forms/using/interactive-communications-overview.md)

* **適用性表單：** 適用性表單是吸引人且回應式的表單。您可以根據使用者回應、裝置或工作環境，新增或移除表單區段，以動態調整以適應使用者輸入。 [製作最適化表單簡介](../../forms/using/introduction-forms-authoring.md)文章提供最適化表單的詳細資訊。

* **最適化表單片段：** 雖然每個表單都是針對特定用途而設計，但大部分表單中都有一些常見的區段，例如提供個人詳細資訊，例如姓名和地址、家庭詳細資訊、收入詳細資訊等。您可以為這類區段建立個別資產。 這些可重複使用的獨立區段稱為最適化表單片段。 如需詳細資訊，請參閱[最適化表單片段](../../forms/using/adaptive-form-fragments.md)文章。

* **表單集：** 表單集是將HTML5表單分組在一起，並以單一表單集呈現給使用者的集合。當最終用戶開始填寫表單集時，表單將從一個表單無縫轉換到另一個表單。 最後，使用者只需按一下，即可以以單一實體提交所有表單。 如需詳細資訊，請參閱[AEM Forms中設定的表單](../../forms/using/formset-in-aem-forms.md)。

* **資料夾：** AEM [!DNL Forms] 使用者介面使用資料夾來排列資產。它支援兩種類型的資料夾：

   * **一般資料夾：** 這些資料夾用於在AEM使用者介面中建 [!DNL Forms] 立的資產。這些資料夾沒有嚴格的資料夾結構。 您可以重新命名、建立子檔案夾，以及儲存這些資料夾中的最適化表單、互動式通訊、最適化表單片段、表單範本(XDP)、PDF forms、檔案和相關資產。
   * **Forms Workflow資料夾：** 當Workbench程式(LiveCycle封存檔)移轉並與AEM使用者介面同步時，會建立Forms工作 [!DNL Forms] 流程資料夾。不得重新命名、建立子資料夾、建立互動式通訊、最適化表單片段或互動式通訊。 此外，您也無法刪除版本資料夾，或建立及上傳最適化表單、最適化表單片段或與版本資料夾平行的互動式通訊。

   ![資料夾](assets/folders.png)

   **A.一** 般資料 **夾B.** Forms Workflow資料夾

「Forms」和「檔案」面板也提供下列選項：

* **從本機儲存匯入檔案：** 您可以匯入PDF forms與檔案、表單範本（XFA表單）和其他資源（XSD的影像和XML結構）。如需逐步指示，請參閱[匯入資產並匯出至AEM Forms](../../forms/using/import-export-forms-templates.md)。
* **將AEM Forms資產與Workbench同步：** 您可以使用「來自Workbench的檔案」選項，將AEM Forms使用者介面與Workbench之間的資產同步。它可確保AEM [!DNL Forms]使用者介面和Workbench的crx-repository資產選取項目中提供所有資產。

### 主題  {#themes}

主題包含元件和面板的樣式詳細資料。 主題具有獨立身份。 因此，您可以在多個最適化表單上重複使用主題。 您可以指定元件的樣式，或修改表單中所使用各種元件的CSS屬性。 樣式包括背景顏色、狀態顏色、透明度和大小等屬性。 您可以將自訂項目儲存在主題中，並將它們連接到表單的元件上作為預設集。 將主題添加到表單時，指定的樣式會反映在表單的相應元件上。 使用AEM 6.2 [!DNL Forms]，您可以建立主題並將其套用至您的表單。

有關建立和使用主題的資訊，請參閱AEM Forms中的[主題](../../forms/using/themes.md)。

### 字母  {#letters}

AEM [!DNL Forms]信函是安全、個人化和互動式通信。 您可以透過簡化的程式，使用AEM [!DNL Forms]，從預先核准和自訂撰寫的內容快速組合字母（也稱為對應）。

有關建立和使用字母的資訊，請參閱[建立字母](../../forms/using/create-letter.md)。

### 文件片段 {#document-fragments}

檔案片段是可重複使用的通信部分或元件，您可使用這些元件來撰寫信函。 文檔片段的類型為文本、清單、條件和佈局片段。 有關建立和使用文檔片段的資訊，請參閱[建立文檔片段](/help/forms/using/document-fragments.md)。

### 資料字典 {#data-dictionaries}

通常，業務用戶不需要XSD（XML架構）和Java類等元資料表示的知識。 但是，通常需要存取這些資料結構和屬性才能建立解決方案。 AEM [!DNL Forms]使用資料字典，讓商務使用者無需了解其基礎資料模型的技術詳細資訊，即可使用後端資料來源的資訊。

有關建立和使用資料字典的資訊，請參閱建立[資料字典文章](../../forms/using/data-dictionary.md)

## 存取AEM [!DNL Forms]設定{#accessing-aem-forms-configurations}

AEM工具面板包含各種元件的工具。 若要導覽至AEM Forms專用工具，請按一下Experience Manager標誌![adobeexperiencemanager](assets/adobeexperiencemanager.png) > tools ![hammer](assets/hammer.png) > **[!UICONTROL Forms]**。 將顯示用於執行以下功能的工具：

* **設定觀看資料夾：** 管理員可設定網路資料夾（稱為觀看資料夾），以便當使用者將檔案（例如PDF檔案）置於觀看資料夾時，會啟動預先設定的操作並操作檔案。如需詳細資訊，請參閱[建立和設定已觀看的資料夾](/help/forms/using/creating-configure-watched-folder.md)。
* **設定Forms應用程式離線服務：** AEM [!DNL Forms] 應用程式離線服務會快取表單中所用資源的路徑或URL。快取表單中所使用資源的路徑或URL可改善伺服器端效能。 若要設定AEM Forms應用程式的伺服器端離線元件，請參閱[在離線模式下工作](/help/forms/using/work-offline-mode.md)。

   ![AEM Forms工具](assets/aem_forms_tools_new.png)

* **設定PDF產生器：** 管理員可以設定AEM  [!DNL Forms] PDF產生器設定、新增使用者帳戶，以及將設定匯入或匯出至PDF產生器。
* **發佈通信管理資產：** AEM [!DNL Forms] 可讓您一次從製作例項發佈所有信函、檔案片段、資料字典和相關相依性。已發佈的資產包含所有通信管理資產和相關相依性。 如需詳細資訊，請參閱[發佈和取消發佈表單與檔案](../../forms/using/publishing-unpublishing-forms.md#publishallthecorrespondencemanagementassets)。
* **匯出通信管理資產：** 您可以從AEM例項以套件形式下載所有通信管理資產和相關相依 [!DNL Forms] 性。如需詳細步驟，請參閱[匯入資產並匯出至AEM Forms](../../forms/using/import-export-forms-templates.md#importandexportassetsincorrespondencemanagement)

## 使用者介面的常見元素 {#commonelements}

* **左側邊欄：** 您可以按一下左側邊欄圖示，左側邊欄 ![](assets/railleftpng.png) 會顯示AEM的「時間軸」和「參照」 [!DNL Forms]功能。

   * **時間軸：** 您可以新增及檢視可在時間軸中檢閱的資產之註解。如需詳細指示，請參閱[建立和管理表單中資產的審核。](../../forms/using/create-reviews-forms.md)
   * **參考：** AEM [!DNL Forms] 資產可用於多個AEM [!DNL Forms] 資產。例如，文檔片段可以用於多個字母。 參考是指所選資產用於的資產清單（其他表單或資源），以及所選資產正在使用的其他資產清單。

* **階層連結：** 階層連結代表目前主控台或資料夾的標題。您可以按一下階層連結選項，在階層中較高的資料夾層級之間導覽。
* **檢視切換器：** 您可以按一下檢視切換器圖示檢視 ![](assets/viewlist.png) 器 ![](assets/viewcard.png) 檢視卡，以快速在清單與卡片檢視之間切換。有關常用用戶介面元件的詳細資訊，請參閱[創作](/help/sites-authoring/author.md)。
* **搜尋：** 搜尋選項 ![](assets/search.png) search提供快速尋找及跳至您所需內容和工具的功能。輸入內容或產品功能的名稱，然後從建議中選取，例如，輸入「Documents」以快速尋找並導覽至&#x200B;**[!UICONTROL Forms與檔案]**&#x200B;或檔案片段主控台。 如需搜尋的詳細資訊，請參閱AEM 6.2 [search](/help/sites-authoring/search.md)文章

* **動作工具列**:選取資產時，動作工具列會顯示在資產清單上方。它包含所選資產的所有管理工具。 您可以將滑鼠移至工具圖示上，檢視說明其功能的工具提示

>[!NOTE]
>
>當使用者執行Forms與檔案的任何主控台搜尋時，邊欄僅包含&#x200B;**篩選器與選項**。 您可以使用「篩選器與選項」來執行進階搜尋。

* **動作工具列**:選取資產時，動作工具列會顯示在資產清單上方。它包含所選資產的所有管理工具。 您可以將滑鼠移至工具圖示上，檢視說明其功能的工具提示

   ![最適化表單的動作工具列](assets/action_toolbar_new.png)

   最適化表單的動作工具列
