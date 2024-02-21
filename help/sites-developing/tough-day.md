---
title: 艱苦的一天
description: 「艱難日」測試可在所有作業同時進行的情況下，模擬在最糟糕的情況下約1000名作者的每日負載。
topic-tags: testing
content-type: reference
exl-id: ceb9671c-57f9-4d81-94c0-0dbccd4d90a2
source-git-commit: b1012548630affd697edd27c90bdac4eeb35125f
workflow-type: tm+mt
source-wordcount: '1825'
ht-degree: 1%

---

# 艱苦的一天{#tough-day}

## 何謂艱難的第2天 {#what-is-tough-day}

「艱難第2天」應用程式可讓您對AEM執行個體的限制進行壓力測試。 您可以立即使用預設的測試套件執行此檔案，也可以根據您的測試需求進行設定。 您可以觀看 [此錄製](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2017/aem-toughday2-stress-testing-benchmarking-tool.html) 以取得應用程式的簡報。

>[!CAUTION]
>
>「艱難第2天」需要Java™ 8。

## 如何執行艱難的第2天 {#how-to-run-tough-day}

從以下網站下載最新版《艱難第2天》： [Adobe存放庫](https://repo1.maven.org/maven2/com/adobe/qe/toughday2/). 下載應用程式後，您可以提供 `host` 引數。 在以下範例中，AEM執行個體會在本機執行，因此 `localhost` 使用的值：

```xml
java -jar toughday2.jar --host=localhost
```

新增引數後執行的預設套裝命名為 `toughday`. 它包含下列使用案例：

* 為其建立頁面和即時副本（包括轉出）
* 取得首頁
* 在querybuilder中執行查詢
* 建立資產階層
* 刪除資產

該套裝包含15%的寫入動作和85%的讀取動作。

若要執行套裝測試，「艱難第2天」將會安裝其預設內容套件。 可藉由設定 `installsamplecontent`引數至 `false`，但請記住，您也應該變更要執行測試的預設路徑。 如果jar是在沒有引數的情況下執行，「第2天」會顯示 [說明資訊](/help/sites-developing/tough-day.md#getting-help).

一般而言，您可以遵循此模式來使用應用程式：

```xml
java -jar toughday2.jar [--help | --help_full | --help_tests | --help_publish]  [<global arguments> | <actions> | --runmode | --publishmode]
```

>[!NOTE]
>
>「艱難第2天」沒有清理步驟。 因此，建議在複製的測試執行個體上執行「艱難第2天」，而不是在主要生產執行個體上執行。 測試後應該捨棄測試執行個體。
>

### 取得協助 {#getting-help}

「困難的第2天」提供多種從命令列存取的說明選項。 例如：

```xml
java -jar toughday2.jar --help_full
```

在下表中，您可以找到相關的說明引數。

<table>
 <tbody>
  <tr>
   <td><strong>參數</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>範例</strong></td>
  </tr>
  <tr>
   <td> — 說明</td>
   <td>列印全域資訊，例如：可用的動作、預先定義的套裝、執行模式和全域引數。</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_publish</td>
   <td>列印出所有可用的發行者。</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_tests</td>
   <td>列印測試類別及其說明。</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_full</td>
   <td>列印上述所有內容，以及測試、發佈者和套裝元件。</td>
   <td> </td>
  </tr>
  <tr>
   <td> —help —runmode/publishmode type=&lt;mode&gt;</td>
   <td>列出有關指定執行或發佈模式的資訊。</td>
   <td><p>Java™ -jar toughday2.jar —help —runmode type=constantload</p> <p>Java™ -jar toughday2.jar —help —publishmode type=intervals</p> </td>
  </tr>
  <tr>
   <td>—help —suite=&lt;suitename&gt;</td>
   <td>列出指定套裝的所有測試及其各自的可設定屬性。</td>
   <td><br /> Java™ -jar toughday2.jar —help —suite=get_tests</td>
  </tr>
  <tr>
   <td> —help —tag=&lt;tag&gt;</td>
   <td><br /> 列出具有指定標籤的所有專案。</td>
   <td>Java™ -jar toughday2.jar —help —tag=publish</td>
  </tr>
  <tr>
   <td> — 說明 &lt;testclass publisherclass=""&gt;</td>
   <td><br /> 列出指定測試或發佈程式的所有可設定屬性。</td>
   <td><p>Java™ -jar toughday2.jar —help UploadPDFTest</p> <p>Java™ -jar toughday2.jar —help CSVPublisher</p> </td>
  </tr>
 </tbody>
</table>

### 全域引數 {#global-parameters}

強悍的第2天提供設定或變更測試環境的全域引數。 這些包括目標主機、連線埠號碼、使用的通訊協定、執行個體的使用者和密碼等等。 例如：

```xml
java -jar toughday2.jar --host=host --protocol=https --port=4502 --duration=30m --dryrun=true
```

您可以在下列清單中找到相關引數：

| **引數** | **說明** | **預設值** | **可能的值** |
|---|---|---|---|
| `--installsamplecontent=<Val>` | 安裝或略過預設的「硬性第2天」內容套件。 | true | true或false |
| `--protocol=<Val>` | 用於主機的通訊協定。 | http | http或https |
| `--host=<Val>` | 目標主機名稱或IP。 |  |  |
| `--port=<Val>` | 主機的連線埠。 | 4502 |  |
| `--user=<Val>` | 執行個體的使用者名稱。 | 管理員 |  |
| `--password=<Val>` | 指定使用者的密碼。 | 管理員 |  |
| `--duration=<Val>` | 測試的持續時間。 可以表達為(**s**)秒，(**m**)inutes， (**h**)我們的和(**d**)天。 | 1d |  |
| `--timeout=<Val>` | 測試會在中斷並標籤為失敗之前執行多久。 以秒為單位表示。 | 180 |  |
| `--suite=<Val>` | 該值可為預先定義的測試套裝的一個或清單（以逗號分隔）。 | toughday |  |
| `--configfile=<Val>` | 目標yaml設定檔。 |  |  |
| `--contextpath=<Val>` | 執行個體的內容路徑。 |  |  |
| `--loglevel=<Val>` | 「艱難第2天」引擎的記錄層級。 | 資訊 | 全部，偵錯，資訊，警告，錯誤，致命，關閉 |
| `--dryrun=<Val>` | 如果為true，則列印結果設定並且不執行任何測試。 | false | true或false |

## 自訂 {#customizing}

可透過兩種方式實現自訂：命令列引數或yaml組態檔。 **設定檔案用於大型自訂套件，可覆寫「艱難第2天」預設引數。 命令列引數會覆寫組態檔和預設引數。**

儲存測試設定的唯一方法是以yaml格式複製它。

### 新增測試 {#adding-a-new-test}

如果您不想使用預設值 `toughday` 套件：您可以使用 `add` 引數。 以下範例說明如何新增 `CreateAssetTreeTest` 使用命令列引數或yaml組態檔進行測試。

使用命令列引數：

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest
```

使用yaml組態檔：

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
```

### 新增相同測試的多個執行個體  {#adding-multiple-instances-of-the-same-test}

您也可以新增並執行相同測試的多個執行個體，但每個執行個體都必須有唯一的名稱。 以下範例說明如何使用命令列引數或yaml組態檔來新增相同測試的兩個執行個體。

使用命令列引數：

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest name=FirstAssetTree --add CreateAssetTreeTest name=SecondAssetTree
```

使用yaml組態檔：

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
    properties:
      name : FirstAssetTree
  - add : CreateAssetTreeTest
    properties:
      name : SecondAssetTree
```

### 變更測試屬性 {#changing-the-test-properties}

如果您需要變更一個或多個測試屬性，可以將該屬性新增到命令列或yaml組態檔。 若要檢視所有可用的測試屬性，請新增 `--help <TestClass/PublisherClass>` 引數到命令列，例如：

```xml
java -jar toughday2.jar --help CreatePageTreeTest
```

請記住，yaml組態檔將覆寫「Touch Day 2」預設引數，而命令列引數將覆寫組態檔和預設值。

以下範例說明如何變更 `template` 的屬性 `CreatePageTreeTest` 使用命令列引數或yaml組態檔進行測試。

使用命令列引數：

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest template=/conf/toughday-templates/settings/wcm/templates/toughday-template
```

使用yaml組態檔：

```xml
globals:
  host : localhost
tests:
  - add : CreatePageTreeTest
    properties:
      template : /conf/toughday-templates/settings/wcm/templates/toughday-template
```

### 使用預先定義的測試套裝 {#working-with-predefined-test-suites}

以下範例說明如何將測試新增至預先定義的套裝，以及如何重新設定並從預先定義的套裝中排除現有的測試。

您可以使用將測試新增至預先定義的套件 `add` 引數並指定目標預先定義的套件。

使用命令列引數：

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest
```

使用yaml組態檔：

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - add : CreatePageTreeTest
```

指定套件中的現有測試也可以使用重新設定 `config`* *引數。 同時指定套裝名稱和測試的實際名稱（而不是「測試類別」名稱）。 您可以在以下位置找到測試名稱： `name` 測試類別的屬性。 如需如何尋找測試屬性的詳細資訊，請參閱 [變更測試屬性](/help/sites-developing/tough-day.md#changing-the-test-properties) 區段。

在以下範例中，的預設資產標題 `CreatePageTreeTest` (已命名 `UploadAsset`)變更為「NewAsset」。

使用命令列引數：

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --config UploadAsset title=NewAsset
```

使用yaml組態檔：

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - config : UploadAsset
    properties :
      title : NewAsset
```

此外，您也可以使用，從預設設定中移除預先定義的套裝或發佈程式測試。 `exclude` 引數。 同時指定套裝名稱和測試的實際名稱（不是測試C） `lass` 名稱)。 您可以在以下位置找到測試名稱： `name` 測試類別的屬性。 在以下範例中， `CreatePageTreeTest` (已命名 `UploadAsset`)測試已從toughday套裝中移除。

使用命令列引數：

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --exclude UploadAsset
```

使用yaml組態檔：

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - exclude : UploadAsset
```

### 執行模式 {#run-modes}

強悍的第2天可以下列其中一個模式執行： **一般** 和 **恆定負載**.

此 **一般** 執行模式有兩個引數：

* `concurrency` - concurrency代表「艱難第2天」將為測試執行建立的對話串數目。 在這些執行緒上，將會執行測試，直到持續時間耗盡或沒有更多要執行的測試為止。

* `waittime`  — 相同執行緒上兩個連續測試執行之間的等待時間。 值必須以毫秒為單位表示。

以下範例說明如何使用命令列新增引數：

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest --runmode=normal concurrency=20
```

或使用yaml組態檔：

```xml
runmode:
  type : normal
  waittime : 300
  concurrency : 200
```

此 **恆定負載** 執行模式與一般執行模式不同，會產生固定數量的已啟動測試執行，而不是固定數量的執行緒。 您可以使用同名的執行模式引數來設定負載。

### 測試選取範圍 {#test-selection}

兩種執行模式的測試選取程式都相同，如下所示：所有測試都有 `weight` 屬性，判斷執行緒中執行的可能性。 例如，如果您有兩個測試，一個具有5的權重，另一個具有10的權重，則後者比前者執行的可能性高兩倍。

此外，測試可以有 `count` 屬性，將執行次數限制在給定數字。 通過此數字後，不會再執行測試。 所有已在執行的測試執行個體都會依照設定完成執行。 下列範例說明如何在命令列或使用yaml組態檔新增這些引數。

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest weight=5 --add CreatePageTreeTest weight=10 count=100 --runmode=normal concurrency=20
```

或

```xml
- add : CreateAssetTreeTest
    properties :
      name : UploadAsset
      weight : 5
      base : 3
      foldertitle : IAmAFolder
      assettitle : IAmAnAsset
      count : 100
```

>[!NOTE]
>
>由於平行執行，實際測試執行次數不會完全符合中設定的數量。 `count` 引數。 預期與執行中執行緒數量成比例的偏差(由 `concurrency parameter`)。

### 試執行 {#dry-run}

試執行會剖析所有指定的輸入（命令列引數或組態檔），將其與預設值合併，然後輸出結果。 它不會執行任何測試。

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest --dryrun=true
```

## 輸出 {#output}

「艱難第2天」會輸出測試量度和記錄。 如需詳細資訊，請閱讀以下章節。

### 測試量度 {#test-metrics}

「艱難第2天」目前報告九個您可以評估的測試量度。 包含的量度 **&#42;** 符號只會在成功執行後報告：

| **名稱** | **說明** |
|---|---|
| 時間戳記 | 上次完成的測試回合的時間戳記。 |
| 已通過 | 成功執行的次數。 |
| 已失敗 | 失敗的執行次數。 |
| 最小值&#42; | 測試執行的最短持續時間。 |
| 最大&#42; | 測試執行的最長持續時間。 |
| 中間值&#42; | 計算的所有測試執行的中位數持續時間。 |
| 平均&#42; | 所有測試執行的計算平均持續時間。 |
| StdDev&#42; | 標準差。 |
| 90p&#42; | 第90個百分位數。 |
| 99p&#42; | 第99個百分位數。 |
| 99.9便士&#42; | 99.9百分位數。 |
| 實際輸送量&#42; | 執行次數除以經過的執行時間。 |

這些量度是在發行者的協助下撰寫，可透過以下方式新增： `add` 引數（與新增測試類似）。 目前有兩個選項：

* **CSVPublisher**  — 輸出為CSV檔案。
* **ConsolePublish**  — 主控台中會顯示輸出。

依預設，兩個發佈程式都會啟用。

此外，有兩種模式可報告量度：

* 此 **簡單** 發佈模式 — 報告從執行開始到發佈時的結果。
* 此 **間隔** 發佈模式 — 在指定的時間範圍內報告結果。 您可以使用以下設定時間範圍 **間隔** 發佈模式引數。

下列範例顯示如何設定 `intervals` 引數，可在命令列上使用，或使用yaml組態檔案使用。

使用命令列引數：

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest --publishmode type=intervals interval=10s
```

使用yaml組態檔：

```xml
publishmode:
     type : intervals
     interval : 10s
     tests:
        -add : CreatePageTreeTest
```

### 記錄 {#logging}

「艱難第2天」會在您執行「艱難第2天」的同一個目錄中建立一個記錄檔資料夾。 此資料夾包含兩種型別的記錄：

* **toughday.log**：包含與應用程式狀態、偵錯資訊和全域訊息相關的訊息。
* **toughday_&lt;testname>.log**：與指定測試相關的訊息。

不會覆寫記錄，後續執行會將訊息附加至現有記錄。 記錄有數個層級，如需詳細資訊，請參閱 [loglevel引數。](#global-parameters).

<!--
#### Example Usage {#example-usage}

#### Known Issues {#known-issues}

[Get File](assets/toughday-6_1.jar)
-->
