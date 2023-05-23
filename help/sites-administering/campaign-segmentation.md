---
title: 配置分段
seo-title: Configuring Segmentation
description: 瞭解如何為市場活動配AEM置細分。
seo-description: Learn how to configure segmentation for AEM Campaign.
uuid: 604ca34d-cdb9-49ff-8f75-02a44b60a8a2
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: c68d5853-684f-42f2-a215-c1eaee06f58a
docset: aem65
exl-id: 6d759907-8796-4749-bd80-306ec7f2c819
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 2%

---

# 配置分段 {#configuring-segmentation}

>[!NOTE]
>
>本文檔介紹與客戶端上下文一起使用的分段配置。 要使用觸摸UI配置ContextHub的段，請參閱 [使用ContextHub配置分段](/help/sites-administering/segmentation.md)。

細分是建立市場活動時的一個關鍵考慮因素。 請參閱 [分詞術語表](/help/sites-authoring/segmentation-overview.md) 分段的工作原理和關鍵術語。

根據您已經收集到的有關站點訪問者的資訊以及您想要實現的目標，您需要定義目標內容所需的段和策略。

然後，這些段被用於向訪問者提供特定的目標內容。 此內容在 [市場活動](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md) 的下界。 此處定義的預告頁面可以作為預告段落包含在任何頁面上，並定義專用內容適用的訪問者段。

使AEM您可以輕鬆建立和更新段、預告和市場活動。 它還允許您驗證定義的結果。

的 **段編輯器** 允許您輕鬆定義段：

![](assets/segmenteditor.png)

你可以 **編輯** 要指定的每個段 **標題**。 **說明** 和 **提升** 因素。 使用可添加的幫手 **和** 和 **或** 要定義的容器 **段邏輯**，然後添加所需的 **分段特徵** 的子菜單。

## 提升因子 {#boost-factor}

每段 **提升** 權因子的參數；數字越大，表示將優先選擇數字越小的段。

* 最小值： `0`
* 最大值： `1000000`

## 段邏輯 {#segment-logic}

以下邏輯容器是現成的，允許您構造段選擇的邏輯。 它們可以從旁邊拖到編輯器：

<table>
 <tbody>
  <tr>
   <td> AND 容器<br /> </td>
   <td> 布爾AND運算子。<br /> </td>
  </tr>
  <tr>
   <td> OR 容器<br /> </td>
   <td> 布爾OR運算子。</td>
  </tr>
 </tbody>
</table>

## 分段特徵 {#segment-traits}

以下片段特徵是現成的；可將它們從旁邊拖到編輯：

<table>
 <tbody>
  <tr>
   <td> IP 範圍<br /> </td>
   <td>定義訪問者可以擁有的IP地址範圍。<br /> </td>
  </tr>
  <tr>
   <td> 頁面點擊<br /> </td>
   <td>請求頁面的頻率。 <br /> </td>
  </tr>
  <tr>
   <td> 頁面屬性<br /> </td>
   <td>已訪問頁面的任何屬性。<br /> </td>
  </tr>
  <tr>
   <td> 引用關鍵字<br /> </td>
   <td>與引用網站中的資訊匹配的關鍵字。 <br /> </td>
  </tr>
  <tr>
   <td> 指令碼</td>
   <td>要計算的Javascript表達式。<br /> </td>
  </tr>
  <tr>
   <td> 區段引用 <br /> </td>
   <td>引用另一段定義。<br /> </td>
  </tr>
  <tr>
   <td> 標記雲<br /> </td>
   <td>要與訪問的頁面中的標籤匹配的標籤。<br /> </td>
  </tr>
  <tr>
   <td> 使用者年齡<br /> </td>
   <td>從用戶配置檔案中取出。<br /> </td>
  </tr>
  <tr>
   <td> 使用者屬性<br /> </td>
   <td>用戶配置檔案中提供的任何其他資訊。 </td>
  </tr>
 </tbody>
</table>

可以使用布爾運算子OR和AND組合這些特徵(請參見 [建立新段](#creating-a-new-segment))以定義選擇此段的確切方案。

當整個語句的計算結果為true時，此段已解析。 倘多個分段適用，則 **[提升](/help/sites-administering/campaign-segmentation.md#boost-factor)** 也使用因子。

>[!CAUTION]
>
>段編輯器不檢查是否有任何循環引用。 例如，段A參照另一段B，該段B又參照段A。必須確保段不包含任何循環參照。

>[!NOTE]
>
>具有 **_i18n** 尾碼由作為個性化的UI客戶端庫的一部分的指令碼設定。 只有在發佈時不需要UI，才會在作者上載入所有與UI相關的客戶端。
>
>因此，在建立具有這些屬性的段時，通常需要依賴 **瀏覽器系列** 例如， **browserFamily_i18n**。

### 建立新段 {#creating-a-new-segment}

要定義新段，請執行以下操作：

1. 在鐵軌中，選擇 **工具>操作>配置**。
1. 按一下 **分段** 的子菜單。
1. 建立 [新頁](/help/sites-authoring/editing-content.md#creatinganewpage) 使用 **段** 的下界。
1. 開啟新頁面以查看段編輯器：

   ![](assets/screen_shot_2012-02-02at101726am.png)

1. 使用邊框或上下文菜單(通常按一下右鍵，然後選擇 **新建……** 開啟「插入新元件」窗口)以查找所需的段特性。 然後將其拖到 **段編輯器** 將顯示在預設 **和** 容器。
1. 按兩下新特徵編輯特定參數；例如滑鼠位置：

   ![](assets/screen_shot_2012-02-02at103135am.png)

1. 按一下 **確定** 保存定義：
1. 你可以 **編輯** 段定義，以給它 **標題**。 **說明** 和 **[提升](#boost-factor)** 系數：

   ![](assets/screen_shot_2012-02-02at103547am.png)

1. 如果需要，添加更多特徵。 可以使用 **和容器** 和 **OR容器** 在 **段邏輯**。 使用段編輯器，您可以刪除不再需要的特徵或容器，或將它們拖到語句中的新位置。

### 使用AND和OR容器 {#using-and-and-or-containers}

可在中構建複雜段AEM。 瞭解以下幾個基本要點有助於：

* 定義的頂層始終是最初建立的AND容器；不能更改，但對段定義的其餘部分沒有影響。
* 確保將容器嵌套是合理的。 容器可以作為布爾表達式的括弧來查看。

以下示例用於選擇以下任一訪問者：

男，16至65歲

或

女性，16至62歲

由於主運算子為OR，因此您需要從 **OR容器**。 在此內，您有2個AND語句，對於每個語句，您都需要 **和容器**&#x200B;可以添加個性特徵。

![](assets/screen_shot_2012-02-02at105145am.png)

## 測試段的應用 {#testing-the-application-of-a-segment}

定義該段後，可借助 **[客戶端上下文](/help/sites-administering/client-context.md)**:

1. 選擇要測試的段。
1. 按 **[Ctrl-Alt-C](/help/sites-authoring/page-authoring.md#keyboardshortcuts)** 開啟 **[客戶端上下文](/help/sites-administering/client-context.md)**，顯示已收集的資料。 為了測試目的，您可以 **編輯** 某些值，或 **載入** 另一個配置檔案，以查看其影響。

1. 根據定義的特性，當前頁可用的資料可能與段定義不匹配。 匹配狀態顯示在定義下面。

例如，簡單的段定義可以基於用戶的年齡和性別。 載入特定配置檔案表明已成功解析段：

![](assets/screen_shot_2012-02-02at105926am.png)

或者不是：

![](assets/screen_shot_2012-02-02at110019am.png)

>[!NOTE]
>
>所有特徵都會立即解析，儘管大多數情況只在重新載入頁面時更改。 對滑鼠位置的更改可立即顯示，因此對於測試目的非常有用。

這種test也可以在內容頁面上和與 **預告** 元件。

預告段落上的滑鼠懸停將顯示所應用的段，無論這些段當前是否已解決，因此，當前預告實例為何已被選擇：

![](assets/chlimage_1-47.png)

### 使用段 {#using-your-segment}

段當前在 [市場活動](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)。 它們用於指導特定目標受眾看到的實際內容。 請參閱 [瞭解段](/help/sites-authoring/segmentation-overview.md) 的子菜單。
