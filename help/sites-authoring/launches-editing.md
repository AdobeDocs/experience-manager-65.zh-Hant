---
title: 編輯啟動
description: 為頁面（或頁面集）建立啟動後，可以在頁面啟動副本中編輯內容。
uuid: 1f2c2e53-73a3-4bd7-b2c7-425491bc0118
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 30aa3177-bcf4-4260-8f64-e73bc907942a
docset: aem65
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 2d441820-b394-47c8-b4ca-a8aede590937
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 18%

---

# 編輯 Launch{#editing-launches}

## 編輯啟動頁 {#editing-launch-pages}

為頁面（或一組頁面）建立啟動後，可以在頁面的啟動副本中編輯內容。

1. 訪問 [從引用啟動（站點控制台）](/help/sites-authoring/launches.md#launches-in-references-sites-console) 按鈕。
1. 選擇 **轉到頁面** 開啟頁面進行編輯。

>[!NOTE]
>
>不允許在啟動中移動頁面。 嘗試此操作將觸發警告消息：
>
>* 警告：此頁是啟動的源。 不允許移動頁面。


### 按即時副本編輯啟動頁面 {#editing-launch-pages-subject-to-a-live-copy}

如果您的發佈基於 [即時拷貝](/help/sites-administering/msm.md) 然後您將：

* 編輯元件（內容和/或屬性）時，請參閱鎖定符號（小掛鎖）。
* 查看 **即時拷貝** 頁籤 **頁面屬性**

livecopy可用來將來源 *分支的內容*** 同步到啟動分支 (以便讓啟動與來源中所做的變更保持最新)。

您可以以編輯標準即時副本的相同方式進行更改；例如：

* 按一下關閉的掛鎖將中斷此同步，並允許您在啟動時對內容進行新更新。 一旦解鎖（開啟掛鎖），您所做的更改將不會被源分支中同一位置所做的任何更改覆蓋。
* **暫停** (和 **繼續**)特定頁面的繼承。

請參閱 [更改即時拷貝內容](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) 的上界。

## 將啟動頁與其源頁進行比較 {#comparing-a-launch-page-to-its-source-page}

若要追蹤您所做的變更，您可以在「參考」中檢視啟動 **** ，並比較啟動頁面與其來源頁面：

1. 在 **站點** 控制台， [導航到啟動的源頁面並選擇它](/help/sites-authoring/basic-handling.md#viewingandselectingyourresources)。
1. 開啟 **[引用](/help/sites-authoring/basic-handling.md#references)** 選擇 **啟動**。
1. 選擇您的特定啟動 **與源比較**:

   ![screen-shot_2019-03-05at121952](assets/screen-shot_2019-03-05at121952.png)

1. 兩個頁面（啟動和源）將並排開啟。

   有關使用此功能的完整資訊，請參見 [頁面差異](/help/sites-authoring/page-diff.md)。

## 更改使用的源頁 {#changing-the-source-pages-used}

您可以隨時向源頁面範圍添加或從源頁面中刪除頁面，以便啟動：

1. 訪問並從以下任一位置選擇啟動：

   * 這樣 [啟動控制台](/help/sites-authoring/launches.md#the-launches-console):

      * 選取&#x200B;**編輯**。
   * [參考（站點控制台）](/help/sites-authoring/launches.md#launches-in-references-sites-console) 顯示可用操作：

      * 選擇 **編輯啟動**。

   將顯示源頁面。

1. 進行必要的變更，然後使用「儲存」 **確認**。

   >[!NOTE]
   >
   >要向發佈添加頁面，這些頁面必須位於公共語言根目錄下；即在單個站點內。

## 編輯啟動配置 {#editing-a-launch-configuration}

您可以隨時編輯啟動的屬性：

1. 訪問並從以下任一位置選擇啟動：

   * 這樣 [啟動控制台](/help/sites-authoring/launches.md#the-launches-console):

      * 選擇 **屬性**。
   * [參考（站點控制台）](/help/sites-authoring/launches.md#launches-in-references-sites-console) 顯示可用操作：

      * 選擇 **編輯屬性**。

   將顯示詳細資訊。

1. 進行必要的變更，然後使用「儲存」 **確認**。

   如需 [「啟動日期」和「生產就緒」欄位的用途和互動相關資訊，請參閱「啟動——事件順序」](/help/sites-authoring/launches.md#launches-the-order-of-events) (Launches - Order of Events ******** )。

## 發現頁面的啟動狀態 {#discovering-the-launch-status-of-a-page}

從「參照」(references)頁籤中選擇特定啟動時，將顯示狀態（請參閱） [在引用（站點控制台）中啟動](/help/sites-authoring/launches.md#launches-in-references-sites-console))。

![螢幕抓拍_2019-03-05at121901](assets/screen-shot_2019-03-05at121901.png)
