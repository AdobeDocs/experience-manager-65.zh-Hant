---
title: MSM 推出衝突
seo-title: MSM Rollout Conflicts
description: 瞭解如何處理多站點管理器部署衝突。
seo-description: Learn how to deal with Multi Site Manager rollout conflicts.
uuid: 7a640905-aae2-498e-b95c-2c73008fa1cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 16db5334-604f-44e2-9993-10d683dee5bb
feature: Multi Site Manager
exl-id: e145e79a-c363-4a33-b9f9-99502ed20563
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 1%

---

# MSM 推出衝突{#msm-rollout-conflicts}

如果在藍圖分支和從屬即時副本分支中都建立了具有相同頁名的新頁，則可能會發生衝突。

這些衝突需要在部署時得到處理和解決。

## 衝突處理 {#conflict-handling}

當衝突頁面確實存在（在藍圖和即時拷貝分支中）時，MSM允許您定義應如何（甚至是如果）處理它們。

為確保部署不被阻止，可能的定義可以包括：

* 在部署過程中，哪一頁（藍圖或即時拷貝）將優先，
* 將更名哪些頁面（以及如何更名）,
* 這會如何影響任何已發佈內容。

   (開箱AEM後)的預設行為是發佈的內容不會受到影響。 因此，如果在即時拷貝分支中手動建立的頁面已發佈，則在衝突處理和部署後，該內容仍將發佈。

除了標準功能外，還可以添加自定義衝突處理程式以實現不同的規則。 這也允許作為單個進程發佈操作。

### 示例方案 {#example-scenario}

在以下各節中，我們使用新頁面的示例 `b`，在藍圖和即時副本分支中建立（手動建立），以說明各種衝突解決方法：

* 藍圖： `/b`

   首頁；有1個子頁，bp-level-1

* 即時拷貝： `/b`

   在即時複製分支中手動建立的頁面；帶一個子頁面， `lc-level-1`。

   * 在發佈時激活為 `/b`，以及子頁面。

**推廣前**

<table>
 <tbody>
  <tr>
   <td><strong>展出前的藍圖</strong></td>
   <td><strong>在部署之前</strong></td>
   <td><strong>發佈前</strong></td>
  </tr>
  <tr>
   <td><code>b</code> <br /> (在藍圖分支中建立，準備部署<br /> </td>
   <td><code>b</code> <br /> （在即時拷貝分支中手動建立）<br /> </td>
   <td><code>b</code> <br /> （包含在即時拷貝分支中手動建立的頁b的內容）</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> （在即時拷貝分支中手動建立）<br /> </td>
   <td><code> /lc-level-1</code> <br /> (包含頁面內容<br /> 在即時拷貝分支中手動建立的子級1)</td>
  </tr>
 </tbody>
</table>

## 部署管理器和衝突處理 {#rollout-manager-and-conflict-handling}

部署管理器允許您激活或停用衝突管理。

這是使用 [OSGi配置](/help/sites-deploying/configuring-osgi.md) 共 **第CQ WCM推出管理器**:

* **處理與手動建立的頁面的衝突**:

   ( `rolloutmgr.conflicthandling.enabled`)

   如果部署管理器應處理在即時副本中建立的頁面中的衝突，並且該頁面的名稱在藍圖中存在，則設定為true。

AEM [衝突管理停用時的預定義行為](#behavior-when-conflict-handling-deactivated)。

## 衝突處理程式 {#conflict-handlers}

使AEM用衝突處理程式解決將內容從藍圖導出到即時副本時存在的任何頁面衝突。 更名頁面是解決此類衝突的一種常用方法。 可以操作多個衝突處理程式，以允許選擇不同的行為。

AEM提供：

* 的 [預設衝突處理程式](#default-conflict-handler):

   * `ResourceNameRolloutConflictHandler`

* 執行 [自定義處理程式](#customized-handlers)。
* 允許您設定每個處理程式的優先順序的服務分級機制。 使用排名最高的服務。

### 預設衝突處理程式 {#default-conflict-handler}

預設衝突處理程式：

* 調用 `ResourceNameRolloutConflictHandler`

* 使用此處理程式，將優先顯示藍圖頁。
* 此處理程式的服務等級設定為低(「低於 `service.ranking` 屬性)，因為假定自定義處理程式需要更高的等級。 但是，排名並非確保必要時靈活性的絕對最小值。

此衝突處理程式優先於藍圖。 即時複製頁 `/b` 將（在即時拷貝分支內）移動到 `/b_msm_moved`。

* 即時拷貝： `/b`

   將（在即時拷貝內）移動到 `/b_msm_moved`。 這將充當備份，並確保不會丟失任何內容。

   * `lc-level-1` 的子菜單。

* 藍圖： `/b`

   已展開到即時副本頁面 `/b`。

   * `bp-level-1` 被卷到livecopy中。

**推出後**

<table>
 <tbody>
  <tr>
   <td><strong>展出後的藍圖</strong></td>
   <td><strong>部署後的即時拷貝</strong><br /> </td>
   <td></td>
   <td><strong>部署後的即時拷貝</strong><br /> <br /> <br /> </td>
   <td><strong>發佈後</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> （具有已展開的藍圖頁b的內容）<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code> <br /> （具有在即時拷貝分支中手動建立的頁面b的內容）</td>
   <td><code>b</code> <br /> （無變動）包含在即時拷貝分支中手動建立的原始頁b的內容，現在稱為b_msm_moved)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code class="code"> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> （無更改）</td>
   <td><code> </code></td>
   <td><code> /lc-level-1</code> <br /> （無更改）</td>
  </tr>
 </tbody>
</table>

### 自定義處理程式 {#customized-handlers}

自定義衝突處理程式允許您實施自己的規則。 使用服務排名機制，您還可以定義它們如何與其他處理程式交互。

自定義衝突處理程式可以：

* 根據你的要求命名。
* 根據您的要求開發/配置；例如，可以開發處理程式，以便優先處理即時副本頁。
* 可設計為使用 [OSGi配置](/help/sites-deploying/configuring-osgi.md);特別是：

   * **服務排名**:

      定義與其他衝突處理程式相關的順序( `service.ranking`)。

      預設值為 0。

### 衝突處理已停用時的行為 {#behavior-when-conflict-handling-deactivated}

如果手動 [停用衝突處理](#rollout-manager-and-conflict-handling) 然AEM後對任何衝突頁面不採取任何操作（非衝突頁面按預期展開）。

>[!CAUTION]
>
>不AEM會指示衝突正在被忽略，因為必須顯式配置此行為，因此假定這是必需的行為。

在這種情況下，即時拷貝實際上優先。 藍圖頁 `/b` 未複製，且即時複製頁 `/b` 保持原狀。

* 藍圖： `/b`

   完全未複製，但被忽略。

* 即時拷貝： `/b`

   保持原樣。

<table>
 <caption>
   推出後
 </caption>
 <tbody>
  <tr>
   <td><strong>展出後的藍圖</strong></td>
   <td><strong>部署後的即時拷貝</strong><br /> <br /> <br /> </td>
   <td><strong>發佈後</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> （無變動）具有在即時拷貝分支中手動建立的頁面b的內容)</td>
   <td><code>b</code> <br /> （無變動）包含在即時拷貝分支中手動建立的頁面b的內容)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code> </td>
   <td><code> /lc-level-1</code> <br /> （無更改）</td>
   <td><code> /lc-level-1</code> <br /> （無更改）</td>
  </tr>
 </tbody>
</table>

### 服務排名 {#service-rankings}

的 [OSGi](https://www.osgi.org/) 服務排名可用於定義單個衝突處理程式的優先順序。
