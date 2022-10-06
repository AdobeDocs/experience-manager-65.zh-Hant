---
title: 模型概觀
seo-title: Models Overview
description: 模型概觀
seo-description: null
uuid: e09dac52-9515-43f7-9d3b-6637e2283d59
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: c8281f98-9811-42f7-9a31-f82dd0f09319
exl-id: 50785534-5784-4354-b123-5e640b7c0242
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# 模型概觀{#models-overview}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

模型管理包括建立和管理模型，以便與最終資料對象建立關聯。 每個模型都包含建立和呈現對象所需的所有屬性和欄位定義。

模型管理涉及建立 **模型**, **實體**，和 **空格**. 下圖說明AEM內容與模型之間的關係。

![chlimage_1-81](assets/chlimage_1-81.png)

## 內容模型 {#the-content-model}

模型描述了內容類型，並表示哪些資訊將可供本機應用程式使用。 這是內容組成部分的說明。 內容模型是如何建立內容片段的規則。 內容模型包含可用的資料、可使用的資產、資產與資料的關係、與其他內容模型的關係，以及可用的中繼資料。

模型也可將現有AEM內容轉換為物件，供原生行動應用程式輕鬆使用。

內容服務將針對常見物件(例如資產、資產集合、HTML頁面、應用程式設定和管道獨立頁面)提供一些現成可用的模型。 這些檔案可設定，以便符合特定客戶需求，而不需要進行AEM開發工作。

使用者可以建立自己的模型。 這可以建立尚未由AEM管理的新內容類型。 建立模型是使用現有基元類型通過UI完成的。

下圖說明AEM Mobile應用程式的內容模型，以及如何將實體、資料夾和空格指派給應用程式。

![chlimage_1-82](assets/chlimage_1-82.png)

### 模型 {#the-models}

模型用於確定圖元的建立方式。 它們會定義實體中可用的項目，以及該資料從AEM內容產生的方式。 開始使用空間、資料夾和實體之前，應先熟悉建立和管理模型。

>[!NOTE]
>
>模型存在於應用程式外部，因為多個應用程式可使用它。

請參閱 **[模型](/help/mobile/administer-mobile-apps.md)** 在控制面板和儲存庫中建立和管理模型。

### 內容模型中的實體 {#entities-in-content-model}

實體是內容模型的例項。 實體會透過內容服務API公開至用戶端資料庫，並提供原生應用程式以不受通道影響的方式存取內容。

若是現有AEM內容，則使用模型和AEM內容來源產生實體。 例如，頁面實體是從AEM頁面和頁面模型產生的與管道和版面無關的物件。

對實體的參考內容進行變更，將導致實體變更。 例如，若 *cq:page* 會更新，則也會更新以該頁面為基礎的任何實體。

請參閱 **[使用實體](/help/mobile/spaces-and-entities.md)** 從模型建立自定義圖元。

>[!NOTE]
>
>如果模型與現有AEM內容不對應，例如客戶建立了新模型，則會有UI，讓客戶可以建立新實體。

### 內容模型中的空格 {#spaces-in-content-model}

空間用於組織實體以方便訪問。 空間可以包含一個或多個實體類型，也可以包含子資料夾。

在AEM端，空間是管理相關實體的便利方式。 它也可用來指派授權權限。 可對空間進行授權，然後空間將保護該空間中的實體。

*例如*,

使用者有三種一般的實體分類。 一個僅供內部使用，另一個僅供公共使用，而第三個僅供許多應用程式使用的通用實體使用。 為了便於管理，用戶建立了三個空間，即 *內部*, *公共* （包含英文和法文內容）和 *公用* 管理下列適當實體：

* /content/entities/internal
* /content/entities/public/en
* /content/entities/public/fr
* /content/entities/common

服務終點將被提供給空間，以便本地客戶端庫可以請求空間內容的清單。 此「清單」將以JSON物件傳回。

請參閱 **[空間和實體](/help/mobile/spaces-and-entities.md)** 來建立和發佈空間。

>[!NOTE]
>
>空間可供許多應用使用，而應用程式可使用多個空間。

### 內容模型中的資料夾 {#folders-in-content-model}

資料夾可讓使用者視需要組織實體，並有助於更精細的ACL控制。 空間可以包含資料夾，以幫助進一步組織空間的內容和資產。 使用者可在空格下建立自己的階層。

請參閱 **[在空間中使用資料夾](/help/mobile/spaces-and-entities.md)** 在空間中建立和管理資料夾。
