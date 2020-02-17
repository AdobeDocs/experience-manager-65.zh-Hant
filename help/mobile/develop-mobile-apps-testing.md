---
title: 測試行動應用程式
seo-title: 測試行動應用程式
description: 'null'
seo-description: 'null'
uuid: 3b402d34-5cab-4280-b8b9-88ad9f8fc5e4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing
content-type: reference
discoiquuid: 5a98e1bd-f5c1-4f2f-ac02-dbd005dc1de7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 測試行動應用程式{#testing-mobile-apps}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

鑑於市面上的各種裝置和即將推出的裝置，測試您的應用程式變得極為重要。 在這個領域，功能和可用性可能會在應用程式商店中獲得低評價，但是單一缺陷可能會導致您的應用程式解除安裝。 測試計畫和品質保證必須謹慎注意。 以下連結涵蓋許多一般需要解決的主題，如：確定環境、定義測試案例、測試類型、假設、客戶參與等。 此外，也討論了有助於測試的工具。 內部工具(例如 [Hobbes](/help/sites-developing/hobbes.md))可協助進行網路UI測試。 [Tough Day](/help/sites-developing/tough-day.md) can stress your instances with a simulated load. 如果您的測試環境已具備使用第三方工具（例如Selenium）的經驗，也可使用這些工具。

在開發行動應用程式時，除了傳統測試之外，還有許多裝置特有的新顧慮。

* 功能——您的應用程式是否符合所有需求？
* 可用性——您的客戶是否能輕鬆使用和瞭解應用程式？
* 效能——使用量尖峰期間會發生什麼？ 應用程式元素（例如滑動和輪盤）是否快速且不會從體驗中消失？
* 失敗或中斷——當應用程式執行時，有來電或通知時會發生什麼？ 如果網路中斷或斷電，會發生什麼情況？
* 安裝與更新——安裝體驗如何？ 更新如何推出？
* 技術——您的應用程式是否耗用太多裝置的功能？
* 本地化——您應用程式中的所有區域都已翻譯嗎？
* 認證——您的應用程式已通過認證嗎？ 客戶是否相信它符合所有資料隱私法規要求？

這些問題應在您進行自動化和手動測試時得到解答。

## 自動化測試 {#automated-testing}

應執行一定程度的自動化測試，以涵蓋各種螢幕大小、記憶體限制、輸入方法和作業系統。 它不僅涵蓋了大部分的測試案例，而且在引入新功能或新裝置時，可加快回歸測試的速度。 在理想情況下，您的自動化工具應該減少或限制重複工作。 使用工具或架構，讓您的測試工作適用於所有平台。 下表顯示測試環境的簡化結構，以用於網路型UI測試和行動應用程式測試。 圖表的左側顯示了一系列帶有瀏覽器的Selenium節點。 SeleniumGrid可將常見、基於Web的UI測試分發到這些節點中的任何節點。 Selenium中樞也可連接至Appium，以進行跨平台應用程式測試。 只顯示模擬器，但您可以為iOS裝置整合adb、Android和Xcode公用程式。 本檔案稍後會提供連結，您可在其中找到上述工具的特定詳細資訊。

![chlimage_1](assets/chlimage_1.jpeg)

## 手動測試 {#manual-testing}

除了自動測試，您的應用程式還應該進行手動測試。 在實際裝置上執行應用程式的客戶無法複製指令碼。 在這裡，你也有很多選擇。 您可以使用HockeyApp等平台來定義誰擁有存取權並收集意見回應。 或者，您可以將整個程式外包給UTest、ManakileStars或Testin等服務。 如果您有一組內部測試者，但裝置沒有變化，則有雲端服務可讓您在其裝置池中執行手動測試。 SauceLabs就是提供此類服務的一員。 您也可以將應用程式遠端建置至PhoneGap Enterprise，並安裝在本機裝置上，做為驗收測試或降級的等級。 請參 [閱PhoneGap網站](https://phonegap.com/) ，以取得其最新功能和檔案。 無論採取何種方法，手動測試都應該；

* 擊中了測試者的大目標，
* 針對大量裝置（最好是實際的裝置，但若實際的裝置不可用，則需要模擬器／模擬器）進行測試，
* 提供資訊性意見回應：

   * 當機報告，
   * 分析／追蹤，
   * 可用性，
   * 關注領域，
   * 效能，
   * 資料／功耗等。

## 工具 {#tools}

測試行動應用程式時，可使用多種工具。 使用的選項將根據您的具體情況而定：功能、價格、支援、涵蓋範圍等。 以下只是部份可用的工具和服務的簡短說明。

**硒**

* 此架構包含測試指令碼的API，以餵送WebDriver並控制各種瀏覽器。
* 您可將它與Appium搭配使用，以在實際裝置上進行測試。
* SeleniumGrid會將測試導向至各節點，以進行並行測試。
* Selenium IDE有助於減少測試用例的編寫。

如需詳細資訊，請參 [閱https://www.seleniumhq.org/](https://www.seleniumhq.org/)。

**Testdroid**

* 雲端測試服務，提供持續整合勾點和實際裝置測試。
* 包含App Crawler，可檢查裝置相容性、分析記錄、遍歷檢視、擷取螢幕擷取及監控效能。

如需詳細資訊，請參 [閱https://testdroid.com/](https://testdroid.com/)。

**Appium**

* Appium是一個常用的跨平台架構，可自動化行動測試。
* 此外，檢查器還包含記錄功能，以協助編寫測試案例。

如需詳細資訊，請參 [閱https://appium.io/](https://appium.io/)。

**SauceLabs**

* SauceLabs提供雲端測試，並與持續整合整合。
* 測試會自動在其雲端環境中執行，或者您可以啟動特定裝置或平台並執行手動測試，以協助除錯問題。

如需詳細資訊，請參 [閱https://saucelabs.com/](https://saucelabs.com/)。

**AppTestNow**

* 測試行動應用程式的外包服務。
* 包含大量裝置，並提供多種測試類型：效能、質量、功能、認證、本地化、資料消耗等。

如需詳細資訊，請參 [閱https://www.apptestnow.com](https://www.apptestnow.com/)。

**HockeyApp**

* HockeyApp受到手動測試，將行動應用程式推送至個人應用程式商店，讓測試者可以下載並試用。

如需詳細資訊，請參 [閱https://hockeyapp.net/features/](https://hockeyapp.net/features/)。

**詹金斯**

* 雖然Jenkins不是測試工具，但它是一個連續的整合框架，為自動化測試提供了骨幹。 許多協力廠商外掛程式都可用來擴充功能。 例如，SeleniumGrid外掛程式提供UI，以協助管理Selenium集線器和節點。

如需詳細資訊，請參 [閱https://jenkins-ci.org/](https://jenkins-ci.org/) 和 [https://wiki.jenkins-ci.org/display/JENKINS/Plugins](https://wiki.jenkins-ci.org/display/JENKINS/Plugins)。
