---
title: 無法還原適用於JEE群集伺服器的損壞的CRX儲存庫
description: 還原損壞的CRX儲存庫的步驟
source-git-commit: a7d125503b0bd3c52cb3a959e2f0dde1a69cbe2b
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 1%

---

# 無法還原損壞的CRX儲存庫 {#unable-to-restore-corrupt-crx-repository}

## 問題 {#issue}

對於部署在JEE上且具有RDB持續性的AEM Forms,AEM Forms主機和資料庫電腦必須具有絕對時間同步。 但是，如果時鐘因故不同步，則CRX儲存庫會損毀，且其URL無法存取。 錯誤為 `AuthenticationsupportService missing` 發生於記錄檔中。

## 解決方案 {#solution}

執行下列步驟以解決問題：
1. 前往  [https://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles).

1. 找出 `oak-core` 捆綁並檢查它是否正在運行。

1. 重新啟動 `oak-core` 套件組合（如果未執行）。 如果暫停按鈕位於 `oak-core` 捆綁，則表示捆綁處於運行狀態。

1. 如果問題仍未解決，請從備份中從CRX存放庫還原，或在無法使用備份時重建CRX存放庫。

   >[!NOTE]
   >
   >執行上述步驟之前，請先備份您的CRX存放庫。

## 套用至 {#applies-to}

此解決方案適用於：

* AEM Forms on JEE叢集伺服器


