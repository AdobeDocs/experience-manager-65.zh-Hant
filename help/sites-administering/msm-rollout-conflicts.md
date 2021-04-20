---
title: MSM推出衝突
seo-title: MSM推出衝突
description: 瞭解如何處理Multi Site Manager的推出衝突。
seo-description: 瞭解如何處理Multi Site Manager的推出衝突。
uuid: 7a640905-aae2-498e-b95c-2c73008fa1cd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 16db5334-604f-44e2-9993-10d683dee5bb
feature: Multi Site Manager
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 0%

---


# MSM Ploot Conflicts{#msm-rollout-conflicts}

如果在Blueprint分支和相依即時副本分支中建立具有相同頁面名稱的新頁面，則可能會發生衝突。

這些衝突需要在推出時處理並解決。

## 衝突處理{#conflict-handling}

當衝突頁面確實存在時（在Blueprint和即時副本分支中）,MSM可讓您定義應如何處理（甚至是如果）這些頁面。

為確保轉出未遭封鎖，可能的定義可包括：

* 首次推出時，哪個頁面（藍圖或即時副本）會優先，
* 將重新命名哪些頁面（以及如何重新命名）,
* 這會如何影響任何發佈的內容。

   預設行為(現AEM成可用)是發佈的內容不會受到影響。 因此，如果在即時副本分支中手動建立的頁面已發佈，該內容仍會在衝突處理和轉出後發佈。

除了標準功能外，還可新增自訂的衝突處理常式，以實作不同的規則。 這些動作也可以允許以個別程式進行發佈動作。

### 藍本{#example-scenario}示例

在以下幾節中，我們使用在Blueprint和即時副本分支（手動建立）中建立的新頁面`b`的示例來說明各種衝突解決方法：

* 藍圖：`/b`

   首頁；1頁，bp-level-1

* 即時副本：`/b`

   在即時副本分支中手動建立的頁面；包含1個子頁面，`lc-level-1`。

   * 在發佈時以`/b`和子頁面一起啟動。

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
   <td><code> /lc-level-1</code> <br /> （包含在即時副本分支中手動建立的page<br /> child-level-1的內容）</td>
  </tr>
 </tbody>
</table>

## 轉出管理器和衝突處理{#rollout-manager-and-conflict-handling}

轉出管理員可讓您啟用或停用衝突管理。

這是使用[**Day CQ WCM Pollout Manager**&#x200B;的OSGi配置](/help/sites-deploying/configuring-osgi.md)完成的：

* **使用手動建立的頁面處理衝突**:

   (`rolloutmgr.conflicthandling.enabled`)

   如果轉出管理員應處理來自即時副本中建立且名稱存在於藍圖的頁面的衝突，則設為true。

已停AEM用衝突管理時具有[預先定義的行為](#behavior-when-conflict-handling-deactivated)。

## 衝突處理程式{#conflict-handlers}

使AEM用衝突處理常式來解決從Blueprint將內容發佈至即時副本時存在的任何頁面衝突。 重新命名頁面是解決此類衝突的一種（通常）方法。 可以操作多個衝突處理程式以允許選擇不同的行為。

AEM提供：

* [預設衝突處理程式](#default-conflict-handler):

   * `ResourceNameRolloutConflictHandler`

* 實施[自訂處理常式](#customized-handlers)的可能性。
* 允許您設定每個單獨處理程式的優先順序的服務排名機制。 使用排名最高的服務。

### 預設衝突處理程式{#default-conflict-handler}

預設衝突處理程式：

* 稱為`ResourceNameRolloutConflictHandler`

* 使用此處理常式時，Blueprint頁面會優先。
* 此處理常式的服務排名設定為低(即在`service.ranking`屬性的預設值之下)，因為自訂處理常式需要較高的排名。 不過，排名並非確保必要時靈活性的絕對最小值。

此衝突處理常式優先於Blueprint。 即時副本頁面`/b`會移動（在即時副本分支內）至`/b_msm_moved`。

* 即時副本：`/b`

   移至（在即時副本內）`/b_msm_moved`。 這可當成備份，並確保不會遺失任何內容。

   * `lc-level-1` 未移動。

* 藍圖：`/b`

   已推出至即時副本頁面`/b`。

   * `bp-level-1` 會推出至livecopy。

**推出後**

<table>
 <tbody>
  <tr>
   <td><strong>推出後的藍圖</strong></td>
   <td><strong>轉出後即可使用拷貝</strong><br /> </td>
   <td></td>
   <td><strong>轉出後即可使用拷貝</strong><br /> <br /> <br /> </td>
   <td><strong>推出後發佈</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> （已推出藍圖頁面b的內容）<br /> </td>
   <td></td>
   <td><code>b_msm_moved</code> <br /> （具有在即時副本分支中手動建立的頁b的內容）</td>
   <td><code>b</code> <br /> （無變動）;包含在即時副本分支中手動建立的原始頁面b的內容，現在稱為b_msm_moved)<br /> </td>
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

### 自定義處理程式{#customized-handlers}

自訂的衝突處理常式可讓您實作自己的規則。 使用服務排名機制，您也可以定義它們與其他處理常式的互動方式。

自訂的衝突處理常式可以：

* 請根據您的需求命名。
* 根據您的需求進行開發／設定；例如，您可以開發處理常式，讓即時副本頁面優先。
* 可設計為使用[OSGi configuration](/help/sites-deploying/configuring-osgi.md)進行配置；特別是：

   * **服務排名**:

      定義與其他衝突處理程式(`service.ranking`)相關的順序。

      預設值為 0。

### 衝突處理停用{#behavior-when-conflict-handling-deactivated}時的行為

如果您手動[停用衝突處理](#rollout-manager-and-conflict-handling)，則AEM對任何衝突頁面不採取任何動作（非衝突頁面會如預期般推出）。

>[!CAUTION]
>
>不AEM會顯示衝突正在被忽略，因為必須明確配置此行為，因此假定這是必需行為。

在這種情況下，有效優先於即時副本。 Blueprint頁面`/b`不會被複製，而即時副本頁面`/b`則不受影響。

* 藍圖：`/b`

   完全不複製，但會被忽略。

* 即時副本：`/b`

   保持不變。

<table>
 <caption>
   推出後
 </caption>
 <tbody>
  <tr>
   <td><strong>推出後的藍圖</strong></td>
   <td><strong>轉出後即可使用拷貝</strong><br /> <br /> <br /> </td>
   <td><strong>推出後發佈</strong><br /> <br /> </td>
  </tr>
  <tr>
   <td><code>b</code></td>
   <td><code>b</code> <br /> （無變動）;具有在即時副本分支中手動建立的頁面b的內容)</td>
   <td><code>b</code> <br /> （無變動）;包含在即時副本分支中手動建立之頁面b的內容)<br /> </td>
  </tr>
  <tr>
   <td><code> /bp-level-1</code> </td>
   <td><code> /lc-level-1</code> <br /> （無變更）</td>
   <td><code> /lc-level-1</code> <br /> （無變更）</td>
  </tr>
 </tbody>
</table>

### 服務排名{#service-rankings}

[OSGi](https://www.osgi.org/)服務排名可用於定義單個衝突處理程式的優先順序。
