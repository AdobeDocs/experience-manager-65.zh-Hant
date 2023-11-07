---
title: 設定分段
seo-title: Configuring Segmentation
description: 瞭解如何設定AEM Campaign的分段。
seo-description: Learn how to configure segmentation for AEM Campaign.
uuid: 604ca34d-cdb9-49ff-8f75-02a44b60a8a2
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: c68d5853-684f-42f2-a215-c1eaee06f58a
docset: aem65
exl-id: 6d759907-8796-4749-bd80-306ec7f2c819
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 1%

---


# 設定分段 {#configuring-segmentation}

>[!NOTE]
>
>本文介紹與Client Context搭配使用之區段的設定。 若要使用觸控式UI以ContextHub設定區段，請參閱 [使用ContextHub設定分段](/help/sites-administering/segmentation.md).

細分是建立行銷活動時的關鍵考量。 另請參閱 [區段字彙表](/help/sites-authoring/segmentation-overview.md) 區段運作方式和主要術語的相關資訊。

根據您已收集到的網站訪客相關資訊以及您想要達成的目標，您必須定義目標內容所需的區段和策略。

接著，這些區段可用來向訪客提供明確鎖定的目標內容。 此內容維護於 [行銷活動](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md) 網站區段。 此處定義的Teaser頁面可包含在任何頁面上作為Teaser段落，並定義專用內容適用的訪客區段。

AEM可讓您輕鬆建立和更新區段、Teaser和促銷活動。 它也可讓您驗證定義的結果。

此 **區段編輯器** 可讓您輕鬆定義區段：

![區段編輯器視窗](assets/segmenteditor.png)

您可以 **編輯** 每個區段以指定 **標題**， **說明** 和 **提升** 因數。 使用sidekick您可以新增 **和** 和 **或** 容器以定義 **區段邏輯**，然後新增必要的 **區段特徵** 以定義選取條件。

## 提升因數 {#boost-factor}

每個區段都有 **提升** 用作加權因子的引數；數字越高表示優先選取區段而不是數字越低的區段。

* 最小值： `0`
* 最大值： `1000000`

## 區段邏輯 {#segment-logic}

下列邏輯容器可立即使用，讓您建構區段選取的邏輯。 它們可以從sidekick拖到編輯者：

<table>
 <tbody>
  <tr>
   <td> AND 容器<br /> </td>
   <td> 布林值AND運運算元。<br /> </td>
  </tr>
  <tr>
   <td> OR 容器<br /> </td>
   <td> 布林值OR運運算元。</td>
  </tr>
 </tbody>
</table>

## 區段特徵 {#segment-traits}

下列區段特徵現成可用；可將它們從Sidekick拖曳至編輯器：

<table>
 <tbody>
  <tr>
   <td> IP 範圍<br /> </td>
   <td>定義訪客可擁有的IP位址範圍。<br /> </td>
  </tr>
  <tr>
   <td> 頁面點擊<br /> </td>
   <td>要求頁面的頻率。 <br /> </td>
  </tr>
  <tr>
   <td> 頁面屬性<br /> </td>
   <td>造訪頁面的任何屬性。<br /> </td>
  </tr>
  <tr>
   <td> 引用關鍵字<br /> </td>
   <td>與引用網站的資訊相符的關鍵字。 <br /> </td>
  </tr>
  <tr>
   <td> 指令碼</td>
   <td>要評估的JavaScript運算式。<br /> </td>
  </tr>
  <tr>
   <td> 區段引用 <br /> </td>
   <td>參考其他區段定義。<br /> </td>
  </tr>
  <tr>
   <td> 標記雲<br /> </td>
   <td>與瀏覽頁面中的標籤進行比對的標籤。<br /> </td>
  </tr>
  <tr>
   <td> 使用者年齡<br /> </td>
   <td>從使用者設定檔中擷取。<br /> </td>
  </tr>
  <tr>
   <td> 使用者屬性<br /> </td>
   <td>使用者設定檔中可用的任何其他資訊。 </td>
  </tr>
 </tbody>
</table>

您可以使用布林運運算元OR和AND來結合這些特徵(請參閱 [建立新區段](#creating-a-new-segment))，以定義選取此區段的確切案例。

當整個陳述式評估為true時，表示此區段已解析。 在適用多個區段的情況下，則 **[提升](/help/sites-administering/campaign-segmentation.md#boost-factor)** 也會使用因數。

>[!CAUTION]
>
>區段編輯器不會檢查任何循環參照。 例如，區段A參照另一個區段B，而後者又參照區段A。您必須確保區段不包含任何循環參照。

>[!NOTE]
>
>具有的屬性 **_i18n** 尾碼是由指令碼設定，此指令碼是個人化UI clientlib的一部分。 所有與UI相關的clientlibs僅載入到作者中，因為發佈時不需要使用UI。
>
>因此，建立具有這類屬性的區段時，通常需要依賴 **browserFamily** 例如，而非 **browserFamily_i18n**.

### 建立新區段 {#creating-a-new-segment}

若要定義新區段，請執行下列動作：

1. 在邊欄中，選擇 **「工具」 > 「作業」 > 「組態」**.
1. 按一下 **細分** 頁面，並導覽至所需位置。
1. 建立 [新頁面](/help/sites-authoring/editing-content.md#creatinganewpage) 使用 **區段** 範本。
1. 開啟新頁面以檢視區段編輯器：

   ![在區段編輯器中建立區段的第一步](assets/screen_shot_2012-02-02at101726am.png)

1. 使用sidekick或內容功能表(通常是按一下滑鼠右鍵，然後選取 **新增……** 以開啟「插入新元件」視窗)來尋找所需的區段特徵。 然後將其拖曳至 **區段編輯器** 它將顯示在預設值 **和** 容器。
1. 按兩下新特徵以編輯特定引數；例如滑鼠位置：

   ![在區段編輯器中編輯元件](assets/screen_shot_2012-02-02at103135am.png)

1. 按一下 **確定** 若要儲存您的定義：
1. 您可以 **編輯** 區段定義，用於提供 **標題**， **說明** 和 **[提升](#boost-factor)** 因數：

   ![在區段編輯器中編輯區段設定](assets/screen_shot_2012-02-02at103547am.png)

1. 如有需要，可新增更多特徵。 您可以使用來制定布林運算式 **AND容器** 和 **OR容器** 在「 」下找到的元件 **區段邏輯**. 使用區段編輯器，您可以刪除不再需要的特徵或容器，或將它們拖曳至陳述式中的新位置。

### 使用AND和OR容器 {#using-and-and-or-containers}

您可以在AEM中建構複雜的區段。 瞭解一些基本要點會有所幫助：

* 定義的最上層一律為最初建立的AND容器；這無法變更，但不會影響區段定義的其餘部分。
* 確定容器的巢狀內嵌有意義。 容器可視為布林運算式的括弧。

下列範例可用來選取符合下列任一條件的訪客：

男性及16至65歲

或

女性及16至62歲之間

由於主要運運算元是OR，因此您必須以 **OR容器**. 其中您有2個AND陳述式，每個陳述式都需要 **AND容器**，您可將個別特徵新增至其中。

![區段編輯器中的AND和OR運運算元範例](assets/screen_shot_2012-02-02at105145am.png)

## 測試區段的應用 {#testing-the-application-of-a-segment}

定義區段後，可透過測試潛在結果 **[使用者端內容](/help/sites-administering/client-context.md)**：

1. 選取要測試的區段。
1. 按下 **[Ctrl-Alt-C](/help/sites-authoring/page-authoring.md#keyboardshortcuts)** 以開啟 **[使用者端內容](/help/sites-administering/client-context.md)**，會顯示已收集的資料。 為了測試目的，您可以 **編輯** 特定值，或 **載入** 另一個設定檔以檢視那裡的影響。

1. 根據定義的特徵，目前頁面的可用資料可能與區段定義相符，也可能不相符。 相符的狀態會顯示在定義下方。

例如，簡單的區段定義可以根據使用者的年齡和性別。 載入特定設定檔會顯示已成功解析區段：

![使用「使用者端內容」視窗來測試AND分段操作](assets/screen_shot_2012-02-02at105926am.png)

或非：

![使用「使用者端內容」視窗來測試NOT分段操作](assets/screen_shot_2012-02-02at110019am.png)

>[!NOTE]
>
>所有特徵會立即解析，但大多數只會隨著頁面重新載入而變更。 滑鼠位置的變更會立即顯示，因此可用於測試目的。

這類測試也可在內容頁面上執行，並結合 **Teaser** 元件。

將滑鼠游標停留在Teaser段落上會顯示套用的區段、目前是否解析以及選取目前Teaser例項的原因：

![區段滑鼠範例](assets/chlimage_1-47.png)

### 使用您的區段 {#using-your-segment}

區段目前使用於 [行銷活動](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md). 它們可用來控管特定目標對象看到的實際內容。 另請參閱 [瞭解區段](/help/sites-authoring/segmentation-overview.md) 以取得詳細資訊。
