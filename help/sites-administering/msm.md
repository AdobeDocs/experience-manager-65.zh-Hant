---
title: 「重複使用內容：多站點管理員和即時副本」
seo-title: "Reusing Content: Multi Site Manager and Live Copy"
description: 了解如何使用Live Copy和Multi Site Manager來重複使用內容。
seo-description: Learn about reusing content with Live Copies and the Multi Site Manager.
uuid: 9f955226-8fc9-4357-b90c-c6896b0dc4b4
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: c21debc3-ecf4-4aa9-ab5a-18ddd5cf2fff
exl-id: 1e839845-fb5c-4200-8ec5-6ff744a96943
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2664'
ht-degree: 0%

---

# 重複使用內容：多網站管理員和即時副本{#reusing-content-multi-site-manager-and-live-copy}

Multi Site Manager(MSM)可讓您在多個位置中使用相同的網站內容。 MSM使用其Live Copy功能來達成此目標：

* 透過MSM，您可以：

   * 先建立內容一次
   * 將此內容複製到其他區域，並在其他區域中重複使用此內容([即時副本](#live-copies))或其他網站。

* 然後MSM會維護來源內容與其即時副本之間的（即時）關係，以便：

   * 當您對來源內容進行變更時，會同步來源和即時副本（以便將這些變更套用至即時副本）。
   * 您可以中斷個別子頁面和/或元件的即時關係，借此調整即時副本的內容。 如此一來，對來源的變更將不再套用至即時副本。

本頁及以下各頁涵蓋相關問題：

* [建立和同步Live Copy](/help/sites-administering/msm-livecopy.md)
* [Live Copy概述主控台](/help/sites-administering/msm-livecopy-overview.md)
* [配置Live Copy同步](/help/sites-administering/msm-sync.md)
* [MSM轉出衝突](/help/sites-administering/msm-rollout-conflicts.md)
* [MSM最佳實務](/help/sites-administering/msm-best-practices.md)

## 可能的情況 {#possible-scenarios}

MSM和Live Copy有許多使用案例，部分案例包括：

* **跨國公司 — 全球到本地公司**

   MSM支援的一個典型使用案例是在多個跨國相同語言網站中重複使用內容。 這可讓核心內容重複使用，同時允許國家變數。

   例如，We.Retail參考網站範例的英文區段是為美國客戶建立的。 此網站中的大部分內容也可用於其他We.Retail網站，以迎合不同國家和文化中講英語的客戶。 所有網站的核心內容都保持不變，而且可進行地區調整。

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
   >MSM不會翻譯內容。 它可用來建立所需的結構並部署內容。
   >
   >
   >請參閱 [轉譯多語言網站的內容](/help/sites-administering/translation.md) 如果您想要延伸此範例。

* **國家 — 總部至區域分部**

   或者，擁有經銷商網路的公司可能希望為各自的經銷商建立不同的網站 — 每個網站都是總部提供的主要網站的變體。 這可能適用於擁有多個地區辦事處的單一公司，或由中央特許經營者和多個地方特許經營者組成的全國特許經營系統。

   總辦事處可提供核心資訊，而區域實體可添加當地資訊，如聯繫詳情、開業時間和活動。

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
   >反對：
   >
   >  * 需要調整多少個單個副本。


## 從UI進行MSM {#msm-from-the-ui}

您可透過適當控制台的各種選項，直接在UI中存取MSM。 要介紹以下內容，請列出主要位置：

* **建立網站** (**網站**)

   * MSM可協助您管理多個共用相同內容的網站；例如，網站通常為國際受眾提供，因此大部分內容在所有國家/地區都是共有的，而且每個國家/地區都有特定內容的子集。 MSM可讓您 [建立即時副本，以根據您的來源網站自動更新一或多個網站](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). 這也可協助您強制建立通用的基礎結構、跨多個網站使用通用內容、維持通用的外觀和風格，並著重於管理實際上不同網站的內容。
   * 需要預先定義的Blueprint配置來指定源。
   * 建立（預先定義）來源的即時副本。
   * 為使用者提供 **轉出** 按鈕。

* **建立即時副本** (**網站**)

   * MSM可讓您 [建立網站個別頁面或子分支的臨機（一次性）即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page);例如，複製子分支以提供關於產品的新版本/更新版本的資訊。
   * 建立隨選即時副本（不需要Blueprint設定）。
   * 可用來（立即）建立任何頁面/分支的即時副本。
   * 需要 **同步** (不提供 **轉出** 按鈕)。

* **檢視屬性** (**網站**)

   * 如果適合，此選項可協助您 [監視即時副本](/help/sites-administering/msm-livecopy.md#monitoring-your-live-copy) 提供有關 **Live Cop** y或 **Blueprint**.

* **參考** (**網站**)

   * 此 [參考](/help/sites-authoring/basic-handling.md#references) 邊欄提供關於 **Live Copies** 以及適當動作的存取權。

* **即時副本概述** (**網站**)

   * 此主控台可讓您 [檢視和管理您的blueprint及其Live Copy](/help/sites-administering/msm-livecopy-overview.md).

* **藍圖** (**工具** - **網站**)

   * 此主控台可讓您 [建立和管理Blueprint配置](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration).

>[!NOTE]
>
>MSM功能的某些方面用於數個其他AEM功能（例如啟動、目錄）;在這些情況下，即時副本是由該功能管理。

### 使用的詞語 {#terms-used}

作為導言，下表概述與MSM搭配使用之主要術語；以下各節及頁面將提供更多詳細資訊：

<table>
 <tbody>
  <tr>
   <td><strong>詞彙</strong></td>
   <td><strong>定義</strong></td>
   <td><strong>更多詳情</strong></td>
  </tr>
  <tr>
   <td><strong>來源</strong></td>
   <td>原始頁面。</td>
   <td>與「藍圖」和/或「藍圖」頁面同義。</td>
  </tr>
  <tr>
   <td><strong>即時副本</strong></td>
   <td>由同步動作維護的復本（來源的），如轉出設定所定義。 </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Live Copy設定</strong></td>
   <td>即時副本的設定詳細資訊定義。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>即時關係</strong><br /> </td>
   <td>對給定資源的繼承的有效定義；源副本和Live Copy之間的連接。<br /> </td>
   <td>確保對源的更改可以與即時副本同步。</td>
  </tr>
  <tr>
   <td><strong>Blueprint</strong></td>
   <td>與源同義。</td>
   <td>可由Blueprint設定定義。</td>
  </tr>
  <tr>
   <td><strong>Blueprint設定</strong></td>
   <td>指定源路徑的預定義配置。</td>
   <td>當Blueprint設定中參考Blueprint頁面時，「轉出」命令即可使用。</td>
  </tr>
  <tr>
   <td><strong>同步</strong></td>
   <td>在來源和即時副本之間同步內容的通用術語（由兩者同時使用） <strong>轉出</strong> 和 <strong>同步</strong>)。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>轉出</strong><br /> </td>
   <td>從來源同步至LiveCopy。<br /> 可由作者（在Blueprint頁面上）或系統事件（由轉出設定定義）觸發。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>轉出設定</strong></td>
   <td>決定要同步哪些屬性、同步方式和同步時間的規則。</td>
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
   <td><strong>擱置</strong></td>
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
    </ul> <p>重置會影響您對頁面屬性、段落系統和元件所做的任何更改。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>淺</strong></td>
   <td>單一頁面的即時副本。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>深入</strong></td>
   <td>頁面的即時副本及其子頁面。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>請參閱 [Java API概觀](/help/sites-developing/extending-msm.md#overview-of-the-java-api) 對象名稱。

## 即時副本 {#live-copies}

MSM即時副本是特定網站內容的復本，其與原始來源的即時關係會維持：

* 即時副本會從其來源繼承內容。
* 當對源進行更改時，同步執行實際內容傳輸。
* 即時副本可視為：

   * 淺：單頁
   * 深：頁面及其子頁面

* 同步規則（稱為轉出設定）可決定要同步的屬性，以及同步發生的時間。

在上一個範例中， `/content/we-retail/language-masters/en` 是全域的英文主網站。 若要重複使用此網站的內容，會建立MSM即時復本：

* 以下內容 `/content/we-retail/language-masters/en` 是來源。

* 以下內容 `/content/we-retail/language-masters/en` 複製到 `/content/we-retail/us/en/`, `/content/we-retail/gb/en`, `/content/we-retail/ca/en`，和 `/content/we-retail/au/en` 節點。 這些是即時副本。

* 作者對下列頁面進行變更 `/content/we-retail/language-masters/en`.
* 觸發時，MSM會將這些變更同步至即時副本。

### 即時副本 — 組成 {#live-copies-composition}

>[!NOTE]
>
>本節中的圖表和說明表示潛在Live Copy的快照。 這些功能並非完整，但會提供概覽以強調特定特性。

最初建立即時副本時，所選源頁面會以1:1的方式反映在即時副本中。 之後，新資源（頁面和/或段落）也可直接在即時副本中建立，因此請務必注意這些變異及其對同步的影響，這是相當實用的。 可能的組合物包括：

* [包含非Live-Copy頁面的Live Copy](#live-copy-with-non-live-copy-pages)
* [巢狀即時副本](#nested-live-copies)

即時副本的基本形式有：

* 以1:1為基礎反映所選來源頁面的即時副本頁面。
* 一個配置定義。
* 為每個資源定義的即時關係：

   * 將即時副本資源與其Blueprint/來源連結。
   * 用於實現繼承和轉出。

* 變更可以是 [已同步](/help/sites-administering/msm-livecopy.md#synchronizing-your-live-copy) 根據要求。

![chlimage_1-367](assets/chlimage_1-367.png)

#### 包含非Live-Copy頁面的Live Copy {#live-copy-with-non-live-copy-pages}

當您在AEM中建立即時副本時，可以查看並導覽即時副本分支，並在即時副本分支上使用一般的AEM功能。 這表示您（或程式）可以在即時副本分支內建立新資源（頁面和/或段落）(例如 `myCanadaOnlyProduct`)。

* 這些資源與來源/Blueprint頁面沒有即時關係，且不會同步。
* MSM可能會以特殊情況處理的情況。 例如，當您（或程式）在來源/藍圖和即時副本分支中建立位置和名稱相同的頁面時。 若是這種情況，請參閱 [MSM轉出衝突](/help/sites-administering/msm-rollout-conflicts.md) 以取得更多資訊。

![chlimage_1-368](assets/chlimage_1-368.png)

#### 巢狀即時副本 {#nested-live-copies}

當您（或程式）建立 [現有即時副本中的新頁面](#live-copy-with-non-live-copy-pages) 此新頁面也可設為不同Blueprint的即時副本。 這稱為巢狀即時副本，其中第二個（內部）即時副本的行為會以下列方式受第一個（外部）即時副本影響：

* 頂層即時副本觸發的深層轉出可繼續進入巢狀即時副本（例如，如果觸發器符合）。
* 來源之間的任何連結將會在即時副本中重寫。

   例如，從第二個到第一個Blueprint的連結將重寫為從巢狀/第二個Live Copy到第一個Live Copy的連結。

![chlimage_1-369](assets/chlimage_1-369.png)

>[!NOTE]
>
>如果您在即時副本分支內移動/重新命名頁面，則（內部）會將其視為巢狀即時副本，以讓AEM追蹤關係。

#### 堆疊即時副本 {#stacked-live-copies}

即時副本建立為淺層即時副本的子項時，即稱為堆疊即時副本。 其行為方式與 [巢狀即時副本](#nested-live-copies).

### 源、藍圖和藍圖配置 {#source-blueprints-and-blueprint-configurations}

任何頁面或頁面的分支皆可作為即時副本的來源。

不過，MSM也可讓您定義Blueprint設定，以指定來源路徑。 使用Blueprint配置的好處是：

* 允許作者使用 **轉出** blueprint上的選項 — 將修改推送（明確）至繼承自此blueprint的即時副本。
* 允許作者使用 **建立網站**;這可讓使用者輕鬆選取語言並設定即時副本的結構。
* 為與Blueprint有關係的Live Copy定義預設轉出設定。

即時副本的來源可以是一般頁面或Blueprint設定涵蓋的頁面，這兩種皆為有效的使用案例。

來源會形成即時副本的藍圖。 當您執行下列任一動作時，就會定義Blueprint:

* [建立Blueprint設定](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration)

   設定會預先定義要用來建立即時副本的頁面。

* [建立頁面的即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   用來建立即時副本的頁面（來源頁面）為Blueprint頁面。

   來源頁面可由Blueprint設定參照，否則。

### 轉出與同步 {#rollout-and-synchronize}

轉出是中央MSM動作，會與其來源同步即時副本。 您可以手動執行轉出，也可以自動執行：

* A [轉出設定](#rollout-configurations) 可定義為 [事件](/help/sites-administering/msm-sync.md#rollout-triggers) 會導致自動轉出。
* 編寫Blueprint頁面時，您可以使用 [轉出](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) 命令將變更推送至即時副本。

   **轉出** 命令可在blueprint配置引用的blueprint頁面上使用。

   ![chlimage_1-370](assets/chlimage_1-370.png)

* 製作即時副本頁面時，您可以使用 [同步](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) 命令將更改從源提取到即時副本。

   此 **同步** 「即時副本」頁面上一律可使用命令（無論來源/blueprint頁面是否包含在blueprint設定中）。

   ![chlimage_1-371](assets/chlimage_1-371.png)

### 轉出設定 {#rollout-configurations}

轉出設定會定義即時副本與來源內容同步的時間和方式。 轉出設定包含觸發器和一或多個同步動作：

* **觸發器**

   觸發器是導致即時動作同步發生的事件，例如啟動來源頁面。 MSM會定義您可使用的觸發器。

* **同步操作**

   會在即時副本上執行，以便與來源同步。 範例動作包括複製內容、排序子節點以及啟動即時副本頁面。 MSM提供一些同步動作。

   >[!NOTE]
   >
   >您可以使用Java API建立執行個體的自訂動作。

轉出設定可重新使用，因此多個即時副本可以使用相同的轉出設定。 數個 [轉出設定](/help/sites-administering/msm-sync.md#installed-rollout-configurations) 包含在標準安裝中。

### 轉出衝突 {#rollout-conflicts}

轉出可能會變得複雜，尤其是當作者同時編輯來源和即時副本中的內容時，因此請務必注意AEM如何處理任何內容 [轉出期間可能發生的衝突](/help/sites-administering/msm-rollout-conflicts.md).

### 掛起和取消繼承和同步 {#suspending-and-cancelling-inheritance-and-synchronization}

即時副本中的每個頁面和元件都會透過即時關係與其來源頁面和元件相關聯。 即時關係配置來源中即時副本內容的同步。

您可以 **暫停** 即時副本頁面的即時副本繼承，以便您可以變更頁面屬性和元件。 暫停繼承時，頁面屬性和元件不再與源同步。

編輯個別頁面時，作者可 **取消繼承** （元件）。 取消繼承時，即時關係會暫停，且該元件不會同步。 當需要自訂內容的子區段時，取消繼承和同步很實用。

### 分離即時副本 {#detaching-a-live-copy}

您也可以 [分離即時副本](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) 從其藍圖中刪除所有連接。

>[!CAUTION]
>
>「分離」(Detach)操作是永久的且不可逆的。

「分離」會永久移除即時副本與其Blueprint頁面之間的即時關係。 所有與MSM相關的屬性會從Live Copy中移除，而Live Copy頁面會變成獨立Copy。

>[!NOTE]
>
>請參閱 [分離即時副本](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) 詳細資訊；包括對子頁面和上層頁面的相關影響。

## 使用MSM的標準步驟 {#standard-steps-for-using-msm}

下列步驟說明使用MSM來重複使用內容及同步即時副本變更的標準程式。

1. 開發來源網站的內容。
1. 決定要使用的轉出設定。

   1. MSM [安裝數項轉出設定](/help/sites-administering/msm-sync.md#installed-rollout-configurations) 可滿足許多使用案例。
   1. （可選）您可以 [建立轉出設定](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) （如果需要）。

1. 決定您需要的位置 [指定要使用的轉出設定](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use) 並視需要進行設定。
1. 如果需要， [建立blueprint設定](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration) 識別即時副本的來源內容。
1. [建立即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy).
1. 視需要變更來源內容。 您應採用貴組織已建立的一般內容審核和核准程式。
1. [轉出](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) 藍圖，或 [同步即時副本](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) 和變更。

## 自訂MSM {#customizing-msm}

MSM提供工具，讓您的實作能因應共用內容時可能存在的異常複雜情況：

* **自訂轉出設定**
   [建立轉出設定](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) 安裝的轉出設定不符合您的需求時。 您可以使用任何可用的轉出觸發器和同步動作。

* **自訂同步動作**
   [建立自訂同步動作](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action) 當安裝的操作不符合您的特定應用程式要求時。 MSM提供用於建立自訂同步動作的Java API。

## 最佳作法 {#best-practices}

此 [MSM最佳實務](/help/sites-administering/msm-best-practices.md) 頁面包含與您的實作相關的重要資訊。
