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
feature: Operations
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
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
>這些報表只能在Classic UI中使用。 若要使用新式UI進行系統監視和報告，請參閱[操作儀表板。](/help/sites-administering/operations-dashboard.md)

所有報表都可以從&#x200B;**工具**&#x200B;主控台存取。 在左側窗格中選取&#x200B;**報表**，然後按兩下右側窗格中的必要報表，即可開啟報表以供檢視、設定或兩者同時開啟。

您也可以從&#x200B;**工具**&#x200B;主控台建立報表的新執行個體。 在左側窗格中選取&#x200B;**報表**，然後從工具列選取&#x200B;**新增……**。 定義&#x200B;**標題**&#x200B;和&#x200B;**名稱**，選取您需要的報表型別，然後按一下&#x200B;**建立**。 您的新報表例項會出現在清單中。 按兩下以開啟，然後從Sidekick拖曳元件，以便建立第一欄並開始報表定義。

>[!NOTE]
>
>除了現成可用的標準AEM報告之外，您還可以[開發您自己的（新）報告](/help/sites-developing/dev-reports.md)。

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
>* [健康狀態檢查](#health-check)使用選取欄位來指定您要報告的資料。
>* [磁碟使用狀況](#disk-usage)使用連結來深入鑽研存放庫結構。
>* [工作流程](/help/sites-administering/reporting.md#workflow-report)提供執行個體上執行的工作流程概觀。
>
>因此，以下欄配置程式不適用。 如需詳細資訊，請參閱個別報表的說明。

### 選取和定位資料欄 {#selecting-and-positioning-the-data-columns}

欄可新增至任何報表、可在其上重新放置或從中移除，無論是標準報表或自訂報表。

Sidekick的&#x200B;**元件**&#x200B;標籤（可在報告頁面上取得）列出可選取為欄的所有資料類別。

若要變更資料選取範圍：

* 若要新增欄，請從sidekick拖曳所需的元件，並將它放置在您想要的位置

   * 綠色勾號表示位置何時有效，而一對箭頭則表示位置正好
   * 紅色的no-go符號表示位置無效

* 若要移動欄，請按一下標題，按住，然後拖曳到新位置
* 若要移除欄，請按住欄標題，然後向上拖曳至報表標題區域（紅色減號表示位置無效）。 放開滑鼠鍵，「刪除元件」對話方塊會要求確認您確實要刪除欄。

### 欄下拉式功能表 {#column-drop-down-menu}

報表中的每一欄都有一個下拉式功能表。 當滑鼠游標移至欄標題儲存格上時，此專案會變成可見。

標題儲存格的最右邊會顯示一個箭頭（不要與表示[目前排序機制](#sorting-the-data)的標題文字右邊的箭頭混淆）。

![reportcolumnsort](assets/reportcolumnsort.png)

功能表上的可用選項取決於欄的設定（如專案開發期間所設定），任何無效選項都會變暗（變灰）。

### 排序資料 {#sorting-the-data}

資料可以根據特定欄排序，方法如下：

* 按一下適當的欄標題；排序會在遞增和遞減之間切換，標題文字旁邊會顯示一個箭頭標頭
* 使用[欄的下拉式功能表](#column-drop-down-menu)，明確選取&#x200B;**遞增排序**&#x200B;或&#x200B;**遞減排序**；再次在標題文字旁邊以箭號表示

### 群組和目前的資料圖表 {#groups-and-the-current-data-chart}

在適當的欄上，您可以從[欄的下拉式功能表](#column-drop-down-menu)中選取&#x200B;**依此欄分組**。 這會根據該欄中的各個不同值將資料分組。 您可以選取多個要分組的欄。 當欄中的資料不適當時，選項會變暗（變灰）。 也就是說，每個專案都是相異且唯一的，因此無法形成任何群組。 例如，使用者報表的使用者ID欄。

至少在一欄分組後，會根據此分組產生&#x200B;**目前資料**&#x200B;的圓餅圖。 如果已將多個欄分組，這會在圖表中指示。

![報告使用者](assets/reportuser.png)

將游標移至圓形圖上會顯示適當區段的彙總值。 這會使用目前為欄定義的彙總；例如count、minimum、average等。

### 篩選和彙總 {#filters-and-aggregates}

您也可以在適當的欄上，從[欄的下拉式功能表](#column-drop-down-menu)設定&#x200B;**篩選設定**&#x200B;和/或&#x200B;**彙總**。

#### 篩選條件 {#filters}

篩選設定可讓您指定要顯示的專案條件。 可用的運運算元包括：

* `contains`
* `equals`

![報告篩選器](assets/reportfilter.png)

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

只有在[使用者報告](#user-report)中使用了[泛型資料行](#generic-column)時，才能使用此選項。

### 歷史資料 {#historic-data}

您可以在&#x200B;**歷史資料**&#x200B;下看到資料隨時間變化的圖表。 這是從定期拍攝的快照衍生而來的。

資料為：

* 收集者（如果有的話）是第一個已排序欄，否則是第一個（非群組）欄
* 依適當的欄分組

可以產生報表：

1. 在必要的資料行上設定&#x200B;**群組**。
1. **編輯**&#x200B;設定，以便定義每小時或每日快照。
1. **完成……**&#x200B;定義，以啟動快照集集合。

   左上方的紅色/綠色滑桿按鈕表示快照的收集時間。

產生的圖表會顯示在右下方：

![報告趨勢](assets/reporttrends.png)

當資料收集開始時，您可以選取：

* **週期**

  您可以選取報表資料顯示的開始日期和結束日期。

* **間隔**

  您可以針對報表的規模和彙總選取月、周、日、小時。

  例如，如果2011年2月有每日快照可用：

   * 如果間隔設定為`Day`，則每個快照都會在圖表中顯示為單一值。
   * 如果間隔設為`Month`，2月的所有快照都會彙總為單一值（在圖表中顯示為單一「點」）。

選取您的需求，然後按一下[執行&#x200B;**&#x200B;**]以套用至報表。 若要在進一步建立快照後更新顯示，請再按一下[執行&#x200B;**]。**

![chlimage_1-43](assets/chlimage_1-43.png)

收集快照時，您可以：

* 再次使用&#x200B;**完成……**&#x200B;來重新初始化集合。

  **完成**&#x200B;會「凍結」報表的結構（亦即指派給報表的欄，這些欄會進行分組、排序、篩選等等），並開始製作快照。

* 開啟&#x200B;**編輯**&#x200B;對話方塊，以便您可以選取&#x200B;**無資料快照**&#x200B;來終止收集，直到需要為止。

  **編輯**&#x200B;只會開啟或關閉快照的製作。 如果快照製作再次開啟，它會使用報表上次完成時的狀態，以製作進一步的快照。

>[!NOTE]
>
>快照儲存在`/var/reports/...`下，其中路徑的其餘部分會反映報告完成時所建立之個別報告和ID的路徑。
>
>
>如果您確定不再需要這些執行個體，可以手動清除舊快照。

>[!NOTE]
>
>預先設定的報表不需要大量使用效能，但仍建議在生產環境中使用每日快照。 如果可能的話，請在網站上沒有太多活動時執行這些每日快照。 這可以用&#x200B;**Day CQ報告組態**&#x200B;的`Daily snapshots (repconf.hourofday)`引數來定義。 如需如何設定的詳細資訊，請參閱[OSGI設定](/help/sites-deploying/configuring-osgi.md)。

#### 顯示限制 {#display-limits}

歷史資料報表的外觀也會因為可設定的限制（根據所選期間的結果數量）而稍微變更。

每條水平線都稱為一個數列（並對應至圖表圖例中的一個專案），每一條垂直的點欄代表彙總的快照。

![chlimage_1-44](assets/chlimage_1-44.png)

若要讓圖表在較長時間內保持乾淨，可設定一些限制。 對於標準報表，這些功能包括：

* 水準數列 — 預設值及系統上限皆為`9`

* 垂直彙總快照 — 預設為`35` （每個水準系列）

因此，當超出（適當的）限制時：

* 點不會顯示
* 歷史資料圖表的圖例可能會顯示與目前資料圖表不同的專案數

![chlimage_1-45](assets/chlimage_1-45.png)

自訂報表也可以顯示所有系列的&#x200B;**總計**&#x200B;值。 這會顯示為序列（水平線和圖例中的專案）。

>[!NOTE]
>
>對於自訂報表，限制可以有不同的設定。

### 編輯（報告） {#edit-report}

**編輯**&#x200B;按鈕會開啟&#x200B;**編輯報告**&#x200B;對話方塊。

這是已定義收集[歷史資料](#historic-data)之快照的期間，但也可以定義其他各種設定的位置：

![reportedit](assets/reportedit.png)

* **標題**

  您可以定義自己的標題。

* **說明**

  您可以定義自己的說明。

* **根路徑** （*僅對特定報告有效*）

  使用此選項可將報告限制在存放庫的（子）區段。

* **報告處理中**

   * **自動重新整理資料**

     每次更新報表定義時，報表資料都會重新整理。

   * **手動重新整理資料**

     當資料量很大時，此選項可用來防止自動重新整理作業造成的延遲。

     選取此項表示報表資料的任何方面變更時，都必須手動重新整理報表設定。 這也表示當您變更組態的任何方面時，報表表格會變成空白。

     選取此選項時，會顯示&#x200B;**[載入資料](#load-data)**&#x200B;按鈕（在報告上的&#x200B;**編輯**&#x200B;旁邊）。 **載入資料**&#x200B;載入資料並重新整理顯示的報表資料。

* **快照**
您可以定義建立快照的頻率；每天、每小時或根本不建立快照。

### 載入資料 {#load-data}

只有從&#x200B;**[編輯](#edit-report)**&#x200B;中選取&#x200B;**手動重新整理資料**&#x200B;時，**載入資料**&#x200B;按鈕才可見。

![chlimage_1-46](assets/chlimage_1-46.png)

按一下「**載入資料**」重新載入資料並更新顯示的報表。

選取以手動重新整理資料表示：

1. 當您變更報表組態時，報表資料表會變成空白。

   例如，如果您變更欄的排序機制，資料不會顯示。

1. 如果您要再次顯示報表資料，必須按一下[載入資料] **&#x200B;**&#x200B;以重新載入資料。

### 完成（報表） {#finish-report}

當您&#x200B;**完成**&#x200B;報告時：

* 截至該時間點&#x200B;*的報告定義*&#x200B;用於建立快照。 之後，您可以繼續處理報表定義，因為它與快照不同。
* 任何現有的快照都會被移除。
* 已針對[歷史資料](#historic-data)收集新快照。

使用此對話方塊，您可以為產生的報告定義或更新自己的標題和說明。

![報告完成時間](assets/reportfinish.png)

## 報表型別 {#report-types}

### 元件報表 {#component-report}

元件報表提供網站如何使用元件的相關資訊。

[資料行](#selecting-and-positioning-the-data-columns)關於：

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

所有元件均包含在產品標準和專案特定中。 使用&#x200B;**編輯**&#x200B;對話方塊，使用者也可以設定定義報告起點的&#x200B;**根路徑** — 該根下的所有元件都視為報告。

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

* 最多&#x200B;**個。 結果**

  最大輸出行數。

  預設： `50`

* 最多&#x200B;**個。 要求**

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

[資料行](#selecting-and-positioning-the-data-columns)關於：

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

頁面活動報告會從稽核記錄中擷取其所有資訊。 依預設，根路徑會設定為位於`/var/audit/com.day.cq.wcm.core.page`的稽核記錄。

![reportpageactivity](assets/reportpageactivity.png)

### 使用者產生的內容報表 {#user-generated-content-report}

此報表提供有關使用者產生內容的資訊；包括評論、評分或論壇。

[資料行](#selecting-and-positioning-the-data-columns)於：

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

![reportusercontent](assets/reportusercontent.png)

### 使用者報表 {#user-report}

此報表提供有關已註冊帳戶及/或設定檔的所有使用者資訊，包括組織內的作者和外部訪客。

[資料行](#selecting-and-positioning-the-data-columns) （可用時）關於：

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

**Generic**&#x200B;資料行可在使用者報告中使用，因此您可以存取自訂資訊，通常從[使用者設定檔](/help/sites-administering/identity-management.md#profiles-and-user-accounts)存取；例如，[最喜愛的色彩，如新增欄位至設定檔定義](/help/sites-administering/identity-management.md#adding-fields-to-the-profile-definition)底下所詳述。

執行下列任一操作時，「類屬」欄對話方塊會開啟：

* 將Generic元件從Sidekick拖曳到報表中。
* 選取現有「一般」資料欄的「資料欄屬性」。

![reportusrgenericcolm](assets/reportusrgenericcolm.png)

從&#x200B;**定義**&#x200B;索引標籤中，您可以定義：

* **標題**

  您自己的通用欄標題。

* **屬性**

  儲存在存放庫中的屬性名稱，通常在使用者的設定檔中。

* **路徑**

  屬性通常取自`profile`。

* **類型**

  從`String`、`Number`、`Integer`、`Date`中選取欄位型別。

* **預設彙總**

  如果欄在至少有一個分組欄的報告中未分組，這會定義預設使用的彙總。 從`Count`、`Minimum`、`Average`、`Maximum`、`Sum`中選取必要的彙總。

  例如，`String`欄位的&#x200B;*Count*&#x200B;表示在彙總狀態的資料行會顯示相異`String`值的數目。

在&#x200B;**延伸**&#x200B;索引標籤中，您也可以定義可用的彙總與篩選器：

![reportusrgenericcolmextented](assets/reportusrgenericcolmextented.png)

### 工作流程例項報表 {#workflow-instance-report}

這可讓您取得簡要的概觀，提供關於執行中及已完成之工作流程的個別執行個體資訊。

[資料行](#selecting-and-positioning-the-data-columns)關於：

* 完成
* 持續時間
* 發起人
* 模型
* 總額
* 開始時間
* 狀態

這表示您可以：

* 監視工作流程的平均持續時間；如果這種狀況定期發生，則可以強調工作流程的問題。

![reportworkflowintance](assets/reportworkflowintance.png)

### 工作流程報告 {#workflow-report}

這可提供您執行個體上執行之工作流程的重要統計資料。

![報告工作流程](assets/reportworkflow.png)

## 在Publish環境中使用報表 {#using-reports-in-a-publish-environment}

一旦您將報告設定為符合您的特定需求，就可以啟動它以將其設定傳輸到發佈環境。

>[!CAUTION]
>
>如果您想要&#x200B;**Publish環境的歷史資料**，請在啟動頁面之前&#x200B;**完成**&#x200B;作者環境的報告。

接著，您可在下方存取適當的報表：

`/etc/reports`

例如，使用者產生的內容報表可在下找到：

`http://localhost:4503/etc/reports/ugcreport.html`

現在會報告從Publish環境收集到的資料。

由於Publish環境中不允許報表設定，**編輯**&#x200B;和&#x200B;**完成**&#x200B;按鈕無法使用。 不過，如果正在收集快照，您可以為&#x200B;**歷史資料**&#x200B;報告選取&#x200B;**期間**&#x200B;和&#x200B;**間隔**。

![reportsucgpublish](assets/reportsucgpublish.png)

>[!CAUTION]
>
>存取這些報告可能是安全性問題；因此，Adobe建議您設定Dispatcher，讓`/etc/reports`無法供外部訪客使用。 如需詳細資訊，請參閱[安全性檢查清單](security-checklist.md)。

## 執行報告所需的許可權 {#permissions-needed-for-running-reports}

所需的許可權取決於動作：

* 使用目前使用者的許可權收集報表資料。
* 歷史資料是使用完成報表之使用者的許可權來收集。

在標準AEM安裝中，報表會預設下列許可權：

* **使用者報告**

  `user administrators` — 讀取和寫入

* **頁面活動報告**

  `contributors` — 讀取和寫入

* **元件報告**

  `contributors` — 讀取和寫入

* **使用者產生的內容報告**

  `contributors` — 讀取和寫入

* **工作流程執行個體報告**

  `workflow-users` — 讀取和寫入

`administrators`群組的所有成員都有建立報告的必要許可權。
