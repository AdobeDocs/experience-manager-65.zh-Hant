---
title: Request Analysis Script
seo-title: Request Analysis Script
description: 製作請求分析指令碼以便於分析access.log檔案，生成可讀報表以供後續處理
seo-description: The request analysis script is made to ease the analysis of the access.log files producing a readable report for later processing
uuid: 24eff3c6-5748-46f3-a30c-4a3a6427ce1d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 1b5e0ccf-4157-45e3-8caf-1d6739d7d9d2
exl-id: e14a9cda-890f-46b7-9433-1b52eb91eae3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 2%

---

# Request Analysis Script{#request-analysis-script}

## 下載 {#download}

製作此指令碼是為了方便分析 `access.log` 產生可讀報表以供後續處理的檔案。

[取得檔案](assets/analyse-access.sh)

## 說明 {#description}

製作此指令碼是為了方便分析 `access.log` 產生可讀報表以供後續處理的檔案。

它會產生總體請求數、GET與POST、隨時間等變化的請求分配。

輸出採用Markdown語法，因此透過pandoc等工具，或透過Markdown檢視器等外掛程式在瀏覽器中顯示，將其轉換為PDF會較為容易。

它可以分析命令行上提供的自定義路徑。

從檔案內的註解中擷取，該註解會告訴您如何執行：

分析CQ `access.log` 外推各種資訊，並產生Markdown輸出， `stdout`.

## 使用狀況 {#usage}

`./analyse-access.sh access.log.2013-&ast;`

您可以提供其他自訂路徑，以便在命令列上進行分析

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

可通過簡單管道保存輸出

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
