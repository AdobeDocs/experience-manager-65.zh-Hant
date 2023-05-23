---
title: 預告和策略
seo-title: Teasers and Strategies
description: 活動往往利用茶具作為一種機制，通過關注遊客興趣的內容來吸引特定群體。 為特定市場活動定義一個或多個預告。
seo-description: Campaigns often use teasers as a mechanism to entice a specific segment of the visitor population through to content focused on their interests. One or more teasers are defined for a specific campaign.
uuid: c78ec858-4b0a-48d5-99b2-5ddd9e15183d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 7f378b94-5233-4358-8d93-a7b3386df00b
docset: aem65
exl-id: 27b8302c-250b-4ce6-b3cf-c938738f2d92
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 6%

---

# 預告和策略{#teasers-and-strategies}

活動往往利用茶具作為一種機制，通過關注遊客興趣的內容來吸引特定群體。 為特定市場活動定義一個或多個預告。

>[!NOTE]
>
>6.2中已棄用TeaserAEM元件。請使用 [目標元件](/help/sites-authoring/content-targeting-touch.md) 的雙曲餘切值。

* **品牌頁面** 儲存在網站的「市場活動」部分中。 一個品牌包含各個活動。
* **市場活動頁面** 儲存在網站的「市場活動」部分中。 每個市場活動都有一個單獨的頁面，在該頁面中保留預告定義。 容器（或概述）頁還包含與單個預告頁有關的某些資訊和統計資訊。

內部AEM茶具由幾部分組成：

* **預告頁** 儲存在相應的市場活動頁面下，並保存針對每個特定市場活動的預告段落的定義。 這些定義用於顯示預告段落；包括內容變化，用於選擇變化和提升因子的段。
* 的 **預偏器元件** 可用，允許您在內容頁面中建立特定預告段落的實例。 您可以將預告元件從側腳中拖動，然後指定預告定義以建立自己的預告段落。 **注：** 6.2中已棄用TeaserAEM元件。請使用 [目標元件](/help/sites-authoring/content-targeting-touch.md) 的雙曲餘切值。
* **預告段落** 是內容頁面中預告的實際實例。 這吸引了一部分遊客，讓他們專注於自己的興趣。
* 保存市場活動內容的頁面集中於特定訪問者段。 通常，「誘惑」段落會引導訪問者訪問此類頁面。

## 策略 {#strategies}

將預告段落添加到頁面時，需要定義 **策略**。

這是因為多個預告都成功解析，因此可供選擇。 的 **策略** 然後指定用於選擇顯示的預告的附加條件：

* **按一下流分數**，基於訪問者客戶端上下文中保存的標籤和相關標籤點擊（顯示訪問者在包含相應標籤的頁面上按一下的次數）。 比較在預告頁上定義的標籤的命中率。
* **隨機**，用於「隨機選擇」；使用為頁面生成的隨機因子，可以通過 [客戶端上下文](/help/sites-administering/client-context.md)。
* **第一個** 的下界。 訂單是市場活動容器頁面中的預告的訂單。

的 [提升因子](/help/sites-administering/campaign-segmentation.md#boost-factor) 對選擇也有影響。 這是添加到段定義中以增加/減少被選擇的相對可能性的加權因子。

通過示例最好地說明了各種選擇標準的過程和相互關係（還可以使用這種方法來確保您的預告將到達所需的受眾）。

如果已建立並分配了以下段各自的Boost Factor:

| 區段 | 提升因子 |
|---|---|
| S1 | 0 |
| S2 | 0 |
| S3 | 10 |
| S4 | 30 |
| S5 | 0 |
| S6 | 100 |

我們使用以下預告定義：

<table>
 <tbody>
  <tr>
   <td>行銷活動</td>
   <td>Teaser</td>
   <td>分配的段</td>
   <td>分配的標籤 </td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T1</td>
   <td>S1 、 S2</td>
   <td>業務、營銷</td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T2 </td>
   <td>S1</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T3</td>
   <td>S3、S4</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T4</td>
   <td>S2、S5</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T5</td>
   <td>S1 、 S2 、 S6</td>
   <td>營銷</td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T6</td>
   <td>S6</td>
   <td>商務<br /> </td>
  </tr>
 </tbody>
</table>

那麼，如果我們將此應用於訪問者：

* **S1**。 **S2** 和 **南6** 成功

* 標籤 **營銷** 有3次擊打
* 標籤 **業務** 有6次點擊

我們可以看到結果：

* 匹配成功 — 是否為當前訪問者成功解決分配給預告的任何段？
* boost factor — 所有適用分部中最高的boost factor
* clickstream score — 所有適用標籤命中的累計總數

策略前計算之公平值：

<table>
 <tbody>
  <tr>
   <td>行銷活動</td>
   <td>Teaser</td>
   <td>分配的段</td>
   <td>標記 </td>
   <td>成功匹配？</td>
   <td>產生的Boost因子</td>
   <td>生成的點擊流分數 </td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T1</td>
   <td>S1 、 S2</td>
   <td>業務、營銷</td>
   <td>是</td>
   <td>0</td>
   <td>9</td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T2 </td>
   <td>S1</td>
   <td><br /> </td>
   <td>是</td>
   <td>0</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T3</td>
   <td>S3、S4</td>
   <td><br /> </td>
   <td>否</td>
   <td><br /> </td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T4</td>
   <td>S2、S5</td>
   <td><br /> </td>
   <td>是<br /> </td>
   <td>0<br /> </td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T5</td>
   <td>S1 、 S2 、 S6</td>
   <td>營銷</td>
   <td>是</td>
   <td>100</td>
   <td>3</td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T6</td>
   <td>S6</td>
   <td>商務</td>
   <td>是</td>
   <td>100</td>
   <td>6 </td>
  </tr>
 </tbody>
</table>

根據 **策略** 項：

<table>
 <tbody>
  <tr>
   <td>策略</td>
   <td>產生的預告</td>
   <td>評論</td>
  </tr>
  <tr>
   <td>第一個</td>
   <td>T5</td>
   <td>只有T5和T6被視為它們的所有部分都已解決 <i>和</i> 他們的刺激因子最高。 返回的清單按T5、T6的順序；因此，T5被選中並顯示。</td>
  </tr>
  <tr>
   <td>隨機</td>
   <td>T5或T6</td>
   <td>兩個預衝器都具有全部解決的段和相同的促進因子。 因此，兩個預衝器按相同比例顯示。</td>
  </tr>
  <tr>
   <td>按一下流分數</td>
   <td>T6</td>
   <td><p>T1 、 T4 、 T5和T6的段都為訪問者解析。 T5和T6的升壓因子越高，T1和T4的升壓因子越低。 最後，T6的較高點擊流分數會導致選擇此項。</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>如果在上述解析度技術之後，有多個預告可供選擇，則內部選擇（隨機）將選擇單個預告供顯示。
>
>例如，如果策略是Clickstream Score，而T5的Clickstream Score與T6具有相同（即6而不是3），則內部選擇（隨機）將用於選擇這兩個策略之一。

「預告頁」/「段落」用於引導特定訪問者段落關注其興趣的內容。 它們可以為訪問者提供一系列選擇，或只顯示一個基於特定訪問者段落的預告段落；例如，所顯示的預告段落可能取決於訪問者的年齡。

通常，預告頁是臨時操作，將持續一段特定時間，直到被下一個預告頁替換為止。

在建立品牌和市場活動後，您可以建立和設定您的預告體驗。

### 為預告建立觸點 {#creating-a-touchpoint-for-your-teaser}

>[!NOTE]
>
>6.2中已棄用TeaserAEM元件。請使用 [目標元件](/help/sites-authoring/content-targeting-touch.md) 的雙曲餘切值。

1. 導航到要放置引導到市場活動頁面的預告段落的內容頁面。
1. 添加 **預告** 元件(在 **個性化** )。 首次建立時，它將顯示市場活動路徑尚未配置：

   ![chlimage_1](assets/chlimage_1.png)

1. 編輯預告元件以添加：

   * **市場活動路徑**
保存單個預告頁的市場活動頁的路徑；段確切地確定顯示哪種偏激。

   * **[策略](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#strategies)**
用於成功解析多個段時進行選擇的方法。
   ![chlimage_1-1](assets/chlimage_1-1.png)

1. 按一下 **確定** 來保存。 根據您在預告上設定的段和您當前登錄的用戶的概要資訊，將顯示相應的內容：

   ![chlimage_1-2](assets/chlimage_1-2.png)

1. 將滑鼠移到預告段落上，以顯示問號表徵圖（元件右下角）。 按一下此按鈕可查看所應用的段以及它們當前是否已解決。

   ![chlimage_1-3](assets/chlimage_1-3.png)

### 預告概述 {#teaser-overview}

除了MCM中的市場活動視圖外，市場活動頁面還提供了與其關聯的茶具的資訊：

1. 從 **網站** 控制台，開啟市場活動頁面；例如：

   `https://localhost:4502/content/campaigns/geometrixx-outdoors/storefront/summer.html`

   這顯示了預告定義和查看統計資訊的概述：

   ![chlimage_1-4](assets/chlimage_1-4.png)
