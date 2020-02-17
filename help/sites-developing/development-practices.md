---
title: 開發實務
seo-title: 開發實務
description: 在AEM上開發的最佳實務
seo-description: 在AEM上開發的最佳實務
uuid: 27a75f7f-6e2c-4113-9e9f-c5013a4594c2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8b0297a1-d922-410f-9aaf-3a6b87e11dc0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 開發實務{#development-practices}

## 根據完成的定義工作 {#work-according-to-a-definition-of-done}

每個團隊對「完成」的含義有不同的定義，但在被接受之前，必須先有一個團隊，並確保故事符合定義的標準。

團隊通常指定的某些標準包括：

* 已檢閱格式設定的程式碼
* 已添加註釋/Javadoc
* 符合所需的測試涵蓋範圍等級
* 通過單元和整合測試
* 在QA環境中驗證
* 實作本地化

沒有明確定義的DoD，就很容易在事情半途而廢的情況下結束。

### 定義並遵守編碼和格式設定慣例 {#define-and-adhere-to-coding-and-formatting-conventions}

縮排等級和空白字元可能並不重要，但正確格式化的程式碼可大幅提升可讀性和可維護性。 應以團隊的身分討論並同意公約，然後在規則中加以遵循。

### 針對高測試覆蓋率 {#aim-for-high-test-coverage}

隨著專案實作的規模增加，測試所需的時間也會增加。 如果沒有良好的測試覆蓋，測試團隊將無法進行擴展，開發人員最終將陷入漏洞之中。

開發人員應練習TDD，在生產代碼滿足要求之前編寫失敗的單元測試。 QA應建立一組自動驗收測試，以確保系統在高層正常運作。

有自訂的架構，例如Jackalope和Prosper，可讓對JCR API的嘲弄更簡單，以確保開發人員在編寫單元測試時的生產力。

### 隨時準備示範 {#stay-demo-ready}

在每次迭代結束時，系統應該可供業務演示。 通過使系統保持在演示就緒狀態，團隊將始終處於生產就緒狀態的迭代過程中，技術負擔將保持在可維護的水準。

### 建置持續整合環境並加以使用 {#implement-a-continuous-integration-environment-and-use-it}

實施連續的整合環境可讓您輕鬆且重複地執行單元測試和整合測試。 它還將使部署與開發團隊脫鈎，使團隊的其他部分更高效，並使部署更穩定、更可預測。

### 將建置時間維持在較低水準，以快速維持開發週期 {#keep-the-development-cycle-fast-by-keeping-build-times-low}

如果單元測試需要很長時間才能執行，開發人員將避免執行這些測試，而且會失去價值。 如果建立和部署程式碼需要很長時間，人們就不會這麼做。 將縮短建置時間作為優先事項，可確保我們投入測試範圍和CI基礎架構的時間，繼續讓團隊提高生產力。

### 微調聲納和其他靜態程式碼分析工具，並依其報告採取行動 {#fine-tune-sonar-and-other-static-code-analysis-tools-and-act-on-their-reports}

程式碼分析工具可能很有價值，但前提是其報告必須讓開發團隊採取行動。 如果不微調這些工具提供的分析，它們產生的建議將不相關，而會失去價值。

### 遵循童子軍規則 {#follow-the-boy-scout-rule}

童子軍有一條規矩：「留下比你找到的要好。」只要開發團隊的所有成員都遵守這項規則，在遇到麻煩時加以清理，程式碼就會不斷改進。

### 避免實作YAGNI功能 {#avoid-implementing-yagni-features}

YAGNI（或You&#39;rent Not Need It）功能是當我們預期未來需要某些東西時（即使我們現在不需要它）實作的。 理想情況下，我們應該實施目前最簡單的操作，並使用持續重構功能來確保系統的體系結構隨著時間的變化而不斷變化。 這可讓我們專注在重要事項上，並防止程式碼膨脹和功能變得蠕變。
