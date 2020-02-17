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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 網站範本 {#site-templates}

「網站範本」主控台與「群組範本」 [主控台非常類似](tools-groups.md) ，主控台著重於「社群」群組感興趣的功能。

>[!NOTE]
>
>用於建立社區站點的控 [制台](sites-console.md)、社 [區站點模板](sites.md)、 [社區組模板和社區功](tools-groups.md)[](functions.md) 能僅供作者環境使用。

## 網站範本主控台 {#site-templates-console}

在作者環境中，若要進入社群網站主控台

* 從全域導覽：工 **[!UICONTROL 具>社群>網站範本]**

此控制台顯示可從中創 [建社區站點](sites-console.md) 的模板，並允許建立新站點模板。

![chlimage_1-18](assets/chlimage_1-18.png)

## 建立網站範本 {#create-site-template}

若要開始建立新網站範本，請選取 `Create`。

這會顯示「網站編輯器」面板，其中包含3個子面板：

### Basic info {#basic-info}

![chlimage_1-19](assets/chlimage_1-19.png)

在「基本資訊」面板上，會設定名稱、說明以及範本是啟用還是停用：

* **[!UICONTROL 社群網站範本名稱]**&#x200B;範本名稱id

* **[!UICONTROL 社群網站範本說明]**&#x200B;範本說明

* **[!UICONTROL 禁用／啟用]**&#x200B;切換開關控制模板是否可引用

### 縮圖 {#thumbnail}

![chlimage_1-20](assets/chlimage_1-20.png)

（可選）選取「上傳影像」圖示，以便向社群網站的建立者顯示縮圖以及名稱和說明。

### 結構 {#structure}

![chlimage_1-21](assets/chlimage_1-21.png)

若要新增社群功能，請依網站功能表連結的顯示順序，從右側拖曳至左側。 在建立網站時，樣式會套用至範本。

例如，如果您想要首頁，請將「頁面」功能從程式庫拖曳至範本產生器下方。 這將導致開啟頁面配置對話框。 有關配置 [對話框的資訊](functions.md) ，請參見函式控制台。

根據此範本，繼續拖放社群網站所需的任何其他社群功能。

頁面函式提供空白頁面。 群組功能可讓您在社群網站中建立群組網站（子社群）。

>[!CAUTION]
>
>群組函式不 *能是**網站結構中的* 第一個函式，也不能是唯一函式。
>
>任何其他函式(例如頁 [面函式](functions.md#page-function))必須先包含並列出。

![chlimage_1-22](assets/chlimage_1-22.png)

### 群組範本功能 {#group-templates-for-groups-function}

在網站範本中包含群組功能時，設定需要指定在發佈環境中建立新群組時允許的群組範本選擇。

>[!CAUTION]
>
>Groups函式不 *能是**網站結構中的* 第一個函式，也不能是唯一函式。

![chlimage_1-23](assets/chlimage_1-23.png)

選擇兩個或兩個以上的社群群組範本後，當實際在社群中建立新群組時，群組管理員便可選擇。

![chlimage_1-24](assets/chlimage_1-24.png)

## 編輯網站範本{#edit-site-template}

在主網站範本主控台中檢 [視網站範本時](#site-templates-console)，可以選取現有的網站範本進行編輯。

此程式提供與建立網站范 [本相同的面板](#create-site-template)。
