---
title: 啟動和停止WebLogic伺服器
seo-title: Starting and stopping WebLogic Server
description: 有幾個過程要求您啟動或停止要在其中部署表單模組的WebLogic ServerAEM實例。 本文檔介紹如何啟動和停止WebLogic Server。
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

有幾個過程要求您啟動或停止要在其中部署表單模組的WebLogic ServerAEM實例。 確保WebLogic Server已停止或正在運行，具體取決於您正在執行的任務。

<table>
 <thead>
  <tr>
   <th><p>活動</p></th>
   <th><p>所需的WebLogic狀態</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>建立WebLogic域</p></td>
   <td><p>已停止</p></td>
  </tr>
  <tr>
   <td><p>建立WebLogic受控伺服器</p></td>
   <td><p>正在執行</p></td>
  </tr>
  <tr>
   <td><p>增加伺服器線程數</p></td>
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
>如果在Red Hat® Enterprise Linux Advanced Server 4.0上運行WebLogic Server，請設定 `LD_ASSUME_KERNEL` 環境變數2.4.19使用 `export LD_ASSUME_KERNEL=2.4.19` 的子菜單。 然後，從設定此環境變數的同一外殼中運行WebLogic Server。

## 啟動WebLogic伺服器 {#start-weblogic-server}

1. 從命令提示符，轉到 *[appserver根]*/user_projects/domains/*[appserverdomain]*。
1. 輸入以下命令：

   * (Windows) `startWebLogic.cmd`
   * (Linux、UNIX)。/ `startWebLogic.sh`

## 停止WebLogic伺服器 {#stop-weblogic-server}

1. 通過鍵入以啟動WebLogic Server管理控制台 `https://[host name]:7001/console` 的子菜單。
1. 通過鍵入建立此WebLogic配置時使用的用戶名和密碼登錄，然後按一下登錄。
1. 在「變更中心」(Change Center)下，按一下「鎖定和編輯」(Lock &amp; Edit)。
1. 在「域結構」下，按一下「環境」>「伺服器」。
1. 按一下AdminServer ，然後在「AdminServer的設定」窗格上按一下「Control（控制）」頁籤。
1. 確保在「伺服器狀態」表中選擇了AdminServer，然後按一下「關閉」。
1. 選擇「工作完成時」以正常關閉伺服器，或選擇「立即強制關閉」以立即停止伺服器，而不完成日常任務。
1. 在「伺服器生命週期助手」窗格上，按一下「是」完成關閉。

WebLogic Server管理控制台不再可用，而您從中運行start命令的命令提示符也可用。

## 啟動WebLogic管理控制台 {#start-weblogic-administration-console}

1. 如果WebLogic管理伺服器尚未運行，請從命令提示符轉到 *[appserver根]\user_projects\domains\[域名]* ，並輸入以下命令：

   * (Windows) `startWebLogic.cmd`
   * (Linux、UNIX)。/ `startWebLogic.sh`

1. 通過鍵入WebLogic Server管理控制台 `https://[host name]:[port]/console` 的子菜單。 *[埠]* 是非安全監聽埠。 預設情況下，此埠值為7001。
1. 在登錄螢幕上，鍵入管理員用戶名和密碼，然後按一下登錄。

## 啟動節點管理器 {#start-node-manager}

1. 確保WebLogic伺服器正在運行。
1. 從新的命令提示符，轉到 *[appserver根]*/server/bin。
1. 輸入以下命令：

   * (Windows) `startNodeManager.cmd`
   * (Linux、UNIX) `./startNodeManager.sh`

## 停止節點管理器 {#stop-node-manager}

關閉WebLogic伺服器後，可以關閉從中調用「節點管理器」的命令提示符。

## 啟動WebLogic受控伺服器 {#start-a-weblogic-managed-server}

>[!NOTE]
>
>只有在建立WebLogic域和受控伺服器後，才能執行此任務。

1. 確保WebLogic伺服器和節點管理器正在運行。
1. 通過鍵入以啟動WebLogic Server管理控制台 `https://host name]:[port]/console` 的子菜單。
1. 在「域結構」下，按一下「環境」>「伺服器」。
1. 在右窗格中，按一下「Control（控制）」頁籤。
1. 選擇要啟動的受控伺服器。
1. 按一下要啟動的受控伺服器下方的「啟動」按鈕。

## 停止WebLogic受控伺服器 {#stop-a-weblogic-managed-server}

1. 通過鍵入以啟動WebLogic Server管理控制台 `https://`*[主機名]:[埠&#x200B;]*`/console` 的子菜單。
1. 在「域結構」下，按一下「環境」>「伺服器」。
1. 在右窗格中，按一下「Control（控制）」頁籤。
1. 選擇要停止的受控伺服器。
1. 按一下要停止的受控伺服器下面的「關閉」按鈕。
1. 選擇「工作完成時」以正常關閉伺服器，或選擇「立即強制關閉」以立即停止伺服器，而不完成日常任務。
1. 在「伺服器生命週期助手」窗格上，按一下「是」完成關閉。

