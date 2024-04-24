---
title: 編碼准則
description: Communities開發人員指導方針、秘訣和訣竅
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a23aab83-1dfa-4d91-9b6b-6246a2103896
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 1%

---

# 編碼准則 {#coding-guidelines}

## 准則、秘訣與技巧 {#guidelines-tips-and-tricks}

使用AEM Communities已經從嚴重依賴Java Server Pages發展為靈活選擇商業邏輯、樣式和頁面內容彼此不同的範本化指令碼語言。

在使用使用者產生的內容(UGC)時，可透過SocialResourceProvider API獲得更多彈性，如此便無須瞭解哪些 [SRP](srp.md) 已為部署選擇選項。

以下是AEM Communities開發人員的各種程式碼准則和最佳作法：

### 程式碼 {#code}

* [使用SRP存取UGC](accessing-ugc-with-srp.md)  — 如何避免撰寫只有在UGC儲存在JCR (JSRP)時才有效的應用程式。
* [SocialUtils重構](socialutils.md)  — 取代SocialUtils的SRP公用程式方法。
* [命名慣例](naming-conventions.md)  — 自訂Java類別的命名慣例。

### 指令碼 {#scripts}

* [側載Communities元件](sideloading.md)  — 如何在頁面載入後動態新增元件。
* [RTF編輯器基本知識](rte.md)  — 如何自訂提供給成員以供發佈內容的RTF文字UI。

### IDE {#ide}

* [使用適用於社群的Maven](maven.md)  — 如何包含Communities API jar。
* [SocialUtils重構](socialutils.md)  — 取代SocialUtils的SRP公用程式方法。
