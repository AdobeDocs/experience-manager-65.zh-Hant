---
title: AEM Forms的Hotfix
description: 提供有關如何下載和安裝AEM Forms的Hotfix的資訊。
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 59d667004bb41a973847e9c53333afaa188ccac1
workflow-type: tm+mt
source-wordcount: '1160'
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
    <td><strong>Hotfix下載連結(AEM Software Distribution連結)</strong></td>
    <td><strong>已修正的問題</strong></td>
  </tr>
  <tr>
    <td>SP23 Hotfix-</td>
    <td>
    <ul>
    <li><strong>Jboss：</strong></li>
    <li>Windows - <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/jboss/adobe-aem-forms-jee-hotfix-6.5.23.0-win-jboss.zip">適用於JBoss JEE伺服器Windows上AEM Service Pack 6.5.23.0的Hotfix</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/jboss/adobe-aem-forms-jee-hotfix-6.5.23.0-linux-jboss.tar.gz">適用於Linux上AEM Service Pack 6.5.23.0的Hotfix （適用於JBoss JEE伺服器）</a></li>
    <li><strong>Weblogic：</strong></li>
    <li>Windows — 適用於Weblogic JEE伺服器的Windows上<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/weblogic/adobe-aem-forms-jee-hotfix-6.5.23.0-win-weblogic.zip">AEM Service Pack 6.5.23.0的Hotfix</a></li>
    <li>Linux- Weblogic JEE伺服器<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/weblogic/adobe-aem-forms-jee-hotfix-6.5.23.0-linux-weblogic.tar.gz">的Linux上AEM Service Pack 6.5.23.0的</a>Hotfix</li>
    <li><strong>Websphere：</strong></li>
    <li>Windows：適用於Websphere JEE伺服器的Windows上AEM Service Pack 6.5.23.0的<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/websphere/adobe-aem-forms-jee-hotfix-6.5.23.0-win-websphere.zip">Hotfix</a></li>
    <li>Linux：適用於Websphere JEE伺服器的Linux上AEM Service Pack 6.5.23.0的<a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-2/websphere/adobe-aem-forms-jee-hotfix-6.5.23.0-linux-websphere.tar.gz">Hotfix</a></li>
    </ul>
    </td>
    <td>
    <ul>
    <li>JEE版AEM Forms的SP23 Hotfix</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2025年3月26日</br> </br>若要安裝此修正，請遵循指示<a href="/help/forms/using/mitigating-spring-framework-vulnerabilities-for-aem-forms-on-jee.md">緩解JEE上AEM Forms的Spring Framework漏洞</a>。</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/jboss/adobe-aem-forms-jee-hotfix-6.5.22.0-win-jboss.tar.gz">適用於JBoss JEE伺服器</a>之Windows上AEM Service Pack 6.5.22.0的Hotfix </li>
      <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/jboss/adobe-aem-forms-jee-hotfix-6.5.22.0-linux-jboss.tar.gz">適用於JBoss JEE伺服器</a>之Linux上AEM Service Pack 6.5.22.0的Hotfix </li>
       <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/weblogic/adobe-aem-forms-jee-hotfix-6.5.22.0-win-weblogic.tar.gz">適用於Weblogic JEE伺服器</a>之Windows上AEM Service Pack 6.5.22.0的Hotfix </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/weblogic/adobe-aem-forms-jee-hotfix-6.5.22.0-linux-weblogic.tar.gz">Linux上Weblogic JEE伺服器專用AEM Service Pack 6.5.22.0的Hotfix</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/websphere/adobe-aem-forms-jee-hotfix-6.5.22.0-win-websphere.tar.gz">適用於Windows上Websphere JEE伺服器</a>的AEM Service Pack 6.5.22.0 Hotfix </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/websphere/adobe-aem-forms-jee-hotfix-6.5.22.0-linux-websphere.tar.gz">Linux上Websphere JEE伺服器專用AEM Service Pack 6.5.22.0的Hotfix</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>緩解JEE上AEM Forms的Spring Framework漏洞</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024年7月10日</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-jboss.zip.zip">適用於JBoss JEE伺服器</a>之Windows上AEM Service Pack 6.5.21.0的Hotfix </li>
      <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/jboss/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-jboss.tar.gz">適用於JBoss JEE伺服器</a>的Linux上AEM Service Pack 6.5.21.0的Hotfix </li>
       <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-websphere.zip.zip">適用於Webshpere JEE伺服器</a>的Windows上AEM Service Pack 6.5.21.0的Hotfix </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/websphere/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-websphere.tar.gz">適用於Webshpere JEE伺服器Linux上AEM Service Pack 6.5.21.0的Hotfix</a> </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/win/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-windows-weblogic.zip.zip">適用於Weblogic JEE伺服器</a>之Windows上AEM Service Pack 6.5.21.0的Hotfix </li>
        <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/aemforms-6-5-0-0089/weblogic/linux/adobe-aem-forms-jee-service-pack-6.5.21.0-hotfix-linux-weblogic.tar.gz">Linux上Weblogic JEE伺服器專用AEM Service Pack 6.5.21.0的Hotfix</a> </li>
     </ul>
     </td>
    <td>
    <ul><li>當使用者在JEE伺服器上更新至AEM Forms Service Pack 20 (6.5.20.0)，並使用輸出服務產生PDF時，PDF會呈現協助工具問題。 (LC-3922112)</li><li>在AEM Forms JEE上使用輸出服務產生的已標籤PDF會顯示「不適當的結構警告」。 (LC-3922038)</li><li>在AEM Forms JEE上提交表單時，會從資料中移除重複的XML元素例項。 (LC-3922017)</li><li>當Linux環境中的使用者在HTML中轉譯最適化表單（在JEE上）時，該表單將無法正確轉譯。 (LC-3921957)</li><li>當使用者使用AEM Forms JEE上的輸出服務將XTG檔案轉換為PostScript格式時，它會失敗並出現錯誤： AEM_OUT_001_003：非預期的例外狀況：PAExecute失敗：XFA_RENDER_FAILURE。 (LC-3921720)</li><li>在JEE伺服器上升級至AEM Forms Service Pack 18 (6.5.18.0)後，當使用者提交表單時，將無法轉譯HTML5或PDF forms，並且XMLFM會當機。 (LC-3921718)
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024年6月21日</td>
     <td>
     <ul>
     <li>JBoss JEE伺服器<a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">上的AEM Service Pack 6.5.21.0或AEM Forms Service Pack 6.5.22.0的</a>Hotfix </li>
      <li>Weblogic JEE伺服器<a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">上的</a>AEM Service Pack 6.5.21.0或AEM Forms Service Pack 6.5.22.0的Hotfix </li>
       <li>Webshpere JEE伺服器<a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">上的</a>AEM Service Pack 6.5.21.0或AEM Forms Service Pack 6.5.22.0的Hotfix </li>
        <li><a href="https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0">OSGi伺服器</a>上AEM Service Pack 6.5.21.0或AEM Forms Service Pack 6.5.22.0的Hotfix </li>
     </ul>
     </td>
    <td>
    <ul>
    <li> 升級至AEM Forms Service Pack 6.5.21.0或AEM Forms Service Pack 6.5.22.0後，PaperCapture服務無法在PDF上執行OCR （光學字元辨識）作業。 如需安裝指示，請參閱<a href="/help/forms/using/papercapture-service-resolution.md">疑難排解</a>文章。(CQDOC-21680) </li>
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
    <li>預覽期間，含XML資料的草稿字母卡在載入狀態。 如需下載和安裝Hotfix的指示，請參閱<a href="#install-hotfix">下載和安裝草稿信件問題</a>的Hotfix區段。(FORMS-14521)</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024年5月16日</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1192-010.zip">適用於Microsoft Windows的AEM Service Pack 6.5.20.0 Hotfix</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1192-010.zip">適用於Linux </a>的AEM Service Pack 6.5.20.0 Hotfix </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1192-010.zip">適用於Apple macOS的AEM Service Pack 6.5.20.0 Hotfix</a> </li>
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
     <li>使用舊版Adobe Analytics雲端服務及使用者認證式驗證的設定無法正常運作，導致Analytics規則無法執行。 (FORMS-15428)
    </ul>
    </td>    
  </tr>
  <tr>
    <td>2024年1月29日</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fforms-foundation-qs-content-4.0.170-FORMS-12692-B0001.zip">JEE伺服器Windows專用AEM Service Pack 6.5.19.0的Hotfix</a> </li>
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
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">適用於Linux的AEM Service Pack 6.5.18.0 Hotfix</a> </li>
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

1. 從Software Distribution連結下載[Hotfix](#hotfix-for-adaptive-forms)。
1. 解壓縮Hotfix封存檔案，以便取得Experience Manager套件(.zip)和套件(.jar)檔案。
1. 透過[封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing)上傳及安裝封裝(.zip)。
1. 開啟設定管理員組合`https://server:host/system/console/bundles`，上傳並安裝組合(.jar)。 已安裝Hotfix。


## 下載並安裝草稿字母問題的Hotfix {#install-hotfix}

若要解決此問題，請執行以下步驟：

1. 從軟體發佈入口網站下載[Hotfix](#hotfix-for-adaptive-forms)。
2. 使用[CRX封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing)上傳及安裝封裝(.zip)。