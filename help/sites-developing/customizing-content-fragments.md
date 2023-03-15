---
title: 自訂和擴充內容片段
seo-title: Customizing and Extending Content Fragments
description: 內容片段會延伸標準資產。
seo-description: A content fragment extends a standard asset.
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 08c88e70-4df9-4627-8a66-1fabe3aee50b
source-git-commit: 9ad531738ac5e3c9d888f685b47c8b322712a89e
workflow-type: tm+mt
source-wordcount: '2778'
ht-degree: 2%

---


# 自訂和擴充內容片段{#customizing-and-extending-content-fragments}

內容片段會延伸標準資產；請參閱：

* [建立和管理內容片段](/help/assets/content-fragments/content-fragments.md) 和 [使用內容片段進行頁面編寫](/help/sites-authoring/content-fragments.md) 以取得內容片段的詳細資訊。

* [管理資產](/help/assets/manage-assets.md) 和 [自訂和擴充資產](/help/assets/extending-assets.md) 以取得標準資產的詳細資訊。

## 架構 {#architecture}

基本 [組成部分](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 內容片段包括：

* A *內容片段，*
* 由一個或多個 *內容元素* s,
* 可以有一個或多個 *內容變異* s.

視片段類型而定，也會使用模型或範本：

>[!CAUTION]
>
>[內容片段模型](/help/assets/content-fragments/content-fragments-models.md) 建議用於建立所有新片段。
>
>內容片段模型用於WKND中的所有範例。

>[!NOTE]
>
>在AEM 6.3之前，內容片段是根據範本而非模型建立。
>
>內容片段範本現已過時。 它們仍可用於建立片段，但建議改用內容片段模型。 片段範本不會新增任何功能，且這些功能將在未來版本中移除。

* 內容片段模型:

   * 用於定義包含結構化內容的內容片段。
   * 內容片段模型會在建立內容片段時定義其結構。
   * 片段會參照模型；因此，模型的變更可能會/將影響任何相依片段。
   * 模型是資料類型的組建。
   * 新增變異等的函式必須據以更新片段。

   >[!CAUTION]
   >
   >對現有內容片段模型的任何變更都可能影響相依片段；這可能會導致這些片段中的孤立屬性。

* 內容片段範本：

   * 用於定義簡單內容片段。
   * 範本會在建立內容片段時，定義內容片段的（基本、僅限文字）結構。
   * 範本建立時會複製到片段；因此，範本的進一步變更將不會反映在現有片段中。
   * 新增變異等的函式必須據以更新片段。
   * [內容片段範本](/help/sites-developing/content-fragment-templates.md) 以與AEM生態系統內其他模板機制（例如頁面模板等）不同的方式操作。 因此，應單獨考慮這些問題。
   * 根據模板管理內容的MIME類型時，根據實際內容進行管理；這表示每個元素和變異都可以有不同的MIME類型。

### 與資產整合 {#integration-with-assets}

內容片段管理(CFM)是AEM Assets的一部分，如下所示：

* 內容片段是資產。
* 它們使用現有的Assets功能。
* 它們已與資產（管理控制台等）完全整合。

#### 將結構化內容片段對應至資產 {#mapping-structured-content-fragments-to-assets}

![片段至資產結構](assets/fragment-to-assets-structured.png)

具有結構化內容的內容片段（即以內容片段模型為基礎）會對應至單一資產：

* 所有內容都儲存在 `jcr:content/data` 資產的節點：

   * 元素資料儲存在主子節點下：
      `jcr:content/data/master`

   * 變數儲存在帶有變數名稱的子節點下：例如 `jcr:content/data/myvariation`

   * 每個元素的資料作為具有元素名稱的屬性儲存在相應的子節點中：例如，元素的內容 `text` 儲存為屬性 `text` on `jcr:content/data/master`

* 元資料和相關內容儲存在下方 `jcr:content/metadata`
除了標題和說明，這些內容不被視為傳統中繼資料並儲存在 
`jcr:content`

#### 將簡單內容片段對應至資產 {#mapping-simple-content-fragments-to-assets}

![chlimage_1-90](assets/chlimage_1-90.png)

簡單內容片段（以範本為基礎）會對應至由主要資產和（選用）子資產組成的複合資產：

* 片段的所有非內容資訊（例如標題、說明、中繼資料、結構）都專門在主資產上管理。
* 片段的第一個元素的內容對應至主要資產的原始轉譯。

   * 第一個元素的變體（如果有的話）會對應至主要資產的其他轉譯。

* 其他元素（如果有）會對應至主要資產的子資產。

   * 這些額外元素的主要內容對應至個別子資產的原始轉譯。
   * 任何其他元素的其他變數（若適用）會對應至個別子資產的其他轉譯。

#### 資產位置 {#asset-location}

與標準資產一樣，內容片段位於：

`/content/dam`

#### 資產權限 {#asset-permissions}

如需詳細資訊，請參閱 [內容片段 — 刪除考量事項](/help/assets/content-fragments/content-fragments-delete.md).

#### 功能整合 {#feature-integration}

* 內容片段管理(CFM)功能以資產核心為基礎，但應盡可能獨立於此功能。
* CFM針對卡片/欄/清單檢視中的項目提供其專屬實作；這些外掛程式會插入現有的Assets內容呈現實作。
* 數個Assets元件已擴充，以符合內容片段。

### 在頁面中使用內容片段 {#using-content-fragments-in-pages}

>[!CAUTION]
>
>此 [內容片段核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html) 現在建議使用。 請參閱 [開發核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=zh-Hant) 以取得更多詳細資訊。

可從AEM頁面參照內容片段，如同任何其他資產類型。 AEM提供 [**內容片段** 核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html) - a [可讓您在頁面上包含內容片段的元件](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page). 您也可以延伸，這 **內容片段** 核心元件。

* 元件使用 `fragmentPath` 屬性來參考實際內容片段。 此 `fragmentPath` 財產的處理方式與其他資產類型的類似財產相同；例如，內容片段移至其他位置時。

* 元件可讓您選取要顯示的變數。
* 此外，可以選擇一系列段落來限制輸出；例如，這可用於多欄輸出。
* 元件允許 [中間內容](/help/sites-developing/components-content-fragments.md#in-between-content):

   * 此元件可讓您放置其他資產（影像等） 在引用片段的段落之間。
   * 針對中間內容，您需要：

      * 注意不穩定的參考資料的可能性；中間內容（製作頁面時新增）與它位於旁邊的段落沒有固定關係，在中間內容的位置之前插入新段落（在內容片段編輯器中）可能會丟失相對位置
      * 請考慮其他參數（例如變異和段落篩選），以避免搜尋結果中出現誤判

>[!NOTE]
>
>**內容片段模型:**
>
>使用以頁面上的內容片段模型為基礎的內容片段時，會參考模型。 這表示如果您在發佈頁面時尚未發佈模型，則會標籤此模型，並將模型新增至要隨頁面發佈的資源。
>
>**內容片段範本：**
>
>使用以頁面上的內容片段範本為基礎的內容片段時，沒有參考，因為建立片段時已複製範本。

#### 使用OSGi控制台進行配置 {#configuration-using-osgi-console}

例如，內容片段的後端實作負責讓頁面上使用的片段例項可供搜尋，或管理混合媒體內容。 此實作需要知道用於轉譯片段的元件，以及轉譯的參數化方式。

此參數的設定可在 [Web主控台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)，針對OSGi套件組合 **內容片段元件設定**.

* **資源類型**
清單 
`sling:resourceTypes` 可提供來定義用於轉譯內容片段的元件，以及應套用背景處理的位置。

* **參考屬性**
屬性清單可被配置以指定對片段的引用被儲存到相應元件的位置。

>[!NOTE]
>
>屬性和元件類型之間沒有直接映射。
>
>AEM只會取用段落上可找到的第一個屬性。 因此，您應謹慎選擇屬性。

![螢幕截圖_2019-03-18at100941](assets/screenshot_2019-03-18at100941.png)

您仍需遵循一些准則，以確保元件與內容片段背景處理相容：

* 要呈現的元素定義所在的屬性名稱必須是 `element` 或 `elementNames`.

* 要呈現的變數所在的屬性名稱必須為 `variation` 或 `variationName`.

* 如果支援多個元素的輸出(使用 `elementNames` )，則實際顯示模式由屬性定義 `displayMode`:

   * 如果值為 `singleText` （且只設定了一個元素），則元素會轉譯為文字，且包含內容、版面支援等。 這是只轉譯一個元素之片段的預設值。
   * 否則，會使用更簡單的方法（可稱為「表單檢視」），其中不支援中間內容，且片段內容會「依原樣」呈現。

* 如果為呈現片段 `displayMode` == `singleText` （隱含或明確）下列其他屬性開始運作：

   * `paragraphScope` 定義是否應呈現所有段落或僅呈現一系列段落(值： `all` vs. `range`)

   * if `paragraphScope` == `range` 然後是屬性 `paragraphRange` 定義要呈現的段落範圍

### 與其他架構整合 {#integration-with-other-frameworks}

內容片段可與：

* **翻譯**

   內容片段已與 [AEM翻譯工作流程](/help/sites-administering/tc-manage.md). 在架構層面，這表示：

   * 內容片段的個別翻譯實際上是個別片段；例如：

      * 它們位於不同的語言根下：

         `/content/dam/<path>/en/<to>/<fragment>`

         vs.

         `/content/dam/<path>/de/<to>/<fragment>`

      * 但它們在語言根底下的相對路徑完全相同：

         `/content/dam/<path>/en/<to>/<fragment>`

         vs.

         `/content/dam/<path>/de/<to>/<fragment>`
   * 除了基於規則的路徑外，內容片段的不同語言版本之間沒有進一步的連接；雖然UI提供在語言變體之間導覽的方式，但這些片段會以兩個不同片段的形式處理。
   >[!NOTE]
   >
   >AEM翻譯工作流程可搭配 `/content`:
   >
   >* 由於內容片段模型位於 `/conf`，則這些內容不會包含在此類翻譯中。 您可以 [將UI字串國際化](/help/sites-developing/i18n-dev.md).
   >
   >* 範本會複製以建立片段，因此會是隱式的。


* **中繼資料結構**

   * 內容片段（重新）使用 [中繼資料結構](/help/assets/metadata-schemas.md)，可使用標準資產來定義。
   * CFM提供其專屬的結構：

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      如有需要，可加以擴充。

   * 各個架構表單與片段編輯器整合。

## 內容片段管理API — 伺服器端 {#the-content-fragment-management-api-server-side}

您可以使用伺服器端API來存取您的內容片段；請參閱：

[com.adobe.cq.dam.cfm](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/package-summary.html)

>[!CAUTION]
>
>強烈建議使用伺服器端API，而非直接存取內容結構。

### 密鑰介面 {#key-interfaces}

以下三個介面可作為入口點：

* **片段範本** ([片段範本](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html))

   使用 `FragmentTemplate.createFragment()` 來建立新片段。

   ```
   Resource templateOrModelRsc = resourceResolver.getResource("...");
   FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
   ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
   ```

   此介面代表：

   * 要從中建立內容片段的內容片段模型或內容片段範本，
   * 及（建立後）該片段的結構資訊

   此資訊可包括：

   * 存取基本資料（標題、說明）
   * 存取片段元素的範本/模型：

      * 清單元素範本
      * 獲取給定元素的結構資訊
      * 存取元素範本(請參閱 `ElementTemplate`)
   * 片段變異的存取範本：

      * 清單變異範本
      * 獲取給定變數的結構資訊
      * 存取變異範本(請參閱 `VariationTemplate`)
   * 取得初始相關內容

   表示重要資訊的介面：

   * `ElementTemplate`

      * 取得基本資料（名稱、標題）
      * 取得初始元素內容
   * `VariationTemplate`

      * 取得基本資料（名稱、標題、說明）






* **內容片段** ([內容片段](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   此介面可讓您以抽象方式處理內容片段。

   >[!CAUTION]
   >
   >強烈建議透過此介面存取片段。 應避免直接變更內容結構。

   該介面提供您以下方法：

   * 管理基本資料(例如取得名稱；get/set title/description)
   * 存取中繼資料
   * 存取元素：

      * 清單元素
      * 依名稱取得元素
      * 建立新元素(請參閱 [警告](#caveats))

      * 存取元素資料(請參閱 `ContentElement`)
   * 為片段定義的清單變化
   * 全域建立新變體
   * 管理相關內容：

      * 清單集合
      * 新增集合
      * 移除集合
   * 存取片段的模型或範本

   代表片段主要元素的介面包括：

   * **內容元素** ([ContentElement](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * 取得基本資料（名稱、標題、說明）
      * 取得/設定內容
      * 元素的存取變化：

         * 清單變數
         * 依名稱取得變體
         * 建立新變體(請參閱 [警告](#caveats))
         * 移除變異(請參閱 [警告](#caveats))
         * 存取變異資料(請參閱 `ContentVariation`)
      * 解決變異的捷徑（如果指定的變異不適用於元素，則套用一些其他的實作專用備援邏輯）
   * **內容變異** ([ContentVariation](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * 取得基本資料（名稱、標題、說明）
      * 取得/設定內容
      * 基於上次修改資訊的簡單同步

   所有三個介面( `ContentFragment`, `ContentElement`, `ContentVariation`)延伸 `Versionable` 介面，新增版本設定功能，內容片段所需：

   * 建立新版本的元素
   * 元素的清單版本
   * 取得版本化元素的特定版本的內容







### 適應 — 使用adapTo() {#adapting-using-adaptto}

可調整下列項目：

* `ContentFragment` 可調整為：

   * `Resource`  — 基礎Sling資源；請注意，更新基礎 `Resource` 直接需要重建 `ContentFragment` 物件。

   * `Asset` - DAM `Asset` 代表內容片段的抽象化；請注意，更新 `Asset` 直接需要重建 `ContentFragment` 物件。

* `ContentElement` 可調整為：

   * `ElementTemplate`  — 存取元素的結構資訊。

* `FragmentTemplate` 可調整為：

   * `Resource` - `Resource` 確定所引用的模型或複製的原始模板；

      * 透過 `Resource` 不會自動反映在 `FragmentTemplate`.

* `Resource` 可調整為：

   * `ContentFragment`
   * `FragmentTemplate`

### 警告 {#caveats}

應當指出：

* 實作API是為了提供UI支援的功能。
* 整個API的設計目的 **not** 自動保留變更（除非API JavaDoc另有說明）。 因此，您必須一律提交個別請求的資源解析器（或您實際使用的解析器）。
* 可能需要付出額外努力的任務：

   * 建立/移除新元素時，不會更新簡單片段的資料結構（根據片段範本）。
   * 建立新變體 `ContentElement` 不會更新資料結構(但會從全域建立 `ContentFragment` 將)。

   * 移除現有變數不會更新資料結構。

## 內容片段管理API — 用戶端 {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>對於AEM 6.5，用戶端API為內部。

### 其他資訊 {#additional-information}

請參閱下列內容：

* `filter.xml`

   此 `filter.xml` 針對內容片段管理所設定，使其與「資產」核心內容套件不重疊。

## 編輯工作階段 {#edit-sessions}

當使用者在其中一個編輯器頁面中開啟內容片段時，就會啟動編輯工作階段。 當使用者借由選取任一選項離開編輯器時，編輯工作階段就會完成 **儲存** 或 **取消**.

### 要求 {#requirements}

控制編輯工作階段的需求為：

* 編輯內容片段可跨越多個檢視(=HTML頁面)，應該是原子。
* 編輯工作也應 *異動*;編輯工作階段結束時，必須提交（儲存）或復原（取消）變更。
* 邊緣案件應妥善處理；這些情況包括使用者手動輸入URL或使用全域導覽離開頁面的情況。
* 應可定期自動儲存（每x分鐘），以防止資料遺失。
* 如果兩個使用者同時編輯內容片段，他們不應覆寫彼此的變更。

#### 程序 {#processes}

涉及的流程包括：

* 開始工作階段

   * 內容片段的新版本隨即建立。
   * 自動儲存已啟動。
   * Cookie已設定；這些定義了目前編輯的片段，並且有一個編輯工作階段開啟。

* 完成工作階段

   * 自動儲存已停止。
   * 提交時：

      * 更新上次修改的資訊。
      * 會移除Cookie。
   * 回滾時：

      * 系統會還原在編輯工作階段啟動時建立的內容片段版本。
      * 會移除Cookie。


* 編輯

   * 所有變更（包括自動儲存）都會在作用中內容片段上完成，不會在分隔的受保護區域中完成。
   * 因此，這些變更會立即反映在參考個別內容片段的AEM頁面上

#### 動作 {#actions}

可能的動作包括：

* 輸入頁面

   * 檢查編輯工作階段是否已存在；檢查個別Cookie即可。

      * 如果存在，請確認已針對目前正在編輯的內容片段啟動編輯工作階段

         * 如果目前片段，請重新建立工作階段。
         * 如果沒有，請嘗試取消對先前編輯的內容片段進行編輯並移除Cookie（之後未出現編輯工作階段）。
      * 如果不存在編輯工作階段，請等待使用者進行的第一次變更（請參閱下方）。
   * 檢查頁面上是否已參考內容片段，若已參考則顯示適當資訊。



* 內容變更

   * 每當使用者變更內容且沒有編輯工作階段時，就會建立新的編輯工作階段(請參閱 [開始工作階段](#processes))。

* 離開頁面

   * 如果編輯工作階段存在，且變更未持續存在，則會顯示強制回應確認對話方塊，以通知使用者可能遺失的內容，並允許他們停留在頁面上。

## 範例 {#examples}

### 範例：存取現有內容片段 {#example-accessing-an-existing-content-fragment}

若要達成此目標，您可以調整代表API的資源，以：

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

### 範例：建立新內容片段 {#example-creating-a-new-content-fragment}

若要以程式設計方式建立新內容片段，您需要使用：

`com.adobe.cq.dam.cfm.ContentFragmentManager#create`

例如：

```java
Resource templateOrModelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### 範例：指定自動儲存間隔 {#example-specifying-the-auto-save-interval}

可使用配置管理器(ConfMgr)定義自動儲存間隔（以秒為單位）:

* 節點： `<*conf-root*>/settings/dam/cfm/jcr:content`
* 屬性名稱: `autoSaveInterval`
* 類型: `Long`

* 預設值： `600` （10分鐘）;此定義於 `/libs/settings/dam/cfm/jcr:content`

如果要設定5分鐘的自動儲存間隔，則需要在節點上定義屬性；例如：

* 節點： `/conf/global/settings/dam/cfm/jcr:content`
* 屬性名稱: `autoSaveInterval`

* 類型: `Long`

* 值： `300` （5分鐘等於300秒）

## 內容片段範本 {#content-fragment-templates}

請參閱 [內容片段範本](/help/sites-developing/content-fragment-templates.md) 以取得完整資訊。

## 頁面製作元件 {#components-for-page-authoring}

如需詳細資訊，請參閱

* [核心元件 — 內容片段元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html) （建議）
* [內容片段元件 — 頁面製作元件](/help/sites-developing/components-content-fragments.md#components-for-page-authoring)
