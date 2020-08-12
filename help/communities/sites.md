---
title: 網站範本
seo-title: 網站範本
description: 如何存取網站範本主控台
seo-description: 如何存取網站範本主控台
uuid: d2f7556e-7e43-424e-82f1-41790aeb2d98
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 202d7dba-2b34-431d-b10f-87775632807f
translation-type: tm+mt
source-git-commit: 6ab91667ad668abf80ccf1710966169b3a187928
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 4%

---


# 網站範本 {#site-templates}

「網站範本」主控台與「群組範本」 [主控台非常類似](tools-groups.md) ，主控台著重於「社群」群組感興趣的功能。

>[!NOTE]
>
>用於建立社區站點的控 [制台](sites-console.md)、社 [區站點模板](sites.md)、 [社區組模板和社](tools-groups.md)[](functions.md) 區功能僅在作者環境中使用。


## 網站範本主控台 {#site-templates-console}

在作者環境中，若要進入社群網站主控台：

* 從全域導覽： **[!UICONTROL 工具>社群>網站範本]**

此控制台顯示可從中創 [建社區站點](sites-console.md) 的模板，並允許建立新站點模板。

![站點模板](assets/site-template.png)

## 建立網站範本 {#create-site-template}

若要開始建立新網站範本，請選取 `Create`。

這會顯示「網站編輯器」面板，其中包含3個子面板：

### Basic info {#basic-info}

![site-template-basicinfo](assets/site-template-basicinfo.png)

在「基本資訊」面板上，會設定名稱、說明以及範本是啟用還是停用：

* **[!UICONTROL 社群網站範本名稱]**

   範本名稱ID。

* **[!UICONTROL 社群網站範本說明]**

   範本說明。

* **[!UICONTROL 已禁用／啟用]**

   控制模板是否可引用的切換開關。

### 縮圖 {#thumbnail}

![site-thumbnail](assets/site-thumbnail.png)

（可選）選取「上傳影像」圖示，以便向社群網站的建立者顯示縮圖以及名稱和說明。

### 結構 {#structure}

![網站結構](assets/site-structure.png)

若要新增社群功能，請依網站功能表連結的顯示順序，從右側拖曳至左側。 在建立網站時，樣式會套用至範本。

例如，如果您想要首頁，請將「頁面」功能從程式庫拖曳至範本產生器下方。 這將導致開啟頁面配置對話框。 有關配置 [對話框的資訊](functions.md) ，請參見函式控制台。

根據此範本，繼續拖放社群網站所需的任何其他社群功能。

頁面函式提供空白頁面。 群組功能可讓您在社群網站中建立群組網站（子社群）。

>[!CAUTION]
>
>群組函式不 *能是**網站結構中的* 第一個函式，也不能是唯一函式。
>
>任何其他函式(例如頁 [面函式](functions.md#page-function))必須先包含並列出。


![站點編輯器](assets/site-editor.png)

### 群組範本功能 {#group-templates-for-groups-function}

在網站範本中包含群組功能時，設定需要指定在發佈環境中建立新群組時允許的群組範本選擇。

>[!CAUTION]
>
>Groups函式不 *能是**網站結構中的* 第一個函式，也不能是唯一函式。


![站點功能](assets/site-functions.png)

選擇兩個或兩個以上的社群群組範本後，當實際在社群中建立新群組時，群組管理員便可選擇。

![site-function](assets/site-functions1.png)

## 編輯網站範本{#edit-site-template}

在主網站範本主控台中檢 [視網站範本時](#site-templates-console)，可以選取現有的網站範本進行編輯。

此程式提供與建立網站范 [本相同的面板](#create-site-template)。
