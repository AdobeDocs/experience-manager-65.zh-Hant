---
title: 商務整合框架(CIF)附加元件的顯著變更
description: 與舊版CIF相比，Commerce Integration Framework(CIF)附加元件有顯著的變更。
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32,c136763f-56aa-450e-8796-bc84bf6c205d
translation-type: tm+mt
source-git-commit: a8dba82029168660b84b085ab46d0406b19961ef
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# 商務整合框架(CIF)附加元件的顯著變更{#notable-changes}

本檔案著重說明商務整合框架(CIF)附加元件與舊版CIF之間的重要差異，主要稱為CIF Classic(Quickstart)和CIF開放原始碼。

## 安裝與更新

CIF附AEM加套件會安裝並更新套件管AEM理器。

**舊版CIF**

* CIF Classic:無需安裝， CIF是快速入門計畫的一部分。 CIF更新是定期或Service Pack更AEM新的一部分
* CIF開放原始碼：透過GitHub進行安裝。 更新是手動更新／維護工作的一部分。

## 端點配置

端點通過OSGi控制台進行配置。

**舊版CIF**

* CIF Classic:透過OSGi組態，於AEM
* CIF開放原始碼：透過CIF組態瀏覽器

## CIF Venia項目的部署

[GitHub指南中提供的項AEM目- CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia)，並通過包管理器完成部AEM署

**舊版CIF**

* CIF Classic:透過套件AEM安裝

## 產品目錄資料

透過即時呼叫支援所需GraphQL API的外部端點，隨選取得產品目錄資料。 這些API支援在任何指定日期存取即時或分段資料。 無需複製。

**舊版CIF**

* CIF Classic:即時和分段產品資料會透過完整或增量產品匯入，匯入並持續存留在AEM Author的JCR中。 即時產品資料會複製至AEM Publish。

## 產品型錄體驗與轉AEM譯

使AEM用已指派給產品和類別的AEM目錄範本即時轉換產品目錄體驗。 無需複製。

**舊版CIF**

* CIF Classic:AEM Author使用目AEM錄藍圖工具為每個類別／產品建立頁面。 這些頁面會複製至AEM Publish。

>[!NOTE]
>
>有關如何搭配受管服務或內部部署使AEM用CIF的其AEM他文檔，請參閱[商務整合架構](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
