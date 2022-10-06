---
title: 配置和配置瀏覽器
description: 了解AEM設定，以及如何在AEM中管理工作區設定。
exl-id: 1be5849b-748c-48e8-afa8-35a9026c27b3
source-git-commit: 84b16dd1a60f731b568dd87ef89699875cb86596
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 1%

---

# 配置和配置瀏覽器 {#configuration-browser}

AEM設定可用於管理AEM中的設定，並作為工作區。

## 什麼是配置？ {#what-is-a-configuration}

可從兩個不同的觀點來考慮配置。

* [管理員](#configurations-administrator) 在AEM內將設定作為工作區來定義和管理設定群組。
* [開發人員](#configurations-developer) 使用實作設定的基礎設定機制，以在AEM中保存和查詢設定。

總之：從管理員的角度來看，設定是您建立工作區以在AEM中管理設定的方式，而開發人員應了解AEM如何在存放庫中使用和管理這些設定。

無論從您的角度來看，設定在AEM中有兩個主要用途：

* 設定可為特定使用者群組啟用特定功能。
* 設定會定義這些功能的存取權限。

## 管理員配置 {#configurations-administrator}

AEM管理員及作者可將設定視為工作區。 這些工作區可用於透過對這些功能實作存取權限，以收集設定群組以及其相關內容，以利於組織用途。

可在AEM中針對許多不同功能建立設定。

* [雲端設定](/help/sites-administering/configurations.md)
* [內容中心區段](/help/sites-administering/segmentation.md)
* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
* [可編輯的範本](/help/sites-authoring/templates.md)

### 範例 {#administrator-example}

例如，管理員可為可編輯的範本建立兩個設定。

* WKND-General
* WKND-Magazine

然後，管理員可使用WKND-General配置建立常規頁面模板，然後使用WKND-Magazine下的雜誌專用模板。

然後，管理員可將WKND-General與WKND網站的所有內容相關聯。 但WKND-Magazine配置只與雜誌網站相關聯。

執行此動作：

* 當內容作者為雜誌建立新頁面時，作者可從一般範本(WKND-General)或雜誌範本(WKND-Magazine)中選擇。
* 當內容作者為網站的其他部分（而非雜誌）建立新頁面時，作者只能從一般範本(WKND-General)中選擇。

不僅可編輯的範本，雲端設定、ContextHub區段和內容片段模型也可進行類似的設定。

### 使用設定瀏覽器 {#using-configuration-browser}

組態瀏覽器可讓管理員輕鬆建立、管理和設定AEM中組態的存取權限。

>[!NOTE]
>
>只有在使用者已 `admin` 權限。 `admin` 為了指派存取權給設定或以其他方式修改設定，也需要權限。

#### 建立設定 {#creating-a-configuration}

使用「設定瀏覽器」在AEM中建立新設定非常簡單。

1. 登入AEMas a Cloud Service，然後從主功能表選取 **工具** -> **一般** -> **配置瀏覽器**.
1. 點選或按一下 **建立**.
1. 提供 **標題** 和 **名稱** 的URL。

   ![建立設定](assets/configuration-create.png)

   * 此 **標題** 應是描述性的。
   * 此 **名稱** 會成為存放庫中的節點名稱。
      * 根據標題自動產生並根據 [AEM命名慣例。](/help/sites-developing/naming-conventions.md)
      * 如有需要，可加以調整。
1. 檢查您要允許的配置類型。
   * [雲端設定](/help/sites-administering/configurations.md)
   * [內容中心區段](/help/sites-administering/segmentation.md)
   * [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
   * [可編輯的範本](/help/sites-authoring/templates.md)
1. 點選或按一下 **建立**.

>[!TIP]
>
>配置可以嵌套。

#### 編輯配置及其訪問權限 {#access-rights}

如果您將設定視為工作區，則可在這些設定上設定存取權限，以強制哪些人可以和哪些人不可以存取這些工作區。

1. 登入AEMas a Cloud Service，然後從主功能表選取 **工具** -> **一般** -> **配置瀏覽器**.
1. 選取您要修改的設定，然後點選或按一下 **屬性** 的下限。
1. 選擇要添加到配置的任何其他功能
   >[!NOTE]
   >
   >建立配置後，無法取消選取特徵。
1. 使用 **有效權限** 按鈕，查看角色矩陣以及它們當前授予配置的權限。
   ![有效權限窗口](assets/configuration-effective-permissions.png)
1. 若要指派新權限，請在 **選擇用戶或組** 欄位 **新增權限** 區段。
   * 此  **選擇用戶或組** 欄位根據現有使用者和角色自動完成。
1. 從自動完成結果中選擇適當的用戶或角色。
   * 您可以選取多個使用者或角色。
1. 檢查所選用戶或角色應具有的訪問選項，然後按一下 **新增**.
   ![將存取權限新增至設定](assets/configuration-edit.png)
1. 重複這些步驟以選取使用者或角色，並視需要指派其他存取權限。
1. 點選或按一下 **儲存並關閉** 完成時。

## 以開發人員身分進行設定 {#configurations-developer}

身為開發人員，請務必了解AEM as a Cloud Service如何搭配設定運作，以及其處理設定解析的方式。

### 分離配置和內容 {#separation-of-config-and-content}

雖然 [管理員和使用者可將設定視為工作場所](#configurations-administrator) 若要管理不同的設定和內容，請務必了解，設定和內容是由AEM在存放庫中個別儲存和管理。

* `/content` 是所有內容的首頁。
* `/conf` 是所有設定的首頁。

內容透過 `cq:conf` 屬性。 AEM會根據內容及其內容執行查詢 `cq:conf` 屬性以尋找適當的設定。

### 範例 {#developer-example}

在此範例中，假設您有一些對DAM設定感興趣的應用程式程式碼。

```java
Conf conf = resource.adaptTo(Conf.class);
ValueMap imageServerSettings = conf.getItem("dam/imageserver");
String bgkcolor = imageServerSettings.get("bgkcolor", "FFFFFF");
```

所有設定查閱的起始點都是內容資源，通常位於 `/content`. 這可以是頁面、頁面內的元件、資產或DAM資料夾。 這是我們要尋找的實際內容，以尋找適用於此情境的正確設定。

現在，透過 `Conf` 對象，我們可以檢索我們感興趣的特定配置項。 在這個例子裡 `dam/imageserver`，此元件為與 `imageserver`. 此 `getItem` 呼叫傳回 `ValueMap`. 我們讀 `bgkcolor` 字串屬性，並提供「FFFFFF」的預設值，以備屬性（或整個設定項目）不存在時使用。

現在，讓我們查看對應的JCR內容：

```text
/content/dam/wknd
    + jcr:content
      - cq:conf = "/conf/wknd"
    + image.png [dam:Asset]

/conf/wkns
    + settings
      + dam
        + imageserver [cq:Page]
          + jcr:content
            - bgkcolor = "FF0000"
```

在此範例中，我們假設有WKND專屬的DAM資料夾和對應的設定。 從該資料夾開始 `/content/dam/wknd`，我們會看到一個名為 `cq:conf` 會參考應套用至子樹狀結構的設定。 屬性通常會設定在 `jcr:content` 或頁面。 這些 `conf` 連結是明確的，因此只要查看CRXDE中的內容，就可輕鬆追蹤連結。

跳進 `/conf`，我們會參照參考資料，看到 `/conf/wknd` 節點。 這是設定。 請注意，其查閱對應用程式程式碼完全透明。 范常式式碼從未有專屬的參照，會隱藏在 `Conf` 物件。 系統會透過JCR內容完全控制套用的設定。

我們看到設定包含 `settings` 包含實際項的節點，包括 `dam/imageserver` 我們需要這個。 此類項目可視為「設定檔案」，通常由 `cq:Page` 包括 `jcr:content` 保存實際內容。

最後，我們看到了 `bgkcolor` 程式碼範例所需的。 此 `ValueMap` 我們從 `getItem` 是根據頁面的 `jcr:content` 節點。

### 配置解析度 {#configuration-resolution}

上述基本範例顯示單一設定。 但在許多情況下，您會想要有不同的設定，例如預設全域設定、每個品牌的不同設定，以及子專案的特定設定。

若要支援此功能，AEM中的設定查閱會依下列偏好順序提供繼承和備援機制：

1. `/conf/<siteconfig>/<parentconfig>/<myconfig>`
   * 引用的特定配置 `cq:conf` 某處 `/content`
   * 階層是任意的，而且可像您的網站結構一樣設計，因此了解這一點並非應用程式程式碼的事務
   * 具有配置權限的用戶在運行時可更改
1. `/conf/<siteconfig>/<parentconfig>`
   * 遍歷備援配置的父級
   * 具有配置權限的用戶在運行時可更改
1. `/conf/<siteconfig>`
   * 遍歷備援配置的父級
   * 具有配置權限的用戶在運行時可更改
1. `/conf/global`
   * 系統全局設定
   * 通常是安裝的全局預設值
   * 由 `admin` 角色
   * 具有配置權限的用戶在運行時可更改
1. `/apps`
   * 應用程式預設值
   * 透過應用程式部署修正
   * 運行時只讀
1. `/libs`
   * AEM產品預設值
   * 僅可按Adobe更改，不允許項目訪問
   * 透過應用程式部署修正
   * 運行時只讀

### 使用配置 {#using-configurations}

AEM中的設定是以Sling內容感知設定為基礎。 Sling套件組合提供服務API，可用來取得內容感知設定。 內容感知配置是與內容資源或資源樹相關的配置，如前 [上一個範例中所述。](#developer-example)

如需內容感知設定的詳細資訊、範例及使用方式， [請參閱Sling檔案。](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html)

### ConfMgr Web控制台 {#confmgr-web-console}

為進行偵錯和測試， **ConfMgr** 網站主控台 `https://<host>:<port>/system/console/conf`，可顯示指定路徑/項目的設定。

![ConfMgr](assets/configuration-confmgr.png)

只需提供：

* **內容路徑**
* **項目**
* **使用者**

按一下 **解決** 查看已解析哪些配置，並接收將解析這些配置的示例代碼。

### 內容感知配置Web控制台 {#context-aware-web-console}

為進行偵錯和測試， **內容感知配置** 網站主控台 `https://<host>:<port>/system/console/slingcaconfig`，可在存放庫中查詢內容感知設定並檢視其屬性。

![內容感知配置Web控制台](assets/configuration-context-aware-console.png)

只需提供：

* **內容路徑**
* **設定名稱**

按一下 **解決** 以檢索選定配置的關聯上下文路徑和屬性。
