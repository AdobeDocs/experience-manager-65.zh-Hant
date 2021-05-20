---
title: 「通信管理：疑難排解」
seo-title: 通信管理疑難排解
description: 通信管理疑難排解
seo-description: 通信管理疑難排解
uuid: 25828cdd-110e-4a84-8f31-d82cd610a54f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: cc473808-e71a-4834-bb30-91e6df783e60
feature: 通信管理
exl-id: cf06796b-bb8c-4a65-8f42-02fb0cfa3ebd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 2%

---

# 通信管理：疑難排解{#correspondence-management-troubleshooting}

## 保存字母{#errors-when-saving-a-letter}時出錯

### 問題 {#issue}

儲存信函時，會顯示下列其中一個錯誤：

* 文本模組的資料綁定不存在
* 請提供以下所需的屬性資訊

### 原因 {#reason}

可能由於以下原因之一而發生這些錯誤：

* 資料字典系結至信函，但伺服器上不存在。
* 資料字典系結至字母，但名稱中有底線(_)。

### 因應措施 {#workaround}

請確定您在信函中使用的資料字典在伺服器上存在，且名稱中沒有底線(_)。

## 預覽字母{#error-when-previewing-a-letter}時出錯

### 問題 {#issue-1}

預覽信函時，出現「載入信函時發生錯誤：無法從XML輸入匯入資產」，即使信函中已發佈先前未發佈的文字資產時亦會出現。

### 解決方法{#workaround-1}

使用下列步驟在發佈執行個體上重設信函快取，然後重試檢視信函：

1. 前往&#x200B;**`https://'[server]:[port]'/[contextPath]/system/console/configMgr`**&#x200B;並以管理員身分登入。
1. 選擇&#x200B;**通信管理配置**。
1. 在&#x200B;**通信管理配置**&#x200B;中，禁用&#x200B;**啟用信函快取**，然後按一下&#x200B;**保存。**
1. 啟用&#x200B;**啟用字母快取**，然後按一下&#x200B;**保存**。
1. 重試查看信函。
