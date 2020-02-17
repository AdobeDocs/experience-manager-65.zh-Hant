---
title: 工作流進程參考
seo-title: 工作流進程參考
description: 'null'
seo-description: 'null'
uuid: de367aa8-4580-4810-b665-2a7b521e36ca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: dbdf981f-791b-4ff7-8ca8-039d0bdc9c92
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 工作流進程參考{#workflow-process-reference}

AEM提供數個可用來建立工作流程模型的流程步驟。 您也可以針對內建步驟未涵蓋的工作新增自訂流程步驟(請參 [閱建立工作流程模型](/help/sites-developing/workflows-models.md))。

## 流程特性 {#process-characteristics}

對於每個過程步驟，描述了以下特性。

### Java類或ECMA路徑 {#java-class-or-ecma-path}

流程步驟由Java類或ECMAScript定義。

* 對於Java類進程，提供完全限定的類名。
* 對於ECMAScript處理指令碼的路徑。

### 裝載 {#payload}

裝載是工作流實例所依據的實體。 裝載由啟動工作流實例的上下文隱式選擇。

例如，如果工作流程套用至AEM頁面 *P* ，則 *P* 會隨著工作流程的進行，逐步傳遞，每個步驟都可選擇以某種方式對 ** P執行。

在最常見的情況下，裝載是儲存庫中的JCR節點（例如AEM頁面或資產）。 JCR節點裝載作為字串傳遞，該字串是JCR路徑或JCR標識符(UUID)。 在某些情況下，裝載可能是JCR屬性（以JCR路徑傳遞）、URL、二進位物件或一般Java物件。 實際作用於裝載的個別處理步驟通常會預期某種類型的裝載，或根據裝載類型採取不同的作用。 對於下面描述的每個過程，將說明預期的裝載類型（如果有）。

### 引數 {#arguments}

某些工作流進程接受管理員在設定工作流步驟時指定的參數。

在工作流編輯器的「屬性」窗格的 **「流程參數** 」屬性中，將參數作為單 **** 一字串輸入。 對於下面描述的每個過程，參數字串的格式以簡單的EBNF語法進行描述。 例如，以下指示引數字串由一個或多個逗號分隔的對組成，其中每對都由名稱（即字串）和值（以雙冒號分隔）組成：

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### 逾時 {#timeout}

在此逾時期間後，工作流程步驟便不再運作。 有些工作流程程式會遵守逾時，而有些則不適用，因此會被忽略。

### 權限 {#permissions}

傳遞給的會話由 `WorkflowProcess` 工作流進程服務的服務用戶支援，該服務用戶在儲存庫的根目錄中具有以下權限：

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

如果這組權限對您的實作不足 `WorkflowProcess` 夠，則必須使用具有所需權限的作業。

建議的方法是使用使用使用所需權限子集（但最小）建立的服務用戶。

>[!CAUTION]
>
>如果您是從AEM 6.2之前的版本升級，您可能需要更新實作。
>
>在舊版中，管理會話會傳遞給實 `WorkflowProcess` 施，然後可以完全訪問儲存庫，而無需定義特定ACL。
>
>權限現在已定義為上述([權限](#permissions))。 建議的實作更新方法亦同。
>
>當程式碼變更不可行時，短期解決方案也可用於回溯相容性的目的：
>
>* 使用Web Console(找 `/system/console/configMgr` 到 **Adobe Granite Workflow Configuration Service**
   >
   >
* 啟用工作 **流程舊模式**
>
>
這將回復為向實施提供管理會話的舊行為，並 `WorkflowProcess` 再次提供對整個儲存庫的無限制訪問。

## 工作流程控製程式 {#workflow-control-processes}

下列程式不會對內容執行任何動作。 它們可用來控制工作流程本身的行為。

### AbsoluteTimeAutoAdvancer (Absolute Time Auto Advancer) {#absolutetimeautoadvancer-absolute-time-auto-advancer}

(絕 `AbsoluteTimeAutoAdvancer` 對時間自動提前器)流程的行為與 **** AutoAdvancer相同，只不過它在指定的時間和日期超時，而不是在指定的時間長度之後。

* **Java類**: `com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **裝載**:沒有。
* **引數**:沒有。
* **逾時**:到達設定的時間和日期時，處理超時。

### AutoAdvancer(Auto Advancer) {#autoadvancer-auto-advancer}

此程 `AutoAdvancer` 序會自動將工作流程推進至下一步。 如果有多個可能的下一步（例如，如果存在OR拆分），則此流程將沿預設路由(如果已指定 *路由*)推進工作流，否則工作流將不進行高級。

* **Java類**: `com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **裝載**:沒有。
* **引數**:沒有。
* **逾時**:在設定的時間長度後，處理逾時。

### ProcessAssembler(Process Assembler) {#processassembler-process-assembler}

該 `ProcessAssembler` 進程在單個工作流步驟中按順序執行多個子進程。 要使用 `ProcessAssembler`，請在工作流中建立此類型的單個步驟，並設定其參數以指明要執行的子進程的名稱和參數。

* **Java類**: `com.day.cq.workflow.impl.process.ProcessAssembler`

* **裝載**:DAM資產、AEM頁面或無裝載（視子程式需求而定）。
* **引數**:

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

* **逾時**:受尊敬。

例如：

* 從資產擷取中繼資料。
* 建立3種指定大小的縮圖。
* 從資產建立JPEG影像，假設資產原本不是GIF或PNG（在這種情況下不會建立JPEG）。
* 在資產上設定上次修改的日期。

```shell
com.day.cq.dam.core.process.ExtractMetadataProcess,
    com.day.cq.dam.core.process.CreateThumbnailProcess::[140:100];[48:48];[319:319:false],
    com.day.cq.dam.core.process.CreateWebEnabledImageProcess::dimension:1280:1280;mimetype:image/jpeg,
    com.day.cq.dam.core.process.AssetSetLastModifiedProcess
```

## 基本流程 {#basic-processes}

下列程式會執行簡單工作或做為範例。

>[!CAUTION]
>
>您 ***不得*** 更改路徑中的任 `/libs` 何內容。
>
>這是因為下次升級 `/libs` 實例時會覆寫的內容（套用修補程式或功能套件時可能會覆寫）。

### 刪除 {#delete}

指定路徑上的項目即會刪除。

* **ECMAScript路徑**: `/libs/workflow/scripts/delete.ecma`

* **裝載**:JCR路徑
* **引數**:無
* **逾時**:已忽略

### noop {#noop}

這是空進程。 它不執行任何操作，但會記錄調試消息。

* **ECMAScript路徑**: `/libs/workflow/scripts/noop.ecma`

* **裝載**:無
* **引數**:無
* **逾時**:已忽略

### rule-false {#rule-false}

這是在方法上返回的 `false` 空進 `check()` 程。

* **ECMAScript路徑**: `/libs/workflow/scripts/rule-false.ecma`

* **裝載**:無
* **引數**:無
* **逾時**:已忽略

### sample {#sample}

這是ECMAScript程式示例。

* **ECMAScript路徑**: `/libs/workflow/scripts/sample.ecma`

* **裝載**:無
* **引數**:無
* **逾時**:已忽略

### urller {#urlcaller}

這是呼叫指定URL的簡單工作流程程式。 通常，URL將是執行簡單任務的JSP（或其它等效servlet）的引用。 此程式僅應用於開發和展示，而不應用於生產環境。 引數指定URL、登入和密碼。

* **ECMAScript路徑**: `/libs/workflow/scripts/urlcaller.ecma`

* **裝載**:無
* **引數**:

```
        args := url [',' login ',' password]
        url := /* The URL to be called */
        login := /* The login to access the URL */
        password := /* The password to access the URL */
```

例如： `http://localhost:4502/my.jsp, mylogin, mypassword`

* **逾時**:已忽略

### LockProcess {#lockprocess}

鎖定工作流的裝載。

* **** Java類： `com.day.cq.workflow.impl.process.LockProcess`

* **** 裝載：JCR_PATH和JCR_UUID
* **** 引數：無
* **** 逾時：已忽略

在下列情況下，該步驟不具效力：

* 裝載已鎖定
* 裝載節點不包含jcr:content子節點

### UnlockProcess {#unlockprocess}

解除鎖定工作流程的裝載。

* **** Java類： `com.day.cq.workflow.impl.process.UnlockProcess`

* **** 裝載：JCR_PATH和JCR_UUID
* **** 引數：無
* **** 逾時：已忽略

在下列情況下，該步驟不具效力：

* 裝載已解除鎖定
* 裝載節點不包含jcr:content子節點

## 版本修訂程式 {#versioning-processes}

以下進程將執行與版本相關的任務。

### CreateVersionProcess {#createversionprocess}

建立工作流程裝載的新版本（AEM頁面或DAM資產）。

* **Java類**: `com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **裝載**:參照頁面或DAM資產的JCR路徑或UUID
* **引數**:無
* **逾時**:受尊重

