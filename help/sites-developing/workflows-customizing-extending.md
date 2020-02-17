---
title: 擴充工作流程功能
seo-title: 擴充工作流程功能
description: 'null'
seo-description: 'null'
uuid: 9f4ea2a8-8b21-4e7c-ac73-dd37d9ada111
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: f23408c3-6b37-4047-9cce-0cab97bb6c5c
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 擴充工作流程功能{#extending-workflow-functionality}

本主題說明如何為工作流程開發自訂步驟元件，以及如何以程式設計方式與工作流程互動。

建立自訂工作流程步驟涉及下列活動：

* 開發工作流步驟元件。
* 以OSGi服務或ECMA指令碼的形式實施步驟功能。

您也可以從 [程式和指令碼與工作流程互動](/help/sites-developing/workflows-program-interaction.md)。

## 工作流程步驟元件——基本概念 {#workflow-step-components-the-basics}

工作流步驟元件定義建立工作流模型時步驟的外觀和行為：

* 工作流側點中的類別和步驟名稱。
* 工作流模型中步驟的外觀。
* 用於配置元件屬性的編輯對話框。
* 在運行時執行的服務或指令碼。

與所有 [元件一樣](/help/sites-developing/components.md)，工作流步驟元件繼承自為屬性指定的組 `sling:resourceSuperType` 件。 下圖顯示構成所有工作流 `cq:component` 步驟元件基礎的節點的層次結構。 此圖還包括「流程步 **驟**」、「參與者步驟 **」和「動態參與者步驟****** 」元件，因為這些元件是開發自定義步驟元件最常見（也是最基本）的起點。

![aem_wf_componentinherit](assets/aem_wf_componentinherit.png)

>[!CAUTION]
>
>您 ***不得*** 更改路徑中的任 `/libs` 何內容。
>
>這是因為下次升級 `/libs` 實例時會覆寫的內容（套用修補程式或功能套件時可能會覆寫）。
>
>配置和其他更改的建議方法為：
>
>1. 重新建立所需項目(例如，在 `/libs``/apps`
>2. 在 `/apps`


元件 `/libs/cq/workflow/components/model/step` 是「流程步驟」、「參與者步驟」和「動態 **參與者步驟」的最接近的共同祖先**********，它們都繼承了以下項目：

* `step.jsp`

   腳 `step.jsp` 本在將步驟元件添加到模型時呈現其標題。

   ![wf-22-1](assets/wf-22-1.png)

* [cq:dialog](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog)

   具有以下頁籤的對話框：

   * **常見**:編輯標題和說明。
   * **進階**:編輯電子郵件通知屬性。
   ![wf-44](assets/wf-44.png)![wf-45](assets/wf-45.png)

   >[!NOTE]
   >
   >當步驟元件的編輯對話框的頁籤與此預設外觀不匹配時，步驟元件具有定義的指令碼、節點屬性或對話框頁籤，這些頁籤覆蓋這些繼承的頁籤。

### ECMA指令碼 {#ecma-scripts}

ECMA指令碼中提供以下對象（取決於步驟類型）:

* [WorkItem](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkItem.html) workItem
* [WorkflowSession](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/WorkflowSession.html) workflowSession
* [WorkflowData](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/WorkflowData.html) workflowData
* `args`:array with process arguments.

* `sling`:存取其他網站服務。
* `jcrSession`

### MetaDataMaps {#metadatamaps}

您可以使用工作流程中繼資料來保存工作流程期間所需的資訊。 工作流程步驟的常見要求是保存資料以供日後在工作流程中使用，或擷取持續的資料。

MetaDataMap物件有三種類型——適 `Workflow`用於 `WorkflowData` 和物 `WorkItem` 件。 它們都有相同的目的——儲存中繼資料。

WorkItem有其自己的MetaDataMap，只能在該工作項目（如步驟）運行時使用。

在整個 `Workflow` 工作流程 `WorkflowData` 中，都會共用中繼資料地圖和中繼資料地圖。 在這些情況下，建議僅使用中繼資 `WorkflowData` 料地圖。

## 建立自訂工作流程步驟元件 {#creating-custom-workflow-step-components}

工作流步驟元件的創 [建方式與任何其它元件相同](/help/sites-developing/components.md)。

要繼承（現有）基本步驟元件之一，請向節點添加以下屬 `cq:Component` 性：

* 名稱: `sling:resourceSuperType`
* 類型: `String`
* 值：解析為基本元件的下列路徑之一：

   * `cq/workflow/components/model/process`
   * `cq/workflow/components/model/participant`
   * `cq/workflow/components/model/dynamic_participant`

### 指定步驟實例的預設標題和說明 {#specifying-the-default-title-and-description-for-step-instances}

使用以下過程為「常用」( **Common** )頁籤上的「標 **題** 」(Title **)和「說明** 」(Description)欄位指定預設值。

>[!NOTE]
>
>當滿足以下兩個要求時，欄位值將出現在步驟實例中：
>
>* 步驟的編輯對話框將標題和說明儲存在以下位置：>
>* `./jcr:title`
>* `./jcr:description` 位置
>
>  
當編輯對話框使用元件實施的「常用」(Common)頁籤時，滿足此 `/libs/cq/flow/components/step/step` 要求。
>
>* 該元件的步驟元件或祖先不會覆蓋該組 `step.jsp` 件實施的 `/libs/cq/flow/components/step/step` 指令碼。


1. 在節點 `cq:Component` 下方，添加以下節點：

   * 名稱: `cq:editConfig`
   * 類型: `cq:EditConfig`
   >[!NOTE]
   >
   >有關cq:editConfig節點的詳細資訊，請參 [閱配置元件的編輯行為](/help/sites-developing/developing-components.md#configuring-the-edit-behavior)。

1. 在節點 `cq:EditConfig` 下方，添加以下節點：

   * 名稱: `cq:formParameters`
   * 類型: `nt:unstructured`

1. 將下 `String` 列名稱的屬性添加到節 `cq:formParameters` 點：

   * `jcr:title`:該值填充了「 **常用** 」( **Common** )頁籤的「標題」(Title)欄位。
   * `jcr:description`:該值填充了「 **常用** 」( **Common** )頁籤的「說明」(Description)欄位。

### 在工作流元資料中保存屬性值 {#saving-property-values-in-workflow-metadata}

>[!NOTE]
>
>請參 [閱持續和存取資料](#persisting-and-accessing-data)。 尤其是，有關在運行時訪問屬性值的資訊，請參 [閱在運行時訪問對話框屬性值](#accessing-dialog-property-values-at-runtime)。

項目的name屬 `cq:Widget` 性指定儲存Widget值的JCR節點。 當工作流程步驟元件對話方塊中的Widget將值儲存在節 `./metaData` 點下方時，就會將值新增至工作流程 `MetaDataMap`。

例如，對話方塊中的文字欄位是具 `cq:Widget` 有下列屬性的節點：

| 名稱 | 類型 | 值 |
|---|---|---|
| `xtype` | `String` | `textarea` |
| `name` | `String` | `./metaData/subject` |
| `fieldLabel` | `String` | `Email Subject` |

在此文本欄位中指定的值將添加到工作流實例的對 ` [MetaDataMap](#metadatamaps)` 像中，並與鍵相 `subject` 關聯。

>[!NOTE]
>
>當密鑰為時， `PROCESS_ARGS`該值即可通過變數在ECMA指令碼實現中 `args` 使用。 在此情況下，name屬性的值為 `./metaData/PROCESS_ARGS.`

### 覆寫步驟實作 {#overriding-the-step-implementation}

每個基本步驟元件都可讓工作流程模型開發人員在設計時設定下列主要功能：

* 流程步驟：要在運行時執行的服務或ECMA指令碼。
* 參與者步驟：指派給所產生工作項目之使用者的ID。
* 動態參與者步驟：選擇指派工作項目之使用者ID的服務或ECMA指令碼。

若要將元件集中用於特定的工作流程藍本中，請在設計中設定關鍵功能，並移除模型開發人員變更它的功能。

1. 在cq:component節點下方，新增下列節點：

   * 名稱: `cq:editConfig`
   * 類型: `cq:EditConfig`
   有關cq:editConfig節點的詳細資訊，請參 [閱配置元件的編輯行為](/help/sites-developing/developing-components.md#configuring-the-edit-behavior)。

1. 在cq:EditConfig節點下方，新增下列節點：

   * 名稱: `cq:formParameters`
   * 類型: `nt:unstructured`

1. 將屬性 `String` 添加到節 `cq:formParameters` 點。 元件super類型決定屬性的名稱：

   * 程序步驟: `PROCESS`
   * 參與者步驟: `PARTICIPANT`
   * 動態參與者步驟: `DYNAMIC_PARTICIPANT`

1. 指定屬性的值：

   * `PROCESS`:實施步驟行為的ECMA指令碼或服務的PID路徑。
   * `PARTICIPANT`:指派給工作項目之使用者的ID。
   * `DYNAMIC_PARTICIPANT`:指向ECMA指令碼或選擇用戶指派工作項的服務的PID的路徑。

1. 若要移除模型開發人員變更屬性值的能力，請覆寫元件super類型的對話方塊。

### 向參與者步驟添加表單和對話框 {#adding-forms-and-dialogs-to-participant-steps}

自定義參與者步驟元件，以提供「表單參與者步驟」和「對 [話參與者步驟](/help/sites-developing/workflows-step-ref.md#form-participant-step) 」組 [件中的功能](/help/sites-developing/workflows-step-ref.md#dialog-participant-step) :

* 在使用者開啟產生的工作項目時，向使用者呈現表格。
* 當使用者完成產生的工作項目時，向使用者呈現自訂對話方塊。

在新元件上執行下列程式(請參 [閱建立自訂工作流程步驟元件](#creating-custom-workflow-step-components)):

1. 在節點 `cq:Component` 下方，添加以下節點：

   * 名稱: `cq:editConfig`
   * 類型: `cq:EditConfig`
   有關cq:editConfig節點的詳細資訊，請參 [閱配置元件的編輯行為](/help/sites-developing/components-basics.md#edit-behavior)。

1. 在cq:EditConfig節點下方，新增下列節點：

   * 名稱: `cq:formParameters`
   * 類型: `nt:unstructured`

1. 要在用戶開啟工作項時顯示表單，請向節點添加以下屬 `cq:formParameters` 性：

   * 名稱: `FORM_PATH`
   * 類型: `String`
   * 值：解析為表單的路徑

1. 要在用戶完成工作項目時顯示自定義對話框，請將以下屬性添加到節 `cq:formParameters` 點

   * 名稱: `DIALOG_PATH`
   * 類型: `String`
   * 值：解析到對話框的路徑

### 設定工作流程步驟執行時期行為 {#configuring-the-workflow-step-runtime-behavior}

在節點 `cq:Component` 下面添加節 `cq:EditConfig` 點。 在添加節 `nt:unstructured` 點(必須命名 `cq:formParameters`)的下面，向該節點添加以下屬性：

* 名稱: `PROCESS_AUTO_ADVANCE`

   * 類型: `Boolean`
   * 值:

      * 當設為工作 `true` 流程時，將執行該步驟並繼續——這是預設值，也建議
      * 工作 `false`流程將運行並停止；這需要額外的處理，所以 `true` 建議

* 名稱: `DO_NOTIFY`

   * 類型: `Boolean`
   * 值：指出是否應針對使用者參與步驟傳送電子郵件通知（並假設郵件伺服器已正確設定）

## 保存和訪問資料 {#persisting-and-accessing-data}

### 後續工作流程步驟的持續資料 {#persisting-data-for-subsequent-workflow-steps}

您可以使用工作流程中繼資料來保存工作流程生命週期期間及各步驟之間所需的資訊。 工作流程步驟的常見要求是保存資料以供日後使用，或從先前步驟擷取持續的資料。

工作流元資料儲存在對 [`MetaDataMap`](#metadatamaps) 像中。 Java API提供傳 [`Workflow.getWorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/Workflow.html) 回提供適當物件 [`WorkflowData`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/exec/WorkflowData.html) 的物件的方 `MetaDataMap` 法。 此 `WorkflowData` 對象 `MetaDataMap` 可用於步驟元件的OSGi服務或ECMA指令碼。

#### Java {#java}

實現的執行方 `WorkflowProcess` 法會傳遞物件 `WorkItem` 。 使用此對象可獲取當 `WorkflowData` 前工作流實例的對象。 下面的示例將項目添加到工作流對 `MetaDataMap` 像中，然後記錄每個項目。 (&quot;mykey&quot;, &quot;My Step Value&quot;)項目可用於工作流中的後續步驟。

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

此變 `graniteWorkItem` 數是目前Java物件的ECMA指令碼 `WorkItem` 表示法。 因此，您可以使用變 `graniteWorkItem` 數來取得工作流程中繼資料。 以下ECMA指令碼可用於實施「 **Process Step** 」(流程步驟 `MetaDataMap` )，以向工作流對象添加項，然後記錄每個項。 這些項目隨後可用於工作流中的後續步驟。

>[!NOTE]
>
>步驟 `metaData` 指令碼可立即使用的變數是步驟的中繼資料。 步驟中繼資料與工作流程中繼資料不同。

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

工作 `MetaDataMap` 流實例的對象對於在整個工作流生命週期中儲存和檢索資料非常有用。 對於工作流步驟元件實施，在 `MetaDataMap` 運行時檢索元件屬性值時特別有用。

>[!NOTE]
>
>有關配置元件對話框以將屬性儲存為工作流元資料的資訊，請參 [閱在工作流元資料中保存屬性值](#saving-property-values-in-workflow-metadata)。

工作流 `MetaDataMap` 可用於Java和ECMA指令碼流程實施：

* 在WorkflowProcess介面的Java實施中，參 `args` 數是工 `MetaDataMap` 作流的對象。

* 在ECMA指令碼實作中，值可使用和變 `args` 數 `metadata` 來。

### 範例：檢索進程步驟元件的參數 {#example-retrieving-the-arguments-of-the-process-step-component}

「流程步驟」元件的 **編輯對話框** ，包含 **Arguments屬性** 。 Arguments屬性的值 **儲存在** worklow元資料中，並與鍵相 `PROCESS_ARGS` 關。

在下圖中， **Arguments屬性的值** 為 `argument1, argument2`:

![wf-24](assets/wf-24.png)

#### Java {#java-1}

以下Java程式碼是 `execute` 實作的方 `WorkflowProcess` 法。 方法會將值記錄在與 `args` 索引鍵 `MetaDataMap` 相關聯的 `PROCESS_ARGS` 中。

```java
public void execute(WorkItem item, WorkflowSession session, MetaDataMap args) throws WorkflowException {
     if (args.containsKey("PROCESS_ARGS")){
      log.info("workflow metadata for key PROCESS_ARGS and value {}",args.get("PROCESS_ARGS","string").toString());
     }
    }
```

當使用此Java實施的進程步驟執行時，日誌包含以下條目：

```xml
16.02.2018 12:07:39.566 *INFO* [JobHandler: /var/workflow/instances/server0/2018-02-16/model_855140139900189:/content/we-retail/de] com.adobe.example.workflow.impl.process.LogArguments workflow metadata for key PROCESS_ARGS and value argument1, argument2
```

#### ECMA 指令碼 {#ecma-script-1}

以下ECMA指令碼用作流程步驟的 **流程**。 它記錄引數數和引數值：

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
>本節介紹如何使用流程步驟的參數。 此資訊也適用於動態參與者選擇器。

>[!NOTE]
>如需將元件屬性儲存在工作流程中繼資料中的另一個範例，請參閱範例：建立記錄程式工作流程步驟。 此範例包含一個對話方塊，可將中繼資料值與PROCESS_ARGS以外的索引鍵建立關聯。

### 指令碼和進程引數 {#scripts-and-process-arguments}

在「流程步驟」組 **件的指令碼中** ，參數可通過對 `args` 像使用。

建立自訂步驟元件時，該物件 `metaData` 可在指令碼中使用。 此物件僅限於單一字串引數。

## 開發流程步驟實施 {#developing-process-step-implementations}

在工作流進程中啟動進程步驟時，步驟會向OSGi服務發送請求或執行ECMA指令碼。 開發執行工作流程所需動作的服務或ECMA指令碼。

>[!NOTE]
>
>有關將流程步驟元件與服務或指令碼關聯的資訊，請參 [閱流程步](/help/sites-developing/workflows-step-ref.md#process-step)[驟或覆蓋步驟實施](#overriding-the-step-implementation)。

### 使用Java類實現進程步驟 {#implementing-a-process-step-with-a-java-class}

要將流程步驟定義為OSGI服務元件（Java包）:

1. 建立套件並將它部署至OSGI容器。 請參閱有關使用 [CRXDE Lite或](/help/sites-developing/developing-with-crxde-lite.md) Eclipse [建立搭售的](/help/sites-developing/howto-projects-eclipse.md)檔案。

   >[!NOTE]
   >
   >OSGI元件需要用其方法 `WorkflowProcess` 實現接 `execute()` 口。 請參閱下方的范常式式碼。

   >[!NOTE]
   >
   >需要將軟體包名稱添加到配 `<*Private-Package*>` 置的部 `maven-bundle-plugin` 分。

1. 添加SCR屬 `process.label` 性並根據需要設定值。 這將是使用通用「流程步驟」( **Process Step** )元件時列出的流程步驟的名稱。 請參閱以下範例。
1. 在「模 **型** 」編輯器中，使用通用「流程步驟」( **Process Step)元件將流程步驟添加到工作流中** 。
1. 在編輯對話框(「流程步 **驟」**)中，轉至「流程」 **** 頁籤並選擇流程實施。
1. 如果在代碼中使用參數，請設定「 **進程參數」**。 例如：false。
1. 保存步驟和工作流模型（模型編輯器的左上角）的更改。

Java方法（分別是實現可執行Java方法的類）註冊為OSGI服務，使您能夠在運行時隨時添加方法。

當裝載為頁面時，下列OSGI `approved` 元件會將屬性新增至頁面內容節點：

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
>如果流程連續三次失敗，則項目會放在工作流管理員的「收件箱」中。

### 使用ECMAScript {#using-ecmascript}

ECMA指令碼可讓指令碼開發人員建置程式步驟。 這些指令碼位於JCR儲存庫中，並從中執行。

下表列出可立即處理指令碼的變數，提供對工作流程Java API物件的存取。

| Java類 | 指令碼變數名稱 | 說明 |
|---|---|---|
| `com.adobe.granite.workflow.exec.WorkItem` | `graniteWorkItem` | 當前步驟實例。 |
| `com.adobe.granite.workflow.WorkflowSession` | `graniteWorkflowSession` | 當前步驟實例的工作流會話。 |
| `String[]` （包含進程引數） | `args` | 步驟引數。 |
| `com.adobe.granite.workflow.metadata.MetaDataMap` | `metaData` | 當前步驟實例的元資料。 |
| `org.apache.sling.scripting.core.impl.InternalScriptHelper` | `sling` | 提供Sling執行時期環境的存取權。 |

以下示例指令碼演示如何訪問表示工作流裝載的JCR節點。 該 `graniteWorkflowSession` 變數適用於JCR會話變數，其用於從有效載荷路徑獲得節點。

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

以下指令碼會檢查裝載是否為映像(文 `.png` 件)，從中建立黑白映像，並將其另存為同級節點。

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

1. 建立指令碼（例如，使用CRXDE Lite）並將其保存在以下儲存庫中 `/apps/myapp/workflow/scripts`
1. 要在「流程步驟編輯」對話框中指定標 **識指令碼的標題** ，請將以下屬性添加到腳 `jcr:content` 本的節點中：

   | 名稱 | 類型 | 值 |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | 要顯示在編輯對話框中的名稱。 |

1. 編輯「 **流程步驟** 」實例並指定要使用的指令碼。

## 開發參與者選擇器 {#developing-participant-choosers}

您可以開發「動態參與者步驟」( **Dynamic Participant Step** )元件的參與者選擇器。

在工作流 **中啟動「動態參與者步驟** 」元件時，該步驟需要確定可將生成的工作項目分配給的參與者。 要執行此操作，請執行以下步驟：

* 向OSGi服務發送請求
* 執行ECMA指令碼以選擇參與者

您可以開發服務或ECMA指令碼，根據工作流的要求選擇參與者。

>[!NOTE]
>
>有關將動態參與者步 **驟元件與服務或指令碼關聯的資訊，請參** 閱動態參與者步驟 [](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step) 或覆蓋步驟實施 [](#persisting-and-accessing-data)。

### 使用Java類開發參與者選擇器 {#developing-a-participant-chooser-using-a-java-class}

要將參與者步驟定義為OSGI服務元件（Java類），請執行以下操作：

1. OSGI元件需要用其方法 `ParticipantStepChooser` 實現接 `getParticipant()` 口。 請參閱下方的范常式式碼。

   建立套件並將它部署至OSGI容器。

1. 添加SCR屬 `chooser.label` 性並根據需要設定值。 這將是使用「動態參與者步驟」( **Dynamic Participant Step** )元件列出參與者選擇器的名稱。 請參閱範例：

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

1. 在「模 **型** 」編輯器中，使用通用的「動態參與者步驟」( **Dynamic Participant Step)元件將動態參與者步驟添加到工作流中** 。
1. 在編輯對話方塊中，選取「參與 **者選擇器** 」標籤，並選取您的選擇器實作。
1. 如果在代碼中使用參數，請設定「 **進程參數」**。 對於此示例： `/content/we-retail/de`。
1. 保存步驟和工作流模型的更改。

### 使用ECMA指令碼開發參與者選擇器 {#developing-a-participant-chooser-using-an-ecma-script}

您可以建立ECMA指令碼，該指令碼選擇分配了參與者步驟生成的工作項 **的用戶** 。 此指令碼必須包含名 `getParticipant` 為的函式，其中不需要參數，並傳 `String` 回包含使用者或群組ID的函式。

指令碼位於JCR儲存庫中，並從中執行。

下表列出可立即存取指令碼中工作流程Java物件的變數。

| Java類 | 指令碼變數名稱 |
|---|---|
| `com.adobe.granite.workflow.exec.WorkItem` | `graniteWorkItem` |
| `com.adobe.granite.workflow.WorkflowSession` | `graniteWorkflowSession` |
| `String[]` （包含進程引數） | `args` |
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

1. 建立指令碼（例如，使用CRXDE Lite）並將其保存在以下儲存庫中 `/apps/myapp/workflow/scripts`
1. 要在「流程步驟編輯」對話框中指定標 **識指令碼的標題** ，請將以下屬性添加到腳 `jcr:content` 本的節點中：

   | 名稱 | 類型 | 值 |
   |---|---|---|
   | `jcr:mixinTypes` | `Name[]` | `mix:title` |
   | `jcr:title` | `String` | 要顯示在編輯對話框中的名稱。 |

1. 編輯「 [動態參與者步驟](/help/sites-developing/workflows-step-ref.md#dynamic-participant-step) 」實例並指定要使用的指令碼。

## 處理工作流包 {#handling-workflow-packages}

[工作流程套件](/help/sites-authoring/workflows-applying.md#specifying-workflow-details-in-the-create-workflow-wizard) ，可以傳遞至工作流程進行處理。 工作流程套件包含對資源（例如頁面和資產）的參考。

>[!NOTE]
>
>下列工作流程程式步驟接受大量頁面啟動的工作流程套件：
>
>* [`com.day.cq.wcm.workflow.process.ActivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/ActivatePageProcess.html)
>* [`com.day.cq.wcm.workflow.process.DeactivatePageProcess`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/process/DeactivatePageProcess.html)
>



您可以開發工作流步驟，以獲取包資源並對其進行處理。 以下包成員提 `com.day.cq.workflow.collection` 供對工作流包的訪問：

* `ResourceCollection`:工作流包類。
* `ResourceCollectionUtil`:用於檢索ResourceCollection對象。
* `ResourceCollectionManager`:建立和擷取系列。 實作部署為OSGi服務。

以下Java類示例演示了如何獲取包資源：

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

開始建立您自訂步驟的簡單方式，是從下列位置複製現有步驟：

`/libs/cq/workflow/components/model`

### 建立基本步驟 {#creating-the-basic-step}

1. 在/apps下重新建立路徑；例如：

   `/apps/cq/workflow/components/model`

   新資料夾的類型為 `nt:folder`:

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

1. 然後將複製的步驟置於/apps檔案夾中；例如：

   `/apps/cq/workflow/components/model/myCustomStep`

   以下是我們自訂範例步驟的結果：

   ![wf-34](assets/wf-34.png)

   >[!CAUTION]
   >
   >因為在標準UI中，卡片上不會顯示只有標題（而非詳細資訊），所以 `details.jsp` 不需要它，就像傳統UI編輯器一樣。

1. 將以下屬性應用於節點：

   `/apps/cq/workflow/components/model/myCustomStep`

   **相關物業：**

   * `sling:resourceSuperType`

      必須繼承現有步驟。

      在此範例中，我們繼承了基本步驟( `cq/workflow/components/model/step`)，但您可以使用其他超類 `participant`型， `process`如、等。

   * `jcr:title`

      是當元件列在步驟瀏覽器（工作流模型編輯器的左側面板）中時顯示的標題。

   * `cq:icon`

      用於指定步 [驟的Coral](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html) 表徵圖。

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

   將「 **我的自訂步驟** 」拖曳至模型時，會顯示卡片：

   ![wf-37](assets/wf-37.png)

   如果尚 `cq:icon` 未定義步驟，則使用標題的前兩個字母來呈現預設表徵圖。 例如：

   ![wf-38](assets/wf-38.png)

#### 定義步驟配置對話框 {#defining-the-step-configure-dialog}

建立 [基本步驟後](#creating-the-basic-step)，按如下方式定義步驟 **** 配置對話框：

1. 按如下方式配置節點上 `cq:editConfig` 的屬性：

   **相關物業：**

   * `cq:inherit`

      如果設定為 `true`，則您的步驟元件將繼承您在中指定的步驟的屬性 `sling:resourceSuperType`。

   * `cq:disableTargeting`

      視需要設定。
   ![wf-39](assets/wf-39.png)

1. 按如下方式配置節點上 `cq:formsParameter` 的屬性：

   **相關物業：**

   * `jcr:title`

      在模型映射和「我的自定義——步驟屬性」配置對話框的「標 **題** 」( **Title** )欄位中設定步驟卡的預設標題。

   * 您也可以定義自己的自訂屬性。
   ![wf-40](assets/wf-40.png)

1. 在節點上配置屬性 `cq:listeners`。

   節點 `cq:listener` 及其屬性可讓您在觸控式UI模型編輯器中設定回應事件的事件處理常式；例如將步驟拖曳至模型頁面或編輯步驟屬性。

   **地產：**

   * `afterMove: REFRESH_PAGE`
   * `afterdelete: CQ.workflow.flow.Step.afterDelete`
   * `afteredit: CQ.workflow.flow.Step.afterEdit`
   * `afterinsert: CQ.workflow.flow.Step.afterInsert`
   此組態是編輯器正常運作的必備組態。 在大多數情況下，此配置不能更改。

   但是，設 `cq:inherit` 置為true(在節點上，請參 `cq:editConfig` 見上面)可讓您繼承此配置，而無需將其明確納入步驟定義中。 如果沒有繼承，則您需要添加具有以下屬性和值的節點。

   在此示例中，繼承已激活，因此我們可以刪除節 `cq:listeners` 點，並且步驟仍可以正確運行。

   ![wf-41](assets/wf-41.png)

1. 您現在可以新增步驟的例項至工作流程模型。 當您設 **定步驟** 時，您會看到對話方塊：

   ![wf-42](assets/wf-42.png)![wf-43](assets/wf-43.png)

#### 此示例中使用的標籤示例 {#sample-markup-used-in-this-example}

自定義步驟的標籤將表示在元件根 `.content.xml` 節點中。 此示 `.content.xml` 例使用的示例：

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

此 `_cq_editConfig.xml` 示例中使用的示例：

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

此 `_cq_dialog/.content.xml` 示例中使用的示例：

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
>注意對話框定義中的公共節點和進程節點。 這些繼承自我們用作自訂步驟超類型的流程步驟：
>
>`sling:resourceSuperType : cq/workflow/components/model/process`

>[!NOTE]
>
>傳統的UI模型編輯器對話框仍可與標準的觸控式UI編輯器搭配使用。
>
>雖然AEM有對話 [方塊轉換工具](/help/sites-developing/dialog-conversion.md) ，但是如果您想要將傳統的UI步驟對話方塊升級為標準的UI對話方塊。 轉換後，某些情況下仍可對對話方塊進行一些手動改進。
>
>* 如果升級的對話方塊是空的，您可以檢視與如何提供 `/libs` 解決方案範例功能類似的對話方塊。 例如：
   >
   >
* `/libs/cq/workflow/components/model`
>* `/libs/cq/workflow/components/workflow`
>* `/libs/dam/components`
>* `/libs/wcm/workflow/components/autoassign`
>* `/libs/cq/projects`
>
>  
您不得修改中的任 `/libs`何內容，只要將它們當做範例。 如果您想要利用任何現有步驟，請將它們複製到該處 `/apps` 並加以修改。
