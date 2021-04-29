---
title: 報告
seo-title: 報告
description: 瞭解如何在中使用報告AEM。
seo-description: 瞭解如何在中使用報告AEM。
uuid: eee4befd-5fa9-4ebc-8eea-56e1534a6b9b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 7e2b30a3-75ff-4735-8038-5c5391ac36f3
docset: aem65
exl-id: 2a0bf59d-8829-4142-9cb4-dcef90f53ae9
translation-type: tm+mt
source-git-commit: 429f3ee859477fb38938fd6b9706c8006623eb03
workflow-type: tm+mt
source-wordcount: '2815'
ht-degree: 4%

---

# 報告 {#reporting}

為協助您監控和分析執行個體的狀態，AEM請提供一組預設報表，可針對個別需求進行設定：

* [元件報表](#component-report)
* [磁碟使用情況](#disk-usage)
* [運行狀況檢查](#health-check)
* [頁面活動報表](#page-activity-report)
* [使用者產生的內容報表](#user-generated-content-report)
* [使用者報表](#user-report)
* [工作流程例項報表](#workflow-instance-report)
* [工作流程報表](#workflow-report)

>[!NOTE]
>
>這些報表僅適用於傳統UI。 有關現代UI中的系統監視和報告，請參閱[操作儀表板。](/help/sites-administering/operations-dashboard.md)

所有報告都可從&#x200B;**工具**&#x200B;控制台訪問。 在左窗格中選擇&#x200B;**報表**，然後按兩下右窗格中的必要報表，以開啟報表供檢視和／或設定。

您也可以從&#x200B;**Tools**&#x200B;控制台建立新的報表例項。 在左窗格中選擇&#x200B;**報表**，然後選擇&#x200B;**新建……**。 定義&#x200B;**Title**&#x200B;和&#x200B;**Name**，選擇所需的報表類型，然後按一下&#x200B;**Create**。 您的新報表例項會出現在清單中。 按兩下此按鈕以開啟，然後從sidekick拖曳元件以建立第一欄並啟動報表定義。

>[!NOTE]
>
>除了現成可用AEM的標準報表外，您還可以[開發您自己的（全新）報表](/help/sites-developing/dev-reports.md)。

## 報表自訂的基本概念{#the-basics-of-report-customization}

報表有多種格式。 下列報表都使用可自訂的欄，如下列各節所述：

* [元件報表](#component-report)
* [頁面活動報表](#page-activity-report)
* [使用者產生的內容報表](#user-generated-content-report)
* [使用者報表](#user-report)
* [工作流程例項報表](#workflow-instance-report)

>[!NOTE]
>
>下列各報表有其專屬的格式和自訂功能：
>
>
>* [Health ](#health-check) Checks使用選擇欄位指定要報告的資料。
>* [Disk ](#disk-usage) Usage使用連結深入鑽研儲存庫結構。
>* [工作](/help/sites-administering/reporting.md#workflow-report) 流程報表概述執行個體上執行的工作流程。

>
>
因此，列配置的下列過程不適用。 如需詳細資訊，請參閱個別報表的說明。

### 選擇並定位資料列{#selecting-and-positioning-the-data-columns}

欄可以新增至標準或自訂的任何報表、重新放置在報表上或從報表中移除。

sidekick的&#x200B;**元件**&#x200B;標籤（可在報表頁面上使用）會列出所有可選為欄的資料類別。

要更改資料選擇：

* 若要新增欄，請將必要元件從sidekick拖放至您要的位置

   * 綠色勾號會指出位置有效的時間，而一對箭頭會指出位置的確切位置
   * 紅色的no-go符號會指出位置無效

* 若要移動欄，請按一下標題，按住並拖曳至新位置
* 若要移除欄，請按一下欄標題，按住並拖曳至報表標題區域（紅色減號會指出位置無效）;釋放滑鼠按鈕，「刪除元件」對話框將請求確認您確實要刪除該列。

### 欄下拉式功能表{#column-drop-down-menu}

報表中的每一欄都有下拉式功能表。 當滑鼠游標移動至欄標題儲存格時，這會變為可見。

箭頭將出現在標題單元格的最右側（不要與標題文本右側的箭頭頭混淆，箭頭頭指示[當前排序機制](#sorting-the-data)）。

![reportcolumnsort](assets/reportcolumnsort.png)

功能表上可用的選項將視欄的設定而定（如在專案開發期間所做），任何無效的選項都會變灰。

### 對資料{#sorting-the-data}排序

資料可依特定欄來排序：

* 按一下適當的欄標題；排序將在遞增和遞減之間切換，在標題文字旁的箭頭標題指示
* 使用[column的下拉菜單](#column-drop-down-menu)具體選擇&#x200B;**升序排序**&#x200B;或&#x200B;**降序排序**;此外，標題文字旁的箭頭將會指出

### 組和當前資料圖表{#groups-and-the-current-data-chart}

在適當的列上，可以從[列的下拉菜單](#column-drop-down-menu)中選擇&#x200B;**按此列分組**。 這會根據該欄內的每個不同值來分組資料。 您可以選取多個要分組的欄。 當欄中的資料不適當時，此選項會變灰；例如，每個項目都是不同且唯一的，因此不能形成任何群組，例如使用者報表的「使用者ID」欄。

在至少對一列進行分組後，將根據此分組生成&#x200B;**當前資料**&#x200B;的餅圖。 如果將多欄分組，圖表上也會指出此點。

![reportuser](assets/reportuser.png)

將游標移到圓形圖上方，將顯示適當區段的匯總值。 這使用當前為列定義的聚合；例如，計數、最小值、平均值等。

### 篩選器和聚合{#filters-and-aggregates}

在適當的欄上，您也可以從[欄的下拉式選單](#column-drop-down-menu)設定&#x200B;**篩選設定**&#x200B;和／或&#x200B;**匯總**。

#### 濾鏡 {#filters}

「篩選設定」可讓您指定要顯示的項目標準。 可用的運算子有：

* `contains`
* `equals`

![reportfilter](assets/reportfilter.png)

若要設定篩選：

1. 從下拉式清單中選取您要的運算子。
1. 輸入要篩選的文本。
1. 按一下&#x200B;**Apply**。

停用篩選：

1. 移除篩選文字。
1. 按一下&#x200B;**Apply**。

#### 聚合{#aggregates}

您也可以選擇聚合方法（這些方法可能因所選列而異）:

![reportagregate](assets/reportaggregate.png)

### 欄屬性 {#column-properties}

只有在[使用者報表](#user-report)中使用了[一般欄](#generic-column)時，此選項才可用。

### 歷史資料 {#historic-data}

您可在&#x200B;**歷史資料**&#x200B;下查看資料隨時間變化的圖表。 這是從以常規間隔拍攝的快照派生的。

資料如下：

* 收集者（若有）是第一個排序的欄，否則是第一個（非分組）欄
* 依適當欄分組

可產生報表：

1. 在所需列上設定&#x200B;**分組**。
1. **編** 輯配置以定義快照的製作頻率；每小時或每日。
1. **完成……** 啟動快照集合的定義。

   左上角的紅色／綠色滑桿按鈕會指示正在收集快照。

結果圖表顯示在右下角：

![reporttrends](assets/reporttrends.png)

資料收集開始後，您可以選取：

* **時段**

   您可以選取要顯示之報表資料的開始和結束日期。

* **間隔**

   可以選取月、周、日、小時作為報表的比例和匯總。

   例如，如果每日快照可用於2011年2月：

   * 如果間隔設定為`Day`，則每個快照在圖表中顯示為一個值。
   * 如果間隔設定為`Month`，則二月的所有快照都將聚合到單個值中（在圖表中顯示為單個「點」）。

選擇您的需求，然後按一下&#x200B;**Go**，將需求套用至報表。 要在建立更多快照後更新顯示，請再次按一下&#x200B;**Go**。

![chlimage_1-43](assets/chlimage_1-43.png)

正在收集快照時，您可以：

* 使用&#x200B;**完成……**，重新初始化系列。

   **完成** 「凍結」報表的結構（即指派給報表的欄，以及分組、排序、篩選等欄）和啟動快照。

* 開啟&#x200B;**編輯**&#x200B;對話框以選擇&#x200B;**無資料快照**&#x200B;以終止收集，直到需要。

   **Editonly** 可切換快照的拍攝。如果拍攝快照再次被開啟，則會使用報告上次完成時的狀態來拍攝更多快照。

>[!NOTE]
>
>快照儲存在`/var/reports/...`下，其中路徑的其餘部分將鏡像各報告的路徑，並在報告完成時建立ID。
>
>
>如果完全確定不再需要這些實例，則可以手動清除舊快照。

>[!NOTE]
>
>預先設定的報表不需要耗費大量的效能，但仍建議您在生產環境中使用每日快照。 如果可能，請在您網站上活動不多時，於一天中的某一時間執行這些每日快照；這可以使用&#x200B;**Day CQ Reporting Configuration**&#x200B;的`Daily snapshots (repconf.hourofday)`參數定義；如需如何設定此設定的詳細資訊，請參閱[OSGI Configuration](/help/sites-deploying/configuring-osgi.md)。

#### 顯示限制{#display-limits}

歷史資料報表也可能因可設定的限制而在外觀上稍有變更，因為可根據所選時段的結果數目進行設定。

每條水準線都稱為系列（並對應於圖表圖例中的條目），每條垂直點列代表聚合快照。

![chlimage_1-44](assets/chlimage_1-44.png)

要在較長的時間段內保持圖表清潔，可以設定限制。 對於標準報表，這些報表包括：

* 水準系列——預設和系統最大值為`9`

* 垂直聚合快照——預設值為`35`（每個水準系列）

因此，當超過（適當）限制時：

* 點不會顯示
* 歷史資料圖表的圖例可能顯示與當前資料圖表不同的條目數

![chlimage_1-45](assets/chlimage_1-45.png)

自訂報表也可顯示所有系列的&#x200B;**Total**&#x200B;值。 這會顯示為系列（圖例中的水準線和條目）。

>[!NOTE]
>
>對於自訂報表，可以以不同方式設定限制。

### 編輯（報告）{#edit-report}

**編輯**&#x200B;按鈕會開啟「編輯報表&#x200B;**」對話方塊。**

這是定義[Historic data](#historic-data)收集快照時段的一個位置，但也可以定義各種其他設定：

![reportedit](assets/reportedit.png)

* **標題**

   您可以定義自己的標題。

* **說明**

   您可以定義自己的說明。

* **根路徑** (*僅對特定報表啟用*)

   使用此選項可將報告限制在儲存庫的（子）部分。

* **報表處理**

   * **自動重新整理資料**

      每次您更新報表定義時，報表資料都會重新整理。

   * **手動重新整理資料**

      此選項可用於防止當有大量資料時，由自動刷新操作引起的延遲。

      選取此選項表示報表設定的任何方面變更時，必須手動重新整理報表資料。 這也表示，當您變更設定的任何方面時，報表表格都會被遮蔽掉。

      選擇此選項後，將顯示&#x200B;**[載入資料](#load-data)**&#x200B;按鈕（在報告的&#x200B;**編輯**&#x200B;旁）。 **載入** 資料將會載入資料並重新整理顯示的報表資料。

* **快**
照可以定義快照的製作頻率；每日、每小時或完全不是。

### 載入資料 {#load-data}

**從**[&#x200B;編輯&#x200B;](#edit-report)**中選擇了**&#x200B;手動刷新資料&#x200B;**時，載入資料**&#x200B;按鈕才顯示。

![chlimage_1-46](assets/chlimage_1-46.png)

按一下&#x200B;**載入資料**&#x200B;將重新載入資料並更新顯示的報表。

選擇手動刷新資料表示：

1. 一旦變更報表設定，報表資料的表格就會被遮蔽掉。

   例如，如果更改列的排序機制，則不會顯示資料。

1. 如果您希望再次顯示報表資料，則需按一下「載入資料&#x200B;**」以重新載入資料。**

### 完成（報告）{#finish-report}

當您&#x200B;**完成**&#x200B;報表時：

* 截至該時間點的報告定義&#x200B;*將用於建立快照（之後，您可以繼續處理報告定義，因為它與快照分開）。*
* 將刪除任何現有快照。
* 會為[Historic data](#historic-data)收集新快照。

使用此對話方塊，您可以定義或更新產生報表的標題和說明。

![reportfinish](assets/reportfinish.png)

## 報表類型{#report-types}

### 元件報表 {#component-report}

元件報表會提供您網站使用元件的相關資訊。

[有關以下](#selecting-and-positioning-the-data-columns) 資訊的列：

* 作者
* 元件路徑
* 元件類型
* 上次修改時間
* 頁面

這表示您可以看到，例如：

* 哪些元件用在何處。

   例如，在測試時很實用。

* 特定元件的例項分佈方式。

   如果特定頁面(即&quot;heavy pages&quot;)遇到效能問題。

* 識別網站中頻繁／較不頻繁的變更。
* 瞭解頁面內容如何隨著時間發展。

所有元件均隨附於產品標準和專案。 使用&#x200B;**編輯**&#x200B;對話方塊，使用者也可以設定定義報表起點的&#x200B;**根路徑** —— 該根目錄下的所有元件皆視為報表。

![報](assets/reportcomponent.png) ![告元件整合](assets/reportcompentall.png)

### 磁碟使用情況 {#disk-usage}

磁碟使用情況報告顯示有關儲存在儲存庫中的資料的資訊。

報告在儲存庫的根(/)中啟動；通過按一下特定的分支，您可以在儲存庫內深入查看（當前路徑將反映在報告標題中）。

![reportdiskusage](assets/reportdiskusage.png)

### 運行狀況檢查{#health-check}

此報表會分析目前的請求記錄：

`<cq-installation-dir>/crx-quickstart/logs/request.log`
以協助您識別指定時段內最昂貴的請求。

若要產生報表，您可以指定：

* **期間（小時）**

   要分析的小時數（過去）。

   預設: `24`

* **最大值. 結果**

   輸出行數上限。

   預設: `50`

* **最大值. 請求**

   要分析的最大請求數。

   預設值：`-1`（全部）

* **電子郵件地址**

   傳送結果至電子郵件地址。

   可選；預設值：空白

* **每日運行於(hh:mm)**

   指定報表每日自動執行的時間。

   可選；預設值：空白

![reportthealth](assets/reporthealth.png)

### 頁面活動報表 {#page-activity-report}

頁面活動報表會列出頁面及其上所執行的動作。

[有關以下](#selecting-and-positioning-the-data-columns) 資訊的列：

* 頁面
* 時間
* 類型
* 使用者

表示您可以監控：

* 最新修改。
* 在特定頁面上工作的作者。
* 最近未修改的頁面，因此可能需要採取行動。
* 最常／最不常變更的頁面。
* 最多／最不活躍的使用者。

頁面活動報表會從稽核記錄檔中擷取其所有資訊。 預設情況下，根路徑配置為`/var/audit/com.day.cq.wcm.core.page`的審計日誌。

![reportpageactivity](assets/reportpageactivity.png)

### 使用者產生的內容報表 {#user-generated-content-report}

本報告提供使用者產生內容的相關資訊；無論是評論、評分還是論壇。

[有關以下](#selecting-and-positioning-the-data-columns) 資訊的列：

* 日期
* IP 位址
* 頁面
* 反向連結
* 類型
* 使用者識別碼

允許您：

* 瞭解哪些頁面收到的留言最多。
* 取得特定網站訪客離開的所有留言的概述，可能是問題相關的。
* 判斷新內容是否在頁面上發表意見時，透過監控來引發意見。

![reportusercontent](assets/reportusercontent.png)

### 使用者報表 {#user-report}

此報告提供所有已註冊帳戶及／或設定檔的使用者的相關資訊；這可包括組織內的作者和外部訪客。

[有關](#selecting-and-positioning-the-data-columns) （如果可用）的資訊欄：

* 年齡
* 國家/地區
* 網域
* 電子郵件
* 姓氏
* 性別
* [通用](#generic-column)
* 名字
* 資訊
* 興趣
* 語言
* NTLM 雜湊碼
* 使用者 ID

允許您：

* 查看您使用者的人口分佈。
* 報告您已新增至描述檔的自訂欄位。

![reportusermanced](assets/reportusercanned.png)

#### 一般欄{#generic-column}

**Generic**&#x200B;欄位可在「使用者報表」中使用，以便您存取自訂資訊，通常是從[使用者描述檔](/help/sites-administering/identity-management.md#profiles-and-user-accounts)存取；例如，[「我的最愛顏色」，如「新增欄位至描述檔定義」下的「我的最愛顏色」。](/help/sites-administering/identity-management.md#adding-fields-to-the-profile-definition)

當您執行下列任一操作時，「一般」(Generic)欄對話方塊將會開啟：

* 將「一般」元件從側腳拖曳至報表。
* 為現有的「通用」列選擇「列屬性」。

![reportusrgenercorml](assets/reportusrgenericcolm.png)

在&#x200B;**Definitions**&#x200B;標籤中，您可以定義：

* **標題**

   您自己的一般欄標題。

* **屬性**

   儲存在儲存庫中的屬性名稱，通常位於用戶的配置檔案中。

* **路徑**

   通常屬性取自`profile`。

* **類型**

   從`String`、`Number`、`Integer`、`Date`中選擇欄位類型。

* **預設聚合**

   如果列在至少具有一個分組列的報告中取消分組，則預設情況下會定義所使用的聚合。 從`Count`、`Minimum`、`Average`、`Maximum`、`Sum`中選擇所需的聚合。

   例如，`String`欄位的&#x200B;*計數*&#x200B;表示在匯總狀態中，會顯示該欄的不同`String`值數。

在&#x200B;**Extended**&#x200B;標籤中，您也可以定義可用的集合和篩選器：

![reportregenericcolmextented](assets/reportusrgenericcolmextented.png)

### 工作流程例項報表 {#workflow-instance-report}

這可提供您簡明的概觀，提供有關執行和完成的個別工作流程例項的資訊。

[有關以下](#selecting-and-positioning-the-data-columns) 資訊的列：

* 完成
* 持續時間
* 發起人
* 模型
* 裝載
* 已開始
* 狀態

意思是您可以：

* 監控工作流程的平均持續時間；如果這種情況經常發生，則會反白顯示工作流程的問題。

![報告流量](assets/reportworkflowintance.png)

### 工作流程報表{#workflow-report}

這可提供執行個體上執行之工作流程的主要統計資料。

![reportworkflow](assets/reportworkflow.png)

## 在發佈環境中使用報表{#using-reports-in-a-publish-environment}

在您根據特定需求設定報表後，您就可以啟動報表，將組態傳輸至發佈環境。

>[!CAUTION]
>
>如果您想要發佈環境的&#x200B;**歷史資料**，請在啟動頁面之前，先&#x200B;**完成作者環境的報表。**

然後，您就可在

`/etc/reports`

例如，「使用者產生的內容」報表可在下列位置找到：

`http://localhost:4503/etc/reports/ugcreport.html`

現在會報告從發佈環境收集到的資料。

由於發佈環境中不允許任何報表配置，因此&#x200B;**Edit**&#x200B;和&#x200B;**Finish**&#x200B;按鈕不可用。 但是，如果正在收集快照，則可以為&#x200B;**歷史資料**&#x200B;報告選擇&#x200B;**Period**&#x200B;和&#x200B;**Interval**。

![reportsucppublish](assets/reportsucgpublish.png)

>[!CAUTION]
>
>存取這些報告可能是安全問題；因此，我們建議您配置Dispatcher，以便`/etc/reports`不適用於外部訪客。 如需詳細資訊，請參閱[安全性檢查清單](security-checklist.md)。

## 運行報告{#permissions-needed-for-running-reports}所需的權限

所需的權限取決於操作：

* 報表資料基本上是使用目前使用者的權限來收集。
* 歷史資料會使用完成報表的使用者權限來收集。

在標準安AEM裝中，報表預設了下列權限：

* **使用者報表**

   `user administrators` -讀取和寫入

* **頁面活動報表**

   `contributors` -讀取和寫入

* **元件報表**

   `contributors` -讀取和寫入

* **使用者產生的內容報表**

   `contributors` -讀取和寫入

* **工作流程例項報表**

   `workflow-users` -讀取和寫入

`administrators`群組的所有成員都具有建立新報表的必要權限。
