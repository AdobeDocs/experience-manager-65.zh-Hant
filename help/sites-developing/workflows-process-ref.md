---
title: 工作流程處理序參考
seo-title: Workflow Process Reference
description: 工作流程處理序參考
seo-description: null
uuid: de367aa8-4580-4810-b665-2a7b521e36ca
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: dbdf981f-791b-4ff7-8ca8-039d0bdc9c92
exl-id: a9de8ec6-6948-4643-89c3-62d9b1f6293a
source-git-commit: cf3b739fd774bc860d9906b9884d22fd532fd5dd
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 1%

---

# 工作流程處理序參考{#workflow-process-reference}

提AEM供了幾個可用於建立工作流模型的流程步驟。 還可以為內置步驟未涵蓋的任務添加自定義流程步驟(請參閱 [建立工作流模型](/help/sites-developing/workflows-models.md))。

## 流程特性 {#process-characteristics}

對於每個過程步驟，描述了以下特徵。

### Java類或ECMA路徑 {#java-class-or-ecma-path}

進程步驟由Java類或ECMAScript定義。

* 對於Java類進程，提供完全限定的類名。
* 對於ECMAScript進程，將提供指向指令碼的路徑。

### 裝載 {#payload}

有效負載是工作流實例對其進行操作的實體。 負載由啟動工作流實例的上下文隱式選擇。

例如，如果將工作流應用於頁AEM面 *P* 然後 *P* 在工作流進行時逐步傳遞，每個步驟可選地在 *P* 以某種方式。

在最常見的情況下，負載是儲存庫中的JCR節點(例如，頁AEM或資產)。 JCR節點負載作為字串傳遞，該字串是JCR路徑或JCR標識符(UUID)。 在某些情況下，負載可以是JCR屬性（作為JCR路徑傳遞）、URL、二進位對象或泛型Java對象。 對負載起作用的單個進程步驟通常期望某種類型的負載，或根據負載類型採取不同的操作。 對於下面描述的每個過程，將說明預期的負載類型（如果有）。

### 引數 {#arguments}

某些工作流進程接受管理員在設定工作流步驟時指定的參數。

參數作為單個字串在 **進程參數** 屬性 **屬性** 對話框。 對於下面描述的每個過程，參數字串的格式都以簡單的EBNF語法進行描述。 例如，以下指示參數字串由一個或多個以逗號分隔的對組成，其中每對都由名稱（即字串）和值組成，用雙冒號分隔：

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### 逾時 {#timeout}

在此超時期後，工作流步驟不再工作。 某些工作流進程會遵守超時，而另一些工作流進程則不適用並會忽略。

### 權限 {#permissions}

會話已傳遞到 `WorkflowProcess` 由工作流進程服務的服務用戶支援，該服務在儲存庫的根目錄下具有以下權限：

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

如果該權限集對您的 `WorkflowProcess` 實現，則它必須使用具有所需權限的會話。

建議的方法是使用建立的具有所需權限子集的服務用戶。

>[!CAUTION]
>
>如果從6.2之前的版AEM本升級，則可能需要更新實施。
>
>在以前的版本中，管理會話已傳遞到 `WorkflowProcess` 實現，並可以完全訪問儲存庫，而無需定義特定ACL。
>
>權限現在定義為上述([權限](#permissions))。 同樣，也是更新實現的推薦方法。
>
>當代碼更改不可行時，短期解決方案也可用於向後相容：
>
>* 使用Web控制台( `/system/console/configMgr` 查找 **Adobe花崗岩工作流配置服務**
>
>* 啟用 **工作流進程舊模式**
>
>這將恢復為向提供管理員會話的舊行為 `WorkflowProcess` 並再次提供對整個儲存庫的無限制訪問。

## 工作流控制進程 {#workflow-control-processes}

以下進程不對內容執行任何操作。 它們用於控制工作流本身的行為。

### AbsoluteTimeAutoAdvancer(Absolute Time Auto Advancer) {#absolutetimeautoadvancer-absolute-time-auto-advancer}

的 `AbsoluteTimeAutoAdvancer` （絕對時間自動高級）流程的行為與 **自動高級**，但是它在給定時間和日期而不是在給定時間長度之後超時。

* **Java類**: `com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **負載**:沒有。
* **參數**:沒有。
* **超時**:達到設定的時間和日期時，處理超時。

### AutoAdvancer(Auto Advancer) {#autoadvancer-auto-advancer}

的 `AutoAdvancer` 進程自動將工作流提前到下一步。 如果有多個可能的下一步（例如，有OR拆分），則此流程將沿 *預設路由*，否則將不高級工作流。

* **Java類**: `com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **負載**:沒有。
* **參數**:沒有。
* **超時**:在設定時間長度後處理超時。

### ProcessAssembler(Process Assembler) {#processassembler-process-assembler}

的 `ProcessAssembler` 進程在一個工作流步驟中按順序執行多個子進程。 使用 `ProcessAssembler`，在工作流中建立此類型的單個步驟，並設定其參數以指示要執行的子進程的名稱和參數。

* **Java類**: `com.day.cq.workflow.impl.process.ProcessAssembler`

* **負載**:DAM資產、頁AEM或無負載（取決於子進程的要求）。
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

* **超時**:尊重。

例如：

* 從資產中提取元資料。
* 建立三個指定大小的縮略圖。
* 從資產建立JPEG影像，假定資產最初既不是GIF也不是PNG(在這種情況下不建立JPEG)。
* 設定資產的上次修改日期。

```shell
com.day.cq.dam.core.process.ExtractMetadataProcess,
    com.day.cq.dam.core.process.CreateThumbnailProcess::[140:100];[48:48];[319:319:false],
    com.day.cq.dam.core.process.CreateWebEnabledImageProcess::dimension:1280:1280;mimetype:image/jpeg,
    com.day.cq.dam.core.process.AssetSetLastModifiedProcess
```

## 基本流程 {#basic-processes}

以下進程執行簡單任務或作為示例。

>[!CAUTION]
>
>你 ***必須*** 沒有改變 `/libs` 路徑。
>
>這是因為 `/libs` 在下次升級實例時被覆蓋（在應用修補程式或功能包時可能被覆蓋）。

### 刪除 {#delete}

將刪除給定路徑上的項。

* **ECMAScript路徑**: `/libs/workflow/scripts/delete.ecma`

* **負載**:JCR路徑
* **參數**:無
* **超時**:已忽略

### 諾普 {#noop}

這是空進程。 它不執行任何操作，但記錄調試消息。

* **ECMAScript路徑**: `/libs/workflow/scripts/noop.ecma`

* **負載**:無
* **參數**:無
* **超時**:已忽略

### 規則錯誤 {#rule-false}

這是一個返回的空進程 `false` 的 `check()` 的雙曲餘切值。

* **ECMAScript路徑**: `/libs/workflow/scripts/rule-false.ecma`

* **負載**:無
* **參數**:無
* **超時**:已忽略

### 樣本 {#sample}

這是一個示例ECMAScript進程。

* **ECMAScript路徑**: `/libs/workflow/scripts/sample.ecma`

* **負載**:無
* **參數**:無
* **超時**:已忽略

### 鎖進程 {#lockprocess}

鎖定工作流的負載。

* **Java類：** `com.day.cq.workflow.impl.process.LockProcess`

* **負載：** JCR_PATH和JCR_UUID
* **參數：** 無
* **超時：** 已忽略

在下列情況下，該步驟無效：

* 負載已鎖定
* 負載節點不包含jcr:content子節點

### 解鎖進程 {#unlockprocess}

解除鎖定工作流的負載。

* **Java類：** `com.day.cq.workflow.impl.process.UnlockProcess`

* **負載：** JCR_PATH和JCR_UUID
* **參數：** 無
* **超時：** 已忽略

在下列情況下，該步驟無效：

* 負載已解鎖
* 負載節點不包含jcr:content子節點

## 版本控制進程 {#versioning-processes}

以下進程執行與版本相關的任務。

### 建立版本進程 {#createversionprocess}

建立工作流負載的新版本(AEM頁或DAM資產)。

* **Java類**: `com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **負載**:引用頁或DAM資產的JCR路徑或UUID
* **參數**:無
* **超時**:受尊重
