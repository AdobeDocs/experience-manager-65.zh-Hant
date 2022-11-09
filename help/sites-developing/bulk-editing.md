---
title: 設定頁面以大量編輯頁面屬性
seo-title: Configuring your Page for Bulk Editing of Page Properties
description: 大量編輯頁面屬性可讓您一次編輯多個頁面的屬性
seo-description: Bulk editing of page properties allows you to edit the properties of multiple pages at once
uuid: 1ad403d2-4b93-4943-ae45-74bf20705b81
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: fe61ee4b-51b6-4a6f-91d8-1c02b29cc1db
exl-id: 1787e643-fc8e-40e0-8e14-97b222a7c320
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 2%

---

# 設定頁面以大量編輯頁面屬性 {#configuring-your-page-for-bulk-editing-of-page-properties}

[大量編輯頁面屬性](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages) 可讓您一次編輯多個頁面的屬性。

由於可能有不同的值，預設不會啟用頁面屬性進行大量編輯。 必須明確允許（啟用）。 定義可用於大量編輯的頁面屬性時，您需要考慮某些含意，例如：

* 某些欄位通常是唯一的；例如頁面標題。 您必須決定在要套用某個值時，啟用這類欄位以進行大量編輯是否有意義。
* 某些欄位可能有多個值，這在呈現時需要有意義的表示。

   例如，表示「已準備好發佈」的核取方塊。 大量編輯前，這可能有數個值（例如就緒、正在審核、正在進行中）。

>[!CAUTION]
>
>大量編輯頁面屬性為：
>
>* 傳統UI中無法使用。
>* 不適用於即時副本中的頁面。
>* 僅適用於資源類型相同的頁面。
>


>[!NOTE]
>
>資產也可進行大量編輯。 這非常相似，但有幾點不同。 請參閱 [編輯多個資產的屬性](/help/assets/metadata.md) 以取得完整資訊。 您可以使用 [結構編輯器](/help/assets/metadata-schemas.md).

## 啟用欄位 {#enabling-a-field}

>[!NOTE]
>
>某些欄位可能有多個值，這在呈現時需要有意義的表示。 因此，您只應啟用下列欄位類型：
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`
>


頁面元件上會啟用欄位(*not* 在範本上):

1. 使用CRXDE Lite（或相同的方法）開啟您的頁面元件。

   例如：`/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >此範例假設已在執行個體上安裝核心元件，如果執行個體執行We.Retail範例內容，即為此情況。 請參閱 [核心元件檔案](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 以取得更多資訊。

1. 導覽至 `cq:dialog` 定義。
1. 在欄位節點上定義下列屬性：

   * **名稱**: `allowBulkEdit`
   * **類型**: `Boolean`
   * **值**: `true`

   例如，對於標準頁面 [基礎元件](/help/sites-authoring/default-components-foundation.md):

   `/libs/foundation/components/page`

   該屬性將定義在：

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >您 ***必須*** 不會變更 `/libs` 路徑。
   >
   >這是因為 `/libs` 下次升級執行個體時即會覆寫（而當您套用Hotfix或Feature Pack時，很可能會覆寫）。
   >
   >設定和其他變更的建議方法為：
   >
   >    1. 重新建立所需項目(亦即， `/libs`)底下 `/apps`
   >    1. 在內進行任何變更 `/apps`


1. 選擇 **全部儲存** 以保留更新。
