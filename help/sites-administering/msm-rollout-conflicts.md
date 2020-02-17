---
title: MSM推出衝突
seo-title: MSM推出衝突
description: 瞭解如何處理Multi Site manager的推出衝突。
seo-description: 瞭解如何處理Multi Site manager的推出衝突。
uuid: 7a640905-aae2-498e-b95c-2c73008fa1cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 16db5334-604f-44e2-9993-10d683dee5bb
translation-type: tm+mt
source-git-commit: 47b69098a45f774501ebb62ee1a14a8d209ad101

---


# MSM推出衝突{#msm-rollout-conflicts}

如果在Blueprint分支和相依即時副本分支中建立具有相同頁面名稱的新頁面，則可能會發生衝突。

這些衝突需要在推出時處理並解決。

## 衝突處理 {#conflict-handling}

當衝突頁面確實存在時（在Blueprint和即時副本分支中）,MSM可讓您定義應如何處理（甚至是如果）這些頁面。

為確保轉出未遭封鎖，可能的定義可包括：

* 首次推出時，哪個頁面（藍圖或即時副本）會優先，
* 將重新命名哪些頁面（以及如何重新命名）,
* 這會如何影響任何發佈的內容。

   AEM（現成可用）的預設行為是發佈的內容不會受到影響。 因此，如果在即時副本分支中手動建立的頁面已發佈，該內容仍會在衝突處理和轉出後發佈。

除了標準功能外，還可新增自訂的衝突處理常式，以實作不同的規則。 這些動作也可以允許以個別程式進行發佈動作。

### 範例藍本 {#example-scenario}

在以下幾節中，我們使用在Blueprint和即時副本分支（手動建立）中建立的新頁面示例來說明各種衝突解決方法： `b`

* blueprint: `/b`

   首頁；1頁，bp-level-1

* live copy: `/b`

   在即時副本分支中手動建立的頁面；包含1個子頁面， `lc-level-1`

   * 在發佈時與子頁 `/b`面一起啟動為。

**推出前**

<table>
 <tbody>
  <tr>
   <td><strong>展開之前的藍圖</strong></td>
   <td><strong>在轉存之前先使用拷貝</strong></td>
   <td><strong>發佈之前先發佈</strong></td>
  </tr>
  <tr>
   <td><code>b</code> <br /> （在Blueprint分支中建立，準備推出）<br /> </td>
   <td><code>b</code> <br /> （在即時副本分支中手動建立）<br /> </td>
   <td><code>b</code> <br /> （包含在即時副本分支中手動建立之頁面b的內容）</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> （在即時副本分支中手動建立）<br /> </td>
   <td><code> /lc-level-1</code> <br /> (包含在即時副本分支中<br /> ，手動建立之頁面child-level-1的內容)</td>
  </tr>
 </tbody>
</table>

## 轉出管理員與衝突處理 {#rollout-manager-and-conflict-handling}

轉出管理員可讓您啟用或停用衝突管理。

這是使用 [Day CQ](/help/sites-deploying/configuring-osgi.md) **WCM Rovolt Manager的OSGi配置完成的**:

* **使用手動建立的頁面處理衝突**:

   ( `rolloutmgr.conflicthandling.enabled`)

   如果轉出管理員應處理來自即時副本中建立且名稱存在於藍圖的頁面的衝突，則設為true。

當衝突管 [理已停用時，AEM已預先定義行為](#behavior-when-conflict-handling-deactivated)。

## 衝突處理程式 {#conflict-handlers}

AEM使用衝突處理常式來解決將內容從Blueprint轉出至即時副本時存在的任何頁面衝突。 重新命名頁面是解決此類衝突的一種（通常）方法。 可以操作多個衝突處理程式以允許選擇不同的行為。

AEM提供：

* 預設 [衝突處理程式](#default-conflict-handler):

   * `ResourceNameRolloutConflictHandler`

* 實作自訂處理常 [式的可能性](#customized-handlers)。
* 允許您設定每個單獨處理程式的優先順序的服務排名機制。 使用排名最高的服務。

### 預設衝突處理程式 {#default-conflict-handler}

預設衝突處理程式：

* 呼叫 `ResourceNameRolloutConflictHandler`

* 使用此處理常式時，Blueprint頁面會優先。
* 此處理常式的服務排名設定為低(即屬性的預設值), `service.ranking` 因為自訂處理常式需要較高的排名。 不過，排名並非確保必要時靈活性的絕對最小值。

此衝突處理常式優先於Blueprint。 即時副本頁 `/b` 面會移動（在即時副本分支內）至 `/b_msm_moved`。

* live copy: `/b`

   會移至（在即時副本中） `/b_msm_moved`。 這可當成備份，並確保不會遺失任何內容。

   * `lc-level-1` 未移動。

* blueprint: `/b`

   已推出至即時副本頁面 `/b`。

   * `bp-level-1` 會推出至livecopy。

**推出後**

<table>
 <tbody>
  <tr>
   <td><strong>推出後的藍圖</strong></td>
   <td><strong>轉出後即可使用拷貝</strong><br /> </td>
   <td></td>
   <td><strong>推出後即時複製</strong><br /><br /><br /> </td>
   <td><strong>轉出後發佈</strong><br /><br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> （已推出藍圖頁面b的內容）<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code> <br /> （具有在即時副本分支中手動建立的頁b的內容）</td>
   <td><code>b</code> <br /> (無變動；包含在即時副本分支中手動建立的原始頁面b的內容，現在稱為b_msm_moved)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code class="code"> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> （無變更）</td>
   <td><code> </code></td>
   <td><code> /lc-level-1</code> <br /> （無變更）</td>
  </tr>
 </tbody>
</table>

### 自訂處理常式 {#customized-handlers}

自訂的衝突處理常式可讓您實作自己的規則。 使用服務排名機制，您也可以定義它們與其他處理常式的互動方式。

自訂的衝突處理常式可以：

* 請根據您的需求命名。
* 根據您的需求進行開發／設定；例如，您可以開發處理常式，讓即時副本頁面優先。
* 可設計為使用 [OSGi配置進行配置](/help/sites-deploying/configuring-osgi.md);特別是：

   * **服務排名**:

      定義與其他衝突處理程式( `service.ranking`)相關的順序。

      預設值為0。

### 已停用衝突處理時的行為 {#behavior-when-conflict-handling-deactivated}

如果您手動 [停用衝突處理](#rollout-manager-and-conflict-handling) ,AEM不會對任何衝突頁面採取任何動作（非衝突頁面會如預期般推出）。

>[!CAUTION]
>
>AEM不會指出衝突正被忽略，因為必須明確設定此行為，因此會假設這是必要行為。

在這種情況下，有效優先於即時副本。 藍圖頁 `/b` 面不會複製，而即時副本頁 `/b` 面則保持不變。

* blueprint: `/b`

   完全不複製，但會被忽略。

* live copy: `/b`

   保持不變。

<table>
 <caption>
   推出後
 </caption>
 <tbody>
  <tr>
   <td><strong>推出後的藍圖</strong></td>
   <td><strong>推出後即時複製</strong><br /><br /><br /> </td>
   <td><strong>轉出後發佈</strong><br /><br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> (無變動；具有在即時副本分支中手動建立的頁面b的內容)</td>
   <td><code>b</code> <br /> (無變動；包含在即時副本分支中手動建立之頁面b的內容)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code> </td>
   <td><code> /lc-level-1</code> <br /> （無變更）</td>
   <td><code> /lc-level-1</code> <br /> （無變更）</td>
  </tr>
 </tbody>
</table>

### 服務排名 {#service-rankings}

OSGi [](https://www.osgi.org/) service排名可用來定義個別衝突處理常式的優先順序。
