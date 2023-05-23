---
title: 在一台伺服器上托管兩個AEM Forms工作區實例
seo-title: Hosting two AEM Forms workspace instances on one server
description: LC管理員如何自定義HTMLWS，以在可通過不同URL訪問的單個伺服器上承載兩個實例。
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

# 在一台伺服器上托管兩個AEM Forms工作區實例 {#hosting-two-aem-forms-workspace-instances-on-one-server}

AEM Forms的預設安裝和設定只允許在伺服器上使用一個AEM Forms工作區。 但是，您可能需要在單個AEM Forms伺服器上托管兩個不同的AEM Forms工作區實例。 兩個實例可通過不同的URL訪問。

AEM Forms管理員自定義工作區，以建立兩個不同的URL，並使兩個工作區在同一伺服器上可用。 在本定制文章中，我們假定兩個工作區可以訪問 `https://'[server]:[port]'/lc/ws` 和 `https://'[server]:[port]':/lc/ws2`。

按照以下步驟配置AEM Forms工作區。

1. 在伺服器上安裝AEM Forms工作區的dev包。 請參閱 [dev程式包](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)，以獲取建立它的說明。
1. 以管理員身份登錄CRXDE Lite，訪問 `https://'[server]:[port]'/lc/crx/de/index.jsp`。
1. 複製節點位於/content ，貼上於/content。 將節點更名為ws2。 按一下 **[!UICONTROL 全部保存]**。 在此節點的屬性中，更改 `sling:resourceType` 到ws2。 按一下 **[!UICONTROL 全部保存]**。

1. 從/libs複製資料夾，然後貼上到/apps。 將資料夾更名為ws2。 按一下 **[!UICONTROL 全部保存]**。
1. 在 `GET.jsp` 在 `/apps/ws2`，進行以下代碼更改。 替換以下

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

   具有以下代碼

   ```html
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. 在 `registry.js` 在 `/apps/ws2/js`，更改模板路徑以參考模板 `/apps/ws2/js/runtime/templates`。 替換以下代碼

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

   具有以下代碼

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

1. 在 `userinfo.js` 在 `/apps/ws2/js/runtime/models` 和 `/apps/ws2/js/runtime/views`，更改字串 `/lc/content/ws` 至 `lc/content/ws2`。

1. 在 `/apps/ws2/js/runtime/services/service.js`，在中更改路徑 `getLocalizationData` 函式指向 `/lc/apps/ws2/Locale.html`。

1. 請參閱 `pdf.html` 中，更改 `pdf.html` 在 `/apps/ws2/js/runtime/views/forms/pdftaskform.js`。

1. 請參閱 `pdf.html` 中，更改 `pdf.html` 和 `WsNextAdapter.swf` 在 `startprocess.html`。 `taskdetails.html`, `processinstancehistory.html` 在 `/apps/ws2/js/runtime/templates`。

1. 複製 `/etc/map/ws` 資料夾和貼上位置 `/etc/map`。 將新資料夾更名為ws2。 按一下「全部保存」。

1. 在屬性中 `ws2`，更改值 `sling:redirect` 至 `content/ws2`。

1. 更改值 `sling:match` 至 `^[^/\||]/[^/\||]/ws2$`。
