---
title: 重複使用最適化表單
seo-title: 重複使用最適化表單
description: 您可以重複使用現有的最適化表單來建立新的最適化表單。
seo-description: 您可以重複使用現有的最適化表單來建立新的最適化表單。
uuid: f1d0fb70-e255-4dd9-8e6d-fd65eaf2e81a
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: ef564750-f107-41cb-887e-fc6d22b7d32e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 重複使用最適化表單 {#reusing-adaptive-forms}

## 簡介 {#introduction}

如果您想要使用現有最適化表單的某些屬性來產生新的屬性，您只需使用複製貼上功能即可。 此外，您也可以將新的最適化表單貼至所需的資料夾路徑。 複製所有中繼資料屬性，並複製XFA和XSD自適應表單的XFA和XSD。

>[!NOTE]
>
>不複製狀態和複查詳細資訊。 例如，如果您的最適化表單已發佈，而您複製了它，則貼上的最適化表單會處於未發佈狀態。 同樣地，如果複製的資產正在複核中，則貼上的資產不在相同的複核中。

### 複製最適化表單 {#copy-an-adaptive-form}

使用下列任一方法複製最適化表單：

1. 按一下「 ![從快速動作複製aem6forms_copy](assets/aem6forms_copy.png) 」圖示。

   >[!NOTE]
   >
   >快速動作是滑鼠暫留時，會在縮圖上顯示的動作項目。

1. 選擇最適化表單。 不同檢視的選取程式不同。

   如果您在卡片檢視中，請按一下選取範圍 ![aem6forms_check-circle](assets/aem6forms_check-circle.png) 圖示以進入選取模式，然後按一下您要複製的所有最適化表單。

   如果您位於清單檢視中，請按一下所有最適化表單的核取方塊以選取它們。

   >[!NOTE]
   >
   >所有選取的資產都必須是最適化表單，因為複製貼上功能僅支援最適化表單，而選取的所有資產都必須位於相同的資料夾中。

   選取資產後，按一下工具列 ![中顯示的複製aem6forms_copy](assets/aem6forms_copy.png) 圖示，以複製選取的最適化表單。

### 貼上最適化表單 {#paste-an-adaptive-form}

按一下複製動作會自動退出選取模式，並讓貼上 ![aem6forms_paste圖示可見](assets/aem6forms_paste.png) 。 現在，請移至所要的檔案夾路徑，然後按一 ![下「貼上aem6forms_paste](assets/aem6forms_paste.png) 」圖示，以貼上複製的最適化表單。

如果您貼上到同一資料夾中，或者此目標資料夾中存在另一個節點名稱相同（與其儲存在CRX儲存庫中）的檔案，則會將1附加到尾碼(例如，myaf變為myaf1，如果myaf1存在於同一位置，則myaf將變為myaf2。 所有其他屬性都與原始最適化表單相同。

按一下「貼上 ![aem6forms_paste」圖示後](assets/aem6forms_paste.png) ，它將再次變成隱藏。 一次只能貼上一次。 若要再次建立相同資產的復本，請再次複製。

### 變更新調適性表單的內容 {#change-contents-of-new-adaptive-form}

您可以使用下列方法變更貼上的最適化表單內容，以使其與複製的表單不同：

1. **變更中繼資料屬性：**

   您可以變更最適化表單的中繼資料屬性，例如標題和說明。 如需中繼資料屬性的詳細資訊以及如何變更這些屬性，請參閱管理 [表單中繼資料](/help/forms/using/manage-form-metadata.md)

1. **針對XFA/XSD架構的最適化表單變更XFA/XSD:**

   您可以變更最適化表單中使用的XFA/XSD。 若要瞭解如何變更這些可調式表單，請參閱管 [理表單中繼資料](/help/forms/using/manage-form-metadata.md)

1. **重新發佈:**

   貼上的資產與複製的資產不同。 您可以將它發佈為新資產，讓使用者可使用。 若要瞭解如何發佈資產，請參閱發佈 [和取消發佈表單](/help/forms/using/publishing-unpublishing-forms.md)

