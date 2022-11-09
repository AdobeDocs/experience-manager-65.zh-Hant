---
title: 自訂頁面屬性的檢視
seo-title: Customizing Views of Page Properties
description: 每個頁面都有一組屬性，您可以視需要編輯
seo-description: Every page has a set of properties that you can edit as required
uuid: cbfca6e6-cb9e-43b1-8889-09a7cc9f8a51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6f8e08d1-831e-441a-ad1a-f5c8788f32d7
exl-id: 292874bf-2ee6-4638-937c-f8f26c93ca65
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 1%

---

# 自訂頁面屬性的檢視{#customizing-views-of-page-properties}

每個頁面都有 [屬性](/help/sites-authoring/editing-page-properties.md) 供使用者檢視及編輯；建立頁面（建立檢視）時需要一些，其他則可在稍後階段檢視及編輯（編輯檢視）。 這些頁面屬性已定義，並可供對話方塊使用( `cq:dialog`)。

>[!CAUTION]
>
>傳統UI中無法自訂頁面屬性的檢視。

每個頁面屬性的預設狀態為：

* 隱藏於建立檢視中(例如 **建立頁面** 精靈)

* 可在編輯檢視中使用(例如 **檢視屬性**)

如果需要任何變更，則必須明確設定欄位。 這是使用適當的節點屬性完成的：

* 可在建立檢視中使用的頁面屬性(例如 **建立頁面** 嚮導):

   * 名稱: `cq:showOnCreate`
   * 類型: `Boolean`

* 可在編輯檢視中使用的頁面屬性(例如 **檢視**/**編輯**) **屬性** 選項):

   * 名稱: `cq:hideOnEdit`
   * 類型: `Boolean`

例如，請參閱 **更多標題和說明** 在 **基本** 頁面元件的頁簽。 這些項目會顯示在 **建立頁面** 嚮導 `cq:showOnCreate` 設為 `true`:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>請參閱 [擴充頁面屬性教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) 以取得自訂頁面屬性的指南。

## 設定頁面屬性 {#configuring-your-page-properties}

您也可以設定頁面元件的對話方塊並套用適當的節點屬性，以設定可用欄位。

例如，依預設， [**建立頁面** 精靈](/help/sites-authoring/managing-pages.md#creating-a-new-page) 顯示分組在下的欄位 **更多標題和說明**. 若要隱藏您設定的這些項目：

1. 在下方建立頁面元件 `/apps`.
1. 建立覆蓋(使用 *對話框差異* 由提供 [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md)) `basic` 的區段；例如：

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >如需參考，請參閱：
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   不過，您 ***必須*** 不會變更 `/libs` 路徑。
   這是因為 `/libs` 下次升級執行個體時即會覆寫（而當您套用Hotfix或Feature Pack時，很可能會覆寫）。
   設定和其他變更的建議方法為：
   1. 重新建立所需項目(亦即， `/libs`)底下 `/apps`
   1. 在內進行任何變更 `/apps`


1. 設定 `path` 屬性 `basic` 指向基本索引標籤的覆寫（也請參閱下一步）。 例如：

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. 建立 `basic` - `moretitles` 路徑的節；例如：

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. 應用相應的節點屬性：

   * **名稱**: `cq:showOnCreate`
   * **類型**: `Boolean`
   * **值**: `false`

   此 **更多標題和說明** 區段將不再顯示於 **建立頁面** 嚮導。

>[!NOTE]
設定頁面屬性以與Live Copy搭配使用時，請參閱 [在頁面屬性上設定MSM鎖](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) 以取得更多詳細資訊。

## 頁面屬性的範例設定 {#sample-configuration-of-page-properties}

此範例示範的對話方塊差異技術 [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md);包括使用 [`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties). 這也說明兩者的使用 `cq:showOnCreate` 和 `cq:hideOnEdit`.

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-extension-page-dialog專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
