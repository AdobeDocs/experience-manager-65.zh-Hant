---
title: 系統資訊服務API
seo-title: 系統資訊服務API
description: 本檔案提供有關係統資訊服務所提供之API的詳細資訊。
seo-description: 本檔案提供有關係統資訊服務所提供之API的詳細資訊。
uuid: 7f624216-56e6-4d49-b9a1-3c9af045dabe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 79fccce2-d090-4b50-9c58-3f2a00e651b2
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# 系統資訊服務API {#system-information-service-apis}

系統資訊服務提供一組REST API以檢索資訊。 下表提供API的詳細資訊：

<table>
 <thead>
  <tr>
   <th><p>名稱</p></th>
   <th><p>URL</p></th>
   <th><p>說明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>SystemInfo.properties</p></td>
   <td><p>https://[server]:[port]/rest/services/SystemInfo.properties`</p></td>
   <td><p>此API是system.getProperties <a href="https://docs.oracle.com/javase/6/docs/api/java/lang/System.html#getProperties()">Java API的包裝函式</a> 。 它檢索當前工作環境的配置。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.envVar</p></td>
   <td><p>https://[server]:[port]/rest/services/SystemInfo.envVar</p></td>
   <td><p>檢索主機作業系統的所有環境變數。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.logs</p></td>
   <td><p>https://[server]:[port]/rest/services/SystemInfo.logs</p></td>
   <td><p>下載包含應用程式伺服器記錄檔的zip檔案。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.config</p></td>
   <td><p>https://[server]:[port]/rest/services/SystemInfo.config</p></td>
   <td><p>擷取config.xml檔案的所有內容。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.services</p></td>
   <td><p>https://[server]:[port]/rest/services/SystemInfo.services</p></td>
   <td><p>擷取AEM表單服務的狀態和設定參數。</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.vitalDetails</p></td>
   <td><p>https://[server]:[port]/rest/services/SystemInfo.vitalDetails</p></td>
   <td><p>檢索伺服器正常運行時間、JVM參數、系統記憶體、堆大小、作業系統名稱、活動線程數和線程數。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.coreSettings</p></td>
   <td><p>https://[server]:[port]/rest/services/SystemInfo.coreSettings</p></td>
   <td><p>擷取下列屬性的值：</p>
    <ul>
     <li><p>AdobeTempDir</p></li>
     <li><p>AdobeServerFontDir</p></li>
     <li><p>CustomerFontDir</p></li>
     <li><p>GlobalDocumentStorageRootDir</p></li>
     <li><p>DefaultDocumentMaxInlineSize</p></li>
     <li><p>DefaultDocumentDissopalTimeout</p></li>
     <li><p>EnableDocumentDBStorage</p></li>
     <li><p>GlobalDocumentStorageUseNetworkShare</p></li>
     <li><p>EnableFIPS</p></li>
     <li><p>EnableWSDL</p></li>
     <li><p>DataServicesConfigFile </p></li>
     <li><p>EnableRDS</p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.database</p></td>
   <td><p>https://[server]:[port]/rest/services/SystemInfo.database</p></td>
   <td><p>檢索有關資料庫的詳細資訊。</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.licenseInfo</p></td>
   <td><p>https://[server]:[port]/rest/services/SystemInfo.licenseInfo</p></td>
   <td><p>擷取已安裝AEM表單元件的版本與授權資訊。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfNo.serverConfig</p></td>
   <td><p>https://[server]:[port]/rest/services/SystemInfo.serverConfig</p></td>
   <td><p>下載主機應用伺服器的配置檔案。 </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>https://[server]:[port]/rest/services/SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>檢索活動線程的計數和堆棧跟蹤。 它接受下列參數：</p>
    <ul>
     <li><p>iterations= [n]:指定迭代計數。 用數字替換n。 </p></li>
     <li><p>延遲= [n]:指定在開始下一個小版本之前要等待的毫秒數。 </p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.info</p></td>
   <td><p>https://[server]:[port]/rest/services/SystemInfo.info</p></td>
   <td><p>此API是所有系統資訊服務API的包裝函式。 在內部，它會執行所有系統資訊API，並下載郵遞區號格式的資訊。 </p><p><i><strong>注意</strong>:SystemInfo.info不提供活動線程的計數和堆棧跟蹤。 </i></p></td>
  </tr>
 </tbody>
</table>

