---
title: 艱難的一天
description: Tough Daytest模擬在最壞情況下的每日大約1000個作者的負載，同時進行所有操作。
topic-tags: testing
content-type: reference
exl-id: ceb9671c-57f9-4d81-94c0-0dbccd4d90a2
source-git-commit: ca6d41740dbb24dbba7cf7691c51435cc40d3ead
workflow-type: tm+mt
source-wordcount: '1849'
ht-degree: 2%

---

# 艱難的一天{#tough-day}

## 艱難的第2天 {#what-is-tough-day}

「艱難的第2天」是一個應用程式，它允許您強調test實例的AEM限制。 它可以使用預設的test套件在開箱後運行，也可以根據您的測試需要配置。 你可以看 [此錄制](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-toughday2-stress-testing-benchmarking-tool.html) 的子菜單。

>[!CAUTION]
>
>艱難的2日需要Java 8。

## 如何運行艱難的第2天 {#how-to-run-tough-day}

從下載 [Adobe儲存庫](https://repo1.maven.org/maven2/com/adobe/qe/toughday2/)。 下載應用程式後，可以通過提供 `host` 的下界。 在以下示例中，實AEM例在本地運行， `localhost` 值：

```xml
java -jar toughday2.jar --host=localhost
```

添加參數後運行的預設套件名為 `toughday`。 它包含以下使用案例：

* 為它們建立頁面和即時拷貝（包括部署）
* 獲取首頁
* 在querybuilder中運行查詢
* 建立資產層次結構
* 刪除資產

套件包含15%的寫操作和85%的讀操作。

要運行套件test, Tough Day 2將安裝其預設內容包。 通過設定 `installsamplecontent`參數 `false`，但請記住，您還應更改要運行的test的預設路徑。 如果jar在沒有參數的情況下運行，則Tough Day 2將顯示 [幫助資訊](/help/sites-developing/tough-day.md#getting-help)。

一般來說，您可以通過以下模式使用應用程式：

```xml
java -jar toughday2.jar [--help | --help_full | --help_tests | --help_publish]  [<global arguments> | <actions> | --runmode | --publishmode]
```

>[!NOTE]
>
>艱難的第2天沒有清理步驟。 因此，建議在克隆的試運行實例上運行Tough Day 2 ，而不是在主生產實例上運行。 應在test後刪除臨時實例。

### 獲取幫助 {#getting-help}

Tough Day 2提供了一系列可以從命令行訪問的幫助選項。 例如：

```xml
java -jar toughday2.jar --help_full
```

在下表中，可找到相關幫助參數。

<table>
 <tbody>
  <tr>
   <td><strong>參數</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>範例</strong></td>
  </tr>
  <tr>
   <td>--說明</td>
   <td>打印全局資訊，例如：可用操作、預定義的套件、運行模式和全局參數。</td>
   <td> </td>
  </tr>
  <tr>
   <td> — 幫助_發佈</td>
   <td>打印所有可用的發佈器。</td>
   <td> </td>
  </tr>
  <tr>
   <td>-help_test</td>
   <td>打印test類及其說明。</td>
   <td> </td>
  </tr>
  <tr>
   <td>-help_full</td>
   <td>打印以上所有元件，以及test、發佈器和套件元件。</td>
   <td> </td>
  </tr>
  <tr>
   <td> —help —runmode/publishmode type=&lt;mode&gt;</td>
   <td>列出有關指定運行或發佈模式的資訊。</td>
   <td><p>java -jar toughday2.jar —help —runmode type=constanload</p> <p>java -jar toughday2.jar — 幫助 — publishmode type=intervals</p> </td>
  </tr>
  <tr>
   <td> — 幫助 — 套件=&lt;suitename&gt;</td>
   <td>列出給定套件的所有test及其各自的可配置屬性。</td>
   <td><br /> java -jar toughday2.jar —help —suite=gettest</td>
  </tr>
  <tr>
   <td>  — 幫助 — 標籤=&lt;tag&gt;</td>
   <td><br /> 列出具有指定標籤的所有項目。</td>
   <td>java -jar toughday2.jar —help -tag=publish</td>
  </tr>
  <tr>
   <td> — 幫助 &lt;testclass publisherclass=""&gt;</td>
   <td><br /> 列出給定test或發佈者的所有可配置屬性。</td>
   <td><p>java -jar toughday2.jar — 幫助UploadPDFTest</p> <p>java -jar toughday2.jar — 幫助CSVPublisher</p> </td>
  </tr>
 </tbody>
</table>

### 全局參數 {#global-parameters}

Tough Day 2提供了設定或更改test環境的全局參數。 這些包括目標主機、埠號、使用的協定、實例的用戶和密碼等。 例如：

```xml
java -jar toughday2.jar --host=host --protocol=https --port=4502 --duration=30m --dryrun=true
```

您可以在以下清單中找到相關參數：

| **參數** | **說明** | **預設值** | **可能的值** |
|---|---|---|---|
| `--installsamplecontent=<Val>` | 安裝或跳過預設的Tough Day 2內容包。 | true | 真或假 |
| `--protocol=<Val>` | 用於主機的協定。 | http | http或https |
| `--host=<Val>` | 要作為目標的主機名或IP。 |  |  |
| `--port=<Val>` | 主機的埠。 | 4502 |  |
| `--user=<Val>` | 實例的用戶名。 | 管理員 |  |
| `--password=<Val>` | 給定用戶的密碼。 | 管理員 |  |
| `--duration=<Val>` | test的持續時間。 可以以(表示&#x200B;**s**)秒，(**米**)inut,(**h**)**d**)。 | 1d |  |
| `--timeout=<Val>` | test在中斷並標籤為失敗之前將運行多長時間。 以秒錶示。 | 180 |  |
| `--suite=<Val>` | 值可以是預定義test套件的一個或清單（用逗號分隔）。 | 艱難 |  |
| `--configfile=<Val>` | 目標yaml配置檔案。 |  |  |
| `--contextpath=<Val>` | 實例的上下文路徑。 |  |  |
| `--loglevel=<Val>` | Tough Day 2引擎的日誌級別。 | 資訊 | 全部、調試、資訊、警告、錯誤、致命、關閉 |
| `--dryrun=<Val>` | 如果為true，則打印結果配置，且不運行任何test。 | false | 真或假 |

## 自定義 {#customizing}

可以通過兩種方式實現定制：命令行參數或yaml配置檔案。 **配置檔案通常用於大型自定義套件，並且它們將覆蓋Tough Day 2預設參數。 命令行參數將覆蓋配置檔案和預設參數。**

保存test配置的唯一方法是以yaml格式複製它。

### 添加新Test {#adding-a-new-test}

如果不想使用預設 `toughday` 您可以使用 `add` 的下界。 以下示例說明如何添加 `CreateAssetTreeTest` test，方法是使用命令行參數或yaml配置檔案。

使用命令行參數：

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest
```

使用yaml配置檔案：

```xml
globals:
  host : localhost
tests:
  - add : CreateAssetTreeTest
```

### 添加同一Test的多個實例  {#adding-multiple-instances-of-the-same-test}

您也可以添加和運行同一test的多個實例，但每個實例必須具有唯一的名稱。 以下示例說明如何使用命令行參數或yaml配置檔案添加同一test的兩個實例。

使用命令行參數：

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest name=FirstAssetTree --add CreateAssetTreeTest name=SecondAssetTree
```

使用yaml配置檔案：

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

### 更改Test屬性 {#changing-the-test-properties}

如果需要更改一個或多個test屬性，可以將該屬性添加到命令行或yaml配置檔案。 要查看所有可用test屬性，請添加 `--help <TestClass/PublisherClass>` 命令行的參數，例如：

```xml
java -jar toughday2.jar --help CreatePageTreeTest
```

請記住，yaml配置檔案將覆蓋Tough Day 2預設參數，命令行參數將覆蓋配置檔案和預設值。

以下示例說明如何更改 `template` 屬性 `CreatePageTreeTest` test，方法是使用命令行參數或yaml配置檔案。

使用命令行參數：

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest template=/conf/toughday-templates/settings/wcm/templates/toughday-template
```

使用yaml配置檔案：

```xml
globals:
  host : localhost
tests:
  - add : CreatePageTreeTest
    properties:
      template : /conf/toughday-templates/settings/wcm/templates/toughday-template
```

### 使用預定義Test套件 {#working-with-predefined-test-suites}

以下示例說明如何將test添加到預定義的套件以及如何從預定義的套件重新配置和排除現有test。

您可以使用 `add` 參數並指定目標預定義套件。

使用命令行參數：

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest
```

使用yaml配置檔案：

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - add : CreatePageTreeTest
```

給定套件中的現有test也可以使用 `config`* *參數。 請注意，您還必須指定套件名稱和test的實際名稱(而不是Test類名稱)。 您可以在 `name` test類的屬性。 有關如何查找test屬性的詳細資訊，請閱讀 [更改Test屬性](/help/sites-developing/tough-day.md#changing-the-test-properties) 的子菜單。

在下面的示例中， `CreatePageTreeTest` （命名） `UploadAsset`)更改為「NewAsset」。

使用命令行參數：

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --config UploadAsset title=NewAsset
```

使用yaml配置檔案：

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - config : UploadAsset
    properties :
      title : NewAsset
```

此外，您還可以使用以下命令從預設配置中刪除預定義套件或發佈伺服器中的test資訊： `exclude` 的下界。 請注意，您還必須指定套件名稱和test的實際名稱(不是TestC) `lass` 名稱)。 您可以在 `name` test類的屬性。 在下面的示例中， `CreatePageTreeTest` （命名） `UploadAsset`)test將從toughday套件中刪除。

使用命令行參數：

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --exclude UploadAsset
```

使用yaml配置檔案：

```xml
globals:
  host : localhost
  suite : toughday
tests:
  - exclude : UploadAsset
```

### 執行模式 {#run-modes}

艱難的第2天可以以下模式之一運行： **正** 和 **恆載荷**。

的 **正** 運行模式有兩個參數：

* `concurrency` - concurrency表示Tough Day 2為執行test而建立的線程數。 在這些線程上，將執行test，直到持續時間已用完或不再執行test。

* `waittime`  — 同一線程上兩個連續test執行之間的等待時間。 該值必須以毫秒為單位表示。

以下示例說明如何使用命令行添加參數：

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest --runmode=normal concurrency=20
```

或使用yaml配置檔案：

```xml
runmode:
  type : normal
  waittime : 300
  concurrency : 200
```

的 **恆載荷** 運行模式與普通運行模式不同，它生成了恆定數量的啟動test執行，而不是恆定數量的線程。 可使用具有相同名稱的運行模式參數來設定載荷。

### Test選擇 {#test-selection}

test選擇過程對於兩種運行模式都相同，如下所示：所有test `weight` 屬性，它確定線程中執行的可能性。 例如，如果我們有兩個test，一個重量為5，另一個重量為10，則後者被執行的可能性是前者的兩倍。

此外，test可以 `count` 屬性，該屬性將執行數限制為給定數。 傳遞此數字後，將不再執行test。 所有已運行的test實例將按照配置完成運行。 以下示例說明如何在命令行或使用yaml配置檔案添加這些參數。

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
>由於並行執行，實際test運行數將與 `count` 的下界。 期望與運行線程數成比例的偏差(由 `concurrency parameter`)。

### 排練 {#dry-run}

乾式運行將解析所有給定輸入（命令行參數或配置檔案），並將其與預設值合併，然後輸出結果。 它不執行任何test。

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest --dryrun=true
```

## 輸出 {#output}

Tough Day 2輸出test度量和日誌。 有關詳細資訊，請閱讀以下部分。

### Test度量 {#test-metrics}

艱難的第2天當前報告9個可評估的test指標。 使用 **&#42;** 符號僅在成功運行後報告：

| **名稱** | **說明** |
|---|---|
| 時間戳 | 上次完成test運行的時間戳。 |
| 已通過 | 成功運行的數量。 |
| 已失敗 | 失敗的運行數。 |
| 最小值&#42; | test執行的最短持續時間。 |
| 最大值&#42; | 執行test的最長時間。 |
| 中等&#42; | 計算所有test執行的中值持續時間。 |
| 平均&#42; | 計算所有test執行的平均持續時間。 |
| 標準開發&#42; | 標準差。 |
| 90便士&#42; | 90百分點。 |
| 99便士&#42; | 99百分點。 |
| 99.9便士&#42; | 99.9百分點。 |
| 實際吞吐量&#42; | 運行數除以已用執行時間。 |

這些度量是在發佈者的幫助下編寫的，發佈者可與 `add` 參數(類似於添加test)。 目前有兩種選擇：

* **CSVPublisher**  — 輸出為CSV檔案。
* **控制台發佈伺服器**  — 輸出顯示在控制台中。

預設情況下，兩個發佈器都處於啟用狀態。

此外，還有兩種模式報告度量：

* 的 **簡單** 發佈模式 — 報告從執行開始到發佈的結果。
* 的 **間隔** 發佈模式 — 在給定時間範圍內報告結果。 可以使用 **間隔** 發佈模式參數。

以下示例說明如何配置 `intervals` 命令行或使用yaml配置檔案來設定參數。

使用命令行參數：

```xml
java -jar toughday2.jar --host=localhost --add CreatePageTreeTest --publishmode type=intervals interval=10s
```

使用yaml配置檔案：

```xml
publishmode:
     type : intervals
     interval : 10s
     tests:
        -add : CreatePageTreeTest
```

### 記錄 {#logging}

Tough Day 2在運行Tough Day 2的同一目錄下建立日誌資料夾。 此資料夾包含兩種類型的日誌：

* **toughday.log**:包含與應用程式狀態、調試資訊和全局消息相關的消息。
* **強日&lt;testname>.日誌**:與指定test相關的消息。

日誌不會被覆蓋，後續運行會將消息附加到現有日誌。 日誌有幾個級別，有關詳細資訊，請參閱 ` [loglevel parameter](/help/sites-developing/tough-day.md#global-parameters)`。

<!--
#### Example Usage {#example-usage}

#### Known Issues {#known-issues}

[Get File](assets/toughday-6_1.jar)
-->
