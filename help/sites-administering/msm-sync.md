---
title: 配置即時拷貝同步
seo-title: 配置即時拷貝同步
description: 瞭解如何設定即時副本同步。
seo-description: 瞭解如何設定即時副本同步。
uuid: a5db0bee-a761-4cff-81dc-31b374525f47
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 6bcf0fcc-481a-4283-b30d-80b517701280
docset: aem65
translation-type: tm+mt
source-git-commit: 4e5e6ef022dc9f083859e13ab9c86b622fc3d46e

---


# 配置即時拷貝同步{#configuring-live-copy-synchronization}

執行下列工作，以控制即時副本與其來源內容同步的方式和時間。

* 決定現有的轉出設定是否符合您的需求，或您是否需要建立一或多個。
* 指定要用於即時副本的轉出設定。

## 安裝和自訂轉出設定 {#installed-and-custom-rollout-configurations}

本節提供有關已安裝的轉出配置及其使用的同步操作的資訊，以及如何根據需要建立自定義配置。

### 轉出觸發器 {#rollout-triggers}

每個轉出設定都使用轉出觸發器，導致轉出發生。 轉出設定可使用下列其中一個觸發器：

* **推出時**:Rovolt **** (轉出 **)命令用於藍色打印頁，或** Synchronize（同步）命令用於即時複製頁。

* **修改時**:源頁面已修改。

* **啟動時**:源頁面被激活。

* **停用時**:來源頁面已停用。

>[!NOTE]
>
>使用「修改時」觸發器會影響效能。 如需詳 [細資訊，請參閱](/help/sites-administering/msm-best-practices.md#onmodify) MSM最佳實務。

### 已安裝的轉出配置 {#installed-rollout-configurations}

下表列出隨AEM安裝的轉出設定。 該表包括每個轉出配置的觸發器和同步操作。 如果安裝的轉出配置操作不符合您的要求，則可以 [建立新的轉出配置](#creating-a-rollout-configuration)。

<table>
 <tbody>
  <tr>
   <th>名稱</th>
   <th>說明</th>
   <th>觸發器</th>
   <th>同步操作<br /> ，另請參 <br /> 閱 <a href="#installed-synchronization-actions">安裝的同步操作</a></th>
  </tr>
  <tr>
   <td>標準轉出設定</td>
   <td>標準轉出設定，允許於轉出觸發時開始轉出程序，並執行下列動作: 建立、更新、刪除內容以及排序子節點。</td>
   <td>於轉出</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> references更新產品<br /> Update order<br /> Children</td>
  </tr>
  <tr>
   <td>在 Blueprint 啟動時啟動</td>
   <td>發佈來源時發佈即時副本。</td>
   <td>啟動時</td>
   <td>targetActivate</td>
  </tr>
  <tr>
   <td>在 Blueprint 停用時停用</td>
   <td>停用來源時停用即時副本。</td>
   <td>停用</td>
   <td>targetDeactivate<br /> </td>
  </tr>
  <tr>
   <td>在發生修改時推送</td>
   <td><p>修改來源時，將內容推送至即時副本。</p> <p>使用On Modification觸發器時，請謹慎使用此轉出設定。</p> </td>
   <td>於修改</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> references更新<br /> orderChildren<br /> </td>
  </tr>
  <tr>
   <td>在發生修改時推送 (淺層)</td>
   <td><p>在修改藍圖頁面時將內容推送至即時副本，而不更新參照（例如淺層副本）。</p> <p>使用On Modification觸發器時，請謹慎使用此轉出設定。</p> </td>
   <td>於修改</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> orderChildren</td>
  </tr>
  <tr>
   <td>提升啟動</td>
   <td>提升啟動頁面的標準轉出設定。</td>
   <td>於轉出</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> references更新順序<br /> Children<br /> markLiveRelationship</td>
  </tr>
  <tr>
   <td>目錄頁面內容轉出設定</td>
   <td>從目錄 Blueprint 套用頁面範本。</td>
   <td>於轉出</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> references更新產品<br /> CreateUpdate<br /> orderChildren</td>
  </tr>
  <tr>
   <td>目錄頁面更新轉出設定</td>
   <td>從目錄藍圖套用目標屬性。 必須在目錄頁面內容轉出設定後執行。</td>
   <td>於轉出</td>
   <td>catalogRovoltHooks</td>
  </tr>
  <tr>
   <td>DPS 發佈轉出設定</td>
   <td>DPS Publication轉出設定，允許在首次轉出時排除FolioProducer系結屬性，同時在轉出觸發時開始轉出程式</td>
   <td>於轉出</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> references更新順序<br /> Children<br /> dpsMetadataFilter</td>
  </tr>
  <tr>
   <td>舊版(5.6.0)目錄轉出設定</td>
   <td>已棄用。轉出目錄時不使用 MSM，並改用 Catalog Generator。</td>
   <td>於轉出</td>
   <td>editProperties</td>
  </tr>
 </tbody>
</table>

### 已安裝的同步操作 {#installed-synchronization-actions}

下表列出與AEM一起安裝的同步動作。 如果安裝的操作不符合您的要求，則可以 [建立新同步操作](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action)。

<table>
 <tbody>
  <tr>
   <th>動作名稱</th>
   <th>說明</th>
   <th>屬性<br /> </th>
  </tr>
  <tr>
   <td>contentCopy</td>
   <td>當源節點在即時拷貝上不存在時，將節點複製到即時拷貝。 <a href="#excluding-properties-and-node-types-from-synchronization">設定「CQ MSM內容複製動作」服務</a> ，以指定要排除的節點類型、段落項目和頁面屬性。 <br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>contentDelete</td>
   <td><p>刪除源上不存在的即時副本的節點。 <a href="#excluding-properties-and-node-types-from-synchronization">設定CQ MSM內容刪除動作服務</a> ，以指定要排除的節點類型、段落項目和頁面屬性。 </p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>contentUpdate</td>
   <td>使用來源的變更來更新即時副本內容。 <a href="#excluding-properties-and-node-types-from-synchronization">設定CQ MSM內容更新動作服務</a> ，以指定要排除的節點類型、段落項目和頁面屬性。 <br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>editProperties</td>
   <td><p>編輯即時副本的屬性。 editMap屬性可決定要編輯的屬性及其值。 editMap屬性的值必須使用下列格式：</p> <p><code>[property_name_1]#[current_value]#</code>[new_value],<br /> <code>[property_name_2]#[current_value]#</code>[new_value],<br /> ...,<br /> [ <code>[property_name_n]#[current_value]#</code>new_value]</p> <p>和 <code>current_value</code> 項 <code>new_value</code> 目是規則運算式。 <br /> </p> <p>例如，請考慮以下editMap值：</p> <p><code>sling:resourceType#/</code>(contentpage|homepage)#/<br /> mobilecontentpage,<br /> cq:template#/contentpage#/mobilecontentpage</p> <p>此值編輯即時副本節點的屬性，如下所示：</p>
    <ul>
     <li>設 <code>sling:resourceType</code> 置為或設定為 <code>contentpage</code> 的 <code>homepage</code> 屬性 <code>mobilecontentpage.</code></li>
     <li>設 <code>cq:template</code> 置為的屬 <code>contentpage</code> 性設定為 <code>mobilecontentpage.</code></li>
    </ul> </td>
   <td><p> </p> <p>editMap:（字串）識別屬性、目前值和新值。 如需詳細資訊，請參閱說明。<br /> </p> </td>
  </tr>
  <tr>
   <td>通知</td>
   <td>傳送已轉出頁面的頁面事件。 為了獲得通知，您必須先訂閱以推出事件。</td>
   <td> </td>
  </tr>
  <tr>
   <td>orderChildren</td>
   <td>在即時副本上，它會根據藍圖上的順序來排序子系（節點）<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>referencesUpdate</td>
   <td><p>在即時副本上，此同步動作會更新參照，例如類似連結。<br /> 它會在即時副本頁面中搜尋指向藍圖中資源的路徑。 找到時，會更新路徑以指向即時副本中的相關資源（而非藍圖）。 在藍圖以外具有目標的參照不會變更。</p> <p><a href="#excluding-properties-and-node-types-from-synchronization">設定「CQ MSM參考更新動作」服務</a> ，以指定要排除的節點類型、段落項目和頁面屬性。 </p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetVersion</td>
   <td><p>建立即時副本的版本。</p> <p>此動作必須是轉出設定中包含的唯一同步動作。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetActivate</td>
   <td><p>啟動即時副本。</p> <p>此動作必須是轉出設定中包含的唯一同步動作。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetDeactivate</td>
   <td><p>停用即時副本。</p> <p>此動作必須是轉出設定中包含的唯一同步動作。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>工作流程</td>
   <td><p>啟動由target屬性定義的工作流程（僅適用於頁面），並將即時副本視為裝載。</p> <p>目標路徑是模型節點的路徑，例如/etc/workflow/models/request_for_activation/jcr:content/model</p> </td>
   <td>目標：（字串）工作流程模型的路徑。<br /> </td>
  </tr>
  <tr>
   <td>強制</td>
   <td><p>將即時副本頁面上多個ACL的權限設定為特定用戶組的只讀權限。 配置了以下ACL:</p>
    <ul>
     <li>ActionSet.ACTION_NAME_REMOVE</li>
     <li>ActionSet.ACTION_NAME_SET_PROPERTY</li>
     <li>ActionSet.ACTION_NAME_ACL_MODIFY</li>
    </ul> <p>此動作僅適用於頁面。</p> </td>
   <td>目標：（字串）您要設定權限之群組的ID。 <br /> </td>
  </tr>
  <tr>
   <td>mandatoryContent</td>
   <td><p>將即時副本頁面上多個ACL的權限設定為特定用戶組的只讀權限。 配置了以下ACL:</p>
    <ul>
     <li>ActionSet.ACTION_NAME_SET_PROPERTY</li>
     <li>ActionSet.ACTION_NAME_ACL_MODIFY</li>
    </ul> <p>此動作僅適用於頁面。</p> </td>
   <td>目標：（字串）您要設定權限之群組的ID。 </td>
  </tr>
  <tr>
   <td>mandatoryStructure</td>
   <td>將ActionSet.ACTION_NAME_REMOVE ACL在即時副本頁上的權限設定為特定用戶組的只讀權限。 此動作僅適用於頁面。</td>
   <td>目標：（字串）您要設定權限之群組的ID。 </td>
  </tr>
  <tr>
   <td>VersionCopyAction</td>
   <td>如果藍圖／來源頁面至少已發佈一次，請使用已發佈的版本建立即時副本頁面。 注意：此動作僅適用於根據已發佈的來源頁面建立即時副本頁面，不適用於更新現有的即時副本頁面。 </td>
   <td> </td>
  </tr>
  <tr>
   <td>PageMoveAction</td>
   <td><p>PageMoveAction會在Blueprint中移動頁面時套用。</p> <p>動作會複製（相關）LiveCopy頁面，而非將頁面從移動前的位置移至之後的位置。</p> <p>PageMoveAction不會變更移動前所在位置的LiveCopy頁面。 因此，對於連續的RovoltConfigurations，它的狀態為「即時關係」而無「藍圖」。</p> <p><a href="#excluding-properties-and-node-types-from-synchronization">設定CQ MSM頁面移動動作服務</a> ，以指定要排除的節點類型、段落項目和頁面屬性。 </p> <p>此動作必須是轉出設定中包含的唯一同步動作。</p> </td>
   <td><p>prop_reference更新：（布爾值）設為true可更新參考。 預設為true。</p> <p> </p> </td>
  </tr>
  <tr>
   <td>productCreateUpdate</td>
   <td>在目錄中建立或更新產品資源。 此動作應用於下列其中一種情況：
    <ul>
     <li>產生或推出目錄（或目錄區段）</li>
     <li>用戶恢復產品元件的同步繼承。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>markLiveRelationship</td>
   <td>表示啟動建立的內容存在即時關係。</td>
   <td> </td>
  </tr>
  <tr>
   <td>catalogRovoltHooks</td>
   <td>執行特定目錄產生轉出勾點。 呼叫CatalogGenerator的executePageRovoltHooks和executeProductRovoltHooks方法。<br /> 請參閱AEM Javadocs中的com.adobe.cq.commerce.pim.api.CatalogGenerator。</td>
   <td> </td>
  </tr>
  <tr>
   <td>productUpdate</td>
   <td>更新產品目錄即時副本中的產品頁面</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 建立轉出設定 {#creating-a-rollout-configuration}

當安裝 [的轉出設定不符合您的應用程式需求時](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration) ，您可以建立轉出設定：

* [建立轉出設定](/help/sites-developing/extending-msm.md#create-the-rollout-configuration)。
* [將同步動作新增至轉出設定](/help/sites-developing/extending-msm.md#add-synchronization-actions-to-the-rollout-configuration)。

然後，當在藍圖或即時副本頁面上設定轉出設定時，您便可使用新的轉出設定。

### 從同步中排除屬性和節點類型 {#excluding-properties-and-node-types-from-synchronization}

您可以配置支援相應同步操作的多個OSGi服務，以便它們不影響特定節點類型和屬性。 例如，許多與AEM內部功能相關的屬性和子節點不應包含在即時副本中。 僅複製與頁面使用者相關的內容。

使用AEM時，有幾種方法可管理此類服務的組態設定；如需詳 [細資訊](/help/sites-deploying/configuring-osgi.md) ，請參閱設定OSGi。

下表列出了可以指定要排除的節點的同步操作。 該表提供了使用Web控制台配置的服務名和使用儲存庫節點配置的PID。

| 同步操作 | Web控制台中的服務名 | 服務PID |
|---|---|---|
| contentCopy | CQ MSM內容複製動作 | com.day.cq.wcm.msm.impl.actions.ContentCopyActionFactory |
| contentDelete | CQ MSM內容刪除動作 | com.day.cq.wcm.msm.impl.actions.ContentDeleteActionFactory |
| contentUpdate | CQ MSM內容更新動作 | com.day.cq.wcm.msm.impl.actions.ContentUpdateActionFactory |
| PageMoveAction | CQ MSM Page Move Action | com.day.cq.wcm.msm.impl.actions.PageMoveActionFactory |
| referencesUpdate | CQ MSM參考更新動作 | com.day.cq.wcm.msm.impl.actions.ReferencesUpdateActionFactory |

下表說明了您可以配置的屬性：

<table>
 <tbody>
  <tr>
   <th>Web控制台屬性/ OSGi屬性</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><p>排除的節點類型</p> <p>cq.wcm.msm.action.excludednodetypes</p> </td>
   <td>與要從同步操作中排除的節點類型相匹配的規則運算式。</td>
  </tr>
  <tr>
   <td><p>排除的段落項目</p> <p>cq.wcm.msm.action.excludedparagraphitems</p> </td>
   <td>與要從同步操作中排除的段落項匹配的規則運算式。</td>
  </tr>
  <tr>
   <td><p>排除的頁面屬性</p> <p>cq.wcm.msm.action.excludedprops</p> </td>
   <td>與要從同步操作中排除的頁面屬性相匹配的規則運算式。</td>
  </tr>
  <tr>
   <td><p>忽略Mixin nodeTypes</p> <p>cq.wcm.msm.action.ignoredMixin</p> </td>
   <td>僅適用於CQ MSM內容更新動作。 與要從同步操作中排除的mixin節點類型名稱匹配的規則運算式。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>在Classic UI中，LiveCopy頁面的「頁面屬性」對話方塊中顯示的鎖定圖示不會反映「排除的頁面屬性」屬性的設定。 即使對於從同步操作中排除的屬性，也會顯示鎖定表徵圖。

>[!NOTE]
>
>在觸控最佳化的UI中，另請參 [閱在頁面屬性上設定MSM鎖定（觸控最佳化的UI）](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-pagep-roperties-touch-optimized-ui)。

#### CQ MSM內容更新動作——排除 {#cq-msm-content-update-action-exclusions}

預設情況下，會排除一些屬性和節點類型，這些屬性和節點類型在 **CQ MSM Content Update Action的OSGi配置中定義**，在 **Excluded Page Properties（排除的頁面屬性）下**。

依預設，在轉出時會排除與下列規則運算式相符的屬性（亦即未更新）:

![chlimage_1](assets/chlimage_1.png)

您可以視需要變更定義排除清單的運算式。

例如，如果您想將頁面標 **題納入考慮轉出的變更** ，請從排 `jcr:title` 除項中移除。 例如，使用regex:

`jcr:(?!(title)$).*`

>[!CAUTION]
>
>在5.5 SP2之前，排除的頁面屬性是在系統主控台的 **Day CQ WCM Rovolt Manager下設定**。 在5.5 SP2及更新版本中，會忽略該面板中排除的頁面屬性設定。 轉出時的屬性排除設定如上所述，在 **CQ MSM內容更新動作中**。
>
>因此，如果您在5.5版以前的SP2安裝中手動調整了此設定，並且要升級到5.5版SP2或更高版本，則 *必須將這些設定從舊配置面板手動傳輸到新配置面板*。

### 配置同步以更新引用 {#configuring-synchronization-for-updating-references}

您可以配置幾個支援與更新引用相關的相應同步操作的OSGi服務。

使用AEM時，有幾種方法可管理此類服務的組態設定；如需詳 [細資訊](/help/sites-deploying/configuring-osgi.md) ，請參閱設定OSGi。

下表列出了可以為其指定引用更新的同步操作。 該表提供了使用Web控制台配置的服務名和使用儲存庫節點配置的PID。

<table>
 <tbody>
  <tr>
   <th>Web控制台屬性/ OSGi屬性</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><p>跨巢狀LiveCopys更新參考</p> <p>cq.wcm.msm.impl.action.referencesupdate.prop_updateNested</p> </td>
   <td>僅適用於CQ MSM參考更新動作。 選擇此選項（Web控制台）或將此布爾屬性設定為true（儲存庫配置），以替換指向位於最頂層LiveCopy分支中的任何資源的引用。</td>
  </tr>
  <tr>
   <td><p>更新參考頁面</p> <p>cq.wcm.msm.impl.actions.pagemove.prop_referenceUpdate</p> </td>
   <td>僅適用於CQ MSM Page Move Action。 選擇此選項（Web控制台）或將此布爾屬性設定為 <code>true</code> （儲存庫配置），以更新任何引用，以使用原始頁來改為引用LiveCopy頁。</td>
  </tr>
 </tbody>
</table>

## 指定要使用的轉出配置 {#specifying-the-rollout-configurations-to-use}

MSM可讓您指定一般使用的轉出組態集，並在需要時，您可以覆寫特定即時副本的組態集。 MSM提供了幾個位置，用於指定要使用的轉出配置。 位置會決定設定是否套用至特定的即時副本。

以下位置清單可指定使用的轉出組態，說明MSM如何決定要用於即時副本的轉出組態：

* **[](/help/sites-administering/msm-sync.md#setting-the-rollout-configurations-for-a-live-copy-page)即時副本頁面屬性&#x200B;**:當即時副本頁面設定為使用一或多個轉出設定時，MSM會使用這些轉出設定。
* **[](/help/sites-administering/msm-sync.md#setting-the-rollout-configuration-for-a-blueprint-page)Blueprint頁面屬性&#x200B;**:當即時副本以藍圖為基礎，且即時副本頁面未設定轉出設定時，會使用與藍圖來源頁面相關聯的轉出設定。
* **** 即時副本父頁面屬性：當即時副本頁面和Blueprint來源頁面都未設定轉出設定時，會使用套用至即時副本頁面父頁面的轉出設定。
* **[](/help/sites-administering/msm-sync.md#setting-the-system-default-rollout-configuration)系統預設&#x200B;**:當無法確定即時副本父頁面的轉出設定時，會使用系統預設的轉出設定。

例如，Blueprint使用We.Retail參考網站做為來源內容。 從Blueprint建立網站。 下列清單中的每個項目說明使用轉出組態的不同情形：

* 未將任何藍圖頁面或即時副本頁面設定為使用轉出設定。 MSM對所有即時副本頁面使用系統預設轉出設定。
* We.Retail參考網站的根頁面已設定數個轉出設定。 MSM會針對所有即時副本頁面使用這些轉出設定。
* We.Retail參考網站的根頁面已設定數個轉出設定，而即時副本網站的根頁面則設定了不同的轉出設定集。 MSM使用在即時副本網站的根頁面上設定的轉出設定。

### 設定即時副本頁面的轉出設定 {#setting-the-rollout-configurations-for-a-live-copy-page}

使用轉出設定來設定即時副本頁面，以便在轉出來源頁面時使用。 預設情況下，子頁繼承配置。 當您設定轉出設定使用時，您會覆寫即時副本頁面繼承自其父項的設定。

您也可以在建立即時副本時，為即時副本頁面設 [定轉出設定](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)。

1. 使用 **Sites** Console來選取即時復本頁面。
1. 從工 **具欄中** ，選擇「屬性」。
1. 開啟「即 **時副本** 」標籤。

   「配 **置** 」部分顯示頁面繼承的轉出配置。

   ![chlimage_1-1](assets/chlimage_1-1.png)

1. 如有需要，請調整「即 **時副本繼承** 」標幟。 如果選中此選項，即時副本配置對所有子項都有效。

1. 清除「從 **父代繼承轉出配置** 」屬性，然後從清單中選擇一個或多個轉出配置。

   選取的轉出設定會顯示在下拉式清單下方。

   ![chlimage_1-2](assets/chlimage_1-2.png)

1. 按一下或點選「 **儲存**」。

### 設定Blueprint頁面的轉出設定 {#setting-the-rollout-configuration-for-a-blueprint-page}

使用轉出設定設定來設定藍圖頁面，以便在展開藍圖頁面時使用。

請注意，Blueprint頁面的子頁面繼承配置。 當您設定使用轉出設定時，您可能會覆寫頁面繼承自其父項的設定。

1. 使用 **Sites** Console來選取Blueprint的根頁面。
1. 從工 **具欄中** ，選擇「屬性」。
1. 開啟「 **Blueprint** 」標籤。
1. 使用下拉式選 **擇器** ，選取一或多個轉出設定。
1. 使用「儲存」保留您 **的更新**。

### 設定系統預設轉出配置 {#setting-the-system-default-rollout-configuration}

指定轉出配置，以用作系統預設值。 若要指定預設值，請設定OSGi服務：

* **Day CQ WCM Live Relationship Manager** the service PID is `com.day.cq.wcm.msm.impl.LiveRelationshipManagerImpl`

使用 [Web Console或儲存庫節點](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) ，配置 [服務](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)。

* 在Web主控台中，要設定的屬性名稱為「預設轉出設定」。
* 使用儲存庫節點時，要配置的屬性的名稱為 `liverelationshipmgr.relationsconfig.default`。

將此屬性值設定為轉出配置的路徑，以用作系統預設值。 預設值為 `/etc/msm/rolloutconfigs/default`標準轉出 **設定**。
