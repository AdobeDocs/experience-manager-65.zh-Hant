---
title: 向AEM Forms進口和出口資產
seo-title: Importing and exporting assets to AEM Forms
description: 您可以從實例中導入和導出自適應表單和模板，也可以在實例中導AEM入和導出。 這有助於遷移表單或跨系統移動表單。
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

# 向AEM Forms進口和出口資產{#importing-and-exporting-assets-to-aem-forms}

您可以在不同的AEM Forms實例之間移動表單和相關資產、主題、資料詞典、文檔片段和字母。 在將系統遷移或表單從舞台伺服器移動到生產伺服器時需要這種移動。 對於支援通過AEM FormsUI上傳和導入的資產，建議使用FormsUI進行導出或導入。 建議不AEM要使用包管理器導出或導入此類資產。

>[!NOTE]
>
>* 在AEMForms6.4中，crx-repository的結構和路徑已發生更改。 如果將資產從以前的版本導入到AEMForms6.4版，並且該表單對舊結構有一些依賴項，則必須手動導出依賴項。 有關儲存庫結構和路徑更改的詳細資訊，請參見 [中的儲存庫重AEM組](/help/sites-deploying/repository-restructuring.md)。
>


## 下載或上載Forms和文檔資產 {#download-or-upload-forms-amp-documents-assets}

AEM Forms用戶介面允許您通過將資AEM產下載為AEMCRX包或二進位檔案來從實例導出資產。 然後，可以將下載AEM的CRX軟體包或二進位檔案導入另AEM一個實例。

除自適應表單模板和自適應表單內容策略外，所有資產都支援通過AEM Forms用戶介面進行導出和導入。 因此，在從AEM FormsUI導出自適應表單時，相關的自適應表單模板和內容策略不會像其他相關資產那樣自動導出。

對於這些資產類型，必須AEM使用包管理器在源伺服器上創AEM建CRX包，並在目標伺服器上安裝包。 有關建立和安裝軟體包的資訊，請參見 [使用包](/help/sites-administering/package-manager.md)。

### 下載Forms和文檔資產 {#download-forms-amp-documents-assets}

下載Forms和文檔資產：

1. 登錄到AEM Forms實例。
1. 點擊Experience Manager ![adobeexperience manager](assets/adobeexperiencemanager.png) 表徵圖 ![羅盤](assets/compass.png) 表徵圖>Forms>Forms和文檔。
1. 選擇表單資產並點擊 **下載** 表徵圖
1. 在下載資產中，選擇以下選項之一，然後點擊 **下載**。

   * **下載為CRX包：** 使用此選項可將所有選定資產和相關依存關係從AEM Forms實例下載並移到另一個實例。 它以crx包的形式下載所有資產和資料夾。 任何表單資產(包括在AEM（自適應表單、交互通信和自適應表單片段）中創作的表單、表單集、表單模板、PDF文檔和資源（XSD、XFS、影像）)都可以作為包從AEM FormsUI下載。
將資產作為包下載的好處是，它還下載被選擇下載的資產使用的資產。 例如，如果您有一個使用表單模板、XSD和影像的自適應表單。 選擇此自適應表單並將其作為包下載時，下載的包還包含表單模板、XSD和映像。 還下載與資產關聯的所有元資料屬性（包括自定義屬性）。

   * **將資產下載為二進位檔案：** 使用此選項只下載表單模板(XDP)、PDF forms(PDF)、文檔(PDF)和資源（影像、架構、樣式表）。 您可以使用外部應用程式編輯這些資產。 它將包含二進位檔案的表單資產(如XSD、XDP、映像、PDF和XDP)下載為.zip檔案。
無法下載自適應表單、Interactive Communications、自適應表單片段、主題和表單集 **將資產下載為二進位檔案** 的雙曲餘切值。 要下載這些資產，您應使用 **下載為CRX包** 的雙曲餘切值。

   選定的資產將作為存檔（.zip檔案）下載。

   >[!NOTE]
   >
   >包文AEM件和二進位檔案都作為存檔檔案（.zip檔案）下載。 不會隨資產一起下載資產模板。 您需要單獨導出資產模板。

### 上載Forms和文檔資產 {#upload-forms-amp-documents-assets}

要上載Forms和文檔資產：

>[!VIDEO](https://vimeo.com/)

1. 登錄到AEM Forms實例。
1. 點擊Experience Manager ![adobeexperience manager](assets/adobeexperiencemanager.png) 表徵圖 ![羅盤](assets/compass.png) 表徵圖>Forms>Forms和文檔。
1. 點擊 **建立** >**檔案上載**。 將出現上載表單或包對話框。
1. 在對話框中，瀏覽並選擇要導入的包或存檔。 您還可以選擇PDF文檔、XSD、影像、樣式表和XDP表單。 點擊 **開啟**。 您選擇的資料夾或檔案名不得包含任何特殊字元。

   在對話框中，驗證上載的資產的詳細資訊，然後點擊 **上載**。

   如果您上載現有的表單資產，則會更新該資產。

   >[!NOTE]
   >
   >上載包不會替換現有資料夾層次結構。 例如，如果在一台伺服器上的/content/dam/formsanddocuments位置有一個名為「Training」的自適應表單。 您可以下載自適應表單，然後將表單上載到另一台伺服器上。 第二台伺服器在同一位置/content/dam/formsanddocuments還有一個名為「Training」的資料夾。 上載失敗。

## 下載或上載主題 {#downloading-or-uploading-a-theme}

使用AEM Forms，您可以建立、下載或上載主題。 建立主題時與表單、文檔和字母等其他資產類似。 您可以建立主題，下載主題，然後將其上載到單獨的實例上以重新使用主題。 有關主題的詳細資訊，請參見 [AEM Forms主題](../../forms/using/themes.md)。

### 下載主題 {#downloading-a-theme}

您可以導出可在其他項目或實例中使用的AEM Forms主題。 可AEM以將主題作為zip檔案下載，並可以在實例上載。

下載主題：

1. 登錄到AEM Forms實例。
1. 點擊Experience Manager ![adobeexperience manager](assets/adobeexperiencemanager.png) 表徵圖 ![羅盤](assets/compass.png) 表徵圖>Forms>主題。
1. 選擇主題並點擊 **下載**。 主題將作為存檔檔案（.zip檔案）下載。

### 上載主題 {#uploading-a-theme}

可以將建立的主題與項目上的樣式預設一起使用。 您可以通過將其他人建立的主題包上載到項目中來導入它們。

上載主題：

1. 在Experience Manager中，導航到 **Forms>主題**。
1. 在「主題」頁中，按一下 **建立>檔案上載**。
1. 在「File Upload（檔案上載）」提示符下，瀏覽並選擇電腦上的主題包，然後按一下 **上載**。
上載的主題可在主題頁中找到。

1. 登錄到AEM Forms實例。
1. 點擊Experience Manager ![adobeexperience manager](assets/adobeexperiencemanager.png) 表徵圖 ![羅盤](assets/compass.png) 表徵圖>Forms>主題。
1. 按一下 **建立** > **檔案上載**。 在「File Upload（檔案上載）」提示符下，瀏覽並選擇電腦上的主題包，然後按一下 **上載**。 主題已上載。

## 通信管理中的進出口資產 {#import-and-export-assets-in-correspondence-management}

要在Tergement Management的兩個不同實現之間共用資產（如資料字典、字母和文檔片段），可以建立和共用.cmp檔案。 .cmp檔案可以包括一個或多個資料字典、字母、文檔片段和表單。

### 導出文檔片段、字母和/或資料字典 {#export-document-fragments-letters-and-or-data-dictionaries}

1. 在字母、文檔片段或資料字典頁面中，點擊並選擇要導出到單個包的資產，然後點擊隊列以下載。 這些資產已排好隊準備出口。
1. 根據需要，重複上述步驟以添加字母、文檔片段和資料字典。
1. 點擊 **下載**。
1. Oracle Temenge Management顯示「下載資產」對話框，其中顯示導出清單中的資產清單。

   ![出口](assets/export.png)

1. 要查看導出的依賴關係，請點擊「解決」。 或者跳到下一步。 即使不點擊「解析」(resolve)，依賴項仍會導出。
1. 要下載.cmp檔案，請點擊 **確定**。
1. 「通信管理」將.cmp檔案下載到您的電腦。

   .cmp檔案包括導出的資產。 您可以與其他人共用.cmp檔案。 其他用戶可以將.cmp檔案導入到其他伺服器中，以獲取新伺服器中的所有資產。

### 將所有Tergement Management資產作為包導出 {#export-all-the-correspondence-management-assets-as-a-package}

使用此選項可以從表單實例將所有Tergement Management資產和相關依賴項作為包AEM下載。

例如，如果Tergement Management有一封使用影像和文本的信件，則下載的檔案包還包含該影像和與該信件相關的文本。 還下載與資產關聯的所有元資料屬性（包括自定義屬性）。 下載包(.cmp)後，您可以 [將包導入到其他AEM Forms實例](../../forms/using/import-export-forms-templates.md#p-upload-forms-documents-assets-p)。

要將所有Tergement Management資產和相關依賴項作為包下載，請完成以下步驟：

1. 以表單用戶身份登錄AEM Forms伺服器。
1. 點擊 **Adobe Experience Manager** 的子菜單。
1. 點擊工具( ![工具](assets/tools.png))，然後點擊 **Forms**。
1. 點擊 **導出信件管理資產**。

   ![發佈 — cmp-assets-1](assets/publish-cmp-assets-1.png)

   (「導出所有通信管理資產」頁面出現，顯示上次嘗試導出進程的資訊以及下載上次成功導出的包的連結。

   ![導出上次運行的詳細資訊](assets/export-last-run-details.png)

1. 點擊 **導出** 在確認消息中，點擊 **確定**。

   批處理完成後，將更新上次運行詳細資訊和下載包的連結。 這包括管理員登錄以及批處理是否成功運行或失敗等資訊。 資產將導出到包，並出現「下載導出的包」連結。

   >[!NOTE]
   >
   >一旦啟動，「導出所有資產」流程將無法取消。 此外，在導出所有操作正在進行時，不要建立、刪除、修改或發佈任何資產或啟動「發佈所有資產」流程。a

1. 點擊 **下載導出的包** 連結以下載包檔案。

   要將包中的資產添加到另一個Tergement Management實例， [將包導入到AEM Forms實例](../../forms/using/import-export-forms-templates.md#p-upload-forms-documents-assets-p)。

### 將文檔片段、信函和/或資料字典導入到通信管理 {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

可以將導出到.cmp檔案的資產導入。 .cmp檔案可以具有一個或多個字母、資料字典、文檔片段和從屬資產。

>[!NOTE]
>
>導入舊Tergement Management資產進行遷移時，請使用管理員帳戶登錄。 有關遷移舊通信管理資產的詳細資訊，請參閱 [將信件管理資產遷AEM移到6.1表單](/help/forms/using/migration-utility.md)。

1. 在資料字典、字母或文檔片段頁面上，點擊 **建立>檔案上載** ，然後選擇.cmp檔案。
1. Oracle Tergement將顯示「導入資產」對話框，其中顯示已導入的資產清單。 點擊 **導入**。

   導入資產後，將更新資產的以下屬性，而其他屬性保持不變：

   * 作者：顯示將資產導入到伺服器的用戶的ID
   * 已修改：將資產導入到伺服器的時間

   >[!NOTE]
   >
   >為了能夠上載XDP（作為cmp檔案或其他檔案的一部分），您需要成為forms-power-users組的一部分。 有關訪問權限，請與管理員聯繫。

## 導出工作流應用程式 {#export-a-workflow-application}

可以使用包管AEM理器導出工作流應用程式。 此過程如下所列：

1. 開啟AEM Forms包管理器。 包管理器的URL為https://&lt;server>:&lt;port>/crx/packmgr。
1. 按一下 **[!UICONTROL 建立包]**。 的 **[!UICONTROL 新建包]** 對話框。
1. 指定包的名稱、版本和組。 按一下&#x200B;**[!UICONTROL 「確定」]**。
1. 按一下 **[!UICONTROL 編輯]** 開啟 **[!UICONTROL 篩選器]** 頁籤。 按一下 **[!UICONTROL 添加篩選器]**。 指定工作流應用程式的路徑。 例如， /etc/fd/dashboard/startpoints/homemtorgage。 按一下 **[!UICONTROL 添加規則]**。

1. 開啟 **[!UICONTROL 高級]** 頁籤。 選擇 **[!UICONTROL 合併]** 或 **[!UICONTROL 覆蓋]** 在「ACL處理」欄位中。 按一下「**[!UICONTROL 儲存]**」。
1. 按一下 **[!UICONTROL 生成]** 的子菜單。

   生成包後，您可以下載該包並將其導入到其他伺服器。 工作流應用程式出現在上載包的伺服器上。

   >[!NOTE]
   >
   >為了使工作流應用程式正常工作，還導出了相應的自適應表單和工作流模型。

## 資料夾和組織資產 {#folders-and-organizing-assets}

AEM Forms用戶介面使用資料夾來排列資產。 這些資料夾用於安排在AEM Forms用戶介面中建立的資產。 您可以更名、建立子資料夾，並將這些資料夾中的資產和文檔儲存。 將文檔和資產組織在資料夾中，可以將檔案分組在一起，以便於管理。 您可以選擇資料夾並選擇下載或刪除它。

要建立資料夾，請完成以下步驟：

### 建立資料夾 {#create-a-folder}

1. 登錄AEM Forms用戶介面 `https://<server>:<port>/aem/forms.html`。
1. 導航到要在其下建立資料夾的位置。
1. 按一下「建立」>「資料夾」。
1. 輸入以下詳細資訊：

   * **標題：** 資料夾的顯示名稱
   * **名稱：** *（強制）* 要在儲存庫中儲存資料夾的節點名稱

   >[!NOTE]
   >
   >預設情況下，名稱欄位的值會自動從標題中填充。 名稱只能包含字母數字字元或連字元(-)和下划線(_)特殊字元。 在標題中輸入的任何其他特殊字元將自動替換為連字元，並提示您確認新名稱。 您可以選擇繼續使用建議的名稱或進一步編輯它。

1. 在資產清單的當前位置顯示具有您定義的標題的新資料夾。

   如果存在具有指定名稱的資料夾，則提交將失敗並出現錯誤。 通過懸停在錯誤上方，可以查看錯誤消息 ![aem6forms_error_alert](assets/aem6forms_error_alert.png) 表徵圖。

   您可以點擊新建立的資料夾進入資料夾並在資料夾中建立資產或資料夾。 此外，您可以選擇資料夾並選擇將其排入隊列以便下載、刪除或編輯其名稱。

   ![編輯刪除下載資料夾](assets/editdeletedownloadafolder.png)

### 建立一個或多個資產或信件的副本 {#create-copies-of-one-or-more-assets-or-letters}

您可以使用現有資產和信件快速建立具有相似屬性、內容和繼承資產的資產和信件。 您可以複製和貼上資料字典、文檔片段和字母。

完成以下步驟以建立資產和信件的副本：

1. 在相關的「資產」或「信函」頁中，選擇一個或多個資產/信函。 UI顯示「複製」表徵圖。
1. 點選「 複製」。UI顯示「貼上」表徵圖。 您還可以選擇在貼上之前在資料夾內進行/導航。 不同的資料夾可以包含具有相同名稱的資產。 有關資料夾的詳細資訊，請參見 [資料夾和組織資產](#folders-and-organizing-assets)。
1. 按一下「貼上」。 此時將出現「貼上」對話框。 系統會自動生成資產/字母的新副本的名稱和標題，但您可以編輯資產/字母的標題和名稱。

   如果要在同一位置複製和貼上資產/字母，則會將尾碼「 — CopyXX」添加到資產/字母的現有名稱中。 如果複製的資產/信件不存在標題，則自動生成的標題欄位仍為空。

1. 如果需要，請編輯要保存資產/信件副本的標題和名稱。
1. 按一下「貼上」。 將建立複製的資產的新副本。

## 搜尋 {#search-forms}

AEM FormsUI允許您搜索內容。 使用頂欄，可以點擊「搜索」 **[A]** 搜索內容以查找資源，如資產和文檔。

搜索資產時，AEM Forms顯示側面板。 也可以點擊 ![僅瀏覽器內容](assets/assets-browser-content-only.png) >篩選 **[B]** 調用側面板。 使用側面板中的各種濾鏡，可以縮小搜索範圍。 側面板還允許您保存搜索。

![搜索頂欄](assets/search_topbar.png)

**答：** 搜索 **B** 篩選

![側面板 — 篩選器](assets/search_sidepanel.png)

側面板 — 篩選器

在側面板上，可使用以下方法縮小搜索結果的範圍：

* 搜索目錄
* 標記
* 搜索標準；例如，「修改日期」、「發佈狀態」、「LiveCopy狀態」。

側面板還允許您使用所選名稱保存搜索設定。

有關使用搜索、篩選、保存的搜索和側面板的詳細資訊和說明，請參見 [搜索](/help/sites-authoring/search.md)。
