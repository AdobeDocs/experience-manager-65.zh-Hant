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
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 0%

---


# 自定義控制台{#customizing-the-consoles}

>[!CAUTION]
>
>本檔案說明如何在現代化觸控式使用者介面中自訂主控台，而不適用於傳統使用者介面。

AEM提供多種機制，讓您自訂製作例項的控制台（以及[頁面製作功能](/help/sites-developing/customizing-page-authoring-touch.md)）。

* Clientlibs
Clientlibs可讓您擴充預設實作，以實現新功能，同時重複使用標準函式、物件和方法。 在自訂時，您可以在`/apps.`下建立自己的clientlib，例如，它可以保存自訂元件所需的程式碼。

* 覆蓋
覆蓋是以節點定義為基礎，可讓您以您自己的自訂功能（在`/libs`中）覆蓋標準功能。 `/apps`當建立覆蓋時，不需要原稿的1:1復本，因為sling資源合併允許繼承。

這些功能可以透過多種方式來擴充AEM主控台。 以下涵蓋小部分選擇（在高層）。

>[!NOTE]
>
>如需詳細資訊，請參閱：
>
>* 使用並建立[clientlibs](/help/sites-developing/clientlibs.md)。
>* 使用並建立[覆蓋](/help/sites-developing/overlays.md)。
>* [花崗岩](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)

>
>
此主題也會在[AEM Gems](https://docs.adobe.com/content/ddc/en/gems.html)工作階段- [AEM 6.0](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html)的使用者介面自訂中討論。

>[!CAUTION]
>
>您&#x200B;***必須***&#x200B;不要變更`/libs`路徑中的任何項目。
>
>這是因為下次升級實例時會覆寫`/libs`的內容（套用修補程式或功能套件時，很可能會覆寫）。
>
>配置和其他更改的建議方法為：
>
>1. 在`/apps`下重新建立所需項目（如`/libs`中所存在）
   >
   >
1. 在`/apps`中進行任何更改

>



例如，`/libs`結構中的以下位置可以重疊：

* 控制台（任何以Granite UI頁面為基礎的控制台）;例如：

   * `/libs/wcm/core/content`

>[!NOTE]
>
>請參閱知識庫文章「疑難排解AEM TouchUI問題」[，以取得更多提示和工具。](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html)

## 自定義控制台{#customizing-the-default-view-for-a-console}的預設視圖

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

   * **名稱**:  `sling:orderBefore`
   * **類型**:  `String`
   * **值**:  `column`

### 新增動作至工具列{#add-new-action-to-the-toolbar}

1. 您可以建立自己的元件，並包含自訂動作的對應用戶端程式庫。 例如，**Promote to Twitter**&#x200B;動作位於：

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   然後，您可以將它連接至主控台上的工具列項目：

   `/apps/<yourProject>/admin/ext/launches`

   例如，在選擇模式中：

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### 將工具列動作限制為特定群組{#restrict-a-toolbar-action-to-a-specific-group}

1. 您可以使用自訂演算條件來覆蓋標準動作，並強加在演算前必須履行的特定條件。

   例如，建立元件以根據群組控制轉譯條件：

   `/apps/myapp/components/renderconditions/group`

1. 要將這些應用於「站點」控制台上的「建立站點」操作，請執行以下操作：

   `/libs/wcm/core/content/sites`

   建立覆蓋：

   `/apps/wcm/core/content/sites`

1. 然後新增動作的轉譯條件：

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   使用此節點上的屬性，可以定義允許執行特定操作的`groups`;例如，`administrators`

### 自定義清單視圖{#customizing-columns-in-the-list-view}中的列

>[!NOTE]
>
>此功能已針對多欄文字欄位最佳化；對於其他資料類型，可以覆蓋`/apps`中的`cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer`。

要自定義清單視圖中的列：

1. 覆蓋可用欄的清單。

   * 在節點上：

      ```
             /apps/wcm/core/content/common/availablecolumns
      ```

   * 新增欄或移除現有欄。
   如需詳細資訊，請參閱[使用覆蓋（和Sling Resource Merger）](/help/sites-developing/overlays.md)。

1. （可選）:

   * 如果您想要插入其他資料，則需要使用[](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageInfoProvider.html)
      `pageInfoProviderType` 屬性.

   例如，請參閱下方所附的類別／搭售（來自GitHub）。

1. 您現在可以在清單檢視的欄設定器中選取欄。

### 篩選資源{#filtering-resources}

使用主控台時，常見的使用案例是使用者必須從資源（例如頁面、元件、資產等）中選擇。 這可以以清單的形式，例如作者必須從中選擇項目。

為了將清單保持在合理大小並且與使用案例相關，可以以自訂謂詞的形式實作篩選器。 如需詳細資訊，請參閱[本文](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources)。
