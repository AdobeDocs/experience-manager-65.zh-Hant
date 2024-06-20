---
title: 無法搭配特定版本的OracleJDK使用Experience Manager Forms
description: 無法搭配特定版本的OracleJDK使用Experience Manager Forms
exl-id: 6a8a7cb7-77d6-4bfc-82f3-82d0fddfc10a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Troubleshooting
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 1%

---

# 無法搭配特定版本的OracleJDK使用Experience Manager Forms {#unable-to-use-forms-with-certain-versions-of-oracle-jdk}

此問題適用於下列版本：

* Experience Manager6.3 Forms
* Experience Manager6.4 Forms
* Experience Manager6.5 Forms

## 問題 {#issue}

使用者遇到下列例外狀況：
`Caused by: javax.xml.xpath.XPathExpressionException: javax.xml.transform.TransformerException: JAXP0801002: the compiler encountered an XPath expression containing '101' operators that exceeds the '100' limit set by 'FEATURE_SECURE_PROCESSING'.`

## 原因 {#reason}

當您執行Experience Manager Forms且其OracleJDK (Java Development Kit)版本大於或等於下列版本時，會發生例外情況：

* [JDK7u341](https://www.oracle.com/java/technologies/javase/7u341-relnotes.html)
* [JDK8u331](https://www.oracle.com/java/technologies/javase/8u331-relnotes.html)
* [JDK11u15](https://www.oracle.com/java/technologies/javase/11-0-15-relnotes.html)

上述和更新版本的Java包括JVM （Java虛擬機器器）中的新XML處理限制，這會造成某些Forms特定作業失敗。

## 因應措施 {#workaround}

1. 停止您的Experience Manager Forms伺服器。
1. 為您的應用程式伺服器設定下列JVM引數：

   `-Djdk.xml.xpathExprOpLimit=2000`

   它會將JVM中的系統屬性設定為相當高的值，這樣就不會達到預設限制。

1. 啟動您的Experience Manager Forms伺服器。
