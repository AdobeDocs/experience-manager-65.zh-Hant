---
title: 刪除表單和相關資源
seo-title: Deleting forms and related resources
description: 如何刪除AEM Forms中的表單或資產，以及對參考和反向連結資產及XFA表單的影響。
seo-description: How to delete a form or an asset in AEM Forms and the impact on referenced and referring assets and XFA forms.
uuid: df522b87-59d8-4678-922d-c9aab82b1381
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: c8519eec-f841-4867-baa9-a9e03042755e
role: Admin
exl-id: b31f9f56-dd33-4478-ad34-01ac7d5a1b40
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# 刪除表單和相關資源 {#deleting-forms-and-related-resources}

您可以刪除表單和資產，從存放庫中移除這些資產。 刪除操作適用於所有資產類型和資料夾。

如果您從製作例項刪除資產，該資產也會從發佈例項中刪除。 AEM Forms伺服器包含製作和發佈執行個體。 製作例項用於建立及管理表單資產和資源。 發佈執行個體包含可供使用者使用的已發佈表單資產和相關資源。

## 如何刪除表單 {#how-to-delete-a-form}

1. 透過存取 `https://[hostname]:'port'/aem/forms.html.`
1. 導覽至並選取您要刪除的表單。 按一下「刪除」 ![aem6forms_delete2](assets/aem6forms_delete2.png) 確認刪除操作。

   >[!NOTE]
   >
   >一次只能刪除一個表單。 個別刪除多個表單或刪除父資料夾。

1. 在您刪除資產之前，AEM Forms會檢查參考並要求明確確認。 如果您想刪除資產而不考慮關係狀態，請按一下「強制刪除」 。

   >[!NOTE]
   >
   >刪除由其他資產參考的資產可能會造成功能問題。

   >[!NOTE]
   >
   >如果選取的資產是資料夾，且其階層中包含這類資產，請個別刪除其他資產或刪除整個資料夾。

## 刪除引用的XFA表單的影響 {#impact-of-deleting-a-referenced-xfa-form}

在AEM Forms中，最適化表單或其他XFA表單範本都可參照XFA表單範本。 此外，範本可以參照資源或其他XFA範本。

不建議刪除最適化表單所參照的XFA表單，因為這可能會損毀最適化表單。 適用性表單參考XFA表單時，其欄位會系結。 刪除XFA後，適用性表單無法將其欄位與XFA欄位同步，且會顯示這類欄位的錯誤訊息。 若要進一步了解引用XFA刪除的影響以及臟AF的相關資訊，請參閱 [更新參考的XFA表單](/help/forms/using/get-xdp-pdf-documents-aem.md#p-updating-referenced-xfa-forms-p).

若要刪除此類XFA表單，請更新最適化表單並移除與XFA欄位的系結。
