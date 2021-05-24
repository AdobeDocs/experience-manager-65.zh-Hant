---
title: OSGI套件組合
seo-title: OSGI套件組合
description: 管理OSGi套件組合的秘訣
seo-description: 管理OSGi套件組合的秘訣
uuid: 07af7089-a233-4e5b-928c-76ddc0af8839
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8d3374ac-51dd-4ff5-84c9-495c937ade12
exl-id: e18065c7-75b9-4b37-8294-cf94122a4dcf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---

# OSGI套件組合{#osgi-bundles}

## 使用語義版本設定{#use-semantic-versioning}

在[https://semver.org/](https://semver.org/)可找到語義版本編號的商定最佳做法。

## 請勿嵌入OSGi套件組合{#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}中嚴格要求的更多類和jar

應將通用程式庫分解為個別套件。 這可讓這些檔案在您的套件組合中重複使用。 在OSGI套件組合中包裝&#x200B;*JAR*&#x200B;時，請務必檢查線上來源，查看之前是否有人已這麼做。 查找現有捆綁包裝的一些常見位置包括：Apache Felix、Apache Sling、Apache Geronimo、Apache ServiceMix、Eclipse套件配方和SpringSource Enterprise套件存放庫。

## 取決於所需的最低捆綁版本{#depend-on-the-lowest-needed-bundle-versions}

對於POM檔案中的編譯時間相依性，一律取決於需要的最低版本，可公開所需的API。 這可提高回溯相容性，並讓回轉修正程式更容易移植至舊版。

## 從OSGi套件組合{#export-a-minimal-set-of-packages-from-osgi-bundles}導出最小的套件集

匯出套件後，我們即建立可供其他人依賴的API。 請務必盡量少匯出，並確認要匯出的是API。 取用私人方法/類別並將其公開比取用先前匯出的項目並使其為私人容易得多。

實作應一律放在個別的&#x200B;*impl*&#x200B;套件中。 依預設，*maven-bundle-plugin*&#x200B;將匯出專案中名稱不含&#x200B;*impl*&#x200B;的任何項目。

## 始終顯式定義導出{#always-explicitly-define-a-semantic-version-for-each-package-exported}的每個包的語義版本

這可讓API的消費者與您一同成長。 執行此操作時，請始終遵循語義版本設定最佳實務。 這可讓API的消費者了解新版本中預期的變更類型。

## 包含公開{#include-metatype-information-where-exposed}的元類型資訊

借由指定有意義的中繼類型資訊，可讓您在Felix主控台中更輕鬆了解您的服務和元件。 SCR注釋和屬性的清單可在以下位置找到：[https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html)。
