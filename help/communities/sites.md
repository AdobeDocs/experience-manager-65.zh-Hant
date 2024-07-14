---
title: 網站範本
description: 瞭解如何存取「網站範本」主控台以建立社群網站。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 05a944a3-adb1-47b4-b4a5-15bac91c995e
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 3%

---

# 網站範本 {#site-templates}

「網站範本」主控台類似於[群組範本](tools-groups.md)主控台，其著重於社群群組感興趣的功能。

>[!NOTE]
>
>建立[社群網站](sites-console.md)、[社群網站範本](sites.md)、[社群群組範本](tools-groups.md)及[社群功能](functions.md)的主控台僅供作者環境使用。

## 網站範本主控台 {#site-templates-console}

在作者環境中，若要存取社群網站主控台：

* 從全域導覽： **[!UICONTROL 工具>社群>網站範本]**

此主控台顯示可從中建立[社群網站](sites-console.md)的範本，並允許建立新的網站範本。

![網站範本](assets/site-template.png)

## 建立網站範本 {#create-site-template}

若要開始建立網站範本，請選取`Create`。

這會開啟包含三個子面板的「網站編輯器」面板：

### 基本資訊 {#basic-info}

![site-template-basicinfo](assets/site-template-basicinfo.png)

在「基本資訊」面板上，會設定名稱、說明，以及範本是啟用還是停用：

* **[!UICONTROL 社群網站範本名稱]**

  範本名稱識別碼。

* **[!UICONTROL 社群網站範本描述]**

  範本說明。

* **[!UICONTROL 已停用/已啟用]**

  控制範本是否可參照的切換開關。

### 縮圖 {#thumbnail}

![網站縮圖](assets/site-thumbnail.png)

（可選）選取「上傳影像」圖示以顯示縮圖，以及社群網站建立者的名稱和說明。

### 結構 {#structure}

![站台結構](assets/site-structure.png)

若要新增社群功能，請從右側向左拖曳網站功能表連結，其顯示順序如下： 樣式會在建立網站期間套用至範本。

例如，如果您想要首頁，請從資料庫拖曳「頁面」函式，放置於範本產生器下。 這會導致頁面設定對話方塊開啟。 如需有關設定對話方塊的資訊，請參閱[函式主控台](functions.md)。

根據此範本，繼續拖放社群網站所需的任何其他社群功能。

page函式提供空白頁面。 「群組」功能可讓您在社群網站內建立群組網站（子社群）。

>[!CAUTION]
>
>Groups函式不得&#x200B;*是網站結構中的第一個或唯一的*&#x200B;函式。
>
>必須包含其他任何函式，例如[頁面函式](functions.md#page-function)，並先列出。

![網站編輯器](assets/site-editor.png)

### 群組功能的群組範本 {#group-templates-for-groups-function}

在場地範本中加入「群組」功能時，組態需要指定在發佈環境中建立新群組時允許的群組範本選擇。

>[!CAUTION]
>
>Groups函式不得&#x200B;*是網站結構中的第一個或唯一的*&#x200B;函式。

![站台函式](assets/site-functions.png)

選取兩個或多個社群群組範本，可在社群中實際建立群組時，為群組管理員提供選項。

![站台函式](assets/site-functions1.png)

## 編輯網站範本 {#edit-site-template}

在主[網站範本主控台](#site-templates-console)中檢視網站範本時，可以選取現有的網站範本進行編輯。

此程式提供與[建立網站範本](#create-site-template)相同的面板。
