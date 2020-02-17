---
title: 增強應用程式伺服器效能
seo-title: 增強應用程式伺服器效能
description: 本檔案說明可供您設定的選用設定，以改善AEM Forms應用程式伺服器的效能。
seo-description: 本檔案說明可供您設定的選用設定，以改善AEM Forms應用程式伺服器的效能。
uuid: 88d2f96a-3b59-410d-8160-20581d27acad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fad65765-d56d-4a9f-82d5-bcceb1758953
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 增強應用程式伺服器效能{#enhancing-application-server-performance}

此內容說明您可設定的選用設定，以改善AEM表單應用程式伺服器的效能。

## 配置應用程式伺服器資料源 {#configuring-application-server-data-sources}

AEM表單會使用AEM表單儲存庫做為其資料來源。 AEM表單儲存庫會儲存應用程式資產，而且在執行時期，服務可從儲存庫擷取資產，以完成自動化商業程式。

根據您執行的AEM表單模組數目和存取應用程式的並行使用者人數，資料來源的存取權可能相當重要。 使用連接集區可以優化資料源訪問。 *連接集區* (Connection pooling)是一種技術，用於避免每次應用程式或伺服器對象需要訪問資料庫時建立新資料庫連接的開銷。 連線集區通常用於網路和企業應用程式，通常由應用程式伺服器處理，但不限於應用程式伺服器。

請務必正確配置連接池參數，以便您永不斷開連接，這會導致應用程式效能惡化。

要正確配置連接池設定，應用程式伺服器管理員必須在一天的尖峰時段監視連接池。 監控可確保應用程式和用戶隨時都能獲得足夠的連接。 大部分的應用程式伺服器都包含監控工具。

您可以使用WebLogic伺服器管理控制台監視域中每個JDBC資料源實例的各種統計資訊。 如需詳細資訊，請參閱WebLogic檔案。

當應用程式伺服器管理員確定正確的連接池設定時，該用戶必須將此資訊通知資料庫管理員。 資料庫管理員需要此資訊，因為資料庫連接數等於資料源的連接池中的連接數。 然後，請完成以下步驟，為應用程式伺服器和資料源類型配置連接池設定。

### 為Oracle和MySQL的WebLogic配置連接池設定 {#configure-connection-pool-settings-for-weblogic-for-oracle-and-mysql}

1. 在「域結構」下，按一下「服務」>「JDBC」>「資料源」，然後在右窗格中按一下「IDP_DS」。
1. 在下一個螢幕中，按一下「配置」>「連接池」頁籤，然後在以下框中輸入值：

   * 初始容量
   * 最大容量
   * 容量增加
   * 語句快取大小

1. 按一下「儲存」，然後按一下「啟用變更」。
1. 重新啟動WebLogic受控伺服器。

### 為SQLServer的WebLogic配置連接池設定 {#configure-connection-pool-settings-for-weblogic-for-sqlserver}

1. 在「變更中心」下，按一下「鎖定與編輯」。
1. 在「域結構」下，按一下「服務」>「JDBC」>「資料源」，然後在右窗格中按一下「EDC_DS」。
1. 在下一個螢幕中，按一下「配置」>「連接池」頁籤，然後在以下框中輸入值：

   * 初始容量
   * 最大容量
   * 容量增加
   * 語句快取大小

1. 按一下「儲存」，然後按一下「啟用變更」。
1. 重新啟動WebLogic受控伺服器。

### 為DB2的WebSphere配置連接池設定 {#configure-connection-pool-settings-for-websphere-for-db2}

1. 在導航樹中，按一下「資源」>「JDBC」>「JDBC提供程式」。 在右窗格中，按一下您建立的資料源，即DB2通用JDBC驅動程式提供程式或LiveCycle - db2 - IDP_DS。
1. 在「其他屬性」下，按一下「資料來源」，然後選取IDP_DS。
1. 在下一個螢幕的「Additional Properties（附加屬性）」下，按一下「Connection Pool Properties（連接池屬性）」 ，然後在「Maximum Connections（最大連接）」框和「Minimum Connections（最小連接）」框中輸入值。
1. 按一下「確定」或「應用」，然後按一下「直接保存到主配置」。

### 為WebSphere for oracle配置連接池設定 {#configure-connection-pool-settings-for-websphere-for-oracle}

1. 在導航樹中，按一下「資源」>「JDBC」>「JDBC提供程式」。 在右窗格中，按一下您建立的Oracle JDBC驅動程式資料源。
1. 在「其他屬性」下，按一下「資料來源」，然後選取IDP_DS。
1. 在下一個螢幕的「Additional Properties（附加屬性）」下，按一下「Connection Pool Properties（連接池屬性）」 ，然後在「Maximum Connections（最大連接）」框和「Minimum Connections（最小連接）」框中輸入值。
1. 按一下「確定」或「應用」，然後按一下「直接保存到主配置」。

### 為SqlServer的WebSphere配置連接池設定 {#configure-connection-pool-settings-for-websphere-for-sqlserver}

1. 在導航樹中，按一下「資源」>「JDBC」>「JDBC提供程式」，然後在右窗格中按一下您建立的用戶定義JDBC驅動程式資料源。
1. 在「其他屬性」下，按一下「資料來源」，然後選取IDP_DS。
1. 在下一個螢幕的「Additional Properties（附加屬性）」下，按一下「Connection Pool Properties（連接池屬性）」 ，然後在「Maximum Connections（最大連接數）」框和「Minimum Connections（最小連接數）」框中輸入值：
1. 按一下「確定」或「應用」，然後按一下「直接保存到主配置」。

## 最佳化內嵌檔案並對JVM記憶體的影響 {#optimizing-inline-documents-and-impact-on-jvm-memory}

如果您通常處理的檔案大小相對較小，則可以改善與檔案傳輸速度和儲存空間相關的效能。 若要這麼做，請實作下列AEM表單產品設定：

* 增加AEM表單的預設檔案最大內嵌大小，使其大於大部分檔案的大小。
* 要處理較大的檔案，請指定高速磁碟系統或RAM磁碟上的儲存目錄。

管理控制台中已設定最大內嵌大小和儲存目錄（AEM表單暫存檔案目錄和GDS目錄）。

### 檔案大小和最大內嵌大小 {#document-size-and-maximum-inline-size}

當AEM表單所傳送的檔案小於或等於預設檔案的最大內嵌大小時，檔案會內嵌儲存在伺服器上，而檔案會以Adobe檔案物件的形式序列化。 將檔案內嵌儲存可大幅提升效能。 不過，如果您使用表單工作流程，內容也可能會儲存在資料庫中，以利追蹤。 因此，增加最大內嵌大小可能會影響資料庫大小。

大於最大內嵌大小的文檔儲存在本地檔案系統上。 傳輸至伺服器和從伺服器傳輸的Adobe Document物件只是該檔案的指標。

當內嵌檔案內容時（即小於最大內嵌大小），內容會儲存在資料庫中，作為檔案序列化裝載的一部分。 因此，增加最大內嵌大小可能會影響資料庫大小。

**變更最大內嵌大小**

1. 在管理控制台中，按一下「設定>核心繫統設定>組態」。
1. 在「預設文檔最大內嵌大小」框中輸入值，然後按一下「確定」。

   >[!NOTE]
   >
   >對於JEE環境上的AEM Forms和OSGi Bundle上的AEM Forms,Document Max Inline Size屬性的值必須相同，JEE環境上的AEM Forms會包含AEM Forms。 此步驟僅更新JEE環境上的AEM Forms值，而不更新OSGi Bundle上的AEM Forms包含JEE環境上的AEM Forms值。

1. 使用以下系統屬性重新啟動應用程式伺服器：

   com.adobe.idp.defaultDocumentMaxInlineSize=步驟2中&#x200B;[*指定的值*]

   >[!NOTE]
   >
   >上述系統屬性會覆寫JEE環境上AEM Forms和OSGi Bundle上AEM Forms的Document Max Inline Size屬性集的值，JEE環境上包含AEM Forms。

>[!NOTE]
>
>預設的最大內嵌大小為65536位元組。

### JVM最大堆大小 {#jvm-maximum-heap-size}

增加最大內嵌大小需要更多記憶體來儲存序列化文檔。 因此，它通常也需要增加JVM的最大堆大小。

處理許多文檔的重載系統可快速使JVM堆記憶體飽和。 為避免OutOfMemoryError，請將JVM最大堆大小增加一個量，該量與內嵌文檔的大小相乘，即在任何給定時間通常執行的文檔數。

JVM最大堆大小增加=（內嵌檔案大小）x（處理的檔案平均數）。

**計算JVM最大堆大小**

在此示例中，當前JVM最大堆設定為512 MB，最大內嵌大小為64 KB。 必須為伺服器配置10個作業同時運行的情況，每個作業有9個輸入檔案和1個結果檔案（每個作業共10個檔案，同時處理100個檔案）。 所有檔案的大小都在512 KB以下。

要內嵌儲存所有檔案，請將最大內嵌大小設定為至少512 KB。

JVM最大堆大小所需的增加是使用以下公式計算的：

(512 KB)x(100)= 51200 KB或50 MB

JVM最大堆大小必須增加50 MB，總計為562 MB。

**考慮堆碎片**

將內嵌檔案的大小設定為大值，會在容易發生堆碎片的系統上產生OutOfMemoryError風險。 要內嵌文檔，JVM堆記憶體必須有足夠的連續空間。 某些作業系統、JVM和廢棄項目收集演算法容易產生堆碎片。 碎片會減少連續堆空間的數量，並且即使存在足夠的總可用空間，也可能導致OutOfMemoryError。

例如，應用程式伺服器上的先前操作使JVM堆處於碎片狀態，而廢棄項目收集器無法充分壓縮堆以重新獲得大塊的可用空間。 即使JVM最大堆大小已調整為最大內嵌大小，OutOfMemoryError仍可能發生。

要考慮堆碎片問題，內嵌文檔大小不能設定為高於堆總大小的0.1%。 例如，JVM最大堆大小為512 MB時，最大內嵌大小為512 MB x 0.001 = 0.512 MB或512 KB。

## WebSphere Application server增強功能 {#websphere-application-server-enhancements}

本節介紹WebSphere Application server環境的特定設定。

### 增加分配給JVM的最大記憶體 {#increasing-the-maximum-memory-allocated-to-the-jvm}

如果您正在運行Configuration Manager或嘗試使用命令行實用程式 *ejbdeploy* ，並且出現OutOfMemory錯誤，則增加分配給JVM的記憶體量。

1. 在 *[appserver root]*/deploytool/itp/目錄中編輯ejbdeploy指令碼：

   * (Windows) `ejbdeploy.bat`
   * （Linux和UNIX） `ejbdeploy.sh`

1. 尋找參 `-Xmx256M` 數並將其變更為較高的值，例如 `-Xmx1024M`。
1. 儲存檔案。
1. 使用Configuration manager運 `ejbdeploy` 行命令或重新部署。

## 使用LDAP提高Windows Server 2003效能 {#improving-windows-server-2003-performance-with-ldap}

本內容說明Microsoft Windows Server 2003作業系統環境的特定設定。

在搜索連接上使用連接池可將所需埠數減少多達50%。 這是因為該連接始終對給定域使用相同的憑據，並且上下文和相關對象被顯式關閉。

### 為連接池配置Windows伺服器 {#configure-your-windows-server-for-connection-pooling}

1. 按一下「開始」>「運行」以啟動註冊表編輯器，然後在「開啟」框中鍵入並 `regedit` 按一下「確定」。
1. 轉到註冊表鍵 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters`
1. 在註冊表編輯器的右窗格中，查找TcpTimedWaitDelay值名稱。 如果未顯示名稱，請從菜單欄中選擇「編輯」>「新建」>「DWORD值」以添加名稱。
1. 在「名稱」(Name)框中，鍵入 `TcpTimedWaitDelay`

   >[!NOTE]
   >
   >如果未看到閃爍的游標並在框內 `New Value #` ，請在右側面板內按一下右鍵，選擇「更名」，然後在「名稱」框中鍵入 `TcpTimedWaitDelay`*。*

1. 對值名稱MaxUserPort、MaxHashTableSize和MaxFreeTcbs重複步驟4。
1. 在右窗格內按兩下以設定TcpTimedWaitDelay值。 在「基本」(Base)下，選擇「小數」(Decimal)，然後在「值」(Value)框中鍵入 `30`。
1. 在右窗格中按兩下，以設定MaxUserPort值。 在「基本」(Base)下，選擇「小數」(Decimal)，然後在「值」(Value)框中鍵入 `65534`。
1. 在右窗格內按兩下，以設定MaxHashTableSize值。 在「基本」(Base)下，選擇「小數」(Decimal)，然後在「值」(Value)框中鍵入 `65536`。
1. 在右窗格內按兩下以設定MaxFreeTcbs值。 在「基本」(Base)下，選擇「小數」(Decimal)，然後在「值」(Value)框中鍵入 `16000`。

>[!NOTE]
>
>如果使用註冊表編輯器或使用其他方法錯誤地修改註冊表，可能會出現嚴重問題。 這些問題可能需要重新安裝作業系統。 自行修改註冊表。

