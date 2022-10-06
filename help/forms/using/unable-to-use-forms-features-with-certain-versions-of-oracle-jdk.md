---
title: 無法將Experience Manager Forms用於某些版本的OracleJDK
seo-title: Unable to use Experience Manager Forms with certain versions of Oracle JDK
description: 無法將Experience Manager Forms用於某些版本的OracleJDK
seo-description: Unable to use Experience Manager Forms with certain versions of Oracle JDK
exl-id: 6a8a7cb7-77d6-4bfc-82f3-82d0fddfc10a
source-git-commit: 0142b46d087d34707b09a1f172910c8b287b839d
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 4%

---

# 無法將Experience Manager Forms用於某些版本的OracleJDK {#unable-to-use-forms-with-certain-versions-of-oracle-jdk}

此問題適用於下列版本：

* Experience Manager6.3Forms
* Experience Manager6.4 Forms
* Experience Manager6.5Forms

## 問題 {#issue}

用戶遇到以下異常：
`Caused by: javax.xml.xpath.XPathExpressionException: javax.xml.transform.TransformerException: JAXP0801002: the compiler encountered an XPath expression containing '101' operators that exceeds the '100' limit set by 'FEATURE_SECURE_PROCESSING'.`

## 原因 {#reason}

當您使用大於或等於下列版本的OracleJDK（Java開發套件）執行Experience Manager Forms時，會發生例外狀況：

* [JDK7u341](https://www.oracle.com/java/technologies/javase/7u341-relnotes.html)
* [JDK8u331](https://www.oracle.com/java/technologies/javase/8u331-relnotes.html)
* [JDK11u15](https://www.oracle.com/java/technologies/javase/11-0-15-relnotes.html)

上述及更新版本的Java，在JVM（Java虛擬機）中加入新的XML處理限制，導致某些Forms特定操作失敗。

## 因應措施 {#workaround}

1. 停止Experience Manager Forms伺服器。
1. 為應用程式伺服器配置以下JVM參數：

   `-Djdk.xml.xpathExprOpLimit=2000`

   它會將JVM中的系統屬性設定為相當高的值，以便不點擊預設限制。

1. 啟動您的Experience Manager Forms伺服器。
