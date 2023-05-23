---
title: AEM Mobile內容個性化
seo-title: AEM Mobile content personalization
description: 關於AEM Mobile內容個性化功能，請訪問此頁AEM，該功能允許作者利用Adobe Target個性化移動應用內容。
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

# AEM Mobile內容個性化{#aem-mobile-content-personalization}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>此文檔是 [AEM Mobile入門](/help/mobile/getting-started-aem-mobile.md) 指南，推薦的AEM Mobile參考起點。

AEM Mobile內容個性化功能允許 [AEM作者](#author) 通過利用 [Adobe Target](https://www.adobe.com/ca/marketing-cloud/testing-targeting.html)。 這允許向移動應用程式用戶提供目標服務。 Adobe Experience Manager Mobile公司提供建立、定向和傳遞內容的能力，這些內容將為用戶提供針對其個人喜好的特定內容。

通常情況下，為AEM了讓作者開始建立此內容，管理員和開發人員需要首先準備環境。

[刪AEM除器](#administrator) 必須在AEM Mobile和Adobe TargetCloud Service之間建立聯繫。

與此同時，AEM Mobile [開發者](#developer) 需要修改其現有指令碼以便於目標內容創作。

## 對於管理員 {#for-administrators}

在內容作者開始為移動應用生成目標內容之前，需要先採取許多步驟：獲取用戶和組的正確權限集、建立雲服務、配置活動應用程式，最後生成內容。

本文將指導您完成配置 [AEM Mobile混合參考應用](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 目標。

今後的假設是，AEM Mobile混合參考應用程式已成功部署並可通過AEM Mobile儀表板訪問。

在作者可以在應用程式內生成目標內容之前，AEM您的實例需要 [配置了Adobe TargetCloud Service。](/help/mobile/aem-mobile-configuring-cloud-service.md)

### 權限 {#permissions}

需要訪問個性化控制台的用戶必須是 `target-activity-authors` 組。

建議在用戶和組設定中將target-activity-group添加到apps-admins組。 通過添加target-activity-authors組，用戶將能夠查看個性化導航菜單條目。

>[!NOTE]
>
>忘記將想要訪問個性化管理控制台的用戶或組添加到target-activity-authors組將阻止用戶看到個性化控制台。

### 雲端服務 {#cloud-services}

要使針對移動應用程式的目標內容工作，需要配置兩種服務：Adobe Target服務和Adobe移動服務。 Adobe Target服務提供處理客戶請求和返回個性化內容的引擎。 Adobe移動服務服務通過AMS Cordova插件使用的ADBMobileConfig.json檔案提供Adobe服務與移動應用程式之間的連接。 在AEM Mobile儀表板中，您可以通過添加兩個服務來配置應用程式。

在AEM Mobile儀表板中找到管理Cloud Services，然後按一下+按鈕。

![chlimage_1-38](assets/chlimage_1-38.png)

在「添加Cloud Service」嚮導中，選擇「Adobe Target」雲服務卡，然後按一下「下一步」。

![chlimage_1-39](assets/chlimage_1-39.png)

從「選擇配置」下拉清單中，您可以建立新配置或從現有配置中進行選擇。 要建立新配置，請從下拉清單中選擇「建立配置」。 輸入目標配置的標題。 輸入與目標帳戶關聯的客戶端代碼、電子郵件和密碼。 如果您不知道這些欄位的值，請與Adobe Target支援部門聯繫。 按一下「驗證」按鈕驗證憑據。 驗證後，按一下「提交」按鈕建立雲服務。

>[!NOTE]
>
>建立的雲服務通過嚮導自動與移動應用程式關聯。 在應用程式組節點的jcr:content節點上設定cq:cloudserviceconfigs屬性值。 對於混合應用示例，將在/content/mobileapps/hybrid-reference-app/jcr:content上設定，其值指向位於/etc/cloudservices/testandarget/adobe-target的自動生成的框架節點 — aem-apps/framework。 框架節點具有預設設定的兩個屬性：性別和年齡。 該框架僅通過預AEM覽使用，對設備沒有任何影響。

完成嚮導後，「管理Cloud Service」磁貼將包含目標雲服務，但它包含有關缺少Adobe移動服務帳戶的警告。

![chlimage_1-40](assets/chlimage_1-40.png)

### Adobe移動服務 {#adobe-mobile-services}

還必須將Adobe移動服務(AMS)帳戶連結到應用程式，AMS服務提供所需的ADBMobileConfig.json檔案，其中包含目標客戶端代碼資訊。 在建立與AMS帳戶的關聯之前，AMS帳戶需要由具有AMS權限的用戶修改。

### 用戶端代碼 {#client-code}

要登錄AMS服務，請訪問 [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/)，選擇移動應用程式，然後按一下設定。 找到「SDK目標選項」欄位，將客戶端代碼放入該欄位，然後按一下「保存」。

![chlimage_1-41](assets/chlimage_1-41.png)

既然客戶端代碼已與移動應用程式關聯，則當通過Adobe移動儀表板配置AMS雲服務時，服務設定的設定將通過ADBMobileConfig.json檔案傳遞。

### Adobe移動服務Cloud Service {#adobe-mobile-service-cloud-service}

既然已配置AMS，現在就應該將移動應用程式關聯到Adobe移動儀表板。 在AEM Mobile儀表板中找到管理Cloud Services，然後按一下+按鈕。

![chlimage_1-42](assets/chlimage_1-42.png)

選擇Adobe移動服務卡，然後按一下「下一步」。

![chlimage_1-43](assets/chlimage_1-43.png)

在「建立」或「選擇」嚮導步驟中，選擇「移動服務」下拉清單，然後選擇「建立配置」條目。 提供標題、公司、用戶名、密碼，並選擇相應的資料中心。 如果您不知道這些值，請與Adobe移動服務管理員聯繫以獲取這些值。 填寫完所有欄位後，按一下「驗證」按鈕。 驗證過程將轉到AMS並驗證帳戶的憑據，在成功驗證後，將填充移動應用程式清單，從下拉清單中選擇關聯的移動應用程式。 按一下「提交」按鈕以完成嚮導。 該過程可能需要一段時間來獲取配置資料以及與應用程式相關的任何分析。 完成該過程後，按一下模式中的「完成」(Done)按鈕，返回Adobe移動儀表板。

返回到Mobile Dashboard時，「管理Cloud Services」磁貼將包含AMS雲服務。 您還將注意到，「分析度量」磁貼將填充生命週期報告。

![chlimage_1-44](assets/chlimage_1-44.png)

## 對於作者 {#for-authors}

**先決條件：** 如上所述，管理員需要先配置到Adobe Target服務的連接，然後作者才能生成新的目標內容。

一旦管理員配置了兩個雲服務，並且開發人員配置了移動審批程式處理程式，內容作者現在就可以開始生成目標體驗。

在AEM Mobile應用中創作目標內容遵循與創作AEM Sites類似的步驟：

請參閱此處瞭解有關 [在中創作目標內AEM容](/help/sites-authoring/personalization.md)

## 面向開發人員 {#for-developers}

開發AEM移動應用程式的開發人員應繼續遵循開發元件時通AEM常使用的模式。 在此，我們將引導您完成必要的步驟，使內容作者能夠建立目標內容：

### Adobe TargetContentSync處理程式 {#adobe-target-contentsync-handlers}

通過呈現由內容作者建立的優惠來生成向用戶的設備內容傳送AEM內容。 要處理目標提供的呈現，有一個新的內容同步處理程式將處理提供。 使用混合引用應用程式作為示例，en（英語）內容包包含帶有 [移動助理](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) 處理程式。 下一步對於向設備呈現優惠資訊至關重要。 mobileapporfers處理程式具有路徑屬性，該路徑屬性標識要用於應用程式的個性化活動的路徑。

例如，如果有活動位於 */內容/市場活動/混合* 複製此路徑並將其貼上為 *路徑* mobileapporfers處理程式的屬性。

>[!NOTE]
>
>對於混合引用應用程式，有兩個移動apporfers處理程式，一個用於開發，一個用於生產。

在mobileapporfers處理程式的路徑屬性中設定活動路徑後，保存處理程式。 處理程式現在將準備好開始為我們的移動設備呈現優惠。

### 呈現模式 {#render-mode}

為發佈和開發設定，移動程式處理程式的配置方式不同。 對於發佈設定，有一個名為 *renderMode* 值為 *發佈* 在cq:ContentSyncConfig節點上設定。 mobileapporffers處理程式引用renderMode，如果設定為發佈，將修改建立的mbox id。 預設情況下，由建立的框AEM的mbox id附加了 — author值。 這表明活動尚未發佈，應使用未發佈的促銷活動解決方案。

當內容通過Adobe移動控制板轉移時，轉移內容被視為生產就緒內容，並通過非開發內容同步配置來呈現。 以這種方式呈現將導致 — 作者從所有mbox id中刪除，並期望在目標伺服器上提供已發佈的活動。 在測試分段內容之前，請確保已發佈該活動。

### 個性化應用開發 {#personalization-app-development}

#### 元件 {#components}

任何內容的基礎通常是頁面元件，它根據您使用的是HTL或JSPAEM而擴展基本頁面元件wcm/foundation/components/page或foundation/components/page。 這些步驟的持續時間將集中於使用wcm/foundation/components/page元件。 頁面元件的基本結構被分解為多個指令碼，每個指令碼都提供了特定目的，允許開發人員根據需要組織和覆蓋其代碼。 Personalization感興趣的兩個指令碼是head.html和body.html。 這兩個指令碼提供了一個區域，可在該區域注入代碼以支援上下文中心、Cloud Services和移動創作。

下面概述了用於啟用內容目標化的兩個主要指令碼。

#### head.html {#head-html}

為了使作者能夠瞄準其內容，需要將目標菜單添加到頁面，以便作者可以將上下文從編輯模式更改為目標模式。 要啟用此功能，開發人員應修改head.html指令碼，以在head.html頂部或靠近 &lt;title>&lt;/title> 元素。

```xml
<meta data-sly-test="${!wcmmode.disabled}">
    <div data-sly-call="${clientLib.all @ categories='personalization.kernel'}" data-sly-unwrap></div>
    <div data-sly-resource="${'config' @ resourceType='cq/personalization/components/clientcontext_optimized/config'}" data-sly-unwrap></div>
    <div data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}" data-sly-unwrap></div>
</meta>
```

>[!NOTE]
>
>請注意，只有在WCM模式未禁用時才應包括該指令碼，以便在禁用WCM模式時（有關詳細資訊，請參閱ContentSync處理程式的部分），該指令碼將不包括在最終應用程式碼中。

要讓作者能夠預覽目標內容，編輯器需要能夠找到Adobe Target雲服務的配置。 下面的代碼塊添加了兩個重要的指令碼。 首先添加頁面查找關聯的目標雲服務並呼叫Adobe Target。 第二個是添加cq.apps.targeting類別。

的 **cq.apps目標** 類別覆蓋預設的cq/個性化/元件/目標元件，並使用移動應用/元件/目標元件，該元件專門為移動應用程式消耗提供服務。 有關此項的詳細資訊，將在「目標元件」部分中討論。

應將代碼添加到head.html中，並放置在 &lt;/head> 的子菜單。

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-include="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" data-sly-unwrap></div>
    <meta data-sly-call="${clientLib.all @ categories='cq.apps.targeting'}" data-sly-unwrap></meta>
</div>
```

>[!NOTE]
>
>請注意，代碼塊在未禁用的WCM模式內包裝，因此只在內容作者正在建立內容時才開始播放。 雲服務指令碼將不會添加到生成的移動運行時代碼中。

#### body.html {#body-html}

要使內容作者能夠testbody.html指令碼中的不同角色，需要將以下代碼塊作為body元素的第一個子項包含在內。

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'clientcontext' @ resourceType='cq/personalization/components/clientcontext_optimized'}" data-sly-unwrap></div>
</div>
```

所需的最後一位代碼位於body.html的最底部。 此代碼位將查找關聯的雲服務，並彈出適當的目標引擎代碼。

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'cloudservices' @ resourceType='cq/cloudserviceconfigs/components/servicecomponents'}" data-sly-unwrap></div>
</div>
```

### 引用應用程式 {#reference-application}

可以在中找到head.html和body.html的示例 [AEM Mobile混合參考應用](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 顯示開發人員將指令碼塊放置在兩個指令碼中的位置。

### 內容同步處理程式 {#content-sync-handlers}

當內容作者完成為移動應用程式建立內容後，下一步是下載源並構建應用程式，或存放要發佈的內容。 開發人員參與了許多步驟來實現此目標。 為了幫助呈現內容，AEM Mobile利用內容同步處理程式來呈現和打包內容。 已為個性化用例引入新的內容同步處理程式來呈現目標內容。 「mobileapporfers」處理程式知道如何呈現由內容作者建立的關聯目標提供。 mobileapporfers處理程式會擴展抽象頁更新處理程式，因此，許多屬性是相似的。 mobileapporfers處理程式的詳細資訊具有以下屬性。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td>
   <td><strong>值</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>重寫</td>
   <td>+相對父路徑<p> - "/"</p> </td>
   <td>rewrite屬性可標識內容中的路徑的重寫方式。</td>
  </tr>
  <tr>
   <td>包括的頁類型</td>
   <td><p>"cq/personalization/components/teaserpage",</p> <p>"cq/個性化/元件/產品代理"</p> </td>
   <td>includePageTypes屬性是可選的，預設為資源類型為cq/personalization/components/teaserpage和cq/personalization/components/offerproxy的頁面。 這兩種資源類型是目標內容時使用的預設資源類型。 如果需要支援其他資源類型，則應將其添加到includePageTypes清單中。</td>
  </tr>
  <tr>
   <td>位置根</td>
   <td>/content/mobileapps/&lt;app&gt;</td>
   <td>應用的位置。</td>
  </tr>
  <tr>
   <td>類型</td>
   <td>移動助理</td>
   <td>處理程式是mobileapporfers的名稱。</td>
  </tr>
  <tr>
   <td>選擇器</td>
   <td>坦德</td>
   <td>tandt選擇器用於呈現目標內容。 </td>
  </tr>
  <tr>
   <td>目標根目錄</td>
   <td>萬維網</td>
   <td>保留呈現內容的根目錄。</td>
  </tr>
  <tr>
   <td>包括影像</td>
   <td>真 |false</td>
   <td>如果為true，則將呈現該優惠中包含的任何影像。 如果跳過假影像。</td>
  </tr>
  <tr>
   <td>包括視頻</td>
   <td>真 |false</td>
   <td>如果為true，則將提供此優惠中包含的任何視頻。 如果跳過假視頻。</td>
  </tr>
  <tr>
   <td>路徑</td>
   <td>/內容/活動/&lt;brand&gt;</td>
   <td>指向活動的品牌，這些產品都參與其中。 目前，所有優惠必須來自同一活動。</td>
  </tr>
  <tr>
   <td>深入</td>
   <td>真 |false</td>
   <td>如果為true，則遞歸呈現所有子頁，如果為false，則不遞歸。 </td>
  </tr>
  <tr>
   <td>擴展</td>
   <td>html</td>
   <td>設定要呈現的資源的擴展。 設定為html，使頁面具有.html副檔名。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>的 [AEM Mobile混合參考應用](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 具有預設的mobileappoffer處理程式的配置。 示例中的路徑屬性為空，因為它取決於市場活動位置。 市場活動作者建立市場活動後，應用程式管理員應通過指定指向市場活動的路徑屬性將市場活動與處理程式相關聯。

### 目標元件 {#target-component}

為了幫助為移動應用程式專門呈現內容，AEM Mobile使用移動應用程式/元件/目標元件。 移動目標元件擴展了cq/個性化/元件/目標元件，並覆蓋engine_tnt.jsp指令碼。 通過覆蓋engine_tnt.jsp,AEM Mobile可以控制移動應用使用案例生成的HTML。 對於內容作者所針對的每個元件，engine_tnt.jsp會建立一個關聯的框。

對於每個框， **CQ靶向** 添加，允許應用程式開發人員編寫自定義代碼，以便使用和使用。 的 [AEM Mobile混合參考應用](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) 有一個使用cq-targeting屬性的Angular指令示例。 內容替換的概念何時以及如何完成，在很大程度上取決於移動應用程式開發人員。 通過/etc/clientlibs/mobileapps/js/mobileapps.js提供的移動SDKAEM提供了調用Adobe目標服務的API。 根據應用程式的設計來指定何時應進行該調用，由應用程式開發人員決定。

## 下一步? {#what-s-next}

1. [啟動我的AEM Mobile應用體驗](/help/mobile/starting-aem-phonegap-app.md)
1. [管理我的應用的內容](/help/mobile/phonegap-manage-app-content.md)
1. [構建我的應用程式](/help/mobile/building-app-mobile-phonegap.md)
1. [使用AdobeMobile Analytics跟蹤我的應用的效能](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [通過Adobe Target提供個性化的應用體驗](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [向我的用戶發送重要消息](/help/mobile/phonegap-push-notifications.md)
