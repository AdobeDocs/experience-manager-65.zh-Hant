---
title: 監控AEM表單部署
seo-title: 監控AEM表單部署
description: 您可以從系統層級和內部層級監控AEM表單部署。 從這份檔案進一步瞭解如何監控AEM表單部署。
seo-description: 您可以從系統層級和內部層級監控AEM表單部署。 從這份檔案進一步瞭解如何監控AEM表單部署。
uuid: 032b7a93-3069-4ad5-a8c6-4c160f290669
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b3e7bca0-5aaf-4f28-bddb-fd7e8ed72ee8
translation-type: tm+mt
source-git-commit: 215ba1cb3e98954418b844849c812c9ba6cf572b

---


# 監控AEM表單部署 {#monitoring-aem-forms-deployments}

您可以從系統層級和內部層級監控AEM表單部署。 您可以使用專業管理工具，例如HP OpenView、IBM Tivoli和CA UniCenter，以及名為 *JConsole的協力廠商JMX監視器* ，專門監控Java活動。 實施監控策略可改善AEM表單部署的可用性、可靠性和效能。

如需監控AEM表單部署的詳細資訊，請參 [閱「監控AEM表單部署的技術指南」](https://www.adobe.com/devnet/livecycle/pdfs/lc_monitoring_wp_ue.pdf)。

## 使用MBeans進行監控 {#monitoring-using-mbeans}

AEM表格提供兩個已註冊的MBean，可提供導覽和統計資訊。 以下是唯一支援整合和檢查的MBean:

* **** 服務統計：此MBean提供有關服務名稱及其版本的資訊。
* **** OperationStatistics:此MBean提供每個表單伺服器服務的統計資料。 管理員可在此處獲取有關特定服務的資訊，如調用時間、錯誤數等。

### ServiceStatisticMbean公共介面 {#servicestatisticmbean-public-interfaces}

ServiceStatistic MBean的以下公共介面可用於測試：

```as3
 public String getServiceId();
 public int getMajorVersion();
 public int getMinorVersion();
```

### OperationStatisticMbean公共介面 {#operationstatisticmbean-public-interfaces}

OperationStatistic MBean的以下公共介面可用於測試：

```as3
 // InvocationCount: The number of times the method is invoked.
 public long getInvocationCount();
 // InvocationStartTime: The time at which the method started to execute.
 public long getInvocationStartTime();
 // InvocationEndTime: The time at which the method finished execution.
 public long getInvocationEndTime();
 // InvocationTime: The time taken for the execution of the method.
 public long getInvocationTime();
 // LastSamplingDateTime: Convert InvocationStartTime to a formatted string
 public String getLastSamplingDateTime();
 // MaxInvocationTime: The maximum time taken for the execution of the method.
 public long getMaxInvocationTime();
 // MinInvocationTime: The minimum time taken for the execution of the method.
 public long getMinInvocationTime();
 // AverageInvocationTime: the averege execution time taken for the execution of the method.
 public double getAverageInvocationTime();
 // ExceptionCount: The number of times the method has thrown an Exception.
 public long getExceptionCount();
 // ExceptionMessage: The message of the last exception occurred.
 public String getExeptionMessage();
 public void setExceptionMessage(String errorMessage);
```

### MBean樹和操作統計資訊 {#mbean-tree-operation-statistics}

使用JMX控制台(JConsole)，可使用OperationStatistic MBean的統計資訊。 這些統計資料是MBean的屬性，可在下列階層樹狀結構下導覽：

**MBean樹**

**** Adobe網域名稱：取決於應用程式伺服器。 如果應用程式伺服器未定義網域，預設為adobe.com。

**** 服務類型：AdobeService是用來列出所有服務的名稱。

**** AdobeServiceName:服務名稱或服務ID。

**** 版本：服務版本。

**操作統計資訊**

**** 調用時間：執行方法所花的時間。 這不包括請求序列化、從用戶端傳送至伺服器，以及取消序列化的時間。

**** 調用計數：調用服務的次數。

**** 平均呼叫時間：自伺服器啟動以來已執行的所有調用的平均時間。

**** 最大調用時間：自伺服器啟動以來執行的最長調用的持續時間。

**** 最小調用時間：自伺服器啟動以來執行的最短調用的持續時間。

**** 例外計數：導致失敗的調用數。

**** 例外消息：發生的最後一個例外的錯誤消息。

**** 上次取樣日期時間：上次調用的日期。

**** 時間單位：預設值為毫秒。

若要啟用JMX監控，應用程式伺服器通常需要一些設定。 請參閱應用程式伺服器檔案以取得詳細資訊。

### 如何設定開放JMX存取的範例 {#examples-of-how-to-set-up-open-jmx-access}

**JBoss 4.0.3/4.2.0 —— 配置JVM啟動**

要從JConsole查看MBean，請配置JBoss應用程式伺服器的JVM啟動參數。 確保JBoss是從run.bat/sh檔案啟動的。

1. 編輯位於InstallJBoss/bin下的run.bat檔案。
1. 查找JAVA_OPTS行並添加以下內容：

   ```as3
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

**WebLogic 9.2 /10 —— 配置JVM啟動**

1. 編輯位於下方的startWebLogic.bat檔案 `[WebLogic home]/user_projects/domains/Adobe_Live_Cycle/bin`。
1. 查找JAVA_OPTS行並添加以下內容：

   ```as3
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

1. 重新啟動WebLogic。

>[!NOTE]
>
>對於WebLogic，您可以使用遠端或IIOP來存取MBean。

**遠程訪問MBean**

1. 啟動JConsole以建立新連線，然後按一下遠端標籤。
1. 輸入主機名和埠（9088，即在JVM的啟動選項期間指定的編號）。

**Websphere 6.1 —— 配置JVM啟動**

1. 在管理控制台（應用程式伺服器> server1 >程式定義> JVM）上，將下列行新增至「一般JVM引數」欄位：

   ```as3
    -Djavax.management.builder.initial= -Dcom.sun.management.jmxremote
   ```

1. 在/opt/IBM/WebSphere/AppServer/java/jre/lib/management/management.properties檔案(或&lt;Your Websphere JRE>/ lib/management/management.properties)中新增或取消註解下列三行：

   ```as3
    com.sun.management.jmxremote.port=9999 //any port you like, but make sure you use this port when you connect
    com.sun.management.jmxremote.authenticate=false
    com.sun.management.jmxremote.ssl=false
   ```

1. 重新啟動WebSphere。

