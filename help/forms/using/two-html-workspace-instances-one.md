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
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---


# 在單一伺服器上托管兩個AEM Forms工作區例項{#hosting-two-aem-forms-workspace-instances-on-one-server}

AEM Forms的預設安裝和設定僅允許伺服器上提供一個AEM Forms工作區。 不過，您可能需要在單一AEM Forms伺服器上托管兩個不同的AEM Forms工作區例項。 這兩個例項可透過不同的URL存取。

AEM Forms管理員可自訂工作區，以建立兩個不同的URL，並讓兩個工作區可在同一伺服器上使用。 在此自訂文章中，我們假設兩個工作區可在`https://'[server]:[port]'/lc/ws`和`https://'[server]:[port]':/lc/ws2`存取。

請依照下列步驟來設定AEM Forms工作區。

1. 在您的伺服器上安裝AEM Forms工作區的開發套件。 有關建立軟體包的說明，請參見[dev package](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)。
1. 以管理員身份登錄到CRXDE Lite，方法是訪問`https://'[server]:[port]'/lc/crx/de/index.jsp`。
1. 複製節點位於/content，貼上於/content。 將節點更名為ws2。 按一下&#x200B;**[!UICONTROL 保存所有]**。 在此節點的屬性中，將`sling:resourceType`的值更改為ws2。 按一下&#x200B;**[!UICONTROL 保存所有]**。

1. 從/libs複製資料夾，並貼在/apps。 將資料夾更名為ws2。 按一下&#x200B;**[!UICONTROL 保存所有]**。
1. 在`GET.jsp`的`/apps/ws2`中，請變更下列程式碼。 取代下列

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

   使用下列程式碼

   ```html
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. 在`/apps/ws2/js`的`registry.js`中，變更範本路徑以參考`/apps/ws2/js/runtime/templates`的範本。 取代下列程式碼

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

1. 在`/apps/ws2/js/runtime/models`和`/apps/ws2/js/runtime/views`的`userinfo.js`中，將字串`/lc/content/ws`變更為`lc/content/ws2`。

1. 在`/apps/ws2/js/runtime/services/service.js`中，將`getLocalizationData`函式中的路徑更改為指向`/lc/apps/ws2/Locale.html`。

1. 要參考新工作區的`pdf.html`，請更改`/apps/ws2/js/runtime/views/forms/pdftaskform.js`中`pdf.html`的路徑。

1. 若要參考新工作區的`pdf.html`，請在`startprocess.html`、`taskdetails.html`和`processinstancehistory.html`中變更`pdf.html`和`WsNextAdapter.swf`的路徑，位於`/apps/ws2/js/runtime/templates`。

1. 複製`/etc/map/ws`資料夾並貼至`/etc/map`。 將新資料夾更名為ws2。 按一下「全部儲存」。

1. 在`ws2`的屬性中，將`sling:redirect`的值變更為`content/ws2`。

1. 將`sling:match`的值變更為`^[^/\||]/[^/\||]/ws2$`。
