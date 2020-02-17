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

---


# 程式碼缺陷{#code-pitfalls}

## 避免Java程式碼中的Sling系結 {#avoid-sling-bindings-in-java-code}

在90%的案例中，Sling Bindings是取得服務的不適當方式。 您應該改用 *@Reference* 或 *@Inject注釋* 。

## 避免Java代碼中的線程中斷 {#avoid-thread-interrupt-in-java-code}

*線程中斷很危險* ，因為當在錯誤的時間調用檔案時，它可以關閉檔案，包括Lucene檔案和永久快取檔案。

## 避免將Java同步與ReadWriteLocks混合 {#avoid-mixing-java-synchronization-with-readwritelocks}

這可能導致程式碼最終陷入死鎖的競賽條件。
