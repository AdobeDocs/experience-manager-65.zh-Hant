---
title: 要求分析指令碼
description: 製作request analysis指令碼是為了便於分析access.log檔案，產生可讀報告以供日後處理
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: e14a9cda-890f-46b7-9433-1b52eb91eae3
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 2%

---

# 要求分析指令碼{#request-analysis-script}

## 下載 {#download}

編寫此指令碼是為了便於分析 `access.log` 產生可讀報告以供日後處理的檔案。

[取得檔案](assets/analyse-access.sh)

## 說明 {#description}

編寫此指令碼是為了便於分析 `access.log` 產生可讀報告以供日後處理的檔案。

這會產生整體請求數量、GET與POST、隨時間變化的請求分佈等等。

輸出為Markdown語法，因此將比較容易轉換成使用pandoc等PDF或使用Markdown檢視器等外掛程式在瀏覽器中顯示。

它可以分析命令列上提供的自訂路徑。

從檔案內告訴您如何執行的註解取得：

分析CQ `access.log` 推斷各種資訊並在上產生Markdown輸出 `stdout`.

## 使用情況 {#usage}

`./analyse-access.sh access.log.2013-&ast;`

您可以提供其他自訂路徑，以便在命令列上分析

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

您可以使用簡單管路儲存輸出

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
