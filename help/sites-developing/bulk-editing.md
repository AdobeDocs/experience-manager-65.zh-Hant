---
title: 配置頁面以批量編輯頁面屬性
seo-title: Configuring your Page for Bulk Editing of Page Properties
description: 批量編輯頁面屬性允許您一次編輯多個頁面的屬性
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

# 配置頁面以批量編輯頁面屬性 {#configuring-your-page-for-bulk-editing-of-page-properties}

[頁面屬性的批量編輯](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages) 允許您一次編輯多頁的屬性。

由於可能有不同的值，因此不會將頁面屬性作為預設值啟用以進行批量編輯。 必須明確允許（啟用）。 在定義可用於批量編輯的頁面屬性時，您需要考慮某些含義，例如：

* 某些欄位通常是唯一的；例如頁面標題。 您必須確定何時應用一個值來啟用此類欄位以進行批量編輯是否有意義。
* 某些欄位可能具有多個值 — 這在呈現時需要有意義的表示。

   例如，一個複選框，指示「準備發佈」。 在批量編輯之前，這可能有幾個值（如就緒、正在審閱、正在進行）。

>[!CAUTION]
>
>頁面屬性的批量編輯為：
>
>* 在傳統UI中不可用。
>* 不可用於即時副本中的頁面。
>* 僅適用於具有相同資源類型的頁。
>


>[!NOTE]
>
>批量編輯也可用於「資產」。 它非常相似，但有幾點不同。 請參閱 [編輯多個資產的屬性](/help/assets/metadata.md) 的雙曲餘切值。 可以使用 [架構編輯器](/help/assets/metadata-schemas.md)。

## 啟用欄位 {#enabling-a-field}

>[!NOTE]
>
>某些欄位可能具有多個值 — 這在呈現時需要有意義的表示。 因此，您只應啟用以下欄位類型：
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`
>


在頁面元件上啟用欄位(*不* ):

1. 使用CRXDE Lite（或等效方法）開啟頁面元件。

   例如：`/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >此示例假定實例上已安裝核心元件，如果實例與We.Retail示例內容一起運行，則此情況是這樣的。 查看 [核心元件文檔](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 的子菜單。

1. 導航到 `cq:dialog` 定義。
1. 在欄位節點上定義以下屬性：

   * **名稱**: `allowBulkEdit`
   * **類型**: `Boolean`
   * **值**: `true`

   例如，對於標準頁 [基礎構件](/help/sites-authoring/default-components-foundation.md):

   `/libs/foundation/components/page`

   該屬性將定義於：

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >你 ***必須*** 沒有改變 `/libs` 路徑。
   >
   >這是因為 `/libs` 在下次升級實例時被覆蓋（在應用修補程式或功能包時很可能被覆蓋）。
   >
   >建議的配置和其他更改方法是：
   >
   >    1. 重新建立所需項(如 `/libs`) `/apps`
   >    1. 在 `/apps`


1. 選擇 **全部保存** 來保留更新。
