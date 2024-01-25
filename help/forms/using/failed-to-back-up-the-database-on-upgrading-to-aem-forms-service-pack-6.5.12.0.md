---
title: 無法在AEM Forms 6.5.12.0上備份先前的資料庫。
description: 當使用者升級至Experience Manager6.5.12.0並按一下「升級MySQL」時，設定管理員無法備份先前的Experience Manager Forms資料庫。
source-git-commit: d232bfdad7b8413eb015f6fe5dd3442cebf1001d
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 1%

---

# 問題(#issue)

當使用者升級至Experience Manager6.5.12.0並按一下「升級MySQL」時，設定管理員無法備份先前的Experience Manager Forms資料庫，它會顯示錯誤：

`Failed to backup the previous Adobe Experience Manager Forms Database`


## 套用至 {#applies-to}

* Experience Manager6.5 Forms

## 解決方案 {#solution}

若要解決此問題，請將資料庫的max_packet_size增加至100 M，或視需要增加至位於的my.ini檔案 {AEM_HOME}/mysql。
