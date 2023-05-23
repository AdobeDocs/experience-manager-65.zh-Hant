---
title: 編輯內容頁面時的注釋
description: 許多與內容直接相關的元件允許您添加註釋。
uuid: 157be55c-8ab8-472e-be32-0dcc02bfa41d
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: aa89326a-ad33-4b0b-8d09-c68c5a5c790a
exl-id: de1ae7e3-db3a-4b5e-8a4f-ae111227181f
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# 編輯頁面時的注釋{#annotations-when-editing-a-page}

將內容添加到網站的頁面通常需要在實際發佈之前進行討論。 為此，許多直接與內容相關的元件（例如，佈局）允許您添加註釋。

批注將在頁面上放置彩色標籤/便箋。 該注釋允許您（或其他用戶）為其他作者/審閱者留下注釋和/或問題。

>[!NOTE]
>
>單個元件類型的定義確定是否可能（或否）在該元件實例上添加註釋。

>[!NOTE]
>
>在傳統用戶介面中建立的注釋將顯示在啟用觸摸的用戶介面中。 但草繪是特定於UI的，它們只顯示在建立它們的UI中。

>[!CAUTION]
>
>刪除資源（如段落）會刪除附加到該資源的所有注釋和草繪，而不管它們在整個頁面上的位置如何。

>[!NOTE]
>
>根據您的要求，您還可以開發一個工作流，以便在添加、更新或刪除注釋時發送通知。

## 註解 {#annotations}

特殊 [模式](/help/sites-authoring/author-environment-tools.md#page-modes) 用於建立和查看注釋。

>[!NOTE]
>
>別忘了 [評論](/help/sites-authoring/basic-handling.md#timeline) 也可用於在頁面上提供反饋。

>[!NOTE]
>
>可以注釋各種資源：
>
>* [注釋資產](/help/assets/manage-assets.md#annotating)
>* [注釋視頻資產](/help/assets/managing-video-assets.md#annotate-video-assets)
>


### 注釋元件 {#annotating-a-component}

「注釋」(Annotate)模式允許您在內容上建立、編輯、移動或刪除注釋：

1. 編輯頁面時，可使用工具欄（右上）中的表徵圖進入「注釋」模式：

   ![](do-not-localize/screen_shot_2018-03-22at110414.png)

   現在，您可以查看任何現有批注。

   >[!NOTE]
   >
   >要退出「注釋」模式，請點擊/按一下頂部工具欄右側的「注釋」表徵圖（x符號）。

1. 按一下/點擊「添加註釋」表徵圖（工具欄左側的加號）開始添加註釋。

   >[!NOTE]
   >
   >要停止添加註釋（並返回查看），請點擊/按一下頂部工具欄左側的「取消」表徵圖（白色圓圈中的x符號）。

1. 按一下/點擊所需元件（可注釋的元件將用藍色邊框加亮）以添加註釋並開啟對話框：

   ![screen_shot_2018-03-22at110606](assets/screen_shot_2018-03-22at110606.png)

   在此，您可以使用相應的欄位和/或表徵圖：

   * 輸入注釋文本。
   * 建立草繪（線和形狀）以加亮元件的區域。

      建立草繪時，游標將變為交叉線。 可以繪製多條不同的線條。 草繪線反映注釋顏色，可以是箭頭、圓或橢圓。
   ![](do-not-localize/screen_shot_2018-03-22at110640.png)

   * 選擇/更改顏色：

   ![](do-not-localize/chlimage_1-19.png)

   * 刪除注釋。

   ![](do-not-localize/screen_shot_2018-03-22at110647.png)

1. 可通過按一下/在對話框外部點擊來關閉注釋對話框。 注釋的截斷視圖（第一個字）以及任何草繪顯示如下：

   ![screen_shot_2018-03-22at110850](assets/screen_shot_2018-03-22at110850.png)

1. 編輯完特定注釋後，可以：

   * 按一下/點擊文本標籤以開啟注釋。 開啟後，您可以查看全文、更改或刪除注釋。

      * 無法獨立於注釋刪除草繪。
   * 重新定位文本標籤。
   * 按一下/點擊草繪線以選取該草繪並將其拖動到所需位置。
   * 移動或複製元件

      * 任何相關注釋及其草圖也將被移動或複製，它們相對於段落的位置將保持不變。


1. 要退出「注釋」模式並返回到先前使用的模式，請點擊/按一下頂部工具欄右側的「注釋」表徵圖（x符號）。

>[!NOTE]
>
>無法將批注添加到已由其他用戶鎖定的頁面。

### 注釋指示器 {#annotation-indicator}

注釋不會在「編輯」模式下顯示，但工具欄右上角的標籤顯示當前頁面存在多少注釋。 標籤將替換預設的「注釋」表徵圖，但仍作為快速連結使用，可切換到/從「注釋」模式：

![chlimage_1-242](assets/chlimage_1-242.png)
