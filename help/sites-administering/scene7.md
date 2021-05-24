---
title: 與Dynamic Media Classic整合
description: 了解如何整合Adobe Experience Manager與Dynamic Media Classic。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: f244cfb5-5550-4f20-92f0-bb296e2bf76e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '5517'
ht-degree: 0%

---

# 與Dynamic Media Classic整合{#integrating-with-dynamic-media-classic-scene}

AdobeDynamic Media Classic是托管解決方案，可管理、增強、發佈及將多媒體資產傳送至網路、行動裝置、電子郵件及與網際網路連線的顯示器及列印。

若要使用Dynamic Media Classic，您必須設定雲端設定，讓Dynamic Media Classic和Adobe Experience Manager Assets可以互動。 本檔案說明如何設定Experience Manager和Dynamic Media Classic。

如需在頁面上使用所有Dynamic Media Classic元件和使用視訊的相關資訊，請參閱[使用Dynamic Media Classic](../assets/scene7.md)。

>[!NOTE]
>
>* Dynamic Media Classic的DHTML檢視器平台已於2014年1月31日正式終止服務。 如需詳細資訊，請參閱[DHTML檢視器生命週期結束常見問題集](../sites-administering/dhtml-viewer-endoflifefaqs.md)。
>* 在將Dynamic Media Classic設定為可搭配Experience Manager使用之前，請參閱[最佳實務](#best-practices-for-integrating-scene-with-aem)，以整合Dynamic Media Classic與Experience Manager。
>* 如果您使用Dynamic Media Classic搭配自訂的Proxy設定，則必須同時設定兩個HTTP用戶端Proxy設定，因為Experience Manager的某些功能使用3.x API，而其他功能則使用4.x API。 3.x以[http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)配置，4.x以[http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)配置。

>



## Experience Manager/Dynamic Media Classic整合與Dynamic Media {#aem-scene-integration-versus-dynamic-media}

Experience Manager使用者可以選擇使用Dynamic Media的兩種解決方案。 您可以使用下列其中一項：

* 將您的Experience Manager例項與Dynamic Media Classic整合。
* 使用已整合至Experience Manager的Dynamic Media。

請使用下列條件來決定要選擇的解決方案：

* 如果您是&#x200B;**現有** Dynamic Media Classic客戶，其豐富型媒體資產位於Dynamic Media Classic以進行發佈和傳送，但您想要將這些資產與Sites(WCM)製作和/或Experience Manager資產整合以進行管理，請使用本檔案所述的[Experience Manager/Dynamic Media Classic點對點整合](#aem-scene-point-to-point-integration)。

* 如果您是具有豐富媒體傳送需求的&#x200B;**new** Experience Manager客戶，請選取[Dynamic Media選項](#aem-dynamic-media)。 如果您沒有現有的S7帳戶，且該系統中儲存了許多資產，此選項最有意義。

* 在某些情況下，請同時使用這兩種解決方案。 [雙用方案](/help/sites-administering/scene7.md#dual-use-scenario)描述了該方案。

### Experience Manager/Dynamic Media Classic點對點整合{#aem-scene-point-to-point-integration}

在此解決方案中使用資產時，您會執行下列其中一項作業：

* 將資產直接上傳至Dynamic Media Classic，然後透過&#x200B;**Dynamic Media Classic**&#x200B;內容瀏覽器存取，以進行頁面編寫或
* 上傳至Experience Manager資產，然後啟用自動發佈至Dynamic Media Classic;您可透過&#x200B;**Assets**&#x200B;內容瀏覽器存取頁面編寫

您用於此整合的元件位於[設計模式的&#x200B;**Dynamic Media Classic**&#x200B;元件區域。](/help/sites-authoring/author-environment-tools.md#page-modes)

### Experience ManagerDynamic Media {#aem-dynamic-media}

Experience ManagerDynamic Media是直接在Experience Manager平台中統一Dynamic Media Classic功能。

在此解決方案中使用資產時，請遵循此工作流程：

1. 直接上傳單一影像和視訊資產至Experience Manager。
1. 直接在Experience Manager中編碼視訊。
1. 直接在Experience Manager中建立影像型集。
1. 若適用，可為影像或影片增加互動功能。

您用於Dynamic Media的元件位於[設計模式](/help/sites-authoring/author-environment-tools.md#page-modes)的&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;元件區域。 包括下列項目：

* **[!UICONTROL Dynamic Media]**  — 動 **[!UICONTROL 態]** 媒體元件是智慧型的，視您新增影像或視訊而定，您有各種選項。元件支援影像預設集、以影像為基礎的檢視器，例如影像集、回轉集、混合媒體集和視訊。 此外，檢視器回應速度快 — 螢幕大小會根據螢幕大小自動變更。 所有檢視器都是HTML5檢視器。

* **[!UICONTROL 互動式媒體]**  - **[!UICONTROL 互]** 動式媒體元件適用於轉盤橫幅、互動式影像和互動式視訊等資產。這些資產在其中具有交互性，這些熱點或影像地圖。 此元件是智慧的。 也就是說，視您新增影像或影片而定，您有各種選項。 此外，檢視器回應速度快 — 螢幕大小會根據螢幕大小自動變更。 所有檢視器都是HTML5檢視器。

### 雙用方案{#dual-use-scenario}

立即可用，您可以同時使用Dynamic Media和Dynamic Media Classic的Experience Manager整合功能。 下列使用案例表說明了何時開啟或關閉某些區域。

若要同時使用Dynamic Media和Dynamic Media Classic:

1. 在Cloud Services中設定[Dynamic Media Classic](#creating-a-cloud-configuration-for-scene)。
1. 請依照您使用案例的特定指示操作：

   <table>
    <tbody>
    <tr>
    <td> </td>
    <td> </td>
    <td><strong>Dynamic Media</strong></td>
    <td> </td>
    <td><strong>Dynamic Media Classic整合</strong></td>
    <td> </td>
    </tr>
    <tr>
    <td><strong>如果您……</strong></td>
    <td><strong>使用案例工作流程</strong></td>
    <td><strong>影像/影片</strong></td>
    <td><strong>動態媒體元件</strong></td>
    <td><strong>S7內容瀏覽器和元件</strong></td>
    <td><strong>從資產自動上傳至S7</strong></td>
    </tr>
    <tr>
    <td>網站與Dynamic Media新手</td>
    <td>上傳資產至Experience Manager，並使用Experience ManagerDynamic Media元件在Sites頁面上製作資產</td>
    <td><p>開啟</p> <p>（請參閱步驟3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">開啟</a></td>
    <td>關閉</td>
    <td>關閉</td>
    </tr>
    <tr>
    <td>零售、Sites和Dynamic Media新手</td>
    <td>上傳非產品資產至Experience Manager以進行管理和傳送。 將產品資產上傳至Dynamic Media Classic，並在Experience Manager和元件中使用Dynamic Media Classic內容瀏覽器，在Sites上製作產品詳細資料頁面。</td>
    <td><p>開啟</p> <p>（請參閱步驟3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">開啟</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">開啟</a></td>
    <td>關閉</td>
    </tr>
    <tr>
    <td>資產與Dynamic Media</td>
    <td>上傳資產至Experience Manager資產，並使用Dynamic Media中發佈的URL/內嵌程式碼</td>
    <td><p>開啟</p> <p>（請參閱步驟3）</p> </td>
    <td>關閉</td>
    <td>關閉</td>
    <td>關閉</td>
    </tr>
    <tr>
    <td>Dynamic Media和範本的新手</td>
    <td>使用Dynamic Media進行影像處理和影片處理。 在Dynamic Media Classic中製作影像範本，並使用Dynamic Media Classic內容尋找器，在Sites頁面中納入範本。</td>
    <td><p>開啟</p> <p>（請參閱步驟3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">開啟</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">開啟</a></td>
    <td>關閉</td>
    </tr>
    <tr>
    <td>Dynamic Media Classic現有客戶，是Sites的新手</td>
    <td>將資產上傳至Dynamic Media Classic，並使用Experience ManagerDynamic Media Classic內容瀏覽器，在Sites頁面上搜尋和撰寫資產</td>
    <td>關閉</td>
    <td>關閉</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">開啟</a></td>
    <td>關閉</td>
    </tr>
    <tr>
    <td>現有Dynamic Media Classic客戶，是Sites和Assets的新手</td>
    <td>將資產上傳至DAM並自動發佈至Dynamic Media Classic以供傳送。 使用Experience ManagerDynamic Media Classic內容瀏覽器，在Sites頁面上搜尋和編寫資產。</td>
    <td>關閉</td>
    <td>關閉</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">開啟</a></td>
    <td><p><a href="#configuringautouploadingfromaemassets">開啟</a></p> <p>（請參閱步驟4）</p> </td>
    </tr>
    <tr>
    <td>現有Dynamic Media Classic客戶和新資產</td>
    <td><p>上傳資產至Experience Manager，並使用Dynamic Media產生轉譯以供下載/共用。 自動將Experience Manager資產發佈至Dynamic Media Classic以進行傳送。</p> <p><strong>重要：</strong> 在Experience Manager中產生的重複處理和轉譯不會同步至Dynamic Media Classic</p> </td>
    <td><p>開啟</p> <p>（請參閱步驟3）</p> </td>
    <td>關閉</td>
    <td>關閉</td>
    <td><p><a href="#configuringautouploadingfromaemassets">開啟</a></p> <p>（請參閱步驟4）</p> </td>
    </tr>
    </tbody>
    </table>

1. (可選；請參閱使用案例表格) — 設定[Dynamic Media雲端設定](/help/assets/config-dynamic.md)和[啟用Dynamic Media伺服器](/help/assets/config-dynamic.md)。
1. (可選；請參閱使用案例表格) — 如果您選擇啟用「從資產自動上傳至Dynamic Media Classic」，則必須新增下列項目：

   1. 設定自動上傳至Dynamic Media Classic。
   1. 在&#x200B;***Dam更新資產**工作流程(`https://<server>:<host>/cf#/etc/workflow/models/dam/update_asset.html)`)結尾的所有Dynamic Media工作流程步驟*&#x200B;之後，新增&#x200B;**Dynamic Media Classic上傳**&#x200B;步驟
   1. （選用）以[https://&lt;server>:&lt;port>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl)中的MIME類型限制Dynamic Media傳統資產上傳。 未在此清單中的資產MIME類型不會上傳至Dynamic Media Classic伺服器。
   1. （選用）在Dynamic Media Classic設定中設定影片。 您可以同時為Dynamic Media和Dynamic Media Classic啟用視訊編碼，或兩者皆啟用。 動態轉譯會用於在Experience Manager例項中在本機預覽和播放，而Dynamic Media Classic視訊轉譯則會產生並儲存在Dynamic Media Classic伺服器上。 為Dynamic Media和Dynamic Media Classic設定視訊編碼服務時，請將[視訊處理設定檔](/help/assets/video-profiles.md)套用至Dynamic Media Classic資產資料夾。
   1. （選用）[在Dynamic Media Classic](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)中設定安全預覽。

#### 限制 {#limitations}

同時啟用Dynamic Media Classic和Dynamic Media時，有下列限制：

* 選取資產並將其拖曳至Dynamic Media頁面上的Dynamic Media Classic元件後，手動上傳至Experience Manager Classic無法運作。
* 即使在Assets中編輯Experience Manager時，Analytics-Dynamic Media Classic同步的資產會自動更新至Dynamic Media Classic，回滾動作不會觸發新上傳。 因此，Dynamic Media Classic在回復後不會立即取得最新版本。 解決方法是在回滾完成後重新編輯。
* 如果您必須將Dynamic Media用於某個使用案例，並將Dynamic Media Classic整合用於另一個使用案例，讓Dynamic Media資產不會與Dynamic Media Classic系統互動，則請勿將Dynamic Media Classic設定套用至Dynamic Media資料夾。 此外，請勿將Dynamic Media設定（處理設定檔）套用至Dynamic Media Classic資料夾。

## 整合Dynamic Media Classic與Experience Manager{#best-practices-for-integrating-scene-with-aem}的最佳實務

將Dynamic Media Classic與Experience Manager整合時，以下方面必須遵循一些重要的最佳實務：

* 測試推動整合
* 若干案例建議直接從Dynamic Media Classic上傳資產

請參閱[已知限制](#known-limitations-and-design-implications)。

### 測試推動整合{#test-driving-your-integration}

Adobe建議您只將根資料夾指向子資料夾，而非整個公司，以此測試整合。

>[!CAUTION]
>
>從現有的Dynamic Media Classic公司帳戶匯入資產可能需花很長的時間才會顯示在Experience Manager中。 請確定您在Dynamic Media Classic中指定的資料夾沒有太多資產（例如，根資料夾經常有太多資產，且可能會導致系統當機）。

### 從Experience Manager資產上傳資產與從Dynamic Media Classic上傳資產{#uploading-assets-from-aem-assets-versus-from-scene}

您可以使用Assets（數位資產管理）功能，或透過Dynamic Media Classic內容瀏覽器直接以Experience Manager方式存取Dynamic Media Classic，以上傳資產。 您選擇哪個取決於下列因素：

* Dynamic Media ClassicExperience Manager尚不支援的資產類型，必須透過Dynamic Media Classic內容瀏覽器，直接從Dynamic Media Classic新增至Experience Manager網站。 例如，影像範本。
* 針對Experience Manager資產和Dynamic Media Classic均支援的資產類型，決定如何上傳取決於下列項目：

   * 資產目前位於
   * 在通用儲存庫中管理這些檔案的重要性

如果資產已在Dynamic Media Classic中，且在通用存放庫中管理這些資產並不重要，則將資產匯出至Experience Manager資產時僅將資產同步回Dynamic Media Classic進行傳送是不必要的往返作業。 否則，建議您將資產保留在單一存放庫中，並僅同步至Dynamic Media Classic進行傳送。

## 設定Dynamic Media Classic整合{#configuring-scene-integration}

您可以設定Experience Manager以將資產上傳至Dynamic Media Classic。 CQ Target資料夾中的Experience Manager可從Target上傳（自動或手動）至Dynamic Media Classic公司帳戶。

>[!NOTE]
>
>Adobe建議您只使用指定的目標資料夾來匯入Dynamic Media Classic資產。 位於目標資料夾外部的數位資產，只能在已啟用Dynamic Media Classic設定的頁面上用於Dynamic Media Classic元件。 此外，這些量度還會放在Dynamic Media Classic的臨機資料夾中。 臨機資料夾未與Experience Manager同步(但可在Dynamic Media Classic內容瀏覽器中找到資產)。

若要設定Dynamic Media Classic以與Experience Manager整合，您必須完成下列步驟：

1. [定義雲端設定](#creating-a-cloud-configuration-for-scene)  — 定義Dynamic Media Classic資料夾和Assets資料夾之間的對應。即使您只想要單向(將資產Experience Manager為Dynamic Media Classic)同步，請完成此步驟。
1. [啟用 **Adobe CQ s7dam Dam監聽器**](#enabling-the-adobe-cq-scene-dam-listener)  — 在OSGiconsole中完  成。
1. 如果您希望Experience Manager資產自動上傳至Dynamic Media Classic，必須開啟該選項，並將Dynamic Media Classic新增至[!UICONTROL DAM更新資產]工作流程。 您也可以手動上傳資產。
1. 將Dynamic Media Classic元件新增至sidekick。 此功能可讓使用者在其Experience Manager頁面上使用Dynamic Media Classic元件。
1. [將設定對應至Experience Manager中的頁面](#enabling-scene-for-wcm)  — 若要檢視您在Dynamic Media Classic中建立的任何視訊預設集，必須執行此步驟。如果您必須從CQ目標資料夾外部執行將資產發佈至Dynamic Media Classic，也需要用到ID服務。

本節說明如何執行所有這些步驟，並列出重要限制。

### Dynamic Media Classic和Experience Manager資產之間的同步如何運作{#how-synchronization-between-scene-and-aem-assets-works}

設定Experience Manager資產和Dynamic Media Classic同步時，請務必了解下列事項：

#### 從Experience Manager資產{#uploading-to-scene-from-aem-assets}上傳至Dynamic Media Classic

* 在Experience Manager中為Dynamic Media Classic上傳指定了同步資料夾。
* 如果將數位資產放在指定的同步資料夾中，則可自動上傳至Dynamic Media Classic。
* Experience Manager中的資料夾和子資料夾結構會在Dynamic Media Classic中複製。

>[!NOTE]
>
>Experience Manager會先將所有中繼資料內嵌為XMP，再將其上傳至Dynamic Media Classic，因此中繼資料節點上的所有屬性都可在Dynamic Media Classic中以XMP形式使用。

#### 已知限制和設計意涵{#known-limitations-and-design-implications}

同步Experience Manager資產和Dynamic Media Classic後，目前有下列限制/設計含意：

<table>
 <tbody>
  <tr>
   <td><strong>限制/設計暗示</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>一個指定的同步（目標）資料夾</td>
   <td>對於Dynamic Media Classic上傳，Experience Manager中每個公司只能有一個指定的資料夾。 如果您必須可存取Dynamic Media Classic中的多個公司帳戶，則可建立多個設定。</td>
  </tr>
  <tr>
   <td>資料夾結構</td>
   <td>如果您刪除包含資產的同步資料夾，所有Dynamic Media Classic遠端資產都會遭刪除，但資料夾仍會保留。</td>
  </tr>
  <tr>
   <td>臨機資料夾</td>
   <td>駐留在WCM中手動上傳至Dynamic Media Classic的目標資料夾外的資產，會自動放置在Dynamic Media Classic的個別臨機資料夾中。 您可以在雲端設定中以Experience Manager配置此資料夾。</td>
  </tr>
  <tr>
   <td>混合媒體</td>
   <td>混合媒體集會顯示在Experience Manager中，但不支援Experience Manager。</td>
  </tr>
  <tr>
   <td>PDF</td>
   <td>從Dynamic Media Classic的eCatalog產生的PDF會匯入至CQ目標資料夾。</td>
  </tr>
  <tr>
   <td>重新整理UI</td>
   <td>在Experience Manager與Dynamic Media Classic之間同步時，請務必重新整理使用者介面以檢視變更。 </td>
  </tr>
  <tr>
   <td>視訊縮圖</td>
   <td>如果上傳視訊至「Experience Manager資產」以透過Dynamic Media Classic進行編碼，視訊縮圖和編碼的視訊可能需要一些時間才能在「Experience Manager資產」中使用，端視視訊處理時間而定。</td>
  </tr>
  <tr>
   <td>Target子資料夾</td>
   <td><p>如果您在目標資料夾內使用子資料夾，請確定您對每個資產使用唯一的名稱（不論位置），或是設定Dynamic Media Classic（在「設定」區域）不會覆寫資產，不論位置。</p> <p>否則，上傳至Dynamic Media Classic目標子資料夾的同名資產將會上傳，但目標資料夾中同名的資產則會刪除。 </p> </td>
  </tr>
 </tbody>
</table>

### 配置Dynamic Media Classic伺服器{#configuring-scene-servers}

如果在代理後運行Experience Manager或具有特殊的防火牆設定，則必須顯式啟用不同區域的主機。 伺服器在`/etc/cloudservices/scene7/endpoints`中的內容中進行管理，並可根據需要自定義。 點選URL，然後編輯以變更URL（如有必要）。 在舊版Experience Manager中，這些值是硬式編碼。

如果導覽至`/etc/cloudservices/scene7/endpoints.html`，您會看到列出的伺服器（並點選URL即可編輯伺服器）:

![chlimage_1-296](assets/chlimage_1-296.png)

### 為Dynamic Media Classic {#creating-a-cloud-configuration-for-scene}建立雲配置

雲端設定定義Dynamic Media Classic資料夾和Experience Manager資產資料夾之間的對應。 必須將其設定為將Experience Manager資產與Dynamic Media Classic同步。 如需詳細資訊，請參閱同步如何運作。

>[!CAUTION]
>
>從現有的Dynamic Media Classic公司帳戶匯入資產可能需花很長的時間才會顯示在Experience Manager中。 請確定您在Dynamic Media Classic中指定的資產不太多的資料夾。 例如，根資料夾通常包含太多資產。
>
>如果您想要測試促進整合，請讓根資料夾只指向子資料夾，而非整個公司。

>[!NOTE]
>
>您可以有多個設定：一個雲端設定代表Dynamic Media Classic公司的一名使用者。 如果您想要存取其他Dynamic Media Classic公司或使用者，必須建立多個設定。

若要設定Experience Manager以將資產發佈至Dynamic Media Classic:

1. 點選Experience Manager圖示並導覽至&#x200B;**[!UICONTROL 部署>Cloud Services]**&#x200B;以存取AdobeDynamic Media Classic。

1. 點選&#x200B;**[!UICONTROL 立即配置]**。

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. 在&#x200B;**[!UICONTROL Title]**&#x200B;欄位中，或者在&#x200B;**[!UICONTROL Name]**&#x200B;欄位中輸入相應資訊。 點選&#x200B;**[!UICONTROL 建立]**。

   >[!NOTE]
   >
   >建立更多配置時，將顯示&#x200B;**[!UICONTROL parent configuration]**&#x200B;欄位。
   >
   >更改父配置。 ****&#x200B;變更上層組態可能會中斷整合。

1. 輸入Dynamic Media Classic帳戶的電子郵件地址、密碼和地區，然後點選&#x200B;**[!UICONTROL 連線至Dynamic Media Classic]**。 您已連線至Dynamic Media Classic伺服器，對話方塊會展開並顯示更多選項。

1. 輸入&#x200B;**[!UICONTROL 公司]**&#x200B;名稱和&#x200B;**[!UICONTROL 根路徑]**。 此資訊是已發佈的伺服器名稱以及您要指定的任何路徑。 如果您不知道已發佈的伺服器名稱，請在Dynamic Media Classic中前往&#x200B;**[!UICONTROL 設定>應用程式設定]**)。

   >[!NOTE]
   >
   >Dynamic Media Classic根路徑是連接的Dynamic Media Classic資料夾Experience Manager。 可縮小到特定資料夾。

   >[!CAUTION]
   >
   >視Dynamic Media Classic資料夾的大小而定，匯入根資料夾可能需要很長時間。 此外，Dynamic Media Classic資料可能會超過Experience Manager儲存空間。 請確定您匯入的資料夾正確無誤。 導入太多資料可能會停止系統。

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. 按一下&#x200B;**[!UICONTROL 「確定」]**。Experience Manager會儲存您的設定。

>[!NOTE]
>
>如果要重新連接：
>
>* 在發佈時重新連線至Dynamic Media Classic時，在發佈時重設密碼或重新連線無法運作（在製作執行個體上沒有問題）。
>* 如果您修改地區、公司名稱等值，必須重新連線至Dynamic Media Classic。 如果已修改但未儲存設定選項，Experience Manager仍錯誤指出設定有效。 請務必重新連線。

>



### 啟用Adobe CQ Dynamic Media Classic Dam監聽器{#enabling-the-adobe-cq-scene-dam-listener}

啟用Adobe CQ Dynamic Media Classic Dam監聽器，此偵聽器預設為停用。

若要啟用Adobe CQ Dynamic Media Classic Dam監聽器：

1. 點選[!UICONTROL 工具]圖示，然後導覽至&#x200B;**[!UICONTROL 操作> Web Console]**。 Web控制台開啟。
1. 導覽至&#x200B;**[!UICONTROL Adobe CQ Dynamic Media Classic Dam Listener]**&#x200B;並選取&#x200B;**[!UICONTROL Enabled]**&#x200B;核取方塊。

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. 點選&#x200B;**[!UICONTROL 儲存]**。

### 將可設定的逾時新增至Dynamic Media Classic上傳工作流程{#adding-configurable-timeout-to-scene-upload-workflow}

依預設，當Experience Manager例項設定為透過Dynamic Media Classic處理視訊編碼時，任何上傳工作都會有35分鐘的逾時。 為了適應運行時間可能更長的視頻編碼作業，可以配置此設定：

1. 導覽至&#x200B;**http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl**。

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. 根據需要在&#x200B;**[!UICONTROL 活動作業超時]**&#x200B;欄位中更改數字。 以秒為單位接受任何非負數。 此數字預設為2100。

   >[!NOTE]
   >
   >最佳實務：大部分資產最多會在數分鐘內擷取（例如影像）。 但在某些情況下（例如較大的視訊），會將逾時值增加至7200秒（2小時），以容納長的處理時間。 否則，此Dynamic Media Classic上傳工作在JCR中繼資料中會標示為&#x200B;**[!UICONTROL UploadFailed]**。

1. 點選&#x200B;**[!UICONTROL 儲存]**。

### 從Experience Manager資產上傳{#autouploading-from-aem-assets}

從Experience Manager6.3.2開始，系統會設定「Experience Manager資產」，如果資產位於CQ目標資料夾中，上傳至資產管理員的所有數位資產都會更新至Dynamic Media Classic。

當資產新增至Experience Manager資產時，資產會自動上傳並發佈至Dynamic Media Classic。

>[!NOTE]
>
>自動從Experience Manager資產上傳至Dynamic Media Classic的檔案大小上限為500 MB。

若要從Experience Manager資產設定自動上傳：

1. 點選Experience Manager圖示並導覽至&#x200B;**[!UICONTROL 部署>Cloud Services]**，然後在Dynamic Media標題下的「可用設定」下，點選&#x200B;**[!UICONTROL dms7(Dynamic Media]**)
1. 點選「**[!UICONTROL Advanced]**」標籤，選取「**[!UICONTROL 啟用自動上傳]**」核取方塊，然後點選「**[!UICONTROL OK]**」。 您現在必須設定DAM Asset工作流程，以納入上傳至Dynamic Media Classic。

   >[!NOTE]
   >
   >請參閱[設定推送至Dynamic Media Classic](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)之資產的狀態（已發佈/未發佈），以取得有關將資產推送至未發佈狀態之Dynamic Media Classic的資訊。

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. 導覽回Experience Manager歡迎頁面，然後點選&#x200B;**[!UICONTROL Workflows]**。 連按兩下&#x200B;**DAM更新資產**&#x200B;工作流程以開啟它。
1. 在sidekick中，導覽至&#x200B;**[!UICONTROL Workflow]**&#x200B;元件，然後選取&#x200B;**[!UICONTROL Dynamic Media Classic]**。 將&#x200B;**[!UICONTROL Dynamic Media Classic]**&#x200B;拖曳至工作流程，然後點選&#x200B;**[!UICONTROL Save]**。 新增至目標資料夾中Experience Manager資產的資產會自動上傳至Dynamic Media Classic。

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* 自動化後新增資產時，如果資產未放在CQ Target資料夾中，則不會上傳至Dynamic Media Classic。
   >* Experience Manager會先將所有中繼資料內嵌為XMP，再將其上傳至Dynamic Media Classic，因此中繼資料節點上的所有屬性都可在Dynamic Media Classic中以XMP形式使用。


### 設定推送至Dynamic Media Classic {#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}的資產狀態（已發佈/未發佈）

如果您要將Experience Manager資產從Assets推送至Dynamic Media Classic，可以自動發佈（預設行為），或以未發佈狀態將資產推送至Dynamic Media Classic。

如果您想在測試環境中測試資產，然後再上線，就可能不想在Dynamic Media Classic上立即發佈資產。 您可以透過Dynamic Media Classic的安全測試環境使用Experience Manager，以取消發佈狀態將資產直接從資產推送至Dynamic Media Classic。

Dynamic Media Classic資產仍可透過安全預覽功能使用。 只有在Experience Manager中發佈資產時，Dynamic Media Classic資產才會上線生產。

如果您想在將資產推送至Dynamic Media Classic時立即發佈資產，則不需要設定任何選項。 此功能為預設行為。

不過，如果您不想將資產推送至Dynamic Media Classic以自動發佈，本節將說明如何設定Experience Manager和Dynamic Media Classic以執行此功能。

#### 將資產推送至Dynamic Media Classic的必要條件未發佈{#prerequisites-to-push-assets-to-scene-unpublished}

您必須先設定下列項目，才能將資產推送至Dynamic Media Classic而不發佈：

1. [使用Admin Console建立支援案例。](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) 在您的支援案例中，請為您的Dynamic Media Classic帳戶啟用安全預覽功能。
1. 請依照[為您的Dynamic Media Classic帳戶設定安全預覽的指示操作。](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html)

這些步驟與您在Dynamic Media Classic中建立任何安全測試設定時要遵循的步驟相同。

>[!NOTE]
>
>如果您的安裝環境是UNIX® 64位作業系統，請參閱[https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)，以了解您必須設定的其他配置選項。

#### 以未發佈狀態推送資產的已知限制{#known-limitations-for-pushing-assets-in-unpublished-state}

如果您使用此功能，請注意下列限制：

* 不支援版本控制。
* 如果Experience Manager中已發佈資產，且已建立後續版本，則新版本會立即發佈至生產環境。 啟動時發佈僅適用於資產的初始發佈。

>[!NOTE]
>
>如果您想要立即發佈資產，最佳實務是將&#x200B;**[!UICONTROL 啟用安全預覽]**&#x200B;設為&#x200B;**[!UICONTROL 立即]**&#x200B;並使用&#x200B;**[!UICONTROL 啟用自動上傳]**&#x200B;功能。

### 將推送至Dynamic Media Classic的資產狀態設為未發佈{#setting-the-state-of-assets-pushed-to-scene-as-unpublished}

>[!NOTE]
>
>如果使用者以Experience Manager發佈資產，則會自動觸發S7資產至生產/即時資產（資產不再安全預覽/取消發佈）。

若要將推送至Dynamic Media Classic的資產狀態設為未發佈：

1. 點選Experience Manager圖示，並導覽至&#x200B;**[!UICONTROL 部署>Cloud Services]**，點選&#x200B;**[!UICONTROL Dynamic Media Classic]**，然後在Dynamic Media Classic中選取您的設定。
1. 點選&#x200B;**[!UICONTROL 進階]**&#x200B;標籤。 在&#x200B;**[!UICONTROL 啟用安全檢視]**&#x200B;下拉式選單中，選取「AEM發佈啟動時&#x200B;]**」 ，即可將資產推送至Dynamic Media Classic，而不需發佈。**[!UICONTROL (預設情況下，此值會設為&#x200B;**[!UICONTROL Immediale]**，其中會立即發佈Dynamic Media Classic資產。)

   請參閱[Dynamic Media Classic檔案](https://help.adobe.com/en_US/scene7/using/WSd968ca97bf00cf72-5eeee3a113268dc80f5-8000.html) ，以取得在公開之前測試資產的詳細資訊。

   ![chlimage_1-302](assets/chlimage_1-302.png)

1. 點選&#x200B;**[!UICONTROL 確定]**。

啟用安全預覽表示資產已取消發佈並推送至安全預覽伺服器。

若要查看是否已啟用安全預覽，請導覽至Dynamic Media Classic元件(位於Experience Manager中的頁面)。 點選「**[!UICONTROL Edit]**」。 資產的URL中列有安全預覽伺服器。 在Experience Manager中發佈後，檔案參考中的伺服器網域會從預覽URL更新至生產URL。

### 為WCM {#enabling-scene-for-wcm}啟用Dynamic Media Classic

為WCM啟用Dynamic Media Classic有兩個必要：

* 它會啟用頁面編寫的通用視訊設定檔下拉式清單。 若沒有此清單，**[!UICONTROL 通用視訊預設集]**&#x200B;下拉式清單會是空白且無法設定。
* 如果數位資產不在目標資料夾中，如果您在頁面屬性中為該頁面啟用Dynamic Media Classic，則可將資產上傳至Dynamic Media Classic。 然後將資產拖放至Dynamic Media Classic元件。 套用一般繼承規則（亦即子頁面會繼承上層頁面的設定）。

如同其他設定一樣，為WCM啟用Dynamic Media Classic時，會套用繼承規則。 您可以在觸控最佳化或傳統式使用者介面中，為WCM啟用Dynamic Media Classic。

#### 在觸控最佳化使用者介面{#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}中啟用Dynamic Media Classic以執行WCM

若要在觸控最佳化UI中為WCM啟用Dynamic Media Classic:

1. 點選Experience Manager圖示並導覽至&#x200B;**[!UICONTROL Sites]**，然後導覽至您網站的根頁面（非語言特定）。

1. 在工具列中，選取[!UICONTROL settings]圖示，然後點選&#x200B;**[!UICONTROL 開啟屬性]**。

1. 點選&#x200B;**[!UICONTROL Cloud Services]**&#x200B;並點選&#x200B;**[!UICONTROL 新增設定]**&#x200B;並選取&#x200B;**[!UICONTROL Dynamic Media Classic]**。
1. 在&#x200B;**[!UICONTROL AdobeDynamic Media Classic]**&#x200B;下拉式清單中，選取所需的設定，然後點選&#x200B;**[!UICONTROL 確定]**。

   ![chlimage_1-303](assets/chlimage_1-303.png)

   該Dynamic Media Classic設定的視訊預設集可用於該頁面和子頁面上與Dynamic Media Classic視訊元件Experience Manager時。

#### 在Classic使用者介面{#enabling-scene-for-wcm-in-the-classic-user-interface}中為WCM啟用Dynamic Media Classic

若要在傳統UI中為WCM啟用Dynamic Media Classic:

1. 在Experience Manager中，點選&#x200B;**[!UICONTROL 網站]**&#x200B;並導覽至您網站的根頁面（非語言特定）。

1. 在sidekick中，點選&#x200B;**[!UICONTROL Page]**&#x200B;圖示，然後點選&#x200B;**[!UICONTROL Page Properties]**。

1. 點選&#x200B;**[!UICONTROL Cloud Services>新增服務> Dynamic Media Classic]**。
1. 在&#x200B;**[!UICONTROL AdobeDynamic Media Classic]**&#x200B;下拉式清單中，選取所需的設定，然後點選&#x200B;**[!UICONTROL 確定]**。

   該Dynamic Media Classic設定的視訊預設集可用於該頁面和子頁面上與Dynamic Media Classic視訊元件Experience Manager時。

### 配置預設配置{#configuring-a-default-configuration}

如果您有多個Dynamic Media Classic設定，您可以指定其中一個作為Dynamic Media Classic內容瀏覽器的預設設定。

指定時間只能將一個Dynamic Media Classic設定標示為預設設定。 預設設定是預設顯示於Dynamic Media Classic內容瀏覽器的公司資產。

要配置預設配置：

1. 點選Experience Manager圖示，並導覽至&#x200B;**[!UICONTROL 部署>Cloud Services]**，點選&#x200B;**[!UICONTROL Dynamic Media Classic]**，然後在Dynamic Media Classic中選取您的設定。
1. 若要開啟設定，請點選&#x200B;**[!UICONTROL 編輯]**。

1. 在&#x200B;**[!UICONTROL 一般]**&#x200B;標籤中，選取&#x200B;**[!UICONTROL 預設設定]**&#x200B;核取方塊，讓它成為顯示在Dynamic Media Classic內容瀏覽器中的預設公司和根路徑。

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >如果只有一個配置，則選擇&#x200B;**[!UICONTROL 預設配置]**&#x200B;複選框無效。

### 配置Ad-hoc資料夾{#configuring-the-ad-hoc-folder}

當資產不在CQ Target資料夾時，您可以設定在Dynamic Media Classic中上傳資產的資料夾。 請參閱從CQ目標資料夾外部發佈資產。

設定臨機資料夾：

1. 點選Experience Manager圖示，並導覽至&#x200B;**[!UICONTROL 部署>Cloud Services]**，點選&#x200B;**[!UICONTROL Dynamic Media Classic]**，然後在Dynamic Media Classic中選取您的設定。
1. 若要開啟設定，請點選&#x200B;**[!UICONTROL 編輯]**。

1. 點選&#x200B;**[!UICONTROL 進階]**&#x200B;標籤。 在&#x200B;**[!UICONTROL Ad-hoc Folder]**&#x200B;欄位中，您可以修改&#x200B;**Ad-hoc**&#x200B;資料夾。 依預設，它是&#x200B;**name_of_the_company/CQ5_adhoc**。

   ![chlimage_1-305](assets/chlimage_1-305.png)

### 配置通用預設集{#configuring-universal-presets}

要配置視頻元件的通用預設，請參閱[Video](/help/assets/s7-video.md)。

## 啟用MIME類型型Assets/Dynamic Media Classic上傳工作參數支援{#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

您可以啟用同步Digital Asset Manager/Dynamic Media Classic資產所觸發的可設定Dynamic Media Classic上傳工作參數。

具體來說，您可以在「Experience ManagerWeb控制台配置」面板的OSGi（開放服務網關計畫）區域中，按MIME類型配置接受的檔案格式。 然後，您可以自訂用於JCR(Java™ Content Repository)中每個MIME類型的個別上傳工作參數。

**若要啟用MIME類型型資產：**

1. 點選Experience Manager圖示並導覽至&#x200B;**[!UICONTROL 工具>作業> Web Console]**。
1. 在「 Adobe Experience Manager Web Console Configuration 」面板的&#x200B;**[!UICONTROL OSGi]**&#x200B;功能表上，點選「 **[!UICONTROL Configuration]** 」。
1. 在「名稱」欄下，尋找並點選&#x200B;**[!UICONTROL Adobe CQ Dynamic Media Classic資產MIME類型Service]**&#x200B;以編輯設定。
1. 在「Mime類型映射」區域中，點選任何加號(+)以添加MIME類型。

   請參閱[支援的MIME類型](/help/assets/assets-formats.md#supported-mime-types)。

1. 在文字欄位中，輸入新的MIME類型名稱。

   例如，您可鍵入`<file_extension>=<mime_type>` ，如`EPS=application/postscript`或`PSD=image/vnd.adobe.photoshop`中。

1. 在設定視窗的右下角，點選&#x200B;**[!UICONTROL Save]**。
1. 返回Experience Manager，在左側導軌中，點選「CRXDE Lite」。
1. 在CRXDE Lite頁面的左側邊欄中，導覽至`/etc/cloudservices/scene7/<environment>`（以實際名稱取代`<environment>`）。
1. 展開`<environment>`（以實際名稱替代`<environment>`）以顯示`mimeTypes`節點。
1. 點選您剛新增的mimeType。

   例如， `mimeTypes > application_postscript`或`mimeTypes > image_vnd.adobe.photoshop`。

1. 在CRXDE Lite頁面的右側，點選「 **[!UICONTROL Properties]**」標籤。
1. 在&#x200B;**[!UICONTROL jobParam]**&#x200B;值欄位中指定Dynamic Media Classic上傳工作參數。

   例如， `psprocess="rasterize"&psresolution=120` 。

   如需可使用的上傳工作參數，請參閱[AdobeDynamic Media Classic影像生產系統API](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-overview.html) 。

   >[!NOTE]
   >
   >如果要上傳PSD檔案，並且要以層提取的模板形式處理這些檔案，請在&#x200B;**[!UICONTROL jobParam]**&#x200B;值欄位中輸入以下內容：
   >
   >`process=MaintainLayers&layerNaming=AppendName&createTemplate=true`
   >
   >確保PSD檔案具有「圖層」。 如果嚴格來說，它是一個影像或帶有遮罩的影像，則它將作為影像處理，因為沒有要處理的圖層。

1. 在CRXDE Lite頁面的左上角，點選「**[!UICONTROL Save All]**」。

## 疑難排解Dynamic Media Classic和Experience Manager整合{#troubleshooting-scene-and-aem-integration}

如果您無法將Experience Manager與Dynamic Media Classic整合，請參閱下列解決方案案例。

**如果您的數位資產發佈至Dynamic Media Classic失敗：**

* 檢查您上傳的資產是否位於&#x200B;**[!UICONTROL CQ目標]**&#x200B;資料夾中(您可在Dynamic Media Classic雲端設定中指定此資料夾)。
* 若未設定，您必須在&#x200B;**[!UICONTROL 頁面屬性]**&#x200B;中設定該頁面的雲端設定，以允許上傳至&#x200B;**[!UICONTROL CQ ad hoc]**&#x200B;資料夾。

* 檢查記錄以取得任何資訊。

**如果未顯示您的視訊預設集：**

* 請確定您已透過&#x200B;**[!UICONTROL 頁面屬性]**&#x200B;設定該頁面的雲端設定。 Dynamic Media Classic視訊元件中提供視訊預設集。

**如果您的視訊資產未以Experience Manager播放：**

* 請確定您使用正確的視訊元件。 Dynamic Media Classic視訊元件與foundation Video元件不同。 請參閱[Foundation視訊元件與Dynamic Media Classic視訊元件比較](/help/assets/s7-video.md)。

**如果Experience Manager中的新資產或修改的資產沒有自動上傳至Dynamic Media Classic:**

* 確認資產位於CQ目標資料夾中。 系統只會自動更新CQ目標資料夾中的資產(前提是您已設定Experience Manager資產以自動上傳資產)。
* 確認您已將Cloud Services設定設為「啟用自動上傳」，且已更新並儲存DAM Asset工作流程，以包含Dynamic Media Classic上傳。
* 將影像上傳至Dynamic Media Classic目標資料夾的子資料夾時，請確定您執行下列其中一項操作：

   * 請確定所有資產的名稱（無論位置為何）都是唯一的。 否則，主目標資料夾中的資產會遭刪除，且只會保留子資料夾中的資產。
   * 變更Dynamic Media Classic覆寫Dynamic Media Classic帳戶「設定」區域中資產的方式。 如果您在子檔案夾中使用名稱相同的資產，則不要設定Dynamic Media Classic以覆寫資產，無論位置為何。

**如果您刪除的資產或資料夾未在Dynamic Media Classic和Experience Manager之間同步：**

* 在「Experience Manager資產」中刪除的資產和資料夾仍會顯示在Dynamic Media Classic的同步資料夾中。 手動刪除。

**如果視訊上傳失敗**

* 如果您的視訊上傳失敗，而您正使用Experience Manager透過Dynamic Media Classic整合來編碼視訊，請參閱[將可設定的逾時新增至Dynamic Media Classic上傳工作流程](#adding-configurable-timeout-to-scene-upload-workflow)。

>[!CAUTION]
>
>從現有的Dynamic Media Classic公司帳戶匯入資產可能需花很長的時間才會顯示在Experience Manager中。 請確定您在Dynamic Media Classic中指定的資產不太多的資料夾。 例如，根資料夾通常包含太多資產。
>
>如果您想要測試促進整合，請讓根資料夾只指向子資料夾，而非整個公司。
