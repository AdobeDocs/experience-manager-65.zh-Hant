---
title: OSGi組合
description: 瞭解在Adobe Experience Manager中管理OSGi套件組合的一些秘訣。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: e18065c7-75b9-4b37-8294-cf94122a4dcf
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# OSGi組合{#osgi-bundles}

## 使用語意版本設定 {#use-semantic-versioning}

語意版本編號的公認最佳實務可在 [https://semver.org/](https://semver.org/).

## 請勿內嵌超過OSGi套件組合嚴格需要的類別和jar {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

通用程式庫應分解為單獨的套件組合。 這可讓您在套件組合中重複使用它們。 包裝時 *JAR* 在OSGi套件組合中，請務必檢查線上來源，以檢視是否有人之前已執行此動作。 尋找現有套裝包裝函式的一些常見位置包括：Apache Felix、Apache Sling、Apache Geronimo、Apache ServiceMix、Eclipse套裝配方和SpringSource企業套裝存放庫。

## 取決於所需的最低套件組合版本 {#depend-on-the-lowest-needed-bundle-versions}

針對POM檔案中的編譯階段相依性，一律取決於公開所需API的最低所需版本。 這樣可以提供更高的回溯相容性，並使得對舊版進行反向移植修正更加容易。

## 從OSGi套件組合匯出最小套件集 {#export-a-minimal-set-of-packages-from-osgi-bundles}

當套件已匯出時，已建立供其他人相依的API。 請務必儘可能減少匯出次數，並確認要匯出的內容為API。 取得私用方法/類別並設為公用會比取得先前已匯出的內容並設為私用要容易得多。

一律將實作放置在不同位置 *實作* 封裝。 根據預設， *maven-bundle-plugin* 匯出專案中沒有 *實作* 在其名稱中。

## 一律明確定義每個匯出套件的語意版本 {#always-explicitly-define-a-semantic-version-for-each-package-exported}

這可讓您API的消費者與您一同發展。 這樣做時，請一律遵循語意版本設定最佳實務。 這可讓您API的消費者知道新版本中預期的變更型別。

## 在公開處包含中繼型別資訊 {#include-metatype-information-where-exposed}

藉由指定有意義的中繼型別資訊，讓您的服務和元件在Felix主控台中更容易理解。 SCR註釋和屬性清單可在以下網址找到： [https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html).
