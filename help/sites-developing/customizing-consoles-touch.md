---
title: 自定義控制台
seo-title: 自定義控制台
description: AEM提供多種機制，讓您自訂製作執行個體的主控台
seo-description: AEM提供多種機制，讓您自訂製作執行個體的主控台
uuid: 8ecce9ff-5907-41e1-af3b-a8646352d633
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 61a4e196-bd53-4ef0-816b-c14401462457
docset: aem65
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835

---


# 自定義控制台 {#customizing-the-consoles}

>[!CAUTION]
>
>本檔案說明如何在現代化觸控式使用者介面中自訂主控台，而不適用於傳統使用者介面。

AEM提供多種機制，讓您自訂製作例項的控制台( [以及頁面製作功能](/help/sites-developing/customizing-page-authoring-touch.md))。

* ClientlibsClientlibs可讓您擴充預設實作，以實現新功能，同時重複使用標準函式、物件和方法。 在自訂時，您可以在「例如，它可以 `/apps.` 保存自訂元件所需的代碼」下建立自己的clientlib。

* 覆蓋覆蓋覆蓋以節點定義為基礎，可讓您將標準功能(在 `/libs`)與您自訂的功能(在 `/apps`)覆蓋。 當建立覆蓋時，不需要原稿的1:1復本，因為sling資源合併允許繼承。

這些功能可以透過多種方式來擴充AEM主控台。 以下涵蓋小部分選擇（在高層）。

>[!NOTE]
>
>如需詳細資訊，請參閱：
>
>* 使用和建立 [clientlibs](/help/sites-developing/clientlibs.md)。
>* 使用和建立 [覆蓋](/help/sites-developing/overlays.md)。
>* [花崗岩](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)
>
>
AEM Gems工作階段- [User interface customization for AEM 6.0中也包含](https://docs.adobe.com/content/ddc/en/gems.html) 此主題 [](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html)。

>[!CAUTION]
>
>您 ***不得*** 更改路徑中的任 `/libs` 何內容。
>
>這是因為下次升級 `/libs` 實例時會覆寫的內容（套用修補程式或功能套件時可能會覆寫）。
>
>配置和其他更改的建議方法為：
>
>1. 重新建立下列項目的必要項目(如中所 `/libs`示): `/apps`
   >
   >
1. 在 `/apps`
>



例如，結構中的下列位 `/libs` 置可以覆蓋：

* 控制台（任何以Granite UI頁面為基礎的控制台）;例如：

   * `/libs/wcm/core/content`

>[!NOTE]
>
>請參閱知識庫文章「疑難排 [解AEM TouchUI問題](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html)」，以取得更多提示和工具。

## 自訂控制台的預設檢視 {#customizing-the-default-view-for-a-console}

您可以自訂控制台的預設檢視（欄、卡片、清單）:

1. 您可以在下面覆蓋所需條目，以重新排序視圖：

   `/libs/wcm/core/content/sites/jcr:content/views`

   第一個項目是預設項目。

   可用的節點與可用的視圖選項關聯：

   * `column`
   * `card`
   * `list`

1. 例如，在清單的覆蓋中：

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   定義下列屬性：

   * **名稱**: `sling:orderBefore`
   * **類型**: `String`
   * **值**: `column`

### 將新動作新增至工具列 {#add-new-action-to-the-toolbar}

1. 您可以建立自己的元件，並包含自訂動作的對應用戶端程式庫。 例如，Promote to twitter **動作** :

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   然後，您可以將它連接至主控台上的工具列項目：

   `/apps/<yourProject>/admin/ext/launches`

   例如，在選擇模式中：

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### 將工具列動作限制為特定群組 {#restrict-a-toolbar-action-to-a-specific-group}

1. 您可以使用自訂演算條件來覆蓋標準動作，並強加在演算前必須履行的特定條件。

   例如，建立元件以根據群組控制轉譯條件：

   `/apps/myapp/components/renderconditions/group`

1. 要將這些應用於「站點」控制台上的「建立站點」操作，請執行以下操作：

   `/libs/wcm/core/content/sites`

   建立覆蓋：

   `/apps/wcm/core/content/sites`

1. 然後新增動作的轉譯條件：

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   使用此節點上的屬性，可以定義 `groups` 允許執行特定操作；例如， `administrators`

### 自訂清單檢視中的欄 {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>此功能已針對多欄文字欄位最佳化；對於其他資料類型，可以在中覆 `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` 蓋 `/apps`。

要自定義清單視圖中的列：

1. 覆蓋可用欄的清單。

   * 在節點上：

      ```
             /apps/wcm/core/content/common/availablecolumns
      ```

   * 新增欄或移除現有欄。
   如需 [詳細資訊，請參閱使用覆蓋（和Sling Resource Merger）](/help/sites-developing/overlays.md) 。

1. （可選）:

   * 如果您想要插入其他資料，則需要使用 [PageInforProvider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageInfoProvider.html)
      `pageInfoProviderType` 屬性.
   例如，請參閱下方所附的類別／搭售（來自GitHub）。

1. 您現在可以在清單檢視的欄設定器中選取欄。

### 篩選資源 {#filtering-resources}

使用主控台時，常見的使用案例是使用者必須從資源（例如頁面、元件、資產等）中選擇。 這可以以清單的形式，例如作者必須從中選擇項目。

為了將清單保持在合理的大小，並且與使用案例相關，篩選器可以以自訂謂詞的形式實施。 如需詳 [細資訊，請參閱](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources) 本文章。
