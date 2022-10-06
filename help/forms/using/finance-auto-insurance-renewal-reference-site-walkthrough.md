---
title: We.金融汽車保險續訂參考網站逐步說明
seo-title: We.Finance Auto Insurance Renewal reference site walkthrough
description: We.金融汽車保險續訂參考網站逐步說明
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

# We.金融汽車保險續訂參考網站逐步說明{#we-finance-auto-insurance-renewal-reference-site-walkthrough}

## We.Finance參考站點方案  {#we-finance-reference-site-scenario}

We.Finance網站是金融服務網站，旨在幫助您了解AEM Forms的互動式通訊功能。

閱讀We.Finance汽車保險使用案例的詳細逐步說明，展示AEM表單及其與Microsoft Dynamics的整合如何協助個人化金融服務公司的客戶體驗。 互動式逐步說明旨在簡化金融公司複雜數位交易和客戶通訊的實作。

**歷程從使用案例開始：**

莎拉·羅絲是We.Finance的現有客戶，已購買了汽車保險單。 現在是她的保險單續期的時候。 We.Finance保險代理Gloria Rios向Sarah發送了關於她保單續期的提醒。 Sarah遵循電子郵件中提供的指示，並成功完成此程式。

## 自動保險應用程式逐步說明 {#auto-insurance-application-walkthrough}

We.Finance自動保險應用程式案例是用戶的視覺旁白，並基於以下兩個角色：

* We.Finance客戶莎拉·羅斯
* Gloria Rios,We.Finance保險代理

### Gloria向We.Finance發送保險單續訂通訊 {#gloria-sends-an-insurance-policy-renewal-communication-from-we-finance}

Gloria登入AEM例項，按一下 **汽車保險續訂，** 然後點按 **開啟代理UI。**&#x200B;按一下「 」，保險單上就會預填Sarah Rose的保單細節。 格洛麗亞點擊次數&#x200B;**提交** 螢幕上會顯示一條消息「已啟動提交」，然後在幾秒內顯示「已成功提交」。

Sarah收到一封電子郵件，主題是「您的汽車保險續訂」。

![Agent UI](assets/agent_ui_email_new.png)

#### 你自己看 {#see-it-yourself}

前往 **Adobe Experience Manager** > **Forms** > **Forms與檔案** > **We.Finance** > **汽車保險**. 選擇自動保險續訂 **互動通信** 按一下 **開啟代理UI**. 互動式通訊會在代理程式UI中開啟。 輸入有效的電子郵件地址以接收附加策略文檔的電子郵件，然後按一下「提交」。

您可以直接從訪問和查看「汽車保險續訂」交互通信 `https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal.`

### Sarah收到We.Finance發來的保險單續訂通訊，並決定續訂 {#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}

Sarah收到一封來自We.Finance的附件電子郵件，提醒她汽車保險政策即將到期。 附件是她的汽車保險信的打印版本。

Sarah點擊 **立即續訂** 並導向至她的汽車保險信網頁版。 在此信的上方，Sarah會找到政策到期的剩餘天數。 該頁為Sarah提供了保險單詳細資訊的基本概覽，如保單編號、到期金額，以及折扣優惠和忠誠獎勵等其他資訊。 莎拉又點了 **立即續訂** 在政策的底層。

![ref1](assets/ref1.png)

#### 運作方式 {#how-it-works}

您的汽車保險信的Web和打印輸出是使用Interactive Communications的多通道功能建立的。

電子郵件中的「立即續約」按鈕會連結至「汽車保險續約」應用程式，此應用程式是發佈執行個體上的互動式通訊。

#### 你自己看 {#see-it-yourself-1}

您必須已收到附加PDF的電子郵件。 PDF是您的汽車保險信的打印版本。 按一下 **立即續訂** 以訪問策略的Web版本。 查看您的個人資訊和策略詳細資訊，然後按一下 **立即續訂** 將您帶到另一個互動式通信。

此 **立即續訂** 電子郵件中的按鈕會將Sarah引導到策略的Web版本。 您可以造訪下列URL:

`https://[authorServer]:[authorPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=1`

您可以檢查汽車保險續訂的詳細摘要，然後按一下 **立即續訂** 頁面底部。

### Sarah到達付款頁面 {#sarah-reaches-the-payment-page}

We.Finance將Sarah帶到「付款」頁。 Sarah會重新檢查其「政策編號」和「到期日」，並附上記錄。 在頁面的右側，她檢查續訂的「付款摘要」，其總金額有10%的溢價折扣。

#### 運作方式 {#how-it-works-1}

「立即續訂」按鈕將Sarah引導到付款頁。 付款頁面是最適化表單。

#### 你自己看 {#see-it-yourself-2}

按一下 **立即續訂** 以到達「付款」頁。 填寫您的信用卡資訊，然後按一下 **付款**.

您可以前往製作執行個體中的付款頁面，網址為

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=1`

### Sarah付款並完成流程 {#sarah-makes-the-payment-and-completes-the-process}

Sarah會填寫信用卡詳情和點按次數 **付款**.

#### 運作方式 {#how-it-works-2}

當Sarah填寫信用卡詳細資訊並按一下「提交」時，將處理她的信用卡付款，螢幕上將顯示以最適化表單配置的感謝消息。

#### 你自己看 {#see-it-yourself-3}

按一下「付款」後，您可以檢視確認訊息(位於

`https://[authorServer]:[authorPort]/content/forms/af/we-finance/credit-card/ccbillpayment/jcr:content/guideContainer.guideThankYouPage.html?owner=admin&status=Submitted`
