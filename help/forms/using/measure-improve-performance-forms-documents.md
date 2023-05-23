---
title: 衡量和改進表格的效力和轉換
seo-title: Measure and improve effectiveness and conversion of forms
description: AEM Forms與Adobe Target和Adobe Analytics解決方案整合，使您能夠測量和改進表單的效能和轉換率。
seo-description: AEM Forms integrates with Adobe Target and Adobe Analytics solutions that allows you to measure and improve the performance and conversion rate of your forms.
uuid: fd2f087c-39f5-457d-8b44-c3ec4400b3fc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: a128877d-239c-4272-99c2-72d6486d5703
docset: aem65
exl-id: 4f45ad22-611b-4b4f-8e89-cb64a122b70a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 0%

---

# 衡量和改進表格的效力和轉換{#measure-and-improve-effectiveness-and-conversion-of-forms}

## 挑戰 {#the-challenge-br}

企業正日益增強能力並鼓勵其客戶跨多個渠道使用數字自助服務進行交易。 然而，如果沒有一對一的反饋機制，衡量成功和嘗試數字表單以增強客戶體驗並增加轉換就變得十分困難。

為了實現最大投資回報，企業必須監控其客戶如何與服務進行交互，並試用其數字工件（表單）以增強客戶體驗。 要衡量成功並定義改進策略，組織需要回答以下問題：

* 有多少客戶嘗試訪問或處理我的表單？
* 其中有多少成功完成了交易？
* 有多少人放棄了表格？
* 客戶面臨哪些問題？
* 我將帶來哪些更改，如何test哪些因素可使轉換更好？

## 解決方案 {#the-solution}

AEM Forms整合 [Adobe Marketing Cloud](https://www.adobe.com/marketing-cloud.html) 解決方案 —  [Adobe Analytics](https://www.adobe.com/marketing-cloud/web-analytics.html) 和 [Adobe Target](https://www.adobe.com/marketing-cloud/testing-targeting.html)  — 可幫助您監控和分析表單的運行情況，並讓您能夠嘗試和識別能夠帶來更好轉換率的體驗。

## 工作流 {#the-workflow}

讓我們深入瞭解您如何衡量表單的效能和提高轉換率的詳細資訊。

### 目標受眾 {#target-audience}

* 負責營銷策略和成功的業務用戶和分析員
* 負責基礎架構和解決方案設定和維護的IT人員

### AEM Forms元件和涉及的功能 {#aem-forms-components-and-features-involved}

* 調適型表單
* 與Adobe Analytics整合以收集、組織和報告與您自適應表單的客戶交互
* 與Adobe Target整合以運行A/Btest以適應形式

### 假設 {#assumptions}

* 您已經擁有Adobe Marketing Cloud帳戶並註冊了分析和目標解決方案。
* 您有一個已發佈的自適應表單，客戶可以訪問該表單。

### 工作流步驟 {#workflow-steps}

#### 步驟1:在AEM Forms配置分析和目標  {#step-configure-analytics-and-target-in-aem-forms-br}

**設定 Analytics**

要深入瞭解客戶與表單的交互，您需要首先在AEM Forms配置分析。 執行以下步驟：

1. 在Adobe Analytics建立報告套件
1. 在中建立雲服務配AEM置
1. 在中建立雲服務框架AEM
1. 在中配置AEM Forms分析配置服AEM務
1. 在中啟用窗體分析AEM

有關詳細步驟，請參見 [為自適應表單配置分析和報告](../../forms/using/configure-analytics-forms-documents.md)。

**配置目標**

要為自適應表單建立和運行A/Btest，請按照中所述在AEM Forms配置目標 [在AEM Forms建立和整合目標](../../forms/using/ab-testing-adaptive-forms.md#p-set-up-and-integrate-target-in-aem-forms-p)。

#### 步驟2:查看分析報告 {#step-view-analytics-report-br}

當您的客戶訪問啟用了Analytics的表單並與其交互時，它們的交互會在高度安全的Analytics資料庫中捕獲。 資料庫由客戶機分段，並可通過安全連接訪問。

您可以從內部查看啟用分析AEM的表單和分析資料的報表。 要查看報表，請執行以下操作：

1. 在服AEM務器上，導航到 **Forms>Forms和文檔**。
1. 選擇要為其生成分析報告的表單。
1. 按一下分析報告表徵圖。 顯示報告。

讓我們看一下分析收集的資料點和報告表單。

**Forms分析報告**

自適應表單的分析報告在表單級別捕獲以下關鍵績效指標(KPI):

* **平均填充時間**:填寫表單所花的平均時間
* **印象**:表單在搜索結果中出現的次數

* **格式副本**:表單已呈現或開啟的次數
* **草稿**:表單保存為草稿的次數

* **提交**:已提交表單的次數
* **中止**:用戶未完成表單而離開的次數
* **訪問/提交**:每次提交的訪問率

此外，您還可以在表單中獲得有關每個面板的以下詳細資訊：

* **時間**:在面板及其欄位上花費的平均時間（秒）

* **錯誤**:每1000個格式副本在面板及其欄位上遇到的錯誤數

* **幫助**:每1000個格式副本中用戶訪問面板及其欄位的上下文幫助的次數

![自適應表單的示例分析報告](assets/summary-report.png)

有關表單分析報表的詳細資訊，請參閱 [查看和瞭解AEM Forms分析報告](../../forms/using/view-understand-aem-forms-analytics-reports.md)。

>[!NOTE]
>
>您可以從Adobe Marketing Cloud的分析帳戶查看詳細報告並深入瞭解客戶及其與表單的交互。

#### 第3步：分析資料點 {#step-analyze-data-points}

在此步驟中，您將分析分析報告中的資料點並推斷表單的執行方式。 如果它不滿足您成功的KPI要求，您將根據資料構建假設，並找到可能的解決方案來解決問題。 例如：

* 如果表單的平均填充時間高於您的預期，則表單可能會很複雜，讓客戶瞭解，表單不使用標準術語，表單太長，等等。 在這種情況下，您可能希望簡化表單結構和欄位，重新編寫表單設計，縮短表單長度，或為非標準表單域添加幫助說明和示例。
* 如果資料表明大多數客戶正在訪問表單面板的幫助資訊，則很明顯客戶對要填寫的資訊感到困惑。 您可能希望使用備用術語或為該面板添加一些示例輸入和幫助說明。
* 如果表單的中止或放棄率高於預期，則可能是由於表單需要較長的渲染時間，客戶無意中在表單上著陸，或者它太複雜。 在這種情況下，您可能希望優化搜索結果中顯示的表單說明、簡化表單、優化表單以加快載入速度等。

分析這些資料點並得出假設後，在表單中進行所需的更改。

#### 第4步：驗證分析和修復 {#step-validate-your-analysis-and-fixes}

在此步驟中，您將驗證在表單中所做的更改，並驗證它是否影響折換率。

**運行A/Btest**

將AEM Forms與目標整合，可建立適應形式的A/Btest。 在A/Btest中，您可以即時隨機向客戶展示表單的不同體驗，以瞭解哪些體驗更有效或導致更多轉換。 一旦您有大量資料表明一種體驗比另一種體驗提供更好的轉換，您就可以宣稱這種體驗是贏家，而且向前看，它將成為所有客戶都能看到的預設體驗。

有關為自適應表單建立A/Btest的詳細資訊，請參見 [自適應形式的A/B測試](../../forms/using/ab-testing-adaptive-forms.md)。

![自適應表單的A/Btest摘要報告示例](assets/ab-test-report-4.png)

## 最佳做法 {#best-practices}

真正的最佳做法是在執行此工作流時確定自己的最佳做法。 它們是您的環境和要求所特有的。 通過工作流捕獲您的學習內容，並將其記錄為最佳做法。

有關設計表單和運行A/Btest的建議如下：

**Forms設計**

* 使窗體簡單、短小且易於導航。 使用導航方向提示。
* 將標準術語或通用術語用於表單域。
* 通過示例或幫助解釋欄位和所需輸入，用戶可能會在這些方面感到困惑。
* 盡可能在用戶鍵入時驗證用戶輸入，以避免在提交表單時出錯。
* 優化台式機和移動設備的佈局。
* 自動填充已知用戶的資訊。

**A/Btest**

* 在運行A/Btest之前，構造假設並確定成功度量。
* 在您的備用體驗中盡量減少變化（最好一次一個），以瞭解影響轉換率的因素。
* Test經常消除低效性。
