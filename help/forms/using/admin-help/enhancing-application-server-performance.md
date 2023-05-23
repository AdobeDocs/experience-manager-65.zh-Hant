---
title: 增強應用伺服器效能
seo-title: Enhancing application server performance
description: 本文檔介紹可配置以提高Forms應用程式伺服器效能AEM的可選設定。
seo-description: This document describes optional settings that you can configure to improve the performance of your AEM forms application server.
uuid: 88d2f96a-3b59-410d-8160-20581d27acad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fad65765-d56d-4a9f-82d5-bcceb1758953
exl-id: 6e2f3d4c-2ead-45b3-98e7-32cacc7e2985
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1863'
ht-degree: 0%

---

# 增強應用伺服器效能{#enhancing-application-server-performance}

此內容介紹可配置以提高Forms應用程式伺服器效能AEM的可選設定。

## 配置應用程式伺服器資料源 {#configuring-application-server-data-sources}

表AEM單使AEM用表單儲存庫作為資料源。 表AEM單儲存庫儲存應用程式資產，在運行時，服務可以從儲存庫中檢索資產，作為完成自動化業務流程的一部分。

對資料源的訪問可能非常重要，具體取決於您正AEM在運行的表單模組數量和訪問應用程式的併發用戶數量。 可以使用連接池優化資料源訪問。 *連接池* 是一種技術，用於避免每次應用程式或伺服器對象需要訪問資料庫時建立新資料庫連接的開銷。 連接池通常用於基於Web和企業的應用程式，通常由應用程式伺服器處理，但不限於應用程式伺服器。

正確配置連接池參數非常重要，這樣您就永遠不會用完連接，這可能導致應用程式效能惡化。

要正確配置連接池設定，應用程式伺服器管理員必須在一天的高峰時段監視連接池。 監控可確保應用程式和用戶始終有足夠的連接。 大多數應用程式伺服器都包括監控工具。

可以使用WebLogic伺服器管理控制台監視域中每個JDBC資料源實例的各種統計資訊。 有關詳細資訊，請參閱WebLogic文檔。

當應用程式伺服器管理員確定正確的連接池設定時，該人員必須將此資訊與資料庫管理員通信。 資料庫管理員需要此資訊，因為資料庫連接數等於資料源連接池中的連接數。 然後，完成以下步驟以配置應用程式伺服器和資料源類型的連接池設定。

### 為WebLogic配置連接池設定以用於Oracle和MySQL {#configure-connection-pool-settings-for-weblogic-for-oracle-and-mysql}

1. 在「域結構」下，按一下「服務」>「JDBC」>「資料源」，然後在右窗格中按一下IDP_DS。
1. 在下一螢幕中，按一下「配置」>「連接池」頁籤，然後在以下框中輸入值：

   * 初始容量
   * 最大容量
   * 容量增量
   * 語句快取大小

1. 按一下「保存」，然後按一下「激活更改」。
1. 重新啟動WebLogic托管伺服器。

### 為SQLServer配置WebLogic的連接池設定 {#configure-connection-pool-settings-for-weblogic-for-sqlserver}

1. 在「變更中心」(Change Center)下，按一下「鎖定和編輯」(Lock &amp; Edit)。
1. 在「域結構」下，按一下「服務」>「JDBC」>「資料源」，然後在右窗格中按一下「EDC_DS」。
1. 在下一螢幕中，按一下「配置」>「連接池」頁籤，然後在以下框中輸入值：

   * 初始容量
   * 最大容量
   * 容量增量
   * 語句快取大小

1. 按一下「保存」，然後按一下「激活更改」。
1. 重新啟動WebLogic托管伺服器。

### 為DB2配置WebSphere的連接池設定 {#configure-connection-pool-settings-for-websphere-for-db2}

1. 在導航樹中，按一下「資源」>「JDBC」>「JDBC提供程式」。 在右窗格中，按一下您建立的資料源，即DB2通用JDBC驅動程式提供程式或LiveCycle- db2 - IDP_DS。
1. 在「其他屬性」下，按一下「資料源」，然後選擇IDP_DS。
1. 在下一螢幕的「其他屬性」下，按一下「連接池屬性」，然後在「最大連接數」框和「最小連接數」框中輸入一個值。
1. 按一下「確定」或「應用」，然後按一下「直接保存到主配置」。

### 為WebSphere配置連接池設定以進行Oracle {#configure-connection-pool-settings-for-websphere-for-oracle}

1. 在導航樹中，按一下「資源」>「JDBC」>「JDBC提供程式」。 在右窗格中，按一下您建立的OracleJDBC驅動程式資料源。
1. 在「其他屬性」下，按一下「資料源」，然後選擇IDP_DS。
1. 在下一螢幕的「其他屬性」下，按一下「連接池屬性」，然後在「最大連接數」框和「最小連接數」框中輸入一個值。
1. 按一下「確定」或「應用」，然後按一下「直接保存到主配置」。

### 為SqlServer的WebSphere配置連接池設定 {#configure-connection-pool-settings-for-websphere-for-sqlserver}

1. 在導航樹中，按一下「資源」>「JDBC」>「JDBC提供程式」，然後在右窗格中按一下您建立的「用戶定義的JDBC驅動程式」資料源。
1. 在「其他屬性」下，按一下「資料源」，然後選擇IDP_DS。
1. 在下一螢幕的「其他屬性」下，按一下「連接池屬性」，然後在「最大連接數」框和「最小連接數」框中輸入一個值：
1. 按一下「確定」或「應用」，然後按一下「直接保存到主配置」。

## 優化內聯文檔和對JVM記憶體的影響 {#optimizing-inline-documents-and-impact-on-jvm-memory}

如果您通常處理的文檔大小相對較小，則可以提高與文檔傳輸速度和儲存空間相關的效能。 為此，請實施以AEM下表單產品配置：

* 增加表單的預設文檔最大內AEM聯大小，使其大於大多數文檔的大小。
* 要處理較大的檔案，請指定高速磁碟系統或RAM磁碟上的儲存目錄。

在管理控制台中配置了最大內聯大小AEM和儲存目錄（表單臨時檔案目錄和GDS目錄）。

### 文檔大小和最大內聯大小 {#document-size-and-maximum-inline-size}

當由表單發送以處理的文AEM檔小於或等於預設文檔的最大內聯大小時，該文檔將內聯儲存在伺服器上，並將該文檔序列化為Adobe文檔對象。 在內部儲存文檔可帶來顯著的效能優勢。 但是，如果您使用表單工作流，則內容也可能儲存在資料庫中以用於跟蹤。 因此，增加最大內聯大小可能會影響資料庫大小。

大於最大內聯大小的文檔儲存在本地檔案系統上。 從伺服器傳輸和傳輸的Adobe文檔對象只是指向該檔案的指針。

當文檔內容被內聯（即小於最大內聯大小）時，內容將作為文檔序列化負載的一部分儲存在資料庫中。 因此，增加最大內聯大小會影響資料庫大小。

**更改最大內聯大小**

1. 在管理控制台中，按一下「設定」>「核心繫統設定」>「配置」。
1. 在「預設文檔最大內聯大小」框中輸入一個值，然後按一下「確定」。

   >[!NOTE]
   >
   >對於JEE環境上的AEM Forms和OSGi捆綁包上的AEM Forms,Document Max Inline Size屬性的值必須相同，JEE環境上的AEM Forms包括在OSGi捆綁包上。 此步驟僅更新了AEM Forms在JEE環境上的價值，而不更新OSGi捆綁包上的AEM Forms在JEE環境上的價值。

1. 使用以下系統屬性重新啟動應用程式伺服器：

   com.adobe.idp.defaultDocumentMaxInlineSize=`[value specified in Step 2]`

   >[!NOTE]
   >
   >上述系統屬性覆蓋為JEE環境上的AEM Forms和OSGi捆綁包上的AEM Forms設定的Document Max Inline Size屬性集的值，JEE環境上的AEM Forms包括在OSGi捆綁包上。

>[!NOTE]
>
>預設最大內聯大小為65536位元組。

### JVM最大堆大小 {#jvm-maximum-heap-size}

增加最大內聯大小需要更多記憶體來儲存序列化文檔。 因此，它通常還需要增加JVM最大堆大小。

處理許多文檔的負載較重的系統可快速使JVM堆記憶體飽和。 為避免OutOfMemoryError，請將JVM最大堆大小增加一個量，該量與內聯文檔的大小相乘，乘以通常在任何給定時間執行的文檔數。

JVM最大堆大小增加=（內聯文檔大小）x（處理的文檔平均數）。

**計算JVM最大堆大小**

在此示例中，當前JVM最大堆設定為512 MB，最大內聯大小為64 KB。 必須為伺服器配置10個作業同時運行的情形，每個作業有9個輸入檔案和1個結果檔案（每個作業總共有10個檔案，同時處理了100個檔案）。 所有檔案的大小都在512 KB以下。

要內聯儲存所有檔案，請將最大內聯大小設定為至少512 KB。

使用以下公式計算JVM最大堆大小所需的增加量：

(512 KB)x(100)= 51200 KB或50 MB

JVM最大堆大小必須增加50 MB，總容量為562 MB。

**考慮堆碎片**

將內聯文檔的大小設定為大值會增加易發生堆碎片的系統上的OutOfMemoryError風險。 要內聯儲存文檔，JVM堆記憶體必須具有足夠的連續空間。 一些作業系統、JVM和垃圾收集算法容易發生堆碎片。 碎片會減少連續堆空間的量，並且即使存在足夠的總可用空間，也可能導致OutOfMemoryError。

例如，應用程式伺服器上的先前操作使JVM堆處於碎片狀態，而垃圾回收器無法充分壓縮堆以重新獲得大塊的可用空間。 即使JVM最大堆大小已針對最大內聯大小的增加進行調整，也可能發生OutOfMemoryError。

要考慮堆碎片，內聯文檔大小不能設定為高於堆總大小的0.1%。 例如，JVM最大堆大小為512 MB時，最大內聯大小可支援512 MB x 0.001 = 0.512 MB或512 KB。

## WebSphere應用程式伺服器增強 {#websphere-application-server-enhancements}

本節介紹特定於WebSphere應用程式伺服器環境的設定。

### 增加分配給JVM的最大記憶體 {#increasing-the-maximum-memory-allocated-to-the-jvm}

如果您正在運行Configuration Manager或嘗試使用命令行實用程式生成Enterprise JavaBeans(EJB)部署代碼 *ejbdeploy* 出現OutOfMemory錯誤，請增加分配給JVM的記憶體量。

1. 在中編輯ejbdeploy指令碼 *[appserver根]*/deploytool/itp/目錄：

   * (Windows) `ejbdeploy.bat`
   * （Linux和UNIX） `ejbdeploy.sh`

1. 查找 `-Xmx256M` 參數並將其更改為更高的值，如 `-Xmx1024M`。
1. 儲存檔案。
1. 運行 `ejbdeploy` 命令或重新部署。

## 使用LDAP提高Windows Server 2003效能 {#improving-windows-server-2003-performance-with-ldap}

此內容描述特定於MicrosoftWindows Server 2003作業系統環境的設定。

在搜索連接上使用連接池可將所需埠數減少50%。 這是因為該連接始終對給定域使用相同的憑據，並且上下文和相關對象被顯式關閉。

### 為連接池配置Windows Server {#configure-your-windows-server-for-connection-pooling}

1. 按一下「開始」>「運行」以啟動註冊表編輯器，並在「開啟」框中鍵入 `regedit` 然後按一下「確定」。
1. 轉到註冊表項 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters`
1. 在註冊表編輯器的右窗格中，找到TcpTimedWaitDelay值名稱。 如果未顯示名稱，請從菜單欄中選擇「編輯」>「新建」>「DWORD值」以添加名稱。
1. 在「名稱」(Name)框中，鍵入 `TcpTimedWaitDelay`

   >[!NOTE]
   >
   >如果沒有看到閃爍的游標 `New Value #` 在框內，按一下右鍵右面板，選擇「更名」，然後在「名稱」框中鍵入 `TcpTimedWaitDelay`*。*

1. 對值名稱MaxUserPort、MaxHashTableSize和MaxFreeTcbs重複步驟4。
1. 在右窗格中按兩下以設定TcpTimedWaitDelay值。 在「基本」(Base)下，選擇「小數」(Decimal)，然後在「值」(Value)框中鍵入 `30`。
1. 在右窗格中按兩下以設定MaxUserPort值。 在「基本」(Base)下，選擇「小數」(Decimal)，然後在「值」(Value)框中鍵入 `65534`。
1. 在右窗格中按兩下以設定MaxHashTableSize值。 在「基本」(Base)下，選擇「小數」(Decimal)，然後在「值」(Value)框中鍵入 `65536`。
1. 在右窗格中按兩下以設定MaxFreeTcbs值。 在「基本」(Base)下，選擇「小數」(Decimal)，然後在「值」(Value)框中鍵入 `16000`。

>[!NOTE]
>
>如果使用註冊表編輯器或使用其他方法錯誤地修改註冊表，則可能會出現嚴重問題。 這些問題可能需要重新安裝作業系統。 自行修改註冊表。
