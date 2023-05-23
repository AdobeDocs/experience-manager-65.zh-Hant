---
title: 查看和瞭解AEM Forms分析報告
seo-title: View and understand AEM Forms analytics reports
description: AEM Forms與Adobe Analytics整合，為您提供有關已發佈自適應表單的摘要和詳細分析。
seo-description: AEM Forms integrates with Adobe Analytics and provides you summary and detailed analytics about your published adaptive forms.
uuid: b15ba5f3-aea7-40f5-893e-aaf3834cbc33
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 3690fa80-6332-4df8-afea-77b5490fe0d1
docset: aem65
exl-id: c5a4e6f6-f331-41e9-a0a9-51a30df6e2cd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1050'
ht-degree: 2%

---

# 查看和瞭解AEM Forms分析報告 {#view-and-understand-aem-forms-analytics-reports}

Adobe Experience Manager Forms與Adobe Analytics整合，使您能夠捕獲和跟蹤已發佈表單和文檔的效能指標。 分析這些指標背後的目標是根據有關使表單或文件更有用所需的變更資料做出明智的決策。

## 設定分析 {#setting-up-analytics}

AEM Forms的分析功能是AEM Forms附加軟體包的一部分。 有關安裝附加軟體包的資訊，請參見 [安裝和配置AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md)。

除了附加包外，您還需要一個Adobe Analytics帳戶。 有關解決方案的資訊，請參見 [Adobe Analytics](https://www.adobe.com/solutions/digital-analytics.html)。

一旦您擁有了AEM Forms附加包和Adobe Analytics帳戶，就將Adobe Analytics帳戶與AEM Forms整合，並啟用對表單或文檔的跟蹤，如中所述 [配置分析和報告](../../forms/using/configure-analytics-forms-documents.md)。

### 如何記錄用戶交互資訊 {#how-user-interaction-information-is-recorded}

當用戶與表單交互時，這些交互會被記錄併發送到分析伺服器。 以下清單指示伺服器對各種用戶活動的調用：

* 每次訪問2次
* 小組訪問1個
* 保存1
* 2個
* 保存2
* 1個幫助
* 每個驗證錯誤1
* 表單格式副本1 +預設面板訪問1 +預設第1次現場訪問1
* 2表示放棄形式

>[!NOTE]
>
>這份清單並非詳盡無遺。

### 查看分析報告 {#summary-report}

執行以下步驟查看分析報告：

1. 登錄到AEM門戶 `https://[hostname]:'port'`
1. 按一下 **Forms>Forms和文檔**。
1. 選擇要查看其分析報表的表單。
1. 選擇 **更多>分析報告**。

![分析報告](assets/analyticsreport.png)

**答：** 分析報表命令

AEM Forms顯示窗體和窗體中每個面板的分析報告，如下所示。

![自適應表單的摘要報告](assets/analyticsdashboard_callout.png)

**答：** 轉換 **B** 表單級摘要 **C.** 面板級摘要 **D** 訪問者瀏覽器 — 篩選器 **E.** 訪問者作業系統 — 篩選器 **F.** 訪問者語言 — 篩選器

預設情況下，將顯示最近七天的分析報告。 您可以查看過去15天、過去一個月等的報表，或指定日期範圍。

>[!NOTE]
>
>「過去7天」和「過去15天」等選項不包括生成分析報告的當天的資料。 要包括當前日的資料，您需要指定包括當前日的日期範圍，然後運行報表。

![日期範圍](assets/date-range.png)

### 用於自適應和HTML5窗體的轉換圖 {#conversions-graph-for-adaptive-and-html-forms}

表單層轉換圖使您能夠瞭解表單在以下關鍵績效指標(KPI)上的表現：

* **格式副本**:開啟窗體的次數
* **訪問者**:窗體的訪問者數
* **提交**:提交表單的次數

![轉換圖](assets/conversion-graph.png)

### 自適應和HTML5表單的分析報告 {#analytics-report-for-adaptive-and-html-forms}

表單層摘要部分讓您能夠深入瞭解表單在以下主要績效指標(KPI)上的表現：

* **平均填充時間**:填寫表單所花的平均時間。 當用戶在表單上花費時間但未提交時，該時間不包括在此計算中。
* **格式副本**:表單已呈現或開啟的次數
* **草稿**:表單保存為草稿的次數
* **提交**:已提交表單的次數
* **中止**:用戶開始填寫表單，然後不填寫表單而離開的次數
* **獨特訪問者**:表單由唯一訪問者呈現的次數。 有關唯一訪問者的詳細資訊，請參閱 [獨特的訪問者、訪問和客戶行為](https://helpx.adobe.com/analytics/kb/unique-visitors-visitor-behavior.html)。

![擴展的表單級摘要分析報告](assets/analytics-report.png)

### 面板報告 {#bottom-summary-report}

面板級摘要部分以格式提供有關每個面板的以下資訊：

* **平均填充時間**:在面板上花費的平均時間，無論表單是否已提交
* **遇到錯誤**:用戶在面板中的欄位上遇到的平均錯誤數。 「遇到的錯誤」是通過將欄位中的總錯誤除以表單的格式副本數來得出的。
* **訪問的幫助**:用戶訪問面板中欄位的上下文幫助的平均次數。 通過將欄位的「幫助」訪問總次數除以表單的格式副本數來達到「訪問幫助」。

#### 詳細面板報告 {#detailed-panel-report}

也可以通過按一下「面板報告」中面板的名稱來查看每個面板的詳細資訊。

![詳細面板報告](assets/panel-report-detailed.png)

詳細報告顯示面板中所有欄位的值。

「面板報告」有三個頁籤：

* **時間報告**（預設）:顯示填充面板中每個欄位所花費的時間（以秒為單位）
* **錯誤報告**:顯示填寫欄位時用戶遇到的錯誤數
* **幫助報告**:訪問特定欄位的幫助的次數

如果有多個面板可用，則可以在面板之間導航。

### 篩選器：瀏覽器、作業系統和語言 {#filters-browser-os-and-language}

「瀏覽器分發」、「作業系統分發」和「語言分發」表顯示窗體用戶的格式副本、訪問者和提交，並按瀏覽器、作業系統和語言顯示。 預設情況下，這些表最多顯示五個條目。 按一下「顯示更多」(Show More)可顯示更多條目，按一下「顯示更少」(Show Less)可返回到常規的五個或更少條目。

要進一步篩選分析資料，可按一下任何表中的條目。 例如，如果在「瀏覽器分發」(Browser Distribution)表中按一下「Google鉻」(Chrome)，則報告將再次呈現，其中包含與Google鉻瀏覽器相關的資料，如下所示：

![應用於分析報告的篩選器 — GoogleChrome ](assets/filter-1.png)

如果在應用篩選器後查看面板報告，則面板報告資料也會根據應用的篩選器顯示。

應用篩選器後：

* 分發表變為只讀，因為一次只能應用一個篩選器。
* 應用的篩選器表消失。
* 可按一下「關閉」(Close)按鈕（在下面突出顯示）以刪除應用的篩選器。

![關閉按鈕以刪除應用的篩選器](assets/close-filter.png)

### A/B測試 {#a-b-testing}

如果啟用了A/B測試並為表單設定了，則報告頁中有一個下拉清單，您可以使用它來顯示A/B測試報告。 A/B測試報告顯示您設定的兩個窗體版本的比較效能。

有關A/B測試的詳細資訊，請參見 [建立和管理自適應表單的A/Btest](../../forms/using/ab-testing-adaptive-forms.md)。
