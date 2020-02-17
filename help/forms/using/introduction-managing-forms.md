---
title: 管理表單簡介
seo-title: 管理表單簡介
description: AEM Forms提供管理Adaptive Forms和相關資產的工具。 本文將向您介紹關鍵表單管理功能和用戶介面元素。
seo-description: AEM Forms提供管理Adaptive Forms和相關資產的工具。 本文將向您介紹關鍵表單管理功能和用戶介面元素。
uuid: 2275a0b6-b31e-4d8e-8154-ccdfff3705aa
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction
discoiquuid: c0e4c9bb-e12a-4f9a-a8fa-1a8ad41d3995
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931

---


# 管理表單簡介{#introduction-to-managing-forms}

AEM Forms提供簡化但功能強大的使用者介面，以建立和管理表單、檔案、主題、字母、檔案片段、資料字典和相關資產。 它可協助管理表單、檔案和相關資產的完整生命週期——從開發人員的案頭，到在入口伺服器上提供給使用者。 您可以使用AEM Forms使用者介面來：

* 存取AEM Forms元件
* 存取AEM Forms設定

>[!NOTE]
>
>如需其他AEM工具和選項的詳細資訊，請參閱「編 [寫」](/help/sites-authoring/author.md)。

## 存取AEM Forms元件 {#access-aem-forms-components}

AEM除了提供建立表單、檔案和相關資產的選項外，還提供建立網站、資產、管理AEM例項等選項。 您可以按一下 ![adobeexperiencemanager](assets/adobeexperiencemanager.png) Experience Manager標誌，導覽至所有可用的工具。 除了其他元件的主控台連結外，它還包含AEM Forms的連結。 若要導覽至AEM Forms，請按一下Experience Manager logo ![adobeexperiencemanager](assets/adobeexperiencemanager.png) >導覽 ![指南](assets/compass.png) > Forms。 將顯示以下控制台的連結：

* 表單與文件
* 主題
* 字母
* 文件片段
* 資料字典

![AEM Forms Console](assets/aem_forms_console_new.png)

### 表單與文件  {#forms-documents}

「表單與檔案」提供建立互動式通訊、最適化表單、最適化表單片段和表單集的選項。 Forms &amp; Documents僅針對JEE上的AEM Forms，提供從本機儲存匯入檔案並與Workbench同步AEM Forms資產的選項。

「建立」按鈕是建立或上傳AEM Forms資產的程式起點。 它提供您建立以下項目的選項：

* **互動式通訊**:互動式通訊是個人化、互動式和裝置友好型的HTML數位通訊、陳述式或檔案。 互動式通訊在本質上是互動式的，並會根據使用者裝置和設定自動變更版面和設計。 如需詳細資訊，請參閱互動 [式通訊概觀](/help/forms/using/interactive-communications-overview.md)

* **** 最適化表單：最適化表單是引人入勝且回應速度快的表單。 您可以根據使用者回應、裝置或工作環境，新增或移除表單區段，以自適應表單，以動態地配合使用者輸入。 製作 [最適化表單簡介](../../forms/using/introduction-forms-authoring.md) ，提供最適化表單的詳細資訊。

* **** 最適化表單片段：雖然每個表單都是專為特定用途而設計，但大部分表單中都有一些常見的區段，例如提供個人詳細資料，例如姓名和地址、家庭詳細資料、收入詳細資料等。 您可以為這些區段建立個別資產。 這些可重複使用、可獨立執行的區段稱為可調式表單片段。 如需詳細資訊，請參閱 [最適化表單片段](../../forms/using/adaptive-form-fragments.md) 文章。

* **** 表單集：表單集是HTML5表單的集合，分組在一起，並以單一表單集的形式呈現給使用者。 當使用者開始填寫表格集時，表格會從一個表格順暢地轉換為另一個表格。 最後，使用者只需按一下，即可將所有表格以單一實體的形式提交。 如需詳細資訊，請參 [閱「AEM Forms中的表單集」](../../forms/using/formset-in-aem-forms.md)。

* **** 資料夾：AEM Forms使用者介面使用資料夾來排列資產。 它支援兩種類型的資料夾：

   * **** 一般資料夾：這些檔案夾用於在AEM Forms使用者介面中建立的資產。 這些資料夾沒有嚴格的資料夾結構。 您可以重新命名、建立子檔案夾，並將最適化表單、互動式通訊、最適化表單片段、表單範本(XDP)、PDF表單、檔案和相關資產儲存在這些檔案夾中。
   * **** Forms Workflow folder:當Workbench進程（LiveCycle封存）移轉並與AEM Forms使用者介面同步時，會建立表單工作流程資料夾。 它不允許更名、建立子資料夾、建立交互通信、自適應表單片段或交互通信。 也不允許刪除版本資料夾，或建立和上傳與版本資料夾平行的最適化表單、最適化表單片段或互動式通訊。

![資料夾](assets/folders.png)

******答：一般資料**&#x200B;夾B.Forms Workflow資料夾

「表單與檔案」面板也提供下列選項：

* **** 從本機儲存區匯入檔案：您可以匯入PDF表單與檔案、表單範本（XFA表單）和其他資源（XSD的影像與XML架構）。 如需逐步指示，請參閱「匯入 [資產並匯出至AEM Forms」](../../forms/using/import-export-forms-templates.md)。
* **** 將AEM Forms資產與Workbench同步：您可以使用「從工作台檔案」選項，在AEM Forms使用者介面和Workbench之間同步資產。 它可確保AEM Forms使用者介面和Workbench的crx-repository資產選擇中提供所有資產。

### 主題  {#themes}

主題包含元件和面板的樣式詳細資訊。 主題具有獨立身份。 因此，您可以在多個調適性表單上重複使用主題。 您可以指定元件的樣式，或修改表單中各種元件的CSS屬性。 樣式包括背景顏色、狀態顏色、透明度和大小等屬性。 您可以將自訂項目儲存在主題中，並將它們移植到表單的元件上做為預設集。 當您將主題新增至表格時，指定的樣式會反映在表格的對應元件上。 有了AEM 6.2 Forms，您就可以建立主題並將它們套用至表單。

如需有關建立和使用主題的詳細資訊，請參 [閱「AEM Forms中的主題」](../../forms/using/themes.md)。

### 字母  {#letters}

AEM表格信函是安全、個人化和互動式的信件往來。 您可以使用AEM Forms，以簡化的程式，從預先核准和自訂製作的內容快速組合字母（也稱為通訊）。

有關建立和使用字母的資訊，請參 [閱建立字母](../../forms/using/create-letter.md)。

### 文件片段 {#document-fragments}

檔案片段是可重複使用的部分或元件，用於合成字母。 檔案片段為文字、清單、條件和版面片段類型。 如需建立和使用檔案片段的詳細資訊，請參 [閱建立檔案片段](/help/forms/using/document-fragments.md)。

### 資料字典 {#data-dictionaries}

一般而言，商業使用者不需要具備中繼資料表示法的知識，例如XSD（XML架構）和Java類別。 但是，通常需要訪問這些資料結構和屬性才能構建解決方案。 AEM Forms使用資料字典，讓商業使用者使用後端資料來源的資訊，而不需瞭解其基礎資料模型的技術詳細資訊。

如需建立和使用資料字典的詳細資訊，請參閱建立 [資料字典文章](../../forms/using/data-dictionary.md)

## 存取AEM Forms設定 {#accessing-aem-forms-configurations}

AEM工具面板包含各種元件的工具。 若要導覽至AEM Forms專用工具，請按一下Experience Manager logo ![adobeexperiencemanager](assets/adobeexperiencemanager.png) >工具 ![槌子](assets/hammer.png) > Forms。 將顯示用於執行下列功能的工具：

* **** 配置監視資料夾：管理員可以配置網路資料夾（稱為監視資料夾），以便當用戶將檔案（如PDF檔案）放置到監視資料夾時，啟動預配置的操作並操作該檔案。 如需詳細資訊，請參 [閱建立和設定受監視的資料夾](/help/forms/using/creating-configure-watched-folder.md)。
* **** 設定Forms App Offline Service:AEM Forms應用程式離線服務會快取表單中使用之資源的路徑或URL。 快取表單中使用之資源的路徑或URL可改善伺服器端效能。 若要設定AEM Forms應用程式的伺服器端離線元件，請參 [閱「在離線模式中工作」](/help/forms/using/work-offline-mode.md)。

![AEM Forms工具](assets/aem_forms_tools_new.png)

* **** 設定PDF產生器：管理員可以設定AEM Forms PDF Generator設定、新增使用者帳戶，以及將設定匯入或匯出至PDF Generator。
* **** 發佈對應管理資產：AEM Forms可讓您一次從作者例項發佈所有字母、檔案片段和資料字典及相關相依性。 發佈的資產包括所有Correponsement Management資產和相關依存關係。 如需詳細資訊，請參 [閱發佈和取消發佈表單與檔案](../../forms/using/publishing-unpublishing-forms.md#publishallthecorrespondencemanagementassets)。
* **** 匯出對應管理資產：您可以從AEM表單例項，以套件形式下載所有Correponsent Management資產和相關相依性。 如需詳細步驟，請參 [閱匯入和匯出資產至AEM Forms](../../forms/using/import-export-forms-templates.md#importandexportassetsincorrespondencemanagement)

## 使用者介面的常見元素 {#commonelements}

* **** 左側欄：您可以按一下左側導軌圖示 ![導軌左側](assets/railleftpng.png) ，以顯示AEM Forms的「時間軸」和「參照」功能。

   * **** 時間軸：您可以新增及檢視可在時間軸中檢視之資產的註解。 如需詳細指示，請參 [閱建立和管理表單中資產的審核](../../forms/using/create-reviews-forms.md)。
   * **** 參考：AEM Forms資產可用於多個AEM Forms資產。 例如，檔案片段可用於多個字母。 參考是指所選資產所使用的資產（其他表單或資源）清單，也是所選資產所使用的其他資產清單。

* **** 麵包屑：Breadcrumb代表目前主控台或資料夾的標題。 您可以按一下「階層連結」選項，在階層中較高的檔案夾層級之間導覽。
* **** 檢視切換器：您可以按一下「檢視切換器」圖示 ![檢視清單](assets/viewlist.png) ，或 ![檢視卡](assets/viewcard.png) ，快速在清單和資訊卡檢視之間切換。 如需一般使用者介面元件的詳細資訊，請參 [閱編寫](/help/sites-authoring/author.md)。
* **** 搜尋：搜尋選項 ![搜尋](assets/search.png) ，可讓您快速尋找並跳至所需的內容和工具。 輸入內容名稱或產品功能並從建議中選擇，例如，輸入「檔案」以快速尋找並導覽至「表單與檔案」或「檔案片段」主控台。 如需搜尋的詳細資訊，請參閱AEM 6.2搜 [尋文章](/help/sites-authoring/search.md)

* **動作工具列**:在選取資產時，動作工具列會顯示在資產清單的上方。 它包含所選資產的所有管理工具。 您可以將滑鼠指標暫留在工具圖示上，以檢視說明其功能的工具提示

>[!NOTE]
>
>當使用者執行任何「表單與檔案」控制台的搜尋時，邊欄僅包含「篩 **選器與選項」**。 您可以使用「篩選與選項」來執行進階搜尋。

* **動作工具列**:在選取資產時，動作工具列會顯示在資產清單的上方。 它包含所選資產的所有管理工具。 您可以將滑鼠指標暫留在工具圖示上，以檢視說明其功能的工具提示

![最適化表單的動作工具列](assets/action_toolbar_new.png)

最適化表單的動作工具列

