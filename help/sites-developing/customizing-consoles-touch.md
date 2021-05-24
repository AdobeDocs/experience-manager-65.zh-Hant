---
title: 自訂主控台
seo-title: 自訂主控台
description: AEM提供多種機制，讓您自訂製作執行個體的主控台
seo-description: AEM提供多種機制，讓您自訂製作執行個體的主控台
uuid: 8ecce9ff-5907-41e1-af3b-a8646352d633
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 61a4e196-bd53-4ef0-816b-c14401462457
docset: aem65
exl-id: 6e67f2b3-78b9-45f2-b496-61776b9fd9cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 0%

---

# 自訂主控台{#customizing-the-consoles}

>[!CAUTION]
>
>本檔案說明如何在現代化、觸控式UI中自訂主控台，且不適用於傳統UI。

AEM提供多種機制，讓您可自訂製作例項的主控台（和[頁面製作功能](/help/sites-developing/customizing-page-authoring-touch.md)）。

* Clientlibs
Clientlibs可讓您擴充預設實作以實現新功能，同時重複使用標準函式、物件和方法。 自訂時，您可以在`/apps.`下建立自己的clientlib，例如，它可以保留自訂元件所需的程式碼。

* 覆蓋
覆蓋是根據節點定義，並可讓您以您自己的自訂功能（在`/apps`中）覆蓋標準功能（在`/libs`中）。 建立覆蓋時不需要原始資料的1:1副本，因為Sling資源合併允許繼承。

這些功能可用於擴充AEM主控台的許多方式。 下面（以高級別）列出了一小部分選項。

>[!NOTE]
>
>如需詳細資訊，請參閱：
>
>* 使用並建立[clientlibs](/help/sites-developing/clientlibs.md)。
>* 使用並建立[覆蓋](/help/sites-developing/overlays.md)。
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)

>
>
[AEM Gems](https://docs.adobe.com/content/ddc/en/gems.html)工作階段 — [針對AEM 6.0](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html)自訂使用者介面中也涵蓋此主題。

>[!CAUTION]
>
>您&#x200B;***必須***&#x200B;不要變更`/libs`路徑中的任何項目。
>
>這是因為下次升級執行個體時會覆寫`/libs`的內容（而當您套用Hotfix或Feature Pack時，很可能會覆寫）。
>
>設定和其他變更的建議方法為：
>
>1. 在`/apps`下重新建立所需項（即`/libs`中存在的項）
   >
   >
1. 在`/apps`內進行任何更改

>



例如，`/libs`結構內的以下位置可重疊：

* 主控台（任何以Granite UI頁面為基礎的主控台）;例如：

   * `/libs/wcm/core/content`

>[!NOTE]
>
>如需進一步提示和工具，請參閱知識庫文章[疑難排解AEM TouchUI問題](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html)。

## 自定義控制台的預設視圖{#customizing-the-default-view-for-a-console}

您可以自訂主控台的預設檢視（欄、卡片、清單）:

1. 您可以從以下位置覆蓋所需條目，以重新排序視圖：

   `/libs/wcm/core/content/sites/jcr:content/views`

   第一個項目將是預設項目。

   可用的節點與可用的視圖選項相關聯：

   * `column`
   * `card`
   * `list`

1. 例如，在清單的覆蓋中：

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   定義下列屬性：

   * **名稱**:  `sling:orderBefore`
   * **類型**:  `String`
   * **值**:  `column`

### 將新操作添加到工具欄{#add-new-action-to-the-toolbar}

1. 您可以建立自己的元件，並包含自訂動作的對應用戶端程式庫。 例如，**提升至Twitter**&#x200B;動作位於：

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   接著，即可將此連結至主控台上的工具列項目：

   `/apps/<yourProject>/admin/ext/launches`

   例如，在選擇模式中：

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### 將工具欄操作限制為特定組{#restrict-a-toolbar-action-to-a-specific-group}

1. 您可以使用自訂轉譯條件來覆蓋標準動作，並強加在轉譯前必須履行的特定條件。

   例如，建立元件以根據群組控制呈現條件：

   `/apps/myapp/components/renderconditions/group`

1. 若要將這些套用至Sites主控台上的「建立網站」動作：

   `/libs/wcm/core/content/sites`

   建立覆蓋：

   `/apps/wcm/core/content/sites`

1. 然後新增動作的呈現條件：

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   使用此節點上的屬性，可以定義允許執行特定操作的`groups`;例如`administrators`

### 自定義清單視圖{#customizing-columns-in-the-list-view}中的列

>[!NOTE]
>
>此功能已針對文字欄位欄位最佳化；對於其他資料類型，可以覆蓋`/apps`中的`cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer`。

要自定義清單視圖中的列：

1. 覆蓋可用欄的清單。

   * 在節點上：

      ```
             /apps/wcm/core/content/common/availablecolumns
      ```

   * 新增欄或移除現有欄。
   如需詳細資訊，請參閱[使用覆蓋（和Sling Resource Merger）](/help/sites-developing/overlays.md) 。

1. （可選）:

   * 如果要插入其他資料，需要使用[](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageInfoProvider.html)
      `pageInfoProviderType` 屬性.

   例如，請參閱下方附加的類別/套件組合（來自GitHub）。

1. 您現在可以在清單檢視的欄設定器中選取欄。

### 篩選資源{#filtering-resources}

使用主控台時，常見的使用案例是使用者必須從資源（例如頁面、元件、資產等）中選取。 這可以採用清單的形式，例如，作者必須從中選擇項目。

為了使清單保持在合理的大小以及與使用案例相關的大小，可以以自訂述詞的形式實施篩選器。 如需詳細資訊，請參閱[本文](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources)。
