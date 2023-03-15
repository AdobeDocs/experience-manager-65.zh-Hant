---
title: 報告
seo-title: Reporting
description: 了解如何在AEM中使用報表。
seo-description: Learn how to work with Reporting in AEM.
uuid: eee4befd-5fa9-4ebc-8eea-56e1534a6b9b
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 7e2b30a3-75ff-4735-8038-5c5391ac36f3
docset: aem65
exl-id: 2a0bf59d-8829-4142-9cb4-dcef90f53ae9
source-git-commit: 429f3ee859477fb38938fd6b9706c8006623eb03
workflow-type: tm+mt
source-wordcount: '2806'
ht-degree: 4%

---

# 報告 {#reporting}

為協助您監視和分析執行個體的狀態，AEM提供一系列預設報表，可依您的個別需求進行設定：

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
>這些報表僅可在傳統UI中使用。 若要在現代UI中進行系統監控和報告，請參閱 [操作儀表板。](/help/sites-administering/operations-dashboard.md)

所有報表均可從 **工具** 控制台。 選擇 **報表** 在左窗格中，按兩下右窗格中的所需報表以開啟它以供檢視和/或設定。

報表的新例項也可從 **工具** 控制台。 選擇 **報表** 在左窗格中， **新……** 的上界。 定義 **標題** 和 **名稱**，選取您需要的報表類型，然後按一下 **建立**. 您的新報表例項會出現在清單中。 連按兩下以開啟，然後從sidekick拖曳元件以建立第一欄並啟動報表定義。

>[!NOTE]
>
>除了現成可用的標準AEM報表外，您還可以 [開發您自己的（全新）報表](/help/sites-developing/dev-reports.md).

## 報表自訂基本概念 {#the-basics-of-report-customization}

可用的報表格式多種多樣。 以下報告均使用可自訂的欄，如下列各節所述：

* [元件報表](#component-report)
* [頁面活動報表](#page-activity-report)
* [使用者產生的內容報表](#user-generated-content-report)
* [使用者報表](#user-report)
* [工作流程例項報表](#workflow-instance-report)

>[!NOTE]
>
>下列各報表有各自的格式和自訂：
>
>
>* [運行狀況檢查](#health-check) 使用選擇欄位來指定要報告的資料。
>* [磁碟使用情況](#disk-usage) 使用連結來深入鑽研儲存庫結構。
>* [工作流程報表](/help/sites-administering/reporting.md#workflow-report) 提供執行個體上執行之工作流程的概觀。
>
>因此，列配置的以下過程不適用。 如需個別報表的詳細資訊，請參閱其說明。

### 選擇和定位資料列 {#selecting-and-positioning-the-data-columns}

欄可以新增至任何報表（標準或自訂）、在報表上重新定位或從報表中移除。

此 **元件** sidekick的索引標籤（可在報表頁面上使用）會列出所有可選為欄的資料類別。

要更改資料選擇：

* 若要新增欄，請從sidekick拖曳必要元件，並放置您想要的位置

   * 綠色勾號會指出位置有效的時間，而一對箭頭會指出其確切放置位置
   * 一個紅色的禁止進入符號將指示位置無效

* 要移動列，請按一下標題，按住並拖動到新位置
* 若要移除欄，請按一下欄標題，按住並拖曳至報表標題區域（紅色減號表示位置無效）;釋放滑鼠按鈕，「刪除元件」對話框將請求確認您確實要刪除該列。

### 欄下拉式功能表 {#column-drop-down-menu}

報表中的每一欄都有下拉式功能表。 當滑鼠游標移至欄標題儲存格上方時，這會顯示。

標題儲存格的最右側會顯示箭頭標題(請勿與標題文字右側緊鄰的箭頭標題混淆，箭頭標題會指出 [當前排序機制](#sorting-the-data))。

![reportcolumnsort](assets/reportcolumnsort.png)

功能表上可用的選項取決於欄的設定（如專案開發期間所做），任何無效選項都會呈現灰色。

### 排序資料 {#sorting-the-data}

資料可依下列其中一項，根據特定欄排序：

* 按一下相應的列標題；排序會在遞增和遞減之間切換，由標題文字旁邊的箭頭標題所指示
* 使用 [欄的下拉式功能表](#column-drop-down-menu) 要特別選擇 **遞增排序** 或 **降序排序**;標題文字旁會加上緊鄰的箭頭標題

### 群組與目前的資料圖表 {#groups-and-the-current-data-chart}

在適當的欄上，您可以選取 **按此列分組** 從 [欄的下拉式功能表](#column-drop-down-menu). 這會根據該欄內每個不同的值來分組資料。 可以選擇多個要分組的列。 當欄中的資料不適當時，選項會變灰；亦即每個項目都是不同且唯一的，因此無法形成任何群組，例如使用者報表的「使用者ID」欄。

將至少一列分組後，將 **目前的資料** 會根據此群組產生。 如果將多個欄分組，圖表也會指出這一點。

![reportuser](assets/reportuser.png)

將游標移至圓形圖上方，會顯示適當區段的匯總值。 這會使用目前為欄定義的匯總；例如，計數、最小、平均等。

### 篩選器和匯總 {#filters-and-aggregates}

在適當的欄上，您也可以設定 **篩選設定** 和/或 **匯總** 從 [欄的下拉式功能表](#column-drop-down-menu).

#### 篩選條件 {#filters}

「篩選設定」可讓您指定要顯示之項目的條件。 可用的運算子為：

* `contains`
* `equals`

![reportfilter](assets/reportfilter.png)

若要設定篩選器：

1. 從下拉式清單中選取您要的運算子。
1. 輸入要篩選的文字。
1. 按一下 **套用**.

停用篩選器：

1. 移除篩選文字。
1. 按一下 **套用**.

#### 匯總 {#aggregates}

您也可以選取匯總方法（這些方法可能會因所選欄而異）:

![reportagregate](assets/reportaggregate.png)

### 欄屬性 {#column-properties}

此選項僅在 [一般欄](#generic-column) 已用於 [使用者報表](#user-report).

### 歷史資料 {#historic-data}

您可在下方查看資料隨時間變更的圖表 **歷史資料**. 這是從以常規間隔拍攝的快照派生而來。

資料為：

* 收集者（如果可用）是第一個排序的欄，否則是第一個（非分組）欄
* 依適當欄分組

可產生報表：

1. 設定 **分組** 填入必填欄。
1. **編輯** 定義快照製作頻率的配置；每小時或每日。
1. **完成……** 啟動快照集合的定義。

   左上角的紅色/綠色滑桿按鈕指示何時收集快照。

產生的圖表顯示在右下方：

![報告趨勢](assets/reporttrends.png)

資料收集一開始，您可以選取：

* **時段**

   您可以選取要顯示報表資料的開始日期和結束日期。

* **間隔**

   可以選取月、周、日、小時，以計算報表的規模和匯總。

   例如，如果每日快照可用於2011年2月：

   * 如果間隔設定為 `Day`，則每個快照在圖表中會顯示為單一值。
   * 如果間隔設定為 `Month`，則2月的所有快照都會匯總為單一值（在圖表中顯示為單一「點」）。

選取您的需求，然後按一下 **開始** 來套用至報表。 要在建立更多快照後更新顯示，請按一下 **開始** 。

![chlimage_1-43](assets/chlimage_1-43.png)

收集快照時，您可以：

* 使用 **完成……** 重新初始化集合。

   **完成** 「凍結」報表的結構（即指派給報表的欄，以及經過分組、排序、篩選等） 開始拍攝快照。

* 開啟 **編輯** 對話框 **無資料快照** 終止收集，直到需要。

   **編輯** 僅切換快照的拍攝開啟或關閉。 如果拍攝快照重新開啟，則會使用上次完成時的報表狀態來拍攝更多快照。

>[!NOTE]
>
>快照儲存在 `/var/reports/...` 其中，路徑的其餘部分反映完成報告時建立的各報表和ID的路徑。
>
>
>如果您完全確定不再需要這些實例，則可以手動清除舊快照。

>[!NOTE]
>
>預先設定的報表不需要大量效能，但仍建議在生產環境中使用每日快照。 如果可以在網站上活動不多時，在一天中的某個時間運行這些每日快照；這可以用 `Daily snapshots (repconf.hourofday)` 參數 **Day CQ報表設定**;請參閱 [OSGI設定](/help/sites-deploying/configuring-osgi.md) 以取得如何設定此項目的詳細資訊。

#### 顯示限制 {#display-limits}

歷史資料報表也可能會因為可設定的限制而在外觀上稍微變更，根據所選期間的結果數量。

每條水準線都稱為系列（並對應至圖表圖例中的項目），每個垂直的點列代表匯總的快照。

![chlimage_1-44](assets/chlimage_1-44.png)

若要在較長的時段內保持圖表乾淨，可設定限制。 對於標準報表，以下是：

* 水準系列 — 預設值和系統最大值都為 `9`

* 垂直聚合快照 — 預設值 `35` （每個水準系列）

因此，當超出（適當）限制時：

* 不會顯示點
* 歷史資料圖表的圖例可能會顯示與當前資料圖表不同的條目數

![chlimage_1-45](assets/chlimage_1-45.png)

自訂報表也可顯示 **總計** 值。 這顯示為系列（圖例中的水準線條和條目）。

>[!NOTE]
>
>對於自訂報表，上限的設定方式不同。

### 編輯（報表） {#edit-report}

此 **編輯** 按鈕開啟 **編輯報表** 對話。

這是收集快照的時段 [歷史資料](#historic-data) 已定義，但也可定義各種其他設定：

![reportedit](assets/reportedit.png)

* **標題**

   您可以定義自己的標題。

* **說明**

   您可以定義自己的說明。

* **根路徑** (*僅對某些報表有效*)

   使用此功能可將報表限制在存放庫的（子）區段。

* **報表處理**

   * **自動重新整理資料**

      每次更新報表定義時，都會重新整理報表資料。

   * **手動重新整理資料**

      此選項可用來防止當有大量資料時，自動重新整理作業所造成的延遲。

      若選取此選項，表示報表設定的任何方面變更時，必須手動重新整理報表資料。 這也表示當您變更設定的任何方面時，報表表格就會變成空白。

      選取此選項時， **[載入資料](#load-data)** 按鈕(在 **編輯** )。 **載入資料** 會載入資料並重新整理顯示的報表資料。

* **快照**
您可以定義快照的製作頻率；每日、每小時或完全不是。

### 載入資料 {#load-data}

此 **載入資料** 按鈕只有在 **手動重新整理資料** 已從 **[編輯](#edit-report)**.

![chlimage_1-46](assets/chlimage_1-46.png)

按一下 **載入資料** 會重新載入資料並更新顯示的報表。

選擇手動刷新資料表示：

1. 變更報表設定後，報表資料表就會變成空白。

   例如，如果您變更欄的排序機制，則不會顯示資料。

1. 如果要再次顯示報表資料，您必須按一下 **載入資料** 重新載入資料。

### 完成（報告） {#finish-report}

當您 **完成** 報告：

* 報表定義 *就是那個時間點* 將用於拍攝快照（之後，您可以繼續處理報告定義，因為它將與快照分開）。
* 將刪除任何現有快照。
* 會為 [歷史資料](#historic-data).

使用此對話方塊，您可以為產生的報表定義或更新自己的標題和說明。

![reportfinish](assets/reportfinish.png)

## 報表類型 {#report-types}

### 元件報表 {#component-report}

元件報表可提供您的網站如何使用元件的相關資訊。

[資訊欄](#selecting-and-positioning-the-data-columns) 關於：

* 作者
* 元件路徑
* 元件類型
* 上次修改時間
* Page

這表示您可以看到，例如：

* 哪些元件用於何處。

   例如，在測試時很實用。

* 如何分配特定元件的例項。

   如果特定頁面(即&quot;heavy pages&quot;)遇到效能問題。

* 識別網站中頻繁/較不頻繁的變更。
* 查看頁面內容在一段時間內的發展情形。

所有元件均包含在內，產品標準和專案專屬元件。 使用 **編輯** 對話方塊使用者也可以設定 **根路徑** 定義報表起始點的參數 — 該根下的所有元件都會被視為報表。

![reportcomponent](assets/reportcomponent.png) ![報告簡編](assets/reportcompentall.png)

### 磁碟使用情況 {#disk-usage}

磁碟使用情況報表顯示儲存在儲存庫中的資料的相關資訊。

報表從存放庫的根(/)開始；按一下特定分支，即可深入檢視存放庫內部（目前路徑會反映在報表標題中）。

![reportdiskusage](assets/reportdiskusage.png)

### 運行狀況檢查 {#health-check}

此報表會分析目前的請求記錄：

`<cq-installation-dir>/crx-quickstart/logs/request.log`
協助您識別指定期間內最昂貴的請求。

若要產生報表，您可以指定：

* **期間（小時）**

   要分析的小時數（過去）。

   預設: `24`

* **最大值. 結果**

   最大輸出行數。

   預設: `50`

* **最大值. 請求**

   要分析的最大請求數。

   預設值： `-1` (all)

* **電子郵件地址**

   將結果傳送至電子郵件地址。

   可選；預設值：空白

* **每日運行時間(hh:mm)**

   指定報表每天自動執行的時間。

   可選；預設值：空白

![reporthealth](assets/reporthealth.png)

### 頁面活動報表 {#page-activity-report}

頁面活動報表會列出頁面，以及在頁面上執行的動作。

[資訊欄](#selecting-and-positioning-the-data-columns) 關於：

* Page
* 時間
* 類型
* 使用者

表示您可以監視：

* 最新修改。
* 在特定頁面上工作的作者。
* 最近未修改的頁面，因此可能需要採取動作。
* 變更次數最多/最少的頁面。
* 最多/最不活躍的使用者。

頁面活動報表會從稽核記錄檔中擷取其所有資訊。 預設情況下，根路徑配置為審核日誌 `/var/audit/com.day.cq.wcm.core.page`.

![reportpageactivity](assets/reportpageactivity.png)

### 使用者產生的內容報表 {#user-generated-content-report}

此報告提供有關用戶生成內容的資訊；無論是評論、評級還是論壇。

[資訊欄](#selecting-and-positioning-the-data-columns) 在：

* 日期
* IP 位址
* Page
* 反向連結
* 類型
* 使用者識別碼

允許您：

* 查看哪些頁面收到的留言最多。
* 取得特定網站訪客離開的所有留言的概述，可能是與問題相關的。
* 在頁面上留言時，透過監控來判斷新內容是否觸發留言。

![reportusercontent](assets/reportusercontent.png)

### 使用者報表 {#user-report}

此報表提供已註冊帳戶和/或設定檔的所有使用者的相關資訊；這可包含組織內的作者和外部訪客。

[資訊欄](#selecting-and-positioning-the-data-columns) （若有）關於：

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

* 查看您的使用者的人口分佈。
* 報告您已新增至設定檔的自訂欄位。

![reportsencated](assets/reportusercanned.png)

#### 一般欄 {#generic-column}

此 **一般** 欄可供使用者報表，以便您存取自訂資訊，通常可從 [使用者設定檔](/help/sites-administering/identity-management.md#profiles-and-user-accounts);例如， [最喜愛的顏色，如在「將欄位添加到配置檔案定義」中詳述](/help/sites-administering/identity-management.md#adding-fields-to-the-profile-definition).

當您執行下列任一操作時，將會開啟「一般」欄對話方塊：

* 將「一般」元件從sidekick拖曳至報表。
* 選擇現有「一般」列的「列屬性」。

![reportusgenercorm](assets/reportusrgenericcolm.png)

從 **定義** 索引標籤來定義：

* **標題**

   一般欄的專屬標題。

* **屬性**

   儲存在存放庫中的屬性名稱，通常位於使用者的設定檔中。

* **路徑**

   通常屬性取自 `profile`.

* **類型**

   從中選擇欄位類型 `String`, `Number`, `Integer`, `Date`.

* **預設匯總**

   這會定義預設使用的匯總（如果在包含至少一個分組列的報告中將該列取消分組）。 從中選擇所需的匯總 `Count`, `Minimum`, `Average`, `Maximum`, `Sum`.

   例如， *計數* a `String` 欄位表示相異的數量 `String` 會針對匯總狀態的欄顯示值。

在 **延伸** 索引標籤，您也可以定義可用的匯總和篩選器：

![reportusgenericcolmextented](assets/reportusrgenericcolmextented.png)

### 工作流程例項報表 {#workflow-instance-report}

這可提供簡潔的概觀，提供執行中和完成之工作流程個別例項的相關資訊。

[資訊欄](#selecting-and-positioning-the-data-columns) 關於：

* 完成
* 持續時間
* 發起人
* 模型
* 裝載
* 已開始
* 狀態

代表您可以：

* 監控工作流程的平均持續時間；如果這會定期發生，可反白標示工作流程的問題。

![reportworkflowinstance](assets/reportworkflowintance.png)

### 工作流程報表 {#workflow-report}

這可提供執行個體上執行之工作流程的關鍵統計資料。

![reportworkflow](assets/reportworkflow.png)

## 在發佈環境中使用報表 {#using-reports-in-a-publish-environment}

將報表設定為符合您的特定需求後，您就可以啟動報表，將設定傳輸至發佈環境。

>[!CAUTION]
>
>如果您想要 **歷史資料** ，則 **完成** 在啟動頁面之前，先報告製作環境。

接著，您即可在

`/etc/reports`

例如，您可在下列位置找到「使用者產生的內容」報表：

`http://localhost:4503/etc/reports/ugcreport.html`

這現在會報告從發佈環境收集到的資料。

由於發佈環境中不允許任何報表設定，因此 **編輯** 和 **完成** 按鈕不可用。 不過，您可以選取 **時段** 和 **間隔** 針對 **歷史資料** 報告是否正在收集快照。

![reportsucpublish](assets/reportsucgpublish.png)

>[!CAUTION]
>
>存取這些報告可能是安全問題；因此，建議您設定Dispatcher，以便 `/etc/reports` 無法供外部訪客使用。 請參閱 [安全性檢查清單](security-checklist.md) 以取得更多詳細資訊。

## 執行報表所需的權限 {#permissions-needed-for-running-reports}

所需的權限取決於動作：

* 報表資料基本上是使用目前使用者的權限收集。
* 系統會使用完成報表之使用者的權限來收集歷史資料。

在標準AEM安裝中，為報表預設了下列權限：

* **使用者報表**

   `user administrators`  — 讀寫

* **頁面活動報表**

   `contributors`  — 讀寫

* **元件報表**

   `contributors`  — 讀寫

* **使用者產生的內容報表**

   `contributors`  — 讀寫

* **工作流程例項報表**

   `workflow-users`  — 讀寫

所有 `administrators` 群組擁有建立新報表的必要權限。
