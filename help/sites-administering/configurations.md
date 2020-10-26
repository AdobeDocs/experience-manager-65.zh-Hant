---
title: 配置和配置瀏覽器
description: 瞭解AEM設定，以及它們在AEM中管理工作區設定的方式。
translation-type: tm+mt
source-git-commit: 8f5159d92f64b218d9e2e72d119e6de9d3e01ce6
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 1%

---


# 配置和配置瀏覽器 {#configuration-browser}

AEM設定可用來管理AEM中的設定，並可當成工作區。

## 什麼是配置？ {#what-is-a-configuration}

從兩個不同的觀點可以考慮配置。

* [管理員](#configurations-administrator) (Administrator)會將設定當做AEM中的工作區來定義和管理設定群組。
* [開發人員](#configurations-developer) (Developer)會使用建置AEM中可持續保留和尋找設定的基礎設定機制。

總之：從管理員的觀點來看，設定是您建立工作區以管理AEM中設定的方式，而開發人員應瞭解AEM在儲存庫中使用和管理這些設定的方式。

無論從您的角度如何，AEM中的設定都有兩個主要用途：

* 設定可為特定使用者群組啟用特定功能。
* 配置定義這些功能的訪問權限。

## 以管理員身份進行的配置 {#configurations-administrator}

AEM管理員和作者可將組態視為工作區。 這些工作區可用來針對這些功能實作存取權限，以收集設定群組及其相關內容，以供組織使用。

您可針對AEM中的許多不同功能建立設定。

* [雲端設定](/help/sites-administering/configurations.md)
* [內容中樞區段](/help/sites-administering/segmentation.md)
* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
* [可編輯的範本](/help/sites-authoring/templates.md)

### 範例 {#administrator-example}

例如，管理員可以為可編輯模板建立兩種配置。

* WKND-General
* WKND-Magazine

然後，管理員可以使用WKND-General配置來建立一般頁面範本，然後在WKND-Magazine下建立雜誌專屬的範本。

然後，管理員可以將WKND-General與WKND網站的所有內容建立關聯。 不過，WKND-Magazine組態將只與雜誌網站相關聯。

執行下列動作：

* 當內容作者為雜誌建立新頁面時，作者可從一般範本(WKND-General)或雜誌範本(WKND-Magazine)中選擇。
* 當內容作者為非雜誌的網站其他部分建立新頁面時，作者只能從一般範本(WKND-General)中選擇。

不僅可編輯範本的設定可能類似，雲端設定、ContextHub區段和內容片段模型也可能有類似的設定。

### 使用配置瀏覽器 {#using-configuration-browser}

「設定瀏覽器」可讓管理員輕鬆建立、管理和設定AEM中設定的存取權限。

>[!NOTE]
>
>只有在您的用戶具有權限時，才能使用配置瀏覽器建立 `admin` 配置。 `admin` 此外，還需要權限才能將訪問權限分配給配置或以其他方式修改配置。

#### 建立配置 {#creating-a-configuration}

在AEM中使用「設定瀏覽器」建立新設定非常簡單。

1. 以雲端服務的身分登入AEM，並從主功能表選取「工 **具** ->一般 **->** 設定瀏覽器 ****」。
1. 點選或按一下「 **建立**」。
1. 為您的 **設定** ，提供 **標題** 和名稱。

   ![建立設定](assets/configuration-create.png)

   * 標 **題** (Title)應為描述性。
   * Name **** （名稱）將成為儲存庫中的節點名稱。
      * 它會根據標題自動產生，並根據 [AEM命名慣例進行調整。](/help/sites-developing/naming-conventions.md)
      * 如有需要，可加以調整。
1. 檢查您希望允許的配置類型。
   * [雲端設定](/help/sites-administering/configurations.md)
   * [內容中樞區段](/help/sites-administering/segmentation.md)
   * [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
   * [可編輯的範本](/help/sites-authoring/templates.md)
1. 點選或按一下「 **建立**」。

>[!TIP]
>
>配置可以嵌套。

#### 編輯配置及其訪問權限 {#access-rights}

如果您將配置視為工作區，則可以對這些配置設定訪問權限，以便強制哪些人可以訪問這些工作區，哪些人可能不訪問這些工作區。

1. 以雲端服務的身分登入AEM，並從主功能表選取「工 **具** ->一般 **->** 設定瀏覽器 ****」。
1. 選擇要修改的配置，然後點選或按一下工具 **欄中** 「屬性」(Properties)。
1. 選擇要添加到配置中的任何其他功能
   >[!NOTE]
   >
   >建立配置後，無法取消選取特徵。
1. 使用「 **有效權限** 」按鈕可查看角色的矩陣以及當前授予配置的權限。
   ![有效權限窗口](assets/configuration-effective-permissions.png)
1. 若要指派新權限，請在「新增權限」區段的「選 **取使用者或群組** 」欄位中 **輸入使用者或群組名稱** 。
   * 「選 **取使用者或群組** 」欄位會根據現有使用者和角色提供自動完成功能。
1. 從自動完成結果中選擇適當的用戶或角色。
   * 您可以選取多個使用者或角色。
1. 檢查所選用戶或角色應具有的訪問選項，然後按一下「添 **加」**。
   ![將訪問權限添加到配置](assets/configuration-edit.png)
1. 重複這些步驟以選擇用戶或角色，並根據需要指派其他訪問權限。
1. 完成時點選或 **按一下「儲存並關閉** 」。

## 以開發人員身分進行的組態 {#configurations-developer}

身為開發人員，請務必瞭解AEM雲端服務如何處理組態，以及它如何處理組態解析。

### 分離配置和內容 {#separation-of-config-and-content}

雖然管 [理員和使用者可能會將組態視為工作場所](#configurations-administrator) ，以管理不同的設定和內容，但請務必瞭解，組態和內容是由AEM在儲存庫中個別儲存和管理。

* `/content` 是所有內容的所在位置。
* `/conf` 是所有配置的首頁。

內容會透過屬性參考其相關 `cq:conf` 組態。 AEM會根據內容執行查閱，其內容屬性會 `cq:conf` 用來尋找適當的設定。

### 範例 {#developer-example}

在此範例中，假設您有一些對DAM設定感興趣的應用程式碼。

```java
Conf conf = resource.adaptTo(Conf.class);
ValueMap imageServerSettings = conf.getItem("dam/imageserver");
String bgkcolor = imageServerSettings.get("bgkcolor", "FFFFFF");
```

所有組態查閱的起點都是內容資源，通常在下方某處 `/content`。 這可以是頁面、頁面內的元件、資產或DAM資料夾。 這是我們要尋找的實際內容，以找出適用於此內容的正確設定。

現在，有了 `Conf` 這個物件，我們就可以擷取我們感興趣的特定設定項目。 在本例中，它 `dam/imageserver`是與相關的一組設定 `imageserver`。 呼 `getItem` 叫傳回 `ValueMap`。 接著，我們會 `bgkcolor` 讀取字串屬性，並在屬性（或整個設定項目）不存在時，提供預設值&quot;FFFFFF&quot;。

現在，讓我們來看一下對應的JCR內容：

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

在此示例中，我們假設此處有一個WKND特定的DAM資料夾和相應的配置。 從該資料夾開 `/content/dam/wknd`始，我們將看到一個名為的字串屬性，該屬 `cq:conf` 性引用應應用於子樹的配置。 屬性通常會設定在資產資 `jcr:content` 料夾或頁面上。 這 `conf` 些連結是明確的，因此只要查看CRXDE中的內容，就可輕鬆追蹤。

跳進去 `/conf`，我們按照參考，看到有一個節 `/conf/wknd` 點。 這是一個配置。 請注意，其查閱對應用程式碼完全透明。 范常式式碼從未有專用的參考，它隱藏在物件之 `Conf` 後。 所套用的組態完全由JCR內容控制。

我們看到此配置包含一個固定命 `settings` 名的節點，其中包含實際項目，包 `dam/imageserver` 括我們的情況。 此類項目可視為「設定檔案」，通常由包含實際內容 `cq:Page` 的 `jcr:content` 項目表示。

最後，我們看到范常式 `bgkcolor` 式碼所需的屬性。 我 `ValueMap` 們從頁面 `getItem` 的節點返回時，會根據頁面的節 `jcr:content` 點。

### 配置解析度 {#configuration-resolution}

上述基本範例顯示單一組態。 但是，在很多情況下，您想要擁有不同的配置，例如預設全局配置、每個品牌的不同配置，以及子項目的特定配置。

若要支援此功能，AEM中的設定查閱會依下列偏好設定順序提供繼承和備援機制：

1. `/conf/<siteconfig>/<parentconfig>/<myconfig>`
   * 特定組態是從 `cq:conf` `/content`
   * 階層是任意的，而且可像您的網站結構一樣進行設計，瞭解這一點並非應用程式碼的事
   * 具有配置權限的用戶在運行時可進行更改
1. `/conf/<siteconfig>/<parentconfig>`
   * 遍歷備用配置的父代
   * 具有配置權限的用戶在運行時可進行更改
1. `/conf/<siteconfig>`
   * 遍歷備用配置的父代
   * 具有配置權限的用戶在運行時可進行更改
1. `/conf/global`
   * 系統全局設定
   * 通常是安裝的全域預設值
   * 由角色設 `admin` 定
   * 具有配置權限的用戶在運行時可進行更改
1. `/apps`
   * 應用程式預設值
   * 已修正應用程式部署
   * 執行時期唯讀
1. `/libs`
   * AEM產品預設值
   * 只有Adobe可變，專案存取權才不允許
   * 已修正應用程式部署
   * 執行時期唯讀

### 使用配置 {#using-configurations}

AEM中的設定是以Sling Context-Aware Configurations為基礎。 Sling bundles提供服務API，可用來取得內容感應設定。 上下文感知配置是與內容資源或資源樹相關的配置，如上 [例中所述。](#developer-example)

如需Context-Aware Configurations的詳細資訊、範例及如何使用，請參 [閱Sling檔案。](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html)

### ConfMgr Web控制台 {#confmgr-web-console}

為了進行調試和測試，在上有 **ConfMgr** web控制台 `https://<host>:<port>/system/console/conf`，它可顯示給定路徑／項的配置。

![ConfMgr](assets/configuration-confmgr.png)

只要提供：

* **內容路徑**
* **項目**
* **使用者**

按一下 **解析** ，查看已解析的配置，並接收將解析這些配置的示例代碼。

### 上下文感知配置Web控制台 {#context-aware-web-console}

為了進行調試和測試，在上有 **Context-Aware Configuration** web控制台 `https://<host>:<port>/system/console/slingcaconfig`，它允許查詢儲存庫中的上下文感知配置並查看其屬性。

![上下文感知配置Web控制台](assets/configuration-context-aware-console.png)

只要提供：

* **內容路徑**
* **配置名稱**

按一下 **解析** ，檢索所選配置的相關上下文路徑和屬性。
