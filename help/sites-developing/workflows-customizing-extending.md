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

本主題介紹如何為工作流開發自定義步驟元件，以及如何以寫程式方式與工作流交互。

建立自定義工作流步驟涉及以下活動：

* 開發工作流步驟元件。
* 將步驟功能作為OSGi服務或ECMA指令碼實現。

您也可以 [通過您的程式和指令碼與您的工作流進行交互](/help/sites-developing/workflows-program-interaction.md)。

## 工作流步驟元件 — 基礎 {#workflow-step-components-the-basics}

工作流步驟元件定義建立工作流模型時步驟的外觀和行為：

* 工作流旁接中的類別和步驟名稱。
* 工作流模型中步驟的外觀。
* 用於配置元件屬性的編輯對話框。
* 在運行時執行的服務或指令碼。

與 [所有元件](/help/sites-developing/components.md)，工作流步驟元件從為 `sling:resourceSuperType` 屬性。 下圖顯示了 `cq:component` 構成所有工作流步驟元件基礎的節點。 該圖還包括 **處理步驟**。 **參與者步驟**, **動態參與者步驟** 元件，因為這些是開發自定義步驟元件的最常見（和基本）起點。

![aem_wf_componentinherit](assets/aem_wf_componentinherit.png)

>[!CAUTION]
>
>你 ***必須*** 沒有改變 `/libs` 路徑。
>
>這是因為 `/libs` 在下次升級實例時被覆蓋（在應用修補程式或功能包時很可能被覆蓋）。
>
>建議的配置和其他更改方法是：
>
>1. 重新建立所需項(如 `/libs` 在 `/apps`
>2. 在 `/apps`


的 `/libs/cq/workflow/components/model/step` 元件是 **處理步驟**。 **參與者步驟**, **動態參與者步驟**，所有項都繼承以下項：

* `step.jsp`

   的 `step.jsp` 指令碼在步驟元件添加到模型時呈現其標題。

   ![wf-22-1](assets/wf-22-1.png)

* [cq：對話框](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog)

   包含以下頁籤的對話框：

   * **常用**:的子菜單。
   * **高級**:編輯電子郵件通知屬性。

   ![wf-44](assets/wf-44.png) ![wf-45](assets/wf-45.png)

   >[!NOTE]
   >
   >當步驟元件的編輯對話框的頁籤與此預設外觀不匹配時，步驟元件已定義了可覆蓋這些繼承頁籤的指令碼、節點屬性或對話框頁籤。

### ECMA指令碼 {#ecma-scripts}

ECMA指令碼中提供了以下對象（取決於步驟類型）:

* [工作項](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkItem.html) 工作項
* [工作流會話](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/WorkflowSession.html) 工作流會話
* [工作流資料](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkflowData.html) 工作流資料
* `args`:具有進程參數的陣列。

* `sling`:訪問其他osgi服務。
* `jcrSession`

### 元資料映射 {#metadatamaps}

您可以使用工作流元資料來保留工作流生命週期中所需的資訊。 工作流步驟的一個常見要求是保留資料以供將來在工作流中使用，或檢索保留的資料。

MetaDataMap對象有三種類型 —  `Workflow`。 `WorkflowData` 和 `WorkItem` 對象。 它們都有著相同的目標 — 儲存元資料。

WorkItem有其自己的MetaDataMap，只能在該工作項（例如步驟）運行時使用。

兩者 `Workflow` 和 `WorkflowData` 元資料集在整個工作流中共用。 對於這些情況，建議僅使用 `WorkflowData` 元資料映射。

## 建立自定義工作流步驟元件 {#creating-custom-workflow-step-components}

工作流步驟元件可以 [建立方式與任何其他元件相同](/help/sites-developing/components.md)。

要從（現有）基本步驟元件之一繼承，請將以下屬性添加到 `cq:Component` 節點：

* 名稱: `sling:resourceSuperType`
* 類型: `String`
* 值：解析為基本元件的以下路徑之一：

   * `cq/workflow/components/model/process`
   * `cq/workflow/components/model/participant`
   * `cq/workflow/components/model/dynamic_participant`

### 指定步驟實例的預設標題和說明 {#specifying-the-default-title-and-description-for-step-instances}

使用以下過程指定 **標題** 和 **說明** 的 **常用** 頁籤。

>[!NOTE]
>
>滿足以下兩個要求時，欄位值將出現在步驟實例中：
>
>* 步驟的編輯對話框將標題和說明儲存在以下位置：>
>* `./jcr:title`
>* `./jcr:description` 位置
>
>  當編輯對話框使用 `/libs/cq/flow/components/step/step` 元件實現。
>
>* 步驟元件或元件的祖先不會覆蓋 `step.jsp` 指令碼 `/libs/cq/flow/components/step/step` 元件實現。


1. 在 `cq:Component` 節點，添加以下節點：

   * 名稱: `cq:editConfig`
   * 類型: `cq:EditConfig`

   >[!NOTE]
   >
   >有關cq:editConfig節點的詳細資訊，請參見 [配置元件的編輯行為](/help/sites-developing/developing-components.md#configuring-the-edit-behavior)。

1. 在 `cq:EditConfig` 節點，添加以下節點：

   * 名稱: `cq:formParameters`
   * 類型: `nt:unstructured`

1. 添加 `String` 以下名稱的屬性 `cq:formParameters` 節點：

   * `jcr:title`:值填充 **標題** 的 **常用** 頁籤。
   * `jcr:description`:值填充 **說明** 的 **常用** 頁籤。

### 在工作流元資料中保存屬性值 {#saving-property-values-in-workflow-metadata}

>[!NOTE]
>
>請參閱 [保留和訪問資料](#persisting-and-accessing-data)。 特別是，有關在運行時訪問屬性值的資訊，請參見 [在運行時訪問對話框屬性值](#accessing-dialog-property-values-at-runtime)。

名稱屬性 `cq:Widget` 項指定儲存小部件值的JCR節點。 當工作流步驟元件對話框中的小部件將值儲存在 `./metaData` 的子目錄。 `MetaDataMap`。

例如，對話框中的文本欄位是 `cq:Widget` 具有以下屬性的節點：

| 名稱 | 類型 | 值 |
|---|---|---|
| `xtype` | `String` | `textarea` |
| `name` | `String` | `./metaData/subject` |
| `fieldLabel` | `String` | `Email Subject` |

在此文本欄位中指定的值將添加到工作流實例的 ` [MetaDataMap](#metadatamaps)` 對象，並與 `subject` 按鈕

>[!NOTE]
>
>當鍵為 `PROCESS_ARGS`，在ECMA指令碼實現中，通過 `args` 變數。 在這種情況下， name屬性的值為 `./metaData/PROCESS_ARGS.`

### 覆蓋步驟實施 {#overriding-the-step-implementation}

每個基本步驟元件都使工作流模型開發人員能夠在設計時配置以下關鍵功能：

* 流程步驟：要在運行時執行的服務或ECMA指令碼。
* 參與者步驟：為生成的工作項分配的用戶的ID。
* 動態參與者步驟：選擇分配了工作項的用戶的ID的服務或ECMA指令碼。

要將元件集中到特定工作流方案中使用，請配置設計中的關鍵功能，並刪除模型開發人員更改該功能的能力。

1. 在cq:component節點下，添加以下節點：

   * 名稱: `cq:editConfig`
   * 類型: `cq:EditConfig`

   有關cq:editConfig節點的詳細資訊，請參見 [配置元件的編輯行為](/help/sites-developing/developing-components.md#configuring-the-edit-behavior)。

1. 在cq:EditConfig節點下，添加以下節點：

   * 名稱: `cq:formParameters`
   * 類型: `nt:unstructured`

1. 添加 `String` 屬性 `cq:formParameters` 的下界。 元件超類型確定屬性的名稱：

   * 程序步驟: `PROCESS`
   * 參與者步驟: `PARTICIPANT`
   * 動態參與者步驟: `DYNAMIC_PARTICIPANT`

1. 指定屬性的值：

   * `PROCESS`:ECMA指令碼的路徑或實現步驟行為的服務的PID。
   * `PARTICIPANT`:為工作項分配的用戶的ID。
   * `DYNAMIC_PARTICIPANT`:ECMA指令碼的路徑或選擇用戶分配工作項的服務的PID。

1. 要刪除模型開發人員更改屬性值的能力，請覆蓋元件超類型的對話框。

### 將Forms和對話框添加到參與者步驟 {#adding-forms-and-dialogs-to-participant-steps}

自定義參與者步驟元件以提供在 [表單參與者步驟](/help/sites-developing/workflows-step-ref.md#form-participant-step) 和 [對話框參與者步驟](/help/sites-developing/workflows-step-ref.md#dialog-participant-step) 元件：

* 在用戶開啟生成的工作項時，向他們呈現表單。
* 在用戶完成生成的工作項目時，向用戶顯示自定義對話框。

在新元件上執行以下過程(請參見 [建立自定義工作流步驟元件](#creating-custom-workflow-step-components)):

1. 在 `cq:Component` 節點，添加以下節點：

   * 名稱: `cq:editConfig`
   * 類型: `cq:EditConfig`

   有關cq:editConfig節點的詳細資訊，請參見 [配置元件的編輯行為](/help/sites-developing/components-basics.md#edit-behavior)。

1. 在cq:EditConfig節點下，添加以下節點：

   * 名稱: `cq:formParameters`
   * 類型: `nt:unstructured`

1. 要在用戶開啟工作項時顯示表單，請將以下屬性添加到 `cq:formParameters` 節點：

   * 名稱: `FORM_PATH`
   * 類型: `String`
   * 值：解析為窗體的路徑

1. 要在用戶完成工作項時顯示自定義對話框，請將以下屬性添加到 `cq:formParameters` 節點

   * 名稱: `DIALOG_PATH`
   * 類型: `String`
   * 值：解析到對話框的路徑

### 配置工作流步驟運行時行為 {#configuring-the-workflow-step-runtime-behavior}

在 `cq:Component` 節點，添加 `cq:EditConfig` 的下界。 下面 `nt:unstructured` 節點(必須命名 `cq:formParameters`)並添加到該節點中，添加以下屬性：

* 名稱: `PROCESS_AUTO_ADVANCE`

   * 類型: `Boolean`
   * 值:

      * 設定為 `true` 工作流將運行該步驟並繼續 — 這是預設值，也建議
      * 何時 `false`工作流將運行並停止；這需要額外處理，所以 `true` 推薦

* 名稱: `DO_NOTIFY`

   * 類型: `Boolean`
   * 值：指示是否應為用戶參與步驟發送電子郵件通知（並假定郵件伺服器已正確配置）

## 保留和訪問資料 {#persisting-and-accessing-data}

### 為後續工作流步驟保留資料 {#persisting-data-for-subsequent-workflow-steps}

您可以使用工作流元資料保留工作流生命期期間和步驟之間所需的資訊。 工作流步驟的一個常見要求是保留資料以供將來使用，或從先前步驟中檢索保留的資料。

工作流元資料儲存在 [`MetaDataMap`](#metadatamaps) 的雙曲餘切值。 Java API提供 [`Workflow.getWorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html) 方法返回 [`WorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html) 提供相應 `MetaDataMap` 的雙曲餘切值。 此 `WorkflowData` `MetaDataMap` 對象可用於步驟元件的OSGi服務或ECMA指令碼。

#### Java {#java}

的執行方法 `WorkflowProcess` 實施通過 `WorkItem` 的雙曲餘切值。 使用此對象獲取 `WorkflowData` 當前工作流實例的對象。 下面的示例將項添加到工作流 `MetaDataMap` 對象，然後記錄每個項。 (「mykey」、「My Step Value」)項可用於工作流中的後續步驟。

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

的 `graniteWorkItem` 變數是當前ECMA指令碼的表示 `WorkItem` Java對象。 因此，您可以 `graniteWorkItem` 變數以獲取工作流元資料。 以下ECMA指令碼可用於實現 **處理步驟** 將項添加到工作流 `MetaDataMap` 對象，然後記錄每個項。 然後，這些項目可用於工作流中的後續步驟。

>[!NOTE]
>
>的 `metaData` 步驟指令碼立即可用的變數是步驟的元資料。 步驟元資料與工作流元資料不同。

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

的 `MetaDataMap` 工作流實例的對象對於在整個工作流生命週期中儲存和檢索資料非常有用。 對於工作流步驟元件實施， `MetaDataMap` 對於在運行時檢索元件屬性值特別有用。

>[!NOTE]
>
>有關配置元件對話框以將屬性儲存為工作流元資料的資訊，請參見 [在工作流元資料中保存屬性值](#saving-property-values-in-workflow-metadata)。

工作流 `MetaDataMap` 可用於Java和ECMA指令碼進程實現：

* 在Java實現的WorkflowProcess介面中， `args` 參數 `MetaDataMap` 對象。

* 在ECMA指令碼實現中，值可使用 `args` 和 `metadata` 變數。

### 示例：檢索進程步驟元件的參數 {#example-retrieving-the-arguments-of-the-process-step-component}

的編輯對話框 **處理步驟** 元件包括 **參數** 屬性。 的值 **參數** 屬性儲存在工作流元資料中，並與 `PROCESS_ARGS` 按鈕

在下圖中， **參數** 屬性 `argument1, argument2`:

![wf-24](assets/wf-24.png)

#### 爪哇 {#java-1}

以下Java代碼是 `execute` 方法 `WorkflowProcess` 執行。 方法將值記錄在 `args` `MetaDataMap` 與 `PROCESS_ARGS` 按鈕

```java
public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {
     if (args.containsKey("PROCESS_ARGS")){
      log.info("workflow metadata for key PROCESS_ARGS and value {}",args.get("PROCESS_ARGS","string").toString());
     }
    }
```

當使用此Java實現的進程步驟執行時，日誌包含以下條目：

```xml
16.02.2018 12:07:39.566 *INFO* [JobHandler: /var/workflow/instances/server0/2018-02-16/model_855140139900189:/content/we-retail/de] com.adobe.example.workflow.impl.process.LogArguments workflow metadata for key PROCESS_ARGS and value argument1, argument2
```

#### ECMA 指令碼 {#ecma-script-1}

以下ECMA指令碼用作 **處理步驟**。 它記錄參數數和參數值：

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
>本節介紹如何使用進程步驟的參數。 該資訊也適用於動態參與者選擇器。

>[!NOTE]
>有關在工作流元資料中儲存元件屬性的另一個示例，請參閱示例：建立記錄程式工作流步驟。 此示例的對話框將元資料值與PROCESS_ARGS以外的鍵相關聯。

### 指令碼和進程參數 {#scripts-and-process-arguments}

在指令碼中 **處理步驟** 元件，參數通過 `args` 的雙曲餘切值。

建立自定義步驟元件時，對象 `metaData` 在指令碼中。 此對象僅限於單個字串參數。

## 開發流程步驟實施 {#developing-process-step-implementations}

當在工作流進程期間啟動進程步驟時，這些步驟將請求發送到OSGi服務或執行ECMA指令碼。 開發執行工作流所需操作的服務或ECMA指令碼。

>[!NOTE]
>
>有關將流程步驟元件與服務或指令碼關聯的資訊，請參閱 [處理步驟](/help/sites-developing/workflows-step-ref.md#process-step) 或 [覆蓋步驟實施](#overriding-the-step-implementation)。

### 使用Java類實現進程步驟 {#implementing-a-process-step-with-a-java-class}

要將進程步驟定義為OSGI服務元件（Java捆綁包），請執行以下操作：

1. 建立捆綁包並將其部署到OSGI容器。 請參閱有關使用 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) 或 [日蝕](/help/sites-developing/howto-projects-eclipse.md)。

   >[!NOTE]
   >
   >OSGI元件需要 `WorkflowProcess` 介面 `execute()` 的雙曲餘切值。 請參閱下面的示例代碼。

   >[!NOTE]
   >
   >需要將包名稱添加到 `<*Private-Package*>` 的下界 `maven-bundle-plugin` 配置。

1. 添加SCR屬性 `process.label`  根據需要設定值。 這將是使用泛型時列出的流程步驟的名稱 **處理步驟** 元件。 請參見下面的示例。
1. 在 **模型** 編輯器，使用通用 **處理步驟** 元件。
1. 在編輯對話框中( **處理步驟**)，轉到 **進程** 頁籤，然後選擇流程實施。
1. 如果在代碼中使用參數，請設定 **進程參數**。 例如：錯誤。
1. 保存步驟和工作流模型（模型編輯器左上角）的更改。

Java方法、分別實現可執行Java方法的類註冊為OSGI服務，使您能夠在運行時隨時添加方法。

以下OSGI元件將添加屬性 `approved` 當負載為頁面時，指向頁面內容節點：

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
>如果流程在一行中失敗三次，則項目將放在工作流管理員的收件箱中。

### 使用ECMAScript {#using-ecmascript}

ECMA指令碼使指令碼開發人員能夠實施過程步驟。 指令碼位於JCR儲存庫中，並從中執行。

下表列出了可立即用於處理指令碼的變數，提供了對工作流Java API對象的訪問。

| Java類 | 指令碼變數名稱 | 說明 |
|---|---|---|
| `com.adobe.granite.workflow.exec.WorkItem` | `graniteWorkItem` | 當前步驟實例。 |
| `com.adobe.granite.workflow.WorkflowSession` | `graniteWorkflowSession` | 當前步驟實例的工作流會話。 |
| `String[]` （包含進程參數） | `args` | 步驟參數。 |
| `com.adobe.granite.workflow.metadata.MetaDataMap` | `metaData` | 當前步驟實例的元資料。 |
| `org.apache.sling.scripting.core.impl.InternalScriptHelper` | `sling` | 提供對Sling運行時環境的訪問。 |

以下示例指令碼演示如何訪問表示工作流負載的JCR節點。 的 `graniteWorkflowSession` 變數適用於JCR會話變數，該會話變數用於從有效載荷路徑獲得節點。

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

以下指令碼檢查負載是否為映像( `.png` 檔案)，從中建立黑白影像，並將其另存為同級節點。

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

1. 建立指令碼(例如，使用CRXDE Lite)並將其保存到下面的儲存庫中 `//apps/workflow/scripts/`
1. 指定標識中指令碼的標題 **處理步驟** 編輯對話框，將以下屬性添加到 `jcr:content` 指令碼的節點：

   | 名稱 | 類型 | 值 |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | 要在編輯對話框中顯示的名稱。 |

1. 編輯 **處理步驟** 實例並指定要使用的指令碼。

## 開發參與者選擇器 {#developing-participant-choosers}

可以開發參與者選擇器 **動態參與者步驟** 元件。

當 **動態參與者步驟** 元件在工作流中啟動，該步驟需要確定可將生成的工作項分配給的參與者。 要執行此步驟，請執行以下操作：

* 向OSGi服務發送請求
* 執行ECMA指令碼以選擇參與者

您可以開發服務或ECMA指令碼，該指令碼根據工作流的要求選擇參與者。

>[!NOTE]
>
>有關關聯的資訊 **動態參與者步驟** 包含服務或指令碼的元件，請參見 [動態參與者步驟](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step) 或 [覆蓋步驟實施](#persisting-and-accessing-data)。

### 使用Java類開發參與者選擇器 {#developing-a-participant-chooser-using-a-java-class}

要將參與者步驟定義為OSGI服務元件（Java類），請執行以下操作：

1. OSGI元件需要 `ParticipantStepChooser` 介面 `getParticipant()` 的雙曲餘切值。 請參閱下面的示例代碼。

   建立捆綁包並將其部署到OSGI容器。

1. 添加SCR屬性 `chooser.label` 並根據需要設定值。 這將是您的參與者選擇者所列出的名稱，使用 **動態參與者步驟** 元件。 請參閱示例：

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

1. 在 **模型** 編輯器，使用通用工具將動態參與者步驟添加到工作流 **動態參與者步驟** 元件。
1. 在編輯對話框中，選擇 **參與者選擇器** 頁籤，然後選擇選擇器實現。
1. 如果在代碼集中使用參數 **進程參數**。 對於此示例： `/content/we-retail/de`。
1. 保存步驟和工作流模型的更改。

### 使用ECMA指令碼開發參與者選擇器 {#developing-a-participant-chooser-using-an-ecma-script}

您可以建立ECMA指令碼，該指令碼將選擇為 **參與者步驟** 生成。 指令碼必須包含名為 `getParticipant` 不需要參數，並返回 `String` 包含用戶或組的ID。

指令碼位於JCR儲存庫中，並從中執行。

下表列出了可立即訪問指令碼中的工作流Java對象的變數。

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

1. 建立指令碼(例如，使用CRXDE Lite)並將其保存到下面的儲存庫中 `//apps/workflow/scripts`
1. 指定標識中指令碼的標題 **處理步驟** 編輯對話框，將以下屬性添加到 `jcr:content` 指令碼的節點：

   | 名稱 | 類型 | 值 |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | 要在編輯對話框中顯示的名稱。 |

1. 編輯 [動態參與者步驟](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step) 實例並指定要使用的指令碼。

## 處理工作流包 {#handling-workflow-packages}

[工作流包](/help/sites-authoring/workflows-applying.md#specifying-workflow-details-in-the-create-workflow-wizard) 可以傳遞到工作流進行處理。 工作流包包含對資源（如頁面和資產）的引用。

>[!NOTE]
>
>以下工作流進程步驟接受用於批量頁面激活的工作流包：
>
>* [`com.day.cq.wcm.workflow.process.ActivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/ActivatePageProcess.html)
>* [`com.day.cq.wcm.workflow.process.DeactivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/DeactivatePageProcess.html)
>


您可以開發獲取包資源並處理這些資源的工作流步驟。 以下成員 `com.day.cq.workflow.collection` 包提供對工作流包的訪問：

* `ResourceCollection`:工作流包類。
* `ResourceCollectionUtil`:用於檢索ResourceCollection對象。
* `ResourceCollectionManager`:建立和檢索集合。 將實現部署為OSGi服務。

以下示例Java類演示了如何獲取包資源：

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

## 示例：建立自定義步驟 {#example-creating-a-custom-step}

開始建立您自己的自定義步驟的簡單方法是從以下位置複製現有步驟：

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

1. 然後將複製的步驟放在/apps資料夾中；例如：

   `/apps/cq/workflow/components/model/myCustomStep`

   下面是示例自定義步驟的結果：

   ![wf-34](assets/wf-34.png)

   >[!CAUTION]
   >
   >因為在標準UI中，卡上不顯示只顯示標題而不顯示詳細資訊， `details.jsp` 不需要它，因為它是標準UI編輯器。

1. 將以下屬性應用於節點：

   `/apps/cq/workflow/components/model/myCustomStep`

   **權益物業：**

   * `sling:resourceSuperType`

      必須從現有步驟繼承。

      在本示例中，我們將從位於 `cq/workflow/components/model/step`，但可以使用其他超類型，如 `participant`。 `process`的子菜單。

   * `jcr:title`

      是在步驟瀏覽器（工作流模型編輯器的左側面板）中列出元件時顯示的標題。

   * `cq:icon`

      用於指定 [珊瑚表徵圖](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) 的上界。

   * `componentGroup`

      必須是以下之一：

      * Collaboration 工作流程
      * DAM 工作流程
      * 表單工作流程
      * 專案
      * WCM 工作流程
      * 工作流程

   ![wf-35](assets/wf-35.png)

1. 現在可以開啟工作流模型進行編輯。 在步驟瀏覽器中，您可以過濾以查看 **我的自定義步驟**:

   ![wf-36](assets/wf-36.png)

   拖動 **我的自定義步驟** 在模型上顯示卡：

   ![wf-37](assets/wf-37.png)

   否 `cq:icon` 定義步驟，然後使用標題的前兩個字母呈現預設表徵圖。 例如：

   ![wf-38](assets/wf-38.png)

#### 定義步驟配置對話框 {#defining-the-step-configure-dialog}

之後 [建立基本步驟](#creating-the-basic-step)，定義步驟 **配置** 對話框：

1. 配置節點上的屬性 `cq:editConfig` 如下：

   **權益物業：**

   * `cq:inherit`

      設定為時 `true`，則步驟元件將繼承您在中指定的步驟中的屬性 `sling:resourceSuperType`。

   * `cq:disableTargeting`

      根據需要設定。
   ![wf-39](assets/wf-39.png)

1. 配置節點上的屬性 `cq:formsParameter` 如下：

   **權益物業：**

   * `jcr:title`

      在模型圖和 **標題** 的 **我的自定義 — 步驟屬性** 「配置」對話框。

   * 您也可以定義自己的自定義屬性。

   ![wf-40](assets/wf-40.png)

1. 配置節點上的屬性 `cq:listeners`。

   的 `cq:listener` 節點及其屬性允許您設定對啟用觸摸的UI模型編輯器中的事件做出響應的事件處理程式；例如，將步驟拖到模型頁面或編輯步驟屬性。

   **權益物業：**

   * `afterMove: REFRESH_PAGE`
   * `afterdelete: CQ.workflow.flow.Step.afterDelete`
   * `afteredit: CQ.workflow.flow.Step.afterEdit`
   * `afterinsert: CQ.workflow.flow.Step.afterInsert`

   此配置對於編輯器的正常工作至關重要。 大多數情況下，不能更改此配置。

   但是，設定 `cq:inherit` 為true(在 `cq:editConfig` 節點，請參閱上面)允許您繼承此配置，而無需在步驟定義中明確包含它。 如果沒有繼承，則需要添加具有以下屬性和值的此節點。

   在本示例中，已激活繼承，因此我們可以刪除 `cq:listeners` 節點和步驟仍能正常工作。

   ![wf-41](assets/wf-41.png)

1. 現在，您可以將步驟的實例添加到工作流模型。 當你 **配置** 您將看到的步驟：

   ![wf-42](assets/wf-42.png) ![wf-43](assets/wf-43.png)

#### 此示例中使用的示例標籤 {#sample-markup-used-in-this-example}

自定義步驟的標籤在 `.content.xml` 的子菜單。 示例 `.content.xml` 用於此示例：

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

的 `_cq_editConfig.xml` 此示例中使用的示例：

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

的 `_cq_dialog/.content.xml` 此示例中使用的示例：

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
>注意對話框定義中的公用節點和進程節點。 這些內容繼承自我們用作自定義步驟超類型的流程步驟：
>
>`sling:resourceSuperType : cq/workflow/components/model/process`

>[!NOTE]
>
>傳統UI模型編輯器對話框仍可與標準的、啟用觸摸的UI編輯器配合使用。
>
>但AEM是 [現代化工具](/help/sites-developing/modernization-tools.md) 的子菜單。 在轉換後，仍可對某些情況的對話框進行一些手動改進。
>
>* 如果升級的對話框為空，則可以在 `/libs` 功能與如何提供解決方案的示例類似。 例如：
>
>* `/libs/cq/workflow/components/model`
>* `/libs/cq/workflow/components/workflow`
>* `/libs/dam/components`
>* `/libs/wcm/workflow/components/autoassign`
>* `/libs/cq/projects`
>
>  您不得修改 `/libs`，只需以它們為例。 如果要利用任何現有步驟，請將它們複製到 `/apps` 並在那裡修改它們。
