---
title: 匯入和匯出資產至AEM Forms
seo-title: Importing and exporting assets to AEM Forms
description: 您可以從AEM例項匯入和匯出最適化表單和範本。 這有助於移轉表單或跨系統移動表單。
seo-description: You can import and export adaptive forms and templates from and in to AEM instances. This helps in migrating forms or moving them across systems.
uuid: 937daedd-56f3-4e02-b695-b194b494d9bf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 69210727-dde3-495a-87b7-2e8173e6b664
docset: aem65
role: Admin
exl-id: b5f6a54e-92d1-4631-a1d1-184f37d174b6
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '2516'
ht-degree: 0%

---

# 匯入和匯出資產至AEM Forms{#importing-and-exporting-assets-to-aem-forms}

您可以在不同的AEM Forms例項之間移動表單和相關資產、主題、資料字典、檔案片段和字母。 在遷移系統或將表單從預備伺服器移動到生產伺服器時，需要進行這樣的移動。 若為支援透過AEM Forms UI上傳和匯入的資產，建議使用Forms UI進行匯出或匯入。 不建議使用AEM Package Manager匯出或匯入這類資產。

>[!NOTE]
>
>* 在AEM 6.4 Forms中，crx-repository的結構和路徑已變更。 如果您將舊版資產匯入AEM 6.4 Forms，而表單對舊結構有某些相依性，則必須手動匯出相依性。 如需存放庫結構和路徑變更的詳細資訊，請參閱 [AEM中的存放庫重新調整](/help/sites-deploying/repository-restructuring.md).
>


## 下載或上傳Forms和檔案資產 {#download-or-upload-forms-amp-documents-assets}

AEM Forms使用者介面可讓您以AEM CRX套件或二進位檔案的形式下載資產，以從AEM執行個體匯出資產。 然後，您可以將下載的AEM CRX套件或二進位檔案匯入另一個AEM例項。

除了「適用性表單範本」和「適用性表單」內容原則外，所有資產都支援透過AEM Forms使用者介面匯出和匯入。 因此，從AEM Forms UI匯出最適化表單時，相關的最適化表單範本和內容原則不會像其他相關資產一樣自動匯出。

對於這些資產類型，您必須使用AEM Package Manager在來源AEM伺服器上建立CRX套件，並在目標伺服器上安裝套件。 有關建立和安裝軟體包的資訊，請參閱 [使用套件](/help/sites-administering/package-manager.md).

### 下載Forms和檔案資產 {#download-forms-amp-documents-assets}

若要下載Forms和檔案資產：

1. 登入AEM Forms例項。
1. 點選Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 圖示>導覽 ![羅盤](assets/compass.png) 圖示> Forms > Forms與檔案。
1. 選取表單資產，然後點選 **下載** 表徵圖。
1. 在「下載資產」中，選擇下列其中一個選項，然後點選 **下載**.

   * **下載為CRX套件：** 使用選項，將所有選取的資產和相關相依性從AEM Forms例項下載並移至其他例項。 它會以crx套件下載所有資產和資料夾。 任何表單資產，包括以AEM製作的表單（最適化表單、互動式通訊和最適化表單片段）、表單集、表單範本、PDF檔案和資源（XSD、XFS、影像），都可從AEM Forms UI以套件形式下載。
以套件形式下載資產的好處，在於也會下載被選取下載的資產所使用的資產。 例如，如果您的適用性表單使用表單範本XSD和影像。 選取此最適化表單並以套件形式下載時，下載的套件也會包含表單範本、XSD和影像。 也會下載與資產相關聯的所有中繼資料屬性（包括自訂屬性）。

   * **以二進位檔案形式下載資產：** 使用選項僅下載表單模板(XDP)、PDF forms(PDF)、文檔(PDF)和資源（影像、結構、樣式表）。 您可以使用外部應用程式編輯這些資產。 它會以.zip檔案的形式下載含有二進位檔的表單資產，例如XSD、XDP、影像、PDF和XDP。
您無法下載最適化表單、互動式通訊、最適化表單片段、主題和表單集，具有 **以二進位檔案形式下載資產** 選項。 若要下載這些資產，您應使用 **下載為CRX套件** 選項。

   選取的資產會以封存檔（.zip檔案）的形式下載。

   >[!NOTE]
   >
   >AEM套件和二進位檔案都會以封存檔（.zip檔案）的形式下載。 系統不會隨資產下載資產的範本。 您需要個別匯出資產範本。

### 上傳Forms和檔案資產 {#upload-forms-amp-documents-assets}

上傳Forms和檔案資產：

>[!VIDEO](https://vimeo.com/)

1. 登入AEM Forms例項。
1. 點選Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 圖示>導覽 ![羅盤](assets/compass.png) 圖示> Forms> Forms與檔案。
1. 點選 **建立** >**檔案上傳**. 上傳表單或套件對話方塊隨即顯示。
1. 在對話方塊中，瀏覽並選取要匯入的套件或封存。 您也可以選擇PDF文檔、XSD、影像、樣式表和XDP表單。 點選 **開啟**. 所選資料夾或檔案名稱不得包含任何特殊字元。

   在對話方塊中，驗證要上傳之資產的詳細資訊，然後點選 **上傳**.

   如果您上傳現有的表單資產，資產便會更新。

   >[!NOTE]
   >
   >上傳套件不會取代現有的資料夾階層。 例如，如果您有一個名為「培訓」的最適化表單，位置為/content/dam/formsanddocuments ，位於一台伺服器上。 您可以下載最適化表單，然後在其他伺服器上傳表單。 第二台伺服器的相同位置/content/dam/formsanddocuments也有一個名為「Training」的資料夾。 上傳失敗。

## 下載或上傳主題 {#downloading-or-uploading-a-theme}

使用AEM Forms，您可以建立、下載或上傳主題。 主題的建立方式與其他資產（如表單、檔案和信函）相同。 您可以建立主題、下載主題，然後將其上傳至個別例項以重複使用。 如需主題的詳細資訊，請參閱 [AEM Forms主題](../../forms/using/themes.md).

### 下載主題 {#downloading-a-theme}

您可以匯出AEM Forms中可用於其他專案或例項的主題。 AEM可讓您以zip檔案的形式下載主題，以便上傳至執行個體。

若要下載主題：

1. 登入AEM Forms例項。
1. 點選Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 圖示>導覽 ![羅盤](assets/compass.png) 表徵圖> Forms>主題。
1. 選取主題並點選 **下載**. 主題會下載為封存（.zip檔案）。

### 上傳主題 {#uploading-a-theme}

您可以在專案上使用具有樣式預設集的已建立主題。 您可以在您的專案上上傳其他人建立的主題套件，借此匯入這些套件。

上傳主題：

1. 在Experience Manager中，導覽至 **Forms >主題**.
1. 在主題頁中，按一下 **建立>檔案上傳**.
1. 在「檔案上傳」提示中，瀏覽並選擇電腦上的主題包，然後按一下 **上傳**.
已上傳的主題可在主題頁面中使用。

1. 登入AEM Forms例項。
1. 點選Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) 圖示>導覽 ![羅盤](assets/compass.png) 表徵圖> Forms>主題。
1. 按一下 **建立** > **檔案上傳**. 在「檔案上傳」提示中，瀏覽並選擇電腦上的主題包，然後按一下 **上傳**. 主題已上傳。

## 在通信管理中匯入和匯出資產 {#import-and-export-assets-in-correspondence-management}

若要在通信管理的兩個不同實施之間共用資產，例如資料字典、字母和檔案片段，您可以建立和共用.cmp檔案。 .cmp檔案可包含一或多個資料字典、字母、檔案片段和表單。

### 匯出檔案片段、字母和/或資料字典 {#export-document-fragments-letters-and-or-data-dictionaries}

1. 在信函、檔案片段或資料字典頁面中，點選並選取您要匯出至單一套件的資產，然後點選「佇列以供下載」。 這些資產排成了出口的隊伍。
1. 視需要，重複上述步驟以新增字母、檔案片段和資料字典。
1. 點選 **下載**.
1. 通信管理會顯示「下載資產」對話方塊，與匯出清單中的資產清單。

   ![匯出](assets/export.png)

1. 要查看導出的依賴項，請點選「解析」。 或跳到下一步。 即使您未點選「解析」，相依性仍會匯出。
1. 若要下載.cmp檔案，請點選 **確定**.
1. 通信管理會將.cmp檔案下載到您的電腦。

   .cmp檔案包含匯出的資產。 您可以與其他人共用.cmp檔案。 其他使用者可以匯入不同伺服器中的.cmp檔案，以取得新伺服器中的所有資產。

### 將所有通信管理資產匯出為套件 {#export-all-the-correspondence-management-assets-as-a-package}

使用此選項，從AEM Forms例項以套件形式下載所有通信管理資產和相關相依性。

例如，如果通信管理包含使用影像和文字的信函，則下載的套件也會包含與信函相關的影像和文字。 也會下載與資產相關聯的所有中繼資料屬性（包括自訂屬性）。 下載套件(.cmp)後，您就可以 [將套件匯入至不同的AEM Forms例項](../../forms/using/import-export-forms-templates.md#p-upload-forms-documents-assets-p).

若要以套件形式下載所有通信管理資產和相關相依性，請完成下列步驟：

1. 以表單使用者身分登入AEM Forms伺服器。
1. 點選 **Adobe Experience Manager** 欄中。
1. 點選工具( ![工具](assets/tools.png))，然後點選 **Forms**.
1. 點選 **匯出通信管理資產**.

   ![publish-cmp-assets-1](assets/publish-cmp-assets-1.png)

   (「匯出所有通信管理資產」頁面隨即顯示上次嘗試匯出程式的相關資訊，以及下載上次成功匯出套件的連結。

   ![export-last-run-details](assets/export-last-run-details.png)

1. 點選 **匯出** 然後，在確認訊息中，點選 **確定**.

   批次處理完成後，會更新上次執行詳細資訊和下載套件的連結。 這包括管理員登錄以及批處理運行成功還是失敗等資訊。 資產會匯出至套件，且會出現「下載已匯出的套件」連結。

   >[!NOTE]
   >
   >一旦啟動，「匯出所有資產」流程便無法取消。 此外，在匯出所有操作進行中時，請勿建立、刪除、修改或發佈任何資產，或起始「發佈所有資產」程式。a

1. 點選 **下載匯出的套件** 連結以下載套件檔案。

   若要將套件中的資產新增至通信管理的另一個例項， [將套件匯入AEM Forms執行個體](../../forms/using/import-export-forms-templates.md#p-upload-forms-documents-assets-p).

### 將檔案片段、信函和/或資料字典匯入通信管理 {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

您可以匯入匯出至.cmp檔案的資產。 .cmp檔案可以有一或多個字母、資料字典、檔案片段和相依資產。

>[!NOTE]
>
>匯入舊的通信管理資產以進行移轉時，請使用管理員帳戶登入。 如需移轉舊通信管理資產的詳細資訊，請參閱 [將通信管理資產移轉至AEM 6.1表單](/help/forms/using/migration-utility.md).

1. 在資料字典、字母或檔案片段頁面上，點選 **建立>檔案上傳** 並選取.cmp檔案。
1. 通信管理會顯示「匯入資產」對話方塊，其中包含匯入的資產清單。 點選 **匯入**.

   匯入資產後，會更新資產的下列屬性，而其他屬性維持不變：

   * 作者：顯示將資產匯入伺服器的使用者ID
   * 已修改：將資產匯入伺服器的時間

   >[!NOTE]
   >
   >若要上傳XDP（作為cmp檔案或其他檔案的一部分），您必須是表單功能使用者群組的成員。 如需存取權限，請聯絡管理員。

## 匯出工作流程應用程式 {#export-a-workflow-application}

您可以使用AEM套件管理器來匯出工作流程應用程式。 此程式如下所列：

1. 開啟AEM Forms套件管理器。 套件管理器的URL為https://&lt;server>:&lt;port>/crx/packmgr。
1. 按一下 **[!UICONTROL 建立套件]**. 此 **[!UICONTROL 新套件]** 對話框。
1. 指定套件的名稱、版本和群組。 按一下&#x200B;**[!UICONTROL 「確定」]**。
1. 按一下 **[!UICONTROL 編輯]** 然後開啟 **[!UICONTROL 篩選器]** 標籤。 按一下 **[!UICONTROL 新增篩選]**. 指定工作流應用程式的路徑。 例如， /etc/fd/dashboard/startpoints/homemortgage。 按一下 **[!UICONTROL 新增規則]**.

1. 開啟 **[!UICONTROL 進階]** 標籤。 選擇 **[!UICONTROL 合併]** 或 **[!UICONTROL 覆寫]** 在ACL處理欄位中。 按一下「**[!UICONTROL 儲存]**」。
1. 按一下 **[!UICONTROL 建置]** 來建立套件。

   建置套件後，您可以下載套件並將其匯入至其他伺服器。 工作流程應用程式會顯示在上傳套件的伺服器上。

   >[!NOTE]
   >
   >為了使工作流應用程式能夠正常工作，還導出了相應的最適化表單和工作流模型。

## 資料夾和組織資產 {#folders-and-organizing-assets}

AEM Forms使用者介面使用資料夾來排列資產。 這些資料夾可用來排列在AEM Forms使用者介面中建立的資產。 您可以重新命名、建立子資料夾，以及儲存這些資料夾中的資產和檔案。 在資料夾中組織檔案和資產可讓您將檔案分組，以方便管理。 您可以選取資料夾，然後選擇下載或刪除資料夾。

若要建立資料夾，請完成下列步驟：

### 建立資料夾 {#create-a-folder}

1. 登入AEM Forms使用者介面： `https://<server>:<port>/aem/forms.html`.
1. 導覽至您要建立資料夾的位置。
1. 點選「建立>資料夾」。
1. 輸入以下詳細資訊：

   * **標題：** 資料夾的顯示名稱
   * **名稱：** *（強制）* 要在儲存庫中儲存資料夾的節點名稱

   >[!NOTE]
   >
   >依預設，名稱欄位的值會自動從標題填入。 名稱只能包含英數字元，或連字型大小(-)和底線(_)特殊字元。 標題中輸入的任何其他特殊字元都會自動以連字型大小取代，系統會提示您確認新名稱。 您可以選擇繼續使用建議的名稱或進一步編輯它。

1. 資產清單中的目前位置會顯示帶有您所定義標題的新資料夾。

   如果資料夾存在並指定名稱，則提交會失敗，並出現錯誤。 您可以將游標移至錯誤上以檢視錯誤訊息 ![aem6forms_error_alert](assets/aem6forms_error_alert.png) 表徵圖，顯示在名稱欄位旁邊。

   您可以點選新建立的資料夾，以前往資料夾內，並在資料夾內建立資產或資料夾。 此外，您可以選取資料夾，並選擇將其排入佇列以供下載、刪除或編輯其名稱。

   ![editdeletedownloadoldafolder](assets/editdeletedownloadafolder.png)

### 建立一或多個資產或信函的復本 {#create-copies-of-one-or-more-assets-or-letters}

您可以使用現有資產和信函，快速建立具有類似屬性、內容及繼承資產的資產和信函。 您可以複製和貼上資料字典、檔案片段和字母。

完成下列步驟以建立資產和信函的復本：

1. 在相關「資產」或「信函」頁面中，選取一或多個資產/信函。 UI會顯示「複製」圖示。
1. 點選「 複製」。UI會顯示「貼上」圖示。 您也可以選擇在貼上前前往/導覽資料夾內。 不同的資料夾可以包含名稱相同的資產。 有關資料夾的詳細資訊，請參閱 [資料夾和組織資產](#folders-and-organizing-assets).
1. 點選「貼上」。 將出現「貼上」對話框。 系統會自動為資產/信函的新副本產生名稱和標題，但您可以編輯資產/信函的標題和名稱。

   如果您複製並貼上相同位置的資產/信函，尾碼「 — CopyXX」會新增至資產/信函的現有名稱。 如果複製的資產/信函沒有標題，自動產生的標題欄位會保留空白。

1. 如有需要，請編輯您要用來儲存資產/信函副本的標題和名稱。
1. 點選「貼上」。 系統會建立複製資產的新復本。

## 搜尋 {#search-forms}

AEM Forms UI可讓您搜尋您的內容。 使用頂端列，您可以點選「搜尋」 **[A]** 來搜尋您的內容以尋找資源，例如資產和檔案。

搜尋資產時，AEM Forms會顯示側面板。 您也可以點選 ![assets-browser-content-only](assets/assets-browser-content-only.png) >篩選 **[B]** 調用側面板。 使用側面板中的各種篩選器，可縮小搜尋範圍。 側面板還允許您保存搜索。

![search_topbar](assets/search_topbar.png)

**答：** 搜尋 **B.** 篩選

![側面板 — 篩選器](assets/search_sidepanel.png)

側面板 — 篩選器

在側面板中，您可以使用下列項目來縮小搜尋結果的範圍：

* 搜索目錄
* 標記
* 搜索標準；例如，修改日期、發佈狀態、LiveCopy狀態。

側面板還允許您將搜索設定與您選擇的名稱一起保存。

有關使用搜索、篩選、保存的搜索和側面板的更多資訊和說明，請參閱 [搜尋](/help/sites-authoring/search.md).
