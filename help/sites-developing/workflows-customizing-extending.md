---
title: 延伸工作流程功能
seo-title: Extending Workflow Functionality
description: 延伸工作流程功能
seo-description: null
uuid: 9f4ea2a8-8b21-4e7c-ac73-dd37d9ada111
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: f23408c3-6b37-4047-9cce-0cab97bb6c5c
exl-id: 9e205912-50a6-414a-b8d4-a0865269d0e0
source-git-commit: 13f15bee38b6b4af4cd59376849810a788f0c467
workflow-type: tm+mt
source-wordcount: '3583'
ht-degree: 1%

---

# 延伸工作流程功能{#extending-workflow-functionality}

本主題說明如何為工作流程開發自訂步驟元件，以及如何以程式設計方式與工作流程互動。

建立自訂工作流程步驟涉及下列活動：

* 開發工作流程步驟元件。
* 以OSGi服務或ECMA指令碼的形式實作步驟功能。

您也可以 [從程式和指令碼中與您的工作流程互動](/help/sites-developing/workflows-program-interaction.md).

## 工作流程步驟元件 — 基本知識 {#workflow-step-components-the-basics}

工作流步驟元件定義建立工作流模型時步驟的外觀和行為：

* 工作流程Sidekick中的類別和步驟名稱。
* 工作流模型中步驟的外觀。
* 用於配置元件屬性的編輯對話框。
* 在執行階段執行的服務或指令碼。

與 [所有元件](/help/sites-developing/components.md)，工作流程步驟元件會繼承為指定的元件 `sling:resourceSuperType` 屬性。 下圖顯示 `cq:component` 構成所有工作流步驟元件基礎的節點。 此圖表也包含 **處理步驟**, **參與者步驟**，和 **動態參與者步驟** 元件，因為這些是開發自訂步驟元件最常見（和基本）的起點。

![aem_wf_componentinherit](assets/aem_wf_componentinherit.png)

>[!CAUTION]
>
>您 ***必須*** 不會變更 `/libs` 路徑。
>
>這是因為 `/libs` 下次升級執行個體時即會覆寫（而當您套用Hotfix或Feature Pack時，很可能會覆寫）。
>
>設定和其他變更的建議方法為：
>
>1. 重新建立所需項目(亦即， `/libs` 在 `/apps`
>2. 在內進行任何變更 `/apps`


此 `/libs/cq/workflow/components/model/step` 元件是 **處理步驟**, **參與者步驟**，和 **動態參與者步驟**，所有項目都會繼承下列項目：

* `step.jsp`

   此 `step.jsp` 指令碼將步驟元件添加到模型時呈現其標題。

   ![wf-22-1](assets/wf-22-1.png)

* [cq:dialog](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog)

   對話方塊包含下列標籤：

   * **常見**:來編輯標題和說明。
   * **進階**:編輯電子郵件通知屬性。

   ![wf-44](assets/wf-44.png) ![wf-45](assets/wf-45.png)

   >[!NOTE]
   >
   >當步驟元件的編輯對話框的頁簽與此預設外觀不匹配時，步驟元件具有定義的指令碼、節點屬性或對話框頁簽，這些頁簽覆蓋這些繼承的頁簽。

### ECMA指令碼 {#ecma-scripts}

ECMA指令碼中可用的對象（取決於步驟類型）如下：

* [工作項](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkItem.html) workItem
* [WorkflowSession](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/WorkflowSession.html) workflowSession
* [WorkflowData](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkflowData.html) workflowData
* `args`:陣列及進程引數。

* `sling`:存取其他osgi服務。
* `jcrSession`

### MetaDataMaps {#metadatamaps}

您可以使用工作流程中繼資料保留工作流程存留期間所需的資訊。 工作流程步驟的常見需求是保留資料以供日後在工作流程中使用，或擷取持續的資料。

有三種類型的MetaDataMap對象 — 用於 `Workflow`, `WorkflowData` 和 `WorkItem` 對象。 它們都有相同的用途 — 儲存元資料。

WorkItem有其自己的MetaDataMap，該MetaDataMap僅可在該工作項（例如步驟）運行時使用。

兩者 `Workflow` 和 `WorkflowData` 中繼資料集會在整個工作流程中共用。 針對這些情況，建議僅使用 `WorkflowData` 中繼資料地圖。

## 建立自訂工作流程步驟元件 {#creating-custom-workflow-step-components}

工作流程步驟元件可以 [以與任何其他元件相同的方式建立](/help/sites-developing/components.md).

要繼承（現有）基本步驟元件之一，請將以下屬性添加到 `cq:Component` 節點：

* 名稱: `sling:resourceSuperType`
* 類型: `String`
* 值：下列路徑之一，解析為基礎元件：

   * `cq/workflow/components/model/process`
   * `cq/workflow/components/model/participant`
   * `cq/workflow/components/model/dynamic_participant`

### 指定步驟實例的預設標題和說明 {#specifying-the-default-title-and-description-for-step-instances}

請依照下列步驟，指定 **標題** 和 **說明** 欄位 **常見** 標籤。

>[!NOTE]
>
>滿足以下兩項要求時，欄位值將出現在步驟實例中：
>
>* 步驟的編輯對話框將標題和說明儲存在以下位置：>
>* `./jcr:title`
>* `./jcr:description` 位置
>
>  當編輯對話框使用「公用」頁簽時，即滿足此要求 `/libs/cq/flow/components/step/step` 元件實作。
>
>* 該元件的步驟元件或上階不會覆寫 `step.jsp` 指令碼 `/libs/cq/flow/components/step/step` 元件實作。


1. 在 `cq:Component` 節點，添加以下節點：

   * 名稱: `cq:editConfig`
   * 類型: `cq:EditConfig`

   >[!NOTE]
   >
   >如需cq:editConfig節點的詳細資訊，請參閱 [設定元件的編輯行為](/help/sites-developing/developing-components.md#configuring-the-edit-behavior).

1. 在 `cq:EditConfig` 節點，添加以下節點：

   * 名稱: `cq:formParameters`
   * 類型: `nt:unstructured`

1. 新增 `String` 屬性 `cq:formParameters` 節點：

   * `jcr:title`:值會填入 **標題** 欄位 **常見** 標籤。
   * `jcr:description`:值會填入 **說明** 欄位 **常見** 標籤。

### 在工作流元資料中儲存屬性值 {#saving-property-values-in-workflow-metadata}

>[!NOTE]
>
>請參閱 [保存和訪問資料](#persisting-and-accessing-data). 尤其是，如需在執行階段存取屬性值的相關資訊，請參閱 [在運行時訪問對話框屬性值](#accessing-dialog-property-values-at-runtime).

名稱屬性 `cq:Widget` 項目會指定儲存介面工具集值的JCR節點。 工作流程步驟元件對話方塊中的介面工具集將值儲存在 `./metaData` 節點，則值會新增至工作流程 `MetaDataMap`.

例如，對話方塊中的文字欄位是 `cq:Widget` 具有以下屬性的節點：

| 名稱 | 類型 | 值 |
|---|---|---|
| `xtype` | `String` | `textarea` |
| `name` | `String` | `./metaData/subject` |
| `fieldLabel` | `String` | `Email Subject` |

此文本欄位中指定的值將添加到工作流實例的 ` [MetaDataMap](#metadatamaps)` 對象，並且與 `subject` 鍵。

>[!NOTE]
>
>當金鑰為 `PROCESS_ARGS`，此值即可透過 `args` 變數。 在此情況下，name屬性的值為 `./metaData/PROCESS_ARGS.`

### 覆寫步驟實作 {#overriding-the-step-implementation}

每個基本步驟元件都使工作流模型開發人員能夠在設計時配置以下主要功能：

* 處理步驟：要在執行階段執行的服務或ECMA指令碼。
* 參與者步驟：為生成的工作項分配的用戶ID。
* 動態參與者步驟：選擇為工作項分配的用戶ID的服務或ECMA指令碼。

若要將元件集中用於特定工作流程案例，請在設計中設定關鍵功能，並移除模型開發人員可加以變更的功能。

1. 在cq:component節點下方新增下列節點：

   * 名稱: `cq:editConfig`
   * 類型: `cq:EditConfig`

   如需cq:editConfig節點的詳細資訊，請參閱 [設定元件的編輯行為](/help/sites-developing/developing-components.md#configuring-the-edit-behavior).

1. 在cq:EditConfig節點下方新增下列節點：

   * 名稱: `cq:formParameters`
   * 類型: `nt:unstructured`

1. 新增 `String` 屬性 `cq:formParameters` 節點。 元件超類型決定屬性的名稱：

   * 程序步驟: `PROCESS`
   * 參與者步驟: `PARTICIPANT`
   * 動態參與者步驟: `DYNAMIC_PARTICIPANT`

1. 指定屬性的值：

   * `PROCESS`:實作步驟行為之服務的ECMA指令碼或PID的路徑。
   * `PARTICIPANT`:為工作項分配的用戶的ID。
   * `DYNAMIC_PARTICIPANT`:ECMA指令碼的路徑或服務的PID，用於選擇用戶來分配工作項。

1. 要移除模型開發人員更改屬性值的能力，請覆蓋元件超類型的對話框。

### 將Forms和對話框添加到參與者步驟 {#adding-forms-and-dialogs-to-participant-steps}

自定義參與者步驟元件以提供 [表單參與者步驟](/help/sites-developing/workflows-step-ref.md#form-participant-step) 和 [對話參與者步驟](/help/sites-developing/workflows-step-ref.md#dialog-participant-step) 元件：

* 在用戶開啟生成的工作項時向用戶呈現表單。
* 當使用者完成產生的工作項目時，向使用者呈現自訂對話方塊。

對新元件執行下列程式(請參閱 [建立自訂工作流程步驟元件](#creating-custom-workflow-step-components)):

1. 在 `cq:Component` 節點，添加以下節點：

   * 名稱: `cq:editConfig`
   * 類型: `cq:EditConfig`

   如需cq:editConfig節點的詳細資訊，請參閱 [設定元件的編輯行為](/help/sites-developing/components-basics.md#edit-behavior).

1. 在cq:EditConfig節點下方新增下列節點：

   * 名稱: `cq:formParameters`
   * 類型: `nt:unstructured`

1. 若要在使用者開啟工作項目時呈現表單，請將下列屬性新增至 `cq:formParameters` 節點：

   * 名稱: `FORM_PATH`
   * 類型: `String`
   * 值：解析至表單的路徑

1. 若要在使用者完成工作項目時顯示自訂對話方塊，請將下列屬性新增至 `cq:formParameters` 節點

   * 名稱: `DIALOG_PATH`
   * 類型: `String`
   * 值：解析到對話框的路徑

### 配置工作流步驟運行時行為 {#configuring-the-workflow-step-runtime-behavior}

在 `cq:Component` 節點，添加 `cq:EditConfig` 節點。 在下方新增 `nt:unstructured` 節點(必須命名 `cq:formParameters`)和新增下列屬性至該節點：

* 名稱: `PROCESS_AUTO_ADVANCE`

   * 類型: `Boolean`
   * 值:

      * 設為 `true` 工作流程將執行該步驟並繼續 — 此為預設值，也建議使用
      * when `false`，工作流程將執行並停止；這需要額外的處理 `true` 建議

* 名稱: `DO_NOTIFY`

   * 類型: `Boolean`
   * 值：指出是否應針對使用者參與步驟傳送電子郵件通知（並假設郵件伺服器已正確設定）

## 保存和訪問資料 {#persisting-and-accessing-data}

### 保留後續工作流程步驟的資料 {#persisting-data-for-subsequent-workflow-steps}

您可以使用工作流程中繼資料保留在工作流程存留期期間以及步驟之間所需的資訊。 工作流程步驟的常見要求是保留資料以供日後使用，或從先前步驟擷取持續保存的資料。

工作流程中繼資料儲存在 [`MetaDataMap`](#metadatamaps) 物件。 Java API提供 [`Workflow.getWorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html) 返回方法 [`WorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html) 提供適當 `MetaDataMap` 物件。 此 `WorkflowData` `MetaDataMap` 物件可供步驟元件的OSGi服務或ECMA指令碼使用。

#### Java {#java}

的執行方法 `WorkflowProcess` 實作已傳遞 `WorkItem` 物件。 使用此物件來取得 `WorkflowData` 物件。 以下範例將項目新增至工作流程 `MetaDataMap` 物件，然後記錄每個項目。 (「mykey」、「My Step Value」)項目可用於工作流程中的後續步驟。

```java
public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {

    MetaDataMap wfd = item.getWorkflow().getWorkflowData().getMetaDataMap();

    wfd.put("mykey", "My Step Value");

    Set<String> keyset = wfd.keySet();
    Iterator<String> i = keyset.iterator();
    while (i.hasNext()){
     Object key = i.next();
     log.info("The workflow medata includes key {} and value {}",key.toString(),wfd.get(key).toString());
    }
}
```

#### ECMA 指令碼 {#ecma-script}

此 `graniteWorkItem` 變數是目前的ECMA指令碼表示 `WorkItem` Java對象。 因此，您可以使用 `graniteWorkItem` 變數取得工作流程中繼資料。 以下ECMA指令碼可用於實作 **處理步驟** 將項目新增至工作流 `MetaDataMap` 物件，然後記錄每個項目。 然後，這些項目便可供工作流程中的後續步驟使用。

>[!NOTE]
>
>此 `metaData` 步驟指令碼立即可用的變數是步驟的中繼資料。 步驟中繼資料與工作流程中繼資料不同。

```
var currentDateInMillis = new Date().getTime();

graniteWorkItem.getWorkflowData().getMetaDataMap().put("hardcodedKey","theKey");

graniteWorkItem.getWorkflowData().getMetaDataMap().put("currentDateInMillisKey",currentDateInMillis);

var iterator = graniteWorkItem.getWorkflowData().getMetaDataMap().keySet().iterator();
while (iterator.hasNext()){
    var key = iterator.next();
    log.info("Workflow metadata key, value = " + key.toString() + ", " + graniteWorkItem.getWorkflowData().getMetaDataMap().get(key));
}
```

### 在運行時訪問對話框屬性值 {#accessing-dialog-property-values-at-runtime}

此 `MetaDataMap` 工作流實例的對象對於在整個工作流的整個生命週期中儲存和檢索資料非常有用。 對於工作流程步驟元件實施， `MetaDataMap` 對於在運行時檢索元件屬性值特別有用。

>[!NOTE]
>
>有關配置元件對話框以將屬性儲存為工作流元資料的資訊，請參見 [在工作流元資料中儲存屬性值](#saving-property-values-in-workflow-metadata).

工作流程 `MetaDataMap` 適用於Java和ECMA指令碼程式實施：

* 在WorkflowProcess介面的Java實施中， `args` 參數為 `MetaDataMap` 物件。

* 在ECMA指令碼實作中，值可使用 `args` 和 `metadata` 變數。

### 範例：檢索進程步驟元件的參數 {#example-retrieving-the-arguments-of-the-process-step-component}

編輯對話方塊 **處理步驟** 元件包括 **引數** 屬性。 的值 **引數** 屬性儲存在工作流元資料中，並與 `PROCESS_ARGS` 鍵。

在下圖中， **引數** 屬性為 `argument1, argument2`:

![wf-24](assets/wf-24.png)

#### Java {#java-1}

以下Java程式碼為 `execute` 方法 `WorkflowProcess` 實作。 方法會將值記錄在 `args` `MetaDataMap` 與 `PROCESS_ARGS` 鍵。

```java
public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {
     if (args.containsKey("PROCESS_ARGS")){
      log.info("workflow metadata for key PROCESS_ARGS and value {}",args.get("PROCESS_ARGS","string").toString());
     }
    }
```

執行使用此Java實作的程式步驟時，記錄檔會包含下列項目：

```xml
16.02.2018 12:07:39.566 *INFO* [JobHandler: /var/workflow/instances/server0/2018-02-16/model_855140139900189:/content/we-retail/de] com.adobe.example.workflow.impl.process.LogArguments workflow metadata for key PROCESS_ARGS and value argument1, argument2
```

#### ECMA 指令碼 {#ecma-script-1}

以下ECMA指令碼是 **處理步驟**. 它會記錄引數和引數值：

```
var iterator = graniteWorkItem.getWorkflowData().getMetaDataMap().keySet().iterator();
while (iterator.hasNext()){
    var key = iterator.next();
    log.info("Workflow metadata key, value = " + key.toString() + ", " + graniteWorkItem.getWorkflowData().getMetaDataMap().get(key));
}
log.info("hardcodedKey "+ graniteWorkItem.getWorkflowData().getMetaDataMap().get("hardcodedKey"));
log.info("currentDateInMillisKey "+ graniteWorkItem.getWorkflowData().getMetaDataMap().get("currentDateInMillisKey"));
```

>[!NOTE]
>
>本節說明如何使用流程步驟的參數。 此資訊也適用於動態參與者選擇器。

>[!NOTE]
>有關在工作流元資料中儲存元件屬性的另一個示例，請參閱示例：建立記錄器工作流程步驟。 此範例提供一個對話方塊，將中繼資料值與PROCESS_ARGS以外的索引鍵建立關聯。

### 指令碼和進程參數 {#scripts-and-process-arguments}

在 **處理步驟** 元件，引數可透過 `args` 物件。

建立自訂步驟元件時，物件 `metaData` 在指令碼中可用。 此物件僅限於單一字串引數。

## 開發流程步驟實施 {#developing-process-step-implementations}

在工作流程處理期間啟動處理步驟時，這些步驟會向OSGi服務發送請求或執行ECMA指令碼。 開發執行工作流程所需動作的服務或ECMA指令碼。

>[!NOTE]
>
>有關將流程步驟元件與服務或指令碼關聯的資訊，請參見 [處理步驟](/help/sites-developing/workflows-step-ref.md#process-step) 或 [覆寫步驟實作](#overriding-the-step-implementation).

### 使用Java類實施處理步驟 {#implementing-a-process-step-with-a-java-class}

要將流程步驟定義為OSGI服務元件（Java套件）:

1. 建立套件組合併將其部署至OSGI容器。 請參閱關於使用建立套件組合的檔案 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) 或 [Eclipse](/help/sites-developing/howto-projects-eclipse.md).

   >[!NOTE]
   >
   >OSGI元件需要實作 `WorkflowProcess` 介面 `execute()` 方法。 請參閱下方的范常式式碼。

   >[!NOTE]
   >
   >套件名稱需要新增至 `<*Private-Package*>` 區段 `maven-bundle-plugin` 設定。

1. 添加SCR屬性 `process.label`  並視需要設定值。 這將是使用通用程式時，程式步驟所列的名稱 **處理步驟** 元件。 請參閱下列範例。
1. 在 **模型** 編輯器中，使用通用工具將處理步驟新增至工作流程 **處理步驟** 元件。
1. 在編輯對話方塊中( **處理步驟**)，前往 **程式** 標籤，然後選取您的程式實作。
1. 如果您在程式碼中使用引數，請設定 **處理參數**. 例如：false。
1. 為步驟和工作流模型（模型編輯器的左上角）保存更改。

Java方法（分別是實現可執行Java方法的類）註冊為OSGI服務，使您能夠在運行時隨時添加方法。

以下OSGI元件新增屬性 `approved` 當裝載為頁面時傳至頁面內容節點：

```java
package com.adobe.example.workflow.impl.process;

import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.exec.WorkflowData;
import com.adobe.granite.workflow.exec.WorkflowProcess;
import com.adobe.granite.workflow.metadata.MetaDataMap;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;

import org.osgi.framework.Constants;

import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

/**
 * Sample workflow process that sets an <code>approve</code> property to the payload based on the process argument value.
 */
@Component
@Service
public class MyProcess implements WorkflowProcess {

 @Property(value = "An example workflow process implementation.")
 static final String DESCRIPTION = Constants.SERVICE_DESCRIPTION;
 @Property(value = "Adobe")
 static final String VENDOR = Constants.SERVICE_VENDOR;
 @Property(value = "My Sample Workflow Process")
 static final String LABEL="process.label";

 private static final String TYPE_JCR_PATH = "JCR_PATH";

 public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {
  WorkflowData workflowData = item.getWorkflowData();
  if (workflowData.getPayloadType().equals(TYPE_JCR_PATH)) {
   String path = workflowData.getPayload().toString() + "/jcr:content";
   try {
    Session jcrSession = session.adaptTo(Session.class);
    Node node = (Node) jcrSession.getItem(path);
    if (node != null) {
     node.setProperty("approved", readArgument(args));
     jcrSession.save();
    }
   } catch (RepositoryException e) {
    throw new WorkflowException(e.getMessage(), e);
   }
  }
 }

 private boolean readArgument(MetaDataMap args) {
  String argument = args.get("PROCESS_ARGS", "false");
  return argument.equalsIgnoreCase("true");
 }
}
```

>[!NOTE]
>
>如果流程連續失敗三次，則會將項目放在工作流程管理員的收件匣中。

### 使用ECMAScript {#using-ecmascript}

ECMA指令碼可讓指令碼開發人員實作程式步驟。 指令碼位於JCR存放庫中，並從中執行。

下表列出可立即用於處理指令碼的變數，以提供對工作流Java API對象的訪問。

| Java類 | 指令碼變數名稱 | 說明 |
|---|---|---|
| `com.adobe.granite.workflow.exec.WorkItem` | `graniteWorkItem` | 目前的步驟例項。 |
| `com.adobe.granite.workflow.WorkflowSession` | `graniteWorkflowSession` | 目前步驟例項的工作流程工作階段。 |
| `String[]` （包含進程參數） | `args` | 步驟引數。 |
| `com.adobe.granite.workflow.metadata.MetaDataMap` | `metaData` | 目前步驟例項的中繼資料。 |
| `org.apache.sling.scripting.core.impl.InternalScriptHelper` | `sling` | 提供Sling執行階段環境的存取權。 |

下列範例指令碼示範如何存取代表工作流程裝載的JCR節點。 此 `graniteWorkflowSession` 變數適用於JCR工作階段變數，用於從裝載路徑取得節點。

```
var workflowData = graniteWorkItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH") {
    var path = workflowData.getPayload().toString();
    var jcrsession = graniteWorkflowSession.adaptTo(Packages.javax.jcr.Session);
    var node = jcrsession.getNode(path);
    if (node.hasProperty("approved")){
     node.setProperty("approved", args[0] == "true" ? true : false);
     node.save();
 }
}
```

下列指令碼會檢查裝載是否為影像( `.png` 檔案)，從中建立黑白影像，並將其另存為同層節點。

```
var workflowData = graniteWorkItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH") {
    var path = workflowData.getPayload().toString();
    var jcrsession = graniteWorkflowSession.adaptTo(Packages.javax.jcr.Session);
    var node = jcrsession.getRootNode().getNode(path.substring(1));
     if (node.isNodeType("nt:file") && node.getProperty("jcr:content/jcr:mimeType").getString().indexOf("image/") == 0) {
        var is = node.getProperty("jcr:content/jcr:data").getStream();
        var layer = new Packages.com.day.image.Layer(is);
        layer.grayscale();
                var parent = node.getParent();
                var gn = parent.addNode("grey" + node.getName(), "nt:file");
        var content = gn.addNode("jcr:content", "nt:resource");
                content.setProperty("jcr:mimeType","image/png");
                var cal = Packages.java.util.Calendar.getInstance();
                content.setProperty("jcr:lastModified",cal);
                var f = Packages.java.io.File.createTempFile("test",".png");
        var tout = new Packages.java.io.FileOutputStream(f);
        layer.write("image/png", 1.0, tout);
        var fis = new Packages.java.io.FileInputStream(f);
                content.setProperty("jcr:data", fis);
                parent.save();
        tout.close();
        fis.close();
        is.close();
        f.deleteOnExit();
    }
}
```

要使用指令碼：

1. 建立指令碼(例如，含有CRXDE Lite)並儲存至下方的存放庫 `//apps/workflow/scripts/`
1. 若要指定標題，以在 **處理步驟** 編輯對話框，將以下屬性添加到 `jcr:content` 指令碼的節點：

   | 名稱 | 類型 | 值 |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | 要在編輯對話方塊中顯示的名稱。 |

1. 編輯 **處理步驟** 例項，並指定要使用的指令碼。

## 開發參與者選擇器 {#developing-participant-choosers}

您可以開發參與者選擇器 **動態參與者步驟** 元件。

當 **動態參與者步驟** 元件在工作流期間啟動，該步驟需要確定可將生成的工作項分配給哪個參與者。 要執行此操作，請執行以下任一步驟：

* 傳送要求至OSGi服務
* 執行ECMA指令碼以選擇參與者

您可以開發服務或ECMA指令碼，以根據工作流的要求選擇參與者。

>[!NOTE]
>
>如需關於將 **動態參與者步驟** 包含服務或指令碼的元件，請參閱 [動態參與者步驟](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step) 或 [覆寫步驟實作](#persisting-and-accessing-data).

### 使用Java類開發參與者選擇器 {#developing-a-participant-chooser-using-a-java-class}

要將參與者步驟定義為OSGI服務元件（Java類），請執行以下操作：

1. OSGI元件需要實作 `ParticipantStepChooser` 介面 `getParticipant()` 方法。 請參閱下方的范常式式碼。

   建立套件組合併將其部署至OSGI容器。

1. 添加SCR屬性 `chooser.label` 並視需要設定值。 這將是列出參與者選擇器的名稱，使用 **動態參與者步驟** 元件。 請參閱範例：

   ```java
   package com.adobe.example.workflow.impl.process;
   
   import com.adobe.granite.workflow.WorkflowException;
   import com.adobe.granite.workflow.WorkflowSession;
   import com.adobe.granite.workflow.exec.ParticipantStepChooser;
   import com.adobe.granite.workflow.exec.WorkItem;
   import com.adobe.granite.workflow.exec.WorkflowData;
   import com.adobe.granite.workflow.metadata.MetaDataMap;
   
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   
   import org.osgi.framework.Constants;
   
   /**
    * Sample dynamic participant step that determines the participant based on a path given as argument.
    */
   @Component
   @Service
   
   public class MyDynamicParticipant implements ParticipantStepChooser {
   
    @Property(value = "An example implementation of a dynamic participant chooser.")
    static final String DESCRIPTION = Constants.SERVICE_DESCRIPTION;
       @Property(value = "Adobe")
       static final String VENDOR = Constants.SERVICE_VENDOR;
       @Property(value = "Dynamic Participant Chooser Process")
       static final String LABEL=ParticipantStepChooser.SERVICE_PROPERTY_LABEL;
   
       private static final String TYPE_JCR_PATH = "JCR_PATH";
   
       public String getParticipant(WorkItem workItem, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
           WorkflowData workflowData = workItem.getWorkflowData();
           if (workflowData.getPayloadType().equals(TYPE_JCR_PATH)) {
               String path = workflowData.getPayload().toString();
               String pathFromArgument = args.get("PROCESS_ARGS", String.class);
               if (pathFromArgument != null && path.startsWith(pathFromArgument)) {
                   return "admin";
               }
           }
           return "administrators";
       }
   }
   ```

1. 在 **模型** 編輯器中，使用通用工具將動態參與者步驟添加到工作流中 **動態參與者步驟** 元件。
1. 在編輯對話方塊中，選取 **參與者選擇器** 標籤，然後選取您的選擇器實作。
1. 如果您在程式碼中使用引數，請設定 **處理參數**. 在此範例中： `/content/we-retail/de`.
1. 為步驟和工作流模型保存更改。

### 使用ECMA指令碼開發參與者選擇器 {#developing-a-participant-chooser-using-an-ecma-script}

您可以建立ECMA指令碼，以選取指派給該工作項目的使用者 **參與者步驟** 產生。 指令碼必須包含名為 `getParticipant` 不需要引數，並傳回 `String` 包含使用者或群組的ID。

指令碼位於JCR存放庫中，並從中執行。

下表列出可讓您立即存取指令碼中的工作流程Java物件的變數。

| Java類 | 指令碼變數名稱 |
|---|---|
| `com.adobe.granite.workflow.exec.WorkItem` | `graniteWorkItem` |
| `com.adobe.granite.workflow.WorkflowSession` | `graniteWorkflowSession` |
| `String[]` （包含進程參數） | `args` |
| `com.adobe.granite.workflow.metadata.MetaDataMap` | `metaData` |
| `org.apache.sling.scripting.core.impl.InternalScriptHelper` | `sling` |

```
function getParticipant() {
    var workflowData = graniteWorkItem.getWorkflowData();
    if (workflowData.getPayloadType() == "JCR_PATH") {
        var path = workflowData.getPayload().toString();
        if (path.indexOf("/content/we-retail/de") == 0) {
            return "admin";
        } else {
            return "administrators";
        }
    }
}
```

1. 建立指令碼(例如，含有CRXDE Lite)並儲存至下方的存放庫 `//apps/workflow/scripts`
1. 若要指定標題，以在 **處理步驟** 編輯對話框，將以下屬性添加到 `jcr:content` 指令碼的節點：

   | 名稱 | 類型 | 值 |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | 要在編輯對話方塊中顯示的名稱。 |

1. 編輯 [動態參與者步驟](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step) 例項，並指定要使用的指令碼。

## 處理工作流程套件 {#handling-workflow-packages}

[工作流程套件](/help/sites-authoring/workflows-applying.md#specifying-workflow-details-in-the-create-workflow-wizard) 可傳遞至工作流程以進行處理。 工作流程套件包含資源（例如頁面和資產）的參考。

>[!NOTE]
>
>以下工作流程處理步驟接受要啟動大量頁面的工作流程套件：
>
>* [`com.day.cq.wcm.workflow.process.ActivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/ActivatePageProcess.html)
>* [`com.day.cq.wcm.workflow.process.DeactivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/DeactivatePageProcess.html)
>


您可以開發工作流程步驟來取得套件資源並加以處理。 下列 `com.day.cq.workflow.collection` 包提供對工作流包的訪問：

* `ResourceCollection`:工作流程包類。
* `ResourceCollectionUtil`:用於檢索ResourceCollection對象。
* `ResourceCollectionManager`:建立並擷取集合。 實作會部署為OSGi服務。

下列範例Java類示範如何取得套件資源：

```java
package com.adobe.example;

import java.util.ArrayList;
import java.util.List;

import com.day.cq.workflow.WorkflowException;
import com.day.cq.workflow.WorkflowSession;
import com.day.cq.workflow.collection.ResourceCollection;
import com.day.cq.workflow.collection.ResourceCollectionManager;
import com.day.cq.workflow.collection.ResourceCollectionUtil;
import com.day.cq.workflow.exec.WorkItem;
import com.day.cq.workflow.exec.WorkflowData;
import com.day.cq.workflow.exec.WorkflowProcess;
import com.day.cq.workflow.metadata.MetaDataMap;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Reference;
import org.osgi.framework.Constants;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import javax.jcr.Node;
import javax.jcr.PathNotFoundException;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

@Component
@Service
public class LaunchBulkActivate implements WorkflowProcess {

 private static final Logger log = LoggerFactory.getLogger(LaunchBulkActivate.class);

 @Property(value="Bulk Activate for Launches")
  static final String PROCESS_NAME ="process.label";
 @Property(value="A sample workflow process step to support Launches bulk activation of pages")
 static final String SERVICE_DESCRIPTION = Constants.SERVICE_DESCRIPTION;

 @Reference
 private ResourceCollectionManager rcManager;
public void execute(WorkItem workItem, WorkflowSession workflowSession) throws Exception {
    Session session = workflowSession.getSession();
    WorkflowData data = workItem.getWorkflowData();
    String path = null;
    String type = data.getPayloadType();
    if (type.equals(TYPE_JCR_PATH) && data.getPayload() != null) {
        String payloadData = (String) data.getPayload();
        if (session.itemExists(payloadData)) {
            path = payloadData;
        }
    } else if (data.getPayload() != null && type.equals(TYPE_JCR_UUID)) {
        Node node = session.getNodeByUUID((String) data.getPayload());
        path = node.getPath();
    }

    // CUSTOMIZED CODE IF REQUIRED....

    if (path != null) {
        // check for resource collection
        ResourceCollection rcCollection = ResourceCollectionUtil.getResourceCollection((Node)session.getItem(path), rcManager);
        // get list of paths to replicate (no resource collection: size == 1
        // otherwise size >= 1
        List<String> paths = getPaths(path, rcCollection);
        for (String aPath: paths) {

            // CUSTOMIZED CODE....

        }
    } else {
        log.warn("Cannot process because path is null for this " + "workitem: " + workItem.toString());
    }
}

/**
 * helper
 */
private List<String> getPaths(String path, ResourceCollection rcCollection) {
    List<String> paths = new ArrayList<String>();
    if (rcCollection == null) {
        paths.add(path);
    } else {
        log.debug("ResourceCollection detected " + rcCollection.getPath());
        // this is a resource collection. the collection itself is not
        // replicated. only its members
        try {
            List<Node> members = rcCollection.list(new String[]{"cq:Page", "dam:Asset"});
            for (Node member: members) {
                String mPath = member.getPath();
                paths.add(mPath);
            }
        } catch(RepositoryException re) {
            log.error("Cannot build path list out of the resource collection " + rcCollection.getPath());
        }
    }
    return paths;
}
}
```

## 範例：建立自訂步驟 {#example-creating-a-custom-step}

開始建立您自己的自訂步驟的簡單方式，是複製現有步驟的來源：

`/libs/cq/workflow/components/model`

### 建立基本步驟 {#creating-the-basic-step}

1. 在/apps下重新建立路徑；例如：

   `/apps/cq/workflow/components/model`

   新資料夾的類型 `nt:folder`:

   ```xml
   - apps
     - cq
       - workflow (nt:folder)
         - components (nt:folder)
           - model (nt:folder)
   ```

   >[!NOTE]
   >
   >此步驟不適用於傳統UI模型編輯器。

1. 然後將複製的步驟放入/apps資料夾中；例如：

   `/apps/cq/workflow/components/model/myCustomStep`

   以下是我們自訂步驟範例的結果：

   ![wf-34](assets/wf-34.png)

   >[!CAUTION]
   >
   >因為在標準UI中，卡片上不會顯示標題而非詳細資訊， `details.jsp` 不像傳統UI編輯器那樣需要。

1. 將下列屬性套用至節點：

   `/apps/cq/workflow/components/model/myCustomStep`

   **權益物業：**

   * `sling:resourceSuperType`

      必須繼承現有步驟。

      在此範例中，我們繼承了 `cq/workflow/components/model/step`，但您可以使用其他超類型，例如 `participant`, `process`、等

   * `jcr:title`

      是在步驟瀏覽器中列出元件時顯示的標題（工作流模型編輯器的左側面板）。

   * `cq:icon`

      用於指定 [珊瑚表徵圖](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) 的下界。

   * `componentGroup`

      必須是下列其中一項：

      * Collaboration 工作流程
      * DAM 工作流程
      * 表單工作流程
      * 專案
      * WCM 工作流程
      * 工作流程

   ![wf-35](assets/wf-35.png)

1. 您現在可以開啟工作流程模型進行編輯。 在步驟瀏覽器中，您可以篩選以查看 **我的自訂步驟**:

   ![wf-36](assets/wf-36.png)

   拖曳 **我的自訂步驟** 在模型上會顯示「 」卡片：

   ![wf-37](assets/wf-37.png)

   若否 `cq:icon` 已為步驟定義，則會使用標題的前兩個字母呈現預設圖示。 例如：

   ![wf-38](assets/wf-38.png)

#### 定義步驟配置對話框 {#defining-the-step-configure-dialog}

之後 [建立基本步驟](#creating-the-basic-step)，定義步驟 **設定** 對話框如下：

1. 在節點上配置屬性 `cq:editConfig` 如下所示：

   **權益物業：**

   * `cq:inherit`

      設為時 `true`，則您的步驟元件將繼承您在 `sling:resourceSuperType`.

   * `cq:disableTargeting`

      視需要設定。
   ![wf-39](assets/wf-39.png)

1. 在節點上配置屬性 `cq:formsParameter` 如下所示：

   **權益物業：**

   * `jcr:title`

      在模型圖和 **標題** 欄位 **我的自訂 — 步驟屬性** 配置對話框。

   * 您也可以定義自己的自訂屬性。

   ![wf-40](assets/wf-40.png)

1. 在節點上配置屬性 `cq:listeners`.

   此 `cq:listener` 節點及其屬性可讓您設定對觸控式UI模型編輯器中的事件做出反應的事件處理常式；例如將步驟拖曳至模型頁面或編輯步驟屬性。

   **權益物業：**

   * `afterMove: REFRESH_PAGE`
   * `afterdelete: CQ.workflow.flow.Step.afterDelete`
   * `afteredit: CQ.workflow.flow.Step.afterEdit`
   * `afterinsert: CQ.workflow.flow.Step.afterInsert`

   此設定是編輯器正常運作的必要項目。 在大多數情況下，此設定不得變更。

   不過，設定 `cq:inherit` 設為true(在 `cq:editConfig` 節點，請參閱上文)，可讓您繼承此設定，而無須將其明確納入步驟定義中。 如果沒有繼承，則您需要使用下列屬性和值來新增此節點。

   在此範例中，已啟動繼承，因此我們可以移除 `cq:listeners` 節點，且步驟仍可正常運作。

   ![wf-41](assets/wf-41.png)

1. 您現在可以將步驟的例項新增至工作流程模型。 當您 **設定** 您將看到對話方塊的步驟：

   ![wf-42](assets/wf-42.png) ![wf-43](assets/wf-43.png)

#### 此示例中使用的標注示例 {#sample-markup-used-in-this-example}

自訂步驟的標籤會顯示在 `.content.xml` 元件根節點。 範例 `.content.xml` 用於此範例：

`/apps/cq/workflow/components/model/myCustomStep/.content.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    cq:icon="bell"
    jcr:primaryType="cq:Component"
    jcr:title="My Custom Step"
    sling:resourceSuperType="cq/workflow/components/model/process"
    allowedParents="[*/parsys]"
    componentGroup="Workflow"/>
```

此 `_cq_editConfig.xml` 此範例中使用的範例：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    cq:disableTargeting="{Boolean}true"
    cq:inherit="{Boolean}true"
    jcr:primaryType="cq:EditConfig">
    <cq:formParameters
        jcr:primaryType="nt:unstructured"
        jcr:title="My Custom Step Card"
        SAMPLE_PROPERY="sample value"/>
    <cq:listeners
        jcr:primaryType="cq:EditListenersConfig"
        afterdelete="CQ.workflow.flow.Step.afterDelete"
        afteredit="CQ.workflow.flow.Step.afterEdit"
        afterinsert="CQ.workflow.flow.Step.afterInsert"
        afterMove="REFRESH_PAGE"/>
</jcr:root>
```

此 `_cq_dialog/.content.xml` 此範例中使用的範例：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    jcr:title="My Custom - Step Properties"
    sling:resourceType="cq/gui/components/authoring/dialog">
    <content
        jcr:primaryType="nt:unstructured"
        sling:resourceType="granite/ui/components/coral/foundation/tabs">
        <items jcr:primaryType="nt:unstructured">
            <common
                cq:hideOnEdit="true"
                jcr:primaryType="nt:unstructured"
                jcr:title="Common"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns"/>
            <process
                cq:hideOnEdit="true"
                jcr:primaryType="nt:unstructured"
                jcr:title="Process"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns"/>
            <mycommon
                jcr:primaryType="nt:unstructured"
                jcr:title="Common"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                <items jcr:primaryType="nt:unstructured">
                    <columns
                        jcr:primaryType="nt:unstructured"
                        sling:resourceType="granite/ui/components/coral/foundation/container">
                        <items jcr:primaryType="nt:unstructured">
                            <title
                                jcr:primaryType="nt:unstructured"
                                sling:resourceType="granite/ui/components/coral/foundation/form/textfield"
                                fieldLabel="Title"
                                name="./jcr:title"/>
                            <description
                                jcr:primaryType="nt:unstructured"
                                sling:resourceType="granite/ui/components/coral/foundation/form/textarea"
                                fieldLabel="Description"
                                name="./jcr:description"/>
                        </items>
                    </columns>
                </items>
            </mycommon>
            <advanced
                jcr:primaryType="nt:unstructured"
                jcr:title="Advanced"
                sling:resourceType="granite/ui/components/coral/foundation/fixedcolumns">
                <items jcr:primaryType="nt:unstructured">
                    <columns
                        jcr:primaryType="nt:unstructured"
                        sling:resourceType="granite/ui/components/coral/foundation/container">
                        <items jcr:primaryType="nt:unstructured">
                            <email
                                jcr:primaryType="nt:unstructured"
                                sling:resourceType="granite/ui/components/coral/foundation/form/checkbox"
                                fieldDescription="Notify user via email."
                                fieldLabel="Email"
                                name="./metaData/PROCESS_AUTO_ADVANCE"
                                text="Notify user via email."
                                value="true"/>
                        </items>
                    </columns>
                </items>
            </advanced>
        </items>
    </content>
</jcr:root>
```

>[!NOTE]
>
>注意對話框定義中的公共節點和進程節點。 這些繼承自我們用來作為自訂步驟超類型的處理步驟：
>
>`sling:resourceSuperType : cq/workflow/components/model/process`

>[!NOTE]
>
>傳統UI模型編輯器對話方塊仍可與標準觸控式UI編輯器搭配使用。
>
>雖然AEM有 [現代化工具](/help/sites-developing/modernization-tools.md) 如果您想要將傳統UI步驟對話方塊升級為標準UI對話方塊。 轉換後，某些情況下仍可手動改善對話方塊。
>
>* 若升級的對話方塊為空白，您可以在 `/libs` 功能類似於如何提供解決方案的範例。 例如：
>
>* `/libs/cq/workflow/components/model`
>* `/libs/cq/workflow/components/workflow`
>* `/libs/dam/components`
>* `/libs/wcm/workflow/components/autoassign`
>* `/libs/cq/projects`
>
>  您不得修改 `/libs`，只需以為範例即可。 如果您想要運用任何現有步驟，請將它們複製到 `/apps` 並在那裡修改它們。
