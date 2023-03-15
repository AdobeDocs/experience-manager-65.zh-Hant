---
title: AEM Mobile內容個人化
seo-title: AEM Mobile content personalization
description: 請詳閱本頁，了解AEM Mobile內容個人化功能，此功能可讓AEM作者運用Adobe Target將行動應用程式內容個人化。
seo-description: Follow this page to learn about AEM Mobile content personalization feature that allows AEM authors to personalize mobile app content by leveraging Adobe Target.
uuid: 9078edd1-8399-485f-8a63-a07e766f7ef9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c9c818dc-c5c4-4a96-94fe-9dc9fe75705b
exl-id: 70d7ee0d-2f6d-4f97-a6e2-b02d84a0ca42
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '2673'
ht-degree: 1%

---

# AEM Mobile內容個人化{#aem-mobile-content-personalization}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>本檔案是 [開始使用AEM Mobile](/help/mobile/getting-started-aem-mobile.md) 指南，此為AEM Mobile參考的建議起點。

AEM Mobile內容個人化功能允許 [AEM作者](#author) 透過 [Adobe Target](https://www.adobe.com/ca/marketing-cloud/testing-targeting.html). 這可讓行動應用程式使用者獲得目標式優惠方案。 Adobe Experience Manager Mobile提供建立、鎖定和傳送內容的功能，可為使用者提供符合其個人口味的內容。

如同AEM中的常見情況，為了讓作者開始建立此內容，管理員和開發人員必須先準備環境。

[AEM管理員](#administrator) 必須在AEM Mobile和Adobe TargetCloud Service之間建立連線。

與此同時，AEM Mobile [開發人員](#developer) 需要修改其現有指令碼，以方便進行目標式內容編寫。

## 管理員 {#for-administrators}

內容作者必須先完成許多步驟，才能開始為行動應用程式產生目標式內容：為使用者和群組取得正確的權限集、建立雲端服務、設定活動的應用程式，最後產生內容。

本文將引導您完成設定 [AEM Mobile混合參考應用程式](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 進行定位。

未來的假設是AEM Mobile混合參考應用程式已成功部署，且可透過AEM Mobile控制面板存取。

作者必須先在應用程式中產生目標式內容，才能執行AEM例項 [已設定Adobe TargetCloud Service。](/help/mobile/aem-mobile-configuring-cloud-service.md)

### 權限 {#permissions}

需要存取個人化控制台的使用者必須屬於 `target-activity-authors` 群組。

建議在使用者和群組設定中，將target-activity-group新增至apps-admins群組。 借由新增target-activity-authors群組，使用者將能查看個人化導覽功能表項目。

>[!NOTE]
>
>忘記將您想要擁有個人化管理控制台存取權的使用者或群組新增至target-activity-authors群組，將會讓使用者看不到個人化主控台。

### 雲端服務 {#cloud-services}

若要讓目標內容適用於行動應用程式，需要設定兩項服務：Adobe Target服務與AdobeMobile Services服務。 Adobe Target服務提供處理用戶端請求及傳回個人化內容的引擎。 AdobeMobile Services服務透過ADBMobileConfig.json檔案（由AMS Cordova外掛程式使用）提供Adobe服務與行動應用程式之間的連線。 從AEM Mobile控制面板，您可以新增兩個服務來設定應用程式。

在AEM Mobile控制面板中找出管理Cloud Services，然後按一下+按鈕。

![chlimage_1-38](assets/chlimage_1-38.png)

從「新增Cloud Service」精靈中選取「Adobe Target」雲端服務卡，然後按一下「下一步」。

![chlimage_1-39](assets/chlimage_1-39.png)

從「選取設定」下拉式清單中，您可以建立新設定或從現有設定中選取。 要建立新配置，請從下拉式清單中選擇「建立配置」。 輸入Target設定的標題。 輸入與您的Target帳戶相關聯的用戶端代碼、電子郵件和密碼。 如果您不知道這些欄位的值，請聯絡Adobe Target支援。 按一下「驗證」按鈕以驗證憑證。 驗證後，按一下提交按鈕以建立雲端服務。

>[!NOTE]
>
>建立的雲端服務會透過精靈自動與行動應用程式相關聯。 在應用程式群組節點的jcr:content節點上設定cq:cloudserviceconfigs屬性值。 對於混合式應用程式範例，會在/content/mobileapps/hybrid-reference-app/jcr:content上設定，值指向位於/etc/cloudservices/testandtarget/adobe-target的自動產生的架構節點 — aem-apps/framework。 框架節點預設設定了兩個屬性，即性別和年齡。 框架僅用於AEM預覽，對裝置沒有任何影響。

精靈完成後，「管理Cloud Service」方塊將包含Target雲端服務，但包含有關遺失AdobeMobile Service帳戶的警告。

![chlimage_1-40](assets/chlimage_1-40.png)

### AdobeMobile Services {#adobe-mobile-services}

您也必須將AdobeMobile Services(AMS)帳戶連結至應用程式，AMS服務會提供必要的ADBMobileConfig.json檔案，其中包含Target用戶端代碼資訊。 在建立與AMS帳戶的關聯之前，AMS帳戶必須由具有AMS權限的使用者修改。

### 用戶端代碼 {#client-code}

若要登入AMS服務，請造訪 [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/)，請選取行動應用程式並按一下設定。 找出「SDK目標選項」欄位，並將用戶端代碼放入欄位中，然後按一下「儲存」。

![chlimage_1-41](assets/chlimage_1-41.png)

現在用戶端代碼已與行動應用程式相關聯，透過Adobe行動控制面板設定AMS雲端服務時，服務設定的設定將透過ADBMobileConfig.json檔案傳送。

### Adobe行動服務Cloud Service {#adobe-mobile-service-cloud-service}

現在AMS已設定完畢，您可以在Adobe行動控制面板中建立行動應用程式的關聯。 在AEM Mobile控制面板中找出管理Cloud Services，然後按一下+按鈕。

![chlimage_1-42](assets/chlimage_1-42.png)

選取「AdobeMobile Services」卡片，然後按一下「下一步」。

![chlimage_1-43](assets/chlimage_1-43.png)

在建立或選取精靈步驟中，選取Mobile Service下拉式清單，然後選取建立設定項目。 提供標題、公司、使用者名稱、密碼，並選取適當的資料中心。 如果您不知道這些值，請連絡您的AdobeMobile Service管理員以取得。 填寫完所有欄位後，按一下「驗證」按鈕。 驗證程式會前往AMS並驗證帳戶的憑證，一旦成功驗證，便會填入行動應用程式清單，您可在此從下拉式清單中選取相關聯的行動應用程式。 按一下「提交」按鈕以完成精靈。 該過程可能需要一些時間來獲取配置資料以及與應用程式的任何關聯分析。 程式完成後，按一下強制回應視窗中的「完成」按鈕，返回「Adobe行動控制面板」。

返回Mobile Dashboard時，「管理Cloud Services」方塊將會包含AMS雲端服務。 您也會注意，「分析量度」方塊將會填入生命週期報表。

![chlimage_1-44](assets/chlimage_1-44.png)

## 供作者使用 {#for-authors}

**先決條件：** 如上所述，管理員必須先設定Adobe Target服務的連線，作者才能產生新的目標內容。

一旦管理員設定了兩個雲端服務，且開發人員已設定mobileappoffers處理常式，內容作者就可以開始產生目標體驗。

在AEM Mobile應用程式中編寫目標內容的程式與編寫AEM Sites類似：

如需的完整概觀，請參閱這裡 [在AEM中製作目標內容](/help/sites-authoring/personalization.md)

## 適用於開發人員 {#for-developers}

建立行動應用程式的AEM開發人員應繼續遵循開發元件時在AEM中常用的模式。 在此，我們會逐步引導您執行必要步驟，讓內容作者建立目標式內容：

### Adobe Target ContentSync處理常式 {#adobe-target-contentsync-handlers}

若要傳送內容至使用者的裝置內容，需透過轉譯由AEM內容作者建立的選件來產生。 若要處理target選件的轉譯，有一個新的內容同步處理常式將處理選件。 以混合參考應用程式為範例，en（英文）內容套件包含ContentSyncConfig，並搭配 [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) 處理常式。 下一個步驟對於向裝置轉譯選件至關重要。 Mobileappoffers處理常式具有path屬性，可識別要用於應用程式的個人化活動的路徑。

例如，如果有位於 */content/campaigns/hybridref* 複製此路徑並貼上為 *路徑* mobileappoffers處理常式的屬性。

>[!NOTE]
>
>對於混合引用應用程式，有兩個mobileappoffer處理程式，一個用於開發，一個用於生產。

在Mobileappoffers處理常式的path屬性中設定活動路徑後，會儲存處理常式。 處理常式現在已準備好開始為行動裝置呈現選件。

### 呈現模式 {#render-mode}

針對發佈和開發設定，Mobileappoffers處理常式的設定不同。 若為發佈設定，有一個屬性稱為 *renderMode* 值為 *發佈* 在cq:ContentSyncConfig節點上設定。 mobileappoffers處理常式會參考renderMode，如果設為publish，則會修改所建立的mbox id。 依預設，由AEM建立的mbox會在mbox id上附加一個 — 作者值。 這可識別活動尚未發佈，應將取消發佈的促銷活動用於優惠方案解決方案。

透過「Adobe行動控制面板」存放內容時，存放內容會視為生產就緒內容，並透過非開發內容同步設定呈現。 以此方式呈現會導致：作者從所有mbox ID中移除，且預期已發佈的活動可在Target伺服器上使用。 測試分段內容之前，請確定活動已發佈。

### 個人化應用程式開發 {#personalization-app-development}

#### 元件 {#components}

任何內容的基礎通常是頁面元件，可根據您使用的是HTL或JSP，延伸其中一個基本AEM頁面元件wcm/foundation/components/page或foundation/components/page。 這些步驟的持續時間將著重於使用wcm/foundation/components/page元件。 頁面元件的基本結構會細分為多個指令碼，每個指令碼都提供特定用途，讓開發人員可視需要組織和覆寫其程式碼。 個人化最感興趣的兩個指令碼是head.html和body.html。 這兩個指令碼提供可插入程式碼的區域，以支援內容中樞、Cloud Services和行動製作。

以下概述用於啟用內容定位的兩個主要指令碼。

#### head.html {#head-html}

為了讓作者能夠鎖定其內容，必須將目標功能表新增至頁面，讓作者能夠將內容從編輯模式變更為目標模式。 若要啟用此功能，開發人員應修改head.html指令碼，將下列程式碼片段加入head.html頂端附近或最接近的 &lt;title>&lt;/title> 元素。

```xml
<meta data-sly-test="${!wcmmode.disabled}">
    <div data-sly-call="${clientLib.all @ categories='personalization.kernel'}" data-sly-unwrap></div>
    <div data-sly-resource="${'config' @ resourceType='cq/personalization/components/clientcontext_optimized/config'}" data-sly-unwrap></div>
    <div data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}" data-sly-unwrap></div>
</meta>
```

>[!NOTE]
>
>請注意，只有在未禁用WCM模式時才應包括該指令碼，這樣當禁用WCM模式時（有關詳細資訊，請參閱ContentSync處理程式的部分），該指令碼才不會包含在最終應用程式代碼中。

為了讓作者能夠預覽目標內容，編輯器必須能夠找到Adobe Target雲端服務的設定。 以下的程式碼區塊新增兩個重要指令碼。 第一個新增頁面找到相關聯Target雲端服務並發出呼叫至Adobe Target的功能。 第二個是新增cq.apps.targeting類別。

此 **cq.apps.targeting** 類別會覆寫預設的cq/personalization/component/target元件，並使用mobileapps/components/target元件，針對行動應用程式使用呈現特定選件。 有關詳細資訊，請參閱目標元件區段。

程式碼應新增至head.html，並放置在 &lt;/head> 元素。

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-include="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" data-sly-unwrap></div>
    <meta data-sly-call="${clientLib.all @ categories='cq.apps.targeting'}" data-sly-unwrap></meta>
</div>
```

>[!NOTE]
>
>請注意，程式碼區塊會包裝在WCM模式中，但不會停用，因此，只有在內容作者正在建立內容時才會開始運作。 雲端服務指令碼將不會新增至產生的行動執行階段程式碼。

#### body.html {#body-html}

若要讓內容作者能夠測試body.html指令碼的不同角色，必須包含下列程式碼區塊作為body元素的第一個子項。

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'clientcontext' @ resourceType='cq/personalization/components/clientcontext_optimized'}" data-sly-unwrap></div>
</div>
```

所需的最後一位程式碼位於body.html的最底部。 此部分程式碼會尋找相關的雲端服務，並插入適當的定位引擎程式碼。

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'cloudservices' @ resourceType='cq/cloudserviceconfigs/components/servicecomponents'}" data-sly-unwrap></div>
</div>
```

### 參考應用程式 {#reference-application}

如需head.html和body.html的範例，請參閱 [AEM Mobile混合參考應用程式](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 顯示開發人員將指令碼區塊置於兩個指令碼內的位置。

### 內容同步處理常式 {#content-sync-handlers}

當內容作者完成為行動應用程式建立內容時，下一步是下載來源並建置應用程式，或預備要發佈的內容。 開發人員需執行許多步驟，才能達成此目的。 為協助轉譯內容，AEM Mobile利用內容同步處理常式來轉譯及封裝內容。 已為個人化使用案例導入新的內容同步處理常式，以呈現目標內容。 「mobileappoffers」處理常式知道如何呈現由內容作者建立的相關目標選件。 mobileappoffers處理常式會延伸抽象頁面更新處理常式，因此許多屬性都類似。 Mobileappoffers處理常式的詳細資訊具有下列屬性。

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
   <td>rewrite屬性可識別內容內的路徑重寫方式。</td>
  </tr>
  <tr>
   <td>includedPageTypes</td>
   <td><p>"cq/personalization/components/teaserpage",</p> <p>"cq/personalization/components/offerproxy"</p> </td>
   <td>包含PageTypes屬性為選用，預設為資源類型為cq/personalization/components/teaserpage和cq/personalization/components/offerproxy的頁面。 這兩種資源類型是目標內容時使用的預設資源類型。 如果需要支援其他資源類型，應將其新增至includePageTypes清單。</td>
  </tr>
  <tr>
   <td>locationRoot</td>
   <td>/content/mobileapps/&lt;app&gt;</td>
   <td>應用程式的位置。</td>
  </tr>
  <tr>
   <td>類型</td>
   <td>mobileappoffers</td>
   <td>為mobileappoffers的處理常式的名稱。</td>
  </tr>
  <tr>
   <td>選擇器</td>
   <td>tandt</td>
   <td>標準選取器可用來轉譯目標內容。 </td>
  </tr>
  <tr>
   <td>targetRootDirectory</td>
   <td>ww</td>
   <td>保存已呈現內容的根目錄。</td>
  </tr>
  <tr>
   <td>includeImages</td>
   <td>true | false</td>
   <td>如果為true，則會轉譯選件中包含的任何影像。 如果會略過假影像。</td>
  </tr>
  <tr>
   <td>includeVideos</td>
   <td>true | false</td>
   <td>如果為true，則會轉譯選件中包含的任何影片。 如果會略過錯誤的影片。</td>
  </tr>
  <tr>
   <td>路徑</td>
   <td>/content/campaigns/&lt;brand&gt;</td>
   <td>指向選件所參與之促銷活動的品牌。 目前，所有優惠方案必須來自相同的促銷活動。</td>
  </tr>
  <tr>
   <td>深入</td>
   <td>true | false</td>
   <td>如果true以遞歸方式呈現所有子頁，如果false則不遞歸。 </td>
  </tr>
  <tr>
   <td>擴充功能</td>
   <td>html</td>
   <td>設定要呈現之資源的擴充功能。 設為html，使得頁面的副檔名為.html。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>此 [AEM Mobile混合式參考應用程式](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 具有預設mobileappoffer處理常式的設定。 範例中的路徑屬性為空白，因為它取決於促銷活動位置。 促銷活動作者建立促銷活動後，應用程式管理員應指定指向促銷活動的路徑屬性，將促銷活動與處理常式建立關聯。

### 目標元件 {#target-component}

為協助您專為行動應用程式轉譯內容，AEM Mobile會使用行動應用程式/元件/目標元件。 行動目標元件會擴充cq/personalization/components/target元件，並覆寫engine_tnt.jsp指令碼。 借由覆寫engine_tnt.jsp,AEM Mobile便可控制行動應用程式使用案例產生的HTML。 對於內容作者所定位的每個元件，engine_tnt.jsp會建立相關的mbox。

對於每個mbox，屬性為 **cq定位** 新增，讓應用程式開發人員可撰寫自訂程式碼，以便使用和使用。 此 [AEM Mobile混合式參考應用程式](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 有使用cq-targeting屬性的Angular指令的範例。 內容取代的時機和方式由行動應用程式開發人員決定。 透過AEM /etc/clientlibs/mobileapps/js/mobileapps.js傳送的Mobile SDK，提供呼叫Adobe鎖定目標服務的API。 應用程式開發人員需自行指定，何時應根據其應用程式的設計進行呼叫。

## 下一步? {#what-s-next}

1. [開始我的AEM Mobile應用程式體驗](/help/mobile/starting-aem-phonegap-app.md)
1. [管理我應用程式的內容](/help/mobile/phonegap-manage-app-content.md)
1. [構建我的應用程式](/help/mobile/building-app-mobile-phonegap.md)
1. [使用Adobe行動分析追蹤我應用程式的效能](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [使用Adobe Target提供個人化應用程式體驗](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [傳送重要訊息給我的使用者](/help/mobile/phonegap-push-notifications.md)
