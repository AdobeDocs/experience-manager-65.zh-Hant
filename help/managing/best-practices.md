---
title: 管理專案 — 最佳實務檢查清單
seo-title: Managing Projects - Best Practices Checklist
description: 管理專案以實作Adobe Experience Manager(AEM)需要規劃和了解。 專案檢查清單是專案傳送的一組最佳實務。 它們指導您完成項目生命週期的所有階段，並提供對您當前狀態的高級監控。
seo-description: Managing a project to implement Adobe Experience Manager (AEM) requires planning and understanding. The Project Checklists are intended as a set of best practices for project delivery. They guide you through all phases of the project life cycle and provide high level monitoring of your current status.
uuid: 859f73f4-535a-49a1-9ae4-a4aacd7f36dd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist, introduction
content-type: reference
discoiquuid: 2bfa287a-aad0-4681-9f9c-d48e8179684c
docset: aem65
exl-id: 94b91996-d2b2-4d4a-b770-334cfa2dc0b7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3264'
ht-degree: 1%

---

# 管理專案 — 最佳實務檢查清單{#managing-projects-best-practices-checklist}

管理要實作Adobe Experience Manager(AEM)的專案，必須要有規劃和了解，才能確保您了解所需要（在實作專案之前和期間）的問題和（相關）決策。

為協助您，最佳實務包括：

* 安 [互動式檢查清單](/help/managing/best-practices-checklist.md) 可讓您透過這些最佳實務來追蹤和監控進度。

   * 根據階段、里程碑和角色定義輸入和交付項。
   * 提供自動概覽（質量、健康和完整性），以指示進度和項目健康。

* 檔案，直接以 [清單](/help/managing/best-practices-checklist.md)，詳細說明：

   * [專案心率](#projectheartbeat) 分析。
   * [按角色的狀態](#status-by-role) 概述。
   * [階段和里程碑](#phases-and-milestones).
   * [關鍵角色](#persona) 並在每個（相關）階段參與。
   * A [字彙表](/help/managing/best-practices-glossary.md) 的 [所需文檔和交付件](#required-documents-and-deliverables).

* [進一步參考](/help/managing/best-practices-further-reference.md) 提供特定區域更多詳情的材料。

## 專案心率控制面板 {#project-heartbeat-dashboard}

此 **專案心率** 工作表提供專案關鍵量度的圖形概觀：

* **相位品質**

   * 指出 [所需文檔和交付件](#required-documents-and-deliverables) 在專案中。

* **階段健康**

   * 項目的高級狀態指標；有助於突出可能面臨風險的領域。

* **階段完整性**

   * 在專案期間的任何時間點，這都表示已針對專案的每個階段完成多少作業。

## 按角色的狀態 {#status-by-role}

此 **按角色的狀態** 工作表顯示詳細的劃分 [**健康**, **品質** 和 **完整性**](#projectheartbeat) by **[階段](#phases-and-milestones)** 和 **[角色](#persona)**.

## 階段和里程碑 {#phases-and-milestones}

項目計劃分為不同的（高級別）階段。

每個階段都包含其自己的里程碑。 針對每個 [角色](#persona) （或角色），將列出相關裡程碑，以及生成定義的交付件所需的文檔。

>[!NOTE]
>
>個別所需文檔和交付件之間沒有直接的1:1關係。

### 準備 {#preparation}

準備專案是整個專案的基礎。 您需要定義關鍵需求，並明確目標和期望：

* **業務邏輯**

   * 開展項目的根本原因和理由。

* **範圍和計畫**

   * 應提供基本範圍和粗略計畫，以定義需要的內容，以及在哪個時間範圍內；如果它有助於澄清情況，您也可以定義範圍之外的內容。

您準備、規劃和運行項目及實施解決方案的方式將受到您在固定預算、固定時間表、內容數量、所需質量等操作限制的影響。

如往常一樣，調整任何因素都會影響其他因素。 例如，縮短時間，但要求相同品質可能會提高價格，同時減少您可以應付的內容數量。 預算往往是關鍵因素，因此這種關係不能被遺忘。

四個因素：

![projectphases_fourphases](assets/projectphases_fourphases.png)

#### 里程碑 {#milestones}

* **驗證**

   在此階段，您需要驗證並確認專案的目標；例如：

   * 您想要達成/提供什麼？
   * 誰會受益？
   * 範圍是什麼？

      * 如果有助於澄清情況，您也可以定義範圍之外的內容。
   * 如何定義成功？
   * 如何衡量成功？
   * 要求、業務和技術是什麼？
   * 是否有要替換的舊系統；如果是，是否有要遷移的資料？
   * 誰會參與？
   * 如何衡量進展？
   * 在項目的生命週期中，您會多久查看進度？


* **預算**

   開始任何專案前，您需要對實作成本進行可靠且切合實際的估計：

   * 使用來自驗證里程碑的資訊作為估計的基礎。
   * 在你的估計中實事求是。
   * 請考慮並遵守客戶可能受到的任何客戶指南、流程或限制。
   * 如果以後需要審查或改進預算，考慮應急和審查程式。
   * 請記住，成本以多種形式產生；購買、使用資源及收費等。

### 規劃 {#planning}

規劃您的專案整合了準備。 在這裡，您需要開始將目標和期望轉化為由具體任務組成的明確路線圖，並受明確溝通的約束，同時要嚴格審查以衡量進展。

#### 里程碑 {#milestones-1}

* **切換**

   乾淨的交接可確保適當的人員/團體了解其在項目中的責任。

   應提供/產生完整詳細資訊，以確保他們全面了解所有相關方面，包括藍圖、範圍、目標、需求和KPI。

* **風險評估**

   為避免令人不快的意外情況，請使用風險評估來識別和量化任何潛在風險及其影響和可能性。

   應在項目生命週期的早期完成這項工作，以確保確定和評估任何效能。 根據調查結果，您可以向利害關係人報告是否可以實施完整要求，並在必要時，是否可以規劃採取和追蹤的適當行動。

* **通訊**

   溝通永遠是任何專案成功的關鍵。 您需要清楚且有效地溝通，以確保每個人都：

   * 努力實現相同的基本目標
   * 從同一資訊庫
   * 具有相同通道

* **啟動**

   啟動會議用於提高對項目正在啟動的認識。 這是一個很好的機會：

   * 邀請所有有關方（或至少團體代表）。
   * 提供有關項目的重要事實。
   * 回答問題。
   * 確保每個人都有相同的知識庫。
   * 讓所有參與者都投入其中 — 這必須贏得。

      * 一旦項目開始時，主要參與者（包括潛在作者）參與進來，您就會增加他們對項目承諾的機會。

### 開發準備 {#development-preparation}

規劃開發是確保項目由具備所需知識的團隊構建在堅實設計的基礎之上的關鍵。

#### 里程碑 {#milestones-2}

* **開發小組人員配備和培訓**

   在開始任何項目之前，您應確保您的開發團隊配備了適當的人員，並且所有團隊成員都接受過相關培訓，以便接受手頭的任務。

* **內容架構**

   內容體系結構定義並描述了內容的未來體系結構；包括：

   * 內容樹；包括資產
   * 基本結構；包括促銷活動等。
   * 多站點和多語言結構（MSM、翻譯等）
   * 支援內容（包括標籤和標籤概念）
   * 快取和內容重複使用策略

* **系統架構**

   系統體系結構定義了系統的概念視圖；包括（包括其他資料）:

   * [系統結構](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) 適用於所有必要環境
   * 子系統
   * 第三方系統
   * 介面；硬體、軟體和人的交互
   * 每個環境的伺服器；請參閱 [技術需求](/help/sites-deploying/technical-requirements.md) 和 [硬體調整指南](/help/managing/hardware-sizing-guidelines.md)

   * 每個環境的流程；例如，部署和維護需求
   * 維護活動（資料存放區GC、TarPM最佳化等）
   * [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) 快取
   * [聚類](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) 發佈/署名共用
   * 用戶端效能（JS縮制、縮圖、css空格、http要求總數等）

* **應用程式架構**

   應用程式體系結構定義並描述了建議應用程式的行為。

   重點在於：

   * 他們如何彼此互動以及與使用者互動。
   * 應用程式使用和生成的資料，而不是其內部結構。

   定義應包括：

   * 專案的基本程式碼結構
   * 程式碼成品（套件、套件等）
   * 範本/元件的劃分及其關係
   * 所需自訂的高階詳細資訊（特定覆蓋稍後會顯示）
   * 設計解決方案所需的工作流程（例如內容建立、核准、發佈、轉換、匯入、匯出等）
   * 對任何複雜模組（例如MSM、商務、第三方整合）進行特別考慮


* **系統整合**

   系統整合需要您規劃（然後實作）:

   * 子系統和 [解決方案整合](/help/sites-administering/integration.md) 將匯集起來，作為一個相干系統運行
   * 如何整合任何第三方系統；連同任何特殊考量，例如離線/線上、用戶端/瀏覽器端或第三方系統故障時的故障處理

* **測試概念**

   在開始開發之前，應先制定一個深入、全面的概念 [測試](/help/sites-developing/planning.md) 專案需求。

   其中應包括：

   * 要執行的所有測試的詳細資訊
   * 準備這些測試所需的任何內容
   * 要使用的任何測試工具的資訊
   * 高級別指示將參與測試的人員；尤其是QA團隊以外的群組
   * 測試自動化的細節；例如，使用Selenium或AEM Developer模式

* **體驗設計**

   外在設計(XD)涉及為您的解決方案設計使用者體驗。

   應針對作者和網站的最終使用者分析和開發使用者體驗。

* **支援設定**

   在開發前，應設定部署、發行、測試和報告問題所需的所有支援流程。

   另請參閱 [Adobe支援入口網站](https://helpx.adobe.com/tw/marketing-cloud/contact-support.html).

### 運營規劃和運營 {#operations-planning-and-operations}

在類似的基礎上，必須正確規劃操作以確保您擁有項目生命週期的所有階段所需的環境。 您還需要適當的程式來維護這些屬性。

#### 里程碑 {#milestones-3}

* **權限**

   您需要針對將使用此解決方案的所有使用者/群組，規劃並實作角色和權限概念。

   例如：

   * 角色清單（即群組），具有 `read`/ `write` 每個

   * 定義影響發佈環境之權限的使用；例如， `replicate`
   * 對於具有最低權限的使用者，應定義工作流程
   * 中的使用者 `editor` 組不應 `admin` 權利或是 `administrators` 群組

   如需詳細資訊，請參閱 [使用者管理與安全性](/help/sites-administering/security.md).

* **監控與維護**

   監控和維護是確保解決方案上線後順利運作的關鍵環節。 為此，您需要定義：

   * 需要監控的內容
   * 維護任務；常用和特殊情況

   另請參閱 [監控與維護](/help/sites-deploying/monitoring-and-maintaining.md) 以取得更多資訊。

* **移轉**

   應審核並驗證來自舊版系統的任何內容，以便遷移。

* **恢復計畫**

   確保已制定恢復計畫。 在緊急情況下，必須提供此功能以確保AEM的生產使用。 這應包括備份、恢復、故障修復等情況。

### 開發 {#development}

開發是一個關鍵階段，需要的不僅僅是編碼。

#### 里程碑 {#milestones-4}

* **開發環境**

   規劃並記錄您的開發環境，包括：

   * 架構
   * [開發工具](/help/sites-developing/dev-tools.md)

      * 典型環境包含：

         * 問題跟蹤系統；比如吉拉
         * IDE;如Eclipse
         * 建造管理工具；如Maven
         * 持續整合的工具；比如詹金斯
         * 版本控制工具；例如GIT/SVN
         * 構建對象儲存庫管理器；如阿奇瓦/Nexus
   * 第三方軟體整合/依賴項
   * [解決方案整合/相依性](/help/sites-administering/integration.md)
   * 部署順序


* **測試系統**

   規劃並記錄您的測試環境，包括：

   * 架構
   * 對發展建設的依賴；包括夜間組建
   * 測試第三方軟體整合/相依性的可能性或限制
   * 測試工具
   * 自動化測試策略

* **生產系統**

   規劃並記錄您的生產環境，包括：

   * 架構
   * 部署順序
   * 第三方軟體整合/依賴項
   * 安全設定
   * 運行 [艱難的日子考驗](/help/sites-developing/tough-day.md) 在生產設定中
   * 效能測試要求；請參閱 [品質保證最佳實務](/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance)

* **整合**

   計畫、記錄和測試系統的所有方面和 [解決方案整合](/help/sites-administering/integration.md)，包括：

   * 自動化測試策略
   * 自動化流程 [將應用程式從開發移動到測試，然後進行生產](/help/managing/enterprise-devops.md#code-movement)
   * 自動化流程 [將內容從生產環境移至測試和開發環境](/help/managing/enterprise-devops.md#content-movement)

* **移轉**

   規劃、記錄和測試內容遷移的各個方面；包括：

   * 內容架構
   * 移轉策略

* **通訊**

   視需要確保所有團隊成員和專案角色都保持最新。

* **文件**

   完整記錄解決方案；包括：

   * 操作手冊
   * 任何可能影響升級的自定義
   * 發行說明

### 效能與測試 {#performance-and-testing}

一旦新應用程式可用，就需要進行嚴格的測試，包括功能和 [效能](/help/sites-deploying/configuring-performance.md).

>[!NOTE]
>
>任何測試團隊都應該可以保持中立，並提供測試結果。
>
>項目經理有責任評估結果的任何影響並決定採取適當行動。

#### 里程碑 {#milestones-5}

* **最終用戶接受測試**

   [使用者接受測試](/help/sites-developing/acceptance-signoff.md) (UAT)對於確保：

   * 該解決方案滿足用戶/客戶需求
   * 客戶/使用者接受解決方案（功能、設計和效能）

   應為客戶移交提供一份正式的清單；理想情況下，對快照進行自動化並每晚運行。 結果應發送給項目經理和開發團隊

* **效能和負載測試**

   使用效能和負載測試來確保解決方案在平均負載和峰值負載下均滿足所需的效能級別。

   有關效能測試的詳細資訊，請參閱：

   * [效能測試](/help/sites-deploying/configuring-performance.md)
   * [如何規劃和執行測試](/help/sites-developing/planning.md)

   * [基本效能指南](/help/sites-deploying/configuring-performance.md#basic-performance-guidelines)
   >[!NOTE]
   >
   >在正常使用AEM期間，這一進程必須繼續，但這些初始階段是最關鍵的。

### 轉出 {#rollout}

新應用程式的推出需要謹慎規劃，以確保順利上線。 這包括確認高安全性、培訓所有潛在使用者，並進行多次干預，以確認所有問題均已解決。

#### 里程碑 {#milestones-6}

* **準備**

   準備和規劃有助於確保順利推出。

* **培訓**

   確保所有有關人員都接受過培訓。

   請參閱 [Adobe Experience Manager](https://training.adobe.com/training/courses.html#solution=adobeExperienceManager) 在課程目錄里。

* **經過培訓的管理員**

   確保您的解決方案管理員具備：

   * 已接受培訓
   * 收到了適當的培訓材料
   * 收到適當檔案

* **已培訓的用戶**

   確保作者具備：

   * 已接受培訓
   * 收到了適當的培訓材料
   * 收到適當檔案；例如，使用手冊

* **滲透測試**

   滲透測試模擬攻擊電腦系統以識別潛在的安全弱點。

* **滲透/安全性測試**

   為確保解決方案的安全性，請執行特定的滲透測試，以及更廣泛的安全測試。

   請參閱 [安全性檢查清單](/help/sites-administering/security-checklist.md) 以取得更多詳細資訊。

### 上線 {#go-live}

您希望「上線」盡可能順暢。 最後的步驟需要規劃以執行乾淨。

#### 里程碑 {#milestones-7}

* **準備**

   準備和規劃有助於確保順利上線。

* **安全性**

   確認內部和外部使用者及其內容的解決方案的安全性。

* **備援**

   上線前，請確定備援所需的所有系統、程式和機制均已就緒。

* **支援**

   確保支援服務已就緒並準備就緒。

* **切換**

   規劃並執行轉變至生產環境和使用者。

* **轉出**

   準備並執行煙霧測試。

## 角色 {#persona}

核取清單由人設計。 這些角色在項目生命週期中具有重要的參與。

還有一些 [其他角色](#other-persona) 都涉及到特定任務。

### 項目贊助商 {#project-sponsor}

項目贊助機構是：

* 負責提供/呈現項目的業務案例。
* 確定和界定項目範圍的關鍵；包括：

   * 成功的定義和標準
   * 主要KPI

* 根據客戶路線圖提供主要里程碑。

### 專案經理 {#project-manager}

項目經理是：

* 根據項目贊助機構提供的要求（如範圍、關鍵績效指標、成功標準和定義）負責項目的整體交付。
* 負責定義預算並根據該預算為項目提供資源。
* 項目中所有角色的主要溝通點。

### 架構師 {#architect}

解決方案架構師：

* 負責解決方案和系統的高級設計。
* 協助定義AEM的實作策略。 例如，是實作叢集安裝、冷備用，還是需要內容傳遞網路(CDN)時。
* 同時根據用戶端需求定義AEM解決方案架構。 這可包括使用者角色的概念（具有相關權限）、範本和元件之間的關係，或何時使用多網站管理。

### 業務分析人員 {#business-analyst}

業務分析師：

* 主要負責收集和分析高級需求，然後將這些需求轉換成規格：

   * 供項目經理在規劃開發時使用
   * 讓開發團隊在設計和開發期間工作。

* 與客戶密切合作以分析需求。 它們會與下列項目相符：

   * 成功的定義。
   * 成功的標準。
   * KPI（以業務和績效為基礎）。

### 開發領導 {#development-lead}

開發領導：

* 負責專案的技術傳送。
* 負責選擇符合客戶要求的開發方法。
* 制定發展戰略：

   * 確保它與業務和效能KPI相協調
   * 考慮成功標準和定義

* 與架構師密切合作(尤其是在制定AEM的開發策略時)，以定義範本與元件之間的關係、第三方應用程式的整合策略以及任何專門功能等方面。

### 品質銷售機會 {#quality-lead}

質量線索：

* 負責交付的質量；確保符合成功標準，以及用戶端定義的任何KPI。
* 定義品質量度、與所有利害關係人保持一致、擬定測試計畫並確保執行。
* 建立報表並傳送給專案利害關係人。

### 系統工程師 {#system-engineer}

系統工程師：

* 負責監管項目基礎架構。
* 負責：

   * 內部開發和測試環境的設定
   * 將這些系統與客戶端系統進行匹配

* 提供硬體建議、監控各種實施，以及在上線之前和之後提供操作支援。

### 安全性領導 {#security-lead}

安全領導：

* 負責解決方案的整體安全概念，確保其與客戶的任何要求和策略保持一致。
* 為任何基於硬體的安全概念提供安全概念、安全操作和建議；例如區域和防火牆。

### 其他角色 {#other-persona}

* 利害關係人

   * 對項目成功感興趣（利益相關）的人（通常來自企業）。 他們經常為預算捐款。

* 法律

   * 在談判合同時需要法律咨詢。

* 培訓員

   * 根據項目的規模和性質，可利用專門培訓員為相關群體制定和舉辦培訓班。

* 技術撰寫人員

   * 根據項目的規模和性質，可利用專業技術撰稿人為特定群體編寫指南和手冊；例如系統管理員維護手冊或作者的使用手冊。

* 系統管理員

   * 負責系統的持續運行。

* 作者和使用者

   * 將使用系統建立和維護您網站內容的人員。

## 所需文檔和交付件 {#required-documents-and-deliverables}

核取清單涵蓋 **必填文檔** 和 **交付件** 每個里程碑。

* 兩者之間沒有1:1的關係；例如，一組所需文檔可產生單個交付項。
* 來自一個角色的交付內容可以是同一里程碑期間另一個角色的必要文檔。

### 必填文檔 {#required-documents}

此 **必填文檔** 在製作交付件時，適當的角色需要這些角色。

針對每個 **必需文檔** 角色應指出：

* **Y/N**:是否已收到。
* **1-3**:已接收文檔的質量指示。

### 交付件 {#deliverables}

對於每個里程碑，適當的角色負責提供特定文檔，從而實現其對特定里程碑的責任。

針對每個 **可交付項目** 角色必須指出：

* **Y/N**:是否已完成。

交付項通常用作 **必填文檔** 適用於目前或更新的里程碑。

## 相關最佳實務 {#related-best-practices}

如需部署、管理、開發或編寫的最佳實務，請參閱下列內容：

* 與管理AEM專案相關的其他最佳作法和准則：
   * [硬體調整指南](/help/managing/hardware-sizing-guidelines.md)
   * [企業 DevOps](/help/managing/enterprise-devops.md)
   * [SEO和URL管理最佳作法](/help/managing/seo-and-url-management.md)
   * [AEM與網頁協助工具准則](/help/managing/web-accessibility.md)
   * [一般資料保護規範](/help/managing/data-protection-and-privacy.md)* [部署和維護最佳實務](/help/sites-deploying/best-practices.md)
* [管理最佳實務](/help/sites-administering/administer-best-practices.md)
* [制定最佳做法](/help/sites-developing/best-practices.md)
* [製作最佳實務](/help/sites-authoring/best-practices.md)

## 重要檔案區域 {#key-documentation-areas}

* AEM檔案此外，AEM檔案的下列章節特別感興趣（不過，本清單並非詳盡無遺）:

   * [安全性](/help/sites-developing/security.md)
   * [建議的部署](/help/sites-deploying/recommended-deploys.md)
   * [企業 DevOps](/help/managing/enterprise-devops.md)
   * [硬體調整](/help/managing/hardware-sizing-guidelines.md)
   * AEM的概念：

      * [開發 — 基本](/help/sites-developing/the-basics.md)
      * [MSM概念](/help/sites-administering/msm.md)
      * [HTML範本語言(HTL)](https://docs.adobe.com/content/help/zh-Hant/experience-manager-htl/using/overview.html)

* 相關檔案

   * Adobe Experience Cloud - [Adobe Experience Cloud規劃](https://helpx.adobe.com/marketing-cloud/how-to/planning.html)
