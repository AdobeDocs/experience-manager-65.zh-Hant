---
title: 最適化表單範本
description: 使用範本編輯器定義基本結構和初始表單內容，以建立最適化表單範本。
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: d7287ee7-fb4e-4d47-b37e-0a9260344070
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2030'
ht-degree: 3%

---

# 最適化表單範本{#adaptive-form-templates}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant)，用來[建立新的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/template-editor.html?lang=zh-Hant) |
| AEM 6.5 | 本文章 |



當您編寫表單時，可在編輯器中新增欄位和元件以定義表單結構、內容和動作。 您在表單容器的`guideRootPanel`中新增欄位和元件。 使用範本編輯器，您可以建立包含基本結構和初始內容的範本，以供作者建立表單。

例如，您希望所有表單作者在登錄檔單中都擁有某些文字方塊、導覽按鈕和提交按鈕。 您可以使用作者可用來建立與其他登錄檔單一致的表單的元件，來建立範本。 作者使用範本建立最適化表單時，新表單會繼承您在範本中指定的結構和元件。 範本編輯器可讓您：

* 在結構圖層中新增表單的頁首與頁尾元件。
* 提供表單的初始內容。
* 指定主題，提交動作。

## 使用範本 {#working-with-templates}

您可以導覽至&#x200B;**Adobe Experience Manager >工具>範本**，從「工具」功能表存取範本編輯器。 範本會整理在啟用可編輯範本的資料夾中。 AEM提供可組織範本的全域資料夾。 但預設不會啟用。 您可以要求管理員啟用全域資料夾或建立範本資料夾。 如需有關如何建立資料夾的詳細資訊，請參閱[範本資料夾](/help/sites-developing/page-templates-editable.md)。

選取開啟資料夾後，您會看到「建立」按鈕，讓您為最適化表單建立範本。

### 建立範本 {#create-template}

建立資料夾後，請開啟資料夾並執行以下步驟來建立範本：

1. 在範本主控台中，選取您已建立的資料夾中的&#x200B;**建立**。
1. 在「挑選範本型別」區段中，選取&#x200B;**最適化表單範本**，然後選取&#x200B;**下一步**。

1. 在[範本詳細資料]區段中，提供範本標題並選取[建立]。**&#x200B;**
您可以提供說明和縮圖，以便在表單製作時選取建立的範本時看得到。

1. 選取&#x200B;**完成**&#x200B;以返回主控台，或選取&#x200B;**開啟**&#x200B;以在編輯器中開啟範本。

### 範本編輯器UI {#template-editor-ui}

開啟範本進行編輯時，您可以看到下列AEM Editor元件：

* **頁面工具列**
包含下列選項：

   * **切換側面板**：可讓您顯示或隱藏側欄。
   * **頁面資訊**：可讓您指定發佈/取消發佈時間、縮圖、使用者端資料庫、頁面原則及頁面設計使用者端資料庫等資訊。
   * **模擬器**：可讓您模擬及自訂不同裝置的外觀。
   * **圖層選擇器：**&#x200B;可讓您變更圖層。
您可以選擇&#x200B;**結構**&#x200B;圖層或&#x200B;**初始內容**&#x200B;圖層。 結構圖層可讓您新增及自訂頁首與頁尾。 初始內容層可讓您自訂表單內容。

   * **預覽：**&#x200B;讓您預覽範本在發佈時的外觀。 您可以使用「圖層選取器」和「預覽」來切換編輯和預覽模式。

* **側欄：**&#x200B;提供內容、屬性、Assets和元件瀏覽器。
* **元件工具列：**&#x200B;選取元件時，您會看到可自訂元件的工具列。
* **頁面**：您新增內容以建立範本的區域。

請參閱[製作最適化表單簡介](../../forms/using/introduction-forms-authoring.md)，瞭解觸控式UI編輯器。

### 編輯範本 {#editing-a-template}

最適化表單範本是使用兩層來建立：

* 結構
* 初始內容

圖層選取器位於熒幕右上角的「預覽」選項旁。

### 結構 {#structure}

在範本編輯器中選取結構圖層時，您可以看到最適化表單容器上方和下方的版面容器。 作者可將這些配置容器用於頁首和頁尾。 您可以新增、編輯或自訂頁首與頁尾。 將版面容器中的最適化表單標題元件拖放到最適化表單容器上方，以自訂範本標題。 將調適型表單頁尾元件拖放至調適型表單容器下方的版面容器中，以自訂範本頁尾。

結構圖層中的![配置容器](assets/header-layer-selector.png)

在結構圖層中配置容器

頁首元件&#x200B;**B.**&#x200B;頁尾元件的配置容器&#x200B;**A.**

將版面容器中的最適化表單標題元件拖放到最適化表單容器上方。 新增元件後，您可以指定其屬性，以讓您新增標誌並提供其標題。

同樣地，將頁尾元件拖放至最適化表單容器下方的版面容器時，可以提供版權資訊和公司詳細資訊。

![頁首與頁尾已新增至結構圖層](assets/header-and-footer.png)

在「結構」圖層新增頁首與頁尾

#### 鎖定/解除鎖定結構層中的元件 {#locking-unlocking-components-in-the-structure-layer}

當您在選取結構圖層的情況下編輯範本時，可以解鎖範本的頁首和頁尾。 如果範本中的元件已解除鎖定，表單作者可以在使用該範本的最適化表單中編輯元件。 鎖定元件可防止表單作者以最適化表單編輯它。 元件工具列中有鎖定選項。

例如，在範本中新增標題元件。 選取元件時，您會在元件工具列中看到鎖定選項。 通常頁首包含公司名稱和標誌，您不希望表單作者變更範本中的標誌和頁首。 在使用範本建立並鎖定頁首元件的調適型表單中，表單作者無法變更標誌和公司名稱。

>[!NOTE]
>
>不建議分別鎖定或解除鎖定頁首元件中的影像或標誌。 您可以解除鎖定標頭元件。

### 初始內容 {#initial-content}

選取「初始內容」選項時，範本的「最適化表單」容器會開啟，就像要編輯的最適化表單一樣。 如同製作最適化表單，您可以指定初始設定，例如選取主題和提交動作。

表單作者可將其用作建立表單的基礎。 內容流程結構是在範本的「初始內容」層中所指定。 若要切換到編輯表單範本的初始內容，在頁面工具列的[預覽]之前，選取![畫佈下拉式清單](assets/canvas-drop-down.png) **>初始內容**。
![範本編輯器中的初始內容層](assets/initial-content-layer.png)

範本編輯器中的初始內容層，顯示為指定屬性而選取的最適化表單容器。

![初始內容](assets/initial-content-layer-1.png)

在「初始內容」圖層中，您會建立最適化表單範本，供作者作為基礎。 製作範本與製作表單類似，您會使用側邊欄中的可用選項。 側欄提供內容、屬性、資產和元件瀏覽器。

請參閱[側欄](../../forms/using/introduction-forms-authoring.md#sidebar)。

>[!NOTE]
>
>當您選取「儲存內容」或「儲存PDF」作為「提交動作」時，您會獲得一個選項來指定「儲存」路徑。 如果您在範本中指定路徑，則以此範本建立的所有表單都會有相同的路徑。 您可以指定正確的儲存路徑，或確保表單作者更新路徑，以防止每個表單中的資料都儲存在相同位置。

#### 建立具有索引標籤和面板的最適化表單範本  {#creating-an-adaptive-form-template-with-tabs-and-panels-nbsp}

例如，您想建立具有下列標籤的範本：

* 一般資訊
* 專業資訊

您已新增標誌、提供標題，並在結構圖層中新增頁尾。 鎖定頁首和頁尾，以防止表單作者在使用範本建立表單時編輯它們。

將圖層從「結構」變更為「初始內容」，並開始將內容新增至表單。 若要建立索引標籤結構，請在最適化表單容器的guideRootPanel中新增子面板。 若要新增面板：

* 選取&#x200B;**將元件拖曳到這裡**&#x200B;選項時，點選&#x200B;**+**&#x200B;按鈕即可新增面板。

* 您可以從側邊欄中的元件瀏覽器拖放面板元件。
* 您可以從元件工具列新增`guideRootPanel`的子面板。

若要建立「一般資訊」和「專業資訊」標籤，請在`guideRootPanel`的子面板中新增兩個面板。 選取面板，然後選取![cmppr](assets/cmppr.png)以開啟側邊欄中的屬性。 將元素名稱變更為`general-info`和`professional-info`，並將標題分別變更為「一般資訊」和「專業資訊」。 在側邊欄中，選取內容以開啟內容瀏覽器。 在[表單物件]索引標籤中，選取`guideRootPanel`。 在編輯器中，選取guideRootPanel。 在元件工具列中選取![cmppr](assets/cmppr.png)以開啟其屬性。 在「面板配置」欄位中，選取&#x200B;**索引標籤在頂端**，然後選取&#x200B;**完成**。 標籤範本結構即會套用。

#### 在索引標籤中新增內容 {#adding-content-in-tabs}

![正在新增最適化表單範本中的欄位](assets/template-edit-initial-content.png)

新增面板並將面板結構為索引標籤後，您即可在索引標籤內新增欄位。 在編輯器中選取索引標籤時，您可以看到&#x200B;**將元件拖曳到這裡**&#x200B;選項。 您可以拖放元件，例如文字方塊、清單專案和按鈕。 您可以從側邊欄中的元件瀏覽器拖放元件。

每個元件都有可增強資料擷取和操作的屬性。 例如，您可以啟用元件的&#x200B;**必要欄位**&#x200B;屬性。 您的作者可以指定客戶在略過填寫必填欄位時看到的訊息。 在&#x200B;**必要欄位訊息**&#x200B;屬性中指定訊息。

在範例範本中，名稱、電話號碼和出生日期欄位會新增到「一般資訊」標籤中。 在「專業資訊」標籤中，新增「目前僱用」、「僱用型別」、「教育資格」欄位。

新增欄位後，您可以新增「提交」和「重設」等按鈕。

### 啟用範本 {#enabling-the-template}

當您建立範本時，它會新增為草稿。 啟用範本以將其用於建立最適化表單。 若要啟用範本：

1. 導覽至&#x200B;**Adobe Experience Manager >工具>範本**，並開啟您建立範本的資料夾。

1. 您建立的範本會標示為「草稿」。
1. 選取範本並在工具列中選取&#x200B;**啟用**。
建立最適化表單時，系統要求您選擇範本時，您會看到範本列出。

## 匯入或匯出範本 {#importing-or-exporting-a-template}

表單可與其範本搭配使用。 下載使用自訂範本建立的最適化表單時，不會下載範本。 當您在其他AEM Forms執行個體上匯入表單時，會匯入表單而不包含其範本。 如果表單已匯入，但其範本無法使用，則不會轉譯表單。 您可以封裝來自`https://<server>:<port>/crx/packmgr`中`/conf`節點的自訂範本，並將其連線您要上傳表單的AEM Forms執行個體。

## 使用範本建立最適化表單 {#creating-an-adaptive-form-using-the-template}

建立並啟用範本後，當您建立最適化表單時，表單管理員便可使用範本。 若要使用範本並建立調適型表單，請參閱[建立調適型表單](../../forms/using/creating-adaptive-form.md)。

## 變更現成範本的顯示選項  {#change-display-option-of-out-of-the-box-templates}

您可以建立最適化表單的自訂範本，以定義基本結構和初始內容。 AEM Forms也提供一組現成可用的最適化表單範本。 您可以選擇顯示或隱藏範本。

執行以下步驟來顯示和隱藏範本：

1. 登入AEM Forms作者執行個體並導覽至&#x200B;**工具** > **作業** > **網頁主控台**。

   >[!NOTE]
   >
   >AEM Web主控台的URL是https://&#39;[伺服器]：[連線埠]&#39;/system/console/configMgr

1. 尋找並開啟&#x200B;**FormsManager組態**&#x200B;設定：

   * 若要顯示或隱藏現成可用的最適化表單範本，請核取或取消核取&#x200B;**包含現成的AF和AD範本**&#x200B;選項。
   * 若要顯示或隱藏已在AEM 6.0 Forms或AEM 6.1 Forms發行版本中新增但現在已棄用的調適型表單範本，請核取或取消核取&#x200B;**包含AEM 6.0 AF範本**&#x200B;選項。 如果已核取此選項，則此選項必須啟用&#x200B;**包含現成可用的AF和AD範本**&#x200B;設定，才能生效。

1. 按一下「**儲存**」。現成範本的顯示選項已變更。

## 建議 {#recommendations}

* 在範本編輯器中修改表單的屬性時，請勿使用BindReference屬性。
* 如果您想要新增中斷點，請在編寫最適化表單範本時建立中斷點。
如需中斷點的詳細資訊，請參閱[回應式配置](/help/sites-authoring/responsive-layout.md)。
