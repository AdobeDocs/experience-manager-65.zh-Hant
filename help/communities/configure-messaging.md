---
title: 傳訊功能
seo-title: 傳訊功能
description: 配置報文傳送元件
seo-description: 配置報文傳送元件
uuid: 8b99ded1-aec2-40c9-82d5-e2e404f614ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9d952604-f9ef-498f-937b-871817c80226
docset: aem65
exl-id: d121dc05-7d15-44ba-8d2d-b59d6c6480c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 3%

---

# 消息功能{#messaging-feature}

除了論壇和留言中公開顯示的互動外，AEM Communities的傳訊功能還可讓社群成員更私下互動。

建立[社群網站](/help/communities/overview.md#communitiessites)時，可包含此功能。

傳訊功能提供下列功能：

****  — 傳送訊息給一或多個社群成員

**B**  — 大量傳送直 [接訊息給社群成員群組](/help/communities/messaging.md#group-messaging)

**C**  — 傳送包含附件的訊息

**D**  — 轉送訊息

**E**  — 回覆訊息

**F**  — 刪除訊息

**G**  — 還原已刪除的訊息

![傳訊區段](assets/messaging-section.png)

![還原消息](assets/restore-message.png)

要啟用和修改消息功能，請參閱：

* [為管理](/help/communities/messaging.md) 員配置消息
* [對開發人員](/help/communities/essentials-messaging.md) 而言至關重要的報文傳送

>[!NOTE]
>
>不支援將`Compose Message, Message, or Message List`元件（可在`Communities`元件群組中找到）新增至作者編輯模式中的頁面。

## 配置消息元件{#configure-messaging-components}

為社群網站啟用傳訊功能時，無需進一步設定即可完成設定。 如果需要變更預設設定，則會提供資訊。

### 配置消息清單（消息框）{#configure-message-list-message-box}

要修改郵件功能的&#x200B;**收件箱**、**已發送項**&#x200B;和&#x200B;**垃圾筒**&#x200B;頁面的郵件清單的配置，請在[作者編輯模式](/help/communities/sites-console.md#authoring-site-content)中開啟站點。

1. 在`Preview`模式中，選擇&#x200B;**Messages**&#x200B;連結以開啟主消息頁。 然後，選擇&#x200B;**收件箱**、**已發送項**&#x200B;或&#x200B;**垃圾筒**&#x200B;以配置該郵件清單的元件。

1. 在`Edit`模式中，選取頁面上的元件。
1. 若要存取設定對話方塊，請選取`link`圖示以取消繼承。
取消繼承後，可以選取「設定」圖示以開啟「設定」對話方塊。

1. 完成配置後，必須通過選擇`broken link`表徵圖來恢復繼承。

![configure-message-list](assets/configure-message-list.png)

#### 基本頁簽{#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **服務選擇器**

   （*必要*）將此值設為[AEM Communities傳訊作業服務](/help/communities/messaging.md#messaging-operations-service)中屬性&#x200B;**`serviceSelector.name`**&#x200B;的值。

* **撰寫頁面**

   （*必要*）成員按一下&#x200B;**`Reply`**&#x200B;按鈕時要開啟的頁面。 目標頁面應包含&#x200B;**撰寫訊息**&#x200B;表單。

* **回覆/檢視為資源**

   如果勾選此選項，回覆URL和檢視URL將參考資源，否則資料會在URL中以查詢參數的形式傳遞。

* **設定檔顯示表單**

   用於顯示發件人配置檔案的配置檔案表單。

* **清除資料夾**

   如果選中此選項，則此「消息清單」元件僅顯示標籤為已刪除（清除）的消息。

* **資料夾路徑**

   （*必要*）參考[AEM Communities傳訊作業服務](/help/communities/messaging.md#messaging-operations-service)中為&#x200B;**inbox.path.name**&#x200B;和&#x200B;**sentitems.path.name**&#x200B;設定的值。 為`Inbox`配置時，使用&#x200B;**inbox.path.name**&#x200B;值添加一個條目。 為`Outbox`進行配置時，請使用&#x200B;**sentitems.path.name**&#x200B;值添加一個條目。 為`Trash`進行配置時，請添加兩個包含這兩個值的條目。

#### 顯示頁簽{#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **標籤讀取按鈕**

   如果選中，則顯示`Read`按鈕，允許將消息標籤為已讀。

* **標籤未讀按鈕**

   如果選中，則顯示`Mark Unread`按鈕，允許將消息標籤為已讀。

* **刪除按鈕**

   如果選中，則顯示`Delete`按鈕，允許將消息標籤為已讀。 如果也檢查了&#x200B;**`Message Options`**，則會複製刪除功能。

* **訊息選項**

   如果選中，則顯示&#x200B;**`Reply`**、**`Reply All`**、**`Forward`**&#x200B;和&#x200B;**`Delete`**&#x200B;按鈕，允許重新發送或刪除消息。 如果也檢查了&#x200B;**`Delete Button`**，則會複製刪除功能。

* **每頁的訊息**

   指定的數量是分頁方案中每頁顯示的最大郵件數。 若未指定數字（保留為空白），則會顯示所有訊息，且沒有分頁。

* **時間戳記模式**

   提供一或多種語言的時間戳記模式。 預設值為en、de、fr、it、es、ja、zh_CN、ko_KR。

* **顯示使用者**

   選擇&#x200B;**`Sender`**&#x200B;或&#x200B;**`Recipients`**&#x200B;以確定是顯示發件人還是收件人。

### 配置撰寫消息{#configure-compose-message}

若要修改撰寫訊息頁面的設定，請在[作者編輯模式](/help/communities/sites-console.md#authoring-site-content)中開啟網站。

* 在`Preview`模式中，選擇&#x200B;**Messages**&#x200B;連結以開啟主消息頁。 然後選擇「新建消息」按鈕以開啟`Compose Message`頁。

* 在`Edit`模式中，在包含Message body的頁面上選擇主元件。
* 若要存取設定對話方塊，請選取`link`圖示以取消繼承。
取消繼承後，可以選取「設定」圖示以開啟「設定」對話方塊。

* 完成配置後，必須通過選擇`broken link`表徵圖來恢復繼承。

![config-compose-message](assets/config-compose-message.png)

#### 基本頁簽{#basic-tab-1}

![基本索引標籤撰寫](assets/basic-tab-compose.png)

* **重新導向URL**

   輸入訊息傳送後顯示之頁面的URL。 例如， `../messaging.html`。

* **取消 URL**

   如果發件人取消郵件，請輸入顯示的頁面URL。 例如， `../messaging.html`。

* **消息主體的最大長度**

   「主旨」欄位中允許的字元數上限。 例如500。 預設為無限制。

* **消息正文的最大長度**

   「內容」欄位中允許的字元數上限。 例如10000。 預設為無限制。

* **服務選擇器**

   （*必要*）將此值設為[AEM Communities傳訊作業服務](/help/communities/messaging.md#messaging-operations-service)中屬性&#x200B;**`serviceSelector.name`**&#x200B;的值。

#### 顯示頁簽{#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **顯示主題欄位**

   若勾選此選項，則顯示`Subject`欄位並啟用將主旨新增至訊息。 未勾選預設值。

* **主旨標籤**

   輸入要在`Subject`欄位旁顯示的文字。 預設值為`Subject`。

* **顯示附加檔案欄位**

   如果選中，則顯示`Attachment`欄位並啟用向郵件添加檔案附件。 未勾選預設值。

* **附加檔案標籤**

   輸入要在`Attachment`欄位旁顯示的文字。 預設值為&#x200B;**`Attach File`**。

* **顯示內容欄位**

   如果選中，則顯示`Content`欄位並啟用添加消息正文。 未勾選預設值。

* **內容標籤**

   輸入要在`Content`欄位旁顯示的文字。 預設值為&#x200B;**`Body`**。

* **具有 RTF 編輯器**

   若勾選此選項，表示使用自訂內容文字方塊及其專屬的RTF編輯器。 未勾選預設值。

* **時間戳記模式**

   提供一或多種語言的時間戳記模式。 預設值為en、de、fr、it、es、ja、zh_CN、ko_KR。
