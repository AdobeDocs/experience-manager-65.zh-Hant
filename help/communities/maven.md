---
title: 使用Maven for Communities
seo-title: 使用Maven for Communities
description: AEM Communities APIjar和AEM Uber APIjar
seo-description: AEM Communities APIjar和AEM Uber APIjar
uuid: ea37a89a-db6c-4018-8ab9-f5717e6c0421
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a726c904-aadd-4678-be84-9e05808ab8be
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用Maven for Communities {#using-maven-for-communities}

## 概覽 {#overview}

AEM Communities檔案的此區段除了：

* [如何使用Apache Maven建立AEM專案](../../help/sites-developing/ht-projects-maven.md)

現在有兩種「優步」文物可取代個別文物：

* AEM [Communities APIjar](#communities-api-jar-artifact)
* AEM [Uber API jar](../../help/sites-developing/ht-projects-maven.md#what-is-the-uberjar)

## Communities API jar對象 {#communities-api-jar-artifact}

以下是AEM Communities API jar的GAV範例：

```xml
<dependency>
    <groupId>com.adobe.cq.social</groupId>
    <artifactId>cq-socialcommunities-api</artifactId>
    <version>1.11.170</version>
    <scope>provided</scope>
</dependency>
```

請確定指定的版本與AEM Communities所安裝的Communities套件版本相符。 要驗證已安裝的版本號：

1. 以管理權限登入。
2. 瀏覽至 [Package Manager](../../help/sites-administering/package-manager.md)。 例如， [http://localhost:4502/crx/packmgr/](http://localhost:4502/crx/packmgr/)

3. 找到 *軟體包cq-socialcommunities-pkg-1.x.xxx*
4. 從包名稱中抽取版本
   * AEM 6.3的第一個版本是1.11.170版
   * 功能套件版本為1.12.xxx

>[!NOTE]
>
>建議您隨時更新最新的社群版本。
>
>請造訪「 [最新版本](deploy-communities.md#latest-releases) 」區段，以識別最新版本。

## Maven相關性示例 {#maven-dependency-example}

必須在Uber APIjar之前指定Communities APIjar。

```xml
<dependency>
    <groupId>com.adobe.cq.social</groupId>
    <artifactId>cq-socialcommunities-api</artifactId>
    <version>1.11.170</version>
    <scope>provided</scope>
</dependency>
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.3.0</version>
    <scope>provided</scope>
    <classifier>apis</classifier>
</dependency>
```
