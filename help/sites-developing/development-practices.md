---
title: 開發實踐
seo-title: Development Practices
description: 開發的最佳做AEM法
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

# 開發實踐{#development-practices}

## 根據完成的定義進行工作 {#work-according-to-a-definition-of-done}

每個團隊對「完成」的含義有不同的定義，但重要的是要有一個，並確保一個故事在被接受之前符合定義的標準。

團隊通常指定的一些標準包括：

* 已檢查格式的代碼
* 添加了注釋/Javadoc
* 滿足所需的test覆蓋級別
* 刀路單元和整合test
* 在QA環境中驗證
* 本地化已實現

如果沒有一個定義明確的DoD，很容易最終出現這樣的局面：許多事情都半途而廢，而且沒有真正的完成。

### 定義並遵守編碼和格式約定 {#define-and-adhere-to-coding-and-formatting-conventions}

縮進級別和空白空間等內容似乎並不重要，但正確格式化的代碼大大提高了可讀性和可維護性。 公約應作為一個小組討論並商定，然後在規則中加以遵守。

### 高test覆蓋率  {#aim-for-high-test-coverage}

隨著項目實施規模的增長，test它所需的時間也會增長。 如果沒有良好的test覆蓋，測試團隊將無法擴展，開發人員最終將陷入蟲洞。

開發人員應該實行TDD，在滿足他們要求的生產代碼之前寫下失敗的單位test。 QA應建立一套自動驗收test，以確保系統從高級別按預期工作。

現有的定製框架（如Jackalope和Prosper）可簡化對JCR API的嘲弄，以確保開發人員的工作效率，同時編寫單元test。

### 準備演示 {#stay-demo-ready}

系統應在每次迭代結束時提供給業務演示。 通過使系統保持為演示就緒狀態，團隊將始終處於生產就緒的迭代內，而技術負債可保持在可維護的水準。

### 實施連續整合環境並使用它 {#implement-a-continuous-integration-environment-and-use-it}

實施連續整合環境將使您能夠輕鬆、可重複地運行設備test和整合test。 它還將部署與開發團隊脫鈎，使團隊的其他部分更高效，並使部署更穩定、更可預測。

### 通過保持低建設時間而快速保持開發週期 {#keep-the-development-cycle-fast-by-keeping-build-times-low}

如果單位test需要很長時間才能運行，開發商將避免運行這些設備，而它們將失去價值。 如果構建和部署代碼需要很長時間，人們就不會那麼頻繁地這樣做。 將縮短構建時間作為優先事項，可確保我們在test覆蓋和CI基礎架構方面投入的時間將繼續提高團隊的工作效率。

### 精調聲納和其他靜態代碼分析工具並對其報告採取行動 {#fine-tune-sonar-and-other-static-code-analysis-tools-and-act-on-their-reports}

代碼分析工具可能很有價值，但前提是其報告導致開發團隊採取行動。 如果不對這些工具提供的分析進行微調，這些工具產生的建議將不相關，並將失去其價值。

### 遵循男孩Scout規則 {#follow-the-boy-scout-rule}

男孩Scout有一條規則：&quot;留得比你找到的好。&quot; 只要開發團隊的所有成員都遵守這一規則，在遇到混亂時收拾東西，代碼就會不斷改進。

### 避免實施YAGNI功能 {#avoid-implementing-yagni-features}

YAGNI（或者您不需要它）功能是當我們期望將來需要某種東西時實施的，即使我們現在不需要它。 理想情況下，我們應該實施目前最簡單的操作，並使用連續重構來確保系統的體系結構隨著需求的發展而發展。 這將使我們能夠專注於重要事項，並防止代碼漏洞和特徵蠕變。
