---
title: 測試行動應用程式
seo-title: Testing Mobile Apps
description: 測試行動應用程式
seo-description: null
uuid: 3b402d34-5cab-4280-b8b9-88ad9f8fc5e4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing
content-type: reference
discoiquuid: 5a98e1bd-f5c1-4f2f-ac02-dbd005dc1de7
exl-id: e10e1904-7016-4eb0-9408-36297285f378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 0%

---

# 測試行動應用程式{#testing-mobile-apps}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

鑑於市場上推出的裝置種類繁多，而且也推出各種裝置，因此測試您的應用程式變得極為重要。 在這個領域中，應用程式商店的功能和可用性可能會獲得低評價，但單一缺陷可能會導致應用程式解除安裝。 測試計畫和品質保證必須謹慎注意。 以下連結涵蓋許多一般需要處理的主題，例如識別您的環境、定義測試案例、測試類型、假設、客戶參與等。 也討論了有助於測試工作的工具。 內部工具，例如 [霍布斯](/help/sites-developing/hobbes.md)，可協助進行網頁型UI測試。 [艱難的一天](/help/sites-developing/tough-day.md) 會以模擬負載來壓縮您的例項。 如果您的測試環境已有使用第三方工具（如Selenium）的經驗，則也可使用這些工具。

在開發行動應用程式時，除了傳統測試外，裝置還有許多新的特別考量。

* 功能 — 應用程式是否符合所有需求？
* 可用性 — 您的客戶是否容易使用並了解該應用程式？
* 效能 — 使用量激增期間會發生什麼事？ 應用程式元素（例如滑鼠和輪播）是否快速，且不會從體驗中去除？
* 失敗或中斷 — 當應用程式執行時，若有來電或通知，會發生什麼事？ 如果發生網路中斷或斷電，會發生什麼情況？
* 安裝和更新 — 安裝體驗如何？ 如何推送更新？
* 技術 — 您的應用程式是否消耗了來自裝置的過多能量？
* 本地化 — 應用程式中的所有區域都翻譯過嗎？
* 認證 — 您的應用程式是否已通過認證？ 客戶能相信嗎？它會遵循所有資料隱私權法律要求？

在您進行自動和手動測試時，應回答這些問題。

## 自動測試 {#automated-testing}

應執行一定程度的自動化測試，以覆蓋各種螢幕大小、記憶體限制、輸入方法和作業系統。 它不僅涵蓋大部分的測試案例，而且在引入新功能或裝置時，可加快回歸測試的速度。 理想情況下，您的自動化工具應該減少或限制工作重複。 使用工具或架構，讓您的測試成果適用於所有平台。 下圖顯示以網頁為基礎之UI測試和行動應用程式測試之測試環境的簡化結構。 圖表左側顯示一系列Selenium節點，包含瀏覽器。 SeleniumGrid可將通用的基於Web的UI測試場到其中的任何節點。 Selenium中樞也可連線至Appium以進行跨平台應用程式測試。 只有顯示的是模擬器，但您可以整合adb、Android適用的，以及iOS裝置的Xcode公用程式。 本檔案稍後會提供連結，您可在其中找到所提及工具的特定詳細資訊。

![chlimage_1](assets/chlimage_1.jpeg)

## 手動測試 {#manual-testing}

除了自動化測試，您的應用程式還應經過一個週期的手動測試。 在實際裝置上執行應用程式的客戶無法由指令碼複製。 你也有很多選擇。 您可以使用HockeApp等平台來定義誰擁有存取權並收集意見。 或者，您可以將整個過程外包給UTest、MoshareStars或Testin等服務。 如果您有一組內部測試者，但設備沒有變化，則有雲服務可讓您對其設備池執行手動測試。 SauceLabs是提供此服務的服務之一。 您也可以遠程建置應用程式至PhoneGap Enterprise，並在本機裝置上安裝，以達到接受測試或降級的等級。 請參閱 [PhoneGap](https://phonegap.com/) 網站以取得其最新功能和檔案。 無論採用何種方法，手動測試都應該；

* 擊中了眾多測試者，
* 針對大型裝置進行測試（理想情況下是真實裝置，若沒有真實裝置則為模擬器/模擬器）,
* 提供資訊反饋：

   * 當機報告，
   * analytics/追蹤，
   * 可用性，
   * 關注領域，
   * 效能，
   * 資料/功耗等

## 工具 {#tools}

測試行動應用程式時，提供多種工具。 要使用的選項將根據您的具體情況而定：功能、價格、支援、覆蓋範圍等。 以下是一些可用工具和服務的簡短說明。

**硒**

* 此架構包含用於測試指令碼的API，用於摘要WebDriver和控制各種瀏覽器。
* 您可將此函式與Appium搭配使用，以在實際裝置上進行測試。
* SeleniumGrid將測試引導到各節點，以便進行並行測試。
* Selenium IDE有助於減少測試用例的編寫。

如需詳細資訊，請參閱 [https://www.seleniumhq.org/](https://www.seleniumhq.org/).

**Testdroid**

* 雲端測試服務，具有持續整合鈎點和真正的裝置測試。
* 包含應用程式編目程式，可檢查裝置相容性、分析記錄、周遊檢視、擷取螢幕擷取畫面，以及監控效能。

如需詳細資訊，請參閱 [https://testdroid.com/](https://testdroid.com/).

**阿皮姆**

* Appium是自動化行動測試的熱門跨平台架構。
* 此外，檢查器還具有記錄功能，可幫助編寫測試案例的代碼。

如需詳細資訊，請參閱 [https://appium.io/](https://appium.io/).

**SauceLabs**

* SauceLabs提供雲端式測試，並與持續整合整合整合。
* 測試會自動在其雲端環境中執行，或者您可以啟動特定裝置或平台並執行手動測試，以協助除錯問題。

如需詳細資訊，請參閱 [https://saucelabs.com/](https://saucelabs.com/).

**AppTestNow**

* 測試行動應用程式的外包服務。
* 包括大量設備，並提供多種類型的測試：效能、品質、功能、認證、本地化、資料耗用等。

如需詳細資訊，請參閱 [https://www.apptestnow.com](https://www.apptestnow.com/).

**HockeApp**

* HockeApp屬於手動測試，將行動應用推送至個人應用程式商店，測試者可在商店下載並試用。

如需詳細資訊，請參閱 [https://hockeyapp.net/features/](https://hockeyapp.net/features/).

**詹金斯**

* Jenkins不是測試工具，但它是一個連續的整合框架，為自動化測試提供骨幹。 有許多第三方外掛程式可延伸功能。 例如，SeleniumGrid插件提供了一個UI，以幫助管理Selenium集線器和節點。

如需詳細資訊，請參閱 [https://jenkins-ci.org/](https://jenkins-ci.org/) 和 [https://wiki.jenkins-ci.org/display/JENKINS/Plugins](https://wiki.jenkins-ci.org/display/JENKINS/Plugins).
