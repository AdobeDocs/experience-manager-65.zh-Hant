---
title: 啟動和停止WebSphere Application Server
description: 有數個程式需要您停止或啟動要部署AEM表單產品的WebSphere執行個體。 本檔案說明如何啟動和停止WebSphere Application Server。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1a4e8f20-0644-4c96-9f52-f7a59521eac9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%
---
# 啟動和停止WebSphere Application Server {#starting-and-stopping-websphere-application-server}

有數個程式需要您停止或啟動要部署AEM表單產品的WebSphere執行個體。 如果您不確定應用程式伺服器是否已啟動，可以先檢視WebSphere Application Server的狀態。

## 檢視WebSphere應用程式伺服器的狀態 {#view-the-status-of-websphere-application-server}

1. 從命令提示字元移至`[appserver root]/bin`目錄。
1. 輸入以下命令，將&#x200B;*server_name*&#x200B;取代為WebSphere Application Server的名稱：

   * (Windows) `serverStatus.bat`*伺服器名稱*
   * (Linux， UNIX) ./ `serverStatus.sh`*伺服器名稱*

## 啟動WebSphere Application Server {#start-websphere-application-server}

1. 從命令提示字元移至`[appserver root]/bin`目錄。
1. 輸入以下命令，將&#x200B;*server_name*&#x200B;取代為WebSphere Application Server的名稱：

   * (Windows) `startServer.bat`*伺服器名稱*
   * (Linux， UNIX) ./ `startServer.sh`*伺服器名稱*

## 停止WebSphere Application Server {#stop-websphere-application-server}

1. 從命令提示字元移至`[appserver root]/bin`目錄。
1. 輸入以下命令，將&#x200B;*server_name*&#x200B;取代為WebSphere Application Server的名稱：

   * (Windows) `stopServer.bat`*伺服器名稱*
   * (Linux， UNIX) ./ `stopServer.sh`*伺服器名稱*
