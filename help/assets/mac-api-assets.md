---
title: '[!DNL Assets] HTTP API。'
description: 使用 [!DNL Adobe Experience Manager Assets]中的HTTP API建立、讀取、更新、刪除、管理數位資產。
contentOwner: AG
role: 開發人員
feature: API、Assets HTTP API、Developer Tools
exl-id: 6bc10f4e-a951-49ba-9c71-f568a7f2e40d
translation-type: tm+mt
source-git-commit: 15f83387629687994bc2ffee4156d7d42dc1c537
workflow-type: tm+mt
source-wordcount: '1730'
ht-degree: 0%

---

# [!DNL Assets] HTTP API  {#assets-http-api}

## 概覽 {#overview}

[!DNL Assets] HTTP API允許對數位資產（包括中繼資料、轉譯和注釋）以及使用[!DNL Experience Manager]內容片段的結構化內容進行建立——讀取——更新——刪除(CRUD)操作。 它在`/api/assets`公開，並實作為REST API。 它包含[內容片段支援](/help/assets/assets-api-content-fragments.md)。

若要存取API:

1. 在`https://[hostname]:[port]/api.json`開啟API服務檔案。
1. 請遵循[!DNL Assets]服務連結，前往`https://[hostname]:[server]/api/assets.json`。

API回應是某些MIME類型的JSON檔案，也是所有MIME類型的回應代碼。 JSON回應是選擇性的，可能無法使用，例如PDF檔案。 請依賴回應程式碼進行進一步分析或動作。

在[!UICONTROL 關閉時間]之後，資產及其轉譯無法透過[!DNL Assets]網頁介面和HTTP API使用。 如果[!UICONTROL 開機時間]是將來或[!UICONTROL 關機時間]是過去，則API會傳回404錯誤訊息。

>[!CAUTION]
>
>[HTTP API會更新命名空](#update-asset-metadata) 間中的中繼資料 `jcr` 屬性。不過，Experience Manager用戶介面會更新`dc`命名空間中的元資料屬性。

## 內容片段 {#content-fragments}

[內容片段](/help/assets/content-fragments/content-fragments.md)是特殊類型的資產。 它可用來存取結構化資料，例如文字、數字、日期等。 由於`standard`資產（例如影像或檔案）有數項差異，因此處理內容片段時會套用一些其他規則。

如需詳細資訊，請參閱Experience Manager資產HTTP API](/help/assets/assets-api-content-fragments.md)中的「內容片段支援」。[

## 資料模型{#data-model}

[!DNL Assets] HTTP API公開兩個主要元素、資料夾和資產（針對標準資產）。

此外，它還會針對描述「內容片段」中結構化內容的自訂資料模型公開更詳細的元素。 如需詳細資訊，請參閱[內容片段資料模型](/help/assets/assets-api-content-fragments.md#content-fragments)。

### 資料夾 {#folders}

資料夾與傳統檔案系統中的目錄類似。 它們是其他資料夾或斷言的容器。 資料夾具有以下元件：

**實體**:資料夾的實體是其子元素，可以是資料夾和資產。

**屬性**:

* `name` 是資料夾的名稱。這與URL路徑中沒有副檔名的最後一個區段相同。
* `title` 是可顯示的資料夾的可選標題，而非其名稱。

>[!NOTE]
>
>資料夾或資產的某些屬性會對應至不同的首碼。 `jcr:title`、`jcr:description`和`jcr:language`的`jcr`前置詞被`dc`前置詞替換。 因此，在傳回的JSON中，`dc:title`和`dc:description`分別包含`jcr:title`和`jcr:description`的值。

**LinksFolders** 會公開三個連結：

* `self`:連結到自己。
* `parent`:連結至父資料夾。
* `thumbnail`:（選用）資料夾縮圖影像的連結。

### 資產 {#assets}

在Experience Manager中，資產包含下列元素：

* 資產的屬性和中繼資料。
* 多個轉譯，例如原始轉譯（原始上傳的資產）、縮圖和各種其他轉譯。 其他轉譯可能是不同大小的影像、不同的視訊編碼，或從PDF或[!DNL Adobe InDesign]檔案擷取的頁面。
* 選用的注釋。

如需內容片段中元素的詳細資訊，請參閱Experience Manager資產HTTP API](/help/assets/assets-api-content-fragments.md#content-fragments)中的內容片段支援。[

在[!DNL Experience Manager]中，資料夾具有以下元件：

* 實體：資產的子系是其轉譯。
* 屬性.
* 連結.

[!DNL Assets] HTTP API包含下列功能：

* [檢索資料夾清單](#retrieve-a-folder-listing)。
* [建立資料夾](#create-a-folder)。
* [建立資產](#create-an-asset)。
* [更新資產二進位檔](#update-asset-binary)。
* [更新資產中繼資料](#update-asset-metadata)。
* [建立資產轉譯](#create-an-asset-rendition)。
* [更新資產轉譯](#update-an-asset-rendition)。
* [建立資產註解](#create-an-asset-comment)。
* [複製資料夾或資產](#copy-a-folder-or-asset)。
* [移動資料夾或資產](#move-a-folder-or-asset)。
* [刪除資料夾、資產或轉譯](#delete-a-folder-asset-or-rendition)。

>[!NOTE]
>
>為方便閱讀，下列範例會省略完整的cURL符號。 事實上，該符號確實與[Resty](https://github.com/micha/resty)相關，後者是`cURL`的指令碼包裝函式。

**必備條件**

* 存取 `https://[aem_server]:[port]/system/console/configMgr`.
* 導覽至&#x200B;**[!UICONTROL Adobe花崗岩CSRF濾鏡]**。
* 請確定屬性&#x200B;**[!UICONTROL 篩選方法]**&#x200B;包含：`POST`、`PUT`、`DELETE`。

## 檢索列出{#retrieve-a-folder-listing}的資料夾

檢索現有資料夾及其子實體（子資料夾或資產）的Siren表示法。

**要求**:  `GET /api/assets/myFolder.json`

**回應碼**:響應代碼為：

* 200 —— 好——成功。
* 404 —— 找不到——資料夾不存在或無法訪問。
* 500 —— 內部伺服器錯誤——如果有其它問題。

**回應**:傳回的實體類別為資產或資料夾。包含實體的屬性是每個實體的完整屬性集的子集。 為了獲得實體的完整表示法，客戶端應檢索連結指向的URL內容，該連結具有`self`的`rel`。

## 建立資料夾{#create-a-folder}

建立新`sling`:`OrderedFolder`。 如果提供`*`而非節點名稱，則servlet將使用參數名稱作為節點名稱。 接受為請求資料是新資料夾的Siren表示法或一組名稱——值配對，編碼為`application/www-form-urlencoded`或`multipart`/ `form`- `data`，對於直接從HTML表單建立資料夾非常有用。 此外，資料夾的屬性可指定為URL查詢參數。

如果所提供路徑的父節點不存在，則API呼叫會以`500`回應代碼失敗。 如果資料夾已存在，則調用返迴響應代碼`409`。

**參數**: `name` 是資料夾名稱。

**要求**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**回應碼**:響應代碼為：

* 201 —— 建立——成功建立。
* 409 —— 衝突——如果資料夾已存在。
* 412 - PRECONDITATION FAILED —— 如果找不到或存取根系列。
* 500 —— 內部伺服器錯誤——如果有其它問題。

## 建立資產{#create-an-asset}

將提供的檔案置於提供的路徑，以在DAM儲存庫中建立資產。 如果提供`*`而非節點名稱，則servlet將使用參數名或檔案名作為節點名。

**參數**:參數是 `name` 用於資產名 `file` 稱和檔案參考。

**要求**

* `POST /api/assets/myFolder/myAsset.png -H"Content-Type: image/png" --data-binary "@myPicture.png"`
* `POST /api/assets/myFolder/* -F"name=myAsset.png" -F"file=@myPicture.png"`

**回應碼**:響應代碼為：

* 201 —— 已建立——如果資產已成功建立。
* 409 —— 衝突——如果資產已存在。
* 412 - PRECONDITATION FAILED —— 如果找不到或存取根系列。
* 500 —— 內部伺服器錯誤——如果有其它問題。

## 更新資產二進位檔{#update-asset-binary}

更新資產的二進位格式（原始名稱的轉譯）。 更新會觸發預設資產處理工作流程，如果已設定，則會執行。

**要求**:  `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: image/png" --data-binary @myPicture.png`

**回應碼**:響應代碼為：

* 200 —— 確定——如果資產已成功更新。
* 404 —— 找不到——如果在提供的URI中找不到或訪問資產，請執行此操作。
* 412 - PRECONDITATION FAILED —— 如果找不到或存取根系列。
* 500 —— 內部伺服器錯誤——如果有其它問題。

## 更新資產中繼資料{#update-asset-metadata}

更新資產中繼資料屬性。 如果您更新`dc:`命名空間中的任何屬性，API會更新`jcr`命名空間中的相同屬性。 API不會同步兩個名稱空間下的屬性。

**要求**:  `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"jcr:title":"My Asset"}}'`

**回應碼**:響應代碼為：

* 200 —— 確定——如果資產已成功更新。
* 404 —— 找不到——如果在提供的URI中找不到或訪問資產，請執行此操作。
* 412 - PRECONDITATION FAILED —— 如果找不到或存取根系列。
* 500 —— 內部伺服器錯誤——如果有其它問題。

### 在`dc`和`jcr`命名空間{#sync-metadata-between-namespaces}之間同步中繼資料更新

API方法會更新`jcr`命名空間中的中繼資料屬性。 使用使用者介面進行的更新會變更`dc`命名空間中的中繼資料屬性。 若要同步`dc`和`jcr`命名空間之間的中繼資料值，您可以建立工作流程，並設定Experience Manager，在資產編輯時執行工作流程。 使用ECMA指令碼來同步所需的中繼資料屬性。 以下示例指令碼將同步`dc:title`和`jcr:title`之間的標題字串。

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

## 建立資產轉譯{#create-an-asset-rendition}

為資產建立新的資產轉譯。 如果未提供請求參數名稱，則會使用檔案名稱做為轉譯名稱。

**參數**:這些參數 `name` 是格式副本的名稱， `file` 並作為檔案參考。

**要求**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**回應碼**:響應代碼為：

* 201 —— 已建立——如果已成功建立轉譯。
* 404 —— 找不到——如果在提供的URI中找不到或訪問資產，請執行此操作。
* 412 - PRECONDITATION FAILED —— 如果找不到或存取根系列。
* 500 —— 內部伺服器錯誤——如果有其它問題。

## 更新資產轉譯{#update-an-asset-rendition}

更新會分別以新的二進位資料取代資產轉譯。

**要求**:  `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**回應碼**:響應代碼為：

* 200 —— 確定——如果已成功更新轉譯。
* 404 —— 找不到——如果在提供的URI中找不到或訪問資產，請執行此操作。
* 412 - PRECONDITATION FAILED —— 如果找不到或存取根系列。
* 500 —— 內部伺服器錯誤——如果有其它問題。

## 在資產{#create-an-asset-comment}上新增註解

建立新資產註解。

**參數**:參數是 `message` 用於注釋的消息主體和 `annotationData` JSON格式的注釋資料。

**要求**:  `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**回應碼**:響應代碼為：

* 201 —— 已建立——如果已成功建立注釋。
* 404 —— 找不到——如果在提供的URI中找不到或訪問資產，請執行此操作。
* 412 - PRECONDITATION FAILED —— 如果找不到或存取根系列。
* 500 —— 內部伺服器錯誤——如果有其它問題。

## 複製資料夾或資產{#copy-a-folder-or-asset}

複製位於提供路徑中的可用資料夾或資產，以連至新目標。

**請求標題**:參數包括：

* `X-Destination` - API解決方案範圍內的新目標URI，用於將資源複製到。
* `X-Depth` - `infinity` 或 `0`。使用`0`僅複製資源及其屬性，而不複製其子項。
* `X-Overwrite` -用 `F` 於防止覆寫現有目標的資產。

**要求**:  `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**回應碼**:響應代碼為：

* 201 —— 已建立——如果資料夾／資產已複製到非現有目標。
* 204 —— 無內容——如果資料夾／資產已複製至現有目的地。
* 412 —— 前提條件失敗——如果缺少請求標題。
* 500 —— 內部伺服器錯誤——如果有其它問題。

## 移動資料夾或資產{#move-a-folder-or-asset}

將指定路徑上的資料夾或資產移動到新目標。

**請求標題**:參數包括：

* `X-Destination` - API解決方案範圍內的新目標URI，用於將資源複製到。
* `X-Depth` - `infinity` 或 `0`。使用`0`僅複製資源及其屬性，而不複製其子項。
* `X-Overwrite` -使用強 `T` 制刪除現有資源或 `F` 防止覆寫現有資源。

**要求**:  `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

請勿在URL中使用`/content/dam`。 移動資產和覆寫現有資產的範例命令如下：

```shell
curl -u admin:admin -X MOVE https://[aem_server]:[port]/api/assets/source/file.png -H "X-Destination: http://[aem_server]:[port]/api/assets/destination/file.png" -H "X-Overwrite: T"
```

**回應碼**:響應代碼為：

* 201 —— 已建立——如果資料夾／資產已複製到非現有目標。
* 204 —— 無內容——如果資料夾／資產已複製至現有目的地。
* 412 —— 前提條件失敗——如果缺少請求標題。
* 500 —— 內部伺服器錯誤——如果有其它問題。

## 刪除資料夾、資產或轉譯{#delete-a-folder-asset-or-rendition}

刪除提供路徑上的資源(-tree)。

**要求**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**回應碼**:響應代碼為：

* 200 —— 確定——如果資料夾已成功刪除。
* 412 - PRECONDITATION FAILED —— 如果找不到或存取根系列。
* 500 —— 內部伺服器錯誤——如果有其它問題。

## 提示和限制{#tips-best-practices-limitations}

* [HTTP API會更新命名空](#update-asset-metadata) 間中的中繼資料 `jcr` 屬性。不過，Experience Manager用戶介面會更新`dc`命名空間中的元資料屬性。

* 資產HTTP API不會傳回完整的中繼資料。 命名空間會以硬式編碼，且只會傳回這些名稱空間。 如需完整的中繼資料，請參閱資產路徑`/jcr_content/metadata.json`。
