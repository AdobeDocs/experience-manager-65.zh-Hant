---
title: We.Finance汽車保險續約參考網站逐步說明
seo-title: We.Finance汽車保險續約參考網站逐步說明
description: 'null'
seo-description: 'null'
uuid: c749a6f7-71f1-4f47-b824-9c7b699072c7
contentOwner: dekalra
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
discoiquuid: ad450124-49a5-4afb-aac3-ed3733d6504b
docset: aem65
translation-type: tm+mt
source-git-commit: b2fd6e0412ee0dacf7b68f4a0b219804dd4a6150

---


# We.Finance汽車保險續約參考網站逐步說明{#we-finance-auto-insurance-renewal-reference-site-walkthrough}

## 先決條件 {#pre-requisites}

依設定中所述設定參考網站， [並設定AEM Forms參考網站](../../forms/using/setup-reference-sites.md)。

## We.Finance參考網站藍本 {#we-finance-reference-site-scenario}

We.Finance網站是金融服務網站，旨在協助您學習AEM Forms的互動式通訊功能。

閱讀We.Finance Auto Insurance使用案例的詳細說明，其中展示AEM表單及其與Microsoft Dynamics的整合如何協助在金融服務公司中個人化客戶體驗。 此互動式逐步教學旨在簡化金融公司複雜數位交易和客戶溝通的實作。

**旅程從使用案例開始：**

Sarah rose是We.Finance的現有客戶，已購買汽車保險單。 現在是續約其保險單的一年中之時。 We.Finance保險代理Gloria Rios向Sarah發出關於續保的提醒。 Sarah會依照電子郵件中提供的指示進行，並順利完成程式。

## 自動保險應用程式逐步說明 {#auto-insurance-application-walkthrough}

We.Finance Auto-Insurance應用程式案例是使用者的視覺化旁白，其基礎為兩個角色：

* We.Finance客戶Sarah Rose
* Gloria Rios,We.Finance保險代理

### Gloria從We.Finance傳送保險單續約通訊 {#gloria-sends-an-insurance-policy-renewal-communication-from-we-finance}

Gloria登入AEM例項，按一下「自動 **續約保險」** ，然後按 **一下「開啟代理UI」。**&#x200B;按一下，會預先填入保險檔案中Sarah Rose的保單詳細資訊。 Gloria按一下&#x200B;**「送出」** ，畫面上會顯示訊息「已開始提交」，然後在幾秒內「已成功送出」。

Sarah收到一封電子郵件，主旨是「您的汽車保險續約」。

![Agent UI](assets/agent_ui_email_new.png)

#### 親眼看看 {#see-it-yourself}

前往 **Adobe Experience Manager** > **Forms** > **Documents** ******** We.Finance Insurance > Auto Insurance Insurance。 選擇「自動保險續約」 **互動式通訊** ，然後按 **一下「開啟代理UI**」。 互動式通訊會在Agent UI中開啟。 輸入有效的電子郵件地址以接收附加政策檔案的電子郵件，然後按一下「送出」。

您可以直接從 `https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal.`

### Sarah收到We.Finance的保險單續約通訊，並決定續約 {#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}

Sarah收到一封附件來自We.Finance的電子郵件，提醒她，她的汽車保險政策即將到期。 附件是她的汽車保險信件的印刷版。

Sarah按一 **下「立即續約** 」，並轉至其Auto Insurance信函的網頁版本。 在此信上，Sarah會找出政策到期的剩餘天數。 該頁為Sarah提供其保單詳細資訊（如保單編號、到期金額）的基本概觀，以及折扣優惠和忠誠度獎勵等其他資訊。 Sarah再次按一下 **策略底部的** 「立即續約」。

![ref1](assets/ref1.png)

#### 運作方式 {#how-it-works}

您的汽車保險信函的網路和印刷輸出是使用互動式通訊的多頻道功能建立。

電子郵件中的「立即續約」按鈕會連結至「自動保險續約」應用程式，此應用程式是發佈例項上的互動式通訊。

#### 親眼看看 {#see-it-yourself-1}

您必須已收到附加PDF的電子郵件。 PDF是您的汽車保險信函的列印版本。 按一 **下「立即續約** 」以存取Web版的原則。 查看您的個人資訊和政策詳細資訊，然後按一 **下立即續約** ，您就可以進入另一個互動式通訊。

電 **子郵件中的** 「立即續約」按鈕會將Sarah引導至原則的Web版本。 您可以造訪下列URL:

`https://[authorServer]:[authorPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=1`

您可以查看汽車保險續約的詳細摘要，然後按一下頁 **面底部的** 「立即續約」。

### Sarah進入付款頁面 {#sarah-reaches-the-payment-page}

We.Finance將Sarah帶到「付款」頁面。 Sarah會重新檢查其記錄中的政策編號和到期日。 在頁面的右側，她會以總金額的10%優惠折扣來檢查續約的「付款摘要」。

#### 運作方式 {#how-it-works-1}

「立即續約」按鈕會將Sarah引導至付款頁面。 付款頁面是最適化表單。

#### 親眼看看 {#see-it-yourself-2}

按一 **下「立即續約** 」以進入「付款」頁面。 填寫您的信用卡資訊，然後按一下「 **付款」**。

您可以在以下網址的撰寫例項中，進入付款頁面：

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=1`

### Sarah付了錢，完成了整個流程 {#sarah-makes-the-payment-and-completes-the-process}

Sarah會填寫信用卡詳細資訊，並按一下「 **付款」**。

#### 運作方式 {#how-it-works-2}

當Sarah填寫信用卡詳細資訊並按一下「送出」時，會處理她的信用卡付款，螢幕上會出現以最適化表單設定的感謝訊息。

#### 親眼看看 {#see-it-yourself-3}

您可以在按一下「付款於」後檢視確認訊息

`https://[authorServer]:[authorPort]/content/forms/af/we-finance/credit-card/ccbillpayment/jcr:content/guideContainer.guideThankYouPage.html?owner=admin&status=Submitted`
