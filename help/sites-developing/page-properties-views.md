---
title: 自訂頁面屬性的檢視
seo-title: Customizing Views of Page Properties
description: 每個頁面都有一組屬性，您可以視需要加以編輯
seo-description: Every page has a set of properties that you can edit as required
uuid: cbfca6e6-cb9e-43b1-8889-09a7cc9f8a51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6f8e08d1-831e-441a-ad1a-f5c8788f32d7
exl-id: 292874bf-2ee6-4638-937c-f8f26c93ca65
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 47%

---

# 自訂頁面屬性的檢視{#customizing-views-of-page-properties}

每個頁面都有一組 [屬性](/help/sites-authoring/editing-page-properties.md) 使用者可以檢視和編輯的專案；建立頁面（建立檢視）時需要某些專案，其他專案可在稍後階段檢視和編輯（編輯檢視）。 這些頁面屬性由適當頁面元件的對話框 (`cq:dialog`) 定義和提供。

>[!CAUTION]
>
>傳統UI中不提供自訂頁面屬性檢視。

每個頁面屬性的預設狀態為：

* 在建立檢視中隱藏(例如， **建立頁面** 精靈)

* 可在編輯檢視中使用(例如， **檢視屬性**)

如果需要任何變更，則必須特別設定欄位。這會使用適當的節點屬性完成：

* 頁面屬性會在建立檢視 (例如，**建立頁面**&#x200B;精靈) 中提供：

   * 名稱：`cq:showOnCreate`
   * 類型：`Boolean`

* 編輯檢視中可用的頁面屬性(例如， **檢視**/**編輯**) **屬性** option)：

   * 名稱：`cq:hideOnEdit`
   * 類型：`Boolean`

例如，請參閱「 」底下群組欄位的設定 **更多標題和說明** 於 **基本** 基礎頁面元件的索引標籤。 這些專案會顯示在 **建立頁面** 精靈為 `cq:showOnCreate` 已設為 `true`：

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>如需自訂頁面屬性的指南，請參閱「[擴充頁面屬性教學課程](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html?lang=zh-Hant)」。

## 設定頁面屬性 {#configuring-your-page-properties}

設定頁面元件的對話框並套用適當的節點屬性，還可以設定可用的欄位。

例如，預設情況下，[**建立頁面**&#x200B;精靈](/help/sites-authoring/managing-pages.md#creating-a-new-page)會顯示在&#x200B;**更多標題和說明**&#x200B;下面分組的欄位。若要隱藏這些，您可以設定：

1. 在 `/apps` 下面建立您的頁面元件。
1. 針對頁面元件的 `basic` 區段建立覆寫 (使用由 [Sling 資源合併](/help/sites-developing/sling-resource-merger.md)所提供的&#x200B;*對話框差異*)；例如：

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >如需參考，請參閱：
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   >
   不過，您 ***必須*** 不會變更中的任何專案 `/libs` 路徑。
   >
   這是因為 `/libs` 下次升級執行個體時會被覆寫（當您套用hotfix或feature pack時，很可能會被覆寫）。
   >
   設定和其他變更的建議方法是：
   >
   1. 重新建立所需專案（即存在於中的專案） `/libs`)下 `/apps`
   1. 進行任何變更 `/apps`

1. 在 `basic` 上設定 `path` 屬性，以指向基本索引標籤的覆寫 (另請參閱下一個步驟)。例如：

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. 在相對應的路徑建立 `basic` - `moretitles` 區段的覆寫；例如：

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. 套用適當的節點屬性：

   * **名稱**：`cq:showOnCreate`
   * **類型**：`Boolean`
   * **值**：`false`

   「**更多標題和說明**」區段即不會再顯示在「**建立頁面**」精靈中。

>[!NOTE]
>
設定要與即時副本一起使用的頁面屬性時，請參閱 [在頁面屬性上設定MSM鎖定](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) 以取得更多詳細資料。

## 頁面屬性的設定範例 {#sample-configuration-of-page-properties}

這個範例示範對話方塊的diff技巧。 [Sling資源合併](/help/sites-developing/sling-resource-merger.md)；包括使用 [`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties). 還會說明 `cq:showOnCreate` 和 `cq:hideOnEdit` 兩者的使用。

GITHUB上的程式碼

您可以在GitHub上找到此頁面的程式碼

* [在GitHub上開啟aem-authoring-extension-page-dialog專案](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
