---
title: "重複使用內容：多網站管理員和 Live Copy"
seo-title: "Reusing Content: Multi Site Manager and Live Copy"
description: 了解如何使用Live Copy和Multi Site Manager來重複使用內容。
seo-description: Learn about reusing content with Live Copies and the Multi Site Manager.
uuid: 9f955226-8fc9-4357-b90c-c6896b0dc4b4
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: c21debc3-ecf4-4aa9-ab5a-18ddd5cf2fff
exl-id: 1e839845-fb5c-4200-8ec5-6ff744a96943
source-git-commit: 53c39e4aa250b18d4fae0327b313b18901677f2c
workflow-type: tm+mt
source-wordcount: '2664'
ht-degree: 31%

---

# 重複使用內容：多網站管理員和 Live Copy{#reusing-content-multi-site-manager-and-live-copy}

Multi Site Manager(MSM)可讓您在多個位置中使用相同的網站內容。 MSM使用其Live Copy功能來達成此目標：

* 有了 MSM，您可以：

   * 建立內容一次，然後
   * 將此內容複製到其他區域，並在其他區域中重複使用此內容([即時副本](#live-copies))或其他網站。

* 然後MSM會維護來源內容與其即時副本之間的（即時）關係，以便：

   * 當您對來源內容進行變更時，會同步來源和即時副本（以便將這些變更套用至即時副本）。
   * 您可以中斷個別子頁面和/或元件的即時關係，借此調整即時副本的內容。 如此一來，對來源的變更將不再套用至即時副本。

本頁及以下各頁涵蓋相關問題：

* [建立和同步 Live Copy](/help/sites-administering/msm-livecopy.md)
* [Live Copy 概觀主控台](/help/sites-administering/msm-livecopy-overview.md)
* [設定 Live Copy 同步](/help/sites-administering/msm-sync.md)
* [MSM 推出衝突](/help/sites-administering/msm-rollout-conflicts.md)
* [MSM 最佳做法](/help/sites-administering/msm-best-practices.md)

## 可能的案例 {#possible-scenarios}

MSM和Live Copy有許多使用案例，部分案例包括：

* **跨國公司 - 全球公司到本地公司**

   MSM 支援的典型使用案例是在多個跨國同語言網站中重複使用內容。這可讓核心內容重複使用，同時允許國家變數。

   例如，We.Retail參考網站範例的英文區段是為美國客戶建立的。 此網站中的大部分內容也可用於其他We.Retail網站，以迎合不同國家和文化中講英語的客戶。 所有網站的核心內容都保持不變，但可以進行區域性調整。

   以下結構可用於美國、英國、加拿大和澳大利亞的場地：

   ```xml
   /content
       |- we.retail
           |- language-masters
               |- en
       |- we.retail
           |- us
               |- en
       |- we.retail
           |- gb
               |- en
       |- we.retail
           |- ca
               |- en
       |- we.retail
           |- au
               |- en
   ```

   >[!NOTE]
   >
   >MSM 不翻譯內容。它用於建立所需結構和部署內容。
   >
   >
   >請參閱 [轉譯多語言網站的內容](/help/sites-administering/translation.md) 如果您想要延伸此範例。

* **全國 - 總公司到地區分公司**

   或者，擁有經銷商網路的公司可能希望為各自的經銷商建立不同的網站 — 每個網站都是總部提供的主要網站的變體。 這可能適用於擁有多個區域辦公室的單一公司，或由特許加盟總部和多個地方加盟店組成的全國特許加盟系統。

   總公司可以提供核心資訊，而區域實體可以加入當地資訊，例如聯絡方式、營業時間和活動。

   ```xml
   /content
       |- head-office-Berlin
       |- branch-Hamburg
       |- branch-Stuttgart
       |- branch-Munich
       |- branch-Frankfurt
   ```

* **多個版本**

   或者，您可以使用MSM建立特定子分支的版本。例如，支援子站點保存特定產品不同版本的詳細資訊，其中基本資訊保持不變，只需更改更新的功能：

   ```xml
   /content
       |- support
           |- product X
               |- v5.0
               |- v4.0
               |- v3.0
               |- v2.0
               |- v1.0
   ```

   >[!NOTE]
   >
   >在這種情況下，始終存在以下問題：是製作簡單的副本還是使用即時副本。
   >
   >平衡如下：
   >
   >  * 多個版本需要更新多少核心內容。
   >
   >對比：
   >
   >  * 需要調整多少個單個副本。


## 從 UI 存取 MSM {#msm-from-the-ui}

MSM 可以使用相關主控台的各種選項直接在 UI 中存取 MSM。要介紹以下內容，請列出主要位置：

* **建立網站**(**Sites**)

   * MSM可協助您管理多個共用相同內容的網站；例如，網站通常為國際受眾提供，因此大部分內容在所有國家/地區都是共有的，而且每個國家/地區都有特定內容的子集。 MSM可讓您 [建立即時副本，以根據您的來源網站自動更新一或多個網站](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). 這也有助於您強制施行共同的基本結構，在多個網站中使用共同內容，保持共同外觀，並集中心力管理實際在網站之間不同的內容。
   * 需要預先定義的藍圖設定以指定來源。
   * 建立（預先定義）來源的即時副本。
   * 為使用者提供&#x200B;**推出**&#x200B;按鈕。

* **建立 Live Copy** (**Sites**)

   * MSM可讓您 [建立網站個別頁面或子分支的臨機（一次性）即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page);例如，複製子分支以提供關於產品的新版本/更新版本的資訊。
   * 建立隨選即時副本（不需要Blueprint設定）。
   * 可用來（立即）建立任何頁面/分支的即時副本。
   * 需要&#x200B;**同步** (不提供&#x200B;**推出**&#x200B;按鈕)。

* **檢視屬性** (**Sites**)

   * 如果適合，此選項可協助您 [監視即時副本](/help/sites-administering/msm-livecopy.md#monitoring-your-live-copy) 提供有關 **Live Cop** y或 **Blueprint**.

* **參考** (**Sites**)

   * [參考](/help/sites-authoring/basic-handling.md#references)邊欄提供關於 **Live Copy** 的資訊以及對適當動作的存取。

* **Live Copy 概觀** (**Sites**)

   * 此主控台可讓您 [檢視和管理您的blueprint及其Live Copy](/help/sites-administering/msm-livecopy-overview.md).

* **藍圖**(**工具** - **Sites**)

   * 此主控台可讓您 [建立和管理Blueprint配置](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration).

>[!NOTE]
>
>MSM功能的某些方面用於數個其他AEM功能（例如啟動、目錄）;在這些情況下，即時副本是由該功能管理。

### 使用的術語 {#terms-used}

作為導言，下表概述與MSM搭配使用之主要術語；以下各節及頁面將提供更多詳細資訊：

<table>
 <tbody>
  <tr>
   <td><strong>術語</strong></td>
   <td><strong>定義</strong></td>
   <td><strong>更多詳情</strong></td>
  </tr>
  <tr>
   <td><strong>來源</strong></td>
   <td>原始頁面。</td>
   <td>與藍圖和/或藍圖頁是同義字.</td>
  </tr>
  <tr>
   <td><strong>Live Copy</strong></td>
   <td>(來源的) 副本，由推出設定定義的同步動作進行維護. </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Live Copy 設定</strong></td>
   <td>即時副本的設定詳細資訊定義。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>即時關係</strong><br /> </td>
   <td>對給定資源的繼承的有效定義；源副本和Live Copy之間的連接。<br /> </td>
   <td>確保對源的更改可以與即時副本同步。</td>
  </tr>
  <tr>
   <td><strong>藍圖</strong></td>
   <td>與來源是同義字.</td>
   <td>可以由藍圖設定來定義.</td>
  </tr>
  <tr>
   <td><strong>藍圖設定</strong></td>
   <td>指定源路徑的預先定義設定.</td>
   <td>在藍圖設定中有參考藍圖頁面時，推出命令即可使用.</td>
  </tr>
  <tr>
   <td><strong>同步</strong></td>
   <td>在來源和即時副本之間同步內容的通用術語（由兩者同時使用） <strong>轉出</strong> 和 <strong>同步</strong>)。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>推出</strong><br /> </td>
   <td>從來源同步至LiveCopy。<br /> 可由作者（在Blueprint頁面上）或系統事件（由轉出設定定義）觸發。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>推出設定</strong></td>
   <td>決定哪些屬性將被同步、如何同步以及何時同步的規則.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>同步</strong></td>
   <td>從LiveCopy頁面進行的手動同步請求。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>繼承</strong></td>
   <td>即時副本頁面/元件會在同步發生時從其來源頁面/元件繼承內容。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>暫停</strong></td>
   <td>暫時移除即時副本與其Blueprint頁面之間的即時關係。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>分離</strong></td>
   <td>永久移除即時副本與其Blueprint頁面之間的即時關係。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>重設</strong></td>
   <td><p>將即時副本頁面重設為：</p>
    <ul>
     <li>刪除所有繼承取消和<br /> </li>
     <li>將頁面傳回與來源頁面相同的狀態。</li>
    </ul> <p>重設會影響您對頁面屬性、段落系統和元件所做的任何變更。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>淺層</strong></td>
   <td>單一頁面的即時副本。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>深層</strong></td>
   <td>頁面的即時副本及其子頁面。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>請參閱 [Java API概觀](/help/sites-developing/extending-msm.md#overview-of-the-java-api) 對象名稱。

## Live Copy {#live-copies}

MSM即時副本是特定網站內容的復本，其與原始來源的即時關係會維持：

* 即時副本會從其來源繼承內容。
* 當對來源進行變更時，同步功能會實際傳輸內容。
* 即時副本可視為：

   * 淺層：單一頁面
   * 深層：頁面及其子頁面

* 同步規則（稱為轉出設定）可決定要同步的屬性，以及同步發生的時間。

在前面的範例中，`/content/we-retail/language-masters/en` 是全球主要英語網站。若要重複使用此網站的內容，會建立MSM即時復本：

* `/content/we-retail/language-masters/en` 下面的內容是來源。

* 以下內容 `/content/we-retail/language-masters/en` 複製到 `/content/we-retail/us/en/`, `/content/we-retail/gb/en`, `/content/we-retail/ca/en`，和 `/content/we-retail/au/en` 節點。 這些是即時副本。

* 作者對 `/content/we-retail/language-masters/en` 下面的頁面進行變更。
* 觸發時，MSM會將這些變更同步至即時副本。

### Live Copy - 組成項目 {#live-copies-composition}

>[!NOTE]
>
>本節中的圖表和說明表示潛在Live Copy的快照。 提供的資訊並不全面，只是概要說明以強調特定的特性。

最初建立即時副本時，所選源頁面會以1:1的方式反映在即時副本中。 之後，新資源（頁面和/或段落）也可直接在即時副本中建立，因此請務必注意這些變異及其對同步的影響，這是相當實用的。 可能的組成項目包括：

* [含非 Live Copy 頁面的 Live Copy](#live-copy-with-non-live-copy-pages)
* [巢狀 Live Copy](#nested-live-copies)

即時副本的基本形式有：

* 以1:1為基礎反映所選來源頁面的即時副本頁面。
* 一個設定定義。
* 為每個資源定義的即時關係：

   * 將即時副本資源與其Blueprint/來源連結。
   * 實現繼承和推出時使用。

* 變更可以根據需要[同步](/help/sites-administering/msm-livecopy.md#synchronizing-your-live-copy)。

![chlimage_1-367](assets/chlimage_1-367.png)

#### 含非 Live Copy 頁面的 Live Copy {#live-copy-with-non-live-copy-pages}

當您在AEM中建立即時副本時，可以查看並導覽即時副本分支，並在即時副本分支上使用一般的AEM功能。 這表示您（或程式）可以在即時副本分支內建立新資源（頁面和/或段落）(例如 `myCanadaOnlyProduct`)。

* 這類資源與來源/藍圖頁面沒有即時關係，並且不同步。
* 可能會發生 MSM 作為特殊案例處理的情況。例如，當您（或程式）在來源/藍圖和即時副本分支中建立位置和名稱相同的頁面時。 對於此類情況，請參閱 [MSM 推出衝突](/help/sites-administering/msm-rollout-conflicts.md)了解更多資訊。

![chlimage_1-368](assets/chlimage_1-368.png)

#### 巢狀 Live Copy {#nested-live-copies}

當您（或程式）建立 [現有即時副本中的新頁面](#live-copy-with-non-live-copy-pages) 此新頁面也可設為不同Blueprint的即時副本。 這稱為巢狀即時副本，其中第二個（內部）即時副本的行為會以下列方式受第一個（外部）即時副本影響：

* 頂層即時副本觸發的深層轉出可繼續進入巢狀即時副本（例如，如果觸發器符合）。
* 來源之間的任何連結將會在即時副本中重寫。

   例如，從第二個到第一個Blueprint的連結將重寫為從巢狀/第二個Live Copy到第一個Live Copy的連結。

![chlimage_1-369](assets/chlimage_1-369.png)

>[!NOTE]
>
>如果您在即時副本分支內移動/重新命名頁面，則（內部）會將其視為巢狀即時副本，以讓AEM追蹤關係。

#### 堆疊 Live Copy {#stacked-live-copies}

即時副本建立為淺層即時副本的子項時，即稱為堆疊即時副本。 其行為方式與 [巢狀即時副本](#nested-live-copies).

### 來源、藍圖和藍圖設定 {#source-blueprints-and-blueprint-configurations}

任何頁面或頁面的分支皆可作為即時副本的來源。

然而，MSM 也可讓您定義會指定來源路徑的藍圖設定。使用藍圖設定的好處是它們：

* 允許作者使用 **轉出** blueprint上的選項 — 將修改推送（明確）至繼承自此blueprint的即時副本。
* 允許作者使用 **建立網站**;這可讓使用者輕鬆選取語言並設定即時副本的結構。
* 為與Blueprint有關係的Live Copy定義預設轉出設定。

即時副本的來源可以是一般頁面或Blueprint設定涵蓋的頁面，這兩種皆為有效的使用案例。

來源會形成即時副本的藍圖。 當您執行以下任一操作時，藍圖即已定義：

* [建立Blueprint設定](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration)

   設定會預先定義要用來建立即時副本的頁面。

* [建立頁面的即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   用來建立即時副本的頁面（來源頁面）為Blueprint頁面。

   來源頁面可由Blueprint設定參照，否則。

### 推出和同步 {#rollout-and-synchronize}

轉出是中央MSM動作，會與其來源同步即時副本。 您可以手動執行轉出，也可以自動執行：

* 可以定義[推出設定](#rollout-configurations)，以便特定的[事件](/help/sites-administering/msm-sync.md#rollout-triggers)可以促使推出自動發生。
* 編寫Blueprint頁面時，您可以使用 [轉出](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) 命令將變更推送至即時副本。

   **可在藍圖設定所參考的藍圖頁面上使用推出**&#x200B;命令。

   ![chlimage_1-370](assets/chlimage_1-370.png)

* 製作即時副本頁面時，您可以使用 [同步](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) 命令將更改從源提取到即時副本。

   此 **同步** 「即時副本」頁面上一律可使用命令（無論來源/blueprint頁面是否包含在blueprint設定中）。

   ![chlimage_1-371](assets/chlimage_1-371.png)

### 推出設定 {#rollout-configurations}

轉出設定會定義即時副本與來源內容同步的時間和方式。 推出設定由觸發器和一個或多個同步動作組成：

* **觸發器**

   觸發器是導致即時動作同步發生的事件，例如啟動來源頁面。 MSM 定義了您可以使用的觸發器。

* **同步操作**

   會在即時副本上執行，以便與來源同步。 範例動作包括複製內容、排序子節點以及啟動即時副本頁面。 MSM提供一些同步動作。

   >[!NOTE]
   >
   >您可以使用 Java API. 為您的執行個體建立自訂動作。

轉出設定可重新使用，因此多個即時副本可以使用相同的轉出設定。 標準安裝中包含多個[推出設定](/help/sites-administering/msm-sync.md#installed-rollout-configurations)。

### 推出衝突 {#rollout-conflicts}

轉出可能會變得複雜，尤其是當作者同時編輯來源和即時副本中的內容時，因此請務必注意AEM如何處理任何內容 [轉出期間可能發生的衝突](/help/sites-administering/msm-rollout-conflicts.md).

### 暫停和取消繼承和同步 {#suspending-and-cancelling-inheritance-and-synchronization}

即時副本中的每個頁面和元件都會透過即時關係與其來源頁面和元件相關聯。 即時關係配置來源中即時副本內容的同步。

您可以 **暫停** 即時副本頁面的即時副本繼承，以便您可以變更頁面屬性和元件。 當您暫停繼承時，頁面屬性和元件將不再與來源同步。

在編輯個別頁面時，作者可以為元件&#x200B;**取消繼承**。取消繼承後，即時關係會暫停，該元件將不會進行同步。當需要自訂內容的子部分時，取消繼承和同步很有用。

### 分離 Live Copy {#detaching-a-live-copy}

您也可以 [分離即時副本](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) 從其藍圖中刪除所有連接。

>[!CAUTION]
>
>分離動作是永久性且無法復原。

「分離」會永久移除即時副本與其Blueprint頁面之間的即時關係。 所有與MSM相關的屬性會從Live Copy中移除，而Live Copy頁面會變成獨立Copy。

>[!NOTE]
>
>請參閱 [分離即時副本](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) 詳細資訊；包括對子頁面和上層頁面的相關影響。

## MSM 標準使用步驟 {#standard-steps-for-using-msm}

下列步驟說明使用MSM來重複使用內容及同步即時副本變更的標準程式。

1. 開發源網站的內容。
1. 決定要使用的推出設定。

   1. MSM [安裝了多個推出設定](/help/sites-administering/msm-sync.md#installed-rollout-configurations)，可滿足多種使用案例。
   1. 如果需要，您可以選擇[建立推出設定](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration)。

1. 決定您需要在哪裡[指定要使用的推出設定](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use)，並根據需要進行設定。
1. 如果需要， [建立blueprint設定](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration) 識別即時副本的來源內容。
1. [建立即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy).
1. 根據需要變更來源內容。您應該採用您組織已建立的一般內容審查和核准流程。
1. [轉出](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) 藍圖，或 [同步即時副本](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) 和變更。

## 自訂 MSM {#customizing-msm}

MSM提供工具，讓您的實作能因應共用內容時可能存在的異常複雜情況：

* **自訂轉出設定**
   [建立轉出設定](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) 安裝的轉出設定不符合您的需求時。 您可以使用任何可用的推出觸發器和同步動作。

* **自訂同步動作**
   [建立自訂同步動作](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action) 當安裝的操作不符合您的特定應用程式要求時。 MSM提供用於建立自訂同步動作的Java API。

## 最佳做法 {#best-practices}

[MSM 最佳做法](/help/sites-administering/msm-best-practices.md)頁面包含與您的實作相關的重要資訊。
