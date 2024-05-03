---
title: JavaScript檔案的縮制
description: 在AEM Forms工作區自訂以最佳化網頁的JS檔案後產生極簡化程式碼的指示。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: d88c6831-8ae9-426d-acb5-2a7e066ad158
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---

# JavaScript檔案的縮制 {#minification-of-the-javascript-files}

縮制會從原始程式碼中移除多餘的字元，例如空格、新行和註解。 這藉由減少程式碼大小來改善效能。 雖然縮制不會影響功能，但會降低程式碼的可讀性。

若要產生語意變更的縮製程式碼，請按照下列步驟操作。

1. 複製 `client-html/src/main/webapp/js` 檔案系統上的src-package。

   >[!NOTE]
   >
   >另請參閱 [自訂AEM Forms工作區簡介](/help/forms/using/introduction-customizing-html-workspace.md) 以取得封裝的詳細資訊。

1. 更新中的路徑 `main.js` 位於client-html/src/main/webapp/js下方，用於新增/更新的模型/檢視。

   例如，新增新的Sharequeue模型（例如mySharequeue）會變更：

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   至

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. 更新 `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` 萬一中別名變更/增加 `main.js`.

   例如，新增新的Sharequeue模型（例如mySharequeue）會變更：

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

1. 在client-html/src/main/webapp/js/minifier，執行命令：

   ```shell
   mvn clean install
   ```

   它會使用縮小的main.js和registry.js來產生client-html/src/main/webapp/js底下的縮小檔案資料夾。

>[!NOTE]
>
>縮制僅適用於64位元JVM。

>[!NOTE]
>
>若您縮制，您的升級會受到影響。
