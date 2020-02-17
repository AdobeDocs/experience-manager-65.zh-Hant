---
title: DHTML檢視器生命週期結束常見問答集
seo-title: DHTML檢視器生命週期結束常見問答集
description: 自2014年1月31日起，Scene7的DHTML檢視器平台將正式停止使用。 此通知會提供常見問題的解答，讓您可準備此項轉換至我們新的HTML5檢視器平台。
seo-description: 自2014年1月31日起，Scene7的DHTML檢視器平台將正式停止使用。 此通知會提供常見問題的解答，讓您可準備此項轉換至我們新的HTML5檢視器平台。
uuid: a78c03b3-6513-42e1-881f-6a9551659769
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d94244ac-a5f6-4c95-ab8c-26b41d25863f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# DHTML檢視器生命週期結束常見問答集{#dhtml-viewer-end-of-life-faqs}

自2014年1月31日起，Scene7的DHTML檢視器平台將正式停止使用。 此通知會提供常見問題的解答，讓您可準備此項轉換至我們新的HTML5檢視器平台。

**有什麼變化？**

自2014年1月31日起，Scene7將正式終止對DHTML檢視器平台的支援。

**生命結束意味著什麼？**

生命週期結束意味著Scene7將(1)不再在DHTML檢視器平台中新增任何功能增強功能(2)不再解決或發佈DHTML檢視器平台上的任何錯誤修正，且(3)客戶服務將不再疑難排解或支援任何DHTML相關的檢視器問題或問題。

**Scene7為何會做出這項變更？**

Web標準日新月異，而DHTML是較舊的Web開發技術，很快被HTML5所取代。 DHTML作為平台的最大限制是，它無法建立HTML5現在可一貫且更輕鬆地支援跨瀏覽器的豐富體驗。 例如，此類限制包括缺乏跨瀏覽器支援：

* 自訂游標
* 圓角
* 動畫（例如翻頁、縮放等）
* 特效（例如陰影、光暈）
* 完整的字型支援
* 無外掛程式視訊播放

針對Scene7 DHTML檢視器平台，JSP解決方案和Javascript API都未針對行動裝置最佳化，以運用多點觸控和手勢功能。 雖然2011/2012年初發行的DHTML檢視器已針對行動裝置最佳化，但由於缺乏彈性的SDK元件式開發架構，因此很難加以自訂和維護。

由於DHTML的這些限制，加上HTML5在桌上型電腦和行動裝置上都是新興標準，所以Scene7決定投資建立以HTML5為基礎的檢視器平台。 此項投資將為客戶提供強穩的平台，讓他們可以建立更豐富、更吸引人的互動式檢視器，以觸及到多種螢幕（包括桌上型電腦、iOS和Android裝置）的使用者。

**我要如何得知我的檢視器是否使用DHTML平台？**

若要判斷貴公司使用的檢視器是否為DHTML，並因此受此變更影響，請檢查：

1. 您的公司使用本表中列出的現成可用的Scene7檢視器，其中「檢視器技術」指定為「DHTML」:

   [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000)

1. 您的公司使用的檢視器是根據本表格中立即可用的Scene7檢視器，以新預設集建立的檢視器，其中「檢視器技術」指定為「DHTML」:

   [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000)

1. 您的公司使用的是從以JSP為基礎的DHTML解決方案建立的自訂檢視器：

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#JSP_Reference](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#JSP_Reference)

1. 您的公司使用從Javascript API建立的自訂檢視器：

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#API_Reference](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#API_Reference)

1. 您的公司使用以DHTML多螢幕彈出API建立的自訂檢視器：

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Multi-screen_Flyout_Viewer](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Multi-screen_Flyout_Viewer)

1. 您的公司使用的是使用DHTML案頭彈出API建立的自訂檢視器：

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Desktop_Flyout_Viewer](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Desktop_Flyout_Viewer)

1. 您的公司使用屬於DHTML檢視器套件的裝置偵測程式庫：

   在您的程式碼中尋找&quot;sj_deviceDetect.js&quot;的JS包含。

   這已由新的JS裝置偵測程式碼取代，網址為： [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Detecting_devices_and_browsers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Detecting_devices_and_browsers) .

**什麼是取代檢視器平台？**

取代DHTML的是Scene7 HTML5檢視器平台，包括：

* HTML5立即可用的檢視器，可針對多種檢視器類型提供行動最佳化互動功能，包括基本縮放、彈出縮放、影像集、色票集、多維回轉和混合媒體。 如需這些檢視器的完整最新範例，請參閱： [https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html](https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html)
* HTML5檢視器SDK可針對HTML5支援的網站和裝置（例如iOS和Android）廣泛自訂Adobe Scene7檢視器，為品牌化檢視器外觀和互動功能提供最大的彈性和創意。 可重複使用效能最佳化元件的優點可降低檢視器開發的整體成本，並加速自訂開發。

**HTML5檢視器平台何時會具備從DHTML檢視器平台轉換所需的功能？**

Scene7於2011年秋季發行第一個HTML5檢視器SDK，並推出5.5版。自此之後，我們為平台新增了許多功能，並延伸了對更多檢視器類型的支援。 針對大部份的檢視器需求，HTML5檢視器平台可能已具備您現在需要移轉的功能。 我們每季都會推出此檢視器平台，繼續大力投資。

若要判斷現今HTML5檢視器平台是否符合您的檢視器需求，請參閱下列檔案：

[https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#About_HTML5_Viewers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#About_HTML5_Viewers) （適用於立即可用的檢視器功能和自訂功能）

[https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html](https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html) （若要存取SDK API檔案）

如果您仍不確定HTML5檢視器SDK是否符合您的需求，請洽詢我們的專業服務團隊。

**我要如何將檢視器轉換至HTML5平台？**

若要將檢視器轉換至HTML5平台，Scene7提供下列選項：

1. 使用其中一個Scene7現成可用的HTML5檢視器，其範例可在以下網址找到： [https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html](https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html)
1. 在SPS應用程式設定下，設定其中一個Scene7現成可用的HTML5檢視器。 這可讓您自訂特定行為，例如檢視器大小、轉場、縮放行為等： [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html)
1. 修改CSS以自訂Scene7現成可用的HTML5檢視器外觀和感覺，以變更視覺設計，例如按鈕圖稿、位置、透明度、背景顏色等： [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Customizing_HTML5_Viewers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Customizing_HTML5_Viewers)
1. 使用SDK從頭開始建立自訂HTML5檢視器，您可從這裡下載： [https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html](https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html)。 您可以與專業服務合作來建立自訂檢視器，或由您自己的網頁開發團隊來建立。

**不支援HTML5的瀏覽器呢？**

HTML5在許多行動裝置和網頁瀏覽器上都受到支援，並持續獲得推廣。 目前，雖然Internet Explorer 8或更低版本不支援HTML5，但Scene7已創新我們的HTML5檢視器平台，將支援範圍擴及至IE 7和IE 8。 有了Scene7 HTML5檢視器平台，您就可透過單一開發平台觸及絕大多數的案頭和行動使用者。

自HTML5 SDK 2.2.1版起的目前系統需求為：

* Microsoft® Windows® XP或更新版本、Macintosh® OS X 10.6或更新版本
* Firefox 17、Safari 5.1、Chrome 23、Internet Explorer 7或更新版本
* iOS 3.2.2或更新版本
* 在iPhone3或更新版本以及iPad1或更新版本（原生瀏覽器）上取得認證
* Android OS 2.2或更新版本

若要檢查您的瀏覽器是否與我們的HTML5檢視器平台相容，請啟動下列範例檢視器：

[https://s7d1.scene7.com/s7viewers/html5/flyout.html?asset=Scene7SharedAssets/Sample%20Image](https://s7d1.scene7.com/s7viewers/html5/flyout.html?asset=Scene7SharedAssets/Sample%20Image)

如果您透過將滑鼠暫留或將手指拖曳到主影像上，看到放大的影像，則是支援的瀏覽器／裝置。

**如果我想要使用現有的DHTML檢視器，維持生產線上狀態，我有哪些選項？**

雖然您仍可使用DHTML檢視器在製作中上線，但請務必注意，在2014年1月31日之後將不會有增強功能、錯誤修正或客戶服務。 因此，我們強烈建議所有客戶移轉至我們更強穩的HTML5檢視器平台。. 但是，如果您的業務狀況在EOL日期之前無法進行此類移轉，您可以選擇與專業服務合約，以延長支援的維護時間。 如需詳細資訊，請連絡您的客戶經理。

**如需詳細資訊，請與誰聯絡？**

如果本常見問答集未回答您的所有問題，請聯絡支援([s7support@adobe.com](mailto:s7support@adobe.com))或您的Adobe客戶經理。
