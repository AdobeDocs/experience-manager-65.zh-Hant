---
title: 自訂和擴充內容片段
seo-title: Customizing and Extending Content Fragments
description: 內容片段擴展標準資產。
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

內容片段擴展了標準資產；請參閱：

* [建立和管理內容片段](/help/assets/content-fragments/content-fragments.md) 和 [帶內容片段的頁面創作](/help/sites-authoring/content-fragments.md) 的子菜單。

* [管理資產](/help/assets/manage-assets.md) 和 [自定義和擴展資產](/help/assets/extending-assets.md) 以獲取有關標準資產的更多資訊。

## 架構 {#architecture}

基本 [組成部分](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) 內容片段的值為：

* A *內容片段，*
* 由一個或多個 *內容元素* s
* 可以有一個或多個 *內容變體* s

根據片段類型，還使用模型或模板：

>[!CAUTION]
>
>[內容片段模型](/help/assets/content-fragments/content-fragments-models.md) 建議建立所有新片段。
>
>WKND中的所有示例都使用內容片段模型。

>[!NOTE]
>
>6.AEM3之前的內容片段是基於模板而不是模型建立的。
>
>內容片段模板現在已棄用。 它們仍可用於建立片段，但建議改用「內容片段模型」。 將不向碎片模板添加任何新功能，並將在將來的版本中刪除這些功能。

* 內容片段模型:

   * 用於定義包含結構化內容的內容片段。
   * 內容片段模型定義內容片段建立時的結構。
   * 片段引用模型；因此，對模型的更改可能會/會影響任何相關片段。
   * 模型是資料類型的集合。
   * 添加新變體等的函式必須相應地更新片段。

   >[!CAUTION]
   >
   >對現有內容片段模型的任何更改都會影響相關片段；這會導致這些片段中的孤立屬性。

* 內容片段模板：

   * 用於定義簡單內容片段。
   * 模板定義內容片段在建立時的（基本、僅文本）結構。
   * 建立模板時，模板將複製到片段；因此對模板的進一步更改不會反映在現有片段中。
   * 添加新變體等的函式必須相應地更新片段。
   * [內容片段模板](/help/sites-developing/content-fragment-templates.md) 以與生態系統內其他模板機制(AEM如頁面模板等)不同的方式運行。 因此，應單獨考慮。
   * 當基於模板時，內容的MIME類型根據實際內容進行管理；這意味著每個元素和變體都可以具有不同的MIME類型。

### 與資產整合 {#integration-with-assets}

內容片段管理(CFM)是AEM Assets的一部分，具體為：

* 內容片段是資產。
* 它們使用現有資產功能。
* 它們與Assets（管理控制台等）完全整合。

#### 將結構化內容片段映射到資產 {#mapping-structured-content-fragments-to-assets}

![分段到資產結構](assets/fragment-to-assets-structured.png)

具有結構化內容（即基於內容片段模型）的內容片段被映射到單個資產：

* 所有內容都儲存在 `jcr:content/data` 節點：

   * 元素資料儲存在主子節點下：
      `jcr:content/data/master`

   * 變體儲存在子節點下，該子節點包含變體名稱：例如 `jcr:content/data/myvariation`

   * 每個元素的資料作為具有元素名稱的屬性儲存在相應的子節點中：例如元素的內容 `text` 儲存為屬性 `text` 上 `jcr:content/data/master`

* 元資料和相關內容儲存在下面 `jcr:content/metadata`
除標題和說明外，這些標題和說明不被視為傳統元資料並儲存在 
`jcr:content`

#### 將簡單內容片段映射到資產 {#mapping-simple-content-fragments-to-assets}

![chlimage_1-90](assets/chlimage_1-90.png)

簡單內容片段（基於模板）被映射到由主資產和（可選）子資產組成的組合：

* 片段的所有非內容資訊（例如標題、描述、元資料、結構）僅在主資產上進行管理。
* 片段的第一元素的內容被映射到主資產的原始格式副本。

   * 第一個元素的變體（如果存在）將映射到主資產的其他格式副本。

* 附加元素（如果存在）被映射到主資產的子資產。

   * 這些附加元素的主要內容映射到相應子資產的原始格式副本。
   * 任何附加要素的其他變體（如適用）都與相應子資產的其他格式副本對應。

#### 資產位置 {#asset-location}

與標準資產一樣，內容片段的持有方式如下：

`/content/dam`

#### 資產權限 {#asset-permissions}

有關詳細資訊，請參閱 [內容片段 — 刪除注意事項](/help/assets/content-fragments/content-fragments-delete.md)。

#### 功能整合 {#feature-integration}

* 內容片段管理(CFM)功能構建在「資產」核心之上，但應盡可能獨立於它。
* CFM為卡/列/清單視圖中的項目提供自己的實現；這些插件將插入現有的Assets內容呈現實現。
* 已擴展了若干Assets元件，以滿足內容片段的需要。

### 在頁面中使用內容片段 {#using-content-fragments-in-pages}

>[!CAUTION]
>
>的 [內容片段核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html) 現在推薦。 請參閱 [開發核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=zh-Hant) 的子菜單。

內容片段可以從頁面AEM中引用，就像其他任何資產類型一樣。 提AEM供 [**內容片段** 核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html) - [允許您在頁面上包含內容片段的元件](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page)。 你也可以延伸，這個 **內容片段** 核心元件。

* 元件使用 `fragmentPath` 引用實際內容片段的屬性。 的 `fragmentPath` 與其他資產類型的同類財產處理相同；例如，當內容片段移動到其他位置時。

* 元件允許您選擇要顯示的變體。
* 此外，還可以選擇一系列段落來限制輸出；例如，這可用於多列輸出。
* 元件允許 [內容](/help/sites-developing/components-content-fragments.md#in-between-content):

   * 在此元件允許您放置其他資產（影像等） 在引用片段的段落之間。
   * 對於中間內容，您需要：

      * 注意不穩定的參考資料的可能性；在內容之間（在創作頁面時添加）與它位於旁邊的段落沒有固定關係，在插入內容的位置丟失相對位置之前插入新段落（在內容片段編輯器中）
      * 考慮附加參數（如變體和段落篩選器）以避免搜索結果中出現誤報

>[!NOTE]
>
>**內容片段模型:**
>
>當使用基於頁面上的內容片段模型的內容片段時，引用該模型。 這意味著，如果在發佈頁面時尚未發佈模型，則會標籤該模型，並將模型添加到要隨頁面一起發佈的資源中。
>
>**內容片段模板：**
>
>使用基於頁面上的內容片段模板的內容片段時，沒有引用，因為建立片段時複製了該模板。

#### 使用OSGi控制台進行配置 {#configuration-using-osgi-console}

例如，內容片段的後端實現負責使用於頁面上的片段的實例可搜索，或用於管理混合媒體內容。 此實現需要知道哪些元件用於渲染片段以及渲染是如何參數化的。

此參數可在 [Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)，用於OSGi捆綁包 **內容片段元件配置**。

* **資源類型**
清單 
`sling:resourceTypes` 可以提供來定義用於呈現內容片段的元件，以及應將後台處理應用到其中。

* **引用屬性**
屬性清單可以被配置以指定對片段的引用儲存於各個元件的位置。

>[!NOTE]
>
>屬性和元件類型之間沒有直接映射。
>
>只AEM需獲取段落中可找到的第一個屬性。 所以你應該仔細選擇這些屬性。

![screpton_2019-03-18at100941](assets/screenshot_2019-03-18at100941.png)

您仍然必須遵循一些准則以確保元件與內容片段後台處理相容：

* 定義要呈現的元素的屬性的名稱必須是 `element` 或 `elementNames`。

* 定義要呈現的變體的屬性的名稱必須是 `variation` 或 `variationName`。

* 如果支援多個元素的輸出(使用 `elementNames` 指定多個元素)，實際顯示模式由屬性定義 `displayMode`:

   * 如果值為 `singleText` （並且只配置了一個元素），然後將元素呈現為具有內容、佈局支援等的文本。 這是僅呈現一個元素的片段的預設值。
   * 否則，使用一種更簡單的方法（可稱為「表單視圖」），其中不支援中間內容，並且片段內容「原樣」呈現。

* 如果為 `displayMode` == `singleText` （隱式或顯式）以下附加屬性開始發揮作用：

   * `paragraphScope` 定義是否應呈現所有段落或僅呈現一系列段落(值： `all` 與 `range`)

   * 如果 `paragraphScope` == `range` 然後 `paragraphRange` 定義要呈現的段落範圍

### 與其他框架整合 {#integration-with-other-frameworks}

內容片段可與以下內容整合：

* **翻譯**

   內容片段與 [AEM翻譯工作流](/help/sites-administering/tc-manage.md)。 在建築層面，這意味著：

   * 內容片段的個別翻譯實際上是分開的片段；例如：

      * 它們位於不同的語言根下：

         `/content/dam/<path>/en/<to>/<fragment>`

         與

         `/content/dam/<path>/de/<to>/<fragment>`

      * 但它們在語言根下面有著完全相同的相對路徑：

         `/content/dam/<path>/en/<to>/<fragment>`

         與

         `/content/dam/<path>/de/<to>/<fragment>`
   * 除了基於規則的路徑外，內容片段的不同語言版本之間沒有進一步的連接；它們被處理為兩個單獨的片段，儘管UI提供了在語言變體之間導航的方法。
   >[!NOTE]
   >
   >翻AEM譯工作流 `/content`:
   >
   >* 由於內容片段模型位於 `/conf`，這些內容不包括在此類翻譯中。 你可以 [國際化UI字串](/help/sites-developing/i18n-dev.md)。
   >
   >* 複製模板以建立片段，因此這是隱式的。


* **中繼資料結構描述**

   * 內容片段（重新）使用 [元資料架構](/help/assets/metadata-schemas.md)，可用標準資產定義。
   * CFM提供其自己的特定架構：

      `/libs/dam/content/schemaeditors/forms/contentfragment`

      如果需要，可以擴展此範圍。

   * 各個模式形式與片段編輯器整合。

## 內容片段管理API — 伺服器端 {#the-content-fragment-management-api-server-side}

您可以使用伺服器端API訪問您的內容片段；請參閱：

[com.adobe.cq.dam.cfm](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/package-summary.html)

>[!CAUTION]
>
>強烈建議使用伺服器端API，而不是直接訪問內容結構。

### 關鍵介面 {#key-interfaces}

以下三個介面可用作入口點：

* **片段模板** ([片段模板](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html))

   使用 `FragmentTemplate.createFragment()` 的子菜單。

   ```
   Resource templateOrModelRsc = resourceResolver.getResource("...");
   FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
   ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
   ```

   此介面表示：

   * 從中建立內容片段的內容片段模型或內容片段模板，
   * 和（在創作後）碎片的結構資訊

   此資訊可包括：

   * 訪問基本資料（標題、說明）
   * 訪問片段元素的模板/模型：

      * 清單元素模板
      * 獲取給定元素的結構資訊
      * 訪問元素模板(請參見 `ElementTemplate`)
   * 訪問片段變體的模板：

      * 清單變體模板
      * 獲取給定變體的結構資訊
      * 訪問變體模板(請參閱 `VariationTemplate`)
   * 獲取初始關聯內容

   表示重要資訊的介面：

   * `ElementTemplate`

      * 獲取基本資料（名稱、標題）
      * 獲取初始元素內容
   * `VariationTemplate`

      * 獲取基本資料（名稱、標題、說明）






* **內容片段** ([內容片段](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

   此介面允許您以抽象方式處理內容片段。

   >[!CAUTION]
   >
   >強烈建議通過此介面訪問片段。 應避免直接更改內容結構。

   該介面提供了以下方法：

   * 管理基本資料(如獲取名稱；獲取/設定標題/說明
   * 訪問元資料
   * 訪問元素：

      * 清單元素
      * 按名稱獲取元素
      * 建立新元素(請參閱 [警告](#caveats))

      * 訪問元素資料(請參見 `ContentElement`)
   * 列出為片段定義的變體
   * 全局建立新變體
   * 管理關聯內容：

      * 清單集合
      * 添加集合
      * 刪除集合
   * 訪問片段的模型或模板

   表示片段主元素的介面包括：

   * **內容元素** ([內容元素](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * 獲取基本資料（名稱、標題、說明）
      * 獲取/設定內容
      * 訪問元素的變體：

         * 清單變體
         * 按名稱獲取變體
         * 建立新變體(請參閱 [警告](#caveats))
         * 刪除變體(請參見 [警告](#caveats))
         * 訪問變體資料(請參見 `ContentVariation`)
      * 解析變體的快捷方式（如果指定的變體不適用於元素，則應用某些附加的特定於實現的回退邏輯）
   * **內容變體** ([內容變體](https://www.adobe.io/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * 獲取基本資料（名稱、標題、說明）
      * 獲取/設定內容
      * 基於上次修改的資訊的簡單同步

   所有三個介面( `ContentFragment`。 `ContentElement`。 `ContentVariation`)擴展 `Versionable` 介面，添加內容片段所需的版本控制功能：

   * 建立元素的新版本
   * 列出元素的版本
   * 獲取版本化元素的特定版本的內容







### 適配 — 使用適配對象() {#adapting-using-adaptto}

可以調整以下內容：

* `ContentFragment` 可適用於：

   * `Resource`  — 基礎Sling資源；請注意，更新基礎 `Resource` 直接，需要重建 `ContentFragment` 的雙曲餘切值。

   * `Asset`  — 水壩 `Asset` 表示內容片段的抽象；注意，更新 `Asset` 直接，需要重建 `ContentFragment` 的雙曲餘切值。

* `ContentElement` 可適用於：

   * `ElementTemplate`  — 用於訪問元素的結構資訊。

* `FragmentTemplate` 可適用於：

   * `Resource` - `Resource` 確定被參照的模型或複製的原始模板；

      * 通過 `Resource` 不會自動反映在 `FragmentTemplate`。

* `Resource` 可適用於：

   * `ContentFragment`
   * `FragmentTemplate`

### 警告 {#caveats}

應當指出：

* 實現該API以提供該UI支援的功能。
* 整個API的設計 **不** 自動保留更改（除非API JavaDoc中另有說明）。 因此，您必須始終提交相應請求（或您實際使用的解析程式）的資源解析程式。
* 可能需要額外工作的任務：

   * 建立/刪除新元素不會更新簡單片段的資料結構（基於片段模板）。
   * 建立新變體 `ContentElement` 不會更新資料結構(但是從全局 `ContentFragment` )。

   * 刪除現有變體不會更新資料結構。

## 內容片段管理API — 客戶端 {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>對於AEM6.5，客戶端API是內部的。

### 其他資訊 {#additional-information}

請參閱下列內容：

* `filter.xml`

   的 `filter.xml` 對於內容片段管理，將其配置為不與Assets核心內容包重疊。

## 編輯會話 {#edit-sessions}

當用戶在編輯器頁面之一中開啟內容片段時啟動編輯會話。 當用戶通過選擇編輯器中的任意一個而離開編輯器時，編輯會話將完成 **保存** 或 **取消**。

### 要求 {#requirements}

控制編輯會話的要求有：

* 編輯可跨多個視圖(=HTML頁)的內容片段應是原子的。
* 編輯還應 *事務*;在編輯會話結束時，必須提交（保存）或回退（取消）更改。
* 應妥善處理邊緣案件；這些情況包括用戶通過手動輸入URL或使用全局導航離開頁面的情況。
* 應提供定期自動保存（每x分鐘），以防止資料丟失。
* 如果內容片段由兩個用戶同時編輯，則不應覆蓋彼此的更改。

#### 程序 {#processes}

涉及的流程包括：

* 啟動會話

   * 建立內容片段的新版本。
   * 自動保存已啟動。
   * Cookie已設定；這些定義當前已編輯的片段，並且存在開啟的編輯會話。

* 完成會話

   * 自動保存已停止。
   * 提交時：

      * 更新上次修改的資訊。
      * 已刪除Cookie。
   * 回滾時：

      * 恢復在啟動編輯會話時建立的內容片段的版本。
      * 已刪除Cookie。


* 編輯

   * 所有更改（包括自動保存）都在活動內容片段上完成 — 而不是在單獨的受保護區域中。
   * 因此，這些改變立即反映在AEM引用相應內容片段的頁面上

#### 動作 {#actions}

可能的操作包括：

* 輸入頁面

   * 檢查是否已存在編輯會話；檢查相應的cookie。

      * 如果存在，請驗證是否為當前正在編輯的內容片段啟動了編輯會話

         * 如果當前片段，請重新建立會話。
         * 如果沒有，請嘗試取消對先前編輯的內容片段的編輯並刪除cookie（以後不存在編輯會話）。
      * 如果不存在編輯會話，請等待用戶進行的第一次更改（請參閱下面）。
   * 檢查內容片段是否已在頁面上引用，如果已引用，則顯示相應資訊。



* 內容更改

   * 每當用戶更改內容且沒有編輯會話時，就會建立新的編輯會話(請參見 [啟動會話](#processes))。

* 離開頁面

   * 如果存在編輯會話且更改尚未永續，則顯示模式確認對話框以通知用戶可能丟失的內容並允許它們留在頁面上。

## 範例 {#examples}

### 示例：訪問現有內容片段 {#example-accessing-an-existing-content-fragment}

要實現此目的，您可以將表示API的資源調整為：

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

### 示例：建立新內容片段 {#example-creating-a-new-content-fragment}

要以寫程式方式建立新內容片段，需要使用：

`com.adobe.cq.dam.cfm.ContentFragmentManager#create`

例如：

```java
Resource templateOrModelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = templateOrModelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### 示例：指定自動保存間隔 {#example-specifying-the-auto-save-interval}

可以使用配置管理器(ConfMgr)定義自動保存間隔（以秒為單位）:

* 節點： `<*conf-root*>/settings/dam/cfm/jcr:content`
* 屬性名稱: `autoSaveInterval`
* 類型: `Long`

* 預設值： `600` （10分鐘）;此定義於 `/libs/settings/dam/cfm/jcr:content`

如果要設定5分鐘的自動儲存間隔，則需要在節點上定義屬性；例如：

* 節點： `/conf/global/settings/dam/cfm/jcr:content`
* 屬性名稱: `autoSaveInterval`

* 類型: `Long`

* 值： `300` （5分鐘等於300秒）

## 內容片段模板 {#content-fragment-templates}

請參閱 [內容片段模板](/help/sites-developing/content-fragment-templates.md) 的雙曲餘切值。

## 頁面創作元件 {#components-for-page-authoring}

有關詳細資訊，請參閱

* [核心元件 — 內容片段元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html) （推薦）
* [內容片段元件 — 頁面創作的元件](/help/sites-developing/components-content-fragments.md#components-for-page-authoring)
