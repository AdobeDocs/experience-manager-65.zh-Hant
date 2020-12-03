---
title: OSGI Bundles
seo-title: OSGI Bundles
description: 管理OSGi組合的秘訣
seo-description: 管理OSGi組合的秘訣
uuid: 07af7089-a233-4e5b-928c-76ddc0af8839
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8d3374ac-51dd-4ff5-84c9-495c937ade12
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---


# OSGI Bundles{#osgi-bundles}

## 使用語義版本化{#use-semantic-versioning}

在[https://semver.org/](https://semver.org/)中，可找到語義版本編號的商定最佳做法。

## 不要嵌入比OSGi bundles {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}中嚴格需要的更多類和jar

應將常用程式庫分解為個別的組合。 這可讓您在整個套件間重複使用這些項目。 在OSGI套件中封裝&#x200B;*JAR*&#x200B;時，請務必檢查線上來源，以查看是否有人之前已這麼做。 尋找現有包裝函式的常見位置有：Apache Felix、Apache Sling、Apache Geronimo、Apache ServiceMix、Eclipse Bundle Recipes和SpringSource Enterprise Bundle Repository。

## 取決於所需的最低包版本{#depend-on-the-lowest-needed-bundle-versions}

對於POM檔案中的編譯時間相關性，請始終依賴於暴露所需API的最低需要版本。 這可讓回溯相容性更高，並讓舊版的回溯修正更容易。

## 從OSGi bundles {#export-a-minimal-set-of-packages-from-osgi-bundles}導出最少一組軟體包

一旦匯出套件，我們便已建立API供其他人依賴。 請務必盡可能少地導出，並確保要導出的是API。 採用私有方法／類並將其公開要比採用以前導出的內容和私有方法容易得多。

實施應始終放在單獨的&#x200B;*impl*&#x200B;包中。 依預設，*maven-bundle-plugin*&#x200B;將匯出專案中名稱中未包含&#x200B;*impl*&#x200B;的任何項目。

## 始終明確定義每個導出{#always-explicitly-define-a-semantic-version-for-each-package-exported}的包的語義版本

這可讓您的API消費者與您一起發展。 在執行此操作時，請始終遵循語義版本修訂最佳實踐。 這可讓API的消費者知道新版本中預期的變更類型。

## 包含公開{#include-metatype-information-where-exposed}的metatype資訊

透過指定有意義的metatype資訊，可讓您在Felix主控台中更容易瞭解您的服務和元件。 SCR注釋和屬性的清單可在以下位置找到：[https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html)。
