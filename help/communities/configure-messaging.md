---
title: 訊息功能
seo-title: 訊息功能
description: 配置消息傳遞元件
seo-description: 配置消息傳遞元件
uuid: 8b99ded1-aec2-40c9-82d5-e2e404f614ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9d952604-f9ef-498f-937b-871817c80226
docset: aem65
translation-type: tm+mt
source-git-commit: e8d8bf89971d3d9d5ec150308dda247aa53c77bb

---


# 訊息功能 {#messaging-feature}

除了在論壇和留言中發生的公開可見互動外，AEM Communities的傳訊功能還可讓社群成員彼此私下互動。

建立社群網站時，可 [加入此](/help/communities/overview.md#communitiessites) 功能。

訊息功能可讓您：

**A** —— 發送消息給一個或多個社區成員&#x200B;**B** - [直接發送給](/help/communities/messaging.md#group-messaging)bulk社區組CC ******************** Message消息——發送消息DD-前轉EJasting —— 前轉消息——回復消息DeleteMessageF-AdaMessageG —— 還原消息——刪除消息——刪除消息

![消息部分](assets/messaging-section.png)![還原消息](assets/restore-message.png)

要啟用和修改消息傳遞功能，請參閱：

* [為管理員配置消息](/help/communities/messaging.md) ,
* [適用於開發人員的Messaging](/help/communities/essentials-messaging.md) Essentials

>[!NOTE]
>
>不支援在作者編輯 `Compose Message, Message, or Message List` 模式中將元件( `Communities`位於元件群組)新增至頁面。

## 配置消息傳遞元件 {#configure-messaging-components}

為社區站點啟用消息傳送時，無需進一步配置即可進行設定。 如果需要更改預設配置，則提供資訊。

### 配置消息清單（消息框） {#configure-message-list-message-box}

要修改消息傳遞功能的「收件箱」、「已發送項目」和「垃圾筒」頁 **面的消息清單的配置，請在作者編輯模**********[](/help/communities/sites-console.md#authoring-site-content)式中開啟站點。

1. 在模 `Preview`式中，選擇「 **消息** 」連結以開啟主消息傳遞頁。 然後選擇「收 **件匣**」、「已 **傳送項目** 」或 **「垃圾桶** 」來設定該訊息清單的元件。

1. 在模 `Edit` 式中，選擇頁面上的元件。
1. 要訪問配置對話框，請通過選擇表徵圖取消 `link`繼承。
取消繼承後，可以選擇配置表徵圖以開啟配置對話框。

1. 配置完成後，必須通過選擇表徵圖來恢復繼 `broken link` 承。

![configure-message-list](assets/configure-message-list.png)

#### Basic tab {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **服務選擇器**

   (必&#x200B;*要*)將此值設為 **`serviceSelector.name`** AEM Communities Messaging Operations Service中屬性的值 [](/help/communities/messaging.md#messaging-operations-service)。

* **合成頁**

   (必&#x200B;*要*)會員按一下按鈕時要開啟的 **`Reply`** 頁面。 目標頁應包含合成 **消息表單** 。

* **回覆／檢視為資源**

   如果勾選，「回覆URL」和「檢視URL」會參考資源，否則資料會作為URL中的查詢參數傳遞。

* **描述檔顯示表單**

   用於顯示寄件者描述檔的描述檔表單。

* **垃圾桶資料夾**

   如果勾選，此「訊息清單」元件只會顯示標示為已刪除（垃圾筒）的訊息。

* **資料夾路徑**

   (必&#x200B;*要*)參考 **AEM Communities Operations Service Messaging中inbox.path.name** 和 ****[](/help/communities/messaging.md#messaging-operations-service)sentitems.path.name所設定的值。 為配置時， `Inbox`請使用inbox.path.name的值 **添加一個條目**。 為配置時， `Outbox`請使用 **sentitems.path.name的值添加一個條目**。 在配置時， `Trash`添加兩個同時具有兩個值的條目。

#### 顯示頁籤 {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **標籤讀取按鈕**

   如果勾選，則顯示 `Read`允許將消息標籤為已讀取的按鈕。

* **標籤未讀按鈕**

   如果勾選，則顯示 `Mark Unread` 一個按鈕，允許將消息標籤為已讀取。

* **刪除按鈕**

   如果勾選，則顯示 `Delete`允許將消息標籤為已讀取的按鈕。 如果也勾選，將複製 **`Message Options`** 刪除功能。

* **訊息選項**

   如果勾選，則會顯 **`Reply`**&#x200B;示、 **`Reply All`****`Forward`****`Delete`** 以及允許重新傳送或刪除訊息的按鈕。 如果也勾選，將複製 **`Delete Button`** 刪除功能。

* **每頁的訊息**

   指定的數目是分頁方案中每頁顯示的最大消息數。 如果未指定數字（留空），則會顯示所有訊息，且無分頁。

* **時間戳記模式**

   提供一或多種語言的時間戳記模式。 預設值為en、de、fr、it、es、ja、zh_CN、ko_KR。

* **顯示使用者**

   選擇或 **`Sender`** 以決 **`Recipients`** 定是顯示「傳送者」或「收件者」。

### 配置合成消息 {#configure-compose-message}

要修改合成消息頁的配置，請在作者編輯模式 [下開啟站點](/help/communities/sites-console.md#authoring-site-content)。

* 在模 `Preview` 式中，選擇「 **消息** 」連結以開啟主消息傳遞頁。 然後選擇「新建消息」按鈕以開啟 `Compose Message` 頁面。

* 在模 `Edit` 式中，選擇包含消息主體的頁面上的主元件。
* 要訪問配置對話框，請通過選擇表徵圖取消繼 `link` 承。
取消繼承後，可以選擇配置表徵圖以開啟配置對話框。

* 配置完成後，必須通過選擇表徵圖來恢復繼 `broken link` 承。

![config-compose](assets/config-compose-message.png)

#### Basic tab {#basic-tab-1}

![基本制表符合](assets/basic-tab-compose.png)

* **重新導向URL**

   輸入訊息傳送後所顯示之頁面的URL。 For example, `../messaging.html`.

* **取消 URL**

   輸入傳送者取消訊息時所顯示的頁面URL。 For example, `../messaging.html`.

* **消息主題的最大長度**

   「主旨」欄位中允許的字元數上限。 例如，500。 預設為無限制。

* **消息正文的最大長度**

   「內容」欄位中允許的字元數上限。 例如，10000。 預設為無限制。

* **服務選擇器**

   (必&#x200B;*要*)將此值設為 **`serviceSelector.name`** AEM Communities Messaging Operations Service中屬性的值 [](/help/communities/messaging.md#messaging-operations-service)。

#### 顯示頁籤 {#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **顯示主題欄位**

   如果勾選，請顯 `Subject` 示欄位並啟用將主旨新增至訊息。 未勾選預設值。

* **主題標籤**

   輸入要顯示在欄位旁的文 `Subject` 字。 預設為 `Subject`。

* **顯示附加檔案欄位**

   如果選中，則顯示 `Attachment` 該欄位並啟用向郵件中添加檔案附件。 未勾選預設值。

* **附加檔案標籤**

   輸入要顯示在欄位旁的文 `Attachment` 字。 預設為 **`Attach File`**。

* **顯示內容欄位**

   如果選中，則顯示 `Content` 該欄位並啟用添加消息主體。 未勾選預設值。

* **內容標籤**

   輸入要顯示在欄位旁的文 `Content` 字。 預設為 **`Body`**。

* **具有 RTF 編輯器**

   如果勾選，表示自訂「內容」文字方塊與其專屬的豐富式文字編輯器搭配使用。 未勾選預設值。

* **時間戳記模式**

   提供一或多種語言的時間戳記模式。 預設值為en、de、fr、it、es、ja、zh_CN、ko_KR。

