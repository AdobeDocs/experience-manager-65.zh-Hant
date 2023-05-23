---
title: Java包名稱中的命名約定
description: Java包名稱中的連字元
uuid: 48086e6c-c35b-4ffc-b216-d01feca7bf9a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 5271feb9-70c6-4c82-8ac7-34a63d80e3aa
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 1%

---

# 命名慣例 {#naming-conventions}

## Java包名稱中的連字元 {#hyphens-in-java-package-name}

在為Java類建立位置時，請注意，包名稱必須與儲存庫資料夾位置的名稱匹配，路徑中的任何連字元必須正確轉義。

雖然在儲存庫項目名稱中使用連字元是開發中推薦的AEM做法，但連字元在Java包名稱中是非法的。

基礎CRX平台必須能夠區分實際下划線 `_ `連字元 `-`。 因此，在JCR中，連字元必須用其unicode值(u002d)替換，並用下划線轉義 `_`。

例如，如果儲存庫路徑為 **/apps/my-example/component/info/Info.java**，包名稱應為 `java package apps.my_002dexample.component.info;`

請注意，下划線同樣必須轉義，這樣 `_` 變成 `_005f`。
