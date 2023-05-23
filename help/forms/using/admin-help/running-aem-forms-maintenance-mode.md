---
title: 在維AEM護模式下運行表單
seo-title: Running AEM forms in maintenance mode
description: 維護模式在執行任務(如修補DSC、升級表AEM單或應用Service Pack)時非常有用。 瞭解有關在維護模AEM式下運行表單的詳細資訊。
seo-description: Maintenance mode is useful when performing tasks such as patching a DSC, upgrading AEM forms, or applying a service pack. Learn more about running AEM forms in maintenance mode.
uuid: 9aa3be20-f17e-4384-b4ce-daaee2898c96
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 94047c12-ba3d-457a-954f-e035c7cc3ecd
exl-id: 6f5ce18b-26b4-4c31-b48a-43ccbb3912f6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# 在維AEM護模式下運行表單 {#running-aem-forms-in-maintenance-mode}

維護模式在執行任務(如修補DSC、升級表AEM單或應用Service Pack)時非常有用。

避免在伺服器處於維護模式時調用任何進程。 如果在伺服器處於維護模式時調用進程，則會發生以下情況：

* 如果該進程是長期的，則它會添加到作業資料庫中，但不會啟動。 退出維護模式時，AEM表單會處理其隊列中的長時間作業，即使伺服器在維護模式下重新啟動也是如此。
* 如果該過程是短期的，則立即進行處理。

**將表AEM單置於維護模式**

1. 在Web瀏覽器中，輸入：

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   瀏覽器窗口中顯示「立即暫停」消息。

   >[!NOTE]
   >
   >如果在伺服器處於維護模式時關閉伺服器，則重新啟動伺服器時伺服器仍將處於維護模式。 完成維護任務後，必須關閉維護模式。

**檢查表AEM單是否在維護模式下運行**

1. 在Web瀏覽器中，輸入：

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   狀態顯示在瀏覽器窗口中。 狀態為「true」表示伺服器正在維護模式下運行，「false」表示伺服器未處於維護模式。

**關閉維護模式**

1. 在Web瀏覽器中，輸入：

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   在瀏覽器窗口中顯示「現在正在運行」消息。
