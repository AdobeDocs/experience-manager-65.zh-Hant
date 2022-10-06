---
title: 以程式設計方式與工作流程互動
seo-title: Interacting with Workflows Programmatically
description: 以程式設計方式與工作流程互動
seo-description: null
uuid: a0f19fc6-b9bd-4b98-9c0e-fbf4f7383026
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: cb621332-a149-4f8d-9425-fd815b033c38
exl-id: 2b396850-e9fb-46d9-9daa-ebd410a9e1a5
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2004'
ht-degree: 0%

---

# 以程式設計方式與工作流程互動{#interacting-with-workflows-programmatically}

當 [自訂和延伸您的工作流程](/help/sites-developing/workflows-customizing-extending.md) 您可以訪問工作流對象：

* [使用工作流程Java API](#using-the-workflow-java-api)
* [在ECMA指令碼中取得工作流程物件](#obtaining-workflow-objects-in-ecma-scripts)
* [使用工作流程REST API](#using-the-workflow-rest-api)

## 使用工作流程Java API {#using-the-workflow-java-api}

工作流程Java API包含 [`com.adobe.granite.workflow`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/package-summary.html) 包和幾個子包。 API最重要的成員是 `com.adobe.granite.workflow.WorkflowSession` 類別。 此 `WorkflowSession` 類提供了對設計時間和運行時工作流對象的訪問：

* 工作流程模型
* 工作項目
* 工作流程例項
* 工作流程資料
* 收件匣項目

類還提供了幾種干預工作流生命週期的方法。

下表提供與工作流程以程式設計方式互動時要使用的多個關鍵Java對象的參考文檔的連結。 下面的示例演示如何獲取和使用代碼中的類對象。

| 功能 | 物件 |
|---|---|
| 存取工作流程 | [`WorkflowSession`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html) |
| 執行和查詢工作流實例 | [`Workflow`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html)</br>[`WorkItem`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkItem.html)</br>[`WorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html) |
| 管理工作流模型 | [`WorkflowModel`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowModel.html)</br>[`WorkflowNode`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowNode.html)</br>[`WorkflowTransition`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowTransition.html) |
| 工作流中（或不）的節點的資訊 | [`WorkflowStatus`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html) |

## 在ECMA指令碼中取得工作流程物件 {#obtaining-workflow-objects-in-ecma-scripts}

如 [找到指令碼](/help/sites-developing/the-basics.md#locating-the-script), AEM（透過Apache Sling）提供執行伺服器端ECMA指令碼的ECMA指令碼引擎。 此 [`org.apache.sling.scripting.core.ScriptHelper`](https://sling.apache.org/apidocs/sling5/org/apache/sling/scripting/core/ScriptHelper.html) 類別會立即供指令碼使用，因為 `sling` 變數。

此 `ScriptHelper` 類提供對 `SlingHttpServletRequest` 最終獲得 `WorkflowSession` 對象；例如：

```
var wfsession = sling.getRequest().getResource().getResourceResolver().adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
```

## 使用工作流程REST API {#using-the-workflow-rest-api}

工作流程主控台大量使用REST API;因此，本頁面說明工作流程的REST API。

>[!NOTE]
>
>curl命令行工具允許您使用Workflow REST API訪問工作流對象並管理實例生命週期。 本頁的範例示範如何透過curl命令列工具使用REST API。

REST API支援下列動作：

* 啟動或停止工作流服務
* 建立、更新或刪除工作流模型
* [啟動、暫停、繼續或終止工作流實例](/help/sites-administering/workflows.md#workflow-status-and-actions)
* 完成或委派工作項目

>[!NOTE]
>
>使用Firebug（用於網頁開發的Firefox擴充功能），便可在控制台運作時遵循HTTP流量。 例如，您可以檢查參數，以及透過 `POST` 請求。

在此頁面中，假設AEM在連接埠的localhost上執行 `4502` 而安裝環境是「 `/`&quot;（根）。 如果不是安裝的情況，則需要相應地調整HTTP請求所應用的URI。

支援的呈現 `GET` 要求為JSON呈現。 的URL `GET` 應該有 `.json` 擴充功能，例如：

`http://localhost:4502/etc/workflow.json`

### 管理工作流程例項 {#managing-workflow-instances}

下列HTTP要求方法適用於：

`http://localhost:4502/etc/workflow/instances`

<table>
 <tbody>
  <tr>
   <td>HTTP要求方法</td>
   <td>動作</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>列出可用的工作流實例。</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td><p>建立新的工作流實例。 參數為：<br /> - <code>model</code>:各工作流模型的ID(URI)<br /> - <code>payloadType</code>:包含裝載的類型(例如 <code>JCR_PATH</code> 或URL)。<br /> 裝載會以參數的形式傳送 <code>payload</code>. A <code>201</code> (<code>CREATED</code>)回應會與位置標題一併傳回，其中包含新工作流程例項資源的URL。</p> </td>
  </tr>
 </tbody>
</table>

#### 按狀態管理工作流實例 {#managing-a-workflow-instance-by-its-state}

下列HTTP要求方法適用於：

`http://localhost:4502/etc/workflow/instances.{state}`

| HTTP要求方法 | 動作 |
|---|---|
| `GET` | 列出可用的工作流程例項及其狀態( `RUNNING`, `SUSPENDED`, `ABORTED` 或 `COMPLETED`) |

#### 依ID管理工作流程例項 {#managing-a-workflow-instance-by-its-id}

下列HTTP要求方法適用於：

`http://localhost:4502/etc/workflow/instances/{id}`

<table>
 <tbody>
  <tr>
   <td>HTTP要求方法</td>
   <td>動作</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>取得例項資料（定義和中繼資料），包括個別工作流程模型的連結。</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>變更例項的狀態。 新狀態會以參數的形式傳送 <code>state</code> 和必須具有下列其中一個值： <code>RUNNING</code>, <code>SUSPENDED</code>，或 <code>ABORTED</code>.<br /> 如果無法存取新狀態（例如，當暫停終止的執行個體時）a <code>409</code> (<code>CONFLICT</code>)回應會傳回給用戶端。</td>
  </tr>
 </tbody>
</table>

### 管理工作流模型 {#managing-workflow-models}

下列HTTP要求方法適用於：

`http://localhost:4502/etc/workflow/models`

<table>
 <tbody>
  <tr>
   <td>HTTP要求方法</td>
   <td>動作</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>列出可用的工作流模型。</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>建立新工作流程模型. 如果參數 <code>title</code> 會傳送，並以指定的標題建立新模型。 將JSON模型定義附加為參數 <code>model</code> 根據提供的定義建立新的工作流模型。<br /> A <code>201</code> 回應(<code>CREATED</code>)會與包含新工作流程模型資源URL的位置標題一併傳回。<br /> 當模型定義附加為檔案參數(稱為 <code>modelfile</code>.<br /> 在以下兩種情況中 <code>model</code> 和 <code>modelfile</code> 參數，稱為 <code>type</code> 是定義序列化格式的必要條件。 可使用OSGI API整合新的序列化格式。 標準JSON序列化程式會與工作流程引擎一併提供。 其類型為JSON。 如需格式的範例，請參閱下方。</td>
  </tr>
 </tbody>
</table>

範例：在瀏覽器中， `http://localhost:4502/etc/workflow/models.json` 會產生類似下列的json回應：

```
[
    {"uri":"/var/workflow/models/activationmodel"}
    ,{"uri":"/var/workflow/models/dam/adddamsize"}
    ,{"uri":"/var/workflow/models/cloudconfigs/dtm-reactor/library-download"}
    ,{"uri":"/var/workflow/models/ac-newsletter-workflow-simple"}
    ,{"uri":"/var/workflow/models/dam/dam-create-language-copy"}
    ,{"uri":"/var/workflow/models/dam/dam-create-and-translate-language-copy"}
    ,{"uri":"/var/workflow/models/dam-indesign-proxy"}
    ,{"uri":"/var/workflow/models/dam-xmp-writeback"}
    ,{"uri":"/var/workflow/models/dam-parse-word-documents"}
    ,{"uri":"/var/workflow/models/dam/process_subasset"}
    ,{"uri":"/var/workflow/models/dam/dam_set_last_modified"}
    ,{"uri":"/var/workflow/models/dam/dam-autotag-assets"}
    ,{"uri":"/var/workflow/models/dam/update_asset"}
    ,{"uri":"/var/workflow/models/dam/update_asset_offloading"}
    ,{"uri":"/var/workflow/models/dam/dam-update-language-copy"}
    ,{"uri":"/var/workflow/models/dam/update_from_lightbox"}
    ,{"uri":"/var/workflow/models/cloudservices/DTM_bundle_download"}
    ,{"uri":"/var/workflow/models/dam/dam_download_asset"}
    ,{"uri":"/var/workflow/models/dam/dynamic-media-encode-video"}
    ,{"uri":"/var/workflow/models/dam/dynamic-media-video-thumbnail-replacement"}
    ,{"uri":"/var/workflow/models/dam/dynamic-media-video-user-uploaded-thumbnail"}
    ,{"uri":"/var/workflow/models/newsletter_bounce_check"}
    ,{"uri":"/var/workflow/models/projects/photo_shoot_submission"}
    ,{"uri":"/var/workflow/models/projects/product_photo_shoot"}
    ,{"uri":"/var/workflow/models/projects/approval_workflow"}
    ,{"uri":"/var/workflow/models/prototype-01"}
    ,{"uri":"/var/workflow/models/publish_example"}
    ,{"uri":"/var/workflow/models/publish_to_campaign"}
    ,{"uri":"/var/workflow/models/screens/publish_to_author_bin"}
    ,{"uri":"/var/workflow/models/s7dam/request_to_publish_to_youtube"}
    ,{"uri":"/var/workflow/models/projects/request_copy"}
    ,{"uri":"/var/workflow/models/projects/request_email"}
    ,{"uri":"/var/workflow/models/projects/request_landing_page"}
    ,{"uri":"/var/workflow/models/projects/request_launch"}
    ,{"uri":"/var/workflow/models/request_for_activation"}
    ,{"uri":"/var/workflow/models/request_for_deactivation"}
    ,{"uri":"/var/workflow/models/request_for_deletion"}
    ,{"uri":"/var/workflow/models/request_for_deletion_without_deactivation"}
    ,{"uri":"/var/workflow/models/request_to_complete_move_operation"}
    ,{"uri":"/var/workflow/models/reverse_replication"}
    ,{"uri":"/var/workflow/models/salesforce-com-export"}
    ,{"uri":"/var/workflow/models/scene7"}
    ,{"uri":"/var/workflow/models/scheduled_activation"}
    ,{"uri":"/var/workflow/models/scheduled_deactivation"}
    ,{"uri":"/var/workflow/models/screens/screens-update-asset"}
    ,{"uri":"/var/workflow/models/translation"}
    ,{"uri":"/var/workflow/models/s7dam/request_to_remove_from_youtube"}
    ,{"uri":"/var/workflow/models/wcm-translation/create_language_copy"}
    ,{"uri":"/var/workflow/models/wcm-translation/prepare_translation_project"}
    ,{"uri":"/var/workflow/models/wcm-translation/translate-i18n-dictionary"}
    ,{"uri":"/var/workflow/models/wcm-translation/sync_translation_job"}
    ,{"uri":"/var/workflow/models/wcm-translation/translate-language-copy"}
    ,{"uri":"/var/workflow/models/wcm-translation/update_language_copy"}
]
```

#### 管理特定工作流程模型 {#managing-a-specific-workflow-model}

下列HTTP要求方法適用於：

`http://localhost:4502*{uri}*`

其中 `*{uri}*` 是儲存庫中模型節點的路徑。

<table>
 <tbody>
  <tr>
   <td>HTTP要求方法</td>
   <td>動作</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>取得 <code>HEAD</code> 模型的版本（定義和中繼資料）。</td>
  </tr>
  <tr>
   <td><code>PUT</code></td>
   <td>更新 <code>HEAD</code> 模型版本（建立新版本）。<br /> 新版本的模型的完整模型定義必須添加為以下參數： <code>model</code>. 此外， <code>type</code> 建立新模型時需要參數，且需要有值 <code>JSON</code>.<br /> </td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>與PUT相同。 需要，因為AEM Widget不支援 <code>PUT</code> 操作。</td>
  </tr>
  <tr>
   <td><code>DELETE</code></td>
   <td>刪除模型。 為了解決防火牆/代理問題， <code>POST</code> 包含 <code>X-HTTP-Method-Override</code> 帶值的標題條目 <code>DELETE</code> 也會接受為 <code>DELETE</code> 請求。</td>
  </tr>
 </tbody>
</table>

範例：在瀏覽器中， `http://localhost:4502/var/workflow/models/publish_example.json` 傳回a `json` 與下列程式碼類似的回應：

```shell
{
  "id":"/var/workflow/models/publish_example",
  "title":"Publish Example",
  "version":"1.0",
  "description":"This example shows a simple review and publish process.",
  "metaData":
  {
    "multiResourceSupport":"true",
    "tags":"wcm,publish"
  },
  "nodes":
  [{
    "id":"node0",
    "type":"START",
    "title":"Start",
    "description":"The start node of the workflow.",
    "metaData":
    {
    }
  },
  {
    "id":"node1",
    "type":"PARTICIPANT",
    "title":"Validate Content",
    "description":"Validate the modified content.",
    "metaData":
    {
      "PARTICIPANT":"admin"
    }
  },
  {
    "id":"node2",
    "type":"PROCESS",
    "title":"Publish Content",
    "description":"Publish the modified content.",
    "metaData":
    {
      "PROCESS_AUTO_ADVANCE":"true",
      "PROCESS":"com.day.cq.wcm.workflow.process.ActivatePageProcess"
    }
  },
  {
    "id":"node3",
    "type":"END",
    "title":"End",
    "description":"The end node of the workflow.",
    "metaData":
    {
    }
  }],
  "transitions":
  [{
    "from":"node0",
    "to":"node1",
    "metaData":
    {
    }
  },
  {
    "from":"node1",
    "to":"node2",
    "metaData":
    {
    }
  },
  {
    "from":"node2",
    "to":"node3",
    "metaData":
    {
    }
  }
]}
```

#### 按工作流模型的版本管理工作流模型 {#managing-a-workflow-model-by-its-version}

下列HTTP要求方法適用於：

`http://localhost:4502/etc/workflow/models/{id}.{version}`

| HTTP要求方法 | 動作 |
|---|---|
| `GET` | 獲取給定版本中模型的資料（如果存在）。 |

### 管理（用戶）收件箱 {#managing-user-inboxes}

下列HTTP要求方法適用於：

`http://localhost:4502/bin/workflow/inbox`

<table>
 <tbody>
  <tr>
   <td>HTTP要求方法</td>
   <td>動作</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>列出使用者收件匣中的工作項目，由HTTP驗證標題識別。</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>完成將URI作為參數發送的工作項 <code>item</code> 並根據工作流實例向下一個節點（由參數定義）推進 <code>route</code> 或 <code>backroute</code> 以防退一步。<br /> 如果參數 <code>delegatee</code> 會傳送，而工作項目會由參數識別 <code>item</code> 已委派給指定的參與者。</td>
  </tr>
 </tbody>
</table>

#### 使用WorkItem ID管理（用戶）收件箱 {#managing-a-user-inbox-by-the-workitem-id}

下列HTTP要求方法適用於：

`http://localhost:4502/bin/workflow/inbox/{id}`

| HTTP要求方法 | 動作 |
|---|---|
| `GET` | 獲取收件箱的資料（定義和元資料） `WorkItem` 由其ID識別。 |

## 範例 {#examples}

### 如何使用其ID取得所有執行中工作流程的清單 {#how-to-get-a-list-of-all-running-workflows-with-their-ids}

若要取得所有執行中工作流程的清單，請執行下列GET:

`http://localhost:4502/etc/workflow/instances.RUNNING.json`

#### 如何以其ID取得所有執行中工作流程的清單 — 使用curl進行REST {#how-to-get-a-list-of-all-running-workflows-with-their-ids-rest-using-curl}

使用curl的範例：

```shell
curl -u admin:admin http://localhost:4502/etc/workflow/instances.RUNNING.json
```

此 `uri` 顯示在結果中，可作為例項使用 `id` 在其他命令中；例如：

```shell
[
    {"uri":"/etc/workflow/instances/server0/2017-03-08/request_for_activation_1"}
]
```

>[!NOTE]
>
>此 `curl` 命令可與任何 [工作流程狀態](/help/sites-administering/workflows.md#workflow-status-and-actions) 取代 `RUNNING`.

### 如何變更工作流程標題 {#how-to-change-the-workflow-title}

若要變更 **工作流程標題** 顯示於 **例項** ，請傳送 `POST` 命令：

* 至: `http://localhost:4502/etc/workflow/instances/{id}`

* 搭配下列參數：

   * `action`:其價值必須是： `UPDATE`
   * `workflowTitle`:工作流程標題

#### 如何使用curl變更工作流程標題 — REST {#how-to-change-the-workflow-title-rest-using-curl}

使用curl的範例：

```shell
curl -u admin:admin -d "action=UPDATE&workflowTitle=myWorkflowTitle" http://localhost:4502/etc/workflow/instances/{id}

# for example
curl -u admin:admin -d "action=UPDATE&workflowTitle=myWorkflowTitle" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
```

### 如何列出所有工作流模型 {#how-to-list-all-workflow-models}

要獲取所有可用工作流模型的清單，請執行以下GET:

`http://localhost:4502/etc/workflow/models.json`

#### 如何列出所有工作流程模型 — 使用curl進行REST {#how-to-list-all-workflow-models-rest-using-curl}

使用curl的範例：

```shell
curl -u admin:admin http://localhost:4502/etc/workflow/models.json
```

>[!NOTE]
>
>另請參閱 [管理工作流模型](#managing-workflow-models).

### 取得WorkflowSession物件 {#obtaining-a-workflowsession-object}

此 `com.adobe.granite.workflow.WorkflowSession` 類別可從 `javax.jcr.Session` 物件或 `org.apache.sling.api.resource.ResourceResolver` 物件。

#### 取得WorkflowSession物件 — Java {#obtaining-a-workflowsession-object-java}

在JSP指令碼（或Servlet類的Java代碼）中，使用HTTP請求對象來獲取 `SlingHttpServletRequest` 對象，提供對 `ResourceResolver` 物件。 調整 `ResourceResolver` 對象 `WorkflowSession`.

```java
<%
%><%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false"
    import="com.adobe.granite.workflow.WorkflowSession,
  org.apache.sling.api.SlingHttpServletRequest"%><%

SlingHttpServletRequest slingReq = (SlingHttpServletRequest)request;
WorkflowSession wfSession = slingReq.getResourceResolver().adaptTo(WorkflowSession.class);
%>
```

#### 取得WorkflowSession物件 — ECMA指令碼 {#obtaining-a-workflowsession-object-ecma-script}

使用 `sling` 變數來取得 `SlingHttpServletRequest` 用於獲取 `ResourceResolver` 物件。 調整 `ResourceResolver` 物件 `WorkflowSession` 物件。

```
var wfsession = sling.getRequest().getResource().getResourceResolver().adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
```

### 建立、讀取或刪除工作流模型 {#creating-reading-or-deleting-workflow-models}

下列範例顯示如何存取工作流程模型：

* Java和ECMA指令碼的程式碼會使用 `WorkflowSession.createNewModel` 方法。
* curl命令直接使用其URL訪問模型。

所用範例：

1. 建立模型(使用ID `/var/workflow/models/mymodel/jcr:content/model`)。
1. 刪除模型。

>[!NOTE]
>
>刪除模型會設定 `deleted` 模型的屬性 `metaData` 子節點到 `true`.
>
>刪除不會刪除模型節點。

建立新模型時：

* 工作流模型編輯器要求模型使用以下的特定節點結構 `/var/workflow/models`. 模型的父節點必須為類型 `cq:Page` 有 `jcr:content` 具有以下屬性值的節點：

   * `sling:resourceType`: `cq/workflow/components/pages/model`
   * `cq:template`: `/libs/cq/workflow/templates/model`

   建立模型時，必須先建立此模型 `cq:Page` 節點及其使用 `jcr:content` 節點作為模型節點的父節點。

* 此 `id` 某些方法識別模型所需的參數是儲存庫中模型節點的絕對路徑：

   `/var/workflow/models/<*model_name>*/jcr:content/model`

   >[!NOTE]
   >
   >請參閱 [如何列出所有工作流模型](#how-to-list-all-workflow-models).

#### 建立、讀取或刪除工作流模型 — Java {#creating-reading-or-deleting-workflow-models-java}

```java
<%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false" import="com.adobe.granite.workflow.WorkflowSession,
                 com.adobe.granite.workflow.model.WorkflowModel,
             org.apache.sling.api.SlingHttpServletRequest"%><%

SlingHttpServletRequest slingReq = (SlingHttpServletRequest)request;
WorkflowSession wfSession = slingReq.getResourceResolver().adaptTo(WorkflowSession.class);
/* Create the parent page */
String modelRepo = new String("/var/workflow/models");
String modelTemplate = new String ("/libs/cq/workflow/templates/model");
String modelName = new String("mymodel");
Page modelParent = pageManager.create(modelRepo, modelName, modelTemplate, "My workflow model");

/* create the model */
String modelId = new String(modelParent.getPath()+"/jcr:content/model")
WorkflowModel model = wfSession.createNewModel("Made using Java",modelId);

/* delete the model */
wfSession.deleteModel(modelId);
%>
```

#### 建立、讀取或刪除工作流模型 — ECMA指令碼 {#creating-reading-or-deleting-workflow-models-ecma-script}

```
var resolver = sling.getRequest().getResource().getResourceResolver();
var wfSession = resolver.adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
var pageManager = resolver.adaptTo(Packages.com.day.cq.wcm.api.PageManager);

//create the parent page node
var workflowPage = pageManager.create("/var/workflow/models", "mymodel", "/libs/cq/workflow/templates/model", "Created via ECMA Script");
var modelId = workflowPage.getPath()+ "/jcr:content/model";
//create the model
var model = wfSession.createNewModel("My Model", modelId);
//delete the model
var model = wfSession.deleteModel(modelId);
```

#### 刪除工作流模型 — 使用curl執行REST {#deleting-a-workflow-model-rest-using-curl}

```shell
# deleting the model by its id
curl -u admin:admin -X DELETE http://localhost:4502/etc/workflow/models/{id}
```

>[!NOTE]
>
>由於需要詳細程度，對於建立和/或讀取模型，curl不被視為實用。

### 檢查工作流狀態時過濾掉系統工作流 {#filtering-out-system-workflows-when-checking-workflow-status}

您可以使用 [WorkflowStatus API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html) 檢索有關節點的工作流狀態的資訊。

各種方法都有參數：

`excludeSystemWorkflows`

此參數可設為 `true` 指示應從相關結果中排除系統工作流。

您 [可以更新OSGi配置](/help/sites-deploying/configuring-osgi.md) **AdobeGranite工作流程PayloadMapCache** 指定工作流 `Models` 視為系統工作流程。 預設（執行階段）工作流模型為：

* `/var/workflow/models/scheduled_activation/jcr:content/model`
* `/var/workflow/models/scheduled_deactivation/jcr:content/model`

### 超時後的自動提前參與者步驟 {#auto-advance-participant-step-after-a-timeout}

如果您需要自動前進 **參與者** 尚未在預先定義的時間內完成的步驟，您可以：

1. 實作OSGI事件接聽程式，以監聽任務建立和修改。
1. 指定逾時（截止時間），然後建立要在該時間觸發的排程Sling工作。
1. 撰寫逾時到期時收到通知的工作處理常式，並觸發工作。

   如果任務尚未完成，此處理程式將對任務執行所需操作

>[!NOTE]
>
>必須明確界定要採取的行動，才能採用這種辦法。

### 與工作流程例項互動 {#interacting-with-workflow-instances}

以下提供如何與工作流程例項互動（程式設計）的基本範例。

#### 與工作流程例項互動 — Java {#interacting-with-workflow-instances-java}

```java
// starting a workflow
WorkflowModel model = wfSession.getModel(workflowId);
WorkflowData wfData = wfSession.newWorkflowData("JCR_PATH", repoPath);
wfSession.startWorkflow(model, wfData);

// querying and managing a workflow
Workflow[] workflows workflows = wfSession.getAllWorkflows();
Workflow workflow= wfSession.getWorkflow(id);
wfSession.suspendWorkflow(workflow);
wfSession.resumeWorkflow(workflow);
wfSession.terminateWorkflow(workflow);
```

#### 與工作流程例項互動 — ECMA指令碼 {#interacting-with-workflow-instances-ecma-script}

```
// starting a workflow
var model = wfSession.getModel(workflowId);
var wfData = wfSession.newWorkflowData("JCR_PATH", repoPath);
wfSession.startWorkflow(model, wfData);

// querying and managing a workflow
var workflows = wfSession.getWorkflows("RUNNING");
var workflow= wfSession.getWorkflow(id);
wfSession.suspendWorkflow(workflow);
wfSession.resumeWorkflow(workflow);
wfSession.terminateWorkflow(workflow);
```

#### 與工作流程例項互動 — 使用curl進行REST {#interacting-with-workflow-instances-rest-using-curl}

* **啟動工作流程**

   ```shell
   # starting a workflow
   curl -d "model={id}&payloadType={type}&payload={payload}" http://localhost:4502/etc/workflow/instances
   
   # for example:
   curl -u admin:admin -d "model=/var/workflow/models/request_for_activation&payloadType=JCR_PATH&payload=/content/we-retail/us/en/products" http://localhost:4502/etc/workflow/instances
   ```

* **列出執行個體**

   ```shell
   # listing the instances
   curl -u admin:admin http://localhost:4502/etc/workflow/instances.json
   ```

   這會列出所有例項；例如：

   ```shell
   [
       {"uri":"/var/workflow/instances/server0/2018-02-26/prototype-01_1"}
       ,{"uri":"/var/workflow/instances/server0/2018-02-26/prototype-01_2"}
   ]
   ```

   >[!NOTE]
   >
   >請參閱 [如何取得所有執行中工作流程的清單](#how-to-get-a-list-of-all-running-workflows-with-their-ids) 及其ID，以列出具有特定狀態的例項。

* **暫停工作流程**

   ```shell
   # suspending a workflow
   curl -d "state=SUSPENDED" http://localhost:4502/etc/workflow/instances/{id}
   
   # for example:
   curl -u admin:admin -d "state=SUSPENDED" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
   ```

* **繼續工作流程**

   ```shell
   # resuming a workflow
   curl -d "state=RUNNING" http://localhost:4502/etc/workflow/instances/{id}
   
   # for example:
   curl -u admin:admin -d "state=RUNNING" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
   ```

* **終止工作流實例**

   ```shell
   # terminating a workflow
   curl -d "state=ABORTED" http://localhost:4502/etc/workflow/instances/{id}
   
   # for example:
   curl -u admin:admin -d "state=ABORTED" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
   ```

### 與工作項目互動 {#interacting-with-work-items}

以下提供如何（程式化）與工作項目互動的基本範例。

#### 與工作項目互動 — Java {#interacting-with-work-items-java}

```java
// querying work items
WorkItem[] workItems = wfSession.getActiveWorkItems();
WorkItem workItem = wfSession.getWorkItem(id);

// getting routes
List<Route> routes = wfSession.getRoutes(workItem);

// delegating
Iterator<Participant> delegatees = wfSession.getDelegatees(workItem);
wfSession.delegateWorkItem(workItem, delegatees.get(0));

// completing or advancing to the next step
wfSession.complete(workItem, routes.get(0));
```

#### 與工作項目互動 — ECMA指令碼 {#interacting-with-work-items-ecma-script}

```
// querying work items
var workItems = wfSession.getActiveWorkItems();
var workItem = wfSession.getWorkItem(id);

// getting routes
var routes = wfSession.getRoutes(workItem);

// delegating
var delegatees = wfSession.getDelegatees(workItem);
wfSession.delegateWorkItem(workItem, delegatees.get(0));

// completing or advancing to the next step
wfSession.complete(workItem, routes.get(0));
```

#### 與工作項目互動 — 使用curl進行REST {#interacting-with-work-items-rest-using-curl}

* **從收件箱中列出工作項**

   ```shell
   # listing the work items
   curl -u admin:admin http://localhost:4502/bin/workflow/inbox
   ```

   將列出當前收件箱中工作項的詳細資訊；例如：

   ```shell
   [{
       "uri_xss": "/var/workflow/instances/server0/2018-02-26/prototype-01_2/workItems/node2_var_workflow_instances_server0_2018-02-26_prototype-01_2",
       "uri": "/var/workflow/instances/server0/2018-02-26/prototype-01_2/workItems/node2_var_workflow_instances_server0_2018-02-26_prototype-01_2",
       "currentAssignee_xss": "workflow-administrators",
       "currentAssignee": "workflow-administrators",
       "startTime": 1519656289274,
       "payloadType_xss": "JCR_PATH",
       "payloadType": "JCR_PATH",
       "payload_xss": "/content/we-retail/es/es",
       "payload": "/content/we-retail/es/es",
       "comment_xss": "Process resource is null",
       "comment": "Process resource is null",
       "type_xss": "WorkItem",
       "type": "WorkItem"
     },{
       "uri_xss": "configuration/configure_analyticstargeting",
       "uri": "configuration/configure_analyticstargeting",
       "currentAssignee_xss": "administrators",
       "currentAssignee": "administrators",
       "type_xss": "Task",
       "type": "Task"
     },{
       "uri_xss": "configuration/securitychecklist",
       "uri": "configuration/securitychecklist",
       "currentAssignee_xss": "administrators",
       "currentAssignee": "administrators",
       "type_xss": "Task",
       "type": "Task"
     },{
       "uri_xss": "configuration/enable_collectionofanonymoususagedata",
       "uri": "configuration/enable_collectionofanonymoususagedata",
       "currentAssignee_xss": "administrators",
       "currentAssignee": "administrators",
       "type_xss": "Task",
       "type": "Task"
     },{
       "uri_xss": "configuration/configuressl",
       "uri": "configuration/configuressl",
       "currentAssignee_xss": "administrators",
       "currentAssignee": "administrators",
       "type_xss": "Task",
       "type": "Task"
     }
   ```

* **委派工作項**

   ```xml
   # delegating
   curl -d "item={item}&delegatee={delegatee}" http://localhost:4502/bin/workflow/inbox
   
   # for example:
   curl -u admin:admin -d "item=/etc/workflow/instances/server0/2017-03-08/request_for_activation_1/workItems/node1_etc_workflow_instances_server0_2017-03-08_request_for_act_1&delegatee=administrators" http://localhost:4502/bin/workflow/inbox
   ```

   >[!NOTE]
   >
   >此 `delegatee` 必須是工作流程步驟的有效選項。

* **完成或推進工作項目到下一步**

   ```xml
   # retrieve the list of routes; the results will be similar to {"results":1,"routes":[{"rid":"233123169","label":"End","label_xss":"End"}]}
   http://localhost:4502/etc/workflow/instances/<path-to-the-workitem>.routes.json
   
   # completing or advancing to the next step; use the appropriate route ID (rid value) from the above list
   curl -d "item={item}&route={route}" http://localhost:4502/bin/workflow/inbox
   
   # for example:
   curl -u admin:admin -d "item=/etc/workflow/instances/server0/2017-03-08/request_for_activation_1/workItems/node1_etc_workflow_instances_server0_2017-03-08_request_for_activation_1&route=233123169" http://localhost:4502/bin/workflow/inbox
   ```

### 監聽工作流程事件 {#listening-for-workflow-events}

使用OSGi事件架構來監聽 [ `com.adobe.granite.workflow.event.WorkflowEvent`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/event/WorkflowEvent.html) 類定義。 此類別也提供數種有用的方法，以取得關於事件主題的資訊。 例如， `getWorkItem` 方法會傳回 `WorkItem` 事件中涉及的工作項的對象。

下列范常式式碼會定義服務，此服務會監聽工作流程事件並根據事件類型執行工作。

```java
package com.adobe.example.workflow.listeners;

import org.apache.sling.event.jobs.JobProcessor;
import org.apache.sling.event.jobs.JobUtil;

import org.osgi.service.event.Event;
import org.osgi.service.event.EventHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;

import com.adobe.granite.workflow.event.WorkflowEvent;
import com.adobe.granite.workflow.exec.WorkItem;

/**
 * The <code>WorkflowEventCatcher</code> class listens to workflow events.
 */
@Component(metatype=false, immediate=true)
@Service(value=org.osgi.service.event.EventHandler.class)
public class WorkflowEventCatcher implements EventHandler, JobProcessor {

 @Property(value=com.adobe.granite.workflow.event.WorkflowEvent.EVENT_TOPIC)
 static final String EVENT_TOPICS = "event.topics";

 private static final Logger logger = LoggerFactory.getLogger(WorkflowEventCatcher.class);

 public void handleEvent(Event event) {
  JobUtil.processJob(event, this);
 }

 public boolean process(Event event) {
  logger.info("Received event of topic: " + event.getTopic());
  String topic = event.getTopic();

  try {
   if (topic.equals(WorkflowEvent.EVENT_TOPIC)) {
    WorkflowEvent wfevent = (WorkflowEvent)event;
    String eventType = wfevent.getEventType();
    String instanceId = wfevent.getWorkflowInstanceId();

    if (instanceId != null) {
     //workflow instance events
     if (eventType.equals(WorkflowEvent.WORKFLOW_STARTED_EVENT) ||
       eventType.equals(WorkflowEvent.WORKFLOW_RESUMED_EVENT) ||
       eventType.equals(WorkflowEvent.WORKFLOW_SUSPENDED_EVENT)) {
      // your code comes here...
     } else if (
       eventType.equals(WorkflowEvent.WORKFLOW_ABORTED_EVENT) ||
       eventType.equals(WorkflowEvent.WORKFLOW_COMPLETED_EVENT)) {
      // your code comes here...
     }
     // workflow node event
     if (eventType.equals(WorkflowEvent.NODE_TRANSITION_EVENT)) {
      WorkItem currentItem = (WorkItem) event.getProperty(WorkflowEvent.WORK_ITEM);
      // your code comes here...
     }
    }
   }
  } catch(Exception e){
   logger.debug(e.getMessage());
   e.printStackTrace();
  }
  return true;
 }
}
```
