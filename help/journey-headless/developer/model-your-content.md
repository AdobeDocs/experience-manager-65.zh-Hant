---
title: 如何建立內容模型
description: 在AEM無頭式開發人員歷程的這部分，了解如何使用內容模型搭配內容片段模型和內容片段，為AEM無頭式傳送建立內容模型。
exl-id: f75b433f-5a81-4259-a9f5-b58954b87970
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1826'
ht-degree: 2%

---

# 如何建立內容模型 {#model-your-content}

在 [AEM Headless Developer Journey](overview.md)，您可以學習如何建立內容結構的模型。 然後，使用內容片段模型和內容片段來實現Adobe Experience Manager(AEM)的結構，以便跨頻道重複使用。

## 迄今為止的故事 {#story-so-far}

開始時 [了解CMS無頭開發](learn-about.md) 已涵蓋無頭內容傳送，以及使用原因。 然後 [AEM Headless快速入門](getting-started.md) 在您自己的專案內容中說明AEM Headless。

在AEM無頭歷程的上一份檔案中， [使用AEM無頭式的第一次體驗路徑](path-to-first-experience.md)，您便了解實作第一個專案所需的步驟。 閱讀後，您應：

* 了解設計內容時的重要規劃考量事項
* 根據您的整合層級需求，了解實作無頭式裝置的步驟。
* 設定必要的工具和AEM設定。
* 了解最佳實務，讓無頭的歷程順暢、保持內容產生的效率，並確保內容能快速傳遞。

本文以這些基本知識為基礎，讓您了解如何準備您自己的AEM無頭專案。

## 目標 {#objective}

* **對象**:入門者
* **目標**:了解如何建立內容結構的模型，然後使用AEM內容片段模型和內容片段來實現該結構：
   * 介紹與資料/內容模型相關的概念和術語。
   * 了解為何無頭式內容傳送需要內容模型。
   * 了解如何使用AEM內容片段模型（以及使用內容片段製作內容）來實現此結構。
   * 了解如何建立內容模型；基本樣本的原則。

>[!NOTE]
>
>資料建模是一個非常大的領域，因為它在開發關係資料庫時使用。 有很多書籍和線上資訊來源。
>
>我們只會考慮在建立資料模型以與AEM Headless搭配使用時需要注意的方面。

## 內容模型 {#content-modeling}

*外面的世界很糟*.

也許，也許不是，但那肯定是個大 ***複雜*** 外在世界，而資料模型則用來定義非常（非常）小的子區段的簡化表示，使用特定用途所需的特定資訊。

>[!NOTE]
>
>當AEM處理內容時，我們將資料模型稱為內容模型。

例如：

學校很多，但它們有不同的共同點：

* 位置
* 校長
* 許多教師
* 許多非教職員
* 許多學生
* 許多前教師
* 許多前學生
* 許多教室
* 許多（多）本書
* 多（多）件設備
* 許多課外活動
* 等等…….

即使在如此小的例子中，這份清單也可能看起來無窮無盡。 但是，如果您只是希望應用程式執行簡單的任務，則需要將資訊限制在基本資訊。

例如，為該地區的所有學校宣傳特殊活動：

* 學校名稱
* 學校位置
* 校長
* 事件類型
* 事件日期
* 教師組織活動

### 概念 {#concepts}

您要說明的項目稱為 **實體**  — 基本上，我們要儲存資訊的「東西」。

我們要儲存的資訊是 **屬性** （屬性），如教師的姓名和資格。

還有各種 **關係** 在圖元之間。 例如，一所學校通常只有一名校長，而許多教師（而校長通常也是一名教師）。

分析和定義這些資訊的過程以及它們之間的關係被稱為 **內容模型**.

### 基本資訊 {#basics}

您通常需要先繪製 **概念結構** 描述實體及其關係的。 這通常是高階（概念）。

穩定後，您可將模型轉譯為 **邏輯架構** 它描述實體、屬性和關係。 在此層級，您應仔細檢查定義，以消除重複並最佳化您的設計。

>[!NOTE]
>
>有時這兩個步驟會合併，通常取決於您的情境的複雜性。

例如，您是否需要 `Head Teacher` 和 `Teacher`，或只是其他屬性 `Teacher` 模型？

### 確保資料完整性 {#data-integrity}

需要資料完整性來保證內容在整個生命週期中的準確性和一致性。 這包括確保內容作者可輕鬆了解要儲存的位置，因此下列項目非常重要：

* 清晰的結構
* 盡可能簡潔（不犧牲精度）的結構
* 驗證個別欄位
* 若適用，將特定欄位的內容限制為有意義的內容

### 消除資料冗餘 {#data-redundancy}

在內容結構中儲存相同資訊兩次時，會發生資料冗餘。 應避免此情況，因為在建立內容時可能會造成混淆，而在查詢時會造成錯誤；更別提儲存空間的濫用了。

### 最佳化與效能 {#optimization-and-performance}

透過最佳化結構，您可以改善效能，包括內容建立和查詢。

一切都是一種平衡行為，但建立一個過於複雜或層次過多的結構可以：

* 對於產生內容的作者而言會令人困惑。

* 如果查詢必須存取多個巢狀（參考）內容片段以擷取所需內容，則會嚴重影響效能。

## AEM無頭的內容模型 {#content-modeling-for-aem-headless}

資料模型是一組已建立的技術，在開發關係資料庫時經常使用，因此，「內容模型」對AEM Headless有何意義？

### 為什麼？ {#why}

為確保應用程式能夠一致且有效地從AEM要求和接收所需內容，此內容必須結構化。

這表示您的應用程式會事先知道回應的形式，因此會知道如何處理。 這比接收自由格式內容容易得多，因為必須對內容進行剖析，以確定內容包含的內容，因此，如何使用它。

### 如何介紹？ {#how}

AEM使用內容片段來提供將內容無頭式傳送至應用程式所需的結構。

內容模型的結構為：

* 由內容片段模型定義所實現，
* 作為內容產生所用內容片段的基礎。

>[!NOTE]
>
>內容片段模型也是AEM GraphQL結構的基礎，用於擷取內容 — 更多關於稍後工作階段的內容。

系統會使用AEM GraphQL API（標準GraphQL API的自訂實作）來請求內容。 AEM GraphQL API可讓您對內容片段執行（複雜）查詢，每個查詢都根據特定的模型類型。

之後，您的應用程式就可以使用傳回的內容。

## 使用內容片段模型建立結構 {#create-structure-content-fragment-models}

內容片段模型提供多種機制，可讓您定義內容的結構。

內容片段模型描述實體。

>[!NOTE]
>您必須在「設定瀏覽器」中啟用「內容片段」功能，才能建立新模型。

>[!TIP]
>
>應命名模型，讓內容作者知道建立內容片段時要選取的模型。

在模型內：

1. **資料類型** 可讓您定義個別屬性。
例如，將保留教師姓名的欄位定義為 **文字** 和他們服役的年數 **數字**.
1. 資料類型 **內容參考** 和 **片段參考** 可讓您建立與AEM內其他內容的關係。
1. 此 **片段參考** 資料類型可讓您透過巢狀內容片段（根據模型類型）來實現多個層級的結構。 這對您的內容模型至關重要。

例如：
![使用內容片段的內容模型](assets/headless-modeling-01.png "使用內容片段的內容模型")

### 資料類型 {#data-types}

AEM提供下列資料類型，供您建立內容模型：

* 單行文字
* 多行文字
* 數量
* 布林值
* 日期時間
* 列舉
* 標記
* 內容參考資料
* 片段引用
* JSON 物件

### 參考和巢狀內容 {#references-nested-content}

兩種資料類型提供特定片段外部內容的參考：

* **內容參考**
這可提供任何類型之其他內容的簡單參考。
例如，您可以在指定的位置參考影像。

* **片段參考**
這可提供其他內容片段的參考。
此類型的參考用於建立巢狀內容，引入建立內容模型所需的關係。
資料類型可設定為允許片段作者：
   * 直接編輯參考的片段。
   * 根據適當的模型建立新內容片段

### 建立內容片段模型 {#creating-content-fragment-models}

您一開始需要為網站啟用內容片段模型，這是在設定瀏覽器中完成；在「工具」 — >「常規」 — >「配置瀏覽器」下。 您可以選取以設定全域項目，或建立新設定。 例如：

![定義配置](assets/cfm-configuration.png)

>[!NOTE]
>
>請參閱設定瀏覽器中的其他資源 — 內容片段

然後可建立內容片段模型並定義結構。 這可在「工具 — >資產 — >內容片段模型」下完成。 例如：

![內容片段模型](assets/cfm-model.png)

>[!NOTE]
>
>請參閱其他資源 — 內容片段模型。

## 使用模型製作內容片段 {#use-content-to-author-content}

內容片段一律以內容片段模型為基礎。 模型提供結構，片段包含內容。

### 選取適當的模型 {#select-model}

實際建立內容的第一步是建立內容片段。 這是使用「資產 — >檔案」下必要資料夾中的「建立 — >內容片段」來完成。 精靈會引導您完成步驟。

內容片段是以特定內容片段模型為基礎，您可選取該模型作為建立程式的第一步。

### 建立和編輯結構化內容 {#create-edit-structured-content}

建立片段後，您可以在內容片段編輯器中開啟它。 您可以在此：

* 以一般或全螢幕模式編輯內容。
* 將內容格式設為全文、純文字或Markdown。
* 建立和管理內容的變體。
* 關聯內容.
* 編輯中繼資料。
* 顯示樹結構。
* 預覽JSON表示法。

### 建立內容片段 {#creating-content-fragments}

選取適當的模型後，內容片段會在內容片段編輯器中開啟以進行編輯：

![內容片段編輯器](assets/cfm-editor.png)

>[!NOTE]
>
>請參閱其他資源 — 使用內容片段。

## 開始使用一些範例 {#getting-started-examples}

<!--
tbc...
...and/or see the structures covered for the GraphQL samples...
...will those (ever) be delivered as an official sample package?
-->

如需範例的基本結構，請參閱範例內容片段結構。

## 下一步 {#whats-next}

現在您已學習如何建立結構模型，並據此建立內容，下一步就是 [了解如何使用GraphQL查詢來存取和擷取您的內容片段內容](access-your-content.md). 這將介紹並討論GraphQL，然後查看一些示例查詢，以了解實際操作中的操作方式。

## 其他資源 {#additional-resources}

* [使用內容片段](/help/assets/content-fragments/content-fragments.md)  — 內容片段的進入頁面
   * [設定瀏覽器中的內容片段](/help/assets/content-fragments/content-fragments-configuration-browser.md)  — 在設定瀏覽器中啟用內容片段功能
   * [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)  — 建立和編輯內容片段模型
   * [管理內容片段](/help/assets/content-fragments/content-fragments-managing.md)  — 建立和編寫內容片段；本頁面將引導您進行其他詳細章節
* [AEM GraphQL結構](access-your-content.md) - GraphQL如何實現模型
* [範例內容片段結構](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)
* [AEM Headless快速入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html)  — 簡短的教學課程系列影片，概述如何使用AEM無周邊功能，包括內容模型和GraphQL
   * [GraphQL建模基本知識](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/video-series/modeling-basics.html)  — 了解如何定義和使用Adobe Experience Manager(AEM)中的內容片段，以便與GraphQL搭配使用。
