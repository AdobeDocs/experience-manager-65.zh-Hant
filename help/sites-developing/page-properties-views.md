---
title: 自訂頁面屬性的檢視
seo-title: 自訂頁面屬性的檢視
description: 每個頁面都有一組屬性，您可視需要加以編輯
seo-description: 每個頁面都有一組屬性，您可視需要加以編輯
uuid: cbfca6e6-cb9e-43b1-8889-09a7cc9f8a51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6f8e08d1-831e-441a-ad1a-f5c8788f32d7
translation-type: tm+mt
source-git-commit: c38c27d6f7172734f80735dd2f42cfa7bf58ad1d
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---


# 自訂頁面屬性的檢視{#customizing-views-of-page-properties}

每個頁面都有一組[屬性](/help/sites-authoring/editing-page-properties.md)可供使用者檢視和編輯；有些是建立頁面（建立檢視）時的必要項目，有些則可在稍後階段檢視和編輯（編輯檢視）。 這些頁面屬性由適當頁面元件的對話方塊(`cq:dialog`)定義並提供。

>[!CAUTION]
>
>傳統UI中無法自訂頁面屬性的檢視。

每個頁面屬性的預設狀態為：

* 隱藏於建立檢視中(例如&#x200B;**建立頁面**&#x200B;精靈)

* (例如，**檢視屬性**)

如果需要任何變更，必須特別設定欄位。 這是使用適當的節點屬性來完成的：

* 頁面屬性可用於建立檢視(例如&#x200B;**建立頁面**&#x200B;精靈):

   * 名稱: `cq:showOnCreate`
   * 類型: `Boolean`

* 可在編輯檢視中使用的頁面屬性(例如&#x200B;**View**/**Edit**)**Properties**&#x200B;選項：

   * 名稱: `cq:hideOnEdit`
   * 類型: `Boolean`

例如，請參閱基礎頁面元件&#x200B;**Basic**&#x200B;標籤上&#x200B;**更多標題和說明**&#x200B;下分組欄位的設定。 在&#x200B;**Create Page**&#x200B;精靈中，這些項目可見，因為`cq:showOnCreate`已設為`true`:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>如需自訂頁面屬性的指南，請參閱[擴充頁面屬性教學課程](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html)。

## 設定您的頁面屬性{#configuring-your-page-properties}

您也可以設定頁面元件的對話方塊並套用適當的節點屬性，以設定可用的欄位。

例如，依預設，[**建立頁面**&#x200B;精靈](/help/sites-authoring/managing-pages.md#creating-a-new-page)會顯示在&#x200B;**更多標題和說明**&#x200B;下方分組的欄位。 若要隱藏您設定的這些項目：

1. 在`/apps`下建立您的頁面元件。
1. 為頁面元件的`basic`區段建立覆寫（使用&#x200B;**&#x200B;由[Sling Resource Merger](/help/sites-developing/sling-resource-merger.md)提供的對話diff&lt;a1/>）;例如：

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >如需參考，請參閱：
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   但是，您&#x200B;***必須***&#x200B;不要變更`/libs`路徑中的任何項目。
   這是因為下次升級實例時會覆寫`/libs`的內容（套用修補程式或功能套件時，很可能會覆寫）。
   配置和其他更改的建議方法為：
   1. 在`/apps`下重新建立所需項目（如`/libs`中所存在）
   1. 在`/apps`中進行任何更改


1. 將`basic`上的`path`屬性設為指向基本頁籤的覆蓋（另請參見下一步）。 例如：

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. 在對應的路徑上建立`basic` - `moretitles`區段的覆寫；例如：

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. 應用適當的節點屬性：

   * **名稱**:  `cq:showOnCreate`
   * **類型**:  `Boolean`
   * **值**:  `false`

   **更多標題和說明**&#x200B;區段將不再顯示在&#x200B;**建立頁面**&#x200B;精靈中。

>[!NOTE]
如需詳細資訊，請參閱[在頁面屬性上設定MSM鎖。](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui)

## 頁面屬性的範例設定{#sample-configuration-of-page-properties}

此範例示範[Sling Resource Merger](/help/sites-developing/sling-resource-merger.md)；的對話比較技術包括[`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties)的使用。 它還說明了`cq:showOnCreate`和`cq:hideOnEdit`的使用。

GITHUB代碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-extension-page-dialog專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
