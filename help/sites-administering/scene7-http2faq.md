---
title: HTTP2 傳送內容常見問答集
description: 瞭解HTTP2內容傳遞。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 2428914c-5fb0-439e-a1ef-8ee30b890f58
source-git-commit: 65af6e33ae3897519491952f4d3a6832700f77b2
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 2%

---

# HTTP2 傳送內容常見問答集{#http-delivery-of-content-faq}

Adobe很高興宣佈HTTP/2內容交付的可用性。 使用HTTP/2時，會注意到整體效能有所提高。

## 什麼是HTTP/2? {#what-is-http}

HTTP/2改進了瀏覽器和伺服器之間的通信方式，允許更快地傳輸資訊，同時減少所需的處理能力。

以下網站簡單地介紹HTTP/2及其優點：

[您必須瞭解HTTP/2](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html)。

## 轉到HTTP/2進行內容傳遞的主要好處是什麼？ {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

效能改進因網站代碼、使用Dynamic Media、客戶設備、螢幕和位置等因素而異。

Adobe自己的測試結果如下：

* 對於影像，響應時間根據設備和瀏覽器而提高7%-28%。 最顯著的效能提升是iOS設備。
* 對於觀看者，載入時間效能提高了15%。

下面的演示說明了HTTP/1與HTTP/2載入的區別：

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## 我是否有資格切換到HTTP/2? {#am-i-eligible-to-switch-over-to-http}

要使用HTTP/2，必須滿足以下要求：

* 對富媒體請求使用安全HTTPS。
* 將Adobe捆綁的CDN（內容分發網路）用作Dynamic Media許可證的一部分。
* 使用專用域(即 `images.company.com` 或 `mycompany.scene7.com`)，不是Dynamic Media域(即， `s7d1.scene7.com`。 `s7d2.scene7.com`或 `s7d13.scene7.com`)。

   要查找域，請開啟 [Dynamic Media Classic台式機應用](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登錄到您的公司帳戶或帳戶。 然後導航到 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 常規設定]**。 查找標有 **已發佈伺服器名稱**。 如果您當前使用的是通用的Dynamic Media域，則可以請求將此過渡過程的一部分移到您自己的自定義域。

## 為我的Dynamic Media帳戶啟用HTTP/2的過程是什麼？ {#what-is-the-process-for-enabling-http-for-my-scene-account}

1. [使用Admin Console建立支援案例](https://helpx.adobe.com/tw/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) 請求切換到HTTP/2;它不會自動為你完成。
1. 在支援案例中提供以下資訊：

   * 主要聯繫人姓名、電子郵件和電話號碼。
   * 要轉換到HTTP2的所有域。 就是， `images.company.com` 或 `mycompany.scene7.com`。

      要查找域，請開啟 [Dynamic Media Classic台式機應用](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登錄到您的公司帳戶或帳戶。 然後導航到 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 常規設定]**。 查找標有 **[!UICONTROL 已發佈伺服器名稱]**。

   * 驗證是否對富媒體請求使用安全HTTPS。
   * 驗證您是否正通過Adobe使用CDN，而不是使用直接關係進行管理。
   * 驗證您正在使用專用域。 就是， `images.company.com` 或 `mycompany.scene7.com`，不是通用Dynamic Media域，如 `s7d1.scene7.com`。 `s7d2.scene7.com`。 `s7d13.scene7.com`。

      要查找域，請開啟 [Dynamic Media Classic台式機應用](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登錄到您的公司帳戶或帳戶。 然後導航到 **[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 常規設定]**。 查找標有 **[!UICONTROL 已發佈伺服器名稱]**。 如果您當前使用的是通用的Dynamic Media域，則可以請求將此過渡過程的一部分移到您自己的自定義域。

1. Adobe客戶支援根據請求提交的順序將您添加到HTTP/2客戶等待清單。
1. 當Adobe準備好處理您的請求時，「支援」會聯繫您以協調過渡並設定目標日期。
1. 完成後將通知您，並可以驗證是否成功轉換到HTTP2。

## 我何時可以過渡到HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

請求按Adobe客戶支援接收的順序進行處理。

>[!NOTE]
>
>提前期較長，因為向HTTP/2的過渡涉及清除快取。 因此，一次只能處理少數客戶過渡。

## 轉到HTTP/2有何風險？ {#what-are-the-risks-with-moving-to-http}

轉換到HTTP/2會清除CDN上的快取，因為它涉及到移動到新的CDN配置。

非快取內容直接命中Adobe的源伺服器，直到重新生成快取。 由於此操作，Adobe計劃一次處理幾個客戶過渡，以便在從Adobe的來源提取請求時保持可接受的效能。

## 如何驗證是否使用HTTP/2激活了URL或網站？ {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

下載可用於Web瀏覽器的擴展。 對於Firefox和Chrome，有一個副檔名為 **[!UICONTROL HTTP/2和SPDY指示器]**。 瀏覽器僅安全地支援HTTP/2，因此需要調用帶HTTPS的URL來驗證。 如果支援HTTP/2，則以藍色Flash符號和標題「X-Firefox-Spdy」的形式表示：&quot;h2&quot;。
