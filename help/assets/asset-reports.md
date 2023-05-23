---
title: 關於資產使用和共用的報告
description: 有關中的資產的報告 [!DNL Adobe Experience Manager Assets] 幫助您瞭解數字資產的使用、活動和共用。
contentOwner: AG
role: User, Admin
feature: Asset Reports,Asset Management
exl-id: b4963a03-3496-4c6c-9d30-8812304d0e9f
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 8%

---

# 資產報表 {#asset-reports}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/asset-reports.html?lang=en) |
| AEM 6.5 | 本文 |

資產報告允許您評估 [!DNL Adobe Experience Manager Assets] 部署。 與 [!DNL Assets]，您可以為數字資產生成各種報告。 這些報告提供有關係統使用情況、用戶如何與資產交互以及下載和共用哪些資產的有用資訊。

使用報告中的資訊來獲取關鍵成功度量，以衡量採用 [!DNL Assets] 企業內部和客戶。

的 [!DNL Assets] 報告框架使用 [!DNL Sling] 作業以按順序非同步處理報表請求。 它可用於大型儲存庫。 非同步報告處理提高了報告生成的效率和速度。

報表管理介面是直觀的，包括用於訪問已存檔的報表和查看報表運行狀態（成功、失敗和排隊）的細粒度選項和控制。

生成報告時，您會通過電子郵件（可選）和收件箱通知收到通知。 您可以從報告清單頁查看、下載或刪除報告，其中顯示所有以前生成的報告。

## 必備條件 {#prerequisite-for-reporting}

要生成報告，請執行以下操作：

* 啟用 [!UICONTROL 第CQ天大壩事件記錄器] 服務 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。
* 選擇要報告的活動或事件。 例如，要生成下載資產的報告，請選擇 [!UICONTROL 已下載資產（已下載）]。

![在Web控制台中啟用資產報告](assets/reports-config-day-cq-dam-event-recorder.png)

## 生成報告 {#generate-reports}

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

[!DNL Adobe Experience Manager] 管理員可以輕鬆生成和自定義這些報告以用於您的實施。 管理員可以按照以下步驟生成報告：

1. 在 [!DNL Experience Manager] 介面，按一下 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 報告]**。

   ![「工具」頁，用於定位資產報表](assets/AssetsReportNavigation.png)

1. 在 [!UICONTROL 資產報表] 的 **[!UICONTROL 建立]** 的子菜單。
1. 從 **[!UICONTROL 建立報告]** 的子菜單。 **[!UICONTROL 下一個]**。

   ![選擇報告類型](assets/choose_report.png)

   >[!NOTE]
   >
   >預設情況下，內容片段和連結共用包含在資產中 [!UICONTROL 下載] 報告。 選擇適當的選項以建立連結共用報告或從下載報告中排除內容片段。

   >[!NOTE]
   >
   >的 [!UICONTROL 下載] 報表僅顯示那些在單獨選擇後下載或使用快速操作下載的資產的詳細資訊。 但是，它不包括下載資料夾內的資產的詳細資訊。

1. 在儲存報告的CRX儲存庫中配置報告詳細資訊，如標題、說明、縮略圖和資料夾路徑。 預設情況下，資料夾路徑為 `/content/dam`。 可以指定其他路徑。

   ![要添加報告詳細資訊的頁](assets/report_configuration.png)

   選擇報表的日期範圍。

   您可以選擇立即或在將來的日期和時間生成報表。

   >[!NOTE]
   >
   >如果您選擇稍後計畫報表，請確保在「日期和時間」欄位中指定日期和時間。 如果未指定任何值，則報告引擎會將其視為要立即生成的報告。

   配置欄位可能因您建立的報告類型而異。 例如， **[!UICONTROL 磁碟使用情況]** report提供了在計算資產使用的磁碟空間時包括資產格式副本的選項。 您可以選擇在子資料夾中包括或排除資產以計算磁碟使用率。

   >[!NOTE]
   >
   >「磁 **[!UICONTROL 碟使用情況]** 」報表不包含日期範圍欄位，因為它僅表示目前的磁碟空間使用情況。

   ![「 Disk Usage 」報告的「 Details 」頁](assets/disk_usage_configuration.png)

   建立 **[!UICONTROL 檔案]** 報表中，您可以包括/排除子資料夾。 但是，您不能為此報表包括資產格式副本。

   ![「Files」報告的詳細資訊頁面](assets/files_report.png)

   的 **[!UICONTROL 連結共用]** 報表顯示與外部用戶共用的資產的URL，這些資產來自 [!DNL Assets]。 它包含共用資產之使用者的電子郵件ID、共用資產之使用者的電子郵件ID、連結的共用日期和到期日。欄無法自訂。

   的 **[!UICONTROL 連結共用]** 不包括子資料夾和格式副本的選項，因為它只發佈顯示在 `/var/dam/share`。

   ![「連結共用」報告的詳細資訊頁面](assets/link_share.png)

1. 按一下 **[!UICONTROL 下一個]** 的子菜單。

1. 在 **[!UICONTROL 配置列]** 的子菜單。 可以選擇更多列。 取消選擇列以將其排除在報表中。

   ![選擇或取消選擇報表列](assets/configure_columns.png)

   要顯示自定義列名或屬性路徑，請在 `jcr:content` 的子目錄。 或者，通過屬性路徑選取器添加它。

   ![選擇或取消選擇報表列](assets/custom_columns.png)

1. 按一下 **[!UICONTROL 建立]** 的子菜單。 消息通知已啟動報告生成。
1. 在 [!UICONTROL 資產報表] 頁，報表生成狀態基於報表作業的當前狀態，例如 [!UICONTROL 成功]。 [!UICONTROL 失敗]。 [!UICONTROL 已排隊]或 [!UICONTROL 計畫]。 通知收件箱中顯示相同的狀態。要查看報告頁，請按一下報告連結。 或者，選擇報告，然後按一下 **[!UICONTROL 視圖]** 的子菜單。

   ![生成的報告](assets/report_page.png)

   按一下 **[!UICONTROL 下載]** 的子菜單。

## 添加自定義列 {#add-custom-columns}

您可以向以下報表添加自定義列，以根據自定義要求顯示更多資料：

* 上傳
* 下載
* 過期
* 修改
* 發佈
* [!DNL Brand Portal] 發佈
* 檔案

要向這些報表添加自定義列，請執行以下步驟：

1. 在 [!DNL Manager interface]按一下 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 報告]**。
1. 在 [!UICONTROL 資產報表] 的 **[!UICONTROL 建立]** 的子菜單。

1. 從 **[!UICONTROL 建立報告]** 的子菜單。 **[!UICONTROL 下一個]**。
1. 根據需要配置報告詳細資訊，如標題、說明、縮略圖、資料夾路徑和日期範圍。

1. 要顯示自定義列，請在「自定義列」下指定列 **[!UICONTROL 的名稱]**。

   ![指定報表的自定義列的名稱](assets/custom_columns-1.png)

1. 在 `jcr:content` 使用屬性路徑選取器的節點。 或者，在屬性路徑欄位中鍵入路徑。

   ![從jcr:content中的路徑映射屬性路徑](assets/property_picker.png)

   要添加更多自定義列，請按一下 **[!UICONTROL 添加]** 重複步驟5和6。

1. 按一下 **[!UICONTROL 建立]** 的子菜單。 消息通知已啟動報告生成。

## 配置清除服務 {#configure-purging-service}

要刪除不再需要的報告，請從Web控制台配置DAM報告清除服務，以根據現有報告的數量和年齡清除這些報告。

1. 從訪問Web控制台（配置管理器） `https://[aem_server]:[port]/system/console/configMgr`。
1. 開啟 **[!UICONTROL DAM報告清除服務]** 配置。
1. 指定清除服務的頻率（時間間隔） `scheduler.expression.name` 的子菜單。 您還可以配置報告的期限和數量閾值。
1. 儲存變更。

## 故障排除資訊、提示和限制 {#best-practices-and-limitations}

* 如果報告中的某些報告或數字不可用或不像預期的那樣，請確保 [!UICONTROL 第CQ天大壩事件記錄器] 服務已啟用。

* 刪除不再需要的報告。 使用「DAM報告清除」服務中的配置選項可配置清除報告的標準。

* 如果未生成磁碟使用情況報告，並且您正在使用 [!DNL Dynamic Media]，確保所有資產都正確運行。 要解決問題，請重新處理資產，然後再次生成報告。
