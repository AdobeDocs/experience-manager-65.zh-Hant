---
title: 整合 Adobe Target
seo-title: Integrating with Adobe Target
description: 瞭解如何整合AEM與Adobe Target。
seo-description: Learn about integrating AEM with Adobe Target.
uuid: b90346e8-9757-4272-a870-bbe5e647303f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 454854f8-6053-406c-888d-f427777bf570
exl-id: 2b17d8cd-a43c-4d54-b990-a6f0cb1db22b
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 1%

---

# 整合 Adobe Target{#integrating-with-adobe-target}

身為Adobe Marketing Cloud的一部分， [Adobe Target](https://www.adobe.com/ro/solutions/testing-targeting/testandtarget.html) 可讓您透過所有管道的目標定位和測量，提高內容關聯性。 行銷人員使用Adobe Target來設計和執行線上測試、建立即時受眾區段（根據行為）以及自動化內容和線上體驗的鎖定目標。 AEM已採用Adobe Target Standard中使用的目標定位工作流程。 如果您使用Target，則會熟悉AEM中的目標定位編輯環境。

將AEM網站與Adobe Target整合，以個人化頁面中的內容：

* 實作內容目標定位。
* 使用Target受眾建立個人化體驗。
* 當訪客與您的頁面互動時，將內容資料提交至Target。
* 追蹤轉換率。

若要與Target整合，請執行下列工作：

1. [執行先決條件任務](/help/sites-administering/target-requirements.md)：向Adobe Target註冊並設定AEM編寫執行個體的某些方面。 您的Adobe Target帳戶必須至少具有**核准者**層級的許可權。 此外，您必須保護發佈節點上的活動設定，讓使用者無法存取。

1. 可以：

   1. [選擇加入Adobe Target](/help/sites-administering/opt-in.md)：選擇加入精靈會考量您的Target帳戶資訊，並建立Adobe Target雲端設定和Target架構。 精靈也會將您的網站與Target架構建立關聯。 如果精靈無法連線到目標，請參閱 [連線故障診斷](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) 區段。 然後，您可以 [修改預設雲端設定](/help/sites-administering/target-configuring.md#modifying-the-opt-in-wizard-configurations)：如有必要，請修改選擇加入精靈建立的雲端設定和架構。 例如，修改架構以傳送其他內容資料至Target。 如果您想要使用Adobe Analytics做為Adobe Target的報表來源，您需要修改雲端設定以指向A4T設定。
   1. [手動與Adobe Target整合](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).

1. [設定活動](/help/sites-authoring/activitylib.md)：將您的活動與Target雲端設定建立關聯。

>[!NOTE]
>
>另請參閱 [使用DTM整合AEM與Adobe Target和Adobe Analytics](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

>[!NOTE]
>
>如果您使用具有自訂Proxy設定的Target，則需要設定HTTP使用者端Proxy設定，因為AEM的某些功能使用3.x API，而其他功能則使用4.x API：
>
>* 3.x已設定為 [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x已設定為 [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>


>[!CAUTION]
>
>您必須保護活動設定節點 **cq：ActivitySettings** ，讓一般使用者無法存取。 活動設定節點應該只能由處理活動同步至Adobe Target的服務存取。
>
>另請參閱 [與Adobe Target整合的必要條件](/help/sites-administering/target-requirements.md#securing-the-activity-settings-node) 詳細資訊。

整合完成後，您可以 [作者目標內容](/help/sites-authoring/content-targeting-touch.md) 將訪客資料傳送至Adobe Target的功能。 請注意，頁面元件需要特定程式碼才能啟用內容目標定位。 (請參閱 [針對目標內容開發](/help/sites-developing/target.md).)

>[!NOTE]
>
>當您在AEM作者中鎖定元件時，該元件會對Adobe Target發出一系列伺服器端呼叫，以註冊行銷活動、設定選件及擷取Adobe Target區段（如果已設定）。 不會從AEM發佈對Adobe Target發出伺服器端呼叫。

## 背景資訊來源 {#background-information-sources}

將AEM與Adobe Target整合需要Adobe Target、AEM Activities管理和AEM Audiences管理的知識。 您應熟悉下列資訊：

* Adobe Target (請參閱 [Adobe Target檔案](https://experienceleague.adobe.com/docs/target/using/target-home.html))。
* AEM活動主控台(請參閱 [管理活動](/help/sites-authoring/activitylib.md))。
* AEM對象(請參閱 [管理對象](/help/sites-authoring/managing-audiences.md))。

>[!NOTE]
>
>使用Adobe Target時，以下是行銷活動中允許的成品數目上限：
>
>* 50個位置
>* 2,000個體驗
>* 50個量度
>* 50個報表區段
>

