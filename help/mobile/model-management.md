---
title: 模型概觀
seo-title: 模型概觀
description: 'null'
seo-description: 'null'
uuid: e09dac52-9515-43f7-9d3b-6637e2283d59
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: c8281f98-9811-42f7-9a31-f82dd0f09319
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 模型概觀{#models-overview}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

模型管理包括建立和管理模型，以便與最終的資料物件建立關聯。 每個模型將包含所需的所有屬性和欄位定義，以便於建立和渲染對象。

「模型管理」涉及 **建立模**&#x200B;型 **、**&#x200B;圖元 ****&#x200B;和空格。 下圖說明AEM內容與模型之間的關係。

![chlimage_1-81](assets/chlimage_1-81.png)

## 內容模型 {#the-content-model}

模型會描述內容類型，並指出原生應用程式可使用的資訊。 它是內容組成部分的說明。 內容模型是如何建立內容的規則。 內容模型包含哪些資料可用、哪些資產可使用、資產與資料之間的關係、與其他內容模型的關係，以及可用的中繼資料。

模型也是將現有AEM內容轉換為原生行動應用程式可輕鬆使用的物件的方式。

Content services將針對常見物件提供一些現成可用的模型，例如資產、資產集合、HTML頁面、應用程式設定和不受通道影響的頁面。 這些設定可進行設定，以符合特定客戶需求，而不需要AEM開發工作。

使用者可建立自己的模型。 如此可建立尚未由AEM管理的新內容類型。 模型建立是透過使用現有基本類型的UI來完成。

下圖說明AEM Mobile應用程式的內容模型，以及如何將實體、檔案夾和空格指派給應用程式。

![chlimage_1-82](assets/chlimage_1-82.png)

### 模型 {#the-models}

模型用於確定圖元的建立方式。 它們會定義實體中可用的項目，以及該資料從AEM內容產生的方式。 在開始使用「空格」(Spaces)、「資料夾」(Folders)和「實體」(Entitys)之前，您應熟悉建立和管理模型。

>[!NOTE]
>
>模型存在於應用程式外部，因為多個應用程式可以使用它。


請參 **[閱Models](/help/mobile/administer-mobile-apps.md)**，以在儀表板和儲存庫中建立和管理模型。

### 內容模型中的實體 {#entities-in-content-model}

實體是內容模型的例項。 實體會透過Content Services API公開至用戶端資料庫，並提供原生應用程式以不受頻道影響的方式存取內容的方式。

在現有AEM內容中，會使用模型和AEM內容來源產生實體。 例如，頁面實體是與頻道和版面無關的物件，會從AEM頁面和頁面模型產生。

變更實體的參考內容，將導致實體變更。 例如，如果更 *新了cq:page* ，則基於該頁面的任何實體也會更新。

請參 **[閱使用實體](/help/mobile/spaces-and-entities.md)**，從模型建立自定義實體。

>[!NOTE]
>
>如果模型未對應現有的AEM內容，例如客戶建立新模型，則會有UI，讓客戶可以建立新實體。


### 內容模型中的空格 {#spaces-in-content-model}

空間用於組織實體以方便訪問。 空間可以包含一個或多個實體類型，也可以包含子資料夾。

在AEM端，空格是管理相關實體的便利方式。 它也可用來指派授權權限。 可以對空間進行授權，然後該空間將保護該空間中的實體。

*例如*,

使用者有三種一般的實體分類。 一個僅供內部使用，另一個則獲准供公眾使用，而第三個則適用於許多應用程式所使用的一般實體。 為方便管理，使用者會建立三個空間 **: *internal* 、public *（同時包含英文和法文內容）和* common for management the appropriate entities，如下所述：

* /content/entities/internal
* /content/entities/public/tw
* /content/entitys/public/fr
* /content/entities/common

將向空間提供服務端點，以便本地客戶端庫可以請求空間內容清單。 此「清單」將傳回為JSON物件。

有關創 **[建和發佈空格](/help/mobile/spaces-and-entities.md)**，請參閱空格和實體。

>[!NOTE]
>
>空間可供許多應用程式使用，而應用程式可以使用許多空間。

### 內容模型中的資料夾 {#folders-in-content-model}

資料夾允許用戶根據需要組織實體，並有助於更精細的ACL控制。 空間可以包含資料夾，以幫助進一步組織空間的內容和資產。 用戶可以在空格下建立自己的層次。

請參 **[閱使用空間中的資料夾](/help/mobile/spaces-and-entities.md)**，以建立和管理空間中的資料夾。
