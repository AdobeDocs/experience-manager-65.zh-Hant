---
title: OSGi組合
description: 瞭解在Adobe Experience Manager中管理OSGi套件組合的一些秘訣。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: e18065c7-75b9-4b37-8294-cf94122a4dcf
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%
---
# OSGi組合{#osgi-bundles}

## 使用語意版本設定 {#use-semantic-versioning}

您可以在[https://semver.org/](https://semver.org/)找到語意版本編號的公認最佳實務。

## 請勿內嵌超過OSGi套件組合嚴格需要的類別和jar {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

通用程式庫應分解為單獨的套件組合。 這可讓您在套件組合中重複使用它們。 在OSGi套件組合中包裝&#x200B;*JAR*&#x200B;時，請務必檢查線上來源，以檢視是否有人之前已執行此動作。 尋找現有套裝包裝函式的一些常見位置包括：Apache Felix、Apache Sling、Apache Geronimo、Apache ServiceMix、Eclipse套裝配方和SpringSource企業套裝存放庫。

## 取決於所需的最低套件組合版本 {#depend-on-the-lowest-needed-bundle-versions}

針對POM檔案中的編譯階段相依性，一律取決於公開所需API的最低所需版本。 這樣可以提供更高的回溯相容性，並使得對舊版進行反向移植修正更加容易。

## 從OSGi套件組合匯出最小套件集 {#export-a-minimal-set-of-packages-from-osgi-bundles}

當套件已匯出時，已建立供其他人相依的API。 請務必儘可能減少匯出次數，並確認要匯出的內容為API。 取得私用方法/類別並設為公用會比取得先前已匯出的內容並設為私用要容易得多。

一律將實作放在單獨的&#x200B;*impl*&#x200B;套件中。 根據預設，*maven-bundle-plugin*&#x200B;會匯出專案中名稱沒有&#x200B;*impl*&#x200B;的任何專案。

## 一律明確定義每個匯出套件的語意版本 {#always-explicitly-define-a-semantic-version-for-each-package-exported}

這可讓您API的消費者與您一同發展。 這樣做時，請一律遵循語意版本設定最佳實務。 這可讓您API的消費者知道新版本中預期的變更型別。

## 在公開處包含中繼型別資訊 {#include-metatype-information-where-exposed}

藉由指定有意義的中繼型別資訊，讓您的服務和元件在Felix主控台中更容易理解。 您可以在[https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html)找到SCR註解和屬性的清單。
