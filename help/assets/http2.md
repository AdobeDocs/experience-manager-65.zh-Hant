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
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '749'
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

效能提升可能大相逕庭。 其基礎許多因素，例如您的網站程式碼、您使用Dynamic Media的方式、消費者的裝置、畫面和位置。

Adobe自己的測試產生以下結果：

* 針對影像，回應時間改善7%至28%，視裝置和瀏覽器而定。 效能提升最明顯的是iOS裝置。
* 對於檢視器而言，載入時間效能提升了15%。

下列示範說明HTTP/1與HTTP/2載入之間的差異：

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## 我是否符合切換至HTTP/2的資格？ {#am-i-eligible-to-switch-over-to-http}

若要使用HTTP/2，您必須符合下列要求：

* 針對您的多媒體請求使用安全HTTPS。
* 使用Adobe套件式CDN （內容傳遞網路），作為Dynamic Media授權的一部分。
* 使用專用（非company-h.assetsadobe#.com）網域。

  如果您已有專屬網域，則可透過Adobe客戶支援選擇加入。

  如果您沒有專用網域，Adobe計畫在2018年安排轉換至HTTP/2。

## 為我的Dynamic Media帳戶啟用HTTP/2的程式為何？ {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

您起始切換至HTTP/2的要求；不會自動為您完成。

1. 若要切換至HTTP/2，請啟動Adobe客戶支援請求。 另請參閱 [開啟支援票證](https://experienceleague.adobe.com/?support-solution=General&amp;lang=en&amp;support-tab=home#support).

   1. 在您的支援要求中提供下列資訊：

      1. 主要連絡人姓名、電子郵件、電話。
      1. 所有要轉換成HTTP/2的網域。
      1. 確認您使用安全HTTPS處理多媒體請求。
      1. 確認您透過Adobe使用CDN，且不是透過直接關係管理。
      1. 確認您使用專屬網域。 如果您使用Dynamic Media，則請使用專用網域。

   1. 客戶支援會根據提交請求的順序，將您新增至HTTP/2客戶輪候表。
   1. 當Adobe準備好處理您的請求時，客戶支援會聯絡您以協調轉換並設定目標日期。
   1. 完成後，您會收到通知，並可以驗證是否成功轉換到HTTP2。

      由於瀏覽器未說明此事實，因此必須下載擴充功能。

      Firefox和Chrome有一個擴充功能，稱為「HTTP/2和SPDY Indicator」。 瀏覽器僅安全地支援http/2，因此有必要呼叫具有https的URL以進行驗證。 如果支援http/2，擴充功能會以藍色Flash符號和標頭「X-Firefox-Spdy」的形式表示：「h2」。

## 我何時可以轉換成HTTP/2？ {#when-can-i-expect-to-be-transitioned-over-to-http}

系統會依客戶支援收到的順序處理請求。

>[!NOTE]
>
>由於轉換至HTTP/2的過程涉及清除快取，因此前置時間可能會很長。 因此，一次只能處理幾個客戶轉換。

## 移至HTTP/2有何風險？ {#what-are-the-risks-with-moving-to-http}

轉換為HTTP/2會清除CDN上的快取，因為它涉及移動到新的CDN設定。

非快取內容會直接點選Adobe的原始伺服器，直到再次重建快取為止。 因此，Adobe計劃一次處理幾個客戶轉換，以便在從來源提取請求時維持可接受的效能。

## 如何確認URL或網站是否以HTTP/2啟動？ {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

由於瀏覽器未說明此事實，因此必須下載擴充功能。

Firefox和Chrome有一個擴充功能，稱為「HTTP/2和SPDY Indicator」。 瀏覽器僅安全地支援http/2，因此有必要呼叫具有https的URL以進行驗證。 如果支援http/2，則會以藍色Flash符號和標頭的形式由擴充功能表示 `X-Firefox-Spdy` ： `h2`.
