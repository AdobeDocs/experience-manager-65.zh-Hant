---
title: 無法還原適用於JEE群集伺服器的損壞的CRX儲存庫
description: 還原損壞的CRX儲存庫的步驟
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
source-git-commit: cf034e8765317ee022aad4693ced37c3fa793ff2
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 2%

---

# 無法還原損壞的CRX儲存庫 {#unable-to-restore-corrupt-crx-repository}

## 問題 {#issue}

若是使用關係資料庫的JEE上的AEM Forms，托管AEM Forms的電腦上的時間和關係資料庫應一律保持絕對同步。 如果這些電腦上的時間不同步，JEE伺服器上AEM Forms的CRX存放庫可能無法存取。 它可能看起來已損壞，並且無法通過URL訪問。 此 `AuthenticationsupportService missing` 記錄錯誤。

## 必備條件 {#prerequisites}

執行下列步驟之前，請先備份CRX存放庫。

## 解決方案 {#solution}

執行下列步驟以解決問題：
1. 前往  `https://[AEM Forms Server]:[port]/system/console/bundles`.

1. 找出 `oak-core` 捆綁並檢查它是否正在運行。

1. 重新啟動 `oak-core` 套件組合（如果未執行）。 若  ![暫停按鈕](/help/forms/using/assets/stop.png) 表徵圖位於 `oak-core` 捆綁，則表示捆綁處於運行狀態。

1. 如果問題仍未解決，請從備份中從CRX-repository還原，或在無法使用備份時重建CRX-repository。


## 套用至 {#applies-to}

此解決方案適用於：

* AEM Forms on JEE叢集環境