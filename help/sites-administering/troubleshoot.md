---
title: 疑難排解AEM
seo-title: Troubleshooting AEM
description: 了解疑難排解AEM的問題。
seo-description: Learn about troubleshooting issues with AEM.
uuid: 72379531-915c-45d0-ba70-42b212665272
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6346cd93-1ca3-4510-9c31-a74c41017ddb
docset: aem65
exl-id: d2d351e7-87a5-4895-b4ec-391fb0b66798
source-git-commit: d1b4cf87291f7e4a0670a21feca1ebf8dd5e0b5e
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 2%

---

# 疑難排解AEM {#troubleshooting-aem}

以下章節說明使用AEM時可能會遇到的一些問題，以及如何疑難排解的建議。

>[!NOTE]
>
>若要疑難排解AEM中的編寫問題，請參閱 [作者疑難排解。](/help/sites-authoring/troubleshooting.md)

>[!NOTE]
>
>遇到問題時，也值得檢查 [已知問題](/help/release-notes/release-notes.md) 適用於您的執行個體（發行和服務套件）。

## 管理員的疑難排解案例 {#troubleshooting-scenarios-for-administrators}

下表概述管理員可能需要進行疑難排解的問題：

<table>
 <tbody>
  <tr>
   <td><strong>角色</strong></td>
   <td><strong>問題 </strong></td>
  </tr>
  <tr>
   <td>系統管理員</td>
   <td><p>按兩下Quickstart Jar不會產生任何效果，或使用其他程式（例如，歸檔管理器）開啟jar檔案</p> </td>
  </tr>
  <tr>
   <td><p>系統管理員</p> </td>
   <td><p>我在CRX上執行的應用程式擲回記憶體不足錯誤</p> </td>
  </tr>
  <tr>
   <td><p>系統管理員</p> </td>
   <td><p>按兩下「AEM CM快速入門」後，瀏覽器中不會顯示「AEM歡迎」畫面</p> </td>
  </tr>
  <tr>
   <td><p>系統管理員</p> <p>管理員使用者</p> </td>
   <td><p>建立線程轉儲</p> </td>
  </tr>
  <tr>
   <td><p>系統管理員</p> <p>管理員使用者</p> </td>
   <td><p>檢查未關閉的JCR會話</p> </td>
  </tr>
 </tbody>
</table>

## 安裝問題 {#installation-issues}

請參閱 [常見安裝問題](/help/sites-deploying/troubleshooting.md#common-installation-issues) 以了解下列疑難排解案例的資訊：

* 按兩下Quickstart Jar不起作用，或JAR檔案與其他程式（如歸檔管理器）一起無效。
* 在CRX上運行的應用程式會擲出記憶體不足錯誤。
* 按兩下「AEM快速入門」後，瀏覽器中不會顯示「AEM歡迎」畫面。

## 疑難排解分析的方法 {#methods-for-troubleshooting-analysis}

### 建立線程轉儲 {#making-a-thread-dump}

線程轉儲是當前活動的所有Java線程的清單。 如果AEM未正確響應，線程轉儲可幫助您識別死鎖或其他問題。

### 使用Sling線程轉儲程式 {#using-sling-thread-dumper}

1. 開啟 **AEM Web Console**;例如 `https://localhost:4502/system/console/`.
1. 選取 **線程**&#x200B;在&#x200B;**狀態** 標籤。

![screen_shot_2012-02-13at43925pm](assets/screen_shot_2012-02-13at43925pm.png)

### 使用jstack（命令列） {#using-jstack-command-line}

1. 尋找AEM Java例項的PID（程式ID）。

   例如，您可以使用 `ps -ef` 或 `jps`.

1. 執行:

   `jstack <pid>`

1. 這將顯示線程轉儲。

>[!NOTE]
>
>您可以使用 `>>` 輸出重定向：
>
>`jstack <pid> >> /path/to/logfile.log`

請參閱 [如何從JVM獲取線程轉儲](https://helpx.adobe.com/cq/kb/TakeThreadDump.html) 檔案以取得詳細資訊

### 檢查未關閉的JCR會話 {#checking-for-unclosed-jcr-sessions}

為AEM WCM開發功能時，可以開啟JCR工作階段（與開啟資料庫連線類似）。 如果開啟的工作階段從未關閉，您的系統可能會出現下列症狀：

* 系統變慢了。
* 您可以看到許多CacheManager:resize日誌檔案中的所有條目；以下數字(大小=&lt;x>)顯示快取的數量，每個會話開啟多個快取。
* 系統有時記憶體不足（幾小時、幾天或幾週後，具體取決於嚴重性）。

要分析未結束的會話，並查明哪個代碼不在結束會話，請參閱知識庫文章 [分析非關閉的會話](https://helpx.adobe.com/crx/kb/AnalyzeUnclosedSessions.html).

### 使用Adobe Experience Manager Web Console {#using-the-adobe-experience-manager-web-console}

OSGi套件組合的狀態也可提供可能問題的初步指示。

1. 開啟 **AEM Web Console**;例如 `https://localhost:4502/system/console/`.
1. 選擇 **套件組合** 在 **OSGI** 標籤。
1. 檢查:

   * 包的狀態。 如果有非活動或未滿足，請嘗試停止並重新啟動套件組合。 如果問題持續存在，則您可能需要使用其他方法進一步調查。
   * 是否有任何包缺少依賴項。 按一下個別套件名稱即為連結（下列範例不含任何問題）即可查看此類詳細資料：

![screen_shot_2012-02-13at44706pm](assets/screen_shot_2012-02-13at44706pm.png)
