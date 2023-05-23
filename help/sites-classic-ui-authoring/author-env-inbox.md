---
title: 您的收件匣
description: 您可以從各個區域接收通知AEM，如有關工作項目或任務的通知，這些任務表示您需要在頁面內容上執行的操作。
uuid: e7ba9150-957d-4f84-a570-2f3d83792472
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: ce2a1475-49cf-43e6-bfb9-006884ce3881
docset: aem65
exl-id: 52ea2ca2-eb1c-4bed-b52d-feef37c6afd6
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 1%

---

# 您的收件匣{#your-inbox}

您可以從各個區域接收通知AEM，如有關工作項目或任務的通知，這些任務表示您需要在頁面內容上執行的操作。

您將在兩個收件箱中收到這些通知，這些收件箱按通知類型分隔：

* 以下部分介紹了一個收件箱，您可以在該收件箱中查看通過訂閱接收的通知。
* 工作流項的專用收件箱在 [參與工作流](/help/sites-classic-ui-authoring/classic-workflows-participating.md) 的子菜單。

## 查看通知 {#viewing-your-notifications}

要查看通知，請執行以下操作：

1. 開啟通知收件箱：的 **網站** 控制台，按一下右上角的「用戶」按鈕，然後選擇 **通知收件箱**。

   ![screen_shot_2012-02-08at105226am](assets/screen_shot_2012-02-08at105226am.png)

   >[!NOTE]
   >
   >您也可以直接在瀏覽器中訪問控制台；例如：
   >
   >
   >` https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. 將列出您的通知。 您可以根據需要採取操作：

   * [訂閱通知](#subscribing-to-notifications)
   * [處理通知](#processing-your-notifications)

   ![chlimage_1-4](assets/chlimage_1-4.jpeg)

## 訂閱通知 {#subscribing-to-notifications}

訂閱通知：

1. 開啟通知收件箱：的 **網站** 控制台，按一下右上角的「用戶」按鈕，然後選擇 **通知收件箱**。

   ![screen_shot_2012-02-08at105226am-1](assets/screen_shot_2012-02-08at105226am-1.png)

   >[!NOTE]
   >
   >您也可以直接在瀏覽器中訪問控制台；例如：
   >
   >
   >`https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. 按一下 **配置……** 的上界。

   ![screen_shot_2012-02-08at111056am](assets/screen_shot_2012-02-08at111056am.png)

1. 選擇通知通道：

   * **收件箱**:通知將顯示在收件箱AEM中。
   * **電子郵件**:通知將通過電子郵件發送到用戶配置檔案中定義的電子郵件地址。

   >[!NOTE]
   >
   >需要配置一些設定才能通過電子郵件通知。 還可以自定義電子郵件模板或為新語言添加電子郵件模板。 請參閱 [配置電子郵件通知](/help/sites-administering/notification.md#configuringemailnotification) 中配置電子郵件通AEM知。

1. 選擇要通知的頁面操作：

   * 已激活：頁面已激活。
   * 已停用：頁面已停用。
   * 已刪除（協同內容）:刪除複製頁面時，即複製對頁面執行的刪除操作時。
刪除或移動頁面時，會自動複製刪除操作：在執行刪除操作的源實例和複製代理定義的目標實例上刪除該頁。

   * 已修改：修改頁面時。
   * 已建立：建立頁面時。
   * 已刪除：通過頁面刪除操作刪除頁面時。
   * 已推出：頁面已展開。

1. 定義將通知您的頁面的路徑：

   * 按一下 **添加** 的子菜單。
   * 按一下 **路徑** 輸入路徑，例如 `/content/docs`。

   * 要通知屬於子樹的所有頁面，請設定 **準確嗎？** 至 **否**。
要僅通知路徑定義的頁面上的操作，請設定 **準確嗎？** 至 **是**。

   * 要允許規則，請設定 **規則** 至 **允許**。 如果設定為 **拒絕**，該規則被拒絕但未被刪除，以後可以允許。

   要刪除定義，請通過按一下表格單元格並按一下 **刪除**。

1. 按一下 **確定** 的子菜單。

## 處理通知 {#processing-your-notifications}

如果您選擇在收件箱中接收通AEM知，則您的收件箱將充滿通知。 你可以 [查看通知](#viewing-your-notifications) 然後選擇所需的通知：

* 通過按一下 **批准**:值 **閱讀** 列設定為 **真**。

* 通過按一下 **刪除**。

![chlimage_1-5](assets/chlimage_1-5.jpeg)
