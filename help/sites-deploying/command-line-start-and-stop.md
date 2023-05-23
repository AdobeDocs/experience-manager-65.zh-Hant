---
title: 命令行啟動和停止
seo-title: Command Line Start and Stop
description: 瞭解如何從命令行啟AEM動和停止。
seo-description: Learn how to start and stop AEM from the command line.
uuid: 585f071c-2286-4a2c-af07-404bf298cba8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9333ff84-f624-4cfa-a9e4-c5e3882171ff
exl-id: 21041b55-240c-487d-9d79-c54c877f4e1e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# 命令行啟動和停止{#command-line-start-and-stop}

## 從命令行啟動Adobe Experience Manager {#starting-adobe-experience-manager-from-the-command-line}

的 `start` 指令碼在 *這樣 &lt;cq-installation>/bin* 的子菜單。 提供了Unix和Windows版本。 指令碼將啟動安裝在 *&lt;cq-installation>* 的子菜單。

這兩個版本支援一個環境變數清單，這些變數可用於啟動和調AEM整實例。

<table>
 <tbody>
  <tr>
   <td><strong>環境變數 </strong></td>
   <td><strong>說明 </strong></td>
  </tr>
  <tr>
   <td>CQ埠</td>
   <td>用於停止和狀態指令碼的TCP埠<br /> </td>
  </tr>
  <tr>
   <td>CQ主機(_H)</td>
   <td>主機名<br /> </td>
  </tr>
  <tr>
   <td>CQ介面</td>
   <td>此伺服器應偵聽的介面<br /> </td>
  </tr>
  <tr>
   <td>CQ_RUNMODE</td>
   <td>用逗號分隔的運行模式<br /> </td>
  </tr>
  <tr>
   <td>CQ_JARFILE</td>
   <td>jarfile的名稱<br /> </td>
  </tr>
  <tr>
   <td>CQ_USE_JAAS</td>
   <td>使用JAAS（如果為true）<br /> </td>
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
>請注意，有些運行模式（包括作者和發佈）需要在首次啟動之前設定，AEM之後不能更改。 在設定應AEM用於生產的實例之前，請參閱 [運行模式文檔](/help/sites-deploying/configure-runmodes.md) 的雙曲餘切值。

### Windows平台start.bat指令碼示例 {#windows-platform-start-bat-script-example}

```shell
SET CQ_PORT=1234 & ./start.bat
```

### Unix平台啟動指令碼示例 {#unix-platform-start-script-example}

```shell
CQ_PORT=1234 ./start
```

>[!NOTE]
>
>啟動指令碼將啟AEM動安裝在 *這樣 &lt;cq-installation>/app* 的子菜單。

## 阻止Adobe Experience Manager {#stopping-adobe-experience-manager}

要停AEM止，請執行下列操作之一：

* 根據您使用的平台：

   * 如果從腳AEM本或命令行啟動，請按 **Ctrl+C** 關閉伺服器。
   * 如果在UNIX上使用了啟動指令碼，則必須使用停止腳AEM本。

* 如果通過雙AEM擊jar檔案啟動，請按一下 **開** 按鈕(然後更改為 **關閉**)關閉伺服器。

   ![chlimage_1-63](assets/chlimage_1-63.png)

## 正在從命令行中停止Adobe Experience Manager {#stopping-adobe-experience-manager-from-the-command-line}

的 `stop` 指令碼在 *這樣 &lt;cq-installation>/bin* 的子菜單。 提供了Unix和Windows版本。 該指令碼將停止安裝在 *&lt;cq-installation>* 的子菜單。

### Unix平台停止指令碼示例 {#unix-platform-stop-script-example}

```shell
./stop
```

### Windows平台stop.bat指令碼示例 {#windows-platform-stop-bat-script-example}

```shell
./stop.bat
```

如果只想預配置儲存庫（不重新定位儲存庫），您只需：

* 提取 `repository.xml` 到所需位置

* 更新 `repository.xml` 按要求

* 建立 `bootstrap.properties` 定義 `repository.config`

同樣，在開始實際安裝之前。
