---
title: 群組範本
seo-title: Group Templates
description: 如何存取群組範本主控台
seo-description: How to access the Group Templates console
uuid: 4cf20c91-32b0-4051-a98d-44e4eb50a231
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e9bfbbce-93fc-455c-a2f7-4ee44e63c03f
docset: aem65
role: Admin
exl-id: aed2c3f2-1b5e-4065-8cec-433abb738ef5
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 3%

---

# 群組範本 {#group-templates}

「群組範本」主控台類似於 [網站範本](/help/communities/sites.md) 控制台。 這兩者都是構成社區站點的一組預佈線頁面和功能的藍圖。 區別在於，網站範本是用於主要社群，而群組範本是用於社群群組（巢狀內嵌於主要社群中的子社群）。

社群群組已整合至網站範本，方法是將 [組函式](/help/communities/functions.md#groups-function) （這不能是範本中的第一個或唯一函式）。

As of Communities [功能包1](/help/communities/deploy-communities.md#latestfeaturepack)，則可在群組範本中加入「群組」函式，以巢狀內嵌群組。

當採取動作建立新社群群組時，即會選取群組的範本（結構）。 選擇取決於將「組」功能添加到站點或組模板時的配置方式。

>[!NOTE]
>
>建立 [社群網站](/help/communities/sites-console.md), [社群網站範本](/help/communities/sites.md), [社群群組範本](/help/communities/tools-groups.md) 和 [社群功能](/help/communities/functions.md) 僅供製作環境使用。

## 群組範本主控台 {#group-templates-console}

若要存取AEM製作環境中的群組範本主控台：

* 選擇 **工具 |社群 |組模板，** 從全局導航。

此主控台會顯示 [社群網站](/help/communities/sites-console.md) 可以建立，並允許建立新的群組範本。

![社群群組範本](assets/groups-template.png)

## 建立群組範本 {#create-group-template}

若要開始建立新群組範本，請選取 `Create`.

這會顯示包含3個子面板的網站編輯器面板：

### 基本資訊 {#basic-info}

![site-basic-info](assets/site-basic-info.png)

在「基本資訊」面板上，會設定名稱、說明，以及範本是否啟用或停用：

* **新群組範本名稱**

   範本名稱id。

* **說明**

   範本說明。

* **禁用/啟用**

   控制模板是否可引用的切換開關。

#### 縮圖 {#thumbnail}

![網站縮圖](assets/site-thumbnail.png)

（可選）選取「上傳影像」圖示，向社群網站的建立者顯示縮圖以及名稱和說明。

#### 結構 {#structure}

>[!CAUTION]
>
>若使用AEM 6.1 Communities FP4或更舊版本，請勿將群組函式新增至群組範本。
>
>巢狀群組功能可從Communities開始使用 [FP1](/help/communities/communities.md#latestfeaturepack).
>
>仍不允許將群組函式新增為範本中的第一個或唯一的函式。

![群組範本編輯器](assets/template-editor.png)

若要新增社群功能，請依網站功能表連結的顯示順序從右側拖曳至左側。 建立網站時，樣式會套用至範本。

例如，如果您想要論壇，請從程式庫拖曳論壇函式，放置到範本產生器下。 這會導致論壇設定對話方塊開啟。 請參閱 [函式主控台](/help/communities/functions.md) ，了解有關配置對話框的資訊。

根據此範本，繼續拖放子社群網站（群組）所需的任何其他社群功能。

![拖曳函式](assets/dragfunctions.png)

將所有所需函式拖放至範本產生器區域並完成設定後，請選取 **儲存** 在右上角。

## 編輯群組範本 {#edit-group-template}

在主目錄中檢視社群群組時 [群組範本主控台](#group-templates-console)，您可以選取現有的群組範本進行編輯。

編輯群組範本不會影響已從範本建立的社群網站。 可以直接 [編輯社群網站](/help/communities/sites-console.md#modify-structure)的結構。

此程式提供與 [建立群組範本](#create-group-template).
