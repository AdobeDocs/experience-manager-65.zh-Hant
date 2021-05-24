---
title: 使用內容片段進行頁面編寫
seo-title: 使用內容片段進行頁面編寫
description: AEM內容片段可讓您設計、建立、組織及使用不受頁面影響的內容
seo-description: AEM內容片段可讓您設計、建立、組織及使用不受頁面影響的內容
uuid: 987de428-8354-4b23-a552-3ea415122184
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 4049a7a5-4b33-4462-a25f-3c0daeb6a8a9
docset: aem65
exl-id: d5dad844-80ca-4ace-a082-38d892d9ffe2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 7%

---

# 使用內容片段進行頁面編寫{#page-authoring-with-content-fragments}

Adobe Experience Manager(AEM)內容片段會建 [立並管理為不受頁面影響的資產](/help/assets/content-fragments/content-fragments.md)。

它們可讓您建立管道中性內容，以及（可能是管道特定的）變化。 然後，您可以在編寫內容頁面時使用這些片段及其變體。

結構化內容片段與更新的JSON匯出工具一起，也可用來透過內容服務將AEM內容傳送至AEM頁面以外的管道。

>[!NOTE]
>
>**內容** 片段和 **[體驗](/help/sites-authoring/experience-fragments.md)** 片段是AEM內的不同功能：
>
>* **內容** 片段是編輯內容，主要是文字和相關影像。它們是純內容，沒有設計和佈局。
>* **體驗** 片段內容已完整規劃；網頁的片段。

>
>
體驗片段可以包含內容片段形式的內容，但不能以相反的方式。

>[!CAUTION]
>
>本頁面在介紹基本術語和概念以及建立和管理片段時，必須與[使用內容片段](/help/assets/content-fragments/content-fragments.md)（及相關頁面）一起閱讀。

內容片段可啟用：

* **行銷和行銷活動策略**

   * 透過集中管理的內容片段檢閱內容。

* **Creative Pro**

   * 透過與內容片段相關聯的集合追蹤創意資產。

* **複製寫入程式**

   * 在AEM內容片段編輯器中寫入。
   * 可以建立內容變數。
   * 可將相關內容與內容片段建立關聯。
   * 可以使用版本設定/工作流。
   * 可以共用內容片段。
   * 可集中管理翻譯。

* **製作人與歷程經理**

   * 在AEM中透過編寫從預先定義的片段和變異中選取。
   * 當複製撰寫人員和創意人員在集中管理的片段和資產中進行更新時，可以仰賴片段和相關內容隨時保持最新。
   * 可依賴組織的相關媒體內容來關聯。
   * 可以即時建立隨選內容變異，同時仍可確保這些變異在片段中保持集中管理。

## 新增內容片段至您的頁面{#adding-a-content-fragment-to-your-page}

1. 開啟您的頁面進行編輯。

1. 新增&#x200B;**內容片段**&#x200B;元件；從&#x200B;**元件**&#x200B;瀏覽器或&#x200B;**插入新元件**。

1. 您可以:

   * 開啟&#x200B;**Assets**&#x200B;瀏覽器，並篩選&#x200B;**內容片段**（預設為影像）。 然後將所需片段拖曳至元件例項。

   * 選取內容片段元件，然後從工具列選取&#x200B;**設定**。 在對話方塊中，您可以開啟選擇對話框以瀏覽並選擇所需的&#x200B;**內容片段**。
   >[!NOTE]
   >
   >另一種方法是直接將特定內容片段拖曳至頁面。 這會自動建立相關的元件（內容片段）。

1. 最初將顯示&#x200B;**Main**&#x200B;元素和&#x200B;**Master**（變化）中的內容。 您可以視需要選取其他元素和/或變異](#selecting-the-element-or-variation)。[

   ![cfm-6420-01](assets/cfm-6420-01.png)

   >[!NOTE]
   >
   >如需進一步編輯功能的詳細資訊，另請參閱：
   >
   >
   >
   >    * [回應式版面](/help/sites-authoring/responsive-layout.md)
   * [編輯頁面內容](/help/sites-authoring/editing-content.md)


### 選擇元素或變化{#selecting-the-element-or-variation}

開啟片段的&#x200B;**Configuration**&#x200B;對話方塊，以設定片段以用於目前頁面。 對話方塊取決於使用的元件。

在適當的設定對話方塊中，您可以選取可用的參數，包括：

* **內容片段**

   指定要使用的片段。

* **顯示模式**:

   * **單文字元素**

   * **多個元素**

* **元素**

   * 預設&#x200B;**Main**&#x200B;將始終可用。
   * 如果片段是使用適當的範本建立，則可使用選取項目。

   >[!NOTE]
   可用的元素取決於使用的範本。

* **變異**

   * 預設主 **版** (Master)將始終可用。
   * 如果已為片段建立變數，則會提供選取項目。

* **段落**:指定要包括的段落範圍：

   * **全部**
   * **範圍**:例如，  `1`,  `3-5`,  `9-*`

      * **將標題當作其段落的一部分來處理**

* **將標題當作其段落的一部分來處理**

### 快速連線至片段編輯器{#quick-connection-to-fragment-editor}

您可以使用元件工具列上的&#x200B;**Edit**&#x200B;圖示，開啟片段來源以進行編輯（資產）。 這可讓您[編輯及管理內容片段](/help/assets/content-fragments/content-fragments.md)。

>[!CAUTION]
和以往一樣，編輯片段來源會影響參考該內容片段的所有頁面。

### 在內容之間添加{#adding-in-between-content}

將特定內容片段新增至頁面時，片段的每個HTML段落（以及上/下）之間會有&#x200B;**拖曳元件至此處**&#x200B;預留位置。

這可讓您在中間（即內容之間）](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments)新增額外內容[，而無須變更根片段。

對於中間內容，您可以：

* 從[元件瀏覽器](/help/sites-authoring/author-environment-tools.md#components-browser)添加元件。
* 從[Assets瀏覽器](/help/sites-authoring/author-environment-tools.md#assets-browser)新增資產。
* 使用[關聯內容](#using-associated-content)作為中間內容的源。

>[!CAUTION]
中間內容是頁面內容。 它不會儲存在內容片段中。

![cfm-6420-02](assets/cfm-6420-02.png)

>[!NOTE]
您也可以[將視覺資產（影像）插入片段本身](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment)。
插入片段本身的視覺資產會附加至片段中的前一段。 這表示您無法在視覺資產與前一段之間放置內容。

>[!CAUTION]
將內容新增至頁面上的內容片段後，若變更基礎內容片段的結構（例如在內容片段編輯器中），可能會導致錯誤/非預期的結果。
發生此情況時，中間內容會保留為：
* 在片段流中的元件序列內具有絕對位置。 即使片段中的段落內容變更，此位置也不會變更。

這可以讓它看起來好像相對位置已改變，因為段落之間與它們位於旁邊的（片段）段落沒有關聯。
* 除非兩款結構相衝突；在這種情況下，不顯示中間內容（儘管它仍在內部存在）。



### 使用關聯內容{#using-associated-content}

如果您有 [與內容片段](/help/assets/content-fragments/content-fragments-assoc-content.md)[相關的內容](/help/assets/content-fragments/content-fragments.md) ，這些資產將可從側面板使用 (在您將片段放在內容頁面後)。關聯內容實際上是中間內容的特 [殊內容來源](#adding-in-between-content)。

>[!NOTE]
有各種方法可將[視覺資產（例如影像）](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)新增至片段和/或頁面。

>[!NOTE]
如果一個頁面上有多個內容片段，**關聯內容**&#x200B;標籤將顯示適合所有片段的資產。

將具有關聯內容的片段新增至頁面後，會在側面板中開啟新索引標籤（**關聯內容**）。

從這裡，您可以將資產拖曳至所需位置（拖曳至現有元件，或拖曳至將建立適當元件的必要位置）:

![cfm-6420-03](assets/cfm-6420-03.png)

### 插入片段{#assets-inserted-into-the-fragment}的資產

如果資產（例如影像）已插入片段本身，則頁面編輯器中編輯這些資產的選項有限。<!-- Removed link as it was a 404 on helpx -->

例如，對於影像，您可以

* 裁切、旋轉或翻轉影像。
* 新增標題或替代文字。
* 指定大小。
* 您也可以設定配置。

必須在片段編輯器中進行其他變更，例如移動、複製、刪除。

### 發佈 {#publishing}

片段必須發佈，才能用於已發佈的網頁上：

* 片段可在[在Assets控制台](/help/assets/content-fragments/content-fragments.md#publishingandreferencingafragment)中建立片段後發佈。
* 如果正在發佈的頁面上使用&#x200B;*未發佈的片段*，則此時也可以發佈片段。
