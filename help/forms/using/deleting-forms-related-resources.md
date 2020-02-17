---
title: 刪除表單和相關資源
seo-title: 刪除表單和相關資源
description: 如何刪除AEM Forms中的表單或資產，以及對參考和反向連結資產和XFA表單的影響。
seo-description: 如何刪除AEM Forms中的表單或資產，以及對參考和反向連結資產和XFA表單的影響。
uuid: df522b87-59d8-4678-922d-c9aab82b1381
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: c8519eec-f841-4867-baa9-a9e03042755e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 刪除表單和相關資源 {#deleting-forms-and-related-resources}

您可以刪除表單和資產，以便從儲存庫中刪除這些資產。 刪除操作適用於所有資產類型和資料夾。

如果您從「作者」例項刪除資產，該資產也會從「發佈」例項中刪除。 AEM Forms伺服器包含「作者」和「發佈」例項。 「作者」例項是用於建立和管理表單資產與資源。 「發佈」例項包含已發佈表單資產和可供使用者使用的相關資源。

## 如何刪除表單 {#how-to-delete-a-form}

1. 存取 `https://[hostname]:[portport]/aem/forms.html.`
1. 導覽至您要刪除的表單並加以選取。 按一下工 ![具列中的「刪除aem6forms_delete2](assets/aem6forms_delete2.png) 」，並確認刪除作業。

   >[!NOTE]
   >
   >一次只能刪除一個表單。 單獨刪除多個表單或刪除父資料夾。

1. 在您刪除資產之前，AEM Forms會檢查參考並要求明確確認。 如果要刪除資產而不考慮關係狀態，請按一下「強制刪除」。

   >[!NOTE]
   >
   >刪除由其他資產引薦的資產可能會導致功能問題。

   >[!NOTE]
   >
   >如果選取的資產是檔案夾，且其階層中包含此類資產，請個別刪除其他資產或刪除整個檔案夾。

## 刪除引用的XFA表單的影響 {#impact-of-deleting-a-referenced-xfa-form}

在AEM Forms中，XFA表單範本可以透過最適化表單或其他XFA表單範本來參考。 此外，範本可參照資源或其他XFA範本。

不建議刪除由自適應表單引用的XFA表單，因為它會損壞自適應表單。 當最適化表單引用XFA表單時，其欄位會系結。 刪除XFA後，自適應表單無法將其欄位與XFA欄位同步，並顯示此類欄位的錯誤消息。 要瞭解有關引用的XFA刪除的影響和有關臟AF的更多資訊，請參 [閱更新引用的XFA表單](/help/forms/using/get-xdp-pdf-documents-aem.md#p-updating-referenced-xfa-forms-p)。

若要刪除此類XFA表單，請更新最適化表單並移除與XFA欄位的系結。
