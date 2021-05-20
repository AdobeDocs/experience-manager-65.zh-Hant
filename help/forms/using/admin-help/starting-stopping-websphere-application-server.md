---
title: 啟動和停止WebSphere應用程式伺服器
seo-title: 啟動和停止WebSphere應用程式伺服器
description: 若要部署AEM表單產品，有數個程式需要您停止或啟動WebSphere執行個體。 本文檔介紹如何啟動和停止WebSphere應用程式伺服器。
seo-description: 若要部署AEM表單產品，有數個程式需要您停止或啟動WebSphere執行個體。 本文檔介紹如何啟動和停止WebSphere應用程式伺服器。
uuid: e0373197-aa57-4087-933d-92a86840a11a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: bcd16691-67ab-4694-9e6b-c9d3e0c7bf0b
exl-id: 1a4e8f20-0644-4c96-9f52-f7a59521eac9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# 啟動和停止WebSphere應用程式伺服器{#starting-and-stopping-websphere-application-server}

若要部署AEM表單產品，有數個程式需要您停止或啟動WebSphere執行個體。 如果您不確定應用程式伺服器是否已啟動，則可以首先查看WebSphere應用程式伺服器的狀態。

## 查看WebSphere應用程式伺服器{#view-the-status-of-websphere-application-server}的狀態

1. 從命令提示字元，轉至`[appserver root]/bin`目錄。
1. 輸入以下命令，將&#x200B;*server_name*&#x200B;替換為WebSphere應用程式伺服器的名稱：

   * (Windows)`serverStatus.bat`*server_name*
   * (Linux、UNIX)。/ `serverStatus.sh`*server name*

## 啟動WebSphere應用程式伺服器{#start-websphere-application-server}

1. 從命令提示字元，轉至`[appserver root]/bin`目錄。
1. 輸入以下命令，將&#x200B;*server_name*&#x200B;替換為WebSphere應用程式伺服器的名稱：

   * (Windows)`startServer.bat`*server_name*
   * (Linux、UNIX)。/ `startServer.sh`*server name*

## 停止WebSphere應用程式伺服器{#stop-websphere-application-server}

1. 從命令提示字元，轉至`[appserver root]/bin`目錄。
1. 輸入以下命令，將&#x200B;*server_name*&#x200B;替換為WebSphere應用程式伺服器的名稱：

   * (Windows)`stopServer.bat`*server_name*
   * (Linux、UNIX)。/ `stopServer.sh`*server name*
