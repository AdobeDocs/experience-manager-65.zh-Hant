---
title: 準備AEM Forms備份
seo-title: Preparing AEM Forms for Backup
description: 了解如何使用備份和還原服務，使用Java API和Web服務API進入並離開AEM Forms伺服器的備份模式。
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

**本檔案中的範例和範例僅適用於JEE環境上的AEM Forms。**

## 關於備份和還原服務 {#about-the-backup-and-restore-service}

備份和還原服務可讓您將AEM Forms *備份模式*，可執行熱備份。 備份和還原服務實際上不會執行AEM Forms備份或還原系統。 相反，它使您的伺服器處於一個狀態，以便進行一致且可靠的備份，同時允許您的伺服器繼續運行。 您負責備份全局文檔儲存(GDS)和連接到表單伺服器的資料庫的操作。 GDS是一個目錄，用於儲存在長期進程中使用的檔案。

備份模式是伺服器進入的狀態，這樣在備份過程進行時，GDS中的檔案就不會被清除。 而是在GDS目錄下建立子目錄，以維護儲存備份模式結束後要清除的檔案記錄。 檔案旨在使系統重新啟動並可跨越數天，甚至數年。 這些檔案是表單伺服器整體狀態的關鍵部分，可能包括PDF檔案、策略或表單模板。 如果這些檔案中的任何一個丟失或損壞，則表單伺服器上的進程可能變得不穩定，資料可能丟失。

您可以選擇執行快照備份，在備份過程中通常會在一段時間內進入備份模式，然後在完成備份活動後離開備份模式。 需要保留備份模式，以便從GDS中清除檔案，以確保檔案不會不必要地增大。 您可以明確地離開備份模式，或等待備份模式會話的時間過期。

您還可以將伺服器保留在永久備份模式，這是滾動備份或連續系統覆蓋的備份策略的典型模式。 滾動備份模式表示系統始終處於備份模式，在釋放前一個會話時立即啟動新備份模式會話。 在連續備份模式下，檔案將在兩個備份模式會話後清除，不再被引用。

您可以使用備份和還原服務將現有應用程式或新應用程式添加到您建立的應用程式中，以執行連接到表單伺服器的GDS或資料庫的備份。

>[!NOTE]
>
>與AEM Forms實施的任何其他方面一樣，您的備份和恢復策略應在開發或測試環境中開發和測試，然後才用於生產環境，以確保整個解決方案能夠正常工作，不會丟失資料。

您可以使用備份和還原服務執行以下任務：

* 進入備份模式。
* 離開備份模式。

>[!NOTE]
>
>有關為AEM Forms執行備份時應考慮哪些事項的詳細資訊，請參見 [管理說明](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>有關備份和還原服務的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

## 在表單伺服器上進入備份模式 {#entering-backup-mode-on-the-forms-server}

您進入備份模式以允許對表單伺服器進行熱備份。 進入備份模式時，根據貴組織的備份過程指定以下資訊：

* 標識備份模式會話的唯一標籤，該會話可能對您的備份過程有用。
* 完成備份過程的時間。
* 指示是否處於連續備份模式的標誌，只有在執行滾動備份時才有用。

在將應用程式寫入備份模式之前，建議您了解將表單伺服器置於備份模式後將使用的備份過程。 有關為AEM Forms執行備份時應考慮哪些事項的詳細資訊，請參見 [管理說明](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>有關備份和還原服務的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary-of-steps}

要建立進入備份模式的應用程式，請執行以下步驟：

1. 包含專案檔案。
1. 建立BackupService客戶端對象。
1. 確定唯一的標籤、執行備份的時間，以及是否處於連續備份模式。
1. 進入備份模式。
1. （可選）檢索伺服器上備份模式會話的相關資訊。
1. 執行GDS（全局資料儲存）和資料庫的備份。

**包含項目檔案**

在您的開發專案中加入必要的檔案。 這些檔案對於在您的項目中包括以正確編譯代碼和使用備份和還原服務API非常重要。

如需這些檔案的位置資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立BackupService客戶端API對象**

要以寫程式方式離開備份模式，請建立一個BackupService客戶端對象以使用備份和還原服務API。

**確定唯一的標籤，確定執行備份的時間，並決定是否處於連續備份模式**

在進入備份模式之前，您應決定一個唯一標籤，確定要分配多少時間執行備份，並決定是否希望表單伺服器保持備份模式。 這些注意事項對於與貴組織建立的備份過程整合非常重要。 (請參閱 [管理說明](https://www.adobe.com/go/learn_aemforms_admin_63).)

**進入備份模式**

使用與貴組織的備份過程一致的參數進入備份模式。

**檢索伺服器上備份模式會話的相關資訊**

進入備份模式後，可以檢索有關會話的資訊。 此資訊可用於與備份過程整合

**執行GDS和資料庫的備份**

成功進入備份模式後，可以執行全局文檔儲存(GDS)和表單伺服器所連接的資料庫的備份。 此步驟特定於您的組織，因為您可以手動執行此步驟，或者可以運行其他工具來執行備份過程。

### 使用Java API進入備份模式 {#enter-backup-mode-using-the-java-api}

使用「備份和還原服務API」進入備份模式：

1. 包含項目檔案

   在您Java專案的類別路徑中，加入必要的用戶端JAR檔案，例如adobe-backup-restore-client-sdk.jar。 要建立Java客戶端應用程式，必須將以下JAR檔案添加到項目的類路徑中：

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar(若AEM Forms部署在JBoss Application Server上則為必要)
   * jbossall-client.jar(若AEM Forms部署在JBoss Application Server上則為必要)

1. 建立BackupService客戶端API對象

   您使用 `ServiceClientFactory` 對象和BackupService客戶端API對象一起。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。 (請參閱 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * 建立 `BackupService` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件。

1. 確定唯一的標籤，確定執行備份的時間，並決定是否處於連續備份模式

   決定唯一的標籤，決定要分配多少時間執行備份，並決定是否希望表單伺服器保持連續備份模式。

1. 進入備份模式

   通過調用 `enterBackupMode` 方法，並搭配下列參數：

   * A `String` 值，指定標識備份模式會話的唯一人類可讀標籤。 建議您不要使用無法編碼為XML格式的空格或字元。
   * 安 `int` 指定在備份模式下保持的分鐘數的值。 您可以從 `1` to `10080` （一週內的分鐘數）。 使用連續備份模式時，會忽略此值。
   * A `Boolean` 指定是否處於連續備份模式的值。 值 `True` 指定為處於連續備份模式。 在連續備份模式下，您為要保持在備份模式下的分鐘數指定的值將被忽略。

      連續備份模式表示在完成當前備份模式會話後將啟動新的備份模式會話。 值 `False` 表示不使用連續備份模式，在離開備份模式後，恢復從GDS中清除檔案。

1. 檢索伺服器上備份模式會話的相關資訊

   使用 `BackupModeEntryResult` 調用 `enterBackupMode` 方法。 進入備份模式後可檢索的資訊對於與備份過程整合可能非常有用。 例如，標籤、備份ID和開始時間可能作為備份過程檔案名的輸入而非常有用。

1. 執行GDS和資料庫的備份

   備份全局文檔儲存(GDS)和您的表單伺服器所連接的資料庫。 執行備份的動作不屬於AEM Forms SDK，甚至可能包括貴組織中備份程式專用的手動步驟。

### 使用Web服務API進入備份模式 {#enter-backup-mode-using-the-web-service-api}

使用Backup and Restore Service API提供的Web服務進入備份模式：

1. 包含項目檔案

   * 建立使用備份和還原服務API WSDL的Microsoft .NET客戶端程式集。
   * 參考Microsoft .NET客戶端程式集。

1. 建立BackupService客戶端API對象

   使用Microsoft .NET客戶端程式集，建立 `BackupServiceService` 對象，方法是調用其預設建構子，並使用 `Credentials` 方法。

1. 確定唯一的標籤，確定執行備份的時間，並決定是否處於連續備份模式

   決定唯一的標籤，決定要分配多少時間執行備份，並決定是否希望表單伺服器保持連續備份模式。

1. 進入備份模式

   要進入備份模式，請調用enterBackupMode方法並傳遞以下值：

   * A `String` 值，指定標識備份模式會話的唯一人類可讀標籤。 建議您不要使用無法編碼為XML格式的空格或字元。
   * A `Uint32` 指定在備份模式下保持的分鐘數的值。 您可以從 `1` to `10080` （一週內的分鐘數）。 使用連續備份模式時，會忽略此值。
   * A `Boolean` 指定是否處於連續備份模式的值。 值 `True` 指定為處於連續備份模式。 在連續備份模式下，您為要保持在備份模式下的分鐘數指定的值將被忽略。 連續備份模式表示在完成當前備份模式會話後將啟動新的備份模式會話。

      值 `False` 表示不使用連續備份模式，在離開備份模式後，恢復從GDS中清除檔案。

1. 檢索伺服器上備份模式會話的相關資訊

   從返回以驗證其是否成功的BackupModeEntryResult中調用enterBackupMode方法之後，檢索有關備份模式會話的資訊。 進入備份模式後可檢索的資訊對於與備份過程整合可能非常有用。 例如，標籤、備份ID和開始時間可能作為備份過程檔案名的輸入而非常有用。

1. 執行GDS和資料庫的備份

   備份全局文檔儲存(GDS)和您的表單伺服器所連接的資料庫。 執行備份的動作不屬於AEM Forms SDK，甚至可能包括貴組織中備份程式專用的手動步驟。

## 在表單伺服器上保留備份模式 {#leaving-backup-mode-on-the-forms-server}

您可以保留備份模式，以便表單伺服器恢復從表單伺服器上的GDS（全局文檔儲存）清除檔案。

在將應用程式寫入到離開模式之前，建議您了解與AEM Forms一起使用的備份過程。 有關為AEM Forms執行備份時應考慮哪些事項的詳細資訊，請參見 [管理說明](https://www.adobe.com/go/learn_aemforms_admin_63).

>[!NOTE]
>
>有關備份和還原服務的詳細資訊，請參見 [AEM Forms服務參考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步驟摘要 {#summary_of_steps-1}

要退出備份模式，請執行以下步驟：

1. 包含專案檔案。
1. 建立BackupService客戶端對象。
1. 離開備份模式。
1. （可選）檢索有關表單伺服器上運行的備份模式會話的資訊。

**包含項目檔案**

在您的開發專案中包含所有必要的檔案。 這些檔案對於正確編譯代碼以及使用備份和還原服務API非常重要。

如需這些檔案的位置資訊，請參閱 [包含AEM Forms Java程式庫檔案](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**建立BackupService客戶端API對象**

要以寫程式方式離開備份模式，請建立一個BackupService客戶端對象以使用備份和還原服務API。

**離開備份模式**

保留備份模式以繼續正常清除全局文檔儲存(GDS)中的檔案。 在離開備份模式之前，您應驗證備份過程已完成。

**檢索有關已結束的備份模式會話的資訊**

離開備份模式後，可以檢索有關會話的資訊。 此資訊可用於與備份過程整合。

### 使用Java API保留備份模式 {#leave-backup-mode-using-the-java-api}

使用備份和還原服務API(Java)保留備份模式：

1. 包含項目檔案

   在您Java專案的類別路徑中，加入必要的用戶端JAR檔案，例如adobe-backup-restore-client-sdk.jar。 要建立Java客戶端應用程式，必須將以下JAR檔案添加到項目的類路徑中：

   * adobe-backup-restore-client-sdk.jar
   * adobe-livecycle-client.jar
   * adobe-usermanager-client.jar
   * adobe-utilities.jar(若AEM Forms部署在JBoss Application Server上則為必要)
   * jbossall-client.jar(若AEM Forms部署在JBoss Application Server上則為必要)

1. 建立BackupService客戶端API對象

   您使用 `ServiceClientFactory` 對象和BackupService客戶端API對象一起。

   * 建立 `ServiceClientFactory` 包含連接屬性的對象。 (請參閱 [設定連接屬性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * 建立 `BackupService` 對象，使用其建構子並傳遞 `ServiceClientFactory` 物件作為參數。

1. 進入備份模式

   調用 `leaveBackupMode` 方法。

1. 檢索伺服器上備份模式會話的相關資訊

   使用 `BackupModeResult` 傳回的物件。 進入備份模式後可檢索的資訊對於與備份過程整合可能非常有用。 例如，標籤、備份ID和開始時間可能作為備份過程檔案名的輸入而非常有用。

### 使用Web服務API保留備份模式 {#leave-backup-mode-using-the-web-service-api}

使用備份和還原服務API（Web服務）保留備份模式：

1. 包含項目檔案

   若要使用Web服務，您必須確定包含Proxy檔案。 請依照下列步驟來設定您的專案，以使用備份和還原服務API作為Web服務。

   * 建立使用備份和還原服務API WSDL的Microsoft .NET客戶端程式集。
   * 參考Microsoft .NET客戶端程式集。

1. 建立BackupService客戶端API對象

   使用Microsoft .NET客戶端程式集，建立 `BackupServiceService` 對象，方法是調用其預設建構子。

1. 進入備份模式

   調用 `leaveBackupMode` 網站服務操作。

1. 檢索伺服器上備份模式會話的相關資訊

   在操作之後檢索備份模式標識符，以驗證其是否成功。 離開備份模式後可以檢索的資訊對於與備份過程整合可能非常有用。
