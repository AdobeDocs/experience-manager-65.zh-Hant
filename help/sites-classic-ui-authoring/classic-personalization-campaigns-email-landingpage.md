---
title: 建立有效的新聞簡報登錄頁
seo-title: Creating an Effective Newsletter Landing Page
description: 有效的新聞簡報登錄頁可幫助您讓盡可能多的人註冊您的新聞簡報（或其他電子郵件營銷活動）。 您可以使用您從新聞簡報註冊中收集到的資訊獲得線索。
seo-description: An effective newsletter landing page helps you get as many people as possible to sign up for your newsletter (or other email marketing campaign). You can use the information you gather from your newsletter sign ups to get leads.
uuid: 0799b954-076b-4e95-8724-3661ae8fddb6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: b41de64a-7d27-4633-a8d5-ac91d47eb1bb
docset: aem65
exl-id: c2fbf858-8815-426e-a2e5-f92bcf909ad0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 0%

---

# 建立有效的新聞簡報登錄頁{#creating-an-effective-newsletter-landing-page}

有效的新聞簡報登錄頁可幫助您讓盡可能多的人註冊您的新聞簡報（或其他電子郵件營銷活動）。 您可以使用您從新聞簡報註冊中收集到的資訊獲得線索。

要建立有效的新聞簡報登錄頁，您需要執行以下操作：

1. 為新聞稿建立清單，以便用戶訂閱該新聞稿。
1. 建立註冊表單。 執行此操作時，添加一個工作流步驟，該步驟會自動將註冊此新聞稿的人員添加到您的銷售線索清單中。
1. 建立「確認」頁，感謝用戶的註冊，並可能為他們提供促銷。
1. 添加茶具。

>[!NOTE]
>
>Adobe不打算進一步增強此功能（管理銷售線索和清單）。
>建議是利用 [Adobe Campaign和AEM](/help/sites-administering/campaign.md)。

## 為新聞簡報建立清單 {#creating-a-list-for-the-newsletter}

建立清單，例如， **Geometrixx通訊**&#x200B;在MCM，為人們訂閱的通訊。 建立清單的說明，請參見 [建立清單](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingnewlists)。

下面顯示了清單示例：

![mcm_listcreate](assets/mcm_listcreate.png)

## 建立註冊表 {#create-a-sign-up-form}

建立新聞稿註冊表，允許用戶訂閱標籤。 示例Geometrixx網站在Geometrixx工具欄中提供新聞簡報頁面，您可以在該頁面建立表單。

要建立您自己的新聞稿表單，請參閱 [Forms文檔](/help/sites-authoring/default-components.md#form)。 新聞稿使用標籤庫中的標籤。 要添加其他標籤，請參見 [標籤管理](/help/sites-authoring/tags.md#tagadministration)。

以下示例中的隱藏欄位提供了最少裸資訊量（電子郵件）;此外，您以後可以添加更多欄位，但這將影響轉換率。

以下示例是在https://localhost:4502/cf#/content/geometrixx/en/toolbar/newsletter.html上建立的表單。

1. 建立窗體。

   ![mcm_ellesterpage](assets/mcm_newsletterpage.png)

1. 按一下 **編輯** 在「表單」元件中，將表單配置為轉到「感謝」頁(請參見 [建立感謝頁](#creating-a-thank-you-page))。

   ![dc_formstart_thankyou](assets/dc_formstart_thankyou.png)

1. 設定「表單」(Form)操作（即在您提交表單時將發生的情況），並配置組以將註冊用戶分配給您以前建立的清單（例如geometrixx-swelter）。

   ![dc_formstart_thankyouadvanced](assets/dc_formstart_thankyouadvanced.png)

### 建立「感謝」頁 {#creating-a-thank-you-page}

當用戶按一下 **立即訂閱**，希望自動開啟「感謝」頁。 在「Geometrixx新聞簡報」頁面中建立「感謝」頁。 建立新聞簡報表單後，編輯表單元件並將路徑添加到感謝頁。

提交請求將用戶帶到 **謝謝** 之後他們將收到一封電子郵件。 此「感謝」頁建立於/content/geometrixx/en/toolbar/selletter/thank_you。

![mcm_selstrey_thankyoupage](assets/mcm_newsletter_thankyoupage.png)

### 添加預告器 {#adding-teasers}

添加 [沖茶器](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers) 針對特定受眾。 例如，您可以將預告添加到「感謝您」頁和「新聞簡訊」註冊頁。

要添加預告以建立有效的新聞簡報登錄頁，請執行以下操作：

1. 為註冊禮品建立預告段落。 選擇 **第一個** 作為策略，並包含通知他們將收到什麼禮物的文本。

   ![dc_teaser_thankyou](assets/dc_teaser_thankyou.png)

1. 為「謝謝」頁建立預告段落。 選擇 **第一個** 作為策略，並包含表示禮品即將送達的文本。

   ![chlimage_1-103](assets/chlimage_1-103.png)

1. 使用兩個預告建立市場活動 — 將一個標籤為業務，另一個標籤為未標籤。

### 將內容推送到訂閱者 {#pushing-content-to-subscribers}

通過MCM中的新聞簡訊功能推送對頁面所做的任何更改。 然後將更新的內容推送到訂閱者。

請參閱 [正在發送新聞稿](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters)。
