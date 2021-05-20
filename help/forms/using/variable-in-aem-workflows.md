---
title: AEM Forms工作流程中的變數
seo-title: AEM Forms工作流程中的變數
description: 建立變數、設定變數的值，然後在AEM Forms工作流程步驟中使用它。
seo-description: 建立變數、設定變數的值，然後在AEM Forms工作流程步驟中使用它。
uuid: 634a75c4-4899-478f-9e5d-a870f5efa583
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: cbf4e35a-7905-44ab-ab68-fb443443f02d
docset: aem65
exl-id: beb2b83e-e8db-40bb-915f-cb6ba3140947
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2113'
ht-degree: 0%

---

# AEM Forms工作流程中的變數{#variables-in-aem-forms-workflows}

工作流程模型中的變數是根據其資料類型儲存值的方式。 然後，您可以在任何工作流程步驟中使用變數的名稱，以擷取儲存在變數中的值。 您也可以使用變數名稱來定義用於進行路由決策的表達式。

在AEM工作流程模型中，您可以：

* [根據](../../forms/using/variable-in-aem-workflows.md#create-a-variable) 您要儲存的資訊類型，建立資料類型的變數。
* [使用「設定變數」工](../../forms/using/variable-in-aem-workflows.md#set-a-variable) 作流程步驟，設定變數的值。
* [在所有AEM Forms](../../forms/using/variable-in-aem-workflows.md#use-a-variable) 工作流步驟中使用變數來檢索儲存的值，在「或」(Split)和「轉至」(Goto)步驟中使用變數來定義工藝路線表達式。

下列影片示範如何在AEM工作流程模型中建立、設定和使用變數：

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_introduction_1_1.mp4)

變數是現有[MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html)介面的擴展。 您可以在ECMAScript中使用[MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html)存取使用變數儲存的中繼資料。

## 建立變數{#create-a-variable}

您可以使用工作流程模型sidekick中可用的「變數」區段來建立變數。 AEM工作流程變數支援下列資料類型：

* **原始資料類型**:長、雙、布林、日期和字串
* **複雜的資料類型**: [檔案](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemfd/docmanager/Document.html)、 [XML](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/Document.html)、 [JSON](https://static.javadoc.io/com.google.code.gson/gson/2.3/com/google/gson/JsonObject.html)和表單資料模型例項。

>[!NOTE]
>
>工作流程僅支援日期類型變數的ISO8601格式。

檔案和表單資料模型資料類型需要[AEM Forms附加套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)。  使用ArrayList資料類型建立變數集合。 您可以為所有基元和複雜資料類型建立ArrayList變數。 例如，建立ArrayList變數，並選取String作為子類型，以使用變數儲存多個字串值。

執行下列步驟以建立變數：

1. 在AEM例項上，導覽至「工具![](/help/forms/using/assets/hammer.png) >工作流程>模型」。
1. 點選&#x200B;**[!UICONTROL 建立]**&#x200B;並指定工作流程模型的標題和選用名稱。 選取模型，然後點選&#x200B;**[!UICONTROL Edit]**。
1. 點選工作流程模型sidekick中可用的變數圖示，然後點選「**[!UICONTROL 新增變數]**」。

   ![新增變數](assets/variables_add_variable_new.png)

1. 在「新增變數」對話方塊中，指定名稱並選取變數的類型。
1. 從&#x200B;**[!UICONTROL Type]**&#x200B;下拉清單中選擇資料類型，並指定以下值：

   * 基元資料類型 — 指定變數的可選預設值。
   * JSON或XML — 指定選用的JSON或XML結構路徑。 系統會在將此架構中可用的屬性映射並儲存到另一個變數時驗證架構路徑。
   * 表單資料模型 — 指定表單資料模型路徑。
   * ArrayList — 指定集合的子類型。

1. 指定變數的可選說明，然後點選![done_icon](assets/done_icon.png)以儲存變更。 變數會顯示在左窗格的可用清單中。

建立變數時，請考量下列實務：

* 建立工作流程所需的變數數量。 但是，為了節約資料庫資源，請使用所需的最小變數數，並盡可能重複使用變數。
* 變數會區分大小寫。 請確定您在工作流程中使用相同的大小寫參考變數。
* 請避免在變數名稱中使用特殊字元

## 設定變數{#set-a-variable}

您可以使用「設定變數」步驟來設定變數的值，並定義值的設定順序。 變數的設定順序為變數對應在設定變數步驟中列出的順序。

變數值的變更只會影響發生變更的程式例項。 例如，當工作流程起始且變數資料變更時，變更只會影響工作流程的該例項。 這些更改不會影響先前啟動或隨後啟動的工作流的其他實例。

根據變數的資料類型，您可以使用下列選項來設定變數的值：

* **常值：** 當您知道要指定的確切值時，可使用選項。

* **運算式：** 根據運算式計算要使用的值時，請使用選項。運算式是在提供的運算式編輯器中建立。

* **JSON點標籤法：** 使用選項從JSON或FDM類型變數擷取值。
* **XPATH:** 使用選項從XML類型變數中擷取值。

* **相對於有效負載：** 如果要儲存至變數的值在相對於有效負載的路徑上可用時，請使用選項。

* **絕對路徑：** 當要儲存至變數的值在絕對路徑上可用時，請使用選項。

您也可以使用JSON DOT標籤法或XPATH標籤法來更新JSON或XML類型變數的特定元素。

### 新增變數{#add-mapping-between-variables}之間的對應

執行下列步驟以新增變數之間的對應：

1. 在工作流程編輯頁面上，點選工作流程模型sidekick中可用的「步驟」圖示。
1. 將&#x200B;**設定變數**&#x200B;步驟拖放至工作流程編輯器，點選該步驟並選取![configure_icon](assets/configure_icon.png)（設定）。
1. 在「設定變數」對話框中，選擇「**[!UICONTROL 映射]** > **[!UICONTROL 添加映射]**」。
1. 在&#x200B;**映射變數**&#x200B;部分中，選擇要儲存資料的變數，選擇映射模式，並指定要儲存在變數中的值。 對應模式會根據變數類型而有所不同。
1. 映射更多變數，以產生有意義的運算式。 點選![done_icon](assets/done_icon.png)以儲存變更。

### 範例1:查詢XML變數以設定字串變數{#example-query-an-xml-variable-to-set-value-for-a-string-variable}的值

選擇XML類型的變數以儲存XML檔案。 查詢XML變數，為XML檔案中可用的屬性設定字串變數的值。 使用&#x200B;**為XML變數**&#x200B;欄位指定XPATH以定義要儲存在字串變數中的屬性。

在此範例中，選取&#x200B;**formdata** XML變數以儲存&#x200B;**cc-app.xml**&#x200B;檔案。 查詢&#x200B;**formdata**&#x200B;變數以設定&#x200B;**emailaddress**&#x200B;字串變數的值，以儲存&#x200B;**cc-app.xml**&#x200B;檔案中可用&#x200B;**emailAddress**&#x200B;屬性的值。

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/set_variable_example1.mp4 "設定變數的值")

### 範例2:使用運算式來根據其他變數儲存值 {#example2}

使用運算式來計算變數的總和，並將結果儲存在變數中。

在此範例中，使用運算式編輯器定義運算式，以計算&#x200B;**assetcost**&#x200B;和&#x200B;**balanceamount**&#x200B;變數的總和，並將結果儲存在&#x200B;**totalvalue**&#x200B;變數中。

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_expression.mp4)

## 使用表達式編輯器{#use-expression-editor}

您也可以使用運算式來計算執行階段上變數的值。 變數提供運算式編輯器來定義運算式。

使用運算式編輯器可：

* 使用其他工作流程變數、數字或數學運算式來設定變數的值。
* 在數學運算式中使用工作流程變數、字串、數字或運算式
* 新增條件以設定變數的值。
* 在條件之間新增運算子。

![運算式編輯器](assets/variables_expression_editor_new.png)

此工具以適用性表單規則編輯器為基礎，並有下列變更。 變數中的規則編輯器：

* 不支援函式。
* 不提供UI來檢視規則摘要
* 沒有代碼編輯器。
* 不支援啟用和禁用對象的值。
* 不支援設定對象的屬性。
* 不支援呼叫Web服務。

如需詳細資訊，請參閱[適用性表單規則編輯器](../../forms/using/rule-editor.md)。

## 使用變數{#use-a-variable}

您可以使用變數來擷取輸入和輸出，或儲存步驟的結果。 工作流程編輯器提供兩種工作流步驟：

* 支援變數的工作流程步驟
* 不支援變數的工作流程步驟

### 支援變數{#workflow-steps-with-support-for-variables}的工作流步驟

「移至」步驟、「或」分割步驟，以及所有AEM Forms工作流程步驟都支援變數。

#### OR拆分步驟{#or-split-step}

「或分割」在工作流中建立分割，之後只有一個分支處於作用中狀態。 此步驟可讓您將條件式處理路徑引入工作流程中。 您可以視需要將工作流程步驟新增至每個分支。

您可以使用規則定義、ECMA指令碼或外部指令碼來定義分支的路由表達式。

您可以使用變數來使用運算式編輯器定義路由運算式。 有關在「或分割」步驟中使用路由表達式的詳細資訊，請參閱[OR分割步驟](/help/sites-developing/workflows-step-ref.md#or-split)。

在此示例中，在定義路由表達式之前，請使用[example 2](../../forms/using/variable-in-aem-workflows.md#example2)來設定&#x200B;**totalvalue**&#x200B;變數的值。 如果&#x200B;**totalvalue**&#x200B;變數的值大於50000，則分支1為活動狀態。 同樣地，如果&#x200B;**totalvalue**&#x200B;變數的值小於50000，您也可以定義規則，使Branch 2生效。

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_orsplit_example.mp4)

同樣，選擇外部指令碼路徑或指定ECMA指令碼，以便路由表達式來評估活動分支。 點選&#x200B;**[!UICONTROL 重新命名分支]**&#x200B;以指定分支的替代名稱。

如需更多範例，請參閱[建立工作流模型](../../forms/using/aem-forms-workflow.md#create-a-workflow-model)。

#### 轉至步驟{#go-to-step}

**轉到步驟**&#x200B;允許您根據路由表達式的結果指定要執行的工作流模型中的下一步。

與「或分割」步驟類似，您可以使用規則定義、ECMA指令碼或外部指令碼來定義「轉到」步驟的路由表達式。

您可以使用變數來使用運算式編輯器定義路由運算式。 有關在轉至步驟中使用路由表達式的詳細資訊，請參閱[轉至步驟](/help/sites-developing/workflows-step-ref.md#goto-step)。

![轉到規則](assets/variables_goto_rule1_new.png)

在此示例中，如果&#x200B;**actiontaked**&#x200B;變數的值等於&#x200B;**需要更多資訊**，則轉到步驟指定「複查信用卡應用程式」作為下一步。

有關在轉至步驟中使用規則定義的更多示例，請參閱[模擬For循環](/help/sites-developing/workflows-step-ref.md#simulateforloop)。

#### Forms以工作流程為中心的工作流程步驟{#forms-workflow-centric-workflow-steps}

所有AEM Forms工作流程步驟都支援變數。 如需詳細資訊，請參閱OSGi](../../forms/using/aem-forms-workflow-step-reference.md)上以[Forms為中心的工作流程。

### 不支援變數{#workflow-steps-without-support-for-variables}的工作流步驟

您可以使用[MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html)介面來存取不支援變數之工作流程步驟中的變數。

#### 檢索變數值{#retrieve-the-variable-value}

在ECMA指令碼中使用下列API，根據資料類型擷取現有變數的值：

| 變數資料類型 | API |
|---|---|
| 基元（長、雙、布林、日期和字串） | workItem.getWorkflowData()。getMetaDataMap()。get(variableName, type) |
| 文件 | Packages.com.adobe.aemfd.docmanager.Document doc = workItem.getWorkflowData()。getMetaDataMap()。get(&quot;docVar&quot;, Packages.com.adobe.aemfd.docmanager.Document.class); |
| XML | Packages.org.w3c.dom.Document xmlObject = workItem.getWorkflowData()。getMetaDataMap()。get(variableName, Packages.org.w3c.dom.Document.class); |
| 表單資料模型 | Packages.com.adobe.aem.dermis.api.FormDataModelInstanceObject = workItem.getWorkflowData()。getMetaDataMap()。get(variableName, Packages.com.adobe.aem.dermis.api.FormDataModelInstance.class); |
| JSON | Packages.com.google.gson.JsonObject jsonObject = workItem.getWorkflowData()。getMetaDataMap()。get(variableName, Packages.com.google.gson.JsonObject.class); |

檔案和表單資料模型變數資料類型需要[AEM Forms附加套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)。

**範例**

使用下列API擷取字串資料類型的值：

```javascript
workItem.getWorkflowData().getMetaDataMap().get(accname, Packages.java.lang.String)
```

#### 更新變數值{#update-the-variable-value}

在ECMA指令碼中使用下列API來更新變數的值：

```javascript
workItem.getWorkflowData().getMetaDataMap().put(variableName, value)
```

**範例**

```javascript
workItem.getWorkflowData().getMetaDataMap().put(salary, 50000)
```

將&#x200B;**salary**&#x200B;變數的值更新為50000。

### 設定變數以叫用工作流程 {#apiinvokeworkflow}

您可以使用API來設定變數，並傳遞變數以叫用工作流程例項。

[workflowSession.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html#startWorkflow-com.adobe.granite.workflow.model.WorkflowModel-com.adobe.granite.workflow.exec.WorkflowData-java.util.Map-) startWorkflow將模型、wfData和metaData用作參數。使用MetaDataMap來設定變數的值。

在此API中，**variableName**&#x200B;變數是使用metaData.put(variableName, value)設為&#x200B;**value**;

```javascript
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*Assume that you already have a workflowSession and modelId along with the payloadType and payload*/
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
metaData.put(variableName, value); //Create a variable "variableName" in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

**範例**

將&#x200B;**doc**&#x200B;文檔對象初始化為路徑(&quot;a/b/c&quot;)，並將&#x200B;**docVar**&#x200B;變數的值設定為文檔對象中儲存的路徑。

```javascript
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkflowData;
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*This example assumes that you already have a workflowSession and modelId along with the payloadType and payload */
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
Document doc = new Document("/a/b/c");// initialize a document object
metaData.put("docVar",doc); //Assuming that you have created a variable "docVar" of type Document in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

## 編輯變數{#edit-a-variable}

1. 在編輯工作流程頁面上，點選工作流程模型邊腳中可用的「變數」圖示。 左窗格中的「變數」區段會顯示所有現有變數。
1. 點選您要編輯之變數名稱旁的![edit](assets/edit.png)（編輯）圖示。
1. 編輯變數資訊，然後點選![done_icon](assets/done_icon.png)以儲存變更。 您無法編輯變數的&#x200B;**[!UICONTROL Name]**&#x200B;和&#x200B;**[!UICONTROL Type]**&#x200B;欄位。

## 刪除變數{#delete-a-variable}

刪除變數之前，請先從工作流程中移除變數的所有參考。 確定變數未用於工作流程中。

執行下列步驟以刪除變數：

1. 在編輯工作流程頁面上，點選工作流程模型邊腳中可用的「變數」圖示。 左窗格中的「變數」區段會顯示所有現有變數。
1. 點選您要刪除之變數名稱旁的「刪除」圖示。
1. 點選![done_icon](assets/done_icon.png)以確認和刪除變數。

## 引用 {#references}

如需在AEM Forms工作流程步驟中使用變數的詳細範例，請參閱AEM工作流程中的[變數](https://helpx.adobe.com/experience-manager/kt/forms/using/authoring_variables_in_aem_forms-workflow1.html)。
