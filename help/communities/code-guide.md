---
title: 編碼准則
seo-title: Coding Guidelines
description: 社區開發人員指南、提示和技巧
seo-description: Communities developer guidelines, tips, and tricks
uuid: 311ef4f7-7f2c-44c3-bcf2-f68713752623
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 244cd43c-a573-495d-b80c-b97ba9d19b75
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---

# 編碼准則 {#coding-guidelines}

## 指南、提示和技巧 {#guidelines-tips-and-tricks}

與AEM Communities合作已從高度依賴Java Server Pages發展為靈活選擇模板指令碼語言，其中業務邏輯、樣式和頁面內容彼此不同。

使用用戶生成的內容(UGC)時的更大靈活性是通過SocialResourceProvider API實現的，這消除了對其的認識的需要 [SRP](srp.md) 選項。

以下是AEM Communities開發商的各種編碼准則和最佳做法：

### 代碼 {#code}

* [使用SRP訪問UGC](accessing-ugc-with-srp.md)  — 如何避免編寫僅當UGC儲存在JCR(JSRP)中時才能使用的應用程式。
* [SocialUtils重構](socialutils.md)  — 替換SocialUtils的SRP的實用方法。
* [命名約定](naming-conventions.md)  — 為自定義Java類命名約定。

### 指令碼 {#scripts}

* [旁載入社區元件](sideloading.md)  — 如何在載入頁面後動態添加元件。
* [富格文本編輯器軟體包](rte.md)  — 如何自定義為發佈內容提供給成員的富文本UI。

### IDE {#ide}

* [將Maven用於社區](maven.md)  — 如何包括社區APIjar。
* [SocialUtils重構](socialutils.md)  — 替換SocialUtils的SRP的實用方法。
