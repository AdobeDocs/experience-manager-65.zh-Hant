---
title: 設定區段
seo-title: 設定區段
description: 了解如何為AEM Campaign設定分段。
seo-description: 了解如何為AEM Campaign設定分段。
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
source-wordcount: '1080'
ht-degree: 2%

---

# 配置分段{#configuring-segmentation}

>[!NOTE]
>
>本檔案說明如何設定與用戶端內容搭配使用的區段。 若要使用觸控式UI使用ContextHub設定區段，請參閱[使用ContextHub設定區段](/help/sites-administering/segmentation.md)。

區段是建立促銷活動時的主要考量。 如需細分運作方式和關鍵字的相關資訊，請參閱[細分字彙表](/help/sites-authoring/segmentation-overview.md)。

根據您已收集的網站訪客相關資訊以及您要達成的目標，您需要定義目標內容所需的區段和策略。

然後，這些區段會用來為訪客提供特定目標內容。 此內容會保留在網站的[Campaigns](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)區段中。 此處定義的預告頁面可納入為任何頁面上的預告段落，並定義專用內容適用的訪客區段。

AEM可讓您輕鬆建立和更新區段、茶匙和促銷活動。 也可讓您驗證定義的結果。

**區段編輯器**&#x200B;可讓您輕鬆定義區段：

![](assets/segmenteditor.png)

您可以&#x200B;**編輯**&#x200B;每個區段以指定&#x200B;**標題**、**說明**&#x200B;和&#x200B;**Boost**&#x200B;因子。 使用sidekick，您可以新增&#x200B;**AND**&#x200B;和&#x200B;**OR**&#x200B;容器來定義&#x200B;**區段邏輯**，然後新增必要的&#x200B;**區段特徵**&#x200B;來定義選取標準。

## 提升因子{#boost-factor}

每個區段都有一個&#x200B;**Boost**&#x200B;參數，用作加權因數；數字越高，表示將會選取區段，而偏好選取數字越小的區段。

* 最小值：`0`
* 最大值：`1000000`

## 區段邏輯{#segment-logic}

下列邏輯容器是現成可用的，可讓您建構區段選取的邏輯。 可將它們從側腳拖曳至編輯器：

<table>
 <tbody>
  <tr>
   <td> AND 容器<br /> </td>
   <td> 布林值AND運算子。<br /> </td>
  </tr>
  <tr>
   <td> OR 容器<br /> </td>
   <td> 布林值OR運算子。</td>
  </tr>
 </tbody>
</table>

## 區段特徵{#segment-traits}

下列區段特徵可立即使用；可將它們從sidekick拖曳至編輯器：

<table>
 <tbody>
  <tr>
   <td> IP 範圍<br /> </td>
   <td>定義訪客可擁有的IP位址範圍。<br /> </td>
  </tr>
  <tr>
   <td> 頁面點擊<br /> </td>
   <td>要求頁面的頻率。<br /> </td>
  </tr>
  <tr>
   <td> 頁面屬性<br /> </td>
   <td>已造訪頁面的任何屬性。<br /> </td>
  </tr>
  <tr>
   <td> 引用關鍵字<br /> </td>
   <td>與反向連結網站資訊相符的關鍵字。<br /> </td>
  </tr>
  <tr>
   <td> 指令碼</td>
   <td>要評估的Javascript表達式。<br /> </td>
  </tr>
  <tr>
   <td> 區段引用 <br /> </td>
   <td>參考其他段定義。<br /> </td>
  </tr>
  <tr>
   <td> 標記雲<br /> </td>
   <td>要與所瀏覽頁面中的標籤相符的標籤。<br /> </td>
  </tr>
  <tr>
   <td> 使用者年齡<br /> </td>
   <td>如從用戶配置檔案中所示。<br /> </td>
  </tr>
  <tr>
   <td> 使用者屬性<br /> </td>
   <td>使用者設定檔中可用的任何其他資訊。 </td>
  </tr>
 </tbody>
</table>

您可以使用布林運算子OR和AND來結合這些特徵（請參閱[建立新區段](#creating-a-new-segment)），以定義選取此區段的確切案例。

當整個陳述式評估為true時，此區段便已解析。 若適用多個區段，則也會使用&#x200B;**[Boost](/help/sites-administering/campaign-segmentation.md#boost-factor)**&#x200B;因子。

>[!CAUTION]
>
>區段編輯器不會檢查任何循環參照。 例如，區段A會參照另一個區段B，而這反過來又會參照區段A。您必須確定您的區段不含任何循環參照。

>[!NOTE]
>
>尾碼為&#x200B;**_i18n**&#x200B;的屬性是由屬於個人化UI clientlib的一部分的指令碼設定。 所有與UI相關的clientlib只會在作者上載入，因為發佈時不需要UI。
>
>因此，使用這類屬性建立區段時，通常需要依賴&#x200B;**browserFamily**&#x200B;來執行，而非&#x200B;**browserFamily_i18n**。

### 建立新區段{#creating-a-new-segment}

若要定義新區段：

1. 在邊欄中，選擇&#x200B;**工具>操作>配置**。
1. 按一下左窗格的&#x200B;**分段**&#x200B;頁面，並導覽至所需位置。
1. 使用&#x200B;**Segment**&#x200B;範本建立[新頁面](/help/sites-authoring/editing-content.md#creatinganewpage)。
1. 開啟新頁面以查看區段編輯器：

   ![](assets/screen_shot_2012-02-02at101726am.png)

1. 使用sidekick或上下文菜單(通常是按滑鼠右鍵，然後選擇&#x200B;**New...**&#x200B;以開啟「插入新元件」視窗)以尋找您需要的區段特徵。 然後將其拖曳至&#x200B;**區段編輯器**，它將出現在預設的&#x200B;**AND**&#x200B;容器中。
1. 連按兩下新特徵以編輯特定參數；例如滑鼠位置：

   ![](assets/screen_shot_2012-02-02at103135am.png)

1. 按一下&#x200B;**OK**&#x200B;以保存定義：
1. 您可以&#x200B;**編輯**&#x200B;區段定義，為其提供&#x200B;**Title**、**Description**&#x200B;和&#x200B;**[Boost](#boost-factor)**&#x200B;因子：

   ![](assets/screen_shot_2012-02-02at103547am.png)

1. 視需要新增更多特徵。 您可以使用&#x200B;**區段邏輯**&#x200B;下的&#x200B;**AND容器**&#x200B;和&#x200B;**OR容器**&#x200B;元件來制定布林運算式。 使用區段編輯器，您可以刪除不再需要的特徵或容器，或將它們拖曳至陳述式內的新位置。

### 使用AND和OR容器{#using-and-and-or-containers}

您可以在AEM中建立複雜的區段。 請注意以下幾個基本要點，會有所幫助：

* 定義的頂層一律為最初建立的AND容器；此項目無法變更，但對其餘的區段定義沒有影響。
* 確保容器的巢狀有意義。 容器可以視為布林運算式的方括弧。

以下範例用於選取下列其中之一的訪客：

男，16至65歲

或

女性，16至62歲

由於主運算子為OR，因此您需要以&#x200B;**OR Container**&#x200B;開頭。 在此內，您有2個AND陳述式，針對每個陳述式，您都需要&#x200B;**AND Container**，以便新增個別特徵。

![](assets/screen_shot_2012-02-02at105145am.png)

## 測試區段{#testing-the-application-of-a-segment}的應用程式

定義區段後，即可在&#x200B;**[用戶端內容](/help/sites-administering/client-context.md)**&#x200B;的協助下測試潛在結果：

1. 選取要測試的區段。
1. 按&#x200B;**[Ctrl-Alt-C](/help/sites-authoring/page-authoring.md#keyboardshortcuts)**&#x200B;開啟&#x200B;**[客戶端上下文](/help/sites-administering/client-context.md)**，其中顯示已收集的資料。 為了測試目的，您可以&#x200B;**編輯**&#x200B;某些值，或&#x200B;**載入**&#x200B;其他設定檔，以查看其影響。

1. 根據定義的特徵，目前頁面可用的資料可能與區段定義不符。 比對的狀態會顯示在定義下。

例如，簡單的區段定義可以根據使用者的年齡和性別。 載入特定設定檔時，會顯示區段已成功解析：

![](assets/screen_shot_2012-02-02at105926am.png)

或者不是：

![](assets/screen_shot_2012-02-02at110019am.png)

>[!NOTE]
>
>所有特徵都會立即解析，不過大部分只會在頁面重新載入時變更。 滑鼠位置的變更可立即顯示，因此對於測試非常有用。

此類測試也可以在內容頁面上，並與&#x200B;**Teaser**&#x200B;元件結合執行。

預告段落上的滑鼠移過會顯示套用的區段（無論這些區段目前是否解決），因此，為何已選取目前的預告例項：

![](assets/chlimage_1-47.png)

### 使用您的區段{#using-your-segment}

目前在[Campaigns](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)中使用區段。 它們可用來指引特定目標對象所看到的實際內容。 如需詳細資訊，請參閱[了解區段](/help/sites-authoring/segmentation-overview.md) 。
