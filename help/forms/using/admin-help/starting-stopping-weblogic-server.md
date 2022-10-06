---
title: 啟動和停止WebLogic伺服器
seo-title: Starting and stopping WebLogic Server
description: 有幾個過程要求您啟動或停止要部署AEM表單模組的WebLogic Server實例。 本文檔介紹如何啟動和停止WebLogic伺服器。
seo-description: Several procedures require you to start or stop the instance of WebLogic Server where you want to deploy AEM forms modules. This document describes how to start and stop the WebLogic Server.
uuid: 957787fe-4cea-4ecd-b49a-c33023c5c309
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c908d064-6596-473a-b218-22a2496c83f7
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 1%

---


# 啟動和停止WebLogic伺服器 {#starting-and-stopping-weblogic-server}

有幾個過程要求您啟動或停止要部署AEM表單模組的WebLogic Server實例。 根據您執行的任務，確保WebLogic Server停止或運行。

<table>
 <thead>
  <tr>
   <th><p>活動</p></th>
   <th><p>所需的WebLogic狀態</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>建立WebLogic網域</p></td>
   <td><p>已停止</p></td>
  </tr>
  <tr>
   <td><p>建立WebLogic托管伺服器</p></td>
   <td><p>正在執行</p></td>
  </tr>
  <tr>
   <td><p>增加伺服器線程計數</p></td>
   <td><p>正在執行</p></td>
  </tr>
  <tr>
   <td><p>部署AEM表單產品</p></td>
   <td><p>正在執行</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>如果在Red Hat® Enterprise Linux Advanced Server 4.0上運行WebLogic Server，請設定 `LD_ASSUME_KERNEL` 環境變數設為2.4.19(使用 `export LD_ASSUME_KERNEL=2.4.19` 命令。 然後，從設定此環境變數的同一個殼層運行WebLogic Server。

## 啟動WebLogic Server {#start-weblogic-server}

1. 從命令提示字元，前往 *[appserver根]*/user_projects/domains/*[appserverdomain]*.
1. 輸入以下命令：

   * (Windows) `startWebLogic.cmd`
   * (Linux、UNIX)。/ `startWebLogic.sh`

## 停止WebLogic伺服器 {#stop-weblogic-server}

1. 輸入 `https://[host name]:7001/console` 在網頁瀏覽器的URL行中。
1. 通過鍵入建立此WebLogic配置時使用的用戶名和密碼登錄，然後按一下「登錄」。
1. 在「更改中心」(Change Center)下，按一下「鎖定和編輯」(Lock &amp; Edit)。
1. 在「域結構」下，按一下「環境」>「伺服器」。
1. 按一下「AdminServer」，然後在「AdminServer的設定」窗格上按一下「控制」頁簽。
1. 確保在「伺服器狀態」表中選擇了AdminServer ，然後按一下「關閉」。
1. 選擇「工作完成時」以正常關閉伺服器，或選擇「立即強制關閉」以立即停止伺服器，而不完成持續的任務。
1. 在「伺服器生命週期助理」窗格上，按一下「是」以完成關閉。

不再提供WebLogic Server管理控制台，並且您從運行start命令的命令提示符可用。

## 啟動WebLogic管理控制台 {#start-weblogic-administration-console}

1. 如果WebLogic管理伺服器尚未運行，請從命令提示符轉到 *[appserver根]\user_projects\domains\[domainname]* 目錄，然後輸入以下命令：

   * (Windows) `startWebLogic.cmd`
   * (Linux、UNIX)。/ `startWebLogic.sh`

1. 輸入 `https://[host name]:[port]/console` 在網頁瀏覽器的URL行中， *[埠]* 是不安全的監聽埠。 預設情況下，此埠值為7001。
1. 在登錄螢幕上，鍵入管理員用戶名和密碼，然後按一下登錄。

## 啟動節點管理器 {#start-node-manager}

1. 確保WebLogic Server正在運行。
1. 從新的命令提示符，轉到 *[appserver根]*/server/bin。
1. 輸入以下命令：

   * (Windows) `startNodeManager.cmd`
   * (Linux、UNIX) `./startNodeManager.sh`

## 停止節點管理器 {#stop-node-manager}

關閉WebLogic伺服器後，可以關閉命令提示符，從中調用Node Manager。

## 啟動WebLogic托管伺服器 {#start-a-weblogic-managed-server}

>[!NOTE]
>
>只有在建立WebLogic域和托管伺服器後，才能執行此任務。

1. 請確定WebLogic伺服器和節點管理器正在運行。
1. 輸入 `https://host name]:[port]/console` 在網頁瀏覽器的URL行中。
1. 在「域結構」下，按一下「環境」>「伺服器」。
1. 在右窗格中，按一下「控制」頁簽。
1. 選擇要啟動的受控伺服器。
1. 按一下要啟動的受控伺服器下方的「啟動」按鈕。

## 停止WebLogic托管伺服器 {#stop-a-weblogic-managed-server}

1. 輸入 `https://`*[主機名稱]:[埠&#x200B;]*`/console` 在網頁瀏覽器的URL行中。
1. 在「域結構」下，按一下「環境」>「伺服器」。
1. 在右窗格中，按一下「控制」頁簽。
1. 選擇要停止的受控伺服器。
1. 按一下要停止的受控伺服器下方的「關閉」按鈕。
1. 選擇「工作完成時」以正常關閉伺服器，或選擇「立即強制關閉」以立即停止伺服器，而不完成持續的任務。
1. 在「伺服器生命週期助理」窗格上，按一下「是」以完成關閉。

