---
title: 自訂和擴充內容片段
description: 內容片段可擴充標準資產。 瞭解如何自訂。
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 08c88e70-4df9-4627-8a66-1fabe3aee50b
solution: Experience Manager, Experience Manager Sites
feature: Content Fragments
role: Developer
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '2728'
ht-degree: 1%

---


# 自訂和擴充內容片段{#customizing-and-extending-content-fragments}

內容片段可擴充標準資產；請參閱：

* [建立和管理內容片段](/help/assets/content-fragments/content-fragments.md)以及使用內容片段進行[頁面製作](/help/sites-authoring/content-fragments.md)，以取得有關內容片段的進一步資訊。

* [管理Assets](/help/assets/manage-assets.md)和[自訂及擴充Assets](/help/assets/extending-assets.md)，以取得有關標準資產的進一步資訊。

## 架構 {#architecture}

內容片段的基本[組成部分](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)為：

* *內容片段，*
* 包含一個或多個&#x200B;*內容元素*，
* 而且可以有一或多個&#x200B;*內容變數*。

視片段型別而定，也會使用模型或範本：

>[!CAUTION]
>
>建議使用[內容片段模型](/help/assets/content-fragments/content-fragments-models.md)來建立所有新片段。
>
>內容片段模型用於WKND中的所有範例。

>[!NOTE]
>
>AEM 6.3之前，內容片段是根據範本而非模型建立的。
>
>內容片段範本現已棄用。 仍可用於建立片段，但建議改用內容片段模型。 片段範本不會新增任何新功能，未來版本中將移除這些功能。

* 內容片段模型：

   * 用於定義儲存結構化內容的內容片段。
   * 內容片段模型會在建立內容片段時定義其結構。
   * 片段會參考模型；因此對模型的變更可能會/將會影響任何相依片段。
   * 模型是由資料型別建立而成。
   * 新增新變數的函式等，必須據此更新片段。

  >[!CAUTION]
  >
  >對現有內容片段模型所做的任何變更都可能影響相依片段；這可能會導致這些片段中的孤立屬性。

* 內容片段範本：

   * 用於定義簡單內容片段。
   * 範本會在建立內容片段時定義內容片段的（基本、僅限文字）結構。
   * 範本在建立時會複製到片段，因此對範本的進一步變更將不會反映在現有片段中。
   * 新增新變數的函式等，必須據此更新片段。
   * [內容片段範本](/help/sites-developing/content-fragment-templates.md)的運作方式與AEM生態系統中的其他範本機制（例如頁面範本等）不同。 因此，應單獨考慮這些事件。
   * 根據範本時，內容的MIME型別是根據實際內容管理的；這表示每個元素和變數可以有不同的MIME型別。

### 與Assets整合 {#integration-with-assets}

內容片段管理(CFM)是AEM Assets的一部分，如下所示：

* 內容片段是資產。
* 他們使用現有的Assets功能。
* 這些控制檯已與Assets （管理主控台等）完全整合。

#### 將結構化內容片段對應至Assets {#mapping-structured-content-fragments-to-assets}

![片段至資產結構](assets/fragment-to-assets-structured.png)

具有結構化內容（即根據內容片段模型）的內容片段對應至單一資產：

* 所有內容都儲存在資產的`jcr:content/data`節點下：

   * 元素資料儲存在主子節點下：
     `jcr:content/data/master`

   * 變數會儲存在子節點下，其中包含變數的名稱：
例如，`jcr:content/data/myvariation`

   * 每個元素的資料都會儲存在個別子節點中，作為具有元素名稱的屬性：
例如，專案`text`的內容儲存為`jcr:content/data/master`上的屬性`text`

* 中繼資料和關聯內容儲存在`jcr:content/metadata`下方
除了標題和說明（不被視為傳統中繼資料，且儲存在`jcr:content`中）

#### 將簡單內容片段對應至Assets {#mapping-simple-content-fragments-to-assets}

![chlimage_1-90](assets/chlimage_1-90.png)

簡易內容片段（根據範本）對應至由主要資產和（選用）子資產組成的複合：

* 片段的所有非內容資訊（例如標題、說明、中繼資料、結構）都只在主要資產上管理。
* 片段第一個元素的內容對應至主要資產的原始轉譯。

   * 第一個元素的變數（如果有的話）會對應至主要資產的其他轉譯。

* 其他元素（如果存在）會對應至主要資產的子資產。

   * 這些額外元素的主要內容對應至個別子資產的原始轉譯。
   * 任何其他元素的其他變數（如果適用）對應至個別子資產的其他轉譯。

#### 資產位置 {#asset-location}

與標準資產一樣，內容片段位於下：

`/content/dam`

#### 資產許可權 {#asset-permissions}

如需詳細資訊，請參閱[內容片段 — 刪除考量事項](/help/assets/content-fragments/content-fragments-delete.md)。

#### 功能整合 {#feature-integration}

* 內容片段管理(CFM)功能以Assets核心為基礎，但應儘可能獨立於此功能。
* CFM針對卡片/欄/清單檢視中的專案提供自己的實作；這些增效模組會插入現有的Assets內容呈現實作。
* 已擴充數個Assets元件，以符合內容片段。

### 在頁面中使用內容片段 {#using-content-fragments-in-pages}

>[!CAUTION]
>
>現在建議使用[內容片段核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html)。 如需詳細資訊，請參閱[開發核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html)。

內容片段可以從AEM頁面引用，就像任何其他資產型別一樣。 AEM提供&#x200B;[**內容片段**&#x200B;核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html) - [元件，可讓您在頁面上包含內容片段](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page)。 您也可以擴充此&#x200B;**內容片段**&#x200B;核心元件。

* 元件使用`fragmentPath`屬性來參考實際內容片段。 `fragmentPath`屬性的處理方式與其他資產型別的類似屬性相同；例如，當內容片段移至其他位置時。

* 元件可讓您選取要顯示的變數。
* 此外，可以選取段落範圍來限制輸出；例如，這可用於多欄輸出。
* 元件允許[中間內容](/help/sites-developing/components-content-fragments.md#in-between-content)：

   * 在這裡，元件可讓您在參照片段的段落之間放置其他資產（影像等）。
   * 對於中間內容，您需要：

      * 請注意參考不穩定的可能性；中間內容（製作頁面時新增）與其旁邊的段落沒有固定的關係，在內容片段編輯器中，中間內容的位置會失去相對位置之前插入新的段落
      * 請考慮其他引數（例如變數和段落篩選器）以避免搜尋結果中的誤判

>[!NOTE]
>
>**內容片段模型：**
>
>使用以頁面上的內容片段模型為基礎的內容片段時，會參考模型。 這表示，如果您在發佈頁面時尚未發佈模型，系統會標籤此模型，並將模型新增至要與頁面一起發佈的資源。
>
>**內容片段範本：**
>
>使用以頁面上的內容片段範本為基礎的內容片段時，由於範本是在建立片段時複製的，因此沒有參考。

#### 使用OSGi控制檯進行設定 {#configuration-using-osgi-console}

例如，內容片段的後端實作負責讓頁面上使用的片段例項可供搜尋，或負責管理混合媒體內容。 此實作需要知道哪些元件用於轉譯片段，以及如何引數化轉譯。

可在[網頁主控台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)中針對OSGi套件&#x200B;**內容片段元件組態**&#x200B;設定此專案的引數。

* **資源型別**
可提供`sling:resourceTypes`的清單，以定義用於轉譯內容片段以及背景處理應套用的元件。

* **參考屬性**
屬性清單可設定為指定針對個別元件將片段的參考儲存的位置。

>[!NOTE]
>
>屬性和元件型別之間沒有直接對應。
>
>AEM只會採用可在段落上找到的第一個屬性。 因此，您應該謹慎選擇屬性。

![熒幕擷圖_2019-03-18at100941](assets/screenshot_2019-03-18at100941.png)

您仍然必須遵循一些准則，以確保您的元件與內容片段背景處理相容：

* 定義要呈現之專案的屬性名稱必須是`element`或`elementNames`。

* 定義要轉譯之變數的屬性名稱必須是`variation`或`variationName`。

* 如果支援多個元素的輸出（使用`elementNames`指定多個元素），則實際顯示模式是由屬性`displayMode`所定義：

   * 如果值為`singleText` （而且只設定了一個元素），則元素會呈現為具有中間內容、版面配置支援等的文字。 這是僅呈現一個元素的片段的預設值。
   * 否則，會使用更簡單的方法（可以稱為「表單檢視」），其中不支援中間內容，而片段內容會依「原樣」呈現。

* 如果為`displayMode`==`singleText` （隱含或明確）轉譯片段，則會使用下列其他屬性：

   * `paragraphScope`定義是否應轉譯所有段落，或僅轉譯段落範圍（值： `all`與`range`）

   * 如果`paragraphScope`==`range`，則屬性`paragraphRange`會定義要轉譯的段落範圍

### 與其他架構整合 {#integration-with-other-frameworks}

內容片段可以整合至：

* **翻譯**

  內容片段已與[AEM翻譯工作流程](/help/sites-administering/tc-manage.md)完全整合。 在架構層級，這表示：

   * 內容片段的個別翻譯實際上是單獨的片段；例如：

      * 它們位於不同的語言根下：

        `/content/dam/<path>/en/<to>/<fragment>`

        與

        `/content/dam/<path>/de/<to>/<fragment>`

      * 但它們與語言根目錄下的相對路徑完全相同：

        `/content/dam/<path>/en/<to>/<fragment>`

        與

        `/content/dam/<path>/de/<to>/<fragment>`

   * 除了規則型路徑以外，內容片段的不同語言版本之間沒有進一步的連線；它們會作為兩個單獨的片段處理，雖然UI提供了在語言變體之間導覽的方法。

  >[!NOTE]
  >
  >AEM翻譯工作流程可搭配`/content`使用：
  >
  >* 由於內容片段模型位於`/conf`，這些翻譯未包含在內。 您可以[國際化UI字串](/help/sites-developing/i18n-dev.md)。
  >
  >* 系統會複製範本來建立片段，因此這是隱含的。

* **中繼資料結構**

   * 內容片段（重新）使用可以使用標準資產定義的[中繼資料結構](/help/assets/metadata-schemas.md)。
   * CFM提供專屬的結構描述：

     `/libs/dam/content/schemaeditors/forms/contentfragment`

     如有需要，可延長此期限。

   * 個別結構表單已與片段編輯器整合。

## 內容片段管理API — 伺服器端 {#the-content-fragment-management-api-server-side}

您可以使用伺服器端API來存取您的內容片段；請參閱：

[com.adobe.cq.dam.cfm](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/package-summary.html)

>[!CAUTION]
>
>強烈建議使用伺服器端API，而非直接存取內容結構。

### 重要介面 {#key-interfaces}

下列三個介面可作為進入點：

* **片段範本** ([FragmentTemplate](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html))

  使用`FragmentTemplate.createFragment()`建立片段。

  ```
  Resource templateOrModelRsc = resourceResolver.getResource("...");
  FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
  ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
  ```

  此介面代表：

   * 要從中建立內容片段的內容片段模型或內容片段範本，
   * 和（建立後）該片段的結構資訊

  此資訊可包括：

   * 存取基本資料（標題、說明）
   * 存取片段元素的範本/模型：

      * 清單元素範本
      * 取得指定元素的結構資訊
      * 存取元素範本（請參閱`ElementTemplate`）

   * 存取片段變數的範本：

      * 清單變數範本
      * 取得指定變數的結構資訊
      * 存取變化範本（請參閱`VariationTemplate`）

   * 取得初始關聯內容

  代表重要資訊的介面：

   * `ElementTemplate`

      * 取得基本資料（名稱、標題）
      * 取得初始元素內容

   * `VariationTemplate`

      * 取得基本資料（名稱、標題、說明）

* **內容片段** ([ContentFragment](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

  此介面可讓您以抽象方式處理內容片段。

  >[!CAUTION]
  >
  >強烈建議透過此介面存取片段。 應避免直接變更內容結構。

  介面提供您執行下列作業的方法：

   * 管理基本資料（例如，取得名稱、取得/設定標題/說明）
   * 存取中繼資料
   * 存取元素：

      * 清單元素
      * 依名稱取得元素
      * 建立新元素（請參閱[注意事項](#caveats)）

      * 存取元素資料（請參閱`ContentElement`）

   * 為片段定義的清單變數
   * 全域建立新變數
   * 管理關聯內容：

      * 清單集合
      * 新增集合
      * 移除集合

   * 存取片段的模型或範本

  代表片段主要元素的介面包括：

   * **Content元素** ([ContentElement](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * 取得基本資料（名稱、標題、說明）
      * 取得/設定內容
      * 存取元素的變數：

         * 清單變數
         * 依名稱取得變數
         * 建立新的變數（請參閱[注意事項](#caveats)）
         * 移除變數（請參閱[警告](#caveats)）
         * 存取變化資料（請參閱`ContentVariation`）

      * 解決變數的捷徑（如果指定的變數不適用於元素，則套用一些額外的實作專用遞補邏輯）

   * **內容變數** ([ContentVariation](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * 取得基本資料（名稱、標題、說明）
      * 取得/設定內容
      * 根據上次修改資訊的簡單同步處理

  所有三個介面( `ContentFragment`、`ContentElement`、`ContentVariation`)都會延伸`Versionable`介面，新增內容片段所需的版本設定功能：

   * 建立元素的新版本
   * 列出元素的版本
   * 取得已建立版本之元素的特定版本內容

### 調整 — 使用adaptTo() {#adapting-using-adaptto}

可調整以下內容：

* `ContentFragment`可以調整為：

   * `Resource` — 基礎Sling資源；請注意，直接更新基礎`Resource`需要重新建置`ContentFragment`物件。

   * `Asset` — 代表內容片段的DAM `Asset`抽象化；請注意，直接更新`Asset`需要重新建置`ContentFragment`物件。

* `ContentElement`可以調整為：

   * `ElementTemplate` — 用於存取專案的結構資訊。

* `FragmentTemplate`可以調整為：

   * `Resource` - `Resource`決定複製的參考模型或原始範本；

      * 透過`Resource`所做的變更不會自動反映在`FragmentTemplate`中。

* `Resource`可以調整為：

   * `ContentFragment`
   * `FragmentTemplate`

### 警告 {#caveats}

請注意：

* 實作API是為了提供UI支援的功能。
* 整個API的設計目的是&#x200B;**不**&#x200B;自動保留變更（除非在API JavaDoc中另有註明）。 因此，您必須一律認可個別要求的資源解析器（或您實際使用的解析器）。
* 可能需要額外努力的任務：

   * 建立/移除新元素將不會更新簡單片段的資料結構（根據片段範本）。
   * 從`ContentElement`建立新的變數將不會更新資料結構（但從`ContentFragment`全域建立變數將會更新）。

   * 移除現有的變數將不會更新資料結構。

## 內容片段管理API — 使用者端 {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>對於AEM 6.5，使用者端API是內部的。

### 其他資訊 {#additional-information}

請參閱下列內容：

* `filter.xml`

  用於內容片段管理的`filter.xml`已設定為不與Assets核心內容套件重疊。

## 編輯工作階段 {#edit-sessions}

當使用者在其中一個編輯器頁面中開啟內容片段時，會啟動編輯工作階段。 當使用者透過選取&#x200B;**儲存**&#x200B;或&#x200B;**取消**&#x200B;而離開編輯器時，編輯工作階段即已完成。

### 要求 {#requirements}

控制編輯工作階段的需求如下：

* 編輯內容片段可跨越多個檢視(=HTML頁面)，這應該是原子性的。
* 編輯也應為&#x200B;*transactional*；在編輯工作階段結束時，必須認可（儲存）或回覆（取消）變更。
* Edge案例應正確處理；這包括使用者手動輸入URL或使用全域導覽離開頁面的情況。
* 應提供定期自動儲存（每x分鐘）以防止資料遺失。
* 如果兩個使用者同時編輯內容片段，他們不應覆寫彼此的變更。

#### 程序 {#processes}

相關程式包括：

* 啟動工作階段

   * 內容片段的新版本隨即建立。
   * 自動儲存已啟動。
   * Cookie已設定；這些會定義目前編輯的片段，且有開啟的編輯工作階段。

* 完成作業階段

   * 自動儲存已停止。
   * 提交時：

      * 上次修改的資訊會更新。
      * Cookie已移除。

   * 復原時：

      * 會還原在編輯工作階段啟動時所建立的內容片段版本。
      * Cookie已移除。

* 編輯

   * 所有變更（包括自動儲存）都是在使用中內容片段上完成的，而不是在分隔的保護區中。
   * 因此，這些變更會立即反映在參照個別內容片段的AEM頁面上

#### 動作 {#actions}

可能的動作包括：

* 進入頁面

   * 檢查編輯工作階段是否已經存在；透過檢查個別Cookie。

      * 如果存在，請確認編輯工作階段已針對目前編輯的內容片段啟動

         * 如果目前片段，請重新建立工作階段。
         * 如果沒有，請嘗試取消編輯先前編輯的內容片段並移除Cookie （之後不會有編輯工作階段存在）。

      * 如果不存在編輯工作階段，請等待使用者進行第一次變更（請參閱下文）。

   * 檢查頁面上是否已參考內容片段，如果有的話，顯示適當的資訊。

* 內容變更

   * 每當使用者變更內容且沒有編輯工作階段出現時，就會建立新的編輯工作階段（請參閱[啟動工作階段](#processes)）。

* 離開頁面

   * 如果存在編輯工作階段且變更尚未持續存在，則會顯示模式確認對話方塊，以通知使用者可能遺失的內容，並允許他們停留在頁面上。

## 範例 {#examples}

### 範例：存取現有的內容片段 {#example-accessing-an-existing-content-fragment}

若要完成此操作，您可以將代表API的資源調整為：

`com.adobe.cq.dam.cfm.ContentFragment`

例如：

```java
// first, get the resource
Resource fragmentResource = resourceResolver.getResource("/content/dam/fragments/my-fragment");
// then adapt it
if (fragmentResource != null) {
    ContentFragment fragment = fragmentResource.adaptTo(ContentFragment.class);
    // the resource is now accessible through the API
}
```

### 範例：建立內容片段 {#example-creating-a-new-content-fragment}

若要以程式設計方式建立內容片段，您需要使用：

`com.adobe.cq.dam.cfm.ContentFragmentManager#create`

例如：

```java
Resource templateOrModelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### 範例：指定自動儲存間隔 {#example-specifying-the-auto-save-interval}

自動儲存間隔（以秒為測量單位）可使用組態管理員(ConfMgr)定義：

* 節點： `<*conf-root*>/settings/dam/cfm/jcr:content`
* 屬性名稱： `autoSaveInterval`
* 類型：`Long`

* 預設： `600` （10分鐘）；這在`/libs/settings/dam/cfm/jcr:content`上定義

如果您想要設定5分鐘的自動儲存間隔，則必須在節點上定義屬性；例如：

* 節點： `/conf/global/settings/dam/cfm/jcr:content`
* 屬性名稱： `autoSaveInterval`

* 類型：`Long`

* 值： `300` （5分鐘等於300秒）

## 內容片段範本 {#content-fragment-templates}

如需完整資訊，請參閱[內容片段範本](/help/sites-developing/content-fragment-templates.md)。

## 用於頁面編寫的元件 {#components-for-page-authoring}

如需詳細資訊，請參閱

* [核心元件 — 內容片段元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html) （建議）
* [內容片段元件 — 頁面編寫專用元件](/help/sites-developing/components-content-fragments.md#components-for-page-authoring)
