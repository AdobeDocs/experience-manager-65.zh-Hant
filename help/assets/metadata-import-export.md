---
title: 大量匯入和匯出資產中繼資料。
description: 大量匯入和匯出數位資產的中繼資料。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 2fd9a32396152eaf46e69c3141cbe1b6a69a3891

---


# 大量匯入和匯出資產中繼資料 {#import-and-export-asset-metadata-in-bulk}

[!DNL Adobe Experience Manager Assets] 可讓您使用CSV檔案大量匯入資產中繼資料。 您可以匯入CSV檔案，對最近上傳的資產或現有資產進行大量更新。 您也可以從協力廠商系統，以CSV格式大量內嵌資產中繼資料。

## 匯入中繼資料 {#import-metadata}

中繼資料匯入是非同步的，不會影響系統效能。 如果已勾選工作流程標幟，由於XMP回寫活動，同步更新多個資產的中繼資料可能會耗費大量資源。 在精簡伺服器使用期間規劃此類匯入，以免影響其他使用者的效能。

>[!NOTE]
>
>若要匯入自訂名稱空間上的中繼資料，請先註冊名稱空間。

1. 導覽至使 [!DNL Assets] 用者介面，然後按一下工 **[!UICONTROL 具列中的]** 「建立」。
1. 從功能表中，選取「中繼 **[!UICONTROL 資料]**」。
1. In the **[!UICONTROL Metadata Import]** page, click **[!UICONTROL Select File]**. 選取包含中繼資料的CSV檔案。
1. 指定下列參數：

   | 中繼資料匯入參數 | 說明 |
   |:---|:---|
   | [!UICONTROL 批次大小] | 要匯入中繼資料的批次中資產數。 預設值為 50。最大值為100。 |
   | [!UICONTROL 欄位分隔符號] | 預設值 `,` 為（逗號）。 您可以指定任何其他字元。 |
   | [!UICONTROL 多值分隔符號] | 中繼資料值的分隔符號。 預設值為 `|`. |
   | [!UICONTROL 啟動工作流程] | 預設為False。 設為且預 `true` 設的啟動程式設定對  DAM中繼資料回寫工作流程（將中繼資料寫入二進位XMP資料）有效。 啟用啟動工作流程會拖慢系統運作速度。 |
   | [!UICONTROL 資產路徑欄名稱] | 定義含資產之CSV檔案的欄名。 |

1. 從工具列點選/ **[!UICONTROL 按一下]** 「匯入」。 匯入中繼資料後，通知會傳送至您的「通知 [!UICONTROL 收件匣] 」。 導覽至資產屬性頁面，並驗證是否正確匯入資產的中繼資料值。

若要在匯入中繼資料時新增日期和時間戳記，請 `YYYY-MM-DDThh:mm:ss.fff-00:00` 使用日期和時間格式。 日期和時間以24小時 `T`格式 `hh` 的小時、納秒和時區偏移 `fff``-00:00` 分隔。 例如， `2020-03-26T11:26:00.000-07:00` 是2020年3月26日太平洋標準時間上午11:26:00.000。

>[!CAUTION]
>
>如果日期格式不符 `YYYY-MM-DDThh:mm:ss.fff-00:00`合，則不設定日期值。 匯出的中繼資料CSV檔案的日期格式為格式 `YYYY-MM-DDThh:mm:ss-00:00`。 如果要匯入，請新增以表示的納秒值，將它轉換為可接受的格式 `fff`。

## 匯出存中繼資料 {#export-metadata}

您可以匯出CSV格式的多個資產的中繼資料。 中繼資料會以非同步方式匯出，不會影響系統的效能。 若要匯出中繼資 [!DNL Experience Manager] 料，請遍歷資產節點及其子節點的 `jcr:content/metadata` 屬性，並將中繼資料屬性匯出為CSV檔案。

大量匯出中繼資料的幾個使用案例包括：

* 移轉資產時，匯入第三方系統中的中繼資料。
* 與更廣大的專案團隊共用資產中繼資料。
* 測試或稽核中繼資料以符合規範。
* 將中繼資料外部化，以便個別地區化。

1. 選取包含您要匯出中繼資料之資產的資產資料夾。 從工具列中，選擇「匯 **[!UICONTROL 出中繼資料]**」。

1. 在「中繼 [!UICONTROL 資料匯出] 」對話方塊中，指定CSV檔案的名稱。 若要匯出子檔案夾中資產的中繼資料，請選取「 **[!UICONTROL 在子檔案夾中包含資產」]**。

   ![匯出資料夾中所有資產的中繼資料的介面和選項匯](assets/export_metadata_page.png "出資料夾中所有資產的中繼資料的介面和選項")

1. 選擇所需的選項。 提供檔案名稱，並視需要提供日期。

1. 在「要 **[!UICONTROL 導出的屬性」(Properties to be exported]** )欄位中，指定要導出所有屬性還是要導出特定屬性。 如果選擇「選擇性屬性」以進行導出，請添加所需的屬性。

1. 在工具列中，按一下「 **[!UICONTROL 匯出]**」。 訊息會確認中繼資料已匯出。 關閉訊息。

1. 開啟導出作業的收件箱通知。選擇作業，然後從工具 **[!UICONTROL 欄中]** ，按一下「開啟」。To download the CSV file with the metadata, click **[!UICONTROL CSV Download]** from the toolbar. 按一下 **[!UICONTROL 關閉]**。

   ![對話方塊，以下載包含大量匯出之中繼資料的CSV檔案](assets/csv_download.png)

   *圖： 對話方塊，以下載包含大量匯出之中繼資料的CSV檔案。*

>[!MORELIKETHIS]
>
>* [在Experience Manager Assets中匯入和匯出中繼資料](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/metadata-import-feature-video-use.html)

