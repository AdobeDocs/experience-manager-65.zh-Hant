---
title: 體驗片段
seo-title: 體驗片段
description: 體驗片段
seo-description: 'null'
uuid: 9a1d12ef-5690-4a2e-8635-a710775efa39
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 4c5b52c3-5e23-4125-9306-48bf2ded23cb
docset: aem65
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1398'
ht-degree: 9%

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
* 支援無頭CMS使用案例。 作者只想AEM用於製作，但不想用於交付給客戶。 協力廠商系統／觸點會使用該體驗，然後傳送給使用者。

>[!NOTE]
>
>體驗片段的寫入存取權要求使用者帳戶必須註冊在群組中：
>
>    `experience-fragments-editors`
如果您遇到任何問題，請聯絡您的系統管理員。

## 何時應使用體驗片段？{#when-should-you-use-experience-fragments}

應使用體驗片段：

* 無論何時您想要重複使用體驗。

   * 可重複使用相同或類似內容的體驗

* 當您用作AEM協力廠商的內容傳送平台時。

   * 任何想要用作內容AEM傳送平台的解決方案
   * 將內容內嵌至協力廠商觸點

* 如果您有「體驗」，但有不同的變化或轉譯。

   * 頻道或內容特定變化
   * 對群組有意義的體驗（例如跨通道具有不同體驗的促銷活動）

* 當您使用全通道商務時。

   * 在[社交媒體](/help/sites-developing/experience-fragments.md#social-variations)頻道上大規模分享商務相關內容
   * 讓觸點成為交易性

## 組織您的體驗片段{#organizing-your-experience-fragments}

建議您：
* 使用資料夾來組織您的體驗片段，

* [在這些資料夾上設定允許的範本](#configure-allowed-templates-folder)。

建立資料夾允許您：

* 為您的體驗片段建立有意義的結構；例如，根據分類

   >[!NOTE]
   您不需要將體驗片段的結構與網站的頁面結構對齊。

* [在資料夾級別分配允許的模板](#configure-allowed-templates-folder)

   >[!NOTE]
   您可以使用[範本編輯器](/help/sites-authoring/templates.md)來建立您自己的範本。

WKND專案會根據`Contributors`建構一些體驗片段。 使用的結構也說明如何使用其他功能，例如多網站管理（包括語言副本）。

請參閱：

`http://localhost:4502/aem/experience-fragments.html/content/experience-fragments/wknd/language-masters/en/contributors/kumar-selveraj/master`

![體驗片段的資料夾](/help/sites-authoring/assets/xf-folders.png)

## 為體驗片段建立和設定資料夾{#creating-and-configuring-a-folder-for-your-experience-fragments}

若要建立並設定您的體驗片段資料夾，建議您：

1. [建立資料夾](/help/sites-authoring/managing-pages.md#creating-a-new-folder)。

1. [設定該資料夾允許的體驗片段範本](#configure-allowed-templates-folder)。

>[!NOTE]
您也可以為實例](#configure-allowed-templates-instance)配置[允許的模板，但建議使用&#x200B;**not**&#x200B;方法，因為升級時可以覆蓋值。

### 配置資料夾{#configure-allowed-templates-folder}的允許模板

>[!NOTE]
這是指定&#x200B;**允許範本**&#x200B;的建議方法，因為升級時不會覆寫值。

1. 導覽至所需的&#x200B;**體驗片段**&#x200B;資料夾。

1. 選擇資料夾，然後選擇&#x200B;**屬性**。

1. 在&#x200B;**允許的範本**&#x200B;欄位中，指定擷取所需範本的規則運算式。

   例如：
   `/conf/(.*)/settings/wcm/templates/experience-fragment(.*)?`

   請參閱：
   `http://localhost:4502/mnt/overlay/cq/experience-fragments/content/experience-fragments/folderproperties.html/content/experience-fragments/wknd`

   ![體驗片段屬性——允許的範本](/help/sites-authoring/assets/xf-folders-templates.png)

   >[!NOTE]
   如需詳細資訊，請參閱[體驗片段範本](/help/sites-developing/experience-fragments.md#templates-for-experience-fragments)。

1. 選擇&#x200B;**保存並關閉**。

### 配置實例{#configure-allowed-templates-instance}的允許模板

>[!CAUTION]
建議不要使用此方法更改&#x200B;**允許的模板**，因為指定的模板可以在升級時被覆蓋。
請僅供參考之用。

1. 導覽至所需的&#x200B;**體驗片段**&#x200B;主控台。

1. 選擇&#x200B;**配置選項**:

   ![「配置」按鈕](assets/ef-02.png)

1. 在&#x200B;**設定體驗片段**&#x200B;對話方塊中指定所需範本：

   ![設定體驗片段](assets/ef-01.png)

   >[!NOTE]
   如需詳細資訊，請參閱[體驗片段範本](/help/sites-developing/experience-fragments.md#templates-for-experience-fragments)。

1. 選擇&#x200B;**保存**。

## 建立體驗片段{#creating-an-experience-fragment}

若要建立體驗片段：

1. 從全域導覽中選取「體驗片段」。

   ![xf-01](assets/xf-01.png)

1. 導航到所需資料夾並選擇&#x200B;**建立**。

   ![xf-02](assets/xf-02.png)

1. 選擇&#x200B;**體驗片段**&#x200B;以開啟&#x200B;**建立體驗片段**&#x200B;精靈。

   依次選擇所需 **的範本**、下 **一步**:

   ![xf-03](assets/xf-03.png)

1. 輸入 **體驗****片段的屬性**。

   **Title**&#x200B;是必填的。 如果&#x200B;**Name**&#x200B;保留為空白，則它將從&#x200B;**Title**&#x200B;派生。

   ![xf-04](assets/xf-04.png)

1. 按一下&#x200B;**建立**。

   將顯示一條消息。 選取:

   * **** Doneto返回控制台

   * **打** 開片段編輯器

## 編輯體驗片段{#editing-your-experience-fragment}

體驗片段編輯器提供與一般頁面編輯器類似的功能。

>[!NOTE]
如需如何使用頁面編輯器的詳細資訊，請參閱[編輯頁面內容](/help/sites-authoring/editing-content.md)。

以下示例過程說明如何為產品建立摘要：

1. 從[元件瀏覽器](/help/sites-authoring/author-environment-tools.md#components-browser)拖放&#x200B;**摘要**。

   ![xf-05](assets/xf-05.png)

1. 從元件工具欄中選擇&#x200B;**[Configure](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste)**。
1. 新增資 **產** ，並視需要 **定義屬性** 。
1. 使用&#x200B;**Done**（勾選圖示）確認定義。
1. 視需要新增更多元件。

## 建立體驗片段變數{#creating-an-experience-fragment-variation}

您可以根據您的需求，建立不同的體驗片段：

1. 開啟[編輯](/help/sites-authoring/experience-fragments.md#editing-your-experience-fragment)的片段。
1. 開啟&#x200B;**Valuations**&#x200B;標籤。

   ![xf-authoring-06](assets/xf-authoring-06.png)

1. **Create** 可讓您建立：

   * **變異**
   * **變數為 live-copy**.

1. 定義所需屬性：

   * **範本**
   * **標題**
   * **名稱**;如果保留空白，則會從「標題」衍生
   * **說明**
   * **變數標記**

   ![xf-08](assets/xf-06.png)

1. 使用&#x200B;**Done**（勾選圖示）確認，新變數將會顯示在面板中：

   ![xf-07](assets/xf-07.png)

## 使用體驗片段{#using-your-experience-fragment}

您現在可以在編寫頁面時使用體驗片段：

1. 開啟任何頁面進行編輯。

   例如：[https://localhost:4502/editor.html/content/we-retail/language-masters/en/products/men.html](https://localhost:4502/editor.html/content/we-retail/language-masters/en/products/men.html)

1. 將元件從「元件」瀏覽器拖曳至頁面段落系統，以建立「體驗片段」元件的例項：

   ![xf-08](assets/xf-08.png)

1. 將實際的體驗片段新增至元件例項；其中：

   * 從「資產瀏覽器」拖曳必要片段至元件
   * 從元件工具欄中選擇&#x200B;**配置**&#x200B;並指定要使用的片段，使用&#x200B;**Done**（勾選）確認

   ![xf-09](assets/xf-09.png)

   >[!NOTE]
   在元件工具列中，編輯會以捷徑方式在片段編輯器中開啟片段。

## 建置區塊 {#building-blocks}

您可以選取一或多個元件，以建立要在片段內回收的建置區塊：

### 建立構建塊{#creating-a-building-block}

要建立新的構建塊：

1. 在「體驗片段」編輯器中，選取您要重複使用的元件：

   ![xf-10](assets/xf-10.png)

1. 從元件工具欄中，選擇&#x200B;**轉換到構建塊**:

   ![xf-authoring-13-icon](assets/xf-authoring-13-icon.png)

1. 輸入建置塊的名 **稱**，並使用 **Convert確認**:

   ![xf-11](assets/xf-11.png)

1. 建 **立區塊** (Building Block)將顯示在頁籤中，並可在段落系統中選擇：

   ![xf-12](assets/xf-12.png)

#### 管理構建塊{#managing-a-building-block}

您的構建塊在&#x200B;**構建塊**&#x200B;頁籤中可見。 對於每個塊，可以執行以下操作：

* 前往主版:在新標籤中開啟主變數
* 重新命名
* 刪除

![xf-13](assets/xf-13.png)

#### 使用構建塊{#using-a-building-block}

您可以將構建塊拖動到任何片段的段落系統，如同任何元件。

## 體驗片段{#details-of-your-experience-fragment}的詳細資訊

您可以查看您片段的詳細資訊：

1. 詳細資訊會顯示在&#x200B;**Experience Fragments**&#x200B;主控台的所有檢視中，**清單檢視**&#x200B;包含匯出至Target](/help/sites-administering/experience-fragments-target.md)的詳細資訊：[

   ![ef-03](assets/ef-03.png)

1. 當您開啟體驗片段的&#x200B;**屬性**&#x200B;時：

   ![ef-04](assets/ef-04.png)

   這些屬性可用於各種頁籤：

   >[!CAUTION]
   當您從「體驗片段」主控台開啟「屬性」****&#x200B;時，會顯示這些標籤。
   如果您 **在編輯體驗片段時開啟屬性** ，則會顯示適當 [的頁面屬性](/help/sites-authoring/editing-page-properties.md) 。

   ![ef-05](assets/ef-05.png)

   * **基本**

      * **標題** -強制

      * **說明**
      * **標記**
      * **變數總數** -僅提供資訊

      * **Web變體數** -僅提供資訊
      * **非Web變數的數目** -僅&#x200B;**提供資訊**

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




## 純HTML轉譯{#the-plain-html-rendition}

使用URL中的`.plain.`選擇器，您可以從瀏覽器存取純HTML轉譯。

>[!NOTE]
雖然這可直接從瀏覽器取得，但[主要用途是允許其他應用程式（例如協力廠商網頁應用程式、自訂行動裝置實作）直接存取體驗片段的內容，只使用URL](/help/sites-developing/experience-fragments.md#the-plain-html-rendition)。

## 匯出體驗片段{#exporting-experience-fragments}

依預設，體驗片段會以HTML格式傳送。 這可同時供第三方通AEM道使用。

若要匯出至Adobe Target，也可使用JSON。 如需完整資訊，請參閱[與體驗片段整合的目標](/help/sites-administering/experience-fragments-target.md)。
