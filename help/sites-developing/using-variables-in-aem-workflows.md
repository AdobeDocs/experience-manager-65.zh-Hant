---
title: AEM工作流程中的變數
description: 建立變數、設定變數的值，並在「OR分割」和「移至AEM」工作流程步驟中使用它。
uuid: cc62ff11-51d4-4db4-9c6d-5dc2caa1da52
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: bbb9936e-ecd2-44b3-b4ae-dd62a3160641
docset: aem65
exl-id: c8aeceec-860c-49ee-b681-d7107e52020d
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1941'
ht-degree: 0%

---

# AEM工作流程中的變數{#variables-in-aem-workflows}

工作流程模型中的變數是根據其資料型別儲存值的方式。 然後，您就可以在任何工作流程步驟中使用變數的名稱，來擷取儲存在變數中的值。 您也可以使用變數名稱來定義用於進行路由決定的運算式。

在AEM工作流程模型中，您可以：

* [建立變數](/help/sites-developing/using-variables-in-aem-workflows.md#create-a-variable) 根據您想要儲存在其中的資訊型別而建立的資料型別。
* [設定變數的值](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable) 使用設定變數工作流程步驟。
* [使用變數](/help/sites-developing/using-variables-in-aem-workflows.md#use-a-variable) 在「OR分割」與「移至AEM」工作流程步驟中，您可以定義用於進行路由決定的運算式。 您也可以在所有AEM Forms工作流程步驟中使用變數。

以下影片示範如何在AEM工作流程模型中建立、設定和使用變數：

<!-- FUTURE ERROR: YouTube and mp4 videos are not supported -->

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/usevariables_example.mp4)

變數是 [中繼資料地圖](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) 介面。 您可以使用 [中繼資料地圖](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) ，存取使用變數儲存的中繼資料。

## 建立變數 {#create-a-variable}

您可以使用工作流程模型Sidekick中可用的變數區段來建立變數。 AEM工作流程變數支援下列資料型別：

* **原始資料型別**：長、雙、布林值、日期和字串
* **複雜的資料型別**： [XML](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/Document.html) 和 [JSON](https://www.javadoc.io/doc/com.google.code.gson/gson/2.3/com/google/gson/JsonObject.html)

>[!NOTE]
>
>工作流程僅支援ISO8601格式用於日期型別變數。

如需AEM Forms工作流程中可用的其他複雜資料型別，請參閱 [AEM Forms工作流程中的變數](/help/forms/using/variable-in-aem-workflows.md). 使用ArrayList資料型別建立變數集合。 您可以為所有基本和複雜資料型別建立ArrayList變數。 例如，建立ArrayList變數並選取String作為子型別，以使用變數儲存多個字串值。

若要建立變數，

1. 在AEM執行個體上，導覽至「工具>工作流程>模型」 。
1. 選取 **[!UICONTROL 建立]** 並指定工作流程模型的標題和選用名稱。 選取模型並選取 **[!UICONTROL 編輯]**.
1. 選取工作流程模型Sidekick中可用的變數圖示，然後選取 **[!UICONTROL 新增變數]**.

   ![新增變數](assets/variables_add_variable_new.png)

1. 在新增變數對話方塊中，指定名稱，並選取變數的型別。
1. 從中選擇資料型別 **[!UICONTROL 型別]** 下拉式清單並指定下列值：

   * 基本資料型別 — 指定變數的選擇性預設值。
   * JSON或XML — 指定選用的JSON或XML結構描述路徑。 將這個結構描述中可用的屬性對應並儲存到另一個變數時，系統會驗證結構描述路徑。
   * 表單資料模型 — 指定表單資料模型路徑。
   * ArrayList — 指定集合的子型別。

1. 指定變數的說明（選擇性），然後選取 ![儲存方塊內以核取記號表示的圖示。](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) 以儲存變更。 變數會顯示在左窗格中可用的清單中。

建立變數時，請考量下列作法：

* 建立工作流程所需數量的變數。 不過，為了節省資料庫資源，請使用最少量的必要變數，並儘可能重複使用變數。
* 變數會區分大小寫。 請務必在工作流程中使用相同大小寫參考變數。
* 避免在變數的名稱中使用特殊字元

## 設定變數 {#set-a-variable}

您可以使用「設定變數」步驟來設定變數的值，並定義設定值的順序。 變數會依照變數對應在設定變數步驟中列出的順序來設定。

變數值的變更只會影響變更發生的程式例項。 例如，啟動工作流程並變更變數資料時，變更只會影響該工作流程例項。 變更不會影響先前已起始或稍後起始之工作流程的其他執行個體。

視變數的資料型別而定，您可以使用下列選項來設定變數的值：

* **常值：** 知道要指定的確切值時使用選項。
* **運算式：** 根據運算式計算要使用的值時，請使用選項。 運算式是在提供的運算式編輯器中建立。
* **JSON點標籤法：** 使用選項從JSON或FDM型別變數擷取值。
* **XPATH：** 使用選項從XML型別變數擷取值。
* **相對於承載：** 當要儲存至變數的值可在相對於承載的路徑取得時，請使用選項。
* **絕對路徑：** 當要儲存至變數的值可在絕對路徑取得時，請使用選項。

您也可以使用JSON DOT Notation或XPATH標籤法更新JSON或XML型別變數的特定元素。

### 新增變數之間的對應 {#add-mapping-between-variables}

若要在變數之間新增對應，請執行下列動作：

1. 在工作流程編輯頁面上，選取工作流程模型Sidekick中可用的步驟圖示。
1. 拖放 **設定變數** 步驟到工作流程編輯器，選取該步驟，然後選取 ![設定扳手所指示的圖示。](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/configure_icon.png) （設定）。
1. 在設定變數對話方塊中，選取 **[!UICONTROL 對應]** > **[!UICONTROL 新增對應]**.
1. 在 **對應變數** 區段，選取要儲存資料的變數、選取對應模式，然後指定要儲存在變數中的值。 對應模式會因變數型別而異。
1. 對應更多變數，以便做出有意義的運算式。 選取 ![儲存方塊內以核取記號表示的圖示。](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) 以儲存變更。

### 範例1：查詢XML變數以設定字串變數的值 {#example-query-an-xml-variable-to-set-value-for-a-string-variable}

選取要儲存XML檔案的XML型別變數。 查詢XML變數，為XML檔案中可用的屬性設定字串變數的值。 使用 **指定XML變數的XPATH** 欄位，定義要儲存在字串變數中的屬性。

在此範例中，選取 **formdata** 要儲存的XML變數 **cc-app.xml** 檔案。 查詢 **formdata** 變數，讓您可以為以下專案設定 **電子郵件地址** 字串變數來儲存的值 **電子郵件地址** 中可用的屬性 **cc-app.xml** 檔案。

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/set_variable_example1.mp4 "設定變數的值")

### 範例2：使用運算式根據其他變數儲存值 {#example2}

使用運算式來計算變數的總和，並將結果儲存在變數中。

在此範例中，使用運算式編輯器定義運算式以計算 **assetscost** 和 **balanceamount** 變數並儲存結果於 **totalvalue** 變數中。

<!-- FUTURE ERROR: YouTube and mp4 videos are not supported -->

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_expression.mp4)

## 使用運算式編輯器 {#use-expression-editor}

您也可以使用運算式，在執行階段計算變數的值。 變數提供運算式編輯器以定義運算式。

使用運算式編輯器可以：

* 使用其他工作流程變數、數字或數學運算式設定變數值。
* 在數學運算式中使用工作流程變數、字串、數字或運算式
* 新增條件，讓您可以設定變數的值。
* 在條件之間新增運運算元。

![運算式編輯器](assets/variables_expression_editor_new.png)

這會根據調適型表單規則編輯器，且有下列變更。 變數中的規則編輯器：

* 不支援函式。
* 不提供可檢視規則摘要的UI
* 沒有程式碼編輯器。
* 不支援啟用和停用物件的值。
* 不支援設定物件的屬性。
* 不支援呼叫網站服務。

如需詳細資訊，請參閱 [調適型表單規則編輯器](/help/forms/using/rule-editor.md).

## 使用變數 {#use-a-variable}

您可以使用變數來擷取輸入和輸出，或儲存步驟的結果。 工作流程編輯器提供兩種型別的工作流程步驟：

* 支援變數的工作流程步驟
* 不支援變數的工作流程步驟

### 支援變數的工作流程步驟 {#workflow-steps-with-support-for-variables}

前往步驟（或「分割」步驟）和所有AEM Forms工作流程步驟都支援變數。

#### OR拆分步驟 {#or-split-step}

「OR分割」會在工作流程中建立分割，之後只有一個分支處於作用中狀態。 此步驟可讓您將條件式處理路徑匯入工作流程中。 您可以視需要將工作流程步驟新增到每個分支。

您可以使用規則定義、ECMA命令檔或外部命令檔來定義分支的路由表示式。

您可以使用變數來定義使用運算式編輯器的路由運算式。 如需有關對「OR分割」步驟使用路由運算式的詳細資訊，請參閱 [OR拆分步驟](/help/sites-developing/workflows-step-ref.md#or-split).

在此範例中，定義路由運算式之前，請使用 [範例2](/help/sites-developing/using-variables-in-aem-workflows.md#example2) 設定 **totalvalue** 變數中。 如果下列專案的值，則分支1為作用中： **totalvalue** 變數大於50000。 同樣地，您可以定義規則以使「分支2」在下列情況下啟動： **totalvalue** 變數小於50000。

<!-- FUTURE ERROR: YouTube and mp4 videos are not supported -->

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_orsplit_example.mp4)

同樣地，選取外部指令集路徑，或指定路由運算式的ECMA指令集以評估作用中分支。 選取 **[!UICONTROL 重新命名分支]** 指定分支的替代名稱。

如需更多範例，請參閱 [建立工作流程模型](/help/forms/using/aem-forms-workflow.md#create-a-workflow-model).

#### 前往步驟 {#go-to-step}

此 **移至步驟** 可讓您根據路由表示式的結果，指定下一個要在工作流程模型中執行的步驟。

與「OR分割」步驟類似，您可以使用規則定義、ECMA指令集或外部指令集來定義「轉至」步驟的路由表示式。

您可以使用變數來定義使用運算式編輯器的路由運算式。 如需在「跳至」步驟中使用路由運算式的詳細資訊，請參閱 [移至步驟](/help/sites-developing/workflows-step-ref.md#goto-step).

![移至規則](assets/variables_goto_rule1_new.png)

在此範例中，如果「 」的值，則「轉至」步驟會將「複查信用卡應用程式」指定為下一個步驟 **已執行動作** 變數等於 **需要更多資訊**.

如需在「跳至」步驟中使用規則定義的更多範例，請參閱 [模擬For回圈](/help/sites-developing/workflows-step-ref.md#simulateforloop).

#### 以Forms工作流程為中心的工作流程步驟 {#forms-workflow-centric-workflow-steps}

所有AEM Forms工作流程步驟都支援變數。 如需詳細資訊，請參閱 [OSGi上以Forms為中心的工作流程](/help/forms/using/aem-forms-workflow-step-reference.md).

### 不支援變數的工作流程步驟 {#workflow-steps-without-support-for-variables}

您可以使用 [中繼資料地圖](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) 介面以存取工作流程步驟中不支援變數的變數。

#### 擷取變數值 {#retrieve-the-variable-value}

若要根據資料型別擷取現有變數的值，請在ECMA指令碼中使用以下API。

| 變數資料型別 | API |
|---|---|
| 原始（長、雙、布林、日期和字串） | workItem.getWorkflowData()。getMetaDataMap()。get(variableName， type) |
| XML | Packages.org.w3c.dom.Document xmlObject = workItem.getWorkflowData()。getMetaDataMap()。get(variableName， Packages.org.w3c.dom.Document.class)； |
| JSON | Packages.com.google.gson.JsonObject jsonObject = workItem.getWorkflowData()。getMetaDataMap()。get(variableName， Packages.com.google.gson.JsonObject.class)； |

如需AEM Forms工作流程中提供之其他複雜變數資料型別的API相關資訊，請參閱 [AEM Forms工作流程中的變數](/help/forms/using/variable-in-aem-workflows.md).

**範例**

使用以下API擷取字串資料型別的值：

```
workItem.getWorkflowData().getMetaDataMap().get(accname, Packages.java.lang.String)
```

#### 更新變數值 {#update-the-variable-value}

若要更新變數的值，請在ECMA指令碼中使用以下API。

```
workItem.getWorkflowData().getMetaDataMap().put(variableName, value)
```

**範例**

```
workItem.getWorkflowData().getMetaDataMap().put(salary, 50000)
```

更新值 **salary** 變數來傳50000。

### 設定變數以叫用工作流程 {#apiinvokeworkflow}

您可以使用API來設定變數，並傳遞它們以叫用工作流程例項。

[workflowSession.startWorkflow](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/workflow/WorkflowSession.html#startWorkflow-com.adobe.granite.workflow.model.WorkflowModel-com.adobe.granite.workflow.exec.WorkflowData-java.util.Map-) 使用model、wfData和metaData作為引數。 使用MetaDataMap設定變數的值。

在此API中， **variableName** 變數設為 **值** 使用metaData.put(variableName， value)；

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

1. 在編輯工作流程頁面上，選取工作流程模型Sidekick中可用的「變數」圖示。 左窗格中的變數區段會顯示所有現有的變數。
1. 選取 ![以鉛筆符號表示的編輯圖示。](https://helpx.adobe.com/content/dam/help/images/en/edit.png) （編輯）圖示加以選取，並位於您要編輯的變數名稱旁。
1. 編輯變數資訊並選取 ![以核取記號指示的儲存圖示。](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) 以儲存變更。 您無法編輯 **[!UICONTROL 名稱]** 和 **[!UICONTROL 型別]** 變數的欄位。

## 刪除變數 {#delete-a-variable}

在刪除變數之前，請從工作流程中移除變數的所有參考。 請確定此變數並未用於工作流程中。

若要刪除變數，

1. 在編輯工作流程頁面上，選取工作流程模型Sidekick中可用的「變數」圖示。 左窗格中的變數區段會顯示所有現有的變數。
1. 選取您要刪除之變數名稱旁的刪除圖示。
1. 選取 ![以核取記號符號表示的「完成」圖示。](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) 以確認並刪除變數。
