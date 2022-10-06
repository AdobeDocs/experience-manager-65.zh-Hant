---
title: 開發實務
seo-title: Development Practices
description: 在AEM上開發的最佳作法
seo-description: Best practices for developing on AEM
uuid: 27a75f7f-6e2c-4113-9e9f-c5013a4594c2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8b0297a1-d922-410f-9aaf-3a6b87e11dc0
exl-id: 65b2029e-03c9-4df4-8579-2b15dbee1035
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 0%

---

# 開發實務{#development-practices}

## 根據完成的定義工作 {#work-according-to-a-definition-of-done}

每個團隊對「完成」的含義有不同的定義，但有一個定義並確保故事在被接受之前符合定義的標準非常重要。

團隊通常會指定的某些條件包括：

* 已審核格式的代碼
* 添加了注釋/Javadoc
* 滿足要求的測試覆蓋級別
* 通過單位和整合測試
* 在QA環境中驗證
* 已實作本地化

如果沒有定義明確的DoD，很容易在這樣一種情況下結束：許多事情都做到了一半，但什麼也沒有真正完成。

### 定義並遵守編碼和格式慣例 {#define-and-adhere-to-coding-and-formatting-conventions}

縮排層級和空白字元之類的內容似乎並不重要，但適當格式化的程式碼有助於提高可讀性和可維護性。 應以團隊身份討論並同意各項公約，然後在規則中加以遵循。

### 針對高測試覆蓋  {#aim-for-high-test-coverage}

隨著專案實作的規模增加，測試所需的時間也會增加。 如果測試覆蓋率不高，測試團隊將無法擴展，開發人員最終將陷入錯誤之中。

開發人員應該練習TDD，在生產代碼滿足其要求之前編寫失敗的單元測試。 QA應建立一組自動的接受測試，以確保系統從高層級正常運作。

有自訂架構可供使用，例如Jackalope和Prosper，讓對JCR API的嘲弄更簡單，以確保開發人員在編寫單元測試時能有效率。

### 保持演示就緒 {#stay-demo-ready}

系統應可在每次迭代結束時向企業演示。 將系統保持在可演示的狀態，團隊將始終處於可生產就緒的迭代過程中，並且技術負債可保持在可維護的級別。

### 實作持續整合環境並加以使用 {#implement-a-continuous-integration-environment-and-use-it}

實施連續整合環境可讓您輕鬆、重複地執行單元測試和整合測試。 它還將部署與開發團隊脫鈎，使團隊的其他部分更高效，並使部署更穩定、更可預測。

### 通過保持建置時間低來快速保持開發週期 {#keep-the-development-cycle-fast-by-keeping-build-times-low}

如果單元測試需要很長的時間才能執行，開發人員將避免執行，而且會失去其價值。 如果建立和部署程式碼需要很長時間，人們的執行頻率就會降低。 將縮短構建時間作為優先事項，可確保我們投入測試覆蓋和CI基礎架構的時間將繼續使團隊更高效。

### 微調聲納和其他靜態代碼分析工具，並對其報告採取行動 {#fine-tune-sonar-and-other-static-code-analysis-tools-and-act-on-their-reports}

程式碼分析工具可能很有價值，但唯有在其報表導致開發團隊採取動作時，才能如此。 若不微調這些工具所提供的分析，它們產生的建議將不相關，而會失去其價值。

### 遵循男孩Scout規則 {#follow-the-boy-scout-rule}

男孩Scout有一個規則：「留下比你找到的好。」 只要開發團隊的所有成員都遵守這項規則，在遇到麻煩時收拾東西，程式碼就會不斷改進。

### 避免實作YAGNI功能 {#avoid-implementing-yagni-features}

YAGNI（或You&#39;t Not Need It）功能是當我們預期未來需要某些東西時（即使我們現在不需要它）實施的。 理想情況下，我們應該實施當今最簡單的工作，並使用連續重構來確保系統的體系結構隨著時間的需求而不斷演化。 這可讓我們專注於重要事項，並防止程式碼膨脹和功能蠕變。
