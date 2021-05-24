---
title: 您的收件匣
seo-title: 您的收件匣
description: 您可以從AEM的各個區域收到通知，例如工作項目或代表您需要在頁面內容上執行之動作的任務通知。
seo-description: 您可以從AEM的各個區域收到通知，例如工作項目或代表您需要在頁面內容上執行之動作的任務通知。
uuid: e7ba9150-957d-4f84-a570-2f3d83792472
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: ce2a1475-49cf-43e6-bfb9-006884ce3881
docset: aem65
exl-id: 52ea2ca2-eb1c-4bed-b52d-feef37c6afd6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# 您的收件匣{#your-inbox}

您可以從AEM的各個區域收到通知，例如工作項目或代表您需要在頁面內容上執行之動作的任務通知。

您會在兩個收件匣中收到這些通知，並依通知類型加以區隔：

* 下節將說明您可在其中查看訂閱後收到的通知的收件匣。
* [參與工作流](/help/sites-classic-ui-authoring/classic-workflows-participating.md)文檔中描述了工作流項的專用收件箱。

## 查看通知{#viewing-your-notifications}

若要檢視通知：

1. 開啟通知收件匣：在&#x200B;**網站**&#x200B;控制台中，按一下右上角的用戶按鈕，然後選擇&#x200B;**通知收件箱**。

   ![screen_shot_2012-02-08at105226am](assets/screen_shot_2012-02-08at105226am.png)

   >[!NOTE]
   >
   >您也可以直接在瀏覽器中存取主控台；例如：
   >
   >
   >` https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. 將會列出您的通知。 您可以視需要採取動作：

   * [訂閱通知](#subscribing-to-notifications)
   * [處理通知](#processing-your-notifications)

   ![chlimage_1-4](assets/chlimage_1-4.jpeg)

## 訂閱通知{#subscribing-to-notifications}

要訂閱通知，請執行以下操作：

1. 開啟通知收件匣：在&#x200B;**網站**&#x200B;控制台中，按一下右上角的用戶按鈕，然後選擇&#x200B;**通知收件箱**。

   ![screen_shot_2012-02-08at105226am-1](assets/screen_shot_2012-02-08at105226am-1.png)

   >[!NOTE]
   >
   >您也可以直接在瀏覽器中存取主控台；例如：
   >
   >
   >`https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. 按一下&#x200B;**配置……** ，開啟設定對話方塊。

   ![screen_shot_2012-02-08at111056am](assets/screen_shot_2012-02-08at111056am.png)

1. 選取通知通道：

   * **收件匣**:通知會顯示在您的AEM收件匣中。
   * **電子郵件**:通知會以電子郵件傳送至您使用者設定檔中定義的電子郵件地址。

   >[!NOTE]
   >
   >需要設定一些設定，才能透過電子郵件收到通知。 您也可以自訂電子郵件範本，或為新語言新增電子郵件範本。 請參閱[設定電子郵件通知](/help/sites-administering/notification.md#configuringemailnotification)以在AEM中設定電子郵件通知。

1. 選取要通知的頁面動作：

   * 已激活：頁面啟動時。
   * 停用：頁面已停用時。
   * 已刪除（聯合）:刪除複製頁面時，即複製頁面上執行的刪除動作時。
刪除或移動頁面時，會自動複製刪除動作：該頁將在執行刪除操作的源實例和複製代理定義的目標實例上刪除。

   * 已修改：頁面修改時。
   * 已建立：建立頁面時。
   * 已刪除：頁面刪除動作刪除頁面時。
   * 推出：當頁面已推出時。

1. 定義要通知您的頁面路徑：

   * 按一下&#x200B;**Add**&#x200B;將新行添加到表中。
   * 按一下&#x200B;**路徑**&#x200B;表格儲存格並輸入路徑，例如`/content/docs`。

   * 要通知屬於子樹的所有頁，請設定&#x200B;**Exact?** 變 **更為否**。若只要收到路徑所定義之頁面上動作的通知，請設定&#x200B;**完全？** 設為 **是**。

   * 若要允許規則，請將&#x200B;**Rule**&#x200B;設定為&#x200B;**Allow**。 如果設為&#x200B;**Deny**，則規則被拒絕，但未被刪除，以後可以允許。

   若要移除定義，請按一下表格儲存格並按一下「**刪除**」來選取列。

1. 按一下&#x200B;**OK**&#x200B;以儲存配置。

## 處理通知{#processing-your-notifications}

如果您已選擇在AEM收件匣中接收通知，您的收件匣將會填入通知。 您可以[檢視通知](#viewing-your-notifications)，然後選取所需通知以：

* 按一下&#x200B;**核准**&#x200B;以核准：**Read**&#x200B;欄中的值設為&#x200B;**true**。

* 按一下&#x200B;**Delete**&#x200B;以刪除它。

![chlimage_1-5](assets/chlimage_1-5.jpeg)
