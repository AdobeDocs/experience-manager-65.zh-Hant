---
title: 升級至MySQL適用的6.5.12.0期間無法備份資料庫。
description: 當使用者升級至Experience Manager6.5.12.0並按一下「升級MySQL」時，設定管理員無法備份先前的Experience Manager Forms資料庫。
exl-id: 1af000fa-439b-4ffd-8b5a-3ba45f0c524c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# 升級至MySQL適用的6.5.12.0期間無法備份資料庫 {#issue}

當使用者升級至Experience Manager6.5.12.0並按一下「升級MySQL」時，設定管理員無法備份先前的Experience Manager Forms資料庫，它會顯示錯誤：

`Failed to backup the previous Adobe Experience Manager Forms Database`


## 套用至 {#applies-to}

* Experience Manager6.5 Forms

## 解決方案 {#solution}

若要解決此問題，請將資料庫的max_packet_size增加至100 M，或視需要增加至位於的my.ini檔案 {AEM_HOME}/mysql。
