---
title: 管理訂閱
seo-title: Managing Subscriptions
description: 在網頁上使用的表單元件的幫助下，可以要求用戶訂閱電子郵件服務提供商的郵件AEM清單。 要準備具有AEM註冊表的頁面以訂閱電子郵件服務郵件清單，您必須將相應的服務配置應AEM用到潛在訂閱者將訪問的頁面。
seo-description: Users can be asked to subscribe to Email Service Provider's mailing lists with the help of the Form component used on an AEM web page. To prepare an AEM page with a sign-up form for subscription to your e-mail service mailing lists, you must apply the corresponding service configuration to the AEM page that the potential subscriber will visit.
uuid: b2578a3d-dba1-4114-b21a-5f34c0cccc5a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 295cb0a6-29db-42aa-824e-9141b37b5086
exl-id: add05d22-3a11-49e9-a554-2315962552d5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 1%

---

# 管理訂閱{#managing-subscriptions}

>[!NOTE]
>
>Adobe不打算進一步增強此功能（管理銷售線索和清單）。
>建議是利用 [Adobe Campaign及其整AEM合](/help/sites-administering/campaign.md)。

可以要求用戶訂閱 **電子郵件服務提供商** 郵件清單 **窗體** 用於網頁的AEM元件。 要準備具有AEM註冊表的頁面以訂閱電子郵件服務郵件清單，您必須將相應的服務配置應AEM用到潛在訂閱者將訪問的頁面。

## 將電子郵件服務配置應用於頁面 {#applying-email-service-configuration-to-a-page}

配置頁AEM面：

1. 導航到 **網站** 頁籤。
1. 選擇需要為服務配置的頁。 按一下右鍵頁面並選擇 **屬性**。

1. 選擇 **Cloud Services** 然後 **添加服務**。 從可用配置清單中選擇配置。

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. 按一下&#x200B;**「確定」**。

## 在頁面上建立註冊表AEM以訂閱/取消訂閱清單 {#creating-a-sign-up-form-on-an-aem-page-for-subscribing-unsubscribing-to-lists}

要建立註冊表並將其配置為訂閱電子郵件服務提供商的郵件清單，請執行以下操作：

1. 開啟AEM用戶將訪問的頁面。
1. 將電子郵件服務提供商的配置應用到該頁。

1. 添加 **窗體** 將元件從側鍵拖動到頁面。 如果元件不可用，請切換到設計模式並啟用 **窗體** 組。
1. 按一下 **編輯** 的 **窗體開頭** 欄，然後導航到 **高級** 頁籤。
1. 在 **窗體** 下拉菜單，選擇 **電子郵件服務：建立訂閱伺服器** 並添加到清單。
1. 在對話框底部，開啟 **操作配置** 下拉框，允許您選擇一個或多個訂閱清單。
1. 在 **選擇清單**，選擇希望用戶訂閱的清單。 可以使用加號按鈕(**添加項**)。

   ![chlimage_1-10](assets/chlimage_1-10.jpeg)

   >[!NOTE]
   >
   >您的對話框可能因電子郵件服務提供商而異。

1. 在 **窗體** 頁籤，選擇希望用戶在提交表單後轉到的「感謝」頁（如果留空，則在提交時表單將重新顯示）。 按一下&#x200B;**「確定」**。安 **電子郵件ID** 元件顯示在表單中，您可以建立一個表單，在該表單中，用戶可以提交其電子郵件地址以訂閱或取消訂閱郵件清單。
1. 添加 **提交** 按鈕元件 **窗體** 分身。

   表格已準備好。 發佈在上述步驟中配置的頁面以及 **謝謝** 頁。 任何潛在訂閱者訪問該頁面都可以填寫表單並訂閱配置中提供的清單。

   >[!NOTE]
   >
   >要使表單訂閱功能正確， [需要在發佈實例上導出和導入來自作者的加密密鑰](#exporting-keys-from-author-and-importing-on-publish)。

## 從作者導出密鑰並在發佈時導入 {#exporting-keys-from-author-and-importing-on-publish}

要通過發佈實例上的註冊表訂閱和取消訂閱電子郵件服務，您需要執行以下步驟：

1. 在作者實例上，導航到包管理器。
1. 建立新包。 將篩選器設定為 `/etc/key`。
1. 生成並下載包。
1. 導航到發佈實例上的包管理器並上載此包。
1. 導航到「發佈」控制台並重新啟動名為 **Adobe花崗岩加密支援**。

## 從清單中取消訂閱用戶 {#unsubscribing-users-from-lists}

要從清單中取消訂閱用戶：

1. 開啟具有註冊表AEM單以取消訂閱潛在顧客的頁面的頁面屬性。
1. 將服務配置應用於頁面。
1. 在頁面上建立註冊表單。
1. 配置元件時，選擇操作 **電子郵件服務**: **從清單中取消訂閱用戶。**
1. 從下拉菜單中，選擇取消訂閱時將從中刪除用戶的相應清單。

   ![chlimage_1-11](assets/chlimage_1-11.jpeg)

1. 導出要發佈的作者的密鑰。

## 為電子郵件服務配置自動響應程式電子郵件 {#configuring-auto-responder-emails-for-email-service}

要為訂閱者配置自動響應程式電子郵件：

1. 開啟具有註冊表AEM格以配置潛在顧客的自動響應程式的頁面的頁面屬性。
1. 將ExactTarget配置應用於頁面。

1. 添加 **窗體** 將元件從側鍵拖動到頁面。 如果元件不可用，請切換到設計模式並啟用 **窗體** 組。
1. 按一下 **編輯** 的 **窗體開頭** 欄，然後導航到 **高級** 頁籤。
1. 在 **窗體** 下拉菜單，選擇 **電子郵件服務：發送自動響應程式電子郵件。**
1. **選擇電子郵件** （這是作為自動響應者電子郵件發送的郵件）。

1. **選擇分類** （此分類用於發送電子郵件）。
1. 選擇 **謝謝** 頁面（用戶提交表單後即被引導到的頁面）。

   在 **窗體** 頁籤，選擇希望用戶在提交表單後轉到的「感謝」頁。 （如果留空，則提交時表單將重新顯示。） 按一下&#x200B;**「確定」**。

1. 導出要發佈的作者的密鑰。
1. 添加 **提交** 按鈕元件 **窗體** 分身。

   註冊表已準備好。 發佈在上述步驟中配置的頁面以及 **謝謝** 頁。 任何潛在訂閱者訪問該頁面都可以填寫表格，在提交表格時，訪問者將在表格中填寫的電子郵件標識上收到自動應答電子郵件。

   >[!NOTE]
   >
   >要使註冊表訂閱功能正確， [需要在發佈實例上導出和導入來自作者的加密密鑰](#exporting-keys-from-author-and-importing-on-publish)。

   ![chlimage_1-12](assets/chlimage_1-12.jpeg)
