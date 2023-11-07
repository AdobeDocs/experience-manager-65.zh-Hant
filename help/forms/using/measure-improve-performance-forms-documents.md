---
title: 衡量及改善表單的成效和轉換
seo-title: Measure and improve effectiveness and conversion of forms
description: AEM Forms與Adobe Target和Adobe Analytics解決方案整合，可讓您測量並改善表單的效能和轉換率。
seo-description: AEM Forms integrates with Adobe Target and Adobe Analytics solutions that lets you measure and improve the performance and conversion rate of your forms.
uuid: fd2f087c-39f5-457d-8b44-c3ec4400b3fc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: a128877d-239c-4272-99c2-72d6486d5703
docset: aem65
exl-id: 4f45ad22-611b-4b4f-8e89-cb64a122b70a
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 0%

---

# 衡量及改善表單的成效和轉換{#measure-and-improve-effectiveness-and-conversion-of-forms}

## 挑戰 {#the-challenge-br}

組織日益增強能力，鼓勵客戶跨多個管道使用數位自助服務進行交易。 但是，在缺乏一對一的意見反應機制的情況下，要評估成功並嘗試數位表格來改善客戶體驗並提高轉換率變得很有挑戰性。

為了最大化ROI，組織必須監控客戶與服務的互動方式，並實驗使用他們的數位成品（表單）以增強客戶體驗。 為了衡量成功和定義改善策略，組織需要獲得以下問題的答案：

* 有多少客戶嘗試存取或處理我的表單？
* 其中有多少人成功完成交易？
* 其中有多少人捨棄此表單？
* 客戶面臨問題的問題區域為何？
* 我帶來了哪些變更，以及要如何測試哪些變更會帶來更好的轉換？

## 解決方案 {#the-solution}

AEM Forms整合 [Adobe Marketing Cloud](https://www.adobe.com/marketing-cloud.html) 解決方案 —  [Adobe Analytics](https://www.adobe.com/marketing-cloud/web-analytics.html) 和 [Adobe Target](https://www.adobe.com/marketing-cloud/testing-targeting.html)  — 可協助您監控及分析表單的執行狀況，並可讓您實驗及識別帶來更佳轉換率的體驗。

## 工作流程 {#the-workflow}

讓我們來詳細瞭解如何測量效能及改善表單的轉換率。

### 目標對象 {#target-audience}

* 負責行銷策略及成功的業務使用者和分析人員
* 負責基礎結構和解決方案設定與維護的IT人員

### 涉及的AEM Forms元件和功能 {#aem-forms-components-and-features-involved}

* 調適型表單
* 與Adobe Analytics整合，以收集、整理和報告客戶與您的最適化表單的互動
* 與Adobe Target整合，執行最適化表單的A/B測試

### 假設 {#assumptions}

* 您已擁有Adobe Marketing Cloud帳戶並註冊Analytics和Target解決方案。
* 您有已發佈的最適化表單可供客戶存取。

### 工作流程步驟 {#workflow-steps}

#### 步驟1：在AEM Forms中設定Analytics和Target  {#step-configure-analytics-and-target-in-aem-forms-br}

**設定 Analytics**

若要深入瞭解客戶與表單的互動，您必須先在AEM Forms中設定Analytics。 執行下列步驟：

1. 在Adobe Analytics中建立報表套裝
1. 在AEM中建立雲端服務設定
1. 在AEM中建立雲端服務架構
1. 在AEM中設定AEM Forms Analytics設定服務
1. 在AEM中對表單啟用分析

如需詳細步驟，請參閱 [為最適化表單設定分析和報表](../../forms/using/configure-analytics-forms-documents.md).

**設定Target**

若要針對最適化表單建立並執行A/B測試，請依照中的說明在AEM Forms中設定Target [在AEM Forms中設定並整合Target](../../forms/using/ab-testing-adaptive-forms.md#p-set-up-and-integrate-target-in-aem-forms-p).

#### 步驟2：檢視分析報表 {#step-view-analytics-report-br}

當您的客戶存取您已啟用Analytics的表單並與之互動時，其互動會被擷取到高度安全的Analytics資料庫中。 資料庫會依使用者端分段，並可透過安全連線存取。

您可以針對啟用Analytics的表單從AEM內檢視報表，並分析資料。 若要檢視報表，請執行下列動作：

1. 在AEM伺服器上，導覽至 **Forms > Forms與檔案**.
1. 選取您要為其建立分析報表的表單。
1. 按一下「Analytics報表」圖示。 報表隨即顯示。

讓我們看看Analytics為表單收集和報告的資料點。

**Forms分析報表**

適用性表單的分析報表可擷取表單層級的下列關鍵績效指標(KPI)：

* **平均填充時間**：填寫表單所花的平均時間
* **曝光數**：表單出現在搜尋結果中的次數

* **轉譯**：表單已轉譯或開啟的次數
* **草稿**：表單儲存為草稿的次數

* **提交內容**：已提交表單的次數
* **中止**：使用者未完成表單而離開的次數
* **瀏覽/提交**：每次提交的造訪比率

此外，您會取得表單中每個面板的下列詳細資料：

* **時間**：面板及其欄位上的平均逗留時間（秒）

* **錯誤**：每1000個表單轉譯在面板及其欄位上遇到的錯誤數

* **說明**：使用者每1000個表單轉譯存取面板及其欄位內容說明的次數

![最適化表單的分析報表範例](assets/summary-report.png)

如需Forms Analytics報表的詳細資訊，請參閱 [檢視和瞭解AEM Forms analytics報表](../../forms/using/view-understand-aem-forms-analytics-reports.md).

>[!NOTE]
>
>您可以透過Adobe Marketing Cloud上的Analytics帳戶，檢視詳細報表，並深入瞭解客戶及其與您表單的互動。

#### 步驟3：分析資料點 {#step-analyze-data-points}

在此步驟中，您將分析分析分析報表中的資料點，並推斷表單的執行方式。 如果不符合您的成功KPI，您將根據資料建構假設，並尋找可能的解決方案以修正問題。 例如：

* 如果表單的平均填寫時間高於預期，表示您的表單可能比較複雜，客戶可能難以理解、表單未使用標準術語、表單太長等等。 在這種情況下，您可能想要簡化表單結構和欄位、重新設計表單設計、縮短表單長度，或為非標準表單欄位新增說明說明和範例。
* 如果資料指出大部分客戶正在存取表單面板的說明，很明顯客戶對於要填寫的資訊感到困惑。 您可能會想要使用替代術語，或為該面板新增一些範例輸入和說明說明。
* 如果表單的中止或放棄率高於預期，可能是由於表單轉譯時間過長、客戶無意中登陸表單或過於複雜所致。 在此情況下，您可能想要最佳化搜尋結果中顯示的表單說明、簡化表單、最佳化表單以加快載入速度等。

分析完這些資料點並得出假設後，請在表單中進行所需的變更。

#### 步驟4：驗證您的分析和修正 {#step-validate-your-analysis-and-fixes}

在此步驟中，您將驗證您在表單中所做的變更，並驗證它是否會影響轉換率。

**執行A/B測試**

AEM Forms與Target的整合可建立最適化表單的A/B測試。 在A/B測試中，您會即時隨機向客戶呈現表單的不同體驗，以瞭解哪些體驗效果更好或導致更多轉換。 一旦您擁有重要資料，指出某個體驗所提供的轉換率優於另一個體驗，您就可以宣告該體驗為獲勝者，並且隨著時間推移，該體驗會成為所有客戶都可見的預設體驗。

如需為最適化表單建立A/B測試的詳細資訊，請參閱 [最適化表單的A/B測試](../../forms/using/ab-testing-adaptive-forms.md).

![最適化表單的A/B測試摘要報告範例](assets/ab-test-report-4.png)

## 最佳做法 {#best-practices}

真正的最佳實務是您在執行此工作流程時自我識別的最佳實務。 它們是您的環境和需求所特有的。 透過工作流程擷取您的學習，並將其記錄為最佳實務。

以下是有關設計表單及執行A/B測試的一些建議：

**Forms設計**

* 保持表單簡單、簡短且易於瀏覽。 使用方向提示進行導覽。
* 使用表單欄位的標準或常用術語。
* 透過範例或說明說明說明欄位和所需的輸入，使用者可能會對此感到困惑。
* 儘可能驗證輸入的使用者輸入，以避免表單提交錯誤。
* 最佳化桌上型電腦和行動裝置的版面配置。
* 自動填入已知使用者的資訊。

**A/B測試**

* 在執行A/B測試之前建構假設並識別成功量度。
* 在您的替代體驗中執行最小的變數（最好一次一個變數），以瞭解影響轉換率的因素。
* 經常測試以消除低效率。
