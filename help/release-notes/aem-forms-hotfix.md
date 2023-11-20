---
title: AEM Form Service Pack的Hotfix
description: 提供如何下載和安裝AEM Forms Service Pack的Hotfix的相關資訊
source-git-commit: 169d407835098add0312b0d12c2c80035b525762
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# Adobe Experience Manager Hotfix{#aem-form-hotfix}

安裝最新版的 [AEM Service Pack](/help/release-notes/release-notes.md) 我們建議您使用，其中包括安全性、效能、穩定性，以及自Adobe Experience Manager 6.5正式發行以來累積的重要客戶修正和增強功能。

## 最適化Forms的Hotfix {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>日期</strong></td>
    <td><strong>Hotfix名稱</strong></td>
    <td><strong>修正</strong></td>
   </tr>
   <tr>
    <td>2023 年 11 月 20 日</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">適用於Linux的AEM Service Pack 6.5.18.0的Hotfix</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">適用於Windows的AEM Service Pack 6.5.18.0的Hotfix</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">適用於Mac作業系統的AEM Service Pack 6.5.18.0 Hotfix</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li>在最適化表單的引導容器中設定重新導向URL時，內嵌簽署會停止運作。 (FORMS-10493)</li>
    <li>記錄檔案(DoR)範本無法針對當地語系化的最適化Forms發佈。 (FORMS-10535)</li>
    <li>含有大型內嵌影像的互動式通訊無法在編輯模式中開啟。 (FORMS-10578)</li>
    </ul>
    </td>    
    </tr>
    <tbody>
     </table>

## 下載和安裝Hotfix {#download-install-hotfix}

執行以下步驟來下載及安裝Hotfix：

1. 下載 [Hotfix](#hotfix-for-adaptive-forms) 從SD連結。
1. 解壓縮Hotfix封存檔案，以便取得Experience Manager套件(.zip)和套件(.jar)檔案。
1. 透過封裝管理員上傳並安裝封裝(.zip)。
1. 開啟Configuration Manager組合 `https://server:host/system/console/bundles`，上傳並安裝套件組合(.jar)。
