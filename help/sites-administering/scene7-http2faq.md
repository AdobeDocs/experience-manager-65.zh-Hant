---
title: HTTP2 傳送內容常見問題集
description: 瞭解HTTP2內容傳遞，以及如何提高網頁內容的整體效能。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 2428914c-5fb0-439e-a1ef-8ee30b890f58
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 1%

---

# HTTP2 傳送內容常見問題集{#http-delivery-of-content-faq}

Adobe很高興宣佈推出HTTP/2內容傳送。 使用HTTP/2時，會注意到整體效能提升。

## 什麼是HTTP/2？ {#what-is-http}

HTTP/2可改善瀏覽器和伺服器的通訊方式，實現更快的資訊傳輸，同時降低所需的處理能力。

以下網站以簡單扼要的方式說明HTTP/2及其優點：

[關於HTTP/2](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html)的須知事項。

## 改用HTTP/2進行內容傳送的主要優點為何？ {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

效能改善會因您網站的程式碼、您使用Dynamic Media的方式、客戶的裝置、畫面和位置等因素而有很大的差異。

Adobe自己的測試產生以下結果：

* 針對影像，回應時間改善7%至28%，視裝置和瀏覽器而定。 效能提升最明顯的是iOS裝置。
* 對於檢視器而言，載入時間效能提升了15%。

下列示範說明HTTP/1與HTTP/2載入之間的差異：

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## 我是否符合切換至HTTP/2的資格？ {#am-i-eligible-to-switch-over-to-http}

若要使用HTTP/2，您必須符合下列要求：

* 針對您的多媒體請求使用安全HTTPS。
* 使用Adobe套件式CDN （內容傳遞網路），作為Dynamic Media授權的一部分。
* 使用專用網域（即`images.company.com`或`mycompany.scene7.com`），而非一般Dynamic Media網域（即`s7d1.scene7.com`、`s7d2.scene7.com`或`s7d13.scene7.com`）。

  若要尋找您的網域，請開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=zh-Hant#getting-started)，然後登入您的公司帳戶或帳戶。 然後瀏覽至&#x200B;**[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 一般設定]**。 尋找標示為&#x200B;**已發佈的伺服器名稱**&#x200B;的欄位。 如果您目前使用一般Dynamic Media網域，您可以在此轉換中要求移至您自己的自訂網域。

## 為我的Dynamic Media帳戶啟用HTTP/2的程式為何？ {#what-is-the-process-for-enabling-http-for-my-scene-account}

1. [使用Admin Console建立支援案例](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html)並要求切換至HTTP/2；系統不會自動為您完成此操作。
1. 在您的支援案例中提供下列資訊：

   * 主要連絡人姓名、電子郵件和電話號碼。
   * 所有要轉換成HTTP2的網域。 即`images.company.com`或`mycompany.scene7.com`。

     若要尋找您的網域，請開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=zh-Hant#getting-started)，然後登入您的公司帳戶或帳戶。 然後瀏覽至&#x200B;**[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 一般設定]**。 尋找標示為&#x200B;**[!UICONTROL 已發佈的伺服器名稱]**&#x200B;的欄位。

   * 確認您使用安全HTTPS處理多媒體請求。
   * 確認您是透過Adobe使用CDN，且不受直接關係管理。
   * 確認您使用專用網域。 即`images.company.com`或`mycompany.scene7.com`，不是一般Dynamic Media網域，例如`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com`。

     若要尋找您的網域，請開啟[Dynamic Media Classic案頭應用程式](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=zh-Hant#getting-started)，然後登入您的公司帳戶或帳戶。 然後瀏覽至&#x200B;**[!UICONTROL 設定]** > **[!UICONTROL 應用程式設定]** > **[!UICONTROL 一般設定]**。 尋找標示為&#x200B;**[!UICONTROL 已發佈的伺服器名稱]**&#x200B;的欄位。 如果您目前使用一般Dynamic Media網域，您可以在此轉換中要求移至您自己的自訂網域。

1. Adobe客戶支援會根據提交請求的順序，將您新增至HTTP/2客戶輪候表。
1. 當Adobe準備好處理您的請求時，「支援」會聯絡您以協調轉變並設定目標日期。
1. 完成後，您將會收到通知，並可以驗證成功轉換到HTTP2。

## 我何時可以轉換到HTTP/2？ {#when-can-i-expect-to-be-transitioned-over-to-http}

系統會依照Adobe客戶支援收到請求的順序來處理請求。

>[!NOTE]
>
>由於轉換至HTTP/2的過程涉及清除快取，因此前置時間較長。 因此，一次只能處理幾個客戶轉換。

## 移至HTTP/2有何風險？ {#what-are-the-risks-with-moving-to-http}

轉換為HTTP/2會清除CDN上的快取，因為它涉及移動到新的CDN設定。

非快取內容會直接點選Adobe的原始伺服器，直到再次重建快取為止。 因為此動作，Adobe計劃一次處理幾個客戶轉換，以便在從Adobe來源提取請求時維持可接受的效能。

## 如何確認URL或網站是否以HTTP/2啟動？ {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

下載可與網頁瀏覽器搭配使用的擴充功能。 Firefox和Chrome有一個名為&#x200B;**[!UICONTROL HTTP/2和SPDY Indicator]**&#x200B;的擴充功能。 瀏覽器僅安全地支援HTTP/2，因此有必要呼叫具有HTTPS的URL以進行驗證。 如果支援HTTP/2，則會以藍色Flash符號和標頭「X-Firefox-Spdy」的格式在擴充功能中標示：「h2」。
