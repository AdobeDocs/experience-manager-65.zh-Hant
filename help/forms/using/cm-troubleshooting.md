---
title: 「通訊管理：疑難排解」
description: 瞭解如何處理在AEM Forms環境中儲存信函的過程中發生的錯誤。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
exl-id: cf06796b-bb8c-4a65-8f42-02fb0cfa3ebd
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 1%

---

# 通訊管理：疑難排解 {#correspondence-management-troubleshooting}

## 儲存字母時發生錯誤 {#errors-when-saving-a-letter}

### 問題 {#issue}

儲存信函時會顯示下列其中一個錯誤：

* 文字模組沒有資料繫結
* 提供下列專案所需的屬性資訊

### 原因 {#reason}

發生這些錯誤可能是因為下列原因之一：

* 資料字典已繫結至信件，但伺服器上不存在。
* 資料字典已繫結至字母，但名稱有底線(_)。

### 因應措施 {#workaround}

確認您在信函中使用的資料字典位於伺服器上，且名稱不含底線(_)。

## 預覽信函時發生錯誤 {#error-when-previewing-a-letter}

### 問題 {#issue-1}

預覽信函時，即使信函中先前未發佈的文字資產已發佈，也會出現「載入信函時發生錯誤：無法從XML輸入匯入資產」錯誤。

### 因應措施 {#workaround-1}

使用以下步驟重設發佈執行個體上的信件快取，然後再次嘗試檢視信件：

1. 前往&#x200B;**`https://'[server]:[port]'/[contextPath]/system/console/configMgr`**&#x200B;並以管理員身分登入。
1. 選取&#x200B;**通訊管理設定**。
1. 在&#x200B;**通訊管理設定**&#x200B;中，停用&#x200B;**啟用信件快取**，然後按一下&#x200B;**[儲存]。**
1. 勾選&#x200B;**啟用信件快取**，然後按一下&#x200B;**儲存**。
1. 重試檢視信件。
