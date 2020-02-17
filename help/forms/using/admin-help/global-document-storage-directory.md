---
title: 全域檔案儲存目錄
seo-title: 全域檔案儲存目錄
description: 全局文檔儲存(GDS)目錄是用於儲存進程內使用的長壽命檔案的目錄。
seo-description: 全局文檔儲存(GDS)目錄是用於儲存進程內使用的長壽命檔案的目錄。
uuid: 7681672c-a0dc-4445-8004-1b1e2ed3d301
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a33b8834-6e39-47eb-a53b-0982d32e80ad
translation-type: tm+mt
source-git-commit: 215ba1cb3e98954418b844849c812c9ba6cf572b

---


# 全域檔案儲存目錄{#global-document-storage-directory}

全 *局文檔儲存(GDS)* 目錄是用於儲存進程內使用的長生命週期檔案的目錄。 這些檔案包含PDF、原則和表單範本。 長期使用的檔案是許多AEM表單部署整體狀態的重要部分。 如果某些或所有長期使用的檔案遺失或損毀，表單伺服器可能會變得不穩定。 非同步作業調用的輸入文檔也儲存在GDS目錄中，並且必須可用於處理請求。 請務必考慮托管GDS目錄的檔案系統的可靠性。 根據您的服務質量和級別需要，使用獨立磁碟冗餘陣列(RAID)或其他技術。

長期使用的檔案可能包含敏感的使用者資訊。 當使用AEM表單API或使用者介面存取此資訊時，可能需要特殊認證。 GDS目錄必須通過作業系統正確保護。 只有用於運行應用程式伺服器的管理員帳戶才應具有對GDS目錄的讀／寫訪問權限。

除了為GDS選擇安全、高可用的目錄外，您還可以選擇在資料庫中啟用文檔儲存。 請注意，即使使用AEM表單資料庫來儲存檔案，AEM表單仍需要GDS目錄。 (請參 [閱資料庫用於文檔儲存時的備份選項](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage)。)

AEM表單應用程式資料位於GDS目錄和AEM表單資料庫中。 下表說明資料及其位置。

<table>
 <thead>
  <tr>
   <th><p>AEM表單資料</p></th>
   <th><p>資料庫</p></th>
   <th><p>GDS</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>應用程式資料（使用者、角色、程式、原則、端點、事件等）。</p></td>
   <td><p>是</p></td>
   <td><p>否</p></td>
  </tr>
  <tr>
   <td><p>部署的服務容器</p></td>
   <td><p>是</p></td>
   <td><p>否</p></td>
  </tr>
  <tr>
   <td><p>檔案管理員 </p></td>
   <td><p>否</p></td>
   <td><p>是</p></td>
  </tr>
  <tr>
   <td><p>Forms Repository</p></td>
   <td><p>是</p></td>
   <td><p>否</p></td>
  </tr>
  <tr>
   <td><p>系統配置</p></td>
   <td><p>是</p></td>
   <td><p>否</p></td>
  </tr>
  <tr>
   <td><p>受監視的資料夾</p></td>
   <td><p>否</p></td>
   <td><p>是</p></td>
  </tr>
 </tbody>
</table>

## 配置GDS目錄 {#configuring-the-gds-directory}

在AEM表單安裝程式期間，可手動設定GDS目錄的位置。 如果位置設定在安裝期間保持空，則位置預設為應用程式伺服器安裝下的目錄，如下所示：

* (JBoss) `[appserver root]/server/[type]/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/[server]/adobe/DocumentServer/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/[server]/DocumentStorage`

## 更改預設GDS位置 {#change-the-default-gds-location}

在AEM表單安裝完成後，您可以變更管理控制台中的GDS位置。 您必須手動重新定位資料以完成該過程。

>[!NOTE]
>
>以下列方式遷移資料，否則將發生資料丟失。

1. 登入管理控制台，然後按一下「設定>核心繫統設定>設定」。
1. 在「全局文檔儲存目錄」框中，輸入到新GDS目錄的完整路徑，然後按一下「確定」。
1. 立即關閉應用程式伺服器。
1. 將所有檔案從舊GDS目錄移動到新位置，保留內部目錄結構。
1. 重新啟動應用程式伺服器。

## 關於部署檔案 {#about-deployment-files}

AEM表單包含兩種部署檔案類型：服務容器和Java 2 Platform, Enterprise Edition(J2EE)EAR檔案。 EAR檔案由標準J2EE應用程式套件組成，其中包含AEM表單的核心功能。 應用程式伺服器專用的EAR檔案如下：

* adobe-core-*[appserver]*.ear
* adobe-core-*[appserver]*-*[OS]*.ear

實作AEM表單需要將已組合的EAR檔案和支援檔案部署至您計畫執行AEM表單解決方案的應用程式伺服器。 如果配置並組裝了多個模組，則可部署模組將打包在可部署的EAR檔案中。 若要部署這些檔案，請將它們複製至 *[appserver首]*&#x200B;頁\server\all\deploy directory。

模組和AEM表單封存檔案會封裝在JAR檔案中。 由於它們不是J2EE類型的檔案，因此不會部署在應用程式伺服器上。 而是複製到GDS目錄，其位置的參考會儲存在AEM表單資料庫中。 因此，必須在群集的所有節點之間共用GDS目錄。 所有節點都必須具有對DSC的中央儲存目錄的訪問權。

>[!NOTE]
>
>在部署服務容器之前，請確保已建立並配置了GDS目錄。 (請參 [閱配置GDS目錄](global-document-storage-directory.md#configuring-the-gds-directory))

