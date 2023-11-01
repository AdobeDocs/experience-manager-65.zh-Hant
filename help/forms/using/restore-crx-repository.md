---
title: 無法還原適用於JEE叢集伺服器的損毀CRX存放庫
description: 瞭解如何還原已損壞的CRX存放庫的步驟。
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
source-git-commit: 000c22028259eb05a61625d43526a2e8314a1d60
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 2%

---

# 無法還原損壞的CRX存放庫 {#unable-to-restore-corrupt-crx-repository}

## 問題 {#issue}

對於使用關聯式資料庫的JEE版AEM Forms ，主控AEM Forms和關聯式資料庫的電腦時間應一律絕對同步。 如果這些電腦上的時間不同步，JEE伺服器上AEM Forms的CRX存放庫可能會變得無法存取。 它可能已損毀，且無法透過URL存取。 此 `AuthenticationsupportService missing` 錯誤已記錄。

## 先決條件 {#prerequisites}

在執行下述步驟之前，請備份CRX存放庫。

## 解決方案 {#solution}

1. 前往 `https://[AEM Forms Server]:[port]/system/console/bundles`。

1. 找到 `oak-core` 套件組合併檢查其是否正在執行。

1. 重新啟動 `oak-core` 套件組合（如果未執行）。 如果  ![暫停按鈕](/help/forms/using/assets/stop.png) 圖示出現在之前 `oak-core` 束，則表示束處於執行狀態。

1. 如果問題仍未解決，請從備份的CRX存放庫還原，或如果備份無法使用，則重建CRX存放庫。


## 套用至 {#applies-to}

此解決方案適用於JEE叢集上的AEM Forms 。
