---
title: 將體驗片段匯出到 Adobe Target
seo-title: Exporting Experience Fragments to Adobe Target
description: 將體驗片段匯出到 Adobe Target
seo-description: Exporting Experience Fragments to Adobe Target
uuid: 2df0faab-5d5e-4fc1-93b3-28b7e6f3c306
contentOwner: carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d4152b4d-531b-4b62-8807-a5bc5afe94c6
docset: aem65
exl-id: f2921349-de8f-4bc1-afa2-aeace99cfc5c
source-git-commit: 88763b318e25efb16f61bc16530082877392c588
workflow-type: tm+mt
source-wordcount: '1553'
ht-degree: 1%

---

# 將體驗片段匯出到 Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>本頁上的某些功能需要應用程AEM序6.5.3.0（或更高版本）。
>
>6.5.3.0:
>
>* **外部化程式域** 的上界。
   >  **注：** 外部化程式域僅與發送到目標的體驗片段的內容相關，而不與諸如查看提供內容之類的元資料相關。
>
>6.5.2.0:
>
>* 可將體驗片段導出到以下任一組：
   >
   >   * 預設工作區。
   >   * 在雲配置中指定的命名工作區。
   >   * **注：** 導出到特定工作區需要「Adobe Target高級」。
>
>* 必AEM須 [與Adobe Target採用IMS.](/help/sites-administering/integration-target-ims.md)。
>
>AEM 6.5.0.0和6.5.1.0:
>
>* 「AEM體驗片段」(Experience Fragments)將導出到Adobe Target的預設工作區。
>* 必AEM須按照Adobe Target [與Adobe Target整合](/help/sites-administering/target.md)。


可以導出 [體驗片段](/help/sites-authoring/experience-fragments.md)，建立於Adobe Experience Manager(AEM)，建立至Adobe Target（目標）。 然後，它們可以用作目標活動中的優惠，以test和個性化規模體驗。

有三種格式選項可用於將體驗片段導出到Adobe Target:

* HTML（預設）:支援Web和混合內容交付
* JSON:支援無頭內容交付
* HTML 和 JSON

可AEM以將「體驗片段」導出到Adobe Target的預設工作區，或導出到Adobe Target的用戶定義的工作區。 這是使用Adobe Developer控制台完成的，AEM必須 [與Adobe Target採用IMS.](/help/sites-administering/integration-target-ims.md)。

>[!NOTE]
>
>Adobe Target工作區在Adobe Target本身不存在。 它們在Adobe IMS(Identity Management系統)中定義和管理，然後使用來自Adobe Developer控制台的整合在解決方案中選擇使用。

>[!NOTE]
>
>Adobe Target工作區可用於僅允許組織（組）的成員建立和管理此組織的聘用和活動；不允許其他用戶訪問。 例如，全球關注的具體國家組織。

>[!NOTE]
>
>有關詳細資訊，請參閱：
>
>* [Adobe Target開發](https://www.adobe.io/apis/experiencecloud/target.html)
>* [核心元件 — 體驗片段](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/experience-fragment.html)
>


## 必備條件 {#prerequisites}

>[!CAUTION]
>
>此頁上的某些功能需要應用程AEM序6.5.3.0。

需要執行以下各種操作：

1. 你必須 [使AEM用IMS與Adobe Target整合](/help/sites-administering/integration-target-ims.md)。
2. 從作者實例導出AEM「體驗片段」，因此您需要 [配置鏈AEM接外部化程式](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer) 在作者實例上，以確保將體驗片段中的任何引用外部化以用於Web傳遞。

   >[!NOTE]
   >
   >對於預設不覆蓋的連結重寫， [體驗片段連結重寫器提供程式](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) 的子菜單。 利用此功能，可以為實例開發自定義規則。

## 添加雲配置 {#add-the-cloud-configuration}

導出片段之前，需要添加 **雲配置** 為 **Adobe Target** 資料夾。 這還允許您：

* 指定要用於導出的格式選項
* 選擇目標工作區作為目標
* 選擇外部化程式域以重寫「體驗片段」中的引用（可選）

可在中選擇所需選項 **頁面屬性** 資料夾和/或片段；將根據需要繼承規範。

1. 導航到 **體驗片段** 控制台。

1. 開啟 **頁面屬性** 資料夾或檔案段。

   >[!NOTE]
   >
   >如果將雲配置添加到「體驗片段」父資料夾，則所有子資料夾都繼承該配置。
   >
   >
   >如果將雲配置添加到體驗片段本身，則所有變數都會繼承該配置。

1. 選擇 **Cloud Services** 頁籤。

1. 下 **Cloud Service配置**&#x200B;選中 **Adobe Target** 從下拉清單中。

   >[!NOTE]
   >
   >可以自定義體驗片段提供的JSON格式。 要執行此操作，請定義客戶體驗片段元件，然後注釋如何在元件Sling模型中導出其屬性。
   >
   >請參閱核心元件：
   >
   >[核心元件 — 體驗片段](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/experience-fragment.html)

   下 **Adobe Target** 選擇：

   * 適當的配置
   * 所需格式選項
   * Adobe Target工作區
   * 如果需要 — 外部化程式域

   >[!CAUTION]
   >
   >外部化器域是可選的。
   >
   >當希AEM望導出的內容指向特定內容時，將配置外部化器 *發佈* 。 有關詳細資訊，請參閱 [配置鏈AEM接外部化器](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer)。
   >
   >另請注意，外部化程式域僅與發送到目標的體驗片段的內容相關，而不與元資料（如查看服務內容）相關。

   例如，對於資料夾：

   ![資料夾 — Cloud Services](assets/xf-target-integration-01.png "資料夾 — Cloud Services")

1. **儲存並關閉**.

## 將體驗片段輸出到Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>對於介質資產（如影像），只有引用會導出到目標。 資產本身仍保存在AEM Assets，並從發佈實例AEM交付。
>
>因此，在導出到目標之前，需要發佈包含所有相關資產的「體驗」片段。

要將體驗片段從導AEM出到目標（指定雲配置後）:

1. 導航到「體驗片段」控制台。
1. 選擇要導出到目標的體驗片段。

   >[!NOTE]
   >
   >它必須是體驗片段網頁變體。

1. 點擊/按一下 **對Adobe Target的出口**。

   >[!NOTE]
   >
   >如果已導出體驗片段，請選擇 **更新Adobe Target**。

1. 點擊/按一下 **導出而不發佈** 或 **發佈** 按需要。

   >[!NOTE]
   >
   >選擇 **發佈** 將立即發佈體驗片段並將其發送到目標。

1. 點擊/按一下 **確定** 的子菜單。

   您的體驗片段現在應位於目標中。

   >[!NOTE]
   >
   >[各種詳細資訊](/help/sites-authoring/experience-fragments.md#details-of-your-experience-fragment) 可在 **清單視圖** 控制台和 **屬性**。

   >[!NOTE]
   >
   >在Adobe Target觀看體驗片段時， *上次修改* 可見的日期是上次修改片段的日期AEM，而不是上次將片段導出到Adobe Target的日期。

>[!NOTE]
>
>或者，也可以使用 [頁面資訊](/help/sites-authoring/author-environment-tools.md#page-information) 的子菜單。

## 用你在Adobe Target的經驗片段 {#using-your-experience-fragments-in-adobe-target}

執行上述任務後，體驗片段將顯示在「目標」中的「優惠」頁上。 請看 [特定目標文檔](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html) 瞭解你能在那裡取得什麼成就。

>[!NOTE]
>
>在Adobe Target觀看體驗片段時， *上次修改* 可見的日期是上次修改片段的日期AEM，而不是上次將片段導出到Adobe Target的日期。

## 刪除已導出到Adobe Target的體驗片段 {#deleting-an-experience-fragment-already-exported-to-adobe-target}

如果刪除已導出到目標的體驗片段，則如果該片段已在目標中的優惠中使用，則可能會導致問題。 如果刪除片段，則當片段內容由傳遞時，將導致提供不可用AEM。

為避免此類情況：

* 如果活動中當前未使用體驗片段，則AEM允許用戶刪除該片段而不顯示警告消息。
* 如果「目標」中的活動當前正在使用「體驗片段」，則會出現一條錯誤消息AEM，警告用戶刪除該片段可能對活動造成的後果。

   中的錯誤AEM消息不禁止用戶（強制）刪除體驗片段。 如果刪除了「體驗」片段：

   * 具有經驗片段的目AEM標產品可能顯示不期望的行為

      * 隨著將「體驗片段」HTML推到「目標」，此報價可能仍將呈現
      * 如果中也刪除了引用的資產，則「體驗」片段中的任何引用可能AEM無法正確工作。
   * 當然，對經驗片段的任何進一步修改都是不可能的，因為經驗片段在中已不存AEM在。



## 從導出到目標的體驗片段中刪除ClientLibs {#removing-clientlibs-from-fragments-exported-target}

「體驗片段」包含完整的html標籤和所有必要的客戶端庫(CSS/JS)，以完全按照「體驗片段內容作者」建立的內容呈現片段。 這是副設計。

當在由提供的頁面上與Adobe Target一起使用體驗片段AEM時，目標頁面已包含所有必要的客戶端庫。 此外，也不需要「體驗片段」服務中的無關html（請參見） [注意事項](#considerations))。

以下是體驗片段提供中html的偽示例：

```html
<!DOCTYPE>
<html>
   <head>
      <title>…</title>
      <!-- all of the client libraries (css/js) -->
      …
   </head>
   <body>
        <!--/* Actual XF Offer content would appear here... */-->
   </body>
</html>
```

在高級別，當將體驗AEM片段導出到Adobe Target時，它會使用多個附加的Sling選擇器。 例如，導出的體驗片段的URL可能如下所示(注意 `nocloudconfigs.atoffer`):

* http://www.your-aem-instance.com/content/experience-fragments/my-offers/my-xf-offer.nocloudconfigs.atoffer.html

的 `nocloudconfigs` 選擇器是通過使用HTL定義的，可通過從以下位置複製它來覆蓋：

* /libs/cq/experience-fragments/components/xfpage/nocloudconfigs.html

的 `atoffer` 選擇器實際應用後處理 [斯林重寫器](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html)。 可以使用它們刪除客戶端庫。

### 範例 {#example}

為此，我們將說明如何 `nocloudconfigs`。

>[!NOTE]
>
>請參閱 [可編輯模板](/help/sites-developing/templates.md#editable-templates) 的上界。

#### 覆蓋 {#overlays}

在本例中， [重疊](/help/sites-developing/overlays.md) 將刪除客戶端庫 *和* 無關的html。 假定您已建立「體驗片段模板類型」。 需要從中複製的必要檔案 `/libs/cq/experience-fragments/components/xfpage/` 包括：

* `nocloudconfigs.html`
* `head.nocloudconfigs.html`
* `body.nocloudconfigs.html`

#### 模板類型覆蓋 {#template-type-overlays}

在本示例中，我們將使用以下結構：

![模板類型覆蓋](assets/xf-target-integration-02.png "模板類型覆蓋")

這些檔案的內容如下：

* `body.nocloudconfigs.html`

   ![body.nocloudconfigs.html](assets/xf-target-integration-03.png "body.nocloudconfigs.html")

* `head.nocloudconfigs.html`

   ![head.nocloudconfigs.html](assets/xf-target-integration-04.png "head.nocloudconfigs.html")

* `nocloudconfigs.html`

   ![nocloudconfigs.html](assets/xf-target-integration-05.png "nocloudconfigs.html")

>[!NOTE]
>
>要使用 `data-sly-unwrap` 刪除所需的body標籤 `nocloudconfigs.html`。

### 考量事項 {#considerations}

如果您需要在Adobe Target使用AEM體驗片段AEM產品同時支援站點和非站點，則需要建立兩個體驗片段（兩種不同的模板類型）:

* 一個具有覆蓋功能以刪除客戶端/額外html

* 沒有覆蓋，因此包括所需客戶端的