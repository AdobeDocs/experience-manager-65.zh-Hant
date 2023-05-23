---
title: 準備AEM Forms備份
seo-title: Preparing AEM Forms for Backup
description: 瞭解如何使用備份和還原服務來使用Java API和Web服務API進入和離開AEM Forms伺服器的備份模式。
seo-description: Learn how to use the Backup and Restore service to enter and leave the Backup mode for AEM Forms server using the Java API and the Web Service API.
uuid: b8ef2bed-62e2-4000-b55a-30d2fc398a5f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e747147e-e96d-43c7-87b3-55947eef81f5
role: Developer
exl-id: aeab003d-ba64-4760-9c56-44638501e9ff
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2520'
ht-degree: 0%

---

# 準備AEM Forms備份 {#preparing-aem-forms-for-backup}

**本文檔中的示例和示例僅針對AEM Forms的JEE環境。**

## 關於備份和恢復服務 {#about-the-backup-and-restore-service}

備份和還原服務允許您將AEM Forms *備份模式*&#x200B;執行熱備份。 備份和還原服務實際上不會執行AEM Forms備份或還原系統。 相反，它使伺服器處於一種狀態，以便進行一致且可靠的備份，同時允許伺服器繼續運行。 您負責執行備份全局文檔儲存(GDS)和連接到表單伺服器的資料庫的操作。 GDS是用於儲存在長生命週期進程中使用的檔案的目錄。

備份模式是伺服器進入的狀態，因此在執行備份過程時不會清除GDS中的檔案。 相反，在GDS目錄下建立子目錄，以在保存備份模式結束後維護要清除的檔案記錄。 檔案旨在使系統重新啟動後能夠繼續運行，並且可以跨越數天甚至數年。 這些檔案是表單伺服器整體狀態的關鍵部分，可能包括PDF檔案、策略或表單模板。 如果這些檔案中的任何檔案丟失或損壞，表單伺服器上的進程可能變得不穩定，資料可能丟失。

您可以選擇執行快照備份，通常在備份過程中進入一段時間的備份模式，然後在完成備份活動後退出備份模式。 需要離開備份模式，以便從GDS中清除檔案，以確保檔案不會不必要地增大。 您可以明確地離開備份模式，也可以等待備份模式會話中的時間過期。

您還可以將伺服器置於永久備份模式，這是滾動備份或連續系統覆蓋的備份策略的典型模式。 滾動備份模式表示系統始終處於備份模式，在上一個會話發佈後立即啟動新的備份模式會話。 在連續備份模式下，檔案在兩個備份模式會話後被清除，不再被引用。

可以使用備份和恢復服務將您建立的現有應用程式或新應用程式添加到其中，以執行連接到表單伺服器的GDS或資料庫的備份。

>[!NOTE]
>
>與您AEM Forms實施的任何其他方面一樣，在將備份和恢復策略用於生產之前，應在開發或試運行環境中進行開發和測試，以確保整個解決方案能夠按預期工作而不丟失資料。

可以使用「備份和還原」服務執行以下任務：

* 進入備份模式。
* 退出備份模式。

>[!NOTE]
>
>有關執行AEM Forms備份時應考慮的內容的詳細資訊，請參見 [管理幫助](https://www.adobe.com/go/learn_aemforms_admin_63)。

>[!NOTE]
>
>有關備份和還原服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

## 在表單伺服器上進入備份模式 {#entering-backup-mode-on-the-forms-server}

您進入備份模式以允許對表單伺服器進行熱備份。 進入備份模式時，根據組織的備份過程指定以下資訊：

* 標識備份模式會話的唯一標籤，該會話可能對您的備份過程有用。
* 備份過程完成的時間。
* 指示是否處於連續備份模式的標誌，只有在執行滾動備份時，該標誌才有用。

在將應用程式寫入備份模式之前，建議您瞭解在將表單伺服器置於備份模式之後將使用的備份過程。 有關執行AEM Forms備份時應考慮的內容的詳細資訊，請參見 [管理幫助](https://www.adobe.com/go/learn_aemforms_admin_63)。

>[!NOTE]
>
>有關備份和還原服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary-of-steps}

要建立進入備份模式的應用程式，請執行以下步驟：

1. 包括項目檔案。
1. 建立BackupService客戶端對象。
1. 確定唯一標籤、執行備份的時間以及是否處於連續備份模式。
1. 進入備份模式。
1. （可選）檢索有關伺服器上備份模式會話的資訊。
1. 執行GDS（全局資料儲存）和資料庫的備份。

**包括項目檔案**

在開發項目中包括必要的檔案。 這些檔案對於正確編譯代碼和使用備份和恢復服務API在項目中包含非常重要。

有關這些檔案位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立BackupService客戶端API對象**

要以寫程式方式退出備份模式，請建立BackupService客戶端對象以使用Backup and Restore Service API。

**確定唯一的標籤，確定執行備份的時間，並決定是否處於連續備份模式**

在進入備份模式之前，您應確定一個唯一標籤，確定要分配多少時間來執行備份，並決定是否希望表單伺服器保持備份模式。 這些注意事項對於與您的組織建立的備份過程整合非常重要。 (請參閱 [管理幫助](https://www.adobe.com/go/learn_aemforms_admin_63)。)

**進入備份模式**

進入備份模式，其參數與組織中的備份過程一致。

**檢索有關伺服器上備份模式會話的資訊**

進入備份模式後，可以檢索有關會話的資訊。 此資訊可用於與備份過程整合

**執行GDS和資料庫的備份**

成功進入備份模式後，可以執行全局文檔儲存(GDS)和表單伺服器所連接的資料庫的備份。 此步驟特定於您的組織，因為您可以手動執行此步驟，也可以運行其他工具來執行備份過程。

### 使用Java API進入備份模式 {#enter-backup-mode-using-the-java-api}

使用備份和還原服務API進入備份模式：

1. 包括項目檔案

   在Java項目的類路徑中包括必要的客戶端JAR檔案，如adobe-backup-restore-client-sdk.jar。 要建立Java客戶端應用程式，必須將以下JAR檔案添加到項目的類路徑中：

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)
   * jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)

1. 建立BackupService客戶端API對象

   使用 `ServiceClientFactory` 對象和BackupService客戶端API對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。 (請參閱 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)
   * 建立 `BackupService` 使用其建構子並傳遞對象 `ServiceClientFactory` 的雙曲餘切值。

1. 確定唯一的標籤，確定執行備份的時間，並決定是否處於連續備份模式

   確定唯一的標籤，確定要分配的時間以執行備份，並決定是否希望表單伺服器保持連續備份模式。

1. 進入備份模式

   通過調用 `enterBackupMode` 方法，其參數如下：

   * A `String` 值，它指定標識備份模式會話的唯一可人讀標籤。 建議不要使用無法編碼為XML格式的空格或字元。
   * 安 `int` 指定在備份模式中停留的分鐘數的值。 可以指定值 `1` 至 `10080` （一週內的分鐘數）。 使用連續備份模式時將忽略此值。
   * A `Boolean` 指定是否處於連續備份模式的值。 值 `True` 指定處於連續備份模式。 在連續備份模式下，將忽略您為在備份模式下停留的分鐘數指定的值。

      連續備份模式意味著在完成當前備份模式會話後啟動新的備份模式會話。 值 `False` 表示不使用連續備份模式，在離開備份模式後，將恢復從GDS清除檔案。

1. 檢索有關伺服器上備份模式會話的資訊

   使用 `BackupModeEntryResult` 調用後返回的對象 `enterBackupMode` 的雙曲餘切值。 進入備份模式後可以檢索的資訊對於與備份過程整合可能非常有用。 例如，標籤、備份ID和開始時間可能作為備份過程檔案名的輸入。

1. 執行GDS和資料庫的備份

   備份全局文檔儲存(GDS)和窗體伺服器所連接的資料庫。 執行備份的操作不是AEM FormsSDK的一部分，甚至可能包括特定於您組織中備份過程的手動步驟。

### 使用Web服務API進入備份模式 {#enter-backup-mode-using-the-web-service-api}

使用Backup and Restore Service API提供的Web服務進入備份模式：

1. 包括項目檔案

   * 建立使用備份和還原服務API WSDL的Microsoft.NET客戶端程式集。
   * 引用Microsoft.NET客戶端程式集。

1. 建立BackupService客戶端API對象

   使用Microsoft.NET客戶端程式集，建立 `BackupServiceService` 通過調用其預設建構子來指定對象，並使用 `Credentials` 的雙曲餘切值。

1. 確定唯一的標籤，確定執行備份的時間，並決定是否處於連續備份模式

   確定唯一的標籤，確定要分配的時間以執行備份，並決定是否希望表單伺服器保持連續備份模式。

1. 進入備份模式

   要進入備份模式，請調用enterBackupMode方法並傳遞以下值：

   * A `String` 值，它指定標識備份模式會話的唯一可人讀標籤。 建議不要使用無法編碼為XML格式的空格或字元。
   * A `Uint32` 指定在備份模式中停留的分鐘數的值。 可以指定值 `1` 至 `10080` （一週內的分鐘數）。 使用連續備份模式時將忽略此值。
   * A `Boolean` 指定是否處於連續備份模式的值。 值 `True` 指定處於連續備份模式。 在連續備份模式下，將忽略您為在備份模式下停留的分鐘數指定的值。 連續備份模式意味著在完成當前備份模式會話後啟動新的備份模式會話。

      值 `False` 表示不使用連續備份模式，在離開備份模式後，將恢復從GDS清除檔案。

1. 檢索有關伺服器上備份模式會話的資訊

   在從BackupModeEntryResult調用enterBackupMode方法後檢索有關備份模式會話的資訊，返回該方法以驗證其是否成功。 進入備份模式後可以檢索的資訊對於與備份過程整合可能非常有用。 例如，標籤、備份ID和開始時間可能作為備份過程檔案名的輸入。

1. 執行GDS和資料庫的備份

   備份全局文檔儲存(GDS)和窗體伺服器所連接的資料庫。 執行備份的操作不是AEM FormsSDK的一部分，甚至可能包括特定於您組織中備份過程的手動步驟。

## 在表單伺服器上退出備份模式 {#leaving-backup-mode-on-the-forms-server}

您可以退出備份模式，以便表單伺服器從表單伺服器上的GDS（全局文檔儲存）恢復清除檔案。

在編寫應用程式進入離開模式之前，建議您瞭解與AEM Forms一起使用的備份過程。 有關執行AEM Forms備份時應考慮的內容的詳細資訊，請參見 [管理幫助](https://www.adobe.com/go/learn_aemforms_admin_63)。

>[!NOTE]
>
>有關備份和還原服務的詳細資訊，請參見 [《AEM Forms服務參考》](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步驟摘要 {#summary_of_steps-1}

要退出備份模式，請執行以下步驟：

1. 包括項目檔案。
1. 建立BackupService客戶端對象。
1. 退出備份模式。
1. （可選）檢索有關在表單伺服器上運行的備份模式會話的資訊。

**包括項目檔案**

在開發項目中包括所有必要的檔案。 這些檔案對於正確編譯代碼和使用備份和恢復服務API非常重要。

有關這些檔案位置的資訊，請參見 [包括AEM FormsJava庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**建立BackupService客戶端API對象**

要以寫程式方式退出備份模式，請建立BackupService客戶端對象以使用Backup and Restore Service API。

**退出備份模式**

保留備份模式以繼續從全局文檔儲存(GDS)中正常清除檔案。 在退出備份模式之前，應驗證備份過程是否已完成。

**檢索有關已結束的備份模式會話的資訊**

退出備份模式後，可以檢索有關會話的資訊。 此資訊可用於與備份過程整合。

### 使用Java API退出備份模式 {#leave-backup-mode-using-the-java-api}

使用備份和還原服務API(Java)退出備份模式：

1. 包括項目檔案

   在Java項目的類路徑中包括必要的客戶端JAR檔案，如adobe-backup-restore-client-sdk.jar。 要建立Java客戶端應用程式，必須將以下JAR檔案添加到項目的類路徑中：

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)
   * jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，則為必需)

1. 建立BackupService客戶端API對象

   使用 `ServiceClientFactory` 對象和BackupService客戶端API對象。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。 (請參閱 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。)
   * 建立 `BackupService` 使用其建構子並傳遞對象 `ServiceClientFactory` 對象。

1. 進入備份模式

   通過調用 `leaveBackupMode` 的雙曲餘切值。

1. 檢索有關伺服器上備份模式會話的資訊

   使用 `BackupModeResult` 返回的對象。 進入備份模式後可以檢索的資訊對於與備份過程整合可能非常有用。 例如，標籤、備份ID和開始時間可能作為備份過程檔案名的輸入。

### 使用Web服務API退出備份模式 {#leave-backup-mode-using-the-web-service-api}

使用備份和還原服務API（Web服務）退出備份模式：

1. 包括項目檔案

   要使用Web服務，必須確保包含代理檔案。 按照以下步驟配置項目，將備份和還原服務API用作Web服務。

   * 建立使用備份和還原服務API WSDL的Microsoft.NET客戶端程式集。
   * 引用Microsoft.NET客戶端程式集。

1. 建立BackupService客戶端API對象

   使用Microsoft.NET客戶端程式集，建立 `BackupServiceService` 調用其預設建構子。

1. 進入備份模式

   通過調用 `leaveBackupMode` Web服務操作。

1. 檢索有關伺服器上備份模式會話的資訊

   在操作後檢索備份模式標識符以驗證其是否成功。 退出備份模式後可以檢索的資訊對於與備份過程整合可能非常有用。
