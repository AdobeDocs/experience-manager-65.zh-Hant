---
title: 規劃升級
seo-title: 規劃升級
description: 本文有助於在規劃升級時建立清楚的目標、階段和交AEM付成果。
seo-description: 本文有助於在規劃升級時建立清楚的目標、階段和交AEM付成果。
uuid: 6128ac53-4115-4262-82d9-a0ad7d498ea6
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 49210824-ad87-4b6a-9ae8-77dcfe2b5c06
docset: aem65
feature: 升級
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2448'
ht-degree: 0%

---


# 規劃升級{#planning-your-upgrade}

## AEM項目概述{#aem-project-overview}

常AEM用於高影響力的部署，可能為數百萬用戶服務。 在大多數情況下，有自訂應用程式會部署在例項上，這會增加複雜性。 升級此類部署的任何努力都必須有條不紊地處理。

本指南可協助您在規劃升級時建立清楚的目標、階段和交付項目。 它著重於整體項目執行和准則。 雖然它提供實際升級步驟的概觀，但是會參考適當的可用技術資源。 它應與檔案所述的可用技術資源一起使用。

升級流AEM程需要謹慎處理規劃、分析和執行階段，並為每個階段定義關鍵交付項。

請注意，您可以直接從AEM6.0版和6.5版升級。5.6.x及以下版本的客戶需要先升級至6.0或更新版本，建議使用6.0(SP3)。 此外，新的OAK區段Tar格式現在自6.3起用於區段節點商店，而資料庫移轉至此新格式是強制的，即使6.0、6.1和6.2亦然。

>[!CAUTION]
>
>如果您從AEM6.2升級至6.3，則應從版本(**6.2-SP1-CFP1 - -6.2SP1-CFP12.1**)或&#x200B;**6.2SP1-CFP15**&#x200B;升級。 否則，如果您要從&#x200B;**6.2SP1-CFP13/6.2SP1CFP14**&#x200B;升級至AEM6.3，您也必須至少升級至版本&#x200B;**6.3.2.2**。 否則，AEM Sites在升級後會失敗。

## 升級範圍和要求{#upgrade-scope-requirements}

以下是典型升級專案中受影響的區AEM域清單：

<table>
 <tbody>
  <tr>
   <td><strong>元件</strong></td>
   <td><strong>影響</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>作業系統</td>
   <td>不確定但微妙的影響</td>
   <td>升級時，可能AEM也是升級作業系統的時候，這可能會產生一些影響。</td>
  </tr>
  <tr>
   <td>Java執行時期</td>
   <td>適中影響</td>
   <td>AEM 6.3需要JRE 1.7.x（64位元）或更新版本。 JRE 1.8是目前Oracle唯一支援的版本。</td>
  </tr>
  <tr>
   <td>硬體</td>
   <td>適中影響</td>
   <td>聯機修訂清除需要等於儲存庫大小25%的可用磁碟空間和15%的可用堆空間<br />才能成功完成。 <br />您可能需要將硬體升級到<br />以確保有足夠的資源用於「線上修訂清除」以完全執行<br />。 此外，如果從6之前的版本升級，AEM則可能會有額外的儲存要求。<br /></td>
  </tr>
  <tr>
   <td>內容儲存庫（CRX或Oak）</td>
   <td>高影響力</td>
   <td>從6.1版開始，AEM不支援CRX2，因此從舊版升級時，需要移轉至<br /> Oak(CRX3)。 AEM 6.3 has<br />實作了新的段節點儲存，該儲存也需要遷移。 <br /> crx2oak工具就是用於此用途。</td>
  </tr>
  <tr>
   <td>元AEM件／內容</td>
   <td>適中影響</td>
   <td><code>/libs</code> 和<code>/apps</code>可透過升級輕鬆處理，但<code>/etc</code>通常需要手動重新應用自訂。</td>
  </tr>
  <tr>
   <td>服AEM務</td>
   <td>低影響</td>
   <td>大部分AEM核心服務都經過升級測試。 這是低衝擊的區域。</td>
  </tr>
  <tr>
   <td>自訂應用程式服務</td>
   <td>低到高影響</td>
   <td>視應用程式和自訂而定，可能會與JVM、作業系統版本和某些與索引相關的<br />變更有<br />相依性，因為索引不會在Oak中自動產生。</td>
  </tr>
  <tr>
   <td>自訂應用程式內容</td>
   <td>低到高影響</td>
   <td>在進行升級之前可以備份不通過升級處理的內容<br />，然後再將其移回儲存庫。<br /> 大部分的內容都可透過移轉工具處理。</td>
  </tr>
 </tbody>
</table>

請務必確保您正在運行受支援的作業系統、Java運行時、httpd和Dispatcher版本。 如需詳細資訊，請參閱[AEM 6.5技術需求頁面](/help/sites-deploying/technical-requirements.md)。 升級這些元件需要在您的專案計畫中加以說明，而且應在升級前進行AEM。

## 項目階段{#project-phases}

規劃和執行升級需要做很多工AEM作。 為了釐清這個過程中的不同努力，我們將規劃和執行練習分為不同的階段。 在以下各節中，每個階段都會產生一個交付內容，而項目的未來階段通常會利用它。

### Planning for Author Training {#planning-for-author-training}

在任何新版本中，UI和使用者工作流程都可能會有所變更。 此外，新版本還引入一些新功能，這些新功能可能有助於企業運用。 我們建議您檢閱已引入的功能變更，並組織計畫來培訓您的使用者有效運用這些變更。

![unu_schient](assets/unu_cropped.png)

6.5中AEM的新功能可在adobe.comAEM](/help/release-notes/release-notes.md)的[區段中找到。 請務必注意您組織中常用的UI或產品功能變更。 當您檢視這些新功能時，也請注意對您的組織有價值的功能。 檢視6.5版中的變AEM更後，為您的作者制定培訓計畫。 這可能包括運用免費提供的資源，例如[Adobe數位學習服務](https://www.adobe.com/training.html)提供的說明功能視訊或正式培訓。

### 建立測試計畫{#creating-a-test-plan}

每個客戶的實作都是獨AEM一無二的，而且已經過自訂，以符合其業務需求。 因此，務必確定對系統進行的所有自定義，以便將其納入測試計畫。 此測試計畫將為我們在升級實例上執行的QA過程提供動力。

![test-plan](assets/test-plan.png)

必須複製實際的生產環境，並在升級後對其執行測試，以確保所有應用程式和自訂程式碼仍視需要執行。 您需要重新執行所有自訂作業，並執行效能、負載和安全性測試。 在組織測試計畫時，請務必涵蓋已對系統進行的所有自訂設定，以及日常操作中運用的現成UI和工作流程。 這些功能包括自訂OSGI服務和servlet、與Adobe Marketing Cloud的整合、透過連接器與協力廠商的整合、自訂協力廠商的整合、自訂元件和範本、自訂UI覆蓋（在中）AEMAEM，以及自訂工作流程。 對於從6之前版本遷移的客戶AEM，應分析任何自定義查詢，因為這些查詢可能需要編製索引。 對於已使用6.x版本的客AEM戶，仍應測試這些查詢，以確保其索引在升級後仍能繼續有效運作。

### 確定需要的體系結構和基礎架構更改{#determining-architectural-and-infrastructure-changes-needed}

在升級時，您可能還需要升級技術堆棧中的其他元件，如作業系統或JVM。 此外，由於儲存庫結構的更改，可能需要額外的硬體。 這通常只適用於從6.x以前版本的例項移轉的客戶，但必須考慮。 最後，您的操作做法可能需要進行更改，包括監控、維護和備份和災難恢復過程。

![doi_schient](assets/doi_cropped.png)

檢閱6.5的技AEM術需求，並確保您目前的硬體和軟體已足夠。 如需作業程式的潛在變更，請參閱下列檔案：

**監控和維護：**

[操作儀表板](/help/sites-administering/operations-dashboard.md)

[Assets 監控最佳實務](/help/assets/assets-monitoring-best-practices.md)

[使用JMX控制台監控伺服器資源](/help/sites-administering/jmx-console.md)

[修訂清除](/help/sites-deploying/revision-cleanup.md)

**備份／恢復和災難恢復：**

[備份和還原](/help/sites-administering/backup-and-restore.md)

[效能與可擴充性](/help/sites-deploying/performance.md)

[如何使用AEMTarMK冷備用](/help/sites-deploying/tarmk-cold-standby.md)

#### 內容重組注意事項{#content-restructuring-considerations}

已AEM對儲存庫結構進行了更改，有助於使升級更順暢。 這些變更包括根據Adobe或客戶是否擁有內容，將內容從/etc檔案夾移出至資料夾（包括/libs、/apps和/content），以限制在發行期間覆寫內容的機率。 資料庫重組的方式是，在6.5升級時不需要變更程式碼，不過建議在規劃升級時，檢閱](/help/sites-deploying/repository-restructuring.md)中「資料庫重組」的AEM[詳細資訊。

### 評估升級複雜性{#assessing-upgrade-complexity}

由於我們的客戶在其環境中適用的自訂數量和性質多種多樣AEM，因此有必要先花一些時間確定在升級時應該付出的總體努力。

您可以採用兩種方法來評估升級的複雜性，初步階段只需使用新推出的模式偵測器，它可在您的AEM6.1、6.2和6.3執行個體上執行。 模式偵測器是使用報告的模式來評估升級整體複雜度最簡單的方式。 模式偵測器報表包含用於識別自訂程式碼基底正在使用之不可用API的模式（這是使用6.3中的升級前相容性檢查來完成）。

在初次評估後，更全面的下一步可能是對測試實例執行升級並執行一些基本煙霧測試。 Adobe也提供一些。 此外，[已過時和已移除功能](/help/release-notes/deprecated-removed-features.md)的清單不僅應該針對您要升級至的版本進行審查，而且應該針對源版本和目標版本之間的任何版本進行審查。 例如，如果從AEM6.2升級至6.5，除了6.5的功能以外，請務必檢閱AEM6.3已過時和已移除的功能AEM。

![trei_schient](assets/trei_cropped.png)

最近推出的圖樣偵測器(Pattern Detector)應能提供您相當精確的預估，以評估在大多數情況下的升級期間預期結果。 但是，對於更複雜的自訂和部署，如果您有不相容的變更，您可以根據[執行就地升級](/help/sites-deploying/in-place-upgrade.md)中的說明，將開發實例升級至AEM6.5。 完成後，在此環境上執行一些高級煙霧測試。 本練習的目的不是詳盡地完成測試案例清單並產生正式的缺陷清單，而是讓我們大致估計升級程式碼以達到6.5相容性所需的工作量。 當結合[模式檢測](/help/sites-deploying/pattern-detector.md)和在前一節中確定的體系結構變化時，可以向項目管理團隊提供粗略的估計，以規劃升級。

### 構建升級和回滾操作手冊{#building-the-upgrade-and-rollback-runbook}

雖然Adobe記錄了升級實例的過AEM程，但每個客戶的網路佈局、部署體系結構和自定義都需要對此方法進行微調和定制。 因此，我們鼓勵您檢閱我們提供的所有檔案，並使用它通知專案特定的操作手冊，其中概述您將在環境中遵循的特定升級和回滾程式。 如果從CRX2升級，請務必評估從CRX2移至Oak時，內容移轉所需的時間。 對於大型儲存庫，它可能相當龐大。

![操作手冊](assets/runbook-diagram.png)

我們在[升級過程](/help/sites-deploying/upgrade-procedure.md)中提供了升級和回滾過程，並在執行[就地升級](/help/sites-deploying/in-place-upgrade.md)中提供了應用升級的逐步說明。 這些說明應經過審查並考慮到您的系統體系結構、自定義和停機時間容限，以確定在升級期間將執行的適當切換和回滾過程。 在起草自訂的操作手冊時，應包含對架構或伺服器大小的任何變更。 必須指出，這應當作為第一稿處理。 當您的團隊完成其QA和開發週期並將升級部署至測試環境時，可能需要執行一些額外步驟。 理想情況下，本檔案應包含足夠的資訊，如果交給營運人員，他們就能完全從內含的資訊完成升級。

### 制定項目計畫{#developing-a-project-plan}

我們可使用先前練習的輸出來建立涵蓋測試或開發工作、訓練和實際升級執行所需時間的專案計畫。

![開發——專案——計畫](assets/develop-project-plan.png)

綜合項目計畫應包括：

* 最後確定開發和測試計畫
* 升級開發和QA環境
* 更新6.5的自訂程AEM式碼庫
* QA測試和修正週期
* 升級測試環境
* 整合、效能與負載測試
* 環境認證
* 上線

### 執行開發和QA {#performing-development-and-qa}

我們提供了與6.5相容的[升級代碼和自定義](/help/sites-deploying/upgrading-code-and-customizations.md)AEM的過程。當執行此反覆程式時，應視需要變更操作手冊。 另請參閱6.5](/help/sites-deploying/backward-compatibility.md)中的[向後相容AEM性，瞭解在大多數情況下，如何讓自訂內容保持向後相容，而不需在升級後立即進行開發。

![patru_schient](assets/patru_cropped.png)

開發和測試過程通常是一個迭代過程。 由於自訂，升級期間所做的變更可能會使整個產品區段無法使用。 一旦開發人員解決問題的根本原因，且測試團隊可以存取這些功能，就有可能發現其他問題。 當發現需要調整升級程式的問題時，請務必將它們新增至您的自訂升級操作手冊。 經過幾次反複測試和修正後，程式碼庫應經過完整驗證，並可部署至測試環境。

### 最終測試{#final-testing}

我們建議在您的組織的QA團隊認證程式碼基底後進行最後一輪測試。 本輪測試將包括在測試環境中驗證您的操作手冊，接著進行使用者接受度、效能和安全性測試。

![cinci_schient](assets/cinci_cropped.png)

此步驟至關重要，因為這是您唯一能夠針對類似生產環境驗證操作手冊中的步驟的時間。 在環境升級後，請務必讓使用者有時間登入，並在日常活動中使用系統時，執行其所執行的活動。 使用者運用先前未考慮的系統部分並不少見。 在上線前找出並修正這些區域的問題，可協助防止昂貴的生產中斷。 由於新版本包含對AEM基礎平台的重大變更，因此在系統上執行效能、負載和安全性測試也很重要，就像我們第一次啟動它一樣。

### 執行升級{#performing-the-upgrade}

一旦收到所有利益相關者的最終簽名，就應該對已定義的操作手冊程式執行。 我們在[升級過程](/help/sites-deploying/upgrade-procedure.md)中提供了升級和回滾的步驟，並在執行[就地升級](/help/sites-deploying/in-place-upgrade.md)作為參考點中提供了安裝步驟。

![執行升級](assets/perform-upgrade.png)

我們在環境驗證的升級說明中提供了一些步驟。 這些檢查包括掃描升級日誌和驗證所有OSGi捆綁包是否已正確啟動等基本檢查，但我們建議您也根據業務流程使用自己的測試案例進行驗證。 我們也建議檢查「線上修訂清AEM除」和相關常式的排程，以確保這些常式會發生在您公司的安靜時間。 這些常式對於長期效能至關重要AEM。
