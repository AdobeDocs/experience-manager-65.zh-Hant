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

工作流模型由各種類型的一系列步驟組成。 根據類型，這些步驟可以設定並擴充為參數和指令碼，以提供您所需的功能和控制。

>[!NOTE]
>
>本節介紹標準工作流程步驟。
>
>如需模組專屬步驟，請參閱下列內容：
>
>* [AEM Forms工作流程步驟參考資料](/help/forms/using/aem-forms-workflow-step-reference.md)
>* [使用媒體處理常式和工作流程處理資產](/help/assets/media-handlers.md)
>


## 步驟屬性 {#step-properties}

每個步驟元件都有 **步驟屬性** 對話框，允許您定義和編輯所需屬性。

### 步驟屬性 — 常見頁簽 {#step-properties-common-tab}

下列屬性的組合適用於大部分的工作流程步驟元件，位於 **常見** 屬性對話框的頁簽：

* **標題**
步驟的標題。

* **說明**
步驟的說明。

* **工作流程分段**

   要套用 [階段](/help/sites-developing/workflows.md#workflow-stages) 到步驟。

* **逾時**

   步驟「逾時」的期間。
您可以選取： **關閉**, **立即**, **1小時**, **6小時**, **12小時**, **24小時**.

* **逾時處理常式**

   在步驟逾時時控制工作流程的處理常式。 例如 `Auto Advancer`

* **處理常式前進**

   選取此選項，即可在執行後自動將工作流程推進至下一個步驟。 如果未選取，實施指令碼必須處理工作流程進階。

### 步驟屬性 — 「用戶/組」頁簽 {#step-properties-user-group-tab}

下列屬性適用於許多工作流程步驟元件，位於 **使用者/群組** 屬性對話框的頁簽：

* **通過電子郵件通知用戶**

   * 當工作流程達到此步驟時，您可以傳送電子郵件通知參與者。
   * 如果已啟用，則會傳送電子郵件給屬性定義的使用者 **使用者/群組**，或群組的每個成員（若已定義群組）。

* **使用者/群組**

   * 下拉式選取方塊可讓您導覽至並選取使用者或群組。
   * 如果您將步驟指派給特定使用者，則只有此使用者可以對步驟採取行動。
   * 如果您將步驟指派給整個群組，則當工作流程達到此步驟時，此群組中的所有使用者都會在其中執行動作 **工作流程收件匣**.
   * 請參閱 [參與工作流程](/help/sites-authoring/workflows-participating.md) 以取得更多資訊。

## AND 拆分 {#and-split}

此 **和分割** 在工作流程中建立分割，之後兩個分支都處於作用中狀態。 您可以視需要將工作流程步驟新增至每個分支。 此步驟可讓您將多個處理路徑引入工作流程中。 例如，您可以允許同時執行某些審核步驟，節省時間。

![wf-26](assets/wf-26.png)

### 和分割 — 設定 {#and-split-configuration}

配置拆分：

* 編輯 **和分割屬性**:

   * **分割名稱**:為解釋性目的指定名稱
   * 選取所需的分支數；2、3、4或5。

* 視需要將工作流程步驟新增至分支。

   ![wf-27](assets/wf-27.png)

## 容器步驟 {#container-step}

容器步驟將啟動另一個作為子工作流執行的工作流模型。

此容器可讓您重複使用工作流模型，以實作常見的步驟順序。 例如，翻譯工作流程模型可用於多個編輯工作流程。

![wf-28](assets/wf-28.png)

### 容器步驟 — 配置 {#container-step-configuration}

若要設定此步驟，請編輯並使用下列標籤：

* [常見](#step-properties-common-tab)
* **容器**

   * **子工作流程**:選取要啟動的工作流程。

## 移至步驟 {#goto-step}

此 **轉至步驟** 可讓您指定在工作流程模型中執行的下一個步驟。 您可以指定規則定義、外部指令碼或ECMA指令碼作為路由表達式，以評估工作流模型的下一步。

* 如果您指定的條件為true，則 **轉至步驟** 完成，工作流程引擎會執行指定的步驟。
* 如果您指定的條件不保留true，則 **轉至步驟** 完成，且一般路由邏輯決定下一個要執行的步驟。

此 **轉至步驟** 使您能夠在工作流模型中實施高級路由結構。 例如，若要實作回圈， **轉至步驟** 可定義以在工作流中執行前一步驟，其中路由表達式評估循環條件。

### 轉到步驟 — 配置 {#goto-step-configuration}

若要設定此步驟，請編輯並使用下列標籤：

* [常見](#step-properties-common-tab)
* **程序**

   * **目標步驟**:選擇在評估路由表達式的條件後要執行的步驟。
   * **路由表達式**:選擇規則定義、外部指令碼或ECMA指令碼，以確定是否執行 **目標步驟**.

      * **規則定義：** 使用 [運算式編輯器](/help/forms/using/variable-in-aem-workflows.md#use-expression-editor) 來定義規則。
      * **外部指令碼：** 外部指令碼的路徑。
      * **ECMA指令碼**:決定是否執行 **轉至步驟**.

#### 模擬循環 {#simulating-a-for-loop}

模擬「for loop」需要您保持已發生循環迭代次數的計數：

* 計數通常代表在工作流程中處理之項目的索引。
* 計數會評估為回圈的退出准則。

例如，若要實作在數個JCR節點上執行動作的工作流程，您可以使用循環計數器作為節點的索引。 若要保留計數，請儲存 `integer` 值。 若要增加計數並比較計數與退出條件，請使用 **轉至步驟**.

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

您也可以使用「規則定義」(Rule Definition)作為路由表達式來模擬for循環。 [建立 **計數** 變數](/help/forms/using/variable-in-aem-workflows.md#create-a-variable) 長資料類型。 使用 **運算式** 作為 **[設定變數](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable)** 設定 **計數** 變數 **計數+ 1** 執行 **設定變數** 步驟。

![模擬for循環](assets/variable_use_case_count_new.png)

在 **轉至步驟**，使用 **設定變數** 作為 **目標步驟** 和 **計數&lt; 5** 作為路由表達式。

![模擬for循環的條件](assets/variable_use_case_count1_new.png)

此 **設定變數** 步驟會重複執行，遞增 **計數** 變數設為1，直到值達到5。

## OR 拆分 {#or-split}

此 **或分割** 在工作流程中建立分割，之後只有一個分支處於作用中狀態。 此步驟可讓您將條件式處理路徑引入工作流程中。 您可以視需要將工作流程步驟新增至每個分支。

>[!NOTE]
>
>請參閱 [或分割步驟](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/using-variables-in-aem-workflows.html?lang=en#use-a-variable)

![使用OR分割進行分支](assets/variables_orsplit_new.png)

### 或分割 — 配置 {#or-split-configuration}

配置拆分：

* 編輯 **或分割屬性**:

   * **常見**

      * 指定拆分名。
   * **分支(*x)***

      * **添加分支：** 新增更多分支至步驟。
      * **選擇路由表達式**:要評估活動分支，請選擇路由表達式。 可能的值包括：規則定義、外部指令碼和ECMA指令碼。
      * **按一下以新增運算式**:添加表達式以計算活動分支（如果選擇） **規則定義** 作為路由表達式。
      * **指令碼路徑**:包含指令碼的檔案路徑，用於評估活動分支（如果您選擇） **外部指令碼** 作為路由表達式。
      * **指令碼**:在方塊中新增指令碼，以評估您選取的作用中分支 **ECMA指令碼** 作為路由表達式。
      * **預設路由**:如果有多個分支，則會依循預設分支。 您只能指定一個分支作為預設值。

   >[!NOTE]
   >
   >    * 一次根據路由表達式計算一個分支。
   >    * 分支由上到下被評估。
   >    * 會執行評估為true的第一個指令碼。
   >    * 如果沒有分支評估為true，則工作流程不會前進。


   >[!NOTE]
   >
   >請參閱 [定義OR分割的規則](/help/sites-developing/workflows-models.md#defineruleecmascript).

* 視需要將工作流程步驟新增至分支。

## 參與者步驟和選擇器 {#participant-steps-and-choosers}

### 參與者步驟 {#participant-step}

A **參與者步驟** 可讓您為特定動作指派所有權。 只有當使用者已手動確認步驟時，工作流程才會進行。 當您希望某人對工作流程採取行動時，會使用此工作流程。 例如，檢閱步驟。

雖然與用戶授權不直接相關，但在分配操作時必須考慮用戶授權；使用者必須擁有工作流程裝載之頁面的存取權。

#### 參與者步驟 — 配置 {#participant-step-configuration}

若要設定此步驟，請編輯並使用下列標籤：

* [常見](#step-properties-common-tab)
* [使用者/群組](#step-properties-user-group-tab)

>[!NOTE]
>
>當發生下列情況時，一律會通知工作流發起程式：
>
>* 工作流程已完成（已完成）。
>* 工作流程已中止（終止）。
>


>[!NOTE]
>
>必須設定某些屬性才能啟用電子郵件通知。 您也可以自訂電子郵件範本，或為新語言新增電子郵件範本。 若要在AEM中設定電子郵件通知，請參閱 [設定電子郵件通知](/help/sites-administering/notification.md#configuringemailnotification).

### 對話方塊參與者步驟 {#dialog-participant-step}

使用 **對話參與者步驟** 從分配了工作項的用戶收集資訊。 此步驟對於收集稍後用於工作流程的少量資料非常有用。

完成此步驟後， **完成工作項** 對話方塊包含您在對話方塊中定義的欄位。 在欄位中收集的資料會儲存在工作流程裝載的節點中。 之後的工作流程步驟便可從存放庫讀取值。

要配置步驟，請指定要為其分配工作項的組或用戶以及對話框的路徑。

#### 對話參與者步驟 — 配置 {#dialog-participant-step-configuration}

若要設定此步驟，請編輯並使用下列標籤：

* [常見](#step-properties-common-tab)
* [使用者/群組](#step-properties-user-group-tab)
* **對話方塊**

   * **對話方塊路徑**:指向的對話框節點的路徑 [對話框](#dialog-participant-step-creating-a-dialog).

#### 對話參與者步驟 — 建立對話 {#dialog-participant-step-creating-a-dialog}

要建立對話框，必須建立對話框：

* 決定產生的資料位置 [儲存在有效負載中](#dialog-participant-step-storing-data-in-the-payload).
* [定義對話方塊；包括定義用於收集和儲存資料的欄位](#dialog-participant-step-dialog-definition).

#### 對話參與者步驟 — 在裝載中儲存資料 {#dialog-participant-step-storing-data-in-the-payload}

您可以在工作流程裝載或工作項元資料中儲存介面工具集資料。 格式 `name` widget節點的屬性決定資料的儲存位置。

* **使用裝載儲存資料**

   * 若要將Widget資料儲存為工作流程裝載的屬性，請對Widget節點的name屬性值使用以下格式：
      `./jcr:content/nodename`

   * 資料會儲存在 `nodename` 裝載節點的屬性。 如果節點不包含該屬性，則會建立屬性。
   * 與裝載一併儲存時，後續使用具有相同裝載的對話方塊會覆寫屬性的值。

* **將資料與工作項一起儲存**

   * 要將Widget資料儲存為工作項元資料的屬性，請對name屬性的值使用以下格式：
      `nodename`

   * 資料會儲存在 `nodename` 工作項的屬性 `metadata`. 如果對話方塊稍後會搭配相同的裝載使用，則會保留資料。

#### 對話參與者步驟 — 對話定義 {#dialog-participant-step-dialog-definition}

1. **對話框結構**

   對話框參與者步驟對話框與為創作元件建立的對話框類似。 它們儲存在：

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
   >請參閱 [建立和設定對話方塊](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog).

1. **對話框路徑屬性**

   此 **對話參與者步驟** 有 **對話方塊路徑** 屬性(連同 [參與者步驟](#participant-step))。 的值 **對話方塊路徑** 屬性是 `dialog` 對話框的節點。

   例如，對話方塊包含在名為 `EmailWatch` 儲存在節點中的：

   `/apps/myapp/workflows/dialogs`

   對於觸控式UI，會使用下列值 **對話方塊路徑** 屬性：

   `/apps/myapp/workflow/dialogs/EmailWatch/cq:dialog`

   ![wf-30](assets/wf-30.png)

1. **示例對話框定義**

   以下XML代碼片段代表一個對話框，用於儲存 `String` 值 `watchEmail` 裝載內容的節點。 標題節點代表 [TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/textfield/index.html) 元件：

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

   在觸控式UI中，此範例會產生下列對話方塊：

   ![chlimage_1-70](assets/chlimage_1-70.png)

### 動態參與者步驟 {#dynamic-participant-step}

此 **動態參與者步驟** 元件類似於 **[參與者步驟](#participant-step)** 在運行時自動選擇參與者的差異。

若要設定步驟，請選取 **參與者選擇器** 標識要將工作項指派給的參與者，以及對話框。

#### 動態參與者步驟 — 配置 {#dynamic-participant-step-configuration}

若要設定此步驟，請編輯並使用下列標籤：

* [常見](#step-properties-common-tab)
* **參與者選擇器**

   * **參與者選擇器**:的名稱 [參與者選擇器](#developingtheparticipantchooser).
   * **引數**:任何必要引數。
   * **電子郵件**:是否應將電子郵件通知傳送給使用者。

* **對話方塊**

   * **對話方塊路徑**:指向的對話框節點的路徑 [建立的對話方塊(如 **對話參與者步驟**)](#dialog-participant-step-creating-a-dialog).

#### 動態參與者步驟 — 開發參與者選擇器 {#dynamic-participant-step-developing-the-participant-chooser}

建立參與者選擇器。 因此，您可以使用任何選擇邏輯或條件。 例如，您的參與者選擇器可以選擇工作項目最少的用戶（在組內）。 您可以建立任意數量的參與者選擇器，以用於 **動態參與者步驟** 元件。

建立OSGi服務或ECMAScript，以選擇用戶將工作項指派給它。

* **ECMAscript**

   指令碼必須包含名為getParticipant的函式，該函式將用戶ID作為 `String` 值。 將自訂指令碼儲存在，例如 `/apps/myapp/workflow/scripts` 或子資料夾。

   標準AEM例項中包含範例指令碼：

   `/libs/workflow/scripts/initiator-participant-chooser.ecma`

   >[!CAUTION]
   >
   >請勿變更 `/libs` 路徑。
   >
   >
   >原因在於 `/libs` 會在您下次升級執行個體時覆寫（當您套用Hotfix或Feature Pack時，則會覆寫）。

   此指令碼選擇工作流啟動器作為參與者：

   ```
   function getParticipant() {
       return workItem.getWorkflow().getInitiator();
   }
   ```

   >[!NOTE]
   >
   >此 **工作流啟動器參與者選擇器** 元件延伸 **動態參與者步驟** 並將此指令碼作為步驟實施。

* **OSGi服務**

   服務必須實作 [com.day.cq.workflow.exec.ParticipantStepChooser](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/workflow/exec/ParticipantStepChooser.html) 介面。 介面定義以下成員：

   * `SERVICE_PROPERTY_LABEL` 欄位：使用此欄位指定參與者選擇器的名稱。 該名稱將出現在 **動態參與者步驟** 屬性。

   * `getParticipant` 方法：以 `String` 值。
   >[!CAUTION]
   >
   >此 `getParticipant` 方法會傳回動態解析的主體id。 此id可以是群組id或使用者id。
   >
   >
   >不過，群組ID只能用於 **參與者步驟**，則返回參與者清單。 若 **動態參與者步驟**，則會傳回空白清單，且無法用於委派。

   讓實施可供使用 **動態參與者步驟** 元件，將您的Java™類添加到導出服務的OSGi捆綁包中，然後將捆綁包部署到AEM伺服器。

   >[!NOTE]
   >
   >**隨機參與者選擇器** 是選取隨機使用者( `com.day.cq.workflow.impl.process.RandomParticipantChooser`)。 此 **隨機參與者選擇** r步驟元件樣本擴展 **動態參與者步驟** 並將此服務作為步驟實施。

#### 動態參與者步驟 — 參與者選擇器服務示例 {#dynamic-participant-step-example-participant-chooser-service}

以下Java™類實現 `ParticipantStepChooser` 介面。 類返回啟動工作流的參與者的名稱。 程式碼使用與範例指令碼(`initiator-participant-chooser.ecma`)使用。

此 `@Property` 注釋設定 `SERVICE_PROPERTY_LABEL` 欄位至 `Workflow Initiator Participant Chooser`.

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

在 **動態參與者步驟** 屬性對話框， **參與者選擇器** 清單包含項目 `Workflow Initiator Participant Chooser (script)`，代表此服務。

啟動工作流模型時，日誌指示啟動工作流的用戶的ID以及為其分配了工作項的用戶。 在此範例中， `admin` 使用者已啟動工作流程。

`13.09.2015 15:48:53.037 *INFO* [10.176.129.223 [1347565733037] POST /etc/workflow/instances HTTP/1.1] com.adobe.example.InitiatorParticipantChooser Assigning Dynamic Participant Step work item to admin`

### 表單參與者步驟 {#form-participant-step}

此 **表單參與者步驟** 在開啟工作項時顯示表單。 當用戶填寫並提交表單時，欄位資料儲存在工作流裝載的節點中。

要配置步驟，請指定要為其分配工作項的組或用戶以及表單的路徑。

>[!CAUTION]
>
>本節內容為 [頁面製作的Foundation元件的Forms區段](/help/sites-authoring/default-components-foundation.md#form).

#### 表單參與者步驟 — 配置 {#form-participant-step-configuration}

若要設定此步驟，請編輯並使用下列標籤：

* [常見](#step-properties-common-tab)
* [使用者/群組](#step-properties-user-group-tab)
* **表單**

   * **表單路徑**:路徑 [建立的表單](#form-participant-step-creating-the-form).

#### 表單參與者步驟 — 建立表單 {#form-participant-step-creating-the-form}

建立表單以與 **表單參與者步驟** 正常。 但是，表單參與者步驟的表單必須有下列配置：

* 此 **表單開始** 元件必須具有 **動作類型** 屬性設定為 `Edit Workflow Controlled Resource(s)`.
* 此 **表單開始** 元件必須具有 `Form Identifier` 屬性。
* 表單元件必須具有 **元素名稱** 屬性設定為儲存欄位資料的節點的路徑。 路徑必須在工作流程裝載內容中找到節點。 值使用下列格式：

   `./jcr:content/path_to_node`

* 表單必須包含 **工作流提交按鈕** 元件。 不配置元件的任何屬性。

工作流程的需求決定您應將欄位資料儲存於何處。 例如，欄位資料可用來設定頁面內容的屬性。 下列值 **元素名稱** 屬性會儲存欄位資料，作為 `redirectTarget` 屬性 `jcr:content` 節點：

`./jcr:content/redirectTarget`

在下列範例中，欄位資料是 **文字** 裝載頁面上的元件：

`./jcr:content/par/text_3/text`

第一個範例可用於 `cq:Page` 元件呈現。 第二個範例僅可在裝載頁面包含 **文字** ID為的元件 `text_3`.

表單可以位於儲存庫中的任意位置，但工作流用戶必須獲得讀取表單的授權。

### 隨機參與者選擇器 {#random-participant-chooser}

此 **隨機參與者選擇器** 步驟是參與者選擇器，它將生成的工作項分配給從清單中隨機選擇的用戶。

![wf-31](assets/wf-31.png)

#### 隨機參與者選擇器 — 配置 {#random-participant-chooser-configuration}

若要設定此步驟，請編輯並使用下列標籤：

* [常見](#step-properties-common-tab)
* **引數**

   * **參與者**:指定可供選擇的用戶清單。 若要將使用者新增至清單，請按一下 **新增項目** 並輸入用戶節點或用戶ID的首頁路徑。 用戶的順序不會影響被分配工作項目的可能性。

### 工作流程發起人參與者選擇器 {#workflow-initiator-participant-chooser}

此 **工作流啟動器參與者選擇器** 步驟是參與者選擇器，它將生成的工作項分配給啟動工作流的用戶。 除了 **常見** 屬性。

#### 工作流啟動器參與者選擇器 — 配置 {#workflow-initiator-participant-chooser-configuration}

若要設定此步驟，請使用下列標籤進行編輯：

* [常見](#step-properties-common-tab)

## 程序步驟 {#process-step}

A **處理步驟** 執行ECMAScript或呼叫OSGi服務以執行自動處理。

![wf-32](assets/wf-32.png)

### 處理步驟 — 配置 {#process-step-configuration}

若要設定此步驟，請編輯並使用下列標籤：

* [常見](#step-properties-common-tab)
* **程序**

   * **程式**:要執行的程式實作。 使用下拉菜單選擇ECMAScript或OSGi服務。 關於後述資訊：:

      * 標準ECMAScript和OSGi服務，請參見 [用於流程步驟的內置流程](/help/sites-developing/workflows-process-ref.md).
      * 為流程步驟建立ECMAScript，請參閱 [使用ECMAScript實作處理步驟](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript).
      * 建立「處理」步驟的OSGi服務，請參閱 [使用Java™類實施處理步驟](/help/sites-developing/workflows-customizing-extending.md#implementing-a-process-step-with-a-java-class).
   * **處理常式進階**:選取此選項，即可在執行後自動將工作流程推進至下一個步驟。 如果未選取，實施指令碼必須處理工作流程進階。
   * **引數**:要傳遞至此進程的參數。


## 設定變數 {#set-variable}

「設定變數」步驟可讓您設定變數的值，並定義值的設定順序。 變數的設定順序為「設定變數」步驟中列出變數對應的順序。

![新增對應以設定變數](assets/set_variable_addmappingnew.png)

### 設定變數 — 設定 {#setvariable}

若要設定此步驟，請編輯並使用下列標籤：

* [常見](/help/sites-developing/workflows-step-ref.md#step-properties-common-tab)
* **映射**

   * **選取變數：** 使用此選項可選取變數以設定其值。
   * **選擇映射模式：**  若要設定變數的值，請選取對應模式。 根據變數的資料類型，您可以使用下列選項來設定變數的值：

      * **常值：** 當您知道要指定的確切值時，請使用選項。
      * **運算式：** 根據運算式計算要使用的值時，請使用選項。 運算式是在提供的運算式編輯器中建立。
      * **JSON點記號：** 使用選項可從JSON或FDM類型變數擷取值。
      * **XPATH:** 使用選項可從XML類型變數中檢索值。
      * **相對於裝載：** 當要儲存至變數的值在與裝載相關的路徑上可用時，請使用選項。
      * **絕對路徑：** 當要儲存至變數的值在絕對路徑上可用時，請使用選項。
   * **指定值：** 若要對應至變數，請指定值。 您在此欄位中指定的值取決於對應模式。
   * **添加映射：** 使用此選項可新增更多對應以設定變數的值。
