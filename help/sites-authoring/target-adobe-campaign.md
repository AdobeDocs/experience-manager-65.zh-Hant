---
title: 鎖定Adobe Campaign
description: 設定細分後，您可以為Adobe Campaign建立鎖定目標的體驗。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
exl-id: fc6fccba-41c5-4c13-aac0-b4ef67767abe
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Architect,Developer
source-git-commit: 389d5fa8de320a7237fc8290992a33743b15db99
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# 鎖定您的Adobe Campaign{#targeting-your-adobe-campaign}

若要鎖定您的Adobe Campaign電子報，您必須先設定分段，而這僅適用於傳統UI （適用於使用者端內容）。 之後，您可以建立Adobe Campaign的鎖定目標體驗。 本節將說明這兩種方式。

## 在AEM中設定分段 {#setting-up-segmentation-in-aem}

若要設定區段，您必須使用傳統UI來設定區段。 其餘步驟可以在標準UI中執行。

設定細分包括建立區段、品牌、行銷活動和體驗。

>[!NOTE]
>
>區段ID必須對應至Adobe Campaign端的ID。

### 建立區段 {#creating-segments}

若要建立區段：

1. 在[&lt;host>：&lt;port>/miscadmin#/etc/segmentation](http://localhost:4502/miscadmin#/etc/segmentation)開啟&#x200B;**分段主控台**。
1. 建立頁面並輸入標題 — 例如&#x200B;**AC區段** — 並選取&#x200B;**區段(Adobe Campaign)**&#x200B;範本。
1. 在左側的樹狀檢視中選取建立的頁面。
1. 建立區段，例如，將目標定位為男性使用者，方法是在您建立的名為「男性」的區段下建立頁面，並選取&#x200B;**區段(Adobe Campaign)**&#x200B;範本。
1. 開啟已建立的區段頁面，並將&#x200B;**區段ID**&#x200B;從Sidekick拖放到頁面上。
1. 按兩下特徵，輸入代表在此案例中定義在Adobe Campaign中的男性區段（例如，**MALE**）的ID，然後按一下&#x200B;**確定**。 應該會顯示下列訊息： *`targetData.segmentCode == "MALE"`*
1. 對另一個區段重複這些步驟，例如以女性使用者為目標的區段。

### 建立品牌 {#creating-a-brand}

若要建立品牌：

1. 在&#x200B;**Sites**&#x200B;中，導覽至&#x200B;**Campaigns**&#x200B;資料夾（例如We.Retail中的）。
1. 按一下&#x200B;**建立頁面**&#x200B;並輸入頁面的標題，例如We.Retail品牌，然後選取&#x200B;**品牌**&#x200B;範本。

### 建立行銷活動 {#creating-a-campaign}

若要建立行銷活動：

1. 開啟您建立的&#x200B;**品牌**&#x200B;頁面。
1. 按一下&#x200B;**建立頁面**&#x200B;並輸入頁面的標題，例如We.Retail行銷活動，然後選取&#x200B;**行銷活動**&#x200B;範本並按一下&#x200B;**建立**。

### 建立體驗 {#creating-experiences}

若要建立區段的體驗：

1. 開啟您建立的&#x200B;**促銷活動**&#x200B;頁面。
1. 按一下「**建立頁面**」並輸入頁面的標題（例如，「男性」）來建立您區段的體驗，然後選取「**體驗**」範本。
1. 開啟已建立的體驗頁面。
1. 按一下[編輯]&#x200B;**&#x200B;**，然後在[區段]下方按一下[新增專案]&#x200B;**&#x200B;**。
1. 輸入男性區段的路徑，例如&#x200B;**/etc/segmentation/ac-segments/male**，然後按一下&#x200B;**確定**。 應該會出現下列訊息： *體驗目標為：男性*
1. 重複上述步驟以建立所有區段的體驗，例如女性目標。
