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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 訊息功能{#messaging-feature}

除了在論壇和留言中公開顯示的互動功能外，****AEM Communities的訊息功能還可讓社群成員彼此私下互動。

建立社群網站時，可 [加入此](/help/communities/overview.md#communitiessites) 功能。

訊息功能可讓您：

**A** —— 發送消息給一個或多個社區成員&#x200B;**B** —— 批量發送直接消息給社區成員組 [](/help/communities/messaging.md#group-messaging)-發送消息——發送附件DD ************ -轉發消息***E —— 回復消息**FA消息——刪除消息* —— 恢復消息*

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

要修改消息傳送功能的「收件箱」、「已發送項目 **」和「**垃圾筒**」**頁的消息清單的配置，請以作者編輯模式打 **開站點**[](/help/communities/sites-console.md#authoring-site-content)。

1. 在模 `Preview`式中，選擇**消息**連結以開啟主消息頁面。 然後選取「收 **件匣**」、「已傳送項目」**或「**垃圾桶」**，以設定該訊息清單的元件。

1. 在模 `Edit` 式中，選擇頁面上的元件。
1. 要訪問配置對話框，請通過選擇表徵圖取消 `link`繼承。
取消繼承後，可以選擇配置表徵圖以開啟配置對話框。

1. 配置完成後，必須通過選擇表徵圖來恢復繼 `broken link` 承。

![configure-message-list](assets/configure-message-list.png)

#### Basic tab {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **服務選擇器**(*必要*)從`serviceSelector.name`AEM Communities Messaging Operations Service將此值設為屬性** [***](/help/communities/messaging.md#messaging-operations-service)。

* **合成頁**(必&#x200B;*要*)成員按一下**`Reply`**按鈕時要開啟的頁。 目標頁應包含合成 **消息表單** 。

* **回覆／檢視為資源**&#x200B;如果勾選，回覆URL和檢視URL將參考資源，否則資料會作為URL中的查詢參數傳遞。

* **描述檔顯示表**&#x200B;單用於顯示傳送者描述檔的描述檔表單。

* **垃圾筒資**&#x200B;料夾：如果勾選，此「訊息清單」元件只會顯示標示為已刪除（垃圾筒）的訊息。

* **資料夾路徑**(*必要*)參考 **AEM Communities Messaging Operations Service中inbox.path.name** 和**sentitems.path.name **設定的值 [](/help/communities/messaging.md#messaging-operations-service)。 為配置時， `Inbox`請使用inbox.path.name的值 **添加一個條目**。 為配置時， `Outbox`請使用 **sentitems.path.name的值添加一個條目**。 為配置時， `Trash`添加兩個具有兩個值的條目。

#### 顯示頁籤 {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **標籤讀取按**&#x200B;鈕如果選中，則顯 `Read`示一個按鈕，允許將消息標籤為已讀取。

* **標籤未讀按**&#x200B;鈕如果選中，則顯示 `Mark Unread` 一個按鈕，允許將消息標籤為已讀取。

* **刪除按鈕**&#x200B;如果選中，則顯示 `Delete`一個按鈕，允許將消息標籤為已讀取。 如果也勾選，將複製 **`Message Options`** 刪除功能。

* **消息選**&#x200B;項如果選中 **`Reply`**，則顯示 **`Reply All`**、**`Forward`**和**`Delete`*按鈕，允許重新發送或刪除消息。 如果也勾選，將複製 **`Delete Button`** 刪除功能。

* **每頁消息**&#x200B;指定的數量是分頁方案中每頁顯示的最大消息數。 如果未指定數字（留空），則會顯示所有訊息，且無分頁。

* **時間戳記模**&#x200B;式提供一或多種語言的時間戳記模式。 預設值為en、de、fr、it、es、ja、zh_CN、ko_KR。

* **顯示用**&#x200B;戶選擇**`Sender`**或**`Recipients`**，以確定是顯示「發送者」還是「接收者」。

### 配置合成消息 {#configure-compose-message}

要修改合成消息頁的配置，請在作者編輯模式 [下開啟站點](/help/communities/sites-console.md#authoring-site-content)。

* 在模 `Preview`式中，選擇**消息**連結以開啟主消息頁面。 然後選擇「新建消息」按鈕以開啟 `Compose Message` 頁面。

* 在模 `Edit` 式中，選擇包含消息主體的頁面上的主元件。
* 要訪問配置對話框，請通過選擇表徵圖取消 `link`繼承。
取消繼承後，可以選擇配置表徵圖以開啟配置對話框。

* 配置完成後，必須通過選擇表徵圖來恢復繼 `broken link`承。

![config-compose](assets/config-compose-message.png)

#### Basic tab {#basic-tab-1}

![基本制表符合](assets/basic-tab-compose.png)

* **重新導向URL**&#x200B;輸入訊息傳送後所顯示之頁面的URL。 例如， `../messaging.html`。

* **取消URL**&#x200B;輸入傳送者取消訊息時顯示之頁面的URL。 例如， `../messaging.html`。

* **消息主題的最大長**&#x200B;度「主題」欄位中允許的字元數上限。 例如，500。 預設為無限制。

* **消息正文的最大長**&#x200B;度「內容」欄位中允許的最大字元數。 例如，10000。 預設為無限制。

* **服務選擇器**(*必要*)從`serviceSelector.name`AEM Communities Messaging Operations Service將此值設為屬性** [***](/help/communities/messaging.md#messaging-operations-service)。

#### 顯示頁籤 {#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **顯示主題欄位**&#x200B;如果選中，則顯示 `Subject` 該欄位並啟用向消息中添加主題。 未勾選預設值。

* **主題標**&#x200B;簽輸入要顯示在欄位旁的文 `Subject` 字。 預設為 `Subject`。

* **顯示附加檔案欄位**&#x200B;如果選中此選項，則顯 `Attachment` 示該欄位並啟用向郵件中添加檔案附件。 未勾選預設值。

* **附加檔案標**&#x200B;簽輸入要顯示在欄位旁的 `Attachment` 文本。 預設為 **`Attach File`**。

* **顯示內容欄位**&#x200B;如果勾選，則顯示欄 `Content` 位並啟用新增訊息內文。 未勾選預設值。

* **內容標**&#x200B;簽輸入要在欄位旁顯示的 `Content` 文字。 預設為 **`Body`**。

* **With Rich Text Editor**（富格文本編輯器）如果選中，則表示使用自定義「內容」文本框及其自己的富格文本編輯器。 未勾選預設值。

* **時間戳記模**&#x200B;式提供一或多種語言的時間戳記模式。 預設值為en、de、fr、it、es、ja、zh_CN、ko_KR。

