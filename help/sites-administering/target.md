---
title: 整合 Adobe Target
seo-title: Integrating with Adobe Target
description: 瞭解與AEMAdobe Target的整合。
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

作為Adobe Marketing Cloud的一部分， [Adobe Target](https://www.adobe.com/ro/solutions/testing-targeting/testandtarget.html) 允許您通過針對所有渠道進行定位和測量來提高內容相關性。 Adobe Target被營銷人員用於設計和執行線上test、建立即時（基於行為）受眾群，以及自動確定內容和線上體驗的目標。 採AEM用了Adobe Target標準的目標工作流程。 如果使用「目標」，您將熟悉中的目標編輯環AEM境。

將您的站AEM點與Adobe Target整合，以個性化頁面中的內容：

* 實施內容目標。
* 使用目標受眾建立個性化體驗。
* 訪問者與您的頁面交互時，將上下文資料提交到目標。
* 跟蹤轉換率。

要與目標整合，請執行以下任務：

1. [執行必備任務](/help/sites-administering/target-requirements.md):向Adobe Target註冊並配置作者實例的AEM某些方面。 您的Adobe Target帳戶必須至少具有**批准者**級別權限。 此外，必須保護發佈節點上的活動設定，以便用戶無法訪問該活動設定。

1. 可以：

   1. [選擇加入Adobe Target](/help/sites-administering/opt-in.md):選擇加入嚮導將獲取目標帳戶資訊並建立Adobe Target雲配置和目標框架。 嚮導還將您的站點與目標框架相關聯。 如果嚮導無法連接到目標，請參閱 [連接故障](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) 的子菜單。 你可以 [修改預設雲配置](/help/sites-administering/target-configuring.md#modifying-the-opt-in-wizard-configurations):如有必要，請修改選擇加入嚮導建立的雲配置和框架。 例如，修改框架以將附加上下文資料發送到目標。 如果要將Adobe Analytics用作Adobe Target的報告源，則需要修改雲配置以指向A4T配置。
   1. [手動與Adobe Target整合](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target)。

1. [配置活動](/help/sites-authoring/activitylib.md):將活動與目標雲配置關聯。

>[!NOTE]
>
>另請參閱 [使用AEMDTM與Adobe Target和Adobe Analytics整合](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html)。

>[!NOTE]
>
>如果將目標與自定義代理配置一起使用，則需要配置兩個HTTP客戶端代理配置AEM，因為其中的某些功能使用3.x API，而其他功能則使用4.x API:
>
>* 3.x配置 [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x配置 [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>


>[!CAUTION]
>
>必須保護活動設定節點的安全 **cq：活動設定** 在發佈實例上，以便普通用戶無法訪問。 活動設定節點只能由處理與Adobe Target的活動同步的服務訪問。
>
>請參閱 [與Adobe Target整合的先決條件](/help/sites-administering/target-requirements.md#securing-the-activity-settings-node) 的上界。

整合完成後，您可以 [作者目標內容](/help/sites-authoring/content-targeting-touch.md) 把訪問者資料發送到Adobe Target。 請注意，頁面元件需要特定代碼才能啟用內容目標。 (請參閱 [為目標內容開發](/help/sites-developing/target.md)。)

>[!NOTE]
>
>當您針對作者中的元件AEM時，該元件會向Adobe Target發出一系列伺服器端呼叫，以註冊市場活動、設定優惠和檢索Adobe Target段（如果已配置）。 發佈到Adobe Target時不會進行AEM伺服器端呼叫。

## 背景資訊源 {#background-information-sources}

與AEMAdobe Target的整合需要Adobe Target、AEM活動管理AEM和受眾管理。 您應熟悉以下資訊：

* Adobe Target(請參閱 [Adobe Target文檔](https://experienceleague.adobe.com/docs/target/using/target-home.html))。
* 活AEM動控制台(請參閱 [管理活動](/help/sites-authoring/activitylib.md))。
* 觀AEM眾(請參閱 [管理受眾](/help/sites-authoring/managing-audiences.md))。

>[!NOTE]
>
>使用Adobe Target時，以下是市場活動中允許的最大工件數：
>
>* 50個地點
>* 2,000次經驗
>* 50個指標
>* 50個報告分部
>

