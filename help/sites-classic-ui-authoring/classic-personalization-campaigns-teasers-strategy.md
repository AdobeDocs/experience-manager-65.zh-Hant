---
title: Teaser和策略
description: 行銷活動經常使用Teaser做為吸引特定訪客群體進入專注於訪客興趣之內容的機制。 已為特定行銷活動定義一或多個Teaser。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 27b8302c-250b-4ce6-b3cf-c938738f2d92
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 3%

---

# Teaser和策略{#teasers-and-strategies}

行銷活動經常使用Teaser做為吸引特定訪客群體進入專注於訪客興趣之內容的機制。 已為特定行銷活動定義一或多個Teaser。

>[!NOTE]
>
>AEM 6.2已棄用Teaser元件。請改用 [目標元件](/help/sites-authoring/content-targeting-touch.md).

* **品牌頁面** 儲存在網站的「促銷活動」區段內。 品牌包含個別行銷活動。
* **行銷活動頁面** 儲存在網站的「促銷活動」區段內。 每個行銷活動都有個別頁面，這些頁面會保留Teaser定義。 容器或概觀頁面也包含有關個別Teaser頁面的某些資訊和統計資料。

AEM中的Teaser由幾個部分組成：

* **Teaser頁面** 儲存在適當的促銷活動頁面下，並儲存每個特定促銷活動可用的Teaser段落定義。 顯示Teaser段落時會使用這些定義，包括內容變數、用來選取變數和提升因子的區段。
* 此 **Teaser元件** 立即可用，並可讓您在內容頁面中建立特定Teaser段落的例項。 您可以從sidekick拖曳Teaser元件，然後指定Teaser定義以建立您自己的Teaser段落。 **注意：** AEM 6.2已棄用Teaser元件。請改用 [目標元件](/help/sites-authoring/content-targeting-touch.md).
* **Teaser段落** 是內容頁面中Teaser的實際例項。 這些功能可吸引部分訪客進入關注其興趣的內容。
* 包含以特定訪客區段為焦點之促銷活動內容的頁面。 通常，Teaser段落會將訪客導向到這類頁面。

## 策略 {#strategies}

將Teaser段落新增至頁面時，您必須定義 **策略**.

這適用於多個Teaser可供選擇的情況，因為它們指派的區段都已成功解析。 此 **策略** 然後指定用於選取所顯示Teaser的額外條件：

* **Clickstream分數**，根據訪客使用者端內容中保留的標籤和相關標籤點選（顯示訪客點按包含個別標籤的頁面的頻率）。 系統會比較Teaser頁面上定義之標籤的點選率。
* **Random**，表示「隨機」選擇；使用針對頁面產生的隨機因子，這可以用以下方式檢視 [使用者端內容](/help/sites-administering/client-context.md).
* **第一** 在已解析區段清單中。 順序是行銷活動容器頁面中Teaser的順序。

此 [提升因數](/help/sites-administering/campaign-segmentation.md#boost-factor) 對選取範圍也有影響。 這是新增至區段定義的加權係數，可增加/減少選取該區段的相對可能性。

各種選取標準的流程和相互關係以範例最能說明（也可以用來確保您的Teaser觸及所需受眾的方法）。

如果已建立下列區段並為其指派個別的提升係數：

| 區段 | 提升因數 |
|---|---|
| S1 | 0 |
| S2 | 0 |
| S3 | 10 |
| S4 | 30 |
| S5 | 0 |
| S6 | 100 |

我們使用下列Teaser定義：

<table>
 <tbody>
  <tr>
   <td>行銷活動</td>
   <td>Teaser</td>
   <td>已指派的區段</td>
   <td>指派的標籤 </td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T1</td>
   <td>S1、S2</td>
   <td>業務，行銷</td>
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
   <td>S1、S2、S6</td>
   <td>行銷</td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T6</td>
   <td>S6</td>
   <td>企業<br /> </td>
  </tr>
 </tbody>
</table>

那麼如果我們將此套用至訪客，其中：

* **S1**、 **S2和 **S6** 已成功解析

* 標籤 **行銷** 有三個點選
* 標籤 **企業** 有六個點選

我們可以看到結果：

* 比對成功 — 是否有任何指派給Teaser的區段成功解析為目前訪客？
* 提升係數 — 所有適用區段中的最高提升係數
* 點按流分數 — 所有適用標籤點選的累積總數

在套用適當策略之前計算得出的值：

<table>
 <tbody>
  <tr>
   <td>行銷活動</td>
   <td>Teaser</td>
   <td>已指派的區段</td>
   <td>標記 </td>
   <td>相符成功？</td>
   <td>產生的提升因數</td>
   <td>產生的Clickstream分數 </td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T1</td>
   <td>S1、S2</td>
   <td>業務，行銷</td>
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
   <td>S1、S2、S6</td>
   <td>行銷</td>
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

這些值是用來決定訪客將會看到的Teaser，實際情形取決於 **策略** 套用至Teaser段落：

<table>
 <tbody>
  <tr>
   <td>策略</td>
   <td>產生的Teaser</td>
   <td>評論</td>
  </tr>
  <tr>
   <td>第一個</td>
   <td>T5</td>
   <td>只有T5和T6被視為其區段都解析 <i>和</i> 它們的提升係數最高。 傳回的清單順序為T5、T6；因此會選取並顯示T5。</td>
  </tr>
  <tr>
   <td>隨機</td>
   <td>T5或T6</td>
   <td>兩個Teaser都有完全解決和相同提升因子的區段。 因此，兩個Teaser會以相等比例顯示。</td>
  </tr>
  <tr>
   <td>Clickstream分數</td>
   <td>T6</td>
   <td><p>T1、T4、T5和T6的區段都會解析給訪客。 T5和T6的較高提升係數會排除T1和T4。 最後，T6的點按資料流分數較高會導致系統選取此專案。</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>在上述解析度技巧之後，如果有多個Teaser可供選取，則內部選取範圍（隨機）會選取單一Teaser進行顯示。
>
>例如，如果策略是Clickstream分數且T5的Clickstream分數與T6相同（即，6而不是三），則會使用內部選擇（隨機）來選取這兩者之一。

Teaser頁面/段落可用來將特定訪客區段引導至聚焦於其興趣的內容。 附註可呈現一系列可供訪客選擇的選項，或僅顯示一個以特定訪客區段為基礎的Teaser段落。 例如，顯示的Teaser段落可能會視訪客的年齡而定。

通常Teaser頁面是持續特定時間的暫時動作，直到被下一個Teaser頁面取代為止。

建立您的品牌和行銷活動後，您可以建立和設定您的Teaser體驗。

### 為您的Teaser建立接觸點 {#creating-a-touchpoint-for-your-teaser}

>[!NOTE]
>
>AEM 6.2已棄用Teaser元件。請改用 [目標元件](/help/sites-authoring/content-targeting-touch.md).

1. 導覽至您要放置Teaser段落的內容頁面，此段落將導向您的行銷活動頁面。
1. 新增 **Teaser** 元件(可在 **個人化** 部分)。 初次建立時，會顯示尚未設定行銷活動路徑：

   ![chlimage_1](assets/chlimage_1.png)

1. 編輯Teaser元件以新增：

   * **行銷活動路徑**
包含個別Teaser頁面的促銷活動頁面路徑；區段會確切決定要顯示哪個Teaser。

   * **[策略](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#strategies)**
成功解析多個區段時用於選取的方法。

   ![chlimage_1-1](assets/chlimage_1-1.png)

1. 按一下 **確定** 以儲存。 根據您在Teaser上設定的區段以及您目前登入身分的使用者設定檔，將會顯示適當的內容：

   ![chlimage_1-2](assets/chlimage_1-2.png)

1. 將游標移至Teaser段落上方，會顯示問號圖示（元件的右下角）。 按一下以檢視套用的區段以及它們目前是否解析。

   ![chlimage_1-3](assets/chlimage_1-3.png)

### Teaser概述 {#teaser-overview}

除了MCM中的行銷活動檢視外，行銷活動頁面也會提供與其連線的Teaser的相關資訊：

1. 從 **網站** 主控台，開啟促銷活動頁面；例如：

   `https://localhost:4502/content/campaigns/geometrixx-outdoors/storefront/summer.html`

   以下顯示Teaser定義和檢視統計資料的概觀：

   ![chlimage_1-4](assets/chlimage_1-4.png)
