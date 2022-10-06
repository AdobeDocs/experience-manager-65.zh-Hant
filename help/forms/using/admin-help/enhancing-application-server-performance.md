---
title: 增強應用程式伺服器效能
seo-title: Enhancing application server performance
description: 本檔案說明您可以進行的選用設定，用以改善AEM表單應用程式伺服器的效能。
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

# 增強應用程式伺服器效能{#enhancing-application-server-performance}

本內容說明可進行配置以改善AEM表單應用程式伺服器效能的可選設定。

## 配置應用程式伺服器資料源 {#configuring-application-server-data-sources}

AEM forms會使用AEM forms存放庫作為資料來源。 AEM表單存放庫會儲存應用程式資產，而且在執行時，服務可從存放庫擷取資產，以完成自動化業務流程。

根據您執行的AEM表單模組數量，以及同時存取應用程式的使用者人數，存取資料來源的權限可能會很重要。 可使用連接池優化資料源訪問。 *連接池* 是一種技術，用於避免每次應用程式或伺服器對象需要訪問資料庫時建立新資料庫連接的開銷。 連接池通常用於基於Web和企業的應用程式中，通常由應用程式伺服器處理，但不限於。

請務必正確配置連接池參數，以便您永遠不會耗盡連接，這可能導致應用程式效能惡化。

要正確配置連接池設定，應用伺服器管理員必須在一天的尖峰時段監視連接池。 監控可確保應用程式和用戶隨時都有足夠的連接。 大多數應用程式伺服器都包括監控工具。

可以使用WebLogic伺服器管理控制台監視域中每個JDBC資料源實例的各種統計資訊。 如需詳細資訊，請參閱WebLogic檔案。

當應用程式伺服器管理員確定正確的連接池設定時，該人員必須將此資訊傳遞給資料庫管理員。 資料庫管理員需要此資訊，因為資料庫連接的數量等於資料源的連接池中的連接數量。 然後，完成以下步驟，為應用程式伺服器和資料源類型配置連接池設定。

### 為Oracle和MySQL配置WebLogic的連接池設定 {#configure-connection-pool-settings-for-weblogic-for-oracle-and-mysql}

1. 在「域結構」下，按一下「服務」>「JDBC」>「資料源」，然後在右窗格中按一下「IDP_DS」。
1. 在下一個螢幕中，按一下「配置」>「連接池」頁簽，然後在以下框中輸入一個值：

   * 初始容量
   * 最大容量
   * 容量增加
   * 語句快取大小

1. 按一下「儲存」，然後按一下「啟動變更」。
1. 重新啟動WebLogic托管伺服器。

### 配置SQLServer的WebLogic的連接池設定 {#configure-connection-pool-settings-for-weblogic-for-sqlserver}

1. 在「更改中心」(Change Center)下，按一下「鎖定和編輯」(Lock &amp; Edit)。
1. 在「域結構」下，按一下「服務」>「JDBC」>「資料源」，然後在右窗格中按一下「EDC_DS」。
1. 在下一個螢幕中，按一下「配置」>「連接池」頁簽，然後在以下框中輸入一個值：

   * 初始容量
   * 最大容量
   * 容量增加
   * 語句快取大小

1. 按一下「儲存」，然後按一下「啟動變更」。
1. 重新啟動WebLogic托管伺服器。

### 為DB2的WebSphere配置連接池設定 {#configure-connection-pool-settings-for-websphere-for-db2}

1. 在導航樹中，按一下「資源」>「JDBC」>「JDBC提供程式」。 在右窗格中，按一下您建立的資料源，DB2通用JDBC驅動程式提供程式或LiveCycle- db2 - IDP_DS。
1. 在「其他屬性」下，按一下「資料來源」 ，然後選取「IDP_DS」。
1. 在下一個螢幕的「其他屬性」下，按一下「連接池屬性」，然後在「最大連接數」框和「最小連接數」框中輸入一個值。
1. 按一下「確定」或「應用」，然後按一下「直接保存到主配置」。

### 為WebSphere配置連接池設定以進行Oracle {#configure-connection-pool-settings-for-websphere-for-oracle}

1. 在導航樹中，按一下「資源」>「JDBC」>「JDBC提供程式」。 在右窗格中，按一下您建立的OracleJDBC驅動程式資料源。
1. 在「其他屬性」下，按一下「資料來源」 ，然後選取「IDP_DS」。
1. 在下一個螢幕的「其他屬性」下，按一下「連接池屬性」，然後在「最大連接數」框和「最小連接數」框中輸入一個值。
1. 按一下「確定」或「應用」，然後按一下「直接保存到主配置」。

### 為SqlServer配置WebSphere的連接池設定 {#configure-connection-pool-settings-for-websphere-for-sqlserver}

1. 在導航樹中，按一下「資源」>「JDBC」>「JDBC提供程式」，然後在右窗格中，按一下您建立的用戶定義的JDBC驅動程式資料源。
1. 在「其他屬性」下，按一下「資料來源」 ，然後選取「IDP_DS」。
1. 在下一個螢幕的「其他屬性」下，按一下「連接池屬性」，然後在「最大連接數」框和「最小連接數」框中輸入一個值：
1. 按一下「確定」或「應用」，然後按一下「直接保存到主配置」。

## 優化內聯文檔和對JVM記憶體的影響 {#optimizing-inline-documents-and-impact-on-jvm-memory}

如果您通常處理的文檔大小相對較小，則可以提高與文檔傳輸速度和儲存空間相關的效能。 若要這麼做，請實作下列AEM表單產品設定：

* 增加AEM表單的預設文檔最大內嵌大小，使其大於大多數文檔的大小。
* 要處理較大的檔案，請指定高速磁碟系統或RAM磁碟上的儲存目錄。

在管理控制台中配置了最大內聯大小和儲存目錄(AEM forms臨時檔案目錄和GDS目錄)。

### 文檔大小和最大內嵌大小 {#document-size-and-maximum-inline-size}

當AEM表單發送的用於處理的文檔小於或等於預設文檔的最大內嵌大小時，該文檔將內嵌儲存在伺服器上，並將該文檔序列化為Adobe文檔對象。 內嵌儲存文檔可以帶來顯著的效能優勢。 不過，如果您使用表單工作流程，內容也可能儲存在資料庫中以用於追蹤用途。 因此，增加最大內聯大小可能會影響資料庫大小。

大於最大內嵌大小的文檔儲存在本地檔案系統上。 傳輸到伺服器和從伺服器傳輸的Adobe文檔對象只是指向該檔案的指針。

內嵌檔案內容時（即小於最大內嵌大小），內容會作為檔案序列化裝載的一部分儲存在資料庫中。 因此，增加最大內聯大小可能會影響資料庫大小。

**更改最大內嵌大小**

1. 在管理控制台中，按一下「設定>核心繫統設定>設定」。
1. 在「預設文檔最大內嵌大小」框中輸入一個值，然後按一下「確定」。

   >[!NOTE]
   >
   >在JEE環境中，AEM Forms和JEE環境中，OSGi套件包含AEM Forms上的AEM Forms的Document Max內嵌大小屬性值必須相同。 此步驟僅針對JEE環境上的AEM Forms更新值，針對OSGi套件上的AEM Forms更新，包括JEE環境上的AEM Forms。

1. 使用以下系統屬性重新啟動應用程式伺服器：

   com.adobe.idp.defaultDocumentMaxInlineSize=`[value specified in Step 2]`

   >[!NOTE]
   >
   >上述系統屬性會覆寫JEE環境中為AEM Forms設定的Document Max Inline Size屬性值，以及JEE環境中為AEM Forms所包含的OSGi套件組合上的AEM Forms設定的值。

>[!NOTE]
>
>預設最大內嵌大小為65536位元組。

### JVM最大堆大小 {#jvm-maximum-heap-size}

最大內聯大小的增加需要更多記憶體來儲存序列化文檔。 因此，通常還需要增加JVM最大堆大小。

正在處理許多文檔的重載系統可使JVM堆記憶體快速飽和。 為避免出現OutOfMemoryError，請將JVM最大堆大小增加與內聯文檔的大小相對應的量，再乘以通常在任何給定時間執行的文檔數。

JVM堆大小最大增加=（內聯文檔大小）x（處理的文檔平均數）。

**計算JVM最大堆大小**

在此示例中，當前JVM最大堆設定為512 MB，最大內聯大小為64 KB。 必須為同時運行10個作業的情況配置伺服器，每個作業有9個輸入檔案和1個結果檔案（每個作業總共有10個檔案，同時處理100個檔案）。 所有檔案的大小都在512 KB以下。

要內嵌儲存所有檔案，請將最大內嵌大小設定為至少512 KB。

使用以下方程式計算JVM最大堆大小所需的增加：

(512 KB)x(100)= 51200 KB，或50 MB

JVM堆大小最大必須增加50 MB，總計為562 MB。

**考慮堆碎片**

將內聯文檔的大小設定為大值會在容易發生堆碎片的系統上引發OutOfMemoryError風險。 要內嵌儲存文檔，JVM堆記憶體必須有足夠的連續空間。 某些作業系統、JVM和垃圾收集算法容易出現堆碎片。 碎片會減少連續堆空間的量，並且即使存在足夠的總可用空間，也可能導致OutOfMemoryError。

例如，應用程式伺服器上以前的操作使JVM堆處於碎片狀態，垃圾收集器無法充分壓縮堆以重新獲得大塊的可用空間。 即使JVM最大堆大小已針對最大內嵌大小的增加進行調整，仍可能發生OutOfMemoryError。

要考慮堆碎片，內聯文檔大小不得設定為大於堆大小總數的0.1%。 例如，最大堆大小為512 MB的JVM可支援最大內聯大小為512 MB x 0.001 = 0.512 MB或512 KB。

## WebSphere應用程式伺服器增強功能 {#websphere-application-server-enhancements}

本節介紹WebSphere應用程式伺服器環境的特定設定。

### 增加分配給JVM的最大記憶體 {#increasing-the-maximum-memory-allocated-to-the-jvm}

如果正在運行Configuration Manager，或嘗試使用命令行實用程式生成企業JavaBeans(EJB)部署代碼 *ejbdeploy* 並出現OutOfMemory錯誤，增加分配給JVM的記憶體量。

1. 在 *[appserver根]*/deploytool/itp/目錄：

   * (Windows) `ejbdeploy.bat`
   * （Linux和UNIX） `ejbdeploy.sh`

1. 尋找 `-Xmx256M` 參數並變更為較高的值，例如 `-Xmx1024M`.
1. 儲存檔案。
1. 執行 `ejbdeploy` 命令或重新部署。

## 使用LDAP提高Windows Server 2003效能 {#improving-windows-server-2003-performance-with-ldap}

本內容介紹Microsoft Windows Server 2003作業系統環境的特定設定。

在搜索連接上使用連接池可將所需的埠數減少50%。 這是因為該連接始終對指定域使用相同的憑據，並且上下文和相關對象被顯式關閉。

### 配置Windows Server以進行連接池 {#configure-your-windows-server-for-connection-pooling}

1. 按一下「開始」>「運行」以啟動註冊表編輯器，並在「開啟」框中鍵入 `regedit` 然後按一下「確定」。
1. 轉到註冊表項 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters`
1. 在註冊表編輯器的右窗格中，查找TcpTimedWaitDelay值名稱。 如果名稱未出現，請從菜單欄中選擇「編輯」>「新建」>「DWORD值」以添加名稱。
1. 在「名稱」(Name)框中，鍵入 `TcpTimedWaitDelay`

   >[!NOTE]
   >
   >如果沒有看到閃爍的游標和 `New Value #` 在框內，在右側面板內按一下右鍵，選擇「更名」，然後在「名稱」框中鍵入 `TcpTimedWaitDelay`*.*

1. 對值名稱MaxUserPort、MaxHashTableSize和MaxFreeTcbs重複步驟4。
1. 按兩下右窗格中的以設定TcpTimedWaitDelay值。 在「基本」(Base)下，選擇「小數」(Decimal)，然後在「值」(Value)框中，鍵入 `30`.
1. 在右窗格內按兩下以設定MaxUserPort值。 在「基本」(Base)下，選擇「小數」(Decimal)，然後在「值」(Value)框中，鍵入 `65534`.
1. 在右窗格內按兩下以設定MaxHashTableSize值。 在「基本」(Base)下，選擇「小數」(Decimal)，然後在「值」(Value)框中，鍵入 `65536`.
1. 在右窗格內按兩下以設定MaxFreeTcbs值。 在「基本」(Base)下，選擇「小數」(Decimal)，然後在「值」(Value)框中，鍵入 `16000`.

>[!NOTE]
>
>如果使用註冊表編輯器或使用其他方法錯誤地修改註冊表，則可能會出現嚴重問題。 這些問題可能需要您重新安裝作業系統。 自行修改註冊表。
