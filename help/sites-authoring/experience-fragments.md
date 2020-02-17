---
title: 體驗片段
seo-title: 體驗片段
description: 'null'
seo-description: 'null'
uuid: 9a1d12ef-5690-4a2e-8635-a710775efa39
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 4c5b52c3-5e23-4125-9306-48bf2ded23cb
docset: aem65
translation-type: tm+mt
source-git-commit: 5c88d9cfdd6238961aa46d36ebc1206a5d0507e0

---


# 體驗片段{#experience-fragments}

「體驗片段」是一組或多個元件，包括可在頁面中參考的內容和版面。 它們可包含任何元件。

體驗片段：

* 是體驗（頁面）的一部分。
* 可跨多頁使用。
* 以範本（僅可編輯）為基礎，以定義結構和元件。
* 由段落系統中具有版面的一個或多個元件組成。
* 可以包含其他體驗片段。
* 可與其他元件（包括其他體驗片段）結合，以形成完整頁面（體驗）。
* 可以有不同的變化，這些變化可能會共用內容和／或元件。
* 可以細分為建置區塊，以便用於多種片段變化。

您可以使用體驗片段：

* 如果作者想要重複使用頁面的部分（體驗的片段），則必須複製並貼上該片段。 建立和維護這些複製／貼上體驗不但耗時，而且容易發生使用者錯誤。 體驗片段可免除複製／貼上的需求。
* 支援無頭CMS使用案例。 作者只想使用AEM來製作內容，但不想將內容傳送給客戶。 協力廠商系統／觸點會使用該體驗，然後傳送給使用者。

>[!NOTE]
>
>體驗片段的寫入存取權要求使用者帳戶必須註冊在群組中：
>
>    `experience-fragments-editors`
如果您遇到任何問題，請聯絡您的系統管理員。

## 何時應使用體驗片段？ {#when-should-you-use-experience-fragments}

應使用體驗片段：

* 無論何時您想要重複使用體驗。

   * 可重複使用相同或類似內容的體驗

* 當您將AEM當做協力廠商的內容傳送平台時。

   * 任何想要使用AEM做為內容傳送平台的解決方案
   * 將內容內嵌至協力廠商觸點

* 如果您有「體驗」，但有不同的變化或轉譯。

   * 頻道或內容特定變化
   * 對群組有意義的體驗（例如跨通道具有不同體驗的促銷活動）

* 當您使用全通道商務時。

   * 在社交媒體頻道上大 [規模分享](/help/sites-developing/experience-fragments.md#social-variations) 商務相關內容
   * 讓觸點成為交易性

## 組織您的體驗片段 {#organizing-your-experience-fragments}

建議您：
* 使用資料夾來組織您的體驗片段，

* [在這些資料夾上設定允許的範本](#configure-allowed-templates-folder)。

建立資料夾允許您：

* 為您的體驗片段建立有意義的結構；例如，根據分類

   >[!NOTE]
   您不需要將體驗片段的結構與網站的頁面結構對齊。

* [在資料夾級別分配允許的模板](#configure-allowed-templates-folder)

   >[!NOTE]
   您可以使用范 [本編輯器](/help/sites-authoring/templates.md) ，建立您自己的範本。

WKND專案會根據此建構一些體驗片段 `Contributors`。 使用的結構也說明如何使用其他功能，例如多網站管理（包括語言副本）。

請參閱：

`http://localhost:4502/aem/experience-fragments.html/content/experience-fragments/wknd/language-masters/en/contributors/kumar-selveraj/master`

![體驗片段的資料夾](/help/sites-authoring/assets/xf-folders.png)

## 建立和設定您的體驗片段的資料夾 {#creating-and-configuring-a-folder-for-your-experience-fragments}

若要建立並設定您的體驗片段資料夾，建議您：

1. [建立資料夾](/help/sites-authoring/managing-pages.md#creating-a-new-folder)。

1. [設定該資料夾允許的體驗片段範本](#configure-allowed-templates-folder)。

>[!NOTE]
您也可以設定例項 [的「允許範本」](#configure-allowed-templates-instance)，但不建議使 **用此方法** ，因為升級時可覆寫值。

### 為資料夾配置允許的模板 {#configure-allowed-templates-folder}

>[!NOTE]
這是指定允許範本的建 **議方法**，因為升級時不會覆寫值。

1. 導覽至所需的 **Experience Fragments** 檔案夾。

1. 選擇資料夾，然後選擇「 **屬性**」。

1. 在「允許的範本」欄位中指定擷取所需範本 **的規則運算式** 。

   例如：
   `/conf/(.*)/settings/wcm/templates/experience-fragment(.*)?`

   請參閱：
   `http://localhost:4502/mnt/overlay/cq/experience-fragments/content/experience-fragments/folderproperties.html/content/experience-fragments/wknd`

   ![體驗片段屬性——允許的範本](/help/sites-authoring/assets/xf-folders-templates.png)

   >[!NOTE]
   如需詳 [細資訊，請參閱體驗片段](/help/sites-developing/experience-fragments.md#templates-for-experience-fragments) 「範本」。

1. 選擇 **保存並關閉**。

### 為實例配置允許的模板 {#configure-allowed-templates-instance}

>[!CAUTION]
建議您不要使用此方 **法變更「允許的範本** 」，因為指定的範本可在升級時覆寫。
請僅供參考之用。

1. 導覽至所需的 **Experience Fragments** Console。

1. 選擇 **配置選項**:

   ![「配置」按鈕](assets/ef-02.png)

1. 在「設定體驗片段」對話 **方塊中指定必要的範本** :

   ![設定體驗片段](assets/ef-01.png)

   >[!NOTE]
   如需詳 [細資訊，請參閱體驗片段](/help/sites-developing/experience-fragments.md#templates-for-experience-fragments) 「範本」。

1. 選擇 **保存**。

## 建立體驗片段 {#creating-an-experience-fragment}

若要建立體驗片段：

1. 從全域導覽中選取「體驗片段」。

   ![xf-01](assets/xf-01.png)

1. 導覽至所需資料夾，然後選取「 **建立**」。

   ![xf-02](assets/xf-02.png)

1. 選擇 **體驗片段** ，以開啟「 **建立體驗片段」精靈** 。

   依次選擇所需 **的範本**、下 **一步**:

   ![xf-03](assets/xf-03.png)

1. 輸入 **體驗****片段的屬性**。

   「標 **題** 」為強制。 如果名 **稱** (Name)留空，則會從標題( **Title)中衍生出來**。

   ![xf-04](assets/xf-04.png)

1. 按一下&#x200B;**「建立」**。

   將顯示一條消息。 選取:

   * **完成** ：返回控制台

   * **開啟** ，以開啟片段編輯器

## 編輯您的體驗片段 {#editing-your-experience-fragment}

體驗片段編輯器提供與一般頁面編輯器類似的功能。

>[!NOTE]
如需 [如何使用頁面編輯器的詳細資訊](/help/sites-authoring/editing-content.md) ，請參閱編輯頁面內容。

以下示例過程說明如何為產品建立摘要：

1. 從元件瀏覽 **器拖放**[摘要](/help/sites-authoring/author-environment-tools.md#components-browser)。

   ![xf-05](assets/xf-05.png)

1. 從組 **[件工具欄](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste)**中選擇「配置」。
1. 新增資 **產** ，並視需要 **定義屬性** 。
1. 使用「完成」(勾選 **圖示** )確認定義。
1. 視需要新增更多元件。

## Creating An Experience Fragment Variation {#creating-an-experience-fragment-variation}

您可以根據您的需求，建立不同的體驗片段：

1. 開啟您的片段以 [進行編輯](/help/sites-authoring/experience-fragments.md#editing-your-experience-fragment)。
1. 開啟「變 **數** 」標籤。

   ![xf-authoring-06](assets/xf-authoring-06.png)

1. **Create** （建立）允許您建立：

   * **變數**
   * **變數為 live-copy**.

1. 定義所需屬性：

   * **範本**
   * **標題**
   * **名稱**;如果保留空白，則會從「標題」衍生
   * **說明**
   * **變數標記**
   ![xf-06](assets/xf-06.png)

1. 使用「完 **成** （勾選圖示）確認」，新變數會顯示在面板中：

   ![xf-07](assets/xf-07.png)

## 使用您的體驗片段 {#using-your-experience-fragment}

您現在可以在編寫頁面時使用體驗片段：

1. 開啟任何頁面進行編輯。

   例如： [https://localhost:4502/editor.html/content/we-retail/language-masters/en/products/men.html](https://localhost:4502/editor.html/content/we-retail/language-masters/en/products/men.html)

1. 將元件從「元件」瀏覽器拖曳至頁面段落系統，以建立「體驗片段」元件的例項：

   ![xf-08](assets/xf-08.png)

1. 將實際的體驗片段新增至元件例項；其中：

   * 從「資產瀏覽器」拖曳必要片段至元件
   * 從組 **件工具欄** ，選擇「設定」，並指定要使用的片段，以「完成 **** （勾選）」確認
   ![xf-09](assets/xf-09.png)

   >[!NOTE]
   在元件工具列中，編輯會以捷徑方式在片段編輯器中開啟片段。

## 建置區塊 {#building-blocks}

您可以選取一或多個元件，以建立要在片段內回收的建置區塊：

### 建立構建塊 {#creating-a-building-block}

要建立新的構建塊：

1. 在「體驗片段」編輯器中，選取您要重複使用的元件：

   ![xf-10](assets/xf-10.png)

1. 從元件工具欄中，選擇「 **轉換為構建塊**:

   ![xf-authoring-13-icon](assets/xf-authoring-13-icon.png)

1. 輸入建置塊的名 **稱**，並使用 **Convert確認**:

   ![xf-11](assets/xf-11.png)

1. 建 **立區塊** (Building Block)將顯示在頁籤中，並可在段落系統中選擇：

   ![xf-12](assets/xf-12.png)

#### 管理構建塊 {#managing-a-building-block}

您的構建塊在「構建塊」( **Building Blocks)頁籤中可見** 。 對於每個塊，可以執行以下操作：

* 前往主版：在新標籤中開啟主變數
* 重新命名
* 刪除

![xf-13](assets/xf-13.png)

#### 使用構建塊 {#using-a-building-block}

您可以將構建塊拖動到任何片段的段落系統，如同任何元件。

## 體驗片段的詳細資訊 {#details-of-your-experience-fragment}

您可以查看您片段的詳細資訊：

1. 詳細資訊會顯示在 **Experience Fragments** console的所有檢視中，「清單檢視」包 **括匯出** 至Target的詳細資訊 [](/help/sites-administering/experience-fragments-target.md):

   ![ef-03](assets/ef-03.png)

1. 當您開啟體驗 **片段的** 「屬性」時：

   ![ef-04](assets/ef-04.png)

   這些屬性可用於各種頁籤：

   >[!CAUTION]
   當您從「體驗片段」控制台開 **啟「屬性** 」時，會顯示這些標籤。
   如果您 **在編輯體驗片段時開啟屬性** ，則會顯示適當 [的頁面屬性](/help/sites-authoring/editing-page-properties.md) 。

   ![ef-05](assets/ef-05.png)

   * **基本**

      * **標題** -必填

      * **說明**
      * **標記**
      * **變數總數** -僅提供資訊

      * **Web變體數** -僅提供資訊
      * **非Web變數的數量** -僅&#x200B;**提供資訊**

      * **使用此片段的頁數** -僅提供資訊
   * **雲端服務**

      * **雲端設定**
      * **雲端服務設定**
      * **Facebook 頁面 ID**
      * **Pinterest Board**
   * **引用**

      * 引用清單。
   * **社交媒體狀態**

      * 社交媒體變化的詳細資料。




## 純HTML轉譯 {#the-plain-html-rendition}

使用URL `.plain.` 中的選取器，您可以從瀏覽器存取純HTML轉譯。

>[!NOTE]
雖然這可直接從瀏覽器取得，但主 [要目的是允許其他應用程式（例如協力廠商網路應用程式、自訂行動裝置實作）僅使用URL直接存取體驗片段的內容](/help/sites-developing/experience-fragments.md#the-plain-html-rendition)。

## 匯出體驗片段 {#exporting-experience-fragments}

依預設，體驗片段會以HTML格式傳送。 AEM和協力廠商管道都可使用此功能。

若要匯出至Adobe Target，也可以使用JSON。 如需 [完整資訊，請參閱Target與體驗片段整合](/help/sites-administering/experience-fragments-target.md) 。
