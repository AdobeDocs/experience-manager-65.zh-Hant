---
title: JavaScript檔案的縮制
description: 在AEM Forms工作區自訂以最佳化網頁的JS檔案後產生極簡化程式碼的指示。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: d88c6831-8ae9-426d-acb5-2a7e066ad158
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 1%
---
# JavaScript檔案的縮制 {#minification-of-the-javascript-files}

縮制會從原始程式碼中移除多餘的字元，例如空格、新行和註解。 這藉由減少程式碼大小來改善效能。 雖然縮制不會影響功能，但會降低程式碼的可讀性。

若要產生語意變更的縮製程式碼，請按照下列步驟操作。

1. 從檔案系統上的src-package複製`client-html/src/main/webapp/js`。

   >[!NOTE]
   >
   >如需封裝的詳細資訊，請參閱[自訂AEM Forms工作區簡介](/help/forms/using/introduction-customizing-html-workspace.md)。

1. 針對新增/更新的模型/檢視，更新位於client-html/src/main/webapp/js下方的`main.js`中的路徑。

   例如，新增新的Sharequeue模型（例如mySharequeue）會變更：

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   收件者

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. 更新`registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,`，以防`main.js`中別名變更/新增。

   例如，新增新的Sharequeue模型（例如mySharequeue）會變更：

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/models/sharequeue.js"
               service="service"/>
   ```

   收件者

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
