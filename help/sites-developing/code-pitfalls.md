---
title: 程式碼陷阱
description: 為AEM開發時應避免的常見編碼陷阱
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: c448c5d5-def8-4c1a-8db4-41eb49d0cd20
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# 程式碼陷阱{#code-pitfalls}

## 避免Java程式碼中的Sling繫結 {#avoid-sling-bindings-in-java-code}

在90%的情況下，使用Sling繫結是不合適存取服務的方式。 您應該改用 *@Reference* 或 *@Inject* 註解。

## 避免Java程式碼中的Thread.interrupt {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* 很危險，因為如果在錯誤的時間呼叫它，它可能會關閉檔案，包括Lucene檔案和持續快取檔案。

## 避免將Java同步與ReadWriteLocks混合 {#avoid-mixing-java-synchronization-with-readwritelocks}

這可能會導致程式碼最終鎖定的競爭條件。
