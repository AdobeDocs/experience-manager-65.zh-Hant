---
title: 設定頁面以大量編輯頁面屬性
seo-title: 設定頁面以大量編輯頁面屬性
description: 大量編輯頁面屬性可讓您一次編輯多個頁面的屬性
seo-description: 大量編輯頁面屬性可讓您一次編輯多個頁面的屬性
uuid: 1ad403d2-4b93-4943-ae45-74bf20705b81
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: fe61ee4b-51b6-4a6f-91d8-1c02b29cc1db
translation-type: tm+mt
source-git-commit: b08149e00c418319ebacec71c56472ad4e8e1089
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 1%

---


# 配置頁面以批量編輯頁面屬性{#configuring-your-page-for-bulk-editing-of-page-properties}

[大量編輯頁](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages) 面屬性可讓您一次編輯多頁的屬性。

由於可能有不同的值，因此頁面屬性不會依預設啟用大量編輯。 必須明確允許（啟用）。 當定義頁面屬性以供批量編輯時，您需要考慮某些含義，例如：

* 某些欄位通常是唯一的；例如頁面標題。 您必須決定在套用一個值時，啟用這些欄位以進行大量編輯是否有意義。
* 某些欄位可能有多個值——這在轉譯時需要有意義的表示法。

   例如，一個核取方塊指出「已準備好進行出版」。 在批量編輯之前，這可能會有數個值（例如，就緒、正在審閱、進行中）。

>[!CAUTION]
>
>頁面屬性的大量編輯是：
>
>* 傳統UI中不提供。
>* 不適用於即時副本中的頁面。
>* 僅適用於具有相同資源類型的頁。

>



>[!NOTE]
>
>Assets也提供大量編輯功能。 很相似，但有幾點不同。 如需完整資訊，請參閱[編輯多個資產的屬性](/help/assets/metadata.md)。 您可以使用[架構編輯器](/help/assets/metadata-schemas.md)自訂資產批量中繼資料編輯器中的欄位。

## 啟用欄位{#enabling-a-field}

>[!NOTE]
>
>某些欄位可能有多個值——這在轉譯時需要有意義的表示法。 因此，您僅應啟用下列欄位類型：
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`

>



頁面元件（範本上的&#x200B;*not*）上會啟用欄位：

1. 使用CRXDE Lite（或相當的方法）開啟您的頁面元件。

   例如：`/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >此範例假設已在執行個體上安裝核心元件，而執行個體與We.Retail範例內容一起執行時，即為此情況。 如需詳細資訊，請參閱[核心元件檔案](https://docs.adobe.com/content/help/zh-Hant/experience-manager-core-components/using/introduction.html)。

1. 導覽至`cq:dialog`定義內的必填欄位。
1. 在欄位節點上定義以下屬性：

   * **名稱**:  `allowBulkEdit`
   * **類型**:  `Boolean`
   * **值**:  `true`

   例如，對於標準頁[foundation元件](/help/sites-authoring/default-components-foundation.md):

   `/libs/foundation/components/page`

   該屬性將定義在：

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >您&#x200B;***必須***&#x200B;不要變更`/libs`路徑中的任何項目。
   >
   >這是因為下次升級實例時會覆寫`/libs`的內容（套用修補程式或功能套件時，很可能會覆寫）。
   >
   >配置和其他更改的建議方法為：
   >
   >    1. 在`/apps`下重新建立所需項目（如`/libs`中所存在）
   >    1. 在`/apps`中進行任何更改


1. 選擇&#x200B;**全部保存**&#x200B;以保存更新。

