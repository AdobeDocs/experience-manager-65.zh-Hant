---
title: 自定義頁面屬性的視圖
seo-title: Customizing Views of Page Properties
description: 每個頁面都有一組屬性，您可以根據需要編輯這些屬性
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

# 自定義頁面屬性的視圖{#customizing-views-of-page-properties}

每頁都有一組 [屬性](/help/sites-authoring/editing-page-properties.md) 用戶可查看和編輯；建立頁面（建立視圖）時需要一些，其他部分則可以在稍後的階段查看和編輯（編輯視圖）。 這些頁面屬性由對話框定義和提供( `cq:dialog`)。

>[!CAUTION]
>
>自定義頁面屬性視圖在傳統UI中不可用。

每個頁屬性的預設狀態為：

* 隱藏在建立視圖中(例如 **建立頁** 嚮導)

* 可在編輯視圖(例如 **查看屬性**)

如果需要更改，必須特別配置欄位。 這是使用適當的節點屬性完成的：

* 可在建立視圖中使用的頁面屬性(例如 **建立頁** ):

   * 名稱: `cq:showOnCreate`
   * 類型: `Boolean`

* 可在編輯視圖中使用的頁面屬性(例如 **視圖**/**編輯**) **屬性** 選項):

   * 名稱: `cq:hideOnEdit`
   * 類型: `Boolean`

例如，請參閱在 **更多標題和說明** 的 **基本** 頁籤。 這些在中可見 **建立頁** 嚮導 `cq:showOnCreate` 已設定為 `true`:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>查看 [擴展頁面屬性教程](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) 的子菜單。

## 配置頁面屬性 {#configuring-your-page-properties}

也可以通過配置頁面元件的對話框和應用相應節點屬性來配置可用欄位。

例如，預設情況下， [**建立頁** 嚮導](/help/sites-authoring/managing-pages.md#creating-a-new-page) 顯示在下面分組的欄位 **更多標題和說明**。 要隱藏您配置的這些內容：

1. 在下面建立頁面元件 `/apps`。
1. 建立覆蓋(使用 *對話框差異* 由 [Sling資源合併](/help/sites-developing/sling-resource-merger.md)) `basic` 頁面元件部分；例如：

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >請參閱：
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   但是，你 ***必須*** 沒有改變 `/libs` 路徑。
   這是因為 `/libs` 在下次升級實例時被覆蓋（在應用修補程式或功能包時很可能被覆蓋）。
   建議的配置和其他更改方法是：
   1. 重新建立所需項(如 `/libs`) `/apps`
   1. 在 `/apps`


1. 設定 `path` 屬性 `basic` 指向對基本頁籤的覆蓋（另請參見下一步）。 例如：

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. 建立對 `basic` - `moretitles` 在相應路徑上分段；例如：

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. 應用相應的節點屬性：

   * **名稱**: `cq:showOnCreate`
   * **類型**: `Boolean`
   * **值**: `false`

   的 **更多標題和說明** 部分將不再顯示在 **建立頁** 的子菜單。

>[!NOTE]
配置用於即時副本的頁面屬性時，請參見 [在頁屬性上配置MSM鎖](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) 的子菜單。

## 頁面屬性配置示例 {#sample-configuration-of-page-properties}

此示例演示了 [Sling資源合併](/help/sites-developing/sling-resource-merger.md);包括使用 [`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties)。 它還說明了兩者的使用 `cq:showOnCreate` 和 `cq:hideOnEdit`。

GITHUB代碼

可以在GitHub上找到此頁的代碼

* [在GitHub上開啟創作擴展頁對話框項目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
