---
title: 在維護模式下執行AEM表單
description: 在執行如修補DSC、升級AEM表單或套用Service Pack等工作時，維護模式相當實用。 進一步瞭解如何在維護模式下執行AEM表單。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6f5ce18b-26b4-4c31-b48a-43ccbb3912f6
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# 在維護模式下執行AEM表單 {#running-aem-forms-in-maintenance-mode}

在執行如修補DSC、升級AEM表單或套用Service Pack等工作時，維護模式相當實用。

伺服器處於維護模式時，請避免叫用任何處理程式。 如果伺服器處於維護模式時叫用程式，以下是發生的情形：

* 如果處理程式是長期的，它會加入至工作資料庫，但不會啟動。 當您結束維護模式時，AEM Forms會處理其佇列中的長期工作，即使伺服器是在維護模式中重新啟動亦然。
* 如果程式是短期的，則會立即處理。

**將AEM表單置於維護模式**

1. 在網頁瀏覽器中輸入：

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   瀏覽器視窗中會顯示「現已暫停」訊息。

   >[!NOTE]
   >
   >如果您在伺服器處於維護模式時將其關閉，則伺服器重新啟動時仍會處於維護模式。 當您完成維護作業時，請關閉維護模式。

**檢查AEM表單是否以維護模式執行**

1. 在網頁瀏覽器中輸入：

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   狀態會顯示在瀏覽器視窗中。 狀態「true」表示伺服器正在維護模式中執行，而「false」表示伺服器不在維護模式中。

**關閉維護模式**

1. 在網頁瀏覽器中輸入：

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   瀏覽器視窗中會顯示「正在執行」訊息。
