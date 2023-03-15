---
title: 體驗片段
seo-title: Experience Fragments
description: 體驗片段
seo-description: null
uuid: 9a1d12ef-5690-4a2e-8635-a710775efa39
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 4c5b52c3-5e23-4125-9306-48bf2ded23cb
docset: aem65
exl-id: 1ff9ac47-9a3a-4a4e-8af8-bc73048e0409
source-git-commit: 2f635d5c856b35794ef2d62c15bc7cf4f4e57773
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 8%

---

# 體驗片段{#experience-fragments}

體驗片段是一或多個元件的群組，包括可在頁面中參照的內容和版面。 它們可包含任何元件。

體驗片段：

* 是體驗（頁面）的一部分。
* 可用於多個頁面。
* 以範本為基礎（僅可編輯），以定義結構和元件。
* 此範本用於建立 *根頁面* 體驗片段的。
* 由段落系統中的一個或多個元件（具有佈局）組成。
* 可包含其他體驗片段。
* 可與其他元件（包括其他體驗片段）結合，以形成完整的頁面（體驗）。
* 可以根據根頁面建立一或多個變異。
* 這些變化可能會共用內容和/或元件。
* 可劃分為可跨片段的多個變數使用的建立區塊。

您可以使用體驗片段：

* 如果作者想要重複使用頁面的部分（體驗的片段），則需要複製並貼上該片段。 建立和維護這些複製/貼上體驗非常耗時，且容易發生使用者錯誤。 體驗片段不需要複製/貼上。
* 支援無頭式CMS使用案例。 作者只想使用AEM進行製作，而不想提供給客戶。 協力廠商系統/接觸點會使用該體驗，然後傳送給使用者。

>[!NOTE]
>
>體驗片段的寫入存取權要求使用者帳戶須在群組中註冊：
>
>    `experience-fragments-editors`
如果您遇到任何問題，請與系統管理員聯繫。

## 何時該使用體驗片段？ {#when-should-you-use-experience-fragments}

該使用體驗片段的情況：

* 每當您想要重複使用體驗時。

   * 將透過相同或類似內容重複使用的體驗

* 當您使用AEM作為協力廠商的內容傳遞平台時。

   * 任何想使用AEM作為內容傳遞平台的解決方案
   * 將內容嵌入第三方接觸點

* 如果您的體驗有不同的變體或轉譯。

   * 管道或內容特定變數
   * 對群組有意義的體驗（例如跨管道具有不同體驗的促銷活動）

* 使用全通路商務時。

   * 共用商務相關內容於 [社交媒體](/help/sites-developing/experience-fragments.md#social-variations) 大規模通道
   * 將接觸點設為交易式

## 組織您的體驗片段 {#organizing-your-experience-fragments}

建議您：
* 使用資料夾來組織您的體驗片段，

* [在這些資料夾上配置允許的模板](#configure-allowed-templates-folder).

建立資料夾可讓您：

* 為您的體驗片段建立有意義的結構；例如，根據分類

   >[!NOTE]
   不需要將體驗片段的結構與網站的頁面結構對齊。

* [在資料夾層級分配允許的範本](#configure-allowed-templates-folder)

   >[!NOTE]
   您可以使用 [範本編輯器](/help/sites-authoring/templates.md) 來建立自己的範本。

WKND專案會根據 `Contributors`. 使用的結構也說明如何使用其他功能，例如多網站管理（包括語言副本）。

請參閱：

`http://localhost:4502/aem/experience-fragments.html/content/experience-fragments/wknd/language-masters/en/contributors/kumar-selveraj/master`

![體驗片段的資料夾](/help/sites-authoring/assets/xf-folders.png)

## 建立和設定體驗片段的資料夾 {#creating-and-configuring-a-folder-for-your-experience-fragments}

若要建立和設定體驗片段的資料夾，建議您：

1. [建立資料夾](/help/sites-authoring/managing-pages.md#creating-a-new-folder).

1. [設定該資料夾允許的體驗片段範本](#configure-allowed-templates-folder).

>[!NOTE]
您也可以設定 [允許的執行個體範本](#configure-allowed-templates-instance)，但此方法 **not** 建議使用，因為值可在升級時覆寫。

### 為資料夾配置允許的模板 {#configure-allowed-templates-folder}

>[!NOTE]
這是指定 **允許的範本**，因為升級時不會覆寫值。

1. 導覽至所需 **體驗片段** 檔案夾。

1. 選取資料夾，然後 **屬性**.

1. 指定用於擷取 **允許的範本** 欄位。

   例如：
   `/conf/(.*)/settings/wcm/templates/experience-fragment(.*)?`

   請參閱：
   `http://localhost:4502/mnt/overlay/cq/experience-fragments/content/experience-fragments/folderproperties.html/content/experience-fragments/wknd`

   ![體驗片段屬性 — 允許的範本](/help/sites-authoring/assets/xf-folders-templates.png)

   >[!NOTE]
   請參閱 [體驗片段的範本](/help/sites-developing/experience-fragments.md#templates-for-experience-fragments) 以取得詳細資訊。

1. 選擇 **儲存並關閉**.

### 為執行個體設定允許的範本 {#configure-allowed-templates-instance}

>[!CAUTION]
不建議變更 **允許的範本** 此方法可讓您在升級時覆寫指定的範本，
請使用此對話框僅供參考。

1. 導覽至所需 **體驗片段** 控制台。

1. 選擇 **配置選項**:

   ![配置按鈕](assets/ef-02.png)

1. 在 **設定體驗片段** 對話框：

   ![設定體驗片段](assets/ef-01.png)

   >[!NOTE]
   請參閱 [體驗片段的範本](/help/sites-developing/experience-fragments.md#templates-for-experience-fragments) 以取得詳細資訊。

1. 選取&#x200B;**儲存**。

## 建立體驗片段 {#creating-an-experience-fragment}

若要建立體驗片段：

1. 從全域導覽中選取體驗片段。

   ![xf-01](assets/xf-01.png)

1. 導覽至所需資料夾，然後選取 **建立**.

   ![xf-02](assets/xf-02.png)

1. 選擇 **體驗片段** 開啟 **建立體驗片段** 嚮導。

   依次選擇所需 **的範本**、下 **一步**:

   ![xf-03](assets/xf-03.png)

1. 輸入 **體驗****片段的屬性**。

   A **標題** 為必填。 若 **名稱** 保留為空白，則會從中衍生 **標題**.

   ![xf-04](assets/xf-04.png)

   >[!NOTE]
   來自體驗片段範本的標籤不會與此體驗片段根頁面上的標籤合併。
   這些是完全不同的。

1. 按一下&#x200B;**建立**。

   將顯示一條消息。 選取:

   * **完成** 返回控制台

   * **開啟** 開啟片段編輯器

## 編輯體驗片段 {#editing-your-experience-fragment}

體驗片段編輯器提供與一般頁面編輯器類似的功能。

>[!NOTE]
請參閱 [編輯頁面內容](/help/sites-authoring/editing-content.md) 以取得如何使用頁面編輯器的詳細資訊。

以下范常式式說明如何為產品建立預告：

1. 拖放 **Teaser** 從 [元件瀏覽器](/help/sites-authoring/author-environment-tools.md#components-browser).

   ![xf-05](assets/xf-05.png)

1. 選擇 **[設定](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste)** （從元件工具欄）。
1. 新增資 **產** ，並視需要 **定義屬性** 。
1. 使用確認定義 **完成** （勾選圖示）。
1. 視需要新增更多元件。

## 建立體驗片段變異 {#creating-an-experience-fragment-variation}

您可以根據您的需求建立體驗片段的變體：

1. 開啟您的片段 [編輯](/help/sites-authoring/experience-fragments.md#editing-your-experience-fragment).
1. 開啟 **變異** 標籤。

   ![xf-authoring-06](assets/xf-authoring-06.png)

1. **建立** 可讓您建立：

   * **變異**
   * **[變數為 live-copy](/help/sites-administering/msm.md#live-copies)**.

1. 定義所需的屬性：

   * **範本**
   * **標題**
   * **名稱**;若保留為空白，則從標題衍生
   * **說明**
   * **變數標記**

   ![xf-06](assets/xf-06.png)

1. 確認為 **完成** （勾選圖示），新變數會顯示在面板中：

   ![xf-07](assets/xf-07.png)

## 使用您的體驗片段 {#using-your-experience-fragment}

編寫頁面時，您現在可以使用體驗片段：

1. 開啟任何頁面進行編輯。

   例如： [https://localhost:4502/editor.html/content/we-retail/language-masters/en/products/men.html](https://localhost:4502/editor.html/content/we-retail/language-masters/en/products/men.html)

1. 從「元件」瀏覽器拖曳元件至頁面段落系統，建立體驗片段元件的例項：

   ![xf-08](assets/xf-08.png)

1. 將實際的體驗片段新增至元件例項；其中之一：

   * 從「資產瀏覽器」拖曳所需片段，並拖放至元件
   * 選擇 **設定** 從元件工具列中，並指定要使用的片段，請使用確認 **完成** （滴答）

   ![xf-09](assets/xf-09.png)

   >[!NOTE]
   在元件工具列中，編輯作為在片段編輯器中開啟片段的捷徑。

## 建置區塊 {#building-blocks}

您可以選取一或多個元件，以建立要在片段內回收的建置區塊：

### 建立建置區塊 {#creating-a-building-block}

要建立新的構建塊：

1. 在體驗片段編輯器中，選取您要重新使用的元件：

   ![xf-10](assets/xf-10.png)

1. 從元件工具欄中，選擇 **轉換為建置區塊**:

   ![xf-authoring-13-icon](assets/xf-authoring-13-icon.png)

1. 輸入建置塊的名 **稱**，並使用 **Convert確認**:

   ![xf-11](assets/xf-11.png)

1. 建 **立區塊** (Building Block)將顯示在頁籤中，並可在段落系統中選擇：

   ![xf-12](assets/xf-12.png)

#### 管理建置區塊 {#managing-a-building-block}

您的建置區塊會顯示在 **建置區塊** 標籤。 對於每個區塊，可使用下列動作：

* 轉到主版：在新索引標籤中開啟根頁面變異
* 重新命名
* 刪除

![xf-13](assets/xf-13.png)

#### 使用建置區塊 {#using-a-building-block}

您可以將建置區塊拖曳至任何片段的段落系統，如同任何元件。

## 體驗片段的詳細資訊 {#details-of-your-experience-fragment}

您可以看到片段的詳細資訊：

1. 詳細資料會顯示在 **體驗片段** 主控台，搭配 **清單檢視** 包括 [匯出至Target](/help/sites-administering/experience-fragments-target.md):

   ![ef-03](assets/ef-03.png)

1. 當您開啟 **屬性** 體驗片段的：

   ![ef-04](assets/ef-04.png)

   屬性可在各種標籤中使用：

   >[!CAUTION]
   這些標籤會在您開啟 **屬性** 從體驗片段主控台。
   如果您 **在編輯體驗片段時開啟屬性** ，則會顯示適當 [的頁面屬性](/help/sites-authoring/editing-page-properties.md) 。

   ![ef-05](assets/ef-05.png)

   * **基本**

      * **標題** 必填

      * **說明**
      * **標記**
      * **變體總數**  — 僅資訊

      * **Web變體數**  — 僅資訊
      * **非Web變體的數量** -inf **僅限**

      * **使用此片段的頁數**  — 僅資訊
   * **雲端服務**

      * **雲端設定**
      * **雲端服務設定**
      * **Facebook 頁面 ID**
      * **Pinterest Board**
   * **引用**

      * 參考清單。
   * **社交媒體狀態**

      * 社交媒體變異的詳細資訊。




## 純HTML轉譯 {#the-plain-html-rendition}

使用 `.plain.` 選取器，您可以從瀏覽器存取純HTML轉譯。

>[!NOTE]
雖然這可直接從瀏覽器取得， [主要用途是允許其他應用程式（例如協力廠商網頁應用程式、自訂行動實作）僅使用URL直接存取體驗片段的內容](/help/sites-developing/experience-fragments.md#the-plain-html-rendition).

## 匯出體驗片段 {#exporting-experience-fragments}

依預設，體驗片段會以HTML格式傳送。 AEM和協力廠商管道皆可使用。

若要匯出至Adobe Target，也可以使用JSON。 請參閱 [Target與體驗片段整合](/help/sites-administering/experience-fragments-target.md) 以取得完整資訊。
