---
title: AEM Forms的Hotfix
description: 提供有關如何下載和安裝AEM Forms的Hotfix的資訊。
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: ad71f1c92bba90000f72319536fffd255fb4db6e
workflow-type: tm+mt
source-wordcount: '673'
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
    <td>2024年6月21日</td>
     <td>
     <ul>
     <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">JBoss JEE伺服器上AEM Service Pack 6.5.21.0的Hotfix </a> </li>
      <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Weblogic JEE伺服器上AEM Service Pack 6.5.21.0的Hotfix </a> </li>
       <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">Webshpere JEE伺服器上AEM Service Pack 6.5.21.0的Hotfix </a> </li>
        <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">OSGi伺服器上AEM Service Pack 6.5.21.0的Hotfix </a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li> 升級至AEM Forms Service Pack 6.5.21.0後，PaperCapture服務無法在PDF上執行OCR （光學字元辨識）作業。 如需安裝指示，請參閱 <a href="/help/forms/using/papercapture-service-resolution.md"> 疑難排解</a> 文章。(CQDOC-21680) </li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024年6月21日</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2Fccm-ccr-content-10.0.206.zip">AEM Service Pack 6.5.21.0的Hotfix </a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>預覽期間，含XML資料的草稿字母卡在載入狀態。 如需Hotfix的下載和安裝指示，請參閱<a href="#install-hotfix"> 下載並安裝草稿字母問題的Hotfix</a> 區段。(FORMS-14521)</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024年5月16日</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1192-010.zip">適用於Microsoft Windows的AEM Service Pack 6.5.20.0 Hotfix</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1192-010.zip">適用於Linux的AEM Service Pack 6.5.20.0的Hotfix </a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1192-010.zip">適用於Apple macOS的AEM Service Pack 6.5.20.0的Hotfix</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>在以XDP為基礎且核取方塊上有內嵌指令碼的最適化表單中，此類核取方塊之後的元素不會執行指令碼。 已針對此問題提供Hotfix。 (FORMS-14244) </li>
     <li> 在具有編輯/顯示模式的欄位中，在快顯Widget中瀏覽月份時，日期選擇器Widget中的列會被截斷。 已針對此問題提供Hotfix。 (FORMS-13620) </li>
     <li>嘗試在後端使用DOR （記錄檔案）服務時，表單提交失敗。 遇到的錯誤訊息為：「提交動作無法完成，因為未正確指派表單資源。」 (FORMS-13798) </li>
     <li>從Adobe Experience Manager發佈執行個體提交最適化表單至Adobe Experience Manager Workflow時，工作流程無法儲存附件。  (FORMS-14209) </li>
     <li> 安裝AEM 6.5 Forms Service Pack 20套件(適用於SP20的AEM Forms附加元件套件)時，AEM Sites使用者介面(UI)效能大幅降低。  (FORMS-13791) </li>
     <li>預填服務在互動式通訊中失敗，並出現Null指標例外狀況。 (CQDOC-21355)</li>
    </ul>
    </td>    
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
    <li> 現成可用的手寫簽名元件無法以最適化表單呈現預覽。 (FORMS-12073)。</li>
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


## 下載並安裝草稿字母問題的Hotfix {#install-hotfix}

若要解決此問題，請執行以下步驟：

1. 下載 [hotfix](#hotfix-for-adaptive-forms) 從軟體發佈入口網站。
2. 使用上傳並安裝套件(.zip) [CRX封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).