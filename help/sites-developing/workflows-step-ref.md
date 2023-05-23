---
title: 工作流程步驟參考
seo-title: Workflow Step Reference
description: 工作流程步驟參考
seo-description: null
uuid: 88bf6997-73a1-4639-82aa-5dff08d3ef86
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e3afffd0-d90c-4bd0-b814-f7aeac6ceb6d
docset: aem65
exl-id: 8de78bde-2fcb-4221-873e-59e347ff2d74
source-git-commit: 768576e300b655962adc3e1db20fc5ec06a5ba6c
workflow-type: tm+mt
source-wordcount: '3246'
ht-degree: 2%

---

# 工作流程步驟參考 {#workflow-step-reference}

工作流模型由一系列不同類型的步驟組成。 根據類型，可以配置和擴展這些步驟，並使用參數和指令碼來提供所需的功能和控制。

>[!NOTE]
>
>本節介紹標準工作流步驟。
>
>有關模組特定的步驟，請參閱：
>
>* [AEM Forms工作流步驟參考](/help/forms/using/aem-forms-workflow-step-reference.md)
>* [使用媒體處理程式和工作流處理資產](/help/assets/media-handlers.md)
>


## 步驟屬性 {#step-properties}

每個步驟元件具有 **步驟屬性** 對話框，可以定義和編輯所需的屬性。

### 「步驟屬性」 — 「公用」頁籤 {#step-properties-common-tab}

以下屬性的組合可用於以下大多數工作流步驟元件： **常用** 的子菜單：

* **標題**
步驟的標題。

* **說明**
步驟的說明。

* **工作流程分段**

   要應用的下拉選擇器 [舞台](/help/sites-developing/workflows.md#workflow-stages) 的下界。

* **逾時**

   步驟「超時」的期間。
您可以在以下之間選擇： **關閉**。 **立即**。 **1小時**。 **6小時**。 **12小時**。 **24小時**。

* **逾時處理常式**

   當步驟超時時控制工作流的處理程式。 例如 `Auto Advancer`

* **處理常式前進**

   選擇此選項可將工作流自動推進到執行後的下一步。 如果未選中，則實施指令碼必須處理工作流進展。

### 步驟屬性 — 用戶/組頁籤 {#step-properties-user-group-tab}

以下屬性可用於以下許多工作流步驟元件： **用戶/組** 的子菜單：

* **通過電子郵件通知用戶**

   * 您可以在工作流到達步驟時向參與者發送電子郵件來通知他們。
   * 如果啟用，則向屬性定義的用戶發送電子郵件 **用戶/組**，或者，如果定義了組，則返回至組的每個成員。

* **使用者/群組**

   * 通過下拉選擇框，您可以導航並選擇用戶或組。
   * 如果將步驟分配給特定用戶，則只有此用戶才能對步驟執行操作。
   * 如果將步驟分配給整個組，則當工作流到達此步驟時，此組中的所有用戶在其中都具有操作 **工作流收件箱**。
   * 請參閱 [參與工作流](/help/sites-authoring/workflows-participating.md) 的子菜單。

## AND 拆分 {#and-split}

的 **和拆分** 在工作流中建立一個拆分，之後兩個分支都處於活動狀態。 根據需要將工作流步驟添加到每個分支。 此步驟允許您將多個處理路徑引入工作流。 例如，您可以允許並行執行某些審閱步驟，從而節省時間。

![wf-26](assets/wf-26.png)

### 和剝離 — 配置 {#and-split-configuration}

要配置剝離，請執行以下操作：

* 編輯 **和拆分屬性**:

   * **拆分名稱**:為解釋性目的指定名稱
   * 選擇所需的分支數；2、3、4或5。

* 根據需要將工作流步驟添加到分支。

   ![wf-27](assets/wf-27.png)

## 容器步驟 {#container-step}

容器步驟啟動作為子工作流執行的另一個工作流模型。

此容器允許您重用工作流模型來實現常見步驟序列。 例如，翻譯工作流模型可用於多個編輯工作流。

![wf-28](assets/wf-28.png)

### 容器步驟 — 配置 {#container-step-configuration}

要配置步驟，請編輯並使用以下頁籤：

* [常見](#step-properties-common-tab)
* **容器**

   * **子工作流**:選擇要啟動的工作流。

## 移至步驟 {#goto-step}

的 **轉至步驟** 允許您指定在工作流模型中執行的下一步。 可以指定規則定義、外部指令碼或ECMA指令碼作為路由表達式，以評估工作流模型的下一步。

* 如果指定的條件為true，則 **轉至步驟** 完成，工作流引擎將執行指定的步驟。
* 如果指定的條件不為true，則 **轉至步驟** 完成，並且常規路由邏輯確定要執行的下一步。

的 **轉至步驟** 使您能夠在工作流模型中實施高級路由結構。 例如，要實現循環， **轉至步驟** 定義為在工作流中執行前一步，路由表達式將評估循環條件。

### 轉至步驟 — 配置 {#goto-step-configuration}

要配置步驟，請編輯並使用以下頁籤：

* [常見](#step-properties-common-tab)
* **程序**

   * **目標步驟**:選擇在計算路由表達式的條件後要執行的步驟。
   * **路由表達式**:選擇規則定義、外部指令碼或ECMA指令碼，以確定是否執行 **目標步驟**。

      * **規則定義：** 使用 [表達式編輯器](/help/forms/using/variable-in-aem-workflows.md#use-expression-editor) 來修改標籤元素的屬性。
      * **外部指令碼：** 外部指令碼的路徑。
      * **ECMA指令碼**:確定是否執行 **轉至步驟**。

#### 模擬用於循環 {#simulating-a-for-loop}

模擬「for循環」要求保持已發生循環迭代次數的計數：

* 該計數通常表示工作流中所處理項的索引。
* 該計數作為循環的退出標準計算。

例如，要實現對多個JCR節點執行操作的工作流，可以使用循環計數器作為節點的索引。 要保持計數，請儲存 `integer` 值。 要增加計數並將計數與退出條件進行比較，請使用 **轉至步驟**。

```
function check(){
   var count=0;
   var keyname="loopcount"
   try{
      if (workflowData.getMetaDataMap().containsKey(keyname)){
        log.info("goto script: found loopcount key");
        count= parseInt(workflowData.getMetaDataMap().get(keyname))+1;
      }

     workflowData.getMetaDataMap().put(keyname,count);

     }catch(err) {
         log.info(err.message);
         return false;
    }
   if (parseInt(count) <7){
       return true;
   } else {
      return false;
   }
}
```

### 使用規則定義模擬for循環 {#simulateforloop}

也可以使用「規則定義」(Rule Definition)作為路由表達式來模擬for循環。 [建立 **計數** 變數](/help/forms/using/variable-in-aem-workflows.md#create-a-variable) 長資料類型。 使用 **表達式** 的 **[設定變數](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable)** 步驟以設定 **計數** 變數 **計數+ 1** 每次執行 **設定變數** 的子菜單。

![模擬for循環](assets/variable_use_case_count_new.png)

在 **轉至步驟**。 **設定變數** 的 **目標步驟** 和 **計數&lt; 5** 作為路由表達式。

![用於模擬for循環的條件](assets/variable_use_case_count1_new.png)

的 **設定變數** 步驟重複運行，遞增 **計數** 每次運行時變數為1，直到值達到5。

## OR 拆分 {#or-split}

的 **或拆分** 在工作流中建立一個拆分，之後只有一個分支處於活動狀態。 此步驟使您能夠將條件處理路徑引入工作流。 根據需要將工作流步驟添加到每個分支。

>[!NOTE]
>
>請參閱 [或拆分步驟](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/using-variables-in-aem-workflows.html?lang=en#use-a-variable)

![使用或拆分進行分支](assets/variables_orsplit_new.png)

### 或拆分 — 配置 {#or-split-configuration}

要配置剝離，請執行以下操作：

* 編輯 **或拆分屬性**:

   * **常見**

      * 指定拆分名稱。
   * **分支(*x)***

      * **添加分支：** 向步驟添加更多分支。
      * **選擇路由表達式**:要計算活動分支，請選擇路由表達式。 可能的值包括：規則定義、外部指令碼和ECMA指令碼。
      * **按一下以添加表達式**:如果選擇，則添加表達式以計算活動分支 **規則定義** 作為路由表達式。
      * **指令碼路徑**:包含指令碼的檔案的路徑，如果選擇 **外部指令碼** 作為路由表達式。
      * **指令碼**:在框中添加指令碼以評估活動分支（如果選擇） **ECMA指令碼** 作為路由表達式。
      * **預設路由**:如果存在多個分支，則遵循預設分支。 只能指定一個分支作為預設值。

   >[!NOTE]
   >
   >    * 一次根據路由表達式計算一個分支。
   >    * 分支從上到下被計算。
   >    * 執行計算為true的第一個指令碼。
   >    * 如果沒有分支計算為true，則工作流不會前進。


   >[!NOTE]
   >
   >請參閱 [定義或分解的規則](/help/sites-developing/workflows-models.md#defineruleecmascript)。

* 根據需要將工作流步驟添加到分支。

## 參與者步驟和選擇器 {#participant-steps-and-choosers}

### 參與者步驟 {#participant-step}

A **參與者步驟** 允許您為特定操作分配所有權。 僅當用戶已手動確認該步驟時，工作流才會繼續。 當您希望某人對工作流執行操作時，會使用此工作流。 例如，審閱步驟。

雖然與操作不直接相關，但在分配操作時必須考慮用戶授權；用戶必須有權訪問作為工作流負載的頁面。

#### 參與者步驟 — 配置 {#participant-step-configuration}

要配置步驟，請編輯並使用以下頁籤：

* [常見](#step-properties-common-tab)
* [使用者/群組](#step-properties-user-group-tab)

>[!NOTE]
>
>在以下情況下，始終通知工作流啟動器：
>
>* 工作流已完成（已完成）。
>* 工作流被中止（終止）。
>


>[!NOTE]
>
>必須配置某些屬性才能啟用電子郵件通知。 您還可以自定義電子郵件模板或為新語言添加電子郵件模板。 要在中配置電子郵件通AEM知，請參閱 [配置電子郵件通知](/help/sites-administering/notification.md#configuringemailnotification)。

### 對話方塊參與者步驟 {#dialog-participant-step}

使用 **對話框參與者步驟** 從分配了工作項的用戶收集資訊。 此步驟對於收集稍後在工作流中使用的少量資料非常有用。

完成步驟後， **完成工作項** 對話框包含您在對話框中定義的欄位。 在欄位中收集的資料儲存在工作流負載的節點中。 隨後的工作流步驟可以從儲存庫中讀取值。

要配置步驟，請指定要將工作項分配給的組或用戶，以及對話框的路徑。

#### 對話框參與者步驟 — 配置 {#dialog-participant-step-configuration}

要配置步驟，請編輯並使用以下頁籤：

* [常見](#step-properties-common-tab)
* [使用者/群組](#step-properties-user-group-tab)
* **對話方塊**

   * **對話框路徑**:到的對話框節點的路徑 [對話框建立](#dialog-participant-step-creating-a-dialog)。

#### 對話框參與者步驟 — 建立對話框 {#dialog-participant-step-creating-a-dialog}

要建立對話框，必須建立對話框：

* 確定結果資料的位置 [儲存在負載中](#dialog-participant-step-storing-data-in-the-payload)。
* [定義對話框；包括定義用於收集和保存資料的欄位](#dialog-participant-step-dialog-definition)。

#### 對話框參與者步驟 — 在負載中儲存資料 {#dialog-participant-step-storing-data-in-the-payload}

您可以在工作流負載或工作項元資料中儲存構件資料。 格式 `name` 構件節點的屬性確定資料儲存的位置。

* **使用負載儲存資料**

   * 要將小部件資料儲存為工作流負載的屬性，請使用以下格式來表示小部件節點名稱屬性的值：
      `./jcr:content/nodename`

   * 資料儲存在 `nodename` 負載節點的屬性。 如果節點不包含該屬性，則建立該屬性。
   * 當與負載一起儲存時，後續使用具有相同負載的對話框將覆蓋屬性的值。

* **將資料與工作項一起儲存**

   * 要將小部件資料儲存為工作項元資料的屬性，請為name屬性的值使用以下格式：
      `nodename`

   * 資料儲存在 `nodename` 工作項的屬性 `metadata`。 如果以後將對話框與相同的負載一起使用，則會保留資料。

#### 對話框參與者步驟 — 對話框定義 {#dialog-participant-step-dialog-definition}

1. **對話框結構**

   「對話框參與者步驟」(Dialog Participant Steps)的對話框與為創作元件建立的對話框類似。 它們儲存在：

   `/apps/myapp/workflow/dialogs`

   標準、啟用觸摸的UI對話框具有以下節點結構：

   ```xml
   newComponent (cq:Component)
     |- cq:dialog (nt:unstructured)
       |- content
         |- layout
           |- items
             |- column
               |- items
                 |- component0
                 |- component1
                 |- ...
   ```

   >[!NOTE]
   >
   >請參閱 [建立和配置對話框](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog)。

1. **對話框路徑屬性**

   的 **對話框參與者步驟** 的 **對話框路徑** 物業(連同 [參與者步驟](#participant-step))。 的值 **對話框路徑** 屬性是 `dialog` 的子菜單。

   例如，該對話框包含在名為 `EmailWatch` 節點中儲存的：

   `/apps/myapp/workflows/dialogs`

   對於啟用觸摸的UI，以下值用於 **對話框路徑** 屬性：

   `/apps/myapp/workflow/dialogs/EmailWatch/cq:dialog`

   ![wf-30](assets/wf-30.png)

1. **示例對話框定義**

   以下XML代碼段表示儲存 `String` 值 `watchEmail` 負載內容的節點。 標題節點表示 [文本欄位](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/textfield/index.html) 元件：

   ```xml
   jcr:primaryType="nt:unstructured"
       jcr:title="Watcher Email Address Dialog"
       sling:resourceType="cq/gui/components/authoring/dialog">
       <content jcr:primaryType="nt:unstructured"
           sling:resourceType="granite/ui/components/foundation/container">
           <layout jcr:primaryType="nt:unstructured"
               margin="false"
               sling:resourceType="granite/ui/components/foundation/layouts/fixedcolumns"
           />
           <items jcr:primaryType="nt:unstructured">
               <column jcr:primaryType="nt:unstructured"
                   sling:resourceType="granite/ui/components/foundation/container">
                   <items jcr:primaryType="nt:unstructured">
                       <title jcr:primaryType="nt:unstructured"
                           fieldLabel="Notification Email Address"
                           name="./jcr:content/watchEmails"
                           sling:resourceType="granite/ui/components/foundation/form/textfield"
                       />
                   </items>
               </column>
           </items>
       </content>
   </cq:dialog>
   ```

   在啟用觸摸的UI中，此示例將生成如下對話框：

   ![chlimage_1-70](assets/chlimage_1-70.png)

### 動態參與者步驟 {#dynamic-participant-step}

的 **動態參與者步驟** 元件與 **[參與者步驟](#participant-step)** 在運行時自動選擇參與者。

要配置步驟，請選擇 **參與者選擇器** 標識要將工作項目指派給的參與者，以及對話框。

#### 動態參與者步驟 — 配置 {#dynamic-participant-step-configuration}

要配置步驟，請編輯並使用以下頁籤：

* [常見](#step-properties-common-tab)
* **參與者選擇器**

   * **參與者選擇器**:名稱 [您建立的參與者選擇器](#developingtheparticipantchooser)。
   * **參數**:任何必需的參數。
   * **電子郵件**:是否應向用戶發送電子郵件通知。

* **對話方塊**

   * **對話框路徑**:到的對話框節點的路徑 [對話框(與 **對話框參與者步驟**)](#dialog-participant-step-creating-a-dialog)。

#### 動態參與者步驟 — 開發參與者選擇器 {#dynamic-participant-step-developing-the-participant-chooser}

建立參與者選擇器。 因此，可以使用任何選擇邏輯或條件。 例如，您的參與者選擇者可以選擇工作項最少的用戶（在組內）。 您可以建立任意數量的參與者選擇器，以便與 **動態參與者步驟** 工作流模型中的元件。

建立OSGi服務或ECMAScript，該OSGi服務或ECMAScript會選擇用戶將工作項分配給。

* **ECMAscript**

   指令碼必須包含名為getParticipant的函式，該函式將用戶ID返回為 `String` 值。 將自定義指令碼儲存在 `/apps/myapp/workflow/scripts` 或子資料夾。

   標準實例中包含一個示例腳AEM本：

   `/libs/workflow/scripts/initiator-participant-chooser.ecma`

   >[!CAUTION]
   >
   >不更改 `/libs` 路徑。
   >
   >
   >原因是 `/libs` 在下次升級實例時被覆蓋（在應用修補程式或功能包時可能被覆蓋）。

   此指令碼選擇工作流啟動器作為參與者：

   ```
   function getParticipant() {
       return workItem.getWorkflow().getInitiator();
   }
   ```

   >[!NOTE]
   >
   >的 **工作流啟動器參與者選擇器** 元件擴展 **動態參與者步驟** 並將此指令碼作為步驟實現。

* **OSGi服務**

   服務必須實施 [com.day.cq.workflow.exec.ParticipantStepChooser](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/workflow/exec/ParticipantStepChooser.html) 。 介面定義以下成員：

   * `SERVICE_PROPERTY_LABEL` 欄位：使用此欄位可指定參與者選擇器的名稱。 該名稱顯示在中的可用參與者選擇器清單中 **動態參與者步驟** 屬性。

   * `getParticipant` 方法：返回動態解析的承擔者ID作為 `String` 值。
   >[!CAUTION]
   >
   >的 `getParticipant` 方法返回動態解析的Principal id。 此ID可以是組ID或用戶ID。
   >
   >
   >但是，組ID只能用於 **參與者步驟**，返回參與者清單。 對於 **動態參與者步驟**，將返回空清單，不能用於委派。

   使您的實施可用於 **動態參與者步驟** 將Java™類添加到導出服務的OSGi捆綁包中，並將捆綁包部署到服AEM務器。

   >[!NOTE]
   >
   >**隨機參與者選擇器** 是選擇隨機用戶( `com.day.cq.workflow.impl.process.RandomParticipantChooser`)。 的 **隨機參與者選擇** r步分量樣本擴展 **動態參與者步驟** 並將此服務作為步驟實現。

#### 動態參與者步驟 — 參與者選擇器服務實例 {#dynamic-participant-step-example-participant-chooser-service}

以下Java™類實現 `ParticipantStepChooser` 。 類返回啟動工作流的參與者的名稱。 代碼使用與示例指令碼(`initiator-participant-chooser.ecma`)使用。

的 `@Property` 注釋設定 `SERVICE_PROPERTY_LABEL` 欄位 `Workflow Initiator Participant Chooser`。

```java
package com.adobe.example;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.osgi.framework.Constants;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.ParticipantStepChooser;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.metadata.MetaDataMap;

@Component
@Service
@Properties({
        @Property(name = Constants.SERVICE_DESCRIPTION, value = "An example implementation of a dynamic participant chooser."),
        @Property(name = ParticipantStepChooser.SERVICE_PROPERTY_LABEL, value = "Workflow Initiator Participant Chooser (service)") })
public class InitiatorParticipantChooser implements ParticipantStepChooser {

 private Logger logger = LoggerFactory.getLogger(this.getClass());

 public String getParticipant(WorkItem arg0, WorkflowSession arg1,
   MetaDataMap arg2) throws WorkflowException {

  String initiator = arg0.getWorkflow().getInitiator();
  logger.info("Assigning Dynamic Participant Step work item to {}",initiator);

  return initiator;
 }
}
```

在 **動態參與者步驟** 屬性對話框， **參與者選擇器** 清單包括項 `Workflow Initiator Participant Chooser (script)`，表示此服務。

啟動工作流模型時，日誌會指示啟動工作流的用戶以及分配工作項的用戶的ID。 在此示例中， `admin` 用戶已啟動工作流。

`13.09.2015 15:48:53.037 *INFO* [10.176.129.223 [1347565733037] POST /etc/workflow/instances HTTP/1.1] com.adobe.example.InitiatorParticipantChooser Assigning Dynamic Participant Step work item to admin`

### 表單參與者步驟 {#form-participant-step}

的 **表單參與者步驟** 開啟工作項時顯示窗體。 當用戶填寫並提交表單時，欄位資料被儲存在工作流負載的節點中。

要配置步驟，請指定要將工作項目分配給的組或用戶，以及表單的路徑。

>[!CAUTION]
>
>本節涉及 [用於頁面創作的Foundation Components的Forms部分](/help/sites-authoring/default-components-foundation.md#form)。

#### 表單參與者步驟 — 配置 {#form-participant-step-configuration}

要配置步驟，請編輯並使用以下頁籤：

* [常見](#step-properties-common-tab)
* [使用者/群組](#step-properties-user-group-tab)
* **表單**

   * **窗體路徑**:到 [建立的](#form-participant-step-creating-the-form)。

#### 表單參與者步驟 — 建立表單 {#form-participant-step-creating-the-form}

建立用於 **表單參與者步驟** 正常。 但是，「表單參與者步驟」的表單必須具有以下配置：

* 的 **窗體開頭** 元件必須具有 **操作類型** 屬性設定為 `Edit Workflow Controlled Resource(s)`。
* 的 **窗體開頭** 元件必須具有 `Form Identifier` 屬性。
* 窗體元件必須 **元素名稱** 屬性設定為儲存欄位資料的節點的路徑。 路徑必須在工作流負載內容中找到節點。 該值使用以下格式：

   `./jcr:content/path_to_node`

* 表單必須包含 **工作流提交按鈕** 元件。 不配置元件的任何屬性。

工作流的要求決定了您應將欄位資料儲存到何處。 例如，欄位資料可用於配置頁面內容的屬性。 以下值 **元素名稱** 屬性將欄位資料儲存為 `redirectTarget` 屬性 `jcr:content` 節點：

`./jcr:content/redirectTarget`

在以下示例中，欄位資料用作 **文本** 負載頁上的元件：

`./jcr:content/par/text_3/text`

第一個示例可用於 `cq:Page` 元件呈現。 第二個示例僅當負載頁包括 **文本** ID為 `text_3`。

表單可以位於儲存庫中的任意位置，但必須授權工作流用戶讀取表單。

### 隨機參與者選擇器 {#random-participant-chooser}

的 **隨機參與者選擇器** 步驟是參與者選擇器，它將生成的工作項目分配給從清單中隨機選擇的用戶。

![wf-31](assets/wf-31.png)

#### 隨機參與者選擇器 — 配置 {#random-participant-chooser-configuration}

要配置步驟，請編輯並使用以下頁籤：

* [常見](#step-properties-common-tab)
* **引數**

   * **參與者**:指定可供選擇的用戶清單。 要將用戶添加到清單，請按一下 **添加項** 鍵入用戶節點或用戶ID的主路徑。 用戶的順序不會影響分配工作項的可能性。

### 工作流程發起人參與者選擇器 {#workflow-initiator-participant-chooser}

的 **工作流啟動器參與者選擇器** 步驟是參與者選擇器，它將生成的工作項目分配給啟動工作流的用戶。 除配置 **常用** 屬性。

#### 工作流啟動器參與者選擇器 — 配置 {#workflow-initiator-participant-chooser-configuration}

要配置步驟，請使用以下頁籤進行編輯：

* [常見](#step-properties-common-tab)

## 程序步驟 {#process-step}

A **處理步驟** 執行ECMAScript或調用OSGi服務以執行自動處理。

![wf-32](assets/wf-32.png)

### 流程步驟 — 配置 {#process-step-configuration}

要配置步驟，請編輯並使用以下頁籤：

* [常見](#step-properties-common-tab)
* **程序**

   * **進程**:要執行的進程實現。 使用下拉菜單選擇ECMAScript或OSGi服務。 關於後述資訊：:

      * 標準ECMAScript和OSGi服務，請參見 [內置流程步驟](/help/sites-developing/workflows-process-ref.md)。
      * 為流程步驟建立ECMAScript，請參見 [使用ECMAScript實現進程步驟](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript)。
      * 為進程步驟建立OSGi服務，請參見 [使用Java™類實現進程步驟](/help/sites-developing/workflows-customizing-extending.md#implementing-a-process-step-with-a-java-class)。
   * **處理程式高級**:選擇此選項可將工作流自動推進到執行後的下一步。 如果未選中，則實施指令碼必須處理工作流進展。
   * **參數**:要傳遞到進程的參數。


## 設定變數 {#set-variable}

「設定變數」(Set Variable)步驟允許您設定變數的值並定義值的設定順序。 變數按變數映射在「設定變數」(Set Variable)步驟中列出的順序設定。

![添加映射以設定變數](assets/set_variable_addmappingnew.png)

### 設定變數 — 配置 {#setvariable}

要配置步驟，請編輯並使用以下頁籤：

* [常見](/help/sites-developing/workflows-step-ref.md#step-properties-common-tab)
* **映射**

   * **選擇變數：** 使用此選項可選擇變數以設定其值。
   * **選擇映射模式：**  要設定變數的值，請選擇映射模式。 根據變數的資料類型，可以使用以下選項來設定變數的值：

      * **文字：** 當知道要指定的精確值時，使用該選項。
      * **表達式：** 在根據表達式計算要使用的值時，使用該選項。 表達式是在提供的表達式編輯器中建立的。
      * **JSON點表示法：** 使用該選項從JSON或FDM類型變數中檢索值。
      * **XPATH:** 使用該選項從XML類型變數中檢索值。
      * **相對於負載：** 當要保存到變數的值在相對於負載的路徑上可用時，請使用該選項。
      * **絕對路徑：** 當要保存到變數的值在絕對路徑上可用時，使用該選項。
   * **指定值：** 要映射到變數，請指定一個值。 在此欄位中指定的值取決於映射模式。
   * **添加映射：** 使用此選項可添加更多映射以設定變數的值。
