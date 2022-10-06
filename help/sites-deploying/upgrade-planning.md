---
title: 規劃升級
seo-title: Planning Your Upgrade
description: 本文有助於在規劃AEM升級時，明確目標、階段和交付項目。
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

# 規劃升級{#planning-your-upgrade}

## AEM專案概述 {#aem-project-overview}

AEM常用於可能為數百萬使用者提供高影響力的部署。 在大多數情況下，會部署在執行個體上的自訂應用程式，這會增加複雜性。 升級此類部署的任何工作都需有條不紊地處理。

本指南有助於在規劃升級時建立明確的目標、階段和交付項。 它著重於整體專案執行和准則。 雖然提供實際升級步驟的概觀，但在適當時參考可用的技術資源。 它應與檔案中提及的可用技術資源一起使用。

AEM升級流程需要謹慎處理規劃、分析和執行階段，並為每個階段定義關鍵交付件。

請注意，可以直接從AEM 6.0版和最高6.5版升級。執行5.6.x及以下版本的客戶需先升級至6.0或更新版本，並建議使用6.0(SP3)。 此外，自6.3版起，新的OAK區段Tar格式會用於區段節點存放區，且即使是6.0、6.1和6.2版，存放庫也必須移轉至此新格式。

>[!CAUTION]
>
>如果您要從AEM 6.2升級至6.3，應從版本(**6.2-SP1-CFP1 —6.2SP1-CFP12.1**)或 **6.2SP1-CFP15** 向前。 否則，如果您要從 **6.2SP1-CFP13/6.2SP1CFP14** 至AEM 6.3，您也必須升級至至少版本 **6.3.2.2**. 否則，AEM Sites在升級後會失敗。

## 升級範圍和要求 {#upgrade-scope-requirements}

以下是典型AEM升級專案中受影響區域的清單：

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
   <td>在AEM升級時，也許該升級作業系統了，這可能會產生一些影響。</td>
  </tr>
  <tr>
   <td>Java運行時</td>
   <td>適度影響</td>
   <td>AEM 6.3需要JRE 1.7.x（64位）或更高版本。 JRE 1.8是Oracle當前唯一支援的版本。</td>
  </tr>
  <tr>
   <td>硬體</td>
   <td>適度影響</td>
   <td>線上修訂清除需要免費<br /> 磁碟空間等於儲存庫大小的25%，可用堆空間為15%<br /> 成功完成。 您可能需要將硬體升級到<br /> 確保有足夠的資源用於線上修訂清除，以完全<br /> 執行。 此外，如果從AEM 6之前的版本升級，請前往<br /> 可能是其他儲存需求。</td>
  </tr>
  <tr>
   <td>內容存放庫（CRX或Oak）</td>
   <td>高影響</td>
   <td>從6.1版開始，AEM不支援CRX2，因此請移轉至<br /> 從舊版升級時需要Oak(CRX3)。 AEM 6.3有<br /> 實作新的「區段節點存放區」，此時也需要移轉。 此<br /> crx2oak工具就用於此用途。</td>
  </tr>
  <tr>
   <td>AEM元件/內容</td>
   <td>適度影響</td>
   <td><code>/libs</code> 和 <code>/apps</code> 易於通過升級處理，但 <code>/etc</code> 通常需要手動重新應用自定義項。</td>
  </tr>
  <tr>
   <td>AEM服務</td>
   <td>低影響</td>
   <td>大部分的AEM核心服務都經過升級測試。 這是低衝擊區。</td>
  </tr>
  <tr>
   <td>自訂應用程式服務</td>
   <td>低到高影響</td>
   <td>根據應用程式和自訂，可能<br /> 對JVM、作業系統版本和某些相關索引的依賴<br /> 變更，因為索引不會在Oak中自動產生。</td>
  </tr>
  <tr>
   <td>自訂應用程式內容</td>
   <td>低到高影響</td>
   <td>無法通過升級處理的內容可以備份<br /> 升級前，再移回存放庫。<br /> 大部分內容都可透過移轉工具處理。</td>
  </tr>
 </tbody>
</table>

請務必確保您執行的是支援的作業系統、Java執行階段、httpd和Dispatcher版本。 如需詳細資訊，請參閱 [AEM 6.5技術需求頁面](/help/sites-deploying/technical-requirements.md). 升級這些元件需要列入您的專案計畫，且應先進行，再升級AEM。

## 專案階段 {#project-phases}

規劃和執行AEM升級需花費大量工作。 為了澄清這一過程中的不同努力，我們將規劃和執行練習細分為不同的階段。 在以下各節中，每個階段都會產生一個交付項，該交付項經常被項目的未來階段利用。

### 製作培訓計畫 {#planning-for-author-training}

隨著任何新版本推出，UI和使用者工作流程都可能會有所變更。 此外，新版本也推出可能對業務有利的新功能。 建議您檢閱已導入的功能變更，並組織計畫，以訓練使用者有效運用這些變更。

![unu_scient](assets/unu_cropped.png)

若需AEM 6.5的新功能，請參閱 [adobe.com的AEM區段](/help/release-notes/release-notes.md). 請務必留意貴組織中常用的UI或產品功能變更。 當您查看新功能時，也請留意任何對您的組織有價值的功能。 查看AEM 6.5中的變更後，為作者制定訓練計畫。 這可能包括利用免費提供的資源，例如透過提供的說明功能影片或正式培訓 [Adobe數位學習服務](https://www.adobe.com/training.html).

### 建立測試計畫 {#creating-a-test-plan}

每個客戶的AEM實作都是獨特的，而且經過自訂，可符合其業務需求。 因此，請務必判斷已對系統進行的所有自訂項目，以便納入測試計畫。 此測試計畫將支援我們在升級執行個體上執行的QA程式。

![測試計畫](assets/test-plan.png)

需要複製確切的生產環境，並在升級後對其執行測試，以確保所有應用程式和自訂程式碼仍可視需要執行。 您需要回復所有自訂，並執行效能、負載和安全性測試。 組織您的測試計畫時，除了現成可用的UI和工作流程外，請務必涵蓋已對系統進行的所有自訂項目，這些UI和工作流程會在日常操作中運用。 這些功能包括自訂OSGI服務和servlet、Adobe Marketing Cloud的整合、透過AEM連接器與協力廠商的整合、自訂協力廠商整合、自訂元件和範本、AEM中的自訂UI覆蓋，以及自訂工作流程。 對於從AEM 6之前的版本移轉的客戶，應分析任何自訂查詢，因為這些查詢可能需要編列索引。 對於已使用AEM 6.x版的客戶，仍應測試這些查詢，以確保其索引在升級後能繼續有效運作。

### 確定需要的體系結構和基礎架構更改 {#determining-architectural-and-infrastructure-changes-needed}

升級時，您可能還需要升級技術堆棧中的其他元件，如作業系統或JVM。 此外，由於儲存庫組成的更改，可能需要額外的硬體。 這通常只適用於從6.x之前的例項移轉的客戶，但請務必考慮。 最後，您的操作做法可能需要一些更改，包括監控、維護以及備份和災難恢復過程。

![doi_scient](assets/doi_cropped.png)

檢閱AEM 6.5的技術需求，並確保您目前的硬體和軟體已足夠。 有關操作流程的潛在更改，請參閱以下文檔：

**監控與維護：**

[操作儀表板](/help/sites-administering/operations-dashboard.md)

[Assets 監控最佳實務](/help/assets/assets-monitoring-best-practices.md)

[使用JMX控制台監視伺服器資源](/help/sites-administering/jmx-console.md)

[修訂清除](/help/sites-deploying/revision-cleanup.md)

**備份/恢復和災難恢復：**

[備份和還原](/help/sites-administering/backup-and-restore.md)

[效能和可擴充性](/help/sites-deploying/performance.md)

[如何使用TarMK冷待機執行AEM](/help/sites-deploying/tarmk-cold-standby.md)

#### 內容重新調整考量事項 {#content-restructuring-considerations}

AEM已對存放庫結構進行變更，有助於更順暢地升級。 這些更改涉及根據Adobe或客戶是否擁有該內容，將內容從/etc資料夾移出到包括/libs、/apps和/content的資料夾，從而限制在發行期間覆蓋內容的可能性。 重新整理存放庫的方式，使得6.5升級時不需要變更程式碼，不過建議您檢閱 [AEM中的存放庫重新調整](/help/sites-deploying/repository-restructuring.md) 進行升級時。

### 評估升級複雜性 {#assessing-upgrade-complexity}

由於我們的客戶在其AEM環境中所套用的自訂數量和性質種類繁多，因此請務必事先花一些時間，以決定您在升級時應該採取的整體工作量。

您可以採取兩種方法來評估升級的複雜性，初步階段只需使用新推出的模式偵測器，此偵測器可在AEM 6.1、6.2和6.3執行個體上執行。 模式檢測器是使用報告的模式評估升級的整體複雜性的最簡單方法。 模式偵測器報表包含用於識別自訂程式碼基底正在使用之不可用API的模式（這是使用6.3中的升級前相容性檢查來完成）。

在初次評估後，更全面的下一步可能是對測試實例執行升級並執行一些基本的煙霧測試。 Adobe也提供一些。 此外， [過時和移除的功能](/help/release-notes/deprecated-removed-features.md) 不僅應針對您要升級至的版本進行審核，也應針對來源版本與目標版本之間的任何版本進行審核。 例如，如果從AEM 6.2升級至6.5，除了AEM 6.5的功能外，請務必檢閱AEM 6.3已棄用和已移除的功能。

![trei_scount](assets/trei_cropped.png)

最近推出的模式偵測器，應能相當精確地預估大部分情況下在升級期間的預期結果。 不過，若是您有不相容變更的更複雜自訂和部署，您可以根據 [執行就地升級](/help/sites-deploying/in-place-upgrade.md). 完成後，對此環境執行一些高級煙霧測試。 本練習的目的不是詳盡地完成測試用例清單並生成缺陷的正式清單，而是讓我們粗略地估計要升級代碼以獲得6.5相容性所需的工作量。 結合 [圖樣偵測](/help/sites-deploying/pattern-detector.md) 在前一節中確定的體系結構更改，可向項目管理小組提供粗略估計，以規劃升級。

### 構建升級和回滾Runbook {#building-the-upgrade-and-rollback-runbook}

雖然Adobe已記錄升級AEM執行個體的程式，但每個客戶的網路配置、部署架構和自訂都需要對此方法進行微調和定制。 因此，我們鼓勵您審閱我們提供的所有文檔，並使用它來通知項目特定的Runbook，該Runbook概述您將在您的環境中遵循的特定升級和回滾過程。 如果從CRX2升級，請務必評估從CRX2移轉至Oak時，內容移轉需要多久的時間。 對於大型存放庫而言，這可能是相當可觀的。

![runbook-diagram](assets/runbook-diagram.png)

我們已在 [升級程式](/help/sites-deploying/upgrade-procedure.md) 以及在執行 [就地升級](/help/sites-deploying/in-place-upgrade.md). 您應審查這些指示，並考慮您的系統架構、自定義和停機容限，以確定在升級期間要執行的適當的切換和回滾過程。 起草自定義Runbook時，應包括對體系結構或伺服器大小的任何更改。 必須指出，應將此作為第一稿。 當您的團隊完成其QA和開發週期，並部署升級至測試環境時，可能需要執行一些其他步驟。 理想情況下，本文檔應包含足夠的資訊，這樣，如果將資訊交給您的運營人員，他們就能夠從內包含的資訊中完全完成升級。

### 制定項目計畫 {#developing-a-project-plan}

我們可以利用前次練習的成果來構建一個項目計畫，涵蓋測試或開發工作、培訓和實際升級執行的預期時間。

![開發項目計畫](assets/develop-project-plan.png)

綜合項目計畫應包括：

* 最後確定發展和測試計畫
* 升級開發和QA環境
* 更新AEM 6.5的自訂程式碼基底
* QA測試和修正週期
* 升級中繼環境
* 整合、效能和負載測試
* 環境認證
* 上線

### 執行開發和QA {#performing-development-and-qa}

我們為 [升級程式碼和自訂](/help/sites-deploying/upgrading-code-and-customizations.md) 與AEM 6.5相容。在執行此迭代過程時，應根據需要對Runbook進行更改。 另請參閱 [AEM 6.5的向後相容性](/help/sites-deploying/backward-compatibility.md) 關於您的自訂項目在大多數情況下可持續向後相容，而不需在升級後立即開發的資訊。

![patru_scount](assets/patru_cropped.png)

開發和測試過程通常是迭代過程。 由於自定義，升級期間所做的更改可能會使產品的整個部分不可用。 一旦開發人員解決了問題的根本原因，且測試團隊可以存取測試這些功能，就有可能發現其他問題。 當發現需要調整升級過程的問題時，請確保將它們添加到自定義升級Runbook中。 經過數次反覆測試和修正後，程式碼基底應經過完整驗證，並可部署至測試環境。

### 最終測試 {#final-testing}

建議在程式碼基底經過貴組織的QA團隊認證後進行最後一輪測試。 這一輪測試將涉及在測試環境中驗證您的Runbook，然後是用戶接受、效能和安全性測試。

![cinci_scient](assets/cinci_cropped.png)

此步驟非常重要，因為這是您能夠針對類似生產環境驗證Runbook中的步驟的唯一一次。 環境升級後，請務必讓使用者有時間登入，並在日常活動中使用系統時進行活動。 使用者運用先前未考慮之系統部分的情況並不少見。 在上線前發現並糾正這些領域的問題有助於防止成本高昂的生產中斷。 由於新版AEM對基礎平台有重大變更，因此在系統上執行效能、負載和安全性測試也很重要，就像我們第一次啟動它一樣。

### 執行升級 {#performing-the-upgrade}

從所有利益相關方收到最終簽核後，就可以對已定義的Runbook過程執行。 我們已提供在 [升級程式](/help/sites-deploying/upgrade-procedure.md) 和安裝步驟(在 [就地升級](/help/sites-deploying/in-place-upgrade.md) 作為參考點。

![執行升級](assets/perform-upgrade.png)

我們已在環境驗證的升級指示中提供一些步驟。 這些檢查包括掃描升級日誌和驗證所有OSGi套件組合是否已正確啟動等基本檢查，但我們建議您根據業務流程使用您自己的測試案例進行驗證。 我們也建議檢查AEM線上修訂清除的排程和相關常式，以確保這些動作會在您公司的安靜時間發生。 這些常式對於AEM的長期效能至關重要。
