---
title: 工作流程步驟參考
seo-title: 工作流程步驟參考
description: 'null'
seo-description: 'null'
uuid: 88bf6997-73a1-4639-82aa-5dff08d3ef86
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e3afffd0-d90c-4bd0-b814-f7aeac6ceb6d
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '3286'
ht-degree: 2%

---


# 工作流步驟參考{#workflow-step-reference}

工作流模型由各種類型的一系列步驟組成。 根據類型，這些步驟可以配置並擴展參數和指令碼，以提供所需的功能和控制。

>[!NOTE]
>
>本節介紹標準的「工作流」步驟。
>
>有關模組特定步驟，另請參閱：
>
>* [AEM Forms工作流程步驟參考](/help/forms/using/aem-forms-workflow-step-reference.md)
>* [使用媒體處理常式和工作流程處理資產](/help/assets/media-handlers.md)

>



## 步驟屬性 {#step-properties}

每個步驟元件都有一個&#x200B;**步驟屬性**&#x200B;對話框，允許您定義和編輯所需屬性。

### 步驟屬性——公共頁籤{#step-properties-common-tab}

在屬性對話框的&#x200B;**Common**&#x200B;頁籤上，大多數工作流步驟元件都可以使用以下屬性組合：

* **標**
題步驟的標題。

* **說**
明步驟說明。

* **工作流程分段**

   將[舞台](/help/sites-developing/workflows.md#workflow-stages)套用至步驟的下拉式選擇器。

* **逾時**

   步驟將在此時段後「逾時」。
您可以選擇：**Off**、**Immediate**、**1h**、**6h**、**12h**、**24h**。

* **逾時處理常式**

   當步驟逾時時，控制工作流程的處理程式；例如：
   `Auto Advancer`

* **處理常式前進**

   選擇此選項可自動將工作流推進到執行後的下一個步驟。 如果未選取，實施指令碼必須處理工作流程的進階。

### 步驟屬性——用戶／組頁籤{#step-properties-user-group-tab}

屬性對話框的&#x200B;**用戶／組**&#x200B;頁籤上的許多工作流步驟元件可以使用以下屬性：

* **透過電子郵件通知使用者**

   * 當工作流程到達步驟時，您可以傳送電子郵件通知參與者。
   * 如果啟用，則會傳送電子郵件給&#x200B;**User/Group**&#x200B;屬性所定義的使用者，或如果已定義群組，則傳送電子郵件給群組的每個成員。

* **使用者/群組**

   * 下拉式選取方塊可讓您導覽並選取使用者或群組。
   * 如果您將步驟指派給特定使用者，則只有此使用者可對步驟採取動作。
   * 如果您將步驟指派給整個群組，則當工作流程到達此步驟時，此群組中的所有使用者都會在其「工作流程收件匣」中執行動作。****
   * 如需詳細資訊，請參閱[參與工作流程](/help/sites-authoring/workflows-participating.md)。

## AND 拆分 {#and-split}

**AND Split**&#x200B;會在工作流中建立拆分，之後兩個分支都將處於活動狀態。 您可以視需要將工作流程步驟新增至每個分支。 此步驟可讓您在工作流程中引入多個處理路徑。 例如，您可以允許同時執行某些審核步驟，以節省時間。

![wf-26](assets/wf-26.png)

### AND Split —— 配置{#and-split-configuration}

要配置拆分：

* 編輯&#x200B;**AND拆分屬性**:

   * **拆分名稱**:為說明性目的指派名稱
   * 選擇所需的分支數；2、3、4或5。

* 視需要將工作流程步驟新增至分支。

   ![wf-27](assets/wf-27.png)

## 容器步驟 {#container-step}

容器步驟會啟動另一個以子工作流程執行的工作流程模型。

此容器可讓您重複使用工作流程模型，以實作常用的步驟順序。 例如，翻譯工作流程模型可用於多個編輯工作流程。

![wf-28](assets/wf-28.png)

### 容器步驟——設定{#container-step-configuration}

若要設定步驟，請編輯並使用下列標籤：

* [常見](#step-properties-common-tab)
* **容器**

   * **子工作流**:選擇要啟動的工作流。

## 移至步驟 {#goto-step}

**轉至步驟**&#x200B;允許您指定要在工作流模型中執行的下一個步驟。 您可以指定規則定義、外部指令碼或ECMA指令碼作為路由表達式，以評估工作流模型的下一步。

* 如果您指定的條件成立，則&#x200B;**Goto步驟**&#x200B;會完成，而工作流程引擎會執行指定的步驟。
* 如果您指定的條件不成立，則&#x200B;**Goto步驟**&#x200B;將完成，而一般路由邏輯將決定要執行的下一步。

**轉至步驟**&#x200B;可讓您在工作流模型中實施高級路由結構。 例如，為了實施循環，可以定義&#x200B;**Goto步驟**&#x200B;以在工作流中執行前一步驟，其中路由表達式評估循環條件。

### Goto Step - Configuration {#goto-step-configuration}

若要設定步驟，請編輯並使用下列標籤：

* [常見](#step-properties-common-tab)
* **程序**

   * **目標步驟**:選擇在評估路由表達式的條件後要執行的步驟。
   * **路由表達式**:選擇規則定義、外部指令碼或ECMA指令碼，以確定是否執行 **目標步驟**。

      * **規則定義：** 使用運算 [式](/help/forms/using/variable-in-aem-workflows.md#use-expression-editor) 編輯器來定義規則。
      * **外部指令碼：** 外部指令碼的路徑。
      * **ECMA指令碼**:決定是否執行「轉至步驟」的 **指令碼**。

#### 模擬循環{#simulating-a-for-loop}

模擬for循環需要您保持已發生循環迭代次數的計數：

* 計數通常表示在工作流中操作的項的索引。
* 計數會評估為循環的退出准則。

例如，要實施對多個JCR節點執行操作的工作流，可以使用循環計數器作為節點的索引。 若要保存計數，請將`integer`值儲存在工作流程例項的資料地圖中。 使用&#x200B;**Goto Step**&#x200B;的指令碼來增加計數，並比較計數與退出標準。

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

### 使用規則定義{#simulateforloop}模擬for循環

也可以使用「規則定義」(Rule Definition)作為路由表達式來模擬for循環。 [建立「 **** ](/help/forms/using/variable-in-aem-workflows.md#create-a-variable) 長」資料類型的countvariable。使用&#x200B;**表達式**&#x200B;作為&#x200B;**[設定變數](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable)**&#x200B;步驟中的映射模式，在&#x200B;**設定變數**&#x200B;步驟的每次執行中，將&#x200B;**count**&#x200B;變數的值設定為&#x200B;**count + 1**。

![模擬for循環](assets/variable_use_case_count_new.png)

在&#x200B;**Goto步驟**&#x200B;中，使用&#x200B;**設定變數**&#x200B;作為&#x200B;**目標步驟**&#x200B;和&#x200B;**計數&lt;5**&#x200B;作為路由表達式。

![用於模擬for環的條件](assets/variable_use_case_count1_new.png)

每次執行時，**設定變數**&#x200B;步驟會重複將&#x200B;**count**&#x200B;變數的值增加1，直到值達到5。

## OR 拆分 {#or-split}

**OR Split**&#x200B;會在工作流中建立拆分，之後只有一個分支處於活動狀態。 此步驟可讓您將條件式處理路徑引入工作流程中。 您可以視需要將工作流程步驟新增至每個分支。

>[!NOTE]
>
>有關建立OR分割的其他資訊，請參閱：[https://helpx.adobe.com/experience-manager/using/aem64_workflow_servlet.html](https://helpx.adobe.com/experience-manager/using/aem64_workflow_servlet.html)

![使用OR分割分支](assets/variables_orsplit_new.png)

### OR Split —— 配置{#or-split-configuration}

要配置拆分：

* 編輯&#x200B;**OR拆分屬性**:

   * **常見**

      * 指定拆分名稱。
   * **分支(*x)***

      * **新增分支：** 新增更多分支至步驟。
      * **選擇路由表達式**:選擇路由表達式以評估活動分支。可能的值包括：規則定義、外部指令碼和ECMA指令碼。
      * **按一下以新增運算式**:如果選擇「規則定義」( **Rule** Definition)作為路由表達式，則添加表達式以評估活動分支。
      * **指令碼路徑**:如果選擇「外部指令碼」作為路由表達式，則包含指令碼的檔案路 **徑** 將評估活動分支。
      * **指令碼**:如果選擇 **ECMA Scripts作為路由表達式，請在框中添加指令碼以評估活動** 分支。
      * **預設路由**:若有多個分支，則會跟隨預設分支。您只能指定一個分支作為預設值。

   >[!NOTE]
   >
   >    * 根據路由表達式一次計算一個分支。
   >    * 分支會從上到下評估。
   >    * 會執行評估為true的第一個指令碼。
   >    * 如果沒有分支評估為true，則工作流程不會前進。


   >[!NOTE]
   >
   >請參閱[定義OR分割的規則](/help/sites-developing/workflows-models.md#defineruleecmascript)。

* 視需要將工作流程步驟新增至分支。

## 參與者步驟和選擇器{#participant-steps-and-choosers}

### 參與者步驟 {#participant-step}

**參與者步驟**&#x200B;可讓您為特定動作指派所有權。 只有當使用者已手動確認步驟時，工作流程才會繼續。 當您希望某人對工作流程採取動作時，就會使用此功能；例如，審核步驟。

雖然不直接相關，但在指派動作時必須考慮使用者授權；使用者必須擁有工作流程裝載之頁面的存取權。

#### 參與者步驟——配置{#participant-step-configuration}

若要設定步驟，請編輯並使用下列標籤：

* [常見](#step-properties-common-tab)
* [使用者/群組](#step-properties-user-group-tab)

>[!NOTE]
>
>當出現以下情況時，始終會通知工作流啟動器：
>
>* 工作流程已完成（完成）。
>* 工作流被中止（終止）。

>



>[!NOTE]
>
>必須設定某些屬性，才能啟用電子郵件通知。 您也可以自訂電子郵件範本，或新增新語言的電子郵件範本。 請參閱[設定電子郵件通知](/help/sites-administering/notification.md#configuringemailnotification)以在AEM中設定電子郵件通知。

### 對話方塊參與者步驟 {#dialog-participant-step}

使用&#x200B;**對話參與者步驟**&#x200B;從指派工作項目的使用者收集資訊。 此步驟對於收集稍後在工作流程中使用的少量資料非常有用。

完成步驟後，**「完成工作項目」(Complete Work Item)**&#x200B;對話框將包含您在對話框中定義的欄位。 在欄位中收集的資料會儲存在工作流程裝載的節點中。 隨後的工作流步驟可以從儲存庫讀取值。

要配置步驟，請指定要將工作項指定給的組或用戶，以及對話框的路徑。

#### 對話方塊參與者步驟——配置{#dialog-participant-step-configuration}

若要設定步驟，請編輯並使用下列標籤：

* [常見](#step-properties-common-tab)
* [使用者/群組](#step-properties-user-group-tab)
* **對話方塊**

   * **對話路徑**:您所建立對話框的對話框節 [點的路徑](#dialog-participant-step-creating-a-dialog)。

#### 對話框參與者步驟——建立對話框{#dialog-participant-step-creating-a-dialog}

要建立對話框，需要建立對話框：

* 確定結果資料將儲存在裝載[中的位置。](#dialog-participant-step-storing-data-in-the-payload)
* [定義對話框；這包括定義用於收集（和儲存）資料的欄位](#dialog-participant-step-dialog-definition)。

#### 對話方塊參與者步驟——將資料儲存在裝載{#dialog-participant-step-storing-data-in-the-payload}

您可以將介面工具集資料儲存在工作流程裝載或工作項目中繼資料中。 介面工具集節點的`name`屬性格式決定資料的儲存位置。

* **將資料與裝載一起儲存**

   * 要將Widget資料儲存為工作流裝載的屬性，請對Widget節點的name屬性值使用以下格式：
      `./jcr:content/nodename`

   * 資料儲存在裝載節點的`nodename`屬性中。 如果節點不包含該屬性，則會建立該屬性。
   * 當與裝載一起儲存時，後續使用相同裝載的對話方塊會覆寫屬性的值。

* **將資料與工作項目一起儲存**

   * 要將Widget資料儲存為工作項目元資料的屬性，請對name屬性的值使用以下格式：
      `nodename`

   * 資料儲存在工作項`metadata`的`nodename`屬性中。 如果對話方塊隨後與相同的裝載搭配使用，則會保留資料。

#### 對話框參與者步驟——對話框定義{#dialog-participant-step-dialog-definition}

1. **對話框結構**

   「對話方塊參與者步驟」(Dialog Participant Steps)對話框與您為編寫元件而建立的對話框類似。 它們儲存在：

   `/apps/myapp/workflow/dialogs`

   標準觸控式UI的對話方塊具有下列節點結構：

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
   >有關詳細資訊，請參閱[建立和配置對話框](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog)。

1. **對話框路徑屬性**

   **對話參與者步驟**&#x200B;具有&#x200B;**對話路徑**&#x200B;屬性（以及[參與者步驟](#participant-step)的屬性）。 **對話路徑**&#x200B;屬性的值是對話框`dialog`節點的路徑。

   例如，該對話框包含在儲存在節點中名為`EmailWatch`的元件中：

   `/apps/myapp/workflows/dialogs`

   對於啟用觸控的UI,**對話路徑**&#x200B;屬性會使用下列值：

   `/apps/myapp/workflow/dialogs/EmailWatch/cq:dialog`

   ![wf-30](assets/wf-30.png)

1. **示例對話框定義**

   以下XML代碼片段代表一個對話框，該對話框將`String`值儲存在裝載內容的`watchEmail`節點中。 標題節點表示[TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/textfield/index.html)元件：

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

   此範例會在啟用觸控功能的UI中產生對話方塊，例如：

   ![chlimage_1-70](assets/chlimage_1-70.png)

### 動態參與者步驟 {#dynamic-participant-step}

**動態參與者步驟**&#x200B;元件與&#x200B;**[參與者步驟](#participant-step)**&#x200B;類似，其差異是在運行時自動選擇參與者。

要配置步驟，請選擇&#x200B;**參與者選擇器**，該選擇器標識要將工作項目分配給的參與者，以及對話框。

#### 動態參與者步驟——配置{#dynamic-participant-step-configuration}

若要設定步驟，請編輯並使用下列標籤：

* [常見](#step-properties-common-tab)
* **參與者選擇器**

   * **參與者選擇器**:您建立的參 [與者選擇器名稱](#developingtheparticipantchooser)。
   * **引數**:任何必要引數。
   * **電子郵件**:是否應將電子郵件通知傳送給使用者。

* **對話方塊**

   * **對話路徑**:您所建立對話框的對話框節 [點的路徑(與「對話 **參與者步驟**」一樣)](#dialog-participant-step-creating-a-dialog)。

#### 動態參與者步驟——開發參與者選擇器{#dynamic-participant-step-developing-the-participant-chooser}

您會建立參與者選擇器。 因此，您可以使用任何選擇邏輯或標準。 例如，您的參與者選擇器可以選取工作項目最少的使用者（在群組內）。 您可以建立任意數量的參與者選擇器，以便用於工作流模型中&#x200B;**動態參與者步驟**&#x200B;元件的不同實例。

建立OSGi服務或ECMAScript，以選擇使用者將工作項目指派給。

* **ECMAscript**

   指令碼必須包含名為getParticipant的函式，其會傳回使用者ID為`String`值。 將自訂指令碼儲存在`/apps/myapp/workflow/scripts`資料夾或子資料夾中。

   標準AEM例項中包含範例指令碼：

   `/libs/workflow/scripts/initiator-participant-chooser.ecma`

   >[!CAUTION]
   >
   >您&#x200B;***必須***&#x200B;不要變更`/libs`路徑中的任何項目。
   >
   >
   >這是因為下次升級實例時會覆寫`/libs`的內容（當您套用修補程式或功能套件時可能會覆寫）。

   此指令碼選擇工作流啟動器作為參與者：

   ```
   function getParticipant() {
       return workItem.getWorkflow().getInitiator();
   }
   ```

   >[!NOTE]
   >
   >**工作流啟動器參與者選擇器**&#x200B;元件擴展&#x200B;**動態參與者步驟**&#x200B;並使用此指令碼作為步驟實施。

* **OSGi服務**

   服務必須實作[com.day.cq.workflow.exec.ParticipantStepChooser](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/ParticipantStepChooser.html)介面。 介面定義以下成員：

   * `SERVICE_PROPERTY_LABEL` 欄位：使用此欄位指定參與者選擇器的名稱。名稱會出現在&#x200B;**動態參與者步驟**&#x200B;屬性中的可用參與者選擇器清單中。

   * `getParticipant` 方法：將動態解析的承擔者ID返回 `String` 值。
   >[!CAUTION]
   >
   >`getParticipant`方法返回動態解析的承擔者ID。 這可以是群組ID或使用者ID。
   >
   >
   >但是，在返回參與者清單時，組ID只能用於&#x200B;**參與者步驟**。 對於&#x200B;**動態參與者步驟**，會傳回空白清單，這無法用於委派。

   若要將您的實作提供給&#x200B;**動態參與者步驟**&#x200B;元件，請將您的Java類別新增至匯出服務的OSGi套件，並將套件部署至AEM伺服器。

   >[!NOTE]
   >
   >**隨機參與** 者選擇是選擇隨機使用者( `com.day.cq.workflow.impl.process.RandomParticipantChooser`)的範例服務。**隨機參與者選擇** r步驟元件示例擴展&#x200B;**動態參與者步驟**&#x200B;並使用此服務作為步驟實施。

#### 動態參與者步驟——參與者選擇器服務示例{#dynamic-participant-step-example-participant-chooser-service}

以下Java類實現`ParticipantStepChooser`介面。 類返回啟動工作流的參與者的名稱。 程式碼使用的邏輯與範例指令碼(`initiator-participant-chooser.ecma`)使用的邏輯相同。

`@Property`注釋將`SERVICE_PROPERTY_LABEL`欄位的值設定為`Workflow Initiator Participant Chooser`。

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

在&#x200B;**動態參與者步驟**&#x200B;屬性對話方塊中，**參與者選擇器**&#x200B;清單包含代表此服務的項目`Workflow Initiator Participant Chooser (script)`。

啟動工作流模型時，日誌會指示啟動工作流的用戶的ID以及為其分配了工作項的用戶。 在此示例中，`admin`用戶啟動了工作流。

`13.09.2015 15:48:53.037 *INFO* [10.176.129.223 [1347565733037] POST /etc/workflow/instances HTTP/1.1] com.adobe.example.InitiatorParticipantChooser Assigning Dynamic Participant Step work item to admin`

### 表單參與者步驟 {#form-participant-step}

**表單參與者步驟**&#x200B;在開啟工作項目時顯示表單。 當用戶填寫並提交表單時，欄位資料被儲存在工作流負載的節點中。

要配置步驟，請指定要將工作項目分配給的組或用戶，以及表單的路徑。

>[!CAUTION]
>
>本節介紹Foundation Components for Page Authoring的[ Forms部分。](/help/sites-authoring/default-components-foundation.md#form)

#### 表單參與者步驟——配置{#form-participant-step-configuration}

若要設定步驟，請編輯並使用下列標籤：

* [常見](#step-properties-common-tab)
* [使用者/群組](#step-properties-user-group-tab)
* **表單**

   * **表單路徑**:您建立的表 [單路徑](#form-participant-step-creating-the-form)。

#### 表單參與者步驟——建立表單{#form-participant-step-creating-the-form}

建立表單，以便正常使用&#x200B;**表單參與者步驟**。 但是，表單參與者步驟的表單必須具備下列組態：

* **Start of Form**&#x200B;元件必須將&#x200B;**Action Type**&#x200B;屬性設定為`Edit Workflow Controlled Resource(s)`。
* **Start of Form**&#x200B;元件必須具有`Form Identifier`屬性的值。
* 表單元件必須將&#x200B;**元素名稱**&#x200B;屬性設定為儲存欄位資料的節點的路徑。 路徑必須在工作流裝載內容中找到節點。 值使用下列格式：

   `./jcr:content/path_to_node`

* 表單必須包含&#x200B;**Workflow Submit Button(s)**&#x200B;元件。 不要配置元件的任何屬性。

工作流程的需求會決定您應將欄位資料儲存在何處。 例如，欄位資料可用來設定頁面內容的屬性。 **元素名稱**&#x200B;屬性的下列值將欄位資料儲存為`jcr:content`節點的`redirectTarget`屬性的值：

`./jcr:content/redirectTarget`

在以下示例中，欄位資料用作裝載頁上&#x200B;**Text**&#x200B;元件的內容：

`./jcr:content/par/text_3/text`

第一個範例可用於`cq:Page`元件轉譯的任何頁面。 第二個範例僅在裝載頁面包含ID為`text_3`的&#x200B;**Text**&#x200B;元件時才可使用。

表單可以位於儲存庫的任意位置，但工作流用戶必須獲得讀取表單的授權。

### 隨機參與者選擇器 {#random-participant-chooser}

**隨機參與者選擇器**&#x200B;步驟是參與者選擇器，用於將生成的工作項目指派給從清單中隨機選擇的用戶。

![wf-31](assets/wf-31.png)

#### 隨機參與者選擇器——配置{#random-participant-chooser-configuration}

若要設定步驟，請編輯並使用下列標籤：

* [常見](#step-properties-common-tab)
* **引數**

   * **參與者**:指定可供選擇的用戶清單。要將用戶添加到清單中，請按一下&#x200B;**添加項目** ，然後鍵入用戶節點或用戶ID的主路徑。 使用者的順序不會影響指派工作項目的可能性。

### 工作流程發起人參與者選擇器 {#workflow-initiator-participant-chooser}

**工作流啟動器參與者選擇器**&#x200B;步驟是參與者選擇器，用於將生成的工作項目分配給啟動工作流的用戶。 除了&#x200B;**Common**&#x200B;屬性外，沒有其他屬性可進行配置。

#### 工作流啟動器參與者選擇器——配置{#workflow-initiator-participant-chooser-configuration}

若要設定步驟，請使用下列標籤進行編輯：

* [常見](#step-properties-common-tab)

## 程序步驟 {#process-step}

**處理步驟**&#x200B;執行ECMAScript或呼叫OSGi服務以執行自動處理。

![wf-32](assets/wf-32.png)

### 流程步驟——配置{#process-step-configuration}

若要設定步驟，請編輯並使用下列標籤：

* [常見](#step-properties-common-tab)
* **程序**

   * **流程**:要執行的進程實施。使用下拉式選單來選取ECMAScript或OSGi服務。 如需下列相關資訊：

      * 標準的ECMAScript和OSGi服務，請參見[內置流程步驟](/help/sites-developing/workflows-process-ref.md)。
      * 為流程步驟建立ECMAScript，請參見[使用ECMAScript](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript)實現流程步驟。
      * 為流程步驟建立OSGi服務，請參閱[使用Java類實施流程步驟](/help/sites-developing/workflows-customizing-extending.md#implementing-a-process-step-with-a-java-class)。
   * **處理常式進階**:選擇此選項可自動將工作流推進到執行後的下一個步驟。如果未選取，實施指令碼必須處理工作流程的進階。
   * **引數**:要傳遞給進程的參數。


## 設定變數 {#set-variable}

「設定變數」(Set Variable)步驟可讓您設定變數的值，並定義值的設定順序。 變數的設定順序為變數映射在「設定變數」步驟中的列出順序。

![新增對應以設定變數](assets/set_variable_addmappingnew.png)

### 設定變數——配置{#setvariable}

若要設定步驟，請編輯並使用下列標籤：

* [常見](/help/sites-developing/workflows-step-ref.md#step-properties-common-tab)
* **映射**

   * **選取變數：** 使用這個選項選取變數以設定其值。
   * **選擇映射模** 式：選擇映射模式以設定變數的值。視變數的資料類型而定，您可以使用下列選項來設定變數的值：

      * **常值：** 當您知道要指定的確切值時，請使用選項。
      * **運算式：** 當根據運算式計算要使用的值時，請使用此選項。表達式在提供的表達式編輯器中建立。
      * **JSON點符號：使** 用選項從JSON或FDM類型變數擷取值。
      * **XPATH：使** 用選項從XML類型變數中檢索值。
      * **相對於裝載：** 當要儲存至變數的值位於相對於裝載的路徑時，請使用此選項。
      * **絕對路徑：** 當要儲存至變數的值在絕對路徑上可用時，請使用此選項。
   * **指定值：** 指定要映射至變數的值。您在此欄位中指定的值取決於對應模式。
   * **新增對應：** 使用此選項新增更多對應，以設定變數的值。
