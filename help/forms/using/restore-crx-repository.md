---
title: 無法還原適用於JEE叢集伺服器的損毀CRX存放庫
description: 瞭解如何還原已損毀的CRX存放庫的步驟。
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 1%

---

# 無法還原損壞的CRX存放庫 {#unable-to-restore-corrupt-crx-repository}

## 問題 {#issue}

對於使用關聯式資料庫的JEE版AEM Forms ，主控AEM Forms和關聯式資料庫的電腦時間應一律絕對同步。 如果這些電腦上的時間不同步，可能無法存取JEE伺服器上AEM Forms的CRX存放庫。 它可能已損毀，且無法透過URL存取。 已記錄`AuthenticationsupportService missing`錯誤。

## 先決條件 {#prerequisites}

在執行下列步驟之前，請備份CRX存放庫。

## 解決方案 {#solution}

1. 移至`https://[AEM Forms Server]:[port]/system/console/bundles`。

1. 找到`oak-core`套件組合併檢查它是否正在執行。

1. 如果`oak-core`套件組合未執行，請重新啟動。 如果![暫停按鈕](/help/forms/using/assets/stop.png)圖示出現在`oak-core`套件組合之前，則表示套件組合處於執行狀態。

1. 如果問題仍未解決，請從備份中從CRX存放庫還原，或如果備份無法使用，重建CRX存放庫。


## 套用至 {#applies-to}

此解決方案適用於JEE叢集上的AEM Forms 。
