---
title: 測試和追蹤工具
seo-title: Testing and Tracking Tools
description: AEM提供測試元件UI的架構，以及測試和偵錯元件的機制
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

# 測試和追蹤工具{#testing-and-tracking-tools}

## 測試 {#testing}

AEM提供：

* [測試元件UI的架構](/help/sites-developing/hobbes.md).
* [用於測試和調試元件的機制](/help/sites-developing/developer-mode.md).

以下是兩種開放原始碼測試工具：

**硒**

Selenium用於在每個活動有一個使用者的瀏覽器中進行函式測試。 它將測試步驟（點按）記錄為HTML表或Java類。

如需詳細資訊，請參閱 [https://www.seleniumhq.org/](https://www.seleniumhq.org/).

**JMeter**

JMeter用於追蹤請求，可用於功能、效能和壓力測試。

如需詳細資訊，請參閱 [https://jakarta.apache.org/jmeter/](https://jakarta.apache.org/jmeter).

還有許多專用工具用於自動化測試和管理測試計畫。

### 追蹤 {#tracking}

您可輕鬆使用下列工具。 但是，所有情況下的一個關鍵問題是項目團隊的所有成員（合作夥伴和客戶）都能獲得資料。

**布吉拉**

可依您自己的需求設定的錯誤追蹤系統。

**試算表**

雖然並非特別是錯誤追蹤工具，但電子錶格通常 *mis*&#x200B;用於此用途，因為使用者容易理解，且大部分使用者都有其功能的體驗。

如果這些用於追蹤，則：

* 應該保持簡單。
* 個別電子錶格的數量應保持在最低水準。
* 必須定期更新。
* 只應維護一個主副本，每個人都應知道主副本的位置。
* 所有項目成員都應能訪問它們。
* 如果安全性是問題（通常發生在大型公司），並且無法進行共同訪問，則只要每個人都知道這些是副本，並且無法更新，就可能分發副本。

此外，還有許多專用工具可追蹤錯誤和功能需求。
