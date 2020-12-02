---
title: 日誌檔案
seo-title: 日誌檔案
description: 應用程式伺服器記錄檔會記錄執行時或啟動錯誤等事件，這些記錄檔可使用任何文字編輯器來開啟。
seo-description: 應用程式伺服器記錄檔會記錄執行時或啟動錯誤等事件，這些記錄檔可使用任何文字編輯器來開啟。
uuid: 6ed9fdcd-ff02-4b35-893f-09261a6a557a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cf140483-470f-4bff-8870-304207508aab
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---


# 日誌檔案{#log-files}

將運行時或啟動錯誤等事件記錄到應用程式伺服器日誌檔案中。 如果您在部署至應用程式伺服器時遇到問題，可使用記錄檔來協助您找出問題。 您可以使用任何文字編輯器開啟記錄檔。

(JBoss)以下日誌檔案位於`[appserver root]/server/'server'/log`目錄中：

* boot.log
* server.log.*[yyyy-mm-dd]*
* server.log

(WebLogic)域日誌檔案位於`[appserverdomain]`目錄中，伺服器日誌檔案位於`[appserverdomain]/servers/[appserver name]/logs`目錄中：

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere)以下日誌檔案位於`[appserver root]/profiles/default/logs/[appserver name]`目錄中：

* SystemErr.log
* SystemOut.log
* StartServer.log

