---
title: 自訂主控台
seo-title: Customizing the Consoles
description: AEM提供多種機制，讓您自訂製作執行個體的主控台
seo-description: AEM provides various mechanisms to enable you to customize the consoles of your authoring instance
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
source-wordcount: '699'
ht-degree: 0%

---

# 自訂主控台 {#customizing-the-consoles}

>[!CAUTION]
>
>本檔案說明如何在現代化、觸控式UI中自訂主控台，且不適用於傳統UI。

AEM提供多種機制，讓您自訂主控台(和 [頁面製作功能](/help/sites-developing/customizing-page-authoring-touch.md))。

* Clientlibs Clientlibs可讓您擴充預設實施以實現新功能，同時重複使用標準函式、物件和方法。 自訂時，您可以在 `/apps.` 例如，它可以保留自訂元件所需的程式碼。

* 覆蓋覆蓋圖是根據節點定義，並可讓您覆蓋標準功能(在 `/libs`)，以及 `/apps`)。 建立覆蓋時不需要原始資料的1:1副本，因為Sling資源合併允許繼承。

這些功能可用於擴充AEM主控台的許多方式。 下面（以高級別）列出了一小部分選項。

>[!NOTE]
>
>如需詳細資訊，請參閱：
>
>* 使用和建立 [clientlibs](/help/sites-developing/clientlibs.md).
>* 使用和建立 [覆蓋](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)
>
>本主題亦於 [AEM Gems](https://docs.adobe.com/content/ddc/en/gems.html) 工作階段 —  [AEM 6.0的使用者介面自訂](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html).

>[!CAUTION]
>
>您 ***必須*** 不會變更 `/libs` 路徑。
>
>這是因為 `/libs` 下次升級執行個體時即會覆寫（而當您套用Hotfix或Feature Pack時，很可能會覆寫）。
>
>設定和其他變更的建議方法為：
>
>1. 重新建立所需項目(亦即， `/libs`)底下 `/apps`
>
>1. 在內進行任何變更 `/apps`

>


例如， `/libs` 結構可重疊：

* 主控台（任何以Granite UI頁面為基礎的主控台）;例如：

   * `/libs/wcm/core/content`

>[!NOTE]
>
>請參閱知識庫文章， [疑難排解AEM TouchUI問題](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html)，以取得更多秘訣和工具。

## 自訂主控台的預設檢視 {#customizing-the-default-view-for-a-console}

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

   * **名稱**: `sling:orderBefore`
   * **類型**: `String`
   * **值**: `column`

### 將新操作添加到工具欄 {#add-new-action-to-the-toolbar}

1. 您可以建立自己的元件，並包含自訂動作的對應用戶端程式庫。 例如， **提升至Twitter** 動作：

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   接著，即可將此連結至主控台上的工具列項目：

   `/apps/<yourProject>/admin/ext/launches`

   例如，在選擇模式中：

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### 將工具列動作限制在特定群組 {#restrict-a-toolbar-action-to-a-specific-group}

1. 您可以使用自訂轉譯條件來覆蓋標準動作，並強加在轉譯前必須履行的特定條件。

   例如，建立元件以根據群組控制呈現條件：

   `/apps/myapp/components/renderconditions/group`

1. 若要將這些套用至Sites主控台上的「建立網站」動作：

   `/libs/wcm/core/content/sites`

   建立覆蓋：

   `/apps/wcm/core/content/sites`

1. 然後新增動作的呈現條件：

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   在此節點上使用屬性，您可以定義 `groups` 允許執行特定動作；例如， `administrators`

### 自訂清單檢視中的欄 {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>此功能已針對文字欄位欄位最佳化；對於其他資料類型，可以覆蓋 `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` in `/apps`.

要自定義清單視圖中的列：

1. 覆蓋可用欄的清單。

   * 在節點上：

      ```
             /apps/wcm/core/content/common/availablecolumns
      ```

   * 新增欄或移除現有欄。
   請參閱 [使用覆蓋（和Sling Resource Merger）](/help/sites-developing/overlays.md) 以取得更多資訊。

1. （可選）:

   * 如果您想要插入其他資料，則需要編寫 [PageInforProvider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageInfoProvider.html) 帶
      `pageInfoProviderType` 屬性.

   例如，請參閱下方附加的類別/套件組合（來自GitHub）。

1. 您現在可以在清單檢視的欄設定器中選取欄。

### 篩選資源 {#filtering-resources}

使用主控台時，常見的使用案例是使用者必須從資源（例如頁面、元件、資產等）中選取。 這可以採用清單的形式，例如，作者必須從中選擇項目。

為了使清單保持在合理的大小以及與使用案例相關的大小，可以以自訂述詞的形式實施篩選器。 請參閱 [這篇文章](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources) 以取得詳細資訊。
