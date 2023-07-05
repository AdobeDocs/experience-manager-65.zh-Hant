---
title: 編輯內容頁面時的註解
description: 許多與內容直接相關的元件可讓您新增附註。
uuid: 157be55c-8ab8-472e-be32-0dcc02bfa41d
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: aa89326a-ad33-4b0b-8d09-c68c5a5c790a
exl-id: de1ae7e3-db3a-4b5e-8a4f-ae111227181f
source-git-commit: e85aacd45a2bbc38f10d03915e68286f0a55364e
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 0%

---

# 編輯頁面時的註解{#annotations-when-editing-a-page}

在實際發佈內容之前，通常需要先進行討論，才能將內容新增至網站的頁面。 為了協助此功能，許多與內容直接相關的元件（例如，與版面配置相反）可讓您新增附註。

註解會在頁面上放置彩色標籤/註解。 註解可讓您（或其他使用者）為其他作者/檢閱者留下評論及/或問題。

>[!NOTE]
>
>個別元件型別的定義會決定是否可在該元件的例證上新增註釋。

>[!NOTE]
>
>在傳統UI中建立的註解將顯示在觸控式UI中。 不過，草圖是UI專屬的，而且只會在建立草圖的UI中顯示。

>[!CAUTION]
>
>刪除資源（例如段落）會刪除附加到該資源的所有註釋和草圖，無論這些註釋和草圖在整個頁面上的位置為何。

>[!NOTE]
>
>您也可以根據您的需求，開發工作流程，以便在新增、更新或刪除註解時傳送通知。

## 註解 {#annotations}

特殊 [模式](/help/sites-authoring/author-environment-tools.md#page-modes) 用於建立和檢視註解。

>[!NOTE]
>
>別忘了 [評論](/help/sites-authoring/basic-handling.md#timeline) 也可在頁面上提供意見回饋。

>[!NOTE]
>
>您可以為各種資源加上註解：
>
>* [為資產加上註釋](/help/assets/manage-assets.md#annotating)
>* [為視訊資產加上註釋](/help/assets/managing-video-assets.md#annotate-video-assets)
>

### 為元件加上註釋 {#annotating-a-component}

「註釋」模式可讓您在內容上建立、編輯、移動或刪除註釋：

1. 編輯頁面時，您可以使用工具列（右上方）中的圖示來進入附註模式：

   ![注釋](do-not-localize/screen_shot_2018-03-22at110414.png)

   您現在可以檢視任何現有的註解。

   >[!NOTE]
   >
   >若要退出「註釋」模式，請點選/按一下頂端工具列右側的「註釋」圖示（x符號）。

1. 按一下/點選「新增註釋」圖示（工具列左側的加號）以開始新增註釋。

   >[!NOTE]
   >
   >若要停止新增註解（並返回檢視），請點選/按一下頂端工具列左側的「取消」圖示（白色圓圈中的x符號）。

1. 按一下/點選所需的元件（可加上註解的元件將以藍色邊框反白顯示）以新增註解，然後開啟對話方塊：

   ![screen_shot_2018-03-22at110606](assets/screen_shot_2018-03-22at110606.png)

   在這裡，您可以使用適當的欄位和/或圖示來：

   * 輸入註釋文字。
   * 建立草繪（線條和形狀）以反白元件的某個區域。

     建立草繪時，游標會變成十字線。 您可以繪製多條不同的線條。 草繪線會反映註釋顏色，可以是箭頭、圓圈或橢圓形。

     ![素描](do-not-localize/screen_shot_2018-03-22at110640.png)

   * 選擇/變更色彩：

     ![選擇/變更色彩](do-not-localize/chlimage_1-19.png)

   * 刪除註解。

     ![刪除註解](do-not-localize/screen_shot_2018-03-22at110647.png)

1. 您可以按一下/點選註釋對話方塊，關閉對話方塊。 隨即顯示截斷的註釋檢視（第一個字）以及任何草圖：

   ![screen_shot_2018-03-22at110850](assets/screen_shot_2018-03-22at110850.png)

1. 編輯完特定註解後，您可以：

   * 按一下/點選文字標籤以開啟附註。 開啟後，您可以檢視全文、進行變更或刪除註釋。

      * 不能獨立於註釋刪除草圖。

   * 重新定位文字標籤。
   * 按一下/點選草圖線以選取該草圖，並將其拖曳至所需位置。
   * 移動或複製元件

      * 任何相關的註釋及其草繪也會移動或複製，而且它們相對於段落的位置將保持不變。

1. 若要退出「註釋」模式並返回先前使用的模式，請點選/按一下頂端工具列右側的「註釋」圖示（x符號）。

>[!NOTE]
>
>註解無法新增至已由其他使用者鎖定的頁面。

### 附註指示器 {#annotation-indicator}

註解不會出現在編輯模式中，但工具列右上方的徽章會顯示目前頁面有多少注解。 徽章會取代預設的「註解」圖示，但仍可作為快速連結來切換至/自「註解」模式：

![註解指示器](assets/chlimage_1-242.png)
