---
title: "[!DNL Assets] HTTP API."
description: 在以下位置使用HTTP API建立、讀取、更新、刪除、管理數位資產： [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Developer
feature: APIs,Assets HTTP API,Developer Tools
exl-id: 6bc10f4e-a951-49ba-9c71-f568a7f2e40d
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '1758'
ht-degree: 1%

---

# [!DNL Assets] HTTP API {#assets-http-api}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/mac-api-assets.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-64/assets/extending/mac-api-assets.html?lang=en) |

## 概觀 {#overview}

此 [!DNL Assets] HTTP API允許對數位資產（包括中繼資料、轉譯和註解）以及使用的結構化內容執行建立 — 讀取 — 更新 — 刪除(CRUD)操作 [!DNL Experience Manager] 內容片段。 在 `/api/assets` 並實作為REST API。 包括 [支援內容片段](/help/assets/assets-api-content-fragments.md).

若要存取API:

1. 在開啟API服務檔案： `https://[hostname]:[port]/api.json`.
1. 關注 [!DNL Assets] 服務連結導向 `https://[hostname]:[server]/api/assets.json`.

API回應是某些MIME類型的JSON檔案，也是所有MIME類型的回應代碼。 JSON回應為選用，例如PDF檔案可能無法使用。 請仰賴回應程式碼進行進一步分析或動作。

在 [!UICONTROL 關閉時間]，資產及其轉譯無法透過 [!DNL Assets] 網頁介面和透過HTTP API。 若 [!UICONTROL 準時] 是未來或 [!UICONTROL 關閉時間] 是過去。

>[!CAUTION]
>
>[HTTP API會更新中繼資料屬性](#update-asset-metadata) 在 `jcr` 命名空間。 不過，Experience Manager使用者介面會更新 `dc` 命名空間。

## 內容片段 {#content-fragments}

A [內容片段](/help/assets/content-fragments/content-fragments.md) 是資產的特殊類型。 它可用來存取結構化資料，例如文字、數字、日期等。 因為 `standard` 資產（例如影像或檔案）、其他一些規則適用於處理內容片段。

如需詳細資訊，請參閱 [Experience Manager Assets HTTP API中的內容片段支援](/help/assets/assets-api-content-fragments.md).

## 資料模型 {#data-model}

此 [!DNL Assets] HTTP API公開兩個主要元素、資料夾和資產（適用於標準資產）。

此外，也會針對描述內容片段中結構化內容的自訂資料模型，公開更詳細的元素。 請參閱 [內容片段資料模型](/help/assets/assets-api-content-fragments.md#content-fragments) 以取得更多資訊。

### 資料夾 {#folders}

資料夾與傳統檔案系統中的目錄類似。 它們是其他資料夾或聲明的容器。 資料夾具有下列元件：

**實體**:資料夾的實體是其子元素，可以是資料夾和資產。

**屬性**:

* `name` 是資料夾的名稱。 這與URL路徑中沒有副檔名的最後一個區段相同。
* `title` 是資料夾的選用標題，可顯示該標題而非其名稱。

>[!NOTE]
>
>資料夾或資產的某些屬性會對應至不同的首碼。 此 `jcr` 前置詞 `jcr:title`, `jcr:description`，和 `jcr:language` 取代為 `dc` 前置詞。 因此，在傳回的JSON中， `dc:title` 和 `dc:description` 包含 `jcr:title` 和 `jcr:description`，分別為。

**連結** 資料夾會公開三個連結：

* `self`:連結到自己。
* `parent`:連結至父資料夾。
* `thumbnail`:（選用）連結至資料夾縮圖影像。

### 資產 {#assets}

在Experience Manager中，資產包含下列元素：

* 資產的屬性和中繼資料。
* 多個轉譯，例如原始轉譯（原本上傳的資產）、縮圖和各種其他轉譯。 其他轉譯可能是不同大小的影像、不同的視訊編碼，或是從PDF或 [!DNL Adobe InDesign] 檔案。
* 可選注釋。

如需內容片段中元素的相關資訊，請參閱 [Experience Manager Assets HTTP API中的內容片段支援](/help/assets/assets-api-content-fragments.md#content-fragments).

在 [!DNL Experience Manager] 資料夾具有下列元件：

* 實體：資產的子項即為其轉譯。
* 屬性.
* 連結.

此 [!DNL Assets] HTTP API包含下列功能：

* [檢索資料夾清單](#retrieve-a-folder-listing).
* [建立資料夾](#create-a-folder).
* [建立資產](#create-an-asset).
* [更新資產二進位檔](#update-asset-binary).
* [更新資產中繼資料](#update-asset-metadata).
* [建立資產轉譯](#create-an-asset-rendition).
* [更新資產轉譯](#update-an-asset-rendition).
* [建立資產註解](#create-an-asset-comment).
* [複製資料夾或資產](#copy-a-folder-or-asset).
* [移動資料夾或資產](#move-a-folder-or-asset).
* [刪除資料夾、資產或轉譯](#delete-a-folder-asset-or-rendition).

>[!NOTE]
>
>為方便閱讀，下列範例會忽略完整的cURL標籤法。 事實上，標籤法與 [雷斯蒂](https://github.com/micha/resty) 是 `cURL`.

**必備條件**

* 存取 `https://[aem_server]:[port]/system/console/configMgr`.
* 導覽至 **[!UICONTROL AdobeGranite CSRF篩選器]**.
* 確認屬性 **[!UICONTROL 篩選方法]** 包括： `POST`, `PUT`, `DELETE`.

## 檢索資料夾清單 {#retrieve-a-folder-listing}

檢索現有資料夾及其子實體（子資料夾或資產）的Siren表示。

**要求**: `GET /api/assets/myFolder.json`

**回應代碼**:回應代碼為：

* 200 — 好 — 成功。
* 404 — 找不到 — 資料夾不存在或無法存取。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

**回應**:傳回的實體類別為資產或資料夾。 包含實體的屬性是每個實體的全部屬性集的子集。 為了取得實體的完整表示法，用戶端應擷取連結所指向之URL的內容，該連結具有 `rel` of `self`.

## 建立資料夾 {#create-a-folder}

建立新 `sling`: `OrderedFolder` 在給定的路徑。 若 `*` 提供的servlet不是節點名稱，而是使用參數名稱作為節點名稱。 「接受為請求」資料是新資料夾的Siren表示，或是一組名稱值對，編碼為 `application/www-form-urlencoded` 或 `multipart`/ `form`- `data`，適合直接從HTML表單建立資料夾。 此外，資料夾的屬性可指定為URL查詢參數。

API呼叫會以 `500` 回應代碼（如果提供路徑的父節點不存在）。 呼叫會傳回回應代碼 `409` 如果資料夾已存在。

**參數**: `name` 是資料夾名稱。

**要求**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"jcr:title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"jcr:title=My Folder"`

**回應代碼**:回應代碼為：

* 201 — 建立 — 成功建立時。
* 409 — 衝突 — 如果資料夾已存在。
* 412 - PINCEPORATE FAILED — 如果找不到或存取根集合。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 建立資產 {#create-an-asset}

將提供的檔案放置在提供的路徑中，以便在DAM存放庫中建立資產。 若 `*` 提供的servlet而不是節點名稱，該servlet將參數名稱或檔案名用作節點名稱。

**參數**:參數為 `name` 針對資產名稱和 `file` （用於檔案引用）。

**要求**

* `POST /api/assets/myFolder/myAsset.png -H"Content-Type: image/png" --data-binary "@myPicture.png"`
* `POST /api/assets/myFolder/* -F"name=myAsset.png" -F"file=@myPicture.png"`

**回應代碼**:回應代碼為：

* 201 — 已建立 — 如果資產已成功建立。
* 409 — 衝突 — 如果資產已存在。
* 412 - PINCEPORATE FAILED — 如果找不到或存取根集合。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 更新資產二進位檔 {#update-asset-binary}

更新資產的二進位檔（名稱為原始的轉譯）。 更新會觸發預設資產處理工作流程來執行（如果已設定）。

**要求**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: image/png" --data-binary @myPicture.png`

**回應代碼**:回應代碼為：

* 200 — 確定 — 如果資產已成功更新。
* 404 — 找不到 — 如果在提供的URI中找不到或存取資產。
* 412 - PINCEPORATE FAILED — 如果找不到或存取根集合。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 更新資產中繼資料 {#update-asset-metadata}

更新資產中繼資料屬性。 如果您更新 `dc:` 命名空間，API會更新 `jcr` 命名空間。 API不會同步兩個命名空間下的屬性。

**要求**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"jcr:title":"My Asset"}}'`

**回應代碼**:回應代碼為：

* 200 — 確定 — 如果資產已成功更新。
* 404 — 找不到 — 如果在提供的URI中找不到或存取資產。
* 412 - PINCEPORATE FAILED — 如果找不到或存取根集合。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

### 同步中繼資料更新於 `dc` 和 `jcr` 命名空間 {#sync-metadata-between-namespaces}

API方法會更新 `jcr` 命名空間。 使用使用者介面進行的更新會變更 `dc` 命名空間。 同步中繼資料值的方式 `dc` 和 `jcr` 命名空間，您可以建立工作流程並設定Experience Manager以在資產編輯時執行工作流程。 使用ECMA指令碼來同步所需的中繼資料屬性。 下列範例指令碼會在 `dc:title` 和 `jcr:title`.

```javascript
var workflowData = workItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH")
{
 var path = workflowData.getPayload().toString();
 var node = workflowSession.getSession().getItem(path);
 var metadataNode = node.getNode("jcr:content/metadata");
 var jcrcontentNode = node.getNode("jcr:content");
if (jcrcontentNode.hasProperty("jcr:title"))
{
 var jcrTitle = jcrcontentNode.getProperty("jcr:title");
 metadataNode.setProperty("dc:title", jcrTitle.toString());
 metadataNode.save();
}
}
```

## 建立資產轉譯 {#create-an-asset-rendition}

為資產建立新的資產轉譯。 如果未提供請求參數名稱，則會將檔案名稱用作格式副本名稱。

**參數**:參數為 `name` 格式副本的名稱，以及 `file` 作為檔案參考。

**要求**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**回應代碼**:回應代碼為：

* 201 — 已建立 — 如果已成功建立轉譯。
* 404 — 找不到 — 如果在提供的URI中找不到或存取資產。
* 412 - PINCEPORATE FAILED — 如果找不到或存取根集合。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 更新資產轉譯 {#update-an-asset-rendition}

更新會分別以新的二進位資料取代資產轉譯。

**要求**: `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**回應代碼**:回應代碼為：

* 200 — 確定 — 如果已成功更新轉譯。
* 404 — 找不到 — 如果在提供的URI中找不到或存取資產。
* 412 - PINCEPORATE FAILED — 如果找不到或存取根集合。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 在資產上新增註解 {#create-an-asset-comment}

建立新資產註解。

**參數**:參數為 `message` 以取得留言的訊息內文，並 `annotationData` ，以取得JSON格式的附註資料。

**要求**: `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**回應代碼**:回應代碼為：

* 201 — 已建立 — 如果已成功建立注釋。
* 404 — 找不到 — 如果在提供的URI中找不到或存取資產。
* 412 - PINCEPORATE FAILED — 如果找不到或存取根集合。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 複製資料夾或資產 {#copy-a-folder-or-asset}

複製提供路徑中可用的資料夾或資產，以前往新目的地。

**請求標題**:參數為：

* `X-Destination` - API解決方案範圍內的新目標URI，可將資源複製到。
* `X-Depth` - `infinity` 或 `0`. 使用 `0` 僅複製資源及其屬性，而不複製其子項。
* `X-Overwrite`  — 使用 `F` 防止覆寫現有目的地的資產。

**要求**: `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**回應代碼**:回應代碼為：

* 201 — 已建立 — 如果資料夾/資產已複製至非現有目的地。
* 204 — 無內容 — 如果資料夾/資產已複製至現有目的地。
* 412 — 先決條件失敗 — 如果缺少請求標題。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 移動資料夾或資產 {#move-a-folder-or-asset}

將指定路徑的資料夾或資產移至新目的地。

**請求標題**:參數為：

* `X-Destination` - API解決方案範圍內的新目標URI，可將資源複製到。
* `X-Depth` - `infinity` 或 `0`. 使用 `0` 僅複製資源及其屬性，而不複製其子項。
* `X-Overwrite`  — 使用 `T` 強制刪除現有資源或 `F` 防止覆寫現有資源。

**要求**: `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

請勿使用 `/content/dam` 中。 移動資產並覆寫現有資產的範例命令如下：

```shell
curl -u admin:admin -X MOVE https://[aem_server]:[port]/api/assets/source/file.png -H "X-Destination: https://[aem_server]:[port]/api/assets/destination/file.png" -H "X-Overwrite: T"
```

**回應代碼**:回應代碼為：

* 201 — 已建立 — 如果資料夾/資產已複製至非現有目的地。
* 204 — 無內容 — 如果資料夾/資產已複製至現有目的地。
* 412 — 先決條件失敗 — 如果缺少請求標題。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 刪除資料夾、資產或轉譯 {#delete-a-folder-asset-or-rendition}

刪除提供路徑上的資源(-tree)。

**要求**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**回應代碼**:回應代碼為：

* 200 — 確定 — 如果已成功刪除資料夾。
* 412 - PINCEPORATE FAILED — 如果找不到或存取根集合。
* 500 — 內部伺服器錯誤 — 如果有其他問題。

## 提示和限制 {#tips-best-practices-limitations}

* [HTTP API會更新中繼資料屬性](#update-asset-metadata) 在 `jcr` 命名空間。 不過，Experience Manager使用者介面會更新 `dc` 命名空間。

* 資產HTTP API不會傳回完整的中繼資料。 命名空間會以硬式編碼撰寫，且只會傳回那些命名空間。 如需完整的中繼資料，請參閱資產路徑 `/jcr_content/metadata.json`.
