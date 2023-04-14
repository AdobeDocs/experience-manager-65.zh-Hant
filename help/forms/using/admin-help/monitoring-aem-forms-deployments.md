---
title: 監控AEM表單部署
seo-title: Monitoring AEM forms deployments
description: 您可以從系統層級和內部層級監控AEM表單部署。 閱讀本檔案，深入了解如何監控AEM表單部署。
seo-description: You can monitor AEM forms deployments from both a system level and an internal level. Learn more about monitoring AEM forms deployments from this document.
uuid: 032b7a93-3069-4ad5-a8c6-4c160f290669
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b3e7bca0-5aaf-4f28-bddb-fd7e8ed72ee8
exl-id: 931e8095-5c7c-4c1f-b95b-75ac2827d4f3
source-git-commit: c47b4dcfd2fbdcb0b98ad815f5b04d8f593e4f64
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---

# 監控AEM表單部署 {#monitoring-aem-forms-deployments}

您可以從系統層級和內部層級監控AEM表單部署。 您可以使用HP OpenView、IBM® Tivoli和CA UniCenter等專業管理工具，以及名為的第三方JMX監視器 *JConsole* 來明確監視Java™活動。 實施監控策略可改善AEM表單部署的可用性、可靠性和效能。

<!-- For more information about monitoring AEM forms deployments, see [A technical guide for monitoring AEM forms deployments](https://www.adobe.com/devnet/livecycle/pdfs/lc_monitoring_wp_ue.pdf). This URL is 404. No suitable replacement URL was found after a search. Do not make this link live if it is dead! -->

## 使用MBean進行監視 {#monitoring-using-mbeans}

AEM Forms提供兩個已註冊的MBean，可提供導覽和統計資訊。 這些部件是唯一支援整合和檢查的MBean:

* **服務統計：** 此MBean提供有關服務名稱及其版本的資訊。
* **操作統計：** 此MBean提供每個AEM Forms伺服器服務的統計資訊。 此MBean可讓管理員獲取有關特定服務的資訊，如調用時間和錯誤數。

### ServiceStatistationMbean公共介面 {#servicestatisticmbean-public-interfaces}

可以訪問ServiceStatistic MBean的以下公共介面以用於測試：

```java
 public String getServiceId();
 public int getMajorVersion();
 public int getMinorVersion();
```

### OperationStatisticMbean公共介面 {#operationstatisticmbean-public-interfaces}

可以訪問OperationStatistic MBean的以下公共介面，以用於測試：

```java
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

使用JMX控制台(JConsole)，可以使用OperationStatistic MBean的統計資訊。 這些統計資訊是MBean的屬性，可以在以下層次結構樹下導航：

**MBean樹**

**Adobe域名：** 取決於應用程式伺服器。 如果應用程式伺服器未定義網域，預設值為adobe.com。

**服務類型：** AdobeService是用於列出所有服務的名稱。

**AdobeServiceName:** 服務名稱或服務ID。

**版本：** 服務的版本。

**操作統計資訊**

**調用時間：** 執行方法所花費的時間。 此操作不包含請求序列化、從客戶端傳輸到伺服器以及反序列化的時間。

**調用計數：** 叫用服務的次數。

**平均調用時間：** 自伺服器啟動以來已執行的所有調用的平均時間。

**最大調用時間：** 自伺服器啟動以來已執行的最長調用的持續時間。

**最小調用時間：** 自伺服器啟動以來執行的最短調用的持續時間。

**例外計數：** 導致失敗的調用次數。

**異常消息：** 上次發生異常的錯誤消息。

**上次取樣日期時間：** 上次調用的日期。

**時間單位：** 預設值為毫秒。

要啟用JMX監視，應用程式伺服器通常需要一些配置。 如需詳細資訊，請參閱應用程式伺服器檔案。

### 如何設定開放式JMX存取的範例 {#examples-of-how-to-set-up-open-jmx-access}

**JBoss® 4.0.3/4.2.0 — 配置JVM啟動**

要從JConsole查看MBean，請配置JBoss應用程式伺服器的JVM啟動參數。 請確定JBoss是從run.bat/sh檔案啟動。

1. 編輯位於InstallJBoss/bin下的run.bat檔案。
1. 查找JAVA_OPTS行並添加以下內容：

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

**WebLogic 9.2 /10 — 配置JVM啟動**

1. 編輯位於 `[WebLogic home]/user_projects/domains/Adobe_Live_Cycle/bin`.
1. 查找JAVA_OPTS行並添加以下內容：

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

1. 重新啟動WebLogic。

>[!NOTE]
>
>對於WebLogic，可以使用遠程或IIOP訪問MBean。

**遠程訪問MBean**

1. 啟動JConsole以建立新連接，然後按一下「遠程」頁簽。
1. 輸入主機名和埠（9088，在JVM的啟動選項期間指定的號碼）。

**WebSphere® 6.1 — 配置JVM啟動**

1. 在Admin Console（「應用程式伺服器」>「伺服器1」>「進程定義」>「JVM」）上，將以下行添加到「通用JVM參數」欄位中：

   ```shell
    -Djavax.management.builder.initial= -Dcom.sun.management.jmxremote
   ```

1. 在/opt/IBM/WebSphere/AppServer/java/jre/lib/management/management.properties檔案(或 &lt;your websphere=&quot;&quot; jre=&quot;&quot;>/ lib/management/management.properties):

   ```shell
    com.sun.management.jmxremote.port=9999 //any port you like, but make sure you use this port when you connect
    com.sun.management.jmxremote.authenticate=false
    com.sun.management.jmxremote.ssl=false
   ```

1. 重新啟動WebSphere。
