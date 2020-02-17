---
title: AEM工作流程中的變數
seo-title: AEM工作流程中的變數
description: 建立變數、設定變數值，並在「或分割」(OR Split)和「轉至AEM」(Goto AEM)工作流程步驟中使用它。
seo-description: 建立變數、設定變數值，並在「或分割」(OR Split)和「轉至AEM」(Goto AEM)工作流程步驟中使用它。
uuid: cc62ff11-51d4-4db4-9c6d-5dc2caa1da52
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: bbb9936e-ecd2-44b3-b4ae-dd62a3160641
docset: aem65
translation-type: tm+mt
source-git-commit: bc042696506bf1691c2eeffc6ab941be85fa274c

---


# AEM工作流程中的變數{#variables-in-aem-workflows}

工作流模型中的變數是根據其資料類型儲存值的方法。 然後，您可以在任何工作流程步驟中使用變數的名稱來擷取儲存在變數中的值。 您也可以使用變數名稱來定義用於做出路由決策的表達式。

在AEM工作流程模型中，您可以：

* [根據您要](/help/sites-developing/using-variables-in-aem-workflows.md#create-a-variable) 儲存的資訊類型，建立資料類型的變數。
* [使用「設定變數」工作流程步驟](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable) ，設定變數的值。
* [使用「OR分割](/help/sites-developing/using-variables-in-aem-workflows.md#use-a-variable) 」(OR Split)和「轉至AEM」(Goto AEM)工作流程步驟中的變數，定義用於做出路由決策的運算式。 您也可以在所有AEM Forms工作流程步驟中使用變數。

下列影片示範如何在AEM工作流程模型中建立、設定和使用變數：

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/usevariables_example.mp4)

變數是 [MetaDataMap介面的擴充功能](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) 。 您可以在ECMAScript [中使用MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) ，存取使用變數儲存的中繼資料。

## 建立變數 {#create-a-variable}

您可使用工作流程模型側腳中的「變數」區段來建立變數。 AEM工作流程變數支援下列資料類型：

* **基本資料類型**:長、雙、布爾、日期和字串
* **複雜的資料類型**: [XML](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/Document.html) 和 [JSON](https://static.javadoc.io/com.google.code.gson/gson/2.3/com/google/gson/JsonObject.html)

>[!NOTE]
>
>工作流程僅支援ISO8601格式的日期類型變數。

如需AEM Forms工作流程中可用的其他複雜資料類型，請參閱「AEM Forms工 [作流程中的變數」](/help/forms/using/variable-in-aem-workflows.md)。  使用ArrayList資料類型來建立變數集合。 您可以為所有基本和複雜資料類型建立ArrayList變數。 例如，建立ArrayList變數，並選擇「字串」作為子類型，以使用變數儲存多個字串值。

執行下列步驟以建立變數：

1. 在AEM例項上，導覽至「工具>工作流程>模型」。
1. 點選「 **[!UICONTROL 建立]** 」，並指定工作流程模型的標題和選用名稱。 選取模型並點選「編 **[!UICONTROL 輯」]**。
1. 點選工作流程模型側點中可用的變數圖示，並點選「新增變 **[!UICONTROL 數」]**。

   ![新增變數](assets/variables_add_variable_new.png)

1. 在「新增變數」對話方塊中，指定名稱並選取變數類型。
1. 從「類型」下拉式清單中 **[!UICONTROL 選取資料類型]** ，並指定下列值：

   * 基本資料類型——指定變數的選用預設值。
   * JSON或XML —— 指定選用的JSON或XML結構描述路徑。 系統在將此模式中的可用屬性映射到另一個變數並將其儲存時驗證模式路徑。
   * 表單資料模型——指定表單資料模型路徑。
   * ArrayList —— 指定系列的子類型。

1. 指定變數的選用說明，並點選以 ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) 儲存變更。 變數會顯示在左窗格的可用清單中。

建立變數時，請考慮下列實務：

* 建立工作流程所需的變數數量。 不過，為了節省資料庫資源，請使用所需的最少變數數，並盡可能重複使用變數。
* 變數會區分大小寫。 請確定您在工作流程中使用相同的案例來參考變數。
* 避免在變數名稱中使用特殊字元

## 設定變數 {#set-a-variable}

您可以使用「設定變數」步驟來設定變數的值，並定義值的設定順序。 變數的設定順序為變數映射在設定變數步驟中列出。

變數值的變更只會影響變更發生的程式例項。 例如，當啟動工作流且變數資料變更時，這些變更只會影響該工作流程的例項。 這些更改不會影響以前啟動或隨後啟動的工作流的其他實例。

視變數的資料類型而定，您可以使用下列選項來設定變數的值：

* **** 常值：當您知道要指定的確切值時，請使用此選項。
* **** 運算式：根據運算式計算要使用的值時，請使用此選項。 表達式在提供的表達式編輯器中建立。
* **** JSON點符號：使用選項從JSON或FDM類型變數擷取值。
* **** XPATH:使用選項從XML類型變數中檢索值。
* **** 相對於負載：當要儲存至變數的值位於相對負載的路徑時，請使用此選項。
* **** 絕對路徑：當要儲存至變數的值位於絕對路徑時，請使用此選項。

您也可以使用JSON DOT符號或XPATH符號來更新JSON或XML類型變數的特定元素。

### 新增變數之間的對應 {#add-mapping-between-variables}

執行下列步驟以新增變數之間的映射：

1. 在工作流程編輯頁面上，點選工作流程模型側點中的「步驟」圖示。
1. 將「設定變數」步驟拖 **放至工作流程編輯器** ，點選該步驟並選取 ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/configure_icon.png) （設定）。
1. 在「設定變數」對話方塊中，選取「 **[!UICONTROL 對應]** >新 **[!UICONTROL 增對應」]**。
1. 在「對 **應變數** 」區段中，選取要儲存資料的變數、選取對應模式，並指定要儲存在變數中的值。 對應模式會根據變數類型而有所不同。
1. 映射更多變數，以建立有意義的運算式。 點選 ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) 以儲存變更。

### 範例1:查詢XML變數以設定字串變數的值 {#example-query-an-xml-variable-to-set-value-for-a-string-variable}

選擇XML類型的變數以儲存XML檔案。 查詢XML變數，為XML檔案中可用的屬性設定字串變數的值。 使用 **為XML變數欄位指定XPATH** ，以定義要儲存在字串變數中的屬性。

在此範例中，選取 **formdata** XML變數以儲存 **cc-app.xml檔案** 。 查詢 **formdata** 變數，以設定電子郵件地址字串變數的值，以儲存 **cc-app.xml檔案中可用的emailAddress** 屬性 ******** 的值。

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/set_variable_example1.mp4 "設定變數的值")

### 範例2:使用運算式以其他變數為基礎來儲存值 {#example2}

使用運算式來計算變數的總和，並將結果儲存在變數中。

在此範例中，使用運算式編輯器來定義運算式，以計算資產 **cost** 和 **balanceamount** 變數的總和，並將結果儲存 **在totalvalue變數中** 。

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_expression.mp4)

## 使用運算式編輯器 {#use-expression-editor}

您也可以使用運算式來計算執行階段中變數的值。 變數提供運算式編輯器來定義運算式。

使用運算式編輯器可：

* 使用其他工作流程變數、數字或數學運算式來設定變數的值。
* 在數學表達式中使用工作流變數、字串、數字或表達式
* 新增條件以設定變數值。
* 在條件之間新增運算子。

![運算式編輯器](assets/variables_expression_editor_new.png)

它以具有下列變更的最適化表單規則編輯器為基礎。 變數中的規則編輯器：

* 不支援函式。
* 不提供UI來檢視規則摘要
* 沒有程式碼編輯器。
* 不支援啟用和禁用對象的值。
* 不支援對象的setting屬性。
* 不支援呼叫Web服務。

如需詳細資訊，請參 [閱最適化表單規則編輯器](/help/forms/using/rule-editor.md)。

## 使用變數 {#use-a-variable}

您可以使用變數來擷取輸入和輸出，或儲存步驟的結果。 工作流編輯器提供兩種工作流步驟：

* 支援變數的工作流程步驟
* 不支援變數的工作流程步驟

### 支援變數的工作流程步驟 {#workflow-steps-with-support-for-variables}

「跳至」步驟、「或分割」步驟和所有AEM Forms工作流程步驟都支援變數。

#### OR分割步驟 {#or-split-step}

「或分割」(OR Split)在工作流中建立一個分割，之後只有一個分支處於活動狀態。 此步驟可讓您將條件式處理路徑引入工作流程。 您可以視需要將工作流程步驟新增至每個分支。

您可以使用規則定義、ECMA指令碼或外部指令碼為分支定義路由表達式。

可以使用變數使用表達式編輯器定義路由表達式。 有關使用「或分割」(OR Split)步驟的路由表達式的詳細資訊，請參 [閱「或分割」(OR Split)步驟](/help/sites-developing/workflows-step-ref.md#or-split)。

在此示例中，在定義路由表達式之前，請使 [用示例2](/help/sites-developing/using-variables-in-aem-workflows.md#example2) 來設定 **totalvalue變數的值** 。 如果總值變數的值大於50000, **則分支** 1是活動的。 同樣地，如果總值變數的值小於50000，您也可以定義 **規則** ，使Branch 2生效。

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_orsplit_example.mp4)

同樣地，選擇外部指令碼路徑或指定路由表達式的ECMA指令碼以評估活動分支。 點選「 **[!UICONTROL 重新命名分支]** 」(Rename Branch)，指定分支的替代名稱。

如需更多範例，請參 [閱建立工作流程模型](/help/forms/using/aem-forms-workflow.md#create-a-workflow-model)。

#### 移至步驟 {#go-to-step}

「轉 **至步驟** 」(Goto Step)允許您指定工作流模型中要執行的下一個步驟，這取決於路由表達式的結果。

與「或分割」步驟類似，您可以使用規則定義、ECMA指令碼或外部指令碼來定義「轉到」步驟的路由表達式。

可以使用變數使用表達式編輯器定義路由表達式。 有關使用「轉至」(Goto)步驟的路由表達式的詳細資訊，請參 [閱「轉至步驟」](/help/sites-developing/workflows-step-ref.md#goto-step)。

![Goto規則](assets/variables_goto_rule1_new.png)

在此範例中，如果actiontaken變數的值等於「需要更多資訊」，則Goto步驟會指定「檢閱信用卡 **應用程式** 」做為下 **一個步驟**。

有關在Goto步驟中使用規則定義的更多示例，請參 [閱模擬For循環](/help/sites-developing/workflows-step-ref.md#simulateforloop)。

#### 以表單工作流程為中心的工作流程步驟 {#forms-workflow-centric-workflow-steps}

所有AEM Forms工作流程步驟都支援變數。 如需詳細資訊，請參 [閱OSGi的表單導向工作流程](/help/forms/using/aem-forms-workflow-step-reference.md)。

### 不支援變數的工作流程步驟 {#workflow-steps-without-support-for-variables}

您可以使 [用MetaDataMap介面](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) ，在不支援變數的工作流程步驟中存取變數。

#### 擷取變數值 {#retrieve-the-variable-value}

在ECMA指令碼中使用下列API，以根據資料類型擷取現有變數的值：

| 變數資料類型 | API |
|---|---|
| 基元（長、雙、布爾、日期和字串） | workItem.getWorkflowData()。getMetaDataMap()。get(variableName, type) |
| XML | Packages.org.w3c.dom.Document xmlObject = workItem.getWorkflowData()。getMetaDataMap()。get(variableName, Packages.org.w3c.dom.Document.class); |
| JSON | Packages.com.google.gson.JsonObjectJsonObject = workItem.getWorkflowData()。getMetaDataMap()。get(variableName, Packages.com.google.gson.JsonObject.class); |

如需AEM Forms工作流程中其他複雜變數資料類型的API資訊，請參閱「AEM Forms工 [作流程中的變數」](/help/forms/using/variable-in-aem-workflows.md)。

**範例**

使用下列API擷取字串資料類型的值：

```
workItem.getWorkflowData().getMetaDataMap().get(accname, Packages.java.lang.String)
```

#### 更新變數值 {#update-the-variable-value}

在ECMA指令碼中使用下列API來更新變數的值：

```
workItem.getWorkflowData().getMetaDataMap().put(variableName, value)
```

**範例**

```
workItem.getWorkflowData().getMetaDataMap().put(salary, 50000)
```

將薪金變數的 **值** 更新為50000。

### 設定變數以叫用工作流程 {#apiinvokeworkflow}

您可以使用API來設定變數，並傳遞這些變數以叫用工作流程例項。

[workflowSession.startWorkflow](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html#startWorkflow-com.adobe.granite.workflow.model.WorkflowModel-com.adobe.granite.workflow.exec.WorkflowData-java.util.Map-) 使用model、wfData和metaData作為參數。 使用MetaDataMap來設定變數的值。

在此API中， **variableName** 變數會使用metaData.put(variableName, value)設定為**value **;

```java
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

## 編輯變數 {#edit-a-variable}

1. 在編輯工作流程頁面上，點選工作流程模型側鍵中的「變數」圖示。 左窗格中的「變數」區段會顯示所有現有變數。
1. 點選 ![](https://helpx.adobe.com/content/dam/help/images/en/edit.png) 您要編輯之變數名稱旁的（編輯）圖示。
1. 編輯變數資訊並點選以 ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) 儲存變更。 您無法編輯變 **[!UICONTROL 數的]** 「名 **[!UICONTROL 稱」]** 和「類型」欄位。

## 刪除變數 {#delete-a-variable}

在刪除變數之前，請從工作流程中移除變數的所有參照。 請確定此變數未用於工作流程。

執行下列步驟以刪除變數：

1. 在編輯工作流程頁面上，點選工作流程模型側鍵中的「變數」圖示。 左窗格中的「變數」區段會顯示所有現有變數。
1. 點選您要刪除之變數名稱旁的「刪除」圖示。
1. 點選 ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) 以確認並刪除變數。

