---
title: 重複使用最適化表單
description: 您可以重複使用現有的最適化表單來建立新的最適化表單。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: ef564750-f107-41cb-887e-fc6d22b7d32e
feature: Adaptive Forms,Foundation Components
exl-id: d8ee4e82-3137-430e-aa47-b00191f2729c
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 11%

---

# 重複使用最適化表單 {#reusing-adaptive-forms}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，用來[建立新的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/manage-metadata/reusing-adaptive-forms.html) |
| AEM 6.5 | 本文章 |

## 簡介 {#introduction}

如果您想使用現有最適化表單的某些屬性來產生新表單，您只需使用複製貼上功能即可。 此外，您還可以在所需的資料夾路徑貼上新的最適化表單。 會複製所有中繼資料屬性，並複製XFA和XSD型最適化表單的XFA和XSD。

>[!NOTE]
>
>不會複製狀態和檢閱詳細資料。 例如，如果您的最適化表單已發佈，然後您複製該表單時，貼上的最適化表單會處於未發佈狀態。 同樣地，如果正在稽核複製的資產，貼上的資產不會處於同一稽核中。

### 複製最適化表單 {#copy-an-adaptive-form}

使用下列其中一種方法複製調適型表單：

1. 按一下「快速動作」中的複製![aem6forms_copy](assets/aem6forms_copy.png)圖示。

   >[!NOTE]
   >
   >快速動作是在滑鼠懸停時顯示在縮圖上的動作專案。

1. 選取最適化表單。 不同檢視的選取程式不同。

   如果您處於卡片檢視，請按一下選取專案![aem6forms_check-circle](assets/aem6forms_check-circle.png)圖示，前往選取模式，然後按一下您要複製的所有最適化表單。

   如果您處於清單檢視中，請按一下所有最適化表單的核取方塊以選取它們。

   >[!NOTE]
   >
   >所有選取的資產都必須是調適型表單，因為調適型表單僅支援複製貼上功能，而且所有選取的資產都必須存在於相同的資料夾中。

   選取資產後，按一下工具列中顯示的複製![aem6forms_copy](assets/aem6forms_copy.png)圖示，以複製選取的最適化表單。

### 貼上最適化表單 {#paste-an-adaptive-form}

按一下複製動作會自動退出選取模式，並顯示貼上![aem6forms_paste](assets/aem6forms_paste.png)圖示。 現在移至所需的資料夾路徑，然後按一下貼上![aem6forms_paste](assets/aem6forms_paste.png)圖示，貼上複製的自適應表單。

如果貼上同一個資料夾或另一個具有相同節點名稱的檔案(儲存於CRX存放庫中)存在於此目標資料夾中，則會將1附加至尾碼(例如，myaf會變成myaf1，而如果myaf1存在於相同位置，myaf會變成myaf2。 所有其他屬性仍維持與原始的最適化表單相同。

按一下貼上![aem6forms_paste](assets/aem6forms_paste.png)圖示後，該圖示將再次隱藏。 您一次只能貼上一次。 若要再次建立相同資產的復本，請再次複製。

### 變更新最適化表單的內容 {#change-contents-of-new-adaptive-form}

您可使用下列方法，變更貼上之最適化表單的內容，使其與複製的表單不同：

1. **變更中繼資料屬性：**

   您可以變更最適化表單的中繼資料屬性，例如標題和說明。 如需有關中繼資料屬性及其變更方式的詳細資訊，請參閱[管理表單中繼資料](/help/forms/using/manage-form-metadata.md)

1. **變更XFA/XSD型最適化Forms的XFA/XSD：**

   您可以變更最適化表單中使用的XFA/XSD。 若要瞭解如何變更這些最適化表單，請參閱[管理表單中繼資料](/help/forms/using/manage-form-metadata.md)

1. **重新發佈：**

   貼上的資產與複製的資產不同。 您可以將其發佈為新資產，以供一般使用者使用。 若要瞭解如何發佈資產，請參閱[發佈與取消發佈表單](/help/forms/using/publishing-unpublishing-forms.md)
