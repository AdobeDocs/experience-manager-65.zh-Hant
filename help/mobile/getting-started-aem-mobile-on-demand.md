---
title: Adobe Experience Manager Mobile On-Demand
description: 開始新的Adobe Experience Manager (AEM)行動應用程式體驗需要角色的內在性，才能準備好進行內容編輯。 請依照本頁面的說明開始使用AEM Mobile On-Demand Services。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
exl-id: 4be199d8-963d-4807-b9bb-e23fa577c5f2
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 1%

---

# AEM Mobile On-Demand{#aem-mobile-on-demand}

{{ue-over-mobile}}

>[!NOTE]
>
>如果您未使用Adobe Experience Manager (AEM)作為內容管理來源，請參閱[AEM Mobile On-demand Services說明](https://helpx.adobe.com/tw/digital-publishing-solution/topics.html)。

AEM提供數種工具，可讓您將內容整合至行動應用程式。

下圖說明AEM Mobile和On-Demand Services的各種元件如何搭配使用，以將內容傳送至行動應用程式。

AEM Preflight應用程式可視為測試環境，可在發佈前預覽應用程式和內容；而AEM Mobile應用程式則是針對發佈而建立的最終應用程式。

>[!NOTE]
>
>若要深入瞭解預檢應用程式，請參閱AEM Mobile On-demand Services說明中的[使用AEM預檢應用程式](https://helpx.adobe.com/tw/digital-publishing-solution/help/preflight-app.html)。

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>在上圖中，對AEM Mobile On-demand Services的典型部署案例不需要AEM Publish執行個體。

## 啟動新的行動應用程式 {#starting-a-new-mobile-app}

AEM Mobile只是構成完整AEM平台的支柱之一。

開始新的AEM Mobile應用程式體驗需要先內建多個角色，才能準備好編輯內容。 下列角色提供建立AEM Mobile應用程式的起點：

* **管理員**
* **開發人員**
* **作者**

>[!NOTE]
>
>在使用AEM Mobile並按照本快速入門手冊中的步驟操作之前，使用者應該熟悉AEM。 在[這裡](/help/sites-deploying/deploy.md)瞭解AEM的基本概念。

### 瞭解AEM Mobile應用程式控制面板 {#understanding-the-aem-mobile-application-dashboard}

在瞭解角色和職責之前，使用者應該完全瞭解&#x200B;**AEM Mobile控制中心**&#x200B;或&#x200B;**應用程式儀表板**。 如需深入瞭解，請按一下[這裡](/help/mobile/mobile-apps-ondemand-application-dashboard.md)。

### AEM 管理員 {#aem-administrator}

***AEM管理員***&#x200B;負責使用建立精靈建立應用程式，或匯入現有應用程式，將應用程式新增至AEM Mobile目錄。 使用AEM Mobile的&#x200B;*建立精靈*&#x200B;建立應用程式的AEM管理員通常會從Adobe現成的參考範例或（通常）由&#x200B;*AEM開發人員建立的自訂應用程式範本中，選取其中一個想要的應用程式範本。*

使用AEM Mobile On-demand Services建立應用程式時，AEM管理員會負責下列工作：

* [設定AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [設定使用者與使用者群組](/help/mobile/aem-mobile-configure-users.md)
* [使用預檢預覽](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [管理內容服務](/help/mobile/developing-content-services.md)

若要開始使用管理員的角色和責任，請參閱[管理內容以使用AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)。

## AEM開發人員 {#aem-developer}

**AEM開發人員**&#x200B;延伸並建立自訂的網頁範本和元件，以讓*AEM作者*建立美觀且吸引人的行動體驗。 這些範本和元件不僅已針對行動應用程式世界最佳化，而且可與裝置和AEM伺服器（任何遠端伺服器）通訊，以連線全通路服務端點。 *AEM作者*&#x200B;使用AEM的內建內容編輯器在應用程式中建立豐富的相關體驗，包括與Adobe Experience Cloud其他部分的整合。

使用AEM Mobile On-demand Services建立應用程式時，AEM開發人員會負責下列工作：

* [應用程式範本和元件](/help/mobile/app-templates-and-components1.md)
* [具有內容同步功能的行動裝置](/help/mobile/mobile-ondemand-contentsync.md)
* [內容屬性和匯出內容](/help/mobile/on-demand-content-properties-exporting.md)
* [開發AEM Mobile內容服務](/help/mobile/developing-content-services.md)

若要開始使用開發人員的角色和責任，請參閱[為AEM Mobile On-demand Services開發AEM內容](/help/mobile/aem-mobile-on-demand.md)。

>[!NOTE]
>
>*AEM開發人員的*&#x200B;角色並非以範本和元件的開發開始和結束。 *AEM開發人員*&#x200B;可以建立全新的應用程式，而不只是擴充現成的參考實作範例。

## AEM 作者 {#aem-author}

***AEM作者* （或&#x200B;*行銷人員*）**&#x200B;會使用自訂開發或現成可用的範本和元件來新增及編輯頁面、拖放元件，以及從DAM新增所有型別的媒體，包括影像、影片和文字片段（內容片段）。 然後&#x200B;*AEM作者*會使用AEM的內建內容編輯器在應用程式中建立豐富的相關體驗，包括與Adobe Experience Cloud其他部分的整合。

使用AEM Mobile On-demand Services建立應用程式時，AEM作者必須瞭解下列主題：

* [AEM Mobile應用程式控制面板](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [應用程式建立和設定動作](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [雲端設定](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [管理內容](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [Content Service概述](/help/mobile/develop-content-as-a-service.md)

若要開始使用作者的角色和責任，請參閱[為AEM Mobile On-demand Services應用程式編寫AEM內容](/help/mobile/mobile-apps-ondemand.md)。

>[!NOTE]
>
>AEM作者也負責設定權益、建立卡片和版面配置，以及傳送推播通知。 此外，如需內容製作方法的詳細資訊；管理文章和集合；在AEM Mobile中建立橫幅、卡片和版面，請參閱[AEM Mobile隨選入口網站](https://helpx.adobe.com/tw/digital-publishing-solution/topics.html#dynamicpod_reference_2)。
