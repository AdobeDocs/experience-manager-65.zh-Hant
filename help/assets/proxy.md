---
title: '"[!DNL Assets] 代理開發」'
description: 代理是 [!DNL Experience Manager] 使用代理工作程式處理作業的實例。 瞭解如何配置 [!DNL Experience Manager] 代理、支援的操作、代理元件以及如何開發自定義代理工作程式。
contentOwner: AG
role: Admin, Architect
exl-id: 42fff236-b4e1-4f42-922c-97da32a933cf
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 0%

---

# [!DNL Assets] 代理開發 {#assets-proxy-development}

[!DNL Adobe Experience Manager Assets] 使用代理來分發特定任務的處理。

代理是一個特定（有時是獨立的）Experience Manager實例，它使用代理工作程式作為處理作業和建立結果的處理器。 代理工作程式可用於各種任務。 在 [!DNL Assets] 代理，可用於載入資產以在資產中呈現。 例如， [IDS代理工作程式](indesign.md) 使用 [!DNL Adobe InDesign] 要在資產中使用的檔案的處理伺服器。

當代理是獨立的 [!DNL Experience Manager] 實例這樣有助於減少 [!DNL Experience Manager] 創作實例。 預設情況下， [!DNL Assets] 在同一JVM（通過代理外部化）中執行資產處理任務，以減少 [!DNL Experience Manager] 創作實例。

## 代理（HTTP訪問） {#proxy-http-access}

當代理配置為接受以下處理作業時，可通過HTTP Servlet使用： `/libs/dam/cloud/proxy`。 此servlet從已發佈的參數建立sling作業。 然後，此操作會添加到代理作業隊列並連接到相應的代理工作程式。

### 支援的操作 {#supported-operations}

* `job`

   **要求**:參數 `jobevent` 必須設定為序列化值映射。 這用於建立 `Event` 作業處理器。

   **結果**:添加新作業。 如果成功，則返回唯一的作業ID。

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

   **要求**:參數 `jobid` 必須設定。

   **結果**:返回作業處理器建立的結果節點的JSON表示形式。

```shell
curl -u admin:admin -F":operation=result" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502   /libs/dam/cloud/proxy
```

* `resource`

   **要求**:必須設定參數jobid。

   **結果**:返回與給定作業關聯的資源。

```shell
curl -u admin:admin -F":operation=resource" -F"jobid=xxxxxxxxxxxx"
    -F"resourcePath=something.pdf" http://localhost:4502/libs/dam/cloud/proxy
```

* `remove`

   **要求**:必須設定參數jobid。

   **結果**:如果找到，則刪除作業。

```shell
curl -u admin:admin -F":operation=remove" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502/libs/dam/cloud/proxy
```

### 代理工作程式 {#proxy-worker}

代理工作程式是負責處理作業並建立結果的處理器。 工作程式駐留在代理實例上，必須實現 [sling作業處理器](https://sling.apache.org/site/eventing-and-jobs.html) 被認定為代理工作者。

>[!NOTE]
>
>工作人員必須實施 [sling作業處理器](https://sling.apache.org/site/eventing-and-jobs.html) 被認定為代理工作者。

### 客戶端API {#client-api}

[`JobService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html) OSGi服務提供建立作業、刪除作業和從這些作業中獲取結果的方法。 此服務的預設實現(`JobServiceImpl`)使用HTTP客戶端與遠程代理servlet通信。

以下是API用法的示例：

```java
@Reference
 JobService proxyJobService;

 // to create a new job
 final Hashtable props = new Hashtable();
 props.put("someproperty", "some value");
 props.put(JobUtil.PROPERTY_JOB_TOPIC, "myworker/job"); // this is an identifier of the worker
 final String jobId = proxyJobService.addJob(props, new Asset[]{asset});

 // to check status (returns JobService.STATUS_FINISHED or JobService.STATUS_INPROGRESS)
 int status = proxyJobService.getStatus(jobId)

 // to get the result
 final String jsonString = proxyJobService.getResult(jobId);

 // to remove job and cleanup
 proxyJobService.removeJob(jobId);
```

### Cloud Service配置 {#cloud-service-configurations}

<!-- TBD: Cannot find com.day.cq.dam.api.proxy at https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html which were generated in May 2020. Hiding this broken link for now.
>[!NOTE]
>
>Reference documentation for the proxy API is available under [`com.day.cq.dam.api.proxy`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/proxy/package-summary.html).
-->

代理和代理工作器配置均可通過雲服務配置獲得，可從以下站點訪問 [!DNL Assets] **工具** 控制台或 `/etc/cloudservices/proxy`。 每個代理工作程式都應在 `/etc/cloudservices/proxy` 對於工作人員特定的配置詳細資訊(例如， `/etc/cloudservices/proxy/workername`)。

>[!NOTE]
>
>請參閱 [InDesign Server代理工作程式配置](indesign.md#configuring-the-proxy-worker-for-indesign-server) 和 [Cloud Services配置](../sites-developing/extending-cloud-config.md) 的子菜單。

以下是API用法的示例：

```java
@Reference(policy = ReferencePolicy.STATIC)
 ProxyConfig proxyConfig;

 // to get proxy config
 Configuration cloudConfig = proxyConfig.getConfiguration();
 final String value = cloudConfig.get("someProperty", "defaultValue");

 // to get worker config
 Configuration cloudConfig = proxyConfig.getConfiguration("workername");
 final String value = cloudConfig.get("someProperty", "defaultValue");
```

### 開發自定義代理工作程式 {#developing-a-customized-proxy-worker}

的 [IDS代理工作程式](indesign.md) 是 [!DNL Assets] 代理工作人員，已提供現成服務來外包InDesign資產的處理。

您還可以開發和配置自己的 [!DNL Assets] 代理工作人員，以建立專門工作人員來派送和外包您 [!DNL Assets] 處理任務。

設定您自己的自定義代理工作程式要求您：

* 設定和實施（使用Sling事件）:

   * 自定義作業主題
   * 自定義作業事件處理程式

* 然後使用JobService API執行以下操作：

   * 將自定義作業派送給代理
   * 管理您的工作

* 如果要從工作流使用代理，則必須使用WorkflowExternalProcess API和JobService API實現自定義外部步驟。

下圖和步驟詳細說明了如何繼續：

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>在以下步驟中，InDesign等價物作為參考示例。

1. A [吊帶作業](https://sling.apache.org/site/eventing-and-jobs.html) ，因此您需要為使用案例定義作業主題。

   例如，請參見 `IDSJob.IDS_EXTENDSCRIPT_JOB` IDS代理工作程式。

1. 外部步驟用於觸發事件，然後等待事件完成；這是通過輪詢id來完成的。 您必須制定自己的步驟來實施新功能。

   實施 `WorkflowExternalProcess`，然後使用JobService API和您的作業主題準備作業事件並將其派送至JobService（OSGi服務）。

   例如，請參見 `INDDMediaExtractProcess`.java（用於IDS代理工作程式）。

1. 為主題實現作業處理程式。 此處理程式需要開發，以便執行您的特定操作並被視為工作程式實現。

   例如，請參見 `IDSJobProcessor.java` IDS代理工作程式。

1. 利用 `ProxyUtil.java` 在水壩共用區。 這允許您使用水壩代理向員工分派工作。

>[!NOTE]
>
>什麼 [!DNL Assets] 代理框架不提供現成池機制。
>
>的 [!DNL InDesign] 整合允許訪問 [!DNL InDesign] 伺服器(IDSPool)。 此池特定於 [!DNL InDesign] 整合，而不是 [!DNL Assets] 代理框架。

>[!NOTE]
>
>結果同步：
>
>如果n個實例使用同一代理，則處理結果與代理保持一致。 客戶端(Experience Manager作者)的作業使用與建立作業時給客戶端的相同唯一作業ID請求結果。 代理只需完成作業，並使結果準備好被請求。
