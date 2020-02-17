---
title: 在維護模式中執行AEM表單
seo-title: 在維護模式中執行AEM表單
description: 在執行例如修補DSC、升級AEM表單或套用服務套件等工作時，維護模式很有用。 進一步瞭解在維護模式中執行AEM表格。
seo-description: 在執行例如修補DSC、升級AEM表單或套用服務套件等工作時，維護模式很有用。 進一步瞭解在維護模式中執行AEM表格。
uuid: 9aa3be20-f17e-4384-b4ce-daaee2898c96
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 94047c12-ba3d-457a-954f-e035c7cc3ecd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 在維護模式中執行AEM表單 {#running-aem-forms-in-maintenance-mode}

在執行例如修補DSC、升級AEM表單或套用服務套件等工作時，維護模式很有用。

避免在伺服器處於維護模式時調用任何進程。 如果在伺服器處於維護模式時調用進程，則會發生這種情況：

* 如果該過程是長期的，則它將添加到作業資料庫中，但未啟動。 當您退出維護模式時，AEM表單會處理佇列中長期存在的工作，即使伺服器在維護模式中重新啟動亦然。
* 如果流程短暫，則會立即處理。

**將AEM表單置於維護模式**

1. 在網頁瀏覽器中，輸入：

   `https://`*[hostname ]*端`:`*[口管]* 理員用戶名 `/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=`*[]*`&password=`*[口令]*

   瀏覽器視窗中會顯示「現在暫停」訊息。

   >[!NOTE]
   >
   >如果在伺服器處於維護模式時關閉伺服器，則在重新啟動伺服器時它仍處於維護模式。 完成維護任務後，必須關閉維護模式。

**檢查AEM表單是否在維護模式中執行**

1. 在網頁瀏覽器中，輸入：

   `https://`*[hostname]:[port ]*`/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=`*[administrator用戶名]* 口 `&password=`*[令&#x200B;]*

   狀態會顯示在瀏覽器視窗中。 狀態為&quot;true&quot;表示伺服器正在維護模式下運行，而&quot;false&quot;表示伺服器未處於維護模式。

**關閉維護模式**

1. 在網頁瀏覽器中，輸入：

   `https://`*[hostname]:[port ]*`/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=`*[administrator用戶名]* 口 `&password=`*[令&#x200B;]*

   瀏覽器視窗中會顯示「現在正在執行」訊息。

