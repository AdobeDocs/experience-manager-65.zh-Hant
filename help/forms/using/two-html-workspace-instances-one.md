---
title: 在單一伺服器上主控兩個AEM Forms工作區執行個體
description: LC管理員如何自訂HTMLWS，以便在可透過不同URL存取的單一伺服器上託管兩個執行個體。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 32a546fc-e33f-46f9-ac3b-45eca0e12239
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---

# 在單一伺服器上主控兩個AEM Forms工作區執行個體 {#hosting-two-aem-forms-workspace-instances-on-one-server}

AEM Forms的預設安裝與設定只允許伺服器上有一個AEM Forms工作區。 不過，您可能需要在單一AEM Forms伺服器上託管兩個不同的AEM Forms工作區例項。 這兩個執行個體可透過不同的URL存取。

AEM Forms管理員可自訂工作區，以建立兩個不同的URL，並讓兩個工作區可在同一部伺服器上使用。 在本自訂文章中，您可以假設兩個工作區可在以下位置存取： `https://'[server]:[port]'/lc/ws` 和 `https://'[server]:[port]':/lc/ws2`.

請依照下列步驟設定AEM Forms工作區。

1. 在伺服器上安裝AEM Forms工作區的開發套件。 另請參閱 [開發套件](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)，以取得建立它的指示。
1. 以管理員身分登入CRXDE Lite，方法是存取 `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. 在/content處複製節點ws，並在/content處貼上。 將節點重新命名為ws2。 按一下 **[!UICONTROL 全部儲存]**. 在此節點的屬性中，變更值 `sling:resourceType` 到ws2。 按一下 **[!UICONTROL 全部儲存]**.

1. 從/libs複製資料夾ws並貼到/apps。 將資料夾重新命名為ws2。 按一下 **[!UICONTROL 全部儲存]**.
1. 在 `GET.jsp` 在 `/apps/ws2`，進行下列程式碼變更。 取代下列專案

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

   ，程式碼如下

   ```html
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. 在 `registry.js` 在 `/apps/ws2/js`，變更範本路徑以參照範本，位於 `/apps/ws2/js/runtime/templates`. 取代下列程式碼

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

   ，程式碼如下

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

1. 在 `userinfo.js` 在 `/apps/ws2/js/runtime/models` 和 `/apps/ws2/js/runtime/views`，變更字串 `/lc/content/ws` 至 `lc/content/ws2`.

1. 在 `/apps/ws2/js/runtime/services/service.js`，變更中的路徑 `getLocalizationData` 指向的函式 `/lc/apps/ws2/Locale.html`.

1. 若要參閱 `pdf.html` ，變更路徑 `pdf.html` 在 `/apps/ws2/js/runtime/views/forms/pdftaskform.js`.

1. 若要參閱 `pdf.html` 變更新工作區的路徑 `pdf.html` 和 `WsNextAdapter.swf` 在 `startprocess.html`， `taskdetails.html`、和 `processinstancehistory.html` 在 `/apps/ws2/js/runtime/templates`.

1. 複製 `/etc/map/ws` 資料夾並貼到 `/etc/map`. 將新資料夾重新命名為ws2。 按一下「儲存全部」。

1. 在屬性中 `ws2`，變更值 `sling:redirect` 至 `content/ws2`.

1. 變更值 `sling:match` 至 `^[^/\||]/[^/\||]/ws2$`.
