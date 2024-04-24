---
title: Java&trade；套件名稱中的命名慣例
description: 瞭解命名慣例和Java&trade；套件名稱中連字型大小的使用方式。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 1%

---

# 命名慣例 {#naming-conventions}

## Java™封裝名稱中的連字型大小 {#hyphens-in-java-package-name}

建立Java™類別的位置時，套件名稱必須與存放庫資料夾位置的名稱相符，且路徑中的所有連字型大小都必須正確逸出。

雖然在AEM開發的建議做法是在存放庫專案的名稱中使用連字型大小，但Java™封裝名稱中的連字型大小是不合法的。

底層CRX平台必須能夠區分實際底線 `_ `和連字型大小 `-`. 因此，在JCR中，連字型大小必須以其Unicode值(u002d)取代，並以底線逸出 `_`.

例如，如果存放庫路徑為 **/apps/my-example/component/info/Info.java**，封裝名稱應為 `java package apps.my_002dexample.component.info;`

請注意，底線必須以類似方式逸出，例如 `_` 變為 `_005f`.
