---
title: Adobe Experience Manager資產HTTP API中的內容片段支援
description: 了解在AEM無頭傳送功能的重要一環Assets HTTP API中支援內容片段。
feature: Content Fragments,Assets HTTP API
source-git-commit: 2f647fc640d3809dc684bce397831ab37fb94b07
workflow-type: tm+mt
source-wordcount: '1934'
ht-degree: 2%

---

# AEM Assets HTTP API 內容片段支援 {#content-fragments-support-in-aem-assets-http-api}

## 概覽 {#overview}

了解在AEM無頭傳送功能的重要一環Assets HTTP API中支援內容片段。

>[!NOTE]
>
>[資產HTTP API](/help/assets/mac-api-assets.md)包含：
>
>* 資產REST API
>* 包括支援內容片段

>
>目前Assets HTTP API的實作是以[REST](https://en.wikipedia.org/wiki/Representational_state_transfer)架構樣式為基礎。

[Assets REST API](/help/assets/mac-api-assets.md)可讓Adobe Experience Manager的開發人員透過CRUD作業（建立、讀取、更新、刪除），直接透過HTTP API存取內容(儲存在AEM中)。

API可讓您將Adobe Experience Manager作為無頭CMS（內容管理系統）來運作，方法是向JavaScript前端應用程式提供內容服務。 或可執行HTTP要求和處理JSON回應的任何其他應用程式。

例如，單頁應用程式(SPA)（以架構為基礎或自訂）需要透過HTTP API提供的內容，通常為JSON格式。

雖然[AEM核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant)提供非常全面、彈性且可自訂的API，可針對此用途提供必要的讀取作業，且可自訂其JSON輸出，但實作時確實需要AEM WCM（Web內容管理）的專業知識，因為它們必須托管於以專用AEM範本為基礎的頁面中。 並非每個SPA開發組織都能直接取得這些知識。

此時即可使用Assets REST API。 開發人員可直接存取資產（例如影像和內容片段），不需先將資產內嵌在頁面中，然後以序列化JSON格式傳送其內容。

>[!NOTE]
>
>無法從Assets REST API自訂JSON輸出。

Assets REST API也可讓開發人員透過建立新資產、更新或刪除現有資產、內容片段和資料夾來修改內容。

Assets REST API:

* 遵循[HATEOAS原則](https://en.wikipedia.org/wiki/HATEOAS)

* 實作[SIREN格式](https://github.com/kevinswiber/siren)

## 必備條件 {#prerequisites}

最新AEM版本的每個現成可用安裝都提供Assets REST API。

## 重要概念 {#key-concepts}

Assets REST API提供[REST](https://en.wikipedia.org/wiki/Representational_state_transfer)樣式的存取權給儲存在AEM例項中的資產。

它使用`/api/assets`端點，且需要資產的路徑來存取它（沒有前導的`/content/dam`）。

* 這表示若要存取資產，請執行下列操作：
   * `/content/dam/path/to/asset`
* 您需要請求：
   * `/api/assets/path/to/asset`

例如，若要存取`/content/dam/wknd/en/adventures/cycling-tuscany`，請求`/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>訪問：
>
>* `/api/assets` **不** 需要使用選取 `.model` 器。
>* `/content/path/to/page` **** 不需要使用選取 `.model` 器。


HTTP方法會決定要執行的操作：

* **GET**  — 擷取資產或資料夾的JSON表示法
* **POST**  — 建立新資產或資料夾
* **PUT**  — 更新資產或資料夾的屬性
* **DELETE**  — 刪除資產或資料夾

>[!NOTE]
>
>請求內文和/或URL參數可用來設定其中一些操作；例如，定義資料夾或資產應由&#x200B;**POST**&#x200B;請求建立。

[API參考](/help/assets/assets-api-content-fragments.md#api-reference)檔案中已定義支援請求的確切格式。

### 交易行為 {#transactional-behavior}

所有請求都是原子。

這表示後續(`write`)請求不能合併為單個實體可能成功或失敗的單個事務。

### AEM(Assets)REST API與AEM元件 {#aem-assets-rest-api-versus-aem-components}

<table>
 <thead>
  <tr>
   <td>外觀</td>
   <td>資產REST API<br/> </td>
   <td>AEM元件<br/>（使用Sling模型的元件）</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>支援的使用案例</td>
   <td>一般用途。</td>
   <td><p>針對單頁應用程式(SPA)或任何其他（內容使用）內容的耗用量最佳化。</p> <p>也可以包含版面資訊。</p> </td>
  </tr>
  <tr>
   <td>支援的操作</td>
   <td><p>建立、讀取、更新、刪除。</p> <p>視實體類型而定，具有其他操作。</p> </td>
   <td>唯讀.</td>
  </tr>
  <tr>
   <td>存取</td>
   <td><p>可直接存取。</p> <p>使用<code>/api/assets </code>端點，對應至<code>/content/dam</code>（在存放庫中）。</p> 
   <p>範例路徑看起來會像： <code>/api/assets/wknd/en/adventures/cycling-tuscany.json</code></p>
   </td>
    <td><p>需透過AEM頁面上的AEM元件參考。</p> <p>使用<code>.model</code>選取器來建立JSON表示法。</p> <p>範例路徑看起來會像：<br/> <code>/content/wknd/language-masters/en/adventures/cycling-tuscany.model.json</code></p> 
   </td>
  </tr>
  <tr>
   <td>安全性</td>
   <td><p>您可以使用多個選項。</p> <p>OAuth被提出；可與標準設定分開設定。</p> </td>
   <td>使用AEM標準設定。</td>
  </tr>
  <tr>
   <td>建築注釋</td>
   <td><p>寫入存取通常會處理製作例項。</p> <p>也可將讀取導向至發佈例項。</p> </td>
   <td>由於此方法為唯讀，因此通常會用於發佈例項。</td>
  </tr>
  <tr>
   <td>輸出</td>
   <td>基於JSON的SIREN輸出：冗長，但功能強大。 允許在內容內導覽。</td>
   <td>基於JSON的專有輸出；可透過Sling Model設定。 導覽內容結構很難實作（但不一定不可能）。</td>
  </tr>
 </tbody>
</table>

### 安全性 {#security}

如果在沒有特定驗證需求的環境中使用AEM REST API，則必須正確設定Assets CORS篩選器。

>[!NOTE]
>
>如需詳細資訊，請參閱：
>
>* [CORS/AEM說明](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html)
>* [影片 — 使用AEM為CORS開發](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/develop-for-cross-origin-resource-sharing.html)

>


在具有特定驗證需求的環境中，建議使用OAuth。

## 可用功能 {#available-features}

內容片段是特定的資產類型，請參閱[使用內容片段](/help/assets/content-fragments/content-fragments.md)。

如需透過API提供之功能的詳細資訊，請參閱：

* [資產REST API](/help/assets/mac-api-assets.md)
* [實體類型](/help/assets/assets-api-content-fragments.md#entity-types)，說明每個支援類型的特定功能（如與內容片段相關）

### 分頁 {#paging}

GETREST API支援透過URL參數進行分頁（適用於資產要求）:

* `offset`  — 要檢索的第一個（子）實體的編號
* `limit`  — 傳回的實體數上限

響應將包含尋呼資訊，作為SIREN輸出的`properties`部分的一部分。 此`srn:paging`屬性包含請求中指定的（子）實體總數(`total`)、偏移和限制(`offset`、`limit`)。

>[!NOTE]
>
>分頁通常套用在容器實體上（即資料夾或含轉譯的資產），因為它與請求的實體的子項相關。

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

## 實體類型 {#entity-types}

### 資料夾 {#folders}

資料夾可作為資產和其他資料夾的容器。 它們反映AEM內容存放庫的結構。

資產REST API會公開資料夾屬性的存取權；例如名稱、標題等。 資產以資料夾子實體和子資料夾的形式公開。

>[!NOTE]
>
>根據子資產和資料夾的資產類型，子實體清單可能已經包含定義各子實體的完整屬性集。 或者，在該子實體清單中，只可針對實體公開縮減的屬性集。

### 資產 {#assets}

如果要求資產，回應會傳回其中繼資料；例如標題、名稱和由個別資產架構定義的其他資訊。

資產的二進位資料以`content`類型的SIREN連結形式公開。

資產可以多次轉譯。 這些格式通常以子實體形式公開，一個例外是縮圖轉譯，該格式副本以`thumbnail`類型(`rel="thumbnail"`)的連結形式公開。

### 內容片段 {#content-fragments}

[內容片段](/help/assets/content-fragments/content-fragments.md)是特殊的資產類型。 它們可用來存取結構化資料，例如文字、數字、日期等。

由於&#x200B;*standard*&#x200B;資產（例如影像或音訊）有幾項差異，因此處理這些差異時會套用其他一些規則。

#### 表示 {#representation}

內容片段：

* 請勿公開任何二進位資料。
* 完全包含在JSON輸出中（位於`properties`屬性內）。

* 也被視為原子，即元素和變異會公開為片段屬性的一部分，而不是連結或子實體。 這允許有效存取片段的裝載。

#### 內容模型和內容片段 {#content-models-and-content-fragments}

目前定義內容片段結構的模型不會透過HTTP API公開。 因此，*consumer*&#x200B;需要了解片段的模型（至少是最小值） — 儘管大部分資訊可從裝載推斷；資料類型等。 是定義的一部分。

若要建立新內容片段，必須提供模型的（內部存放庫）路徑。

#### 相關聯的內容 {#associated-content}

相關內容目前未公開。

## 使用 {#using}

使用方式會因您使用AEM製作環境或發佈環境，以及您的特定使用案例而異。

* 強烈建議建立作業系結至製作例項([，目前沒有方法使用此API](/help/assets/assets-api-content-fragments.md#limitations)復製片段以發佈。
* 兩者皆可傳送，因為AEM只會以JSON格式提供請求的內容。

   * 從AEM製作例項的儲存和傳送應足以在防火牆後、媒體程式庫應用程式中使用。

   * 若為即時Web傳送，建議使用AEM發佈例項。

>[!CAUTION]
>
>AEM例項上的Dispatcher設定可能會封鎖對`/api`的存取。

>[!NOTE]
>
>如需詳細資訊，請參閱[ API參考](/help/assets/assets-api-content-fragments.md#api-reference)。 尤其是[Adobe Experience Manager Assets API — 內容片段](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html)。

### 讀取/傳送 {#read-delivery}

使用方式為：

`GET /{cfParentPath}/{cfName}.json`

例如：

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

回應會序列化JSON，內容會以內容片段中的結構化形式顯示。 參考會以參考URL的形式傳送。

可能有兩種讀取操作：

* 依路徑讀取特定內容片段，這會傳回內容片段的JSON表示法。
* 依路徑讀取內容片段的資料夾：這會傳回資料夾中所有內容片段的JSON表示法。

### 建立 {#create}

使用方式為：

`POST /{cfParentPath}/{cfName}`

內文必須包含要建立之內容片段的JSON表示法，包括應在內容片段元素上設定的任何初始內容。 必須設定`cq:model`屬性，且必須指向有效的內容片段模型。 若無法這麼做，將會導致錯誤。 還需要添加設為`application/json`的標題`Content-Type`。

### 更新 {#update}

使用方式為

`PUT /{cfParentPath}/{cfName}`

內文必須包含指定內容片段要更新內容的JSON表示法。

這只能是內容片段的標題或說明、單一元素或所有元素值和/或中繼資料。

### 刪除 {#delete}

使用方式為：

`DELETE /{cfParentPath}/{cfName}`

## 限制 {#limitations}

有幾項限制：

* **目前不支援內容片段模型**:無法讀取或建立。若要建立新內容片段或更新現有內容片段，開發人員必須知道內容片段模型的正確路徑。 目前唯一可透過管理UI來取得這些概觀的方法。
* **會忽略參考**。目前沒有檢查是否參考現有內容片段。 因此，例如，刪除內容片段可能會在包含對已刪除內容片段之參考的頁面上造成問題。
* **JSON資** 料類型JSON資料類型的REST API輸 *出目* 前是 *以字串為基礎的輸出*。

## 狀態代碼和錯誤消息 {#status-codes-and-error-messages}

在相關情況下，可看到下列狀態代碼：

* **200** (OK)在以下情況下返回：

   * 透過`GET`請求內容片段
   * 透過`PUT`成功更新內容片段

* **201** （已建立）在下列情況下傳回：

   * 透過`POST`成功建立內容片段

* **404** （找不到）在下列情況下返回：

   * 請求的內容片段不存在

* **500** （內部伺服器錯誤）

   >[!NOTE]
   >
   >傳回此錯誤：
   >
   >* 無法識別特定程式碼的錯誤發生時
   >* 當指定的有效負載無效時


   以下列出返回此錯誤狀態時的常見情況，以及生成的錯誤消息（空格）:

   * 父資料夾不存在（透過`POST`建立內容片段時）
   * 未提供內容片段模型（缺少cq:model）、無法讀取（由於路徑無效或權限問題）或沒有有效的片段模型：

      * `No content fragment model specified`
      * `Cannot create a resource of given model '/foo/bar/qux'`
   * 無法建立內容片段（可能是權限問題）:

      * `Could not create content fragment`
   * 無法更新標題和說明：

      * `Could not set value on content fragment`
   * 無法設定元資料：

      * `Could not set metadata on content fragment`
   * 找不到內容元素或無法更新

      * `Could not update content element`
      * `Could not update fragment data of element`

   詳細的錯誤訊息通常會以下列方式傳回：

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

如需詳細的API參考，請參閱這裡：

* [Adobe Experience Manager Assets API — 內容片段](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/assets-api-content-fragments/index.html)
* [Assets HTTP API](/help/assets/mac-api-assets.md)

   * [可用功能](/help/assets/mac-api-assets.md#assets)

## 其他資源 {#additional-resources}

如需詳細資訊，請參閱：

* [Assets HTTP API檔案](/help/assets/mac-api-assets.md)
* [AEM Gem課程：OAuth](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-oauth-server-functionality-in-aem.html)
