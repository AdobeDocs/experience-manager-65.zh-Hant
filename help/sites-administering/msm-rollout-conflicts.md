---
title: MSM轉出衝突
seo-title: MSM Rollout Conflicts
description: 了解如何處理多網站管理員轉出衝突。
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
ht-degree: 0%

---

# MSM轉出衝突{#msm-rollout-conflicts}

如果在Blueprint分支和相依的即時副本分支中建立了具有相同頁面名稱的新頁面，則可能會發生衝突。

這類衝突需要在推出時處理和解決。

## 衝突處理 {#conflict-handling}

當發生衝突的頁面確實存在時（在Blueprint和Live Copy分支中）,MSM可讓您定義應如何（甚至是）處理這些頁面。

為確保轉出未遭到封鎖，可能的定義可能包括：

* 轉出期間哪個頁面（blueprint或即時副本）會具有優先順序，
* 將重新命名哪些頁面（以及如何）,
* 這會如何影響任何已發佈的內容。

   AEM的預設行為（現成）是已發佈內容將不會受到影響。 因此，如果發佈了在即時副本分支中手動建立的頁面，該內容在衝突處理和轉出後仍會發佈。

除了標準功能外，還可以添加自定義衝突處理程式以實施不同的規則。 這些也可允許以個別程式發佈動作。

### 範例案例 {#example-scenario}

在以下幾節中，我們使用新頁面的範例 `b`，在blueprint和live copy分支中建立（手動建立），以說明各種衝突解決方法：

* blueprint: `/b`

   主版頁面；1個子頁，bp-level-1

* 即時副本： `/b`

   在即時副本分支中手動建立的頁面；包含1個子頁面， `lc-level-1`.

   * 發佈時啟動為 `/b`，連同子頁面。

**轉出前**

<table>
 <tbody>
  <tr>
   <td><strong>開始使用的Blueprint</strong></td>
   <td><strong>轉出前的即時副本</strong></td>
   <td><strong>轉出前發佈</strong></td>
  </tr>
  <tr>
   <td><code>b</code> <br /> （在blueprint分支中建立，可轉出）<br /> </td>
   <td><code>b</code> <br /> （在即時副本分支中手動建立）<br /> </td>
   <td><code>b</code> <br /> （包含在即時副本分支中手動建立之頁面b的內容）</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code> <br /> （在即時副本分支中手動建立）<br /> </td>
   <td><code> /lc-level-1</code> <br /> (包含頁面的內容<br /> child-level-1，在即時副本分支中手動建立)</td>
  </tr>
 </tbody>
</table>

## 轉出管理員和衝突處理 {#rollout-manager-and-conflict-handling}

轉出管理器可讓您啟用或停用衝突管理。

這是使用 [OSGi配置](/help/sites-deploying/configuring-osgi.md) of **Day CQ WCM轉出管理器**:

* **使用手動建立的頁面處理衝突**:

   ( `rolloutmgr.conflicthandling.enabled`)

   如果轉出管理器應處理來自即時副本中建立之頁面的衝突，且該頁面的名稱存在於Blueprint中，則設為true。

AEM [停用衝突管理時的預先定義行為](#behavior-when-conflict-handling-deactivated).

## 衝突處理程式 {#conflict-handlers}

AEM使用衝突處理常式來解決從Blueprint將內容轉出至Live Copy時存在的任何頁面衝突。 更名頁面是解決此類衝突的一種（通常）方法。 可以操作多個衝突處理程式以允許選擇不同的行為。

AEM提供：

* 此 [預設衝突處理程式](#default-conflict-handler):

   * `ResourceNameRolloutConflictHandler`

* 實施 [自訂處理常式](#customized-handlers).
* 允許您設定每個個別處理常式之優先順序的服務排名機制。 會使用排名最高的服務。

### 預設衝突處理程式 {#default-conflict-handler}

預設衝突處理程式：

* 呼叫 `ResourceNameRolloutConflictHandler`

* 使用此處理常式時，Blueprint頁面會優先。
* 此處理常式的服務排名設為低(即低於 `service.ranking` 屬性)，因為自訂處理常式需要較高的排名。 然而，排名並非確保必要時靈活性的絕對最小值。

此衝突處理程式優先於Blueprint。 即時副本頁面 `/b` 會移至（在即時副本分支內） `/b_msm_moved`.

* 即時副本： `/b`

   會移動（在即時副本內）至 `/b_msm_moved`. 這可作為備份，並確保不會遺失任何內容。

   * `lc-level-1` 未移動。

* blueprint: `/b`

   已推出至即時副本頁面 `/b`.

   * `bp-level-1` 會轉出至livecopy。

**轉出後**

<table>
 <tbody>
  <tr>
   <td><strong>轉出後的blueprint</strong></td>
   <td><strong>轉出後的即時副本</strong><br /> </td>
   <td></td>
   <td><strong>轉出後的即時副本</strong><br /> <br /> <br /> </td>
   <td><strong>轉出後發佈</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> （具有已推出的blueprint頁面b的內容）<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code> <br /> （具有在即時副本分支中手動建立之頁面b的內容）</td>
   <td><code>b</code> <br /> （無變化）;包含在即時副本分支中手動建立的原始頁面b的內容，現在稱為b_msm_moved)<br /> </td>
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

### 自訂處理常式 {#customized-handlers}

自定義的衝突處理程式允許您實施自己的規則。 使用服務排名機制，您也可以定義它們與其他處理常式的互動方式。

自定義衝突處理程式可以：

* 根據你的要求命名。
* 根據您的需求開發/配置；例如，您可以開發處理常式，讓即時副本頁面優先。
* 可設計為使用 [OSGi配置](/help/sites-deploying/configuring-osgi.md);尤其是：

   * **服務排名**:

      定義與其他衝突處理程式( `service.ranking`)。

      預設值為 0。

### 停用衝突處理時的行為 {#behavior-when-conflict-handling-deactivated}

如果您手動 [停用衝突處理](#rollout-manager-and-conflict-handling) 然後，AEM不會對任何衝突頁面採取任何動作（非衝突頁面會如預期般推出）。

>[!CAUTION]
>
>AEM不會指出衝突正在遭到忽略，因為此行為必須明確設定，因此會假設這是必要行為。

在這種情況下，有效的即時副本優先。 Blueprint頁面 `/b` 不會複製，且Live Copy頁面不會複製 `/b` 未動。

* blueprint: `/b`

   完全不會複製，但會忽略。

* 即時副本： `/b`

   保持不變。

<table>
 <caption>
   轉出後
 </caption>
 <tbody>
  <tr>
   <td><strong>轉出後的blueprint</strong></td>
   <td><strong>轉出後的即時副本</strong><br /> <br /> <br /> </td>
   <td><strong>轉出後發佈</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> （無變化）;具有在即時副本分支中手動建立之頁面b的內容)</td>
   <td><code>b</code> <br /> （無變化）;包含在即時副本分支中手動建立之頁面b的內容)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code> </td>
   <td><code> /lc-level-1</code> <br /> （無更改）</td>
   <td><code> /lc-level-1</code> <br /> （無更改）</td>
  </tr>
 </tbody>
</table>

### 服務排名 {#service-rankings}

此 [OSGi](https://www.osgi.org/) 服務排名可用於定義單個衝突處理程式的優先順序。
