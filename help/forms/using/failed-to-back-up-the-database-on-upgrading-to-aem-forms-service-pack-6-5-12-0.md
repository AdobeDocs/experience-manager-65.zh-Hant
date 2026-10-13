---
title: 升級至MySQL適用的6.5.12.0期間無法備份資料庫。
description: 當使用者升級至Experience Manager 6.5.12.0並按一下「升級MySQL」時，設定管理員無法備份先前的Experience Manager Forms資料庫。
exl-id: 1af000fa-439b-4ffd-8b5a-3ba45f0c524c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 94663796-0ee7-58b9-84f4-b425ebb69e83
    internal-label: AEM Forms on JEE
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 2%
---
# 在升級為MySQL的6.5.12.0期間無法備份資料庫 {#issue}

當使用者升級至Experience Manager 6.5.12.0並按一下[升級MySQL]時，組態管理員無法備份先前的Experience Manager Forms資料庫，它會顯示錯誤：

`Failed to backup the previous Adobe Experience Manager Forms Database`


## 適用於 {#applies-to}

* Experience Manager 6.5 Forms

## 解決方案 {#solution}

若要解決此問題，請將資料庫的max_packet_size增加至100 M，或視位於{AEM_HOME}/mysql的my.ini檔案需要增加。
