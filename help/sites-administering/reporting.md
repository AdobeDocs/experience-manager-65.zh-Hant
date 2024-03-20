---
title: 報告
description: 瞭解如何在Adobe Experience Manager (AEM)中使用報表。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: 2a0bf59d-8829-4142-9cb4-dcef90f53ae9
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2782'
ht-degree: 3%

---

# 報告 {#reporting}

為協助您監控及分析執行個體的狀態，Adobe Experience Manager (AEM)提供一系列預設報表，您可依個別需求加以設定：

* [元件報表](#component-report)
* [磁碟使用情況](#disk-usage)
* [健康情況檢查](#health-check)
* [頁面活動報表](#page-activity-report)
* [使用者產生的內容報表](#user-generated-content-report)
* [使用者報表](#user-report)
* [工作流程例項報表](#workflow-instance-report)
* [工作流程報告](#workflow-report)

>[!NOTE]
>
>這些報表只能在Classic UI中使用。 如需新式UI中的系統監控和報告，請參閱 [操作控制面板。](/help/sites-administering/operations-dashboard.md)

所有報表都可從以下位置存取： **工具** 主控台。 選取 **報表** 在左側窗格中，連按兩下右側窗格中的必要報表，以便開啟報表以供檢視、設定或同時開啟兩者。

您也可以從以下專案建立新的報表例項： **工具** 主控台。 選取 **報表** 在左窗格中，然後 **新增……** 工具列中的。 定義 **標題** 和 **名稱**，選取您需要的報表型別，然後按一下 **建立**. 您的新報表例項會出現在清單中。 按兩下以開啟，然後從Sidekick拖曳元件，以便建立第一欄並開始報表定義。

>[!NOTE]
>
>除了可立即使用的標準AEM報表之外，您也可以 [開發您自己的（新）報告](/help/sites-developing/dev-reports.md).

## 報表自訂的基本概念 {#the-basics-of-report-customization}

有多種可用的報表格式。 下列報表都使用可自訂的欄，詳見以下章節：

* [元件報表](#component-report)
* [頁面活動報表](#page-activity-report)
* [使用者產生的內容報表](#user-generated-content-report)
* [使用者報表](#user-report)
* [工作流程例項報表](#workflow-instance-report)

>[!NOTE]
>
>以下各報表有各自的格式和自訂：
>
>
>* [健康情況檢查](#health-check) 使用選取欄位來指定您要報告的資料。
>* [磁碟使用量](#disk-usage) 會使用連結來向下鑽研存放庫結構。
>* [工作流程](/help/sites-administering/reporting.md#workflow-report) 提供執行個體上執行的工作流程概觀。
>
>因此，以下欄配置程式不適用。 如需詳細資訊，請參閱個別報表的說明。

### 選取和定位資料欄 {#selecting-and-positioning-the-data-columns}

欄可新增至任何報表、可在其上重新放置或從中移除，無論是標準報表或自訂報表。

此 **元件** sidekick的索引標籤（可在報告頁面上取得）列出了可選取為欄的所有資料類別。

若要變更資料選取範圍：

* 若要新增欄，請從sidekick拖曳所需的元件，並將它放置在您想要的位置

   * 綠色勾號表示位置何時有效，而一對箭頭則表示位置正好
   * 紅色的no-go符號表示位置無效

* 若要移動欄，請按一下標題，按住，然後拖曳到新位置
* 若要移除欄，請按住欄標題，然後向上拖曳至報表標題區域（紅色減號表示位置無效）。 放開滑鼠鍵，「刪除元件」對話方塊會要求確認您確實要刪除欄。

### 欄下拉式功能表 {#column-drop-down-menu}

報表中的每一欄都有一個下拉式功能表。 當滑鼠游標移至欄標題儲存格上時，此專案會變成可見。

箭頭顯示在標題儲存格的最右側(不要與標題文字右側的箭頭混淆，標題文字指示 [目前的排序機制](#sorting-the-data))。

![reportcolumnsort](assets/reportcolumnsort.png)

功能表上的可用選項取決於欄的設定（如專案開發期間所設定），任何無效選項都會變暗（變灰）。

### 排序資料 {#sorting-the-data}

資料可以根據特定欄排序，方法如下：

* 按一下適當的欄標題；排序會在遞增和遞減之間切換，標題文字旁邊會顯示一個箭頭標頭
* 使用 [欄的下拉式功能表](#column-drop-down-menu) 特別選取 **升序排序** 或 **降序排序**；同樣地，這由緊鄰標題文字的箭頭表示

### 群組和目前的資料圖表 {#groups-and-the-current-data-chart}

在適當的欄上，您可以選取 **依此欄分組** 從 [欄的下拉式功能表](#column-drop-down-menu). 這會根據該欄中的各個不同值將資料分組。 您可以選取多個要分組的欄。 當欄中的資料不適當時，選項會變暗（變灰）。 也就是說，每個專案都是相異且唯一的，因此無法形成任何群組。 例如，使用者報表的使用者ID欄。

將至少一個欄分組後，圓餅圖會顯示 **目前資料** 會根據此分組產生。 如果已將多個欄分組，這會在圖表中指示。

![報告使用者](assets/reportuser.png)

將游標移至圓形圖上會顯示適當區段的彙總值。 這會使用目前為欄定義的彙總；例如count、minimum、average等。

### 篩選和彙總 {#filters-and-aggregates}

您也可以在適當的欄上設定 **篩選器設定** 和/或 **彙總** 從 [欄的下拉式功能表](#column-drop-down-menu).

#### 篩選條件 {#filters}

篩選設定可讓您指定要顯示的專案條件。 可用的運運算元包括：

* `contains`
* `equals`

![reportfilter](assets/reportfilter.png)

若要設定篩選，請執行下列動作：

1. 從下拉式清單中選取您想要的運運算元。
1. 輸入要篩選的文字。
1. 按一下「**套用**」。

若要停用篩選：

1. 移除篩選文字。
1. 按一下「**套用**」。

#### 彙總 {#aggregates}

您也可以選取聚總方法（根據選取的欄位而有所不同）：

![reportaggregate](assets/reportaggregate.png)

### 欄屬性 {#column-properties}

此選項僅在 [通用欄](#generic-column) 已用於 [使用者報告](#user-report).

### 歷史資料 {#historic-data}

您可以在下方看到資料隨時間變化的圖表 **歷史資料**. 這是從定期拍攝的快照衍生而來的。

資料為：

* 收集者（如果有的話）是第一個已排序欄，否則是第一個（非群組）欄
* 依適當的欄分組

可以產生報表：

1. 設定 **分組** 在必要欄上。
1. **編輯** 設定，讓您可以定義每小時或每日快照。
1. **完成……** 啟動快照集合的定義。

   左上方的紅色/綠色滑桿按鈕表示快照的收集時間。

產生的圖表會顯示在右下方：

![reporttrends](assets/reporttrends.png)

當資料收集開始時，您可以選取：

* **期間**

  您可以選取報表資料顯示的開始日期和結束日期。

* **間隔**

  您可以針對報表的規模和彙總選取月、周、日、小時。

  例如，如果2011年2月有每日快照可用：

   * 如果間隔設定為 `Day`，每個快照在圖表中都會顯示為單一值。
   * 如果間隔設定為 `Month`，所有2月的快照都會彙總為單一值（在圖表中顯示為單一「點」）。

選取您的需求，然後按一下 **前往** 以將其套用至報表。 若要在進一步建立快照之後更新顯示，請按一下 **前往** 再來一次。

![chlimage_1-43](assets/chlimage_1-43.png)

收集快照時，您可以：

* 使用 **完成……** 以重新初始化集合。

  **完成** 「凍結」報表的結構（也就是指派給報表的欄，以及分組、排序、篩選等專案）並開始製作快照。

* 開啟 **編輯** 對話方塊，讓您可以選取 **無資料快照** 以終止集合，直到需要為止。

  **編輯** 僅開啟或關閉快照的製作。 如果快照製作再次開啟，它會使用報表上次完成時的狀態，以製作進一步的快照。

>[!NOTE]
>
>快照會儲存在 `/var/reports/...` 其中路徑的其餘部分映象了報告完成時建立的各個報告的路徑和ID。
>
>
>如果您確定不再需要這些執行個體，可以手動清除舊快照。

>[!NOTE]
>
>預先設定的報表不需要大量使用效能，但仍建議在生產環境中使用每日快照。 如果可能的話，請在網站上沒有太多活動時執行這些每日快照。 這可以透過以下定義 `Daily snapshots (repconf.hourofday)` 的引數 **Day CQ報告設定**. 另請參閱 [OSGI設定](/help/sites-deploying/configuring-osgi.md) 以取得有關如何設定此專案的詳細資訊。

#### 顯示限制 {#display-limits}

歷史資料報表的外觀也會因為可設定的限制（根據所選期間的結果數量）而稍微變更。

每條水平線都稱為一個數列（並對應至圖表圖例中的一個專案），每一條垂直的點欄代表彙總的快照。

![chlimage_1-44](assets/chlimage_1-44.png)

若要讓圖表在較長時間內保持乾淨，可設定一些限制。 對於標準報表，這些功能包括：

* 水準數列 — 預設值及系統最大值皆為 `9`

* 垂直彙總快照 — 預設為 `35` （依水準數列）

因此，當超出（適當的）限制時：

* 點不會顯示
* 歷史資料圖表的圖例可能會顯示與目前資料圖表不同的專案數

![chlimage_1-45](assets/chlimage_1-45.png)

自訂報表也可顯示 **總計** 所有數列的值。 這會顯示為序列（水平線和圖例中的專案）。

>[!NOTE]
>
>對於自訂報表，限制可以有不同的設定。

### 編輯（報告） {#edit-report}

此 **編輯** 按鈕開啟 **編輯報告** 對話方塊。

這是收集快照的期間所在的位置 [歷史資料](#historic-data) 已定義，但也可定義各種其他設定：

![reportedit](assets/reportedit.png)

* **標題**

  您可以定義自己的標題。

* **說明**

  您可以定義自己的說明。

* **根路徑** (*僅適用於特定報告*)

  使用此選項可將報告限制在存放庫的（子）區段。

* **報表處理**

   * **自動重新整理資料**

     每次更新報表定義時，報表資料都會重新整理。

   * **手動重新整理資料**

     當資料量很大時，此選項可用來防止自動重新整理作業造成的延遲。

     選取此項表示報表資料的任何方面變更時，都必須手動重新整理報表設定。 這也表示當您變更組態的任何方面時，報表表格會變成空白。

     選取此選項時， **[載入資料](#load-data)** 按鈕隨即顯示(在 **編輯** （于報表中）。 **載入資料** 載入資料，並重新整理顯示的報表資料。

* **快照**
您可以定義建立快照的頻率；每天、每小時或根本不建立快照。

### 載入資料 {#load-data}

此 **載入資料** 按鈕僅在以下情況下可見 **手動重新整理資料** 已選取自 **[編輯](#edit-report)**.

![chlimage_1-46](assets/chlimage_1-46.png)

按一下 **載入資料** 重新載入資料並更新顯示的報表。

選取以手動重新整理資料表示：

1. 當您變更報表組態時，報表資料表會變成空白。

   例如，如果您變更欄的排序機制，資料不會顯示。

1. 若要讓報表資料再次顯示，您必須按一下 **載入資料** 以重新載入資料。

### 完成（報表） {#finish-report}

當您 **完成** 報告：

* 報表定義 *截至該時間點* 用於製作快照。 之後，您可以繼續處理報表定義，因為它與快照不同。
* 任何現有的快照都會被移除。
* 系統會為收集新的快照 [歷史資料](#historic-data).

使用此對話方塊，您可以為產生的報告定義或更新自己的標題和說明。

![報告完成時間](assets/reportfinish.png)

## 報表型別 {#report-types}

### 元件報表 {#component-report}

元件報表提供網站如何使用元件的相關資訊。

[資訊欄](#selecting-and-positioning-the-data-columns) 關於：

* 作者
* 元件路徑
* 元件類型
* 上次修改時間
* 頁面

這表示您可以看到下列內容：

* 使用哪些元件以及使用位置。

  很有用，例如，在測試時。

* 特定元件的例項分佈方式。

  如果特定頁面（即「大量頁面」）發生效能問題，這可能很有趣。

* 識別網站有頻繁/較少變更的部分。
* 瞭解頁面內容如何隨著時間發展。

所有元件均包含在產品標準和專案特定中。 使用 **編輯** 對話方塊使用者也可設定 **根路徑** 會定義報表的起點 — 報表會考慮該根下的所有元件。

![reportcomponent](assets/reportcomponent.png) ![reportcompentall](assets/reportcompentall.png)

### 磁碟使用情況 {#disk-usage}

「磁碟使用情況」報表會顯示存放庫中儲存之資料的相關資訊。

報表從存放庫的根( / )開始；按一下您可以在存放庫中向下鑽研的特定分支（目前路徑會反映在報表標題中）。

![reportdiskusage](assets/reportdiskusage.png)

### 健康情況檢查 {#health-check}

此報表會分析目前的請求記錄：

`<cq-installation-dir>/crx-quickstart/logs/request.log`

協助您識別特定期間內最昂貴的請求。

若要產生報表，您可以指定下列專案：

* **期間（小時）**

  要分析的時數（過去）。

  預設： `24`

* **最大 結果**

  最大輸出行數。

  預設： `50`

* **最大 請求**

  要分析的請求數上限。

  預設： `-1` （全部）

* **電子郵件地址**

  將結果傳送至電子郵件地址。

  選用；預設：空白

* **每日執行於(hh：mm)**

  指定報表每天自動執行的時間。

  選用；預設：空白

![reporthealth](assets/reporthealth.png)

### 頁面活動報表 {#page-activity-report}

頁面活動報表會列出頁面以及在這些頁面上執行的動作。

[資訊欄](#selecting-and-positioning-the-data-columns) 關於：

* 頁面
* 時間
* 類型
* 使用者

表示您可以監視：

* 最新的修改。
* 在特定頁面上工作的作者。
* 最近未修改的頁面，因此可能需要進行動作。
* 變更最多/最不頻繁的頁面。
* 最多/最少的活躍使用者。

頁面活動報告會從稽核記錄中擷取其所有資訊。 依預設，根路徑會設定為稽核記錄，位於 `/var/audit/com.day.cq.wcm.core.page`.

![reportpageactivity](assets/reportpageactivity.png)

### 使用者產生的內容報表 {#user-generated-content-report}

此報表提供有關使用者產生內容的資訊；包括評論、評分或論壇。

[資訊欄](#selecting-and-positioning-the-data-columns) 於：

* 日期
* IP 位址
* 頁面
* 反向連結
* 類型
* 使用者識別碼

可讓您：

* 檢視哪些頁面收到的評論最多。
* 取得特定網站訪客離開的所有評論的概觀，可能是相關問題。
* 透過監視頁面上何時產生評論來判斷新內容是否引起評論。

![reportuser內容](assets/reportusercontent.png)

### 使用者報表 {#user-report}

此報表提供有關已註冊帳戶及/或設定檔的所有使用者資訊，包括組織內的作者和外部訪客。

[資訊欄](#selecting-and-positioning-the-data-columns) （可用時）關於：

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

可讓您：

* 檢視使用者的人口統計分佈。
* 報告您新增至設定檔的自訂欄位。

![reportusercanned](assets/reportusercanned.png)

#### 通用欄 {#generic-column}

此 **通用** 欄可用於使用者報告，如此一來您就可以存取自訂資訊，通常是從 [使用者設定檔](/help/sites-administering/identity-management.md#profiles-and-user-accounts)；例如， [新增欄位至設定檔定義底下所詳述的我的最愛顏色](/help/sites-administering/identity-management.md#adding-fields-to-the-profile-definition).

執行下列任一操作時，「類屬」欄對話方塊會開啟：

* 將Generic元件從Sidekick拖曳到報表中。
* 選取現有「一般」資料欄的「資料欄屬性」。

![reportusrgenericcolm](assets/reportusrgenericcolm.png)

從 **定義** 標籤您可以定義：

* **標題**

  您自己的通用欄標題。

* **屬性**

  儲存在存放庫中的屬性名稱，通常在使用者的設定檔中。

* **路徑**

  屬性通常取自 `profile`.

* **類型**

  從中選擇欄位型別 `String`， `Number`， `Integer`， `Date`.

* **預設彙總**

  如果欄在至少有一個分組欄的報告中未分組，這會定義預設使用的彙總。 從以下專案選取所需的彙總： `Count`， `Minimum`， `Average`， `Maximum`， `Sum`.

  例如， *計數* 針對 `String` 欄位表示相異的數量 `String` 值會顯示在彙總狀態的欄中。

在 **延伸** 索引標籤上，您也可以定義可用的彙總和篩選器：

![reportusrgenericcolmextented](assets/reportusrgenericcolmextented.png)

### 工作流程例項報表 {#workflow-instance-report}

這可讓您取得簡要的概觀，提供關於執行中及已完成之工作流程的個別執行個體資訊。

[資訊欄](#selecting-and-positioning-the-data-columns) 關於：

* 完成
* 持續時間
* 發起人
* 模型
* 總額
* 開始時間
* 狀態

這表示您可以：

* 監視工作流程的平均持續時間；如果這種狀況定期發生，則可以強調工作流程的問題。

![reportworkflowinstance](assets/reportworkflowintance.png)

### 工作流程報告 {#workflow-report}

這可提供您執行個體上執行之工作流程的重要統計資料。

![報告工作流程](assets/reportworkflow.png)

## 在發佈環境中使用報表 {#using-reports-in-a-publish-environment}

一旦您將報告設定為符合您的特定需求，就可以啟動它以將其設定傳輸到發佈環境。

>[!CAUTION]
>
>如果您願意 **歷史資料** 針對「發佈」環境，則 **完成** 啟動頁面前製作環境的報告。

接著，您可在下方存取適當的報表：

`/etc/reports`

例如，使用者產生的內容報表可在下找到：

`http://localhost:4503/etc/reports/ugcreport.html`

現在會報告從發佈環境收集的資料。

由於發佈環境中不允許報表設定，因此 **編輯** 和 **完成** 按鈕無法使用。 不過，您可以選取 **期間** 和 **間隔** 針對 **歷史資料** 報告是否正在收集快照。

![reportsucgpublish](assets/reportsucgpublish.png)

>[!CAUTION]
>
>存取這些報告可能是安全問題；因此Adobe建議您設定Dispatcher，以便 `/etc/reports` 外部訪客無法使用。 請參閱 [安全性檢查清單](security-checklist.md) 以取得更多詳細資料。

## 執行報告所需的許可權 {#permissions-needed-for-running-reports}

所需的許可權取決於動作：

* 使用目前使用者的許可權收集報表資料。
* 歷史資料是使用完成報表之使用者的許可權來收集。

在標準AEM安裝中，報表會預設下列許可權：

* **使用者報告**

  `user administrators`  — 讀取和寫入

* **頁面活動報表**

  `contributors`  — 讀取和寫入

* **元件報表**

  `contributors`  — 讀取和寫入

* **使用者產生的內容報表**

  `contributors`  — 讀取和寫入

* **工作流程例項報告**

  `workflow-users`  — 讀取和寫入

所有成員 `administrators` 群組具有建立報告的必要許可權。
