---
title: 計畫升級
seo-title: Planning Your Upgrade
description: 本文有助於在規劃升級時建立明確的目標、階段和交AEM付件。
seo-description: This article helps establish clear goals, phases and deliverables when planning the AEM upgrade.
uuid: 6128ac53-4115-4262-82d9-a0ad7d498ea6
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 49210824-ad87-4b6a-9ae8-77dcfe2b5c06
docset: aem65
feature: Upgrading
exl-id: 0dea2b3e-fd7c-4811-a04a-6852ffc1e6d6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2430'
ht-degree: 0%

---

# 計畫升級{#planning-your-upgrade}

## 項AEM目概述 {#aem-project-overview}

常AEM用於可能為數百萬用戶服務的高影響部署。 大多數情況下，在實例上部署了自定義應用程式，這增加了複雜性。 升級此類部署的任何工作都需要有條不紊地處理。

本指南有助於在規劃升級時確定明確的目標、階段和交付項。 它側重於整個項目執行和指導方針。 它提供了實際升級步驟的概述，但在適當情況下，它指的是可用的技術資源。 它應與檔案中提到的現有技術資源一起使用。

升級AEM過程需要仔細處理規劃、分析和執行階段，並為每個階段定義關鍵交付項。

請注意，可以直接從6.0版AEM和最高6.5版升級。運行5.6.x及以下版本的客戶需要首先升級到6.0或更高版本，建議使用6.0(SP3)。 此外，自6.3以來，新的OAK段Tar格式現在用於段節點儲存，而且即使對於6.0、6.1和6.2，也必須將儲存庫遷移到此新格式。

>[!CAUTION]
>
>如果從6.2升AEM級到6.3，則應從版本(**6.2-SP1-CFP1 —6.2SP1-CFP12.1**)或 **6.2SP1-CFP15** 向前。 否則，如果要從 **6.2SP1-CFP13/6.2SP1CFP14** 至AEM6.3，您還必須至少升級 **6.3.2.2**。 否則，AEM Sites升級後會失敗。

## 升級範圍和要求 {#upgrade-scope-requirements}

在下面，您將找到一個受典型升級項目影響的AEM區域清單：

<table>
 <tbody>
  <tr>
   <td><strong>Component</strong></td>
   <td><strong>影響</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>作業系統</td>
   <td>不確定但微妙的影響</td>
   <td>在升級時，AEM可能也該升級作業系統了，這可能會產生一些影響。</td>
  </tr>
  <tr>
   <td>Java運行時</td>
   <td>中等影響</td>
   <td>AEM 6.3需要JRE 1.7.x（64位）或更高版本。 JRE 1.8是Oracle當前支援的唯一版本。</td>
  </tr>
  <tr>
   <td>硬體</td>
   <td>中等影響</td>
   <td>聯機修訂版清除需要免費<br /> 磁碟空間等於儲存庫大小的25%和可用堆空間的15%<br /> 成功完成。 您可能需要將硬體升級到<br /> 確保有足夠的資源用於線上修訂版清理，以完全<br /> 執行。 此外，如果從6之前的版本升AEM級，<br /> 可能是其他儲存要求。</td>
  </tr>
  <tr>
   <td>內容儲存庫（CRX或Oak）</td>
   <td>高影響</td>
   <td>從6.1版開始，AEM不支援CRX2，因此遷移到<br /> 從舊版本升級時需要Oak(CRX3)。 AEM6.3<br /> 實現了新的段節點儲存，這也需要遷移。 的<br /> crx2oak工具用於此目的。</td>
  </tr>
  <tr>
   <td>組AEM件/內容</td>
   <td>中等影響</td>
   <td><code>/libs</code> 和 <code>/apps</code> 易於通過升級處理，但 <code>/etc</code> 通常需要手動重新應用自定義項。</td>
  </tr>
  <tr>
   <td>服AEM務</td>
   <td>低影響</td>
   <td>大多數AEM核心服務都經過升級測試。 這是一個衝擊小的區域。</td>
  </tr>
  <tr>
   <td>自定義應用程式服務</td>
   <td>低到高衝擊</td>
   <td>根據應用程式和自定義，可能<br /> 與JVM、作業系統版本和某些索引相關的依賴項<br /> 更改，因為索引不會在Oak中自動生成。</td>
  </tr>
  <tr>
   <td>自定義應用程式內容</td>
   <td>低到高衝擊</td>
   <td>無法通過升級處理的內容可以備份<br /> 升級之前，然後移回儲存庫。<br /> 大多數內容都可以通過遷移工具處理。</td>
  </tr>
 </tbody>
</table>

確保您運行的是受支援的作業系統、Java運行時、httpd和Dispatcher版本，這一點非常重要。 有關詳細資訊，請參見 [AEM6.5技術要求頁](/help/sites-deploying/technical-requirements.md)。 升級這些元件需要在您的項目計畫中進行說明，並應在升級之前進AEM行。

## 項目階段 {#project-phases}

在規劃和執行升級方面需要做很多AEM工作。 為了明確這一過程中的不同努力，我們將規劃和執行工作分為不同的階段。 在下面各節中，每個階段都會生成交付項，該項目的未來階段通常利用交付項。

### 編寫者培訓計畫 {#planning-for-author-training}

對於任何新版本，都可能會對UI和用戶工作流進行潛在更改。 此外，新版本還引入了一些新功能，這些功能可能對企業有利。 我們建議您查看已引入的功能更改，並組織計畫來培訓您的用戶如何有效利用這些更改。

![unu_screntd](assets/unu_cropped.png)

6.5中AEM的新功能可在 [adobeAEM.com的部分](/help/release-notes/release-notes.md)。 請務必注意對組織中常用的UI或產品功能的任何更改。 當您查看新功能時，還要注意任何對您的組織有價值的功能。 查看6.5中的變AEM化後，為您的作者制定培訓計畫。 這可能涉及利用免費可用資源，如通過以下方式提供的幫助功能視頻或正式培訓 [Adobe數字學習服務](https://www.adobe.com/training.html)。

### 建立Test計畫 {#creating-a-test-plan}

每個客戶的實施AEM都是獨特的，而且已定制以滿足其業務需求。 因此，必須確定對系統進行的所有自定義，以便將這些自定義包含在test計畫中。 此test計畫將為我們在升級實例上執行的QA過程提供動力。

![test計畫](assets/test-plan.png)

需要複製確切的生產環境，並在升級後對其執行測試，以確保所有應用程式和自定義代碼仍按需要運行。 您需要重新執行所有定制，並執行效能、負載和安全測試。 在組織test計畫時，確保除了在日常操作中使用的開箱UI和工作流外，還包括對系統進行的所有自定義。 這些功能可包括定制OSGI服務和Servlet、與Adobe Marketing Cloud的整合、通過連接器與第AEM三方的整合、定制第三方整合、定制元件和模板、定制UI覆蓋AEM以及定制工作流。 對於從6之前版本遷移的客戶AEM，應分析任何自定義查詢，因為可能需要對這些查詢進行索引。 對於已使用6.x版AEM本的客戶，仍應測試這些查詢，以確保其索引在升級後繼續有效工作。

### 確定所需的體系結構和基礎架構更改 {#determining-architectural-and-infrastructure-changes-needed}

升級時，可能還需要升級技術堆棧中的其他元件，如作業系統或JVM。 此外，由於儲存庫中的更改，可能需要額外的硬體。 這通常只適用於從6.x之前的實例進行遷移的客戶，但是必須考慮這一點。 最後，您的操作實踐可能需要一些更改，包括監控、維護以及備份和災難恢復過程。

![doi_screntd](assets/doi_cropped.png)

查看6.5的技AEM術要求，確保您當前的硬體和軟體足夠。 有關操作流程的潛在更改，請參閱以下文檔：

**監控和維護：**

[操作儀表板](/help/sites-administering/operations-dashboard.md)

[Assets 監控最佳實務](/help/assets/assets-monitoring-best-practices.md)

[使用JMX控制台監視伺服器資源](/help/sites-administering/jmx-console.md)

[修訂清除](/help/sites-deploying/revision-cleanup.md)

**備份/恢復和災難恢復：**

[備份和還原](/help/sites-administering/backup-and-restore.md)

[效能和可擴充性](/help/sites-deploying/performance.md)

[TarMK冷備AEM用如何運行](/help/sites-deploying/tarmk-cold-standby.md)

#### 內容重組注意事項 {#content-restructuring-considerations}

已AEM對儲存庫結構進行了更改，有助於使升級更加無縫。 這些更改涉及根據內容是Adobe還是客戶擁有，將內容從/etc資料夾移出到包括/libs 、 /apps和/content的資料夾，從而限制了在發佈期間覆蓋內容的機會。 資料庫重組的方式是，在6.5升級時不需要更改代碼，但建議在以下位置查看詳細資訊： [中的儲存庫重AEM組](/help/sites-deploying/repository-restructuring.md) 計畫升級時。

### 評估升級複雜性 {#assessing-upgrade-complexity}

由於我們的客戶在其環境中應用的定製數量和性質多種多樣AEM，因此有必要提前一段時間確定在升級中應期望的總體工作級別。

您可以採用兩種方法來評估升級的複雜性，一個初步階段只需使用新引入的模式檢測器即可，該檢測器可在您的AEM6.1、6.2和6.3實例上運行。 模式檢測器是使用報告的模式評估預期升級的整體複雜性的最簡單方法。 模式檢測器報告包括用於識別自定義代碼庫正在使用的不可用API的模式（這是在6.3中使用升級前相容性檢查完成的）。

在初始評估後，下一步可能是對test實例執行升級並執行一些基本煙霧測試。 Adobe也提供了一些。 此外， [已棄用和已刪除的功能](/help/release-notes/deprecated-removed-features.md) 不僅應查看要升級到的版本，還應查看源版本和目標版本之間的任何版本。 例如，如果從AEM6.2升級到6.5，則除了6.5的功能外，還要查看AEM6.3已棄用和已刪除的功能，這一點非常重要AEM。

![trei_scrientd](assets/trei_cropped.png)

最近引入的模式檢測器應該能夠相當準確地估計大多數情況下在升級期間的預期。 但是，對於更複雜的自定義和部署，如果您有不相容的更改，您可以根據中的說明將開發實例AEM升級到6.5 [執行就地升級](/help/sites-deploying/in-place-upgrade.md)。 完成後，對此環境執行一些高級煙霧測試。 本練習的目的不是全面完成test案例清單並生成正式缺陷清單，而是為我們粗略估計升級代碼以實現6.5相容性所需的工作量。 與 [圖案檢測](/help/sites-deploying/pattern-detector.md) 以及前一部分確定的體系結構更改，可以向項目管理團隊提供粗略的評估，以規劃升級。

### 生成升級和回滾Runbook {#building-the-upgrade-and-rollback-runbook}

雖然Adobe已記錄了升級實例的過程AEM，但每個客戶的網路佈局、部署體系結構和自定義都需要對此方法進行微調和定制。 因此，我們鼓勵您查看我們提供的所有文檔，並使用它通知項目特定的Runbook，該Runbook概括了您將在環境中遵循的特定升級和回滾過程。 如果從CRX2升級，請確保評估從CRX2遷移到Oak時內容遷移需要多長時間。 對於大型儲存庫而言，這可能是一件大事。

![Runbook圖](assets/runbook-diagram.png)

我們在中提供了升級和回滾過程 [升級過程](/help/sites-deploying/upgrade-procedure.md) 以及在執行升級時應用升級的逐步說明 [就地升級](/help/sites-deploying/in-place-upgrade.md)。 這些說明應與您的系統體系結構、自定義設定和停機時間容限一起審查和考慮，以確定在升級過程中要執行的適當的切換和回滾過程。 在起草自定義Runbook時，應包括對體系結構或伺服器大小的任何更改。 必須指出，這應當作為第一稿處理。 當您的團隊完成其QA和開發週期並部署升級到臨時環境時，可能需要執行一些其他步驟。 理想情況下，本文檔應包含足夠的資訊，這樣，如果將資訊交給您的操作人員，他們就可以完全從中包含的資訊完成升級。

### 制定項目計畫 {#developing-a-project-plan}

我們可以使用先前練習的結果來構建一個項目計畫，涵蓋test或開發工作、培訓和實際升級執行的預期時間表。

![開發項目計畫](assets/develop-project-plan.png)

綜合項目計畫應包括：

* 最後確定發展和test計畫
* 升級開發和QA環境
* 更新6.5的自定義AEM代碼庫
* QAtest和修復週期
* 升級暫存環境
* 整合、效能和負載測試
* 環境認證
* 上線

### 執行開發和QA {#performing-development-and-qa}

我們已提供 [升級代碼和自定義](/help/sites-deploying/upgrading-code-and-customizations.md) 與6AEM.5相容。執行此迭代過程時，應根據需要對Runbook進行更改。 另請參閱 [6.5中的AEM向後相容性](/help/sites-deploying/backward-compatibility.md) 有關在大多數情況下如何向後相容自定義的資訊，無需在升級後立即進行開發。

![patru_scrientd](assets/patru_cropped.png)

開發和測試過程通常是一個迭代過程。 由於自定義，升級期間所做的更改可能會使產品的整個部分無法使用。 一旦開發人員解決了問題的根本原因，並且測試團隊有權test這些功能，就有可能發現其他問題。 發現需要調整升級過程的問題時，請確保將它們添加到自定義升級Runbook中。 經過多次測試和修復，代碼庫應經過完全驗證並準備好部署到臨時環境。

### 最終測試 {#final-testing}

我們建議在代碼庫經貴組織的QA團隊認證後進行最後一輪測試。 此輪測試將涉及在轉移環境上驗證您的Runbook，然後進行幾輪用戶接受、效能和安全性測試。

![cinci_scrientd](assets/cinci_cropped.png)

此步驟至關重要，因為這是您能夠針對類似生產的環境驗證Runbook中的步驟的唯一時間。 環境升級後，讓最終用戶有時間登錄並完成在日常活動中使用系統時所執行的活動，這一點非常重要。 用戶利用以前未考慮過的一部分系統的情況並不少見。 在投入使用前發現和糾正這些領域的問題有助於防止成本高昂的生產中斷。 由於新版本AEM包含對基礎平台的重大更改，因此在系統上執行效能、負載和安全test也很重要，就像我們第一次啟動它一樣。

### 執行升級 {#performing-the-upgrade}

一旦從所有利益相關方接收到最終簽名，就該對已定義的Runbook過程執行了。 我們提供了升級和回滾的步驟 [升級過程](/help/sites-deploying/upgrade-procedure.md) 以及執行 [就地升級](/help/sites-deploying/in-place-upgrade.md) 作為參照點。

![執行升級](assets/perform-upgrade.png)

我們已在升級說明中提供了一些環境驗證步驟。 這些檢查包括掃描升級日誌和驗證所有OSGi捆綁包是否已正確啟動等基本檢查，但我們建議還根據您的業務流程使用您自己的test案例進行驗證。 我們還建議檢查聯機修訂版清AEM理和相關常式的計畫，以確保它們在您公司的安靜時間內發生。 這些例行程式對於公司的長期業績至關重要AEM。
