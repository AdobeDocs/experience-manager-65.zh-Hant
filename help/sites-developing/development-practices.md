---
title: 開發實務
description: 在Adobe Experience Manager上進行開發的最佳實務。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 65b2029e-03c9-4df4-8579-2b15dbee1035
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# 開發實務{#development-practices}

## 根據完成定義(DoD)的工作 {#work-according-to-a-definition-of-done}

每個團隊對「完成」的意思都有不同的定義，但重要的是要有一個定義，並確保劇本在被接受前符合定義的標準。

團隊通常指定的某些條件包括：

* 已檢閱程式碼以設定格式
* 已新增評論/Javadoc
* 符合必要的測試涵蓋範圍
* 通過單位和整合測試
* 已在QA環境中驗證
* 已實施本地化

如果沒有定義明確的DoD，很容易發生許多事情已進行到一半，而沒有任何真正完成的情況。

### 定義並遵守編碼和格式慣例 {#define-and-adhere-to-coding-and-formatting-conventions}

縮排層級和空白字元這類專案可能並不重要，但擁有正確格式化的程式碼可大幅提升可讀性和可維護性。 應以團隊的形式討論並同意慣例，然後在程式碼中遵循。

### 目標為高測試涵蓋率  {#aim-for-high-test-coverage}

隨著專案實作的大小增加，測試所需的時間也會隨之增加。 如果沒有良好的測試涵蓋範圍，測試團隊就無法擴展，開發人員最終會被埋沒在漏洞之中。

開發人員應該練習測試驅動開發(TDD)，在滿足其需求的生產計畫碼之前編寫失敗的單元測試。 QA應建立一組自動化的驗收測試，以確保系統可如預期般從高層次運作。

有可用的自訂架構（例如Jackalope和Prosper），可讓您更輕鬆地模擬JCR API，以確保開發人員在撰寫單元測試時的生產力。

### 保持示範就緒 {#stay-demo-ready}

系統應在每個反複專案結束時提供給企業展示。 透過讓系統保持為示範就緒狀態，團隊將始終處於生產就緒的迭代中，並且可以將技術債務保持在可維護的級別。

### 實作持續整合環境並加以使用 {#implement-a-continuous-integration-environment-and-use-it}

實作持續整合環境可讓您輕鬆且重複地執行單元測試和整合測試。 它也會將部署與開發團隊分離，讓團隊的其他部分更有效率，並促成更穩定和可預測的部署。

### 藉由降低建置時間，讓開發週期保持快速 {#keep-the-development-cycle-fast-by-keeping-build-times-low}

如果單元測試需要很長時間才能執行，開發人員會避免執行，而且會失去其價值。 如果建置程式碼和部署程式碼需要很長時間，人們會比較少這樣做。 將短期建置時間列為優先要務，可確保您投資於測試涵蓋範圍和CI基礎建設的時間能持續讓團隊提高生產力。

### 微調Sonar和其他靜態程式碼分析工具，並對其報告採取行動 {#fine-tune-sonar-and-other-static-code-analysis-tools-and-act-on-their-reports}

程式碼分析工具可能很有價值，但前提是其報表會導致開發團隊採取行動。 若不微調這些工具所提供的分析，這些工具所產生的建議就會變得無關緊要，並失去其價值。

### 遵循男孩Scout規則 {#follow-the-boy-scout-rule}

「男孩」Scout有一個規則：「不要比原來發現更好。」 只要開發團隊的所有成員都遵守此規則，並在遇到問題時進行清理，程式碼就會持續改善。

### 避免實作YAGNI功能 {#avoid-implementing-yagni-features}

YAGNI (You Won&#39;t Need It)功能是我們預期未來會需要某樣東西時所實作的功能，即使我們現在不需要。 在理想狀況下，我們應該實作目前最簡單的工作方式，並使用持續重構，以確保系統的架構會隨著需求演化。 這可讓我們專注於重要事項，並防止程式碼膨脹和特徵潛移。
