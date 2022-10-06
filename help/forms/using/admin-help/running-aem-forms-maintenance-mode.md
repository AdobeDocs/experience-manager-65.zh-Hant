---
title: 以維護模式執行AEM表單
seo-title: Running AEM forms in maintenance mode
description: 維護模式在執行修補DSC、升級AEM表單或套用Service Pack等工作時很有用。 進一步了解如何以維護模式執行AEM表單。
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

# 以維護模式執行AEM表單 {#running-aem-forms-in-maintenance-mode}

維護模式在執行修補DSC、升級AEM表單或套用Service Pack等工作時很有用。

避免在伺服器處於維護模式時調用任何進程。 如果在伺服器處於維護模式時調用進程，則會發生以下情況：

* 如果該進程已長期存在，則它將添加到作業資料庫中，但未啟動。 當您退出維護模式時，即使伺服器在維護模式中重新啟動，AEM表單仍會處理其佇列中長期存在的作業。
* 如果處理過程短暫，則會立即處理。

**將AEM表單置於維護模式**

1. 在網頁瀏覽器中，輸入：

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   瀏覽器視窗中會顯示「現已暫停」訊息。

   >[!NOTE]
   >
   >如果在伺服器處於維護模式時關閉伺服器，則重新啟動時伺服器仍處於維護模式。 完成維護任務後，必須關閉維護模式。

**檢查AEM表單是否在維護模式中執行**

1. 在網頁瀏覽器中，輸入：

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   狀態會顯示在瀏覽器視窗中。 狀態為「true」表示伺服器正在維護模式下運行，而「false」表示伺服器未處於維護模式。

**關閉維護模式**

1. 在網頁瀏覽器中，輸入：

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   瀏覽器視窗中會顯示「現在執行中」訊息。
