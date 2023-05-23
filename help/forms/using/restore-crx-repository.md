---
title: 無法還原適用於JEE群集伺服器的損壞的CRX儲存庫
description: 恢復損壞的CRX儲存庫的步驟
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
source-git-commit: c4f776b08cb8cc8c6eea78a3757735e063bec20c
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 2%

---

# 無法還原損壞的CRX儲存庫 {#unable-to-restore-corrupt-crx-repository}

## 問題 {#issue}

對於使用關係資料庫的JEE上的AEM Forms，承載AEM Forms和關係資料庫的電腦上的時間應始終處於絕對同步狀態。 如果這些電腦上的時間不同步，則JEE伺服器上的AEM Forms的CRX-repository可能無法訪問。 它可能已損壞，並且無法通過URL訪問。 的 `AuthenticationsupportService missing` 記錄錯誤。

## 必備條件 {#prerequisites}

執行以下步驟之前，請先備份CRX儲存庫。

## 解決方案 {#solution}

請執行以下步驟來解決問題：
1. 前往  `https://[AEM Forms Server]:[port]/system/console/bundles`.

1. 查找 `oak-core` 並檢查它是否正在運行。

1. 重新啟動 `oak-core` 包。 如果  ![暫停按鈕](/help/forms/using/assets/stop.png) 表徵圖在前面 `oak-core` 綁定，則表示該綁定處於運行狀態。

1. 如果問題仍未解決，請從備份中從CRX-repository恢復，或者在備份不可用時重建CRX-repository。


## 應用於 {#applies-to}

此解決方案適用於：

* AEM FormsJEE集群