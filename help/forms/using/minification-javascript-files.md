---
title: JavaScript檔案的縮制
seo-title: Minification of the JavaScript files
description: 在AEM Forms工作區自訂後產生縮製程式碼的指示，以最佳化網頁的JS檔案。
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

# JavaScript檔案的縮制 {#minification-of-the-javascript-files}

縮制會從原始碼中移除多餘的字元，例如空白字元、新行和註解。 這可以縮小程式碼的大小，進而改善效能。 縮制不會影響功能，但會降低程式碼的可讀性。

要生成語義更改的縮制代碼，請執行以下步驟。

1. 複製 `client-html/src/main/webapp/js` 從檔案系統上的src-package。

   >[!NOTE]
   >
   >請參閱 [自訂AEM Forms工作區簡介](/help/forms/using/introduction-customizing-html-workspace.md) 以取得套件的詳細資訊。

1. 更新 `main.js` 位於client-html/src/main/webapp/js下，以取得已新增/更新的模型/檢視。

   例如，添加新的Sharequeue模型（如mySharequeue），請更改：

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   至

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. 更新 `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` 若 `main.js`.

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

   它會在client-html/src/main/webapp/js下產生一個資料夾縮制檔案，其中包含縮制的main.js和registry.js。

>[!NOTE]
>
>縮制只能在64位元JVM上運作。

>[!NOTE]
>
>如果您縮制，升級會受到影響。
