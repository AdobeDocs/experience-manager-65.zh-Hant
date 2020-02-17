---
title: 艱難的一天
seo-title: 艱難的一天
description: Tough Day test模擬大約1000位作者在最壞情況下的每日負載，同時進行所有作業。
seo-description: Tough Day test模擬大約1000位作者在最壞情況下的每日負載，同時進行所有作業。
uuid: 1b672182-40f5-4580-b038-2e3c8fbfb8b7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: ea6b40fe-b6e1-495c-b34f-8815a4e2e42e
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# 艱難的一天{#tough-day}

## 艱難的一天2 {#what-is-tough-day}

「Tough Day 2」是一套應用程式，可讓您壓力測試AEM執行個體的限制。 它可在預設測試套裝的包裝盒內執行，或是設定成符合您的測試需求。 您可以觀 [看此錄](https://docs.adobe.com/ddc/en/gems/Toughday2---A-new-and-improved-stress-testing-and-benchmarking-tool.html) ，以呈現應用程式。

## 如何經營艱難的第2天 {#how-to-run-tough-day}

從 [Adobe Repository下載Tough Day 2的最新版本](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/qe/toughday2/)。 下載應用程式後，您就可以透過提供參數，立即將它執 `host` 行。 在下列範例中，AEM例項會在本機執行，因此 `localhost` 會使用值：

```xml
java -jar toughday2.jar --host=localhost
```

新增參數後執行的預設套裝會命名 `toughday`。 它包含下列使用案例：

* 為其建立頁面和即時副本（包括展示）
* 取得首頁
* 在querybuilder中執行查詢
* 建立資產階層
* 刪除資產

套件包含15%的寫入動作和85%的讀取動作。

若要執行套裝測試，Tough Day 2將安裝其預設內容套件。 若要避免此問題，請 `installsamplecontent`將參數設 `false`定為，但請記住，您也應變更您要執行之測試的預設路徑。 如果jar在沒有參數的情況下運行，則Tough Day 2將顯示幫 [助資訊](/help/sites-developing/tough-day.md#getting-help)。

一般而言，您可依下列模式使用應用程式：

```xml
java -jar toughday2.jar [--help | --help_full | --help_tests | --help_publish]  [<global arguments> | <actions> | --runmode | --publishmode]
```

>[!NOTE]
>
>艱難的第2天沒有清理的步驟。 因此，建議在複製的測試執行個體上執行Tough Day 2，而不是在主生產執行個體上。 測試後應刪除測試例項。


### 取得說明 {#getting-help}

Thugh Day 2提供多種說明選項，可從命令列存取。 例如：

```xml
java -jar toughday2.jar --help_full
```

在下表中，您可以找到相關的說明參數。

<table>
 <tbody>
  <tr>
   <td><strong>參數</strong></td>
   <td><strong>說明</strong></td>
   <td><strong>範例</strong></td>
  </tr>
  <tr>
   <td>--說明</td>
   <td>打印全局資訊，例如：可用動作、預先定義的套件、執行模式和全域參數。</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_publish</td>
   <td>列印所有可用的發行者。</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_tests</td>
   <td>打印測試類及其說明。</td>
   <td> </td>
  </tr>
  <tr>
   <td>—help_full</td>
   <td>列印上述所有功能，以及測試、發佈器和套件元件。</td>
   <td> </td>
  </tr>
  <tr>
   <td> —help —runmode/publishmode type=&lt;Mode&gt;</td>
   <td>列出有關指定運行或發佈模式的資訊。</td>
   <td><p>java -jar toughday2.jar —help —runmode type=constantload</p> <p>java -jar toughday2.jar —help —publishmode type=intervals</p> </td>
  </tr>
  <tr>
   <td>—help —suite=&lt;SuiteName&gt;</td>
   <td>列出指定套裝的所有測試及其各自的可設定屬性。</td>
   <td><br /> java -jar toughday2.jar —help —suite=get_tests</td>
  </tr>
  <tr>
   <td> —help —tag=&lt;Tag&gt;</td>
   <td><br /> 列出所有具有指定標籤的項目。</td>
   <td>java -jar toughday2.jar —help —tag=publish</td>
  </tr>
  <tr>
   <td>—help &lt;TestClass/PublisherClass&gt;</td>
   <td><br /> 列出給定測試或發佈者的所有可配置屬性。</td>
   <td><p>java -jar toughday2.jar —help UploadPDFest</p> <p>java -jar toughday2.jar —help CSVPublisher</p> </td>
  </tr>
 </tbody>
</table>

### 全域參數 {#global-parameters}

Tough Day 2提供全域參數，可設定或變更測試環境。 這些包括目標主機、埠號、使用的通訊協定、例項的使用者和密碼等等。 例如：

```xml
java -jar toughday2.jar --host=host --protocol=https --port=4502 --duration=30m --dryrun=true
```

您可以在下列清單中找到相關參數：

| **參數** | **說明** | **預設值** | **可能的值** |
|---|---|---|---|
| `--installsamplecontent=<Val>` | 安裝或跳過預設的Tough Day 2內容套件。 | true | true或false |
| `--protocol=<Val>` | 用於主機的協定。 | http | http或https |
| `--host=<Val>` | 要定位的主機名或IP。 |  |  |
| `--port=<Val>` | 主機的埠。 | 4502 |  |
| `--user=<Val>` | 實例的用戶名。 | 管理員 |  |
| `--password=<Val>` | 給定使用者的密碼。 | 管理員 |  |
| `--duration=<Val>` | 測試的持續時間。 可以以(**s**)秒、(**m**)分鐘、(**h**)和(**** d Ays)表示。 | 1d |  |
| `--timeout=<Val>` | 測試在中斷並標示為失敗之前會執行多久。 以秒為單位表示。 | 180 |  |
| `--suite=<Val>` | 值可以是預先定義測試套裝的一或一個清單（以逗號分隔）。 | toughday |  |
| `--configfile=<Val>` | 目標yaml配置檔案。 |  |  |
| `--contextpath=<Val>` | 實例的上下文路徑。 |  |  |
| `--loglevel=<Val>` | Tough Day 2引擎的記錄層級。 | 資訊 | 全部，調試，資訊，警告，錯誤，致命，關閉 |
| `--dryrun=<Val>` | 如果為true，則列印產生的設定，且不執行任何測試。 | false | true或false |

## 自訂 {#customizing}

定制可以通過兩種方式實現：命令行參數或yaml配置檔案。 **設定檔案通常用於大型自訂套裝，而且會覆寫Tough Day 2預設參數。 命令行參數會覆蓋配置檔案和預設參數。**

儲存測試設定的唯一方式是以yaml格式複製。 如需詳細資訊，請參 [閱以下各節中的toughday.yaml](https://repo.adobe.com/nexus/service/local/repositories/releases/content/com/adobe/qe/toughday2/0.2.1/toughday2-0.2.1.yaml) 組態和yaml組態範例。

### 新增測試 {#adding-a-new-test}

如果您不想使用預設套裝，可 `toughday` 以使用參數新增您選擇的測 `add` 試。 下列範例說明如何使用命 `CreateAssetTreeTest` 令列參數或yaml組態檔來新增測試。

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

### 新增相同測試的多個例項 {#adding-multiple-instances-of-the-same-test}

您也可以新增並執行相同測試的多個例項，但每個例項必須有唯一的名稱。 以下範例說明如何使用命令列參數或yaml組態檔新增兩個相同測試的例項。

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

### 變更測試屬性 {#changing-the-test-properties}

如果您需要變更一或多個測試屬性，可將該屬性新增至命令列或yaml組態檔。 要查看所有可用的測試屬性，請 `--help <TestClass/PublisherClass>` 將參數添加到命令行，例如：

```xml
java -jar toughday2.jar --help CreatePageTreeTest
```

請記住，yaml組態檔將會覆寫Tough Day 2預設參數，而命令列參數會覆寫組態檔和預設值。

下列範例說明如何使用命 `template` 令列參數或 `CreatePageTreeTest` yaml組態檔來變更測試的屬性。

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

### 使用預先定義的測試套裝 {#working-with-predefined-test-suites}

下列範例說明如何新增測試至預先定義的套裝，以及如何從預先定義的套裝重新設定和排除現有測試。

您可以使用參數並指定目標的預先定義套裝，將 `add` 新測試新增至預先定義的套裝。

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

您也可以使用**參數重新設定指定套件中 `config`的現有測試。 請注意，您也必須指定測試的套裝名稱和實際名稱（而非測試類別名稱）。 您可以在測試類的屬性中 `name` 找到測試名稱。 如需如何尋找測試屬性的詳細資訊，請閱讀變更測 [試屬性一節](/help/sites-developing/tough-day.md#changing-the-test-properties) 。

在下方範例中，（已命名）的預 `CreatePageTreeTest` 設資產標 `UploadAsset`題會變更為「NewAsset」。

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

此外，您也可以使用參數，從預先定義的套裝或發佈者，從預設組態移除測 `exclude` 試。 請注意，您也必須指定測試的套裝名稱和實際名稱(而非測試C `lass` 名稱)。 您可以在測試類的屬性中 `name` 找到測試名稱。 在下列範例中，會從 `CreatePageTreeTest` toughday套 `UploadAsset`裝中移除（已命名）測試。

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

Tough Day 2可在下列其中一種模式中執行：正 **常** 和 **恆定載荷**。

正常 **運行模** 式有兩個參數：

* `concurrency` -並發表示Tough Day 2為測試執行而建立的線程數。 在這些線程上，將執行測試，直到持續時間已用完或不再執行測試為止。

* `waittime` -同一線程上兩個連續測試執行之間的等待時間。 值必須以毫秒錶示。

以下示例說明如何使用命令行添加參數：

```xml
java -jar toughday2.jar --host=localhost --add CreateAssetTreeTest --runmode=normal concurrency=20
```

或者，使用yaml配置檔案：

```xml
runmode:
  type : normal
  waittime : 300
  concurrency : 200
```

恆 **定負載運行模式** ，通過生成恆定數量的啟動測試執行而不是恆定數量的線程，不同於正常運行模式。 可以使用具有相同名稱的運行模式參數來設定載荷。

### 測試選擇 {#test-selection}

測試選擇過程對於兩種運行模式都相同，其步驟如下：所有測試都有 `weight` 一個屬性，它決定了線程中執行的可能性。 例如，如果我們有兩項測試，一項是5，另一項是10，後者執行的可能性是前者的2倍。

此外，測試可以有 `count` 一個屬性，可將執行數限制為指定數目。 通過此數字後，將不再執行測試。 所有已執行的測試例項都會依設定完成執行。 以下示例說明如何在命令行或通過使用yaml配置檔案添加這些參數。

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
>由於並行執行，實際測試執行數將不完全與參數中設定的量相 `count` 同。 期望偏差與運行線程數成比例(由控 `concurrency parameter`制)。

### 排練 {#dry-run}

乾式執行會剖析所有指定的輸入（命令列參數或組態檔），並將其與預設值合併，然後輸出結果。 它不執行任何測試。

```xml
java -jar toughday2.jar --host=localhost --suite=toughday --add CreatePageTreeTest --dryrun=true
```

## 輸出 {#output}

Tough Day 2輸出測試量度和記錄檔。 如需詳細資訊，請閱讀下列章節。

### 測試量度 {#test-metrics}

艱難的第2天目前報告9個可供您評估的測試量度。 含*符號 **的量度** ，只有在成功執行後才會報告：

| **名稱** | **說明** |
|---|---|
| 時間戳記 | 上次完成測試執行的時間戳記。 |
| 已通過 | 成功執行的次數。 |
| 已失敗 | 失敗的執行數。 |
| 最小值* | 測試執行的最短持續時間。 |
| 最大值* | 測試執行的最長持續時間。 |
| 中等* | 計算所有測試執行的中值持續時間。 |
| 平均* | 計算所有測試執行的平均持續時間。 |
| StdDev* | 標準差。 |
| 90p* | 90個百分點。 |
| 99p* | 99個百分點。 |
| 99.9p* | 99.9個百分點。 |
| 實際吞吐量* | 執行次數除以已用執行時間。 |

這些量度是在發佈者的協助下編寫，而發佈者可隨參數 `add` 新增（類似於新增測試）。 目前有兩種選擇：

* **CSVPublisher** —— 輸出為CSV檔案。
* **ConsolePublisher** —— 輸出顯示在控制台中。

依預設，會啟用兩個發佈者。

此外，報表量度有兩種模式：

* 簡 **單發佈模式** -報告從執行開始到發佈點的結果。
* 間隔 **發佈模式** -在指定的時間範圍內報告結果。 您可以使用間隔發佈模式參 **數來設** 定時間範圍。

以下示例說明如何在命 `intervals` 令行或通過使用yaml配置檔案配置參數。

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

Tough Day 2會在您執行Tough Day 2時所在的目錄中建立記錄檔資料夾。 此資料夾包含兩種記錄檔類型：

* **toughday.log**:包含與應用程式狀態、調試資訊和全局消息相關的消息。
* **toughday_&lt;testname>.log**:與指定測試相關的訊息。

不會覆寫記錄檔，後續執行會將訊息附加至現有記錄檔。 記錄檔有數個層級，如需詳細資訊，請參閱 ` [loglevel parameter](/help/sites-developing/tough-day.md#global-parameters)`。

#### 範例使用 {#example-usage}

#### 已知問題 {#known-issues}

[取得檔案](assets/toughday-6_1.jar)
