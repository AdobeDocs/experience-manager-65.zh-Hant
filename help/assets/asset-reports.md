---
title: 有關您數位資產的報告
description: 瞭解AEM Assets中有關您資產的報表，以協助您瞭解數位資產的使用、活動和共用。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 70a88085a0fd6e949974aa7f1f92fdc3def3d98e

---


# 資產報表 {#asset-reports}

資產報告是評估Adobe Experience Manager(AEM)資產部署公用程式的重要工具。 有了AEM Assets，您就可以為數位資產產生各種報表。 這些報表提供您系統使用情況、使用者與資產的互動方式，以及哪些資產被下載和共用的實用資訊。

使用報表中的資訊衍生關鍵成功度量，以評估您企業內部及客戶對AEM Assets的接受度。

AEM Assets報告架構使用Sling工作以有序方式非同步處理報表請求。 它適用於大型儲存庫。 非同步報表處理可提高報表產生的效率和速度。

報表管理介面是直覺式的，包含存取已封存報表及檢視報表執行狀態（成功、失敗和佇列）的精細選項和控制項。

產生報表時，您會透過電子郵件（可選）和收件匣通知收到通知。 您可以從報表清單頁面檢視、下載或刪除報表，其中會顯示所有先前產生的報表。

## 產生報表 {#generate-reports}

AEM Assets會為您產生下列標準報表：

* 上傳
* 下載
* 過期
* 修改
* 發佈
* 品牌入口網站發佈
* 磁碟使用情況
* 檔案
* 連結共用

AEM管理員可輕鬆產生並自訂這些報表，以供您實作。 管理員可依照下列步驟產生報表：

1. 點選／按一下AEM標誌，然後前往「工 **[!UICONTROL 具]** >資 **[!UICONTROL 產]** > **[!UICONTROL 報表]**」。

![導覽資產報表](assets/AssetsReportNavigation.png)

1. 在「資產報表」頁面中，點選／按一下工 **[!UICONTROL 具列中]** 的「建立」。
1. 從「建 **[!UICONTROL 立報表]** 」頁面，選擇您要建立的報表，並點選／按「下一 **[!UICONTROL 步」]**。

   ![choose_report](assets/choose_report.png)

   >[!NOTE]
   >
   >在您產生「已下載 **[!UICONTROL 資產」報表]** ，請確定已啟用「資產下載」服務。 從Web主控台(`https://[aem_server]:[port]/system/console/configMgr`)開啟「 **[!UICONTROL Day CQ DAM Event Recorder」（日CQ DAM事件記錄器）設定，並在「事件類型」中選取「]** Asset Downloaded(DOWNLOADED) **** 」選項（如果尚未選取）。

   >[!NOTE]
   >
   >依預設，「內容片段」和連結分享會包含在「已下載資產」報表中。 選取適當的選項，以建立連結共用的報表，或從下載報表中排除內容片段。

1. 在儲存報表的CRX儲存庫中設定報表詳細資訊，例如標題、說明、縮圖和資料夾路徑。 依預設，資料夾路徑 *為/content/dam*。 您可以指定不同的路徑。

   ![report_configuration](assets/report_configuration.png)

   選擇報表的日期範圍。

   您可以選擇立即產生報表，或在未來的日期和時間產生報表。

   >[!NOTE]
   >
   >如果您選擇稍後排程報表，請確定您在「日期和時間」欄位中指定日期和時間。 如果您未指定任何值，報表引擎會將其視為要立即產生的報表。

   設定欄位可能會因您建立的報表類型而異。 例如，「磁碟使 **[!UICONTROL 用情況]** 」報表提供選項，可在計算資產使用的磁碟空間時包含資產轉譯。 您可以選擇在子資料夾中包含或排除資產，以便計算磁碟使用情況。

   >[!NOTE]
   >
   >「磁 **[!UICONTROL 碟使用情況]** 」報表不包含日期範圍欄位，因為它僅表示目前的磁碟空間使用情況。

   ![disk_usage_configuration](assets/disk_usage_configuration.png)

   當您建立「檔 **[!UICONTROL 案]** 」報表時，可以包含／排除子資料夾。 不過，您無法為此報表包含資產轉譯。

   ![files_report](assets/files_report.png)

   「連 **[!UICONTROL 結共用]** 」報表會顯示資產的URL，這些資產是從AEM Assets內與外部使用者共用的。 它包含共用資產之使用者的電子郵件ID、共用資產之使用者的電子郵件ID、連結的共用日期和到期日。 欄無法自訂。

   「連 **[!UICONTROL 結共用]** 」報表不包含子資料夾和轉譯的選項，因為它只會發佈顯示在下方的共用URL `/var/dam/share`。

   ![link_share](assets/link_share.png)

1. 從工具列點選/ **[!UICONTROL 按一下]** 「下一步」。

1. 在「設 **[!UICONTROL 定欄]** 」頁面中，某些欄會依預設顯示在報表中。 您可以選取更多欄。 取消選取選取的欄，將其排除在報表中。

   ![configure_columns](assets/configure_columns.png)

   若要顯示自訂欄名稱或屬性路徑，請在CRX的jcr:content節點下，設定資產二進位檔的屬性。 或者，透過屬性路徑選擇器加入。

   ![custom_columns](assets/custom_columns.png)

1. 從工具列點選/ **[!UICONTROL 按一下]** 「建立」。 訊息會通知報表產生已開始。
1. 在「資產報表」頁面中，報表產生狀態是根據報表工作的目前狀態，例如「成功」、「失敗」、「已佇列」或「已排程」。 通知收件匣中會顯示相同的狀態。若要檢視報表頁面，請點選／按一下報表連結。 或者，選取報表，並從工具列點選 **[!UICONTROL 「檢視]** 」。

   ![report_page](assets/report_page.png)

   從工 **[!UICONTROL 具列點選]** 「下載」，以下載CSV格式的報表。

## 新增自訂欄 {#add-custom-columns}

您可以新增自訂欄至下列報表，以顯示更多符合自訂需求的資料：

* 上傳
* 下載
* 過期
* 修改
* 發佈
* 品牌入口網站發佈
* 檔案

1. 點選／按一下AEM標誌，然後前往「工 **[!UICONTROL 具]** >資 **[!UICONTROL 產]** > **[!UICONTROL 報表]**」。
1. 在「資產報表」頁面中，點選／按一下工 **[!UICONTROL 具列中]** 的「建立」。

1. 從「建 **[!UICONTROL 立報表]** 」頁面，選擇您要建立的報表，並點選／按「下一 **[!UICONTROL 步」]**。
1. 視需要設定報表詳細資訊，例如標題、說明、縮圖、資料夾路徑和日期範圍。

1. 要顯示自定義列，請在「自定義列」下指定列 **[!UICONTROL 的名稱]**。

   ![custom_columns-1](assets/custom_columns-1.png)

1. 使用屬性路徑選擇器在CRXDE `jcr:content` 的節點下添加屬性路徑。 或者，在屬性路徑欄位中鍵入路徑。

   ![property_picker](assets/property_picker.png)

   若要新增更多自訂欄，請點選／按 **[!UICONTROL 一下]** 「新增」，然後重複步驟5和6。

1. 從工具列點選/ **[!UICONTROL 按一下]** 「建立」。 訊息會通知報表產生已開始。

## 配置清除服務 {#configure-purging-service}

若要移除不再需要的報表，請從Web主控台設定DAM報表清除服務，以根據現有報表的數量和年齡來清除報表。

1. 從訪問Web控制台（配置管理器） `https://[aem_server]:[port]/system/console/configMgr`。
1. 開啟「 **[!UICONTROL DAM報表清除服務]** 」設定。
1. 在欄位中指定清除服務的頻率（時間間隔） `scheduler.expression.name` 。 您也可以設定報表的年齡和數量臨界值。
1. 儲存變更。
