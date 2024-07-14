---
title: 在AEM Forms工作區中使用表單集
description: 表單集是一組HTML5表單，以單一表單集形式提供給一般使用者。 瞭解如何在AEM Forms工作區中使用表單集。
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 76a8f93f-eb8a-4e68-8626-efa6dc67668f
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 1%

---

# 在AEM Forms工作區中使用表單集{#working-with-formsets-in-aem-forms-workspace}

表單集是一組HTML5表單，以單一表單集形式提供給一般使用者。 使用者開始填寫表單集時，會順暢地從一個表單轉換為另一個表單。 然後，您只需按一下即可提交該組表單。 如需表單集及其設定方式的詳細資訊，請參閱AEM Forms中的[表單集](../../forms/using/formset-in-aem-forms.md)。

AEM Forms工作區支援表單集。 使用表單集，可以分組與服務或流程相關的多個表單，以自動化業務流程並向終端使用者呈現。 在這種情況下，使用者可以完整填寫整個集，無需檔案、提交和追蹤個別表單或流程。

## 將表單集附加到AEM Forms工作區應用程式中的起點 {#attaching-a-formset-to-startpoint-in-an-aem-forms-workspace-app-br}

1. 在「維護作業」中建立業務處理工作流程。 如需詳細資訊，請參閱[Workbench說明](https://www.adobe.com/go/learn_aemforms_workbench_63)。
1. 從起點的程式屬性中，選取&#x200B;**在簡報與資料中使用CRX資產**。

   ![1-3](assets/1-3.png)

1. 按一下CRX資產路徑旁的![瀏覽](assets/browse.png) （瀏覽）。 選取表單資產對話方塊隨即顯示。

   ![2-1](assets/2-1.png)

1. 按一下&#x200B;**表單集**&#x200B;標籤，從清單中選取相關的表單集，然後按一下&#x200B;**確定**。

1. 在更新其他相關程式屬性之後部署應用程式。

## 使用AEM Forms工作區中的表單集 {#using-formset-in-nbsp-aem-forms-workspace}

將表單集附加到起點後，就可以像叫用任何其他起點一樣，從AEM Forms工作區叫用起點。

透過AEM Forms工作區支援在表單集上的作業包括：

* 另存為草稿
* 鎖定
* 放棄
* 提交
* 新增附件
* 新增附註
* 使用「上一步」或「下一步」按鈕在表單集中的表單之間移動

![3-1](assets/3-1.png)

>[!NOTE]
>
>為了在表單集中從上一個和下一個表單移動期間改善效能，在相關表單完全呈現之前，所有Workspace按鈕(「上一步」、「下一個」、「儲存」、「提交」和…… （更多）)都會停用。
