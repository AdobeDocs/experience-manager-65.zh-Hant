---
title: "[!DNL Assets] HTTP API."
description: 在中使用HTTP API建立、讀取、更新、刪除及管理數位資產 [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Developer
feature: APIs,Assets HTTP API,Developer Tools
exl-id: 6bc10f4e-a951-49ba-9c71-f568a7f2e40d
hide: true
source-git-commit: 71b3f7c6ad2c7712762a29518de6cf0639081cb7
workflow-type: tm+mt
source-wordcount: '1746'
ht-degree: 1%

---

# [!DNL Assets] HTTP API {#assets-http-api}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/mac-api-assets.html?lang=en) |
| AEM 6.5 | 本文章 |

## 概觀 {#overview}

此 [!DNL Assets] HTTP API允許對數位資產進行建立 — 讀取 — 更新 — 刪除(CRUD)操作，包括對中繼資料、轉譯和評論的操作，以及結構化內容使用 [!DNL Experience Manager] 內容片段。 它公開於 `/api/assets` 和實作為REST API。 內容包括 [支援內容片段](/help/assets/assets-api-content-fragments.md).

若要存取API：

1. 開啟API服務檔案，位於 `https://[hostname]:[port]/api.json`.
1. 請遵循 [!DNL Assets] 服務連結前往 `https://[hostname]:[server]/api/assets.json`.

API回應是部分MIME型別的JSON檔案，以及所有MIME型別的回應代碼。 JSON回應為選用專案，且可能無法使用(例如PDF檔案)。 仰賴回應程式碼進行進一步分析或動作。

在 [!UICONTROL 關閉時間]，資產及其轉譯無法透過 [!DNL Assets] 網頁介面以及透過HTTP API。 如果 [!UICONTROL 準時] 是未來或 [!UICONTROL 關閉時間] 是過去的。

>[!CAUTION]
>
>[HTTP API會更新中繼資料屬性](#update-asset-metadata) 在 `jcr` 名稱空間。 不過，Experience Manager使用者介面會更新 `dc` 名稱空間。

## 內容片段 {#content-fragments}

A [內容片段](/help/assets/content-fragments/content-fragments.md) 是一種特殊型別的資產。 它可用來存取結構化資料，例如文字、數字、日期等。 由於有許多差異， `standard` 資產（例如影像或檔案），則處理內容片段會套用一些其他規則。

如需詳細資訊，請參閱 [Experience Manager Assets HTTP API中的內容片段支援](/help/assets/assets-api-content-fragments.md).

## 資料模型 {#data-model}

此 [!DNL Assets] HTTP API會顯示兩個主要元素：資料夾和資產（適用於標準資產）。

此外，它會公開自訂資料模型的更詳細元素，這些模型說明內容片段中的結構化內容。 另請參閱 [內容片段資料模型](/help/assets/assets-api-content-fragments.md#content-fragments) 以取得進一步資訊。

### 資料夾 {#folders}

資料夾就像傳統檔案系統中的目錄。 它們是其他資料夾或判斷提示的容器。 資料夾包含下列元件：

**實體**：資料夾的實體是它的子元素，可以是資料夾和資產。

**屬性**:

* `name` 是資料夾的名稱。 這與URL路徑中沒有副檔名的最後一個區段相同。
* `title` 是資料夾的選用標題，可顯示而非其名稱。

>[!NOTE]
>
>資料夾或資產的某些屬性會對應至不同的首碼。 此 `jcr` 前置詞 `jcr:title`， `jcr:description`、和 `jcr:language` 已取代為 `dc` 前置詞。 因此在傳回的JSON中， `dc:title` 和 `dc:description` 包含下列專案的值： `jcr:title` 和 `jcr:description`，依序輸入。

**連結** 資料夾會顯示三個連結：

* `self`：連結至本身。
* `parent`：連結至上層資料夾。
* `thumbnail`：（選用）連結至資料夾縮圖影像。

### Assets {#assets}

在Experience Manager中，資產包含以下元素：

* 資產的屬性和中繼資料。
* 多種轉譯，例如原始轉譯（原始上傳的資產）、縮圖和各種其他轉譯。 其他轉譯可能是不同大小的影像、不同的視訊編碼，或從PDF或擷取的頁面 [!DNL Adobe InDesign] 檔案。
* 選擇性註解。

如需內容片段中元素的相關資訊，請參閱 [Experience Manager Assets HTTP API中的內容片段支援](/help/assets/assets-api-content-fragments.md#content-fragments).

在 [!DNL Experience Manager] 資料夾包含下列元件：

* 實體：資產的子系是其轉譯。
* 屬性.
* 連結.

此 [!DNL Assets] HTTP API包含下列功能：

* [擷取資料夾清單](#retrieve-a-folder-listing).
* [建立資料夾](#create-a-folder).
* [建立資產](#create-an-asset).
* [更新資產二進位檔](#update-asset-binary).
* [更新資產中繼資料](#update-asset-metadata).
* [建立資產轉譯](#create-an-asset-rendition).
* [更新資產轉譯](#update-an-asset-rendition).
* [建立資產註解](#create-an-asset-comment).
* [複製資料夾或資產](#copy-a-folder-or-asset).
* [行動資料夾或資產](#move-a-folder-or-asset).
* [刪除資料夾、資產或轉譯](#delete-a-folder-asset-or-rendition).

>[!NOTE]
>
>為方便閱讀，下列範例會忽略完整的cURL標籤法。 事實上，標籤法確實與 [重新整理](https://github.com/micha/resty) 的指令碼包裝函式 `cURL`.

**必備條件**

* 存取 `https://[aem_server]:[port]/system/console/configMgr`.
* 瀏覽至 **[!UICONTROL AdobeGranite CSRF篩選器]**.
* 確定屬性 **[!UICONTROL 篩選方法]** 包含： `POST`， `PUT`， `DELETE`.

## 擷取資料夾清單 {#retrieve-a-folder-listing}

擷取現有資料夾及其子系圖元（子資料夾或資產）的Siren表示。

**請求**： `GET /api/assets/myFolder.json`

**回應代碼**：回應程式碼為：

* 200 — 確定 — 成功。
* 404 - NOT FOUND — 資料夾不存在或無法存取。
* 500 — 內部伺服器錯誤 — 如果發生其他錯誤。

**回應**：傳回實體的類別是資產或資料夾。 包含之圖元的屬性是每個圖元之完整屬性集的子集。 為了取得實體的完整表示法，使用者端應擷取具有的連結所指向的URL內容 `rel` 之 `self`.

## 建立資料夾 {#create-a-folder}

建立新的 `sling`： `OrderedFolder` 於指定路徑。 如果 `*` 提供的不是節點名稱，而是引數名稱，此servlet會使用引數名稱作為節點名稱。 接受為請求資料是新資料夾的Siren表示或一組名稱 — 值組，編碼為 `application/www-form-urlencoded` 或 `multipart`/ `form`- `data`，對於直接從HTML表單建立資料夾很有用。 此外，資料夾的屬性可指定為URL查詢引數。

API呼叫失敗，因為 `500` 回應代碼（如果所提供路徑的父節點不存在）。 呼叫傳回回應代碼 `409` 若資料夾已存在。

**引數**： `name` 是資料夾名稱。

**要求**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"jcr:title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"jcr:title=My Folder"`

**回應代碼**：回應程式碼為：

* 201 — 建立 — 成功建立時。
* 409 — 衝突 — 如果資料夾已經存在。
* 412 - PRECONDITION FAILED — 如果找不到或無法存取根集合。
* 500 — 內部伺服器錯誤 — 如果發生其他錯誤。

## 建立資產 {#create-an-asset}

將提供的檔案放置在提供的路徑，以在DAM存放庫中建立資產。 如果 `*` 提供的不是節點名稱，而servlet會使用引數名稱或檔案名稱作為節點名稱。

**引數**：引數為 `name` 資產名稱和 `file` 作為檔案參照。

**要求**

* `POST /api/assets/myFolder/myAsset.png -H"Content-Type: image/png" --data-binary "@myPicture.png"`
* `POST /api/assets/myFolder/* -F"name=myAsset.png" -F"file=@myPicture.png"`

**回應代碼**：回應程式碼為：

* 201 — 已建立 — 資產是否已成功建立。
* 409 — 衝突 — 如果資產已經存在。
* 412 - PRECONDITION FAILED — 如果找不到或無法存取根集合。
* 500 — 內部伺服器錯誤 — 如果發生其他錯誤。

## 更新資產二進位檔 {#update-asset-binary}

更新資產的二進位檔（以原始名稱轉譯）。 如果已設定，更新會觸發預設資產處理工作流程執行。

**請求**： `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: image/png" --data-binary @myPicture.png`

**回應代碼**：回應程式碼為：

* 200 — 確定 — 如果資產已成功更新。
* 404 - NOT FOUND — 如果在提供的URI中找不到或無法存取資產。
* 412 - PRECONDITION FAILED — 如果找不到或無法存取根集合。
* 500 — 內部伺服器錯誤 — 如果發生其他錯誤。

## 更新資產中繼資料 {#update-asset-metadata}

更新資產中繼資料屬性。 如果您更新 `dc:` 名稱空間中，API會更新 `jcr` 名稱空間。 此API不會同步兩個名稱空間下的屬性。

**請求**： `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"jcr:title":"My Asset"}}'`

**回應代碼**：回應程式碼為：

* 200 — 確定 — 如果資產已成功更新。
* 404 - NOT FOUND — 如果在提供的URI中找不到或無法存取資產。
* 412 - PRECONDITION FAILED — 如果找不到或無法存取根集合。
* 500 — 內部伺服器錯誤 — 如果發生其他錯誤。

### 同步中繼資料更新，介於 `dc` 和 `jcr` 名稱空間 {#sync-metadata-between-namespaces}

API方法會更新 `jcr` 名稱空間。 使用使用者介面進行的更新會變更 `dc` 名稱空間。 若要同步處理中繼資料值，請執行下列步驟： `dc` 和 `jcr` 名稱空間，您可以建立工作流程並設定Experience Manager，以在編輯資產時執行工作流程。 使用ECMA指令碼來同步所需的中繼資料屬性。 以下範例指令碼會同步標題字串，介於 `dc:title` 和 `jcr:title`.

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

為資產建立新的資產轉譯。 如果未提供請求引數名稱，則會使用檔案名稱作為轉譯名稱。

**引數**：引數為 `name` 代表轉譯的名稱和 `file` 作為檔案參照。

**要求**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**回應代碼**：回應程式碼為：

* 201 - CREATED — 表示已成功建立轉譯。
* 404 - NOT FOUND — 如果在提供的URI中找不到或無法存取資產。
* 412 - PRECONDITION FAILED — 如果找不到或無法存取根集合。
* 500 — 內部伺服器錯誤 — 如果發生其他錯誤。

## 更新資產轉譯 {#update-an-asset-rendition}

更新會分別以新的二進位資料取代資產轉譯。

**請求**： `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**回應代碼**：回應程式碼為：

* 200 — 確定 — 如果已成功更新轉譯。
* 404 - NOT FOUND — 如果在提供的URI中找不到或無法存取資產。
* 412 - PRECONDITION FAILED — 如果找不到或無法存取根集合。
* 500 — 內部伺服器錯誤 — 如果發生其他錯誤。

## 在資產上新增註解 {#create-an-asset-comment}

建立新的資產註解。

**引數**：引數為 `message` 和的訊息內文 `annotationData` 用於JSON格式的附注資料。

**請求**： `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**回應代碼**：回應程式碼為：

* 201 - CREATED — 如果評論已成功建立。
* 404 - NOT FOUND — 如果在提供的URI中找不到或無法存取資產。
* 412 - PRECONDITION FAILED — 如果找不到或無法存取根集合。
* 500 — 內部伺服器錯誤 — 如果發生其他錯誤。

## 複製資料夾或資產 {#copy-a-folder-or-asset}

將所提供路徑下可用的資料夾或資產複製到新目的地。

**請求標頭**：引數包括：

* `X-Destination` - API解決方案範圍內的新目的地URI，可將資源複製到其中。
* `X-Depth`  — 任一 `infinity` 或 `0`. 使用 `0` 僅複製資源及其屬性，不複製其子項。
* `X-Overwrite`  — 使用 `F` 以防止覆寫現有目的地的資產。

**請求**： `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**回應代碼**：回應程式碼為：

* 201 - CREATED — 若資料夾/資產已複製到不存在的目的地。
* 204 — 無內容 — 若資料夾/資產已複製到現有目的地。
* 412 — 先決條件失敗 — 如果缺少請求標頭。
* 500 — 內部伺服器錯誤 — 如果發生其他錯誤。

## 行動資料夾或資產 {#move-a-folder-or-asset}

將指定路徑的資料夾或資產移至新目的地。

**請求標頭**：引數包括：

* `X-Destination` - API解決方案範圍內的新目的地URI，可將資源複製到其中。
* `X-Depth`  — 任一 `infinity` 或 `0`. 使用 `0` 僅複製資源及其屬性，不複製其子項。
* `X-Overwrite`  — 使用 `T` 強制刪除現有資源或 `F` 以防止覆寫現有資源。

**請求**： `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

不要使用 `/content/dam` 在URL中。 移動資產和覆寫現有資產的範例命令為：

```shell
curl -u admin:admin -X MOVE https://[aem_server]:[port]/api/assets/source/file.png -H "X-Destination: https://[aem_server]:[port]/api/assets/destination/file.png" -H "X-Overwrite: T"
```

**回應代碼**：回應程式碼為：

* 201 - CREATED — 若資料夾/資產已複製到不存在的目的地。
* 204 — 無內容 — 若資料夾/資產已複製到現有目的地。
* 412 — 先決條件失敗 — 如果缺少請求標頭。
* 500 — 內部伺服器錯誤 — 如果發生其他錯誤。

## 刪除資料夾、資產或轉譯 {#delete-a-folder-asset-or-rendition}

在提供的路徑刪除資源(-tree)。

**要求**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**回應代碼**：回應程式碼為：

* 200 — 確定 — 如果資料夾已成功刪除。
* 412 - PRECONDITION FAILED — 如果找不到或無法存取根集合。
* 500 — 內部伺服器錯誤 — 如果發生其他錯誤。

## 提示和限制 {#tips-best-practices-limitations}

* [HTTP API會更新中繼資料屬性](#update-asset-metadata) 在 `jcr` 名稱空間。 不過，Experience Manager使用者介面會更新 `dc` 名稱空間。

* Assets HTTP API未傳回完整的中繼資料。 系統會以硬式編碼撰寫名稱空間，而且只會傳回這些名稱空間。 如需完整的中繼資料，請參閱資產路徑 `/jcr_content/metadata.json`.
