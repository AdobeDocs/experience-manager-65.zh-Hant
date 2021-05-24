---
title: 工作流程處理序參考
seo-title: 工作流程處理序參考
description: 工作流程處理序參考
seo-description: 'null'
uuid: de367aa8-4580-4810-b665-2a7b521e36ca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: dbdf981f-791b-4ff7-8ca8-039d0bdc9c92
exl-id: a9de8ec6-6948-4643-89c3-62d9b1f6293a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 2%

---

# 工作流程處理序參考{#workflow-process-reference}

AEM提供可用於建立工作流程模型的數個處理步驟。 也可以針對內建步驟未涵蓋的任務新增自訂流程步驟（請參閱[建立工作流模型](/help/sites-developing/workflows-models.md)）。

## 進程特性{#process-characteristics}

對於每個過程步驟，描述了以下特性。

### Java類或ECMA路徑{#java-class-or-ecma-path}

處理步驟由Java類或ECMAScript定義。

* 對於Java類進程，提供完全限定的類名。
* 對於ECMAScript，會提供指令碼的路徑。

### 裝載 {#payload}

有效負載是工作流程例項據以運作的實體。 裝載由啟動工作流實例的上下文隱式選擇。

例如，如果將工作流應用到AEM頁面&#x200B;*P*，則隨著工作流的前進，會逐步傳遞&#x200B;*P*，每個步驟可選地以某種方式作用於&#x200B;*P*。

在最常見的情況下，裝載是存放庫中的JCR節點(例如AEM頁面或資產)。 JCR節點裝載會以字串的形式傳遞，該字串是JCR路徑或JCR識別碼(UUID)。 在某些情況下，裝載可能是JCR屬性（以JCR路徑傳遞）、URL、二進位物件或一般Java物件。 對有效負載採取行動的個別處理步驟通常會預期特定類型的有效負載，或根據有效負載類型採取不同的行動。 對於下面描述的每個過程，將說明預期的有效負載類型（如果有）。

### 引數 {#arguments}

某些工作流進程接受管理員在設定工作流步驟時指定的參數。

在工作流編輯器的&#x200B;**屬性**&#x200B;窗格的&#x200B;**處理參數**&#x200B;屬性中，參數作為單個字串輸入。 對於下面描述的每個過程，參數字串的格式以簡單的EBNF文法描述。 例如，以下指示參數字串由一個或多個逗號分隔對組成，其中每對都由名稱（即字串）和值組成，由雙冒號分隔：

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### 逾時 {#timeout}

在此逾時期間後，工作流程步驟便不再運作。 有些工作流程程式會遵守逾時，有些則不適用，且會忽略。

### 權限 {#permissions}

傳遞給`WorkflowProcess`的會話由工作流進程服務的服務用戶支援，該服務在儲存庫的根目錄中具有以下權限：

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

如果這組權限不足以供您的`WorkflowProcess`實作使用，則必須使用具有必要權限的工作階段。

建議的做法是使用使用使用所需權限子集（但最少）建立的服務使用者。

>[!CAUTION]
>
>如果您從AEM 6.2之前的版本升級，則可能需要更新實作。
>
>在舊版中，管理工作階段會傳遞至`WorkflowProcess`實作，然後即可完整存取存放庫，而無須定義特定ACL。
>
>權限現在定義如上([Permissions](#permissions))。 更新實作的建議方法亦同。
>
>當程式碼變更不可行時，也提供短期解決方案供回溯相容用途：
>
>* 使用Web控制台(`/system/console/configMgr`)查找&#x200B;**AdobeGranite工作流配置服務**
   >
   >
* 啟用&#x200B;**工作流進程舊模式**
>
>
這會回復為向`WorkflowProcess`實作提供管理員工作階段的舊行為，並再次提供對存放庫整體的無限制存取。

## 工作流控制進程{#workflow-control-processes}

下列程式不會對內容執行任何動作。 它們可用來控制工作流程本身的行為。

### AbsoluteTimeAutoAdvancer（絕對時間自動提前器）{#absolutetimeautoadvancer-absolute-time-auto-advancer}

`AbsoluteTimeAutoAdvancer`（絕對時間自動提前器）進程的行為與&#x200B;**AutoAdvancer**&#x200B;相同，只是它在指定的時間和日期超時，而不是在指定的時間長度之後。

* **Java類**:  `com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **裝載**:無。
* **引數**:無。
* **逾時**:達到設定的時間和日期時，處理會逾時。

### AutoAdvancer(Auto Advancer){#autoadvancer-auto-advancer}

`AutoAdvancer`進程會自動將工作流推進到下一步。 如果有多個可能的下一步（例如，如果存在OR拆分），則此進程將沿&#x200B;*預設路由*&#x200B;推進工作流，如果已指定，則不進行工作流。

* **Java類**:  `com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **裝載**:無。
* **引數**:無。
* **逾時**:在設定的時間長度後處理超時。

### ProcessAssembler(Process Assembler){#processassembler-process-assembler}

`ProcessAssembler`進程在單個工作流步驟中按順序執行多個子進程。 要使用`ProcessAssembler`，請在工作流中建立此類型的單個步驟，並設定其參數以指示要執行的子進程的名稱和參數。

* **Java類**:  `com.day.cq.workflow.impl.process.ProcessAssembler`

* **裝載**:DAM資產、AEM頁面或無裝載（視子程式的需求而定）。
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

* **逾時**:尊重。

例如：

* 從資產中擷取中繼資料。
* 建立三個指定大小的縮圖。
* 假設資產原本既不是GIF也不是PNG，則從資產建立JPEG影像（在這種情況下不會建立JPEG）。
* 在資產上設定上次修改的日期。

```shell
com.day.cq.dam.core.process.ExtractMetadataProcess,
    com.day.cq.dam.core.process.CreateThumbnailProcess::[140:100];[48:48];[319:319:false],
    com.day.cq.dam.core.process.CreateWebEnabledImageProcess::dimension:1280:1280;mimetype:image/jpeg,
    com.day.cq.dam.core.process.AssetSetLastModifiedProcess
```

## 基本進程{#basic-processes}

下列程式會執行簡單工作或做為範例。

>[!CAUTION]
>
>您&#x200B;***必須***&#x200B;不要變更`/libs`路徑中的任何項目。
>
>這是因為下次升級執行個體時會覆寫`/libs`的內容（當您套用Hotfix或Feature Pack時，則會覆寫）。

### 刪除 {#delete}

會刪除指定路徑上的項目。

* **ECMAScript路徑**:  `/libs/workflow/scripts/delete.ecma`

* **裝載**:JCR路徑
* **引數**:無
* **逾時**:已忽略

### noop {#noop}

這是Null進程。 它不會執行任何操作，但會記錄除錯訊息。

* **ECMAScript路徑**:  `/libs/workflow/scripts/noop.ecma`

* **裝載**:無
* **引數**:無
* **逾時**:已忽略

### rule-false {#rule-false}

這是在`check()`方法上傳回`false`的空進程。

* **ECMAScript路徑**:  `/libs/workflow/scripts/rule-false.ecma`

* **裝載**:無
* **引數**:無
* **逾時**:已忽略

### 範例 {#sample}

這是ECMAScript程式的範例。

* **ECMAScript路徑**:  `/libs/workflow/scripts/sample.ecma`

* **裝載**:無
* **引數**:無
* **逾時**:已忽略

### urlcaller {#urlcaller}

這是呼叫指定URL的簡單工作流程程式。 通常，URL將是執行簡單任務的JSP（或其它等效的Servlet）的引用。 此程式只應在開發和展示期間使用，不應用於生產環境。 引數會指定URL、登入和密碼。

* **ECMAScript路徑**:  `/libs/workflow/scripts/urlcaller.ecma`

* **裝載**:無
* **引數**:

```
        args := url [',' login ',' password]
        url := /* The URL to be called */
        login := /* The login to access the URL */
        password := /* The password to access the URL */
```

例如：`http://localhost:4502/my.jsp, mylogin, mypassword`

* **逾時**:已忽略

### LockProcess {#lockprocess}

鎖定工作流程的裝載。

* **Java類：** `com.day.cq.workflow.impl.process.LockProcess`

* **裝載：** JCR_PATH和JCR_UUID
* **引數：** 無
* **逾時：** 忽略

此步驟於下列情況下並無作用：

* 裝載已鎖定
* 裝載節點不包含jcr:content子節點

### 解鎖進程 {#unlockprocess}

解除鎖定工作流程的裝載。

* **Java類：** `com.day.cq.workflow.impl.process.UnlockProcess`

* **裝載：** JCR_PATH和JCR_UUID
* **引數：** 無
* **逾時：** 忽略

此步驟於下列情況下並無作用：

* 裝載已解除鎖定
* 裝載節點不包含jcr:content子節點

## 版本設定進程{#versioning-processes}

以下進程執行版本相關任務。

### CreateVersionProcess {#createversionprocess}

建立新版本的工作流程裝載(AEM頁面或DAM資產)。

* **Java類**:  `com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **裝載**:參照頁面或DAM資產的JCR路徑或UUID
* **引數**:無
* **逾時**:受尊重
