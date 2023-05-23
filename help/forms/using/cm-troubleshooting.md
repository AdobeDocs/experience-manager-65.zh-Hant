---
title: 「通信管理：故障排除"
seo-title: Correspondence Management Troubleshooting
description: 通信管理故障排除
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

# 通信管理：故障排除 {#correspondence-management-troubleshooting}

## 保存信件時出錯 {#errors-when-saving-a-letter}

### 問題 {#issue}

保存信件時顯示以下錯誤之一：

* 文本模組不存在資料綁定
* 請提供以下資訊所需的屬性資訊

### 原因 {#reason}

由於以下原因之一，可能會發生這些錯誤：

* 資料字典綁定到字母，但伺服器上不存在。
* 資料字典綁定到字母，但其名稱中有下划線(_)。

### 解決方法 {#workaround}

確保您在字母中使用的資料字典在伺服器上存在，且其名稱中沒有下划線(_)。

## 預覽字母時出錯 {#error-when-previewing-a-letter}

### 問題 {#issue-1}

預覽字母時，出現錯誤「載入字母時出錯：無法從XML輸入導入資產」，即使在信函中發佈以前未發佈的文本資產時也會顯示。

### 解決方法 {#workaround-1}

使用以下步驟重置發佈實例上的字母快取，然後重試查看字母：

1. 轉到 **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** 以管理員身份登錄。
1. 選擇 **通信管理配置**。
1. 在 **通信管理配置**，禁用 **啟用字母快取**&#x200B;然後按一下&#x200B;**保存。**
1. 啟用 **啟用字母快取** 然後按一下 **保存**。
1. 請重試查看信件。
