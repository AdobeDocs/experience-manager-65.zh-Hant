---
title: HTTP2內容傳送
description: HTTP/2改善了瀏覽器和伺服器通訊的方式，讓資訊傳輸更快速，同時降低了所需的處理能力。
uuid: d9deb945-bdf5-4d6b-95c8-8bae4442e618
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: c8e145ad-f021-4043-8190-62151775e296
role: Business Practitioner, Administrator
exl-id: 9eb9f309-33e5-4694-84d2-fb2cd3de50a6
feature: Publishing,Configuration
translation-type: tm+mt
source-git-commit: c9aec973faf4caef741961d92a6f258646aeddb7
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 2%

---

# HTTP/2內容傳送{#http-delivery-of-content}

Adobe 很榮幸宣佈推出有助於提升整體效能的 HTTP/2 內容傳送。

>[!NOTE]
>
>此功能需要您使用隨附於Adobe Experience Manager·Dynamic Media的現成可用CDN。 此功能不支援任何其他自訂CDN。

## 什麼是HTTP/2?{#what-is-http}

HTTP/2改善了瀏覽器和伺服器通訊的方式，讓資訊傳輸更快速，同時降低了所需的處理能力。

以下網站以簡單簡單的方式說明HTTP/2及其優點：

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## 轉換至HTTP/2以進行內容傳送的主要優點為何？{#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

效能的改善可能會有很大不同。 它以許多因素為基礎，例如您網站的程式碼、您使用Dynamic Media、消費者的裝置、螢幕和位置。

Adobe的自行測試得出如下結果：

* 對於影像，視裝置和瀏覽器而定，回應時間提高了7%至28%。 在iOS裝置上，效能提升最顯著。
* 對於檢視器，載入時間效能提升了15%。

下列展示說明HTTP/1與HTTP/2載入之間的差異：

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## 我是否符合切換至HTTP/2的資格？{#am-i-eligible-to-switch-over-to-http}

若要使用HTTP/2，您必須符合下列需求：

* 針對您的豐富式媒體要求使用安全的HTTPS。
* 使用Adobe搭售的CDN（內容傳送網路）做為您的Dynamic Media授權的一部分。
* 使用專用（非公司-h.assetsadobe#.com）網域。

   如果您已有專屬網域，則可透過技術支援選擇加入。

   如果您沒有專用網域，Adobe計畫在2018年安排您的HTTP/2轉換。

## 為我的Dynamic Media帳戶啟用HTTP/2的程式為何？{#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

您會提出切換至HTTP/2的要求；它不會自動為您完成。

1. 若要切換至HTTP/2，請起始Adobe客戶服務要求。 請參閱[訪問AEM支援門戶](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)。

   1. 在您的支援要求中提供下列資訊：

      1. 主要聯絡人姓名、電子郵件、電話。
      1. 所有要轉換為HTTP/2的網域。
      1. 確認您對多媒體要求使用安全的HTTPS。
      1. 驗證您是否透過Adobe使用CDN，且未透過直接關係進行管理。
      1. 確認您使用專用網域。 如果您使用Dynamic Media，則會使用專屬網域。
   1. 客戶服務會根據請求的提交順序，將您新增至HTTP/2客戶候補清單。
   1. 當Adobe準備好處理您的請求時，客戶服務會聯絡您以協調轉換並設定目標日期。
   1. 完成後，您會收到通知，並可驗證轉換是否成功轉換至HTTP2。

      由於瀏覽器未說明此情況，因此必須下載擴充功能。

      對於Firefox和Chrome，有一個副檔名稱為「HTTP/2和SPDY指標」。 瀏覽器僅安全支援http/2，因此必須使用https呼叫URL以進行驗證。 如果支援http/2，則會以藍色Flash符號的副檔名和標題&quot;X-Firefox-Spdy&quot;來指出：&quot;h2&quot;。


## 我何時可以轉換為HTTP/2?{#when-can-i-expect-to-be-transitioned-over-to-http}

請求會依客戶服務收到的順序處理。

>[!NOTE]
>
>由於轉換至HTTP/2需要清除快取，因此可能需要較長的前置時間。 因此，一次只能處理幾次客戶轉場。

## 改用HTTP/2有哪些風險？{#what-are-the-risks-with-moving-to-http}

轉換至HTTP/2會清除CDN中的快取，因為它需要移至新的CDN設定。

非快取內容會直接點擊Adobe的原始伺服器，直到重新建立快取為止。 因此，Adobe計劃一次處理幾次客戶轉場，以便在從來源提取請求時仍能維持可接受的效能。

## 如何驗證URL或網站是否已使用HTTP/2啟動？{#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

由於瀏覽器未說明此情況，因此必須下載擴充功能。

對於Firefox和Chrome，有一個副檔名稱為「HTTP/2和SPDY指標」。 瀏覽器僅安全支援http/2，因此必須使用https呼叫URL以進行驗證。 如果支援http/2，則以藍色Flash符號形式的副檔名表示，並且標題`X-Firefox-Spdy` :`h2`。
