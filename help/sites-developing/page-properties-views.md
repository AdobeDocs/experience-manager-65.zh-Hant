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

---


# 自訂頁面屬性的檢視{#customizing-views-of-page-properties}

每個頁面都有一組 [屬性](/help/sites-authoring/editing-page-properties.md) ，供使用者檢視和編輯；有些是建立頁面（建立檢視）時的必要項目，有些則可在稍後階段檢視和編輯（編輯檢視）。 這些頁面屬性由適當頁面元件的對話方塊( `cq:dialog`)定義並提供。

>[!CAUTION]
>
>傳統UI中無法自訂頁面屬性的檢視。

每個頁面屬性的預設狀態為：

* 隱藏於建立檢視中(例如「建立 **頁面精靈** 」)

* 可在編輯檢視中使用(例如「檢視 **屬性」**)

如果需要任何變更，必須特別設定欄位。 這是使用適當的節點屬性來完成的：

* 可在建立視圖中使用的頁屬性(例如「創 **建頁面** 」嚮導):

   * 名稱: `cq:showOnCreate`
   * 類型: `Boolean`

* 可在編輯檢視中使用的頁面屬性(例如 **View**/**Edit**) **屬性** 選項):

   * 名稱: `cq:hideOnEdit`
   * 類型: `Boolean`

例如，請參閱「基礎頁面」元件「基本」標 **簽上「更多標題和說明」****** ，下方分組欄位的設定。 在「建立頁面」 **嚮導中** ，這些 `cq:showOnCreate` 選項將顯示為 `true`:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>如需自訂 [頁面屬性的指南](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) ，請參閱延伸頁面屬性教學課程。

## 設定您的頁面屬性 {#configuring-your-page-properties}

您也可以設定頁面元件的對話方塊並套用適當的節點屬性，以設定可用的欄位。

例如，依預設，「建立頁 [**面」精靈會顯示「更多標題和說&#x200B;**明」下方的欄位](/help/sites-authoring/managing-pages.md#creating-a-new-page)****。 若要隱藏您設定的這些項目：

1. 在下面建立您的頁面元件 `/apps`。
1. 為您的頁面元件 *區段建立覆寫* (使用 [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md)提供的對話區 `basic` 別);例如：

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >如需參考，請參閱：
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   但是，您 ***不得*** 變更路徑中的任 `/libs` 何項目。
   這是因為下次升級 `/libs` 實例時會覆寫的內容（套用修補程式或功能套件時可能會覆寫）。
   配置和其他更改的建議方法為：
   1. 重新建立必要項目(如中所 `/libs`示) `/apps`
   1. 在 `/apps`


1. 將上的 `path` 屬性設 `basic` 為指向基本標籤的覆寫（另請參閱下一步驟）。 例如：

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. 在對應路徑上 `basic` 建立- `moretitles` 節的覆寫；例如：

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. 應用適當的節點屬性：

   * **名稱**: `cq:showOnCreate`
   * **類型**: `Boolean`
   * **值**: `false`
   「建 **立頁面」精靈中** ，將不再顯示「更多標題 **和說明」區段** 。

>[!NOTE]
配置頁面屬性以用於即時副本時，請參 [閱Configuring MSM Locks on Page Properties](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) ，以瞭解詳細資訊。

## 頁面屬性的範例設定 {#sample-configuration-of-page-properties}

此範例示範 [Sling Resource Merger的對話區分技術](/help/sites-developing/sling-resource-merger.md);包括使用 [`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties)。 它還說明了和的 `cq:showOnCreate` 使用 `cq:hideOnEdit`。

GITHUB代碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-extension-page-dialog專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
