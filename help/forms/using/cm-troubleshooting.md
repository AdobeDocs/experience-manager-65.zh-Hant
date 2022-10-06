---
title: 「通信管理：疑難排解」
seo-title: Correspondence Management Troubleshooting
description: 通信管理疑難排解
seo-description: Correspondence Management Troubleshooting
uuid: 25828cdd-110e-4a84-8f31-d82cd610a54f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: cc473808-e71a-4834-bb30-91e6df783e60
feature: Correspondence Management
exl-id: cf06796b-bb8c-4a65-8f42-02fb0cfa3ebd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 1%

---

# 通信管理：疑難排解 {#correspondence-management-troubleshooting}

## 儲存信函時發生錯誤 {#errors-when-saving-a-letter}

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

## 預覽信函時出錯 {#error-when-previewing-a-letter}

### 問題 {#issue-1}

預覽信函時，出現「載入信函時發生錯誤：無法從XML輸入匯入資產」，即使信函中已發佈先前未發佈的文字資產時亦會出現。

### 因應措施 {#workaround-1}

使用下列步驟在發佈執行個體上重設信函快取，然後重試檢視信函：

1. 前往 **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** 並以管理員身分登入。
1. 選擇 **通信管理配置**.
1. 在 **通信管理配置**，停用 **啟用信函快取**&#x200B;然後按一下&#x200B;**儲存。**
1. 啟用 **啟用信函快取** 然後按一下 **儲存**.
1. 重試查看信函。
