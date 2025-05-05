---
title: 管理專案 — 最佳實務檢查清單
description: 管理專案以實施Adobe Experience Manager (AEM)需要計畫和瞭解。 專案檢查清單旨在作為專案傳送的一組最佳實務。 它們會引導您完成專案生命週期的所有階段，並提供您狀態的高層級監控。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist, introduction
content-type: reference
docset: aem65
exl-id: 94b91996-d2b2-4d4a-b770-334cfa2dc0b7
solution: Experience Manager, Experience Manager 6.5
feature: Compliance
role: Admin,Architect,Data Architect,Developer,Leader
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '3214'
ht-degree: 0%

---

# 管理專案 — 最佳實務檢查清單{#managing-projects-best-practices-checklist}

管理專案以實施Adobe Experience Manager (AEM)需要規劃和瞭解，以便於在實施專案之前和期間瞭解您必須所做的問題和（相關）決策。

為協助您，最佳實務包括：

* [互動式檢查清單](/help/managing/best-practices-checklist.md)，可讓您追蹤並監控您運用這些最佳實務的進度。

   * 根據階段、里程碑和角色定義輸入和交付專案。
   * 提供自動概覽（品質、健全和完整性）來指示進度和專案健全狀態。

* 根據詳細說明下列專案的[檢查清單](/help/managing/best-practices-checklist.md)提供檔案：

   * [專案心率](#projectheartbeat)分析。
   * [依角色的狀態](#status-by-role)總覽。
   * [階段和里程碑](#phases-and-milestones)。
   * [關鍵角色](#persona)及其在每個（相關）階段的參與。
   * [必要檔案和交付專案](#required-documents-and-deliverables)的[字彙表](/help/managing/best-practices-glossary.md)。

* [進一步參考](/help/managing/best-practices-further-reference.md)資料以提供特定區域的更多詳細資料。

## 專案心率控制面板 {#project-heartbeat-dashboard}

**專案心率**&#x200B;工作表提供專案關鍵量度的圖形化概觀：

* **階段品質**

   * 表示專案中[必要檔案和交付專案](#required-documents-and-deliverables)的品質。

* **階段健康狀況**

   * 您專案的高層級狀態指標；突顯可能有風險的區域很有用。

* **階段完整性**

   * 在專案期間的任何時間點，這表示專案每個階段的已完成程度。

## 按角色顯示狀態 {#status-by-role}

[角色狀態&#x200B;**]工作表顯示**&#x200B;[&#x200B;階段&#x200B;](#phases-and-milestones)**與**&#x200B;[&#x200B;角色&#x200B;](#persona)**之&lbrace;2**&#x200B;健康狀態&#x200B;**、&lbrace;品質及&#x200B;**&#x200B;完整性&#x200B;**[&#128279;](#projectheartbeat)&#x200B;的詳細劃分。**&#x200B;**

## 階段和里程碑 {#phases-and-milestones}

專案計畫會劃分為不同的（高階）階段。

每個階段都包含自己的里程碑。 針對每個[角色](#persona) （或角色），會列出相關的里程碑，以及產生已定義交付專案所需的檔案。

>[!NOTE]
>
>個別必要檔案和交付專案之間沒有直接的1:1關係。

### 準備 {#preparation}

專案的準備工作會構成整個專案的基礎。 定義主要需求，以及以下專案的明確目標和期望：

* **商業基本原則**

   * 進行專案的基本原因與理由。

* **範圍和排程**

   * 應提供基本範圍和粗略排程，以定義所需的內容以及時間範圍；如果有助於釐清情況，您也可以定義範圍以外的內容。

您準備、規劃及執行專案與實施解決方案的方式，會受到您作業所依據的限制所影響。 例如，固定預算、固定時間表、內容數量、所需品質。

一如既往，調整任何因素都會影響其他因素。 例如，縮短時間，但要求相同的品質等級，可能會提高價格，同時減少您可滿足的內容數量。 預算通常是關鍵因素，因此這類關係無法忘記。

四個因素：

![projectphoits_fourphods](assets/projectphases_fourphases.png)

#### 里程碑 {#milestones}

* **驗證**

  在此階段中，您必須驗證並確認專案的目標，例如：

   * 您想要實現什麼/提供什麼？
   * 哪些人有好處？
   * 範圍為何？

      * 如果這有助於釐清狀況，您也可以定義範圍以外的內容。

   * 您如何定義成功？
   * 如何衡量成功？
   * 有哪些需求、業務與技術？
   * 是否有要取代的舊系統，若是的話，是否有要移轉的資料？
   * 誰與此有關？
   * 如何測量進度？
   * 在專案生命週期中，您多久檢視一次進度？

* **預算**

  在開始任何專案之前，您需要對實作成本做出可靠且實際的估計：

   * 使用驗證里程碑的資訊作為預估的基礎。
   * 在預估中請務實地考量。
   * 考慮並遵守使用者端必須遵守的任何使用者端准則、程式或限制。
   * 如果稍後需要複查或調整預算，請考慮應急及複查程式。
   * 請記住，成本有多種形式，例如購買、使用資源和費用等。

### 規劃 {#planning}

計畫您的專案會整合準備工作。 您應該在此開始將目標與期望轉換成由具體任務所組成的定義良好的藍圖，並以明確的溝通和嚴格的審查來衡量進度。

#### 里程碑 {#milestones-1}

* **交接**

  簡潔的交接可確保適當的角色/群組瞭解其在專案中的責任。

  應提供/產生完整細節，以確保他們完全瞭解所有相關方面，包括藍圖、範圍、目標、要求和KPI。

* **風險評估**

  為避免意外的令人不快，請使用風險評估來識別和量化任何潛在風險及其影響和機率。

  這應在專案生命週期的初期完成，以確保識別並評估任何漏洞。 您可以根據調查結果，向利害關係人報告是否可實施完整需求，以及是否可能計畫要採取和追蹤的適當動作（如有必要）。

* **通訊**

  溝通永遠是任何專案成功的關鍵。 清楚有效率地溝通，確保每個人都能：

   * 致力於相同的基本目標
   * 來自相同資訊庫
   * 使用相同的管道

* **啟動**

  「啟動」會議用於提高人們對專案正在啟動的意識。 這是您進行下列操作的絕佳機會：

   * 邀請所有感興趣的當事方（或至少是群組代表）。
   * 呈現專案的關鍵事實。
   * 回答問題。
   * 確保每個人都擁有相同的知識庫。
   * 獲得所有參與者的承諾 — 必須贏取承諾。

      * 若在專案開始時讓主要參與者（包括潛在作者）參與，您就更有可能獲得他們對專案的承諾。

### 開發準備 {#development-preparation}

規劃開發是確保專案是由具備所需知識的團隊以可靠的設計為基礎而建置的關鍵。

#### 里程碑 {#milestones-2}

* **開發團隊已配備人員並接受訓練**

  開始任何專案之前，您應該確保開發團隊已配置適當的人員，且所有團隊成員都已接受手頭任務的培訓。

* **內容架構**

  內容架構會定義並描述內容的未來架構，包括：

   * 內容樹狀結構；包括資產
   * 基本結構；包括行銷活動等。
   * 多網站和多語言結構（MSM、翻譯等）
   * 支援內容（包括標籤和標籤概念）
   * 快取和內容重複使用策略

* **系統架構**

  系統架構定義系統的概念檢視；包括（其他資訊）：

   * 所有必要環境的[系統結構](/help/sites-deploying/recommended-deploys.md#deployment-scenarios)
   * 子系統
   * 協力廠商系統
   * 介面；硬體、軟體和人力互動
   * 每個環境的伺服器；請參閱[技術需求](/help/sites-deploying/technical-requirements.md)和[硬體大小調整准則](/help/managing/hardware-sizing-guidelines.md)

   * 每個環境的程式；例如，部署和維護需求
   * 維護活動（Datastore GC、TarPM最佳化等）
   * [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hant)快取
   * [叢集](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) Publish/Authorshare
   * 使用者端的效能（JS精簡、concat、css指令集、http請求總數及其他）

* **應用程式架構**

  應用程式架構會定義並描述建議應用程式的行為。

  重點在於：

   * 他們如何彼此互動以及與使用者互動。
   * 由應用程式使用和產生的資料，而非其內部結構。

  定義應涵蓋：

   * 專案的基本程式碼結構
   * 程式碼成品（套件組合、套件等）
   * 範本/元件及其關係的劃分
   * 所需自訂的高層級細節（特定覆蓋圖將於稍後顯示）
   * 設計解決方案所需的工作流程（例如內容建立、核准、發佈、轉換、匯入和匯出）
   * 任何複雜模組(例如MSM、Commerce、協力廠商整合)的特別考量

* **系統整合**

  系統整合需要您規劃（然後實作）：

   * 如何將所有子系統與[解決方案整合](/help/sites-administering/integration.md)整合在一起，以便作為一個連貫的系統來運作
   * 任何協力廠商系統如何整合；以及任何特殊考量，例如離線/線上、使用者端/瀏覽器端，或在協力廠商系統故障時進行遞減處理

* **測試概念**

  在開始開發之前，您應該針對專案的所有[測試](/help/sites-developing/planning.md)需求，擬定一個深入而完整的概念。

  這應該包括（其中包括）：

   * 要執行之所有測試的詳細資訊
   * 準備這些測試所需的任何內容
   * 要使用的任何測試工具的資訊
   * 高層級指示將參與測試的對象；尤其是QA團隊以外的群組
   * 測試自動化的詳細資訊；例如，使用Selenium或AEM開發人員模式

* **體驗設計**

  體驗設計(XD)涉及為解決方案設計使用者體驗。

  您應該針對作者和網站的最終使用者來分析和開發使用者體驗。

* **支援安裝程式**

  在開發之前，應設定部署、發行、測試和報告問題所需的所有支援流程。

  另請參閱[Adobe支援入口網站](https://experienceleague.adobe.com/zh-hant?support-solution=General&amp;support-tab=home#support)。

### 作業計畫與作業 {#operations-planning-and-operations}

在類似的基礎上，必須正確規劃作業，以確保您擁有所需的環境 — 專案生命週期的所有階段。 您還需要適當的程式來進行維護。

#### 里程碑 {#milestones-3}

* **許可權**

  您必須針對將使用此解決方案的所有使用者/群組規劃，然後實作角色和許可權概念。

  例如：

   * 角色清單（亦即群組），具有每個角色的`read`/ `write`存取定義

   * 影響發佈環境的許可權使用定義；例如，`replicate`
   * 對於具有最低許可權的使用者，應定義工作流程
   * `editor`群組中的使用者不應有`admin`許可權，也不應屬於`administrators`群組

  如需詳細資訊，請參閱[使用者管理與安全性](/help/sites-administering/security.md)。

* **監視與維護**

  監控與維護是確保解決方案上線後順暢運作的關鍵環節。 為此，您需要定義：

   * 需要監控的專案
   * 維護任務；包括一般和特殊情況

  另請參閱[監視與維護](/help/sites-deploying/monitoring-and-maintaining.md)以取得詳細資訊。

* **移轉**

  任何來自舊版系統的內容皆應檢閱及驗證以進行移轉。

* **復原計畫**

  確定您已制定復原計畫。 在緊急情況下，這必須可用於保護AEM的生產使用。 這應該包括備份、還原、容錯移轉和其他情況。

### 開發 {#development}

開發是關鍵階段，不僅需要程式碼。

#### 里程碑 {#milestones-4}

* **開發環境**

  規劃並記錄您的開發環境，包括：

   * 架構
   * [開發工具](/help/sites-developing/dev-tools.md)

      * 典型的環境包括：

         * 問題追蹤系統；例如Jira
         * IDE；例如Eclipse
         * 組建管理工具，例如Maven
         * 持續整合的工具；例如Jenkins
         * 版本控制工具，例如GIT/SVN
         * 組建成品存放庫管理員，例如Archiva/Nexus

   * 協力廠商軟體整合/相依性
   * [解決方案整合/相依性](/help/sites-administering/integration.md)
   * 部署步調

* **測試系統**

  規劃並記錄您的測試環境，包括：

   * 架構
   * 依賴開發組建；包括夜間組建
   * 測試協力廠商軟體整合/相依性的可能性或限制
   * 測試工具
   * 自動化測試策略

* **生產系統**

  規劃並記錄您的生產環境，包括：

   * 架構
   * 部署步調
   * 協力廠商軟體整合/相依性
   * 安全性設定
   * 基準效能已透過在生產設定上執行[嚴苛日測試](/help/sites-developing/tough-day.md)驗證
   * 效能測試的需求；請參閱[品質保證的最佳實務](/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance)

* **整合**

  規劃、記錄及測試系統與[解決方案整合](/help/sites-administering/integration.md)的所有層面，包括：

   * 自動化測試策略
   * 自動化處理以[將應用程式從開發移至測試，然後移至生產環境](/help/managing/enterprise-devops.md#code-movement)
   * 自動化程式以[將內容從生產環境移至測試和開發環境](/help/managing/enterprise-devops.md#content-movement)

* **移轉**

  規劃、記錄及測試內容移轉的各個層面；包括：

   * 內容架構
   * 移轉策略

* **通訊**

  確保所有團隊成員和專案角色在必要時保持最新。

* **文件**

  完整記錄解決方案；包括：

   * 操作手冊
   * 可能影響升級的任何自訂
   * 發行說明

### 效能與測試 {#performance-and-testing}

新應用程式推出後，必須經過嚴格的功能和[效能](/help/sites-deploying/configuring-performance.md)測試。

>[!NOTE]
>
>任何測試團隊都應被允許保持中立並交付測試結果。
>
>專案經理有責任評估結果的任何影響，並決定適當的行動。

#### 里程碑 {#milestones-5}

* **使用者驗收測試**

  [使用者接受度測試](/help/sites-developing/acceptance-signoff.md) (UAT)對於確保：

   * 此解決方案符合使用者/客戶的需求
   * 客戶/使用者接受解決方案（功能、設計和效能）

  客戶交接應該有正式的核對清單；理想情況下，此清單會自動執行，每晚針對快照執行。 應將結果傳送給專案經理和開發團隊

* **效能和負載測試**

  使用效能和負載測試，確保解決方案在平均和尖峰負載下均符合所需的效能等級。

  如需效能測試的詳細資訊，請參閱：

   * [效能測試](/help/sites-deploying/configuring-performance.md)
   * [如何規劃及執行測試](/help/sites-developing/planning.md)

   * [基本效能准則](/help/sites-deploying/configuring-performance.md#basic-performance-guidelines)

  >[!NOTE]
  >
  >在正常使用AEM期間必須繼續此程式，但這些初始階段最關鍵。

### 推出 {#rollout}

新應用程式的推出需要仔細規劃，以確保順利上線。 這包括確認高水準的安全性、培訓所有潛在的使用者，以及進行多次練習以確認所有問題皆已解決。

#### 里程碑 {#milestones-6}

* **準備**

  準備和規劃將有助於確保順利推出。

* **培訓**

  確保所有參與的工作人員都經過培訓。

  請參閱課程目錄中的[Adobe Experience Manager](https://training.adobe.com/training/courses.html#solution=adobeExperienceManager)。

* **已訓練的管理員**

  確保您的解決方案管理員具備：

   * 已訓練
   * 已收到適當的訓練資料
   * 已收到適當的檔案

* **已訓練的使用者**

  請確認您的作者擁有：

   * 已訓練
   * 已收到適當的訓練資料
   * 已收到適當的檔案；例如，使用手冊

* **滲透測試**

  滲透測試會模擬電腦系統上的攻擊，以找出潛在的安全性弱點。

* **滲透/安全性測試**

  為確保解決方案的安全性，請執行特定的滲透測試，以及範圍更廣的安全性測試。

  如需詳細資訊，請參閱[安全性檢查清單](/help/sites-administering/security-checklist.md)。

### 上線 {#go-live}

您希望您的上線儘可能流暢。 同樣地，最後步驟需要規劃為全新執行。

#### 里程碑 {#milestones-7}

* **準備**

  準備和規劃將有助於確保順利上線。

* **安全性**

  確認您的解決方案對內部和外部使用者及其內容的安全性。

* **遞補**

  確定遞補所需的所有系統、程式和機制在上線前均已準備就緒。

* **支援**

  確保支援服務準備就緒。

* **轉變**

  規劃並執行轉換至您的生產環境和使用者。

* **轉出**

  準備並執行您的煙霧測試。

## 角色 {#persona}

核對清單由人員設計。 這些角色與專案生命週期有重大的關係。

還有一些[其他角色](#other-persona)參與特定工作。

### 專案贊助者 {#project-sponsor}

專案贊助者為：

* 負責提供/展示專案的業務案例。
* 決定和定義專案範圍的關鍵；包括：

   * 成功的定義和條件
   * 主要KPI

* 根據使用者端藍圖提供主要里程碑。

### 專案經理 {#project-manager}

專案經理是：

* 根據專案贊助者提供的需求（例如範圍、KPI、成功標準和定義），負責專案的整體交付。
* 負責定義預算，並根據該預算為專案編列資源。
* 專案中所有角色的主要通訊點。

### 架構者 {#architect}

解決方案架構師：

* 負責解決方案與系統的高階設計。
* 協助定義AEM的實作策略。 例如，是否實作叢集安裝、冷待命或需要內容傳遞網路(CDN)時。
* 您也可以根據使用者端需求定義AEM解決方案架構。 這可以包括使用者角色（具有相關許可權）的概念、範本與元件之間的關係，或何時使用多網站管理。

### 業務分析師 {#business-analyst}

業務分析人員：

* 主要負責收集和分析高階需求，然後將這些需求轉換成規格：

   * 供專案經理在規劃開發時使用
   * 供開發團隊在設計和開發期間使用。

* 與客戶緊密合作以分析需求。 這些條件可比對至：

   * 成功的定義。
   * 成功的標準。
   * KPI （以業務和效能為基礎）。

### 開發負責人 {#development-lead}

開發負責人：

* 負責專案的技術傳遞。
* 負責選取符合使用者端需求的開發方法。
* 擬定開發策略：

   * 確保符合業務和效能KPI
   * 將成功標準和定義納入考量

* 與架構師緊密合作(尤其是在草擬AEM的開發策略時)以定義範本與元件之間的關係、第三方應用程式的整合策略及任何特殊功能等方面。

### 品質銷售機會 {#quality-lead}

品質銷售機會：

* 負責傳遞品質；確保符合成功標準及使用者端定義的任何KPI。
* 定義品品質度、與所有利害關係人一致、制定測試計畫並確保其執行。
* 建立報表並傳送給專案關係人。

### 系統工程師 {#system-engineer}

系統工程師：

* 負責監督專案基礎結構。
* 負責：

   * 內部開發和測試環境的設定
   * 將這些系統與使用者端系統配對

* 提供硬體建議、監控各種實作，以及在上線前和之後提供操作支援。

### 安全性主管 {#security-lead}

安全性主管：

* 負責解決方案的整體安全性概念，確保符合客戶的任何需求和政策。
* 針對任何硬體式安全性概念（例如區域與防火牆），提供安全性概念、安全性作業與建議。

### 其他角色 {#other-persona}

* 利害關係人

   * 對專案成功有利害關係（股權）的人員（通常來自企業）。 他們經常會貢獻預算。

* 法律

   * 洽談合約時需要法律建議。

* 訓練人員

   * 根據專案的規模與性質，可利用專業教員為相關團隊制定與展示訓練課程。

* 技術作者

   * 根據專案的規模和性質，可以使用專業技術作者為特定群組編寫准則和手冊。 例如，供系統管理員使用的維護手冊或供作者使用的使用指南。

* 系統管理員

   * 負責系統的持續運作。

* 作者與一般使用者

   * 使用系統建立及維護您網站內容的人員。

## 必要檔案與交付專案 {#required-documents-and-deliverables}

檢查清單涵蓋每個里程碑的&#x200B;**必要檔案**&#x200B;和&#x200B;**交付專案**。

* 這些之間沒有1:1關係；例如，一組必要檔案可以產生單一交付專案。
* 來自一個角色的可交付成果可以是在相同里程碑期間另一個角色的必要檔案。

### 必要檔案 {#required-documents}

產生傳遞專案時，適當的角色需要&#x200B;**必要檔案**。

對於每個&#x200B;**必要檔案**，角色應該指出：

* **Y/N**：是否已經收到。
* **1-3**：所接收檔案的品質指示。

### 交付專案 {#deliverables}

對於每個里程碑，適當的角色會負責傳遞特定檔案，因此會實現其對於特定里程碑的職責。

對於每個&#x200B;**交付專案**，角色必須表示：

* **Y/N**：是否已完成。

傳遞專案經常被用作目前或之後里程碑的&#x200B;**必要檔案**。

## 相關最佳實務 {#related-best-practices}

如需部署、管理、開發或編寫的最佳實務，請參閱下列內容：

* 與管理AEM專案相關的其他最佳實務和准則：
   * [硬體大小調整准則](/help/managing/hardware-sizing-guidelines.md)
   * [企業 DevOps](/help/managing/enterprise-devops.md)
   * [SEO和URL管理最佳作法](/help/managing/seo-and-url-management.md)
   * [AEM與網頁協助工具准則](/help/managing/web-accessibility.md)
   * [一般資料保護規範](/help/managing/data-protection-and-privacy.md)* [部署及維護最佳實務](/help/sites-deploying/best-practices.md)
* [管理最佳實務](/help/sites-administering/administer-best-practices.md)
* [開發最佳實務](/help/sites-developing/best-practices.md)
* [製作最佳實務](/help/sites-authoring/best-practices.md)

## 重要檔案領域 {#key-documentation-areas}

* AEM檔案
此外，AEM檔案的下列章節也特別令人感興趣（不過，這份清單並非詳盡無遺）：

   * [安全性](/help/sites-developing/security.md)
   * [建議的部署](/help/sites-deploying/recommended-deploys.md)
   * [企業 DevOps](/help/managing/enterprise-devops.md)
   * [硬體大小](/help/managing/hardware-sizing-guidelines.md)
   * AEM的概念：

      * [開發 — 基本知識](/help/sites-developing/the-basics.md)
      * [MSM概念](/help/sites-administering/msm.md)
      * [HTML範本語言(HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=zh-Hant)

* 相關檔案

   * Adobe Experience Cloud - [規劃Adobe Experience Cloud](https://experienceleague.adobe.com/docs/core-services/interface/services/core-services.html?lang=zh-Hant)
