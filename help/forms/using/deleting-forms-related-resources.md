---
title: 刪除表單和相關資源
description: 如何刪除AEM Forms中的表單或資產，以及對引用和反向連結資產和XFA表單的影響。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
role: Admin
exl-id: b31f9f56-dd33-4478-ad34-01ac7d5a1b40
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# 刪除表單和相關資源 {#deleting-forms-and-related-resources}

您可以刪除表單和資產，以從存放庫移除這些資產。 刪除操作適用於所有資產型別和資料夾。

如果您從製作例項中刪除資產，該資產也會從發佈例項中刪除。 AEM Forms伺服器包含作者和發佈執行個體。 製作例項用於建立及管理表單資產和資源。 發佈執行個體包含可供一般使用者使用的已發佈表單資產和相關資源。

## 如何刪除表單 {#how-to-delete-a-form}

1. 登入AEM Forms使用者介面，方法是存取 `https://[hostname]:'port'/aem/forms.html.`
1. 導覽至並選取您要刪除的表單。 按一下刪除 ![aem6forms_delete2](assets/aem6forms_delete2.png) 工具列並確認刪除操作。

   >[!NOTE]
   >
   >一次只能刪除一個表單。 個別刪除多個表單或刪除父資料夾。

1. 在刪除資產之前，AEM Forms會檢查參考資料並要求明確確認。 如果您想要刪除資產，無論關係狀態為何，請按一下「強制刪除」 。

   >[!NOTE]
   >
   >刪除其他資產所參照的資產可能會造成功能問題。

   >[!NOTE]
   >
   >如果選取的資產是檔案夾，且在其階層中包含此類資產，請個別刪除其他資產或刪除整個檔案夾。

## 刪除參照的XFA表單的影響 {#impact-of-deleting-a-referenced-xfa-form}

在AEM Forms中，XFA表單範本可由最適化表單或其他XFA表單範本參照。 此外，範本可以參照資源或其他XFA範本。

不建議刪除最適化表單參考的XFA表單，因為這樣可能會損毀最適化表單。 當最適化表單參考XFA表單時，其欄位會受到限制。 刪除XFA後，最適化表單無法將其欄位與XFA欄位同步，並顯示此類欄位的錯誤訊息。 若要進一步瞭解參照的XFA刪除的影響以及已修改的AF，請參閱 [更新參考的XFA表單](/help/forms/using/get-xdp-pdf-documents-aem.md#p-updating-referenced-xfa-forms-p).

若要刪除這類XFA表單，請更新最適化表單並移除與XFA欄位的繫結。
