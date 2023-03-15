---
title: 傳訊功能
seo-title: Messaging Feature
description: 配置報文傳送元件
seo-description: Configuring Messaging components
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
source-wordcount: '927'
ht-degree: 3%

---

# 傳訊功能 {#messaging-feature}

除了論壇和留言中公開顯示的互動外，AEM Communities的傳訊功能還可讓社群成員更私下互動。

若 [社群網站](/help/communities/overview.md#communitiessites) 中所有規則的URL區段。

傳訊功能提供下列功能：

**A**  — 向一個或多個社區成員發送消息

**B**  — 在 [批量到社區成員組](/help/communities/messaging.md#group-messaging)

**C**  — 發送包含附件的郵件

**D**  — 轉發消息

**E**  — 回覆訊息

**F**  — 刪除訊息

**G**  — 還原已刪除的消息

![傳訊區段](assets/messaging-section.png)

![還原消息](assets/restore-message.png)

要啟用和修改消息功能，請參閱：

* [配置消息](/help/communities/messaging.md) 管理員
* [Messaging Essentials](/help/communities/essentials-messaging.md) 開發人員

>[!NOTE]
>
>不支援添加 `Compose Message, Message, or Message List` 元件(可在 `Communities`元件群組)至作者編輯模式中的頁面。

## 配置消息傳遞元件 {#configure-messaging-components}

為社群網站啟用傳訊功能時，無需進一步設定即可完成設定。 如果需要變更預設設定，則會提供資訊。

### 配置消息清單（消息框） {#configure-message-list-message-box}

修改的消息清單的配置 **收件匣**, **已傳送項目**，和 **垃圾** 頁面，在 [作者編輯模式](/help/communities/sites-console.md#authoring-site-content).

1. 在 `Preview` 模式，請選擇 **訊息** 連結以開啟主要傳訊頁面。 然後選取 **收件匣**, **已傳送項目** 或 **垃圾** 配置該消息清單的元件。

1. 在 `Edit` 模式，請在頁面上選取元件。
1. 若要存取設定對話方塊，請選取 `link` 表徵圖。
取消繼承後，可以選取「設定」圖示以開啟「設定」對話方塊。

1. 完成設定後，必須選取 `broken link` 表徵圖。

![configure-message-list](assets/configure-message-list.png)

#### 基本標籤 {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **服務選擇器**

   (*必填*)將此值設為屬性的值 **`serviceSelector.name`** 從 [AEM Communities傳訊作業服務](/help/communities/messaging.md#messaging-operations-service).

* **撰寫頁面**

   (*必填*)成員按一下 **`Reply`** 按鈕。 目標頁面應包含 **撰寫訊息** 表單。

* **回覆/檢視為資源**

   如果勾選此選項，回覆URL和檢視URL將參考資源，否則資料會在URL中以查詢參數的形式傳遞。

* **設定檔顯示表單**

   用於顯示發件人配置檔案的配置檔案表單。

* **清除資料夾**

   如果選中此選項，則此「消息清單」元件僅顯示標籤為已刪除（清除）的消息。

* **資料夾路徑**

   (*必填*)參考為 **inbox.path.name** 和 **sentitems.path.name** 在 [AEM Communities傳訊作業服務](/help/communities/messaging.md#messaging-operations-service). 為 `Inbox`，請使用 **inbox.path.name**. 為 `Outbox`，請使用 **sentitems.path.name**. 為配置時 `Trash`，請新增兩個包含這兩個值的項目。

#### 顯示標籤 {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **標籤讀取按鈕**

   若勾選，則會顯示 `Read`按鈕，允許將消息標籤為已讀。

* **標籤未讀按鈕**

   若勾選，則會顯示 `Mark Unread` 按鈕，允許將消息標籤為已讀。

* **刪除按鈕**

   若勾選，則會顯示 `Delete` 按鈕，允許將消息標籤為已讀。 若 **`Message Options`** 也會勾選。

* **訊息選項**

   若勾選，則顯示 **`Reply`**, **`Reply All`**, **`Forward`** 和 **`Delete`** 按鈕允許重新發送或刪除消息。 若 **`Delete Button`** 也會勾選。

* **每頁的訊息**

   指定的數量是分頁方案中每頁顯示的最大郵件數。 若未指定數字（保留為空白），則會顯示所有訊息，且沒有分頁。

* **時間戳記模式**

   提供一或多種語言的時間戳記模式。 預設值為en、de、fr、it、es、ja、zh_CN、ko_KR。

* **顯示使用者**

   選擇 **`Sender`** 或 **`Recipients`** ，以決定要顯示寄件者或收件者。

### 配置撰寫消息 {#configure-compose-message}

若要修改撰寫訊息頁面的設定，請在中開啟網站 [作者編輯模式](/help/communities/sites-console.md#authoring-site-content).

* 在 `Preview` 模式，請選擇 **訊息** 連結以開啟主要傳訊頁面。 然後選取「新增訊息」按鈕以開啟 `Compose Message` 頁面。

* 在 `Edit` 模式，在包含消息正文的頁上選擇主元件。
* 若要存取設定對話方塊，請選取 `link` 表徵圖。
取消繼承後，可以選取「設定」圖示以開啟「設定」對話方塊。

* 完成設定後，必須選取 `broken link` 表徵圖。

![config-compose-message](assets/config-compose-message.png)

#### 基本標籤 {#basic-tab-1}

![基本索引標籤撰寫](assets/basic-tab-compose.png)

* **重新導向URL**

   輸入訊息傳送後顯示之頁面的URL。 例如, `../messaging.html`.

* **取消 URL**

   如果發件人取消郵件，請輸入顯示的頁面URL。 例如, `../messaging.html`.

* **消息主體的最大長度**

   「主旨」欄位中允許的字元數上限。 例如500。 預設為無限制。

* **消息正文的最大長度**

   「內容」欄位中允許的字元數上限。 例如10000。 預設為無限制。

* **服務選擇器**

   (*必填*)將此值設為屬性的值 **`serviceSelector.name`** 從 [AEM Communities傳訊作業服務](/help/communities/messaging.md#messaging-operations-service).

#### 顯示標籤 {#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **顯示主題欄位**

   若勾選，則顯示 `Subject` 欄位，並啟用將主旨新增至訊息。 未勾選預設值。

* **主旨標籤**

   輸入要顯示在 `Subject` 欄位。 預設為 `Subject`.

* **顯示附加檔案欄位**

   若勾選，則顯示 `Attachment` 欄位，並啟用將檔案附件新增至訊息的功能。 未勾選預設值。

* **附加檔案標籤**

   輸入要顯示在 `Attachment` 欄位。 預設為 **`Attach File`**.

* **顯示內容欄位**

   若勾選，則顯示 `Content` 欄位並啟用添加消息正文。 未勾選預設值。

* **內容標籤**

   輸入要顯示在 `Content` 欄位。 預設為 **`Body`**.

* **具有 RTF 編輯器**

   若勾選此選項，表示使用自訂內容文字方塊及其專屬的RTF編輯器。 未勾選預設值。

* **時間戳記模式**

   提供一或多種語言的時間戳記模式。 預設值為en、de、fr、it、es、ja、zh_CN、ko_KR。
