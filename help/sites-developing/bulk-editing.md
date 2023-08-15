---
title: 設定頁面以大量編輯頁面屬性
seo-title: Configuring your Page for Bulk Editing of Page Properties
description: 大量編輯頁面屬性可讓您一次編輯多個頁面的屬性
seo-description: Bulk editing of page properties lets you edit the properties of multiple pages at once
uuid: 1ad403d2-4b93-4943-ae45-74bf20705b81
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: fe61ee4b-51b6-4a6f-91d8-1c02b29cc1db
exl-id: 1787e643-fc8e-40e0-8e14-97b222a7c320
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 23%

---

# 設定頁面以大量編輯頁面屬性 {#configuring-your-page-for-bulk-editing-of-page-properties}

[大量編輯頁面屬性](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages) 可讓您一次編輯多個頁面的屬性。

由於可能有不同的值，頁面屬性不會預設為啟用大量編輯功能。 必須明確允許（啟用）。 定義可進行批次編輯的頁面屬性時，您需要考慮特定意涵，例如：

* 某些欄位通常是唯一的；例如頁面標題。 套用一個值時，您必須決定啟用這類欄位進行批次編輯是否有意義。
* 某些欄位可能有多個值 — 這在轉譯時需要有意義的表示。

  例如，顯示「準備發佈」的核取方塊。 在大量編輯之前，這可能會有數個值（例如，就緒、稽核中、進行中）。

>[!CAUTION]
>
>頁面屬性的批次編輯有以下特性：
>
>* 傳統UI中不提供。
>* 不適用於 Live Copy 內的頁面。
>* 僅適用於具有相同資源類型的頁面。
>

>[!NOTE]
>
>大量編輯也適用於Assets。 兩者非常類似，但僅有少數幾個差異點。 另請參閱 [編輯多個資產的屬性](/help/assets/metadata.md) 以取得完整資訊。 您可以使用來自訂資產的大量中繼資料編輯器中的欄位 [結構描述編輯器](/help/assets/metadata-schemas.md).

## 啟用欄位 {#enabling-a-field}

>[!NOTE]
>
>某些欄位可能有多個值 — 這在轉譯時需要有意義的表示。 因此，您應該只啟用下列欄位型別：
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`
>

在頁面元件上啟用欄位(*非* （在範本上）：

1. 使用CRXDE Lite（或同等方法）開啟頁面元件。

   例如：`/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >此範例假設核心元件已安裝在例項上，若例項搭配We.Retail範例內容執行即是如此。 請參閱 [核心元件檔案](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 以取得詳細資訊。

1. 瀏覽至 `cq:dialog` 定義內的所需欄位。
1. 在欄位節點上定義以下屬性：

   * **名稱**：`allowBulkEdit`
   * **類型**：`Boolean`
   * **值**：`true`

   例如，對於標準頁面 [基礎元件](/help/sites-authoring/default-components-foundation.md)：

   `/libs/foundation/components/page`

   屬性將會定義於：

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >您 ***必須*** 不會變更中的任何專案 `/libs` 路徑。
   >
   >這是因為 `/libs` 下次升級執行個體時會被覆寫（當您套用hotfix或feature pack時，很可能會被覆寫）。
   >
   >設定和其他變更的建議方法是：
   >
   >    1. 重新建立所需專案（即該專案存在於中） `/libs`)下 `/apps`
   >    1. 進行任何變更 `/apps`

1. 選取「**儲存全部**」即可保留您的更新。
