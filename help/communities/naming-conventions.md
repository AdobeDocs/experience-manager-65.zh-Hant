---
title: 命名慣例
seo-title: 命名慣例
description: Java包名稱中的連字型大小
seo-description: Java包名稱中的連字型大小
uuid: 48086e6c-c35b-4ffc-b216-d01feca7bf9a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 5271feb9-70c6-4c82-8ac7-34a63d80e3aa
exl-id: 863900c3-5fe8-41a3-a151-466d0c62eeea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# 命名慣例{#naming-conventions}

## Java包名稱{#hyphens-in-java-package-name}中的連字型大小

為Java類建立位置時，請注意，包名稱必須與儲存庫資料夾位置的名稱匹配，並且路徑中的任何連字型大小都會正確轉義。

雖然在AEM開發中建議在存放庫項目名稱中使用連字型大小，但在Java套件名稱中使用連字型大小是非法的。

基礎的CRX平台必須能夠區分實際的底線`_ `和連字型大小`-`。 因此，在JCR中，連字型大小必須替換為其unicode值(u002d)，並以下划線`_`逸出。

例如，如果儲存庫路徑為&#x200B;**/apps/my-example/component/info/Info.java**，則包名稱應為`java package apps.my_002dexample.component.info;`

請注意，底線也必須同樣逸出，使`_`變成`_005f`。
