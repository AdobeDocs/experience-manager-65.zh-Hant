---
title: 「通信管理：疑難排解」
seo-title: 通信管理故障排除
description: 通信管理故障排除
seo-description: 通信管理故障排除
uuid: 25828cdd-110e-4a84-8f31-d82cd610a54f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: cc473808-e71a-4834-bb30-91e6df783e60
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 通信管理：疑難排解 {#correspondence-management-troubleshooting}

## 保存信件時出錯 {#errors-when-saving-a-letter}

### 問題 {#issue}

保存字母時顯示以下錯誤之一：

* 文字模組不存在資料綁定
* 請提供下列項目所需的屬性資訊

### 原因 {#reason}

這些錯誤可能由於以下原因之一：

* 資料字典系結至字母，但不存在於伺服器上。
* 資料字典系結至字母，但名稱中有底線(_)。

### 解決方法 {#workaround}

請確定您在字母中使用的資料字典在伺服器上存在，且名稱中沒有底線(_)。

## 預覽字母時出錯 {#error-when-previewing-a-letter}

### 問題 {#issue-1}

在預覽字母時，出現「載入字母時出錯：無法從XML輸入匯入資產」，即使先前未發佈的文字資產已發佈在信函中，也會顯示。

### 解決方法 {#workaround-1}

使用以下步驟重設發佈實例上的字母快取，然後重試查看字母：

1. 前往並 **`https://[server]:[port]/[contextPath]/system/console/configMgr`** 以管理員身分登入。
1. 選擇「 **對應管理配置」**。
1. 在「對 **應管理配置」中**，禁用「 **啟用字母快取」,**&#x200B;然後按一下&#x200B;**「保存」。**
1. 啟用 **字母快取** ，然後按一 **下儲存**。
1. 重試查看信函。

