---
title: 整合 Adobe Target
seo-title: Integrating with Adobe Target
description: 了解如何整合AEM與Adobe Target。
seo-description: Learn about integrating AEM with Adobe Target.
uuid: b90346e8-9757-4272-a870-bbe5e647303f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 454854f8-6053-406c-888d-f427777bf570
exl-id: 2b17d8cd-a43c-4d54-b990-a6f0cb1db22b
source-git-commit: 37d2c70bff770d13b8094c5959e488f5531aef55
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 1%

---

# 整合 Adobe Target{#integrating-with-adobe-target}

作為Adobe Marketing Cloud的一部分， [Adobe Target](https://www.adobe.com/ro/solutions/testing-targeting/testandtarget.html) 可讓您透過鎖定目標和測量所有管道，來提升內容關聯性。 行銷人員使用Adobe Target來設計和執行線上測試、建立即時受眾區段（根據行為），以及自動鎖定內容和線上體驗。 AEM已採用Adobe Target Standard中使用的鎖定工作流程。 如果您使用Target，您將熟悉AEM中的目標編輯環境。

將您的AEM網站與Adobe Target整合，以個人化您頁面中的內容：

* 實作內容鎖定目標。
* 使用Target受眾建立個人化體驗。
* 當訪客與您的頁面互動時，將內容資料提交至Target。
* 追蹤轉換率。

若要與Target整合，請執行下列工作：

1. [執行先決條件任務](/help/sites-administering/target-requirements.md):向Adobe Target註冊，並設定AEM製作例項的某些方面。 您的Adobe Target帳戶至少必須具**核准**級權限。 此外，您必須保護發佈節點上的活動設定，讓使用者無法存取該設定。

1. 其中之一：

   1. [選擇加入Adobe Target](/help/sites-administering/opt-in.md):選擇加入精靈會擷取您的Target帳戶資訊，並建立Adobe Target雲端設定和Target架構。 精靈也會將您的網站與Target架構建立關聯。 如果嚮導無法連接到目標，請參閱 [連接故障排除](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) 區段。 然後 [修改預設雲配置](/help/sites-administering/target-configuring.md#modifying-the-opt-in-wizard-configurations):如有必要，請修改選擇加入精靈建立的雲端設定和架構。 例如，修改框架以傳送其他內容資料至Target。 如果您想要使用Adobe Analytics做為Adobe Target的報表來源，需要修改雲端設定以指向A4T設定。
   1. [手動整合Adobe Target](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).

1. [設定活動](/help/sites-authoring/activitylib.md):將活動與Target雲端設定建立關聯。

>[!NOTE]
>
>另請參閱 [使用DTM整合AEM與Adobe Target和Adobe Analytics](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

>[!NOTE]
>
>如果您使用Target搭配自訂的代理設定，您需要設定兩個HTTP用戶端代理設定，因為AEM的某些功能使用3.x API，而其他一些則使用4.x API:
>
>* 3.x的設定 [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x的設定 [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>


>[!CAUTION]
>
>您必須保護活動設定節點的安全 **cq:ActivitySettings** 發佈例項，使一般使用者無法存取。 處理活動同步至Adobe Target的服務只應能存取活動設定節點。
>
>請參閱 [與Adobe Target整合的必要條件](/help/sites-administering/target-requirements.md#securing-the-activity-settings-node) 以取得詳細資訊。

整合完成時，您可以 [作者目標內容](/help/sites-authoring/content-targeting-touch.md) 會將訪客資料傳送至Adobe Target。 請注意，頁面元件需要特定的程式碼才能啟用內容鎖定目標。 (請參閱 [針對目標內容開發](/help/sites-developing/target.md).)

>[!NOTE]
>
>當您在AEM作者中定位元件時，元件會向Adobe Target發出一系列伺服器端呼叫，以註冊促銷活動、設定選件及擷取Adobe Target區段（如果已設定）。 不會從AEM發佈至Adobe Target進行伺服器端呼叫。

## 背景資訊來源 {#background-information-sources}

將AEM與Adobe Target整合需要Adobe Target、AEM活動管理和AEM對象管理的相關知識。 您應熟悉下列資訊：

* Adobe Target(請參閱 [Adobe Target檔案](https://docs.adobe.com/content/help/en/target/using/target-home.html))。
* AEM活動主控台(請參閱 [管理活動](/help/sites-authoring/activitylib.md))。
* AEM對象(請參閱 [管理對象](/help/sites-authoring/managing-audiences.md))。

>[!NOTE]
>
>使用Adobe Target時，以下是促銷活動中允許的成品數量上限：
>
>* 50個地點
>* 2,000個體驗
>* 50個量度
>* 50個報告區段
>

