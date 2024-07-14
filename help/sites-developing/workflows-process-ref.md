---
title: 工作流程處理序參考
description: 請參閱此程式參考資料，瞭解Adobe Experience Manager中的工作流程。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: a9de8ec6-6948-4643-89c3-62d9b1f6293a
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 1%

---

# 工作流程處理序參考{#workflow-process-reference}

AEM提供了幾個可用於建立工作流程模型的流程步驟。 您也可以為內建步驟未涵蓋的任務新增自訂程式步驟（請參閱[建立工作流程模型](/help/sites-developing/workflows-models.md)）。

## 程式特性 {#process-characteristics}

對於每個處理步驟，將說明下列特性。

### Java™類別或ECMA路徑 {#java-class-or-ecma-path}

處理步驟是由Java™類別或ECMAScript所定義。

* 對於Java™類別處理程式，會提供完整類別名稱。
* 對於ECMAScript程式，會提供指令碼的路徑。

### 總額 {#payload}

裝載是工作流程例項作用所在的實體。 裝載是由啟動工作流程執行個體的內容隱含選取。

例如，如果工作流程套用至AEM頁面&#x200B;*P*，則工作流程進行時會在不同步驟之間傳遞&#x200B;*P*，每個步驟會以某種方式選擇性地對&#x200B;*P*&#x200B;執行動作。

在最常見的情況下，有效負載是存放庫中的JCR節點(例如AEM頁面或資產)。 JCR節點承載會以字串形式傳遞，且是JCR路徑或JCR識別碼(UUID)。 有時有效負載可能是JCR屬性（作為JCR路徑傳遞）、URL、二進位物件或通用Java™物件。 對裝載採取動作的個別程式步驟通常會預期某種型別的裝載，或根據裝載型別採取不同的動作。 對於下述每個程式，都會說明預期的裝載型別（若有）。

### 引數 {#arguments}

有些工作流程處理會接受管理員在設定工作流程步驟時指定的引數。

在工作流程編輯器的&#x200B;**屬性**&#x200B;窗格中的&#x200B;**處理序引數**&#x200B;屬性中，以單一字串的形式輸入引數。 對於下述的每個程式，引數字串的格式都以簡單的EBNF文法加以說明。 例如，下列表示引數字串包含一或多個以逗號分隔的引數對，其中每一對都包含名稱（即字串）和值（以雙冒號分隔）：

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### 逾時 {#timeout}

在此逾時期間後，工作流程步驟不再運作。 有些工作流程會遵循逾時，有些則不適用並被忽略。

### 權限 {#permissions}

傳遞至`WorkflowProcess`的工作階段由工作流程服務的服務使用者提供支援，其在存放庫的根目錄擁有下列許可權：

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

如果該組許可權不足以進行您的`WorkflowProcess`實作，則它必須使用具有必要許可權的工作階段。

建議方法是使用以必要但最小許可權子集建立的服務使用者。

>[!CAUTION]
>
>如果您從AEM 6.2之前的版本升級，您可能需要更新實作。
>
>在舊版中，管理員工作階段會傳遞至`WorkflowProcess`實作，然後可以完全存取存放庫，而不必定義特定ACL。
>
>這些許可權現在定義如上（[許可權](#permissions)）。 更新實作的建議方法為。
>
>若無法進行程式碼變更，短期解決方案也可用於回溯相容性：
>
>* 使用Web主控台( `/system/console/configMgr`找到&#x200B;**AdobeGranite工作流程組態服務**
>
>* 啟用&#x200B;**工作流程舊模式**
>
>這回覆成為`WorkflowProcess`實作提供管理員工作階段的舊行為，並再次提供整個存放庫的不受限制存取權。

## 工作流程控制程式 {#workflow-control-processes}

下列程式不會對內容執行任何動作。 它們用於控制工作流程本身的行為。

### AbsoluteTimeAutoAdvancer （絕對時間自動提前器） {#absolutetimeautoadvancer-absolute-time-auto-advancer}

`AbsoluteTimeAutoAdvancer` （絕對時間自動提前器）處理序的行為與&#x200B;**自動提前器**&#x200B;相同，唯一例外是在指定的時間和日期逾時，而不是在指定的時間長度之後。

* **Java™類別**： `com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **承載**：無。
* **引數**：無。
* **逾時**：達到設定的時間和日期時，處理序逾時。

### 自動提前器（自動提前器） {#autoadvancer-auto-advancer}

`AutoAdvancer`程式會自動將工作流程推進到下一個步驟。 如果有多個可能的下一步（例如，如果有OR分割），則此程式將沿著&#x200B;*預設路由*&#x200B;推進工作流程（如果已指定），否則將不會推進工作流程。

* **Java™類別**： `com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **承載**：無。
* **引數**：無。
* **逾時**：處理序在設定時間長度後逾時。

### ProcessAssembler （程式組合器） {#processassembler-process-assembler}

`ProcessAssembler`處理序會在單一工作流程步驟中依序執行多個子處理序。 若要使用`ProcessAssembler`，請在工作流程中建立此型別的單一步驟，並設定其引數以指出您要執行的子處理程式的名稱和引數。

* **Java™類別**： `com.day.cq.workflow.impl.process.ProcessAssembler`

* **裝載**： DAM資產、AEM頁面或無裝載（取決於子程式的需求）。
* **引數**：

```
        args := arg [',' arg]
        arg := processname ['::' processargs]
        processname := /* A fully qualified Java Class or absolute
        repository path to an ECMAScript */
        processargs := processarg [';' processarg]*
        processarg := '[' nobracketprocessarg ']' | nobracketprocessarg
        nobracketprocessarg := listitem [':' listitem]*
        listitem := /* A string */
```

* **逾時**：已遵守。

例如：

* 從資產中擷取中繼資料。
* 建立三種指定大小的縮圖。
* 假設資產原本不是JPEG或PNG (在此情況下不會建立GIF)，從資產建立JPEG影像。
* 設定資產的上次修改日期。

```shell
com.day.cq.dam.core.process.ExtractMetadataProcess,
    com.day.cq.dam.core.process.CreateThumbnailProcess::[140:100];[48:48];[319:319:false],
    com.day.cq.dam.core.process.CreateWebEnabledImageProcess::dimension:1280:1280;mimetype:image/jpeg,
    com.day.cq.dam.core.process.AssetSetLastModifiedProcess
```

## 基本流程 {#basic-processes}

下列程式會執行簡單工作或作為範例。

>[!CAUTION]
>
>請勿變更`/libs`路徑中的任何專案。
>
>這是因為下次升級執行個體時，`/libs`的內容會被覆寫（當您套用Hotfix或Feature Pack時，可能會遭到覆寫）。

### 刪除 {#delete}

指定路徑的專案即被刪除。

* **ECMAScript路徑**： `/libs/workflow/scripts/delete.ecma`

* **承載**： JCR路徑
* **引數**：無
* **逾時**：已忽略

### 空位 {#noop}

這是Null程式。 它不執行任何操作，但會記錄偵錯訊息。

* **ECMAScript路徑**： `/libs/workflow/scripts/noop.ecma`

* **承載**：無
* **引數**：無
* **逾時**：已忽略

### rule-false {#rule-false}

這是Null處理序，在`check()`方法上傳回`false`。

* **ECMAScript路徑**： `/libs/workflow/scripts/rule-false.ecma`

* **承載**：無
* **引數**：無
* **逾時**：已忽略

### 範例 {#sample}

這是ECMAScript程式的範例。

* **ECMAScript路徑**： `/libs/workflow/scripts/sample.ecma`

* **承載**：無
* **引數**：無
* **逾時**：已忽略

### 鎖定程式 {#lockprocess}

鎖定工作流程的裝載。

* **Java™類別：** `com.day.cq.workflow.impl.process.LockProcess`

* **承載：** JCR_PATH和JCR_UUID
* **引數：**&#x200B;無
* **逾時：**&#x200B;已忽略

此步驟在下列情況下不會產生任何影響：

* 承載已鎖定
* 裝載節點不包含jcr：content子節點

### UnlockProcess {#unlockprocess}

解鎖工作流程的裝載。

* **Java™類別：** `com.day.cq.workflow.impl.process.UnlockProcess`

* **承載：** JCR_PATH和JCR_UUID
* **引數：**&#x200B;無
* **逾時：**&#x200B;已忽略

此步驟在下列情況下不會產生任何影響：

* 承載已解鎖
* 裝載節點不包含jcr：content子節點

## 版本設定流程 {#versioning-processes}

下列程式會執行版本相關工作。

### CreateVersionProcess {#createversionprocess}

建立工作流程裝載(AEM頁面或DAM資產)的版本。

* **Java™類別**： `com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **裝載**：參考頁面或DAM資產的JCR路徑或UUID
* **引數**：無
* **逾時**：已遵守
