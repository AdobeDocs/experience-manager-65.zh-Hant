---
title: 測試行動應用程式
description: 瞭解如何使用各種工具自動化或手動測試您的行動應用程式。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing
content-type: reference
exl-id: e10e1904-7016-4eb0-9408-36297285f378
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 0%

---

# 測試行動應用程式{#testing-mobile-apps}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案，使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md)。

鑑於市場上有多種裝置和裝置正在發行，測試您的應用程式已勢在必行。 這是功能和可用性在應用程式商店中可能會獲得較少評論的區域，但單一缺陷可能會導致您的應用程式解除安裝。 測試計畫與品質保證必須謹慎處理。 以下連結涵蓋許多必須一般解決的主題，例如識別您的環境、定義測試案例、測試型別、假設和客戶參與。 此外，還討論有助於測試工作的工具。 內部工具，例如 [Hobbes](/help/sites-developing/hobbes.md)，可協助您進行網頁式UI測試。 [艱苦的一天](/help/sites-developing/tough-day.md) 可以用模擬的負載來強調例證。 如果您的測試環境已有使用Selenium等協力廠商工具的經驗，也可以使用這些工具。

在開發行動應用程式時，有許多裝置專屬的新問題，必須與傳統測試一起解決。

* 功能 — 您的應用程式是否符合所有要求？
* 可用性 — 您的客戶是否可輕鬆使用並瞭解應用程式？
* 效能 — 使用量尖峰期間會發生什麼事？ 應用程式元素（例如撥動和輪播）是否很快，而且不會影響體驗？
* 失敗或中斷 — 當您的應用程式執行中有來電或通知時，會發生什麼情況？ 如果網路中斷或電源關閉，會發生什麼情況？
* 安裝和更新 — 安裝體驗如何？ 如何推出更新？
* 技術 — 您的應用程式是否消耗裝置過多的電力？
* 本地化 — 應用程式中的所有區域都經過翻譯嗎？
* 認證 — 您的應用程式是否已通過認證？ 客戶是否信任其會遵循所有資料隱私權法律規定？

這些問題應在您的自動化和手動測試期間獲得解答。

## 自動化測試 {#automated-testing}

應該執行一定程度的自動化測試，以涵蓋各種熒幕大小、記憶體限制、輸入方法和作業系統。 它不僅涵蓋許多測試案例，還可在引入新功能或裝置時加快回歸測試。 理想情況下，您的自動化工具應該減少或限制重複工作。 請使用工具或架構，讓您的測試工作適用於所有平台。 下圖顯示用於網頁式UI測試和行動應用程式測試的測試環境的簡化結構。 圖表左側顯示一系列具有瀏覽器的Selenium節點。 SeleniumGrid可以將常見的Web式UI測試部署至這些節點。 Selenium中心也可以連線至Appium，以進行跨平台應用程式測試。 只顯示模擬器，但您可以納入adb (適用於Android™)和Xcode (適用於iOS裝置)公用程式。 本檔案稍後會提供連結，讓您找到所提及工具的特定詳細資訊。

![chlimage_1](assets/chlimage_1.jpeg)

## 手動測試 {#manual-testing}

除了自動化測試以外，您的應用程式還應進行一連串的手動測試。 指令碼無法複製在真實裝置上執行應用程式的客戶。 在這裡，您也有許多選項。 您可以使用HockeyApp等平台來定義誰有權存取及收集意見回饋。 或者，您可以將整個程式外包給UTest、ElusiveStars或Testn等服務。 如果您有一組內部測試者，但缺少裝置的差異，則可使用雲端服務在其裝置集區上執行手動測試。 其中一項服務是SauceLabs。 您也可以從遠端建立應用程式至PhoneGap Enterprise，並安裝在本機裝置上，作為驗收測試或降級等級。 請參閱PhoneGap (`https://phonegap.com/`)網站以取得其最新功能和檔案。 無論採用何種方法，手動測試都應執行以下操作：

* 撞上了一大群測試者，
* 針對大型裝置集區進行測試（最好是真正的裝置，但如果沒有真正的裝置則為模擬器/模擬器），
* 提供資訊性意見反應：

   * 當機報告，
   * 分析/追蹤，
   * 可用性，
   * 需要注意的領域，
   * 效能，
   * 資料/耗電量等等。

## 工具 {#tools}

測試行動應用程式時可使用多種工具。 應根據您的特定情況來選擇要使用的解決方案：功能、價格、支援、涵蓋範圍等。 以下只是一些可用工具與服務的小說明。

**Selenium**

* 此架構包含用於測試指令碼的API，以提供WebDriver並控制各種瀏覽器。
* 您可以將此用於Appium，在實際裝置上進行測試。
* SeleniumGrid會跨節點指引測試，以進行平行測試。
* Selenium IDE有助於減少測試案例的寫入。

如需詳細資訊，請參閱 [https://www.selenium.dev/](https://www.selenium.dev/).

**Testdroid**

* 雲端型測試服務，包含持續的整合掛接和真實的裝置測試。
* 其中包括應用程式編目程式，可檢查裝置相容性、分析記錄、周遊檢視、擷取熒幕擷取畫面及監視效能。

如需詳細資訊，請參閱 [https://testdroid.com/](https://testdroid.com/).

**Appium**

* Appium是用於自動化行動測試的熱門跨平台架構。
* 此外，還隨附了檢查器，以幫助編寫測試案例的程式碼。

如需詳細資訊，請參閱 [https://appium.io/](https://appium.io/).

**醬汁實驗室**

* SauceLabs提供雲端型測試，並與持續整合整合。
* 測試會在他們的雲端環境中自動執行，或者您可以啟動特定裝置或平台，並執行手動測試以幫助偵錯問題。

如需詳細資訊，請參閱 [https://saucelabs.com/](https://saucelabs.com/).

<!-- **AppTestNow**

* An outsourcing service that tests your mobile apps.
* Included is a large pool of devices and offers a wide range of types of testing: performance, quality, functional, certification, localization, data consumption, and so on.

For more information, see [https://apptestnow.com/](https://apptestnow.com/). -->

**HockeyApp**

* HockeyApp屬於手動測試類別，行動應用程式會推送至個人應用程式商店，以供測試人員下載及試用。

如需詳細資訊，請參閱 [https://hockeyapp.net/features/](https://hockeyapp.net/features/).

**Jenkins**

* 雖然Jenkins不是測試工具，它是一種持續整合架構，提供自動化測試的骨幹。 可使用許多協力廠商外掛程式來擴充功能。 例如，SeleniumGrid外掛程式提供UI來協助管理Selenium中心和節點。

如需詳細資訊，請參閱 [https://www.jenkins.io/](https://www.jenkins.io/) 和 [https://plugins.jenkins.io/](https://plugins.jenkins.io/).
