---
title: 配置Live Copy同步
seo-title: Configuring Live Copy Synchronization
description: 了解如何設定Live Copy同步。
seo-description: Learn about configuring Live Copy Synchronization.
uuid: a5db0bee-a761-4cff-81dc-31b374525f47
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 6bcf0fcc-481a-4283-b30d-80b517701280
docset: aem65
feature: Multi Site Manager
exl-id: ac24b8b4-b3ed-47fa-9a73-03f0c9e68ac8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2697'
ht-degree: 3%

---

# 配置Live Copy同步{#configuring-live-copy-synchronization}

執行以下任務以控制即時副本與其源內容同步的方式和時間。

* 決定現有的轉出設定是否符合您的需求，或您是否需要建立一或多個轉出設定。
* 指定要用於即時副本的轉出設定。

## 安裝和自訂轉出設定 {#installed-and-custom-rollout-configurations}

本節提供有關已安裝轉出設定及其使用的同步動作，以及如有需要如何建立自訂設定的資訊。

>[!CAUTION]
>
>更新或變更現成可用（已安裝）的轉出設定為 **not** 建議。 如果需要自訂即時動作，則應將其新增至自訂轉出設定。

### 轉出觸發器 {#rollout-triggers}

每個轉出設定都使用轉出觸發器，而導致轉出發生。 轉出設定可使用下列其中一個觸發器：

* **轉出時**:此 **轉出** 命令用於藍色打印頁，或 **同步** 命令。

* **修改**:已修改源頁。

* **啟動時**:源頁面已激活。

* **停用時**:源頁面已停用。

>[!NOTE]
>
>使用「修改時」觸發器可能會影響效能。 請參閱 [MSM最佳實務](/help/sites-administering/msm-best-practices.md#onmodify) 以取得更多資訊。

### 安裝的轉出設定 {#installed-rollout-configurations}

下表列出隨AEM安裝的轉出設定。 表格包含每個轉出設定的觸發和同步動作。 如果安裝的轉出設定動作不符合您的需求，您可以 [建立新的轉出設定](#creating-a-rollout-configuration).

<table>
 <tbody>
  <tr>
   <th>名稱</th>
   <th>說明</th>
   <th>觸發器</th>
   <th>同步操作<br /> <br /> 另請參閱 <a href="#installed-synchronization-actions">已安裝的同步操作</a></th>
  </tr>
  <tr>
   <td>標準轉出設定</td>
   <td>標準轉出設定，允許於轉出觸發時開始轉出程序，並執行下列動作: 建立、更新、刪除內容以及排序子節點。</td>
   <td>於轉出</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> productUpdate<br /> orderChildren</td>
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
   <td><p>修改來源時推送內容至即時副本。</p> <p>請謹慎使用此轉出設定，因為它使用「修改時」觸發器。</p> </td>
   <td>於修改</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> orderChildren<br /> </td>
  </tr>
  <tr>
   <td>在發生修改時推送 (淺層)</td>
   <td><p>修改Blueprint頁面時推送內容至即時副本，而不更新參考（例如淺層副本）。</p> <p>請謹慎使用此轉出設定，因為它使用「修改時」觸發器。</p> </td>
   <td>於修改</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> orderChildren</td>
  </tr>
  <tr>
   <td>提升啟動</td>
   <td>提升啟動頁面的標準轉出設定。</td>
   <td>於轉出</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> orderChildren<br /> markLiveRelationship</td>
  </tr>
  <tr>
   <td>目錄頁面內容轉出設定</td>
   <td>從目錄 Blueprint 套用頁面範本。</td>
   <td>於轉出</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> productCreateUpdate<br /> orderChildren</td>
  </tr>
  <tr>
   <td>目錄頁面更新轉出設定</td>
   <td>從目錄藍圖套用目標屬性。 必須在目錄頁面內容轉出設定後執行。</td>
   <td>於轉出</td>
   <td>catalogRollotHooks</td>
  </tr>
  <tr>
   <td>DPS 發佈轉出設定</td>
   <td>DPS發佈轉出設定，允許在轉出觸發時開始轉出程式，同時在初始轉出時排除FolioProducer系結屬性</td>
   <td>於轉出</td>
   <td>contentUpdate<br /> contentCopy<br /> contentDelete<br /> referencesUpdate<br /> orderChildren<br /> dpsMetadataFilter</td>
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

下表列出隨AEM安裝的同步操作。 如果已安裝的動作不符合您的需求，您可以 [建立新的同步操作](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action).

<table>
 <tbody>
  <tr>
   <th>動作名稱</th>
   <th>說明</th>
   <th>屬性<br /> </th>
  </tr>
  <tr>
   <td>contentCopy</td>
   <td>如果Live Copy上不存在源節點，則將節點複製到Live Copy。 <a href="#excluding-properties-and-node-types-from-synchronization">設定CQ MSM內容複製動作服務</a> 指定要排除的節點類型、段落項和頁面屬性。 <br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>contentDelete</td>
   <td><p>刪除源上不存在的即時副本節點。 <a href="#excluding-properties-and-node-types-from-synchronization">設定CQ MSM內容刪除動作服務</a> 指定要排除的節點類型、段落項和頁面屬性。 </p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>contentUpdate</td>
   <td>使用來源的變更更新即時副本內容。 <a href="#excluding-properties-and-node-types-from-synchronization">設定CQ MSM內容更新動作服務</a> 指定要排除的節點類型、段落項和頁面屬性。 <br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>editProperties</td>
   <td><p>編輯即時副本的屬性。 editMap屬性決定要編輯的屬性及其值。 editMap屬性的值必須使用下列格式：</p> <p><code>[property_name_1]#[current_value]#</code>[new_value],<br /> <code>[property_name_2]#[current_value]#</code>[new_value],<br /> ... ,<br /> <code>[property_name_n]#[current_value]#</code>[new_value]</p> <p>此 <code>current_value</code> 和 <code>new_value</code> 項目是規則運算式。 <br /> </p> <p>例如，請考量下列editMap值：</p> <p><code>sling:resourceType#/</code>(contentpage|homepage)#/<br /> mobilecontentpage,<br /> cq:template#/contentpage#/mobilecontentpage</p> <p>此值會編輯即時副本節點的屬性，如下所示：</p>
    <ul>
     <li>此 <code>sling:resourceType</code> 屬性 <code>contentpage</code> 或 <code>homepage</code> 設為 <code>mobilecontentpage.</code></li>
     <li>此 <code>cq:template</code> 設為的屬性 <code>contentpage</code> 設為 <code>mobilecontentpage.</code></li>
    </ul> </td>
   <td><p> </p> <p>editMap:（字串）識別屬性、目前值和新值。 如需詳細資訊，請參閱說明。<br /> </p> </td>
  </tr>
  <tr>
   <td>通知</td>
   <td>傳送已轉出頁面的頁面事件。 若要收到通知，需先訂閱轉出事件。</td>
   <td> </td>
  </tr>
  <tr>
   <td>orderChildren</td>
   <td>在即時副本上，會根據Blueprint上的順序來排序子項（節點）<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>referencesUpdate</td>
   <td><p>在即時副本上，此同步動作會更新類似連結的參考。<br /> 它會搜尋即時副本頁面中指向Blueprint內資源的路徑。 找到後，會更新路徑，以指向即時副本（而非Blueprint）中的相關資源。 在Blueprint外具有目標的參照不會變更。</p> <p><a href="#excluding-properties-and-node-types-from-synchronization">設定CQ MSM參考更新動作服務</a> 指定要排除的節點類型、段落項和頁面屬性。 </p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetVersion</td>
   <td><p>建立即時副本的版本。</p> <p>此動作必須是轉出設定中唯一包含的同步動作。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetActivate</td>
   <td><p>啟動即時副本。</p> <p>此動作必須是轉出設定中唯一包含的同步動作。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>targetDeactivate</td>
   <td><p>停用即時副本。</p> <p>此動作必須是轉出設定中唯一包含的同步動作。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>工作流程</td>
   <td><p>啟動由target屬性定義的工作流程（僅適用於頁面），並將即時副本視為裝載。</p> <p>目標路徑是模型節點的路徑。</p> </td>
   <td>目標：（字串）工作流程模型的路徑。<br /> </td>
  </tr>
  <tr>
   <td>強制</td>
   <td><p>將即時副本頁面上多個ACL的權限設定為特定用戶組的只讀權限。 配置了以下ACL:</p>
    <ul>
     <li>ActionSet.ACTION_NAME_REMOVE</li>
     <li>ActionSet.ACTION_NAME_SET_PROPERTY</li>
     <li>ActionSet.ACTION_NAME_ACL_MODIFY</li>
    </ul> <p>僅對頁面使用此動作。</p> </td>
   <td>目標：（字串）您要設定權限之群組的ID。 <br /> </td>
  </tr>
  <tr>
   <td>mandatoryContent</td>
   <td><p>將即時副本頁面上多個ACL的權限設定為特定用戶組的只讀權限。 配置了以下ACL:</p>
    <ul>
     <li>ActionSet.ACTION_NAME_SET_PROPERTY</li>
     <li>ActionSet.ACTION_NAME_ACL_MODIFY</li>
    </ul> <p>僅對頁面使用此動作。</p> </td>
   <td>目標：（字串）您要設定權限之群組的ID。 </td>
  </tr>
  <tr>
   <td>mandatoryStructure</td>
   <td>將ActionSet.ACTION_NAME_REMOVE ACL在Live Copy頁上的權限設定為特定用戶組的只讀。 僅對頁面使用此動作。</td>
   <td>目標：（字串）您要設定權限之群組的ID。 </td>
  </tr>
  <tr>
   <td>VersionCopyAction</td>
   <td>如果Blueprint/來源頁面至少已發佈一次，則會使用已發佈的版本建立即時副本頁面。 注意：此動作僅適用於根據已發佈的來源頁面建立即時副本頁面，不適用於更新現有的即時副本頁面。 </td>
   <td> </td>
  </tr>
  <tr>
   <td>PageMoveAction</td>
   <td><p>當頁面在Blueprint中移動時，PageMoveAction即會套用。</p> <p>動作會複製，而非將（相關的）LiveCopy頁面從移動前的位置移至之後的位置。</p> <p>PageMoveAction不會變更移動前位置的LiveCopy頁面。 因此，對於連續的RolloutConfigurations，其狀態為不含Blueprint的LiveRelationship。</p> <p><a href="#excluding-properties-and-node-types-from-synchronization">設定CQ MSM頁面移動動作服務</a> 指定要排除的節點類型、段落項和頁面屬性。 </p> <p>此動作必須是轉出設定中唯一包含的同步動作。</p> </td>
   <td><p>prop_referenceUpdate:（布林值）設為true可更新參考。 預設為true。</p> <p> </p> </td>
  </tr>
  <tr>
   <td>productCreateUpdate</td>
   <td>在目錄中建立或更新產品資源。 此動作應用於下列其中一種情況：
    <ul>
     <li>產生或轉出目錄（或目錄區段）</li>
     <li>用戶恢復產品元件的同步繼承。</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>markLiveRelationship</td>
   <td>指出啟動建立的內容存在即時關係。</td>
   <td> </td>
  </tr>
  <tr>
   <td>catalogRollotHooks</td>
   <td>執行目錄產生專用轉出鈎點。 呼叫目錄產生器的executePageRolloutHooks和executeProductRolloutHooks方法。<br /> 請參閱AEM Javadocs中的com.adobe.cq.commerce.pim.api.CatalogGenerator 。</td>
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

您可以 [建立轉出設定](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration) 當安裝的轉出設定不符合您的應用程式需求時：

* [建立轉出設定](/help/sites-developing/extending-msm.md#create-the-rollout-configuration).
* [將同步化動作新增至轉出設定](/help/sites-developing/extending-msm.md#add-synchronization-actions-to-the-rollout-configuration).

接著，當您在Blueprint或Live Copy頁面上設定轉出設定時，即可使用新的轉出設定。

### 從同步中排除屬性和節點類型 {#excluding-properties-and-node-types-from-synchronization}

您可以配置多個支援相應同步操作的OSGi服務，以使其不影響特定節點類型和屬性。 例如，與AEM內部功能相關的許多屬性和子節點不應包含在即時副本中。 只應複製與頁面使用者相關的內容。

使用AEM時，有數種方法可管理這類服務的組態設定；請參閱 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以取得詳細資訊和建議的實務。

下表列出了可以指定要排除的節點的同步操作。 該表提供了使用Web控制台進行配置的服務的名稱，以及使用儲存庫節點進行配置的PID。

| 同步操作 | Web控制台中的服務名 | 服務PID |
|---|---|---|
| contentCopy | CQ MSM內容複製動作 | com.day.cq.wcm.msm.impl.actions.ContentCopyActionFactory |
| contentDelete | CQ MSM內容刪除動作 | com.day.cq.wcm.msm.impl.actions.ContentDeleteActionFactory |
| contentUpdate | CQ MSM內容更新動作 | com.day.cq.wcm.msm.impl.actions.ContentUpdateActionFactory |
| PageMoveAction | CQ MSM頁面移動動作 | com.day.cq.wcm.msm.impl.actions.PageMoveActionFactory |
| referencesUpdate | CQ MSM參考更新動作 | com.day.cq.wcm.msm.impl.actions.ReferencesUpdateActionFactory |

下表說明了可以配置的屬性：

<table>
 <tbody>
  <tr>
   <th>Web控制台屬性/ OSGi屬性</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><p>排除的節點類型</p> <p>cq.wcm.msm.action.excludednodetypes</p> </td>
   <td>與要從同步操作中排除的節點類型匹配的規則表達式。</td>
  </tr>
  <tr>
   <td><p>排除的段落項目</p> <p>cq.wcm.msm.action.excludedparagraphitems</p> </td>
   <td>與要從同步操作中排除的段落項相匹配的規則表達式。</td>
  </tr>
  <tr>
   <td><p>排除的頁面屬性</p> <p>cq.wcm.msm.action.excludedprops</p> </td>
   <td>符合要從同步動作中排除之頁面屬性的規則運算式。</td>
  </tr>
  <tr>
   <td><p>忽略的Mixin NodeTypes</p> <p>cq.wcm.msm.action.ignoredMixin</p> </td>
   <td>僅適用於CQ MSM內容更新動作。 與要從同步操作中排除的mixin節點類型的名稱匹配的規則表達式。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>在傳統UI中，LiveCopy頁面的「頁面屬性」對話方塊中顯示的鎖定圖示不會反映「排除的頁面屬性」屬性的設定。 即使是從同步操作中排除的屬性，也會顯示鎖定表徵圖。

>[!NOTE]
>
>在觸控最佳化UI中，另請參閱 [在頁面屬性上設定MSM鎖（觸控最佳化UI）](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-pagep-roperties-touch-optimized-ui).

#### CQ MSM內容更新動作 — 排除項目 {#cq-msm-content-update-action-exclusions}

預設會排除數個屬性和節點類型，這些會在的OSGi設定中定義 **CQ MSM內容更新動作**，在 **排除的頁面屬性**.

依預設，轉出時會排除與下列規則運算式相符的屬性（即未更新）:

![chlimage_1](assets/chlimage_1.png)

您可以視需要變更定義排除清單的運算式。

例如，如果您想要頁面 **標題** 若要納入考慮轉出的變更中，請移除 `jcr:title` 從排除項目。 例如，使用規則運算式：

`jcr:(?!(title)$).*`

### 配置更新引用的同步 {#configuring-synchronization-for-updating-references}

您可以配置多個OSGi服務，這些服務支援與更新引用相關的相應同步操作。

使用AEM時，有數種方法可管理這類服務的組態設定；請參閱 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以取得詳細資訊和建議的實務。

下表列出了可以為其指定引用更新的同步操作。 該表提供了使用Web控制台進行配置的服務的名稱，以及使用儲存庫節點進行配置的PID。

<table>
 <tbody>
  <tr>
   <th>Web控制台屬性/ OSGi屬性</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><p>跨巢狀LiveCopy更新參考</p> <p>cq.wcm.msm.impl.action.referencesupdate.prop_updateNested</p> </td>
   <td>僅適用於CQ MSM參考更新動作。 選擇此選項（Web控制台）或將此布林屬性設定為true（儲存庫配置）以替換指向位於最頂層LiveCopy分支內的任何資源的引用。</td>
  </tr>
  <tr>
   <td><p>更新引用頁面</p> <p>cq.wcm.msm.impl.actions.pagemove.prop_referenceUpdate</p> </td>
   <td>僅適用於CQ MSM頁面移動動作。 選擇此選項（Web控制台），或將此布林屬性設定為 <code>true</code> （存放庫設定）來更新任何參照，以使用原始頁面來改為參考LiveCopy頁面。</td>
  </tr>
 </tbody>
</table>

## 指定要使用的轉出設定 {#specifying-the-rollout-configurations-to-use}

MSM可讓您指定一般使用的轉出設定集，並在需要時，您可以針對特定即時副本覆寫這些設定。 MSM提供數個位置，用以指定要使用的轉出設定。 位置會決定設定是否套用至特定即時副本。

下列位置清單可讓您指定要使用的轉出設定，說明MSM如何決定要用於即時副本的轉出設定：

* **[即時副本頁面屬性](/help/sites-administering/msm-sync.md#setting-the-rollout-configurations-for-a-live-copy-page):** 將即時副本頁面設定為使用一或多個轉出設定時，MSM會使用這些轉出設定。
* **[Blueprint頁面屬性](/help/sites-administering/msm-sync.md#setting-the-rollout-configuration-for-a-blueprint-page):** 當即時副本以Blueprint為基礎，且即時副本頁面未設定轉出設定時，會使用與Blueprint來源頁面相關聯的轉出設定。
* **Live Copy上層頁面屬性：** 當即時副本頁面和Blueprint來源頁面皆未設定轉出設定時，會使用套用至即時副本頁面上層頁面的轉出設定。
* **[系統預設值](/help/sites-administering/msm-sync.md#setting-the-system-default-rollout-configuration):** 當無法判斷即時副本上層頁面的轉出設定時，會使用系統預設的轉出設定。

例如，Blueprint使用We.Retail參考網站作為來源內容。 從Blueprint建立網站。 下列清單中的每個項目說明使用轉出設定的不同案例：

* 未將任何Blueprint頁面或即時副本頁面設定為使用轉出設定。 MSM會對所有即時副本頁面使用系統預設轉出設定。
* We.Retail參考網站的根頁面已設定數個轉出設定。 MSM會對所有即時副本頁面使用這些轉出設定。
* We.Retail參考網站的根頁面已設定數個轉出設定，而即時副本網站的根頁面則設定了一組不同的轉出設定。 MSM會使用即時副本網站根頁面上設定的轉出設定。

### 設定即時副本頁面的轉出設定 {#setting-the-rollout-configurations-for-a-live-copy-page}

使用轉出設定設定設定即時副本頁面，以便在轉出來源頁面時使用。 子頁預設繼承配置。 將轉出設定設為使用時，會覆寫即時副本頁面從其上層繼承的設定。

您也可以在您 [建立即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page).

1. 使用 **網站** 主控台來選取即時副本頁面。
1. 選擇 **屬性** 的上界。
1. 開啟 **Live Copy** 標籤。

   此 **設定** 節顯示頁面繼承的轉出配置。

   ![chlimage_1-1](assets/chlimage_1-1.png)

1. 如有需要，請調整 **即時副本繼承** 標籤。 如果已勾選，則即時副本配置對所有子項都有效。

1. 清除 **從父級繼承轉出配置** 屬性，然後從清單中選取一或多個轉出設定。

   選取的轉出設定會顯示在下拉式清單下方。

   ![chlimage_1-2](assets/chlimage_1-2.png)

1. 按一下或點選 **儲存**.

### 設定Blueprint頁面的轉出設定 {#setting-the-rollout-configuration-for-a-blueprint-page}

使用轉出設定設定設定藍圖頁面，以在Blueprint頁面推出時使用。

請注意，Blueprint頁面的子頁面會繼承設定。 將轉出配置配置配置為使用時，可能正在覆蓋頁面從其父級繼承的配置。

1. 使用 **網站** 控制台，以選取blueprint的根頁面。
1. 選擇 **屬性** 的上界。
1. 開啟 **Blueprint** 標籤。
1. 選取一或多個 **轉出設定** 使用下拉式選取器。
1. 將更新保留為 **儲存**.

### 設定系統預設轉出配置 {#setting-the-system-default-rollout-configuration}

指定轉出設定以作為系統預設值。 若要指定預設值，請設定OSGi服務：

* **Day CQ WCM Live Relationship Manager**
服務PID為 
`com.day.cq.wcm.msm.impl.LiveRelationshipManagerImpl`

使用 [Web主控台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 或 [存放庫節點](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository).

* 在Web主控台中，要設定的屬性名稱為「預設轉出設定」。
* 使用儲存庫節點時，要配置的屬性名稱為 `liverelationshipmgr.relationsconfig.default`.

將此屬性值設定為轉出配置的路徑，以用作系統預設值。 預設值為 `/libs/msm/wcm/rolloutconfigs/default`，即 **標準轉出設定**.
