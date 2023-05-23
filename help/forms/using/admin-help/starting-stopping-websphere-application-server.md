---
title: 啟動和停止WebSphere應用程式伺服器
seo-title: Starting and stopping WebSphere Application Server
description: 幾個過程要求您停止或啟動要在其中部署表單產品AEM的WebSphere實例。 本文檔介紹如何啟動和停止WebSphere應用程式伺服器。
seo-description: Several procedures require you to stop or start the instance of WebSphere where you want to deploy AEM forms products. This document describes how to start and stop the WebSphere Application Server.
uuid: e0373197-aa57-4087-933d-92a86840a11a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: bcd16691-67ab-4694-9e6b-c9d3e0c7bf0b
exl-id: 1a4e8f20-0644-4c96-9f52-f7a59521eac9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# 啟動和停止WebSphere應用程式伺服器 {#starting-and-stopping-websphere-application-server}

幾個過程要求您停止或啟動要在其中部署表單產品AEM的WebSphere實例。 如果不確定應用程式伺服器是否已啟動，可以首先查看WebSphere應用程式伺服器的狀態。

## 查看WebSphere應用程式伺服器的狀態 {#view-the-status-of-websphere-application-server}

1. 在命令提示符下，轉到 `[appserver root]/bin` 的子菜單。
1. 輸入以下命令，替換 *伺服器名* WebSphere應用程式伺服器的名稱：

   * (Windows) `serverStatus.bat`*伺服器名*
   * (Linux 、 UNIX)。/ `serverStatus.sh`*伺服器名*

## 啟動WebSphere應用程式伺服器 {#start-websphere-application-server}

1. 在命令提示符下，轉到 `[appserver root]/bin` 的子菜單。
1. 輸入以下命令，替換 *伺服器名* WebSphere應用程式伺服器的名稱：

   * (Windows) `startServer.bat`*伺服器名*
   * (Linux 、 UNIX)。/ `startServer.sh`*伺服器名*

## 停止WebSphere應用程式伺服器 {#stop-websphere-application-server}

1. 在命令提示符下，轉到 `[appserver root]/bin` 的子菜單。
1. 輸入以下命令，替換 *伺服器名* WebSphere應用程式伺服器的名稱：

   * (Windows) `stopServer.bat`*伺服器名*
   * (Linux 、 UNIX)。/ `stopServer.sh`*伺服器名*
