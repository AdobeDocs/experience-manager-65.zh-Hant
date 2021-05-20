---
title: 編碼准則
seo-title: 編碼准則
description: Communities開發人員准則、提示和秘訣
seo-description: Communities開發人員准則、提示和秘訣
uuid: 311ef4f7-7f2c-44c3-bcf2-f68713752623
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 244cd43c-a573-495d-b80c-b97ba9d19b75
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# 編碼指南{#coding-guidelines}

## 准則、提示與秘訣{#guidelines-tips-and-tricks}

使用AEM Communities已從嚴重依賴Java伺服器頁面，變成在選擇範本指令碼語言時具有彈性，其中業務邏輯、樣式和頁面內容彼此不同。

使用使用者產生的內容(UGC)時，有更大的彈性是透過SocialResourceProvider API，這就不需要為部署選擇[SRP](srp.md)選項的感知。

以下為AEM Communities開發人員適用的各種編碼准則和最佳實務：

### 程式碼 {#code}

* [使用SRP存取UGC](accessing-ugc-with-srp.md)  — 如何避免寫入僅當UGC儲存在JCR(JSRP)中時有效的應用程式。
* [SocialUtils重構](socialutils.md)  — 用於取代SocialUtils之SRP的公用程式方法。
* [命名慣例](naming-conventions.md)  — 自訂Java類的命名慣例。

### 指令碼 {#scripts}

* [側載Communities元件](sideloading.md)  — 如何在頁面載入後動態新增元件。
* [RTF編輯器要點](rte.md)  — 如何自訂為發佈內容而提供給成員的RTF UI。

### IDE {#ide}

* [使用Maven for Communities](maven.md)  — 如何包含Communities API Jar。
* [SocialUtils重構](socialutils.md)  — 用於取代SocialUtils之SRP的公用程式方法。
