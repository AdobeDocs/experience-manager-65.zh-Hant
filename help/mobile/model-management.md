---
title: 模型概述
seo-title: Models Overview
description: 模型概述
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

# 模型概述{#models-overview}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

模型管理涉及建立和管理模型，以便與最終資料對象關聯。 每個模型都將包括為便於建立和呈現對象而需要的所有屬性和欄位定義。

模型管理涉及建立 **模型**。 **實體**, **空間**。 下圖說明了「內容」與AEM模型之間的關係。

![chlimage_1-81](assets/chlimage_1-81.png)

## 內容模型 {#the-content-model}

模型描述內容類型，並表示可用於本機應用程式的資訊。 它是內容組成的描述。 內容模型是構建內容的規則。 內容模型包括哪些資料可用、哪些資產可以使用、資產和資料之間的關係、與其他內容模型的關係以及可用元資料。

模型還用作將現有內容轉換AEM為可供本地移動應用輕鬆使用的對象的方法。

Content Services將為常見對象(如資產、資產收集、HTML頁、應用程式配置和渠道獨立頁面)提供一些現成模型。 這些功能可配置，因此無需開發工作即可滿足特定客AEM戶需求。

用戶可以建立自己的模型。 這允許建立尚未由管理的新內容類AEM型。 通過UI使用現有基元類型建立模型。

下圖說明了AEM Mobile應用的內容模型，以及如何將實體、資料夾和空格分配給應用。

![chlimage_1-82](assets/chlimage_1-82.png)

### 《模型》 {#the-models}

模型用於確定如何建立圖元。 它們定義實體中可用的內容，以及從內容生成資料的AEM方式。 在開始使用「空間」、「資料夾」和「實體」之前，應熟悉建立和管理模型。

>[!NOTE]
>
>一個模型存在於應用程式之外，因為多個應用程式可以使用它。

請參閱 **[模型](/help/mobile/administer-mobile-apps.md)** 建立和管理儀表板和儲存庫中的模型。

### 內容模型中的實體 {#entities-in-content-model}

實體是內容模型的實例。 實體通過Content Services API暴露到客戶端庫，並為本地應用提供以獨立於渠道的方式訪問內容的方式。

在現有內容的AEM情況下，使用模型和內容源生AEM成實體。 例如，頁面實體是從頁面和頁面模型生成的與通道和佈局AEM無關的對象。

對實體的引用內容所做的更改將導致對實體所做的更改。 例如，如果 *cq：頁* 更新，則基於該頁的所有實體也將更新。

請參閱 **[使用實體](/help/mobile/spaces-and-entities.md)** 從模型建立自定義圖元。

>[!NOTE]
>
>如果模型與現有內容不AEM對應，例如客戶建立了新模型，則會有一個UI，以便客戶可以建立新實體。

### 內容模型中的空格 {#spaces-in-content-model}

空間用於組織實體以便於訪問。 空間可包含一個或多個實體類型，並可包含子資料夾。

在一AEM側，空間是管理相關實體的方便方法。 它還可用於分配授權權限。 可以對空間進行授權，然後該空間將保護該空間中的實體。

*例如*。

用戶對實體有三種一般分類。 一個僅供內部使用，另一個只供公共使用，而第三個只供許多應用使用的公共實體使用。 為便於管理，用戶建立三個空間，即 *內部*。 *公共* （包含英語和法語內容） *共* 管理下列適當實體：

* /content/entities/internal
* /content/entities/public/en
* /content/entities/public/fr
* /content/entities/common

將向空間提供服務端點，以便本地客戶端庫可以請求空間內容的清單。 此「清單」將作為JSON對象返回。

請參閱 **[空格和圖元](/help/mobile/spaces-and-entities.md)** 建立和發佈空間。

>[!NOTE]
>
>一個空間可以被許多應用使用，一個應用可以使用多個空間。

### 內容模型中的資料夾 {#folders-in-content-model}

資料夾允許用戶根據需要組織實體，並有助於更好的ACL控制。 共用空間可以包含資料夾，以幫助進一步組織空間的內容和資產。 用戶可以在空間下建立自己的層次結構。

請參閱 **[在空間中使用資料夾](/help/mobile/spaces-and-entities.md)** 建立和管理空間中的資料夾。
