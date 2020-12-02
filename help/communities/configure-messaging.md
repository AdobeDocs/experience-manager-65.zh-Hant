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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 3%

---


# 消息傳遞功能{#messaging-feature}

除了在論壇和留言中發生的公開可見互動外，AEM Communities的傳訊功能還可讓社群成員彼此私下互動。

建立[社區站點](/help/communities/overview.md#communitiessites)時，可包含此功能。

訊息功能可讓您：

**A** -傳送訊息給一或多個社群成員

**B** -大量傳送直接訊息 [給社群成員群組](/help/communities/messaging.md#group-messaging)

**C** -發送包含附件的郵件

**D** -轉發消息

**E** -回覆訊息

**F** -刪除消息

**G** -恢復已刪除的消息

![消息部分](assets/messaging-section.png)

![還原消息](assets/restore-message.png)

要啟用和修改消息傳遞功能，請參閱：

* [為管理](/help/communities/messaging.md) 員配置消息
* [對開發人員](/help/communities/essentials-messaging.md) 而言的訊息本質

>[!NOTE]
>
>不支援將`Compose Message, Message, or Message List`元件（位於`Communities`元件組中）添加到作者編輯模式下的頁面。

## 配置消息傳遞元件{#configure-messaging-components}

為社區站點啟用消息傳送時，無需進一步配置即可進行設定。 如果需要更改預設配置，則提供資訊。

### 配置消息清單（消息框）{#configure-message-list-message-box}

要修改消息傳送功能的&#x200B;**收件箱**、**已發送項目**&#x200B;和&#x200B;**垃圾筒**&#x200B;頁面的消息清單配置，請以[作者編輯模式](/help/communities/sites-console.md#authoring-site-content)開啟站點。

1. 在`Preview`模式中，選擇&#x200B;**消息**&#x200B;連結以開啟主消息傳遞頁。 然後選擇&#x200B;**收件箱**、**已發送項目**&#x200B;或&#x200B;**垃圾筒**&#x200B;來配置該郵件清單的元件。

1. 在`Edit`模式中，選擇頁面上的元件。
1. 要訪問配置對話框，請通過選擇`link`表徵圖取消繼承。
取消繼承後，可以選擇配置表徵圖以開啟配置對話框。

1. 配置完成後，必須通過選擇`broken link`表徵圖恢復繼承。

![configure-message-list](assets/configure-message-list.png)

#### 基本頁籤{#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **服務選擇器**

   (*Required*)將此值設為[ AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service)中屬性&#x200B;**`serviceSelector.name`**&#x200B;的值。

* **合成頁**

   (*Required*)當成員按一下&#x200B;**`Reply`**&#x200B;按鈕時要開啟的頁。 目標頁應包含&#x200B;**合成消息**&#x200B;表單。

* **回覆／檢視為資源**

   如果勾選，「回覆URL」和「檢視URL」會參考資源，否則資料會作為URL中的查詢參數傳遞。

* **描述檔顯示表單**

   用於顯示寄件者描述檔的描述檔表單。

* **垃圾桶資料夾**

   如果勾選，此「訊息清單」元件只會顯示標示為已刪除（垃圾筒）的訊息。

* **資料夾路徑**

   (*Required*)參考[AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service)中&#x200B;**inbox.path.name**&#x200B;和&#x200B;**sentitems.path.name**&#x200B;的值集。 為`Inbox`配置時，請使用&#x200B;**inbox.path.name**&#x200B;的值添加一個條目。 設定`Outbox`時，請使用&#x200B;**sentitems.path.name**&#x200B;的值新增一個項目。 為`Trash`配置時，請添加兩個具有兩個值的條目。

#### 顯示頁籤{#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **標籤讀取按鈕**

   如果選中，則顯示`Read`按鈕，允許將消息標籤為已讀取。

* **標籤未讀按鈕**

   如果選中，則顯示`Mark Unread`按鈕，允許將消息標籤為已讀取。

* **刪除按鈕**

   如果選中，則顯示`Delete`按鈕，允許將消息標籤為已讀取。 如果&#x200B;**`Message Options`**&#x200B;也已勾選，將複製刪除功能。

* **訊息選項**

   如果選中，則顯示&#x200B;**`Reply`**、**`Reply All`**、**`Forward`**&#x200B;和&#x200B;**`Delete`**&#x200B;按鈕，允許重新發送或刪除消息。 如果&#x200B;**`Delete Button`**&#x200B;也已勾選，將複製刪除功能。

* **每頁的訊息**

   指定的數目是分頁方案中每頁顯示的最大消息數。 如果未指定數字（留空），則會顯示所有訊息，且無分頁。

* **時間戳記模式**

   提供一或多種語言的時間戳記模式。 預設值為en、de、fr、it、es、ja、zh_CN、ko_KR。

* **顯示使用者**

   選擇&#x200B;**`Sender`**&#x200B;或&#x200B;**`Recipients`**&#x200B;以決定要顯示「傳送者」或「收件者」。

### 配置合成消息{#configure-compose-message}

要修改合成消息頁的配置，請在[作者編輯模式](/help/communities/sites-console.md#authoring-site-content)中開啟該站點。

* 在`Preview`模式中，選擇&#x200B;**消息**&#x200B;連結以開啟主消息傳遞頁。 然後選擇「新建消息」按鈕以開啟`Compose Message`頁。

* 在`Edit`模式中，選擇包含消息主體的頁面上的主元件。
* 要訪問配置對話框，請通過選擇`link`表徵圖取消繼承。
取消繼承後，可以選擇配置表徵圖以開啟配置對話框。

* 配置完成後，必須通過選擇`broken link`表徵圖恢復繼承。

![config-compose](assets/config-compose-message.png)

#### 基本頁籤{#basic-tab-1}

![基本制表符合](assets/basic-tab-compose.png)

* **重新導向URL**

   輸入訊息傳送後所顯示之頁面的URL。 例如，`../messaging.html`。

* **取消 URL**

   輸入傳送者取消訊息時所顯示的頁面URL。 例如，`../messaging.html`。

* **消息主題的最大長度**

   「主旨」欄位中允許的字元數上限。 例如，500。 預設為無限制。

* **消息正文的最大長度**

   「內容」欄位中允許的字元數上限。 例如，10000。 預設為無限制。

* **服務選擇器**

   (*Required*)將此值設為[ AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service)中屬性&#x200B;**`serviceSelector.name`**&#x200B;的值。

#### 顯示頁籤{#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **顯示主題欄位**

   如果選中，則顯示`Subject`欄位並啟用向消息中添加主題。 未勾選預設值。

* **主題標籤**

   在`Subject`欄位旁輸入要顯示的文字。 預設值為`Subject`。

* **顯示附加檔案欄位**

   如果選中，則顯示`Attachment`欄位並啟用向郵件中添加檔案附件。 未勾選預設值。

* **附加檔案標籤**

   在`Attachment`欄位旁輸入要顯示的文字。 預設值為&#x200B;**`Attach File`**。

* **顯示內容欄位**

   如果選中，則顯示`Content`欄位並啟用添加消息主體。 未勾選預設值。

* **內容標籤**

   在`Content`欄位旁輸入要顯示的文字。 預設值為&#x200B;**`Body`**。

* **具有 RTF 編輯器**

   如果勾選，表示自訂「內容」文字方塊與其專屬的豐富式文字編輯器搭配使用。 未勾選預設值。

* **時間戳記模式**

   提供一或多種語言的時間戳記模式。 預設值為en、de、fr、it、es、ja、zh_CN、ko_KR。

