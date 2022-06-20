---
title: '"[!DNL Assets] HTTP API。"'
description: 使用HTTP API建立、讀取、更新、刪除、管理數字資產 [!DNL Adobe Experience Manager Assets]。
contentOwner: AG
role: Developer
feature: APIs,Assets HTTP API,Developer Tools
exl-id: 6bc10f4e-a951-49ba-9c71-f568a7f2e40d
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
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

的 [!DNL Assets] HTTP API允許對數字資產（包括元資料、格式副本和注釋）以及結構化內容（使用）執行建立 — 讀取 — 更新 — 刪除(CRUD)操作 [!DNL Experience Manager] 內容片段。 它在 `/api/assets` 並作為REST API實現。 包括 [支援內容片段](/help/assets/assets-api-content-fragments.md)。

要訪問API:

1. 在以下位置開啟API服務文檔： `https://[hostname]:[port]/api.json`。
1. 關注 [!DNL Assets] 服務連結導向 `https://[hostname]:[server]/api/assets.json`。

API響應是某些MIME類型的JSON檔案，是所有MIME類型的響應代碼。 JSON響應是可選的，可能不可用，例如，PDF檔案。 依靠響應代碼進行進一步分析或操作。

在 [!UICONTROL 關機時間]，資產及其格式副本不可通過 [!DNL Assets] Web介面和通過HTTP API。 如果 [!UICONTROL 準時] 是將來的 [!UICONTROL 關機時間] 是過去。

>[!CAUTION]
>
>[HTTP API更新元資料屬性](#update-asset-metadata) 的 `jcr` 命名空間。 但是，Experience Manager用戶介面將更新 `dc` 命名空間。

## 內容片段 {#content-fragments}

A [內容片段](/help/assets/content-fragments/content-fragments.md) 是一種特殊的資產類型。 它可用於訪問結構化資料，如文本、數字、日期等。 由於有幾種不同 `standard` 資產（如影像或文檔），某些附加規則適用於處理內容片段。

有關詳細資訊，請參閱 [Experience Manager AssetsHTTP API中的內容片段支援](/help/assets/assets-api-content-fragments.md)。

## 資料模型 {#data-model}

的 [!DNL Assets] HTTP API公開兩個主要元素，資料夾和資產（對於標準資產）。

此外，它還為描述內容片段中結構化內容的自定義資料模型顯示了更詳細的元素。 請參閱 [內容片段資料模型](/help/assets/assets-api-content-fragments.md#content-fragments) 的上界。

### 資料夾 {#folders}

資料夾類似於傳統檔案系統中的目錄。 它們是其他資料夾或斷言的容器。 資料夾具有以下元件：

**實體**:資料夾的實體是其子元素，可以是資料夾和資產。

**屬性**:

* `name` 是資料夾的名稱。 這與URL路徑中沒有副檔名的最後一個段相同。
* `title` 是資料夾的可選標題，可以顯示該標題，而不是其名稱。

>[!NOTE]
>
>資料夾或資產的某些屬性映射到其他前置詞。 的 `jcr` 前置詞 `jcr:title`。 `jcr:description`, `jcr:language` 替換為 `dc` 前置詞。 因此，在返回的JSON中， `dc:title` 和 `dc:description` 包含 `jcr:title` 和 `jcr:description`的下界。

**連結** 資料夾公開三個連結：

* `self`:連結到自身。
* `parent`:連結到父資料夾。
* `thumbnail`:（可選）指向資料夾縮略圖的連結。

### Assets {#assets}

在Experience Manager中，資產包含以下元素：

* 資產的屬性和元資料。
* 多個格式副本，如原始格式副本（最初上載的資產）、縮略圖和各種其他格式副本。 其他格式副本可以是不同大小的影像、不同的視頻編碼，或從PDF或 [!DNL Adobe InDesign] 的子菜單。
* 可選注釋。

有關內容片段中元素的資訊，請參見 [Experience Manager AssetsHTTP API中的內容片段支援](/help/assets/assets-api-content-fragments.md#content-fragments)。

在 [!DNL Experience Manager] 資料夾具有以下元件：

* 實體：資產的子項是其格式副本。
* 屬性.
* 連結.

的 [!DNL Assets] HTTP API包括以下功能：

* [檢索資料夾清單](#retrieve-a-folder-listing)。
* [建立資料夾](#create-a-folder)。
* [建立資產](#create-an-asset)。
* [更新資產二進位](#update-asset-binary)。
* [更新資產元資料](#update-asset-metadata)。
* [建立資產格式副本](#create-an-asset-rendition)。
* [更新資產格式副本](#update-an-asset-rendition)。
* [建立資產注釋](#create-an-asset-comment)。
* [複製資料夾或資產](#copy-a-folder-or-asset)。
* [移動資料夾或資產](#move-a-folder-or-asset)。
* [刪除資料夾、資產或格式副本](#delete-a-folder-asset-or-rendition)。

>[!NOTE]
>
>為便於讀取，以下示例省略了完整的cURL符號。 事實上，符號的確與 [雷斯蒂](https://github.com/micha/resty) 是的 `cURL`。

**必備條件**

* 存取 `https://[aem_server]:[port]/system/console/configMgr`.
* 導航到 **[!UICONTROL Adobe花崗岩CSRF濾池]**。
* 確保屬性 **[!UICONTROL 篩選方法]** 包括： `POST`。 `PUT`。 `DELETE`。

## 檢索資料夾清單 {#retrieve-a-folder-listing}

檢索現有資料夾及其子實體（子資料夾或資產）的Siren表示法。

**請求**: `GET /api/assets/myFolder.json`

**響應代碼**:響應代碼為：

* 200 — 好 — 成功。
* 404 — 未找到 — 資料夾不存在或無法訪問。
* 500 — 內部伺服器錯誤 — 如果出現其他問題。

**響應**:返回的實體類是資產或資料夾。 包含的實體的屬性是每個實體的全部屬性集的子集。 為了獲得實體的完整表示形式，客戶端應檢索連結指向的URL的內容 `rel` 共 `self`。

## 建立資料夾 {#create-a-folder}

建立新 `sling`: `OrderedFolder` 在給定路徑上。 如果 `*` 提供而不是節點名稱，servlet將參數名稱用作節點名稱。 接受為請求資料是新資料夾的Siren表示形式或一組名稱 — 值對，編碼為 `application/www-form-urlencoded` 或 `multipart`/ `form`- `data`，用於直接從HTML窗體建立資料夾。 此外，可以將資料夾的屬性指定為URL查詢參數。

API調用失敗， `500` 響應代碼（如果提供路徑的父節點不存在）。 呼叫返迴響應代碼 `409` 資料夾。

**參數**: `name` 是資料夾名稱。

**要求**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"jcr:title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"jcr:title=My Folder"`

**響應代碼**:響應代碼為：

* 201 — 建立 — 成功建立。
* 409 — 衝突 — 如果資料夾已存在。
* 412 - PRECONTIDE FAILED — 如果找不到或無法訪問根集合。
* 500 — 內部伺服器錯誤 — 如果出現其他問題。

## 建立資產 {#create-an-asset}

將提供的檔案放在提供的路徑上，以在DAM儲存庫中建立資產。 如果 `*` 提供而不是節點名稱，servlet使用參數名或檔案名作為節點名稱。

**參數**:參數為 `name` 資產名稱和 `file` 的子菜單。

**要求**

* `POST /api/assets/myFolder/myAsset.png -H"Content-Type: image/png" --data-binary "@myPicture.png"`
* `POST /api/assets/myFolder/* -F"name=myAsset.png" -F"file=@myPicture.png"`

**響應代碼**:響應代碼為：

* 201 — 已建立 — 如果資產已成功建立。
* 409 — 衝突 — 如果資產已存在。
* 412 - PRECONTIDE FAILED — 如果找不到或無法訪問根集合。
* 500 — 內部伺服器錯誤 — 如果出現其他問題。

## 更新資產二進位 {#update-asset-binary}

更新資產的二進位檔案（名稱為原始格式的格式副本）。 更新觸發要執行的預設資產處理工作流（如果已配置）。

**請求**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: image/png" --data-binary @myPicture.png`

**響應代碼**:響應代碼為：

* 200 — 確定 — 如果資產已成功更新。
* 404 — 未找到 — 如果在提供的URI中找不到或無法訪問資產。
* 412 - PRECONTIDE FAILED — 如果找不到或無法訪問根集合。
* 500 — 內部伺服器錯誤 — 如果出現其他問題。

## 更新資產元資料 {#update-asset-metadata}

更新資產元資料屬性。 如果更新中的任何屬性 `dc:` 命名空間， API更新 `jcr` 命名空間。 API不同步兩個命名空間下的屬性。

**請求**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"jcr:title":"My Asset"}}'`

**響應代碼**:響應代碼為：

* 200 — 確定 — 如果資產已成功更新。
* 404 — 未找到 — 如果在提供的URI中找不到或無法訪問資產。
* 412 - PRECONTIDE FAILED — 如果找不到或無法訪問根集合。
* 500 — 內部伺服器錯誤 — 如果出現其他問題。

### 同步元資料更新 `dc` 和 `jcr` 命名空間 {#sync-metadata-between-namespaces}

API方法更新中的元資料屬性 `jcr` 命名空間。 使用用戶介面進行的更新更改了 `dc` 命名空間。 在以下位置同步元資料值： `dc` 和 `jcr` 命名空間，您可以建立工作流並配置Experience Manager以在資產編輯時執行工作流。 使用ECMA指令碼同步所需的元資料屬性。 以下示例指令碼將標題字串同步於 `dc:title` 和 `jcr:title`。

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

## 建立資產格式副本 {#create-an-asset-rendition}

為資產建立新資產格式副本。 如果未提供請求參數名，則檔案名將用作格式副本名稱。

**參數**:參數為 `name` 格式副本的名稱和 `file` 檔案引用。

**要求**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**響應代碼**:響應代碼為：

* 201 — 已建立 — 如果已成功建立格式副本。
* 404 — 未找到 — 如果在提供的URI中找不到或無法訪問資產。
* 412 - PRECONTIDE FAILED — 如果找不到或無法訪問根集合。
* 500 — 內部伺服器錯誤 — 如果出現其他問題。

## 更新資產格式副本 {#update-an-asset-rendition}

更新分別用新二進位資料替換資產格式副本。

**請求**: `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**響應代碼**:響應代碼為：

* 200 — 確定 — 如果格式副本已成功更新。
* 404 — 未找到 — 如果在提供的URI中找不到或無法訪問資產。
* 412 - PRECONTIDE FAILED — 如果找不到或無法訪問根集合。
* 500 — 內部伺服器錯誤 — 如果出現其他問題。

## 在資產上添加註釋 {#create-an-asset-comment}

建立新資產注釋。

**參數**:參數為 `message` 以獲取注釋和 `annotationData` 標籤。

**請求**: `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**響應代碼**:響應代碼為：

* 201 — 已建立 — 如果已成功建立注釋。
* 404 — 未找到 — 如果在提供的URI中找不到或無法訪問資產。
* 412 - PRECONTIDE FAILED — 如果找不到或無法訪問根集合。
* 500 — 內部伺服器錯誤 — 如果出現其他問題。

## 複製資料夾或資產 {#copy-a-folder-or-asset}

複製在提供的路徑中可用到新目標的資料夾或資產。

**請求標題**:參數包括：

* `X-Destination` - API解決方案作用域內的新目標URI，將資源複製到。
* `X-Depth` - `infinity` 或 `0`。 使用 `0` 只複製資源及其屬性，而不複製其子項。
* `X-Overwrite`  — 使用 `F` 來防止覆蓋現有目標上的資產。

**請求**: `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**響應代碼**:響應代碼為：

* 201 — 已建立 — 如果資料夾/資產已複製到非現有目標。
* 204 — 無內容 — 如果資料夾/資產已複製到現有目標。
* 412 - PRECONTIDE FAILED — 如果缺少請求標頭。
* 500 — 內部伺服器錯誤 — 如果出現其他問題。

## 移動資料夾或資產 {#move-a-folder-or-asset}

將給定路徑上的資料夾或資產移動到新目標。

**請求標題**:參數包括：

* `X-Destination` - API解決方案作用域內的新目標URI，將資源複製到。
* `X-Depth` - `infinity` 或 `0`。 使用 `0` 只複製資源及其屬性，而不複製其子項。
* `X-Overwrite`  — 使用 `T` 強制刪除現有資源或 `F` 來防止覆蓋現有資源。

**請求**: `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

不使用 `/content/dam` 的子菜單。 移動資產並覆蓋現有資產的命令示例如下：

```shell
curl -u admin:admin -X MOVE https://[aem_server]:[port]/api/assets/source/file.png -H "X-Destination: http://[aem_server]:[port]/api/assets/destination/file.png" -H "X-Overwrite: T"
```

**響應代碼**:響應代碼為：

* 201 — 已建立 — 如果資料夾/資產已複製到非現有目標。
* 204 — 無內容 — 如果資料夾/資產已複製到現有目標。
* 412 - PRECONTIDE FAILED — 如果缺少請求標頭。
* 500 — 內部伺服器錯誤 — 如果出現其他問題。

## 刪除資料夾、資產或格式副本 {#delete-a-folder-asset-or-rendition}

刪除所提供路徑上的資源(-tree)。

**要求**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**響應代碼**:響應代碼為：

* 200 — 確定 — 如果資料夾已成功刪除。
* 412 - PRECONTIDE FAILED — 如果找不到或無法訪問根集合。
* 500 — 內部伺服器錯誤 — 如果出現其他問題。

## 提示和限制 {#tips-best-practices-limitations}

* [HTTP API更新元資料屬性](#update-asset-metadata) 的 `jcr` 命名空間。 但是，Experience Manager用戶介面將更新 `dc` 命名空間。

* 資產HTTP API不返回完整的元資料。 命名空間是硬編碼的，只返回那些命名空間。 有關完整元資料，請參閱資產路徑 `/jcr_content/metadata.json`。
