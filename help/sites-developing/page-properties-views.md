---
title: 自訂頁面屬性的檢視
seo-title: 自訂頁面屬性的檢視
description: 每個頁面都有一組屬性，您可以視需要編輯
seo-description: 每個頁面都有一組屬性，您可以視需要編輯
uuid: cbfca6e6-cb9e-43b1-8889-09a7cc9f8a51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6f8e08d1-831e-441a-ad1a-f5c8788f32d7
exl-id: 292874bf-2ee6-4638-937c-f8f26c93ca65
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# 自訂頁面屬性的檢視{#customizing-views-of-page-properties}

每個頁面都有一組[properties](/help/sites-authoring/editing-page-properties.md)，可供使用者檢視及編輯；建立頁面（建立檢視）時需要一些，其他則可在稍後階段檢視及編輯（編輯檢視）。 這些頁面屬性已定義，並可由適當頁面元件的對話方塊(`cq:dialog`)使用。

>[!CAUTION]
>
>傳統UI中無法自訂頁面屬性的檢視。

每個頁面屬性的預設狀態為：

* 隱藏於建立檢視中(例如&#x200B;**建立頁面**&#x200B;精靈)

* 可在編輯檢視中使用(例如&#x200B;**查看屬性**)

如果需要任何變更，則必須明確設定欄位。 這是使用適當的節點屬性完成的：

* 可在建立檢視中使用的頁面屬性(例如&#x200B;**建立頁面**&#x200B;精靈):

   * 名稱: `cq:showOnCreate`
   * 類型: `Boolean`

* 可在編輯檢視中使用的頁面屬性(例如&#x200B;**查看**/**編輯**)**屬性**&#x200B;選項):

   * 名稱: `cq:hideOnEdit`
   * 類型: `Boolean`

例如，請參閱基礎頁面元件&#x200B;**Basic**&#x200B;標籤上&#x200B;**More Titles and Description**&#x200B;下分組欄位的設定。 在&#x200B;**建立頁面**&#x200B;精靈中，這些顯示為，因為`cq:showOnCreate`已設為`true`:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>如需自訂頁面屬性的指南，請參閱[擴充頁面屬性教學課程](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html)。

## 設定頁面屬性{#configuring-your-page-properties}

您也可以設定頁面元件的對話方塊並套用適當的節點屬性，以設定可用欄位。

例如，預設情況下，[**建立頁面**&#x200B;精靈](/help/sites-authoring/managing-pages.md#creating-a-new-page)顯示在&#x200B;**更多標題和說明**&#x200B;下分組的欄位。 若要隱藏您設定的這些項目：

1. 在`/apps`下建立頁面元件。
1. 為頁面元件的`basic`區段建立覆寫（使用[Sling Resource Merger](/help/sites-developing/sling-resource-merger.md)提供的&#x200B;*dialog diff*）;例如：

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >如需參考，請參閱：
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   但是，您&#x200B;***必須***&#x200B;不更改`/libs`路徑中的任何內容。
   這是因為下次升級執行個體時會覆寫`/libs`的內容（而當您套用Hotfix或Feature Pack時，很可能會覆寫）。
   設定和其他變更的建議方法為：
   1. 在`/apps`下重新建立所需項（即`/libs`中存在的項）
   1. 在`/apps`內進行任何更改


1. 在`basic`上設定`path`屬性，以指向基本索引標籤的覆寫（另請參閱下一步）。 例如：

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. 在對應路徑建立`basic` - `moretitles`區段的覆寫；例如：

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. 應用相應的節點屬性：

   * **名稱**:  `cq:showOnCreate`
   * **類型**:  `Boolean`
   * **值**:  `false`

   **更多標題和說明**&#x200B;區段將不再顯示在&#x200B;**建立頁面**&#x200B;精靈中。

>[!NOTE]
如需詳細資訊，請參閱[在頁面屬性上設定MSM鎖](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) 。

## 頁面屬性的設定範例{#sample-configuration-of-page-properties}

此範例示範[Sling Resource Merger](/help/sites-developing/sling-resource-merger.md)；的對話方塊差異技術包括使用[`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties)。 它也說明了`cq:showOnCreate`和`cq:hideOnEdit`的使用。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-extension-page-dialog專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
