---
title: 編碼准則
seo-title: 編碼准則
description: 社群開發人員准則、秘訣與訣竅
seo-description: 社群開發人員准則、秘訣與訣竅
uuid: 311ef4f7-7f2c-44c3-bcf2-f68713752623
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 244cd43c-a573-495d-b80c-b97ba9d19b75
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 編碼准則 {#coding-guidelines}

## 准則、秘訣與訣竅 {#guidelines-tips-and-tricks}

與AEM Communities合作已從嚴重依賴Java Server Pages轉變為靈活選擇範本指令碼語言，其中商業邏輯、樣式和頁面內容彼此不同。

使用使用者產生的內容(UGC)的更大彈性是透過SocialResourceProvider API，這樣就不需要瞭解 [SRP](srp.md) 選項是選擇用於部署。

以下是AEM Communities開發人員的各種編碼准則和最佳實務：

### 程式碼 {#code}

* [使用SRP存取UGC](accessing-ugc-with-srp.md) —— 如何避免編寫僅在UGC儲存在JCR(JSRP)中時才能運作的應用程式。
* [SocialUtils重構](socialutils.md) -取代SocialUtils之SRP的公用程式方法。
* [命名慣例](naming-conventions.md) -自訂Java類別的命名慣例。

### 指令碼 {#scripts}

* [側載社群元件](sideloading.md) -如何在頁面載入後動態新增元件。
* [Rich Text Editor Essentials](rte.md) —— 如何自訂提供給會員的Rich Text UI，以發佈內容。

### IDE {#ide}

* [使用Maven for Communities](maven.md) —— 如何包含Communities APIjar。
* [SocialUtils重構](socialutils.md) -取代SocialUtils之SRP的公用程式方法。

