---
title: 準備AEM Forms以進行備份
seo-title: 準備AEM Forms以進行備份
description: 'null'
seo-description: 'null'
uuid: b8ef2bed-62e2-4000-b55a-30d2fc398a5f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e747147e-e96d-43c7-87b3-55947eef81f5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 準備AEM Forms以進行備份 {#preparing-aem-forms-for-backup}

## 關於備份和恢復服務 {#about-the-backup-and-restore-service}

「備份和還原」服務可讓您將AEM Forms置於備 *份模式*，以便執行熱備份。 Backup and Restore服務實際上不會執行AEM Forms的備份或還原系統。 相反地，它使伺服器處於一致可靠的備份狀態，同時允許伺服器繼續運行。 您負責備份全局文檔儲存(GDS)和連接到表單伺服器的資料庫的操作。 GDS是一個目錄，用於儲存在長期進程中使用的檔案。

備份模式是伺服器進入的狀態，因此在執行備份過程時，GDS中的檔案不會被清除。 而是在GDS目錄下建立子目錄，以保存保存備份模式結束後要清除的檔案記錄。 檔案可在系統重新啟動後繼續運行，並且可以跨越數天甚至數年。 這些檔案是表單伺服器整體狀態的重要部分，可能包含PDF檔案、原則或表單範本。 如果這些檔案中有任何檔案丟失或損壞，表單伺服器上的進程可能變得不穩定，資料可能丟失。

您可以選擇執行快照備份，通常在備份過程中進入備份模式，然後在完成備份活動後離開備份模式。 需要離開備份模式，以便從GDS中清除檔案，以確保檔案不會不必要地變大。 您可以明確離開備份模式，也可以等待備份模式會話的過期時間。

您還可以將伺服器保留在永久備份模式，這是滾動備份或連續系統涵蓋範圍的備份策略的典型模式。 滾動備份模式表示系統始終處於備份模式，而新備份模式會話在前一會話發佈後立即啟動。 在連續備份模式下，檔案在兩個備份模式會話後被清除，不再被引用。

您可以使用備份和還原服務將建立的應用程式添加到現有應用程式或新應用程式中，以執行連接到表單伺服器的GDS或資料庫的備份。

>[!NOTE]
>
>與AEM Forms實作的任何其他方面一樣，您的備份和復原策略應在開發或測試環境中開發並測試，然後才會用於生產環境，以確保整個解決方案能如預期般運作，而不會造成資料遺失。

您可以使用「備份和還原」服務執行以下任務：

* 進入備份模式。
* 離開備份模式。

>[!NOTE]
>
>如需執行AEM Forms備份時要考慮的詳細資訊，請參閱管理 [說明](https://www.adobe.com/go/learn_aemforms_admin_63)。

>[!NOTE]
>
>如需Backup and Restore服務的詳細資訊，請參閱「AEM Forms的 [服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

## 在表單伺服器上進入備份模式 {#entering-backup-mode-on-the-forms-server}

您進入備份模式以允許對表單伺服器進行熱備份。 當您進入備份模式時，會根據組織的備份程式指定下列資訊：

* 用於標識備份模式會話的唯一標籤，該會話可能對備份過程有用。
* 備份過程完成的時間。
* 用於指示是否處於連續備份模式的標誌，僅當執行滾動備份時，此標籤才有用。

在寫入應用程式以進入備份模式之前，建議您瞭解將表單伺服器置於備份模式後將使用的備份過程。 如需執行AEM Forms備份時要考慮的詳細資訊，請參閱管理 [說明](https://www.adobe.com/go/learn_aemforms_admin_63)。

>[!NOTE]
>
>如需Backup and Restore服務的詳細資訊，請參閱「AEM Forms的 [服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

要建立進入備份模式的應用程式，請執行以下步驟：

1. 包含專案檔案。
1. 建立BackupService客戶端對象。
1. 確定唯一標籤、執行備份的時間，以及是否處於連續備份模式。
1. 進入備份模式。
1. （可選）檢索伺服器上備份模式會話的相關資訊。
1. 執行GDS（全局資料儲存）和資料庫的備份。

**包含專案檔案**

在您的開發專案中加入必要的檔案。 這些檔案必須包含在您的專案中，才能正確編譯程式碼並使用備份與還原服務API。

如需這些檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立BackupService客戶端API對象**

要以寫程式方式離開備份模式，請建立BackupService客戶端對象以使用Backup and Restore Service API。

**確定唯一的標籤，確定執行備份的時間，並決定是否處於連續備份模式**

在進入備份模式之前，您應確定一個唯一的標籤，確定要分配多少時間來執行備份，並決定是否希望表單伺服器保持備份模式。 這些注意事項對於與您組織建立的備份程式整合非常重要。 (請參閱 [管理說明](https://www.adobe.com/go/learn_aemforms_admin_63)。)

**進入備份模式**

使用與組織中的備份過程一致的參數進入備份模式。

**檢索伺服器上備份模式會話的資訊**

進入備份模式後，可以檢索有關會話的資訊。 此資訊可用於與備份過程整合

**執行GDS和資料庫的備份**

成功進入備份模式後，可以執行全局文檔儲存(GDS)和表單伺服器所連接的資料庫的備份。 此步驟是您的組織專屬的，因為您可以手動執行此步驟，也可以執行其他工具來執行備份程式。

### 使用Java API進入備份模式 {#enter-backup-mode-using-the-java-api}

使用備份和還原服務API進入備份模式：

1. 包含專案檔案

   在Java專案的類別路徑中加入必要的用戶端JAR檔案，例如adobe-backup-restore-client-sdk.jar。 要建立Java客戶端應用程式，必須將以下JAR檔案添加到項目的類路徑中：

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar（如果AEM Forms部署在JBoss Application server上，則為必要項）
   * jbossall-client.jar（如果AEM Forms部署在JBoss Application server上，則為必需）

1. 建立BackupService客戶端API對象

   您一起使 `ServiceClientFactory` 用對象和BackupService客戶端API對象。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。 (請參 [閱設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)
   * 使用其 `BackupService` 建構函式並傳遞物件，以建立物 `ServiceClientFactory` 件。

1. 確定唯一的標籤，確定執行備份的時間，並決定是否處於連續備份模式

   確定唯一的標籤，確定要分配多少時間來執行備份，並確定是否希望表單伺服器保持連續備份模式。

1. 進入備份模式

   使用以下參數調用方 `enterBackupMode` 法進入備份模式：

   * 一個 `String` 值，它指定標識備份模式會話的唯一人可讀標籤。 建議您不要使用無法編碼為XML格式的空格或字元。
   * 一 `int` 個值，它指定在備份模式下保持的分鐘數。 您可以指定一個值， `1` 從 `10080` 到（一週內的分鐘數）。 使用連續備份模式時，將忽略此值。
   * 指定 `Boolean` 是否處於連續備份模式的值。 指定為 `True` 處於連續備份模式的值。 在連續備份模式下，您為保持備份模式所指定的分鐘數指定的值將被忽略。

      連續備份模式意味著在完成當前備份模式會話後將啟動新的備份模式會話。 值表示 `False` 不使用連續備份模式，在離開備份模式後，將恢復從GDS中清除檔案。

1. 檢索伺服器上備份模式會話的資訊

   使用調用方 `BackupModeEntryResult` 法後返回的對象檢索 `enterBackupMode` 資訊。 進入備份模式後可檢索的資訊對於與備份過程整合非常有用。 例如，標籤、備份ID和開始時間可作為備份過程檔案名的輸入。

1. 執行GDS和資料庫的備份

   備份Global Document Storage(GDS)和您的表單伺服器所連接的資料庫。 執行備份的動作不屬於AEM Forms SDK的一部分，甚至可能包含貴組織中特定備份程式的手動步驟。

### 使用web service API進入備份模式 {#enter-backup-mode-using-the-web-service-api}

使用Backup and Restore Service API提供的Web服務進入備份模式：

1. 包含專案檔案

   * 建立一個使用備份和還原服務API WSDL的Microsoft .NET客戶端元件。
   * 參考Microsoft .NET客戶端元件。

1. 建立BackupService客戶端API對象

   使用Microsoft .NET客戶端元件，通過調用其缺 `BackupServiceService` 省建構子建立對象，並使用方法指定憑據 `Credentials` 。

1. 確定唯一的標籤，確定執行備份的時間，並決定是否處於連續備份模式

   確定唯一的標籤，確定要分配多少時間來執行備份，並確定是否希望表單伺服器保持連續備份模式。

1. 進入備份模式

   要進入備份模式，請調用enterBackupMode方法並傳遞以下值：

   * 一個 `String` 值，它指定標識備份模式會話的唯一人可讀標籤。 建議您不要使用無法編碼為XML格式的空格或字元。
   * 一 `Uint32` 個值，它指定在備份模式下保持的分鐘數。 您可以指定一個值，從 `1` 到( `10080` 一週內的分鐘數)。 使用連續備份模式時，將忽略此值。
   * 指定 `Boolean` 是否處於連續備份模式的值。 指定為 `True` 處於連續備份模式的值。 在連續備份模式下，您為保持備份模式所指定的分鐘數指定的值將被忽略。 連續備份模式意味著在完成當前備份模式會話後將啟動新的備份模式會話。

      值表示 `False` 不使用連續備份模式，在離開備份模式後，將恢復從GDS中清除檔案。

1. 檢索伺服器上備份模式會話的資訊

   在從BackupModeEntryResult調用enterBackupMode方法後，檢索有關備份模式會話的資訊，該方法返回以驗證其是否成功。 進入備份模式後可檢索的資訊對於與備份過程整合非常有用。 例如，標籤、備份ID和開始時間可作為備份過程檔案名的輸入。

1. 執行GDS和資料庫的備份

   備份Global Document Storage(GDS)和您的表單伺服器所連接的資料庫。 執行備份的動作不屬於AEM Forms SDK的一部分，甚至可能包含貴組織中特定備份程式的手動步驟。

## 在表單伺服器上退出備份模式 {#leaving-backup-mode-on-the-forms-server}

您將保留備份模式，以便表單伺服器繼續從表單伺服器上的GDS（全局文檔儲存）清除檔案。

在您編寫應用程式以進入離開模式之前，建議您瞭解AEM Forms使用的備份程式。 如需執行AEM Forms備份時要考慮的詳細資訊，請參閱管理 [說明](https://www.adobe.com/go/learn_aemforms_admin_63)。

>[!NOTE]
>
>如需Backup and Restore服務的詳細資訊，請參閱「AEM Forms的 [服務參考」](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

要離開備份模式，請執行以下步驟：

1. 包含專案檔案。
1. 建立BackupService客戶端對象。
1. 離開備份模式。
1. （可選）擷取在表單伺服器上執行之備份模式作業的相關資訊。

**包含專案檔案**

在您的開發專案中包含所有必要的檔案。 這些檔案對於正確編譯程式碼和使用備份與還原服務API非常重要。

如需這些檔案位置的詳細資訊，請參 [閱「包含AEM Forms java程式庫檔案」](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立BackupService客戶端API對象**

要以寫程式方式離開備份模式，請建立BackupService客戶端對象以使用Backup and Restore Service API。

**離開備份模式**

保留備份模式以繼續從全局文檔儲存(GDS)中正常清除檔案。 在離開備份模式之前，您應驗證備份過程是否已完成。

**檢索有關已結束的備份模式會話的資訊**

離開備份模式後，可以檢索有關會話的資訊。 此資訊可用於與備份過程整合。

### 使用Java API保留備份模式 {#leave-backup-mode-using-the-java-api}

使用備份和還原服務API(Java)使備份模式保持不變：

1. 包含專案檔案

   在Java專案的類別路徑中加入必要的用戶端JAR檔案，例如adobe-backup-restore-client-sdk.jar。 要建立Java客戶端應用程式，必須將以下JAR檔案添加到項目的類路徑中：

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar（如果AEM Forms部署在JBoss Application server上，則為必要項）
   * jbossall-client.jar（如果AEM Forms部署在JBoss Application server上，則為必需）

1. 建立BackupService客戶端API對象

   您一起使 `ServiceClientFactory` 用對象和BackupService客戶端API對象。

   * 建立包 `ServiceClientFactory` 含連接屬性的對象。 (請參 [閱設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)
   * 使用其 `BackupService` 建構函式並將物件傳遞為參數，以 `ServiceClientFactory` 建立物件。

1. 進入備份模式

   通過調用方法使備份模式保 `leaveBackupMode` 持不變。

1. 檢索伺服器上備份模式會話的資訊

   使用返回的對象檢索有關 `BackupModeResult` 操作的資訊。 進入備份模式後可檢索的資訊對於與備份過程整合非常有用。 例如，標籤、備份ID和開始時間可作為備份過程檔案名的輸入。

### 使用web service API離開備份模式 {#leave-backup-mode-using-the-web-service-api}

使用備份和還原服務API（web服務）保持備份模式：

1. 包含專案檔案

   若要使用web services，您必須確定已包含proxy檔案。 請依照下列步驟來設定您的專案，將備份與還原服務API當做web service。

   * 建立一個使用備份和還原服務API WSDL的Microsoft .NET客戶端元件。
   * 參考Microsoft .NET客戶端元件。

1. 建立BackupService客戶端API對象

   使用Microsoft .NET客戶端元件，通過調用其缺 `BackupServiceService` 省建構子建立對象。

1. 進入備份模式

   通過調用Web服務操作， `leaveBackupMode` 使備份模式保持不變。

1. 檢索伺服器上備份模式會話的資訊

   在操作後檢索備份模式標識符，以驗證其是否成功。 在離開備份模式後可以檢索的資訊對於與備份過程整合非常有用。

