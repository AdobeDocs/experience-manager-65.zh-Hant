---
title: 管理Workspace中顯示的類別
description: 在Workspace中，使用者可啟動的流程會以類別顯示在左側導覽窗格中。 瞭解如何管理Workspace中顯示的這些類別。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 62621fe9-f69f-4bc0-aecc-d7bcc3064516
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# 管理Workspace中顯示的類別 {#managing-the-categories-displayed-in-workspace}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

在Workspace中，使用者可啟動的流程會以類別顯示在左側導覽窗格中。 您可以在管理主控台中設定類別，或流程設計人員可以在Workbench中設定類別。 流程設計人員建立流程時，會將流程指派給類別。

指定類別名稱后，請建立類別名稱，好讓類別名稱可正確顯示在Workspace導覽窗格中。 依預設，左側導覽窗格的固定寬度為210畫素，約為24個字元。 如果您指定的類別名稱太長，無法符合左側導覽窗格的固定寬度，則會截斷該名稱。 只有當滑鼠指標停留在全名上時，才會顯示全名。 請避免類別名稱被截斷。 下列範例說明符合的類別名稱和截斷的類別名稱：

**適合的類別名稱：**&#x200B;出席與休假

**截斷的類別名稱：**&#x200B;出席和休假（美國）

在Workspace中，類別中的程式通常會在開始程式頁面上顯示為卡片。 一般而言，在使用者需要捲動才能檢視剩餘卡片之前，類別的6張卡片可以顯示在畫面上。 因為捲動會使得尋找程式變得更加困難，請考慮將每個類別限製為六個程式，或者根據您的解析度限制畫面上可顯示的程式數目，而不需要任何捲動。

如果您使用MySQL做為AEM表單資料庫，Administration Console無法區分僅使用擴充字元的不同類別名稱。 例如，如果您建立名為abcde的類別和名為abcde的類別，系統會將兩者視為相同。

## 新增類別 {#add-a-category}

1. 在Administration Console中，按一下「服務>應用程式和服務>類別管理」。
1. 按一下「新增」。 如果您想要新增子類別，請選取類別，然後按一下「新增」。
1. 在「名稱」方塊中，輸入類別的名稱，並在「描述」方塊中，輸入類別的說明。
1. 按一下「新增」。 類別會顯示在「類別管理」頁面上。

   ***附註&#x200B;**：建立類別時，您最多只能新增五個階層層級。*

## 編輯類別 {#edit-a-category}

1. 在Administration Console中，按一下「服務>應用程式和服務>類別管理」。
1. 選取您要編輯的類別，然後按一下「編輯」。 或者，您可以連按兩下類別以進行編輯。
1. 在「名稱」方塊中編輯類別的名稱。

## 移除類別 {#remove-a-category}

您只能移除未使用的類別。

1. 在Administration Console中，按一下「服務>應用程式和服務>類別管理」。
1. 在「類別管理」頁面上，選取要移除之類別的核取方塊，然後按一下「移除」。 類別不再顯示。
