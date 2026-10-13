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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 1%
---
# 命名慣例 {#naming-conventions}

## Java™封裝名稱中的連字型大小 {#hyphens-in-java-package-name}

建立Java™類別的位置時，套件名稱必須與存放庫資料夾位置的名稱相符，且路徑中的所有連字型大小都必須正確逸出。

雖然在AEM開發中，建議在存放庫專案的名稱中使用連字型大小，但Java™封裝名稱中使用連字型大小是不合法的。

基礎CRX平台必須能夠區分實際底線`_ `和連字型大小`-`。 因此，在JCR中，連字型大小必須以其Unicode值(u002d)取代，並以底線`_`逸出。

例如，如果存放庫路徑是&#x200B;**/apps/my-example/component/info/Info.java**，封裝名稱應該是`java package apps.my_002dexample.component.info;`

請注意，底線同樣必須逸出，這樣`_`會變成`_005f`。
