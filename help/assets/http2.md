---
title: HTTP2 傳送內容
description: HTTP/2改進了瀏覽器和伺服器之間的通信方式，允許更快地傳輸資訊，同時降低所需的處理能力。
uuid: d9deb945-bdf5-4d6b-95c8-8bae4442e618
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: c8e145ad-f021-4043-8190-62151775e296
role: User, Admin
exl-id: 9eb9f309-33e5-4694-84d2-fb2cd3de50a6
feature: Publishing,Configuration
source-git-commit: a78de999992d4ab2fc63b5f7e796aa0d5527cb26
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 3%

---

# HTTP/2 內容傳送 {#http-delivery-of-content}

Adobe 很榮幸宣佈推出有助於提升整體效能的 HTTP/2 內容傳送。

>[!NOTE]
>
>此功能要求您使用與Adobe Experience ManagerDynamic Media捆綁的現成CDN。 此功能不支援任何其他自定義CDN。

## 什麼是HTTP/2? {#what-is-http}

HTTP/2改進了瀏覽器和伺服器之間的通信方式，允許更快地傳輸資訊，同時減少所需的處理能力。

以下網站簡單地介紹HTTP/2及其優點：

[您必須瞭解HTTP/2](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html)

## 轉到HTTP/2進行內容傳遞的主要好處是什麼？ {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

效能改進可能有很大差異。 它基於許多因素，如網站代碼、使用Dynamic Media方式、消費者設備、螢幕和位置。

Adobe自己的測試結果如下：

* 對於影像，響應時間根據設備和瀏覽器而提高7%-28%。 最顯著的效能提升是iOS設備。
* 對於觀看者，載入時間效能提高了15%。

下面的演示說明了HTTP/1與HTTP/2載入的區別：

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## 我是否有資格切換到HTTP/2? {#am-i-eligible-to-switch-over-to-http}

要使用HTTP/2，必須滿足以下要求：

* 對富媒體請求使用安全HTTPS。
* 將Adobe捆綁的CDN（內容分發網路）用作Dynamic Media許可證的一部分。
* 使用專用（非公司 — h.assetsadobe#.com）域。

   如果您已經擁有專用域，則可以通過Adobe客戶支援選擇。

   如果您沒有專用域，Adobe計畫在2018年安排向HTTP/2的過渡。

## 為我的Dynamic Media帳戶啟用HTTP/2的過程是什麼？ {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

啟動切換到HTTP/2的請求；它不會自動為你完成。

1. 要切換到HTTP/2，請啟動Adobe客戶支援請求。 請參閱 [開啟支援票證](https://experienceleague.adobe.com/?support-solution=General&amp;lang=en&amp;support-tab=home#support)。

   1. 在支援請求中提供以下資訊：

      1. 主要聯繫人姓名，電子郵件，電話。
      1. 要轉換到HTTP/2的所有域。
      1. 驗證是否對富媒體請求使用安全HTTPS。
      1. 驗證您是否通過Adobe使用CDN，並且未通過直接關係進行管理。
      1. 驗證您是否使用專用域。 如果你使用Dynamic Media，那麼你使用一個專用域。
   1. 「客戶支援」會根據請求提交的順序將您添加到HTTP/2客戶等待清單。
   1. 當Adobe準備好處理您的請求時，客戶支援會聯繫您以協調過渡並設定目標日期。
   1. 完成後將通知您，並可以驗證是否成功轉換到HTTP2。

      由於瀏覽器沒有說明這一事實，因此需要下載擴展。

      對於Firefox和Chrome，有一個名為「HTTP/2和SPDY指示器」的擴展。 瀏覽器僅安全地支援http/2，因此需要調用帶有https的URL來驗證。 如果支援http/2，則擴展以藍色Flash符號和標題「X-Firefox-Spdy」的形式表示：&quot;h2&quot;。


## 我何時可以過渡到HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

請求按客戶支援接收的順序進行處理。

>[!NOTE]
>
>由於向HTTP/2的過渡涉及清除快取，因此可能有較長的提前期。 因此，一次只能處理少數客戶過渡。

## 轉到HTTP/2有何風險？ {#what-are-the-risks-with-moving-to-http}

轉換到HTTP/2會清除CDN上的快取，因為它涉及到移動到新的CDN配置。

非快取內容直接命中Adobe的源伺服器，直到重新生成快取。 因此，Adobe計劃一次處理幾個客戶過渡，以便在從原點拉回請求時保持可接受的效能。

## 如何驗證是否使用HTTP/2激活了URL或網站？ {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

由於瀏覽器沒有說明這一事實，因此需要下載擴展。

對於Firefox和Chrome，有一個名為「HTTP/2和SPDY指示器」的擴展。 瀏覽器僅安全地支援http/2，因此需要調用帶有https的URL來驗證。 如果支援http/2，則擴展以藍色Flash符號和標題的形式表示 `X-Firefox-Spdy` : `h2`。
