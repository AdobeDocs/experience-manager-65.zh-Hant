---
title: HTTP2內容傳送常見問答集
seo-title: HTTP2內容傳送常見問答集
description: 瞭解HTTP2內容傳送。
seo-description: 瞭解HTTP2內容傳送。
uuid: e837c3e0-6e48-46f1-b510-847c9976807a
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: afbe9f80-c2a3-4a46-b9d6-4c9406667d7f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# HTTP2內容傳送常見問答集{#http-delivery-of-content-faq}

Adobe很高興宣佈推出HTTP/2內容傳送。 使用HTTP/2時，您會注意到整體效能有所提升。

## 什麼是HTTP/2? {#what-is-http}

HTTP/2改善了瀏覽器和伺服器通訊的方式，讓資訊傳輸更快速，同時降低了所需的處理能力。

以下網站以簡單簡單的方式說明HTTP/2及其優點：

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## 轉換至HTTP/2以進行內容傳送的主要優點為何？ {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

效能的提升會因您網站的程式碼、您使用Scene7的方式、消費者的裝置、螢幕和位置等因素而有所不同。

Adobe自己的測試產生了下列結果：

* 對於影像，視裝置和瀏覽器而定，回應時間提高了7%至28%。 在iOS裝置上，效能提升最顯著。
* 對於檢視器，載入時間效能提升了15%。

下列展示說明HTTP/1與HTTP/2載入之間的差異：

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## 我是否符合切換至HTTP/2的資格？ {#am-i-eligible-to-switch-over-to-http}

若要使用HTTP/2，您必須符合下列需求：

* 針對您的豐富式媒體要求使用安全的HTTPS。
* 使用Adobe搭售的CDN（內容傳送網路）做為Dynamic Media Classic授權的一部分。
* 使用專用網域(即 `images.company.com` 或 `mycompany.scene7.com`)，而非一般Dynamic Media Classic網域(即、、 `s7d1.scene7.com`或 `s7d2.scene7.com``s7d13.scene7.com`)。

   若要尋找您的網域， [請針對每個公司帳戶登入您的Scene7 Publishing System](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) 例項。

   按一 **[!UICONTROL 下「設定>應用程式設定>一般設定」]**。 尋找標示為「已發佈伺服 **器名稱」的欄位**。 如果您目前使用一般的Scene7網域，則可請求移至您自己的自訂網域，做為轉換的一部分。

## 為我的Dynamic Media Classic帳戶啟用HTTP/2的程式為何？ {#what-is-the-process-for-enabling-http-for-my-scene-account}

您必須提出Adobe技術支援(`s7support@adobe.com`)要求，以切換至HTTP/2;它不會自動為您完成。

1. 在您的支援要求中提供下列資訊：

   * 主要聯絡人姓名、電子郵件和電話號碼。
   * 要轉換到HTTP2的所有網域。 就是， `images.company.com` 或者 `mycompany.scene7.com`。
   若要尋找您的網域， [請針對每個公司帳戶登入您的Scene7 Publishing System](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) 例項。

   按一 **[!UICONTROL 下「設定>應用程式設定>一般設定」]**。 尋找標示為「已發佈伺服 **[!UICONTROL 器名稱」的欄位]**。

   * 確認您對多媒體請求使用安全的HTTPS。
   * 確認您是透過Adobe使用CDN，且未透過直接關係進行管理。
   * 確認您使用的是專用網域。 即，或 `images.company.com` 不 `mycompany.scene7.com`是一般的Scene7網域， `s7d1.scene7.com`例如 `s7d2.scene7.com`、 `s7d13.scene7.com`。
   若要尋找您的網域， [請針對每個公司帳戶登入您的Scene7 Publishing System](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) 例項。

   按一 **[!UICONTROL 下「設定>應用程式設定>一般設定」]**。 尋找標示為「已發佈伺服 **[!UICONTROL 器名稱」的欄位]**。 如果您目前使用一般的Scene7網域，則可請求移至您自己的自訂網域，做為轉換的一部分。

   1. 技術支援會根據提交請求的順序，將您新增至HTTP/2客戶候補清單。
   1. 當Adobe準備好處理您的請求時，支援部門會與您聯絡，協調轉場並設定目標日期。
   1. 完成後，您將會收到通知，並可驗證是否成功轉換至HTTP2。



## 我何時可以轉換為HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

請求的處理順序為技術支援部門接收請求的順序。

>[!NOTE]
>
>由於轉換至HTTP/2需要清除快取，因此可能需要較長的前置時間。 因此，一次只能處理幾次客戶轉場。

## 改用HTTP/2有哪些風險？ {#what-are-the-risks-with-moving-to-http}

轉換至HTTP/2會清除CDN中的快取，因為它需要移至新的CDN設定。

非快取內容會直接點擊Adobe的原始伺服器，直到重新建立快取為止。 因此，Adobe計劃一次處理數個客戶轉場，以便在從我們的來源提取要求時仍能維持可接受的效能。

## 如何驗證URL或網站是否已使用HTTP/2啟動？ {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

您需要下載外部版本，才能與網頁瀏覽器搭配使用。 對於Firefox和Chrome，有一個名為 **[!UICONTROL HTTP/2和SPDY Indicator的擴充功能]**。 瀏覽器僅安全支援HTTP/2，因此必須使用HTTPS呼叫URL以進行驗證。 如果支援HTTP/2，則以藍色Flash符號形式的擴充功能來指出，並加上標題&quot;X-Firefox-Spdy&quot;:&quot;h2&quot;。
