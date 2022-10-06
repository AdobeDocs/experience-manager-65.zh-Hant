---
title: 從作業管理員資料庫中清除記錄
seo-title: Purge records from the Job Manager database
description: 大型處理資料可能導致AEM表單效能下降。 當不再需要記錄時，最好清除流程資料。
seo-description: Large process data can result in lower AEM forms performance. It is good practice to purge process data when records are no longer necessary.
uuid: cf214498-36e9-4dcc-b4d4-e7c46f80dbab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 69a406f2-4fa8-40bb-b671-7b0f5b6a2c4c
exl-id: 5279f6c3-5954-472c-9ea0-18e8a7ec860e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# 從作業管理員資料庫中清除記錄 {#purge-records-from-the-job-manager-database}

調用長壽命進程時生成的進程資料可能會變得太大，導致AEM表單效能降低，並且會使用不必要的磁碟空間。 當不再需要記錄時，最好清除流程資料。

您可以使用管理控制台執行一次性清除過期記錄，或排程定期自動清除。 清除過時記錄的其他方法在 [清除流程資料](/help/forms/using/admin-help/purging-process-data.md#purging-process-data).

**訪問「作業清除調度程式」頁**

1. 在管理控制台中，按一下頁面右上角的健康監視器。
1. 按一下「作業清除計畫程式」頁簽。

有關任何當前計劃清除的資訊將顯示在「作業清除計畫程式資訊」框中。

>[!NOTE]
>
>按一下「停止排程器」會停止未來排程的任何清除，但不會停止正在進行的清除作業。

**計劃一次性清除**

1. 僅選擇一次。
1. 在「清除已完成的記錄篩選器」區域中，指定記錄被視為過時並準備清除的天數或周數。

   >[!NOTE]
   >
   >與尚未完成的進程相關的記錄不會清除，即使這些記錄早於指定的年齡。

1. 指定清除的發生時間。 選擇「使用當前日期和時間」複選框，或清除該複選框，然後按一下日曆和時鐘錶徵圖以指定執行清除的日期和時間。

   >[!NOTE]
   >
   >如果指定的開始日期和時間過去，則按一下「開始排程器」時，會立即清除。

1. 按一下「啟動排程器」。 任何先前排程的排程器設定都會取代為新設定。

**配置自動清除計畫**

1. 選擇「循環間隔」，並指定清除之間的天數或周數。
1. 在「清除已完成的記錄篩選器」區域中，指定記錄被視為過時並準備清除的天數或周數。 您無法將值設為 `0`.

   >[!NOTE]
   >
   >與尚未完成的進程相關的記錄不會清除，即使這些記錄早於指定的年齡。

1. 指定清除將於何時開始。 選擇「使用當前日期和時間」複選框，或清除該複選框，然後按一下日曆和時鐘錶徵圖以指定執行清除的日期和時間。

   >[!NOTE]
   >
   >如果您指定的開始日期和時間是過去的，AEM Forms會根據您指定的日期計算邏輯的下一個開始日期。 例如，如果您將工作清除排程為從4月7日開始每週進行，現在是4月9日，則第一次清除將發生在4月14日。

1. 按一下「啟動排程器」。 任何先前排程的排程器設定都會取代為新設定。
