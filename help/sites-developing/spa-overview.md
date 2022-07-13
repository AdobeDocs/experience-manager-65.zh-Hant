---
title: 編SPA輯器概述
seo-title: SPA Editor Overview
description: 本文全面概述了編輯SPA器及其工作方式，包括了編輯器在內交互的SPA詳細工AEM作流。
seo-description: This article gives a comprehensive overview of the SPA Editor and how it works included detailed workflows of interaction of the SPA Editor within AEM.
uuid: c283abab-f5bc-414a-bc81-bf3bdce38534
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 06b8c0be-4362-4bd1-ad57-ea5503616b17
docset: aem65
exl-id: 7b34be66-bb61-4697-8cc8-428f7c63a887
source-git-commit: a547b2e24205c63284a0e77f2e7f5678ae24968b
workflow-type: tm+mt
source-wordcount: '1657'
ht-degree: 1%

---

# 編SPA輯器概述{#spa-editor-overview}

單頁應用程式 (SPA) 可為網站使用者提供引人入勝的體驗。開發人員希望能夠使用框架構建站SPA點，而作者希望無縫地編輯使用這AEM種框架構建的站點的內容。

編輯SPA器提供了一個全面的解決方案，用於SPA支援內AEM部。 本頁概述了支SPA持的結構AEM、編SPA輯器的工作SPA方式以及框架和AEM保持同步。

>[!NOTE]
>
>編輯SPA器是需要基於框架的SPA客戶端呈現(例如，反應或Angular)的項目的推薦解決方案。

## 簡介 {#introduction}

使用常SPA用框架(如React和Angular)構建的站點通過動態JSON載入其內容，並且不提供頁面編輯器能夠放置編輯控AEM件所必需的HTML結構。

要啟用在中的編SPA輯AEM，需要在儲存庫中的JSON輸SPA出和內容模型之AEM間進行映射以保存對內容的更改。

SPA中的AEM支援引入了一個精簡JS層，當載入到頁面編輯器中時，該層與SPAJS代碼交互，可通過該層發送事件，並激活編輯控制項的位置以允許上下文編輯。 此功能基於Content Services API端點概念，因為來自內容的內SPA容需要通過Content Services載入。

有關中的更SPA多詳AEM細資訊，請參閱以下文檔：

* [藍SPA圖](/help/sites-developing/spa-blueprint.md) 的技術要SPA求
* [入SPA門AEM](/help/sites-developing/spa-getting-started-react.md) 快速瀏覽一SPA下

## Design {#design}

某的頁元件SPA不會通過JSP或HTL檔案提供其子元件的HTML元素。 此操作已委託到該SPA框架。 子元件或模型的表示從JCR中作為JSON資料結構提取。 然SPA後根據該結構將元件添加到頁面。 此行為將頁面元件的初始主體組合與非對SPA應項區分。

### 頁面模型管理 {#page-model-management}

頁面模型之解決方案及管理已委託 `PageModel` 的下界。 必須SPA使用頁面模型庫才能初始化並由編輯器SPA創作。 「頁面模型」庫通過以下方式間AEM接提供給「頁面」元件： `aem-react-editable-components` npm。 頁面模型是和之間的解AEM釋器，因SPA此必須始終存在。 創作頁面時，附加庫 `cq.authoring.pagemodel.messaging` 必須添加才能啟用與頁面編輯器的通信。

如果頁SPA面元件繼承自頁面核心元件，則有兩個選項 `cq.authoring.pagemodel.messaging` 客戶端庫類別可用：

* 如果模板是可編輯的，請將其添加到頁面策略中。
* 或使用 `customfooterlibs.html`。

對於導出模型中的每個資源，SPA將映射一個將執行渲染的實際元件。 然後，使用容器內的元件映射來呈現表示為JSON的模型。
![screen_shot_2018-08-20at144152](assets/screen_shot_2018-08-20at144152.png)

>[!CAUTION]
>
>包含 `cq.authoring.pagemodel.messaging` 類別應限於編輯器的上SPA下文。

### 通信資料類型 {#communication-data-type}

當 `cq.authoring.pagemodel.messaging` 類別被添加到頁面中，它將向頁面編輯器發送消息以建立JSON通信資料類型。 當通信資料類型設定為JSON時，GET請求將與元件的Sling Model端點通信。 在頁面編輯器中發生更新後，更新元件的JSON表示形式將發送到頁面模型庫。 然後，頁面模型庫通知SPA更新。

![screen_shot_2018-08-20at143628](assets/screen_shot_2018-08-20at143628.png)

## 工作流程 {#workflow}

您可以通過將編輯作為SPA兩者之AEM間的調SPA解者來理解和之間的交互。

* 頁面編輯器與之之間的SPA通信是使用JSON而不是HTML。
* 頁面編輯器通過iframe和消息傳遞API向SPA提供頁面模型的最新版本。
* 頁面模型管理器通知編輯器已準備好編輯，並將頁面模型作為JSON結構傳遞。
* 編輯器不會改變或甚至訪問正在創作的頁面的DOM結構，而是提供最新的頁面模型。

![screen_shot_2018-08-20at144324](assets/screen_shot_2018-08-20at144324.png)

### 基本編SPA輯器工作流 {#basic-spa-editor-workflow}

在編輯器的關鍵要素SPA中，在中編輯的高級工作SPA流AEM將如下所示。

![無標題1](assets/untitled1.gif)

1. 編SPA輯器載入。
1. 裝SPA載在單獨的框架中。
1. 請SPA求JSON內容並呈現元件客戶端。
1. 編SPA輯器檢測渲染元件並生成疊加。
1. 作者按一下「覆蓋」，顯示元件的編輯工具欄。
1. 編SPA輯器繼續編輯，並向伺服器發出POST請求。
1. 編SPA輯器向編輯器請SPA求更新的JSON，該編輯器將用DOM事SPA件發送到。
1. 重SPA新呈現相關元件，更新其DOM。

>[!NOTE]
>
>記住：
>
>* 總是SPA由顯示器負責。
>* 編SPA輯器與本SPA身隔離。
>* 在生產（發佈）中，從SPA不載入編輯器。
>


### 客戶端 — 伺服器頁編輯工作流 {#client-server-page-editing-workflow}

這是編輯時客戶端與伺服器交互的更詳細概SPA述。

![page_editor_spa_authoringmediator-2](assets/page_editor_spa_authoringmediator-2.png)

1. 初始SPA化自身，並從Sling模型導出器請求頁面模型。
1. Sling模型導出器請求從儲存庫合成頁面的資源。
1. 儲存庫返回資源。
1. Sling模型導出器返回頁面的模型。
1. 根SPA據頁面模型實例化其元件。
1. **6a** 內容通知編輯器它已準備好進行創作。

   **6b** 頁面編輯器請求元件創作配置。

   **6c** 頁面編輯器接收元件配置。
1. 當作者編輯元件時，頁面編輯器將修改請求發佈到預設POSTservlet。
1. 資源在儲存庫中更新。
1. 將更新的資源提供給POSTservlet。
1. 預設POSTservlet通知頁面編輯器資源已更新。
1. 頁面編輯器請求新頁面模型。
1. 從儲存庫請求構成頁面的資源。
1. 組成頁面的資源由儲存庫提供給Sling模型導出器。
1. 更新的頁面模型將返回給編輯器。
1. 頁面編輯器更新的頁面模型引SPA用。
1. 根SPA據新頁面模型引用更新其元件。
1. 更新頁面編輯器的元件配置。

   **17a** 該信SPA號指示頁面編輯器內容已就緒。

   **17b** 頁面編輯器為SPA提供元件配置。

   **17c** 提供SPA更新的元件配置。

### 創作工作流 {#authoring-workflow}

這是更詳細的概述，重點介紹創作體驗。

![spa_content_authoring模型](assets/spa_content_authoringmodel.png)

1. 讀取SPA頁面模型。
1. **2a** 頁面模型為編輯器提供創作所需的資料。

   **2b** 當收到通知後，component orchestrator將更新頁面的內容結構。
1. 元件orchestrator查詢資源類AEM型和元件之SPA間的映射。
1. 元件管理器基於頁面模SPA型和元件映射動態實例化元件。
1. 頁面編輯器更新頁面模型。
1. **6a** 頁面模型向頁面編輯器提供更新的創作資料。

   **6b** 頁面模型將更改派發給component orchestrator。
1. 元件orchestrator讀取元件映射。
1. 元件orchestrator更新頁面的內容。
1. 完成SPA頁面內容更新後，頁面編輯器將載入創作環境。

## 要求和限制 {#requirements-limitations}

要使作者能夠使用頁面編輯器編輯內容SPA，必SPA須實現應用程式以與編輯器AEMSDKSPA交互。 請參閱 [入SPA門AEM](/help/sites-developing/spa-getting-started-react.md) 你至少需要知道的檔案才能運行。

### 支援的框架 {#supported-frameworks}

Editor SPA SDK支援以下最低版本：

* 響應16.x和更高
* Angular6.x及更高

這些框架的早期版本可能與AEM編SPA輯器SDK配合使用，但不受支援。

### 附加框架 {#additional-frameworks}

可SPA以實施其他框架以與AEMEditorSPA SDK配合使用。 請參閱 [藍SPA圖](/help/sites-developing/spa-blueprint.md) 文檔，說明框架必須滿足的要求，以便建立由模組、元件和服務組成的框架特定層，以便與編AEM輯器SPA協作。

### 使用多個選擇器 {#multiple-selectors}

可以定義其他自定義選擇器，並將其用SPA作為為AEMSDK開發的一SPA部分。 但是，此支援要求 `model` 選擇器是第一個選擇器，副檔名是 `.json` 如 [JSON導出器所需。](json-exporter-components.md#multiple-selectors)

### 文本編輯器要求 {#text-editor-requirements}

如果要使用在中建立的文本元件的就地編輯器，SPA則需要其他配置。

1. 在包含文本HTML的容器包裝元素上設定屬性（可以是任意屬性）。 如果是WKND日誌樣本內容，則 `<div>` 元素和已使用的選擇器 `data-rte-editelement`。
1. 設定配置 `editElementQuery` 對應文AEM本元件的 `cq:InplaceEditingConfig` 指向該選擇器，例如 `data-rte-editelement`。 這樣編輯器就能知道HTML文本的HTML元素。

有關如何執行此操作的示例，請參見 [WKND日誌示例內容。](https://github.com/adobe/aem-sample-we-retail-journal/pull/16/files)

有關 `editElementQuery` 屬性和富格文本編輯器的配置，請參見 [配置RTF編輯器。](/help/sites-administering/rich-text-editor.md)

### 限制 {#limitations}

Editor AEM SDK隨AEM6.4 Service Pack 2而推出。 它得到Adobe的充分支援，並繼續得到加強和擴大。 編輯AEM器尚不支援以SPA下功能：

* 目標模式
* ContextHub
* 內聯影像編輯
* 編輯配置(例如 監聽器)
* 撤消/重做
* 頁面差異和時間偏差
* 執行HTML重寫伺服器端的功能，如連結檢查器、CDN重寫器服務、URL縮短等。
* 開發人員模式
* 啟AEM動
