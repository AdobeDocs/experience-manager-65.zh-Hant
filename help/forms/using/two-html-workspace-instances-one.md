---
title: 將兩個AEM Forms工作區執行個體托管在一部伺服器上
seo-title: 將兩個AEM Forms工作區執行個體托管在一部伺服器上
description: LC管理員如何自訂HTML WS，以在可透過不同URL存取的單一伺服器上托管兩個執行個體。
seo-description: LC管理員如何自訂HTML WS，以在可透過不同URL存取的單一伺服器上托管兩個執行個體。
uuid: 0584f512-6b92-4418-b71c-93605cfa1927
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 1254a7c2-2c67-4661-803e-afd53e817916
exl-id: 32a546fc-e33f-46f9-ac3b-45eca0e12239
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# 在一個伺服器{#hosting-two-aem-forms-workspace-instances-on-one-server}上托管兩個AEM Forms工作區例項

AEM Forms的預設安裝與設定只允許在伺服器上使用一個AEM Forms工作區。 不過，您可能需要在單一AEM Forms伺服器上托管兩個不同的AEM Forms工作區例項。 這兩個例項可由不同URL存取。

AEM Forms管理員可自訂工作區，以建立兩個不同的URL，並讓兩個工作區可在同一伺服器上使用。 在本自訂文章中，我們假設兩個工作區可在`https://'[server]:[port]'/lc/ws`和`https://'[server]:[port]':/lc/ws2`存取。

請依照下列步驟來設定AEM Forms工作區。

1. 在伺服器上安裝AEM Forms工作區的開發套件。 有關建立包的說明，請參閱[開發包](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)。
1. 通過訪問`https://'[server]:[port]'/lc/crx/de/index.jsp`以管理員身份登錄CRXDE Lite。
1. 複製節點在/content，然後貼到/content。 將節點更名為ws2。 按一下「**[!UICONTROL 全部保存]**」。 在此節點的屬性中，將`sling:resourceType`的值更改為ws2。 按一下「**[!UICONTROL 全部保存]**」。

1. 從/libs複製資料夾並貼到/apps。 將資料夾更名為ws2。 按一下「**[!UICONTROL 全部保存]**」。
1. 在`GET.jsp`的`/apps/ws2`中，變更下列程式碼。 取代下列項目

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

1. 在`/apps/ws2/js`的`registry.js`中，將範本路徑變更為在`/apps/ws2/js/runtime/templates`參考範本。 取代下列程式碼

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

1. 在`/apps/ws2/js/runtime/models`和`/apps/ws2/js/runtime/views`的`userinfo.js`中，將字串`/lc/content/ws`更改為`lc/content/ws2`。

1. 在`/apps/ws2/js/runtime/services/service.js`中，將`getLocalizationData`函式中的路徑更改為指向`/lc/apps/ws2/Locale.html`。

1. 若要參照新工作區的`pdf.html`，請變更`/apps/ws2/js/runtime/views/forms/pdftaskform.js`中的`pdf.html`路徑。

1. 若要參照新工作區的`pdf.html`，請在`startprocess.html`、`taskdetails.html`和`processinstancehistory.html`的`/apps/ws2/js/runtime/templates`中變更`pdf.html`和`WsNextAdapter.swf`的路徑。

1. 複製`/etc/map/ws`資料夾並貼到`/etc/map`。 將新資料夾更名為ws2。 按一下「全部儲存」 。

1. 在`ws2`的屬性中，將`sling:redirect`的值變更為`content/ws2`。

1. 將`sling:match`的值變更為`^[^/\||]/[^/\||]/ws2$`。
