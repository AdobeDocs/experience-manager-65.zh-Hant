---
title: 模型概述
description: 瞭解如何使用模型管理，其中包含建立和管理用於與最終資料物件建立關聯的模型。
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 50785534-5784-4354-b123-5e640b7c0242
source-git-commit: 06a6d4e0ba2aeaefcfb238233dd98e8bbd6731da
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 0%

---

# 模型概述{#models-overview}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案，使用SPA編輯器。 [深入了解](/help/sites-developing/spa-overview.md)。

模型管理涉及建立和管理與最終資料物件相關聯的模型。 每個模型都包含建立及演算物件所需的所有屬性和欄位定義。

模型管理涉及建立 **模型**， **實體**、和 **空間**. 下圖說明AEM內容與模型之間的關係。

![chlimage_1-81](assets/chlimage_1-81.png)

## 內容模型 {#the-content-model}

模型可描述內容型別，並代表原生應用程式可使用哪些資訊。 這是構成內容之部分的說明。 內容模型是用來建立內容片段的規則。 內容模型包含哪些資料可用、可使用哪些資產、資產與資料之間的關係、與其他內容模型的關係，以及可用的中繼資料。

模型也可作為將現有AEM內容轉換為可讓原生行動應用程式輕鬆使用的物件的方式。

Content Services為資產、資產集合、HTML頁面、應用程式設定和頻道獨立頁面等常見物件提供一些現成的模型。 這些是可設定的，因此可滿足特定客戶需求而無需AEM開發工作。

使用者可以建立自己的模型。 如此可讓您建立尚未由AEM管理的新內容型別。 模型建立是透過UI使用現有基本型別完成的。

下圖說明AEM Mobile應用程式的內容模型，以及如何將實體、資料夾和空間指派給應用程式。

![chlimage_1-82](assets/chlimage_1-82.png)

### 模型 {#the-models}

模型可用來決定如何建立圖元。 它們定義實體中可用的內容以及從AEM內容產生資料的方式。 開始使用「空間」、「資料夾」和「圖元」之前，您應該熟悉模型的建立和管理。

>[!NOTE]
>
>模型存在於應用程式之外，因為有多個應用程式可以使用它。
>

若要在控制面板和存放庫中建立和管理模型，請參閱 **[模型](/help/mobile/administer-mobile-apps.md)**.

### 內容模型中的實體 {#entities-in-content-model}

實體是內容模型的例項。 實體會透過Content Services API公開至使用者端資源庫，並提供原生應用程式可獨立存取內容的方式。

如果存在現有的AEM內容，則會使用模型和AEM內容來源產生實體。 例如，頁面實體是從AEM頁面和頁面模型產生的獨立於色版和版面配置的物件。

實體參考內容的變更會導致實體的變更。 例如，如果 *cq：page* 會更新，然後也會更新基於該頁面的任何實體。

若要從模型建立自訂圖元，請參閱 **[使用實體](/help/mobile/spaces-and-entities.md)**.

>[!NOTE]
>
>如果模型未對應至現有AEM內容，例如客戶已建立模型，則有UI讓客戶可建立實體。
>

### 內容模型中的空間 {#spaces-in-content-model}

空間可用來組織實體以方便存取。 空間可以包含一或多個實體型別，也可以包含子資料夾。

在AEM端，空間是管理相關實體的便利方式。 它也可用於指派授權許可權。 可以對空間進行授權，以保護該空間中的實體。

*例如*，

使用者有三個一般實體分類。 一個僅供內部使用，另一個已核准供公眾使用，還有第三個是用於許多應用程式使用的通用實體。 為了方便管理，使用者會建立三個空間，即 *內部*， *公共* （包含英文和法文內容），以及 *一般* 管理適當的實體，如下所示：

* /content/entities/internal
* /content/entities/public/en
* /content/entities/public/fr
* /content/entities/common

系統會提供服務端點給空間，讓原生使用者端程式庫可以要求空間內容的清單。 此「清單」會以JSON物件傳回。

另請參閱 **[空間與實體](/help/mobile/spaces-and-entities.md)** 建立和發佈空間。

>[!NOTE]
>
>一個空間可供許多應用程式使用，而一個應用程式可使用許多空間。

### 內容模型中的資料夾 {#folders-in-content-model}

資料夾可讓使用者依需求組織實體，並有助於更精細的ACL控制。 空間可以包含資料夾，以協助進一步組織空間的內容和資產。 使用者可以在空間下建立自己的階層。

若要建立和管理空間內的資料夾，請參閱 **[使用空間中的資料夾](/help/mobile/spaces-and-entities.md)**.
