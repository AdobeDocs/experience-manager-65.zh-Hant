---
title: 在We.Retail中試用回應式版面
description: 瞭解如何使用We.Retail在Adobe Experience Manager中試用回應式版面。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 6df5fb10-a7f1-4d5d-ac00-b4be3d5d3d18
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 4%

---

# 在We.Retail中試用回應式版面{#trying-out-responsive-layout-in-we-retail}

所有We.Retail頁面都會使用版面容器元件，以實施回應式設計。 版面容器提供段落系統，讓您在回應式格線內放置元件。 此格線可根據裝置/視窗大小和格式重新排列版面。 此元件與頁面編輯器中的&#x200B;**配置**&#x200B;模式搭配使用，可讓您建立和編輯相依於裝置的回應式配置。

## 正在試用中 {#trying-it-out}

1. 編輯語言主分支體驗區段中的「北極地區衝浪」頁面。

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html

1. 切換至&#x200B;**預覽**，檢視呈現給網站訪客的頁面。 向下捲動至文章&#x200B;*Norther Norway的Aloha spirits*&#x200B;內容。

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. 重新調整瀏覽器視窗大小，並在版面動態調整大小時觀看。

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. 切換到佈局模式。 模擬器工具列會自動顯示，可讓您針對每個目標裝置規劃版面。

   選取元件時，會在「編輯」選單中顯示浮動和隱藏選項，以及調整元件操作框的大小。

   ![chlimage_1-180](assets/chlimage_1-180.png)

1. 抓取並拖曳元件的調整大小控點會自動顯示版面格點，協助您調整大小。

   ![chlimage_1-181](assets/chlimage_1-181.png)

## 更多資訊 {#further-information}

如需詳細資訊，請參閱撰寫檔案[回應式配置](/help/sites-authoring/responsive-layout.md)或管理員檔案[設定配置容器和配置模式](/help/sites-administering/configuring-responsive-layout.md)，以取得完整的技術細節。
