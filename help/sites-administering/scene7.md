---
title: 將Adobe Experience Manager與Dynamic Media Classic整合
description: 瞭解如何將Adobe Experience Manager與Dynamic Media Classic整合。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: f244cfb5-5550-4f20-92f0-bb296e2bf76e
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: tm+mt
source-wordcount: '5405'
ht-degree: 1%

---

# 將Adobe Experience Manager與Dynamic Media Classic整合 {#integrating-with-dynamic-media-classic-scene}

Adobe Dynamic Media Classic是託管式解決方案，可管理、增強和發佈多媒體資產，並將其遞送至網路、行動裝置、電子郵件和網際網路連線的顯示和列印。

若要使用Dynamic Media Classic，您必須設定雲端設定，以便Dynamic Media Classic和Adobe Experience Manager Assets可以相互互動。 本檔案說明如何設定Experience Manager和Dynamic Media Classic。

如需在頁面上使用所有Dynamic Media Classic元件以及使用視訊的詳細資訊，請參閱[使用Dynamic Media Classic](../assets/scene7.md)。

>[!NOTE]
>
>* Dynamic Media Classic的DHTML檢視器平台於2014年1月31日正式終止服務。 如需詳細資訊，請參閱[DHTML檢視器生命週期結束常見問答集](../sites-administering/dhtml-viewer-endoflifefaqs.md)。
>* 在設定Dynamic Media Classic以搭配Experience Manager使用之前，請參閱[將Dynamic Media Classic與Experience Manager整合的最佳實務](#best-practices-for-integrating-scene-with-aem)。
>* 如果您使用Dynamic Media Classic搭配自訂Proxy設定，則必須同時設定HTTP使用者端Proxy設定，因為Experience Manager的某些功能會使用3.x API，而其他功能則會使用4.x API。 3.x是以[http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)設定，而4.x是以[http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)設定。
>

## Experience Manager/Dynamic Media Classic整合與Dynamic Media比較 {#aem-scene-integration-versus-dynamic-media}

Experience Manager使用者可以選擇使用兩個解決方案，以搭配Dynamic Media使用。 您可以使用下列其中一項：

* 將您的Experience Manager執行個體與Dynamic Media Classic整合。
* 使用整合至Experience Manager的Dynamic Media。

請使用下列條件來決定要選擇的解決方案：

* 您是否為&#x200B;**現有**&#x200B;個Dynamic Media Classic客戶，其資產位於Dynamic Media Classic以進行發佈和交付，但您想要將這些資產與Sites (WCM)製作或Experience Manager Assets （或兩者）整合？ 若是如此，請使用本檔案所述的[Experience Manager/Dynamic Media Classic點對點整合](#aem-scene-point-to-point-integration)。

* 如果您是&#x200B;**新**&#x200B;的Experience Manager客戶，且有豐富的媒體傳遞需求，請選取[動態媒體選項](#aem-dynamic-media)。 如果您沒有現有的S7帳戶且系統中儲存許多資產，此選項將最有意義。

* 在某些情況下，請同時使用這兩個解決方案。 [雙重使用案例](/help/sites-administering/scene7.md#dual-use-scenario)說明該案例。

### Experience Manager/Dynamic Media Classic點對點整合 {#aem-scene-point-to-point-integration}

在此解決方案中使用資產時，需執行下列任一項作業：

* 將資產直接上傳到Dynamic Media Classic，然後透過&#x200B;**Dynamic Media Classic**&#x200B;內容瀏覽器進行存取，以進行頁面製作或
* 上傳至Experience Manager Assets，然後啟用自動發佈至Dynamic Media Classic；您透過&#x200B;**Assets**&#x200B;內容瀏覽器存取以進行頁面製作

您用於此整合的元件可在[設計模式](/help/sites-authoring/author-environment-tools.md#page-modes)的&#x200B;**Dynamic Media Classic**&#x200B;元件區域中找到。

### Experience Manager動態媒體 {#aem-dynamic-media}

Experience Manager Dynamic Media是直接在Experience Manager平台中統一的Dynamic Media Classic功能。

在此解決方案中使用資產時，請遵循此工作流程：

1. 將單一影像和視訊資產直接上傳至Experience Manager。
1. 直接在Experience Manager中編碼視訊。
1. 直接在Experience Manager中建立影像型集合。
1. 如果適用，請將互動性新增至影像或視訊。

您用於Dynamic Media的元件可在[設計模式](/help/sites-authoring/author-environment-tools.md#page-modes)中的&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;元件區域中找到。 這些功能包括：

* **[!UICONTROL Dynamic Media]** - **[!UICONTROL Dynamic Media]**&#x200B;元件是智慧型的 — 視您新增影像或視訊而定，您有各種選項。 元件支援影像預設集、影像型檢視器（例如影像集、迴轉集、混合媒體集及視訊）。 此外，檢視器會回應 — 畫面大小會自動根據畫面大小變更。 所有檢視器皆為HTML5檢視器。

* **[!UICONTROL 互動媒體]** - **[!UICONTROL 互動媒體]**&#x200B;元件適用於轉盤橫幅、互動影像和互動視訊等資產。 這類資產具有互動功能，例如熱點或影像地圖。 此元件是智慧型的。 也就是說，視您新增影像或影片而定，您有各種選項。 此外，檢視器會回應 — 畫面大小會自動根據畫面大小變更。 所有檢視器皆為HTML5檢視器。

### 雙重使用案例 {#dual-use-scenario}

開箱即用地同時使用Experience Manager的Dynamic Media和Dynamic Media Classic整合功能。 下列使用案例表格說明何時開啟及關閉某些區域。

若要同時使用Dynamic Media和Dynamic Media Classic：

1. 在Cloud Services中設定[Dynamic Media Classic](#creating-a-cloud-configuration-for-scene)。
1. 請依照使用案例的特定指示：

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
    <td><strong>影像/視訊</strong></td>
    <td><strong>動態媒體元件</strong></td>
    <td><strong>S7內容瀏覽器和元件</strong></td>
    <td><strong>從Assets自動上傳至S7</strong></td>
    </tr>
    <tr>
    <td>Sites和Dynamic Media的新手</td>
    <td>將資產上傳至Experience Manager並使用Experience Manager Dynamic Media元件在Sites頁面上製作資產</td>
    <td><p>於</p> <p>（請參閱步驟3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">於</a></td>
    <td>關閉</td>
    <td>關閉</td>
    </tr>
    <tr>
    <td>零售業中，以及Sites和Dynamic Media的新手</td>
    <td>將非產品資產上傳至Experience Manager以進行管理和傳送。 將產品資產上傳到Dynamic Media Classic，並使用Experience Manager中的Dynamic Media Classic內容瀏覽器和元件在網站上製作產品詳細資料頁面。</td>
    <td><p>於</p> <p>（請參閱步驟3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">於</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">於</a></td>
    <td>關閉</td>
    </tr>
    <tr>
    <td>Assets和Dynamic Media的新手</td>
    <td>將資產上傳至Experience Manager Assets，並使用從Dynamic Media發佈的URL/內嵌程式碼</td>
    <td><p>於</p> <p>（請參閱步驟3）</p> </td>
    <td>關閉</td>
    <td>關閉</td>
    <td>關閉</td>
    </tr>
    <tr>
    <td>Dynamic Media與範本化的新手</td>
    <td>使用Dynamic Media來處理影像和視訊。 在Dynamic Media Classic中製作影像範本，並使用Dynamic Media Classic內容尋找器將範本納入Sites頁面。</td>
    <td><p>於</p> <p>（請參閱步驟3）</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">於</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">於</a></td>
    <td>關閉</td>
    </tr>
    <tr>
    <td>現有的Dynamic Media Classic客戶和Sites的新客戶</td>
    <td>將資產上傳至Dynamic Media Classic，並使用Experience Manager Dynamic Media Classic內容瀏覽器在Sites頁面上搜尋及編寫資產</td>
    <td>關閉</td>
    <td>關閉</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">於</a></td>
    <td>關閉</td>
    </tr>
    <tr>
    <td>現有的Dynamic Media Classic客戶，並且是網站和Assets的新手</td>
    <td>將資產上傳至DAM並自動發佈至Dynamic Media Classic以進行傳送。 使用Experience Manager Dynamic Media Classic內容瀏覽器來搜尋及編寫Sites頁面上的資產。</td>
    <td>關閉</td>
    <td>關閉</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">於</a></td>
    <td><p><a href="#configuringautouploadingfromaemassets">於</a></p> <p>（請參閱步驟4）</p> </td>
    </tr>
    <tr>
    <td>現有的Dynamic Media Classic客戶和Assets的新客戶</td>
    <td><p>將資產上傳到Experience Manager並使用Dynamic Media產生轉譯以供下載/共用。 自動發佈Experience Manager資產至Dynamic Media Classic以進行傳送。</p> <p><strong>重要：</strong>發生重複處理，且Experience Manager中產生的轉譯未同步至Dynamic Media Classic</p> </td>
    <td><p>於</p> <p>（請參閱步驟3）</p> </td>
    <td>關閉</td>
    <td>關閉</td>
    <td><p><a href="#configuringautouploadingfromaemassets">於</a></p> <p>（請參閱步驟4）</p> </td>
    </tr>
    </tbody>
    </table>

1. （選用；請參閱使用案例表） — 設定[Dynamic Media雲端設定](/help/assets/config-dynamic.md)並[啟用Dynamic Media伺服器](/help/assets/config-dynamic.md)。
1. （選用；請參閱使用案例表格） — 如果您選擇啟用從Assets自動上傳到Dynamic Media Classic，則必須新增下列專案：

   1. 設定自動上傳至Dynamic Media Classic。
   1. 在&#x200B;***Dam更新資產**工作流程(`https://<server>:<host>/cf#/etc/workflow/models/dam/update_asset.html)`)結尾的所有Dynamic Media工作流程步驟*&#x200B;後新增&#x200B;**Dynamic Media Classic上傳**&#x200B;步驟
   1. （選用）在[https://&lt;server>：&lt;port>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl)中依MIME型別限制Dynamic Media Classic資產上傳。 此清單中沒有的資產MIME型別不會上傳至Dynamic Media Classic伺服器。
   1. （選用）在Dynamic Media Classic設定中設定視訊。 您可以同時為Dynamic Media和/或Dynamic Media Classic啟用視訊編碼。 動態轉譯可用於在Experience Manager例項本機預覽和播放，而Dynamic Media Classic視訊轉譯則會產生並儲存在Dynamic Media Classic伺服器上。 為Dynamic Media和Dynamic Media Classic設定視訊編碼服務時，請將[視訊處理設定檔](/help/assets/video-profiles.md)套用至Dynamic Media Classic資產資料夾。
   1. （選用） [在Dynamic Media Classic中設定安全預覽](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)。

#### 限制 {#limitations}

同時啟用Dynamic Media Classic和動態媒體時，會有下列限制：

* 在Dynamic Media Classic頁面上選取資產並將其拖曳至Dynamic Media Classic元件，以手動方式上傳至Experience Manager無法運作。
* 即使在Assets中編輯資產時，Experience Manager-Dynamic Media Classic同步資產會自動更新至Dynamic Media Classic，復原動作不會觸發新的上傳。 因此，Dynamic Media Classic不會在復原後立即取得最新版本。 因應措施是在復原完成後再次編輯。
* 您是否需要將Dynamic Media用於一個使用案例，並將Dynamic Media Classic整合用於另一個使用案例，以便Dynamic Media資產不會與Dynamic Media Classic系統互動？ 若是如此，請勿將Dynamic Media Classic設定套用至Dynamic Media資料夾。 此外，請勿將Dynamic Media設定（處理設定檔）套用至Dynamic Media Classic資料夾。

## 將Dynamic Media Classic與Experience Manager整合的最佳做法 {#best-practices-for-integrating-scene-with-aem}

將Dynamic Media Classic與Experience Manager整合時，請務必遵循下列重要的最佳作法：

* 測試推動您的整合
* 建議在某些情況下直接從Dynamic Media Classic上傳資產

請參閱[已知限制](#known-limitations-and-design-implications)。

### 測試推動您的整合 {#test-driving-your-integration}

Adobe建議您讓根資料夾僅指向子資料夾，而非整個公司，以測試整合。

>[!CAUTION]
>
>從現有的Dynamic Media Classic公司帳戶匯入資產時，可能需要花很長時間才能在Experience Manager中顯示。 請務必在Dynamic Media Classic中指定不含太多資產的資料夾（例如，根資料夾通常含有太多資產，可能會導致系統當機）。

### 從Experience Manager Assets上傳資產與從Dynamic Media Classic上傳資產 {#uploading-assets-from-aem-assets-versus-from-scene}

您可以使用Assets （數位資產管理）功能，或直接在Experience Manager中，透過Dynamic Media Classic內容瀏覽器存取Dynamic Media Classic ，上傳資產。 選擇哪一種取決於下列因素：

* Experience Manager Assets尚未支援的Dynamic Media Classic資產型別必須直接透過Dynamic Media Classic內容瀏覽器，從Dynamic Media Classic新增至Experience Manager網站。 例如影像範本。
* 對於Experience Manager Assets和Dynamic Media Classic都支援的資產型別，決定如何上傳它們取決於以下因素：

   * 資產目前所在的位置，以及
   * 在通用存放庫中管理這些區段的重要性

假設資產已在Dynamic Media Classic中，在通用存放庫管理這些資產並不重要。 如果是這種情況，那麼將資產匯出至Experience Manager Assets時，只需將其同步回Dynamic Media Classic進行傳送，就不需要進行往返測試。 Adobe建議您將資產放在單一存放庫中，並同步至Dynamic Media Classic以僅供傳送。

## 設定Dynamic Media Classic整合 {#configuring-scene-integration}

您可以設定Experience Manager將資產上傳至Dynamic Media Classic。 CQ目標資料夾中的Assets可以從Experience Manager （自動或手動）上傳至Dynamic Media Classic公司帳戶。

>[!NOTE]
>
>Adobe建議您只使用指定的目標資料夾來匯入Dynamic Media Classic資產。 位於目標資料夾之外的數位資產只能在已啟用Dynamic Media Classic設定的頁面上的Dynamic Media Classic元件中使用。 此外，它們會被放在Dynamic Media Classic的隨選資料夾中。 隨選資料夾未與Experience Manager同步(但資產可在Dynamic Media Classic內容瀏覽器中找到)。

**若要設定Dynamic Media Classic以與Experience Manager整合：**

1. [定義雲端設定](#creating-a-cloud-configuration-for-scene) — 定義Dynamic Media Classic資料夾與Assets資料夾之間的對應。 即使您只想要單向(Experience Manager Assets到Dynamic Media Classic)同步，請完成此步驟。
1. [啟用&#x200B;**Adobe CQ s7dam Dam接聽程式**](#enabling-the-adobe-cq-scene-dam-listener) — 在[!UICONTROL OSGi]主控台中完成。
1. 如果您希望Experience Manager Assets自動上傳至Dynamic Media Classic，您必須開啟該選項，並將Dynamic Media Classic新增至[!UICONTROL DAM更新資產]工作流程。 您也可以手動上傳資產。
1. 將Dynamic Media Classic元件新增至Sidekick。 此功能可讓使用者在其Experience Manager頁面上使用Dynamic Media Classic元件。
1. [將設定對應到Experience Manager中的頁面](#enabling-scene-for-wcm) — 檢視您在Dynamic Media Classic中建立的任何視訊預設集都需要此步驟。 如果您必須從CQ目標資料夾外部將資產發佈到Dynamic Media Classic，也需要用到API。

本節說明如何執行上述所有步驟，並列出重要限制。

### Dynamic Media Classic與Experience Manager Assets之間的同步運作方式 {#how-synchronization-between-scene-and-aem-assets-works}

設定Experience Manager Assets和Dynamic Media Classic同步時，請務必瞭解下列事項：

#### 從Experience Manager Assets上傳至Dynamic Media Classic {#uploading-to-scene-from-aem-assets}

* Experience Manager中有一個指定的同步資料夾可供Dynamic Media Classic上傳。
* 如果數位資產放在指定的同步資料夾中，上傳至Dynamic Media Classic的操作可以自動化。
* Experience Manager中的資料夾和子資料夾結構會複製到Dynamic Media Classic。

>[!NOTE]
>
>Experience Manager會將所有中繼資料都內嵌為XMP，然後再上傳至Dynamic Media Classic，因此中繼資料節點上的所有屬性都可在Dynamic Media Classic as XMP中使用。

#### 已知限制和設計含意 {#known-limitations-and-design-implications}

透過Experience Manager Assets與Dynamic Media Classic之間的同步，目前有下列限制/設計影響：

<table>
 <tbody>
  <tr>
   <td><strong>限制/設計影響</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>一個指定的同步（目標）資料夾</td>
   <td>在Experience Manager中，每個公司只能有一個指定的資料夾用於Dynamic Media Classic上傳。 如果您必須在Dynamic Media Classic中擁有多個公司帳戶的存取權，則可建立多個設定。</td>
  </tr>
  <tr>
   <td>檔案夾結構</td>
   <td>如果您刪除與資產同步的資料夾，則會刪除所有Dynamic Media Classic遠端資產，但會保留資料夾。</td>
  </tr>
  <tr>
   <td>隨選資料夾</td>
   <td>在WCM中手動上傳至Dynamic Media Classic的目標資料夾以外的Assets，會自動放置在Dynamic Media Classic上的個別隨選資料夾中。 您可以在Experience Manager的雲端設定中設定此資料夾。</td>
  </tr>
  <tr>
   <td>混合媒體</td>
   <td>混合媒體集會顯示在Experience Manager中，不過在Experience Manager中並不支援。</td>
  </tr>
  <tr>
   <td>PDF</td>
   <td>從Dynamic Media Classic中的eCatalogs產生的PDF會匯入至CQ目標資料夾。</td>
  </tr>
  <tr>
   <td>UI重新整理</td>
   <td>在Experience Manager和Dynamic Media Classic之間同步時，請務必重新整理使用者介面以檢視變更。 </td>
  </tr>
  <tr>
   <td>視訊縮圖</td>
   <td>如果透過Dynamic Media Classic將視訊上傳至Experience Manager Assets以進行編碼，視訊縮圖和編碼視訊可能需要一些時間才能在Experience Manager Assets中使用，實際時間取決於視訊處理時間。</td>
  </tr>
  <tr>
   <td>目標子資料夾</td>
   <td><p>如果您在目標資料夾中使用子資料夾，請務必對每個資產使用唯一名稱（無論位置為何）。 此外，請務必將Dynamic Media Classic （在設定區域中）設定為不覆寫資產，無論位置為何。</p> <p>否則，系統會上傳名稱相同，但上傳至Dynamic Media Classic目標子資料夾的資產，但會刪除目標資料夾中名稱相同的資產。 </p> </td>
  </tr>
 </tbody>
</table>

### 設定Dynamic Media Classic伺服器 {#configuring-scene-servers}

如果您透過Proxy執行Experience Manager或進行特殊的防火牆設定，您必須明確啟用不同區域的主機。 伺服器在`/etc/cloudservices/scene7/endpoints`的內容中進行管理，並可視需要自訂。 選取URL，然後視需要編輯以變更URL。 在舊版Experience Manager中，這些值會加上硬式編碼。

如果您導覽至`/etc/cloudservices/scene7/endpoints.html`，您會看到列出的伺服器（並可點選URL加以編輯）：

![chlimage_1-296](assets/chlimage_1-296.png)

### 建立Dynamic Media Classic的雲端設定 {#creating-a-cloud-configuration-for-scene}

雲端設定會定義Dynamic Media Classic資料夾與Experience Manager Assets資料夾之間的對應。 必須將其設定為將Experience Manager Assets與Dynamic Media Classic同步。 如需詳細資訊，請參閱同步化的運作方式。

>[!CAUTION]
>
>從現有的Dynamic Media Classic公司帳戶匯入資產時，可能需要花很長時間才能在Experience Manager中顯示。 請務必在Dynamic Media Classic中指定沒有太多資產的資料夾。 例如，根資料夾通常有太多資產。
>
>如果您想要測試整合，請讓根資料夾僅指向子資料夾，而非整個公司。

>[!NOTE]
>
>您可以有多個設定：一個雲端設定代表一家Dynamic Media Classic公司的一名使用者。 如果您想要存取其他Dynamic Media Classic公司或使用者，您必須建立多個設定。

**若要建立Dynamic Media Classic的雲端設定：**

1. 選取Experience Manager圖示並導覽至&#x200B;**[!UICONTROL 部署]** > **[!UICONTROL 雲端服務]**，讓您能夠存取Adobe Dynamic Media Classic。

1. 選取&#x200B;**[!UICONTROL 立即設定]**。

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. 在&#x200B;**[!UICONTROL Title]**&#x200B;欄位中，以及選擇性地在&#x200B;**[!UICONTROL Name]**&#x200B;欄位中，輸入適當的資訊。 選取「**[!UICONTROL 建立]**」。

   >[!NOTE]
   >
   >建立更多組態時，會顯示&#x200B;**[!UICONTROL 父組態]**&#x200B;欄位。
   >
   >請&#x200B;**不**&#x200B;變更父設定。 變更父設定可能會中斷整合。

1. 輸入您Dynamic Media Classic帳戶的電子郵件地址、密碼和地區，然後選取&#x200B;**[!UICONTROL 連線至Dynamic Media Classic]**。 您已連線至Dynamic Media Classic伺服器，且對話方塊會展開並顯示更多選項。

1. 輸入&#x200B;**[!UICONTROL 公司]**&#x200B;名稱和&#x200B;**[!UICONTROL 根路徑]**。 此資訊是發佈的伺服器名稱以及您要指定的任何路徑。 如果您不知道已發佈的伺服器名稱，請在Dynamic Media Classic中移至&#x200B;**[!UICONTROL 設定>應用程式設定]**。

   >[!NOTE]
   >
   >Dynamic Media Classic根路徑是Experience Manager連線到的Dynamic Media Classic資料夾。 可將其縮小至特定資料夾。

   >[!CAUTION]
   >
   >根據Dynamic Media Classic資料夾的大小，匯入根資料夾可能需要很長的時間。 此外，Dynamic Media Classic資料可能會超過Experience Manager儲存空間。 請確定您匯入的資料夾正確。 匯入太多資料可能會停止系統。

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. 選取&#x200B;**[!UICONTROL 確定]**。 Experience Manager會儲存您的設定。

>[!NOTE]
>
>如果您要重新連線：
>
>* 在發佈時重新連線到Dynamic Media Classic時，在發佈或重新連線時重設密碼不起作用（在作者執行個體上不是問題）。
>* 若您修改了地區、公司名稱等值，則必須重新連線至Dynamic Media Classic。 如果組態選項經修改後仍未儲存，Experience Manager仍會錯誤地指出組態有效。 請務必重新連線。
>

### 啟用Adobe CQ Dynamic Media Classic Dam監聽器 {#enabling-the-adobe-cq-scene-dam-listener}

啟用Adobe CQ Dynamic Media Classic Dam接聽程式，此功能預設為停用。

**若要啟用Adobe CQ Dynamic Media Classic Dam接聽程式：**

1. 選取[!UICONTROL 工具]圖示，然後導覽至&#x200B;**[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]**。
1. 在Web主控台中，導覽至&#x200B;**[!UICONTROL Adobe CQ Dynamic Media Classic Dam接聽程式]**，並選取&#x200B;**[!UICONTROL 已啟用]**&#x200B;核取方塊。

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. 選取「**[!UICONTROL 儲存]**」。

### 將可設定的逾時新增至Dynamic Media Classic上傳工作流程 {#adding-configurable-timeout-to-scene-upload-workflow}

當Experience Manager執行個體設定為透過Dynamic Media Classic處理視訊編碼時，依預設，任何上傳工作都有35分鐘的逾時。 若要因應可能較長的視訊編碼工作，您可以設定此設定。

1. 導覽至&#x200B;**http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl**。

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. 視需要在&#x200B;**[!UICONTROL 作用中工作逾時]**&#x200B;欄位中變更數字。 任何非負數皆可接受，並以秒為單位測量。 此數字預設為2100。

   >[!NOTE]
   >
   >最佳實務：大部分資產至多會在數分鐘內擷取（例如影像）。 但在某些情況下（例如較大的影片），請將逾時值增加到7200秒（兩個小時），以因應較長的處理時間。 否則，此Dynamic Media Classic上傳工作在JCR (Java™內容存放庫)中繼資料中會標示為&#x200B;**[!UICONTROL UploadFailed]**。

1. 選取「**[!UICONTROL 儲存]**」。

### 從Experience Manager Assets自動上傳 {#autouploading-from-aem-assets}

從Experience Manager 6.3.2開始，Experience Manager Assets已設定為如果任何上傳的數位資產位於CQ目標資料夾，則會更新至Dynamic Media Classic。

將資產新增至Experience Manager Assets後，系統會自動將其上傳並發佈至Dynamic Media Classic。

>[!NOTE]
>
>從Experience Manager Assets自動上傳到Dynamic Media Classic的檔案大小上限為500 MB。

**從Experience Manager Assets自動上傳：**

1. 選取Experience Manager圖示並導覽至&#x200B;**[!UICONTROL 部署]** > **[!UICONTROL 雲端服務]**。
1. 在「動態媒體」標題的「可用設定」下方，選取&#x200B;**[!UICONTROL dms7 (Dynamic Media]**)。
1. 選取&#x200B;**[!UICONTROL 進階]**&#x200B;標籤，選取&#x200B;**[!UICONTROL 啟用自動上傳]**&#x200B;核取方塊，然後選取&#x200B;**[!UICONTROL 確定]**。 設定DAM資產工作流程，以包含上傳至Dynamic Media Classic的內容。

   >[!NOTE]
   >
   >請參閱[設定推送至Dynamic Media Classic的資產狀態（已發佈/未發佈）](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)，以取得將資產推送至處於未發佈狀態的Dynamic Media Classic的資訊。

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. 導覽回Experience Manager歡迎頁面，並選取&#x200B;**[!UICONTROL 工作流程]**。 連按兩下&#x200B;**DAM更新資產**&#x200B;工作流程，使其開啟。
1. 在Sidekick中，導覽至&#x200B;**[!UICONTROL 工作流程]**&#x200B;元件，並選取&#x200B;**[!UICONTROL Dynamic Media Classic]**。 將&#x200B;**[!UICONTROL Dynamic Media Classic]**&#x200B;拖曳至工作流程並選取&#x200B;**[!UICONTROL 儲存]**。 目標資料夾中新增至Experience Manager Assets的Assets會自動上傳至Dynamic Media Classic。

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* 在自動化後新增資產時，如果這些資產未放置在CQ目標資料夾中，則不會上傳到Dynamic Media Classic。
   >* Experience Manager會將所有中繼資料都內嵌為XMP，然後再上傳至Dynamic Media Classic，因此中繼資料節點上的所有屬性都可在Dynamic Media Classic as XMP中使用。

### 設定推送至Dynamic Media Classic的資產狀態（已發佈/未發佈） {#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}

如果您要將資產從Experience Manager Assets推送到Dynamic Media Classic，您可以自動發佈（預設行為）或是在未發佈狀態下將資產推送到Dynamic Media Classic。

如果您想要在資產上線前在中繼環境中測試資產，您可能不想立即在Dynamic Media Classic上發佈資產。 您可以使用Experience Manager搭配Dynamic Media Classic的安全測試環境，以未發佈狀態直接從Assets推送資產至Dynamic Media Classic。

Dynamic Media Classic資產仍可透過安全預覽使用。 只有當資產在Experience Manager內發佈時，Dynamic Media Classic資產才會正式上線。

如果您想要在推送資產至Dynamic Media Classic時立即發佈資產，則不需要設定任何選項。 此功能為預設行為。

不過，如果您不希望推送至Dynamic Media Classic的資產自動發佈，本節將說明如何設定Experience Manager和Dynamic Media Classic來執行此功能。

#### 將資產推送至Dynamic Media Classic取消發佈的先決條件 {#prerequisites-to-push-assets-to-scene-unpublished}

您必須先設定下列專案，才能在不發佈資產的情況下將資產推送至Dynamic Media Classic：

1. [使用Admin Console建立支援案例](https://helpx.adobe.com/tw/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)。 在您的支援案例中，要求為您的Dynamic Media Classic帳戶啟用安全預覽。
1. [為您的Dynamic Media Classic帳戶設定安全預覽](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html)。

這些步驟與您在Dynamic Media Classic中建立任何安全測試設定時所遵循的步驟相同。

#### 推送處於未發佈狀態之資產的已知限制  {#known-limitations-for-pushing-assets-in-unpublished-state}

如果您使用此功能，請注意下列限制：

* 不支援版本控制。
* 如果資產已在Experience Manager中發佈並建立後續版本，則會立即將該新版本即時發佈至生產環境。 啟動時發佈僅適用於資產的初始發佈。

>[!NOTE]
>
>如果您想要立即發佈資產，最佳實務是將&#x200B;**[!UICONTROL 啟用安全預覽]**&#x200B;設定為&#x200B;**[!UICONTROL 立即]**，並使用&#x200B;**[!UICONTROL 啟用自動上傳]**&#x200B;功能。

### 將推送至Dynamic Media Classic的資產狀態設為未發佈 {#setting-the-state-of-assets-pushed-to-scene-as-unpublished}

>[!NOTE]
>
>如果使用者在Experience Manager中發佈資產，則會自動將S7資產觸發至生產/即時資產（資產不再處於安全預覽/取消發佈狀態）。

**若要將推送至Dynamic Media Classic的資產狀態設為未發佈：**

1. 選取Experience Manager圖示並導覽至&#x200B;**[!UICONTROL 部署]** > **[!UICONTROL 雲端服務]**。
1. 選取&#x200B;**[!UICONTROL Dynamic Media Classic]**。
1. 在Dynamic Media Classic中選取您的設定。
1. 選取&#x200B;**[!UICONTROL 進階]**&#x200B;標籤。
1. 在&#x200B;**[!UICONTROL 啟用安全檢視]**&#x200B;下拉式功能表中，選取&#x200B;**[!UICONTROL AEM發佈啟動時]**&#x200B;將資產推送到Dynamic Media Classic而不發佈。 (預設情況下，此值會設為&#x200B;**[!UICONTROL 立即]**，此處會立即發佈Dynamic Media Classic資產。)

   請參閱[Dynamic Media Classic檔案](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html)，以取得公開資產前測試資產的詳細資訊。

   ![chlimage_1-302](assets/chlimage_1-302.png)

1. 選取&#x200B;**[!UICONTROL 確定]**。

啟用安全預覽表示您的資產會推送至安全預覽伺服器並取消發佈。

若要檢視&#x200B;**[!UICONTROL 安全預覽]**&#x200B;是否已啟用，請導覽至Experience Manager中某個頁面上的Dynamic Media Classic元件。 選取&#x200B;**[!UICONTROL 編輯]**。 該資產的URL中列出了安全預覽伺服器。 在Experience Manager中發佈後，檔案參考中的伺服器網域會從預覽URL更新為生產URL。

### 為WCM啟用Dynamic Media Classic {#enabling-scene-for-wcm}

出於兩個原因，需要為WCM啟用Dynamic Media Classic：

* 它會啟用通用視訊設定檔的下拉式清單，以進行頁面製作。 若沒有此清單，**[!UICONTROL 通用視訊預設集]**&#x200B;下拉式清單就會是空的，無法設定。
* 如果數位資產不在目標資料夾中，且您在頁面屬性中為該頁面啟用Dynamic Media Classic ，則可將該資產上傳至Dynamic Media Classic。 然後將資產拖放至Dynamic Media Classic元件上。 套用一般繼承規則（表示子頁面會繼承父頁面的設定）。

如其他設定一樣，為WCM啟用Dynamic Media Classic時，會套用繼承規則。 您可以在觸控最佳化或傳統使用者介面中啟用適用於WCM的Dynamic Media Classic。

#### 在觸控最佳化的使用者介面中啟用適用於WCM的Dynamic Media Classic {#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}

1. 選取Experience Manager圖示並導覽至&#x200B;**[!UICONTROL 網站]**，然後導覽至您網站的根頁面（非特定語言）。

1. 在工具列中選取[!UICONTROL 設定]圖示，然後選取&#x200B;**[!UICONTROL 開啟屬性]**。

1. 選取&#x200B;**[!UICONTROL 雲端服務]**&#x200B;並選取&#x200B;**[!UICONTROL 新增設定]**&#x200B;並選取&#x200B;**[!UICONTROL Dynamic Media Classic]**。
1. 在&#x200B;**[!UICONTROL Adobe Dynamic Media Classic]**&#x200B;下拉式清單中，選取所需的組態，然後選取&#x200B;**[!UICONTROL 確定]**。

   ![chlimage_1-303](assets/chlimage_1-303.png)

   來自該Dynamic Media Classic設定的視訊預設集可與該頁面及子頁面上的Dynamic Media Classic視訊元件搭配用於Experience Manager。

#### 在傳統使用者介面中啟用適用於WCM的Dynamic Media Classic {#enabling-scene-for-wcm-in-the-classic-user-interface}

1. 在Experience Manager中，選取&#x200B;**[!UICONTROL 網站]**&#x200B;並導覽至您網站的根頁面（非特定語言）。

1. 在Sidekick中，選取&#x200B;**[!UICONTROL 頁面]**&#x200B;圖示並選取&#x200B;**[!UICONTROL 頁面屬性]**。

1. 選取&#x200B;**[!UICONTROL 雲端服務]** > **[!UICONTROL 新增服務]** > **[!UICONTROL Dynamic Media Classic]**。
1. 在&#x200B;**[!UICONTROL Adobe Dynamic Media Classic]**&#x200B;下拉式清單中，選取所需的組態，然後選取&#x200B;**[!UICONTROL 確定]**。

   來自該Dynamic Media Classic設定的視訊預設集可與該頁面及子頁面上的Dynamic Media Classic視訊元件搭配用於Experience Manager。

### 設定預設設定 {#configuring-a-default-configuration}

如果您有多個Dynamic Media Classic設定，您可以將其中一個設定指定為Dynamic Media Classic內容瀏覽器的預設值。

在指定時刻，只能將一個Dynamic Media Classic設定標示為預設。 預設設定是預設顯示在Dynamic Media Classic內容瀏覽器中的公司資產。

**設定預設組態：**

1. 選取Experience Manager圖示並導覽至&#x200B;**[!UICONTROL 部署]** > **[!UICONTROL 雲端服務]**。
1. 選取&#x200B;**[!UICONTROL Dynamic Media Classic]**。
1. 在Dynamic Media Classic中選取您的設定。
1. 若要開啟設定，請選取&#x200B;**[!UICONTROL 編輯]**。

1. 在「**[!UICONTROL 一般]**」標籤中，選取「**[!UICONTROL 預設設定]**」核取方塊，使其成為Dynamic Media Classic內容瀏覽器中顯示的預設公司和根路徑。

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >如果只有一個組態，則選取&#x200B;**[!UICONTROL 預設組態]**&#x200B;核取方塊不會產生任何效果。

### 設定臨機資料夾 {#configuring-the-ad-hoc-folder}

當資產不在CQ目標資料夾中時，您可以設定在Dynamic Media Classic中上傳資產的隨選資料夾。 請參閱從CQ目標資料夾外部發佈資產。

**設定臨機資料夾：**

1. 選取Experience Manager圖示並導覽至&#x200B;**[!UICONTROL 部署]** > **[!UICONTROL 雲端服務]**。
1. 選取&#x200B;**[!UICONTROL Dynamic Media Classic]**。
1. 在Dynamic Media Classic中選取您的設定。
1. 若要開啟設定，請選取&#x200B;**[!UICONTROL 編輯]**。

1. 選取&#x200B;**[!UICONTROL 進階]**&#x200B;標籤。 在&#x200B;**[!UICONTROL 臨機資料夾]**&#x200B;欄位中，您可以修改&#x200B;**臨機**&#x200B;資料夾。 預設為&#x200B;**name_of_the_company/CQ5_adhoc**。

   ![chlimage_1-305](assets/chlimage_1-305.png)

### 設定通用視訊預設集 {#configuring-universal-presets}

若要設定視訊元件的通用視訊預設集，請參閱[視訊](/help/assets/s7-video.md)。

## 啟用MIME型別型Assets/Dynamic Media Classic上傳工作引數支援 {#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

您可以啟用可設定的Dynamic Media Classic上傳作業引數，這些引數是透過同步Digital Asset Manager/Dynamic Media Classic資產所觸發。

具體來說，您可以在Experience Manager Web主控台設定面板的OSGi (Open Service Gateway initiative)區域中，依MIME型別設定接受的檔案格式。 接著，您可以自訂JCR (Java™ Content Repository)中每個MIME型別使用的個別上傳工作引數。

**若要啟用MIME型別型別資產：**

1. 選取Experience Manager圖示並導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]**。
1. 在「Adobe Experience Manager Web主控台設定」面板的&#x200B;**[!UICONTROL OSGi]**&#x200B;功能表上，選取&#x200B;**[!UICONTROL 設定]**。
1. 在「名稱」欄下，尋找並選取&#x200B;**[!UICONTROL Adobe CQ Dynamic Media Classic Asset MIME型別服務]**&#x200B;以編輯設定。
1. 在「MIME型別對應」區域中，選取任何加號(+)來新增MIME型別。

   請參閱[支援的MIME型別](/help/assets/assets-formats.md#supported-mime-types)。

1. 在文字欄位中，輸入新的MIME型別名稱。

   例如，您應在`EPS=application/postscript`或`PSD=image/vnd.adobe.photoshop`中輸入`<file_extension>=<mime_type>`。

1. 在設定視窗的右下角，選取&#x200B;**[!UICONTROL 儲存]**。
1. 返回Experience Manager，然後在左側邊欄中選取&#x200B;**[!UICONTROL CRXDE Lite]**。
1. 在CRXDE Lite頁面的左側邊欄中，導覽至`/etc/cloudservices/scene7/<environment>` （將`<environment>`取代實際名稱）。
1. 展開`<environment>` （將`<environment>`取代實際名稱）以顯示`mimeTypes`節點。
1. 選取您剛才新增的mimeType。

   例如，`mimeTypes > application_postscript`或`mimeTypes > image_vnd.adobe.photoshop`。

1. 在CRXDE Lite頁面的右側，選取「**[!UICONTROL 屬性]**」標籤。
1. 在&#x200B;**[!UICONTROL jobParam]**&#x200B;值欄位中指定Dynamic Media Classic上載工作引數。

   例如，`psprocess="rasterize"&psresolution=120` 。

   如需更多您可使用的上傳工作引數，請參閱[Adobe Dynamic Media Classic Image Production System API](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-overview.html)。

   >[!NOTE]
   >
   >如果您正在上傳PSD檔案，而且想要以圖層擷取的範本形式處理這些檔案，請在&#x200B;**[!UICONTROL jobParam]**&#x200B;值欄位中輸入下列內容：
   >
   >`process=MaintainLayers&layerNaming=AppendName&createTemplate=true`
   >
   >確定您的PSD檔案有「圖層」。 如果它嚴格是一個影像或含有遮色片的影像，則會處理為影像，因為沒有要處理的圖層。

1. 在CRXDE Lite頁面的左上角，選取「**[!UICONTROL 儲存全部]**」。

## 疑難排解Dynamic Media Classic和Experience Manager整合 {#troubleshooting-scene-and-aem-integration}

如果您在整合Experience Manager與Dynamic Media Classic時遇到問題，請參閱以下解決方案案例。

**如果您的數位資產發佈至Dynamic Media Classic失敗：**

* 檢查您要上傳的資產是否位於&#x200B;**[!UICONTROL CQ目標]**&#x200B;資料夾中(您在Dynamic Media Classic雲端設定中指定此資料夾)。
* 如果沒有，您必須在該頁面的&#x200B;**[!UICONTROL 頁面屬性]**&#x200B;中設定雲端設定，以允許上傳至&#x200B;**[!UICONTROL CQ ad hoc]**&#x200B;資料夾。

* 檢查記錄檔以取得任何資訊。

**如果您的視訊預設集未出現：**

* 請確定您已透過&#x200B;**[!UICONTROL 頁面屬性]**&#x200B;設定該頁面的雲端設定。 Dynamic Media Classic視訊元件中提供視訊預設集。

**如果您的視訊資產無法在Experience Manager中播放：**

* 確定您使用正確的視訊元件。 Dynamic Media Classic視訊元件與foundation視訊元件不同。 檢視[Foundation視訊元件與Dynamic Media Classic視訊元件](/help/assets/s7-video.md)。

**如果Experience Manager中的新資產或修改的資產未自動上傳至Dynamic Media Classic：**

* 請確定資產位於CQ目標資料夾中。 系統只會自動更新CQ目標資料夾中的資產(前提是您已將Experience Manager Assets設定為自動上傳資產)。
* 確認您已將Cloud Services設定為「啟用自動上傳」，且已更新並儲存DAM資產工作流程，以包含Dynamic Media Classic上傳。
* 將影像上傳至Dynamic Media Classic目標資料夾的子資料夾時，請務必執行下列任一項作業：

   * 請確定所有資產的名稱（無論位於何處）都是唯一的。 否則，會刪除主要目標資料夾中的資產，而僅保留子資料夾中的資產。
   * 在Dynamic Media Classic帳戶的設定區域中變更Dynamic Media Classic覆寫資產的方式。 如果您在子檔案夾中使用同名資產，請勿設定Dynamic Media Classic覆寫資產，而不論位置為何。

**如果您刪除的資產或資料夾未在Dynamic Media Classic和Experience Manager之間同步：**

* 在Experience Manager Assets中刪除的Assets和資料夾仍會顯示在Dynamic Media Classic的已同步資料夾中。 手動刪除。

**如果視訊上傳失敗：**

* 如果您的視訊上傳失敗，而且您正使用Experience Manager透過Dynamic Media Classic整合來編碼視訊，請參閱[將可設定的逾時新增至Dynamic Media Classic上傳工作流程](#adding-configurable-timeout-to-scene-upload-workflow)。

>[!CAUTION]
>
>從現有的Dynamic Media Classic公司帳戶匯入資產時，可能需要花很長時間才能在Experience Manager中顯示。 請務必在Dynamic Media Classic中指定沒有太多資產的資料夾。 例如，根資料夾通常有太多資產。
>
>如果您想要測試整合，請讓根資料夾僅指向子資料夾，而不是整個公司。
