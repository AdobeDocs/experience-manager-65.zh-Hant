---
title: Assets HTTP API中的Adobe Experience Manager內容片段支援
description: 瞭解資產HTTP API支援內容片段，這是AEM Headless傳送功能的重要部分。
feature: Content Fragments,Assets HTTP API
role: Developer
exl-id: 0f9efb47-a8d1-46d9-b3ff-a6c0741ca138
hide: true
source-git-commit: 48131c5accfe73b83197bd581ed5a22bc4890a56
workflow-type: tm+mt
source-wordcount: '1957'
ht-degree: 24%

---

# AEM Assets HTTP API 內容片段支援 {#content-fragments-support-in-aem-assets-http-api}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/assets-api-content-fragments.html?lang=zh-Hant) |
| AEM 6.5 | 本文 |


## 概觀 {#overview}

瞭解資產HTTP API支援內容片段，這是AEM Headless傳送功能的重要部分。

>[!NOTE]
>
>此 [Assets HTTP API](/help/assets/mac-api-assets.md) 包含：
>
>* Assets REST API
>* 包含支援內容片段
>
>Assets HTTP API目前的實施是根據 [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) 架構樣式。

此 [Assets REST API](/help/assets/mac-api-assets.md) 可讓Adobe Experience Manager的開發人員透過CRUD操作（建立、讀取、更新、刪除），直接透過HTTP API存取內容(儲存在AEM中)。

此API可讓您藉由向JavaScript前端應用程式提供內容服務，將Adobe Experience Manager當作Headless CMS （內容管理系統）來運作。 或者任何其他可以執行 HTTP 要求並處理 JSON 回應的應用程式。

例如，單頁應用程式(SPA)，以框架為基礎或自訂，需要透過HTTP API提供的內容，通常為JSON格式。

當 [AEM Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 提供非常完整、彈性且可自訂的API，可提供此用途所需的讀取作業，且可自訂其JSON輸出，由於實施作業必須託管於以專用AEM範本為基礎的頁面中，因此實施作業確實需要AEM WCM （網頁內容管理）專門技術。 並非每個SPA開發組織都能直接存取這些知識。

此時可使用Assets REST API。 它可讓開發人員直接存取資產（例如影像和內容片段），而不需要先將資產內嵌在頁面中，並以序列化JSON格式傳送其內容。

>[!NOTE]
>
>無法從Assets REST API自訂JSON輸出。

Assets REST API也可讓開發人員透過建立新、更新或刪除現有資產、內容片段和資料夾來修改內容。

Assets REST API：

* 遵循 [HATEOAS原則](https://en.wikipedia.org/wiki/HATEOAS)

* 實作 [警笛格式](https://github.com/kevinswiber/siren)

## 必備條件 {#prerequisites}

Assets REST API適用於近期AEM版本的每個現成安裝。

## 重要概念 {#key-concepts}

Assets REST API提供 [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) — 樣式存取AEM例項中儲存的資產。

它會使用 `/api/assets` 端點，並需要資產的路徑才能存取該端點(開頭不為 `/content/dam`)。

* 這表示要存取以下位置的資產：
   * `/content/dam/path/to/asset`
* 您需要要求：
   * `/api/assets/path/to/asset`

例如，若要存取 `/content/dam/wknd/en/adventures/cycling-tuscany`，要求 `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>存取：
>
>* `/api/assets`**不需要**&#x200B;使用 `.model` 選擇器。
>* `/content/path/to/page` **需要**&#x200B;使用 `.model` 選擇器。

HTTP 方法決定要執行的操作：

* **GET** - 檢索資產或資料夾的 JSON 表示
* **POST** - 建立新資產或資料夾
* **PUT** - 更新資產或資料夾的屬性
* **DELETE** - 刪除資產或資料夾

>[!NOTE]
>
>要求內文和/或 URL 參數可用於設定其中一些操作；例如，定義資料夾或資產應由 **POST** 要求建立。

受支援請求的確切格式定義於 [API參考](/help/assets/assets-api-content-fragments.md#api-reference) 說明檔案。

### 交易行為 {#transactional-behavior}

所有要求都是原子的。

這表示後續的(`write`)要求無法合併為單一交易，而此交易可作為單一實體成功或失敗。

### AEM (Assets) REST API與AEM元件 {#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>外觀</td>
   <td>Assets REST API<br/> </td>
   <td>AEM元件<br/> （使用Sling模型的元件）</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>支援的使用案例</td>
   <td>一般用途。</td>
   <td><p>針對單頁應用程式(SPA)或任何其他（使用內容）內容中的使用情況最佳化。</p> <p>也可以包含版面配置資訊。</p> </td>
  </tr>
  <tr>
   <td>支援的作業</td>
   <td><p>建立、讀取、更新、刪除。</p> <p>根據圖元型別使用其他操作。</p> </td>
   <td>唯讀.</td>
  </tr>
  <tr>
   <td>存取</td>
   <td><p>可直接存取。</p> <p>使用 <code>/api/assets </code>端點，對應至 <code>/content/dam</code> （在存放庫中）。</p> 
   <p>範例路徑如下所示： <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>需要透過AEM頁面上的AEM元件參考。</p> <p>使用 <code>.model</code> 選取器以建立JSON表示法。</p> <p>範例路徑如下所示：<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>安全性</td>
   <td><p>可能有多個選項。</p> <p>建議使用OAuth；可與標準設定分開設定。</p> </td>
   <td>使用AEM標準設定。</td>
  </tr>
  <tr>
   <td>架構註解</td>
   <td><p>寫入存取權通常會處理作者執行個體。</p> <p>也可以將讀取導向至發佈執行個體。</p> </td>
   <td>由於此方法是唯讀的，它通常用於發佈執行個體。</td>
  </tr>
  <tr>
   <td>輸出</td>
   <td>JSON型SIREN輸出：冗長但功能強大。 允許在內容中導覽。</td>
   <td>JSON型專有輸出；可透過Sling模型設定。 導覽內容結構難以實作（但未必不可能）。</td>
  </tr>
 </tbody>
</table>

### 安全性 {#security}

如果是在沒有特定驗證需求的環境中使用Assets REST API，則需要正確設定AEM CORS篩選器。

>[!NOTE]
>
>如需進一步詳細資訊，請參閱：
>
>* [CORS/AEM 說明](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html)
>* [影片 - 使用 AEM 開發 CORS](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/develop-for-cross-origin-resource-sharing.html)
>

在有特定驗證需求的環境中，建議使用OAuth。

## 可用功能 {#available-features}

內容片段是特定型別的資產，請參閱 [使用內容片段](/help/assets/content-fragments/content-fragments.md).

如需透過API可用功能的進一步資訊，請參閱：

* 此 [Assets REST API](/help/assets/mac-api-assets.md)
* [實體型別](/help/assets/assets-api-content-fragments.md#entity-types)，其中說明每種支援型別（與內容片段相關）的特定功能

### 分頁 {#paging}

Assets REST API支援透過URL引數分頁(針對GET請求)：

* `offset`  — 要擷取的第一個（子項）實體編號
* `limit`  — 傳回的最大實體數

回應將包含分頁資訊，作為 `properties` 部分。 此 `srn:paging` 屬性包含（子）實體的總數( `total`)、位移和限制( `offset`， `limit`)。

>[!NOTE]
>
>分頁通常會套用至容器實體（亦即資料夾或具有轉譯的資產），因為它與請求實體的子系相關。

#### 範例：分頁 {#example-paging}

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

## 實體型別 {#entity-types}

### 資料夾 {#folders}

資料夾可作為資產和其他資料夾的容器。 它們反映了AEM內容存放庫的結構。

Assets REST API會公開資料夾屬性的存取權；例如其名稱、標題等。 資產會公開為資料夾和子資料夾的子實體。

>[!NOTE]
>
>根據子項資產和檔案夾的資產型別，子項實體的清單可能已經包含定義各個子項實體的完整屬性集。 或者，對於此子系圖元清單中的圖元，只能顯示縮減的屬性集。

### Assets {#assets}

如果請求資產，回應會傳回其中繼資料，例如標題、名稱和其他由個別資產結構描述定義的資訊。

資產的二進位資料會公開為型別的SIREN連結 `content`.

資產可以有多個轉譯。 這些通常會顯示為子實體，有一個例外是縮圖轉譯，這會顯示為型別的連結 `thumbnail` ( `rel="thumbnail"`)。

### 內容片段 {#content-fragments}

A [內容片段](/help/assets/content-fragments/content-fragments.md) 是一種特殊型別的資產。 它們可用來存取結構化資料，例如文字、數字、日期等。

由於有幾項差異， *標準* 資產（例如影像或音訊），則處理這些資產需適用其他規則。

#### Presentation {#representation}

內容片段：

* 不要公開任何二進位資料。
* 完全包含在JSON輸出中(在 `properties` 屬性)。

* 也視為原子元素，即元素和變數會作為片段屬性的一部分公開，而會作為連結或子實體公開。 這允許對片段的有效裝載存取。

#### 內容模型和內容片段 {#content-models-and-content-fragments}

目前定義內容片段結構的模型不會透過HTTP API公開。 因此， *消費者* 需要瞭解片段的模型（至少是最低限度） — 儘管大多數資訊可以從承載中推斷；作為資料型別等。 是定義的一部分。

若要建立新內容片段，必須提供模型的（內部存放庫）路徑。

#### 相關聯的內容 {#associated-content}

關聯內容目前未公開。

## 使用 {#using}

根據您使用的是 AEM 作者環境還是發佈環境，以及您的特定使用案例，使用情況可能會有所不同。

* 強烈建議將建立繫結至作者執行個體([目前沒有方法可復製片段以使用此API發佈](/help/assets/assets-api-content-fragments.md#limitations))。
* 都可以從兩者傳遞，因為 AEM 僅以 JSON 格式提供要求的內容。

   * 來自 AEM 作者執行個體的儲存和傳遞操作應該足以滿足防火牆後的媒體庫應用程式的需求。

   * 如果是即時 Web 傳遞，則建議使用 AEM 發佈執行個體。

>[!CAUTION]
>
>AEM執行個體上的Dispatcher設定可能會封鎖對的存取 `/api`.

>[!NOTE]
>
>如需詳細資訊，請參閱 [API參考](/help/assets/assets-api-content-fragments.md#api-reference). 特別是 [Adobe Experience Manager Assets API - 內容片段](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html)。

### 讀取/傳遞 {#read-delivery}

使用方式：

`GET /{cfParentPath}/{cfName}.json`

例如：

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

回應是序列化的 JSON，其內容結構與內容片段中的一樣。參考是以參考 URL 的形式傳遞。

可能有兩種類型的讀取操作：

* 按路徑讀取特定內容片段，這將傳回內容片段的 JSON 表示。
* 按路徑讀取內容片段資料夾：這將傳回資料夾內所有內容片段的 JSON 表示。

### 建立 {#create}

使用方式：

`POST /{cfParentPath}/{cfName}`

內文必須包含要建立的內容片段的 JSON 表示，包括應在內容片段元素上設定的任何初始內容。必須設定 `cq:model` 屬性，並且它必須指向有效的內容片段模型。未這麼做會導致錯誤。也必須加上標頭 `Content-Type`，其設定為 `application/json`。

### 更新 {#update}

使用方式：

`PUT /{cfParentPath}/{cfName}`

內文必須包含給定內容片段要更新之內容的 JSON 表示。

這可以只是內容片段的標題或描述，或單一元素，或所有元素值和/或中繼資料。

### 刪除 {#delete}

使用方式：

`DELETE /{cfParentPath}/{cfName}`

## 限制 {#limitations}

有幾項限制：

* **目前不支援內容片段模型**：無法讀取或建立。 為了能夠建立新的或更新現有的內容片段，開發人員必須知道內容片段模型的正確路徑。 目前，取得這些資訊概觀的唯一方法是透過管理UI。
* **會忽略參照**. 目前沒有檢查現有內容片段是否被引用。 因此，例如，刪除內容片段可能會導致包含已刪除內容片段參照的頁面發生問題。
* **JSON資料型別** 的REST API輸出 *JSON資料型別* 目前為 *字串型輸出*.

## 狀態代碼和錯誤訊息 {#status-codes-and-error-messages}

在相關情況下可以看到下列狀態代碼：

* **200** （確定）傳回時間：

   * 透過請求內容片段 `GET`
   * 透過成功更新內容片段 `PUT`

* **201** （已建立）傳回時間：

   * 透過成功建立內容片段 `POST`

* **404** （找不到）傳回時間：

   * 請求的內容片段不存在

* **500** （內部伺服器錯誤）

  >[!NOTE]
  >
  >傳回此錯誤：
  >
  >* 當發生無法使用特定程式碼識別的錯誤時
  >* 當指定的裝載無效時

  以下列出傳回此錯誤狀態的常見案例，以及產生的錯誤訊息（等寬）：

   * 父資料夾不存在（透過建立內容片段時） `POST`)
   * 未提供任何內容片段模型（缺少cq：model）、無法讀取（由於無效路徑或許可權問題）或沒有有效的片段模型：

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`

   * 無法建立內容片段（可能是許可權問題）：

      * `Could not create content fragment`

   * 無法更新標題和/或說明：

      * `Could not set value on content fragment`

   * 無法設定中繼資料：

      * `Could not set metadata on content fragment`

   * 找不到內容元素或無法更新

      * `Could not update content element`
      * `Could not update fragment data of element`

  詳細錯誤訊息通常會以下列方式傳回：

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

## API 參考 {#api-reference}

如需詳細的API參考資料，請參閱此處：

* [Adobe Experience Manager Assets API - 內容片段](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html)
* [Assets HTTP API](/help/assets/mac-api-assets.md)

   * [可用功能](/help/assets/mac-api-assets.md#assets)

## 其他資源 {#additional-resources}

如需進一步詳細資訊，請參閱：

* [Assets HTTP API檔案](/help/assets/mac-api-assets.md)
* [AEM Gem工作階段： OAuth](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-oauth-server-functionality-in-aem.html)
