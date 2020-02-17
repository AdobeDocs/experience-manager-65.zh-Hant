---
title: 命名慣例
seo-title: 命名慣例
description: Java包名稱中的連字元
seo-description: Java包名稱中的連字元
uuid: 48086e6c-c35b-4ffc-b216-d01feca7bf9a
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 5271feb9-70c6-4c82-8ac7-34a63d80e3aa
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 命名慣例 {#naming-conventions}

## Java包名稱中的連字元 {#hyphens-in-java-package-name}

建立Java類的位置時，請注意，包名必須與儲存庫資料夾位置的名稱匹配，路徑中的任何連字元都正確逸出。

雖然在AEM開發中建議在儲存庫項目名稱中使用連字型大小，但連字型大小在Java套件名稱中是非法的。

基礎的CRX平台必須能夠區分實際下划線&#39;_&#39;和連字元&#39;-&#39;。 因此，在JCR中，連字型大小必須以其unicode值(u002d)取代，並以底線&#39;_&#39;逸出。

例如，如果儲存庫路徑是 **/apps/my-example/component/info/Info.java**，則包名應為 `java package apps.my_002dexample.component.info;`

請注意，下划線同樣必須逸出，這樣便 `_` 會變 `_005f`成。
