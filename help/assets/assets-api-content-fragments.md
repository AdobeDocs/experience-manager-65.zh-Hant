---
title: Adobe Experience Manager資產HTTP API中的內容片段支援
description: 瞭解資產HTTP API中對內容片段的支援，這是無頭傳遞功能AEM的重要部分。
feature: Content Fragments,Assets HTTP API
exl-id: 0f9efb47-a8d1-46d9-b3ff-a6c0741ca138
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '1957'
ht-degree: 2%

---

# AEM Assets HTTP API 內容片段支援 {#content-fragments-support-in-aem-assets-http-api}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/assets-api-content-fragments.html?lang=en) |
| AEM 6.5 | 本文 |


## 概觀 {#overview}

瞭解資產HTTP API中對內容片段的支援，這是無頭傳遞功能AEM的重要部分。

>[!NOTE]
>
>的 [資產HTTP API](/help/assets/mac-api-assets.md) 包括：
>
>* 資產REST API
>* 包括對內容片段的支援
>
>Assets HTTP API的當前實現基於 [休息](https://en.wikipedia.org/wiki/Representational_state_transfer) 建築風格。

的 [資產REST API](/help/assets/mac-api-assets.md) 允許Adobe Experience Manager開發人員通過CRUD操作(建立、讀取、更新、刪除AEM)直接通過HTTP API訪問內容（儲存在中）。

通過向JavaScript前端應用程式提供內容服務，API允許您將Adobe Experience Manager作為無頭CMS（內容管理系統）進行操作。 或可以執行HTTP請求和處理JSON響應的任何其他應用程式。

例如，單頁應用程式(SPA)、基於框架或自定義，需要通過HTTP API提供的內容，通常為JSON格式。

同時 [核AEM心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant) 提供非常全面、靈活和可自定義的API，可為此目的提供所需的讀取操作，並且其JSON輸出可以自定義，因此它們確實需要AEMWCM（Web內容管理）技術來實施，因為它們必須承載在基於專用模板的頁AEM面中。 並非每個SPA發展組織都能直接獲得這些知識。

此時可以使用Assets REST API。 它允許開發人員直接訪問資產（例如，影像和內容片段），而無需首先將它們嵌入到頁面中，並以序列化JSON格式傳送其內容。

>[!NOTE]
>
>無法從Assets REST API自定義JSON輸出。

Assets REST API還允許開發人員通過建立新資產、更新或刪除現有資產、內容片段和資料夾來修改內容。

資產REST API:

* 後面 [HATEOAS原則](https://en.wikipedia.org/wiki/HATEOAS)

* 實現 [SIREN格式](https://github.com/kevinswiber/siren)

## 必備條件 {#prerequisites}

Assets REST API可用於最新版本的每個出廠安裝AEM。

## 重要概念 {#key-concepts}

資產REST API提供 [休息](https://en.wikipedia.org/wiki/Representational_state_transfer)-style訪問實例中儲存的AEM資產。

它使用 `/api/assets` 端點，並需要資產的路徑才能訪問它(沒有前導 `/content/dam`)。

* 這意味著訪問以下位置的資產：
   * `/content/dam/path/to/asset`
* 您需要請求：
   * `/api/assets/path/to/asset`

例如，訪問 `/content/dam/wknd/en/adventures/cycling-tuscany`。 `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>訪問：
>
>* `/api/assets` **不** 需要使用 `.model` 選擇器。
>* `/content/path/to/page` **是** 要求使用 `.model` 選擇器。


HTTP方法確定要執行的操作：

* **GET**  — 檢索資產或資料夾的JSON表示法
* **POST**  — 建立新資產或資料夾
* **PUT**  — 更新資產或資料夾的屬性
* **DELETE**  — 刪除資產或資料夾

>[!NOTE]
>
>請求正文和/或URL參數可用於配置其中的一些操作；例如，定義資料夾或資產應由 **POST** 請求。

支援請求的確切格式在 [API參考](/help/assets/assets-api-content-fragments.md#api-reference) 文檔。

### 事務性行為 {#transactional-behavior}

所有請求都是原子的。

這表示後續(`write`)請求不能合併到單個事務中，該事務可以作為單個實體成功或失敗。

### (AEM資產)REST API與組AEM件 {#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>方面</td>
   <td>資產REST API<br/> </td>
   <td>組AEM件<br/> （使用吊具模型的元件）</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>支援的用例</td>
   <td>一般用途。</td>
   <td><p>已針對單頁應用程式(SPA)或任何其他（內容消耗）上下文中的消耗進行優化。</p> <p>也可以包含佈局資訊。</p> </td>
  </tr>
  <tr>
   <td>支援的操作</td>
   <td><p>建立、讀取、更新、刪除。</p> <p>具有附加操作，具體取決於實體類型。</p> </td>
   <td>唯讀.</td>
  </tr>
  <tr>
   <td>存取</td>
   <td><p>可以直接訪問。</p> <p>使用 <code>/api/assets </code>終結點，映射到 <code>/content/dam</code> （在儲存庫中）。</p> 
   <p>示例路徑如下所示： <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>需要通過頁面上AEM的元件引AEM用。</p> <p>使用 <code>.model</code> 選擇器以建立JSON表示法。</p> <p>示例路徑如下所示：<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>安全性</td>
   <td><p>可能有多個選項。</p> <p>提出了OAuth;可以與標準設定分開配置。</p> </td>
   <td>使用標AEM準設定。</td>
  </tr>
  <tr>
   <td>建築注釋</td>
   <td><p>寫訪問通常會針對作者實例。</p> <p>也可將讀取定向到發佈實例。</p> </td>
   <td>由於此方法是只讀的，因此它通常用於發佈實例。</td>
  </tr>
  <tr>
   <td>輸出</td>
   <td>基於JSON的SIRN輸出：冗餘，但功能強大。 允許在內容中導航。</td>
   <td>基於JSON的專有輸出；可通過Sling Models配置。 瀏覽內容結構很難實現（但未必不可能）。</td>
  </tr>
 </tbody>
</table>

### 安全性 {#security}

如果在沒有特定身份驗證要求的環境中使用Assets REST API ,AEM則需要正確配置CORS篩選器。

>[!NOTE]
>
>有關詳細資訊，請參閱：
>
>* [CORS/解AEM釋](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html)
>* [視頻 — 為CORS開AEM發](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/develop-for-cross-origin-resource-sharing.html)
>


在具有特定身份驗證要求的環境中，建議使用OAuth。

## 可用功能 {#available-features}

內容片段是特定類型的資產，請參見 [使用內容片段](/help/assets/content-fragments/content-fragments.md)。

有關通過API提供的功能的詳細資訊，請參閱：

* 的 [資產REST API](/help/assets/mac-api-assets.md)
* [實體類型](/help/assets/assets-api-content-fragments.md#entity-types)，其中說明了特定於每個支援類型（與內容片段相關）的功能

### 分頁 {#paging}

Assets REST API支援通過URL參數進行分頁(用於GET請求):

* `offset`  — 要檢索的第一個（子）實體的編號
* `limit`  — 返回的最大實體數

響應將包含作為 `properties` 的下界。 此 `srn:paging` 屬性包含（子）實體總數( `total`)、偏移和限制( `offset`。 `limit`)。

>[!NOTE]
>
>分頁通常應用於容器實體（即資料夾或具有格式副本的資產），因為它與所請求實體的子代相關。

#### 示例：分頁 {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```json
...
"properties": {
    ...
    "srn:paging": {
        "total": 7,
        "offset": 2,
        "limit": 3
    }
    ...
}
...
```

## 實體類型 {#entity-types}

### 資料夾 {#folders}

資料夾用作資產和其他資料夾的容器。 它們反映了內容儲存AEM庫的結構。

Assets REST API公開了對資料夾屬性的訪問；例如，其名稱、標題等。 資產作為資料夾和子資料夾的子實體公開。

>[!NOTE]
>
>根據子資產和資料夾的資產類型，子實體清單可能已經包含定義相應子實體的全套屬性。 或者，對於子實體清單中的實體，只能公開縮減的屬性集。

### Assets {#assets}

如果請求資產，響應將返回其元資料；如標題、名稱和由相應資產架構定義的其他資訊。

資產的二進位資料作為類型的SIREN連結公開 `content`。

資產可以具有多個格式副本。 它們通常作為子實體公開，一個例外是縮略圖格式副本，該格式副本作為類型連結公開 `thumbnail` ( `rel="thumbnail"`)。

### 內容片段 {#content-fragments}

A [內容片段](/help/assets/content-fragments/content-fragments.md) 是一種特殊的資產類型。 它們可用於訪問結構化資料，如文本、數字、日期等。

由於有幾種不同 *標準* 資產（如影像或音頻），某些附加規則適用於處理這些資產。

#### 表示法 {#representation}

內容片段：

* 不要公開任何二進位資料。
* 完全包含在JSON輸出中(位於 `properties` 屬性)。

* 也被視為原子，即元素和變體作為片段屬性的一部分而作為連結或子實體而暴露。 這允許有效訪問片段的負載。

#### 內容模型和內容片段 {#content-models-and-content-fragments}

當前定義內容片段結構的模型不會通過HTTP API公開。 因此 *消費者* 需要瞭解碎片的模型（至少至少要知道一個） — 儘管大多數資訊都可以從有效載荷中推斷出來；資料類型等。 是定義的一部分。

要建立新內容片段，必須提供模型（內部儲存庫）路徑。

#### 相關聯的內容 {#associated-content}

關聯內容當前未公開。

## 使用 {#using}

使用情況可能會因您使用的是作者還是AEM發佈環境以及您的特定使用案例而異。

* 強烈建議將建立綁定到作者實例([目前沒有方法使用此API複製要發佈的片段](/help/assets/assets-api-content-fragments.md#limitations))。
* 可從兩者進行傳遞，因AEM為僅以JSON格式提供請求的內容。

   * 從作者實例AEM進行儲存和傳遞應足以滿足防火牆後的媒體庫應用程式。

   * 對於即時Web交AEM付，建議使用發佈實例。

>[!CAUTION]
>
>實例上的調度AEM程式配置可能阻止訪問 `/api`。

>[!NOTE]
>
>有關詳細資訊，請參閱 [API參考](/help/assets/assets-api-content-fragments.md#api-reference)。 特別是， [Adobe Experience Manager資產API — 內容片段](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html)。

### 讀取/傳遞 {#read-delivery}

用法：

`GET /{cfParentPath}/{cfName}.json`

例如：

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

響應是以內容片段中的結構化內容進行序列化的JSON。 引用作為引用URL傳遞。

有兩種讀操作：

* 按路徑讀取特定內容片段，這將返回內容片段的JSON表示。
* 按路徑讀取內容片段的資料夾：這將返回資料夾內所有內容片段的JSON表示法。

### 建立 {#create}

用法：

`POST /{cfParentPath}/{cfName}`

主體必須包含要建立的內容片段的JSON表示法，包括應在內容片段元素上設定的任何初始內容。 必須設定 `cq:model` 屬性，並且它必須指向有效的內容片段模型。 如果無法執行此操作，將導致錯誤。 還需要添加標題 `Content-Type` 設定為 `application/json`。

### 更新 {#update}

使用是通過

`PUT /{cfParentPath}/{cfName}`

主體必須包含為給定內容片段更新的內容的JSON表示。

這可以只是內容片段、單個元素或所有元素值和/或元資料的標題或說明。

### 刪除 {#delete}

用法：

`DELETE /{cfParentPath}/{cfName}`

## 限制 {#limitations}

有幾個限制：

* **當前不支援內容片段模型**:無法讀取或建立。 要能夠建立新內容片段或更新現有內容片段，開發人員必須知道指向內容片段模型的正確路徑。 目前，獲取這些概述的唯一方法是通過管理UI。
* **忽略引用**。 當前沒有檢查是否引用了現有內容片段。 因此，例如，刪除內容片段可能會導致包含對已刪除內容片段的引用的頁面出現問題。
* **JSON資料類型** 的REST API輸出 *JSON資料類型* 當前 *基於字串的輸出*。

## 狀態代碼和錯誤消息 {#status-codes-and-error-messages}

在相關情況下，可以看到以下狀態代碼：

* **200** （確定）在以下情況下返回：

   * 通過 `GET`
   * 通過 `PUT`

* **201** （已建立）在以下情況下返回：

   * 通過 `POST`

* **404** （未找到）在以下情況下返回：

   * 請求的內容片段不存在

* **500** （內部伺服器錯誤）

   >[!NOTE]
   >
   >返回此錯誤：
   >
   >* 發生無法用特定代碼標識的錯誤時
   >* 當給定負載無效時


   以下列出返回此錯誤狀態時的常見方案以及生成的錯誤消息（等寬）:

   * 父資料夾不存在（通過建立內容片段時） `POST`)
   * 未提供任何內容片段模型（缺少cq:model）、無法讀取（由於路徑無效或權限問題）或沒有有效片段模型：

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`
   * 無法建立內容片段（可能是權限問題）:

      * `Could not create content fragment`
   * 無法更新標題和或說明：

      * `Could not set value on content fragment`
   * 無法設定元資料：

      * `Could not set metadata on content fragment`
   * 找不到或無法更新內容元素

      * `Could not update content element`
      * `Could not update fragment data of element`

   詳細的錯誤消息通常按以下方式返回：

   ```xml
   {
     "class": "core/response",
     "properties": {
       "path": "/api/assets/foo/bar/qux",
       "location": "/api/assets/foo/bar/qux.json",
       "parentLocation": "/api/assets/foo/bar.json",
       "status.code": 500,
       "status.message": "...{error message}.."
     }
   }
   ```

## API參考 {#api-reference}

請參閱此處瞭解詳細的API參考：

* [Adobe Experience Manager資產API — 內容片段](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html)
* [Assets HTTP API](/help/assets/mac-api-assets.md)

   * [可用功能](/help/assets/mac-api-assets.md#assets)

## 其他資源 {#additional-resources}

有關詳細資訊，請參閱：

* [資產HTTP API文檔](/help/assets/mac-api-assets.md)
* [AEM Gem會話：OAuth](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-oauth-server-functionality-in-aem.html)
