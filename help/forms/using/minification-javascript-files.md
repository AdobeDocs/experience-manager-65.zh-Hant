---
title: JavaScript檔案的精簡化
seo-title: JavaScript檔案的精簡化
description: 在AEM Forms工作區自訂後產生精簡程式碼的指示，以最佳化適用於網頁的JS檔案。
seo-description: 在AEM Forms工作區自訂後產生精簡程式碼的指示，以最佳化適用於網頁的JS檔案。
uuid: ad91e380-a988-4740-9534-e09657e0322a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c88a3013-5da2-4b09-9f29-ac1fb00822ec
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# JavaScript檔案的精簡化{#minification-of-the-javascript-files}

精簡功能會從原始程式碼中移除多餘的字元，例如空格、新行和註解。 如此可減少程式碼的大小，以改善效能。 雖然精簡化不會影響功能，但會降低程式碼的可讀性。

要生成用於語義更改的精簡代碼，請遵循以下步驟。

1. 從檔案系統上的src-package複製`client-html/src/main/webapp/js`。

   >[!NOTE]
   >
   >如需套件的詳細資訊，請參閱[自訂AEM Forms工作區簡介](/help/forms/using/introduction-customizing-html-workspace.md)。

1. 更新位於client-html/src/main/webapp/js下方的`main.js`中路徑，以取得已新增／更新的模型／檢視。

   例如，新增新的Sharequeue模型（例如mySharequeue），請變更：

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   至

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. 更新`registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,`，以備`main.js`中更改／添加別名。

   例如，新增新的Sharequeue模型（例如mySharequeue），請變更：

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

1. 在client-html/src/main/webapp/js/minifier上，執行命令：

   ```shell
   mvn clean install
   ```

   它會在client-html/src/main/webapp/js下，以minified main.js和registry.js產生檔案夾minified-files。

>[!NOTE]
>
>精簡功能僅適用於64位元JVM。

>[!NOTE]
>
>如果您進行微型化，升級將受到影響。
