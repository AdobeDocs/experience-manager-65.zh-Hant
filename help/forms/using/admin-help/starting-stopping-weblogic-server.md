---
title: 啟動和停止WebLogic伺服器
seo-title: 啟動和停止WebLogic伺服器
description: 若干程式會要求您啟動或停止要部署AEM表單模組的WebLogic Server例項。 本檔案說明如何啟動和停止WebLogic Server。
seo-description: 若干程式會要求您啟動或停止要部署AEM表單模組的WebLogic Server例項。 本檔案說明如何啟動和停止WebLogic Server。
uuid: 957787fe-4cea-4ecd-b49a-c33023c5c309
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c908d064-6596-473a-b218-22a2496c83f7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 啟動和停止WebLogic伺服器 {#starting-and-stopping-weblogic-server}

若干程式會要求您啟動或停止要部署AEM表單模組的WebLogic Server例項。 根據您執行的任務，確定WebLogic server已停止或正在運行。

<table>
 <thead>
  <tr>
   <th><p>活動</p></th>
   <th><p>必要的WebLogic狀態</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>建立WebLogic網域</p></td>
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
>如果您在Red Hat® Enterprise Linux Advanced Server 4.0上運行WebLogic Server，請使用命令將 `LD_ASSUME_KERNEL` 環境變數設定為2.4.19 `export LD_ASSUME_KERNEL=2.4.19` 。 然後，從您設定此環境變數的相同殼層執行WebLogic Server。

## 啟動WebLogic Server {#start-weblogic-server}

1. 在命令提示符下，轉 *[至appserver root]*/user_projects/domains/*[appserverdomain]*。
1. 輸入以下命令：

   * (Windows) `startWebLogic.cmd`
   * (Linux、UNIX)。/ `startWebLogic.sh`

## 停止WebLogic伺服器 {#stop-weblogic-server}

1. 在Web瀏覽器的URL行中鍵入， `https://[host name]:7001/console` 以啟動WebLogic server管理控制台。
1. 輸入建立此WebLogic設定時使用的使用者名稱和密碼以登入，然後按一下登入。
1. 在「變更中心」下，按一下「鎖定與編輯」。
1. 在「域結構」下，按一下「環境」>「伺服器」。
1. 按一下「AdminServer」，然後在「AdminServer的設定」窗格上，按一下「控制」標籤。
1. 確保在「伺服器狀態」表中選擇了AdminServer ，然後按一下「關閉」。
1. 選擇「工作完成時」以正常關閉伺服器，或選擇「立即強制關閉」以立即停止伺服器，而不完成正在進行的任務。
1. 在Server Life Cycle Assistant窗格中，按一下是完成關閉。

WebLogic server管理控制台不再可用，而您從中運行start命令的命令提示符也可用。

## 啟動WebLogic管理控制台 {#start-weblogic-administration-console}

1. 如果WebLogic Admin server尚未運行，請從命令提示符進入 *[appserver root]\user_projects\domains\[domainname]*目錄，然後輸入以下命令：

   * (Windows) `startWebLogic.cmd`
   * (Linux、UNIX)。/ `startWebLogic.sh`

1. 在Web瀏覽器的URL行中輸入 `https://*[host name]:`[Port] ( `/console`*[]* Port是不安全的監聽埠)，以存取WebLogic server管理控制台。 預設情況下，此埠值為7001。
1. 在登入畫面上，輸入您的管理員使用者名稱和密碼，然後按一下登入。

## 啟動節點管理器 {#start-node-manager}

1. 確保WebLogic server正在運行。
1. 從新的命令提示符中，轉 *[到appserver root]*/server/bin。
1. 輸入以下命令：

   * (Windows) `startNodeManager.cmd`
   * (Linux、UNIX) `./startNodeManager.sh`

## 停止節點管理器 {#stop-node-manager}

關閉WebLogic伺服器後，可以關閉從中調用節點管理器的命令提示符。

## 啟動WebLogic受控伺服器 {#start-a-weblogic-managed-server}

>[!NOTE]
>
>只有在建立WebLogic域和受控伺服器後，才能執行此任務。

1. 確保WebLogic伺服器和節點管理器正在運行。
1. 在Web瀏覽器的URL行中輸 `https://`*[入主機名]:[port ]*`/console`，啟動WebLogic Server管理控制台。
1. 在「域結構」下，按一下「環境」>「伺服器」。
1. 在右窗格中，按一下「Control（控制）」頁籤。
1. 選擇要啟動的受控伺服器。
1. 按一下要啟動的受控伺服器下面的「啟動」按鈕。

## 停止WebLogic受控伺服器 {#stop-a-weblogic-managed-server}

1. 在Web瀏覽器的URL行中輸 `https://`*[入主機名]:[port ]*`/console`，啟動WebLogic Server管理控制台。
1. 在「域結構」下，按一下「環境」>「伺服器」。
1. 在右窗格中，按一下「Control（控制）」頁籤。
1. 選擇要停止的受控伺服器。
1. 按一下要停止的受控伺服器下面的「關閉」按鈕。
1. 選擇「工作完成時」以正常關閉伺服器，或選擇「立即強制關閉」以立即停止伺服器，而不完成正在進行的任務。
1. 在Server Life Cycle Assistant窗格中，按一下是完成關閉。

