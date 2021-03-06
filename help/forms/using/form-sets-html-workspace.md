---
title: 在AEM Forms工作區中使用表單集
seo-title: 在AEM Forms工作區中使用表單集
description: 表單集是將HTML5表單分組，並以單一表單集呈現給使用者的集合。 了解如何在AEM Forms工作區中使用表單集。
seo-description: 表單集是將HTML5表單分組，並以單一表單集呈現給使用者的集合。 了解如何在AEM Forms工作區中使用表單集。
uuid: 1a5f3ce8-1d6a-497e-90d0-49765e40cf3b
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: f550b747-2def-4317-9ef7-dc6c1e7bb404
docset: aem65
exl-id: 76a8f93f-eb8a-4e68-8626-efa6dc67668f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 2%

---

# 在AEM Forms工作區中使用表單集{#working-with-formsets-in-aem-forms-workspace}

表單集是將HTML5表單分組，並以單一表單集呈現給使用者的集合。 當最終用戶開始填寫表單集時，他們將從一個表單無縫轉換到另一個表單。 然後，只需按一下即可提交一組表單。 有關表單集以及如何設定的詳細資訊，請參閱AEM Forms中的[表單集](../../forms/using/formset-in-aem-forms.md)。

AEM Forms工作區支援表單集。 使用表單集，可以將與服務或流程相關的多個表單分組，以自動執行業務流程並向最終用戶呈現。 在這種情況下，使用者可以將整組表單填入為一，而且不需要檔案、提交及追蹤個別表單或程式。

## 將表單集附加至AEM Forms工作區應用程式{#attaching-a-formset-to-startpoint-in-an-aem-forms-workspace-app-br}中的起始點

1. 在Workbench中建立業務流程工作流。 如需詳細資訊，請參閱[Workbench說明](https://www.adobe.com/go/learn_aemforms_workbench_63)。
1. 從起始點的流程屬性中，選擇「演示和資料」中的「使用CRX資產」**。**

   ![1-3](assets/1-3.png)

1. 按一下CRX資產路徑旁的![browse](assets/browse.png)（瀏覽）。 此時將出現「選擇表單資產」對話框。

   ![2-1](assets/2-1.png)

1. 按一下&#x200B;**Formset**&#x200B;標籤，從清單中選擇相關表單集，然後按一下&#x200B;**OK**。

1. 更新其他相關進程屬性後部署應用程式。

## 在AEM Forms工作區{#using-formset-in-nbsp-aem-forms-workspace}中使用表單集

表單集附加至起始點後，即可從AEM Forms工作區叫用起始點，如同叫用任何其他起始點一樣。

透過AEM Forms工作區對表單集支援的操作有：

* 另存為草稿
* 鎖定
* 放棄
* 提交
* 新增附件
* 新增附註
* 使用上一頁或下一頁按鈕，在表單集中的表單之間移動

![3-1](assets/3-1.png)

>[!NOTE]
>
>為了在表單集中從上一個表單和下一個表單移動期間改善效能，在相關表單完全呈現之前，所有工作區按鈕(上一頁、下一頁、保存、提交和……（更多）)都被禁用。
