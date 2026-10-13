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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 2%
---
# 要求分析指令碼{#request-analysis-script}

## 下載 {#download}

編寫此指令碼是為了方便分析`access.log`個檔案，產生可讀報告以供日後處理。

[取得檔案](assets/analyse-access.sh)

## 說明 {#description}

編寫此指令碼是為了方便分析`access.log`個檔案，產生可讀報告以供日後處理。

這會產生整體請求數、GET與POST、隨時間變化的請求分佈等等。

輸出為Markdown語法，因此將比較容易轉換成使用pandoc等工具的PDF，或在瀏覽器中使用Markdown檢視器等外掛程式顯示。

它可以分析命令列上提供的自訂路徑。

從檔案內告訴您如何執行的註解取得：

分析CQ `access.log`推斷各種資訊，並在`stdout`上產生Markdown輸出。

## 用途 {#usage}

`./analyse-access.sh access.log.2013-&ast;`

您可以提供其他自訂路徑，以便在命令列上分析

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

您可以使用簡單管路儲存輸出

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
