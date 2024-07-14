---
title: 傳訊功能
description: 瞭解如何設定AEM Communities的傳訊功能，以允許社群成員更私密地互相互動。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: d121dc05-7d15-44ba-8d2d-b59d6c6480c8
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 0%

---

# 傳訊功能 {#messaging-feature}

除了在論壇和評論中公開可見的互動以外，AEM Communities的傳訊功能也可讓社群成員更私密地互相互動。

建立[社群網站](/help/communities/overview.md#communitiessites)時可包含此功能。

傳訊功能可讓您進行下列工作：

**A** — 傳送訊息給一或多個社群成員

**B** — 以[大量傳送直接訊息給社群成員群組](/help/communities/messaging.md#group-messaging)

**C** — 傳送包含附件的郵件

**D** — 轉寄訊息

**E** — 回複訊息

**F** — 刪除訊息

**G** — 還原已刪除的郵件

![傳訊區段](assets/messaging-section.png)

![還原訊息](assets/restore-message.png)

若要啟用及修改傳訊功能，請參閱：

* [設定系統管理員的傳訊](/help/communities/messaging.md)
* 開發人員的[傳訊要點](/help/communities/essentials-messaging.md)

>[!NOTE]
>
>不支援將`Compose Message, Message, or Message List`元件（位於`Communities`元件群組中）新增至作者編輯模式下的頁面。

## 設定傳訊元件 {#configure-messaging-components}

為社群網站啟用傳訊功能時，系統不會進行進一步的設定。 如果需要變更預設設定，則會提供資訊。

### 設定訊息清單（訊息方塊） {#configure-message-list-message-box}

若要修改傳訊功能之&#x200B;**收件匣**、**已傳送專案**&#x200B;及&#x200B;**垃圾桶**&#x200B;頁面的郵件清單設定，請在[作者編輯模式](/help/communities/sites-console.md#authoring-site-content)中開啟網站。

1. 在`Preview`模式中，選取&#x200B;**訊息**&#x200B;連結以開啟主要訊息頁面。 然後選取&#x200B;**收件匣**、**已傳送專案**&#x200B;或&#x200B;**垃圾桶**&#x200B;來設定該郵件清單的元件。

1. 在`Edit`模式中，選取頁面上的元件。
1. 若要存取設定對話方塊，請選取`link`圖示以取消繼承。
取消繼承後，可以選取設定圖示以開啟設定對話方塊。

1. 組態完成後，必須選取`broken link`圖示來還原繼承。

![configure-message-list](assets/configure-message-list.png)

#### 基本索引標籤 {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **服務選擇器**

  （*必要*）從[AEM Communities訊息操作服務](/help/communities/messaging.md#messaging-operations-service)將此設定為屬性&#x200B;**`serviceSelector.name`**&#x200B;的值。

* **撰寫頁面**

  （*必要*）成員按一下&#x200B;**`Reply`**&#x200B;按鈕時要開啟的頁面。 目標頁面應包含&#x200B;**撰寫訊息**&#x200B;表單。

* **回覆/檢視為資源**

  如果勾選，回覆URL和檢視URL會參照資源，否則資料會以查詢引數的形式傳遞到URL中。

* **設定檔顯示表單**

  用來顯示寄件者設定檔的設定檔表單。

* **垃圾桶資料夾**

  如果勾選，此訊息清單元件只會顯示標示為已刪除（垃圾桶）的訊息。

* **資料夾路徑**

  （*必要*）參考[AEM Communities訊息操作服務](/help/communities/messaging.md#messaging-operations-service)中為&#x200B;**inbox.path.name**&#x200B;和&#x200B;**sentitems.path.name**&#x200B;設定的值。 設定`Inbox`時，請使用&#x200B;**inbox.path.name**&#x200B;的值新增一個專案。 設定`Outbox`時，請使用&#x200B;**sentitems.path.name**&#x200B;的值新增一個專案。 為`Trash`設定時，新增兩個同時含有兩個值的專案。

#### 顯示標籤 {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **標示讀取按鈕**

  如果勾選，會顯示`Read`按鈕，允許將訊息標示為已讀取。

* **標籤未讀取按鈕**

  如果勾選，會顯示`Mark Unread`按鈕，允許將訊息標示為已讀取。

* **刪除按鈕**

  如果勾選，會顯示`Delete`按鈕，允許將訊息標示為已讀取。 如果也核取&#x200B;**`Message Options`**，則複製刪除功能。

* **訊息選項**

  如果勾選，會顯示&#x200B;**`Reply`**、**`Reply All`**、**`Forward`**&#x200B;和&#x200B;**`Delete`**&#x200B;按鈕，允許重新傳送或刪除訊息。 如果也核取&#x200B;**`Delete Button`**，則複製刪除功能。

* 每頁&#x200B;**則訊息**

  指定的數字是分頁配置中每頁顯示的最大訊息數。 如果未指定數字（保留為空白），則會顯示所有訊息，而且沒有分頁。

* **時間戳記模式**

  提供一或多個語言的時間戳記模式。 en、de、fr、it、es、ja、zh_CN、ko_KR的預設為。

* **顯示使用者**

  選擇&#x200B;**`Sender`**&#x200B;或&#x200B;**`Recipients`**，以決定要顯示寄件者還是收件者。

### 設定撰寫訊息 {#configure-compose-message}

若要修改撰寫訊息頁面的設定，請以[作者編輯模式](/help/communities/sites-console.md#authoring-site-content)開啟網站。

* 在`Preview`模式中，選取&#x200B;**訊息**&#x200B;連結以開啟主要訊息頁面。 然後選取[新增訊息]按鈕，讓您開啟`Compose Message`頁面。

* 在`Edit`模式中，在包含訊息內文的頁面上選取主要元件。
* 若要存取設定對話方塊，請選取`link`圖示以取消繼承。
取消繼承後，可以選取設定圖示以開啟設定對話方塊。

* 組態完成後，必須選取`broken link`圖示來還原繼承。

![config-compose-message](assets/config-compose-message.png)

#### 基本索引標籤 {#basic-tab-1}

![basic-tab-compose](assets/basic-tab-compose.png)

* **重新導向URL**

  輸入在傳送訊息之後顯示之頁面的URL。 例如，`../messaging.html`。

* **取消URL**

  輸入寄件者取消郵件時所顯示之頁面的URL。 例如，`../messaging.html`。

* **訊息主旨的長度上限**

  主旨欄位中允許的字元數量上限。 例如：500。 預設為無限制。

* **訊息本文的最大長度**

  「內容」欄位中允許的最大字元數。 例如， 10000。 預設為無限制。

* **服務選擇器**

  （*必要*）從[AEM Communities訊息操作服務](/help/communities/messaging.md#messaging-operations-service)將此設定為屬性&#x200B;**`serviceSelector.name`**&#x200B;的值。

#### 顯示標籤 {#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **顯示主旨欄位**

  如果勾選，顯示`Subject`欄位並啟用新增主旨至郵件。 未勾選預設值。

* **主旨標籤**

  輸入您要顯示在`Subject`欄位旁的文字。 預設值為`Subject`。

* **顯示附加檔案欄位**

  如果勾選，顯示`Attachment`欄位並啟用新增檔案附件至郵件。 未勾選預設值。

* **附加檔案標籤**

  輸入您要顯示在`Attachment`欄位旁的文字。 預設值為&#x200B;**`Attach File`**。

* **顯示內容欄位**

  如果勾選，則顯示`Content`欄位並啟用新增訊息本文。 未勾選預設值。

* **內容標籤**

  輸入您要顯示在`Content`欄位旁的文字。 預設值為&#x200B;**`Body`**。

* **使用Rtf編輯器**

  如果勾選，表示使用具有自己RTF編輯器的自訂內容文字方塊。 未勾選預設值。

* **時間戳記模式**

  提供一或多個語言的時間戳記模式。 en、de、fr、it、es、ja、zh_CN、ko_KR的預設為。
