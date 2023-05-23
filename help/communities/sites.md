---
title: 網站範本
seo-title: Site Templates
description: 如何訪問站點模板控制台
seo-description: How to access the Site Templates console
uuid: d2f7556e-7e43-424e-82f1-41790aeb2d98
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 202d7dba-2b34-431d-b10f-87775632807f
role: Admin
exl-id: 05a944a3-adb1-47b4-b4a5-15bac91c995e
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 4%

---

# 網站範本 {#site-templates}

站點模板控制台與 [組模板](tools-groups.md) console，它側重於社區組所關心的功能。

>[!NOTE]
>
>用於建立 [社區站點](sites-console.md)。 [社區網站模板](sites.md)。 [社區組模板](tools-groups.md) 和 [社區功能](functions.md) 僅在作者環境中使用。

## 站點模板控制台 {#site-templates-console}

在作者環境中，要訪問社區站點控制台：

* 從全局導航： **[!UICONTROL 工具>社區>站點模板]**

此控制台顯示 [社區站點](sites-console.md) 可以建立並允許建立新的站點模板。

![站點模板](assets/site-template.png)

## 建立網站範本 {#create-site-template}

要開始建立新網站模板，請選擇 `Create`。

這將顯示包含3個子面板的「站點編輯器」面板：

### 基本資訊 {#basic-info}

![站點模板 — basicinfo](assets/site-template-basicinfo.png)

在「基本資訊」面板上，配置了名稱、說明以及模板是啟用還是禁用：

* **[!UICONTROL 社群網站範本名稱]**

   模板名稱ID。

* **[!UICONTROL 社群網站範本說明]**

   模板說明。

* **[!UICONTROL 已禁用/已啟用]**

   控制模板是否可引用的切換開關。

### 縮圖 {#thumbnail}

![站點縮略圖](assets/site-thumbnail.png)

（可選）選擇「上載影像」表徵圖，以向社區網站的建立者顯示縮略圖以及名稱和說明。

### 結構 {#structure}

![站點結構](assets/site-structure.png)

要添加社區功能，請按站點菜單連結的顯示順序從右側向左拖動。 在建立站點期間，樣式將應用於模板。

例如，如果想要首頁，請將「頁面」功能從庫中拖放到模板生成器下。 這將導致開啟頁面配置對話框。 查看 [函式控制台](functions.md) 的子菜單。

根據此模板繼續拖放社區站點所需的任何其他社區功能。

頁函式提供空頁。 組功能提供了在社區站點內建立組站點（子社區）的功能。

>[!CAUTION]
>
>組函式必須 *不* 是 *第一，也是唯一* 的子菜單。
>
>任何其他函式，如 [頁面函式](functions.md#page-function)，必須先包括並列出。

![站點編輯器](assets/site-editor.png)

### 組模板功能 {#group-templates-for-groups-function}

在站點模板中包括組功能時，配置要求指定在發佈環境中建立新組時允許的組模板選項。

>[!CAUTION]
>
>「組」函式必須 *不* 是 *第一，也是唯一* 的子菜單。

![站點函式](assets/site-functions.png)

通過選擇兩個或多個社區組模板，在社區中實際建立新組時，將向組管理員提供一個選項。

![站點函式](assets/site-functions1.png)

## 編輯網站範本 {#edit-site-template}

在主目錄中查看站點模板時 [站點模板控制台](#site-templates-console)，可以選擇現有網站模板進行編輯。

此過程提供與 [建立網站模板](#create-site-template)。
