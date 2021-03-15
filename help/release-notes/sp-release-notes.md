---
title: '[!DNL Experience Manager] 6.5 Service Pack發行說明'
description: ' [!DNL Adobe Experience Manager] 6.5 service pack 8的發行說明'
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 60764db23115e7f548a82a67955331da2b858973
workflow-type: tm+mt
source-wordcount: '2812'
ht-degree: 2%

---


# [!DNL Adobe Experience Manager] 6.5 Service Pack發行說明  {#aem-service-pack-release-notes}

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.8.0 |
| 類型 | Service Pack版本 |
| 日期 | 2021 年 3 月 11 日 |
| 下載URL | [軟體散發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip) |

<!-- TBD: Update the SD link when SP8 is available. Same link is duplicated below in install -->

## [!DNL Adobe Experience Manager] 6.5.8.0 {#what-s-included-in-aem}中包含的內容

[!DNL Adobe Experience Manager] 6.5.8.0包含自2019年4月6.5版發行以來發行的新功能、客戶要求的重要增強功能，以及效能、穩定性和安全性增強功能。[!DNL Adobe Experience Manager] 6.5上安裝了Service Pack。

[!DNL Adobe Experience Manager] 6.5.8.0中引入的主要功能和增強功能包括：

<!-- TBD:
* Using the Connected Assets functionality, it is now possible to connect up to 3 [!DNL Sites] instances with 1 [!DNL Assets] instances. The configuration user interface now allows the administrators to provide the details of these [!DNL Sites] instances. -->

* 使用[連接的資產功能](/help/assets/use-assets-across-connected-assets-instances.md)時，您現在可以檢視使用資產的所有[!DNL Sites]頁面的清單。 資產的[!UICONTROL 屬性]頁面提供這些資產參考。 這可讓管理員、行銷人員和圖書管理員全面瞭解資產使用情況，進而提高追蹤、管理和品牌一致性。

* 刪除網頁中參考的資產時，[!DNL Experience Manager] [會顯示警告](/help/assets/use-assets-across-connected-assets-instances.md#asset-usage-references)。 您可以強制刪除引用的資產，或檢查並修改顯示在資產[!DNL Properties]頁面中的引用。 按一下參照可開啟本地和遠程[!DNL Sites]頁。

* 使用[!UICONTROL Name]、[!UICONTROL 上次修改日期、]和[!UICONTROL 上次轉出日期]屬性，對可開始的即時副本頁面排序。

* 內建儲存庫(Apache Jackrabbit Oak)已更新為1.22.6。<!-- TBD: Mention the version -->

如需[!DNL Experience Manager] 6.5.8.0中推出的完整功能與增強功能清單，請參閱 [!DNL Adobe Experience Manager]  6.5 Service Pack 8](new-features-latest-service-pack.md)中的新增功能。[

以下是[!DNL Experience Manager] 6.5.8.0版中提供的修正清單。

### [!DNL Sites] {#sites-6580}

* 當頁面移至Blueprint時，不會更新連結的目的地(NPR-35724)。
* Tizen型播放器無法在特定瀏覽器上驗證。 不支援samesite=none屬性的瀏覽器發生問題(NPR-35589)。
* 解除鎖定的回應式容器不會顯示允許的元件(NPR-35565)。
* 當您建立新增頁面的即時副本時，語言主版會為每個網域建立兩個副本(NPR-35545)。
* 當由於`org.apache.felix.scr.impl.ComponentRegistry`計時器而阻止多個線程時，SCR元件註冊表中的死鎖。 因此，[!DNL Experience Manager]會無限期停止響應(GRANITE-33125,FELIX-6252)。
* 當您在側欄中搜尋特定資產時，結果會包含一些未搜尋的資產(NPR-35524)。
* 為Experience Manager實例啟用SSL時，會刪除上下文路徑(NPR-35477)。
* 當您建立清單、新增一些文字作為第一個元素、新增表格作為第二個元素，以及新增表格內的清單時，父清單會扭曲(NPR-35465)。
* 當您在連續的清單項目上使用不同的外掛程式時，會新增額外的<br>標籤至清單項目(NPR-35464)。
* 在兩段之間放置清單時，不能將表添加到清單(NPR-35356)。
* 當您開始從AEM6.3升級至AEM6.5AEM的執行個體時，升級執行個體的啟動時間會較長(NPR-35323)。
* 複製包含括AEM括弧()的資產時。 在名稱中，複製失敗(GRANITE-27004、NPR-35315)。
* 將標題添加到富格文本編輯器時，段落按鈕被禁用(NPR-35256)。
* 將項目添加到現有清單時，它將刪除後續的可折疊或切換清單(NPR-35206)。
* 當選取「轉出頁面」選項時，會出現一個對話方塊，其中包含所有可用的即時副本，並自動轉出。 頁面的即時副本可發佈至所有地區，而不需使用者動作(NPR-35138)。
* 使用包含子項選項時，「管理出版物」選項不會列出所有頁面。 僅列出22頁(NPR-35086)。
* 編輯策略時，文本元件不保留策略更改(NPR-35070)。
* 在編號清單中縮進某些項目時，所有項目的編號都保持相同，但對於具有相同縮進的項目，編號應從1開始(CQ-4313011)。
* 啟用精簡功能時，您無法編輯任何頁面或元件。 問題在安裝AEM6.5 Service Pack 7(CQ-4311133)後開始。
* Omni搜尋和資產篩選器會傳回不相關或無結果(CQ-4312322、NPR-35793)。
* 當多個頁面同時存取用戶端程式庫時，HTML程式庫管理員無法載入用戶端程式庫。 這會導致頁面呈現不正確(NPR-35538)。
* 當您在[!DNL Experience Manager]中設定SSL時，內容路徑會自動移除(NPR-35294)。
* 在按一下「註銷」選項後，包管理器不會註銷用戶(NPR-35160)。

### [!DNL Assets] {#assets-6580}

[!DNL Adobe Experience Manager] 6.5.8.0修正 [!DNL Assets] 下列問題，並提供下列增強功能。

* 在還原舊版資產時，OSGi主控台不會觸發事件DamEvent.Type RESTORED(NPR-35789)。
* `IndexWriter.merge` 由於 `OutOfMemoryError` 智慧標籤功能會建立大 `/oak:index/lucene` 型 `/oak:index/ntBaseLucene` 和索引(NPR-35651)，因此會導致錯誤。
* 嘗試儲存[!UICONTROL 資產貢獻]類型資料夾時，會顯示錯誤訊息(NPR-35605)。
* 使用階層式中繼資料子類型欄位時，會發生錯誤的「請填寫此欄位」錯誤(NPR-35643)。
* 當在[!DNL Assets]使用者介面上拖曳現有資產並建立新版本時，中繼資料中的變更不會持續(NPR-34940)。
* 在階層式選單的中繼資料結構編輯器中建立規則時，[!UICONTROL 依存於]選項會重複相同的名稱(NPR-35596)。
* 編輯[!UICONTROL 資產管理搜尋邊欄]後，相似性搜尋無法運作(NPR-35588)。
* 從資料夾中，如果您按一下「[!UICONTROL 篩選器]」開啟左側導軌中的資產搜尋，則「[!UICONTROL 狀態] > [!UICONTROL 結帳] > [!UICONTROL 結帳]」中的篩選器將無法運作(NPR-35530)。
* 如果您嘗試刪除資產的所有智慧型標籤並儲存變更，則不會移除標籤。 不過，使用者介面會指出已儲存變更(NPR-35519)。
* 使用者無法在清單檢視中重新排列或排序可訂購的資料夾中的資產(NPR-35516)。
* 如果您編輯預設中繼資料結構，資產的[!UICONTROL 屬性]頁面中的標籤欄位會變更為文字欄位。 這項變更可讓不知情的使用者新增隨選標籤，而標籤會儲存為儲存庫中的字串(NPR-35478)。
* 下載資產時，如果您提供的名稱沒有有效的電子郵件地址，則無法使用下載選項。 不過，如果選取下載對話方塊中的其他選項，則會啟用按鈕，但不會傳送電子郵件(NPR-35365)。
* 使用者在編輯[!DNL Adobe InDesign]中的資產後無法登入資產，並收到有關缺乏權限的錯誤(NPR-35341)。
* Handlebars JavaScript程式庫已升級至v4.7.6(NPR-35333)。
* 當您從大量中繼資料編輯開始並取消選取項目時，中繼資料編輯器介面會停止正常運作，直到選取單一項目為止(NPR-35144)。
* 從`assets.html`頁面按一下全域導覽時，無法開啟正確的主控台(CQ-4312311)。
* [!DNL Assets] 不會針對具有RGB轉譯的資產顯示RGB轉譯(CQ-4310190)。
* 菜單中的[!UICONTROL Relate]選項未在[!UICONTROL Properties]頁中正確顯示(CQ-4310188)。
* 如果檔案的檔案類型篩選器用於搜尋資產並建立智慧型系列，則在存取系列時不會套用篩選器。 相反，所有類型的資產都顯示在搜索中(NPR-35759)。
* 您無法從[!DNL Assets]使用者介面(NPR-35901)將資產拖曳並新增至燈箱。
* 在解決命名衝突後建立新版本的現有資產時，會覆寫原始資產的中繼資料(CQ-4313594)。
* 當您使用搜尋篩選器或謂詞篩選資產搜尋時，開啟資產以檢視或編輯資產，然後返回搜尋結果頁面，篩選器將無法運作。 所有搜尋的資產都會列在未篩選的清單中(NPR-35913)。

#### [!DNL Dynamic Media] {#dynamic-media-6580}

* 資產詳細資訊頁面上會啟用RESS影像預設集的URL選項。 現在，當在動態轉譯區段中選取RESS影像預設集時，資產詳細資料頁面上會提供URL和RESS選項。 (CQ-4311241)
* 互動式媒體元件——如果使用者具有選擇性發佈設定的[!DNL Experience Manager]，互動式視訊將無法運作(CQ-4311054)。
* 如果您跨資料夾移動資產，透過API在[!DNL Experience Manager]和[!DNL Dynamic Media–Scene7]之間的同步速度會非常慢(CQ-4310001)。
* 使用Omnisearch時，記錄檔大小會顯著增加(CQ-4309153)。
* 當啟用選擇性同步且資產複製（未移動）至同步資料夾時，它不會如預期同步(CQ-4307122)。
* 對於自動發佈至DM的已上傳資產，狀態不會顯示於AEM。 此外，「Dynamic Media發佈」狀態欄不會顯示正確的發佈狀態(CQ-4306415)。
* 如果資產發佈在[!DNL Experience Manager]上，並設定在啟動時發佈到[!DNL Dynamic Media]，則`scene7FileStatus`中繼資料值不會如預期般更新(CQ-4308269)。
* 編輯視訊設定檔時，[!DNL Experience Manager]不會顯示視訊預設集的高度和位元速率值設定。 欄位會顯示為空白(CQ-4311828)。

### [!DNL Commerce] {#commerce-6580}

* 無法為商務中的所有產品建立自訂標籤(CQ-4310682)。

* 產品資產參考更新導致複製線程處於等待狀態，直到ProductAssetListener線程完成對JCR的提交(NPR-35269)。

### 平台 {#platform-6580}

* 當您使用沒有標籤的Coral Tab View元件並觸發Foundation驗證器時，會發生下列錯誤(NPR-35636):

   ```TXT
    Uncaught TypeError: Cannot set property 'invalid' of undefined
     at enable (foundation.js:10703)
     at foundation.js:10710
   ```

* SCD轉發複製對於名稱中包含逗號的節點的刪除事件失敗(NPR-35191)。

* 升級至AEM6.5.7後，組建會開始失敗。 原因是，uber-jar中嵌入了舊版或沒有jackson-core(GRANITE-33006)。

### 使用者介面{#ui-6580}

* 當您在「資產」主控台的檔案夾中，從「卡片檢視」切換為「清單檢視」時，排序無法正常運作(NPR-35842)。

* 當您超連結文字元件中的文字時，搜尋功能不會顯示適當的結果(NPR-35849)。

* 當未將值提供給標籤為必需的隱藏欄位時，它會阻止您保存元件(NPR-35219)。

### Integrations {#integrations-6580}

* 當您對IMS租用戶ID和目標用戶端代碼使用不同的值時，[!DNL Experience Manager]無法與[!DNL Adobe Target]整合(NPR-35342)。

### 翻譯項目{#translation-6580}

* 在[!DNL Experience Manager]中導出或導入翻譯作業時出現的問題(NPR-35259)。

### 行銷活動 {#campaign-6580}

* 當您使用Touch UI中的現成範本建立促銷活動頁面，並在頁面屬性對話方塊中開啟「電子郵件」標籤時，主旨和內文欄位的個人化變數仍會停用(CQ-4312388)。

### [!DNL Communities] {#communities-6580}

* 在將頁面結構新增至社群群組時，階層連結中的[!UICONTROL 群組]標題會變更為第一個[!UICONTROL 頁面]的標題(NPR-35803)。
* 與協調者不同，標準社群成員無法存取和編輯任何草稿貼文(NPR-35339)。
* 使用DSRPReindexServlet中斷存取控制和拒絕服務，將社群網站拖曳至索引完成(NPR-35591)。
* 從[!UICONTROL 管理員]欄位移除[!UICONTROL 所有使用者]並不會實際從後端移除他們(NPR-35592、NPR-35611)。
* 當輸入的文本是部分匹配時，[!UICONTROL 合成消息]元件不會返回任何結果(NPR-35666)。

### [!DNL Brand Portal] {#brandportal-6580}

* 將成員添加到[!UICONTROL Asset Contribution]類型資料夾會在用戶介面中顯示[!UICONTROL 添加用戶或組]標題，儘管只支援品牌門戶活動用戶，而不支援組(NPR-35332)。

### [!DNL Forms] {#forms-6580}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 會在排程的[!DNL Experience Manager] Service Pack 發行日期一週後發行附加元件的套件。

如需安全性更新的詳細資訊，請參閱[Experience Manager安全性公告頁面](https://helpx.adobe.com/security/products/experience-manager.html)。

## 安裝6.5.8.0 {#install}

**設定需求和詳細資訊**

* Experience Manager6.5.8.0需要第6.5號Experience Manager。請參閱[升級檔案](/help/sites-deploying/upgrade.md)以取得詳細指示。
* Service Pack下載可在[軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)Adobe上獲得。
* 在使用MongoDB和多個實例的部署中，使用包管理器將6.5.8.0Experience Manager安裝在其中一個「作者」實例上。

>[!NOTE]
>
>Adobe不建議刪除或卸載[!DNL Adobe Experience Manager] 6.5.8.0軟體包。

### 安裝Service Pack {#install-service-pack}

要在[!DNL Adobe Experience Manager] 6.5實例上安裝Service Pack，請執行以下步驟：

1. 如果實例處於更新模式，則在安裝之前重新啟動實例（在從舊版更新實例時也是如此）。 Adobe還建議在實例的當前正常運行時間較長時重新啟動。

1. 在安裝之前，請為[!DNL Experience Manager]實例建立快照或新備份。

1. 從[軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip)下載服務包。

1. 開啟套件管理器，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。如需詳細資訊，請參閱[Package Manager](/help/sites-administering/package-manager.md)。

1. 選擇軟體包並按一下&#x200B;**[!UICONTROL Install]**。

1. 要更新S3連接器，請在安裝Service Pack後停止實例，用安裝資料夾中提供的新二進位檔案替換現有連接器，然後重新啟動實例。 請參閱[AmazonS3資料儲存](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)。

>[!NOTE]
>
>在安裝Service Pack時，有時會退出Package Manager UI的對話方塊。 Adobe建議您先等待錯誤記錄穩定，再存取部署。 請等待與解除安裝更新程式套件相關的特定記錄，然後確定安裝成功。 通常，這會發生在[!DNL Safari]上，但是在任何瀏覽器上都會偶爾發生。

**自動安裝**

在工作實例上自動安裝Adobe Experience Manager6.5.8.0有兩種方法：

答：當伺服器聯機時，將軟體包放入`../crx-quickstart/install`資料夾。 軟體包會自動安裝。

B.使用「套件管理員」的[HTTP API](/help/sites-administering/package-manager.md#package-share)。 使用`cmd=install&recursive=true`以安裝嵌套的軟體包。

>[!NOTE]
>
>Adobe Experience Manager6.5.8.0不支援安裝Bootstrap。

**驗證安裝**

1. 產品資訊頁面(`/system/console/productinfo`)在[!UICONTROL 安裝的產品]下顯示更新的版本字串`Adobe Experience Manager (6.5.8.0)`。

1. 所有OSGi捆綁包在OSGi控制台中都是&#x200B;**[!UICONTROL ACTIVE]**&#x200B;或&#x200B;**[!UICONTROL FRAGMENT]**(使用Web控制台：`/system/console/bundles`)。

1. OSGi bundle `org.apache.jackrabbit.oak-core`是1.22.3版或更新版本(使用Web Console:`/system/console/bundles`)。

要瞭解經認證可與此版本一起使用的平台，請參閱[技術要求](/help/sites-deploying/technical-requirements.md)。

### UberJar {#uber-jar}

[Maven Central儲存庫](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.8/)中提供了用於6.5.8.0Experience Manager的UberJar。

要在Maven項目中使用UberJar，請參閱[如何使用UberJar](/help/sites-developing/ht-projects-maven.md)並在項目POM中包括以下相關性：

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.8</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar和其他相關對象可在Maven Central Repository中使用，而不是AdobePublic Maven儲存庫(`repo.adobe.com`)。 主UberJar檔案更名為`uber-jar-<version>.jar`。 因此，`dependency`標籤沒有`classifier`,`apis`值。

## 過時的功能 {#removed-deprecated-features}

以下是已標示為已過時的[!DNL Experience Manager] 6.5.7.0功能清單。功能已標示為不建議使用，未來版本會先移除。 通常會提供替代選項。

檢視您在部署中是否使用功能。 此外，您也打算將實施變更為使用替代選項。

| 區域 | 功能 | 替代方案 |
|---|---|---|
| Integrations | **[!UICONTROL AEM Cloud Services Opt-In]**&#x200B;畫面已過時。 隨著Experience Manager與Adobe Target的整合在Experience Manager6.5中更新，以支援Adobe Target標準API(透過AdobeIMS和I/O使用驗證)，以及Adobe啟動在分析與個人化Experience Manager頁面檢測方面的作用日益增強，選擇加入精靈在功能上已變得無關緊要。 | 透過各自的Adobe雲端服務，設定系統連線、Experience ManagerIMS驗證和[!DNL Adobe I/O]整合。 |
| 連接器 | 針對Microsoft SharePoint 2010和Microsoft SharePoint 2013的AdobeJCR Connector已不適用於Experience Manager6.5。 | N/A |

## 已知問題 {#known-issues}

* 如果您要將[!DNL Experience Manager]實例從6.5升級到6.5.8.0版，則可以在`error.log`檔案中查看`RRD4JReporter`異常。 重新啟動實例以解決問題。

* 如果您在[!DNL Experience Manager] 6.5上安裝[!DNL Experience Manager] 6.5 Service Pack 5或之前的Service Pack，則會刪除資產自訂工作流程模型（在`/var/workflow/models/dam`中建立）的執行時期副本。
若要擷取您的執行時期副本，Adobe建議使用HTTP API，將自訂工作流程模型的設計時副本與其執行時期副本同步化：
   `<designModelPath>/jcr:content.generate.json`。

* 如果您在使用[!UICONTROL 定義規則]對話方塊的[!UICONTROL 資料夾中繼資料結構Forms編輯器]和[!UICONTROL 中繼資料結構Forms編輯器]中編輯和建立階層式規則時遇到問題，請連絡Adobe客戶服務。 已建立和儲存的規則會如預期般運作。

* 如果階層中的檔案夾在[!DNL Experience Manager Assets]中重新命名，且包含資產的巢狀檔案夾已發佈至[!DNL Brand Portal]，則在[!DNL Brand Portal]中不會更新檔案夾的標題，直到重新發佈根檔案夾為止。

* 當使用者第一次選擇以最適化表單來設定欄位時，儲存設定的選項不會顯示在「屬性瀏覽器」中。 在相同編輯器中選取以設定最適化表單的其他欄位，可解決此問題。

* 如果[!UICONTROL Connected assets configuration]嚮導在安裝後返回404錯誤消息，請使用包管理器手動重新安裝`cq-remotedam-client-ui-content`和`cq-remotedam-client-ui-components`包。

* 在安裝6.5.x.xExperience Manager時，可能會顯示以下錯誤和警告消息：
   * 「當使用Target Standard API（IMS驗證）在Experience Manager中設定Adobe Target整合時，將體驗片段匯出至Target會導致建立錯誤的選件類型。 Target會建立數個選件，而非「體驗片段」/來源「Adobe Experience Manager」，其類型為「HTML」/來源「Adobe Target經典」。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`:在granite/operations/maintenance中找不到維護視窗。
   * 當使用SUM、MAX和MIN等集合函式時，Adaptive Form伺服器端驗證將失敗。 CQ-4274424
   * `com.adobe.granite.maintenance.impl.TaskScheduler` -在granite/operations/maintenance中找不到維護視窗。
   * 透過可購買橫幅檢視器預覽資產時，Dynamic Media互動式影像中的熱點不可見。

## 包含{#osgi-bundles-and-content-packages-included}的OSGi捆綁包和內容包

以下文本文檔列出[!DNL Experience Manager] 6.5.8.0中包含的OSGi組合和內容包：

* [6.5.8.0Experience Manager中包含的OSGi捆綁包清單](assets/6580_bundles.txt)

* [6.5.8.0Experience Manager中包含的內容包清單](assets/6580_packages.txt)

## 受限制的網站{#restricted-sites}

這些網站僅提供給客戶使用。 如果您是客戶，需要存取權，請連絡您的Adobe客戶經理。

* [產品下載，請造訪licensing.adobe.com](https://licensing.adobe.com/)
* 請參閱[如何聯絡Adobe客戶服務](https://experienceleague.adobe.com/docs/customer-one/using/home.html)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5發行說明](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] 產品頁面](https://www.adobe.com/tw/marketing/experience-manager.html)
>* [[!DNL Experience Manager] 6.5檔案](https://experienceleague.adobe.com/docs/experience-manager-65.html)
>* [訂閱 Adobe 優先產品更新](https://www.adobe.com/subscription/priority-product-update.html)

