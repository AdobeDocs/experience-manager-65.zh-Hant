---
title: 程式碼陷阱
seo-title: 程式碼陷阱
description: 為AEM開發時應避免的常見編碼陷阱
seo-description: 為AEM開發時應避免的常見編碼陷阱
uuid: e7413bdc-4889-45ff-bdcb-b0893d33a3b7
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 01362026-a696-4a5d-94e9-ea784eaa6e4b
exl-id: c448c5d5-def8-4c1a-8db4-41eb49d0cd20
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# 程式碼陷阱{#code-pitfalls}

## 避免Java代碼{#avoid-sling-bindings-in-java-code}中的Sling綁定

在90%的情況下，Sling系結是存取服務的不適當方式。 請改為使用&#x200B;*@Reference*&#x200B;或&#x200B;*@Inject*&#x200B;註解。

## 避免Java代碼{#avoid-thread-interrupt-in-java-code}中的Thread.interrupt

*Thread.* 中斷是危險的，因為當在錯誤的時間調用時，它可以關閉檔案，包括Lucene檔案和持久快取檔案。

## 避免將Java同步與ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}混合

這可能會導致競爭條件，其中程式碼最終會死鎖。
