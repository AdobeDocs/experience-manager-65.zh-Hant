---
title: 命令列啟動和停止
description: 瞭解如何從命令列啟動和停止Adobe Experience Manager。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 21041b55-240c-487d-9d79-c54c877f4e1e
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# 命令列啟動和停止{#command-line-start-and-stop}

## 從命令列啟動Adobe Experience Manager {#starting-adobe-experience-manager-from-the-command-line}

此 `start` 指令碼位於 *此 &lt;cq-installation>/bin* 目錄。 同時提供UNIX®和Windows版本。 指令碼會啟動安裝在中的執行個體 *&lt;cq-installation>* 目錄。

這兩個版本支援可用於啟動和調整Adobe Experience Manager (AEM)執行個體的環境變數清單。

<table>
 <tbody>
  <tr>
   <td><strong>環境變數 </strong></td>
   <td><strong>說明 </strong></td>
  </tr>
  <tr>
   <td>CQ_PORT</td>
   <td>用於停止和狀態指令碼的TCP連線埠<br /> </td>
  </tr>
  <tr>
   <td>CQ_HOST</td>
   <td>主機名稱<br /> </td>
  </tr>
  <tr>
   <td>CQ_INTERFACE</td>
   <td>此伺服器應監聽的介面<br /> </td>
  </tr>
  <tr>
   <td>CQ_RUNMODE</td>
   <td>以逗號分隔的執行模式<br /> </td>
  </tr>
  <tr>
   <td>CQ_JARFILE</td>
   <td>Jarfile的名稱<br /> </td>
  </tr>
  <tr>
   <td>CQ_USE_JAAS</td>
   <td>使用JAAS （若為true）<br /> </td>
  </tr>
  <tr>
   <td>CQ_JAAS_CONFIG</td>
   <td>JAAS設定的路徑<br /> </td>
  </tr>
  <tr>
   <td>CQ_JVM_OPTS</td>
   <td>預設JVM選項<br /> </td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>某些執行模式（包括製作和發佈）必須在首次啟動AEM之前設定，且之後不能變更。 在設定用於生產環境的AEM執行個體之前，請參閱 [執行模式檔案](/help/sites-deploying/configure-runmodes.md) 以取得詳細資訊。

### Windows平台start.bat指令碼範例 {#windows-platform-start-bat-script-example}

```shell
SET CQ_PORT=1234 & ./start.bat
```

### UNIX®平台啟動指令碼範例 {#unix-platform-start-script-example}

```shell
CQ_PORT=1234 ./start
```

>[!NOTE]
>
>啟動指令碼會啟動安裝在以下位置的AEM快速入門： *此 &lt;cq-installation>/app* 資料夾。

## 停止Adobe Experience Manager {#stopping-adobe-experience-manager}

若要停止AEM，請執行下列任一項動作：

* 根據您使用的平台：

   * 如果您是從指令碼或命令列啟動AEM，請按下 **Ctrl+C** 關閉伺服器。
   * 如果您已在UNIX®上使用啟動指令碼，則必須使用停止指令碼來停止AEM。

* 如果您是透過按兩下jar檔案來啟動AEM，請按一下 **開啟** 啟動視窗上的按鈕(按鈕會變更為 **關閉**)關閉伺服器。

  ![chlimage_1-63](assets/chlimage_1-63.png)

## 從命令列停止Adobe Experience Manager {#stopping-adobe-experience-manager-from-the-command-line}

此 `stop` 指令碼位於 *此 &lt;cq-installation>/bin* 目錄。 同時提供UNIX®和Windows版本。 指令碼會停止在中安裝的執行中執行個體 *&lt;cq-installation>* 目錄。

### UNIX®平台停止指令碼範例 {#unix-platform-stop-script-example}

```shell
./stop
```

### Windows平台stop.bat指令碼範例 {#windows-platform-stop-bat-script-example}

```shell
./stop.bat
```

如果您只想預先設定存放庫（而不想重新定位），您只需：

* Extract `repository.xml` 至所需位置

* 更新 `repository.xml` 視需要

* 建立 `bootstrap.properties` 並定義 `repository.config`

同樣地，在開始實際安裝之前。
