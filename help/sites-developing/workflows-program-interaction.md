---
title: 以程式設計方式與工作流程互動
seo-title: 以程式設計方式與工作流程互動
description: 'null'
seo-description: 'null'
uuid: a0f19fc6-b9bd-4b98-9c0e-fbf4f7383026
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: cb621332-a149-4f8d-9425-fd815b033c38
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 以程式設計方式與工作流程互動{#interacting-with-workflows-programmatically}

當自 [訂和擴充工作流程時](/help/sites-developing/workflows-customizing-extending.md) ，您可以存取工作流程物件：

* [使用Workflow Java API](#using-the-workflow-java-api)
* [在ECMA指令碼中獲取工作流對象](#obtaining-workflow-objects-in-ecma-scripts)
* [使用Workflow REST API](#using-the-workflow-rest-api)

## 使用Workflow Java API {#using-the-workflow-java-api}

工作流Java API由包和 [`com.adobe.granite.workflow`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/package-summary.html) 多個子包組成。 API中最重要的成員是 `com.adobe.granite.workflow.WorkflowSession` 類別。 該類 `WorkflowSession` 別可同時訪問設計時間和運行時工作流對象：

* 工作流模型
* 工作項目
* 工作流程實例
* 工作流資料
* 收件箱項目

該類還提供了幾種干預工作流生命週期的方法。

下表提供在以程式設計方式與工作流程互動時，要使用的數個關鍵Java物件參考檔案的連結。 下面的示例演示如何獲取和使用代碼中的類對象。

<table>
 <tbody>
  <tr>
   <th>功能<a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html"></a></th>
   <th>物件<br /> </th>
  </tr>
  <tr>
   <td>存取工作流程<br /> </td>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html"><code>WorkflowSession</code></a><br /> </td>
  </tr>
  <tr>
   <td>執行和查詢工作流實例<br /> </td>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html"><code>Workflow</code></a><br /> <a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkItem.html"><code>WorkItem</code></a><br /> <a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html"><code>WorkflowData</code></a><br /> </td>
  </tr>
  <tr>
   <td>管理工作流模型<br /> </td>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowModel.html"><code>WorkflowModel</code></a><br /> <a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowNode.html"><code>WorkflowNode</code></a><br /> <a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/model/WorkflowTransition.html"><code>WorkflowTransition</code></a><br /> </td>
  </tr>
  <tr>
   <td>處於工作流（或不處於）中的節點的資訊 </td>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html"><code>WorkflowStatus</code></a></td>
  </tr>
 </tbody>
</table>

## 在ECMA指令碼中獲取工作流對象 {#obtaining-workflow-objects-in-ecma-scripts}

如「尋找 [指令碼」中所述](/help/sites-developing/the-basics.md#locating-the-script),AEM（透過Apache Sling）提供執行伺服器端ECMA指令碼的ECMA指令碼引擎。 類別 [`org.apache.sling.scripting.core.ScriptHelper`](https://sling.apache.org/apidocs/sling5/org/apache/sling/scripting/core/ScriptHelper.html) 可立即供您的指令碼使用，做為變 `sling` 數。

類 `ScriptHelper` 可以訪問您最 `SlingHttpServletRequest` 終可以用來獲取對象的 `WorkflowSession` 類；例如：

```
var wfsession = sling.getRequest().getResource().getResourceResolver().adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
```

## 使用Workflow REST API {#using-the-workflow-rest-api}

Workflow Console大量使用REST API;因此，本頁面說明了工作流程的REST API。

>[!NOTE]
>
>使用curl命令行工具，可以使用Workflow REST API訪問工作流對象並管理實例生命週期。 本頁中的示例演示了如何通過捲曲命令行工具使用REST API。

REST API支援下列動作：

* 啟動或停止工作流服務
* 建立、更新或刪除工作流程模型
* [啟動、暫停、繼續或終止工作流實例](/help/sites-administering/workflows.md#workflow-status-and-actions)
* 完成或委派工作項目

>[!NOTE]
>
>使用Firefox擴充功能Firebug進行網頁開發，可在控制台運作時追蹤HTTP流量。 例如，您可以檢查參數和傳送至AEM伺服器的值並附上 `POST` 請求。

在本頁中，我們假設AEM在連接埠的localhost上 `4502` 執行，且安裝內容是&quot; `/`&quot;（根）。 如果安裝時不適用，則需相應調整HTTP請求所適用的URI。

請求支援的轉 `GET` 譯是JSON轉譯。 URL的副 `GET` 檔名應 `.json` 該為，例如：

`http://localhost:4502/etc/workflow.json`

### 管理工作流程例項 {#managing-workflow-instances}

下列HTTP請求方法適用於：

`http://localhost:4502/etc/workflow/instances`

<table>
 <tbody>
  <tr>
   <td>HTTP請求方法</td>
   <td>動作</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>列出可用的工作流實例。</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td><p>建立新的工作流程例項。 <br /> 參數包括：- <code>model</code>:相應工作流程模型的ID(URI)<br /> - <code>payloadType</code>:包含裝載的類型(例如 <code>JCR_PATH</code> 或URL)。<br /> 裝載會以參數傳送 <code>payload</code>。 ( <code>201</code> )回<code>CREATED</code>應會以位置標題傳回，其中包含新工作流程例項資源的URL。</p> </td>
  </tr>
 </tbody>
</table>

#### 按狀態管理工作流實例 {#managing-a-workflow-instance-by-its-state}

下列HTTP請求方法適用於：

`http://localhost:4502/etc/workflow/instances.{state}`

| HTTP請求方法 | 動作 |
|---|---|
| `GET` | 列出可用的工作流實例及其狀 `RUNNING`態( `SUSPENDED`、 `ABORTED` 或 `COMPLETED`) |

#### 依其ID管理工作流程例項 {#managing-a-workflow-instance-by-its-id}

下列HTTP請求方法適用於：

`http://localhost:4502/etc/workflow/instances/{id}`

<table>
 <tbody>
  <tr>
   <td>HTTP請求方法</td>
   <td>動作</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>取得例項資料（定義和中繼資料），包括到各工作流程模型的連結。</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>變更例項的狀態。 新狀態會以參數形式傳 <code>state</code> 送，且必須有下列值之一： <code>RUNNING</code>、 <code>SUSPENDED</code>或 <code>ABORTED</code>。<br /> 如果無法到達新狀態（例如，暫停終止的實例時），則 <code>409</code> (<code>CONFLICT</code>)響應會傳回給客戶端。</td>
  </tr>
 </tbody>
</table>

### 管理工作流模型 {#managing-workflow-models}

下列HTTP請求方法適用於：

`http://localhost:4502/etc/workflow/models`

<table>
 <tbody>
  <tr>
   <td>HTTP請求方法</td>
   <td>動作</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>列出可用的工作流模型。</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>建立新工作流程模型. 如果發送 <code>title</code> 參數，則使用指定標題建立新模型。 附加JSON模型定義為參數 <code>model</code> 會根據提供的定義建立新的工作流程模型。<br /> 回 <code>201</code> 應(<code>CREATED</code>)會以包含新工作流程模型資源之URL的位置標題傳回。<br /> 當模型定義附加為名為的檔案參數時，也會發生同樣的情況 <code>modelfile</code>。<br /> 在和參數兩種情況 <code>model</code> 下， <code>modelfile</code> 都需要一個名為的 <code>type</code> 附加參數來定義序列化格式。 新的序列化格式可使用OSGI API進行整合。 標準JSON序列化程式會隨工作流程引擎一起提供。 其類型為JSON。 請參閱以下格式範例。</td>
  </tr>
 </tbody>
</table>

範例：在瀏覽器中，要產生類 `http://localhost:4502/etc/workflow/models.json` 似下列的json回應的請求：

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

#### 管理特定的工作流模型 {#managing-a-specific-workflow-model}

下列HTTP請求方法適用於：

`http://localhost:4502*{uri}*`

其中 `*{uri}*` 是儲存庫中模型節點的路徑。

<table>
 <tbody>
  <tr>
   <td>HTTP請求方法</td>
   <td>動作</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>獲取模 <code>HEAD</code> 型版本（定義和元資料）。</td>
  </tr>
  <tr>
   <td><code>PUT</code></td>
   <td>更新 <code>HEAD</code> 模型版本（建立新版本）。<br /> 必須將新版本模型的完整模型定義添加為名為的參數 <code>model</code>。 此外， <code>type</code> 建立新模型時需要參數，且必須有值 <code>JSON</code>。<br /> </td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>與PUT的行為相同。 需要，因為AEM Widget不支援 <code>PUT</code> 作業。</td>
  </tr>
  <tr>
   <td><code>DELETE</code></td>
   <td>刪除模型。 為瞭解決防火牆／代理問題， <code>POST</code> 包含具有值 <code>X-HTTP-Method-Override</code> 的標題項 <code>DELETE</code> 也將被接受為請 <code>DELETE</code> 求。</td>
  </tr>
 </tbody>
</table>

範例：在瀏覽器中，傳回類似 `http://localhost:4502/var/workflow/models/publish_example.json` 於下 `json` 列程式碼之回應的請求：

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

#### 依其版本管理工作流模型 {#managing-a-workflow-model-by-its-version}

下列HTTP請求方法適用於：

`http://localhost:4502/etc/workflow/models/{id}.{version}`

| HTTP請求方法 | 動作 |
|---|---|
| `GET` | 獲取給定版本中模型的資料（如果存在）。 |

### 管理（用戶）收件箱 {#managing-user-inboxes}

下列HTTP請求方法適用於：

`http://localhost:4502/bin/workflow/inbox`

<table>
 <tbody>
  <tr>
   <td>HTTP請求方法</td>
   <td>動作</td>
  </tr>
  <tr>
   <td><code>GET</code></td>
   <td>列出用戶收件箱中的工作項目，用戶由HTTP驗證標頭標識。</td>
  </tr>
  <tr>
   <td><code>POST</code></td>
   <td>完成其URI作為參數發送的工作項 <code>item</code> ，並將相應的工作流實例推進到下一個節點（由參數定義） <code>route</code><code>backroute</code> ，或在退一步時。<br /> 如果發送 <code>delegatee</code> 了參數，則由參數標識的工作項 <code>item</code> 被委託給指定的參與者。</td>
  </tr>
 </tbody>
</table>

#### 使用WorkItem ID管理（用戶）收件箱 {#managing-a-user-inbox-by-the-workitem-id}

下列HTTP請求方法適用於：

`http://localhost:4502/bin/workflow/inbox/{id}`

| HTTP請求方法 | 動作 |
|---|---|
| `GET` | 獲取由其ID標識的收件箱的資料(定 `WorkItem` 義和元資料)。 |

## 範例 {#examples}

### 如何取得所有執行中工作流程的清單及其ID {#how-to-get-a-list-of-all-running-workflows-with-their-ids}

若要取得所有執行中工作流程的清單，請執行下列動作：

`http://localhost:4502/etc/workflow/instances.RUNNING.json`

#### 如何取得所有執行中工作流程的清單及其ID —— 使用捲動進行REST {#how-to-get-a-list-of-all-running-workflows-with-their-ids-rest-using-curl}

使用捲曲的範例：

```shell
curl -u admin:admin http://localhost:4502/etc/workflow/instances.RUNNING.json
```

結 `uri` 果中顯示的可作為其他命令 `id` 的實例；例如：

```shell
[
    {"uri":"/etc/workflow/instances/server0/2017-03-08/request_for_activation_1"}
]
```

>[!NOTE]
>
>此 `curl` 命令可用於任何 [工作流狀態](/help/sites-administering/workflows.md#workflow-status-and-actions) ，而不是 `RUNNING`。

### 如何變更工作流程標題 {#how-to-change-the-workflow-title}

要更改在工 **作流控制台的「例項** 」( **Instances** )頁籤中顯示的「工作流標題」(Workflow Title)，請發送 `POST` 命令：

* 至: `http://localhost:4502/etc/workflow/instances/{id}`

* 使用下列參數：

   * `action`:其價值必須是： `UPDATE`
   * `workflowTitle`:工作流程標題

#### 如何使用捲曲來變更工作流程標題- REST {#how-to-change-the-workflow-title-rest-using-curl}

使用捲曲的範例：

```shell
curl -u admin:admin -d "action=UPDATE&workflowTitle=myWorkflowTitle" http://localhost:4502/etc/workflow/instances/{id}

# for example
curl -u admin:admin -d "action=UPDATE&workflowTitle=myWorkflowTitle" http://localhost:4502/etc/workflow/instances/server0/2017-03-08/request_for_activation_1
```

### 如何列出所有工作流模型 {#how-to-list-all-workflow-models}

若要取得所有可用工作流程模型的清單，請執行下列動作：

`http://localhost:4502/etc/workflow/models.json`

#### 如何列出所有工作流模型——使用捲曲的REST {#how-to-list-all-workflow-models-rest-using-curl}

使用捲曲的範例：

```shell
curl -u admin:admin http://localhost:4502/etc/workflow/models.json
```

>[!NOTE]
>
>另請參 [閱管理工作流模型](#managing-workflow-models)。

### 獲取WorkflowSession對象 {#obtaining-a-workflowsession-object}

類 `com.adobe.granite.workflow.WorkflowSession` 可從對象或對 `javax.jcr.Session` 像進行 `org.apache.sling.api.resource.ResourceResolver` 調整。

#### 獲取WorkflowSession對象- Java {#obtaining-a-workflowsession-object-java}

在JSP指令碼（或Servlet類的Java代碼）中，使用HTTP請求對象獲取對 `SlingHttpServletRequest` 像，該對象提供對對象的 `ResourceResolver` 訪問。 將物件 `ResourceResolver` 調整為 `WorkflowSession`。

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

#### 獲取WorkflowSession對象- ECMA指令碼 {#obtaining-a-workflowsession-object-ecma-script}

使用變 `sling` 數來取得用 `SlingHttpServletRequest` 來取得物件的物 `ResourceResolver` 件。 將物件 `ResourceResolver` 與物件相 `WorkflowSession` 配。

```
var wfsession = sling.getRequest().getResource().getResourceResolver().adaptTo(Packages.com.adobe.granite.workflow.WorkflowSession);
```

### 建立、讀取或刪除工作流模型 {#creating-reading-or-deleting-workflow-models}

下列範例說明如何存取工作流程模型：

* Java和ECMA指令碼的代碼使用該 `WorkflowSession.createNewModel` 方法。
* curl命令可直接使用其URL訪問模型。

使用的範例：

1. 建立模型(使用ID `/var/workflow/models/mymodel/jcr:content/model`)。
1. 刪除模型。

>[!NOTE]
>
>刪除模型會將模 `deleted` 型的子節點的屬 `metaData` 性設定為 `true`。
>
>刪除不會刪除模型節點。

建立新模型時：

* 工作流模型編輯器要求模型使用以下特定的節點結構 `/var/workflow/models`。 模型的父節點必須為具有以下 `cq:Page` 屬性值 `jcr:content` 的節點類型：

   * `sling:resourceType`: `cq/workflow/components/pages/model`
   * `cq:template`: `/libs/cq/workflow/templates/model`
   建立模型時，必須首先建立此節 `cq:Page` 點，並將其節 `jcr:content` 點用作模型節點的父節點。

* 某些 `id` 方法識別模型所需的參數是儲存庫中模型節點的絕對路徑：

   `/var/workflow/models/<*model_name>*/jcr:content/model`

   >[!NOTE]
   >
   >請參 [閱如何列出所有工作流模型](#how-to-list-all-workflow-models)。

#### 建立、讀取或刪除工作流模型- Java {#creating-reading-or-deleting-workflow-models-java}

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

#### 建立、讀取或刪除工作流模型- ECMA指令碼 {#creating-reading-or-deleting-workflow-models-ecma-script}

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

#### 刪除工作流模型——使用捲曲刪除REST {#deleting-a-workflow-model-rest-using-curl}

```shell
# deleting the model by its id
curl -u admin:admin -X DELETE http://localhost:4502/etc/workflow/models/{id}
```

>[!NOTE]
>
>由於需要詳細程度，所以在建立和／或讀取模型時不認為捲曲是可行的。

### 檢查工作流狀態時過濾掉系統工作流 {#filtering-out-system-workflows-when-checking-workflow-status}

您可以使用 [WorkflowStatus API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/status/WorkflowStatus.html) ，檢索有關節點工作流狀態的資訊。

各種方法都有參數：

`excludeSystemWorkflows`

此參數可設為指 `true` 出系統工作流程應排除在相關結果之外。

您可 [以更新OSGi組態](/help/sites-deploying/configuring-osgi.md)**Adobe Granite Workflow PayloadMapCache** ，指定要視 `Models` 為系統工作流程的工作流程。 預設（執行時期）工作流程模型為：

* `/var/workflow/models/scheduled_activation/jcr:content/model`
* `/var/workflow/models/scheduled_deactivation/jcr:content/model`

### 逾時後的自動進階參與者步驟 {#auto-advance-participant-step-after-a-timeout}

如果您需要自動提前在預先定 **義時間內未完成的「參與者** 」步驟，您可以：

1. 實作OSGI事件偵聽器，以監聽任務建立和修改。
1. 指定逾時（截止日期），然後建立要在當時觸發的排程sling工作。
1. 編寫逾時到期時會通知的工作處理常式，並觸發工作。

   如果任務尚未完成，此處理程式將對任務執行所需的操作

>[!NOTE]
>
>必須明確界定要採取的行動才能採用這一辦法。

### 與工作流程例項互動 {#interacting-with-workflow-instances}

以下提供如何與工作流程例項互動（程式化）的基本範例。

#### 與工作流程例項互動- Java {#interacting-with-workflow-instances-java}

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

#### 與工作流實例交互- ECMA指令碼 {#interacting-with-workflow-instances-ecma-script}

```
// starting a workflow
var model = wfSession.getModel(workflowId);
var wfData = wfSession.newWorkflowData("JCR_PATH", repoPath);
wfSession.startWorkflow(model, wfData);

// querying and managing a workflow
var workflows = wfSession.getWorkflows(“RUNNING“);
var workflow= wfSession.getWorkflow(id);
wfSession.suspendWorkflow(workflow);
wfSession.resumeWorkflow(workflow);
wfSession.terminateWorkflow(workflow);
```

#### 與工作流程例項互動——使用捲動進行REST {#interacting-with-workflow-instances-rest-using-curl}

* **啟動工作流**

   ```shell
   # starting a workflow
   curl -d "model={id}&payloadType={type}&payload={payload}" http://localhost:4502/etc/workflow/instances
   
   # for example:
   curl -u admin:admin -d "model=/var/workflow/models/request_for_activation/jcr:content/model&payloadType=JCR_PATH&payload=/content/we-retail/us/en/products" http://localhost:4502/etc/workflow/instances
   ```

* **列出例項**

   ```shell
   # listing the instances
   curl -u admin:admin http://localhost:4502/etc/workflow/instances.json
   ```

   這將列出所有實例；例如：

   ```shell
   [
       {"uri":"/var/workflow/instances/server0/2018-02-26/prototype-01_1"}
       ,{"uri":"/var/workflow/instances/server0/2018-02-26/prototype-01_2"}
   ]
   ```

   >[!NOTE]
   >
   >如 [](#how-to-get-a-list-of-all-running-workflows-with-their-ids) 需列出具特定狀態之例項的資訊，請參閱如何取得所有執行中工作流程的ID清單。

* **暫停工作流**

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

以下提供如何與工作項目互動（程式化）的基本範例。

#### 與工作項目互動- Java {#interacting-with-work-items-java}

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

#### 與工作項目互動- ECMA指令碼 {#interacting-with-work-items-ecma-script}

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

#### 與工作項目互動——使用捲動進行REST {#interacting-with-work-items-rest-using-curl}

* **從收件箱列出工作項目**

   ```shell
   # listing the work items
   curl -u admin:admin http://localhost:4502/bin/workflow/inbox
   ```

   「收件箱」中當前工作項目的詳細資訊將列出；例如：

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

* **委託工作項目**

   ```xml
   # delegating
   curl -d "item={item}&delegatee={delegatee}" http://localhost:4502/bin/workflow/inbox
   
   # for example:
   curl -u admin:admin -d "item=/etc/workflow/instances/server0/2017-03-08/request_for_activation_1/workItems/node1_etc_workflow_instances_server0_2017-03-08_request_for_act_1&delegatee=administrators" http://localhost:4502/bin/workflow/inbox
   ```

   >[!NOTE]
   >
   >對於 `delegatee` 工作流步驟，必須是有效的選項。

* **完成或推動工作項目進入下一步**

   ```xml
   # retrieve the list of routes; the results will be similar to {"results":1,"routes":[{"rid":"233123169","label":"End","label_xss":"End"}]}
   http://localhost:4502/etc/workflow/instances/<path-to-the-workitem>.routes.json
   
   # completing or advancing to the next step; use the appropriate route ID (rid value) from the above list
   curl -d "item={item}&route={route}" http://localhost:4502/bin/workflow/inbox
   
   # for example:
   curl -u admin:admin -d "item=/etc/workflow/instances/server0/2017-03-08/request_for_activation_1/workItems/node1_etc_workflow_instances_server0_2017-03-08_request_for_activation_1&route=233123169" http://localhost:4502/bin/workflow/inbox
   ```

### 監聽工作流程事件 {#listening-for-workflow-events}

使用OSGi事件框架來監聽類定義的 [ 事 `com.adobe.granite.workflow.event.WorkflowEvent`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/event/WorkflowEvent.html) 件。 此類別也提供數種有用的方法，以取得事件主題的相關資訊。 例如，該方 `getWorkItem` 法返回 `WorkItem` 事件中涉及的工作項的對象。

下列范常式式碼定義一種服務，可監聽工作流程事件並根據事件類型執行工作。

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

