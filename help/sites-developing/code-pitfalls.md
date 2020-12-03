---
title: 程式碼缺陷
seo-title: 程式碼缺陷
description: 針對AEM進行開發時應避免的常見編碼錯誤
seo-description: 針對AEM進行開發時應避免的常見編碼錯誤
uuid: e7413bdc-4889-45ff-bdcb-b0893d33a3b7
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 01362026-a696-4a5d-94e9-ea784eaa6e4b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---


# 程式碼缺陷{#code-pitfalls}

## 避免Java程式碼{#avoid-sling-bindings-in-java-code}中的Sling系結

在90%的案例中，Sling Bindings是取得服務的不適當方式。 您應該改用&#x200B;*@Reference*&#x200B;或&#x200B;*@Inject*&#x200B;註解。

## 避免Java代碼{#avoid-thread-interrupt-in-java-code}中的線程中斷

*線程。* 中斷是危險的，因為在調用錯誤時，它可以關閉檔案，包括Lucene檔案和持久快取檔案。

## 避免將Java同步與ReadWriteLocks {#avoid-mixing-java-synchronization-with-readwritelocks}混合

這可能導致程式碼最終陷入死鎖的競賽條件。
