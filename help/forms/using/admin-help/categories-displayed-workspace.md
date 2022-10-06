---
title: 管理工作區中顯示的類別
seo-title: Managing the categories displayed in Workspace
description: 在工作區中，使用者可啟動的程式會顯示在左側導覽窗格的類別中。 了解如何管理工作區中顯示的這些類別。
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

# 管理工作區中顯示的類別 {#managing-the-categories-displayed-in-workspace}

在工作區中，使用者可啟動的程式會顯示在左側導覽窗格的類別中。 您可以在管理控制台中設定類別，或流程設計人員可以在Workbench中設定類別。 當流程設計人員建立流程時，他們會將它們指派給類別。

當您指定類別名稱時，請建立類別名稱，使其在「工作區」導覽窗格中正確顯示。 依預設，左側導覽窗格的固定寬度為210像素，大約為24個字元。 如果您指定的類別名稱太長，無法放入左側導覽窗格的固定寬度內，則會截斷名稱。 只有當滑鼠指針暫停在滑鼠指針上時，全名才會出現。 嘗試避免類別名稱遭截斷。 下列範例說明適合的類別名稱和截斷的類別名稱：

**適合以下項目的類別名稱：** 出勤假

**截斷的類別名稱：** 出勤假（美國）

在工作區中，類別內的程式通常會在「開始程式」頁面上顯示為卡片。 一般而言，某類別的畫面上可顯示6張卡片，然後使用者才需要捲動才能檢視剩餘的卡片。 由於滾動使查找進程更加困難，請考慮將每個類別限制為六個進程，或根據您的解析度限制螢幕上顯示的進程數，而不需要任何滾動。

如果您使用MySQL作為AEM表單資料庫，Administration Console無法區分兩個類別名稱，這兩個名稱僅在使用擴展字元時有所不同。 例如，如果您建立名為abcde的類別和名為âbcdè的類別，則它們被視為相同。

## 新增類別 {#add-a-category}

1. 在管理控制台中，按一下「服務>應用程式和服務>類別管理」。
1. 按一下「新增」。如果要添加子類別，請選擇一個類別，然後按一下「添加」。
1. 在「名稱」框中，鍵入類別的名稱，在「說明」框中，鍵入類別的說明。
1. 按一下「新增」。類別會顯示在「類別管理」頁面上。

   ***附註&#x200B;**:建立類別時，最多只能新增五個階層層級。*

## 編輯類別 {#edit-a-category}

1. 在管理控制台中，按一下「服務>應用程式和服務>類別管理」。
1. 選擇要編輯的類別，然後按一下「編輯」。 或者，您也可以連按兩下要編輯的類別。
1. 在「名稱」(Name)框中編輯類別的名稱。

## 移除類別 {#remove-a-category}

您只能移除未使用的類別。

1. 在管理控制台中，按一下「服務>應用程式和服務>類別管理」。
1. 在「類別管理」頁上，選擇要刪除的類別的複選框，然後按一下「刪除」。 類別不再顯示。
