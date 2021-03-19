---
title: 群組範本
seo-title: 群組範本
description: 如何存取群組範本主控台
seo-description: 如何存取群組範本主控台
uuid: 4cf20c91-32b0-4051-a98d-44e4eb50a231
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e9bfbbce-93fc-455c-a2f7-4ee44e63c03f
docset: aem65
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 4%

---


# 群組範本 {#group-templates}

群組範本主控台類似於[網站範本](/help/communities/sites.md)主控台。 兩者都是構成社群網站的預先連線頁面和功能的藍圖。 區別在於，網站範本是主社群的範本，而群組範本是社群群組（主社群內巢狀的子社群）的範本。

社區組通過包括[Groups函式](/help/communities/functions.md#groups-function)（該函式可能不是模板中的第一個或唯一的函式）而合併到站點模板中。

從Communities [功能套件1](/help/communities/deploy-communities.md#latestfeaturepack)開始，您就可將群組功能加入群組範本中，以巢狀內嵌群組。

當採取動作建立新社群群組時，就會選取群組的範本（結構）。 選取範圍取決於新增至網站或群組範本時，群組功能的設定方式。

>[!NOTE]
>
>用於建立[社區站點](/help/communities/sites-console.md)、[社區站點模板](/help/communities/sites.md)、[社區組模板](/help/communities/tools-groups.md)和[社區功能](/help/communities/functions.md)的控制台僅用於作者環境。

## 群組範本主控台{#group-templates-console}

若要觸及AEM Author環境中的群組範本主控台：

* 選擇&#x200B;**工具 |社群 |群組範本，**&#x200B;來自全域導覽。

此控制台顯示可從中建立[社區站點](/help/communities/sites-console.md)的模板，並允許建立新的組模板。

![社群群組範本](assets/groups-template.png)

## 建立群組範本 {#create-group-template}

若要開始建立新的群組範本，請選取`Create`。

這會顯示「網站編輯器」面板，其中包含3個子面板：

### 基本資訊 {#basic-info}

![site-basic-info](assets/site-basic-info.png)

在「基本資訊」面板上，會設定名稱、說明以及範本是啟用還是停用：

* **新群組範本名稱**

   範本名稱ID。

* **說明**

   範本說明。

* **已禁用／啟用**

   控制模板是否可引用的切換開關。

#### 縮圖 {#thumbnail}

![site-thumbnail](assets/site-thumbnail.png)

（可選）選取「上傳影像」圖示，向社群網站的建立者顯示縮圖以及名稱和說明。

#### 結構 {#structure}

>[!CAUTION]
>
>如果使AEM用6.1 Communities FP4或更舊版本，請勿將群組功能新增至群組範本。
>
>從Communities [FP1](/help/communities/communities.md#latestfeaturepack)開始，即可使用巢狀群組功能。
>
>仍不允許將群組函式新增為範本中的第一個或唯一函式。

![群組範本編輯器](assets/template-editor.png)

若要新增社群功能，請依網站功能表連結的顯示順序，從右側拖曳至左側。 在建立網站時，樣式會套用至範本。

例如，如果您想要論壇，請將論壇函式從程式庫拖曳至範本產生器下方。 這將導致論壇配置對話框開啟。 有關配置對話框的資訊，請參見[functions console](/help/communities/functions.md)。

根據此範本，繼續拖放子社群網站（群組）所需的任何其他社群功能。

![拖曳函式](assets/dragfunctions.png)

將所有需要的函式拖放到範本產生器區域並加以設定後，請選取右上角的「儲存」。****

## 編輯群組範本{#edit-group-template}

在主[組模板控制台](#group-templates-console)中查看社區組時，可以選擇現有的組模板進行編輯。

編輯群組範本不會影響已從範本建立的社群網站。 可以直接[編輯社區站點](/help/communities/sites-console.md#modify-structure)的結構。

此程式提供與[建立群組範本](#create-group-template)相同的面板。
