---
title: 無法將Experience Manager Forms與某些版本的OracleJDK一起使用
seo-title: Unable to use Experience Manager Forms with certain versions of Oracle JDK
description: 無法將Experience Manager Forms與某些版本的OracleJDK一起使用
seo-description: Unable to use Experience Manager Forms with certain versions of Oracle JDK
exl-id: 6a8a7cb7-77d6-4bfc-82f3-82d0fddfc10a
source-git-commit: 0142b46d087d34707b09a1f172910c8b287b839d
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 4%

---

# 無法將Experience Manager Forms與某些版本的OracleJDK一起使用 {#unable-to-use-forms-with-certain-versions-of-oracle-jdk}

此問題適用於以下版本：

* Experience Manager六點三Forms
* Experience Manager六點四Forms
* Experience Manager六點五Forms

## 問題 {#issue}

用戶遇到以下異常：
`Caused by: javax.xml.xpath.XPathExpressionException: javax.xml.transform.TransformerException: JAXP0801002: the compiler encountered an XPath expression containing '101' operators that exceeds the '100' limit set by 'FEATURE_SECURE_PROCESSING'.`

## 原因 {#reason}

當您使用大於或等於以下版本的OracleJDK（Java開發工具包）版本運行Experience Manager Forms時，會出現異常：

* [JDK7u341](https://www.oracle.com/java/technologies/javase/7u341-relnotes.html)
* [JDK8u331](https://www.oracle.com/java/technologies/javase/8u331-relnotes.html)
* [JDK11u15](https://www.oracle.com/java/technologies/javase/11-0-15-relnotes.html)

上述和更高版本的Java包括JVM（Java虛擬機）中的新XML處理限制，這會導致某些Forms特定操作失敗。

## 解決方法 {#workaround}

1. 停止您的Experience Manager Forms伺服器。
1. 為應用程式伺服器配置以下JVM參數：

   `-Djdk.xml.xpathExprOpLimit=2000`

   它將JVM中的系統屬性設定為相當高的值，以便不會達到預設限制。

1. 啟動您的Experience Manager Forms伺服器。
