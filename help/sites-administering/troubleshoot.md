---
title: 故障排除Adobe Experience Manager
description: 瞭解與有關的故障排除AEM問題。
uuid: 72379531-915c-45d0-ba70-42b212665272
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6346cd93-1ca3-4510-9c31-a74c41017ddb
docset: aem65
exl-id: d2d351e7-87a5-4895-b4ec-391fb0b66798
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 2%

---

# 故障排除Adobe Experience Manager {#troubleshooting-aem}

以下部分介紹在使用(Adobe Experience Manager)時可能遇到的AEM一些問題，以及有關如何解決這些問題的建議。

>[!NOTE]
>
>如果要排除中的創作問題，請AEM參閱 [作者故障排除。](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>當遇到問題時，也值得檢查 [已知問題](/help/release-notes/release-notes.md) 例如（發行版和服務包）。

## 為管理員排除故障方案 {#troubleshooting-scenarios-for-administrators}

下表概述了管理員可以解決的問題：

<table>
 <tbody>
  <tr>
   <td><strong>角色</strong></td>
   <td><strong>問題 </strong></td>
  </tr>
  <tr>
   <td>系統管理員</td>
   <td><p>按兩下Quickstart jar無效，或使用其他程式（例如，存檔管理器）開啟jar檔案</p> </td>
  </tr>
  <tr>
   <td><p>系統管理員</p> </td>
   <td><p>我在CRX上運行的應用程式引發記憶體不足錯誤</p> </td>
  </tr>
  <tr>
   <td><p>系統管理員</p> </td>
   <td><p>按兩下AEMCM Quickstart後，瀏覽器中不顯示歡迎AEM螢幕</p> </td>
  </tr>
  <tr>
   <td><p>系統管理員</p> <p>管理員用戶</p> </td>
   <td><p>建立線程轉儲</p> </td>
  </tr>
  <tr>
   <td><p>系統管理員</p> <p>管理員用戶</p> </td>
   <td><p>檢查未關閉的JCR會話</p> </td>
  </tr>
 </tbody>
</table>

## 安裝問題 {#installation-issues}

請參閱 [常見安裝問題](/help/sites-deploying/troubleshooting.md#common-installation-issues) 有關以下故障排除方案的資訊：

* 按兩下Quickstart jar無效，或使用其他程式（如存檔管理器）的JAR檔案。
* 在CRX上運行的應用程式會出現記憶體不足錯誤。
* 按兩下AEM「Quickstart（快速啟動）」後，「Welcome（歡迎）」螢幕不會顯示AEM在瀏覽器中。

## 故障排除分析的方法 {#methods-for-troubleshooting-analysis}

### 建立線程轉儲 {#making-a-thread-dump}

線程轉儲是當前處於活動狀態的所有Java™線程的清單。 如AEM果響應不正確，線程轉儲可幫助您識別死鎖或其他問題。

### 使用吊索螺紋卸荷器 {#using-sling-thread-dumper}

1. 開啟 **Web控AEM制台**;例如，在 `https://localhost:4502/system/console/`。
1. 選擇 **線程**&#x200B;在&#x200B;**狀態** 頁籤。

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### 使用jstack（命令行） {#using-jstack-command-line}

1. 查找Java™實例的AEMPID（進程ID）。

   例如，您可以 `ps -ef` 或 `jps`。

1. 執行:

   `jstack <pid>`

1. 顯示線程轉儲。

>[!NOTE]
>
>可以使用 `>>` 輸出重定向：
>
>`jstack <pid> >> /path/to/logfile.log`

查看 [如何從JVM獲取線程轉儲](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17452.html?lang=en) 文檔，以獲取詳細資訊

### 檢查未關閉的JCR會話 {#checking-for-unclosed-jcr-sessions}

為WCM開發功能時AEM，可以開啟JCR會話（與開啟資料庫連接類似）。 如果開啟的會話從未關閉，則您的系統可能會出現以下症狀：

* 系統變慢。
* 您可以看到CacheManager的很多內容：調整日誌檔案中的所有條目；以下數字(大小=&lt;x>)顯示快取數，每個會話開啟多個快取。
* 系統不時記憶體不足（幾小時、幾天或幾週後，具體取決於嚴重性）。

要分析未關閉的會話並找出哪些代碼未關閉會話，請參閱知識庫文章 [分析未關閉的會話](https://helpx.adobe.com/experience-manager/kb/AnalyzeUnclosedSessions.html)。

### 使用Adobe Experience ManagerWeb控制台 {#using-the-adobe-experience-manager-web-console}

OSGi捆綁包的狀態還可以提前指示可能的問題。

1. 開啟 **Web控AEM制台**;例如，在 `https://localhost:4502/system/console/`。
1. 選擇 **捆綁** 在 **奧斯吉** 頁籤。
1. 檢查:

   * 束的狀態。 如果有「非活動」或「未滿足」，請嘗試停止並重新啟動捆綁包。 如果問題仍然存在，請使用其他方法進行進一步調查。
   * 是否有任何束缺少依賴項。 通過按一下單個捆綁包名稱（即連結）可以看到這些詳細資訊（以下示例沒有任何問題）:

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)
