---
title: 全局文檔儲存目錄
seo-title: Global document storage directory
description: 全局文檔儲存(GDS)目錄是用於儲存進程內使用的長期檔案的目錄。
seo-description: The global document storage (GDS) directory is a directory used to store long-lived files that are used within a process.
uuid: 7681672c-a0dc-4445-8004-1b1e2ed3d301
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a33b8834-6e39-47eb-a53b-0982d32e80ad
exl-id: 7a64a643-808b-4644-8fd3-0dafe83e8dd9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 1%

---

# 全局文檔儲存目錄{#global-document-storage-directory}

此 *全局文檔儲存(GDS)* 目錄是用於儲存進程內使用的長期檔案的目錄。 這些檔案包括PDF、策略和表單模板。 長期檔案是許多AEM表單部署整體狀態的關鍵部分。 如果某些或所有長期文檔丟失或損壞，表單伺服器可能會變得不穩定。 非同步作業調用的輸入文檔也儲存在GDS目錄中，並且必須可用於處理請求。 請務必考慮承載GDS目錄的檔案系統的可靠性。 根據您的服務質量和級別需求，使用獨立磁碟冗餘陣列(RAID)或其他適當技術。

長期檔案可能包含敏感的用戶資訊。 透過AEM Forms API或使用者介面存取時，此資訊可能需要特殊憑證。 GDS目錄必須通過作業系統正確保護。 只有用於運行應用程式伺服器的管理員帳戶才應具有對GDS目錄的讀/寫訪問權限。

除了為GDS選擇安全、高可用的目錄外，您還可以選擇啟用資料庫中的文檔儲存。 請注意，即使使用AEM表單資料庫來儲存檔案，AEM表單仍需要GDS目錄。 (請參閱 [將資料庫用於文檔儲存時的備份選項](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage).)

AEM forms應用程式資料位於GDS目錄和AEM forms資料庫中。 下表說明資料及其位置。

<table>
 <thead>
  <tr>
   <th><p>AEM forms資料</p></th>
   <th><p>資料庫</p></th>
   <th><p>GDS</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>應用程式資料（用戶、角色、進程、策略、端點、事件等）。</p></td>
   <td><p>是</p></td>
   <td><p>否</p></td>
  </tr>
  <tr>
   <td><p>已部署的服務容器</p></td>
   <td><p>是</p></td>
   <td><p>否</p></td>
  </tr>
  <tr>
   <td><p>檔案管理員 </p></td>
   <td><p>否</p></td>
   <td><p>是</p></td>
  </tr>
  <tr>
   <td><p>Forms存放庫</p></td>
   <td><p>是</p></td>
   <td><p>否</p></td>
  </tr>
  <tr>
   <td><p>系統配置</p></td>
   <td><p>是</p></td>
   <td><p>否</p></td>
  </tr>
  <tr>
   <td><p>監看的資料夾</p></td>
   <td><p>否</p></td>
   <td><p>是</p></td>
  </tr>
 </tbody>
</table>

## 配置GDS目錄 {#configuring-the-gds-directory}

在AEM表單安裝過程中，可以手動配置GDS目錄的位置。 如果安裝期間位置設定保持空，則位置預設為應用程式伺服器安裝下的目錄，如下所示：

* (JBoss) `[appserver root]/server/[type]/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/DocumentServer/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

## 更改預設GDS位置 {#change-the-default-gds-location}

完成AEM表單安裝後，您可以在管理控制台中變更GDS位置。 您必須手動重新定位資料以完成程式。

>[!NOTE]
>
>以下列方式遷移資料，否則資料將丟失。

1. 登入管理控制台，然後按一下「設定>核心繫統設定>設定」。
1. 在全局文檔儲存目錄框中，輸入新GDS目錄的完整路徑，然後按一下確定。
1. 立即關閉應用程式伺服器。
1. 將所有檔案從舊的GDS目錄移動到新位置，保留內部目錄結構。
1. 重新啟動應用程式伺服器。

## 關於部署檔案 {#about-deployment-files}

AEM表單包含兩種部署檔案：服務容器和Java 2 Platform, Enterprise Edition(J2EE)EAR檔案。 EAR檔案包含標準J2EE應用程式套件組合，其中包含AEM表單的核心功能。 應用程式伺服器專用的EAR檔案如下：

* adobe-core-*[appserver]*.ear
* adobe-core-*[appserver]*-*[作業系統]*.ear

實作AEM表單時，需要將組合好的EAR檔案和支援檔案部署至您打算執行AEM表單解決方案的應用程式伺服器。 如果配置並裝配了多個模組，則可部署模組將封裝在可部署的EAR檔案中。 要部署這些檔案，請將它們複製到 *[appserver首頁]*\server\all\deploy directory。

模組和AEM表單存檔檔案會封裝在JAR檔案中。 因為它們不是J2EE類型的檔案，所以不部署到應用程式伺服器。 而是會複製到GDS目錄，而AEM表單資料庫中會儲存對其位置的參考。 因此，必須在群集的所有節點之間共用GDS目錄。 所有節點都必須能夠訪問DSC的中央儲存目錄。

>[!NOTE]
>
>部署服務容器之前，請確保已建立並配置了GDS目錄。 (請參閱 [配置GDS目錄](global-document-storage-directory.md#configuring-the-gds-directory))
