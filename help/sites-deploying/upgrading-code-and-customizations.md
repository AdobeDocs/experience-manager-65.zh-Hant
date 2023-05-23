---
title: 升級代碼和自定義
seo-title: Upgrading Code and Customizations
description: 瞭解有關升級中的自定義代碼的詳細信AEM息。
seo-description: Learn more about upgrading custom code in AEM.
uuid: dec11ef0-bf85-4e4e-80ac-dcb94cc3c256
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 59780112-6a9b-4de2-bf65-f026c8c74a31
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: a36a310d-5943-4ff5-8ba9-50eaedda98c5
source-git-commit: a296e459461973fc2dbd0641c6fdda1d89d8d524
workflow-type: tm+mt
source-wordcount: '2115'
ht-degree: 0%

---

# 升級代碼和自定義{#upgrading-code-and-customizations}

在規劃升級時，必須調查並處理以下實施領域。

* [升級代碼庫](#upgrade-code-base)
* [與6.5儲存庫結構對齊](#align-repository-structure)
* [自定AEM義](#aem-customizations)
* [測試過程](#testing-procedure)

## 概觀 {#overview}

1. **圖案檢測器**  — 運行模式檢測器，如升級計畫中所述，並在 [此頁](/help/sites-deploying/pattern-detector.md)。 除目標版本中不可用的API/捆綁包外，您還會得到一個模式檢測器報告，其中包含必須解決的區域的詳細資訊AEM。 「Pattern Detection」（模式檢測）報告會指示代碼中的任何不相容之處。 如果不存在，則您的部署已相容6.5。 您仍然可以選擇使用6.5功能進行新開發，但您不僅需要它來維護相容性。 如果報告了不相容問題，則可以選擇在相容模式下運行，並推遲開發，以獲得新的6.5功能或相容性。 或者，您可以決定在升級後進行開發，然後轉到步驟2。 請參閱 [6.5中的AEM向後相容性](/help/sites-deploying/backward-compatibility.md) 的子菜單。

1. **為6.5開發代碼庫** — 為目標版本的代碼庫建立專用分支或儲存庫。 使用升級前相容性中的資訊來規劃要更新的代碼區域。
1. **使用6.5 Uber jar編譯** — 更新代碼庫POM以指向6.5 Uber jar並編譯針對它的代碼。
1. **更新自AEM定義*** - *任何自定義或擴展AEM都應更新/驗證，以在6.5中運行，並添加到6.5代碼庫。 包括UI搜索Forms、資產自定義、使用/mnt/overlay的任何內容

1. **部署到6.5環境**  — 應在開發/QAAEM環境中啟用一個乾淨的6.5實例（作者+發佈）。 應部署更新的代碼庫和具有代表性的內容示例（來自當前生產）。
1. **QA驗證和錯誤修復** - QA應在6.5的「作者」和「發佈」實例上驗證應用程式。發現的任何錯誤都應被修復並提交到6.5代碼庫。 根據需要重複Dev-Cycle，直到修復所有錯誤。

在繼續升級之前，您應該有一個穩定的應用程式碼庫，該庫已針對的目標版本進行了徹底測AEM試。 根據測試中的觀察，可以對自定義代碼進行優化。 例如，它可能包括重構代碼以避免遍歷儲存庫、自定義索引以優化搜索，或使用JCR中的未排序節點等。

除了可選地升級代碼庫和自定義以與新版AEM本配合使用外， 6.5還幫助使用向後相容性功能更高效地管理自定義 [此頁](/help/sites-deploying/backward-compatibility.md)。

如上所述，如下圖所示，運行 [圖案檢測器](/help/sites-deploying/pattern-detector.md) 第一步可幫助您評估升級的整體複雜性。 它還可以幫助您確定是要在相容模式下運行，還是更新自定義以使用所有AEM新的6.5功能。 查看 [6.5中的AEM向後相容性](/help/sites-deploying/backward-compatibility.md) 的子菜單。
[ ![opt_screftd](assets/opt_cropped.png)](assets/upgrade-code-base-highlevel.png)

## 升級代碼庫 {#upgrade-code-base}

### 在版本控制中為6.5代碼建立專用分支 {#create-a-dedicated-branch-for-6.5-code-in-version-control}

實施所需的所有代碼和AEM配置都應使用某種形式的版本控制進行管理。 應建立版本控制中的專用分支，以管理目標版本中的代碼庫所需的任何更AEM改。 在此分支中管理針對目標版本和後續錯誤修AEM復的代碼庫的迭代測試。

### 更新AEMUber Jar版本 {#update-the-aem-uber-jar-version}

Uber AEMjar將所AEM有API作為Maven項目的單個依賴項 `pom.xml`。 將Uber Jar作為單個依賴項而不是包括單個API依賴項始終是最佳AEM做法。 升級代碼庫時，請更改Uber Jar的版本以指向的目標版本AEM。 如果項目是在存在Uber Jar之AEM前基於的版本開發的，請刪除所有單獨AEM的API依賴項。 替換為將Uber Jar作為目標版本AEM。 根據新版本的Uber Jar重新編譯代碼庫。 更新任何已棄用的API或方法，使其與的目標版本兼AEM容。

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

### 逐步停用管理資源解析器 {#phase-out-use-of-administrative-resource-resolver}

通過 `SlingRepository.loginAdministrative()` 和 `ResourceResolverFactory.getAdministrativeResourceResolver()` 6.0之前在代碼AEM庫中很普遍。由於安全原因，這些方法的訪問範圍太廣，因此已被棄用。 [在Sling的未來版本中，這些方法將被刪除](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecation-of-administrative-authentication)。 強烈建議重新構造任何代碼以改用「服務用戶」。 有關服務用戶和 [如何逐步取消管理會話，可在此處找到](/help/sites-administering/security-service-users.md#how-to-phase-out=admin-sessions)。

### 查詢和Oak索引 {#queries-and-oak-indexes}

在升級代碼庫時，必須徹底測試代碼庫中任何查詢的使用。 對於從Jackrabbit 2(6.0版以AEM上版本)升級的客戶，此測試尤其重要，因為Oak不會自動為內容編製索引，應建立自定義索引。 如果從6.x版AEM本升級，Oak索引定義的現成版本可能已更改，並可能影響現有查詢。

以下工具可用於分析和檢查查詢效能：

* [索AEM引工具](/help/sites-deploying/queries-and-indexing.md)

* [操作診斷工具 — 查詢效能](/help/sites-administering/operations-dashboard.md#diagnosis-tools)

<!-- URL is 404 as of 04/24/23; commenting out * [Oak Utils](https://oakutils.appspot.com/). This is an open source tool that is not maintained by Adobe. -->

### 經典UI創作 {#classic-ui-authoring}

經典UI創作在6.5中AEM仍可用，但已棄用。 可以找到更多資訊 [這裡](/help/release-notes/deprecated-removed-features.md#pre-announcement-for-next-release)。 如果應用程式在Classic UI作者環境上運行，建議升級到AEM6.5並繼續使用Classic UI。 然後，可以將遷移到Touch UI作為單獨的項目進行規劃，以在多個開發週期中完成。 要在6.5中使用AEMClassic UI，必須將幾個OSGi配置提交到代碼庫。 有關如何配置的詳細資訊，請參閱 [這裡](/help/sites-administering/enable-classic-ui.md)。

## 與6.5儲存庫結構對齊 {#align-repository-structure}

為了使升級更輕鬆，並確保在升級期間不會覆蓋配置，系統將以6.4的格式重構儲存庫，將內容與配置分開。

因此，必須將若干設定移動到不再位於 `/etc` 和過去一樣。 要審查必須在更新至6.4時加以審查和解決的整套資料庫重AEM組問題，請參見 [6.AEM4中的儲存庫重組](/help/sites-deploying/repository-restructuring.md)。

## 自定AEM義  {#aem-customizations}

必須標識源AEM版本中對創作環境的AEM所有自定義。 一旦確定，建議將每個自定義內容儲存在版本控制中或作為內容包的一部分至少備份一次。 所有定制都應在生產升級之前在運行目標版本的QA或臨時環境AEM中部署和驗證。

### 總體覆蓋 {#overlays-in-general}

通常的做法是，在/libAEM下將節點和/或檔案與/apps下的其他節點重疊，從而擴展開箱功能。 應在版本控制中跟蹤這些覆蓋，並針對的目標版本進行測試AEM。 如果檔案（如JS、JSP、HTL）被重疊，Adobe建議您對所增強的功能留下注釋，以便更輕鬆地對的目標版本進行回歸測AEM試。 有關一般覆蓋的詳細資訊 [這裡](/help/sites-developing/overlays.md)。 下面可找AEM到有關特定疊加的說明。

### 升級自定義搜索Forms {#upgrading-custom-search-forms}

自定義搜索小平面需要在升級後進行一些手動調整才能正常工作。 有關詳細資訊，請參閱 [升級自定義搜索Forms](/help/sites-deploying/upgrading-custom-search-forms.md)。

### 資產UI自定義 {#assets-ui-customizations}

>[!NOTE]
>
>僅從6.2版以前的版本升級AEM時，才需要此過程。

必須為升級準備具有自定義資產部署的實例。 此操作是確保所有自定義內容都與新的6.4節點結構相容所必需的。

通過執行以下操作，可以準備對資產UI的自定義：

1. 在正在升級的實例上，通過轉到 *https://server:port/crx/de/index.jsp*

1. 轉到以下節點：

   * `/apps/dam/content`

1. 將內容節點更名為 **內容備份** 按一下右鍵窗口左側的瀏覽器窗格，然後選擇 **更名**。

1. 更名節點後，在下面建立一個名為content的節點 `/apps/dam` 命名 **內容** 將其節點類型設定為 **sling：資料夾**。

1. 移動的所有子節點 **內容備份** 通過按一下右鍵瀏覽器窗格中的每個子節點並選擇 **移動**。

1. 刪除 **內容備份** 的下界。

1. 下面的更新節點 `/apps/dam` 節點類型正確 `sling:Folder` 最好將其保存到版本控制中，並與代碼庫一起部署，或至少將其備份為內容包。

### 為現有資產生成資產ID {#generating-asset-ids-for-existing-assets}

要為現有資產生成資產ID，請在將實例升級為運行6.5AEM時升AEM級資產。此步驟是啟用 [資產透視功能](/help/assets/asset-insights.md)。 有關詳細資訊，請參閱 [添加嵌入代碼](/help/assets/use-page-tracker.md#add-embed-code)。

要升級資產，請在JMX控制台中配置關聯資產ID包。 根據儲存庫中的資產數量， `migrateAllAssets` 可能需要很長時間。 Adobe的內部test估計，TarMK上125000項資產大約需要1小時。

![1487758945977](assets/1487758945977.png)

如果您需要整個資產子集的資產ID，請使用 `migrateAssetsAtPath` API。

對於所有其他目的，請使用 `migrateAllAssets()` API。

### InDesign指令碼自定義 {#indesign-script-customizations}

Adobe建議在 `/apps/settings/dam/indesign/scripts` 位置。 有關InDesign指令碼自定義項的詳細資訊 [這裡](/help/assets/indesign.md#configuring-the-aem-assets-workflow)。

### 恢復ContextHub配置 {#recovering-contexthub-configurations}

ContextHub配置受升級的影響。 有關如何恢復現有ContextHub配置的說明 [這裡](/help/sites-developing/ch-configuring.md#recovering-contexthub-configurations-after-upgrading)。

### 工作流自定義 {#workflow-customizations}

在現成工作流中編輯以添加或刪除不需要的功能是一種常見做法。 自定義的通用工作流 [!UICONTROL DAM更新資產] 工作流。 應備份自定義實施所需的所有工作流並將其儲存在版本控制中，因為在升級過程中可能會覆蓋這些工作流。

### 可編輯的範本 {#editable-templates}

>[!NOTE]
>
>此過程僅對使用6.2版可編輯模板進行站點升級AEM時是必需的

「可編輯」模板的結構在AEM6.2和6.3之間更改。如果從6.2或更低版本升級，並且您的站點內容是使用可編輯模板建立的，則必須使用 [響應節點清理工具](https://github.com/Adobe-Marketing-Cloud/aem-sites-template-migration)。 該工具旨在運行 **後** 升級以清除內容。 在「作者」和「發佈」層上運行它。

### CUG實施更改 {#cug-implementation-changes}

關閉用戶組的實施已發生重大變化，以解決以前版本的效能和可擴充性限AEM制。 6.3中不建議使用以前版本的CUG，並且只有Touch UI支援新的實現。 如果從6.2或更低版本升級，則可以找到遷移到新CUG實施的說明 [這裡](/help/sites-administering/closed-user-groups.md#upgradetoaem63)。

## 測試過程 {#testing-procedure}

應為測試升級準備全面的test計畫。 測試升級後的代碼庫和應用程式必須首先在較低環境中完成。 發現的任何錯誤都應以迭代方式加以修復，直到代碼庫穩定為止，只有這樣才應升級更高級別的環境。

### 測試升級過程 {#testing-the-upgrade-procedure}

應在開發和QA環境上測試此處概述的升級過程，如您的自定義運行手冊中所述(請參見 [計畫升級](/help/sites-deploying/upgrade-planning.md))。 應重複升級過程，直到升級運行手冊中記錄了所有步驟，並且升級過程順利。

### 實施Test領域  {#implementation-test-areas-}

以下是在升級環境AEM並部署升級的代碼庫後，test計畫應涵蓋的任何實施的關鍵領域。

<table>
 <tbody>
  <tr>
   <td><strong>功能Test區</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>已發佈站點</td>
   <td>測試發AEM布層上的實現和關聯代碼<br /> 通過調度員。 應包括頁面更新和<br /> 快取無效。</td>
  </tr>
  <tr>
   <td>編寫</td>
   <td>在作AEM者層測試實現和關聯代碼。 應包括頁面、元件創作和對話框。</td>
  </tr>
  <tr>
   <td>與Experience Cloud解決方案的整合</td>
   <td>驗證與Analytics、DTM和Target等產品的整合。</td>
  </tr>
  <tr>
   <td>與第三方系統的整合</td>
   <td>驗證作者和發佈層上的任何第三方整合。</td>
  </tr>
  <tr>
   <td>身份驗證、安全性和權限</td>
   <td>應驗證任何身份驗證機制，如LDAP/SAML。<br /> 權限和組應同時在「作者」和「發佈」上測試<br /> 層。</td>
  </tr>
  <tr>
   <td>查詢</td>
   <td>自定義索引和查詢應與查詢效能一起進行測試。</td>
  </tr>
  <tr>
   <td>UI自定義</td>
   <td>作者環境中對UIAEM的任何擴展或自定義。</td>
  </tr>
  <tr>
   <td>工作流程</td>
   <td>定制和/或開箱即用的工作流和功能。</td>
  </tr>
  <tr>
   <td>效能測試</td>
   <td>應對模擬真實場景的作者層和發佈層執行負載測試。</td>
  </tr>
 </tbody>
</table>

### 文檔Test計畫和結果 {#document-test-plan-and-results}

應制定涵蓋上述執行test領域的test計畫。 通常，將test計畫按作者和發佈任務清單分開是合理的。 升級生產環境之前，應在開發環境、QA環境和階段環境上執行此test計畫。 Test結果和效能指標應在較低的環境中捕獲，以便在升級階段和生產環境時提供比較。
