---
title: 有關數位資產的使用與分享的報告。
description: 有關您資產的報 [!DNL Adobe Experience Manager Assets] 告，可協助您瞭解數位資產的使用、活動和共用。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a8c4bc1992a48dd01a3f58498e9e924dcc9e886a
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 8%

---


# Asset Reports {#asset-reports}

資產報表可讓您評估部署的實用 [!DNL Adobe Experience Manager Assets] 程式。 有了 [!DNL Assets]，您就可以產生各種數位資產的報表。 這些報表提供您系統使用情況、使用者與資產的互動方式，以及哪些資產被下載和共用的實用資訊。

使用報表中的資訊衍生關鍵成功度量，以評估您企業內 [!DNL Assets] 部和客戶的接受度。

報告 [!DNL Assets] 框架使用作 [!DNL Sling] 業以有序方式非同步處理報告請求。 它適用於大型儲存庫。 非同步報表處理可提高報表產生的效率和速度。

報表管理介面是直覺式的，包含存取已封存報表及檢視報表執行狀態（成功、失敗和佇列）的精細選項和控制項。

產生報表時，您會透過電子郵件（可選）和收件匣通知收到通知。 您可以從報表清單頁面檢視、下載或刪除報表，其中會顯示所有先前產生的報表。

## 先決條件 {#prerequisite-for-reporting}

若要產生報表，請確定下列項目：

* 從「 [!UICONTROL 工具」>「作業」]**[!UICONTROL >「Web主控台]** 」啟用「Day CQ DAM Event Recorder **[!UICONTROL 」]******&#x200B;服務。
* 選擇您要報告的活動或事件。 例如，若要產生已下載資產的報表，請選取「已 [!UICONTROL 下載資產」(DOWNLOADED)]。

![在Web Console中啟用資產報告功能](assets/reports-config-day-cq-dam-event-recorder.png)

## 產生報表 {#generate-reports}

[!DNL Experience Manager Assets] 為您生成以下標準報表：

* 上傳
* 下載
* 過期
* 修改
* 發佈
* [!DNL Brand Portal] 發佈
* 磁碟使用情況
* 檔案
* 連結共用

[!DNL Adobe Experience Manager] 管理員可輕鬆產生和自訂這些報表，以供您的實作使用。 管理員可依照下列步驟產生報表：

1. 在介 [!DNL Experience Manager] 面中，按一下「 **[!UICONTROL 工具]** >資 **[!UICONTROL 產]** > **[!UICONTROL 報表]**」。

![「工具」頁面，以導覽資產報表](assets/AssetsReportNavigation.png)

1. 在「資 [!UICONTROL 產報表] 」頁面上，按 **[!UICONTROL 一下工具]** 列中的「建立」。
1. 從「建 **[!UICONTROL 立報表]** 」頁面，選擇您要建立的報表，然後按一下「下 **[!UICONTROL 一步」]**。

   ![選擇報表類型](assets/choose_report.png)

   >[!NOTE]
   >
   >依預設，「內容片段」和連結分享會包含在資產「下載 [!UICONTROL 」報] 表中。 選取適當的選項，以建立連結共用的報表，或從下載報表中排除內容片段。

   >[!NOTE]
   >
   >「下 [!UICONTROL 載] 」報表只會顯示個別選取並使用「快速動作」下載或下載的資產的詳細資訊。 但是，它不包含已下載資料夾中資產的詳細資料。
1. 在儲存報表的CRX儲存庫中設定報表詳細資訊，例如標題、說明、縮圖和資料夾路徑。 預設情況下，資料夾路徑為 `/content/dam`。 您可以指定不同的路徑。

   ![新增報表詳細資訊的頁面](assets/report_configuration.png)

   選擇報表的日期範圍。

   您可以選擇立即產生報表，或在未來的日期和時間產生報表。

   >[!NOTE]
   >
   >如果您選擇稍後排程報表，請確定您在「日期和時間」欄位中指定日期和時間。 如果您未指定任何值，報表引擎會將其視為要立即產生的報表。

   設定欄位可能會因您建立的報表類型而異。 例如，「磁碟使 **[!UICONTROL 用情況]** 」報表提供選項，可在計算資產使用的磁碟空間時包含資產轉譯。 您可以選擇在子資料夾中包含或排除資產，以便計算磁碟使用情況。

   >[!NOTE]
   >
   >「磁 **[!UICONTROL 碟使用情況]** 」報表不包含日期範圍欄位，因為它僅表示目前的磁碟空間使用情況。

   ![「 Disk Usage 」報告的詳細資訊頁](assets/disk_usage_configuration.png)

   當您建立「檔 **[!UICONTROL 案]** 」報表時，可以包含／排除子資料夾。 不過，您無法為此報表包含資產轉譯。

   ![「檔案」報表的詳細資訊頁面](assets/files_report.png)

   The **[!UICONTROL Link Share]** report displays URLs to assets that are shared with external users from within [!DNL Assets]. 它包含共用資產之使用者的電子郵件ID、共用資產之使用者的電子郵件ID、連結的共用日期和到期日。欄無法自訂。

   The **[!UICONTROL Link Share]** report, does not include options for sub-folders and renditions because it merely publishes the shared URLs that appear under `/var/dam/share`.

   ![「連結共用」報表的詳細資訊頁面](assets/link_share.png)

1. 從工具 **[!UICONTROL 列按一下]** 「下一步」。

1. 在「設 **[!UICONTROL 定欄]** 」頁面中，某些欄會依預設顯示在報表中。 您可以選取更多欄。 取消選取選取的欄，將其排除在報表中。

   ![選取或取消選取報表欄](assets/configure_columns.png)

   若要顯示自訂欄名稱或屬性路徑，請在CRX的節點下設定資產二進位 `jcr:content` 檔案的屬性。 或者，透過屬性路徑選擇器加入。

   ![選取或取消選取報表欄](assets/custom_columns.png)

1. 從工具 **[!UICONTROL 列按一下]** 「建立」。 訊息會通知報表產生已開始。
1. 在「報 [!UICONTROL 表] 」頁面上，報表產生狀態是根據報表作業的目前狀態，例如 [!UICONTROL Success]、FailedFailed [!UICONTROL 、]Queued Asset或ScheduledScheduledReports。 通知收件箱中會顯示相同的狀態。要查看報告頁，請按一下報告連結。 或者，選取報表，然後從工具列按 **[!UICONTROL 一下]** 「檢視」。

   ![產生的報表](assets/report_page.png)

   按一 **[!UICONTROL 下工具]** 列中的「下載」，以下載CSV格式的報表。

## 新增自訂欄 {#add-custom-columns}

您可以新增自訂欄至下列報表，以顯示更多符合自訂需求的資料：

* 上傳
* 下載
* 過期
* 修改
* 發佈
* [!DNL Brand Portal] 發佈
* 檔案

若要新增自訂欄至這些報表，請依照下列步驟進行：

1. 在中，按 [!DNL Manager interface]一下「 **[!UICONTROL 工具]** >資 **[!UICONTROL 產]** > **[!UICONTROL 報表]**」。
1. 在「資 [!UICONTROL 產報表] 」頁面上，按 **[!UICONTROL 一下工具]** 列中的「建立」。

1. 從「建 **[!UICONTROL 立報表]** 」頁面，選擇您要建立的報表，然後按一下「下 **[!UICONTROL 一步」]**。
1. 視需要設定報表詳細資訊，例如標題、說明、縮圖、資料夾路徑和日期範圍。

1. 要顯示自定義列，請在「自定義列」下指定列 **[!UICONTROL 的名稱]**。

   ![指定報表的自訂欄名稱](assets/custom_columns-1.png)

1. 使用屬性路徑選擇器在CRXDE `jcr:content` 的節點下添加屬性路徑。 或者，在屬性路徑欄位中鍵入路徑。

   ![從jcr:content中的路徑映射屬性路徑](assets/property_picker.png)

   若要新增更多自訂欄，請按一 **[!UICONTROL 下「新增]** 」，然後重複步驟5和6。

1. 從工具 **[!UICONTROL 列按一下]** 「建立」。 訊息會通知報表產生已開始。

## 配置清除服務 {#configure-purging-service}

若要移除不再需要的報表，請從Web主控台設定DAM報表清除服務，以根據現有報表的數量和年齡來清除報表。

1. 從訪問Web控制台（配置管理器） `https://[aem_server]:[port]/system/console/configMgr`。
1. 開啟「 **[!UICONTROL DAM報表清除服務]** 」設定。
1. 在欄位中指定清除服務的頻率（時間間隔） `scheduler.expression.name` 。 您也可以設定報表的年齡和數量臨界值。
1. 儲存變更。
