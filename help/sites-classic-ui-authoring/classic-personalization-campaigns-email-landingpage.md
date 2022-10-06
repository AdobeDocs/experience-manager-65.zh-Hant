---
title: 建立有效的電子報登陸頁面
seo-title: Creating an Effective Newsletter Landing Page
description: 有效的電子報登陸頁面可協助您讓盡可能多的人註冊電子報（或其他電子郵件行銷活動）。 您可以使用從電子報註冊中收集的資訊來獲取線索。
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

# 建立有效的電子報登陸頁面{#creating-an-effective-newsletter-landing-page}

有效的電子報登陸頁面可協助您讓盡可能多的人註冊電子報（或其他電子郵件行銷活動）。 您可以使用從電子報註冊中收集的資訊來獲取線索。

若要建立有效的電子報登陸頁面，您必須執行下列動作：

1. 為電子報建立清單，方便人們訂閱電子報。
1. 建立註冊表單。 執行此操作時，新增工作流程步驟，自動將註冊電子報的人員新增至銷售機會清單。
1. 建立「確認」頁面，感謝使用者註冊，並可能提供促銷。
1. 加茶匙。

>[!NOTE]
>
>Adobe不打算進一步增強此功能（管理銷售機會和清單）。
>建議是利用 [Adobe Campaign與AEM整合](/help/sites-administering/campaign.md).

## 建立電子報清單 {#creating-a-list-for-the-newsletter}

建立清單，例如 **Geometrixx電子報**，在MCM上，以取得人們應該訂閱的電子報。 如需建立清單的相關說明，請參閱 [建立清單](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingnewlists).

以下是清單的範例：

![mcm_listcreate](assets/mcm_listcreate.png)

## 建立註冊表單 {#create-a-sign-up-form}

建立電子報註冊表單，讓使用者訂閱標籤。 範例Geometrixx網站會在Geometrixx工具列中提供電子報頁面，供您建立表單。

若要建立自己的電子報表單，請參閱 [Forms檔案](/help/sites-authoring/default-components.md#form). 電子報使用標籤庫中的標籤。 若要新增其他標籤，請參閱 [標籤管理](/help/sites-authoring/tags.md#tagadministration).

以下示例中的隱藏欄位提供了最少量的資訊（電子郵件）;此外，您稍後可以新增更多欄位，但這會影響轉換率。

以下範例是在https://localhost:4502/cf#/content/geometrixx/en/toolbar/newsletter.html建立的表單。

1. 建立表單。

   ![mcm_newsletterpage](assets/mcm_newsletterpage.png)

1. 按一下 **編輯** 在「表單」元件中設定表單以前往感謝頁面(請參閱 [建立感謝頁面](#creating-a-thank-you-page))。

   ![dc_formstart_thankyou](assets/dc_formstart_thankyou.png)

1. 設定Form動作（這是提交表單時會發生的情形）並設定群組，將註冊使用者指派至您先前建立的清單（例如geometrixx-newsletter）。

   ![dc_formstart_thankyouadvanced](assets/dc_formstart_thankyouadvanced.png)

### 建立感謝頁面 {#creating-a-thank-you-page}

當使用者點按 **立即訂閱**，您希望自動開啟「感謝」頁面。 在Geometrixx電子報頁面中建立感謝頁面。 建立電子報表單後，請編輯表單元件並新增路徑至感謝頁面。

提交請求會將使用者帶往 **謝謝** 頁面，之後會收到電子郵件。 此「感謝」頁面是在/content/geometrixx/en/toolbar/newsletter/thank_you建立。

![mcm_newsletter_thankyoupage](assets/mcm_newsletter_thankyoupage.png)

### 添加茶匙 {#adding-teasers}

新增 [茶匙](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers) 來鎖定特定對象。 例如，您可以在「感謝」頁面新增茶匙，並在「電子報」註冊頁面新增茶匙。

若要新增茶匙，以建立有效的電子報登陸頁面：

1. 為註冊禮品建立預告段落。 選擇 **第一個** 作為策略，並加入文字，通知他們將收到哪些禮物。

   ![dc_teaser_thankyou](assets/dc_teaser_thankyou.png)

1. 為感謝頁面建立預告段落。 選擇 **第一個** 作為策略，並包含指示送禮的文字。

   ![chlimage_1-103](assets/chlimage_1-103.png)

1. 使用兩茶匙建立促銷活動 — 標籤一茶匙有生意，另一個沒有標籤。

### 推送內容給訂閱者 {#pushing-content-to-subscribers}

在MCM中透過電子報功能推送任何變更至頁面。 然後您推送更新內容給訂閱者。

請參閱 [傳送電子報](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters).
