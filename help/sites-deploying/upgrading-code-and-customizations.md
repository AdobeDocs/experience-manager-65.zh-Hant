---
title: 升級程式碼和自訂
seo-title: 升級程式碼和自訂
description: 進一步瞭解如何升級自訂程式碼AEM。
seo-description: 進一步瞭解如何升級自訂程式碼AEM。
uuid: dec11ef0-bf85-4e4e-80ac-dcb94cc3c256
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 59780112-6a9b-4de2-bf65-f026c8c74a31
docset: aem65
targetaudience: target-audience upgrader
feature: 升級
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2205'
ht-degree: 0%

---


# 升級代碼和自定義{#upgrading-code-and-customizations}

在規劃升級時，需要調查並解決實施的下列領域。

* [升級程式碼庫](#upgrade-code-base)
* [與6.5儲存庫結構對齊](#align-repository-structure)
* [自AEM訂](#aem-customizations)
* [測試程式](#testing-procedure)

## 概覽 {#overview}

1. **模式偵測器**  [](/help/sites-deploying/pattern-detector.md) -如升級規劃中所述及本頁中所述執行模式偵測器，以取得模式偵測器報表，其中包含除了Target版本中無法使用的API/組合以外，還需要解決的區域的詳細資訊AEM。「模式偵測」報表應指出程式碼中有任何不相容之處，如果沒有相容，則您的部署已相容於6.5，您仍可選擇使用6.5功能進行新開發，但您不需要它來維持相容性。 如果報告了不相容性，則可以選擇a)以相容性模式運行，並推遲開發新6.5功能或相容性； b)在升級後決定進行開發，然後轉到步驟2。 請參閱[6.5](/help/sites-deploying/backward-compatibility.md)中的AEM向後相容性，以取得詳細資訊。

1. **開發6.5版的程式碼庫**-為Target版本的程式碼庫建立專用的分支或儲存庫。 使用升級前相容性的資訊來規劃要更新的程式碼區域。
1. **使用6.5 Uberjar編譯**-將代碼庫POM更新為指向6.5 Uberjar並編譯代碼。
1. **更新AEM自訂*** - *對的任何自訂或擴充功AEM能應更新／驗證，以便在6.5版中運作，並新增至6.5版程式碼庫。包含UI搜尋Forms、資產自訂、任何使用/mnt/overlay的項目

1. **部署至6.5環境** -在Dev/QA環境中，AEM應啟用6.5（作者+發佈）的簡潔實例。應部署更新的程式碼庫和代表性的內容範例（來自目前的生產環境）。
1. **QA驗證和錯誤修正** - QA應驗證6.5作者和發佈例項的應用程式。發現的任何錯誤都應修正並提交至6.5程式碼庫。視需要重複「開發週期」，直到修正所有錯誤。

在繼續升級之前，您應擁有穩定的應用程式碼庫，並已針對目標版本的完整測試AEM。 根據測試中的觀察，可以有方法最佳化自訂程式碼。 這可能包括重構代碼以避免遍歷儲存庫、自定義索引以優化搜索，或在JCR中使用無序節點等。

除了升級程式碼庫和自訂以搭配新版本使用的選項外AEM, 6.5還可協助您使用[本頁](/help/sites-deploying/backward-compatibility.md)所述的「向後相容性」功能，更有效率地管理自訂。

如上圖所示，在第一步中運行[模式檢測器](/help/sites-deploying/pattern-detector.md)將幫助您評估升級的整體複雜性，以及您是否要在相容模式下運行或更新自定義以使用所有新的AEM6.5功能。 如需詳細資訊，請參閱6.5&lt;a1/AEM>中的[向後相容性頁面。
](/help/sites-deploying/backward-compatibility.md)[ ![opt_schient](assets/opt_cropped.png)](assets/upgrade-code-base-highlevel.png)

## 升級代碼庫{#upgrade-code-base}

### 在版本控制{#create-a-dedicated-branch-for-6.5-code-in-version-control}中為6.5代碼建立專用分支

您實作所需的所有程式碼AEM和組態都應使用某種版本控制來管理。 應建立版本控制中的專用分支，以管理目標版本中代碼庫所需的任何更改AEM。 此分支將管理針對目標版本及後續錯誤修AEM正的程式碼庫反覆測試。

### 更新AEMUber Jar版本{#update-the-aem-uber-jar-version}

Uber AEM jar將所有AEMAPI作為單一依賴項包含在Maven項目的`pom.xml`中。 將Uber Jar納入為單一相依性，而不是納入個別API相依性，永遠是最佳AEM做法。 升級代碼庫時，應將Uber Jar的版本更改為指向的目標版本AEM。 如果您的專案是在Uber Jar存在之AEM前開發的版本，則所有個AEM別API相依性都應移除，並由目標版本的Uber Jar中的單一包含項取代AEM。 然後，應根據新版Uber Jar重新編譯代碼庫。 任何已過時的API或方法都應更新為與的目標版本相AEM容。

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

### 淘汰管理資源解析器{#phase-out-use-of-administrative-resource-resolver}

通過`SlingRepository.loginAdministrative()`和`ResourceResolverFactory.getAdministrativeResourceResolver()`使用管理會話在6.0之前的代碼庫中非常普遍AEM。由於這些方法的存取範圍太廣，因此已因安全原因而遭到淘汰。 [在Sling的未來版本中，這些方法將會移除](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecation-of-administrative-authentication)。強烈建議您重新調整任何程式碼，以改用「服務使用者」。 有關服務用戶和[如何淘汰管理會話的詳細資訊，請參閱此處](/help/sites-administering/security-service-users.md#how-to-phase-out=admin-sessions)。

### 查詢和Oak索引{#queries-and-oak-indexes}

在升級程式碼庫時，任何對程式碼庫的查詢使用都需要經過徹底的測試。 對於從Jackrabbit 2(6.0以AEM上版本)升級的客戶而言，這一點尤其重要，因為Oak不會自動為內容建立索引，而且可能需要建立自訂索引。 如果從6.x版AEM本升級，Oak索引定義可能已變更，而且可能會影響現有查詢。

有幾種工具可用來分析和檢查查詢效能：

* [索AEM引工具](/help/sites-deploying/queries-and-indexing.md)

* [操作診斷工具——查詢效能](/help/sites-administering/operations-dashboard.md#diagnosis-tools)

* [奧克·尤蒂爾](https://oakutils.appspot.com/)。這是開放原始碼工具，不由Adobe維護。

### Classic UI編寫{#classic-ui-authoring}

傳統的UI編寫功能仍可在AEM6.5中使用，但已過時。 如需詳細資訊，請至[這裡](/help/release-notes/deprecated-removed-features.md#pre-announcement-for-next-release)。 如果您的應用程式目前在Classic UI作者環境上執行，建議升級至AEM6.5並繼續使用Classic UI。 然後可規劃為個別專案，以在數個開發週期中完成移轉至Touch UI。 為了在6.5版中使AEM用Classic UI，需要將數種OSGi配置提交到代碼庫。 有關如何配置此選項的詳細資訊，請參閱[此處](/help/sites-administering/enable-classic-ui.md)。

## 與6.5儲存庫結構{#align-repository-structure}對齊

為了使升級更輕鬆，並確保升級期間不會覆蓋配置，6.4版中的儲存庫將進行重組，以將內容與配置分開。

因此，必須移動一些設定，使之不再像過去那樣位於`/etc`下方。 要複查在更新到6.4時必須審查並滿足的全套資料庫重組問題，請參見6.4&lt;a1/AEM>中的AEM[資料庫重組。](/help/sites-deploying/repository-restructuring.md)

## AEM自定義{#aem-customizations}

需要確定源AEM版本中編寫環境的AEM所有自定義。 在識別後，建議您將每個自訂項目儲存在版本控制中，或至少儲存在內容套件的備份中。 所有自訂應在生產升級之前，在執行目標版本的QA或測試環境AEM中部署和驗證。

### 一般{#overlays-in-general}的覆蓋

通常的做法是在/libs下AEM將節點和／或檔案覆蓋在/apps下，並加上其他節點，以擴充現成可用的功能。 這些覆蓋應在版本控制中追蹤，並針對目標版本進行測試AEM。 如果檔案（不論是JS、JSP、HTL）已覆蓋，建議您留下註解已擴充的功能，以便更輕鬆地對目標版本的回歸測試AEM。 有關覆蓋的更多一般資訊，請參閱[這裡](/help/sites-developing/overlays.md)。 下方提供AEM特定覆蓋的指示。

### 升級自訂搜尋Forms{#upgrading-custom-search-forms}

自訂搜尋刻面需要在升級後進行一些手動調整，才能正常運作。 如需詳細資訊，請參閱[升級自訂搜尋Forms](/help/sites-deploying/upgrading-custom-search-forms.md)。

### 資產UI自訂{#assets-ui-customizations}

>[!NOTE]
>
>只有從6.2以前的版本升級時，才需AEM要此程式。

必須為具有自訂資產部署的例項準備升級。 這是為了確保所有自訂內容都與新的6.4節點結構相容所需。

您可以執行下列動作，準備資產UI的自訂設定：

1. 在需要升級的實例上，通過轉到&#x200B;*https://server:port/crx/de/index.jsp*&#x200B;開啟CRXDE Lite

1. 轉到以下節點：

   * `/apps/dam/content`

1. 將內容節點更名為&#x200B;**content_backup**。 要執行此操作，請按一下右鍵窗口左側的瀏覽器窗格，然後選擇&#x200B;**更名**。

1. 在重新命名節點後，在`/apps/dam`下建立名為content的新節點，名為&#x200B;**content**，並將其節點類型設為&#x200B;**sling:Folder**。

1. 將&#x200B;**content_backup**&#x200B;的所有子節點移動到新建的內容節點。 要執行此操作，請按一下右鍵瀏覽器窗格中的每個子節點，然後選擇&#x200B;**移動**。

1. 刪除&#x200B;**content_backup**&#x200B;節點。

1. `/apps/dam`下更新的節點類型為`sling:Folder`時，最好將其保存到版本控制中，並與代碼庫一起部署，或至少將其備份為內容包。

### 為現有資產產生資產ID {#generating-asset-ids-for-existing-assets}

若要為現有資產產生資產ID，請在您將例項升級至執行AEM6.AEM5時升級資產。這是啟用[資產前瞻分析功能](/help/assets/asset-insights.md)的必要條件。 如需詳細資訊，請參閱[新增內嵌代碼](/help/assets/use-page-tracker.md#add-embed-code)。

若要升級資產，請在JMX主控台中設定Associate Asset IDs套件。 根據儲存庫中的資產數量，`migrateAllAssets`可能需要很長的時間。 我們的內部測試估計，TarMK上的12.5萬個資產大約需要一小時。

![1487758945977](assets/1487758945977.png)

如果您需要資產ID做為整個資產的子集，請使用`migrateAssetsAtPath` API。

對於所有其他用途，請使用`migrateAllAssets()` API。

### InDesign指令碼自定義{#indesign-script-customizations}

Adobe建議將自訂指令碼放在`/apps/settings/dam/indesign/scripts`位置。 有關InDesign指令碼定製的詳細資訊，請參閱[此處](/help/assets/indesign.md#configuring-the-aem-assets-workflow)。

### 恢復ContextHub配置{#recovering-contexthub-configurations}

ContextHub組態受升級影響。 有關如何恢復現有ContextHub配置的說明，請參閱[此處](/help/sites-developing/ch-configuring.md#recovering-contexthub-configurations-after-upgrading)。

### 工作流定制{#workflow-customizations}

您通常會在開箱即用的工作流程中進行更新，以新增或移除不需要的功能。 自訂的常見工作流程是[!UICONTROL DAM更新資產]工作流程。 自訂實作所需的所有工作流程都應備份並儲存在版本控制中，因為升級期間可能會覆寫這些工作流程。

### 可編輯的範本 {#editable-templates}

>[!NOTE]
>
>只有使用6.2版可編輯範本的網站升級才需AEM要此程式

可編輯範本的結構在6.2AEM和6.3之間變更。如果您是從6.2或更舊版本升級，而且如果您的網站內容是使用可編輯的範本建立，則需要使用[回應式節點清理工具](https://github.com/Adobe-Marketing-Cloud/aem-sites-template-migration)。 此工具的用途是在&#x200B;**升級後執行**，以清除內容。 它必須同時在「作者」和「發佈」層上執行。

### CUG實施變更{#cug-implementation-changes}

封閉使用者群組的實施已大幅改變，以解決舊版的效能與延展性限AEM制。 舊版CUG已在6.3中停用，而新實作僅在Touch UI中受支援。 如果從6.2或更新版本升級，則可以在[此處](/help/sites-administering/closed-user-groups.md#upgradetoaem63)找到遷移到新CUG實施的說明。

## 測試過程{#testing-procedure}

應為測試升級準備完整的測試計畫。 測試升級後的程式碼庫和應用程式時，必須先在較低的環境中完成。 發現的任何錯誤都應以反覆方式加以修正，直到代碼庫穩定為止，只有當代碼庫穩定時，才應升級更高級別的環境。

### 測試升級過程{#testing-the-upgrade-procedure}

此處概述的升級程式應如您的自訂執行手冊中所述，在開發與QA環境上進行測試（請參閱[規劃您的升級](/help/sites-deploying/upgrade-planning.md)）。 應重複升級過程，直到升級運行手冊中記錄了所有步驟，並且升級過程很順暢。

### 實施測試區域{#implementation-test-areas-}

以下是在升級環AEM境並部署升級的代碼庫後，測試計畫應涵蓋的任何實施的關鍵部分。

<table>
 <tbody>
  <tr>
   <td><strong>功能測試區</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>發佈網站</td>
   <td>透過調AEM度器在發佈層<br />上測試實作和相關的程式碼。 應包含頁面更新和<br />快取失效的條件。</td>
  </tr>
  <tr>
   <td>製作</td>
   <td>在「作AEM者」層測試實作和相關的程式碼。 應包含頁面、元件編寫和對話方塊。</td>
  </tr>
  <tr>
   <td>與Marketing Cloud解決方案整合</td>
   <td>驗證與Analytics、DTM和Target等產品的整合。</td>
  </tr>
  <tr>
   <td>與第三方系統整合</td>
   <td>任何協力廠商整合都應在「作者」和「發佈」層上驗證。</td>
  </tr>
  <tr>
   <td>驗證、安全性和權限</td>
   <td>任何驗證機制（例如LDAP/SAML）都應經過驗證。<br /> 權限和群組應同時在作者和發佈者上<br /> 測試。</td>
  </tr>
  <tr>
   <td>查詢</td>
   <td>自訂索引和查詢應與查詢效能一起測試。</td>
  </tr>
  <tr>
   <td>UI自訂</td>
   <td>在作者環境中對UI的任AEM何擴充功能或自訂。</td>
  </tr>
  <tr>
   <td>工作流程</td>
   <td>自訂和／或現成可用的工作流程和功能。</td>
  </tr>
  <tr>
   <td>效能測試</td>
   <td>應同時在模擬真實場景的「作者」和「發佈」層執行負載測試。</td>
  </tr>
 </tbody>
</table>

### 文檔測試計畫和結果{#document-test-plan-and-results}

應建立涵蓋上述實作測試範圍的測試計畫。 在許多情況下，依「作者」和「發佈」工作清單來區隔測試計畫是合理的。 在升級生產環境之前，此測試計畫應在開發、QA和階段環境上執行。 在較低的環境中，應擷取測試結果和效能度量，以便在升級「階段」和「生產」環境時提供比較。
