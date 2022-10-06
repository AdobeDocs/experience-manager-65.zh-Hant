---
title: 將兩個AEM Forms工作區執行個體托管在一部伺服器上
seo-title: Hosting two AEM Forms workspace instances on one server
description: LC管理員如何自訂HTMLWS以在可透過不同URL存取的單一伺服器上托管兩個執行個體。
seo-description: How LC administrators can customize HTML WS to host two instances on a single server accessible via different URLs.
uuid: 0584f512-6b92-4418-b71c-93605cfa1927
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 1254a7c2-2c67-4661-803e-afd53e817916
exl-id: 32a546fc-e33f-46f9-ac3b-45eca0e12239
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# 將兩個AEM Forms工作區執行個體托管在一部伺服器上 {#hosting-two-aem-forms-workspace-instances-on-one-server}

AEM Forms的預設安裝與設定只允許在伺服器上使用一個AEM Forms工作區。 不過，您可能需要在單一AEM Forms伺服器上托管兩個不同的AEM Forms工作區例項。 這兩個例項可由不同URL存取。

AEM Forms管理員可自訂工作區，以建立兩個不同的URL，並讓兩個工作區可在同一伺服器上使用。 在此自訂文章中，我們假設兩個工作區可在 `https://'[server]:[port]'/lc/ws` 和 `https://'[server]:[port]':/lc/ws2`.

請依照下列步驟來設定AEM Forms工作區。

1. 在伺服器上安裝AEM Forms工作區的開發套件。 請參閱 [開發套件](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)，以取得建立此範本的指示。
1. 以管理員身分登入CRXDE Lite，方法是存取 `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. 複製節點在/content，然後貼到/content。 將節點更名為ws2。 按一下 **[!UICONTROL 全部儲存]**. 在此節點的屬性中，更改 `sling:resourceType` 到ws2。 按一下 **[!UICONTROL 全部儲存]**.

1. 從/libs複製資料夾並貼到/apps。 將資料夾更名為ws2。 按一下 **[!UICONTROL 全部儲存]**.
1. 在 `GET.jsp` at `/apps/ws2`，請變更下列程式碼。 取代下列項目

   ```html
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/libs/ws/index.html'" /><html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/libs/ws/index.html'" />
   ```

   及下列程式碼

   ```html
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. 在 `registry.js` at `/apps/ws2/js`，請變更範本路徑，以參考範本(位於 `/apps/ws2/js/runtime/templates`. 取代下列程式碼

   ```css
   "tasklist" : {
   "name": "tasklist",
   "path": "tasklistview",
   "model": "tasklist",
   "template": "text!/lc/libs/ws/js/runtime/templates/tasklist.html",
   "utility": "utility",
   "view": "taskview",
   "errorModel": null
   }
   ```

   及下列程式碼

   ```css
   "tasklist" : {
   "name": "tasklist",
   "path": "tasklistview",
   "model": "tasklist",
   "template": "text!/lc/apps/ws2/js/runtime/templates/tasklist.html",
   "utility": "utility",
   "view": "taskview",
   "errorModel": null
   }
   ```

1. 在 `userinfo.js` at `/apps/ws2/js/runtime/models` 和 `/apps/ws2/js/runtime/views`，變更字串 `/lc/content/ws` to `lc/content/ws2`.

1. 在 `/apps/ws2/js/runtime/services/service.js`，請變更 `getLocalizationData` 函式指向 `/lc/apps/ws2/Locale.html`.

1. 若要參閱 `pdf.html` ，請變更 `pdf.html` in `/apps/ws2/js/runtime/views/forms/pdftaskform.js`.

1. 若要參閱 `pdf.html` ，變更 `pdf.html` 和 `WsNextAdapter.swf` in `startprocess.html`, `taskdetails.html`，和 `processinstancehistory.html` at `/apps/ws2/js/runtime/templates`.

1. 複製 `/etc/map/ws` 資料夾和貼上位置 `/etc/map`. 將新資料夾更名為ws2。 按一下「全部儲存」 。

1. 在的屬性中 `ws2`，變更值 `sling:redirect` to `content/ws2`.

1. 變更值 `sling:match` to `^[^/\||]/[^/\||]/ws2$`.
