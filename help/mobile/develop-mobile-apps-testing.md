---
title: 測試移動應用
seo-title: Testing Mobile Apps
description: 測試移動應用
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

# 測試移動應用{#testing-mobile-apps}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

鑑於市場上推出的設備種類繁多，而且正在發佈的設備種類繁多，測試您的應用變得極其重要。 在這個領域，功能和可用性可能會在應用商店上獲得低評價，但單個缺陷可能會導致卸載應用。 在測試計畫和質量保證中必須小心。 以下連結涵蓋許多一般需要解決的主題，例如，確定您的環境、定義test案例、測試類型、假設、客戶參與等。 還討論了有助於測試工作的工具。 內部工具，如 [霍布斯](/help/sites-developing/hobbes.md)，可幫助進行基於Web的UI測試。 [艱難的一天](/help/sites-developing/tough-day.md) 可以在模擬載荷下對實例施加壓力。 如果您的測試環境已經有使用第三方工具（如Selenium）的經驗，也可以使用這些工具。

在開發移動應用時，除了傳統測試外，還有許多新的關注點需要解決。

* 功能 — 您的應用是否滿足所有要求？
* 可用性 — 您的客戶是否易於使用和理解該應用？
* 效能 — 在使用率激增期間發生什麼？ 應用程式元素，比如水手和菜單，是否快速而且不會影響體驗？
* 失敗或中斷 — 當應用運行時有來電或通知時會發生什麼情況？ 如果網路中斷或斷電，會發生什麼情況？
* 安裝和更新 — 安裝體驗如何？ 如何推出更新？
* 技術 — 您的應用是否從設備消耗了太多電力？
* 本地化 — 是否翻譯了應用中的所有區域？
* 認證 — 您的應用是否已認證？ 客戶能否相信它遵守了所有資料隱私法律要求？

這些問題應在您的自動和手動測試期間回答。

## 自動測試 {#automated-testing}

應執行一定程度的自動測試，以涵蓋螢幕大小、記憶體約束、輸入方法和作業系統。 它不僅覆蓋了大部分test案例，而且在引入新特性或新設備時，還可加快回歸測試的速度。 理想情況下，您的自動化工具應減少或限制重複工作。 使用工具或框架，以便您的測試工作適用於所有平台。 下圖顯示了基於Web的UI測試和移動應用測試的測試環境的簡化結構。 圖表的左側顯示了一系列帶有瀏覽器的Selenium節點。 SeleniumGrid可以將通用、基於Web的UItest農場到這些節點中的任何節點。 Selenium集線器還可以連接到Appium，以便跨平台應用測試。 只顯示模擬器，但您可以為Android和Xcode實用程式合併ADB，用於iOS設備。 本文檔稍後提供了連結，您可以在其中找到所述工具的特定詳細資訊。

![chlimage_1](assets/chlimage_1.jpeg)

## 手動測試 {#manual-testing}

除了自動測試外，您的應用程式還應經過一個週期的手動測試。 在實際設備上運行應用的客戶不能被指令碼複製。 你也有很多選擇。 您可以使用HockeApp等平台來定義誰有權訪問和收集反饋。 或者，您可以將整個過程外包給UTest 、 FolasureStars或Testin等服務。 如果您有一組內部測試人員，但缺少設備的變化，則有雲服務可在其設備池上執行手動測試。 提供這種服務的是SauceLabs。 您還可以遠程構建應用到PhoneGap Enterprise，並在本地設備上安裝，作為驗收測試或降級的級別。 查看 [電話間隙](https://phonegap.com/) 的子菜單。 無論採用何種方法，手動測試都應該；

* 擊中大量測試人員，
* test大型設備池（理想情況下是真實設備，但如果真實設備不可用則是模擬器/模擬器）,
* 提供資訊反饋：

   * 崩潰報告，
   * 分析/跟蹤，
   * 可用性，
   * 關注領域，
   * 效能，
   * 資料/功耗等。

## 工具 {#tools}

有多種工具可用於測試移動應用。 根據您的具體情況選擇使用：功能、價格、支援、覆蓋範圍等。 以下只是一些可用的工具和服務的簡短說明。

**硒**

* 框架，包括用於test指令碼以饋送WebDriver和控制各種瀏覽器的API。
* 您可以將此功能與Appium結合使用，以在實際設備上進行測試。
* SeleniumGrid將test定向到節點之間，以進行並行測試。
* Selenium IDE有助於減少test寫入。

有關詳細資訊，請參閱 [https://www.seleniumhq.org/](https://www.seleniumhq.org/)。

**測試程式**

* 一種基於雲的測試服務，具有連續整合掛接和真實設備測試。
* 包括App Crawler，用於檢查設備相容性、分析日誌、遍歷視圖、獲取螢幕截圖和監視效能。

有關詳細資訊，請參閱 [https://testdroid.com/](https://testdroid.com/)。

**阿皮姆**

* Appium是用於自動化移動test的流行跨平台框架。
* 此外，還包括具有記錄能力的檢查器，以幫助對test案例進行編碼。

有關詳細資訊，請參閱 [https://appium.io/](https://appium.io/)。

**沙司實驗室**

* SauceLabs提供基於雲的測試，並與持續整合整合整合。
* Test可以在其雲環境中自動運行，或者您可以啟動特定設備或平台並執行手動測試以幫助調試問題。

有關詳細資訊，請參閱 [https://saucelabs.com/](https://saucelabs.com/)。

**AppTestNow**

* 將test移動應用的外包服務。
* 包括大量設備，並提供多種類型的測試：效能、質量、功能、認證、本地化、資料消耗等。

有關詳細資訊，請參閱 [https://www.apptestnow.com](https://www.apptestnow.com/)。

**曲棍球應用**

* HockeApp處於手動測試階段，移動應用被推送到個人應用商店，測試人員可以在商店下載並試用。

有關詳細資訊，請參閱 [https://hockeyapp.net/features/](https://hockeyapp.net/features/)。

**詹金斯**

* 儘管Jenkins不是測試工具，但它是一個連續的整合框架，為自動化test提供支柱。 許多第三方插件可用於擴展功能。 一個示例是，SeleniumGrid插件提供了一個UI來幫助管理Selenium集線器和節點。

有關詳細資訊，請參閱 [https://jenkins-ci.org/](https://jenkins-ci.org/) 和 [https://wiki.jenkins-ci.org/display/JENKINS/Plugins](https://wiki.jenkins-ci.org/display/JENKINS/Plugins)。
