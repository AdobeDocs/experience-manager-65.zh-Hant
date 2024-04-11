---
title: MSM 推出衝突
description: 瞭解如何處理「多網站管理員」轉出衝突。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
feature: Multi Site Manager
exl-id: e145e79a-c363-4a33-b9f9-99502ed20563
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 1%

---

# MSM 推出衝突{#msm-rollout-conflicts}

如果在Blueprint分支和相依即時副本分支中同時建立具有相同頁面名稱的新頁面，則可能會發生衝突。

轉出時必須處理和解決此類衝突。

## 衝突處理 {#conflict-handling}

當Blueprint和即時副本分支中的頁面確實存在衝突時，MSM可讓您定義應如何（甚至是否）處理衝突。

為確保轉出不被封鎖，可能的定義可以包括：

* 轉出時哪個頁面（Blueprint或即時副本）優先，
* 哪些頁面會重新命名（以及重新命名方式），
* 這會如何影響任何已發佈的內容。

  Adobe Experience Manager (AEM) （現成可用）的預設行為是發佈內容不受影響。 因此，如果在即時副本分支中手動建立的頁面已發佈，該內容在衝突處理和轉出後仍會發佈。

除了標準功能外，您也可以新增自訂的衝突處理常式，以實作不同的規則。 這些功能也可以允許將動作發佈為個別程式。

### 範例情境 {#example-scenario}

在下列段落中，您必須使用新頁面的範例 `b`，同時在Blueprint和即時副本分支中建立（手動建立），以說明解決衝突的各種方法：

* Blueprint： `/b`

  主版頁面；具有一個子頁面bp-level-1。

* 即時副本： `/b`

  在即時副本分支中手動建立的頁面；具有一個子頁面、 `lc-level-1`.

   * 發佈時啟用為 `/b`，以及子頁面。

**轉出前**

<table>
 <tbody>
  <tr>
   <td><strong>轉出前的Blueprint</strong></td>
   <td><strong>轉出前的即時副本</strong></td>
   <td><strong>轉出前發佈</strong></td>
  </tr>
  <tr>
   <td><code>b</code><br /> <br /> （在Blueprint分支中建立，可準備轉出）<br /> </td>
   <td><code>b</code><br /> <br /> （在即時副本分支中手動建立）<br /> </td>
   <td><code>b</code><br /> <br /> （包含在即時副本分支中手動建立的頁面b內容）</td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code> /lc-level-1</code><br /> <br /> （在即時副本分支中手動建立）<br /> </td>
   <td><code> /lc-level-1</code><br /> <br /> （包含頁面的內容）<br /> child-level-1 （已在即時副本分支中手動建立）</td>
  </tr>
 </tbody>
</table>

## 轉出管理程式與衝突處理 {#rollout-manager-and-conflict-handling}

轉出管理員可讓您啟用或停用衝突管理。

這是使用來完成的 [OSGi設定](/help/sites-deploying/configuring-osgi.md) 之 **Day CQ WCM轉出管理員**：

* **處理與手動建立的頁面衝突**：

  ( `rolloutmgr.conflicthandling.enabled`)

  如果轉出管理員應處理在即時副本中建立的頁面與Blueprint中已存在的名稱之間的衝突，則設為true。

AEM具有 [已停用衝突管理時的預先定義行為](#behavior-when-conflict-handling-deactivated).

## 衝突處理常式 {#conflict-handlers}

AEM使用衝突處理常式，來解決將內容從Blueprint轉出至即時副本時存在的任何頁面衝突。 重新命名頁面是解決這類衝突的一種（一般）方法。 可以執行多個衝突處理常式，以允許選取不同的行為。

AEM提供：

* 此 [預設衝突處理常式](#default-conflict-handler)：

   * `ResourceNameRolloutConflictHandler`

* 實作 [自訂處理常式](#customized-handlers).
* 此服務排名機制可讓您設定每個個別處理常式的優先順序。 使用排名最高的服務。

### 預設衝突處理常式 {#default-conflict-handler}

預設衝突處理常式：

* 已呼叫 `ResourceNameRolloutConflictHandler`

* 使用此處理常式，Blueprint頁面會獲得優先權。
* 此處理常式的服務排名設定為低(即低於 `service.ranking` 屬性)，因為假設自訂處理常式需要較高的排名。 不過，排名並非在需要時確保彈性的絕對最低值。

此衝突處理常式會賦予Blueprint優先權。 即時副本頁面 `/b` （在即時副本分支中）移至 `/b_msm_moved`.

* 即時副本： `/b`

  移動（在即時副本中）至 `/b_msm_moved`. 這會作為備份，並確保不會遺失任何內容。

   * `lc-level-1` 不會移動。

* Blueprint： `/b`

  轉出到即時副本頁面 `/b`.

   * `bp-level-1` 轉出至即時副本。

**轉出後**

<table>
 <tbody>
  <tr>
   <td><strong>轉出後的Blueprint</strong></td>
   <td><strong>轉出後的即時副本</strong><br /> </td>
   <td></td>
   <td><strong>轉出後的即時副本</strong><br /> <br /> <br /> </td>
   <td><strong>轉出後發佈</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code><br /> <br /> （具有已轉出的blueprint頁面b的內容）<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code><br /> <br /> （具有在即時副本分支中手動建立的頁面b的內容）</td>
   <td><code>b</code><br /> <br /> （無變更；包含在即時副本分支中手動建立的原始頁面b的內容，現在稱為b_msm_moved）<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code></td>
   <td><code class="code"> /bp-level-1</code></td>
   <td><code> /lc-level-1</code><br /> <br /> （無變更）</td>
   <td><code> </code></td>
   <td><code> /lc-level-1</code><br /> <br /> （無變更）</td>
  </tr>
 </tbody>
</table>

### 自訂處理常式 {#customized-handlers}

自訂衝突處理常式可讓您實作自己的規則。 使用服務排名機制，您也可以定義它們如何與其他處理常式互動。

自訂的衝突處理常式可以有以下內容：

* 根據您的需求命名。
* 根據您的需求開發/設定；例如，您可以開發處理常式，好讓即時副本頁面獲得優先權。
* 設計為使用 [OSGi設定](/help/sites-deploying/configuring-osgi.md)；尤其是：

   * **服務排名**：

     定義與其他衝突處理常式相關的順序( `service.ranking`)。

     預設值為 0。

### 衝突處理停用時的行為 {#behavior-when-conflict-handling-deactivated}

如果您手動 [停用衝突處理](#rollout-manager-and-conflict-handling)，則AEM不會對任何衝突頁面採取任何動作（非衝突頁面會如預期般轉出）。

>[!CAUTION]
>
>AEM不會指出系統忽略衝突，因為此行為必須明確設定，因此我們假設這是必要的行為。

在此情況下，即時副本會有效取得優先權。 Blueprint頁面 `/b` 不會複製且即時副本頁面 `/b` 保持不變。

* Blueprint： `/b`

  完全不會複製，但會忽略。

* 即時副本： `/b`

  相同。

<table>
 <caption>
   轉出後
 </caption>
 <tbody>
  <tr>
   <td><strong>轉出後的Blueprint</strong></td>
   <td><strong>轉出後的即時副本</strong><br /> <br /> <br /> </td>
   <td><strong>轉出後發佈</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code><br /> <br /> （無變更；具有在即時副本分支中手動建立的頁面b的內容）</td>
   <td><code>b</code><br /> <br /> （無變更；包含在即時副本分支中手動建立的頁面b內容）<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code><br /> </td>
   <td><code> /lc-level-1</code><br /> <br /> （無變更）</td>
   <td><code> /lc-level-1</code><br /> <br /> （無變更）</td>
  </tr>
 </tbody>
</table>

### 服務排名 {#service-rankings}

此 [osgi](https://www.osgi.org/) 服務排名可用來定義個別衝突處理常式的優先順序。
