---
title: "[!DNL Assets] proxy development"
description: Proxy是使用Proxy Worker處理工作的 [!DNL Experience Manager] 執行個體。 瞭解如何設定 [!DNL Experience Manager] Proxy、支援的作業、Proxy元件，以及如何開發自訂Proxy Worker。
contentOwner: AG
role: Admin, Architect
exl-id: 42fff236-b4e1-4f42-922c-97da32a933cf
solution: Experience Manager, Experience Manager Assets
feature: Proxy Workers
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---

# [!DNL Assets] Proxy開發 {#assets-proxy-development}

[!DNL Adobe Experience Manager Assets]使用Proxy來分配特定工作的處理。

Proxy是一種特定（有時是獨立的）Experience Manager執行個體，它使用Proxy背景工作器作為負責處理工作和建立結果的處理器。 Proxy Worker可用於多種任務。 如果有[!DNL Assets] Proxy，這可用來載入資產，以便在Assets中呈現。 例如，[IDS Proxy背景工作](indesign.md)使用[!DNL Adobe InDesign]伺服器來處理檔案以用於Assets。

當Proxy是單獨的[!DNL Experience Manager]執行個體時，這有助於減少[!DNL Experience Manager]編寫執行個體的負載。 根據預設，[!DNL Assets]會在相同的JVM中執行資產處理工作（透過Proxy外部化），以減少[!DNL Experience Manager]編寫執行個體的負載。

## Proxy （HTTP存取） {#proxy-http-access}

Proxy可透過HTTP Servlet使用，當它設定為接受處理工作於： `/libs/dam/cloud/proxy`時。 此servlet會根據發佈的引數建立Sling作業。 然後，這會新增至Proxy工作佇列，並連線至適當的Proxy背景工作。

### 支援的作業 {#supported-operations}

* `job`

  **需求**：引數`jobevent`必須設定為序列化值對應。 這可用來建立工作處理器的`Event`。

  **結果**：新增工作。 如果成功，則會傳回唯一的工作ID。

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

  **需求**：必須設定引數`jobid`。

  **結果**：傳回作業處理器建立之結果Node的JSON表示法。

```shell
curl -u admin:admin -F":operation=result" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502   /libs/dam/cloud/proxy
```

* `resource`

  **需求**：必須設定引數jobid。

  **結果**：傳回與指定工作關聯的資源。

```shell
curl -u admin:admin -F":operation=resource" -F"jobid=xxxxxxxxxxxx"
    -F"resourcePath=something.pdf" http://localhost:4502/libs/dam/cloud/proxy
```

* `remove`

  **需求**：必須設定引數jobid。

  **結果**：移除工作（如果找到）。

```shell
curl -u admin:admin -F":operation=remove" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502/libs/dam/cloud/proxy
```

### Proxy Worker {#proxy-worker}

Proxy Worker是負責處理工作和建立結果的處理器。 Worker位於Proxy執行個體上，必須實作[sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html)才能辨識為Proxy Worker。

>[!NOTE]
>
>背景工作必須實作[sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html)，才能辨識為Proxy背景工作。

### 使用者端API {#client-api}

[`JobService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html)可用作OSGi服務，提供建立工作、移除工作以及從這些工作取得結果的方法。 此服務的預設實作(`JobServiceImpl`)使用HTTP使用者端與遠端Proxy servlet通訊。

以下是API使用方式的範例：

```java
@Reference
 JobService proxyJobService;

 // to create a job
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

### Cloud Service設定 {#cloud-service-configurations}

<!-- TBD: Cannot find com.day.cq.dam.api.proxy at https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html which were generated in May 2020. Hiding this broken link for now.
>[!NOTE]
>
>Reference documentation for the proxy API is available under [`com.day.cq.dam.api.proxy`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/proxy/package-summary.html).
-->

Proxy和Proxy Worker組態均可透過雲端服務組態使用，可從[!DNL Assets] **工具**&#x200B;主控台或`/etc/cloudservices/proxy`下存取。 每個Proxy背景工作應該在`/etc/cloudservices/proxy`下新增節點，以取得背景工作的特定組態詳細資料（例如，`/etc/cloudservices/proxy/workername`）。

>[!NOTE]
>
>如需詳細資訊，請參閱[InDesign ServerProxy Worker設定](indesign.md#configuring-the-proxy-worker-for-indesign-server)和[Cloud Service設定](../sites-developing/extending-cloud-config.md)。

以下是API使用方式的範例：

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

### 開發自訂的Proxy Worker {#developing-a-customized-proxy-worker}

[IDS Proxy Worker](indesign.md)是[!DNL Assets] Proxy Worker的範例，已提供現成可用以委外InDesign資產的處理。

您也可以開發並設定您自己的[!DNL Assets] Proxy Worker，以建立專門的Worker來分派及委外您的[!DNL Assets]處理工作。

設定您自己的自訂Proxy Worker需要您：

* 設定和實作（使用Sling事件）：

   * 自訂工作主題
   * 自訂工作事件處理常式

* 然後使用JobService API來：

   * 將您的自訂工作分派給Proxy
   * 管理您的工作

* 如果您想要使用工作流程的Proxy，您必須使用WorkflowExternalProcess API和JobService API實作自訂外部步驟。

以下圖表和步驟詳細說明如何繼續：

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>在下列步驟中，會以參照範例來指示對等InDesign。

1. 已使用[Sling工作](https://sling.apache.org/site/eventing-and-jobs.html)，因此您需要為使用案例定義工作主題。

   例如，請參閱`IDSJob.IDS_EXTENDSCRIPT_JOB`以取得IDS Proxy背景工作。

1. 外部步驟會用於觸發事件，然後等待直到完成；這是透過輪詢ID來完成。 開發您自己的步驟來實作新功能。

   實作`WorkflowExternalProcess`，然後使用JobService API和您的工作主題來準備工作事件，並將其分派到JobService （OSGi服務）。

   例如，請參閱`INDDMediaExtractProcess`.java以取得IDS Proxy背景工作。

1. 實作您主題的工作處理常式。 此處理常式需要開發，以便執行您的特定動作，並被視為背景工作實作。

   例如，請參閱`IDSJobProcessor.java`以取得IDS Proxy背景工作。

1. 在dam-commons中使用`ProxyUtil.java`。 這可讓您使用dam Proxy將工作分派給背景工作。

>[!NOTE]
>
>[!DNL Assets] Proxy架構未提供現成可用的是集區機制。
>
>[!DNL InDesign]整合允許存取[!DNL InDesign]部伺服器(IDSPool)的集區。 此集區專屬於[!DNL InDesign]整合，不是[!DNL Assets] Proxy架構的一部分。

>[!NOTE]
>
>結果的同步化：
>
>如果有n個執行個體使用相同的Proxy，處理結果會保留在Proxy。 使用者端(Experience Manager作者)的作業是使用在建立作業時提供給使用者端的相同唯一作業ID來請求結果。 Proxy只會讓工作完成，並讓結果準備好進行要求。
