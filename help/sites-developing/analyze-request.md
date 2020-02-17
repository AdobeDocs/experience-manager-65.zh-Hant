---
title: 請求分析指令碼
seo-title: 請求分析指令碼
description: 請求分析指令碼可輕鬆分析access.log檔案，產生可讀報告以供日後處理
seo-description: 請求分析指令碼可輕鬆分析access.log檔案，產生可讀報告以供日後處理
uuid: 24eff3c6-5748-46f3-a30c-4a3a6427ce1d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 1b5e0ccf-4157-45e3-8caf-1d6739d7d9d2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 請求分析指令碼{#request-analysis-script}

## 下載 {#download}

此指令碼可簡化產生可讀報表 `access.log` 的檔案分析，以供日後處理。

[取得檔案](assets/analyse-access.sh)

## 說明 {#description}

此指令碼可簡化產生可讀報表 `access.log` 的檔案分析，以供日後處理。

它會產生整體請求編號、GET與POST、隨時間的請求分發等。

輸出採用Markdown語法，因此使用pandoc等工具將它轉換為PDF，或在瀏覽器中使用Markdown檢視器等增效模組來顯示它會更輕鬆。

它可以分析命令行上提供的自定義路徑。

從檔案中擷取註解，告知您如何執行它：

分析CQ外 `access.log` 推各種資訊並產生Markdown輸出 `stdout`。

## 使用狀況 {#usage}

`./analyse-access.sh access.log.2013-&ast;`

您可以提供其他自訂路徑，以便在命令列上進行分析

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

可通過簡單管道保存輸出

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
