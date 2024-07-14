---
title: 群組範本
description: 瞭解如何存取群組範本主控台，以存取一組可形成社群網站的預先有線頁面和功能。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: aed2c3f2-1b5e-4065-8cec-433abb738ef5
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 2%

---

# 群組範本 {#group-templates}

群組範本主控台類似於[網站範本](/help/communities/sites.md)主控台。 兩者都是組成社群網站的一組預佈線頁面和功能的藍圖。 其差異在於網站範本適用於主要社群，而群組範本適用於社群群組，即巢狀內嵌於主要社群的子社群。

加入[群組函式](/help/communities/functions.md#groups-function) （可能不是範本中的第一個或唯一函式），便將社群群組合併到網站範本中。

從Communities [功能套件1](/help/communities/deploy-communities.md#latestfeaturepack)開始，只要在群組範本中加入Groups函式，就可以巢狀內嵌群組。

執行動作建立社群群組時，即會選取群組的範本（結構）。 選取範圍取決於群組功能新增至網站或群組範本時的設定方式。

>[!NOTE]
>
>建立[社群網站](/help/communities/sites-console.md)、[社群網站範本](/help/communities/sites.md)、[社群群組範本](/help/communities/tools-groups.md)及[社群功能](/help/communities/functions.md)的主控台僅供作者環境使用。

## 群組範本主控台 {#group-templates-console}

若要在AEM作者環境中存取群組範本主控台：

* 選取&#x200B;**工具 | Communities | 群組範本，**&#x200B;來自全域導覽。

此主控台顯示可從中建立[社群網站](/help/communities/sites-console.md)的範本，並允許建立新的群組範本。

![社群群組範本](assets/groups-template.png)

## 建立群組範本 {#create-group-template}

若要開始建立群組範本，請選取`Create`。

這會顯示包含三個子面板的「網站編輯器」面板：

### 基本資訊 {#basic-info}

![site-basic-info](assets/site-basic-info.png)

在「基本資訊」面板上，會設定名稱、說明，以及範本是啟用還是停用：

* **新群組範本名稱**

  範本名稱識別碼。

* **說明**

  範本說明。

* **已停用/已啟用**

  控制範本是否可參照的切換開關。

#### 縮圖 {#thumbnail}

![網站縮圖](assets/site-thumbnail.png)

（選用）選取「上傳影像」圖示，向社群網站建立者顯示縮圖以及名稱和說明。

#### 結構 {#structure}

>[!CAUTION]
>
>如果使用AEM 6.1 Communities FP4或較舊版本，請勿將群組功能新增至群組範本。
>
>巢狀群組功能自Communities [FP1](/help/communities/communities.md#latestfeaturepack)起即可使用。
>
>仍不允許將「群組」函式新增為範本中的第一個或唯一函式。

![群組範本編輯器](assets/template-editor.png)

若要新增社群功能，請從右側向左拖曳網站功能表連結，其顯示順序如下： 樣式會在建立網站期間套用至範本。

例如，如果您想要論壇，請從資料庫拖曳論壇功能，然後放置在範本產生器下。 這將導致論壇設定對話方塊開啟。 如需有關設定對話方塊的資訊，請參閱[函式主控台](/help/communities/functions.md)。

根據此範本，繼續拖放子社群網站（群組）所需的任何其他社群功能。

![拖曳函式](assets/dragfunctions.png)

將所有需要的功能放入範本產生器區域並設定後，選取右上角的&#x200B;**儲存**。

## 編輯群組範本 {#edit-group-template}

在主[群組範本主控台](#group-templates-console)中檢視社群群組時，可以選取現有的群組範本進行編輯。

編輯群組範本不會影響已從範本建立的社群網站。 您可以直接[編輯社群網站](/help/communities/sites-console.md#modify-structure)的結構。

此程式提供與[建立群組範本](#create-group-template)相同的面板。
