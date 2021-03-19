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
feature: 通信管理
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 2%

---


# 通信管理：疑難排解{#correspondence-management-troubleshooting}

## 保存字母{#errors-when-saving-a-letter}時出錯

### 問題 {#issue}

保存字母時顯示以下錯誤之一：

* 文字模組不存在資料綁定
* 請提供下列項目所需的屬性資訊

### 原因 {#reason}

這些錯誤可能由於以下原因之一：

* 資料字典系結至字母，但不存在於伺服器上。
* 資料字典系結至字母，但名稱中有底線(_)。

### 解決方法{#workaround}

請確定您在字母中使用的資料字典在伺服器上存在，且名稱中沒有底線(_)。

## 預覽字母{#error-when-previewing-a-letter}時出錯

### 問題 {#issue-1}

在預覽字母時，出現「載入字母時出錯：無法從XML輸入匯入資產」，即使先前未發佈的文字資產已發佈在信函中，也會顯示。

### 解決方法{#workaround-1}

使用以下步驟重設發佈實例上的字母快取，然後重試查看字母：

1. 前往&#x200B;**`https://'[server]:[port]'/[contextPath]/system/console/configMgr`**&#x200B;並以管理員身分登入。
1. 選擇&#x200B;**Corresponce Management Configurations**。
1. 在&#x200B;**通信管理配置**&#x200B;中，禁用&#x200B;**啟用字母快取**，然後按一下&#x200B;**保存。**
1. 啟用&#x200B;**啟用字母快取** ，然後按一下&#x200B;**保存**。
1. 重試查看信函。

