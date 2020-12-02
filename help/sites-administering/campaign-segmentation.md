---
title: 設定區段
seo-title: 設定區段
description: 瞭解如何設定AEM Campaign的區段。
seo-description: 瞭解如何設定AEM Campaign的區段。
uuid: 604ca34d-cdb9-49ff-8f75-02a44b60a8a2
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: c68d5853-684f-42f2-a215-c1eaee06f58a
docset: aem65
translation-type: tm+mt
source-git-commit: 684d2d5f73d571a15c8155e7870134c28dc892b7
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 2%

---


# 設定區段{#configuring-segmentation}

>[!NOTE]
>
>本檔案涵蓋「用戶端內容」中使用的區段設定。 若要使用觸控式UI設定區段與ContextHub，請參閱[使用ContextHub](/help/sites-administering/segmentation.md)設定區段。

區段是建立促銷活動時的主要考量。 如需細分運作方式和關鍵詞語的詳細資訊，請參閱[分段辭彙表](/help/sites-authoring/segmentation-overview.md)。

根據您已收集的網站訪客相關資訊以及您要達到的目標，您需要定義目標內容所需的區段和策略。

然後，這些區段會用來為訪客提供特定的目標內容。 此內容會保留在網站的[Campaigns](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)區段中。 此處定義的摘要頁面可以納入為任何頁面上的摘要段落，並定義專業內容適用的訪客區段。

AEM可讓您輕鬆建立和更新區段、預告和促銷活動。 它還允許您驗證定義的結果。

**區段編輯器**&#x200B;可讓您輕鬆定義區段：

![](assets/segmenteditor.png)

您可以&#x200B;**編輯**&#x200B;每個區段以指定&#x200B;**標題**、**說明**&#x200B;和&#x200B;**Boost**&#x200B;因子。 使用側腳，您可新增&#x200B;**AND**&#x200B;和&#x200B;**OR**&#x200B;容器來定義&#x200B;**區段邏輯**，然後新增所需的&#x200B;**區段特徵**&#x200B;來定義選擇標準。

## Boost Factor {#boost-factor}

每個區段都有一個&#x200B;**Boost**&#x200B;參數，用作加權系數；數字越大，表示區段將優先選取數字越低的區段。

* 最小值：`0`
* 最大值：`1000000`

## 區段邏輯{#segment-logic}

下列邏輯容器是現成可用的，可讓您建構區段選擇的邏輯。 它們可從側腳拖曳至編輯器：

<table>
 <tbody>
  <tr>
   <td> AND 容器<br /> </td>
   <td> 布林AND運算子。<br /> </td>
  </tr>
  <tr>
   <td> OR 容器<br /> </td>
   <td> 布林OR運算子。</td>
  </tr>
 </tbody>
</table>

## 區段特徵{#segment-traits}

以下是現成可用的區段特徵；它們可從側腳拖曳至編輯器：

<table>
 <tbody>
  <tr>
   <td> IP 範圍<br /> </td>
   <td>定義訪客可擁有的IP位址範圍。<br /> </td>
  </tr>
  <tr>
   <td> 頁面點擊<br /> </td>
   <td>請求頁面的頻率。<br /> </td>
  </tr>
  <tr>
   <td> 頁面屬性<br /> </td>
   <td>已瀏覽頁面的任何屬性。<br /> </td>
  </tr>
  <tr>
   <td> 引用關鍵字<br /> </td>
   <td>與反向連結網站資訊相符的關鍵字。<br /> </td>
  </tr>
  <tr>
   <td> 指令碼</td>
   <td>要評估的Javascript運算式。<br /> </td>
  </tr>
  <tr>
   <td> 區段引用 <br /> </td>
   <td>參考其他區段定義。<br /> </td>
  </tr>
  <tr>
   <td> 標記雲<br /> </td>
   <td>要與瀏覽頁面中的標籤相符的標籤。<br /> </td>
  </tr>
  <tr>
   <td> 使用者年齡<br /> </td>
   <td>根據用戶配置檔案。<br /> </td>
  </tr>
  <tr>
   <td> 使用者屬性<br /> </td>
   <td>使用者設定檔中提供的任何其他資訊。 </td>
  </tr>
 </tbody>
</table>

您可以使用布林運算子OR和AND來結合這些特性（請參閱[建立新區段](#creating-a-new-segment)），以定義選取此區段的確切藍本。

當整個語句評估為true時，此段已解決。 若有多個區段可適用，則也會使用&#x200B;**[Boost](/help/sites-administering/campaign-segmentation.md#boost-factor)**&#x200B;因子。

>[!CAUTION]
>
>段編輯器不檢查任何循環參照。 例如，區段A會參照另一個區段B，反過來參照區段A。您必須確保區段不包含任何循環參照。

>[!NOTE]
>
>具有&#x200B;**_i18n**&#x200B;字尾的屬性由個人化UI客戶程式庫的一部份指令碼設定。 所有UI相關的用戶端僅會載入作者，因為發佈時不需要UI。
>
>因此，建立具有此類屬性的區段時，通常需要依賴&#x200B;**browserFamily**（例如），而非&#x200B;**browserFamily_i18n**。

### 建立新區段{#creating-a-new-segment}

要定義新段，請執行以下操作：

1. 在滑軌中，選擇「**工具>操作>配置**」。
1. 按一下左窗格中的&#x200B;**區段**&#x200B;頁面，並導覽至所需位置。
1. 使用&#x200B;**Segment**&#x200B;範本建立[新頁面](/help/sites-authoring/editing-content.md#creatinganewpage)。
1. 開啟新頁面以檢視區段編輯器：

   ![](assets/screen_shot_2012-02-02at101726am.png)

1. 使用sidekick或上下文功能表(通常為滑鼠右鍵按一下，然後選取「新增……」**以開啟「插入新元件」視窗)，以尋找所需的區段特徵。**&#x200B;然後將其拖曳至&#x200B;**區段編輯器**，它會出現在預設的&#x200B;**AND**&#x200B;容器中。
1. 連按兩下新特徵以編輯特定參數；例如，滑鼠位置：

   ![](assets/screen_shot_2012-02-02at103135am.png)

1. 按一下&#x200B;**確定**&#x200B;保存定義：
1. 您可以&#x200B;**編輯**&#x200B;區段定義，以提供&#x200B;**Title**、**Description**&#x200B;和&#x200B;**[Boost](#boost-factor)**&#x200B;系數：

   ![](assets/screen_shot_2012-02-02at103547am.png)

1. 視需要新增更多特徵。 您可使用&#x200B;**AND Container**&#x200B;和&#x200B;**OR Container**&#x200B;元件來建立布林運算式，這些元件位於&#x200B;**區段邏輯**&#x200B;下。 使用區段編輯器，您可以刪除不再需要的特徵或容器，或將它們拖曳至陳述式中的新位置。

### 使用AND和OR容器{#using-and-and-or-containers}

您可以在AEM中建構複雜的區段。 瞭解以下幾個基本要點有幫助：

* 定義的頂層永遠是最初建立的AND容器；這無法變更，但對您的其餘區段定義沒有影響。
* 確保容器巢狀結構合理。 容器可以視為布林運算式的括弧。

以下範例用於選擇其中一個訪客：

男，16歲到65歲

或

16至62歲的女性

由於主運算子為OR，因此您需要從&#x200B;**OR Container**&#x200B;開始。 在此中，您有2個AND陳述式，對於每個陳述式，您都需要&#x200B;**AND Container**，您可將個別特徵加入其中。

![](assets/screen_shot_2012-02-02at105145am.png)

## 測試區段{#testing-the-application-of-a-segment}的應用程式

定義區段後，即可透過&#x200B;**[用戶端內容](/help/sites-administering/client-context.md)**&#x200B;測試潛在結果：

1. 選取要測試的區段。
1. 按&#x200B;**[Ctrl-Alt-C](/help/sites-authoring/page-authoring.md#keyboardshortcuts)**&#x200B;以開啟&#x200B;**[用戶端內容](/help/sites-administering/client-context.md)**，顯示已收集的資料。 為進行測試，您可以&#x200B;**編輯**&#x200B;某些值，或&#x200B;**載入**&#x200B;其他描述檔，以檢視其影響。

1. 根據定義的特性，目前頁面的可用資料可能與區段定義不符。 相符的狀態會顯示在定義下方。

例如，簡單的區段定義可以根據使用者的年齡和性別。 載入特定描述檔會顯示區段已成功解決：

![](assets/screen_shot_2012-02-02at105926am.png)

或者不：

![](assets/screen_shot_2012-02-02at110019am.png)

>[!NOTE]
>
>所有特徵都會立即解決，不過大部分只會在頁面重新載入時變更。 對滑鼠位置的變更會立即顯示，因此在測試時非常實用。

此類測試也可在內容頁面上，並搭配&#x200B;**Teaser**&#x200B;元件執行。

摘要段落上的滑鼠移過會顯示套用的區段，不論這些區段目前是否解析，以及選取目前摘要例項的原因：

![](assets/chlimage_1-47.png)

### 使用您的區段{#using-your-segment}

區段目前用於[促銷活動](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)。 它們可用來調整特定目標對象所看到的實際內容。 如需詳細資訊，請參閱[瞭解區段](/help/sites-authoring/segmentation-overview.md)。
