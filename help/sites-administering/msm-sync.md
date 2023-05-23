---
title: 設定 Live Copy 同步
seo-title: Configuring Live Copy Synchronization
description: 瞭解配置即時複製同步。
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
source-git-commit: 96aa75dec7433aa3961944fa57a80c4719316ba5
workflow-type: tm+mt
source-wordcount: '2696'
ht-degree: 4%

---

# 設定 Live Copy 同步{#configuring-live-copy-synchronization}

執行以下任務來控制即時拷貝與其源內容同步的方式和時間。

* 決定現有的推廣配置是否滿足您的要求，或者您是否需要建立一個或多個。
* 指定要用於即時副本的推廣配置。

## 已安裝和自定義部署配置 {#installed-and-custom-rollout-configurations}

本節提供有關已安裝的部署配置及其使用的同步操作的資訊，以及如何根據需要建立自定義配置。

>[!CAUTION]
>
>更新或更改現成（已安裝）的部署配置 **不** 推薦。 如果需要自定義即時操作，則應在自定義部署配置中添加該操作。

### 推廣觸發器 {#rollout-triggers}

每個推廣配置都使用一種引發推廣的觸發器。 推廣配置可以使用以下觸發器之一：

* **推出時**:的 **推廣** 命令用於藍色打印頁面，或 **同步** 命令用於即時複製頁面。

* **論修改**:源頁面已修改。

* **激活時**:源頁面已激活。

* **停用時**:源頁面已停用。

>[!NOTE]
>
>使用「修改時」觸發器會影響效能。 請參閱 [MSM最佳做法](/help/sites-administering/msm-best-practices.md#onmodify) 的子菜單。

### 已安裝的部署配置 {#installed-rollout-configurations}

下表列出了隨之安裝的部署配AEM置。 該表包括每個轉出配置的觸發器和同步操作。 如果安裝的推廣配置操作不符合您的要求，您可以 [建立新的部署配置](#creating-a-rollout-configuration)。

<table>
 <tbody>
  <tr>
   <th>名稱</th>
   <th>說明</th>
   <th>觸發器</th>
   <th>同步操作<br /> <br /> 參見 <a href="#installed-synchronization-actions">已安裝的同步操作</a></th>
  </tr>
  <tr>
   <td>標準轉出設定</td>
   <td>標準轉出設定，允許於轉出觸發時開始轉出程序，並執行下列動作: 建立、更新、刪除內容以及排序子節點。</td>
   <td>於轉出</td>
   <td>內容更新<br /> 內容複製<br /> 內容刪除<br /> 引用更新<br /> 產品更新<br /> 訂單子項</td>
  </tr>
  <tr>
   <td>在 Blueprint 啟動時啟動</td>
   <td>發佈源時發佈即時副本。</td>
   <td>啟動時</td>
   <td>目標激活</td>
  </tr>
  <tr>
   <td>在 Blueprint 停用時停用</td>
   <td>在禁用源時停用即時副本。</td>
   <td>停用</td>
   <td>目標停用<br /> </td>
  </tr>
  <tr>
   <td>在發生修改時推送</td>
   <td><p>修改源時將內容推送到即時副本。</p> <p>在使用「修改時」觸發器時，請節省使用此部署配置。</p> </td>
   <td>於修改</td>
   <td>內容更新<br /> 內容複製<br /> 內容刪除<br /> 引用更新<br /> 訂單子項<br /> </td>
  </tr>
  <tr>
   <td>在發生修改時推送 (淺層)</td>
   <td><p>在修改藍圖頁面時將內容推送到即時副本，而不更新引用（例如，對於淺拷貝）。</p> <p>在使用「修改時」觸發器時，請節省使用此部署配置。</p> </td>
   <td>於修改</td>
   <td>內容更新<br /> 內容複製<br /> 內容刪除<br /> 訂單子項</td>
  </tr>
  <tr>
   <td>提升啟動</td>
   <td>提升啟動頁面的標準轉出設定。</td>
   <td>於轉出</td>
   <td>內容更新<br /> 內容複製<br /> 內容刪除<br /> 引用更新<br /> 訂單子項<br /> markLiveRelationship</td>
  </tr>
  <tr>
   <td>目錄頁內容部署配置</td>
   <td>從目錄 Blueprint 套用頁面範本。</td>
   <td>於轉出</td>
   <td>內容更新<br /> 內容複製<br /> 內容刪除<br /> 引用更新<br /> productCreateUpdate<br /> 訂單子項</td>
  </tr>
  <tr>
   <td>目錄頁面更新轉出設定</td>
   <td>應用目錄藍圖中的目標屬性。 必須在目錄頁內容部署配置後運行。</td>
   <td>於轉出</td>
   <td>catalogOullotHooks</td>
  </tr>
  <tr>
   <td>DPS 發佈轉出設定</td>
   <td>DPS發佈展出配置，允許在展出觸發器上啟動展出過程，同時在初始展出時排除FolioProducer綁定屬性</td>
   <td>於轉出</td>
   <td>內容更新<br /> 內容複製<br /> 內容刪除<br /> 引用更新<br /> 訂單子項<br /> dps元資料篩選器</td>
  </tr>
  <tr>
   <td>舊版(5.6.0)目錄部署配置</td>
   <td>已棄用。轉出目錄時不使用 MSM，並改用 Catalog Generator。</td>
   <td>於轉出</td>
   <td>編輯屬性</td>
  </tr>
 </tbody>
</table>

### 已安裝的同步操作 {#installed-synchronization-actions}

下表列出了隨安裝的同步操AEM作。 如果安裝的操作不符合您的要求，您可以 [建立新同步操作](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action)。

<table>
 <tbody>
  <tr>
   <th>操作名稱</th>
   <th>說明</th>
   <th>屬性<br /> </th>
  </tr>
  <tr>
   <td>內容複製</td>
   <td>如果源的節點在即時拷貝上不存在，則將節點複製到即時拷貝。 <a href="#excluding-properties-and-node-types-from-synchronization">配置CQ MSM內容複製操作服務</a> 指定要排除的節點類型、段落項和頁面屬性。 <br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>內容刪除</td>
   <td><p>刪除源上不存在的活動副本的節點。 <a href="#excluding-properties-and-node-types-from-synchronization">配置CQ MSM內容刪除操作服務</a> 指定要排除的節點類型、段落項和頁面屬性。 </p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>內容更新</td>
   <td>使用源中的更改更新即時拷貝內容。 <a href="#excluding-properties-and-node-types-from-synchronization">配置CQ MSM內容更新操作服務</a> 指定要排除的節點類型、段落項和頁面屬性。 <br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>編輯屬性</td>
   <td><p>編輯即時副本的屬性。 editMap屬性確定要編輯的屬性及其值。 editMap屬性的值必須使用以下格式：</p> <p><code>[property_name_1]#[current_value]#</code>[new_value],<br /> <code>[property_name_2]#[current_value]#</code>[new_value],<br /> ...。<br /> <code>[property_name_n]#[current_value]#</code>[new_value]</p> <p>的 <code>current_value</code> 和 <code>new_value</code> 項是規則運算式。 <br /> </p> <p>例如，請考慮editMap的以下值：</p> <p><code>sling:resourceType#/</code>（內容頁|首頁）#/<br /> 移動網頁，<br /> cq:template#/contenpage#/mobilecontentpage</p> <p>此值編輯即時複製節點的屬性，如下所示：</p>
    <ul>
     <li>的 <code>sling:resourceType</code> 屬性設定為 <code>contentpage</code> 或 <code>homepage</code> 設定為 <code>mobilecontentpage.</code></li>
     <li>的 <code>cq:template</code> 設定為的屬性 <code>contentpage</code> 設定為 <code>mobilecontentpage.</code></li>
    </ul> </td>
   <td><p> </p> <p>編輯映射：（字串）標識屬性、當前值和新值。 有關資訊，請參閱說明。<br /> </p> </td>
  </tr>
  <tr>
   <td>通知</td>
   <td>發送已滾出頁面的頁面事件。 要得到通知，首先需要訂閱推廣活動。</td>
   <td> </td>
  </tr>
  <tr>
   <td>訂單子項</td>
   <td>在即時拷貝中，它根據藍圖上的順序對子（節點）進行排序<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td>引用更新</td>
   <td><p>在即時拷貝上，此同步操作會更新引用，如連結。<br /> 它在即時複製頁中搜索指向藍圖中資源的路徑。 找到後，它會更新路徑以指向即時副本（而不是藍圖）中的相關資源。 在藍圖之外具有目標的參照不會更改。</p> <p><a href="#excluding-properties-and-node-types-from-synchronization">配置CQ MSM引用更新操作服務</a> 指定要排除的節點類型、段落項和頁面屬性。 </p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>目標版本</td>
   <td><p>建立即時副本的版本。</p> <p>此操作必須是部署配置中包含的唯一同步操作。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>目標激活</td>
   <td><p>激活即時副本。</p> <p>此操作必須是部署配置中包含的唯一同步操作。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>目標停用</td>
   <td><p>停用即時副本。</p> <p>此操作必須是部署配置中包含的唯一同步操作。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td>工作流程</td>
   <td><p>啟動由目標屬性定義的工作流（僅適用於頁面），並將即時副本作為負載。</p> <p>目標路徑是模型節點的路徑。</p> </td>
   <td>目標：（字串）工作流模型的路徑。<br /> </td>
  </tr>
  <tr>
   <td>強制</td>
   <td><p>將即時複製頁上多個ACL的權限設定為特定用戶組的只讀權限。 配置了以下ACL:</p>
    <ul>
     <li>ActionSet.ACTION_NAME_REMOVE</li>
     <li>ActionSet.ACTION_NAME_SET_PROPERTY</li>
     <li>ActionSet.ACTION_NAME_ACL_MODIFY</li>
    </ul> <p>僅對頁面使用此操作。</p> </td>
   <td>目標：（字串）要為其設定權限的組的ID。 <br /> </td>
  </tr>
  <tr>
   <td>強制內容</td>
   <td><p>將即時複製頁上多個ACL的權限設定為特定用戶組的只讀權限。 配置了以下ACL:</p>
    <ul>
     <li>ActionSet.ACTION_NAME_SET_PROPERTY</li>
     <li>ActionSet.ACTION_NAME_ACL_MODIFY</li>
    </ul> <p>僅對頁面使用此操作。</p> </td>
   <td>目標：（字串）要為其設定權限的組的ID。 </td>
  </tr>
  <tr>
   <td>強制結構</td>
   <td>將ActionSet.ACTION_NAME_REMOVE ACL在即時複製頁上的權限設定為特定用戶組的只讀。 僅對頁面使用此操作。</td>
   <td>目標：（字串）要為其設定權限的組的ID。 </td>
  </tr>
  <tr>
   <td>版本複製操作</td>
   <td>如果藍圖/源頁面至少已發佈一次，則使用已發佈的版本建立即時副本頁面。 注：此操作僅可用於基於已發佈的源頁面建立即時拷貝頁面，而不可用於更新現有即時拷貝頁面。 </td>
   <td> </td>
  </tr>
  <tr>
   <td>頁移動操作</td>
   <td><p>在藍圖中移動頁面時，PageMoveAction將應用。</p> <p>操作將複製（相關）LiveCopy頁面，而不是將其從移動之前的位置移動到之後的位置。</p> <p>PageMoveAction不會更改移動前位置的LiveCopy頁面。 因此，對於連續的SollutConfigurations，它的狀態為LiveRelationhip（無Bluepint）。</p> <p><a href="#excluding-properties-and-node-types-from-synchronization">配置CQ MSM頁移動操作服務</a> 指定要排除的節點類型、段落項和頁面屬性。 </p> <p>此操作必須是部署配置中包含的唯一同步操作。</p> </td>
   <td><p>prop_referenceUpdate:（布爾值）設定為true以更新引用。 預設值為true。</p> <p> </p> </td>
  </tr>
  <tr>
   <td>productCreateUpdate</td>
   <td>在目錄中建立或更新產品資源。 此操作應用於以下情況之一：
    <ul>
     <li>生成或滾出目錄（或目錄部分）</li>
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
   <td>catalogOullotHooks</td>
   <td>執行特定於目錄生成的轉出掛接。 調用CatalogGenerator的executePageSolutHooks和executeProductSoultHooks方法。<br /> 請參見Javadocs中的com.adobe.cq.commerce.pim.api.CatalogGeneratorAEM。</td>
   <td> </td>
  </tr>
  <tr>
   <td>產品更新</td>
   <td>在產品目錄的即時副本中更新產品頁面</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### 建立部署配置 {#creating-a-rollout-configuration}

你可以 [建立部署配置](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration) 當安裝的部署配置不滿足您的應用程式要求時：

* [建立部署配置](/help/sites-developing/extending-msm.md#create-the-rollout-configuration)。
* [將同步操作添加到展示配置](/help/sites-developing/extending-msm.md#add-synchronization-actions-to-the-rollout-configuration)。

然後，在藍圖或即時複製頁上設定部署配置時，您可以使用新的部署配置。

### 從同步中排除屬性和節點類型 {#excluding-properties-and-node-types-from-synchronization}

您可以配置幾個支援相應同步操作的OSGi服務，以便它們不會影響特定的節點類型和屬性。 例如，與內部功能相關的許多屬性和子節AEM點不應包含在即時副本中。 只應複製與頁面用戶相關的內容。

使用時，AEM有幾種方法管理此類服務的配置設定；見 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 的子菜單。

下表列出了可以指定要排除的節點的同步操作。 該表提供了使用Web控制台進行配置的服務的名稱和使用儲存庫節點進行配置的PID。

| 同步操作 | Web控制台中的服務名稱 | 服務PID |
|---|---|---|
| 內容複製 | CQ MSM內容複製操作 | com.day.cq.wcm.msm.impl.actions.ContentCopyActionFactory |
| 內容刪除 | CQ MSM內容刪除操作 | com.day.cq.wcm.msm.impl.actions.ContentDeleteActionFactory |
| 內容更新 | CQ MSM內容更新操作 | com.day.cq.wcm.msm.impl.actions.ContentUpdateActionFactory |
| 頁移動操作 | CQ MSM頁移動操作 | com.day.cq.wcm.msm.impl.actions.PageMoveActionFactory |
| 引用更新 | CQ MSM引用更新操作 | com.day.cq.wcm.msm.impl.actions.ReferencesUpdateActionFactory |

下表介紹了可以配置的屬性：

<table>
 <tbody>
  <tr>
   <th>Web控制台屬性/OSGi屬性</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><p>排除的節點類型</p> <p>cq.wcm.msm.action.excludednodetypes</p> </td>
   <td>與要從同步操作中排除的節點類型匹配的規則運算式。</td>
  </tr>
  <tr>
   <td><p>排除的段落項</p> <p>cq.wcm.msm.action.excludedparagraphitems</p> </td>
   <td>與要從同步操作中排除的段落項匹配的規則運算式。</td>
  </tr>
  <tr>
   <td><p>排除的頁面屬性</p> <p>cq.wcm.msm.action.excludedprops</p> </td>
   <td>與要從同步操作中排除的頁面屬性相匹配的規則運算式。</td>
  </tr>
  <tr>
   <td><p>忽略的混合節點類型</p> <p>cq.wcm.msm.action.ignoredMixin</p> </td>
   <td>僅適用於CQ MSM內容更新操作。 與要從同步操作中排除的混合節點類型的名稱相匹配的規則運算式。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>在「經典」UI中，LiveCopy頁的「頁屬性」對話框中顯示的鎖定表徵圖不反映「排除的頁屬性」屬性的配置。 即使對於從同步操作中排除的屬性，也會顯示鎖定表徵圖。

>[!NOTE]
>
>在觸控優化的UI中，另請參閱 [在頁面屬性上配置MSM鎖（觸控優化UI）](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-pagep-roperties-touch-optimized-ui)。

#### CQ MSM內容更新操作 — 排除 {#cq-msm-content-update-action-exclusions}

預設情況下，會排除一些屬性和節點類型，這些屬性和節點類型在OSGi配置中定義 **CQ MSM內容更新操作**&#x200B;下 **排除的頁面屬性**。

預設情況下，與以下規則運算式匹配的屬性在部署時被排除（即未更新）:

![chlimage_1](assets/chlimage_1.png)

您可以根據需要更改定義排除清單的表達式。

例如，如果您希望 **標題** 要包括在考慮部署的更改中，請刪除 `jcr:title` 排除項。 例如，使用regex:

`jcr:(?!(title)$).*`

### 配置同步以更新引用 {#configuring-synchronization-for-updating-references}

您可以配置多個OSGi服務，這些服務支援與更新引用相關的相應同步操作。

使用時，AEM有幾種方法管理此類服務的配置設定；見 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 的子菜單。

下表列出了可為其指定引用更新的同步操作。 該表提供了使用Web控制台進行配置的服務的名稱和使用儲存庫節點進行配置的PID。

<table>
 <tbody>
  <tr>
   <th>Web控制台屬性/OSGi屬性</th>
   <th>說明</th>
  </tr>
  <tr>
   <td><p>跨嵌套LiveCopys更新引用</p> <p>cq.wcm.msm.impl.action.referencesupdate.prop_updateNested</p> </td>
   <td>僅可用於CQ MSM引用更新操作。 選擇此選項（Web控制台）或將此布爾屬性設定為true（儲存庫配置），以替換針對位於最頂層LiveCopy分支中的任何資源的引用。</td>
  </tr>
  <tr>
   <td><p>更新引用頁</p> <p>cq.wcm.msm.impl.actions.pagemove.prop_referenceUpdate</p> </td>
   <td>僅可用於CQ MSM頁面移動操作。 選擇此選項（Web控制台）或將此布爾屬性設定為 <code>true</code> （儲存庫配置），以更新任何引用，以使用原始頁引用LiveCopy頁。</td>
  </tr>
 </tbody>
</table>

## 指定要使用的展示配置 {#specifying-the-rollout-configurations-to-use}

MSM使您能夠指定一些通常使用的推廣配置集，並且如果需要，可以覆蓋特定即時副本的這些配置集。 MSM提供了多個位置，用於指定要使用的推廣配置。 該位置確定配置是否適用於特定即時副本。

以下位置清單可指定要使用的部署配置，說明MSM如何確定用於即時拷貝的部署配置：

* **[即時複製頁屬性](/help/sites-administering/msm-sync.md#setting-the-rollout-configurations-for-a-live-copy-page):** 將即時拷貝頁面配置為使用一個或多個部署配置時，MSM使用這些部署配置。
* **[藍圖頁屬性](/help/sites-administering/msm-sync.md#setting-the-rollout-configuration-for-a-blueprint-page):** 當即時拷貝基於藍圖，且即時拷貝頁面未配置有部署配置時，將使用與藍圖源頁面關聯的部署配置。
* **即時複製父頁屬性：** 如果未使用部署配置配置即時拷貝頁和藍圖源頁，則使用應用於即時拷貝頁的父頁的部署配置。
* **[系統預設值](/help/sites-administering/msm-sync.md#setting-the-system-default-rollout-configuration):** 當無法確定即時副本的父頁的部署配置時，將使用系統預設的部署配置。

例如，藍圖使用We.Retail參考站點作為源內容。 根據藍圖建立站點。 以下清單中的每個項目都描述了有關部署配置使用的不同方案：

* 未將藍圖頁面或即時拷貝頁面配置為使用部署配置。 MSM對所有即時拷貝頁使用系統預設部署配置。
* We.Retail參考站點的根頁配置了幾個部署配置。 MSM將這些部署配置用於所有即時拷貝頁面。
* We.Retail Reference網站的根頁配置了多個推廣配置，而即時拷貝網站的根頁配置了一組不同的推廣配置。 MSM使用在即時拷貝站點的根頁面上配置的部署配置。

### 設定即時複製頁的部署配置 {#setting-the-rollout-configurations-for-a-live-copy-page}

使用展開配置配置配置動態複製頁，以便在展開源頁時使用。 預設情況下，子頁繼承配置。 將部署配置配置為使用時，將覆蓋即時複製頁從其父級繼承的配置。

您還可以配置即時拷貝頁面的部署配置 [建立即時拷貝](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)。

1. 使用 **站點** 控制台，以選擇即時複製頁。
1. 選擇 **屬性** 的子菜單。
1. 開啟 **即時拷貝** 頁籤。

   的 **配置** 部分顯示頁面繼承的展開配置。

   ![chlimage_1-1](assets/chlimage_1-1.png)

1. 如果需要，請調整 **即時複製繼承** 。 如果選中，則即時複製配置對所有子項都有效。

1. 清除 **從父代繼承展示配置** 屬性，然後從清單中選擇一個或多個部署配置。

   選定的部署配置顯示在下拉清單下方。

   ![chlimage_1-2](assets/chlimage_1-2.png)

1. 按一下或點擊 **保存**。

### 設定藍圖頁的部署配置 {#setting-the-rollout-configuration-for-a-blueprint-page}

使用展開配置配置配置藍圖頁，以在展開藍圖頁時使用。

請注意，藍圖頁的子頁繼承配置。 配置要使用的展示配置時，可以覆蓋頁面從其父級繼承的配置。

1. 使用 **站點** 控制台，以選擇藍圖的根頁。
1. 選擇 **屬性** 的子菜單。
1. 開啟 **藍圖** 頁籤。
1. 選擇一個或多個 **推廣配置** 使用下拉選擇器。
1. 保留更新 **保存**。

### 設定系統預設部署配置 {#setting-the-system-default-rollout-configuration}

指定要用作系統預設值的轉出配置。 要指定預設值，請配置OSGi服務：

* **第CQ WCM Live關係管理器**
服務PID為 
`com.day.cq.wcm.msm.impl.LiveRelationshipManagerImpl`

使用 [Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) 或 [儲存庫節點](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)。

* 在Web控制台中，要配置的屬性的名稱為預設的部署配置。
* 使用儲存庫節點，要配置的屬性的名稱為 `liverelationshipmgr.relationsconfig.default`。

將此屬性值設定為要用作系統預設值的推廣配置路徑。 預設值為 `/libs/msm/wcm/rolloutconfigs/default`，即 **標準部署配置**。
