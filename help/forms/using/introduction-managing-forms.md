---
title: 管理表單簡介
description: AEM Forms提供管理最適化Forms和相關資產的工具。 本文向您介紹主要表單管理功能和使用者介面元素。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager, introduction
docset: aem65
exl-id: 3e063456-7f96-483d-86a3-6a414746db8a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1566'
ht-degree: 1%

---

# 管理表單簡介 {#introduction-to-managing-forms}

AEM [!DNL Forms]提供簡化但功能強大的使用者介面，以建立和管理表單、檔案、主題、信件、檔案片段、資料字典和相關資產。 它有助於管理表單、檔案和相關資產的完整生命週期 — 從開發人員的案頭到產品
它位於入口網站伺服器上，以供一般使用者使用。 您可以使用AEM [!DNL Forms]使用者介面來：

* 存取AEM [!DNL Forms]元件
* 存取AEM [!DNL Forms]設定

>[!NOTE]
>
>如需其他AEM工具和選項的詳細資訊，請參閱[製作](/help/sites-authoring/author.md)。

## 存取AEM Forms元件 {#access-aem-forms-components}

除了建立表單、檔案和相關資產的選項，AEM還提供建立網站、資產、管理AEM執行個體等選項。 您可以按一下![adobeexperiencemanager](assets/adobeexperiencemanager.png)Experience Manager標誌，以導覽至所有可用的工具。 除了其他元件主控台的連結，它還包含AEM [!DNL Forms]的連結。 若要導覽至AEM [!DNL Forms]，請按一下Experience Manager標誌![adobeexperiencemanager](assets/adobeexperiencemanager.png) >導覽![Compass](assets/compass.png) > **[!UICONTROL Forms]**。 下列主控台的連結隨即顯示：

* 表單與文件
* 主題
* 字母
* 文件片段
* 資料字典

  ![AEM Forms主控台](assets/aem_forms_console_new.png)

### 表單與文件  {#forms-documents}

Forms &amp; Documents提供建立互動式通訊、最適化表單、最適化表單片段和表單集的選項。 只有JEE上的AEM [!DNL Forms]，Forms &amp; Documents才提供從本機儲存匯入檔案的選項，並可將AEM [!DNL Forms]資產與Workbench同步。

建立按鈕是建立或上傳AEM [!DNL Forms]資產的程式起點。 它提供可建立的選項：

* **互動式通訊**：互動式通訊是一種個人化、互動式且適合裝置使用的HTML式數位通訊、陳述式或檔案。 互動式通訊本質上是回應式通訊，並根據使用者裝置和設定自動變更版面和設計。 如需詳細資訊，請參閱[互動式通訊概述](/help/forms/using/interactive-communications-overview.md)

* **最適化表單：**&#x200B;最適化表單是吸引人的回應式表單。 您可以根據使用者回應、裝置或工作環境，透過新增或移除表格區段，撰寫調適型表單以動態調整使用者的輸入。 [製作最適化表單簡介](../../forms/using/introduction-forms-authoring.md)文章提供最適化表單的詳細資訊。

* **最適化表單片段：**&#x200B;雖然每個表單都是針對特定目的而設計，但大多數表單中都有一些常見的區段，例如提供個人詳細資訊，例如姓名和地址、家庭詳細資訊、收入詳細資訊等。 您可以為此類區段建立個別資產。 這些可重複使用的獨立區段稱為自適應表單片段。 如需詳細資訊，請參閱[最適化表單片段](../../forms/using/adaptive-form-fragments.md)文章。

* **表單集：**&#x200B;表單集是分組在一起的HTML5表單集合，並以單一表單集呈現給一般使用者。 當使用者開始填寫表單集時，表單會順暢地從一個表單轉換為另一個表單。 最後，使用者只需按一下即可提交所有表單，作為單一實體。 如需詳細資訊，請參閱[AEM Forms中的表單集](../../forms/using/formset-in-aem-forms.md)。

* **資料夾：** AEM [!DNL Forms]使用者介面使用資料夾來排列資產。 它支援兩種型別的資料夾：

   * **一般資料夾：**&#x200B;這些資料夾用於在AEM [!DNL Forms]使用者介面中建立的資產。 這些資料夾沒有嚴格的資料夾結構。 您可以重新命名、建立子資料夾，並將最適化表單、互動式通訊、最適化表單片段、表單範本(XDP)、PDF forms、檔案和相關資產儲存在這些資料夾中。
   * **Forms Workflow資料夾：** Forms工作流程資料夾是在Workbench程式(LiveCycle封存)移轉並與AEM [!DNL Forms]使用者介面同步時建立的。 不允許重新命名、建立子資料夾、建立互動式通訊、最適化表單片段或互動式通訊。 也不允許刪除版本資料夾或建立及上傳最適化表單、最適化表單片段或與版本資料夾同時進行的互動式通訊。

  ![資料夾](assets/folders.png)

  **A.**&#x200B;一般資料夾&#x200B;**B.** Forms Workflow資料夾

Forms和「檔案」面板也提供以下選項：

* **從本機儲存匯入檔案：**&#x200B;您可以匯入PDF forms和檔案、表單範本（XFA表單）及其他資源（XSD的影像和XML結構描述）。 如需逐步指示，請參閱[匯入和匯出資產至AEM Forms](../../forms/using/import-export-forms-templates.md)。
* **與Workbench同步AEM Forms資產：**&#x200B;您可以使用「來自Workbench的檔案」選項，在AEM Forms使用者介面與Workbench之間同步資產。 這可確保所有資產都可在AEM [!DNL Forms]使用者介面和Workbench的crx存放庫資產選擇中使用。

### 主題  {#themes}

主題包含元件和面板的樣式詳細資訊。 主題具有獨立的身分。 因此，您可以在多個最適化表單上重複使用主題。 您可以指定元件的樣式，或修改表單上使用的各種元件的CSS屬性。 樣式包含諸如背景顏色、狀態顏色、透明度及大小等屬性。 您可以將自訂內容儲存在主題中，並將其作為預設集移植到表單的元件上。 將主題新增至表單時，指定的樣式會反映在表單的對應元件上。 使用AEM 6.2 [!DNL Forms]，您可以建立主題並將其套用至您的表單。

如需有關建立和使用主題的資訊，請參閱[AEM Forms中的主題](../../forms/using/themes.md)。

### 字母  {#letters}

AEM [!DNL Forms]信函是安全、個人化和互動式通訊。 您可以使用AEM [!DNL Forms]，透過簡化的程式，從預先核准和自訂撰寫的內容快速組合字母（也稱為對應）。

如需建立及使用字母的詳細資訊，請參閱[建立字母](../../forms/using/create-letter.md)。

### 文件片段 {#document-fragments}

檔案片段是可重複使用的對應部分或元件，您可以使用這些部分或元件來撰寫信件。 檔案片段的型別為文字、清單、條件和佈局片段。 如需有關建立和使用檔案片段的資訊，請參閱[建立檔案片段](/help/forms/using/document-fragments.md)。

### 資料字典 {#data-dictionaries}

一般來說，業務使用者不需要瞭解中繼資料表示法，例如XSD （XML架構）和Java類別。 但是，它們通常需要存取這些資料結構和屬性才能建置解決方案。 AEM [!DNL Forms]使用資料字典，讓商務使用者能夠使用來自後端資料來源的資訊，而不需要知道其基礎資料模型的技術細節。

如需建立及使用資料字典的詳細資訊，請參閱建立[資料字典文章](../../forms/using/data-dictionary.md)

## 存取AEM [!DNL Forms]設定 {#accessing-aem-forms-configurations}

「AEM工具」面板包含各種元件的工具。 若要瀏覽至AEM Forms專用工具，請按一下Experience Manager標誌![adobeexperiencemanager](assets/adobeexperiencemanager.png) >工具![hammer](assets/hammer.png) > **[!UICONTROL Forms]**。 會顯示執行下列功能的工具：

* **設定Watched資料夾：**&#x200B;系統管理員可以設定網路資料夾，稱為watched資料夾，這樣當使用者將檔案(例如PDF檔案)放入watched資料夾時，就會啟動預先設定的作業並操作檔案。 如需詳細資訊，請參閱[建立並設定watched資料夾](/help/forms/using/creating-configure-watched-folder.md)。
* **設定Forms App離線服務：** AEM [!DNL Forms] App離線服務會快取表單中所使用資源的路徑或URL。 快取表單中使用的資源的路徑或URL可改善伺服器端效能。 若要設定AEM Forms應用程式的伺服器端離線元件，請參閱[在離線模式下工作](/help/forms/using/work-offline-mode.md)。

  ![AEM Forms工具](assets/aem_forms_tools_new.png)

* **設定PDF Generator：**&#x200B;管理員可以設定AEM [!DNL Forms]PDF Generator設定、新增使用者帳戶，以及將設定匯入或匯出至PDF Generator。
* **Publish Correspondence Management Assets：** AEM [!DNL Forms]可讓您一次從製作執行個體發佈所有信件、檔案片段和資料字典以及相關相依性。 發佈的資產包含所有「對應管理」資產和相關相依性。 如需詳細資訊，請參閱[發佈與取消發佈表單與檔案](../../forms/using/publishing-unpublishing-forms.md#publishallthecorrespondencemanagementassets)。
* **匯出通訊管理Assets：**&#x200B;您可以從AEM [!DNL Forms]執行個體將所有Correspondence Management資產和相關相依性下載為套件。 如需詳細步驟，請參閱[匯入和匯出資產至AEM Forms](../../forms/using/import-export-forms-templates.md#importandexportassetsincorrespondencemanagement)

## 使用者介面的通用元素 {#commonelements}

* **左側邊欄：**&#x200B;您可以按一下左側邊欄圖示![railleftpng](assets/railleftpng.png)，以顯示AEM [!DNL Forms]的時間軸和參考功能。

   * **時間表：**&#x200B;您可以在時間表中可供檢閱的資產上新增並檢視註解。 如需詳細指示，請參閱[建立和管理表單中資產的稽核](../../forms/using/create-reviews-forms.md)。
   * **參考：** AEM [!DNL Forms]資產可用於多個AEM [!DNL Forms]資產。 例如，檔案片段可用於多個字母。 參考是所選資產使用的資產（其他表單或資源）清單，也是所選資產正在使用的其他資產清單。

* **階層連結：**&#x200B;階層連結代表目前主控台或資料夾的標題。 您可以按一下「階層連結」選項，在階層中較高的資料夾層級之間導覽。
* **檢視切換器：**&#x200B;您可以按一下[檢視切換器]圖示![檢視清單](assets/viewlist.png)或![檢視卡](assets/viewcard.png)，在清單和卡片檢視之間快速切換。 如需一般使用者介面元件的詳細資訊，請參閱[製作](/help/sites-authoring/author.md)。
* **搜尋：**&#x200B;搜尋選項![搜尋](assets/search.png)提供快速尋找及跳至您所需內容與工具的功能。 輸入內容或產品功能的名稱，然後從建議中選取，例如，輸入「Documents」以快速尋找並導覽至&#x200B;**[!UICONTROL Forms和檔案]**&#x200B;或檔案片段主控台。 如需搜尋的詳細資訊，請參閱AEM 6.2 [搜尋](/help/sites-authoring/search.md)文章

* **動作工具列**：選取資產時，動作工具列會出現在資產清單上方。 它包含所選資產的所有管理工具。 您可以將滑鼠停留在工具圖示上，即可檢視描述其功能的工具提示

>[!NOTE]
>
>當使用者執行搜尋Forms和檔案的任何主控台時，邊欄僅包含&#x200B;**篩選器和選項**。 您可以使用「篩選和選項」來執行進階搜尋。

* **動作工具列**：選取資產時，動作工具列會出現在資產清單上方。 它包含所選資產的所有管理工具。 您可以將滑鼠停留在工具圖示上，即可檢視描述其功能的工具提示

  最適化表單的![動作工具列](assets/action_toolbar_new.png)

  最適化表單的動作工具列
