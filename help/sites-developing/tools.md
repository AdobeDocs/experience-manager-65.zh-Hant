---
title: 測試和追蹤工具
seo-title: 測試和追蹤工具
description: AEM提供測試元件UI的架構，以及測試和除錯元件的機制
seo-description: AEM提供測試元件UI的架構，以及測試和除錯元件的機制
uuid: 12abedb5-4ee7-4389-9340-e628adbbc053
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 3cf0fd8d-7fc8-468a-bb1e-1debb68a82a5
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# 測試和追蹤工具{#testing-and-tracking-tools}

## 測試 {#testing}

AEM提供：

* [測試元件UI的架構](/help/sites-developing/hobbes.md)。
* [測試和除錯元件的機制](/help/sites-developing/developer-mode.md)。

以下是兩種開放原始碼測試工具：

**硒**

Selenium用於瀏覽器中的函式測試，每個活動有一個用戶。 它會將測試步驟（點按）記錄為HTML表格或Java類別。

如需詳細資訊，請參 [閱https://www.seleniumhq.org/](https://www.seleniumhq.org/)。

**JMeter**

JMeter可用來追蹤要求，並可用於功能、效能和壓力測試。

如需詳細資訊，請參 [閱https://jakarta.apache.org/jmeter/](https://jakarta.apache.org/jmeter)。

此外，還有許多專屬工具可自動化測試和管理測試計畫。

### 追蹤 {#tracking}

您可輕鬆使用下列工具。 但是，所有情況下的一個關鍵問題是，項目團隊的所有成員（合作夥伴和客戶）都可以獲得資料。

**布齊拉**

可依您自己的需求設定的錯誤追蹤系統。

**試算表**

雖然並非特別是錯誤追蹤工具，但試算表 **&#x200B;通常會因此遭誤用，因為它們易於理解，而且大部分使用者都有其功能的經驗。

如果這些用於追蹤，則：

* 應該保持簡單。
* 個別試算表的數量應保持在最低。
* 必須定期更新。
* 只應維護一個主副本，每個人都應知道主副本的位置。
* 所有專案成員都應可存取這些項目。
* 如果安全性有問題（通常發生在大公司）且無法進行共同存取，則只要每個人都知道這些是副本，而且無法更新，就可以分發副本。

此外，還有許多專屬工具可追蹤錯誤和功能需求。
