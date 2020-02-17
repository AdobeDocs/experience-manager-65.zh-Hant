---
title: 與Adobe Target整合
seo-title: 與Adobe Target整合
description: 瞭解如何將AEM與Adobe Target整合。
seo-description: 瞭解如何將AEM與Adobe Target整合。
uuid: b90346e8-9757-4272-a870-bbe5e647303f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 454854f8-6053-406c-888d-f427777bf570
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 與Adobe Target整合{#integrating-with-adobe-target}

作為Adobe Marketing cloud的一部分， [Adobe Target](http://www.adobe.com/ro/solutions/testing-targeting/testandtarget.html) 可讓您透過跨所有通道的鎖定和測量來提升內容關聯性。 行銷人員使用Adobe target來設計和執行線上測試、建立即時受眾細分（根據行為）並自動鎖定內容和線上體驗。 AEM已採用Adobe Target Standard中使用的定位工作流程。 如果您使用Target，您將熟悉AEM中的定位編輯環境。

將您的AEM網站與Adobe target整合，以個人化頁面內容：

* 實作內容定位。
* 使用Target受眾建立個人化體驗。
* 當訪客與您的頁面互動時，將上下文資料提交至Target。
* 追蹤轉換率。

若要與Target整合，請執行下列工作：

1. [執行先決條件任務](/help/sites-administering/target-requirements.md):向Adobe target註冊，並設定AEM作者例項的某些方面。 您的Adobe target帳戶至少必須擁有**核准者**層級權限。 此外，您必須保護發佈節點上的活動設定，讓使用者無法存取。

1. 其中之一：

   1. [選擇加入Adobe Target](/help/sites-administering/opt-in.md):選擇加入精靈會取用您的Target帳戶資訊，並建立Adobe Target雲端設定和Target Framework。 此精靈也會將您的網站與Target Framework建立關聯。 如果嚮導無法連接到目標，請參閱「連 [接故障診斷](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) 」部分。 然後，您可 [以修改預設雲端設定](/help/sites-administering/target-configuring.md#modifying-the-opt-in-wizard-configurations):如有必要，請修改選擇加入精靈所建立的雲端設定和架構。 例如，修改框架以傳送其他上下文資料至Target。 如果您想要將Adobe Analytics用作Adobe target的報表來源，則必須修改雲端設定以指向A4T設定。
   1. [手動與Adobe Target整合](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target)。

1. [設定活動](/help/sites-authoring/activitylib.md):將您的活動與Target雲端設定關聯。

>[!NOTE]
>
>另請參 [閱「使用DTM整合AEM與Adobe Target和Adobe Analytics](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html)」。

>[!NOTE]
>
>如果您將Target與自訂的Proxy設定搭配使用，則需要設定兩個HTTP Client Proxy設定，因為AEM的某些功能是使用3.x API，而其他部分則使用4.x API:
>
>* 3.x已設定為 [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x已設定為 [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>



>[!CAUTION]
>
>您必須保護發佈例項上的活動設 **定節點cq:ActivitySettings** ，如此一般使用者便無法存取它。 處理Adobe Target活動同步的服務只能訪問活動設定節點。
>
>如需詳 [細資訊，請參閱與Adobe target整合的必要條件](/help/sites-administering/target-requirements.md#securing-the-activity-settings-node) 。

整合完成後，您可以製作將 [訪客資料傳送](/help/sites-authoring/content-targeting-touch.md) 至Adobe Target的目標內容。 請注意，頁面元件需要特定的程式碼才能啟用內容定位。 (請參 [閱開發目標內容](/help/sites-developing/target.md)。)

>[!NOTE]
>
>當您在AEM作者中定位元件時，元件會對Adobe Target進行一連串的伺服器端呼叫，以註冊促銷活動、設定選件及擷取Adobe Target區段（如果已設定）。 AEM發佈至Adobe Target時，不會進行伺服器端呼叫。

## 背景資訊來源 {#background-information-sources}

將AEM與Adobe target整合需要具備Adobe Target、AEM活動管理和AEM觀眾管理的相關知識。 您應熟悉下列資訊：

* Adobe Target(請參閱 [Adobe Target檔案](https://marketing.adobe.com/resources/help/en_US/target/))。
* AEM活動主控台(請參 [閱管理活動](/help/sites-authoring/activitylib.md))。
* AEM觀眾(請參閱 [管理觀眾](/help/sites-authoring/managing-audiences.md))。

>[!NOTE]
>
>使用Adobe Target時，下列是促銷活動中允許的最大對象數：
>
>* 50個地點
>* 2,000次體驗
>* 50個量度
>* 50個報告分部
>



