---
title: 在單一伺服器上托管兩個AEM Forms工作區例項
seo-title: 在單一伺服器上托管兩個AEM Forms工作區例項
description: LC管理員如何自訂HTML WS，在可透過不同URL存取的單一伺服器上主控兩個例項。
seo-description: LC管理員如何自訂HTML WS，在可透過不同URL存取的單一伺服器上主控兩個例項。
uuid: 0584f512-6b92-4418-b71c-93605cfa1927
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 1254a7c2-2c67-4661-803e-afd53e817916
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 在單一伺服器上托管兩個AEM Forms工作區例項 {#hosting-two-aem-forms-workspace-instances-on-one-server}

AEM Forms的預設安裝和設定僅允許伺服器上提供一個AEM Forms工作區。 不過，您可能需要在單一AEM Forms伺服器上托管兩個不同的AEM Forms工作區例項。 這兩個例項可透過不同的URL存取。

AEM Forms管理員可自訂工作區，以建立兩個不同的URL，並讓兩個工作區可在同一伺服器上使用。 在本自訂文章中，我們假設兩個工作區可在和 `https://[server]:[port]/lc/ws` 存取 `https://[server]:[port]:/lc/ws2`。

請依照下列步驟來設定AEM Forms工作區。

1. 在您的伺服器上安裝AEM Forms工作區的開發套件。 如需 [建立封裝的指示](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)，請參閱開發套件。
1. 以管理員身分登入CRXDE Lite，方法是存取 `https://[server]:[port]/lc/crx/de/index.jsp`。
1. 複製節點位於/content，貼上於/content。 將節點更名為ws2。 按一下「 **[!UICONTROL 全部儲存]**」。 在此節點的屬性中，將值 `sling:resourceType` 更改為ws2。 按一下「 **[!UICONTROL 全部儲存]**」。

1. 從/libs複製資料夾，並貼在/apps。 將資料夾更名為ws2。 按一下「 **[!UICONTROL 全部儲存]**」。
1. 在 `GET.jsp` 中， `/apps/ws2`請變更下列程式碼。 取代下列

   ```
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

   使用下列程式碼

   ```
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. 在 `registry.js` 中， `/apps/ws2/js`請更改模板的路徑以引用位於的模板 `/apps/ws2/js/runtime/templates`。 取代下列程式碼

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

   使用下列程式碼

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

1. 在 `userinfo.js` at `/apps/ws2/js/runtime/models` 和 `/apps/ws2/js/runtime/views`中，將字串 `/lc/content/ws` 更改為 `lc/content/ws2`。

1. 在中 `/apps/ws2/js/runtime/services/service.js`，將函式中的路 `getLocalizationData` 徑更改為指向 `/lc/apps/ws2/Locale.html`。

1. 要參考新工 `pdf.html` 作區，請更改中的路 `pdf.html` 徑 `/apps/ws2/js/runtime/views/forms/pdftaskform.js`。

1. 若要參 `pdf.html` 考新工作區，請變更中、中、中和中 `pdf.html` 的 `WsNextAdapter.swf` 路 `startprocess.html`徑， `taskdetails.html`以及 `processinstancehistory.html` at `/apps/ws2/js/runtime/templates`。

1. 複製 `/etc/map/ws` 資料夾並貼在 `/etc/map`。 將新資料夾更名為ws2。 按一下「全部儲存」。

1. 在的屬 `ws2`性中，將值 `sling:redirect` 更改為 `content/ws2`。

1. 將值 `sling:match` 更改為 `^[^/\||]/[^/\||]/ws2$`。

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
