---
title: 自定義控制台
seo-title: Customizing the Consoles
description: 提AEM供了各種機制，使您能夠自定義創作實例的控制台
seo-description: AEM provides various mechanisms to enable you to customize the consoles of your authoring instance
uuid: 8ecce9ff-5907-41e1-af3b-a8646352d633
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 61a4e196-bd53-4ef0-816b-c14401462457
docset: aem65
exl-id: 6e67f2b3-78b9-45f2-b496-61776b9fd9cc
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 1%

---

# 自定義控制台 {#customizing-the-consoles}

>[!CAUTION]
>
>本文檔介紹如何在現代的、支援觸摸的UI中自定義控制台，不適用於傳統UI。

AEM提供各種機制，使您能夠自定義控制台 [頁面創作功能](/help/sites-developing/customizing-page-authoring-touch.md))。

* 客戶端客戶端允許您擴展預設實現以實現新功能，同時重用標準函式、對象和方法。 自定義時，可以在 `/apps.` 例如，它可以保存自定義元件所需的代碼。

* 「疊加」(Overlays)基於節點定義，允許您疊加標準功能(在 `/libs`) `/apps`)。 在建立覆蓋時，不需要原件的1:1副本，因為吊索資源合併允許繼承。

這些功能可用於擴展控制台AEM。 下面（在高級別）覆蓋了小的選區。

>[!NOTE]
>
>如需進一步詳細資訊，請參閱：
>
>* 使用和建立 [客戶端](/help/sites-developing/clientlibs.md)。
>* 使用和建立 [重疊](/help/sites-developing/overlays.md)。
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)
>



>[!CAUTION]
>
>你 ***必須*** 沒有改變 `/libs` 路徑。
>
>這是因為 `/libs` 在下次升級實例時被覆蓋（在應用修補程式或功能包時很可能被覆蓋）。
>
>建議的配置和其他更改方法是：
>
>1. 重新建立所需項(如 `/libs`) `/apps`
>
>1. 在 `/apps`

>


例如， `/libs` 結構可以重疊：

* 控制台（任何基於Granite UI頁面的控制台）;例如：

   * `/libs/wcm/core/content`

>[!NOTE]
>
>請參閱知識庫文章， [TouchUI問題AEM疑難解答](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html)，以獲取更多提示和工具。

## 自定義控制台的預設視圖 {#customizing-the-default-view-for-a-console}

可以自定義控制台的預設視圖（列、卡、清單）:

1. 通過從下面覆蓋所需條目，可以重新排序視圖：

   `/libs/wcm/core/content/sites/jcr:content/views`

   第一個條目將是預設值。

   可用的節點與可用的視圖選項相關聯：

   * `column`
   * `card`
   * `list`

1. 例如，在清單覆蓋中：

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   定義以下屬性：

   * **名稱**: `sling:orderBefore`
   * **類型**: `String`
   * **值**: `column`

### 將新操作添加到工具欄 {#add-new-action-to-the-toolbar}

1. 您可以構建自己的元件，並包括相應的客戶端庫以執行自定義操作。 例如， **提升到Twitter** 操作：

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   然後，可以將其連接到控制台上的工具欄項：

   `/apps/<yourProject>/admin/ext/launches`

   例如，在選擇模式中：

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### 將工具欄操作限制到特定組 {#restrict-a-toolbar-action-to-a-specific-group}

1. 您可以使用自定義渲染條件來覆蓋標準操作並施加在渲染之前必須滿足的特定條件。

   例如，建立一個元件以根據組控制渲染條件：

   `/apps/myapp/components/renderconditions/group`

1. 要將這些應用於「站點」控制台上的「建立站點」操作：

   `/libs/wcm/core/content/sites`

   建立覆蓋：

   `/apps/wcm/core/content/sites`

1. 然後為操作添加渲染條件：

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   使用此節點上的屬性可以定義 `groups` 允許執行特定操作；比如說， `administrators`

### 自定義清單視圖中的列 {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>此功能已針對文本欄位的列進行優化；對於其他資料類型，可以覆蓋 `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` 在 `/apps`。

要自定義清單視圖中的列：

1. 覆蓋可用列的清單。

   * 在節點上：

      ```
             /apps/wcm/core/content/common/availablecolumns
      ```

   * 添加新列 — 或刪除現有列。
   請參閱 [使用重疊（和吊具資源合併）](/help/sites-developing/overlays.md) 的子菜單。

1. （可選）:

   * 如果要插入其他資料，則需要編寫 [PageInforProvider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) 帶
      `pageInfoProviderType` 屬性.

   例如，請參見下面附加的類/捆綁包（從GitHub）。

1. 現在，您可以在清單視圖的列配置器中選擇該列。

### 篩選資源 {#filtering-resources}

在使用控制台時，通用使用情形是用戶必須從資源（如頁面、元件、資產等）中進行選擇。 這可以採用清單的形式，例如，作者必須從中選擇一個項。

為了使清單保持在合理的大小並且與使用情形相關，可以以自定義謂語的形式實現過濾器。 請參閱 [這篇文章](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources) 的雙曲餘切值。
