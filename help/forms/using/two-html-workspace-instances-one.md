---
title: 在單一伺服器上主控兩個AEM Forms工作區執行個體
description: LC管理員如何自訂HTMLWS，以便在可透過不同URL存取的單一伺服器上託管兩個執行個體。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 32a546fc-e33f-46f9-ac3b-45eca0e12239
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---

# 在單一伺服器上主控兩個AEM Forms工作區執行個體 {#hosting-two-aem-forms-workspace-instances-on-one-server}

AEM Forms的預設安裝與設定只允許伺服器上有一個AEM Forms工作區。 不過，您可能需要在單一AEM Forms伺服器上託管兩個不同的AEM Forms工作區例項。 這兩個執行個體可透過不同的URL存取。

AEM Forms管理員可自訂工作區，以建立兩個不同的URL，並讓兩個工作區可在同一部伺服器上使用。 在這篇自訂文章中，您可以假設兩個工作區可在`https://'[server]:[port]'/lc/ws`和`https://'[server]:[port]':/lc/ws2`存取。

請依照下列步驟設定AEM Forms工作區。

1. 在伺服器上安裝AEM Forms工作區的開發套件。 請參閱[開發封裝](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)以取得建立它的指示。
1. 透過存取`https://'[server]:[port]'/lc/crx/de/index.jsp`，以系統管理員身分登入CRXDE Lite。
1. 在/content處複製節點ws，並在/content處貼上。 將節點重新命名為ws2。 按一下&#x200B;**[!UICONTROL 全部儲存]**。 在此節點的屬性中，將`sling:resourceType`的值變更為ws2。 按一下&#x200B;**[!UICONTROL 全部儲存]**。

1. 從/libs複製資料夾ws並貼到/apps。 將資料夾重新命名為ws2。 按一下&#x200B;**[!UICONTROL 全部儲存]**。
1. 在`GET.jsp`的`/apps/ws2`中，進行下列程式碼變更。 取代下列專案

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

1. 在`registry.js`的`/apps/ws2/js`中，變更範本路徑以參考位於`/apps/ws2/js/runtime/templates`的範本。 取代下列程式碼

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

1. 在`userinfo.js`的`/apps/ws2/js/runtime/models`和`/apps/ws2/js/runtime/views`中，將字串`/lc/content/ws`變更為`lc/content/ws2`。

1. 在`/apps/ws2/js/runtime/services/service.js`中，將`getLocalizationData`函式中的路徑變更為指向`/lc/apps/ws2/Locale.html`。

1. 若要參考新Workspace的`pdf.html`，請在`/apps/ws2/js/runtime/views/forms/pdftaskform.js`中變更`pdf.html`的路徑。

1. 若要參考新Workspace的`pdf.html`，請在`/apps/ws2/js/runtime/templates`變更`startprocess.html`、`taskdetails.html`和`processinstancehistory.html`中的`pdf.html`和`WsNextAdapter.swf`路徑。

1. 複製`/etc/map/ws`資料夾並貼到`/etc/map`。 將新資料夾重新命名為ws2。 按一下「儲存全部」。

1. 在`ws2`的屬性中，將`sling:redirect`的值變更為`content/ws2`。

1. 將`sling:match`的值變更為`^[^/\||]/[^/\||]/ws2$`。
