---
title: 檢視和瞭解AEM Forms分析報表
description: AEM Forms與Adobe Analytics整合，為您提供有關已發佈的最適化表單的摘要和詳細分析。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
docset: aem65
exl-id: c5a4e6f6-f331-41e9-a0a9-51a30df6e2cd
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
feature: Adaptive Forms
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 0%

---

# 檢視和瞭解AEM Forms分析報表 {#view-and-understand-aem-forms-analytics-reports}

Adobe Experience Manager Forms與Adobe Analytics整合，可讓您擷取及追蹤已發佈表單和檔案的績效量度。 分析這些量度背後的目的是，根據使表單或檔案更易於使用所需的變更相關資料，做出明智的決定。

## 設定分析 {#setting-up-analytics}

AEM Forms中的分析功能屬於AEM Forms附加元件套件的一部分。 如需有關安裝附加元件套件的資訊，請參閱[安裝和設定AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md)。

除了附加元件套件之外，您還需要Adobe Analytics帳戶。 如需解決方案的詳細資訊，請參閱[Adobe Analytics](https://www.adobe.com/solutions/digital-analytics.html)。

取得AEM Forms附加元件套件和Adobe Analytics帳戶後，請將Adobe Analytics帳戶與AEM Forms整合，並如[設定分析和報表](../../forms/using/configure-analytics-forms-documents.md)中所述，啟用表單或檔案上的追蹤。

### 如何記錄使用者互動資訊 {#how-user-interaction-information-is-recorded}

使用者與表單互動時，系統會記錄互動並傳送至Analytics伺服器。 下列清單指示各種使用者活動的伺服器呼叫：

* 每次造訪每個欄位2次呼叫
* 1代表面板造訪
* 1表示儲存
* 2以提交
* 儲存2
* 1以取得說明
* 每個驗證錯誤為1
* 1代表表單轉譯+ 1代表預設面板造訪+ 1代表預設第一個欄位造訪
* 2表示表單放棄

>[!NOTE]
>
>此清單並非詳盡無遺。

### 檢視分析報表 {#summary-report}

執行以下步驟以檢視分析報表：

1. 在`https://[hostname]:'port'`登入AEM入口網站
1. 按一下「**Forms > Forms與檔案**」。
1. 選取您要檢視其分析報表的表單。
1. 選取&#x200B;**更多> Analytics報表**。

![analyticsreport](assets/analyticsreport.png)

**A.**&#x200B;分析報告命令

AEM Forms會顯示表單及表單中每個面板的analytics報表，如下所示。

![最適化表單的摘要報告](assets/analyticsdashboard_callout.png)

**A.**&#x200B;轉換&#x200B;**B.**&#x200B;表單層級摘要&#x200B;**C.**&#x200B;面板層級摘要&#x200B;**D.**&#x200B;訪客瀏覽器 — 篩選訪客的&#x200B;**E.**&#x200B;作業系統 — 篩選&#x200B;**F.**&#x200B;訪客的語言 — 篩選

依預設，會顯示過去七天的分析報表。 您可以檢視最近15天、最近一個月等的報告，或指定日期範圍。

>[!NOTE]
>
>「最近7天」和「最近15天」等選項不包含您產生分析報表當天的資料。 若要包含當天的資料，您必須指定包含當天的日期範圍，然後執行報表。

![日期範圍](assets/date-range.png)

### 最適化和HTML5表單的轉換圖 {#conversions-graph-for-adaptive-and-html-forms}

表單層級轉換圖表可讓您深入瞭解表單在下列關鍵績效指標(KPI)上的執行情形：

* **轉譯**：表單開啟的次數
* **訪客**：表單的訪客數量
* **提交專案**：提交表單的次數

![轉換圖形](assets/conversion-graph.png)

### 最適化和HTML5表單的Analytics報表 {#analytics-report-for-adaptive-and-html-forms}

表單層級摘要區段可讓您深入瞭解表單在下列關鍵績效指標(KPI)上的執行情形：

* **平均填寫時間**：填寫表單所花費的平均時間。 當使用者在表單上花費時間但未提交時，該時間未包含在此計算中。
* **轉譯**：表單已轉譯或開啟的次數
* **草稿**：表單已儲存為草稿的次數
* **提交專案**：已提交表單的次數
* **中止**：使用者開始填寫表單後離開而未完成表單的次數
* **不重複訪客**：表單由不重複訪客轉譯的次數。 如需不重複訪客的詳細資訊，請參閱[不重複訪客、造訪和客戶行為](https://helpx.adobe.com/tw/analytics/kb/unique-visitors-visitor-behavior.html)。

![已展開的表單層級摘要分析報告](assets/analytics-report.png)

### 面板報告 {#bottom-summary-report}

面板層級摘要區段提供表單中每個面板的下列相關資訊：

* **平均填滿時間**：在面板上的平均逗留時間，無論表單是否提交
* **發生錯誤**：使用者在面板的欄位上遇到的平均錯誤數。 將欄位中的錯誤總數除以表單的轉譯數目，即可得出遇到的錯誤。
* **已存取說明**：使用者存取面板中欄位之內容中說明的平均次數。 已存取說明的到達方式是將欄位已存取說明的總次數除以表單轉譯次數。

#### 詳細面板報告 {#detailed-panel-report}

您也可以按一下「面板報表」中面板的名稱，以檢視每個面板的詳細資訊。

![詳細面板報告](assets/panel-report-detailed.png)

詳細報告會顯示面板中所有欄位的值。

面板報告有三個索引標籤：

* **時間報表**（預設）：顯示填滿面板中每個欄位所花費的時間（以秒為單位）
* **錯誤報告**：顯示使用者在填寫欄位時遇到的錯誤數目
* **說明報告**：存取特定欄位說明的次數

如果有多個面板可供使用，您可在面板之間導覽。

### 篩選器：瀏覽器、作業系統和語言 {#filters-browser-os-and-language}

「瀏覽器分送」、「OS分送」和「語言分送」表格會依瀏覽器、作業系統和表單使用者的語言顯示轉譯、訪客和提交。 預設情況下，這些表格最多會顯示五個專案。 您可以按一下「顯示更多」來顯示更多專案，然後按一下「顯示更少」來返回一般五個或更少專案。

若要進一步篩選分析資料，您可以按一下任何表格中的專案。 例如，如果您按一下「瀏覽器散佈」表格中的Google Chrome ，報表會再次呈現並包含與Google Chrome瀏覽器相關的資料，如下所示：

![套用至Analytics報告的篩選器 — Google Chrome ](assets/filter-1.png)

如果您在套用篩選器後檢視面板報表，面板報表資料也會根據套用的篩選器顯示。

套用篩選器後：

* 發佈表格會變成唯讀，因為一次只能套用一個篩選器。
* 套用的篩選器表格會消失。
* 您可以按一下「關閉」按鈕（在下方反白顯示）來移除套用的篩選器。

![關閉按鈕以移除套用的篩選器](assets/close-filter.png)

### A/B測試 {#a-b-testing}

如果您已啟用並設定表單的A/B測試，報表頁面會有一個下拉式清單，可用來顯示A/B測試報表。 A/B測試報告會顯示您已設定的兩個表單版本的比較效能。

如需A/B測試的詳細資訊，請參閱[建立和管理最適化表單的A/B測試](../../forms/using/ab-testing-adaptive-forms.md)。
