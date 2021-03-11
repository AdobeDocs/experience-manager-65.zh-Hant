---
title: 與Dynamic Media經典整合
description: 瞭解如何將Adobe Experience Manager與Dynamic Media經典整合。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
translation-type: tm+mt
source-git-commit: 4090b1641467c6fb02b2fcce4df97b9fd5da4e2f
workflow-type: tm+mt
source-wordcount: '5452'
ht-degree: 0%

---


# 與Dynamic Media經典{#integrating-with-dynamic-media-classic-scene}整合

AdobeDynamic Media經典是一套代管解決方案，用於管理、增強、發佈和提供多媒體資產至網路、行動裝置、電子郵件和網際網路連線的顯示器與印刷品。

若要使用Dynamic Media經典，您必須設定雲端組態，讓Dynamic Media經典與AEM Assets能夠互動。 本檔案說明如何設定AEM和Dynamic Media經典。

有關使用頁面上所有的Dynamic Media經典元件和使用視頻的資訊，請參見[使用Dynamic Media經典](../assets/scene7.md)。

>[!NOTE]
>
>* Dynamic MediaClassic的DHTML檢視器平台已於2014年1月31日正式停止使用。 如需詳細資訊，請參閱[DHTML檢視器生命週期結束的常見問答集](../sites-administering/dhtml-viewer-endoflifefaqs.md)。
>* 在將Dynamic Media經典配置為使用AEM之前，請參閱[將Dynamic Media經典與整合的最佳實踐](#best-practices-for-integrating-scene-with-aem) AEM。
>* 如果您使用的是自訂的Proxy設定，則需要設定兩個HTTP Client Proxy設定，因為其中的某些功能是使用AEM3.x API，而其他功能是使用4.x API。 3.x配置有[http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient),4.x配置有[http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)。

>



## AEM/Dynamic Media經典整合與Dynamic Media{#aem-scene-integration-versus-dynamic-media}

AEM用戶可以選擇兩種解決方案來與Dynamic Media合作：要麼將其實例與AEMDynamic Media經典軟體整合，要麼使用與之整合的Dynamic Media解決方案AEM。

使用下列准則來判斷要選擇的解決方案：

* 如果您是&#x200B;**現有**&#x200B;的Dynamic Media經典客戶，其豐富型媒體資產位於Dynamic Media經典出版和發佈，但您想要將這些資產與網站(WCM)製作和／或AEM Assets整合以進行管理，則請使用本檔案所述的[AEM/Dynamic Media經典點對點整合](#aem-scene-point-to-point-integration)。

* 如果您是&#x200B;**新**&#x200B;客戶，AEM並有豐富式媒體傳送需求，請選擇[Dynamic Media選項](#aem-dynamic-media)。 如果您沒有現有的S7帳戶，且該系統中儲存了許多資產，這個選項最有意義。

* 在某些情況下，您可能想要同時使用這兩種解決方案。 [雙用方案](/help/sites-administering/scene7.md#dual-use-scenario)說明該方案。

### AEM/Dynamic Media經典點對點整合{#aem-scene-point-to-point-integration}

當您在此解決方案中使用資產時，請執行下列其中一項作業：

* 直接將資產上傳至Dynamic Media經典網頁，然後透過&#x200B;**Dynamic Media經典網頁內容瀏覽器存取網頁製作或**
* 上傳至AEM Assets，然後自動發佈至Dynamic Media經典；您可透過&#x200B;**Assets**&#x200B;內容瀏覽器存取頁面製作

您用於此整合的元件位於[設計模式的&#x200B;**Dynamic Media經典**&#x200B;元件區域。](/help/sites-authoring/author-environment-tools.md#page-modes)

### AEMDynamic Media{#aem-dynamic-media}

AEMDynamic Media是Dynamic Media經典功能直接在平台內AEM統一。

當您在此解決方案中使用資產時，請遵循下列工作流程：

1. 將單一影像和視訊資產直接上傳至AEM。
1. 直接在中編碼視AEM訊。
1. 直接在內部建立以影像為基礎的AEM集合。
1. 如果適用，請在影像或視訊中加入互動功能。

您用於Dynamic Media的元件位於[設計模式](/help/sites-authoring/author-environment-tools.md#page-modes)的&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;元件區域。 其中包括：

* **[!UICONTROL Dynamic Media]** -  **** Dynamic Mediacomponent是智慧型的——視您新增影像或視訊而定，您有多種選項。此元件支援影像預設集、影像檢視器，例如影像集、回轉集、混合媒體集和視訊。 此外，檢視器具有互動功能——螢幕大小會根據螢幕大小自動變更。 所有檢視器都是HTML5檢視器。

* **[!UICONTROL 互動式媒體]** -互動式媒 **[!UICONTROL 體]** 元件適用於這些資產，例如轉盤橫幅、互動式影像和互動式視訊，這些資產在熱點或影像地圖上具有互動性。此元件是智慧型的——視您新增影像或視訊而定，您有各種選項。 此外，檢視器具有互動功能——螢幕大小會根據螢幕大小自動變更。 所有檢視器都是HTML5檢視器。

### 雙用方案{#dual-use-scenario}

立即可用，您可同時使用Dynamic Media和Dynamic Media經典的整合功AEM能。 下表說明您開啟和關閉特定區域時的使用案例。

同時使用Dynamic Media和Dynamic Media經典：

1. 在雲服務中配置[Dynamic Media經典](#creating-a-cloud-configuration-for-scene)。
1. 請依照您使用案例的特定指示進行：

   <table>
    <tbody>
    <tr>
    <td> </td>
    <td> </td>
    <td><strong>Dynamic Media</strong></td>
    <td> </td>
    <td><strong>Dynamic Media經典整合</strong></td>
    <td> </td>
    </tr>
    <tr>
    <td><strong>如果您是……</strong></td>
    <td><strong>使用案例工作流程</strong></td>
    <td><strong>影像／視訊</strong></td>
    <td><strong>動態媒體元件</strong></td>
    <td><strong>S7內容瀏覽器和元件</strong></td>
    <td><strong>自動從資產上傳至S7</strong></td>
    </tr>
    <tr>
    <td>網站與Dynamic Media</td>
    <td>上傳資產至AEM並使用AEMDynamic Media元件在「網站」頁面上製作資產</td>
    <td><p>開啟</p> <p>（請參閱步驟3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">開啟</a></td>
    <td>關閉</td>
    <td>關閉</td>
    </tr>
    <tr>
    <td>零售業，是網站和Dynamic Media的新手</td>
    <td>將非產品資產上傳至AEM以進行管理和傳送。 將PRODUCT資產上傳至Dynamic Media經典網站，並在和元件中使用Dynamic Media經典內AEM容瀏覽器來製作網站上的產品詳細資訊頁面。</td>
    <td><p>開啟</p> <p>（請參閱步驟3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">開啟</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">開啟</a></td>
    <td>關閉</td>
    </tr>
    <tr>
    <td>資產與Dynamic Media</td>
    <td>將資產上傳至AEM Assets，並使用從Dynamic Media發佈的URL/內嵌代碼</td>
    <td><p>開啟</p> <p>（請參閱步驟3）</p> </td>
    <td>關閉</td>
    <td>關閉</td>
    <td>關閉</td>
    </tr>
    <tr>
    <td>Dynamic Media和坦普林新手</td>
    <td>使用Dynamic Media進行影像和視訊。 在「Dynamic Media經典」中編寫影像範本，並使用「Dynamic Media經典」內容搜尋器將範本加入「網站」頁面。</td>
    <td><p>開啟</p> <p>（請參閱步驟3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">開啟</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">開啟</a></td>
    <td>關閉</td>
    </tr>
    <tr>
    <td>現有的Dynamic MediaClassic客戶，是Sites的新手</td>
    <td>將資產上傳至Dynamic Media經典網站，並使AEM用Dynamic Media經典內容瀏覽器搜尋及製作網站頁面上的資產</td>
    <td>關閉</td>
    <td>關閉</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">開啟</a></td>
    <td>關閉</td>
    </tr>
    <tr>
    <td>現有的Dynamic MediaClassic客戶，是網站和資產的新手</td>
    <td>將資產上傳至DAM，並自動發佈至Dynamic MediaClassic以進行傳送。 使用AEMDynamic Media傳統內容瀏覽器搜尋及製作網站頁面上的資產。</td>
    <td>關閉</td>
    <td>關閉</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">開啟</a></td>
    <td><p><a href="#configuringautouploadingfromaemassets">開啟</a></p> <p>（請參閱步驟4）</p> </td>
    </tr>
    <tr>
    <td>現有Dynamic Media經典客戶與新資產</td>
    <td><p>將資產上傳AEM至並使用Dynamic Media產生轉譯以供下載／分享。 自動將AEM資產發佈至Dynamic MediaClassic以進行傳送。</p> <p><strong>重要：在</strong> 中產生的重複處理和轉譯AEM將不會同步到Dynamic Media經典</p> </td>
    <td><p>開啟</p> <p>（請參閱步驟3）</p> </td>
    <td>關閉</td>
    <td>關閉</td>
    <td><p><a href="#configuringautouploadingfromaemassets">開啟</a></p> <p>（請參閱步驟4）</p> </td>
    </tr>
    </tbody>
    </table>

1. (可選；請參閱使用案例表)-設定[Dynamic Media雲端組態](/help/assets/config-dynamic.md)和[啟用Dynamic Media伺服器](/help/assets/config-dynamic.md)。
1. (可選；請參閱使用案例表格)-如果您選擇啟用「從資產自動上傳至Dynamic Media經典」，則需要新增下列項目：

   1. 設定自動上傳至Dynamic Media經典。
   1. 在&#x200B;*****Dam更新資產工作流程(`https://<server>:<host>/cf#/etc/workflow/models/dam/update_asset.html)`)結束時，在所有Dynamic Media工作流程步驟*&#x200B;之後添加&#x200B;**Dynamic Media經典上載**&#x200B;步驟()
   1. （可選）以[https://&lt;server>:&lt;port>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl)的MIME類型限制Dynamic Media傳統資產上傳。 不在此清單中的資產MIME類型將不會上傳至Dynamic Media經典伺服器。
   1. （可選）在Dynamic Media經典配置中設定視頻。 您可以同時為Dynamic Media和Dynamic Media古典音樂啟用視訊編碼。 動態轉譯用於本機實例中的預AEM覽和播放，而Dynamic Media經典視訊轉譯則產生並儲存在Dynamic Media經典伺服器上。 為Dynamic Media和Dynamic Media經典設定視訊編碼服務時，請將[視訊處理設定檔](/help/assets/video-profiles.md)套用至Dynamic Media經典資產資料夾。
   1. （可選）[在Dynamic MediaClassic](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)中配置安全預覽。

#### 限制 {#limitations}

當您同時啟用Dynamic Media經典和Dynamic Media時，會有下列限制：

* 手動上傳至Dynamic Media經典，方法是選取資產並將其拖曳至頁面上的Dynamic Media經典元AEM件無法運作。
* 即使在「資AEM產」中編輯資產時，已同步的資產會自動更新至「Dynamic Media經典」，但回滾動作不會觸發新的上傳，因此，回滾後，Dynamic Media經典不會立即取得最新版本。 因應措施是在回滾完成後再次編輯。
* 如果您需要將Dynamic Media用於某個使用案例，而Dynamic Media經典整合用於另一個使用案例，以便Dynamic Media資產不與Dynamic Media經典系統交互，則不要將Dynamic Media經典配置應用於Dynamic Media資料夾，也不要將Dynamic Media配置（處理配置檔案）應用於Dynamic Media經典資料夾。

## 將Dynamic Media經典與AEM{#best-practices-for-integrating-scene-with-aem}整合的最佳做法

將Dynamic Media經典與整AEM合時，需要在以下方面遵守一些重要的最佳做法：

* 測試推動整合
* 針對特定情況，建議直接從Dynamic Media經典上傳資產

請參閱[已知限制](#known-limitations-and-design-implications)。

### 測試推動整合{#test-driving-your-integration}

Adobe建議您只將根資料夾指向子資料夾，而非整個公司，以測試整合。

>[!CAUTION]
>
>從現有的Dynamic Media經典公司帳戶匯入資產可能需要很長時間才能顯示AEM。 請確定您在Dynamic Media經典中指定的資料夾沒有太多資產（例如，根資料夾通常擁有太多資產，而且可能會造成系統當機）。

### 從AEM Assets與Dynamic Media經典上傳資產{#uploading-assets-from-aem-assets-versus-from-scene}

您可以使用「資產」（數位資產管理）功能或透過「Dynamic Media經典」內容瀏覽器直接存取「Dynamic Media經典」，來AEM上傳資產。 您選擇哪一種取決於以下因素：

* Dynamic Media尚未支援的經典資產類型，必須透過AEM Assets經典內容瀏覽器（例如影像範本），從AEMDynamic Media經典網站直接新增至網站。
* 對於AEM Assets和Dynamic Media經典都支援的資產類型，決定如何上傳這些資產類型取決於：

   * 資產現在位於何處
   * 在通用儲存庫中管理這些檔案的重要性

如果資產已位於Dynamic Media經典中，且在通用儲存庫中管理資產並不重要，則將資產匯出至AEM Assets，僅將資產同步回Dynamic Media經典中以進行傳送，將是不必要的往返作業。 否則，最好將資產保留在單一儲存庫中，並同步至Dynamic MediaClassic僅供傳送。

## 配置Dynamic Media經典整合{#configuring-scene-integration}

您可以設AEM定上傳資產至Dynamic Media經典。 CQ目標資料夾中的資產可以從Dynamic Media傳統公司帳戶上傳（自動或手動）AEM至該帳戶。

>[!NOTE]
>
>Adobe建議您只使用指定的目標資料夾來導入Dynamic Media經典資產。 駐留在目標資料夾之外的數字資產只能用於已啟用Dynamic Media經典配置的頁面上的Dynamic Media經典元件。 此外，它們會放在Dynamic Media經典的臨機資料夾中。 臨機資料夾未與同步AEM(但資產可在Dynamic Media傳統內容瀏覽器中找到)。

若要將Dynamic MediaClassic設定為AEM與整合，您必須完成下列步驟：

1. [定義雲端設定](#creating-a-cloud-configuration-for-scene) -定義「Dynamic Media經典」檔案夾與「資產」檔案夾之間的對應。即使您只想要單向(AEM Assets到Dynamic Media經典)同步，也需要完成此步驟。
1. [啟用 **Adobe CQ的s7dam Dam Listener**](#enabling-the-adobe-cq-scene-dam-listener)  —— 在  OSGiconsole中完成。
1. 如果您想AEM要資產自動上傳至Dynamic Media經典，您必須開啟該選項，並將Dynamic Media經典新增至[!UICONTROL DAM更新資產]工作流程。 您也可以手動上傳資產。
1. 將Dynamic Media經典元件添加到sidekick。 這可讓使用者在其頁面上使用Dynamic Media經典AEM元件。
1. [將設定對應至中的頁AEM面——此步驟是檢視您在Dynamic Media傳統影像中建立的任何視訊預設集的必要步驟。](#enabling-scene-for-wcm) 如果您需要從CQ目標資料夾外部執行資產發佈至Dynamic Media經典，則此為必要項目。

本節介紹如何執行所有這些步驟，並列出重要限制。

### Dynamic Media經典與AEM Assets的同步如何運作{#how-synchronization-between-scene-and-aem-assets-works}

在設定AEM Assets和Dynamic Media經典同步時，請務必瞭解以下內容：

#### 從AEM Assets上傳至Dynamic Media經典{#uploading-to-scene-from-aem-assets}

* 中為Dynamic Media經典上載指定AEM的同步資料夾。
* 如果數位資產放在指定的同步資料夾中，則可自動上傳至Dynamic Media經典。
* 中的資料夾和子資料夾結AEM構在Dynamic Media經典中複製。

>[!NOTE]
>
>將所AEM有中繼資料內嵌在XMP上傳至Dynamic Media經典之前，因此中繼資料節點上的所有屬性在Dynamic Media經典中都可使用XMP。

#### 已知限制和設計含義{#known-limitations-and-design-implications}

隨著AEM Assets與Dynamic Media經典網站的同步，目前有下列限制／設計含義：

<table>
 <tbody>
  <tr>
   <td><strong>限制／設計暗示</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>一個指定的同步（目標）資料夾</td>
   <td>對於Dynamic Media經典上傳，每個公司只能有一個AEM指定的資料夾。 如果您需要存取Dynamic MediaClassic中的多個公司帳戶，可以建立多種組態。</td>
  </tr>
  <tr>
   <td>資料夾結構</td>
   <td>如果您刪除具有資產的同步資料夾，則會刪除所有Dynamic Media經典遠端資產，但資料夾仍會保留。</td>
  </tr>
  <tr>
   <td>臨機資料夾</td>
   <td>位於WCM中手動上傳至Dynamic Media經典的目標資料夾外的資產，會自動置於Dynamic Media經典的個別臨機資料夾中。 您可在中的雲端設定中設定此項AEM。</td>
  </tr>
  <tr>
   <td>混合媒體</td>
   <td>混合媒體集在中AEM顯示，但不支援AEM。</td>
  </tr>
  <tr>
   <td>PDF</td>
   <td>從Dynamic MediaClassic的eCatalogs產生的PDF會匯入CQ目標檔案夾。</td>
  </tr>
  <tr>
   <td>UI重新整理</td>
   <td>在與Dynamic Media經AEM典同步時，請務必重新整理使用者介面以檢視變更。 </td>
  </tr>
  <tr>
   <td>視訊縮圖</td>
   <td>如果上傳視訊至AEM Assets以透過Dynamic Media經典進行編碼，視訊縮圖和編碼視訊可能需要一些時間才能在AEM Assets上市，視視訊處理時間而定。</td>
  </tr>
  <tr>
   <td>Target子檔案夾</td>
   <td><p>如果您使用目標檔案夾中的子檔案夾，請確定您對每個資產使用唯一名稱（不論位置），或設定「Dynamic Media傳統」（在「設定」區域），以不覆寫資產，不論其位置。</p> <p>否則，將上載與上載到Dynamic Media經典目標子資料夾同名的資產，但目標資料夾中的同名資產將被刪除。 </p> </td>
  </tr>
 </tbody>
</table>

### 配置Dynamic Media經典伺服器{#configuring-scene-servers}

如果您在AEM代理後運行或具有特殊的防火牆設定，則可能需要明確啟用不同區域的主機。 伺服器在`/etc/cloudservices/scene7/endpoints`的內容中進行管理，並可根據需要進行自定義。 點選URL，然後視需要編輯以變更URL。 在舊版中，AEM這些值是硬式編碼。

如果您導覽至`/etc/cloudservices/scene7/endpoints.html`，您會看到列出的伺服器（並可按一下URL加以編輯）:

![chlimage_1-296](assets/chlimage_1-296.png)

### 為Dynamic Media經典建立雲配置{#creating-a-cloud-configuration-for-scene}

雲配置定義了Dynamic Media經典資料夾和AEM Assets資料夾之間的映射。 它必須配置為使AEM Assets與Dynamic Media經典同步。 有關詳細資訊，請參見同步如何工作。

>[!CAUTION]
>
>從現有的Dynamic Media經典公司帳戶匯入資產可能需要很長時間才能顯示AEM。 請確定您在Dynamic Media經典中指定的資料夾沒有太多資產（例如，根資料夾通常擁有太多資產）。
>
>如果您想要測試整合，您可能希望根資料夾只指向子資料夾，而非整個公司。

>[!NOTE]
>
>您可以有多種配置：一個雲端組態代表Dynamic MediaClassic公司的一位使用者。 如果您想要存取其他Dynamic MediaClassic公司或使用者，則需要建立多種組態。

若要設AEM定能夠發佈資產至Dynamic Media經典：

1. 點選圖AEM示並導覽至&#x200B;**[!UICONTROL 部署>Cloud Services]**&#x200B;以存取AdobeDynamic Media經典。

1. 點選「立即設定」。]****[!UICONTROL 

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. 在&#x200B;**[!UICONTROL Title]**&#x200B;欄位中，或者在&#x200B;**[!UICONTROL Name]**&#x200B;欄位中輸入適當的資訊。 點選&#x200B;**[!UICONTROL 建立。]**

   >[!NOTE]
   >
   >建立其他配置時，將顯示&#x200B;**[!UICONTROL parent configuration]**&#x200B;欄位。
   >
   >請&#x200B;**not**&#x200B;更改父配置。 變更父配置會中斷整合。

1. 輸入您的Dynamic Media經典帳戶的電子郵件地址、密碼和地區，然後點選&#x200B;**[!UICONTROL 連線至Dynamic Media經典。]** 您已連接到Dynamic Media經典伺服器，對話框將展開更多選項。

1. 輸入&#x200B;**[!UICONTROL Company]**&#x200B;名稱和&#x200B;**[!UICONTROL Root Path]**(這是發佈的伺服器名稱以及要指定的任何路徑；如果您不知道已發佈的伺服器名稱，請在Dynamic Media經典中，轉至「設定」>「應用程式設定」。]**)**[!UICONTROL 

   >[!NOTE]
   >
   >Dynamic Media經典根路徑是連接到的Dynamic Media經典AEM資料夾。 您可以將其縮小到特定的資料夾。

   >[!CAUTION]
   >
   >根據「Dynamic Media經典」資料夾的大小，導入根資料夾可能需要很長的時間。 此外，Dynamic Media經典資料可能超出儲存AEM空間。 請確定您匯入的資料夾正確無誤。 匯入過多的資料會停止您的系統。

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. 按一下&#x200B;**[!UICONTROL 「確定」。]** AEM保存配置。

>[!NOTE]
>
>如果要重新連接：
>
>* 在發佈時重新連線至Dynamic Media經典時，您可能需要在發佈時重設密碼，或重新連線將無法運作。 這不是作者例項的問題。
>* 如果您修改地區、公司名稱等值，您必須重新連線至Dynamic Media經典。 如果配置選項已修改但未保存，AEM則仍錯誤地指示配置有效。 請務必重新連接。

>



### 啟用Adobe CQDynamic Media經典Dam偵聽器{#enabling-the-adobe-cq-scene-dam-listener}

您必須啟用Adobe CQDynamic Media經典Dam偵聽器，預設情況下禁用該偵聽器。

若要啟用它：

1. 點選「[!UICONTROL 工具]」圖示，然後導覽至「**[!UICONTROL 作業> Web Console」。]** Web控制台隨即開啟。
1. 導航至&#x200B;**[!UICONTROL Adobe CQDynamic Media傳統Dam監聽器]**&#x200B;並選擇&#x200B;**[!UICONTROL 啟用]**&#x200B;複選框。

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. 點選&#x200B;**[!UICONTROL 儲存。]**

### 將可配置超時添加到「Dynamic Media經典上傳」工作流{#adding-configurable-timeout-to-scene-upload-workflow}

當例AEM項設定為透過Dynamic Media傳統型來處理視訊編碼時，任何上傳工作都會有35分鐘逾時。 若要容納可能較長執行時間的視訊編碼工作，您可以設定此設定：

1. 導覽至&#x200B;**http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl**。

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. 在&#x200B;**[!UICONTROL 活動作業超時]**&#x200B;欄位中視需要變更數字。 任何非負數皆以測量單位（以秒為單位）接受。 預設為2100。

   >[!NOTE]
   >
   >最佳實務：大部分資產最多在幾分鐘內收集（例如影像）。 但在某些情況下（例如較大的視訊），逾時值應增加至7200秒（2小時），以容納長的處理時間。 否則，此Dynamic Media經典上載作業在JCR元資料中標籤為&#x200B;**[!UICONTROL UploadFailed]**。

1. 點選&#x200B;**[!UICONTROL 儲存。]**

### 從AEM Assets出發{#autouploading-from-aem-assets}

從AEM6.3.2開始，AEM Assets現在已為您設定，如此，您上傳至數位資產管理員的任何數位資產，如果資產位於CQ目標資料夾中，就會自動更新至Dynamic Media經典。

當資產新增至AEM Assets時，會自動上傳並發佈至Dynamic Media經典。

>[!NOTE]
>
>從AEM Assets自動上傳至Dynamic Media經典的檔案大小上限為500 MB。

要配置來自AEM Assets的自動部署：

1. 點選圖AEM示並導覽至「**[!UICONTROL 部署>Cloud Services]**」，然後在「Dynamic Media」標題下的「可用配置」下，點選「**[!UICONTROL dms7」(Dynamic Media]**)
1. 點選「**[!UICONTROL 進階]**」標籤，選取「啟用自動上傳」核取方塊，然後點選「確定」。******** 您現在需要設定DAM資產工作流程，以包含上傳至Dynamic Media經典。

   >[!NOTE]
   >
   >請參閱[設定推送至Dynamic MediaClassic](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)之資產的狀態（已發佈／未發佈），以取得有關將資產推送至未發佈狀態之Dynamic MediaClassic的資訊。

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. 返回歡迎頁AEM面並點選「**[!UICONTROL 工作流程」。]** 連按兩下「 **DAM更新資** 料流」以開啟它。
1. 在sidekick中，導覽至&#x200B;**[!UICONTROL Workflow]**&#x200B;元件，並選取&#x200B;**[!UICONTROL Dynamic Media經典。]** 將「 **[!UICONTROL Dynamic Media]** 類別」拖曳至工作流程並點選「 **[!UICONTROL 儲存」。]** 在目標資料夾中新增至AEM Assets的資產會自動上傳至Dynamic Media經典。

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* 在自動化後新增資產時，如果資產未放在CQ目標資料夾中，則不會上傳至Dynamic Media經典。
   >* 將所AEM有中繼資料內嵌在XMP上傳至Dynamic Media經典之前，因此中繼資料節點上的所有屬性在Dynamic Media經典中都可使用XMP。


### 設定推送至Dynamic MediaClassic {#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}之資產的狀態（已發佈／未發佈）

如果您要將資產從AEM Assets推送至Dynamic Media經典，您可以自動發佈（預設行為），或將資產推送至未發佈狀態的Dynamic Media經典。

如果您想在測試環境中測試資產後再上線，可能不想立即在Dynamic Media經典上發佈資產。 您可搭AEM配Dynamic Media經典的安全測試環境，將資產直接從資產推送至未發佈狀態的Dynamic Media經典。

Dynamic Media經典資產仍可透過安全預覽提供。 只有在內部發佈資AEM產時，Dynamic Media經典資產才會上線生產。

如果您想在將資產推送至Dynamic Media經典時立即發佈資產，則不需要設定任何選項。 這是預設行為。

不過，如果您不想將資產推送至Dynamic Media經典網站以自動發佈，本節將說明如何設定AEM和Dynamic Media經典網站。

#### 將資產推送至Dynamic Media經典未發佈的先決條件{#prerequisites-to-push-assets-to-scene-unpublished}

您必須先設定下列項目，才能將資產推送至Dynamic Media經典，而不需發佈：

1. [使用Admin Console建立支援案例。](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) 在您的支援案例中，請要求您的Dynamic Media經典帳戶啟用安全預覽。
1. 按照[為您的Dynamic Media經典帳戶設定安全預覽的指示操作。](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html)

這些步驟與您在Dynamic Media經典中建立任何安全測試設定時所遵循的步驟相同。

>[!NOTE]
>
>如果您的安裝環境是Unix 64位作業系統，請參見[https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)，瞭解您需要設定的其他配置選項。

#### 在未發佈狀態推送資產的已知限制{#known-limitations-for-pushing-assets-in-unpublished-state}

如果您使用此功能，請注意下列限制：

* 不支援版本控制。
* 如果資產已在中發佈，AEM且已建立後續版本，則新版本將立即即時發佈至生產環境。 啟動時發佈僅適用於資產的初始發佈。

>[!NOTE]
>
>如果您想要立即發佈資產，最佳實務是將&#x200B;**[!UICONTROL 啟用安全預覽]**&#x200B;設為&#x200B;**[!UICONTROL 立即]**，並使用&#x200B;**[!UICONTROL 啟用自動上傳]**&#x200B;功能。

### 將推送至Dynamic Media經典的資產狀態設定為未發佈{#setting-the-state-of-assets-pushed-to-scene-as-unpublished}

>[!NOTE]
>
>如果使用者在中發佈資AEM產，會自動將S7資產觸發至生產／即時資產（資產將不再處於安全預覽／未發佈狀態）。

將推送至「Dynamic Media經典」的資產狀態設為未發佈：

1. 點選圖AEM示並導覽至「部署>Cloud Services ]**」、點選「Dynamic Media經典]**」，然後在「Dynamic Media經典」中選取您的設定。**[!UICONTROL **[!UICONTROL 
1. 點選&#x200B;**[!UICONTROL Advanced]**&#x200B;標籤。 在&#x200B;**[!UICONTROL 啟用保全檢視]**&#x200B;下拉式選單中，選取「AEM發佈啟動時&#x200B;]**」，將資產推送至Dynamic Media經典，而不發佈。**[!UICONTROL (依預設，此值會設為&#x200B;**[!UICONTROL Immediately]**，其中會立即發佈Dynamic Media經典資產。)

   請參閱[Dynamic Media經典檔案](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html)，以取得在公開之前測試資產的詳細資訊。

   ![chlimage_1-302](assets/chlimage_1-302.png)

1. 點選&#x200B;**[!UICONTROL 確定。]**

啟用「安全檢視」表示您的資產會未發佈推送至安全預覽伺服器。

您可以瀏覽至中某頁上的Dynamic Media經典元件，然後點選AEM **[!UICONTROL 編輯，以檢查此問題。]** 資產的URL中會列出安全預覽伺服器。在中發佈AEM後，檔案參考中的伺服器網域會從預覽URL更新至生產URL。

### 為WCM啟用Dynamic Media經典{#enabling-scene-for-wcm}

需要為WCM啟用Dynamic Media經典軟體，原因有二：

* 若要啟用頁面製作通用視訊設定檔的下拉式清單。 如果沒有此選項，則&#x200B;**[!UICONTROL 通用視訊預設集]**&#x200B;下拉式清單是空的，無法設定。
* 如果目標資料夾中未包含數位資產，如果您在頁面屬性中為該頁面啟用「Dynamic Media經典」，並將資產拖放至「Dynamic Media經典」元件上，則可將資產上傳至「Dynamic Media經典」。 套用一般繼承規則（這表示子頁面將繼承父頁面的設定）。

為WCM啟用Dynamic Media經典時，請注意，與其他配置一樣，繼承規則也適用。 您可以在觸控最佳化或傳統的使用者介面中，為WCM啟用Dynamic MediaClassic。

#### 在觸控最佳化使用者介面{#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}中啟用WCM專用的Dynamic Media經典

若要在觸控最佳化的UI中啟用WCM專用的Dynamic Media經典：

1. 點選圖AEM示並導覽至&#x200B;**[!UICONTROL Sites]**，然後導覽至您網站的根頁面（非特定語言）。

1. 在工具列中，選擇[!UICONTROL settings]圖示，然後點選&#x200B;**[!UICONTROL 開啟屬性。]**

1. 點選&#x200B;**[!UICONTROL Cloud Services]**&#x200B;並點選&#x200B;**[!UICONTROL 新增設定]**&#x200B;並選取&#x200B;**[!UICONTROL Dynamic Media經典。]**
1. 在&#x200B;**[!UICONTROL Adobe的Dynamic Media經典]**&#x200B;下拉式清單中，選取所需的組態，然後點選&#x200B;**[!UICONTROL 確定。]**

   ![chlimage_1-303](assets/chlimage_1-303.png)

   該配置的Dynamic Media經典視頻預設集可用於該頁AEM面和子頁面上的Dynamic Media經典視頻元件。

#### 在Classic用戶介面{#enabling-scene-for-wcm-in-the-classic-user-interface}中為WCM啟用Dynamic Media經典

若要在傳統UI中啟用WCM的Dynamic MediaClassic:

1. 在AEM中，點選「**[!UICONTROL 網站]**」並導覽至您網站的根頁面（非特定語言）。

1. 在sidekick中，點選&#x200B;**[!UICONTROL Page]**&#x200B;圖示並點選&#x200B;**[!UICONTROL Page Properties.]**

1. 點選&#x200B;**[!UICONTROL Cloud Services>新增服務>Dynamic Media經典。]**
1. 在&#x200B;**[!UICONTROL Adobe的Dynamic Media經典]**&#x200B;下拉式清單中，選取所需的組態，然後點選&#x200B;**[!UICONTROL 確定。]**

   該配置的Dynamic Media經典視頻預設集可用於該頁AEM面和子頁面上的Dynamic Media經典視頻元件。

### 配置預設配置{#configuring-a-default-configuration}

如果您有多個Dynamic Media經典配置，則可以指定其中一個配置作為Dynamic Media經典內容瀏覽器的預設配置。

在給定時刻，只能將一個Dynamic Media經典配置標籤為預設。 預設組態是預設會在「Dynamic Media傳統內容瀏覽器」中顯示的公司資產。

要配置預設配置：

1. 點選圖AEM示並導覽至「部署>Cloud Services ]**」、點選「Dynamic Media經典]**」，然後在「Dynamic Media經典」中選取您的設定。**[!UICONTROL **[!UICONTROL 
1. 點選&#x200B;**[!UICONTROL 編輯]**&#x200B;以開啟設定。

1. 在&#x200B;**[!UICONTROL General]**&#x200B;標籤中，選中&#x200B;**[!UICONTROL Default Configuration]**&#x200B;複選框，使此複選框成為顯示在Dynamic Media經典內容瀏覽器中的預設公司和根路徑。

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >如果只有一個配置，則選擇&#x200B;**[!UICONTROL Default Configuration]**&#x200B;複選框將無效。

### 配置臨機資料夾{#configuring-the-ad-hoc-folder}

當資產未位於CQ目標資料夾時，您可以設定資產上傳至Dynamic Media經典資料夾。 請參閱「從CQ目標資料夾外部發佈資產」。

要配置臨機資料夾：

1. 點選圖AEM示並導覽至「部署>Cloud Services ]**」、點選「Dynamic Media經典]**」，然後在「Dynamic Media經典」中選取您的設定。**[!UICONTROL **[!UICONTROL 
1. 點選&#x200B;**[!UICONTROL 編輯]**&#x200B;以開啟設定。

1. 點選&#x200B;**[!UICONTROL Advanced]**&#x200B;標籤。 在&#x200B;**[!UICONTROL 臨機資料夾]**&#x200B;欄位中，您可以修改&#x200B;**臨機資料夾**。 依預設，它是&#x200B;**name_of_the_company/CQ5_adhoc**。

   ![chlimage_1-305](assets/chlimage_1-305.png)

### 設定通用預設集{#configuring-universal-presets}

若要設定視訊元件的「通用預設集」，請參閱[Video](/help/assets/s7-video.md)。

## 啟用MIME類型型資產/Dynamic Media經典上傳作業參數支援{#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

您可以啟用由同步Digital Asset Manager/Dynamic Media經典資產觸發的可配置Dynamic Media經典上載作業參數。

具體來說，您可以在「Web控制台配置」面板的OSGi(Open Service Gateway initiative)區域中按MIME類型配置接受的AEM檔案格式。 然後，您可以自訂JCR（Java內容儲存庫）中每個MIME類型所使用的個別上傳工作參數。

**若要啟用MIME類型型資產：**

1. 點選圖AEM示並導覽至「**[!UICONTROL 工具>作業> Web Console」。]**
1. 在「Adobe Experience ManagerWeb控制台配置」面板的&#x200B;**[!UICONTROL OSGi]**&#x200B;菜單上，按一下&#x200B;**[!UICONTROL 配置。]**
1. 在「名稱」列下，查找並點選&#x200B;**[!UICONTROL Adobe CQDynamic Media經典資產MIME類型服務]**&#x200B;以編輯配置。
1. 在「Mime類型映射」區域中，點選任何加號(+)以新增MIME類型。

   請參閱[支援的MIME類型](/help/assets/assets-formats.md#supported-mime-types)。

1. 在文字欄位中，輸入新的MIME類型名稱。

   例如，您可鍵入`<file_extension>=<mime_type>`作為`EPS=application/postscript`或`PSD=image/vnd.adobe.photoshop`。

1. 在配置窗口的右下角，按一下「保存」。****
1. 返回左AEM側導軌，點選CRXDE Lite。
1. 在CRXDE Lite頁面上，在左側導軌中，導覽至`/etc/cloudservices/scene7/<environment>`（以`<environment>`取代實際名稱）。
1. 展開`<environment>`（以`<environment>`取代實際名稱）以顯示`mimeTypes`節點。
1. 點選您剛新增的mimeType。

   例如，`mimeTypes > application_postscript` OR `mimeTypes > image_vnd.adobe.photoshop`。

1. 在CRXDE Lite頁面的右側，點選&#x200B;**[!UICONTROL 屬性]**&#x200B;標籤。
1. 在&#x200B;**[!UICONTROL jobParam]**&#x200B;值欄位中指定Dynamic Media傳統上傳工作參數。

   例如，`psprocess="rasterize"&psresolution=120` 。

   有關您可使用的其他上載作業參數，請參閱[AdobeDynamic Media經典映像生產系統API](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-overview.html)。

   >[!NOTE]
   >
   >如果要上傳PSD檔案，而您想要以圖層擷取的範本處理，請在&#x200B;**[!UICONTROL jobParam]**&#x200B;值欄位中輸入下列：
   >
   >`process=MaintainLayers&createTemplate=true`
   >
   >請確定您的PSD檔案有「圖層」。 如果它只是一張影像或具有遮色片的影像，則會視為影像處理，因為沒有要處理的圖層。

1. 在CRXDE Lite頁面的左上角，點選「全部儲存」。]****[!UICONTROL 

## 疑難排解Dynamic MediaAEM經典與整合{#troubleshooting-scene-and-aem-integration}

如果您無法與Dynamic MediaClassic整AEM合，請參閱下列解決方案案例。

**如果您的數位資產發佈至Dynamic Media經典網站失敗：**

* 檢查您嘗試上傳的資產是否位於&#x200B;**[!UICONTROL CQ target]**&#x200B;資料夾中(您在Dynamic MediaClassic雲端設定中指定此資料夾)。
* 如果沒有，您必須在&#x200B;**[!UICONTROL 頁面屬性]**&#x200B;中設定該頁面的雲端設定，以允許上傳至&#x200B;**[!UICONTROL CQ adhoc]**&#x200B;資料夾。

* 檢查日誌中是否有任何資訊。

**如果您的視訊預設集未出現：**

* 請確定您已透過&#x200B;**[!UICONTROL 頁面屬性設定該頁面的雲端設定。]** Dynamic Media經典視訊元件提供視訊預設集。

**如果您的視訊資產未在中播放AEM:**

* 請確定您已使用正確的視訊元件。 Dynamic Media傳統視訊元件與基礎視訊元件不同。 請參閱[Foundation Video Component vs.Dynamic Media經典視頻元件](/help/assets/s7-video.md)。

**如果中的新資產或已修AEM改資產未自動上傳至Dynamic Media經典：**

* 請確定資產位於CQ目標資料夾中。 只有CQ目標資料夾中的資產會自動更新(前提是您設定AEM Assets自動上傳資產)。
* 請確定您已將Cloud Services設定設定為「啟用自動上傳」，且您已更新並儲存DAM資產工作流程，以包含Dynamic Media傳統上傳。
* 將影像上傳至「Dynamic Media經典」目標檔案夾的子檔案夾時，請確定您執行下列其中一項作業：

   * 請確定所有資產的名稱（不論位置）都是唯一的。 否則，主目標資料夾中的資產將被刪除，並且只保留子資料夾中的資產。
   * 變更Dynamic Media經典帳戶設定區域中資產覆寫方式。 若您在子檔案夾中使用同名資產，請勿將Dynamic Media·Classic設定為覆寫資產，不論其位置為何。

**如果您刪除的資產或資料夾未在Dynamic Media經典與AEM:**

* 在AEM Assets刪除的資產和資料夾仍顯示在Dynamic Media經典的同步資料夾中。 您必須手動刪除它們。

**如果視訊上傳失敗**

* 如果您的視訊上傳失敗，而您正使用AEM透過Dynamic Media傳統型整合來編碼視訊，請參閱「新增可設定逾時至Dynamic Media傳統型上傳工作流程」](#adding-configurable-timeout-to-scene-upload-workflow)。[

>[!CAUTION]
>
>從現有的Dynamic Media經典公司帳戶匯入資產可能需要很長時間才能顯示AEM。 請確定您在Dynamic Media經典中指定的資料夾沒有太多資產（例如，根資料夾通常擁有太多資產）。
>
>如果您想要測試整合，您可能希望根資料夾只指向子資料夾，而非整個公司。

