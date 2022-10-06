---
title: 商務整合架構(CIF)附加元件的重大變更
description: 與舊版CIF相比，Commerce Integration Framework(CIF)附加元件有顯著變更。
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
source-git-commit: 78359fb8ecbcc0227ab5a3910175aed73d823902
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# 商務整合架構(CIF)附加元件的重大變更{#notable-changes}

本檔案著重說明Commerce Integration Framework(CIF)附加元件與舊版CIF之間的重要差異，主要稱為CIF Classic(Quickstart)和CIF開放原始碼。

## 安裝和更新

AEM CIF附加套件會安裝並更新為AEM Package Manager。

**舊版CIF**

* CIF Classic:無需安裝，CIF是快速入門的一部分。 CIF更新是一般AEM或Service Pack更新的一部分
* CIF開放原始碼：透過GitHub進行安裝。 更新是手動更新/維護工作的一部分。

## 端點配置

端點會透過OSGi主控台進行設定。

**舊版CIF**

* CIF Classic:在AEM中透過OSGi設定
* CIF開放原始碼：透過CIF組態瀏覽器

## CIF Venia項目部署

可用專案 [GitHub AEM指南 — CIF Venia專案](https://github.com/adobe/aem-cif-guides-venia) 和透過AEM Package Manager完成部署。

**舊版CIF**

* CIF Classic:透過AEM套件安裝

## 產品目錄資料

透過對支援所需GraphQL API的外部端點的即時呼叫，隨選要求產品目錄資料。 這些API支援在任何指定日期存取即時或暫存資料。 無需複製。

**舊版CIF**

* CIF Classic:即時和分段產品資料會透過完整或增量產品匯入，匯入並保存在AEM Author的JCR中。 即時產品資料會複製至AEM Publish。

## 透過AEM轉譯提供產品目錄體驗

AEM會使用指派給產品和類別的AEM目錄範本，即時轉譯產品目錄體驗。 無需複製。

**舊版CIF**

* CIF Classic:AEM作者會使用目錄Blueprint工具，為每個類別/產品建立AEM頁面。 這些頁面會復寫至AEM Publish。

>[!NOTE]
>
>如需如何搭配AEM Managed Service或AEM On-Premise使用CIF的其他檔案，請參閱 [商務整合架構](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
