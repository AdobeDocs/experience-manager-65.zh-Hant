---
title: 如何重新啟動AEM SDK？
description: 重新啟動AEM SDK的最佳實務
role: Admin, Developer, User
feature: Adaptive Forms,AEM Forms on JEE,AEM Forms on OSGi
exl-id: f5d69d04-b842-4329-b1b3-57b88266d13d
solution: Experience Manager, Experience Manager Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 1%

---

# 重新啟動AEM SDK

如果您以停止Java™程式來重新啟動AEM SDK，可能會導致AEM開發環境不一致，並出現下列錯誤：

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![Restart-aem-sdk-error](/help/forms/using/assets/restart-sdk-error.png)

## 解決方案

若要重新啟動AEM SDK，請移至使用中命令視窗並按 `Ctrl + C` 重新啟動SDK的命令。

建議您使用&#39;Ctrl + C&#39;命令重新啟動SDK。 使用替代方法重新啟動AEM SDK (例如停止Java™程式)可能會導致AEM開發環境不一致。
