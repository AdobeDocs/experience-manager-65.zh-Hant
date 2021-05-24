---
title: 命令行開始和停止
seo-title: 命令行開始和停止
description: 了解如何從命令列啟動和停止AEM。
seo-description: 了解如何從命令列啟動和停止AEM。
uuid: 585f071c-2286-4a2c-af07-404bf298cba8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9333ff84-f624-4cfa-a9e4-c5e3882171ff
exl-id: 21041b55-240c-487d-9d79-c54c877f4e1e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# 命令行開始和停止{#command-line-start-and-stop}

## 從命令行{#starting-adobe-experience-manager-from-the-command-line}啟動Adobe Experience Manager

`start`指令碼可在&#x200B;*&lt;cq-installation>/bin*&#x200B;目錄下使用。 提供Unix和Windows版本。 指令碼將啟動安裝在&#x200B;*&lt;cq-installation>*&#x200B;目錄中的實例。

這兩個版本支援可用來啟動及調整AEM例項的環境變數清單。

<table>
 <tbody>
  <tr>
   <td><strong>環境變數 </strong></td>
   <td><strong>說明 </strong></td>
  </tr>
  <tr>
   <td>CQ_PORT</td>
   <td>用於停止和狀態指令碼的TCP埠<br /> </td>
  </tr>
  <tr>
   <td>CQ_HOST</td>
   <td>主機名<br /> </td>
  </tr>
  <tr>
   <td>CQ_INTERFACE</td>
   <td>此伺服器應監聽的介面<br /> </td>
  </tr>
  <tr>
   <td>CQ_RUNMODE</td>
   <td>以逗號<br />分隔的運行模式 </td>
  </tr>
  <tr>
   <td>CQ_JARFILE</td>
   <td>jarfile<br />的名稱 </td>
  </tr>
  <tr>
   <td>CQ_USE_JAAS</td>
   <td>使用JAAS（若為true）<br /> </td>
  </tr>
  <tr>
   <td>CQ_JAAS_CONFIG</td>
   <td>JAAS配置的路徑<br /> </td>
  </tr>
  <tr>
   <td>CQ_JVM_OPTS</td>
   <td>預設JVM選項<br /> </td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>請注意，某些執行模式（包括製作和發佈）必須在首次啟動AEM之前設定，且之後無法變更。 在設定應用於生產環境的AEM執行個體之前，請參閱[執行模式檔案](/help/sites-deploying/configure-runmodes.md)以取得詳細資訊。

### Windows平台start.bat指令碼示例{#windows-platform-start-bat-script-example}

```shell
SET CQ_PORT=1234 & ./start.bat
```

### Unix平台啟動指令碼示例{#unix-platform-start-script-example}

```shell
CQ_PORT=1234 ./start
```

>[!NOTE]
>
>啟動指令碼會啟動安裝在&#x200B;*&lt;cq-installation>/app*&#x200B;資料夾下的AEM Quickstart。

## 停止Adobe Experience Manager {#stopping-adobe-experience-manager}

若要停止AEM，請執行下列其中一項操作：

* 視您使用的平台而定：

   * 如果從指令碼或命令行啟動AEM，請按&#x200B;**Ctrl+C**&#x200B;以關閉伺服器。
   * 如果在UNIX上使用了啟動指令碼，則必須使用停止指令碼來停止AEM。

* 如果您通過按兩下jar檔案來啟動AEM，請按一下啟動窗口上的&#x200B;**On**&#x200B;按鈕（該按鈕隨後更改為&#x200B;**Off**）以關閉伺服器。

   ![chlimage_1-63](assets/chlimage_1-63.png)

## 從命令行{#stopping-adobe-experience-manager-from-the-command-line}停止Adobe Experience Manager

`stop`指令碼可在&#x200B;*&lt;cq-installation>/bin*&#x200B;目錄下使用。 提供Unix和Windows版本。 指令碼會停止&#x200B;*&lt;cq-installation>*&#x200B;目錄中安裝的執行個體。

### Unix平台停止指令碼示例{#unix-platform-stop-script-example}

```shell
./stop
```

### Windows平台stop.bat指令碼示例{#windows-platform-stop-bat-script-example}

```shell
./stop.bat
```

如果只想預配置儲存庫（而不重新調整儲存庫的位置），則只需：

* 將`repository.xml`提取到所需位置

* 視需要更新`repository.xml`

* 建立`bootstrap.properties`並定義`repository.config`

同樣，在開始實際安裝之前。
