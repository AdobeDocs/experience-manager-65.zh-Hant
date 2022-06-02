---
title: 錯誤日誌中有關不建議使用的API的錯誤消息
description: 錯誤日誌中有關不建議使用的API的錯誤消息
source-git-commit: b05666883645ca11784292e4bfb5bf9c1e35a43b
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 7%

---


# 錯誤日誌中有關不建議使用的API的錯誤消息 {#error-messages-about-deprecated-apis-in-error-logs}

此問題適用於以下版本：

* Experience Manager六點五Forms

## 問題 {#issue}

* error.log檔案中出現以下錯誤消息：
   ` *WARN* [default task-36] org.apache.jackrabbit.oak.spi.security.principal.AclGroupDeprecation use of deprecated java.acl.Group-related API - this method is going to be removed in future Oak releases - see OAK-7358 for details` (NPR-38282)

## 解析度 {#workaround}

1. 安裝 [Experience Manager FormsService Pack 13或更高版本(6.5.13.0或更高版本)](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=zh-Hant)
1. 使用以下連結從軟體分發下載包（.jar檔案，解析度）:

   https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]pack/com.adobe.liveccycle.dsc.externalloginmodule-4.0.8.jar

1. 開啟Experience Manager配置管理器並安裝下載的com.adobe.liveccycle.dsc.externalloginmodule-4.0.8.jar檔案。

問題已解決。