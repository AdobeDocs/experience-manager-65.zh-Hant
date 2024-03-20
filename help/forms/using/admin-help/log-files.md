---
title: 記錄檔
description: 執行階段或啟動錯誤等事件會記錄到應用程式伺服器記錄檔中，這些記錄檔可使用任何文字編輯器開啟。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 23a65be4-3277-4c73-9189-a9b4d7be73cd
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# 記錄檔 {#log-files}

執行階段或啟動錯誤等事件會記錄到應用程式伺服器記錄檔中。 如果部署到應用程式伺服器時發生任何問題，您可以使用記錄檔來協助您尋找問題。 您可以使用任何文字編輯器開啟記錄檔。

(JBoss)以下記錄檔位於 `[appserver root]/server/'server'/log` 目錄：

* boot.log
* server.log.*[yyyy-mm-dd]*
* server.log

(WebLogic)網域記錄檔位於 `[appserverdomain]` 目錄和伺服器記錄檔位於 `[appserverdomain]/servers/[appserver name]/logs` 目錄：

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere)下列記錄檔位於 `[appserver root]/profiles/default/logs/[appserver name]` 目錄：

* SystemErr.log
* SystemOut.log
* StartServer.log
