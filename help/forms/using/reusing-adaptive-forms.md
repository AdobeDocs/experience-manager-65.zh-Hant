---
title: 重複使用最適化表單
seo-title: Reusing adaptive forms
description: 您可以重複使用現有的最適化表單來建立新的最適化表單。
seo-description: You can reuse an existing adaptive form to create new adaptive forms.
uuid: f1d0fb70-e255-4dd9-8e6d-fd65eaf2e81a
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: ef564750-f107-41cb-887e-fc6d22b7d32e
feature: Adaptive Forms
exl-id: d8ee4e82-3137-430e-aa47-b00191f2729c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# 重複使用最適化表單 {#reusing-adaptive-forms}

## 簡介 {#introduction}

如果您想要使用現有適用性表單的某些屬性來產生新表單，您只需使用複製貼上功能即可。 此外，您可以將新的最適化表單貼到所需的資料夾路徑。 會複製所有中繼資料屬性，並複製XFA和XSD型適用性表單的XFA和XSD。

>[!NOTE]
>
>不會複製狀態和審閱詳細資訊。 例如，如果您的最適化表單已發佈，而您複製了該表單，則貼上的最適化表單會處於未發佈狀態。 同樣地，如果複製的資產正在審閱中，貼上的資產不在同一次審閱中。

### 複製最適化表單 {#copy-an-adaptive-form}

使用下列其中一種方法複製最適化表單：

1. 按一下複製 ![aem6forms_copy](assets/aem6forms_copy.png) 表徵圖。

   >[!NOTE]
   >
   >快速動作是滑鼠暫留時在縮圖上顯示的動作項目。

1. 選取最適化表單。 不同視圖的選擇過程不同。

   如果您處於卡片檢視中，請按一下選取項目，以前往選取模式 ![aem6forms_check-circle](assets/aem6forms_check-circle.png) 圖示，然後按一下您要複製的所有最適化表單。

   如果您處於清單檢視中，請按一下所有適用性表單的核取方塊以加以選取。

   >[!NOTE]
   >
   >所有選取的資產都必須是最適化表單，因為僅適用性表單支援複製貼上功能，且選取的所有資產都必須顯示在相同的資料夾中。

   選取資產後，按一下復本 ![aem6forms_copy](assets/aem6forms_copy.png) 工具列中顯示的圖示，以複製選取的最適化表單。

### 貼上最適化表單 {#paste-an-adaptive-form}

按一下複製動作會自動退出選取模式並進行貼上 ![aem6forms_paste](assets/aem6forms_paste.png) 表徵圖。 現在，前往所需的資料夾路徑，然後按一下貼上 ![aem6forms_paste](assets/aem6forms_paste.png) 圖示來貼上複製的最適化表單。

如果您貼入相同資料夾，或此目標資料夾中存在另一個節點名稱相同（與CRX儲存庫儲存）的檔案，則1會附加到尾碼(例如，myaf會變成myaf1，而如果myaf1存在於相同位置，myaf會變成myaf2。 所有其他屬性仍與原始最適化表單相同。

按一下貼上後 ![aem6forms_paste](assets/aem6forms_paste.png) 表徵圖，它將再次被隱藏。 一次您只能貼上一次。 若要再次建立相同資產的復本，請再次複製。

### 變更新最適化表單的內容 {#change-contents-of-new-adaptive-form}

您可以使用下列方法來變更貼上的最適化表單的內容，使其與複製的表單不同：

1. **更改元資料屬性：**

   您可以變更最適化表單的中繼資料屬性，例如標題和說明。 如需中繼資料屬性的詳細資訊，以及如何變更，請參閱 [管理表單中繼資料](/help/forms/using/manage-form-metadata.md)

1. **針對XFA/XSD型適用性Forms變更XFA/XSD:**

   您可以變更適用性表單中使用的XFA/XSD。 若要了解如何變更這些最適化表單，請參閱 [管理表單中繼資料](/help/forms/using/manage-form-metadata.md)

1. **重新發佈:**

   貼上的資產與複製的資產不同。 您可以將其發佈為新資產，以供使用者使用。 若要了解如何發佈資產，請參閱 [發佈和取消發佈表單](/help/forms/using/publishing-unpublishing-forms.md)
