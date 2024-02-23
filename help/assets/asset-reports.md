---
title: 資產使用和共用相關報表
description: 有關您在中之資產的報表 [!DNL Adobe Experience Manager Assets] 可協助您瞭解數位資產的使用、活動和共用。
contentOwner: AG
role: User, Admin
feature: Asset Reports,Asset Management
exl-id: b4963a03-3496-4c6c-9d30-8812304d0e9f
hide: true
source-git-commit: 93d0a38d13223a8580f54786bc4ffe149efe99f1
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 8%

---

# 資產報表 {#asset-reports}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/asset-reports.html?lang=en) |
| AEM 6.5 | 本文章 |

資產報告可讓您評估 [!DNL Adobe Experience Manager Assets] 部署。 替換為 [!DNL Assets]，您可為數位資產產生各種報表。 這些報表提供關於您系統使用情況、使用者如何與資產互動，以及哪些資產已下載和共用的有用資訊。

使用報告中的資訊取得關鍵成功度量，以測量採用程度 [!DNL Assets] 企業內部和客戶。

此 [!DNL Assets] 報告框架使用 [!DNL Sling] 非同步處理報表請求的作業。 其可擴展至大型存放庫。 非同步報表處理可提高報表產生的效率和速度。

報表管理介面是直覺式的，並包含存取已封存報表和檢視報表執行狀態（成功、失敗和已排入佇列）的細微選項和控制項。

產生報表時，系統會透過電子郵件（選用）和收件匣通知來通知您。 您可以從報告清單頁面檢視、下載或刪除報告，該頁面會顯示所有先前產生的報告。

## 必備條件 {#prerequisite-for-reporting}

若要產生報表，請執行下列動作：

* 啟用 [!UICONTROL Day CQ DAM事件記錄器] 服務來源 **[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]**.
* 選取您要報告的活動或事件。 例如，若要產生已下載資產的報表，請選取「 」 [!UICONTROL 資產已下載（已下載）].

![在Web控制檯中啟用資產報告](assets/reports-config-day-cq-dam-event-recorder.png)

## 產生報表 {#generate-reports}

[!DNL Experience Manager Assets] 會為您產生下列標準報表：

* 上傳
* 下載
* 過期
* 修改
* 發佈
* [!DNL Brand Portal] 發佈
* 磁碟使用情況
* 檔案
* 連結共用

[!DNL Adobe Experience Manager] 管理員可輕鬆地產生和自訂這些報表，以供您實作。 管理員可以依照下列步驟產生報表：

1. 在 [!DNL Experience Manager] 介面，按一下 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 報表]**.

   ![用於導覽資產報表的「工具」頁面](assets/AssetsReportNavigation.png)

1. 在 [!UICONTROL 資產報表] 頁面，按一下 **[!UICONTROL 建立]** 工具列中的。
1. 從 **[!UICONTROL 建立報告]** 頁面上，選擇要建立的報表，然後按一下 **[!UICONTROL 下一個]**.

   ![選取報表型別](assets/choose_report.png)

   >[!NOTE]
   >
   >依預設，內容片段和連結共用會包含在資產中 [!UICONTROL 下載] 報告。 選取適當的選項以建立連結共用報表，或從下載報表中排除內容片段。

   >[!NOTE]
   >
   >此 [!UICONTROL 下載] 報表只會顯示個別選取後下載的資產，或使用快速動作下載的資產的詳細資訊。 但不包含下載資料夾內資產的詳細資訊。

1. 設定報告詳細資訊，例如，標題、說明、縮圖和儲存報告的CRX存放庫中的資料夾路徑。 依預設，資料夾路徑為 `/content/dam`. 您可以指定不同的路徑。

   ![新增報告詳細資料的頁面](assets/report_configuration.png)

   選擇報表的日期範圍。

   您可以選擇現在產生報表，或在未來的日期和時間產生報表。

   >[!NOTE]
   >
   >如果您選擇稍後排程報表，請務必在「日期」和「時間」欄位中指定日期和時間。 如果您未指定任何值，報表引擎會將其視為要立即產生的報表。

   設定欄位可能會因您建立的報告型別而異。 例如， **[!UICONTROL 磁碟使用量]** 報表提供計算資產使用的磁碟空間時，包含資產轉譯的選項。 您可以選擇在子資料夾中包含或排除資產以計算磁碟使用量。

   >[!NOTE]
   >
   >「磁 **[!UICONTROL 碟使用情況]** 」報表不包含日期範圍欄位，因為它僅表示目前的磁碟空間使用情況。

   ![「磁碟使用情況」報告的「詳細資訊」頁面](assets/disk_usage_configuration.png)

   當您建立 **[!UICONTROL 檔案]** 報告，您可以包含/排除子資料夾。 不過，您無法包含此報表的資產轉譯。

   ![檔案報告的詳細資訊頁面](assets/files_report.png)

   此 **[!UICONTROL 連結共用]** 報表會顯示資產的URL，這些資產是從中與外部使用者共用的 [!DNL Assets]. 它包含共用資產之使用者的電子郵件ID、共用資產之使用者的電子郵件ID、連結的共用日期和到期日。欄無法自訂。

   此 **[!UICONTROL 連結共用]** 不包含子資料夾和轉譯的選項，因為它只會發佈顯示在下的共用URL `/var/dam/share`.

   ![連結共用報告的詳細資訊頁面](assets/link_share.png)

1. 按一下 **[!UICONTROL 下一個]** 工具列中的。

1. 在 **[!UICONTROL 設定欄]** 頁面中，某些欄會依預設選取顯示在報表中。 您可以選取更多欄。 取消選取欄以在報告中將其排除。

   ![選取或取消選取報表欄](assets/configure_columns.png)

   若要顯示自訂欄名稱或屬性路徑，請在 `jcr:content` CRX中的節點。 或者，透過屬性路徑選擇器新增路徑。

   ![選取或取消選取報表欄](assets/custom_columns.png)

1. 按一下 **[!UICONTROL 建立]** 工具列中的。 訊息會通知已啟動報表產生作業。
1. 在 [!UICONTROL 資產報表] 頁面時，報表產生狀態會根據報表工作的目前狀態，例如 [!UICONTROL 成功]， [!UICONTROL 已失敗]， [!UICONTROL 已排入佇列]，或 [!UICONTROL 已排程]. 相同的狀態會顯示在通知收件匣中。若要檢視報告頁面，請按一下報告連結。 或者，選取報告，然後按一下 **[!UICONTROL 檢視]** 工具列中的。

   <!--![A generated report](assets/report_page.png)-->
   [報告狀態](assets/report-status.JPG)

   按一下 **[!UICONTROL 下載]** 從工具列下載CSV格式的報表。

## 新增自訂欄 {#add-custom-columns}

您可以將自訂欄新增到以下報表，以顯示更多符合自訂需求的資料：

* 上傳
* 下載
* 過期
* 修改
* 發佈
* [!DNL Brand Portal] 發佈
* 檔案

若要新增自訂欄到這些報表，請執行下列步驟：

1. 在 [!DNL Manager interface]，按一下 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 報表]**.
1. 在 [!UICONTROL 資產報表] 頁面，按一下 **[!UICONTROL 建立]** 工具列中的。

1. 從 **[!UICONTROL 建立報告]** 頁面上，選擇要建立的報表，然後按一下 **[!UICONTROL 下一個]**.
1. 視情況設定標題、說明、縮圖、資料夾路徑和日期範圍等報表詳細資訊。

1. 要顯示自定義列，請在「自定義列」下指定列 **[!UICONTROL 的名稱]**。

   ![指定報表自訂欄的名稱](assets/custom_columns-1.png)

1. 將屬性路徑新增至 `jcr:content` CRXDE中的節點（使用屬性路徑選擇器）。 或者，在屬性路徑欄位中輸入路徑。

   ![從jcr：content中的路徑對應屬性路徑](assets/property_picker.png)

   若要新增更多自訂欄，請按一下 **[!UICONTROL 新增]** 並重複步驟5和6。

1. 按一下 **[!UICONTROL 建立]** 工具列中的。 訊息會通知已啟動報表產生作業。

## 設定清除服務 {#configure-purging-service}

若要移除您不再需要的報表，請從Web主控台設定「DAM報表清除」服務，以根據其數量和年齡清除現有報表。

1. 從存取Web主控台（設定管理員） `https://[aem_server]:[port]/system/console/configMgr`.
1. 開啟 **[!UICONTROL DAM報表清除服務]** 設定。
1. 在中指定清除服務的頻率（時間間隔） `scheduler.expression.name` 欄位。 您也可以設定報表的年齡和數量臨界值。
1. 儲存變更。

## 疑難排解資訊、提示和限制 {#best-practices-and-limitations}

* 如果報表中的某些報表或數字無法使用或無法如預期使用，請確定 [!UICONTROL Day CQ DAM事件記錄器] 服務已啟用。

* 移除不再需要的報表。 使用DAM報告清除服務中的設定選項來設定清除報告的條件。

* 如果未產生「磁碟使用情況報表」，而您正在使用 [!DNL Dynamic Media]，確認所有資產皆正確繼續。 若要解決，請重新處理資產，然後再次產生報表。
