---
title: 刪除表單和相關資源
seo-title: Deleting forms and related resources
description: 如何刪除AEM Forms的表單或資產，以及對引用和引用資產和XFA表單的影響。
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

您可以刪除表單和資產，以從儲存庫中刪除這些資產。 刪除操作可用於所有資產類型和資料夾。

如果從「作者」實例中刪除資產，則資產也會從「發佈」實例中刪除。 AEM Forms伺服器由作者和發佈實例組成。 「作者」實例用於建立和管理表單資產和資源。 「發佈」實例包含可供最終用戶使用的已發佈表單資產和相關資源。

## 如何刪除表單 {#how-to-delete-a-form}

1. 登錄AEM Forms用戶介面，訪問 `https://[hostname]:'port'/aem/forms.html.`
1. 導航到要刪除的表單並選擇。 按一下刪除 ![aem6forms_delete2](assets/aem6forms_delete2.png) 確認刪除操作。

   >[!NOTE]
   >
   >一次只能刪除一個表單。 單獨刪除多個表單或刪除父資料夾。

1. 在刪除資產之前，AEM Forms會檢查引用並請求明確確認。 如果要刪除資產而不考慮關係狀態，請按一下「強制刪除」。

   >[!NOTE]
   >
   >刪除由其他資產引用的資產可能會導致功能問題。

   >[!NOTE]
   >
   >如果所選資產是資料夾，且其層次結構中包含此資產，則單獨刪除其他資產或刪除整個資料夾。

## 刪除引用的XFA表單的影響 {#impact-of-deleting-a-referenced-xfa-form}

在AEM Forms,XFA表單模板可以由自適應表單或另一個XFA表單模板引用。 此外，模板可以引用資源或其他XFA模板。

不建議刪除由自適應表單引用的XFA表單，因為它可能會損壞自適應表單。 當自適應表單引用XFA表單時，其欄位將被綁定。 刪除XFA後，自適應表單無法將其欄位與XFA欄位同步，並會顯示此類欄位的錯誤消息。 有關引用的XFA刪除的影響和臟AF的詳細資訊，請參見 [更新引用的XFA表單](/help/forms/using/get-xdp-pdf-documents-aem.md#p-updating-referenced-xfa-forms-p)。

要刪除此類XFA表單，請更新自適應表單並刪除與XFA欄位的綁定。
