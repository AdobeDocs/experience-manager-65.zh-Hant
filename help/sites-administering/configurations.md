---
title: 設定和設定瀏覽器
description: 了AEM解中的配置及其管理工作區設定AEM的方式。
exl-id: 1be5849b-748c-48e8-afa8-35a9026c27b3
source-git-commit: 84b16dd1a60f731b568dd87ef89699875cb86596
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 6%

---

# 設定和設定瀏覽器 {#configuration-browser}

配AEM置用於管理工AEM作區中的設定。

## 什麼是設定？ {#what-is-a-configuration}

配置可以從兩個不同的視點考慮。

* [管理員](#configurations-administrator) 將配置用作中的工AEM作區，以定義和管理設定組。
* [開發者](#configurations-developer) 使用實現配置的底層配置機制來保留和查找中的設AEM置。

總之：從管理員的角度來看，配置是您建立工作區以管理中的設定的方式AEM，而開發人員應瞭解在儲存庫中AEM如何使用和管理這些配置。

無論從您的角度如何，配置都可用於以下兩個主要目AEM的：

* 配置為特定用戶組啟用某些功能。
* 配置定義這些功能的訪問權限。

## 作為管理員的配置 {#configurations-administrator}

管AEM理員和作者都可以將配置視為工作區。 通過對這些功能實施訪問權限，這些工作區可用於將設定組及其關聯內容收集到一起，以便組織使用。

可以為內部的許多不同功能建立配AEM置。

* [雲端設定](/help/sites-administering/configurations.md)
* [上下文中心段](/help/sites-administering/segmentation.md)
* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
* [可編輯的範本](/help/sites-authoring/templates.md)

### 範例 {#administrator-example}

例如，管理員可以為可編輯模板建立兩種配置。

* WKND-General
* WKND雜誌

然後，管理員可以使用WKND-General配置建立一般頁面模板，然後在WKND-Magazine下建立特定於該雜誌的模板。

然後，管理員可以將WKND-General與WKND站點的所有內容相關聯。 但是，WKND-Magazine配置將僅與雜誌網站關聯。

通過執行以下操作：

* 當內容作者為雜誌建立新頁面時，作者可以從常規模板(WKND-General)或雜誌模板(WKND-Magazine)中進行選擇。
* 當內容作者為網站的另一部分（不是雜誌）建立新頁面時，作者只能從常規模板(WKND-General)中進行選擇。

不僅可編輯模板，而且雲配置、上下文中心段和內容片段模型也可進行類似的設定。

### 使用配置瀏覽器 {#using-configuration-browser}

配置瀏覽器允許管理員輕鬆建立、管理和配置中的配置訪問權AEM限。

>[!NOTE]
>
>只有在用戶具有 `admin` 。 `admin` 為了分配對配置的訪問權限或以其他方式修改配置，還需要有權限。

#### 建立設定 {#creating-a-configuration}

使用配置瀏覽器在中建立新AEM配置非常簡單。

1. 登錄AEM到as a Cloud Service並從主菜單選擇 **工具** -> **常規** -> **配置瀏覽器**。
1. 點選或按一下&#x200B;**建立**。
1. 提供設定的&#x200B;**標題**&#x200B;和&#x200B;**名稱**。

   ![建立設定](assets/configuration-create.png)

   * **標題** 應該是描述性的。
   * **名稱**&#x200B;將成為存放庫中的節點名稱。
      * 它會根據標題自動產生，並根據[AEM 命名慣例](/help/sites-developing/naming-conventions.md)進行調整
      * 如有需要，可加以調整。
1. 檢查您希望允許的配置類型。
   * [雲端設定](/help/sites-administering/configurations.md)
   * [上下文中心段](/help/sites-administering/segmentation.md)
   * [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)
   * [可編輯的範本](/help/sites-authoring/templates.md)
1. 點選或按一下&#x200B;**建立**。

>[!TIP]
>
>配置可以嵌套。

#### 編輯配置及其訪問權限 {#access-rights}

如果將配置視為工作區，則可以對這些配置設定訪問權限，以強制哪些人可以訪問這些工作區，哪些人可能不訪問這些工作區。

1. 登錄AEM到as a Cloud Service並從主菜單選擇 **工具** -> **常規** -> **配置瀏覽器**。
1. 選擇要修改的配置，然後點擊或按一下 **屬性** 的雙曲餘切值。
1. 選擇要添加到配置的任何附加功能
   >[!NOTE]
   >
   >建立配置後，不能取消選取特徵。
1. 使用 **有效權限** 按鈕，查看角色清單以及當前授予配置的權限。
   ![有效權限窗口](assets/configuration-effective-permissions.png)
1. 要分配新權限，請在 **選擇用戶或組** 的 **添加新權限** 的子菜單。
   * 的  **選擇用戶或組** 欄位根據現有用戶和角色提供自動完成功能。
1. 從自動完成結果中選擇相應的用戶或角色。
   * 您可以選擇多個用戶或角色。
1. 檢查所選用戶或角色應具有的訪問選項，然後按一下 **添加**。
   ![向配置添加訪問權限](assets/configuration-edit.png)
1. 重複這些步驟以選擇用戶或角色，並根據需要分配其他訪問權限。
1. 點擊或按一下 **保存並關閉** 的子菜單。

## 作為開發人員的配置 {#configurations-developer}

作為開發人員，瞭解as a Cloud Service與配AEM置的工作方式及其如何處理配置解析非常重要。

### 配置和內容的分離 {#separation-of-config-and-content}

儘管 [管理員和用戶可能將配置視為工作區](#configurations-administrator) 要管理不同的設定和內容，必須瞭解配置和內容是由儲存庫中單獨儲存和AEM管理的。

* `/content` 是所有內容的家。
* `/conf` 是所有配置的主目錄。

內容通過 `cq:conf` 屬性。 根AEM據內容及其上下文執行查找 `cq:conf` 屬性，以查找相應的配置。

### 範例 {#developer-example}

在此示例中，假設您有一些對DAM設定感興趣的應用程式碼。

```java
Conf conf = resource.adaptTo(Conf.class);
ValueMap imageServerSettings = conf.getItem("dam/imageserver");
String bgkcolor = imageServerSettings.get("bgkcolor", "FFFFFF");
```

所有配置查找的起點是內容資源，通常位於 `/content`。 這可以是頁面、頁面內的元件、資產或DAM資料夾。 這是我們要查找的實際內容，這些內容適用於此上下文。

現在 `Conf` 對象在手中，我們可以檢索我們感興趣的特定配置項目。 在這個例子裡 `dam/imageserver`，是與 `imageserver`。 的 `getItem` 呼叫返回 `ValueMap`。 然後我們讀 `bgkcolor` string屬性，並在屬性（或整個配置項）不存在時提供預設值「FFFFFF」。

現在，讓我們看一下相應的JCR內容：

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

在此示例中，我們假定此處是WKND特定的DAM資料夾和相應的配置。 從該資料夾開始 `/content/dam/wknd`，我們將看到一個名為 `cq:conf` 引用應用於子樹的配置。 該屬性通常在 `jcr:content` 的子菜單。 這些 `conf` 連結是明確的，因此只需查看CRXDE中的內容就可以輕鬆跟蹤。

跳入 `/conf`，我們參考一下 `/conf/wknd` 的下界。 這是配置。 請注意，其查找對應用程式碼完全透明。 示例代碼從未對它有專門的引用，它隱藏在 `Conf` 的雙曲餘切值。 應用哪種配置通過JCR內容完全控制。

我們看到配置包含一個固定名稱 `settings` 包含實際項的節點，包括 `dam/imageserver` 我們需要的。 此類項目可視為「設定文檔」，通常由 `cq:Page` 包括 `jcr:content` 保存實際內容。

最後，我們看到 `bgkcolor` 我們的樣本代碼需要的。 的 `ValueMap` 我們從 `getItem` 是基於頁面 `jcr:content` 的下界。

### 配置解析 {#configuration-resolution}

上面的基本示例顯示了單個配置。 但是，在很多情況下，您希望擁有不同的配置，例如預設的全局配置、每個品牌的不同配置，以及子項目的特定配置。

要支援此功能，中的配置查AEM找具有繼承和回退機制，其優先順序如下：

1. `/conf/<siteconfig>/<parentconfig>/<myconfig>`
   * 引用的特定配置 `cq:conf` 某處 `/content`
   * 層次結構是任意的，可以像您的站點結構一樣設計，但知道這一點不是應用程式碼的業務
   * 具有配置權限的用戶在運行時可更改
1. `/conf/<siteconfig>/<parentconfig>`
   * 遍歷備用配置的父級
   * 具有配置權限的用戶在運行時可更改
1. `/conf/<siteconfig>`
   * 遍歷備用配置的父級
   * 具有配置權限的用戶在運行時可更改
1. `/conf/global`
   * 系統全局設定
   * 通常是安裝的全局預設值
   * 由 `admin` 角色
   * 具有配置權限的用戶在運行時可更改
1. `/apps`
   * 應用程式預設值
   * 通過應用程式部署修復
   * 運行時只讀
1. `/libs`
   * 產AEM品預設值
   * 僅按Adobe更改，不允許項目訪問
   * 通過應用程式部署修復
   * 運行時只讀

### 使用配置 {#using-configurations}

中的配AEM置基於Sling上下文感知配置。 Sling捆綁包提供可用於獲取上下文感知配置的服務API。 上下文感知配置是與內容資源或資源樹相關的配置 [上例中介紹。](#developer-example)

有關上下文感知配置、示例以及如何使用這些配置的詳細資訊， [請參閱Sling文檔。](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html)

### ConfMgr Web控制台 {#confmgr-web-console}

為了調試和測試， **ConfMgr** Web控制台 `https://<host>:<port>/system/console/conf`，可顯示給定路徑/項的配置。

![ConfMgr](assets/configuration-confmgr.png)

只需提供：

* **內容路徑**
* **項目**
* **使用者**

按一下 **解決** 查看已解析的配置並接收將解析這些配置的示例代碼。

### 上下文感知配置Web控制台 {#context-aware-web-console}

為了調試和測試， **上下文感知配置** Web控制台 `https://<host>:<port>/system/console/slingcaconfig`，它允許查詢儲存庫中的上下文感知配置並查看其屬性。

![上下文感知配置Web控制台](assets/configuration-context-aware-console.png)

只需提供：

* **內容路徑**
* **配置名稱**

按一下 **解決** 檢索選定配置的關聯上下文路徑和屬性。
