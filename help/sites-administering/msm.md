---
title: "重複使用內容：多網站管理員和 Live Copy"
seo-title: "Reusing Content: Multi Site Manager and Live Copy"
description: 瞭解如何使用即時副本和多站點管理器重新使用內容。
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

多站點管理器(MSM)使您能夠在多個位置使用相同的站點內容。 MSM使用其Live Copy功能實現以下目標：

* 有了 MSM，您可以：

   * 建立內容一次，然後
   * 將此內容複製到其他區域，並在其中重新使用此內容([即時拷貝](#live-copies))。

* 然後，MSM將維護源內容與其即時副本之間的（即時）關係，以便：

   * 當您對源內容進行更改時，源副本和即時副本將同步（以將這些更改也應用到即時副本）。
   * 通過斷開單個子頁面和/或元件的即時關係，可以對即時副本的內容進行調整。 通過執行此操作，對源的更改將不再應用於即時副本。

本頁及以下各頁介紹相關問題：

* [建立和同步 Live Copy](/help/sites-administering/msm-livecopy.md)
* [Live Copy 概觀主控台](/help/sites-administering/msm-livecopy-overview.md)
* [設定 Live Copy 同步](/help/sites-administering/msm-sync.md)
* [MSM 推出衝突](/help/sites-administering/msm-rollout-conflicts.md)
* [MSM 最佳做法](/help/sites-administering/msm-best-practices.md)

## 可能的案例 {#possible-scenarios}

MSM和即時拷貝有許多使用情形，有些情形包括：

* **跨國公司 - 全球公司到本地公司**

   MSM 支援的典型使用案例是在多個跨國同語言網站中重複使用內容。這允許核心內容被重新使用，同時允許國家變化。

   例如，We.Retail參考網站示例的英文部分是為美國客戶建立的。 此網站中的大部分內容也可用於其他We.Retail網站，這些網站面向不同國家和文化中講英語的客戶。 所有網站的核心內容都保持不變，但可以進行區域性調整。

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
   >請參閱 [翻譯多語言站點的內容](/help/sites-administering/translation.md) 如果想擴展這樣的示例。

* **全國 - 總公司到地區分公司**

   或者，擁有經銷商網路的公司可能希望為各自的經銷商建立單獨的網站 — 每個網站都是總部提供的主要網站的變體。 這可能適用於擁有多個區域辦公室的單一公司，或由特許加盟總部和多個地方加盟店組成的全國特許加盟系統。

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
   >在這種情況下，總是存在是製作直接拷貝還是使用即時拷貝的問題。
   >
   >有一個平衡：
   >
   >  * 多少核心內容需要通過多個版本進行更新。
   >
   >對比：
   >
   >  * 需要調整多少個副本。


## 從 UI 存取 MSM {#msm-from-the-ui}

MSM 可以使用相關主控台的各種選項直接在 UI 中存取 MSM。要提供簡介，請列出主要位置：

* **建立網站**(**Sites**)

   * MSM可幫助您管理多個共用公共內容的網站；例如，網站通常為國際受眾提供，因此大多數內容在所有國家都是共有的，而每個國家都有特定內容的子集。 MSM允許您 [建立基於源站點自動更新一個或多個站點的即時拷貝](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)。 這也有助於您強制施行共同的基本結構，在多個網站中使用共同內容，保持共同外觀，並集中心力管理實際在網站之間不同的內容。
   * 需要預先定義的藍圖設定以指定來源。
   * 建立（預定義）源的即時副本。
   * 為使用者提供&#x200B;**推出**&#x200B;按鈕。

* **建立 Live Copy** (**Sites**)

   * MSM允許您 [建立網站單個頁面或子分支的即席（一次性）即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page);例如，複製子分支以提供有關產品的新/更新版本的資訊。
   * 建立即席即時拷貝（不需要藍圖配置）。
   * 可用於（立即）建立任何頁/分支的即時副本。
   * 需要&#x200B;**同步** (不提供&#x200B;**推出**&#x200B;按鈕)。

* **檢視屬性** (**Sites**)

   * 在適當情況下，此選項可幫助您 [監視即時拷貝](/help/sites-administering/msm-livecopy.md#monitoring-your-live-copy) 提供有關 **《現場警察》** y或 **藍圖**。

* **參考** (**Sites**)

   * [參考](/help/sites-authoring/basic-handling.md#references)邊欄提供關於 **Live Copy** 的資訊以及對適當動作的存取。

* **Live Copy 概觀** (**Sites**)

   * 此控制台允許您 [查看和管理您的藍圖及其即時副本](/help/sites-administering/msm-livecopy-overview.md)。

* **藍圖**(**工具** - **Sites**)

   * 此控制台允許您 [建立和管理藍圖配置](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration)。

>[!NOTE]
>
>MSM功能的方面用於其AEM它幾個功能（例如啟動、目錄）;在這些情況下，即時拷貝由該功能管理。

### 使用的術語 {#terms-used}

作為導言，下表概述了MSM使用的主要術語；以下章節和頁面將詳細介紹這些內容：

<table>
 <tbody>
  <tr>
   <td><strong>術語</strong></td>
   <td><strong>定義</strong></td>
   <td><strong>更多詳細資訊</strong></td>
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
   <td>即時副本的配置詳細資訊的定義。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>即時關係</strong><br /> </td>
   <td>對給定資源的繼承進行有效定義；源副本和即時副本之間的連接。<br /> </td>
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
   <td>用於在源副本和即時副本之間同步內容的通用術語（由兩者同時使用） <strong>推廣</strong> 和 <strong>同步</strong>)。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>推出</strong><br /> </td>
   <td>從源同步到livecopy。<br /> 可以由作者（在藍圖頁面上）或系統事件（由部署配置定義）觸發。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>推出設定</strong></td>
   <td>決定哪些屬性將被同步、如何同步以及何時同步的規則.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>同步</strong></td>
   <td>從livecopy頁面發出的手動同步請求。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>繼承</strong></td>
   <td>當同步發生時，即時拷貝頁/元件從其源頁/元件繼承內容。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>暫停</strong></td>
   <td>臨時刪除即時副本與其藍圖頁面之間的即時關係。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>分離</strong></td>
   <td>永久刪除即時副本與其藍圖頁面之間的即時關係。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>重設</strong></td>
   <td><p>將即時複製頁重置為：</p>
    <ul>
     <li>刪除所有繼承取消和<br /> </li>
     <li>將頁面返回到與源頁面相同的狀態。</li>
    </ul> <p>重設會影響您對頁面屬性、段落系統和元件所做的任何變更。</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>淺層</strong></td>
   <td>單頁的即時副本。</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>深層</strong></td>
   <td>頁面及其子頁面的即時副本。</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>請參閱 [Java API概述](/help/sites-developing/extending-msm.md#overview-of-the-java-api) 的子菜單。

## Live Copy {#live-copies}

MSM即時拷貝是與原始源保持即時關係的特定站點內容的拷貝：

* 即時拷貝從其源繼承內容。
* 當對來源進行變更時，同步功能會實際傳輸內容。
* 即時拷貝可以視為：

   * 淺層：單一頁面
   * 深層：頁面及其子頁面

* 同步規則（稱為轉出配置）可確定要同步的屬性以及同步發生的時間。

在前面的範例中，`/content/we-retail/language-masters/en` 是全球主要英語網站。要重用此站點的內容，將建立MSM即時拷貝：

* `/content/we-retail/language-masters/en` 下面的內容是來源。

* 以下內容 `/content/we-retail/language-masters/en` 複製到 `/content/we-retail/us/en/`。 `/content/we-retail/gb/en`。 `/content/we-retail/ca/en`, `/content/we-retail/au/en` 節點。 這些是現場拷貝。

* 作者對 `/content/we-retail/language-masters/en` 下面的頁面進行變更。
* 觸發時，MSM將這些更改同步到即時副本。

### Live Copy - 組成項目 {#live-copies-composition}

>[!NOTE]
>
>本節中的圖和說明表示潛在即時拷貝的快照。 提供的資訊並不全面，只是概要說明以強調特定的特性。

初始建立即時副本時，所選源頁面將以1:1的基準反映在即時副本中。 此後，也可以直接在即時拷貝中建立新資源（頁面和/或段落），因此瞭解這些變化以及它們如何影響同步非常有用。 可能的組成項目包括：

* [含非 Live Copy 頁面的 Live Copy](#live-copy-with-non-live-copy-pages)
* [巢狀 Live Copy](#nested-live-copies)

即時拷貝的基本形式有：

* 即時複製頁面，以1:1為基礎反映所選源頁面。
* 一個設定定義。
* 為每個資源定義的即時關係：

   * 將即時拷貝資源與其藍圖/源連結。
   * 實現繼承和推出時使用。

* 變更可以根據需要[同步](/help/sites-administering/msm-livecopy.md#synchronizing-your-live-copy)。

![chlimage_1-367](assets/chlimage_1-367.png)

#### 含非 Live Copy 頁面的 Live Copy {#live-copy-with-non-live-copy-pages}

在中建立即時拷貝時，AEM您可以查看並瀏覽即時拷貝分支，並在即時拷貝分支AEM上使用常規功能。 這意味著您（或流程）可以在即時複製分支內建立新資源（頁面和/或段落）(例如 `myCanadaOnlyProduct`)。

* 這類資源與來源/藍圖頁面沒有即時關係，並且不同步。
* 可能會發生 MSM 作為特殊案例處理的情況。例如，當您（或進程）在源/藍圖和即時複製分支中建立位置和名稱相同的頁面時。 對於此類情況，請參閱 [MSM 推出衝突](/help/sites-administering/msm-rollout-conflicts.md)了解更多資訊。

![chlimage_1-368](assets/chlimage_1-368.png)

#### 巢狀 Live Copy {#nested-live-copies}

建立 [現有即時拷貝中的新頁面](#live-copy-with-non-live-copy-pages) 此新頁面也可以設定為不同藍圖的即時副本。 這稱為「嵌套即時拷貝」，其中第二個（內部）即時拷貝的行為受第一個（外部）即時拷貝的影響方式如下：

* 為頂級即時副本觸發的深度部署可以繼續到嵌套的即時副本中（例如，如果觸發器匹配）。
* 源之間的任何連結都將在即時副本中重寫。

   例如，從第二個到第一個藍圖的連結將被重寫為從嵌套的/第二個即時拷貝到第一個即時拷貝的連結。

![chlimage_1-369](assets/chlimage_1-369.png)

>[!NOTE]
>
>如果在即時複製分支中移動/更名頁面，則（內部）該頁面將被視為嵌套的即時複製，以便AEM跟蹤關係。

#### 堆疊 Live Copy {#stacked-live-copies}

當作為淺即時副本的子級建立即時副本時，該副本稱為「堆疊即時副本」。 它的行為方式與 [嵌套即時複製](#nested-live-copies)。

### 來源、藍圖和藍圖設定 {#source-blueprints-and-blueprint-configurations}

任何頁面或頁面分支都可用作即時副本的源。

然而，MSM 也可讓您定義會指定來源路徑的藍圖設定。使用藍圖設定的好處是它們：

* 允許作者使用 **推廣** 中的選項 — 將修改推送到從此藍圖繼承的活動副本。
* 允許作者使用 **建立站點**;這允許用戶輕鬆選擇語言並配置即時副本的結構。
* 為與藍圖有關的即時副本定義預設的部署配置。

即時副本的源可以是藍圖配置包含的常規頁面或頁面 — 這兩種情況都是有效的使用案例。

源將構成即時副本的藍圖。 當您執行以下任一操作時，藍圖即已定義：

* [建立藍圖配置](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration)

   配置預先定義了用於建立即時副本的頁面。

* [建立頁面的即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   用於建立即時副本（源頁）的頁是藍圖頁。

   源頁面可以由藍圖配置引用，也可以不引用。

### 推出和同步 {#rollout-and-synchronize}

部署是使即時拷貝與其源同步的中央MSM操作。 您可以手動執行部署，也可以自動執行：

* 可以定義[推出設定](#rollout-configurations)，以便特定的[事件](/help/sites-administering/msm-sync.md#rollout-triggers)可以促使推出自動發生。
* 建立藍圖頁面時，可以使用 [推廣](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) 命令將更改推送到即時副本。

   **可在藍圖設定所參考的藍圖頁面上使用推出**&#x200B;命令。

   ![chlimage_1-370](assets/chlimage_1-370.png)

* 創作即時拷貝頁面時，您可以使用 [同步](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) 命令將更改從源拉入即時副本。

   的 **同步** 命令始終可在即時拷貝頁上使用（無論源/藍圖頁是否包含在藍圖配置中）。

   ![chlimage_1-371](assets/chlimage_1-371.png)

### 推出設定 {#rollout-configurations}

部署配置定義即時拷貝與源內容同步的時間和方式。 推出設定由觸發器和一個或多個同步動作組成：

* **觸發器**

   觸發器是導致即時操作同步發生的事件，例如激活源頁。 MSM 定義了您可以使用的觸發器。

* **同步操作**

   在即時副本上執行，以將其與源同步。 示例操作包括複製內容、訂購子節點和激活即時複製頁。 MSM提供許多同步操作。

   >[!NOTE]
   >
   >您可以使用 Java API. 為您的執行個體建立自訂動作。

可以重新使用部署配置，以便多個即時拷貝可以使用相同的部署配置。 標準安裝中包含多個[推出設定](/help/sites-administering/msm-sync.md#installed-rollout-configurations)。

### 推出衝突 {#rollout-conflicts}

部署可能會變得複雜，尤其是當作者正在編輯源和即時拷貝中的內容時，因此瞭解如何處理任何內容是AEM很有用的 [在部署過程中可能發生的衝突](/help/sites-administering/msm-rollout-conflicts.md)。

### 暫停和取消繼承和同步 {#suspending-and-cancelling-inheritance-and-synchronization}

即時副本中的每個頁面和元件通過即時關係與其源頁面和元件相關聯。 即時關係配置來自源的即時拷貝內容的同步。

你可以 **掛起** 即時複製頁的即時複製繼承，以便您可以更改頁面屬性和元件。 當您暫停繼承時，頁面屬性和元件將不再與來源同步。

在編輯個別頁面時，作者可以為元件&#x200B;**取消繼承**。取消繼承後，即時關係會暫停，該元件將不會進行同步。當需要自訂內容的子部分時，取消繼承和同步很有用。

### 分離 Live Copy {#detaching-a-live-copy}

您也可以 [分離即時副本](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) 從藍圖中移除所有連接。

>[!CAUTION]
>
>分離動作是永久性且無法復原。

「分離」永久刪除即時副本與其藍圖頁面之間的即時關係。 所有與MSM相關的屬性都從即時拷貝中刪除，而即時拷貝頁面則變成獨立拷貝。

>[!NOTE]
>
>請參閱 [分離即時副本](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) 詳細資訊；包括對子及母頁的相關影響。

## MSM 標準使用步驟 {#standard-steps-for-using-msm}

以下步驟介紹了使用MSM重用內容並將更改同步到即時副本的標準過程。

1. 開發源網站的內容。
1. 決定要使用的推出設定。

   1. MSM [安裝了多個推出設定](/help/sites-administering/msm-sync.md#installed-rollout-configurations)，可滿足多種使用案例。
   1. 如果需要，您可以選擇[建立推出設定](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration)。

1. 決定您需要在哪裡[指定要使用的推出設定](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use)，並根據需要進行設定。
1. 如果需要， [建立藍圖配置](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration) 標識即時副本的源內容。
1. [建立即時副本](/help/sites-administering/msm-livecopy.md#creating-a-live-copy)。
1. 根據需要變更來源內容。您應該採用您組織已建立的一般內容審查和核准流程。
1. [展開](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) 藍圖，或者 [同步即時拷貝](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) 和更改。

## 自訂 MSM {#customizing-msm}

MSM提供了各種工具，以便您的實施能夠適應共用內容時可能存在的異常複雜性：

* **自定義部署配置**
   [建立部署配置](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) 安裝的部署配置不符合您的要求時。 您可以使用任何可用的推出觸發器和同步動作。

* **自定義同步操作**
   [建立自定義同步操作](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action) 安裝的操作不符合您的特定應用程式要求時。 MSM提供用於建立自定義同步操作的Java API。

## 最佳做法 {#best-practices}

[MSM 最佳做法](/help/sites-administering/msm-best-practices.md)頁面包含與您的實作相關的重要資訊。
