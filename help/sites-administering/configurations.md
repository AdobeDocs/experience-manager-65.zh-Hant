---
title: 配置和配置瀏覽器
description: 瞭解AEM設定，以及它們在AEM中管理工作區設定的方式。
translation-type: tm+mt
source-git-commit: 8f5159d92f64b218d9e2e72d119e6de9d3e01ce6
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 1%

---


# 配置和配置瀏覽器{#configuration-browser}

AEM設定可用來管理AEM中的設定，並可當成工作區。

## 什麼是配置？{#what-is-a-configuration}

從兩個不同的觀點可以考慮配置。

* [管理](#configurations-administrator) 員會使用設定作為AEM中的工作區，以定義和管理設定群組。
* [開發](#configurations-developer) 人員會使用基本的組態機制，來建置在AEM中持續存在和尋找設定的組態。

總之：從管理員的觀點來看，設定是您建立工作區以管理AEM中設定的方式，而開發人員應瞭解AEM在儲存庫中使用和管理這些設定的方式。

無論從您的角度如何，AEM中的設定都有兩個主要用途：

* 設定可為特定使用者群組啟用特定功能。
* 配置定義這些功能的訪問權限。

## 以{#configurations-administrator}管理員身份進行的配置

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

### 使用配置瀏覽器{#using-configuration-browser}

「設定瀏覽器」可讓管理員輕鬆建立、管理和設定AEM中設定的存取權限。

>[!NOTE]
>
>只有當您的用戶具有`admin`權限時，才能使用配置瀏覽器建立配置。 `admin` 此外，還需要權限才能將訪問權限分配給配置或以其他方式修改配置。

#### 建立配置{#creating-a-configuration}

在AEM中使用「設定瀏覽器」建立新設定非常簡單。

1. 以雲端服務的身分登入AEM，並從主功能表選擇「工具」**「** -> **「一般」** -> 「設定瀏覽器」**。**
1. 點選或按一下「建立&#x200B;**」。**
1. 為您的配置提供&#x200B;**Title**&#x200B;和&#x200B;**Name**。

   ![建立設定](assets/configuration-create.png)

   * **Title**&#x200B;應為描述性。
   * **Name**&#x200B;將成為儲存庫中的節點名。
      * 系統會根據標題自動產生，並根據[AEM命名慣例進行調整。](/help/sites-developing/naming-conventions.md)
      * 如有需要，可加以調整。
1. 檢查您希望允許的配置類型。
   * [雲端設定](/help/sites-administering/configurations.md)
   * [內容中樞區段](/help/sites-administering/segmentation.md)
   * [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
   * [可編輯的範本](/help/sites-authoring/templates.md)
1. 點選或按一下「建立&#x200B;**」。**

>[!TIP]
>
>配置可以嵌套。

#### 編輯配置及其訪問權限{#access-rights}

如果您將配置視為工作區，則可以對這些配置設定訪問權限，以便強制哪些人可以訪問這些工作區，哪些人可能不訪問這些工作區。

1. 以雲端服務的身分登入AEM，並從主功能表選擇「工具」**「** -> **「一般」** -> 「設定瀏覽器」**。**
1. 選擇要修改的配置，然後點選或按一下工具欄中的&#x200B;**屬性**。
1. 選擇要添加到配置中的任何其他功能
   >[!NOTE]
   >
   >建立配置後，無法取消選取特徵。
1. 使用&#x200B;**有效權限**按鈕可查看角色矩陣以及它們當前授予配置的權限。
   ![有效權限窗口](assets/configuration-effective-permissions.png)
1. 要分配新權限，請在&#x200B;**添加新權限**&#x200B;部分的&#x200B;**選擇用戶或組**&#x200B;欄位中輸入用戶或組名。
   * **選擇用戶或組**&#x200B;欄位提供基於現有用戶和角色的自動完成。
1. 從自動完成結果中選擇適當的用戶或角色。
   * 您可以選取多個使用者或角色。
1. 檢查所選用戶或角色應具有的訪問選項，然後按一下&#x200B;**添加**。
   ![將訪問權限添加到配置](assets/configuration-edit.png)
1. 重複這些步驟以選擇用戶或角色，並根據需要指派其他訪問權限。
1. 完成後，點選或按一下「儲存並關閉」。****

## 以{#configurations-developer}開發人員身份進行的設定

身為開發人員，請務必瞭解AEM雲端服務如何處理組態，以及它如何處理組態解析。

### 配置和內容分離{#separation-of-config-and-content}

雖然[管理員和使用者可能將組態視為工作場所](#configurations-administrator)來管理不同的設定和內容，但請務必瞭解AEM會在儲存庫中個別儲存和管理組態和內容。

* `/content` 是所有內容的所在位置。
* `/conf` 是所有配置的首頁。

內容會透過`cq:conf`屬性參考其相關的組態。 AEM會根據內容執行查閱，其內容`cq:conf`屬性會提供相關設定。

### 範例 {#developer-example}

在此範例中，假設您有一些對DAM設定感興趣的應用程式碼。

```java
Conf conf = resource.adaptTo(Conf.class);
ValueMap imageServerSettings = conf.getItem("dam/imageserver");
String bgkcolor = imageServerSettings.get("bgkcolor", "FFFFFF");
```

所有組態查閱的起點都是內容資源，通常位於`/content`下方。 這可以是頁面、頁面內的元件、資產或DAM資料夾。 這是我們要尋找的實際內容，以找出適用於此內容的正確設定。

現在，有了`Conf`物件，我們就可以擷取我們感興趣的特定設定項目。 在本例中，它是`dam/imageserver`，是與`imageserver`相關的設定集合。 `getItem`呼叫傳回`ValueMap`。 接著，我們讀取`bgkcolor`字串屬性，並在屬性（或整個設定項目）不存在時提供預設值&quot;FFFFFF&quot;。

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

在此示例中，我們假設此處有一個WKND特定的DAM資料夾和相應的配置。 從該資料夾`/content/dam/wknd`開始，我們將看到一個名為`cq:conf`的字串屬性，它引用應該應用於子樹的配置。 屬性通常會設定在資產資料夾或頁面的`jcr:content`上。 這些`conf`連結是明確的，因此只要查看CRXDE中的內容，就可輕鬆追蹤。

在`/conf`內跳過時，我們會遵循參考，看到有一個`/conf/wknd`節點。 這是一個配置。 請注意，其查閱對應用程式碼完全透明。 范常式式碼從未有專用的參考，它隱藏在`Conf`物件後面。 所套用的組態完全由JCR內容控制。

我們看到此配置包含一個固定名稱的`settings`節點，該節點包含實際項目，包括我們的情況所需的`dam/imageserver`。 此類項目可視為「設定檔案」，通常由`cq:Page`表示，其中包含保存實際內容的`jcr:content`。

最後，我們會看到范常式式碼所需的`bgkcolor`屬性。 我們從`getItem`返回的`ValueMap`基於頁面的`jcr:content`節點。

### 配置解析度{#configuration-resolution}

上述基本範例顯示單一組態。 但是，在很多情況下，您想要擁有不同的配置，例如預設全局配置、每個品牌的不同配置，以及子項目的特定配置。

若要支援此功能，AEM中的設定查閱會依下列偏好設定順序提供繼承和備援機制：

1. `/conf/<siteconfig>/<parentconfig>/<myconfig>`
   * `/content`中`cq:conf`某處引用的特定配置
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
   * 由`admin`角色設定
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

### 使用配置{#using-configurations}

AEM中的設定是以Sling Context-Aware Configurations為基礎。 Sling bundles提供服務API，可用來取得內容感應設定。 上下文感知配置是與內容資源或資源樹相關的配置，如上例中所述。](#developer-example)[

如需上下文感知組態的詳細資訊、範例及如何使用，請[參閱Sling檔案。](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html)

### ConfMgr Web控制台{#confmgr-web-console}

為了進行調試和測試，`https://<host>:<port>/system/console/conf`**ConfMgr** Web控制台位於&lt;a2/> ，可顯示給定路徑／項的配置。

![ConfMgr](assets/configuration-confmgr.png)

只要提供：

* **內容路徑**
* **項目**
* **使用者**

按一下&#x200B;**Resolve**&#x200B;查看哪些配置已解析並接收將解析這些配置的示例代碼。

### 上下文感知配置Web控制台{#context-aware-web-console}

為了進行調試和測試，`https://<host>:<port>/system/console/slingcaconfig`**** Web控制台中提供&lt;a0/>上下文感知配置&lt;a1/> ，允許查詢儲存庫中的上下文感知配置並查看其屬性。

![上下文感知配置Web控制台](assets/configuration-context-aware-console.png)

只要提供：

* **內容路徑**
* **配置名稱**

按一下&#x200B;**Resolve**&#x200B;以檢索選定配置的相關上下文路徑和屬性。
