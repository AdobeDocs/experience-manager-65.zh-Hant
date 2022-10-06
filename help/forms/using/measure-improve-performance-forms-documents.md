---
title: 測量並改善表單的效用和轉換
seo-title: Measure and improve effectiveness and conversion of forms
description: AEM Forms與Adobe Target和Adobe Analytics解決方案整合，可讓您測量並改善表單的效能和轉換率。
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

# 測量並改善表單的效用和轉換{#measure-and-improve-effectiveness-and-conversion-of-forms}

## 挑戰 {#the-challenge-br}

組織正日益增強其能力，並鼓勵客戶使用跨多個管道的數位自助服務進行交易。 然而，如果沒有一對一的意見回饋機制，測量成功並試驗數位表單以增強客戶體驗並提高轉換率就變得十分困難。

為了實現最大的投資回報，組織必須監控其客戶與服務的交互方式，並試驗其數字成品（表單）以增強客戶體驗。 為了衡量成功並定義改進策略，組織需要回答以下問題：

* 有多少客戶嘗試使用我的表單存取或處理？
* 其中有多少人成功完成了交易？
* 有多少人放棄了表格？
* 客戶面臨問題的問題領域是什麼？
* 我要帶入哪些變更，以及如何測試什麼會造成更好的轉換？

## 解決方案 {#the-solution}

AEM Forms整合 [Adobe Marketing Cloud](https://www.adobe.com/marketing-cloud.html) 解決方案 —  [Adobe Analytics](https://www.adobe.com/marketing-cloud/web-analytics.html) 和 [Adobe Target](https://www.adobe.com/marketing-cloud/testing-targeting.html)  — 可協助您監控和分析表單的執行情形，並讓您試驗和識別可帶來更高轉換率的體驗。

## 工作流程 {#the-workflow}

讓我們詳細了解您如何測量效能並改善表單的轉換率。

### 目標對象 {#target-audience}

* 負責行銷策略與成功的業務使用者和分析人員
* 負責基礎架構和解決方案設定與維護的IT人員

### AEM Forms元件和相關功能 {#aem-forms-components-and-features-involved}

* 調適型表單
* 與Adobe Analytics整合，以收集、組織和報告客戶與最適化表單的互動
* 與Adobe Target整合，執行最適化表單的A/B測試

### 假設 {#assumptions}

* 您已有Adobe Marketing Cloud帳戶，且已註冊Analytics和Target解決方案。
* 您有已發佈的最適化表單，客戶可以存取。

### 工作流程步驟 {#workflow-steps}

#### 步驟1:在AEM Forms中設定Analytics和Target  {#step-configure-analytics-and-target-in-aem-forms-br}

**設定 Analytics**

若要深入了解客戶與表單的互動，您必須先在AEM Forms中設定Analytics。 執行下列步驟：

1. 在Adobe Analytics中建立報表套裝
1. 在AEM中建立雲端服務設定
1. 在AEM中建立雲端服務架構
1. 在AEM中設定AEM Forms Analytics設定服務
1. 在AEM的表單上啟用analytics

如需詳細步驟，請參閱 [為最適化表單設定分析和報表](../../forms/using/configure-analytics-forms-documents.md).

**設定Target**

若要建立並執行適用性表單的A/B測試，請依照 [在AEM Forms中設定和整合Target](../../forms/using/ab-testing-adaptive-forms.md#p-set-up-and-integrate-target-in-aem-forms-p).

#### 步驟2:檢視分析報表 {#step-view-analytics-report-br}

當您的客戶存取並與已啟用Analytics的表單互動時，其互動會擷取到高度安全的Analytics資料庫中。 資料庫由客戶端分段，並可通過安全連接訪問。

您可以從AEM中檢視報表，以取得啟用分析的表單並分析資料。 若要檢視報表：

1. 在AEM伺服器上，導覽至 **Forms > Forms與檔案**.
1. 選取您要其分析報表的表單。
1. 按一下「Analytics報表」圖示。 報表隨即顯示。

讓我們來看看Analytics收集的資料點，以及針對表單製作報表。

**Forms analytics報表**

適用性表單的分析報表會在表單層級擷取下列關鍵績效指標(KPI):

* **平均填充時間**:填寫表單的平均逗留時間
* **曝光數**:表單出現在搜尋結果中的次數

* **轉譯**:表單呈現或開啟的次數
* **草稿**:表單已儲存為草稿的次數

* **提交**:提交表單的次數
* **中止**:使用者未填妥表單就離開的次數
* **瀏覽/提交**:每次提交的造訪率

此外，您還可在表單中取得每個面板的下列詳細資料：

* **時間**:面板及其欄位上的平均逗留時間（秒數）

* **錯誤**:每1000個表單轉譯在面板及其欄位上遇到的錯誤數

* **說明**:每1000個表單轉譯中，使用者存取面板及其欄位的內容說明的次數

![最適化表單的分析報表範例](assets/summary-report.png)

如需表單分析報表的詳細資訊，請參閱 [檢視及了解AEM Forms分析報表](../../forms/using/view-understand-aem-forms-analytics-reports.md).

>[!NOTE]
>
>您可以在Adobe Marketing Cloud上的Analytics帳戶中，檢視詳細報表，並深入了解客戶及其與表單的互動。

#### 步驟3:分析資料點 {#step-analyze-data-points}

在此步驟中，您將分析分析報表中的資料點，並推斷表單的執行方式。 如果它不符合您的成功KPI，您將會根據資料建立假設，並尋找可能的解決方案來修正問題。 例如：

* 如果表單的平均填寫時間高於預期，則您的表單可能會很複雜，讓客戶了解，表單不使用標準術語，表單太長，以此類推。 在這種情況下，您可能希望簡化表單結構和欄位、重新工作表單設計、縮短表單長度，或為非標準表單欄位添加幫助說明和示例。
* 如果資料指出大部分客戶都在存取表單面板的說明，顯然客戶對要填入的資訊感到困惑。 您可能想要使用替代術語，或為該面板新增一些範例輸入和說明說明。
* 如果表單的中止或放棄率高於預期，可能是因為表單需要很長時間才能呈現、客戶無意中登陸表單，或表單太複雜。 在這種情況下，您可能希望優化搜索結果中顯示的表單說明、簡化表單、優化表單以加快載入速度等。

分析這些資料點並得出假設後，請在表單中進行必要的變更。

#### 步驟4:驗證分析和修正 {#step-validate-your-analysis-and-fixes}

在此步驟中，您將驗證您在表單中所做的變更，並確認其是否影響轉換率。

**執行A/B測試**

AEM Forms與Target的整合可建立最適化表單的A/B測試。 在A/B測試中，您會隨機即時向客戶呈現不同的表單體驗，以了解哪個體驗更有效或導致更多轉換。 一旦您有重要資料指出某個體驗提供的轉換比另一個體驗更好，您就可以宣告該體驗為獲勝者，而隨後，它將成為所有客戶皆可看到的預設體驗。

如需針對適用性表單建立A/B測試的詳細資訊，請參閱 [適用性表單的A/B測試](../../forms/using/ab-testing-adaptive-forms.md).

![最適化表單A/B測試的範例摘要報表](assets/ab-test-report-4.png)

## 最佳實務 {#best-practices}

真正的最佳實務是您在執行此工作流程時自行識別的實務。 它們與您的環境和需求不同。 透過工作流程擷取您的學習成果，並將其記錄為最佳實務。

有關設計表單和執行A/B測試的建議如下：

**Forms設計**

* 使表單簡單、簡短且易於導覽。 使用方向提示進行導覽。
* 對表單欄位使用標準或通用術語。
* 透過範例或說明說明欄位和必要的輸入，說明使用者可能會混淆。
* 盡可能在使用者輸入內容時驗證其輸入內容，以避免表單提交時發生錯誤。
* 最佳化案頭和行動裝置的配置。
* 自動填入已知使用者的資訊。

**A/B測試**

* 執行A/B測試前，請先建立假設並識別成功量度。
* 在替代體驗中盡量減少變異（最好一次一個），以了解影響轉換率的因素。
* 經常測試以消除低效。
