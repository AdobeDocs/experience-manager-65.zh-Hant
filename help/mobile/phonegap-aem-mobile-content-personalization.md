---
title: AEM mobile內容個人化
seo-title: AEM mobile內容個人化
description: 請依照本頁瞭解AEM mobile內容個人化功能，這項功能可讓AEM作者運用Adobe Target個人化行動應用程式內容。
seo-description: 請依照本頁瞭解AEM mobile內容個人化功能，這項功能可讓AEM作者運用Adobe Target個人化行動應用程式內容。
uuid: 9078edd1-8399-485f-8a63-a07e766f7ef9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c9c818dc-c5c4-4a96-94fe-9dc9fe75705b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM mobile內容個人化{#aem-mobile-content-personalization}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>本檔案是「AEM Mobile快速入門手冊」( [](/help/mobile/getting-started-aem-mobile.md) AEM Mobile參考的建議起點)的一部分。

AEM mobile內容個人化功能可讓 [AEM作者運用](#author) Adobe Target [，個人化行動應用程式內容](https://www.adobe.com/ca/marketing-cloud/testing-targeting.html)。 這可讓針對行動應用程式使用者傳遞目標選件。 Adobe Experience Manager mobile提供建立、鎖定和傳遞內容的能力，為使用者提供符合其個人喜好的內容。

和AEM中的常見情況一樣，為了讓作者開始建立此內容，管理員和開發人員必須先準備環境。

[AEM管理員](#administrator) 必須建立AEM mobile與Adobe Target cloud服務之間的連線。

同時，AEM Mobile開發人 [員需要修改其現有的指令碼](#developer) ，以利製作目標明確的內容。

## 針對管理員 {#for-administrators}

在內容作者開始為行動應用程式產生目標內容之前，需要先整合許多步驟：您可以為使用者和群組取得適當的權限集、建立雲端服務、設定活動的應用程式，最後產生內容。

本文將引導您完成設定 [AEM Mobile Hybrid Reference Application以進行定位的程式](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 。

未來的假設是，AEM Mobile Hybrid Reference Application已成功部署並可透過AEM Mobile儀表板存取。

作者必須先使用Adobe Target cloud服務設定您的AEM實 [例，才能在應用程式中產生目標內容。](/help/mobile/aem-mobile-configuring-cloud-service.md)

### 權限 {#permissions}

需要存取個人化主控台的使用者必須屬於群組的一 `target-activity-authors` 部分。

建議在使用者和群組設定中，將target-activity-group新增至應用程式管理員群組。 新增target-activity-authors群組，可讓使用者查看個人化導覽功能表項目。

>[!NOTE]
>
>忘記將您想要擁有個人化管理控制台存取權的使用者或群組新增至target-activity-authors群組，將會防止使用者看到個人化主控台。

### 雲端服務 {#cloud-services}

若要讓針對行動應用程式的目標內容運作，需要設定兩項服務：Adobe Target服務和Adobe Mobile services服務。 Adobe Target服務提供處理用戶端要求及傳回個人化內容的引擎。 Adobe Mobile services服務透過ADBMobileConfig.json檔案（由AMS Cordova增效模組使用）提供Adobe服務與行動應用程式之間的連線。 從AEM Mobile Dashboard，您可以新增兩個服務來設定您的應用程式。

從AEM Mobile Dashboard找到「管理雲端服務」，然後按一下+按鈕。

![chlimage_1-38](assets/chlimage_1-38.png)

從「新增雲端服務」精靈中，選取「Adobe Target」雲端服務卡，然後按「下一步」。

![chlimage_1-39](assets/chlimage_1-39.png)

從「選擇配置」下拉式清單中，您可以建立新的配置或從現有的配置中選擇。 要建立新配置，請從下拉清單中選擇「建立配置」。 輸入Target設定的標題。 輸入您的客戶代碼、電子郵件和密碼，這些程式碼與您的Target帳戶相關聯。 如果您不知道這些欄位的值，請連絡Adobe Target支援。 按一下「驗證」按鈕以驗證憑據。 在驗證後，按一下「提交」按鈕以建立雲端服務。

>[!NOTE]
>
>建立的雲端服務會透過精靈自動與行動應用程式關聯。 cq:cloudserviceconfiges屬性值會設定在應用程式群組節點的jcr:content節點上。 對於混合應用程式範例，它會設定在/content/mobileapps/hybrid-reference-app/jcr:content上，其值指向位於/etc/cloudservices/testandtarget/adobe-target—aem-apps/framework的自動產生的架構節點。 框架節點預設設定兩個屬性，性別和年齡。 此架構僅供AEM預覽使用，對裝置沒有任何影響。

精靈完成後，「管理雲端服務」方塊將包含Target雲端服務，但包含有關遺失Adobe Mobile服務帳戶的警告。

![chlimage_1-40](assets/chlimage_1-40.png)

### Adobe Mobile Services {#adobe-mobile-services}

AMS服務也必須將Adobe Mobile Services(AMS)帳戶連結至應用程式，提供必要的ADBMobileConfig.json檔案，其中包含Target用戶端程式碼資訊。 在建立與AMS帳戶的關聯之前，AMS帳戶需要由具有AMS權限的使用者修改。

### 用戶端代碼 {#client-code}

若要登入AMS服務，請造 [訪https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/)，選取行動應用程式，然後按一下設定。 找到「SDK目標選項」欄位，並將用戶端程式碼放入欄位中，然後按一下「儲存」。

![chlimage_1-41](assets/chlimage_1-41.png)

現在用戶端程式碼已與行動應用程式關聯，當透過Adobe Mobile Dashboard設定AMS雲端服務時，服務設定的設定將會透過ADBMobileConfig.json檔案傳送。

### Adobe Mobile Service cloud服務 {#adobe-mobile-service-cloud-service}

現在已設定AMS，是時候在Adobe Mobile Dashboard中建立行動應用程式的關聯了。 從AEM Mobile Dashboard找到「管理雲端服務」，然後按一下+按鈕。

![chlimage_1-42](assets/chlimage_1-42.png)

選取Adobe Mobile services卡，然後按一下「下一步」。

![chlimage_1-43](assets/chlimage_1-43.png)

從「建立」或「選取」精靈步驟中，選取「Mobile Service」下拉式清單，並選取「建立設定」項目。 提供標題、公司、使用者名稱、密碼，並選取適當的資料中心。 如果您不知道這些值，請連絡您的Adobe Mobile服務管理員以取得這些值。 填寫完所有欄位後，按一下「驗證」按鈕。 驗證程式會移至AMS並驗證帳戶的憑證，一旦成功驗證，就會填入行動應用程式清單，您可從下拉式清單中選取關聯的行動應用程式。 按一下「提交」按鈕以完成嚮導。 此程式可能需要一些時間才能取得設定資料以及與應用程式相關的任何分析。 完成程式後，按一下模型中的「完成」按鈕，返回Adobe Mobile Dashboard。

「管理雲端服務」圖格會返回Mobile Dashboard，其中包含AMS雲端服務。 您也會注意到，「分析量度」方塊將會填入生命週期報表。

![chlimage_1-44](assets/chlimage_1-44.png)

## 針對作者 {#for-authors}

**** 先決條件：如上所述，管理員必須先設定Adobe Target服務的連線，作者才能產生新的目標內容。

一旦管理員設定了兩個雲端服務，而開發人員已設定了mobileapporfers處理常式，內容作者現在就可以開始產生目標體驗。

在AEM mobile應用程式中製作目標內容時，會遵循類似的程式來製作AEM Sites:

請參閱此處以取得有關在AEM中編寫 [目標內容的完整概觀](/help/sites-authoring/personalization.md)

## 針對開發人員 {#for-developers}

建立行動應用程式的AEM開發人員在開發元件時，應繼續遵循AEM中常用的模式。 在此，我們將逐步引導您執行必要步驟，讓內容作者建立目標內容：

### Adobe Target ContentSync處理常式 {#adobe-target-contentsync-handlers}

若要將內容傳送至使用者的裝置內容，請轉譯由AEM內容作者建立的選件。 若要處理目標選件的轉譯，有新的內容同步處理常式會處理選件。 以Hybrid Reference Application為範例，en（英文）內容套件包含ContentSyncConfig和 [mobileapporfers處理常式](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) 。 下一步是向裝置轉譯選件的關鍵。 Mobileapporfers處理常式具有path屬性，可識別要用於應用程式的個人化活動路徑。

例如，如果有位於 */content/campaigns/hybridref的活動複製此路徑，並將其貼為值至mobileapporfers處理常式的*** path屬性。

>[!NOTE]
>
>對於混合參考應用程式，有兩個mobileapporfer處理常式，一個用於開發，另一個用於製作。

在mobileapporfers處理常式的path屬性中設定活動路徑後，會儲存處理常式。 處理常式現在已準備好開始轉換我們行動裝置的選件。

### 演算模式 {#render-mode}

Mobileapporfers處理常式的設定與發佈和開發設定不同。 對於發佈設定，有一個名 *為renderMode* 的屬性，其值 ** 在cq:ContentSyncConfig節點上設定。 Mobileapporfers處理常式會參考renderMode，如果設為publish，則會修改建立的mbox ID。 依預設，由AEM建立的mbox會在mbox ID中附加一個—author值。 這可識別活動尚未發佈，且應使用未發佈的促銷活動來解決選件。

當內容透過Adobe Mobile Dashboard進行轉移時，轉移內容會被視為生產就緒內容，並會透過非開發內容同步設定轉譯。 以此方式呈現會導致-author從所有mbox ID中移除，並預期Target伺服器上會有已發佈的活動。 測試分段內容之前，請確定活動已發佈。

### 個人化應用程式開發 {#personalization-app-development}

#### 元件 {#components}

任何內容的基礎通常是頁面元件，可依您使用的是HTL或JSP，延伸其中一個基本AEM頁面元件wcm/foundation/components/page或foundation/components/page。 這些步驟的持續時間將著重於使用wcm/foundation/components/page元件。 頁面元件的基本結構會細分為多個指令碼，每個指令碼都提供特定用途，讓開發人員視需要組織及覆寫其程式碼。 個人化最感興趣的兩個指令碼是head.html和body.html。 這兩個指令碼提供可插入程式碼的區域，以支援內容中樞、雲端服務和行動內容製作。

以下是用於啟用內容定位的兩個主要指令碼的概述。

#### head.html {#head-html}

為了讓作者能夠定位其內容，必須將目標功能表新增至頁面，讓作者可以將內容從編輯模式變更為定位模式。 若要啟用此功能，開發人員應修改head.html指令碼，將下列程式碼片段加入head.html頂端附近，或盡可能加入&lt;title>&lt;/title>元素。

```xml
<meta data-sly-test="${!wcmmode.disabled}">
    <div data-sly-call="${clientLib.all @ categories='personalization.kernel'}" data-sly-unwrap></div>
    <div data-sly-resource="${'config' @ resourceType='cq/personalization/components/clientcontext_optimized/config'}" data-sly-unwrap></div>
    <div data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}" data-sly-unwrap></div>
</meta>
```

>[!NOTE]
>
>請注意，只有在WCM模式未停用時才應包含指令碼，如此當WCM模式停用時（如需詳細資訊，請參閱ContentSync處理常式的章節），指令碼才不會包含在最終的應用程式碼中。

若要讓作者能夠預覽目標內容，編輯者必須能夠找到Adobe Target雲端服務的設定。 下面的代碼塊添加了兩個重要的指令碼。 第一個新增頁面尋找相關Target雲端服務並呼叫Adobe Target的功能。 第二個是新增cq.apps.targeting類別。

cq.apps.targeting **** 類別會覆寫預設的cq/personalization/component/target元件，並使用mobileapps/components/target元件來呈現特別用於行動應用程式使用的選件。 有關此項的詳細資訊，請參閱「目標元件」區段。

程式碼應新增至head.html中，並置於&lt;/head>元素結尾之前。

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-include="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" data-sly-unwrap></div>
    <meta data-sly-call="${clientLib.all @ categories='cq.apps.targeting'}" data-sly-unwrap></meta>
</div>
```

>[!NOTE]
>
>請注意，程式碼區塊會封裝在WCM模式中，但不會停用，因此只有在內容作者正在建立內容時才會開始運作。 雲端服務指令碼不會新增至產生的行動執行時期程式碼。

#### body.html {#body-html}

若要讓內容作者能夠測試body.html指令碼的不同角色，必須將下列程式碼區塊加入為body元素的第一個子系。

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'clientcontext' @ resourceType='cq/personalization/components/clientcontext_optimized'}" data-sly-unwrap></div>
</div>
```

所需的最後一位程式碼位於body.html的最底部。 此程式碼位會尋找相關的雲端服務，並插入適當的定位引擎程式碼。

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'cloudservices' @ resourceType='cq/cloudserviceconfigs/components/servicecomponents'}" data-sly-unwrap></div>
</div>
```

### 參考應用程式 {#reference-application}

如需head.html和body.html的範例，請參閱 [AEM Mobile Hybrid Reference Application](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) （AEM Mobile混合參考應用程式），其中顯示開發人員將指令碼區塊置於兩個指令碼中的位置。

### 內容同步處理常式 {#content-sync-handlers}

當內容作者完成行動應用程式的內容建立後，下一步是下載來源並建立應用程式，或儲存要發佈的內容。 開發人員需要執行許多步驟，才能做到這一點。 為協助轉換內容，AEM mobile運用內容同步處理常式來轉換和封裝內容。 個人化使用案例已引入新的內容同步處理常式，可轉譯目標內容。 「mobileappoffers」處理常式瞭解如何轉譯由內容作者建立的相關目標選件。 Mobileapporfers處理常式會延伸抽象頁面更新處理常式，因此許多屬性都類似。 mobileapporfers處理常式的詳細資料包含下列屬性。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>值</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>重寫</td>
   <td>+ relativeParentPath<p> - "/"</p> </td>
   <td>rewrite屬性可識別內容中的路徑的重寫方式。</td>
  </tr>
  <tr>
   <td>includedPageTypes</td>
   <td><p>"cq/personalization/components/teaserpage",</p> <p>"cq/personalization/components/offerproxy"</p> </td>
   <td>includePageTypes屬性為選用屬性，預設為具有資源類型cq/personalization/components/teaserpage和cq/personalization/components/offerproxy的頁面。 這兩種資源類型是定位內容時使用的預設資源類型。 如果需要支援其他資源類型，應將其新增至includePageTypes清單。</td>
  </tr>
  <tr>
   <td>locationRoot</td>
   <td>/content/mobileapps/&lt;app&gt;</td>
   <td>應用程式的位置。</td>
  </tr>
  <tr>
   <td>類型</td>
   <td>mobileapporfers</td>
   <td>處理常式的名稱為mobileapporfers。</td>
  </tr>
  <tr>
   <td>選擇器</td>
   <td>tandt</td>
   <td>標準選擇器用於呈現目標內容。 </td>
  </tr>
  <tr>
   <td>targetRootDirectory</td>
   <td>www</td>
   <td>保存所呈現內容的根目錄。</td>
  </tr>
  <tr>
   <td>includeImages</td>
   <td>true| false</td>
   <td>如果為true，則會轉譯選件中包含的任何影像。 如果略過假影像。</td>
  </tr>
  <tr>
   <td>includeVideos</td>
   <td>true| false</td>
   <td>如果為真，則會呈現選件中包含的任何影片。 如果略過假影片。</td>
  </tr>
  <tr>
   <td>路徑</td>
   <td>/content/campaigns/&lt;brand&gt;</td>
   <td>指向選件參與的促銷活動品牌。 目前所有選件都必須來自相同的促銷活動。</td>
  </tr>
  <tr>
   <td>深入</td>
   <td>true| false</td>
   <td>如果true以遞歸方式呈現所有子頁面，如果false則不會遞歸。 </td>
  </tr>
  <tr>
   <td>extension</td>
   <td>html</td>
   <td>設定要呈現的資源的副檔名。 設為html，讓頁面具有。html副檔名。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AEM Mobile Hybrid Reference App [](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) （AEM Mobile混合參考應用程式）具有預設mobileappoffer處理常式的設定。 範例中的路徑屬性是空的，因為它取決於促銷活動位置。 促銷活動作者建立促銷活動後，應用程式管理員應指定指向促銷活動的路徑屬性，將促銷活動與處理常式建立關聯。

### Target元件 {#target-component}

為了協助您針對行動應用程式呈現內容，AEM mobile使用mobileapps/components/target元件。 行動目標元件會延伸cq/personalization/components/target元件，並覆寫engine_tnt.jsp指令碼。 借由覆寫engine_tnt.jsp,AEM mobile可控制行動應用程式使用案例的產生HTML。 對於內容作者所定位的每個元件，都會由engine_tnt.jsp建立相關的mbox。

針對每個mbox新增 **cq定位屬性** ，讓應用程式開發人員可編寫自訂程式碼，以便使用和使用。 [AEM Mobile Hybrid Reference App](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) （AEM Mobile混合參考應用程式）有一個使用cq-targeting屬性的Angular指令範例。 內容取代的時機和方式，完全由行動應用程式開發人員決定。 Mobile SDK會透過AEM /etc/clientlibs/mobileapps/js/mobileapps.js提供，提供API來呼叫Adobe Targeting服務。 應用程式開發人員必鬚根據應用程式的設計來指定何時應進行該呼叫。

## 下一步是什麼？ {#what-s-next}

1. [開始我的AEM mobile應用程式體驗](/help/mobile/starting-aem-phonegap-app.md)
1. [管理我的應用程式內容](/help/mobile/phonegap-manage-app-content.md)
1. [建立我的應用程式](/help/mobile/building-app-mobile-phonegap.md)
1. [使用Adobe Mobile Analytics追蹤我的應用程式效能](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [使用Adobe Target提供個人化的應用程式體驗](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [傳送重要訊息給我的使用者](/help/mobile/phonegap-push-notifications.md)
