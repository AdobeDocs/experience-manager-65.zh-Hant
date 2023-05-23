---
title: 管理在工作區中顯示的類別
seo-title: Managing the categories displayed in Workspace
description: 在工作區中，用戶可以啟動的進程顯示在左側導航窗格中的類別中。 瞭解如何管理Workspace中顯示的這些類別。
seo-description: In Workspace, the processes that a user can start are displayed in categories in the left navigation pane. Learn how you can manage these categories displayed in Workspace.
uuid: c2a275f5-872e-467f-9f07-4b130631e8a8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0d1536a2-10ac-4031-bd7f-264b02d0d75f
exl-id: 62621fe9-f69f-4bc0-aecc-d7bcc3064516
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---

# 管理在工作區中顯示的類別 {#managing-the-categories-displayed-in-workspace}

在工作區中，用戶可以啟動的進程顯示在左側導航窗格中的類別中。 您可以在管理控制台中設定類別，或者流程設計人員可以在Workbench中設定類別。 當流程設計器建立流程時，它們會將其分配給類別。

指定類別名稱時，請建立它們，以便它們能正確顯示在「工作區」導航窗格中。 預設情況下，左側導航窗格的固定寬度為210像素，大約為24個字元。 如果指定的類別名稱太長，無法容納在左導航窗格的固定寬度內，則它將被截斷。 僅當滑鼠指針暫停在其上時，全名才顯示。 嘗試避免截斷的類別名稱。 以下示例說明適合的類別名稱和截斷的類別名稱：

**適合的類別名稱：** 出勤和休假

**截斷的類別名稱：** 出席和休假（美國）

在Workspace中，類別中的進程通常顯示為「開始進程」頁上的卡。 通常，在要求用戶滾動查看剩餘的卡之前，可在螢幕上顯示某個類別的6張卡。 由於滾動使查找進程更加困難，請考慮將每個類別限制為六個進程，或者根據解析度限制可在螢幕上顯示的進程數，而無需任何滾動。

如果將MySQL用作表單數AEM據庫，則管理控制台無法區分兩個類別名稱，這兩個類別名稱僅在使用擴展字元時不同。 例如，如果您建立名為abcde的類別和名為âbcdè的類別，則它們被視為相同。

## 添加類別 {#add-a-category}

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「類別管理」。
1. 按一下「添加」。 如果要添加子類別，請選擇一個類別，然後按一下「添加」。
1. 在「名稱」(Name)框中，鍵入類別的名稱，在「說明」(Description)框中，鍵入類別的說明。
1. 按一下「添加」。 該類別顯示在「類別管理」頁上。

   ***附註&#x200B;**:在建立類別時，最多只能添加五個層次。*

## 編輯類別 {#edit-a-category}

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「類別管理」。
1. 選擇要編輯的類別，然後按一下「編輯」。 或者，可按兩下要編輯的類別。
1. 在「名稱」(Name)框中編輯類別的名稱。

## 刪除類別 {#remove-a-category}

您只能刪除未使用的類別。

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「類別管理」。
1. 在「類別管理」頁上，選中要刪除的類別的複選框，然後按一下「刪除」。 類別不再顯示。
