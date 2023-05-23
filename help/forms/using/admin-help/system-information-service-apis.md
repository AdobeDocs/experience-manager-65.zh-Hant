---
title: 系統資訊服務API
seo-title: System information Service APIs
description: 本文檔提供有關係統資訊服務提供的API的詳細資訊。
seo-description: This document provides detailed information about the APIs provided bythesystem information service.
uuid: 7f624216-56e6-4d49-b9a1-3c9af045dabe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 79fccce2-d090-4b50-9c58-3f2a00e651b2
exl-id: 4da96c8f-8bd0-4cad-9087-18e324f084e7
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# 系統資訊服務API {#system-information-service-apis}

系統資訊服務提供一組REST API以檢索資訊。 下表提供了有關API的詳細資訊：

<table>
 <thead>
  <tr>
   <th><p>名稱</p></th>
   <th><p>URL</p></th>
   <th><p>描述</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>SystemInfo.properties</p></td>
   <td><p>https://'[伺服器]:[port]'/rest/services/SystemInfo.properties'</p></td>
   <td><p>此API是 <a href="https://docs.oracle.com/javase/6/docs/api/java/lang/System.html#getProperties()">system.getProperties</a> Java API。 它檢索當前工作環境的配置。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.envVar</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.envVar</p></td>
   <td><p>檢索主機作業系統的所有環境變數。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.logs</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.logs</p></td>
   <td><p>下載包含應用程式伺服器日誌的zip檔案。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.config</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.config</p></td>
   <td><p>檢索config.xml檔案的所有內容。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.services</p></td>
   <td><p>https://'[server]:[port]'/rest/services/SystemInfo.services</p></td>
   <td><p>檢索表單服務的狀態AEM和配置參數。</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.vitalDetails</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.vitalDetails</p></td>
   <td><p>檢索伺服器正常運行時間、JVM參數、系統記憶體、堆大小、作業系統名稱、活動線程數和線程計數。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.coreSettings</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.coreSettings</p></td>
   <td><p>檢索以下屬性的值：</p>
    <ul>
     <li><p>AdobeTempDir</p></li>
     <li><p>AdobeServerFontDir</p></li>
     <li><p>客戶字型目錄</p></li>
     <li><p>GlobalDocumentStorageRootDir</p></li>
     <li><p>DefaultDocumentMaxInlineSize</p></li>
     <li><p>DefaultDocumentDisposationTimeout</p></li>
     <li><p>啟用DocumentDBStorage</p></li>
     <li><p>GlobalDocumentStorageUseNetworkShare</p></li>
     <li><p>啟用FIPS</p></li>
     <li><p>啟用WSDL</p></li>
     <li><p>資料服務配置檔案 </p></li>
     <li><p>啟用RDS</p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.database</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.database</p></td>
   <td><p>檢索有關資料庫的詳細資訊。</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.licenseInfo</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.licenseInfo</p></td>
   <td><p>檢索已安裝表單元件的版AEM本和許可證資訊。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfNo.serverConfig</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.serverConfig</p></td>
   <td><p>下載主機應用程式伺服器的配置檔案。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>檢索活動線程的計數和堆棧跟蹤。 它接受以下參數：</p>
    <ul>
     <li><p>迭代= [n]:指定迭代次數。 用數字替換n。 </p></li>
     <li><p>延遲= [n]:指定在啟動下一迭代之前等待的毫秒數。 </p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.info</p></td>
   <td><p>https://'[server]:[port]'/rest/services/SystemInfo.info</p></td>
   <td><p>此API是所有系統資訊服務API的包裝。 在內部，它運行所有系統資訊API並以zip格式下載資訊。 </p><p><i><strong>附註</strong>:SystemInfo.info不提供活動線程的計數和堆棧跟蹤。 </i></p></td>
  </tr>
 </tbody>
</table>
