---
title: HTTP2 傳送內容常見問答集
description: 了解HTTP2內容傳送。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 2428914c-5fb0-439e-a1ef-8ee30b890f58
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 1%

---

# HTTP2 傳送內容常見問答集{#http-delivery-of-content-faq}

Adobe很高興能宣佈推出HTTP/2內容傳送。 使用HTTP/2時，您會發現整體效能有所提升。

## 什麼是HTTP/2?{#what-is-http}

HTTP/2改進了瀏覽器和伺服器的通信方式，允許更快地傳輸資訊，同時降低所需的處理能力。

以下網站以簡單簡短的方式說明HTTP/2及其優點：

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## 轉移至HTTP/2以進行內容傳送的主要優點為何？{#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

效能改善會因網站程式碼、您使用Dynamic Media的方式、消費者裝置、畫面和位置等因素而有所不同。

Adobe自己的測試得出以下結果：

* 針對影像，視裝置和瀏覽器而定，回應時間已改善7%至28%。 iOS裝置上效能提升最顯著。
* 對於檢視器，載入時間效能提升了15%。

下列示範說明HTTP/1與HTTP/2載入的差異：

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## 我是否有資格切換至HTTP/2?{#am-i-eligible-to-switch-over-to-http}

若要使用HTTP/2，您必須符合下列需求：

* 為您的多媒體請求使用安全HTTPS。
* 將Adobe隨附的CDN（內容傳遞網路）作為Dynamic Media授權的一部分。
* 使用專用網域（即`images.company.com`或`mycompany.scene7.com`），而非通用Dynamic Media網域（即`s7d1.scene7.com`、`s7d2.scene7.com`或`s7d13.scene7.com`）。

   若要尋找您的網域，請開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的公司帳戶或帳戶。 然後點選「 **[!UICONTROL 設定>應用程式設定>一般設定]**」。 查找標籤為&#x200B;**已發佈伺服器名稱**&#x200B;的欄位。 如果您目前使用一般Dynamic Media網域，可以請求移轉至您自己的自訂網域，作為此轉變的一部分。

## 為我的Dynamic Media帳戶啟用HTTP/2的程式為何？{#what-is-the-process-for-enabling-http-for-my-scene-account}

1. 您必須[使用Admin Console建立支援案例](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)並請求切換至HTTP/2;不會自動為您完成。
1. 在您的支援案例中提供下列資訊：

   * 主要聯繫人姓名、電子郵件和電話號碼。
   * 要轉換為HTTP2的所有網域。 即`images.company.com`或`mycompany.scene7.com`。

      若要尋找您的網域，請開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的公司帳戶或帳戶。 然後點選「 **[!UICONTROL 設定>應用程式設定>一般設定]**」。 查找標籤為&#x200B;**[!UICONTROL 已發佈伺服器名稱的欄位。]**

   * 確認您對多媒體請求使用安全HTTPS。
   * 確認您是透過Adobe使用CDN，而非以直接關係進行管理。
   * 確認您使用的是專用網域。 即`images.company.com`或`mycompany.scene7.com`，而非一般的Dynamic Media網域，例如`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com`。

      若要尋找您的網域，請開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然後登入您的公司帳戶或帳戶。 然後點選「 **[!UICONTROL 設定>應用程式設定>一般設定]**」。 查找標籤為&#x200B;**[!UICONTROL Published Server Name的欄位。]** 如果您目前使用一般Dynamic Media網域，可以請求移轉至您自己的自訂網域，作為此轉變的一部分。

1. 技術支援會根據提交請求的順序，將您新增至HTTP/2客戶等待清單。
1. 當Adobe準備好處理您的請求時，「支援」會聯絡您以協調轉變並設定目標日期。
1. 完成後會收到通知，並可驗證是否成功轉換至HTTP2。

## 何時可望轉換為HTTP/2?{#when-can-i-expect-to-be-transitioned-over-to-http}

系統會依照技術支援接收請求的順序來處理請求。

>[!NOTE]
>
>可能會有很長的前置時間，因為轉換至HTTP/2涉及清除快取。 因此，一次只能處理少數客戶轉變。

## 轉到HTTP/2有什麼風險？{#what-are-the-risks-with-moving-to-http}

轉換至HTTP/2會清除CDN中的快取，因為它涉及移至新的CDN設定。

非快取內容會直接點擊Adobe的原始伺服器，直到重新建置快取為止。 因此，Adobe計劃一次處理一些客戶轉變，以在從來源提取請求時維持可接受的效能。

## 如何驗證URL或網站是否已透過HTTP/2啟動？{#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

您需要下載外部版本才能與網頁瀏覽器搭配使用。 對於Firefox和Chrome，有一個名為&#x200B;**[!UICONTROL HTTP/2和SPDY Indicator的擴充功能。]** 瀏覽器僅安全支援HTTP/2，因此必須使用HTTPS呼叫URL以進行驗證。如果支援HTTP/2，則會以藍色Flash符號和標題「X-Firefox-Spdy」的形式以擴充功能表示：&quot;h2&quot;。
