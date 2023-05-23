---
title: JavaScript檔案的精簡
seo-title: Minification of the JavaScript files
description: 在AEM Forms工作區自定義後生成簡化代碼以優化Web的JS檔案的說明。
seo-description: Instructions to generate minified code after AEM Forms workspace customizations to optimize the JS files for the web.
uuid: ad91e380-a988-4740-9534-e09657e0322a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c88a3013-5da2-4b09-9f29-ac1fb00822ec
exl-id: d88c6831-8ae9-426d-acb5-2a7e066ad158
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 1%

---

# JavaScript檔案的精簡 {#minification-of-the-javascript-files}

精簡會從原始碼中刪除冗餘字元，如空白、新行和注釋。 這通過減小代碼的大小來改善效能。 雖然精簡不會影響功能，但會降低代碼的可讀性。

要生成用於語義更改的簡化代碼，請執行以下步驟。

1. 複製 `client-html/src/main/webapp/js` 檔案系統上的src-package。

   >[!NOTE]
   >
   >請參閱 [自定義AEM Forms工作區簡介](/help/forms/using/introduction-customizing-html-workspace.md) 的子菜單。

1. 更新中的路徑 `main.js` 位於client-html/src/main/webapp/js下，用於添加/更新的模型/視圖。

   例如，添加新的Sharequeue模型（如mySharequeue），請更改：

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   至

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. 更新 `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` 以防更改/添加別名 `main.js`。

   例如，添加新的Sharequeue模型（如mySharequeue），請更改：

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/models/sharequeue.js"
               service="service"/>
   ```

   至

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/myModels/mySharequeue.js"
               service="service"/>
   ```

1. 在client-html/src/main/webapp/js/minifier上，運行命令：

   ```shell
   mvn clean install
   ```

   它在client-html/src/main/webapp/js下生成帶有minified main.js和registry.js的資料夾minified-files。

>[!NOTE]
>
>精簡僅在64位JVM上工作。

>[!NOTE]
>
>如果進行微型化，則升級會受到影響。
