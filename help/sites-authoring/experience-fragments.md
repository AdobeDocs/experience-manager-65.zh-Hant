---
title: 體驗片段
description: Adobe Experience Manager Sites製作中的體驗片段。
exl-id: 1ff9ac47-9a3a-4a4e-8af8-bc73048e0409
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Experience Fragments
role: User
source-git-commit: 382368d7a91ba2229ce1cdfe19f3b9871b93498e
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 4%

---

# 體驗片段{#experience-fragments}

在Adobe Experience Manager (AEM)中，體驗片段是一組一或多個元件，包括可在頁面中參考的內容和版面。 它們可以包含任何元件。

體驗片段：

* 是體驗（頁面）的一部分。
* 可用於多個頁面（以可編輯的範本為基礎）。
* 以範本為基礎（僅可編輯）以定義結構和元件。
* 此範本用於建立體驗片段的&#x200B;*根頁面*。
* 由段落系統中一或多個元件組成，具有版面。
* 可以包含其他體驗片段。
* 可與其他元件（包括其他體驗片段）結合以形成完整頁面（體驗）。
* 您可以根據根頁面建立一或多個變數。
* 這些變化可能會共用內容和/或元件。
* 可以劃分為可在片段的多個變體中使用的建置區塊。

您可以使用體驗片段：

* 如果作者想要重複使用頁面的部分（體驗的片段），他們需要複製並貼上該片段。 建立及維護這些複製/貼上體驗非常耗時，而且容易發生使用者錯誤。 體驗片段不需要複製/貼上。
* 支援Headless CMS使用案例。 作者只想將AEM用於製作，而不是用於提供給客戶。 協力廠商系統/接觸點會取用該體驗，然後傳送給一般使用者。
* 具有[多網站管理(MSM)](/help/sites-administering/msm.md)；作為體驗片段是頁面的一部分。 這同時適用於個別片段及其所在的資料夾。

>[!NOTE]
>
>體驗片段的寫入許可權需要在群組中註冊使用者帳戶：
>
>    `experience-fragments-editors`
>
>如果您遇到任何問題，請聯絡您的系統管理員。

## 何時應使用體驗片段？ {#when-should-you-use-experience-fragments}

該使用「體驗片段」的情況：

* 每當您想要重複使用體驗時。

   * 將與相同或類似內容重複使用的體驗

* 當您使用AEM做為協力廠商的內容傳遞平台時。

   * 任何想要使用AEM作為內容傳遞平台的解決方案
   * 將內容內嵌於第三方接觸點

* 如果您有具有不同變數或轉譯的體驗。

   * 管道或內容特定變數
   * 適合群組的體驗（例如，跨頻道具有不同體驗的行銷活動）

* 當您使用全通道Commerce時。

   * 大規模共用[社群媒體](/help/sites-developing/experience-fragments.md#social-variations)頻道上的商業相關內容
   * 讓接觸點成為異動

## 組織您的體驗片段 {#organizing-your-experience-fragments}

建議您：
* 使用資料夾來組織您的體驗片段，

* [在這些資料夾上設定允許的範本](#configure-allowed-templates-folder)。

建立資料夾可讓您：

* 為您的體驗片段建立有意義的結構；例如，根據分類

  >[!NOTE]
  >
  >您不需要將體驗片段的結構與網站的頁面結構對齊。

* [在檔案夾層級配置允許的範本](#configure-allowed-templates-folder)

  >[!NOTE]
  >
  >您可以使用[範本編輯器](/help/sites-authoring/templates.md)來建立您自己的範本。

WKND專案會根據`Contributors`建構一些體驗片段。 使用的結構也說明了如何使用其他功能，例如「多網站管理」（包括語言副本）。

請參閱：

`http://localhost:4502/aem/experience-fragments.html/content/experience-fragments/wknd/language-masters/en/contributors/kumar-selveraj/master`

體驗片段的![資料夾](/help/sites-authoring/assets/xf-folders.png)

## 為您的體驗片段建立和設定資料夾 {#creating-and-configuring-a-folder-for-your-experience-fragments}

若要為體驗片段建立及設定資料夾，建議您：

1. [建立資料夾](/help/sites-authoring/managing-pages.md#creating-a-new-folder)。

1. [為該資料夾設定允許的體驗片段範本](#configure-allowed-templates-folder)。

>[!NOTE]
>
>也可以為您的執行個體](#configure-allowed-templates-instance)設定[允許的範本，但此方法&#x200B;**不**&#x200B;建議使用，因為升級時會覆寫這些值。

### 設定資料夾的允許範本 {#configure-allowed-templates-folder}

>[!NOTE]
>
>這是指定&#x200B;**允許的範本**&#x200B;的建議方法，因為升級時不會覆寫這些值。

1. 導覽至必要的&#x200B;**體驗片段**&#x200B;資料夾。

1. 選取資料夾，然後選取&#x200B;**屬性**。

1. 在&#x200B;**允許的範本**&#x200B;欄位中，指定用於擷取所需範本的規則運算式。

   例如：
   `/conf/(.*)/settings/wcm/templates/experience-fragment(.*)?`

   請參閱：
   `http://localhost:4502/mnt/overlay/cq/experience-fragments/content/experience-fragments/folderproperties.html/content/experience-fragments/wknd`

   ![體驗片段屬性 — 允許的範本](/help/sites-authoring/assets/xf-folders-templates.png)

   >[!NOTE]
   >
   >如需詳細資訊，請參閱[體驗片段的範本](/help/sites-developing/experience-fragments.md#templates-for-experience-fragments)。

1. 選取&#x200B;**儲存並關閉**。

### 為您的執行個體設定允許的範本 {#configure-allowed-templates-instance}

>[!CAUTION]
>
>不建議使用此方法變更&#x200B;**允許的範本**，因為指定的範本在升級時會被覆寫。
>
>使用此對話方塊僅供參考。

1. 導覽至必要的&#x200B;**體驗片段**&#x200B;主控台。

1. 選取&#x200B;**組態選項**：

   ![設定按鈕](assets/ef-02.png)

1. 在&#x200B;**設定體驗片段**&#x200B;對話方塊中指定必要的範本：

   ![設定體驗片段](assets/ef-01.png)

   >[!NOTE]
   >
   >如需詳細資訊，請參閱[體驗片段的範本](/help/sites-developing/experience-fragments.md#templates-for-experience-fragments)。

1. 選取「**儲存**」。

## 建立體驗片段 {#creating-an-experience-fragment}

若要建立體驗片段：

1. 從全域導覽中選取體驗片段。

   ![xf-01](assets/xf-01.png)

1. 導覽至所需的資料夾，並選取&#x200B;**建立**。

   ![xf-02](assets/xf-02.png)

1. 選取&#x200B;**體驗片段**&#x200B;以開啟&#x200B;**建立體驗片段**&#x200B;精靈。

   依次選擇所需 **的範本**、下 **一步**:

   ![xf-03](assets/xf-03.png)

1. 輸入 **體驗****片段的屬性**。

   **標題**&#x200B;為必填。 如果&#x200B;**Name**&#x200B;留空，則會從&#x200B;**Title**&#x200B;衍生它。

   ![xf-04](assets/xf-04.png)

   >[!NOTE]
   >
   >體驗片段範本中的標籤不會與此體驗片段根頁面上的標籤合併。
   >
   >它們是完全獨立的。

1. 按一下&#x200B;**建立**。

   畫面會顯示訊息。 選取：

   * **完成**&#x200B;以返回主控台

   * **開啟**&#x200B;以開啟片段編輯器

## 編輯您的體驗片段 {#editing-your-experience-fragment}

體驗片段編輯器提供與一般頁面編輯器類似的功能。

>[!NOTE]
>
>如需如何使用頁面編輯器的詳細資訊，請參閱[編輯頁面內容](/help/sites-authoring/editing-content.md)。

下列範例程式說明如何建立產品的Teaser：

1. 從[元件瀏覽器](/help/sites-authoring/author-environment-tools.md#components-browser)拖放&#x200B;**Teaser**。

   ![xf-05](assets/xf-05.png)

1. 從元件工具列選取&#x200B;**[設定](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste)**。
1. 新增資 **產** ，並視需要 **定義屬性** 。
1. 使用&#x200B;**完成** （勾選圖示）確認定義。
1. 視需要新增更多元件。

## 建立體驗片段變數 {#creating-an-experience-fragment-variation}

您可以根據自己的需求，建立體驗片段的變數：

1. 開啟您的片段以進行[編輯](/help/sites-authoring/experience-fragments.md#editing-your-experience-fragment)。
1. 開啟&#x200B;**變數**&#x200B;標籤。

   ![xf-authoring-06](assets/xf-authoring-06.png)

1. **建立**&#x200B;可讓您建立：

   * **變異**
   * **變數為[即時副本](/help/sites-administering/msm.md#live-copies)**。

     >[!NOTE]
     >
     >將初始變數建立為Live Copy時，將會使用Live Copy Source作為主要變數來繼承標題。

1. 定義必要的屬性：

   * **範本**
   * **標題**
   * **名稱**；如果留空，將從「標題」衍生名稱
   * **說明**
   * **變數標籤**

   ![xf-06](assets/xf-06.png)

1. 使用&#x200B;**完成** （勾選圖示）確認，新的變數會顯示在面板中：

   ![xf-07](assets/xf-07.png)

## 使用您的體驗片段 {#using-your-experience-fragment}

您現在可以在編寫頁面時使用您的體驗片段：

1. 開啟任何頁面進行編輯。

   >[!NOTE]
   >
   >頁面必須以可編輯的範本為基礎。

   例如： [https://localhost:4502/editor.html/content/we-retail/language-masters/en/products/men.html](https://localhost:4502/editor.html/content/we-retail/language-masters/en/products/men.html)

1. 從元件瀏覽器將元件拖曳至頁面段落系統，建立體驗片段元件的例項：

   ![xf-08](assets/xf-08.png)

1. 將實際的體驗片段新增到元件例項；可以：

   * 從Assets瀏覽器拖曳所需的片段，並放置到元件上
   * 從元件工具列選取&#x200B;**設定**&#x200B;並指定要使用的片段，以&#x200B;**完成** （勾號）確認

   ![xf-09](assets/xf-09.png)

   >[!NOTE]
   >
   >元件工具列中的「編輯」可作為在片段編輯器中開啟片段的捷徑。

## 建置區塊 {#building-blocks}

您可以選取一或多個元件，以建立要在片段中回收的建置區塊：

### 建立建置區塊 {#creating-a-building-block}

若要建立建置區塊：

1. 在體驗片段編輯器中，選取您要重複使用的元件：

   ![xf-10](assets/xf-10.png)

1. 從元件工具列中選取&#x200B;**轉換成建置區塊**：

   ![xf-authoring-13-icon](assets/xf-authoring-13-icon.png)

1. 輸入建置塊的名 **稱**，並使用 **Convert確認**:

   ![xf-11](assets/xf-11.png)

1. **建置區塊**&#x200B;會顯示在索引標籤中，並可在段落系統中選取：

   ![xf-12](assets/xf-12.png)

#### 管理建置區塊 {#managing-a-building-block}

您的建置區塊會顯示在&#x200B;**建置區塊**&#x200B;標籤中。 對於每個區塊，都可使用下列動作：

* 前往主版：在新標籤中開啟根頁面變數
* 重新命名
* 刪除

![xf-13](assets/xf-13.png)

#### 使用建置區塊 {#using-a-building-block}

您可以將建置區塊拖曳至任何片段的段落系統，就像對任何元件一樣。

## 您的體驗片段的詳細資料 {#details-of-your-experience-fragment}

您可以檢視片段的詳細資訊：

1. 詳細資訊會顯示在&#x200B;**體驗片段**&#x200B;主控台的所有檢視中，其中&#x200B;**清單檢視**&#x200B;包含[匯出至Target](/help/sites-administering/experience-fragments-target.md)的詳細資訊：

   ![ef-03](assets/ef-03.png)

1. 當您開啟體驗片段的&#x200B;**屬性**&#x200B;時：

   ![ef-04](assets/ef-04.png)

   屬性位於各種標籤中：

   >[!CAUTION]
   >
   >當您從體驗片段主控台開啟&#x200B;**屬性**&#x200B;時，會顯示這些標籤。
   >
   >
   >如果您 **在編輯體驗片段時開啟屬性** ，則會顯示適當 [的頁面屬性](/help/sites-authoring/editing-page-properties.md) 。

   ![ef-05](assets/ef-05.png)

   * **基本**

      * **標題** — 必要

      * **說明**
      * **標籤**
      * **變體總數** — 僅供參考

      * **網路變體的數目** — 僅供參考
      * **非網路變數的數目** — 僅資訊&#x200B;**資訊**

      * **使用此片段的頁數** — 僅供參考

   * **Cloud Service**

      * **雲端設定**
      * **Cloud Service設定**
      * **Facebook頁面ID**
      * **Pinterest展示板**

   * **個參考**

      * 參考清單。

   * **社群媒體狀態**

      * 社群媒體變數的詳細資訊。

## 純HTML轉譯 {#the-plain-html-rendition}

使用URL中的`.plain.`選取器，您可以從瀏覽器存取純HTML轉譯。

>[!NOTE]
>
>雖然這可以直接從瀏覽器取得，但[主要目的是允許其他應用程式（例如協力廠商網頁應用程式、自訂行動實作）僅使用URL](/help/sites-developing/experience-fragments.md#the-plain-html-rendition)直接存取體驗片段的內容。

## 匯出體驗片段 {#exporting-experience-fragments}

依預設，體驗片段會以HTML格式傳送。 AEM和協力廠商管道均可使用此函式。

若要匯出至Adobe Target，也可以使用JSON。 如需完整資訊，請參閱[Target與體驗片段的整合](/help/sites-administering/experience-fragments-target.md)。
