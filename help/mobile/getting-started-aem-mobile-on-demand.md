---
title: Adobe Experience Manager Mobile按需
description: 啟動新的AEM Mobile應用程式體驗需要先將角色凝聚起來，然後才能準備好進行內容編輯。 按照本頁開始AEM移動按需服務。
uuid: 175c609d-3cb8-4a1b-bfea-278df272e500
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: dc6891cd-19cc-4dff-8bda-a41ed8af8bfb
exl-id: 4be199d8-963d-4807-b9bb-e23fa577c5f2
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 1%

---

# AEM Mobile按需{#aem-mobile-on-demand}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>如果您未用作AEM內容管理源，請參閱 [AEM Mobile On-demand Services幫助](https://helpx.adobe.com/digital-publishing-solution/topics.html)。

提AEM供了多種工具，使您能夠將內容整合到移動應用程式中。

下圖說明了AEM Mobile和按需服務的各個元件如何結合在一起，以便向移動應用提供內容。

印AEM前檢查應用可視為一種測試環境，在發佈前預覽應用和內容；而AEM Mobile應用是最後一款為發佈而構建的應用。

>[!NOTE]
>
>要瞭解有關印前檢查應用的詳細資訊，請參閱 [使用印AEM前檢查應用](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) 在AEM Mobile On-demand Services。

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>在上圖中，AEM發佈實例對於到AEM Mobile On-demand Services的典型部署方案不是必需的。

## 啟動新移動應用 {#starting-a-new-mobile-app}

AEM Mobile只是構成整個平台的一個支AEM柱。

啟動新的AEM Mobile應用程式體驗需要先將角色凝聚起來，然後才能準備好進行內容編輯。 以下角色為建立新的AEM Mobile應用程式提供了起點：

* **管理員**
* **開發人員**
* **作者**

>[!NOTE]
>
>在與AEM Mobile合作並遵循本入門指南中的步驟之前，用戶應該熟悉AEM。 瞭解基本信AEM息 [這裡](/help/sites-deploying/deploy.md)。

### 瞭解AEM Mobile應用程式儀表板 {#understanding-the-aem-mobile-application-dashboard}

在瞭解角色和職責之前，用戶應充分瞭解 **AEM Mobile控制中心** 或 **應用程式儀表板**。 按一下 [這裡](/help/mobile/mobile-apps-ondemand-application-dashboard.md) 來加深理解。

### AEM 管理員 {#aem-administrator}

安 ***AEM管理員*** 負責將新應用程式添加到AEM Mobile目錄，方法是使用建立嚮導建立新應用程式，或導入現有應用程式。 使用AEMAEM Mobile建立新應用的管理員 *建立嚮導* 通常從我們的現成參考示例或（在大多數情況下）由建立的自定義應用模板中選擇一個所需的應用模板 *開AEM發商。*

使用AEMAEM Mobile On-demand Services建立應用程式時，管理員負責以下任務：

* [設定AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [配置用戶和用戶組](/help/mobile/aem-mobile-configure-users.md)
* [使用印前檢查預覽](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [管理Content Services](/help/mobile/developing-content-services.md)

要開始管理員的角色和職責，請參閱 [管理內容以使用AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)。

## 開發AEM人員 {#aem-developer}

安 **開發AEM商** 擴展並建立自定義Web模板和元件，使*AEM Author *能夠建立美妙而迷人的移動體驗。 這些模板和元件不僅針對移動應用世界進行了優化；但要與設備和伺服器AEM（任何遠程伺服器）通信到全通道服務端點。 內AEM置內容編輯器由 *AEM作者* 在應用中創造豐富且相關的體驗，包括與Adobe Marketing Cloud其他地區的整合。

開發人員AEM在使用AEM Mobile On-demand Services建立應用時負責以下任務：

* [應用程式模板和元件](/help/mobile/app-templates-and-components1.md)
* [帶內容同步的移動](/help/mobile/mobile-ondemand-contentsync.md)
* [內容屬性和導出內容](/help/mobile/on-demand-content-properties-exporting.md)
* [開發AEM Mobile內容服務](/help/mobile/developing-content-services.md)

要開始瞭解開發人員的角色和職責，請參閱 [開發AEMAEM Mobile On-demand Services內容](/help/mobile/aem-mobile-on-demand.md)。

>[!NOTE]
>
>安 *開AEM發商* 角色不以模板和元件的開發開始和結束。 安 *開發AEM商* 可以建立一個全新的應用，而不是簡單地擴展現成參考實現示例。

## AEM 作者 {#aem-author}

安 ***AEM作者* 或 *營銷商*)**使用自定義開發或預置的模板和元件來添加和編輯頁面、拖放元件以及添加DAM中所有類型的媒體，包括影像、視頻和文本片段（內容片段）。 內AEM置內容編輯器隨後由 *AEM作者* 在應用中創造豐富且相關的體驗，包括與Adobe Marketing Cloud其他地區的整合。

使用AEMAEM Mobile On-demand Services建立應用程式時，作者必須瞭解以下主題：

* [AEM Mobile應用程式儀表板](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [應用程式建立和配置操作](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [雲端設定](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [管理內容](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [內容服務概述](/help/mobile/develop-content-as-a-service.md)

要開始使用作者的角色和職責，請參閱 [AEM Mobile On-demand ServicesAEM應用的創作內容](/help/mobile/mobile-apps-ondemand.md)。

>[!NOTE]
>
>AEM作者還負責設定權利、建立卡片和佈局以及發送推送通知。 另外，有關內容創作方法的更多資訊；管理文章和收藏；在AEM Mobile建立橫幅、卡片和佈局，請參閱 [AEM Mobile按需門戶](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2)。
