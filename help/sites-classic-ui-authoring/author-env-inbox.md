---
title: 您的收件匣
description: 您可以從AEM的各種區域接收通知，例如有關工作專案的通知或代表您必須在頁面內容上執行之動作的任務。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 52ea2ca2-eb1c-4bed-b52d-feef37c6afd6
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 1%

---

# 您的收件匣{#your-inbox}

您可以從AEM的各種區域接收通知，例如有關工作專案的通知或代表您必須在頁面內容上執行之動作的任務。

您會在兩個收件匣中收到這些通知，收件匣依通知型別分隔：

* 下節將介紹您可在其中檢視因訂閱而收到之通知的收件匣。
* 工作流程專案的專用收件匣在[參與工作流程](/help/sites-classic-ui-authoring/classic-workflows-participating.md)檔案中進行了說明。

## 檢視您的通知 {#viewing-your-notifications}

若要檢視您的通知：

1. 開啟通知收件匣：在&#x200B;**網站**&#x200B;主控台中，按一下右上角的[使用者]按鈕，然後選取&#x200B;**通知收件匣**。

   ![screen_shot_2012-02-08at105226am](assets/screen_shot_2012-02-08at105226am.png)

   >[!NOTE]
   >
   >您也可以直接在瀏覽器中存取主控台；例如：
   >
   >
   >` https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. 系統會列出您的通知。 您可以視需要執行動作：

   * [訂閱通知](#subscribing-to-notifications)
   * [處理您的通知](#processing-your-notifications)

   ![chlimage_1-4](assets/chlimage_1-4.jpeg)

## 訂閱通知 {#subscribing-to-notifications}

若要訂閱通知：

1. 開啟通知收件匣：在&#x200B;**網站**&#x200B;主控台中，按一下右上角的[使用者]按鈕，然後選取&#x200B;**通知收件匣**。

   ![screen_shot_2012-02-08at105226am-1](assets/screen_shot_2012-02-08at105226am-1.png)

   >[!NOTE]
   >
   >您也可以直接在瀏覽器中存取主控台；例如：
   >
   >
   >`https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. 按一下左上角的&#x200B;**設定……**&#x200B;以開啟設定對話方塊。

   ![screen_shot_2012-02-08at111056am](assets/screen_shot_2012-02-08at111056am.png)

1. 選取通知通道：

   * **收件匣**：通知會顯示在AEM收件匣中。
   * **電子郵件**：通知會以電子郵件傳送至您使用者設定檔中定義的電子郵件地址。

   >[!NOTE]
   >
   >必須設定一些設定，才能透過電子郵件接收通知。 您也可以自訂電子郵件範本，或新增新語言的電子郵件範本。 請參閱[設定電子郵件通知](/help/sites-administering/notification.md#configuringemailnotification)以在AEM中設定電子郵件通知。

1. 選取要通知的頁面動作：

   * 已啟動：頁面已啟動時。
   * 已停用：頁面已停用時。
   * 已刪除（整合）：當頁面已經刪除復寫時，亦即復寫在頁面上執行的刪除動作時。
刪除或移動頁面時，會自動復寫刪除動作：執行刪除動作的來源執行處理以及復寫代理程式定義的目的地執行處理上，將會刪除頁面。

   * 已修改：頁面已修改時。
   * 已建立：頁面已建立時。
   * 已刪除：透過頁面刪除動作刪除頁面時。
   * 已轉出：頁面已轉出時。

1. 定義您將收到通知的頁面的路徑：

   * 按一下&#x200B;**新增**&#x200B;以新增資料列至資料表。
   * 按一下&#x200B;**路徑**&#x200B;資料表儲存格並輸入路徑，例如`/content/docs`。

   * 若要收到屬於子樹狀結構之所有頁面的通知，請將&#x200B;**設定為精確？**&#x200B;至&#x200B;**否**。
若要僅收到路徑所定義之頁面上動作的通知，請設定**精確？**&#x200B;至&#x200B;**是**。

   * 若要允許規則，請將&#x200B;**規則**&#x200B;設定為&#x200B;**允許**。 若設為&#x200B;**Deny**，則系統會拒絕該規則，但不會將其移除，之後可允許該規則。

   若要移除定義，請按一下表格儲存格，然後按一下&#x200B;**刪除**&#x200B;來選取列。

1. 按一下&#x200B;**確定**&#x200B;以儲存組態。

## 處理您的通知 {#processing-your-notifications}

如果您已選擇在AEM收件匣中接收通知，則收件匣會填滿通知。 您可以[檢視您的通知](#viewing-your-notifications)，然後選取必要的通知：

* 按一下&#x200B;**核准**&#x200B;接受它： **讀取**&#x200B;資料行中的值設定為&#x200B;**true**。

* 按一下&#x200B;**刪除**&#x200B;以排除它。

![chlimage_1-5](assets/chlimage_1-5.jpeg)
