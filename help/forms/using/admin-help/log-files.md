---
title: 記錄檔
seo-title: 記錄檔
description: 運行時或啟動錯誤等事件將記錄到應用程式伺服器日誌檔案中，可以使用任何文本編輯器開啟這些日誌檔案。
seo-description: 運行時或啟動錯誤等事件將記錄到應用程式伺服器日誌檔案中，可以使用任何文本編輯器開啟這些日誌檔案。
uuid: 6ed9fdcd-ff02-4b35-893f-09261a6a557a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cf140483-470f-4bff-8870-304207508aab
exl-id: 23a65be4-3277-4c73-9189-a9b4d7be73cd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# 日誌檔案{#log-files}

運行時或啟動錯誤等事件將記錄到應用程式伺服器日誌檔案中。 如果部署到應用程式伺服器時遇到任何問題，可以使用日誌檔案幫助您找到問題。 您可以使用任何文字編輯器開啟記錄檔。

(JBoss)以下日誌檔案位於`[appserver root]/server/'server'/log`目錄中：

* boot.log
* server.log.*[yyyy-mm-dd]*
* server.log

(WebLogic)域日誌檔案位於`[appserverdomain]`目錄中，而伺服器日誌檔案位於`[appserverdomain]/servers/[appserver name]/logs`目錄中：

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere)以下日誌檔案位於`[appserver root]/profiles/default/logs/[appserver name]`目錄中：

* SystemErr.log
* SystemOut.log
* StartServer.log
