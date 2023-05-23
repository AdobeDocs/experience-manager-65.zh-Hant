---
title: 群組範本
seo-title: Group Templates
description: 如何訪問組模板控制台
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

組模板控制台與 [站點模板](/help/communities/sites.md) 控制台。 這兩個都是一組預先佈線的頁面和功能的藍圖，它們構成了一個社區網站。 不同之處在於，站點模板用於主社區，而組模板用於社區組，即嵌套在主社區中的子社區。

社區組通過包括 [組函式](/help/communities/functions.md#groups-function) （它可能不是模板中的第一個或唯一的函式）。

截至社區 [功能包1](/help/communities/deploy-communities.md#latestfeaturepack)，可以通過在組模板中包含「組」功能來嵌套組。

當執行建立新社區組的操作時，將選擇該組的模板（結構）。 選擇取決於在添加到站點或組模板時如何配置組功能。

>[!NOTE]
>
>用於建立 [社區站點](/help/communities/sites-console.md)。 [社區網站模板](/help/communities/sites.md)。 [社區組模板](/help/communities/tools-groups.md) 和 [社區功能](/help/communities/functions.md) 僅在作者環境中使用。

## 組模板控制台 {#group-templates-console}

要訪問AEM Author環境中的組模板控制台：

* 選擇 **工具 |社區 |組模板，** 的子菜單。

此控制台顯示 [社區站點](/help/communities/sites-console.md) 可以建立，並允許建立新組模板。

![社區組模板](assets/groups-template.png)

## 建立群組範本 {#create-group-template}

要開始建立新組模板，請選擇 `Create`。

這將顯示包含3個子面板的「站點編輯器」面板：

### 基本資訊 {#basic-info}

![站點基本資訊](assets/site-basic-info.png)

在「基本資訊」面板上，配置了名稱、說明以及模板是啟用還是禁用：

* **新群組範本名稱**

   模板名稱ID。

* **說明**

   模板說明。

* **已禁用/已啟用**

   控制模板是否可引用的切換開關。

#### 縮圖 {#thumbnail}

![站點縮略圖](assets/site-thumbnail.png)

（可選）選擇「上載影像」表徵圖以向社區網站的建立者顯示縮略圖以及名稱和說明。

#### 結構 {#structure}

>[!CAUTION]
>
>如果使用AEM6.1社區FP4或更低版本，則不要向組模板添加組函式。
>
>自社區起，嵌套組功能可用 [FP1](/help/communities/communities.md#latestfeaturepack)。
>
>仍不允許將組函式添加為模板中的第一個或唯一函式。

![組模板編輯器](assets/template-editor.png)

要添加社區功能，請按站點菜單連結的顯示順序從右側向左拖動。 在建立站點期間，樣式將應用於模板。

例如，如果想要論壇，請將論壇功能從庫中拖放到模板生成器下。 這將導致論壇配置對話框開啟。 查看 [函式控制台](/help/communities/functions.md) 的子菜單。

根據此模板，繼續拖放子社區站點（組）所需的任何其他社區功能。

![拖動函式](assets/dragfunctions.png)

將所有所需函式拖放到模板生成器區域並進行配置後，選擇 **保存** 在右上角。

## 編輯群組範本 {#edit-group-template}

在主中查看社區組時 [組模板控制台](#group-templates-console)，可以選擇現有組模板進行編輯。

編輯組模板不會影響已從該模板建立的社區站點。 可以直接 [編輯社區網站](/help/communities/sites-console.md#modify-structure)改為結構。

此過程提供與 [建立組模板](#create-group-template)。
