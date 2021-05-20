---
title: AEM Mobile On-Demand
seo-title: AEM Mobile On-Demand
description: 若要啟動新的AEM Mobile應用程式體驗，必須先具備一致的角色，才能準備好進行內容編輯。 請詳閱本頁，開始使用AEM Mobile On-Demand Services。
seo-description: 若要啟動新的AEM Mobile應用程式體驗，必須先具備一致的角色，才能準備好進行內容編輯。 請詳閱本頁，開始使用AEM Mobile On-Demand Services。
uuid: 175c609d-3cb8-4a1b-bfea-278df272e500
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: dc6891cd-19cc-4dff-8bda-a41ed8af8bfb
exl-id: 4be199d8-963d-4807-b9bb-e23fa577c5f2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 1%

---

# AEM Mobile On-Demand{#aem-mobile-on-demand}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>如果您沒有使用AEM作為內容管理來源，請參閱[AEM Mobile On-demand Services說明](https://helpx.adobe.com/digital-publishing-solution/topics.html)。

AEM提供數種工具，可讓您將內容整合至行動應用程式。

下圖說明AEM Mobile和On-Demand Services的各種元件如何搭配使用，以將內容提供至行動應用程式。

AEM預檢應用程式可視為測試環境，以在發佈前預覽應用程式和內容；而AEM Mobile應用程式是建置供發佈的最終應用程式。

>[!NOTE]
>
>若要深入了解Preflight應用程式，請參閱AEM Mobile On-demand Services說明中的[使用AEM Preflight應用程式](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html)。

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>在上圖中，一般部署案例若要部署至AEM Mobile On-demand Services，則不需要AEM Publish例項。

## 啟動新行動應用程式{#starting-a-new-mobile-app}

AEM Mobile只是構成完整AEM平台的一個支柱。

若要啟動新的AEM Mobile應用程式體驗，必須先具備一致的角色，才能準備好進行內容編輯。 下列角色提供建立新AEM Mobile應用程式的起點：

* **管理員**
* **開發人員**
* **作者**

>[!NOTE]
>
>使用AEM Mobile並依照本快速入門手冊中的步驟操作之前，請先熟悉AEM。 在這裡](/help/sites-deploying/deploy.md)了解AEM的基本知識。[

### 了解AEM Mobile應用程式控制面板{#understanding-the-aem-mobile-application-dashboard}

在了解角色和責任之前，用戶應具有對&#x200B;**AEM Mobile控制中心**&#x200B;或&#x200B;**應用程式儀表板**&#x200B;的充分了解。 按一下[這裡](/help/mobile/mobile-apps-ondemand-application-dashboard.md)了解詳情。

### AEM 管理員 {#aem-administrator}

***AEM管理員***&#x200B;負責使用建立精靈建立新應用程式或匯入現有應用程式，將新應用程式新增至AEM Mobile目錄。 使用AEM Mobile的&#x200B;*建立精靈*&#x200B;建立新應用程式的AEM管理員，通常會從現成的參考範例或（在大多數情況下）由&#x200B;*AEM開發人員建立的自訂應用程式範本中，選取所需的應用程式範本之一。*

使用AEM Mobile On-demand Services建立應用程式時，AEM管理員負責下列工作：

* [設定AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [設定您的使用者和使用者群組](/help/mobile/aem-mobile-configure-users.md)
* [使用預檢預覽](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [管理內容服務](/help/mobile/developing-content-services.md)

若要開始使用管理員的角色和責任，請參閱[管理內容以使用AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)。

## AEM開發人員{#aem-developer}

**AEM開發人員**&#x200B;擴充並建立自訂網頁範本和元件，以啟用*AEM Author *，建立美觀且吸引人的行動體驗。 這些範本和元件不僅針對行動應用程式領域而最佳化；但會同時與裝置和AEM伺服器（任何遠端伺服器）通訊至全通道服務端點。 AEM內建的內容編輯器由&#x200B;*AEM作者*&#x200B;使用，以在應用程式內建立豐富且相關的體驗，包括與Adobe Marketing Cloud其他部分的整合。

使用AEM Mobile On-demand Services建立應用程式時，AEM開發人員需負責下列工作：

* [應用程式範本和元件](/help/mobile/app-templates-and-components1.md)
* [具有內容同步的行動裝置](/help/mobile/mobile-ondemand-contentsync.md)
* [內容屬性和匯出內容](/help/mobile/on-demand-content-properties-exporting.md)
* [開發AEM Mobile內容服務](/help/mobile/developing-content-services.md)

若要開始使用開發人員的角色和責任，請參閱[開發適用於AEM Mobile On-demand Services的AEM內容](/help/mobile/aem-mobile-on-demand.md)。

>[!NOTE]
>
>*AEM開發人員的*&#x200B;角色不會從範本和元件的開發開始和結束。 *AEM開發人員*&#x200B;可建立全新的應用程式，而非只是擴充現成可用的參考實作範例。

## AEM 作者 {#aem-author}

***AEM作者*（或&#x200B;*行銷人員*）**使用自訂開發或現成可用的範本和元件，來新增和編輯頁面、拖放元件以及新增DAM中所有類型的媒體，包括影像、影片和文字片段（內容片段）。 然後&#x200B;*AEM作者*會使用AEM內建的內容編輯器，在應用程式內建立豐富且相關的體驗，包括與Adobe Marketing Cloud其餘部分的整合。

使用AEM Mobile On-demand Services建立應用程式時，AEM作者必須了解下列主題：

* [AEM Mobile應用程式控制面板](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [應用程式建立和配置操作](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [雲端設定](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [管理內容](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [內容服務概述](/help/mobile/develop-content-as-a-service.md)

若要開始使用作者的角色和責任，請參閱[為AEM Mobile On-demand Services應用程式編寫AEM內容](/help/mobile/mobile-apps-ondemand.md)。

>[!NOTE]
>
>AEM作者也負責設定權限、建立資訊卡和配置，以及傳送推播通知。 此外，如需內容製作方法的詳細資訊；管理文章和集合；在AEM Mobile中建立橫幅、卡片和配置，請參閱[AEM Mobile隨選入口網站](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2)。
