---
title: 管理項目 — 最佳做法核對表
seo-title: Managing Projects - Best Practices Checklist
description: 管理項目以實施Adobe Experience Manager(AEM)需要規劃和理解。 項目核對表旨在作為一組項目交付的最佳做法。 它們指導您完成項目生命週期的所有階段，並提供對當前狀態的高級監控。
seo-description: Managing a project to implement Adobe Experience Manager (AEM) requires planning and understanding. The Project Checklists are intended as a set of best practices for project delivery. They guide you through all phases of the project life cycle and provide high level monitoring of your current status.
uuid: 859f73f4-535a-49a1-9ae4-a4aacd7f36dd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist, introduction
content-type: reference
discoiquuid: 2bfa287a-aad0-4681-9f9c-d48e8179684c
docset: aem65
exl-id: 94b91996-d2b2-4d4a-b770-334cfa2dc0b7
source-git-commit: 43a30b5ba76ea470cc50a962d4f04b4a1508964d
workflow-type: tm+mt
source-wordcount: '3262'
ht-degree: 1%

---

# 管理項目 — 最佳做法核對表{#managing-projects-best-practices-checklist}

管理項目以實施Adobe Experience Manager(AEM)需要規劃和理解，以確保您瞭解在實施項目之前和實施期間需要做出的問題和（相關）決策。

為幫助您，最佳做法包括：

* 安 [互動式核對表](/help/managing/best-practices-checklist.md) 使您能夠跟蹤和監控使用這些最佳實踐的進度。

   * 根據階段、里程碑和角色定義輸入和交付項。
   * 提供自動概覽（質量、運行狀況和完整性），以指示進度和項目運行狀況。

* 文檔，直接基於 [清單](/help/managing/best-practices-checklist.md)，詳細說明：

   * [項目心跳](#projectheartbeat) 分析。
   * [按角色列出的狀態](#status-by-role) 概述。
   * [階段和里程碑](#phases-and-milestones)。
   * [關鍵角色](#persona) 以及在每個（相關）階段的參與。
   * A [辭彙表](/help/managing/best-practices-glossary.md) 的 [所需文檔和交付件](#required-documents-and-deliverables)。

* [進一步參考](/help/managing/best-practices-further-reference.md) 提供更多有關特定領域的詳細資訊。

## 項目心跳儀儀表板 {#project-heartbeat-dashboard}

的 **項目心跳** 工作表提供了項目關鍵指標的圖形概覽：

* **階段質量**

   * 指示 [所需文檔和交付件](#required-documents-and-deliverables) 整個項目。

* **階段健康**

   * 項目的高級狀態指標；有助於突出可能存在風險的領域。

* **階段完整性**

   * 在項目期間的任何時間點，它都表示已為項目的每個階段完成了多少。

## 按角色列出的狀態 {#status-by-role}

的 **按角色列出的狀態** 工作表顯示詳細細目 [**健康**。 **質量** 和 **完整性**](#projectheartbeat) 按 **[階段](#phases-and-milestones)** 和 **[人物](#persona)**。

## 階段和里程碑 {#phases-and-milestones}

項目計劃分為不同的（高級別）階段。

每個階段都包含其自己的里程碑。 每個 [人物](#persona) （或角色），列出相關裡程碑以及生成定義的交付項所需的文檔。

>[!NOTE]
>
>單個所需文檔和交付項之間沒有直接的1:1關係。

### 準備 {#preparation}

項目的準備是整個項目的基礎。 您需要定義關鍵要求以及明確的目標和期望：

* **業務邏輯**

   * 開展項目的基本原因和理由。

* **範圍和計畫**

   * 應提供一個基本範圍和大致的時間表，以確定需要什麼，在什麼時限內；如果有助於澄清情況，您也可以定義範圍之外的內容。

您如何準備、計畫和運行項目以及實施解決方案將受到您在固定預算、固定時間表、內容數量和所需質量等限制的影響。

與以往一樣，任何因素的調整都會影響其他因素。 例如，縮短時間，但要求相同質量可能會提高價格，同時減少您可以滿足的內容數量。 預算往往是關鍵因素，因此這種關係不能被遺忘。

四個因素：

![項目階段_四階段](assets/projectphases_fourphases.png)

#### 里程碑 {#milestones}

* **驗證**

   在此階段，您需要驗證並確認項目目標；例如：

   * 您希望實現/提供什麼？
   * 誰會受益？
   * 範圍是什麼？

      * 如果有助於澄清情況，您還可以定義範圍外的內容。
   * 如何定義成功？
   * 你如何衡量成功？
   * 要求、業務和技術是什麼？
   * 是否要替換舊系統，如果是，是否要遷移資料？
   * 誰會參與？
   * 如何衡量進展？
   * 在項目的整個生命週期中，您將多長時間查看進度？


* **預算**

   在開始任何項目之前，您需要對實施成本進行可靠而現實的估計：

   * 使用驗證里程碑中的資訊作為估計的基礎。
   * 在你的估計中要實事求是。
   * 考慮並尊重客戶機可能遵守的任何客戶機准則、流程或限制。
   * 如果以後需要審查或改進預算，則考慮應急和審查程式。
   * 記住，成本會以多種形式出現；購買、使用資源及費用（其中包括）。

### 規劃 {#planning}

計畫項目可合併準備。 在此，您需要開始將目標和期望轉換為一個定義明確的路線圖，其中包括具體任務，以明確的溝通為約束，並進行嚴格的審查以衡量進展。

#### 里程碑 {#milestones-1}

* **移交**

   乾淨的移交確保適當的個人/群體瞭解他們在項目中的責任。

   應提供/生成完整的詳細資訊，以確保他們全面瞭解所有相關方面，包括路線圖、範圍、目標、要求和關鍵績效指標。

* **風險評估**

   為避免令人不快的意外，請使用風險評估來識別和量化任何潛在風險及其影響和概率。

   應在項目生命週期早期完成這項工作，以確保確定和評估任何可靠性。 根據調查結果，您可以向利益相關方報告是否可以實施全部要求，以及是否可能規劃要採取和跟蹤的適當行動。

* **通信**

   溝通總是任何項目成功的關鍵。 您需要清晰、高效地進行溝通，以確保每個人都：

   * 努力實現相同的基本目標
   * 從同一資訊庫
   * 具有相同頻道

* **啟動**

   啟動會議用於提高對項目正在啟動的認識。 這是一個很好的機會：

   * 邀請所有感興趣的方（或至少團體代表）。
   * 提出項目的關鍵事實。
   * 回答問題。
   * 確保每個人都有相同的知識庫。
   * 從所有參與者那裡獲得承諾 — 這必須得到。

      * 通過在項目開始時讓主要參與者（包括潛在作者）參與，您將增加他們對項目承諾的機會。

### 開發準備 {#development-preparation}

規劃開發是確保您的項目由具備所需知識的團隊構建在堅固設計之上的關鍵。

#### 里程碑 {#milestones-2}

* **開發團隊人員配備和培訓**

   在開始任何項目之前，您應確保您的開發團隊配備了適當的人員，並且所有團隊成員都接受過針對手頭任務的培訓。

* **內容體系結構**

   內容體系結構定義了並描述了未來的內容體系結構；包括：

   * 內容樹；包括資產
   * 基本結構；包括活動等。
   * 多站點和多語言結構（MSM、翻譯等）
   * 支援內容（包括標籤和標籤概念）
   * 快取和內容重用策略

* **系統體系結構**

   系統體系結構定義了系統的概念視圖；包括（其中包括）:

   * [系統結構](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) 適用於所有所需環境
   * 子系統
   * 第三方系統
   * 介面；硬體、軟體和人機交互
   * 每個環境的伺服器；查看 [技術要求](/help/sites-deploying/technical-requirements.md) 和 [硬體調整指南](/help/managing/hardware-sizing-guidelines.md)

   * 每個環境的流程；例如，部署和維護要求
   * 維護活動（資料儲存GC、TarPM優化等）
   * [調度程式](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html) 快取
   * [聚類](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) 發佈/授權共用
   * 客戶端效能（JS minify、concat、csssprite、http請求總數等）

* **應用程式體系結構**

   應用程式體系結構定義並描述建議的應用程式的行為。

   重點是：

   * 它們如何彼此和用戶交互。
   * 應用程式要使用和生成的資料，而不是其內部結構。

   定義應包括：

   * 項目的基本代碼結構
   * 代碼對象（包、包等）
   * 模板/元件及其關係的細目
   * 所需自定義的高級詳細資訊（稍後將提供特定的覆蓋）
   * 解決方案所需的工作流設計（例如，內容建立、批准、發佈、轉換、導入、導出等）
   * 對任何複雜模組（如MSM、Commerce、第三方整合）進行特別考慮


* **系統整合**

   系統整合要求您規劃（然後實施）:

   * 所有子系統和 [解決方案整合](/help/sites-administering/integration.md) 將匯聚一堂，作為一個協調系統運行
   * 如何整合任何第三方系統；與任何特殊注意事項一起使用，如離線/聯機、客戶端/瀏覽器端或第三方系統關閉時的錯誤處理

* **Test概念**

   在開始發展前，要樹立全面，深入的觀念， [測試](/help/sites-developing/planning.md) 項目的要求。

   這應包括（除其他外）:

   * 要執行的所有test的詳細資訊
   * 準備這些test所需的任何內容
   * 要使用的任何test工具的資訊
   * 對誰將參與測試的高級別指示；尤其是QA團隊以外的組
   * test自動化的細節；例如，使用Selenium或AEMDeveloper模式

* **體驗設計**

   系統設計(XD)涉及為您的解決方案設計用戶體驗。

   應為您的作者和網站的最終用戶分析和開發用戶體驗。

* **支援設定**

   在開發之前，應設定部署、發佈、test和報告問題所需的所有支援流程。

   另請參閱 [Adobe支援門戶](https://helpx.adobe.com/tw/marketing-cloud/contact-support.html)。

### 運營計畫和運營 {#operations-planning-and-operations}

在類似的基礎上，必須正確規劃操作，以確保您擁有項目生命週期所有階段所需的環境。 您還需要適當的流程來維護它們。

#### 里程碑 {#milestones-3}

* **權限**

   您需要為將使用此解決方案的所有用戶/組規劃並實施角色和權限概念。

   例如：

   * 具有 `read`/ `write` 每個訪問定義

   * 定義影響發佈環境的權限的使用；比如說， `replicate`
   * 對於具有最小權限的用戶，應定義工作流
   * 中的用戶 `editor` 組不應 `admin` 權利或不是 `administrators` 組

   有關詳細資訊，請參見 [用戶管理和安全](/help/sites-administering/security.md)。

* **監控和維護**

   監控和維護是確保解決方案在投入使用後順利運行的關鍵方面。 為此，您需要定義：

   * 需要監控的內容
   * 維護任務；常規和特殊情況

   另請參閱 [監控和維護](/help/sites-deploying/monitoring-and-maintaining.md) 的子菜單。

* **移轉**

   應檢查和驗證舊系統中的任何內容以進行遷移。

* **恢復計畫**

   確保已制定恢復計畫。 在緊急情況下，必須提供此功能以確保生產AEM使用…… 這應包括備份、恢復、故障修復等情形。

### 開發 {#development}

發展是一個不僅需要編碼的關鍵階段。

#### 里程碑 {#milestones-4}

* **開發環境**

   規劃並記錄您的開發環境，包括：

   * 架構
   * [開發工具](/help/sites-developing/dev-tools.md)

      * 典型環境包括：

         * 問題跟蹤系統；比如吉拉
         * IDE;如Eclipse
         * 建築管理工具；比如馬文
         * 持續整合的工具；比如詹金斯
         * 版本控制工具；例如GIT/SVN
         * 構建項目儲存庫管理器；如Archiva/Nexus
   * 第三方軟體整合/依賴項
   * [解決方案整合/依賴項](/help/sites-administering/integration.md)
   * 部署順序


* **Test系統**

   規劃並記錄您的test環境，包括：

   * 架構
   * 對發展建設的依賴；包括夜間生成
   * 測試第三方軟體整合/依賴項的可能性或限制
   * 測試工具
   * 自動化測試策略

* **生產系統**

   規劃並記錄您的生產環境，包括：

   * 架構
   * 部署順序
   * 第三方軟體整合/依賴項
   * 安全設定
   * 運行 [艱難日test](/help/sites-developing/tough-day.md) 在生產設定上
   * 績效test要求；見 [質量保證的最佳做法](/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance)

* **整合**

   規劃、記錄和test系統的所有方面， [解決方案整合](/help/sites-administering/integration.md)，包括：

   * 自動化測試策略
   * 自動化流程 [將應用程式從開發移到test，然後進行生產](/help/managing/enterprise-devops.md#code-movement)
   * 自動化流程 [將內容從生產移動到test和開發](/help/managing/enterprise-devops.md#content-movement)

* **移轉**

   規劃、記錄和test內容遷移的所有方面；包括：

   * 內容體系結構
   * 遷移策略

* **通信**

   確保所有團隊成員和項目角色都根據需要保持最新。

* **文件**

   全面記錄解決方案；包括：

   * 操作手冊
   * 可能影響升級的任何自定義
   * 發行說明

### 效能和測試 {#performance-and-testing}

新應用程式一經推出，就需要經過嚴格的測試，包括功能和 [效能](/help/sites-deploying/configuring-performance.md)。

>[!NOTE]
>
>應允許任何測試團隊保持中立並提供測試結果。
>
>項目經理有責任評估結果的任何影響並決定採取適當行動。

#### 里程碑 {#milestones-5}

* **最終用戶接受Test**

   [用戶驗收測試](/help/sites-developing/acceptance-signoff.md) (UAT)對於確保：

   * 該解決方案滿足用戶/客戶的要求
   * 客戶/用戶接受該解決方案（功能、設計和效能）

   應為客戶移交制定一份正式的清單；最理想地是自動化，並針對快照每晚運行。 結果應發送給項目經理和開發團隊

* **效能和負載Test**

   效能和負載test用於確保解決方案在平均負載和峰值負載上滿足所需的效能級別。

   有關效能測試的詳細資訊，請參閱：

   * [效能測試](/help/sites-deploying/configuring-performance.md)
   * [如何規劃和運行測試](/help/sites-developing/planning.md)

   * [基本效能指南](/help/sites-deploying/configuring-performance.md#basic-performance-guidelines)
   >[!NOTE]
   >
   >在正常使用期間必須繼續這一進AEM程，但最關鍵的是這些初始階段。

### 推出 {#rollout}

新應用程式的部署需要仔細規劃，以確保順利實現。 這包括確認高級安全性、培訓所有潛在用戶並進行多次干預，以確認已處理所有問題。

#### 里程碑 {#milestones-6}

* **準備**

   準備和規劃將有助於確保順利推出。

* **培訓**

   確保所有相關人員都接受過培訓。

   請參閱 [Adobe Experience Manager](https://training.adobe.com/training/courses.html#solution=adobeExperienceManager) 在課程目錄中。

* **經培訓的管理員**

   確保您的解決方案管理員：

   * 已培訓
   * 已收到適當的培訓材料
   * 收到相應的文檔

* **已培訓的用戶**

   確保您的作者具有：

   * 已培訓
   * 已收到適當的培訓材料
   * 收到適當檔案；例如，《使用手冊》

* **滲透Test**

   穿透test模擬對電腦系統的攻擊，以識別潛在的安全弱點。

* **滲透/安全Test**

   為確保解決方案的安全性，請執行特定的滲透test，以及範圍更廣的安全test。

   查看 [安全核對表](/help/sites-administering/security-checklist.md) 的子菜單。

### 上線 {#go-live}

你希望你的Go Live盡可能流暢。 最後的步驟需要規劃以執行乾淨。

#### 里程碑 {#milestones-7}

* **準備**

   準備和規劃將有助於確保順利實現。

* **安全性**

   確認您的解決方案對內部和外部用戶及其內容的安全性。

* **回退**

   確保備用所需的所有系統、過程和機制在投入使用前都已到位。

* **支援**

   確保支援服務已就位並準備就緒。

* **切換**

   規劃並執行到生產環境和用戶的過渡。

* **展開**

   準備並執行您的煙test。

## 角色 {#persona}

核對表由個人設計。 這些角色在項目生命週期中具有重要的參與。

還有一些 [其他角色](#other-persona) 涉及特定任務。

### 項目發起人 {#project-sponsor}

項目發起人是：

* 負責提供/演示項目的業務案例。
* 確定和界定項目範圍的關鍵；包括：

   * 成功的定義和標準
   * 主要KPI

* 根據客戶端路線圖提供主要里程碑。

### 專案經理 {#project-manager}

項目經理是：

* 根據項目發起人提供的要求（如範圍、關鍵績效指標、成功標準和定義）負責項目的整體交付。
* 負責定義預算並根據該預算為項目分配資源。
* 項目中所有角色的主要溝通點。

### 建築師 {#architect}

解決方案架構師：

* 負責解決方案和系統的高級設計。
* 幫助定義實施策AEM略。 例如，是實施群集安裝，還是實施冷備用，還是需要內容分發網路(CDN)。
* 還根據客戶AEM機需求定義解決方案體系結構。 這可包括用戶角色（具有相關權限）的概念、模板和元件之間的關係，或何時使用多站點管理。

### 業務分析師 {#business-analyst}

業務分析師：

* 主要負責收集和分析高級需求，然後將這些需求轉換為規格：

   * 供項目經理在計劃開發時使用
   * 以供開發團隊在設計和開發期間工作。

* 與客戶密切合作以分析需求。 它們與以下對應：

   * 成功的定義。
   * 成功的標準。
   * 關鍵績效指標（以業務及表現為基礎）。

### 開發領導 {#development-lead}

開發領導：

* 負責項目的技術交付。
* 負責選擇符合客戶要求的開發方法。
* 制定發展戰略：

   * 確保它與業務和效能KPI一致
   * 考慮到成功標準和定義

* 與架構師密切協作(尤其是在為其制定開發策略時AEM)，以定義各方面，如模板和元件之間的關係、第三方應用程式的整合策略以及任何專用功能。

### 質量線索 {#quality-lead}

質量線索：

* 負責交付質量；確保它符合成功標準以及客戶端定義的任何KPI。
* 定義質量指標，與所有利益相關方保持一致，擬定測試計畫並確保它們得到執行。
* 建立報告並向項目利益相關方提供報告。

### 系統工程師 {#system-engineer}

系統工程師：

* 負責監督項目基礎架構。
* 負責：

   * 內部開發和test環境的設定
   * 將這些系統與客戶機系統匹配

* 提供硬體建議，監控各種實施，並提供運行前和運行後的操作支援。

### 安全領導 {#security-lead}

安全線索：

* 負責解決方案的總體安全概念，確保它與來自客戶的任何要求和策略保持一致。
* 為任何基於硬體的安全概念提供安全概念、安全操作和建議；例如區域和防火牆。

### 其他角色 {#other-persona}

* 利益相關方

   * 對項目成功感興趣（利益）的人（通常來自企業）。 他們經常為預算捐款。

* 法律

   * 談判合同時需要法律咨詢。

* 培訓員

   * 根據項目的規模和性質，可利用專門培訓員為相關群體制定和舉辦培訓班。

* 技術作者

   * 根據項目的規模和性質，可使用專業技術編寫人員為特定群體編寫指南和手冊；例如，系統管理員的維護手冊或作者的使用手冊。

* 系統管理員

   * 負責系統的持續運行。

* 作者和最終用戶

   * 將使用系統建立和維護網站內容的人員。

## 所需文檔和交付件 {#required-documents-and-deliverables}

檢查表覆蓋 **所需文檔** 和 **交付項** 每個里程碑。

* 兩者之間沒有1:1的關係；例如，一組必需的文檔可以生成單個交付項。
* 在同一里程碑期間，來自一個角色的可交付內容可以是另一個角色的必需文檔。

### 所需文檔 {#required-documents}

的 **所需文檔** 在生成交付項時，需要適當的人格。

每個 **所需文檔** 角色應表明：

* **是/否**:是否已收到。
* **1-3**:顯示所接收文檔的質量。

### 交付項 {#deliverables}

對於每個里程碑，適當的角色負責提供特定文檔，從而實現他們對特定里程碑的責任。

每個 **可交付** 角色必須指明：

* **是/否**:是否已完成。

交付項通常用作 **所需文檔** 當前里程碑或以後里程碑。

## 相關最佳實踐 {#related-best-practices}

有關部署、管理、開發或創作的最佳做法，請參閱以下內容：

* 與管理項目相關的其他最佳做法和AEM指導原則：
   * [硬體調整指南](/help/managing/hardware-sizing-guidelines.md)
   * [企業 DevOps](/help/managing/enterprise-devops.md)
   * [SEO和URL管理最佳實踐](/help/managing/seo-and-url-management.md)
   * [和AEMWeb輔助功能指南](/help/managing/web-accessibility.md)
   * [一般資料保護法規](/help/managing/data-protection-and-privacy.md)* [部署和維護最佳做法](/help/sites-deploying/best-practices.md)
* [管理最佳做法](/help/sites-administering/administer-best-practices.md)
* [制定最佳做法](/help/sites-developing/best-practices.md)
* [編寫最佳做法](/help/sites-authoring/best-practices.md)

## 關鍵文檔區域 {#key-documentation-areas}

* 文AEM件此外，檔案AEM的以下部分特別感興趣（但是，這份清單並不詳盡）:

   * [安全性](/help/sites-developing/security.md)
   * [建議的部署](/help/sites-deploying/recommended-deploys.md)
   * [企業 DevOps](/help/managing/enterprise-devops.md)
   * [硬體調整](/help/managing/hardware-sizing-guidelines.md)
   * 概念AEM:

      * [開發 — 基礎](/help/sites-developing/the-basics.md)
      * [MSM概念](/help/sites-administering/msm.md)
      * [HTML模板語言(HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)

* 相關文檔

   * Adobe Experience Cloud [規劃Adobe Experience Cloud](https://helpx.adobe.com/marketing-cloud/how-to/planning.html)
