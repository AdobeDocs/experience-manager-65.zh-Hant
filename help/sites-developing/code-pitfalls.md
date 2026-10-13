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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%
---
# 程式碼陷阱{#code-pitfalls}

## 避免Java程式碼中的Sling繫結 {#avoid-sling-bindings-in-java-code}

在90%的情況下，使用Sling繫結是不合適存取服務的方式。 您應該改用&#x200B;*@Reference*&#x200B;或&#x200B;*@Inject*&#x200B;註解。

## 避免Java程式碼中的Thread.interrupt {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt*&#x200B;很危險，因為它可以在錯誤時間呼叫時關閉檔案，包括Lucene檔案和持續快取檔案。

## 避免將Java同步與ReadWriteLocks混合 {#avoid-mixing-java-synchronization-with-readwritelocks}

這可能會導致程式碼最終鎖定的競爭條件。
