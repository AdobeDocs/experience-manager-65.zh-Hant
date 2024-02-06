---
title: AEM Forms的Hotfix
description: 提供有關如何下載和安裝AEM Forms的Hotfix的資訊。
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
source-git-commit: 5ab1fd033af0d6d5595fe41de003455ab9ba28a6
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Adobe Experience Manager Forms Hotfix{#aem-form-hotfix}

本文列出為解決已知問題、改善系統穩定性及增強AEM Forms整體效能而實作的重大修正。

>[!NOTE]
>
> 這些Hotfix的設計是累積性的，包含所有先前的修正。 將最新Hotfix套用至某個版本時，不僅可解決最近的問題，還可整合所有先前的錯誤修正和增強功能。

## 最適化Forms的Hotfix {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>日期</strong></td>
    <td><strong>Hotfix下載連結(AEM軟體發佈連結)</strong></td>
    <td><strong>已修正的問題</strong></td>
  </tr>
  <tr>
    <td>2024年1月29日</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fforms-foundation-qs-content-4.0.170-FORMS-12692-B0001.zip">JEE伺服器上Windows適用的AEM Service Pack 6.5.19.0 Hotfix</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>在JEE伺服器上的AEM Forms上，使用內容路徑的HTML5 Forms無法轉譯。 (FORMS-12485、FORMS-12691)。</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024年1月29日</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-win-pkg-6.0.1016-004.zip">適用於Microsoft Windows的AEM Service Pack 6.5.18.0 Hotfix</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-linux-pkg-6.0.1016-004.zip">適用於Linux的AEM Service Pack 6.5.18.0的Hotfix</a></li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-osx-pkg-6.0.1016-004.zip">適用於Apple macOS的AEM Service Pack 6.5.18.0的Hotfix</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li> OOTB手寫簽名元件無法以最適化表單呈現預覽。 (FORMS-12073)。</li>
    </ul>
    </td>    
   </tr>
   <tr>
    <td>2023年11月20日</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">適用於Linux的AEM Service Pack 6.5.18.0的Hotfix</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">適用於Microsoft Windows的AEM Service Pack 6.5.18.0 Hotfix</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">適用於Apple macOS的AEM Service Pack 6.5.18.0的Hotfix</a></li>
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

## 下載並安裝Hotfix {#download-install-hotfix}

執行以下步驟來下載及安裝Hotfix：

1. 下載 [Hotfix](#hotfix-for-adaptive-forms) 從Software Distribution連結。
1. 解壓縮Hotfix封存檔案，以便取得Experience Manager套件(.zip)和套件(.jar)檔案。
1. 透過上傳並安裝套件(.zip) [封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).
1. 開啟Configuration Manager組合 `https://server:host/system/console/bundles`，上傳並安裝套件組合(.jar)。 已安裝Hotfix。
