---
title: 商業整合框架(CIF)附加項的顯著變化
description: 與舊的CIF版本相比，Commerce Integration Framework(CIF)附加模組發生了顯著變化。
exl-id: 41dee21a-9ae2-4067-a32a-2d4633323fc4
source-git-commit: a2ababa9dd9115e963b91a7271d204d287557c40
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 1%

---

# 對商業整合框架(CIF)附加項的顯著更改{#notable-changes}

本文檔重點介紹了Commerce Integration Framework(CIF)附加版和舊CIF版之間的重要區別，這些版本主要稱為CIF Classic(Quickstart)和CIF Open-source。

## 安裝和更新

CIF附AEM加程式包將安裝並使用程式包管AEM理器更新。

**以前的CIF版本**

* CIF經典：無需安裝， CIF是Quickstart的一部分。 CIF更新是常規或Service Pack更AEM新的一部分
* CIF開源：通過GitHub進行安裝。 更新是手動更新/維護工作的一部分。

## 終結點配置

通過OSGi控制台配置端點。

**以前的CIF版本**

* CIF經典：通過OSGi配AEM置
* CIF開源：通過CIF配置瀏覽器

## 部署CIF Venia項目

項目可用於 [GitHubAEM參考線 — CIF Venia項目](https://github.com/adobe/aem-cif-guides-venia) 和通過包管理AEM器完成部署。

**以前的CIF版本**

* CIF經典：通過包AEM安裝

## 產品目錄資料

通過即時調用支援所需GraphQLAPI的外部端點，產品目錄資料可按需獲得。 這些API支援在任何給定日期訪問即時或暫存資料。 不需要複製。

**以前的CIF版本**

* CIF經典：通過完整或增量產品導入，即時和分段產品資料將導入並保留在AEM Author上的JCR中。 將即時產品資料複製到AEM發佈。

## 產品目錄體驗與呈AEM現

使AEM用已分配給產品和類別的AEM目錄模板即時呈現產品目錄體驗。 不需要複製。

**以前的CIF版本**

* CIF經典：AEM作者使用目AEM錄藍圖工具為每個類別/產品建立一個頁面。 這些頁面被複製到AEM發佈。

>[!NOTE]
>
>有關如何將CIF與托管服務或本地AEM服務一起使用AEM的其他文檔，請參閱 [商務整合框架](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
