---
title: HTTP2傳送內容
description: 瞭解HTTP/2如何改善瀏覽器和伺服器的通訊方式，以加快資訊傳輸，同時降低所需的處理能力。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
exl-id: 9eb9f309-33e5-4694-84d2-fb2cd3de50a6
feature: Publishing,Configuration
solution: Experience Manager, Experience Manager Assets
source-git-commit: 20d6c716b4ba799a7d4ae2858459f7c38cf3da02
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 3%

---

# HTTP/2 內容傳送 {#http-delivery-of-content}

Adobe 很榮幸宣佈推出有助於提升整體效能的 HTTP/2 內容傳送。

>[!NOTE]
>
>此功能需要您使用Adobe Experience Manager Dynamic Media隨附的現成可用CDN。 此功能不支援任何其他自訂CDN。

## 什麼是HTTP/2？ {#what-is-http}

HTTP/2可改善瀏覽器和伺服器的通訊方式，實現更快的資訊傳輸，同時降低所需的處理能力。

以下網站以簡單扼要的方式說明HTTP/2及其優點：

[關於HTTP/2您必須知道的事項](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html)

## 改用HTTP/2進行內容傳送的主要優點為何？ {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

效能提升可能大相逕庭。 其基礎許多因素，例如網站程式碼、您使用Dynamic Media的方式、消費者的裝置、畫面和位置等。

Adobe自己的測試產生以下結果：

* 針對影像，回應時間改善7%至28%，視裝置和瀏覽器而定。 效能提升最明顯的是iOS裝置。
* 對於檢視器而言，載入時間效能提升了15%。

<!--
The following demonstration illustrates the difference between HTTP/1 versus HTTP/2 loading:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)
-->

## 我是否符合切換至HTTP/2的資格？ {#am-i-eligible-to-switch-over-to-http}

若要使用HTTP/2，您必須符合下列要求：

* 針對您的多媒體請求使用安全HTTPS。
* 使用Adobe隨附的CDN （內容傳遞網路），作為Dynamic Media授權的一部分。
* 使用專用（非company-h.assetsadobe#.com）網域。

  如果您已有專屬網域，則可透過Adobe客戶支援選擇加入。

  如果您沒有專用網域，Adobe計畫在2018年安排轉換至HTTP/2。

## 為我的Dynamic Media帳戶啟用HTTP/2的程式為何？ {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

You initiate the request to switch over to HTTP/2; it is not automatically done for you.

1. To switch over to HTTP/2, initiate an Adobe Customer Support request. See [Open a support ticket](https://experienceleague.adobe.com/zh-hant?support-solution=General&lang=en&support-tab=home#support).

   1. Provide the following information in your support request:

      1. Primary contact name, email, phone.
      1. All domains to be transitioned over to HTTP/2.
      1. Verify that you use secure HTTPS for rich media requests.
      1. Verify that you use the CDN through Adobe and are not managed with a direct relationship.
      1. Verify that you use a dedicated domain. If you use Dynamic Media, then you use a dedicated domain.

   1. Customer Support adds you to the HTTP/2 customer waitlist based in the order in which requests were submitted.
   1. When Adobe is ready to handle your request, Customer Support contacts you to coordinate the transition and set a target date.
   1. You are notified after completion and can verify successful transition over to HTTP2.

      Because the browser does not state this fact, it is necessary to download an extension.

      For Firefox and Chrome, there is an extension called &quot;HTTP/2 and SPDY Indicator.&quot; Browsers only support http/2 securely, so it is necessary to call a URL with https to verify. If http/2 is supported, the extension indicates i. The extension is in the form of a blue Flash symbol, and a header `X-Firefox-Spdy` : `h2`.

## When can I expect the transition to HTTP/2 to occur? {#when-can-i-expect-to-be-transitioned-over-to-http}

Requests are processed in the order in which Customer Support receives them.

>[!NOTE]
>
>There can be a long lead time because the transition to HTTP/2 involves clearing the cache. Therefore, only a few customer transitions can be handled at a time.

## What are the risks with moving to HTTP/2? {#what-are-the-risks-with-moving-to-http}

The transition to HTTP/2 clears out your cache at the CDN because it involves moving to a new CDN configuration.

The non-cached content directly hits Adobe&#39;s origin servers until the cache is rebuilt again. 因此，Adobe計劃一次處理幾個客戶轉換，以便在從來源提取請求時維持可接受的效能。

## 如何確認URL或網站是否以HTTP/2啟動？ {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

由於瀏覽器未說明此事實，因此必須下載擴充功能。

Firefox和Chrome有一個擴充功能，稱為「HTTP/2和SPDY Indicator」。 瀏覽器僅安全地支援http/2，因此有必要呼叫具有https的URL以進行驗證。 如果支援http/2，擴充功能會加以指示。 擴充功能採用藍色Flash符號和標題`X-Firefox-Spdy`的形式： `h2`。
