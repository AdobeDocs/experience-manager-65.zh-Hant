---
title: 啟動和停止WebSphere Application Server
seo-title: 啟動和停止WebSphere Application Server
description: 若干程式會要求您停止或啟動要部署AEM表單產品的WebSphere執行個體。 本文檔介紹如何啟動和停止WebSphere Application Server。
seo-description: 若干程式會要求您停止或啟動要部署AEM表單產品的WebSphere執行個體。 本文檔介紹如何啟動和停止WebSphere Application Server。
uuid: e0373197-aa57-4087-933d-92a86840a11a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: bcd16691-67ab-4694-9e6b-c9d3e0c7bf0b
translation-type: tm+mt
source-git-commit: 67ea825215d1ca7cc2e350ed1c128c3146de45ec

---


# 啟動和停止WebSphere Application Server {#starting-and-stopping-websphere-application-server}

若干程式會要求您停止或啟動要部署AEM表單產品的WebSphere執行個體。 如果您不確定應用程式伺服器是否已啟動，您可以先檢視WebSphere應用程式伺服器的狀態。

## 查看WebSphere Application server的狀態 {#view-the-status-of-websphere-application-server}

1. 在命令提示符下，轉到目 `[appserver root]/bin` 錄。
1. 輸入以下命令， *用WebSphere應用程式伺服器的名稱替換server_name* :

   * (Windows) `serverStatus.bat`*server_name *
   * (Linux、UNIX)。/ `serverStatus.sh`*server_name *

## 啟動WebSphere Application Server {#start-websphere-application-server}

1. 在命令提示符下，轉到目 `[appserver root]/bin` 錄。
1. 輸入以下命令， *用WebSphere應用程式伺服器的名稱替換server_name* :

   * (Windows) `startServer.bat`*server_name *
   * (Linux、UNIX)。/ `startServer.sh`*server_name *

## 停止WebSphere Application Server {#stop-websphere-application-server}

1. 在命令提示符下，轉到目 `[appserver root]/bin` 錄。
1. 輸入以下命令， *用WebSphere應用程式伺服器的名稱替換server_name* :

   * (Windows) `stopServer.bat`*server_name *
   * (Linux、UNIX)。/ `stopServer.sh`*server_name *

