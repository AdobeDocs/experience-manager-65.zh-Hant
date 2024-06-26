---
title: 設定頁面以大量編輯頁面屬性
description: 大量編輯頁面屬性可讓您一次編輯多個頁面的屬性
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 1787e643-fc8e-40e0-8e14-97b222a7c320
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Developer
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 21%

---

# 設定頁面以大量編輯頁面屬性 {#configuring-your-page-for-bulk-editing-of-page-properties}

[頁面屬性的批次編輯](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages)可讓您同時編輯多個頁面的屬性。

由於可能有不同的值，頁面屬性不會預設為啟用大量編輯功能。 必須明確允許（啟用）。 定義可進行大量編輯的頁面屬性時，您需要考慮特定意涵，例如：

* 某些欄位通常是唯一的；例如，頁面標題。 決定啟用這些欄位進行大量編輯是否有意義（何時將套用一個值）。
* 某些欄位可能有多個值 — 這在轉譯時需要有意義的表示。

  例如，顯示「準備發佈」的核取方塊。 在大量編輯之前，這可能會有數個值（例如，就緒、稽核中、進行中）。

>[!CAUTION]
>
>頁面屬性的大量編輯有以下特性：
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
   >此範例假設核心元件已安裝在例項上，若例項搭配We.Retail範例內容執行即是如此。 請參閱 [核心元件檔案](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hant) 以取得詳細資訊。

1. 導覽至 `cq:dialog` 定義內的所需欄位。
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
   >    1. 重新建立所需專案（即存在於中的專案） `/libs`)下 `/apps`
   >    1. 進行任何變更 `/apps`

1. 選取「**儲存全部**」即可保留您的更新。
