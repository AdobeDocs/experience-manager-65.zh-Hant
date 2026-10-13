---
title: 無法還原適用於JEE叢集伺服器的損毀CRX存放庫
description: 瞭解如何還原已損毀的CRX存放庫的步驟。
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 2%
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


## 適用於 {#applies-to}

此解決方案適用於JEE叢集上的AEM Forms 。
