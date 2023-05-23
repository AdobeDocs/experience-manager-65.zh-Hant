---
title: OSGI捆綁包
seo-title: OSGI Bundles
description: 管理OSGi捆綁包的提示
seo-description: Tips for managing your OSGi bundles
uuid: 07af7089-a233-4e5b-928c-76ddc0af8839
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8d3374ac-51dd-4ff5-84c9-495c937ade12
exl-id: e18065c7-75b9-4b37-8294-cf94122a4dcf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# OSGI捆綁包{#osgi-bundles}

## 使用語義版本控制 {#use-semantic-versioning}

有關語義版本編號的商定最佳做法，請參見 [https://semver.org/](https://semver.org/)。

## 不要在OSGi捆綁包中嵌入超出嚴格要求的類和Jar {#do-not-embed-more-classes-and-jars-than-strictly-needed-in-osgi-bundles}

應將常用庫納入單獨的捆綁包。 這樣，它們就可以在您的捆綁包中重複使用。 包裝時 *JAR* 在OSGI捆綁包中，確保檢查聯機源以查看是否有人以前已經這樣做。 查找現有捆綁包裝的一些常見位置是：Apache Felix、Apache Sling、Apache Geronimo、Apache ServiceMix、Eclipse Bundle Recipes和SpringSource Enterprise Bundle Repository。

## 取決於最低需要的捆綁包版本 {#depend-on-the-lowest-needed-bundle-versions}

對於POM檔案中的編譯時依賴項，請始終依賴於暴露所需API的最低所需版本。 這將允許更高的向後相容性，並使對舊版本的備份修復更容易。

## 從OSGi捆綁包導出最小的包集 {#export-a-minimal-set-of-packages-from-osgi-bundles}

一旦導出了包，我們就建立了一個API供其他人依賴。 確保盡可能少地導出，並確保導出的是API。 將私有方法/類轉為公開比將以前導出的內容轉為私有要容易得多。

應始終將實施放在單獨的 *撞擊* 檔案。 預設情況下， *Maven捆綁插件* 將導出項目中沒有 *撞擊* 名字。

## 始終為導出的每個包顯式定義語義版本 {#always-explicitly-define-a-semantic-version-for-each-package-exported}

這將允許您的API的使用者隨您一起發展。 執行此操作時，請始終遵循語義版本化最佳實踐。 這樣，您的API的使用者就可以知道新版本中需要哪些類型的更改。

## 包括暴露的元類型資訊 {#include-metatype-information-where-exposed}

通過指定有意義的元類型資訊，將使您的服務和元件在Felix控制台中更容易理解。 SCR注釋和屬性清單可在以下位置找到： [https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/scr-annotations.html)。
