---
title: 重用自適應表單
seo-title: Reusing adaptive forms
description: 可以重用現有自適應表單來建立新的自適應表單。
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

# 重用自適應表單 {#reusing-adaptive-forms}

## 簡介 {#introduction}

如果要使用現有自適應表單的某些屬性來生成新表單，則只需使用複製貼上功能即可。 此外，還可以在所需資料夾路徑上貼上新的自適應表單。 複製所有元資料屬性，並複製基於XFA和XSD的自適應表單的XFA和XSD。

>[!NOTE]
>
>不複製狀態和審閱詳細資訊。 例如，如果發佈了自適應表單，然後複製了該表單，則貼上的自適應表單處於未發佈狀態。 同樣，如果正在複查複製的資產，則貼上的資產不在同一審閱下。

### 複製自適應窗體 {#copy-an-adaptive-form}

使用以下任一方法複製自適應表單：

1. 按一下「複製」 ![aem6forms_copy](assets/aem6forms_copy.png) 表徵圖。

   >[!NOTE]
   >
   >快速操作是滑鼠懸停時在縮略圖上顯示的操作項。

1. 選擇自適應窗體。 不同視圖的選擇過程不同。

   如果處於卡視圖中，請通過按一下選擇進入選擇模式 ![aem6forms_check circle](assets/aem6forms_check-circle.png) 表徵圖，然後按一下要複製的所有自適應表單。

   如果處於清單視圖中，請按一下所有自適應表單的複選框以選擇它們。

   >[!NOTE]
   >
   >所有選定的資產都必須是自適應表單，因為只支援自適應表單的複製貼上功能，並且所有選定的資產必須位於同一資料夾中。

   選擇資產後，按一下副本 ![aem6forms_copy](assets/aem6forms_copy.png) 表徵圖，以複製選定的自適應窗體。

### 貼上自適應表單 {#paste-an-adaptive-form}

按一下複製操作會自動退出選擇模式並進行貼上 ![aem6forms_paste](assets/aem6forms_paste.png) 表徵圖。 現在轉到所需的資料夾路徑，然後按一下貼上 ![aem6forms_paste](assets/aem6forms_paste.png) 表徵圖以貼上複製的自適應窗體。

如果貼上到同一資料夾或具有相同節點名稱（與其一起儲存在CRX儲存庫中）的其他檔案存在於此目標資料夾中，則1會附加到尾碼(例如，myaf變為myaf1，如果myaf1位於同一位置，則myaf變為myaf2。 所有其它屬性都與原始自適應表單相同。

按一下貼上後 ![aem6forms_paste](assets/aem6forms_paste.png) 表徵圖，它將再次隱藏。 一次只能貼上一次。 要再次建立同一資產的副本，請再次複製。

### 更改新自適應窗體的內容 {#change-contents-of-new-adaptive-form}

可以使用以下方法更改貼上的自適應表單的內容，使其與複製的表單不同：

1. **更改元資料屬性：**

   您可以更改自適應表單的元資料屬性，例如標題和說明。 有關元資料屬性以及如何更改這些屬性的詳細資訊，請參見 [管理表單元資料](/help/forms/using/manage-form-metadata.md)

1. **為基於XFA/XSD的自適應Forms更改XFA/XSD:**

   您可以更改自適應表單中使用的XFA/XSD。 要瞭解如何更改這些自適應表單，請參見 [管理表單元資料](/help/forms/using/manage-form-metadata.md)

1. **重新發佈:**

   貼上的資產與複製的資產不同。 您可以將其作為新資產發佈，以使其可供最終用戶使用。 要瞭解如何發佈資產，請參閱 [發佈和取消發佈表單](/help/forms/using/publishing-unpublishing-forms.md)
