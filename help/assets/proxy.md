---
title: '[!DNL Assets] 代理開發'
description: 代理是 [!DNL Experience Manager] instance that uses proxy workers to process jobs. Learn how to configure an [!DNL Experience Manager] 代理，支援的操作、代理元件以及如何開發自定義代理工作器。
contentOwner: AG
role: Admin, Architect
exl-id: 42fff236-b4e1-4f42-922c-97da32a933cf
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 0%

---

# [!DNL Assets] 代理開發 {#assets-proxy-development}

[!DNL Adobe Experience Manager Assets] 使用代理來分發特定任務的處理。

代理是特定（有時也是獨立的）Experience Manager實例，它使用代理工作者作為處理者，負責處理工作並建立結果。 代理工作器可用於各種任務。 若為[!DNL Assets]代理，則可用來載入資產，以便在資產內呈現。 例如， [IDS代理工作器](indesign.md)使用[!DNL Adobe InDesign]伺服器來處理要在資產中使用的檔案。

當Proxy是個別的[!DNL Experience Manager]例項時，這有助於減少[!DNL Experience Manager]製作例項的負載。 依預設，[!DNL Assets]會在相同JVM（透過Proxy外部化）中執行資產處理任務，以減少[!DNL Experience Manager]製作例項的負載。

## 代理（HTTP訪問） {#proxy-http-access}

當代理設定為接受處理作業時，可通過HTTP Servlet使用：`/libs/dam/cloud/proxy`。 此Servlet會從發佈的參數建立Sling作業。 然後，此代碼將添加到代理作業隊列，並連接到相應的代理工作器。

### 支援的操作 {#supported-operations}

* `job`

   **需求**:參數 `jobevent` 必須設定為序列化值映射。這用於為作業處理器建立`Event`。

   **結果**:新增工作。如果成功，則會傳回唯一的工作ID。

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

   **需求**:必須 `jobid` 設定參數。

   **結果**:返回由作業處理器建立的結果節點的JSON表示。

```shell
curl -u admin:admin -F":operation=result" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502   /libs/dam/cloud/proxy
```

* `resource`

   **需求**:必須設定參數jobid。

   **結果**:傳回與指定作業相關聯的資源。

```shell
curl -u admin:admin -F":operation=resource" -F"jobid=xxxxxxxxxxxx"
    -F"resourcePath=something.pdf" http://localhost:4502/libs/dam/cloud/proxy
```

* `remove`

   **需求**:必須設定參數jobid。

   **結果**:如果找到作業，則刪除該作業。

```shell
curl -u admin:admin -F":operation=remove" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502/libs/dam/cloud/proxy
```

### 代理工作人員 {#proxy-worker}

代理工作人員是負責處理作業和建立結果的處理器。 工作程式位於代理執行個體上，且必須實作[sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html)才能辨識為代理工作程式。

>[!NOTE]
>
>該工作人員必須實施[sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html)才能被識別為代理工作人員。

### 用戶端API {#client-api}

[`JobService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html) 可作為OSGi服務使用，該服務提供建立作業、移除作業以及從這些作業中獲取結果的方法。此服務的預設實現(`JobServiceImpl`)使用HTTP客戶端與遠程代理Servlet通信。

以下是API使用的範例：

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

>[!NOTE]
>
>[`com.day.cq.dam.api.proxy`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/proxy/package-summary.html)下方提供Proxy API的參考檔案。

Proxy和Proxy工作程式設定皆可透過雲端服務設定使用，可從[!DNL Assets] **Tools**&#x200B;主控台或`/etc/cloudservices/proxy`下存取。 每個代理工作器應在`/etc/cloudservices/proxy`下添加一個節點，以了解工作器特定配置詳細資訊（例如`/etc/cloudservices/proxy/workername`）。

>[!NOTE]
>
>有關詳細資訊，請參閱[InDesign Server代理工作器配置](indesign.md#configuring-the-proxy-worker-for-indesign-server)和[Cloud Services配置](../sites-developing/extending-cloud-config.md)。

以下是API使用的範例：

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

### 開發自定義代理工作器 {#developing-a-customized-proxy-worker}

[IDS代理工作器](indesign.md)是[!DNL Assets]代理工作器的示例，該代理工作器已經提供到現成可用，用於外包InDesign資產的處理。

您也可以開發和配置自己的[!DNL Assets]代理工作人員，以建立專門工作人員來派送和外包您的[!DNL Assets]處理任務。

設定您自己的自訂代理工作程式時，您必須：

* 設定和實作（使用Sling事件）:

   * 自訂工作主題
   * 自訂工作事件處理常式

* 然後使用JobService API來執行下列動作：

   * 將自訂作業派送給代理
   * 管理您的作業

* 如果您想從工作流程使用代理，必須使用WorkflowExternalProcess API和JobService API實作自訂外部步驟。

下列圖表和步驟詳細說明如何繼續：

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>在下列步驟中，將InDesign等效值指示為參考範例。

1. 系統會使用[Sling工作](https://sling.apache.org/site/eventing-and-jobs.html)，因此您需要為使用案例定義工作主題。

   例如，請參閱`IDSJob.IDS_EXTENDSCRIPT_JOB`以了解IDS代理工作器的資訊。

1. 外部步驟用於觸發事件，然後等待完成；這是透過輪詢id來完成。 您必須自行開發步驟，才能實作新功能。

   實作`WorkflowExternalProcess`，然後使用JobService API和您的工作主題準備工作事件，並將其發送到JobService（OSGi服務）。

   例如，請參閱IDS代理工作程式的`INDDMediaExtractProcess`.java。

1. 實作主題的工作處理常式。 此處理常式需要開發，以便執行您的特定動作，且視為背景實作。

   例如，請參閱`IDSJobProcessor.java`以了解IDS代理工作器的資訊。

1. 在dam-commons中使用`ProxyUtil.java`。 這可讓您使用dam代理將工作分派給員工。

>[!NOTE]
>
>[!DNL Assets]代理框架不提供的是池機制。
>
>[!DNL InDesign]整合允許訪問[!DNL InDesign]伺服器池(IDSPool)。 此池特定於[!DNL InDesign]整合，而非[!DNL Assets]代理框架的一部分。

>[!NOTE]
>
>結果同步：
>
>若有n個例項使用相同的Proxy，處理結果會與Proxy一起。 是用戶端(Experience Manager作者)的工作，使用與建立工作時提供給用戶端的相同唯一作業ID來請求結果。 代理只需完成該作業，並使結果準備好被請求。
