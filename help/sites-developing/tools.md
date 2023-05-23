---
title: 測試和跟蹤工具
seo-title: Testing and Tracking Tools
description: 提AEM供了元件UI測試框架和元件測試和調試機制
seo-description: AEM provides a framework for testing component UI and a mechanism for testing and debugging components
uuid: 12abedb5-4ee7-4389-9340-e628adbbc053
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 3cf0fd8d-7fc8-468a-bb1e-1debb68a82a5
docset: aem65
exl-id: bb5d1c7c-56ce-4d1e-a3cb-4e74d6922137
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# 測試和跟蹤工具{#testing-and-tracking-tools}

## 測試 {#testing}

AEM提供：

* [元件UI測試框架](/help/sites-developing/hobbes.md)。
* [用於測試和調試元件的機制](/help/sites-developing/developer-mode.md)。

以下是兩個開源測試工具：

**硒**

Selenium用於在瀏覽器中進行功能測試，每個活動有一個用戶。 它將測試步驟（按一下）記錄為HTML表或Java類。

有關詳細資訊，請參閱 [https://www.seleniumhq.org/](https://www.seleniumhq.org/)。

**JMeter**

JMeter用於跟蹤請求，可用於功能、效能和壓力test。

有關詳細資訊，請參閱 [https://jakarta.apache.org/jmeter/](https://jakarta.apache.org/jmeter)。

還有許多專有工具用於自動test和管理test計畫。

### 跟蹤 {#tracking}

以下工具可輕鬆使用。 但是，在所有情況下，一個關鍵問題是項目團隊的所有成員 — 合作夥伴和客戶 — 都能獲得資料。

**布吉利亞**

可根據您自己的要求配置的錯誤跟蹤系統。

**試算表**

雖然不是專門的錯誤跟蹤工具，但電子錶格通常 *管理*&#x200B;用於此目的，因為他們易於理解，而且大多數用戶都有其功能的經驗。

如果這些用於跟蹤，則：

* 應該保持簡單。
* 個別電子錶格的數量應保持在最少。
* 必須定期更新。
* 只應維護一個主副本，每個人都應知道主副本的位置。
* 所有項目成員都可以訪問。
* 如果安全性是問題（通常發生在大型公司），並且不可能進行通用訪問，則只要每個人都知道這些是副本，並且無法更新，就可能分發副本。

同樣，有許多專用工具用於跟蹤錯誤和功能要求。
