---
title: We.Finance汽車保險續約參考網站漫談
seo-title: We.Finance Auto Insurance Renewal reference site walkthrough
description: We.Finance汽車保險續約參考網站漫談
uuid: c749a6f7-71f1-4f47-b824-9c7b699072c7
contentOwner: dekalra
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
discoiquuid: ad450124-49a5-4afb-aac3-ed3733d6504b
docset: aem65
exl-id: b6ded6ac-4fb1-49f9-b272-16774c3e89a3
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---

# We.Finance汽車保險續約參考網站漫談{#we-finance-auto-insurance-renewal-reference-site-walkthrough}

## We.Finance參考站點方案  {#we-finance-reference-site-scenario}

We.Finance網站是一個金融服務網站，旨在幫助您學習AEM Forms的互動式通信功能。

閱讀We.Finance汽車保險使用案例的詳細演示，該演示將如何AEM表單以及與Microsoft動力的整合，幫助在金融服務公司中個性化客戶體驗。 互動演練旨在簡化金融公司複雜數字交易和客戶溝通的實施。

**旅程從使用案例開始：**

Sarah Rose是We.Finance的現有客戶，已購買汽車保險單。 現在是一年中她的保險單延期的時候。 Gloria Rios,We.Finance保險代理，向Sarah發出關於她續保的提醒。 Sarah按照電子郵件中提供的說明完成該過程。

## 汽車保險申請漫遊 {#auto-insurance-application-walkthrough}

We.Finance自動保險應用方案是用戶的可視旁白，它基於兩個角色：

* 莎拉·羅絲，We.Finance的客戶
* Gloria Rios，我們金融保險代理

### Gloria從We.Finance發送保險單續訂通信 {#gloria-sends-an-insurance-policy-renewal-communication-from-we-finance}

Gloria登錄實AEM例，按一下 **汽車保險續保，** 然後點擊 **開啟代理UI。**&#x200B;按一下此按鈕將預先填充保險文檔，其中包含Sarah Rose的保單詳細資訊。 格洛麗亞點擊&#x200B;**提交** 在「提交已啟動」螢幕上顯示一條消息，然後在幾秒內顯示「已成功提交」。

Sarah收到一封郵件，主題是「您的汽車保險續期」。

![Agent UI](assets/agent_ui_email_new.png)

#### 親眼看看 {#see-it-yourself}

轉到 **Adobe Experience Manager** > **Forms** > **Forms和文檔** > **We.Finance** > **汽車保險**。 選擇汽車保險續訂 **交互通信** 按一下 **開啟代理UI**。 交互通信在代理UI中開啟。 輸入有效的電子郵件地址以接收附加策略文檔的電子郵件，然後按一下「提交」。

您可以直接從訪問和複查「汽車保險續訂」互動式通信 `https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal.`

### Sarah收到We.Finance發來的保險單續訂通信，並決定續訂 {#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}

Sarah收到一封附有We.Finance附件的電子郵件，提醒她她的汽車保險政策即將到期。 附件是她的汽車保險信的印刷版。

莎拉點擊 **立即續訂** 並指向她的汽車保險信的網路版。 在此信的上方，Sarah會找到其策略到期的剩餘天數。 該頁為Sarah提供了基本的保單詳細資訊（如保單編號、到期金額）以及折扣優惠和忠誠獎勵等其他資訊的概述。 莎拉又點擊了 **立即續訂** 在政策的底層。

![ref1](assets/ref1.png)

#### 它的工作原理 {#how-it-works}

您的汽車保險信函的Web和打印輸出是使用Interactive Communications的多通道功能建立的。

電子郵件中的「立即續訂」按鈕連結到「汽車保險續訂」應用程式，該應用程式是發佈實例上的互動式通信。

#### 親眼看看 {#see-it-yourself-1}

您一定收到了一封帶有附加PDF的電子郵件。 PDF是您的汽車保險信函的打印版本。 按一下 **立即續訂** 訪問策略的Web版本。 檢查您的個人資訊和策略詳細資訊，然後按一下 **立即續訂** 這會帶你進入另一個互動交流。

的 **立即續訂** 按鈕，將Sarah引導到策略的Web版本。 您可以訪問以下URL:

`https://[authorServer]:[authorPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=1`

您可以檢查汽車保險續訂的詳細摘要，然後按一下 **立即續訂** 在頁面底部。

### 莎拉到付款頁 {#sarah-reaches-the-payment-page}

We.Finance將Sarah帶到付款頁。 Sarah用其記錄重新檢查其策略編號和到期日。 在頁面右側，她檢查其續訂的「付款摘要」，其總金額有10%的溢價折扣。

#### 它的工作原理 {#how-it-works-1}

「立即續訂」按鈕將Sarah引導至付款頁。 付款頁是自適應表單。

#### 親眼看看 {#see-it-yourself-2}

按一下 **立即續訂** 到付款頁面。 填寫信用卡資訊，然後按一下 **付款**。

您可以在以下位置訪問創作實例中的付款頁：

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=1`

### 莎拉付了錢，完成了這個過程 {#sarah-makes-the-payment-and-completes-the-process}

Sarah填寫信用卡詳細資訊並點擊 **付款**。

#### 它的工作原理 {#how-it-works-2}

當Sarah填寫信用卡詳細資訊並按一下「提交」時，將處理她的信用卡付款，螢幕上將顯示以自適應表單配置的感謝消息。

#### 親眼看看 {#see-it-yourself-3}

按一下「付款」後，您可以查看確認消息

`https://[authorServer]:[authorPort]/content/forms/af/we-finance/credit-card/ccbillpayment/jcr:content/guideContainer.guideThankYouPage.html?owner=admin&status=Submitted`
