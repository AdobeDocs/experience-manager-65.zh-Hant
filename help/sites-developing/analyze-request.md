---
title: 請求分析指令碼
seo-title: Request Analysis Script
description: 建立請求分析指令碼以簡化對access.log檔案的分析，生成可讀報告以供以後處理
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

# 請求分析指令碼{#request-analysis-script}

## 下載 {#download}

製作此指令碼是為了簡化 `access.log` 生成可讀報告以供以後處理的檔案。

[取得檔案](assets/analyse-access.sh)

## 說明 {#description}

製作此指令碼是為了簡化 `access.log` 生成可讀報告以供以後處理的檔案。

它產生總的請求數、GET與POST、請求分佈，時間長度等。

輸出採用Markdown語法，因此使用pandoc等工具將其轉換為PDF或在帶有Markdown查看器等插件的瀏覽器中顯示將更加容易。

它可以分析命令行上提供的自定義路徑。

從檔案中告訴您如何運行注釋中獲取：

分析CQ `access.log` 外推各種資訊並生成關於 `stdout`。

## 使用狀況 {#usage}

`./analyse-access.sh access.log.2013-&ast;`

可以提供附加的自定義路徑以在命令行上分析

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

可通過簡單管道保存輸出

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
