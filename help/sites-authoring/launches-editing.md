---
title: 編輯啟動
description: 為您的頁面（或一組頁面）建立啟動後，您可以在頁面的啟動副本中編輯內容。
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 2d441820-b394-47c8-b4ca-a8aede590937
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Launches
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 18%

---

# 編輯啟動{#editing-launches}

## 編輯啟動頁面 {#editing-launch-pages}

建立頁面（或一組頁面）的啟動後，您可以在頁面的啟動副本中編輯內容。

1. 從[參考] （網站主控台）](/help/sites-authoring/launches.md#launches-in-references-sites-console)存取[啟動項，以顯示可用的動作。
1. 選取&#x200B;**移至頁面**&#x200B;以開啟要編輯的頁面。

>[!NOTE]
>
>您不能在啟動項中移動頁面。 嘗試此動作將觸發警告訊息：
>
>* 警告：此頁面是啟動項的來源。 不允許移動頁面。

### 編輯以即時副本為主題的啟動頁面 {#editing-launch-pages-subject-to-a-live-copy}

如果您的啟動項以[即時副本](/help/sites-administering/msm.md)為基礎，則您將：

* 編輯元件（內容和/或屬性）時，請參閱鎖定元件（小掛鎖）。
* 檢視&#x200B;**頁面屬性**&#x200B;中的&#x200B;**即時副本**&#x200B;索引標籤

livecopy可用來將來源 *分支的內容*** 同步到啟動分支 (以便讓啟動與來源中所做的變更保持最新)。

您可以使用與編輯標準即時副本相同的方式進行變更；例如：

* 按一下已關閉的掛鎖將會中斷此同步作業，並讓您對啟動項中的內容進行新的更新。 解除鎖定（開啟掛鎖）後，在來源分支內的相同位置所做的任何變更都不會覆寫您的變更。
* **暫停** (和 **繼續**)特定頁面的繼承。

如需進一步資訊，請參閱[變更即時副本內容](/help/sites-administering/msm-livecopy.md#changing-live-copy-content)。

## 比較Launch頁面與其Source頁面 {#comparing-a-launch-page-to-its-source-page}

若要追蹤您所做的變更，您可以在「參考」中檢視啟動 **** ，並比較啟動頁面與其來源頁面：

1. 在&#x200B;**網站**&#x200B;主控台中，[導覽至啟動項的來源頁面，並選取它](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources)。
1. 開啟&#x200B;**[參考](/help/sites-authoring/basic-handling.md#references)**&#x200B;面板，然後選取&#x200B;**啟動**。
1. 選取您的特定啟動，然後&#x200B;**與Source比較**：

   ![screen-shot_2019-03-05at121952](assets/screen-shot_2019-03-05at121952.png)

1. 兩個頁面（啟動項和來源）將並排開啟。

   如需有關使用此功能的完整資訊，請參閱[頁面差異](/help/sites-authoring/page-diff.md)。

## 變更使用的Source頁面 {#changing-the-source-pages-used}

您隨時可以在啟動項的來源頁面範圍中，新增或移除頁面：

1. 從下列任一位置存取並選取啟動：

   * [啟動主控台](/help/sites-authoring/launches.md#the-launches-console)：

      * 選取&#x200B;**編輯**。

   * [參考（網站主控台）](/help/sites-authoring/launches.md#launches-in-references-sites-console)以顯示可用的動作：

      * 選取&#x200B;**編輯啟動項**。

   此時會顯示來源頁面。

1. 進行必要的變更，然後使用「儲存」 **確認**。

   >[!NOTE]
   >
   >若要將頁面新增至啟動，這些頁面必須位於共同語言根目錄下；也就是說，在單一網站內。

## 編輯啟動設定 {#editing-a-launch-configuration}

您隨時可以編輯啟動項的屬性：

1. 從下列任一位置存取並選取啟動：

   * [啟動主控台](/help/sites-authoring/launches.md#the-launches-console)：

      * 選取&#x200B;**屬性**。

   * [參考（網站主控台）](/help/sites-authoring/launches.md#launches-in-references-sites-console)以顯示可用的動作：

      * 選取&#x200B;**編輯屬性**。

   詳細資訊隨即顯示。

1. 進行必要的變更，然後使用「儲存」 **確認**。

   如需 [「啟動日期」和「生產就緒」欄位的用途和互動相關資訊，請參閱「啟動——事件順序」](/help/sites-authoring/launches.md#launches-the-order-of-events) (Launches - Order of Events ******** )。

## 探索頁面的啟動狀態 {#discovering-the-launch-status-of-a-page}

當您從「參考」(References)標籤選取特定啟動時，會顯示狀態(請參閱「參考」(Sites Console)](/help/sites-authoring/launches.md#launches-in-references-sites-console)中的[啟動)。

![screen-shot_2019-03-05at121901](assets/screen-shot_2019-03-05at121901.png)
