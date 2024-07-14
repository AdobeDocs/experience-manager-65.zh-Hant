---
title: 建立有效的Newsletter登陸頁面
description: 有效的電子報登陸頁面可協助您讓儘可能多的使用者註冊您的電子報（或其他電子郵件行銷活動）。 您可以使用從電子報註冊收集到的資訊來取得銷售機會。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: c2fbf858-8815-426e-a2e5-f92bcf909ad0
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# 建立有效的Newsletter登陸頁面{#creating-an-effective-newsletter-landing-page}

有效的電子報登陸頁面可協助您讓儘可能多的使用者註冊您的電子報（或其他電子郵件行銷活動）。 您可以使用從電子報註冊收集到的資訊來取得銷售機會。

若要建立有效的Newsletter登陸頁面，您需要執行下列動作：

1. 建立Newsletter清單，讓使用者可以訂閱Newsletter。
1. 建立登錄檔單。 這樣做時，請新增工作流程步驟，自動將註冊電子報的人員新增到您的潛在客戶清單中。
1. 建立「確認」頁面，感謝使用者註冊，並可能會提供促銷活動。
1. 新增Teaser。

>[!NOTE]
>
>Adobe不打算進一步增強此功能（管理銷售機會和清單）。
>建議使用[Adobe Campaign以及與AEM](/help/sites-administering/campaign.md)的整合。

## 建立Newsletter的清單 {#creating-a-list-for-the-newsletter}

在MCM中建立人員應訂閱之電子報的清單，例如&#x200B;**Geometrixx電子報**。 建立清單的說明請參閱[建立清單](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingnewlists)。

以下顯示清單的範例：

![mcm_listcreate](assets/mcm_listcreate.png)

## 建立登錄檔單 {#create-a-sign-up-form}

建立電子報登錄檔單，讓使用者訂閱標籤。 範例Geometrixx網站在Geometrixx工具列中提供一個新聞稿頁面，您可以在其中建立表單。

若要建立您自己的Newsletter表單，請參閱[Forms檔案](/help/sites-authoring/default-components.md#form)中有關建立表單的資訊。 Newsletter使用標籤庫中的標籤。 若要新增其他標籤，請參閱[標籤管理](/help/sites-authoring/tags.md#tagadministration)。

下列範例中的隱藏欄位提供最低限度的資訊量（電子郵件）；此外，您可以稍後新增更多欄位，但這會影響轉換率。

以下範例是在https://localhost:4502/cf#/content/geometrixx/en/toolbar/newsletter.html建立的表單。

1. 建立表單。

   ![mcm_newsletterpage](assets/mcm_newsletterpage.png)

1. 按一下表單元件中的&#x200B;**編輯**，將表單設定為移至感謝頁面（請參閱[建立感謝頁面](#creating-a-thank-you-page)）。

   ![dc_formstart_thankyou](assets/dc_formstart_thankyou.png)

1. 設定「表單」動作（提交表單時就會發生這種情況），並設定群組以將註冊使用者指派給您先前建立的清單（例如geometrixx-newsletter）。

   ![dc_formstart_thankyouadvanced](assets/dc_formstart_thankyouadvanced.png)

### 建立感謝頁面 {#creating-a-thank-you-page}

當使用者按一下&#x200B;**立即訂閱**&#x200B;時，您想要自動開啟[感謝您]頁面。 在Geometrixx電子報頁面中建立「感謝您」頁面。 建立Newsletter表單後，請編輯表單元件並新增感謝頁面的路徑。

提交要求會將使用者帶往&#x200B;**感謝您**&#x200B;頁面，使用者將在頁面之後收到電子郵件。 此感謝頁面建立於/content/geometrixx/en/toolbar/newsletter/thank_you。

![mcm_newsletter_thankyoupage](assets/mcm_newsletter_thankyoupage.png)

### 新增Teaser {#adding-teasers}

新增[Teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers)以鎖定特定對象。 例如，您可以將Teaser新增至「感謝您」頁面和Newsletter註冊頁面。

若要新增Teaser以產生有效的Newsletter登陸頁面：

1. 為註冊禮物建立Teaser段落。 選取&#x200B;**第一個**&#x200B;作為策略，並包含通知他們將會收到哪些禮品的文字。

   ![dc_teaser_thankyou](assets/dc_teaser_thankyou.png)

1. 為感謝頁面建立Teaser段落。 選取&#x200B;**First**&#x200B;作為策略，並包含表示禮物即將送出的文字。

   ![chlimage_1-103](assets/chlimage_1-103.png)

1. 使用兩個Teaser建立行銷活動 — 標籤一個有業務，另一個沒有標籤。

### 將內容推播給訂閱者 {#pushing-content-to-subscribers}

透過MCM中的Newsletter功能推送任何頁面變更。 接著，您可將更新內容推送至訂閱者。

請參閱[傳送電子報](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters)。
