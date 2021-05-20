---
title: '[!DNL Experience Manager] 6.5 service pack發行說明'
description: ' [!DNL Adobe Experience Manager] 6.5 service pack 8的發行說明'
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: 024f03c04a980c544ac59e736caeaa24f7565582
workflow-type: tm+mt
source-wordcount: '3409'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager] 6.5 service pack發行說明  {#aem-service-pack-release-notes}

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.8.0 |
| 類型 | Service Pack發行 |
| 日期 | 2021 年 3 月 11 日 |
| 下載URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip) |

<!-- TBD: Update the SD link when SP8 is available. Same link is duplicated below in install -->

## [!DNL Adobe Experience Manager] 6.5.8.0 {#what-s-included-in-aem}中包含的內容

[!DNL Adobe Experience Manager] 6.5.8.0包含自2019年4月發行6.5版以來所推出的新功能、客戶要求的重要增強功能，以及效能、穩定性和安全性等改善項目。Service Pack安裝在[!DNL Adobe Experience Manager] 6.5上。

[!DNL Adobe Experience Manager] 6.5.8.0中引入的主要功能和增強包括：

<!-- TBD:
* Using the Connected Assets functionality, it is now possible to connect up to 3 [!DNL Sites] instances with 1 [!DNL Assets] instances. The configuration user interface now allows the administrators to provide the details of these [!DNL Sites] instances. -->

* 使用[連線資產功能](/help/assets/use-assets-across-connected-assets-instances.md)時，您現在可以檢視使用資產的所有[!DNL Sites]頁面清單。 資產的[!UICONTROL 屬性]頁面會提供這些資產參考。 這可讓管理員、行銷人員和圖書館員全面了解資產使用情形，進而提供更佳的追蹤、管理和品牌一致性。

* 刪除網頁中參考的資產時， [!DNL Experience Manager] [會顯示警告](/help/assets/use-assets-across-connected-assets-instances.md#asset-usage-references)。 您可以強制刪除參照的資產，或檢查並修改顯示在資產[!DNL Properties]頁面中的參照。 按一下參照會開啟本機和遠端[!DNL Sites]頁面。

* 使用[!UICONTROL Name]、[!UICONTROL Last modified date,]和[!UICONTROL Last roult date]屬性排序可轉出的Live Copy頁面。

* 內建存放庫(Apache Jackrabbit Oak)更新至1.22.6。<!-- TBD: Mention the version -->

如需[!DNL Experience Manager] 6.5.8.0中推出的完整功能和增強功能清單，請參閱[ [!DNL Adobe Experience Manager]  6.5 Service Pack 8](new-features-latest-service-pack.md)中的新功能。

以下是[!DNL Experience Manager] 6.5.8.0版本中提供的修正清單。

### [!DNL Sites] {#sites-6580}

* 將頁面移至Blueprint時，連結的目的地不會更新(NPR-35724)。
* 基於Tizen的播放器無法在某些瀏覽器上驗證。 不支援samesite=none屬性的瀏覽器發生問題(NPR-35589)。
* 未鎖定的回應式容器未顯示允許的元件(NPR-35565)。
* 當您建立新增頁面的即時副本時，語言主版會為每個網域建立兩個副本(NPR-35545)。
* 由於`org.apache.felix.scr.impl.ComponentRegistry`計時器而阻止許多線程時，SCR元件註冊表中的死鎖。 因此，[!DNL Experience Manager]會無限期停止回應(GRANITE-33125、FELIX-6252)。
* 在側邊欄中搜尋特定資產時，結果會包含一些未搜尋的資產(NPR-35524)。
* 為Experience Manager例項啟用SSL時，內容路徑已移除(NPR-35477)。
* 建立清單時，新增一些文字作為第一個元素、新增表格作為第二個元素，以及在表格內新增清單，父清單會扭曲(NPR-35465)。
* 在連續的清單項目上使用不同的外掛程式時，額外的<br>標籤會新增至清單項目(NPR-35464)。
* 在兩段之間放置清單時，無法將表格新增至清單(NPR-35356)。
* 當您開始從AEM 6.3升級至AEM 6.5的AEM執行個體時，升級執行個體需要較長的時間才能開始(NPR-35323)。
* 複製包含括弧()的AEM資產時。 在名稱中，復寫會失敗(GRANITE-27004、NPR-35315)。
* 在RTF編輯器中新增標題時，段落按鈕遭到停用(NPR-35256)。
* 將項目新增至現有清單時，它會刪除後續的可折疊或切換清單(NPR-35206)。
* 選取轉出頁面選項時，會出現一個對話方塊，其中包含所有可用的即時副本，並自動轉出。 頁面的即時副本會推出至所有地理位置，不需使用者動作(NPR-35138)。
* 使用包含子項選項時，「管理出版物」選項不會列出所有頁面。 僅列出22頁(NPR-35086)。
* 編輯原則時，文字元件不會保留原則變更(NPR-35070)。
* 在編號清單中縮進某些項目時，所有項目都會保持相同的編號，但具有相同縮進的項目的編號應從1開始(CQ-4313011)。
* 啟用縮制時，您無法編輯任何頁面或元件。 安裝AEM 6.5 Service Pack 7後開始出現問題(CQ-4311133)。
* 全方位搜尋和資產篩選器會傳回不相關或沒有結果(CQ-4312322、NPR-35793)。
* 當多個頁面同時存取用戶端程式庫時，HTML程式庫管理員無法載入用戶端程式庫。 這會導致不正確的頁面轉譯(NPR-35538)。
* 在[!DNL Experience Manager]中設定SSL時，內容路徑會自動移除(NPR-35294)。
* 封裝管理員在按一下「登出」選項後沒有登出使用者(NPR-35160)。

### [!DNL Assets] {#assets-6580}

[!DNL Adobe Experience Manager] 6.5.8.0修正 [!DNL Assets] 下列問題，並提供下列增強功能。

* 還原舊版資產時，OSGi主控台不會觸發事件DamEvent.Type RESTORED(NPR-35789)。
* `IndexWriter.merge` 造 `OutOfMemoryError` 成錯誤，因為智慧標籤功能會 `/oak:index/lucene` 建 `/oak:index/ntBaseLucene` 立大型和索引(NPR-35651)。
* 嘗試儲存[!UICONTROL 資產貢獻]類型資料夾時，名稱中含有多位元組字元時，會顯示錯誤訊息(NPR-35605)。
* 使用階層式中繼資料子類型欄位時，發生錯誤的「請填寫此欄位」錯誤(NPR-35643)。
* 在[!DNL Assets]使用者介面上拖曳現有資產並建立新版本時，中繼資料中的變更不會持續存在(NPR-34940)。
* 在階層式功能表的中繼資料結構編輯器中建立規則時，[!UICONTROL 相依於]選項會重複相同的名稱(NPR-35596)。
* 編輯[!UICONTROL Assets管理搜尋邊欄]後，相似性搜尋沒有作用(NPR-35588)。
* 在資料夾內，如果您按一下[!UICONTROL Filter]開啟左側邊欄中的資產搜尋， [!UICONTROL Status] > [!UICONTROL Checkout] > [!UICONTROL Checkout]中的篩選器無法運作(NPR-35530)。
* 如果您嘗試刪除資產的所有智慧標籤並儲存變更，則不會移除標籤。 不過，使用者介面會指出已儲存變更(NPR-35519)。
* 使用者無法重新排列或排序可排序資料夾中清單檢視中的資產(NPR-35516)。
* 如果您編輯預設中繼資料結構，資產的[!UICONTROL 屬性]頁面中的標籤欄位會變更為文字欄位。 這項變更可讓不知情的使用者新增隨選標籤，且標籤會儲存為存放庫中的字串(NPR-35478)。
* 下載資產時，如果您提供的名稱沒有有效的電子郵件地址，則下載選項無法使用。 不過，如果選取下載對話方塊中的其他選項，按鈕會啟用，但不會傳送電子郵件(NPR-35365)。
* 在[!DNL Adobe InDesign]中編輯資產後，使用者無法簽入資產，並收到關於缺少權限的錯誤(NPR-35341)。
* Handlebars JavaScript程式庫已升級至v4.7.6(NPR-35333)。
* 從大量中繼資料編輯開始並取消選取項目時，中繼資料編輯器介面會停止正常運作，直到仍選取單一項目為止(NPR-35144)。
* 從`assets.html`頁面內按一下時，全域導覽無法開啟正確的主控台(CQ-4312311)。
* [!DNL Assets] 不會針對具有RGB轉譯的資產顯示RGB轉譯(CQ-4310190)。
* 功能表中的[!UICONTROL Relate]選項未正確顯示在[!UICONTROL Properties]頁面(CQ-4310188)中。
* 如果使用檔案的檔案類型篩選器來搜尋資產和建立智慧型集合，則存取集合時不會套用篩選器。 而是在搜尋中顯示所有類型的資產(NPR-35759)。
* 您無法從[!DNL Assets]使用者介面拖曳並新增Lightbox中的資產(NPR-35901)。
* 解決命名衝突後建立新版本的現有資產時，會覆寫原始資產的中繼資料(CQ-4313594)。
* 使用搜尋篩選器或述詞篩選資產搜尋時，請開啟資產以檢視或編輯資產，然後返回搜尋結果頁面，篩選器無法運作。 所有搜尋的資產都會未篩選列出(NPR-35913)。

#### [!DNL Dynamic Media] {#dynamic-media-6580}

* RESS影像預設集的URL選項會在資產詳細資訊頁面上啟用。 現在，當在動態轉譯區段中選取RESS影像預設集時，URL和RESS選項都可在資產詳細資訊頁面上使用。 (CQ-4311241)
* 互動式媒體元件 — 如果使用者具有選擇性發佈設定的[!DNL Experience Manager](CQ-4311054)，互動式視訊將無法運作。
* 如果您跨資料夾移動資產，透過API在[!DNL Experience Manager]和[!DNL Dynamic Media–Scene7]之間的同步速度會很慢(CQ-4310001)。
* 使用Omnisearch時，記錄檔的大小會顯著增加(CQ-4309153)。
* 啟用選擇性同步且資產複製（未移動）至同步資料夾時，不會如預期同步(CQ-4307122)。
* 對於自動發佈至DM的已上傳資產，狀態不會顯示在AEM上。 此外，Dynamic Media發佈狀態欄未顯示正確的發佈狀態(CQ-4306415)。
* 如果資產發佈於[!DNL Experience Manager]，且設為在啟用時發佈至[!DNL Dynamic Media],`scene7FileStatus`中繼資料值不會如預期更新(CQ-4308269)。
* 編輯視訊設定檔時，[!DNL Experience Manager]不會顯示為視訊預設集設定的高度和位元速率值。 欄位會顯示為空白(CQ-4311828)。

### [!DNL Commerce] {#commerce-6580}

* 無法為商務中的所有產品建立自訂標籤(CQ-4310682)。

* 產品資產參考更新會導致復寫執行緒處於等候狀態，直到ProductAssetListener執行緒完成對JCR的提交為止(NPR-35269)。

### 平台 {#platform-6580}

* 使用沒有標籤的Coral Tab檢視元件並觸發Foundation驗證器時，會發生下列錯誤(NPR-35636):

   ```TXT
    Uncaught TypeError: Cannot set property 'invalid' of undefined
     at enable (foundation.js:10703)
     at foundation.js:10710
   ```

* 對於名稱中包含逗號的節點，SCD轉發復寫無法刪除事件(NPR-35191)。

* 升級至AEM 6.5.7後，組建會開始失敗。 原因是，uber-jar中內嵌舊版或未內嵌jackson-core(GRANITE-33006)。

### 使用者介面{#ui-6580}

* 在Assets控制台中，從卡片檢視切換為資料夾中檔案的清單檢視時，排序無法正常運作(NPR-35842)。

* 當您超連結文字元件中的文字時，搜尋功能沒有顯示適當的結果(NPR-35849)。

* 未將值提供給標示為必要的隱藏欄位時，會阻擋您儲存元件(NPR-35219)。

### Integrations {#integrations-6580}

* 當您對IMS租用戶ID和Target用戶端代碼使用不同的值時，[!DNL Experience Manager]無法與[!DNL Adobe Target]整合(NPR-35342)。

### 翻譯專案{#translation-6580}

* 在[!DNL Experience Manager]中匯出或匯入翻譯工作時發生問題(NPR-35259)。

### 行銷活動 {#campaign-6580}

* 當您使用觸控式UI中的現成可用範本建立促銷活動頁面，並在頁面屬性對話方塊上開啟「電子郵件」標籤時，主旨和內文欄位的個人化變數仍為停用狀態(CQ-4312388)。

### [!DNL Communities] {#communities-6580}

* 將頁面結構新增至社群群組時，階層連結中的[!UICONTROL 群組]標題會變更為第一個[!UICONTROL 頁面]的標題(NPR-35803)。
* 與協調者不同，標準社群成員無法存取和編輯任何草稿貼文(NPR-35339)。
* `DSRPReindexServlet`的存取控制和拒絕服務中斷，導致Communities網站癱瘓，直到索引完成(NPR-35591)。
* 從[!UICONTROL Administrators]欄位移除[!UICONTROL All Users]實際上並未從後端移除(NPR-35592、NPR-35611)。
* 當輸入的文字部分相符時，[!UICONTROL 撰寫訊息]元件沒有傳回任何結果(NPR-35666)。

* 嘗試借由選取&#x200B;**[!UICONTROL 新增標籤]**&#x200B;來將標籤新增至新部落格時，您可能會注意到效能受到某些影響和速度緩慢。 若要改善效能，請安裝[cqTagLucene-0.0.1.zip hotfix](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/cqTagLucene-0.0.1.zip)。

### [!DNL Brand Portal] {#brandportal-6580}

* 將成員新增至[!UICONTROL Asset Contribution]類型資料夾會在使用者介面中顯示[!UICONTROL Add User or Group]註解，不過僅支援Brand Portal作用中使用者，不支援群組(NPR-35332)。

### [!DNL Forms] {#forms-6580}

>[!NOTE]
>
>[!DNL Experience Manager Forms] 會在排程的 [!DNL Experience Manager] Service Pack 發行日期一週後發行附加元件的套件。

**調適型表單**

* 將具有可重複列的表格插入具有適用性表單中多個例項的可重複面板時，表格一律會新增至面板的第一個例項(NPR-35635)。

* 在以最適化表單成功驗證CAPTCHA元件後，當標籤焦點再次抵達CAPTCHA元件時，[!DNL Experience Manager Forms]會顯示`Provide Captcha phrase to proceed`錯誤訊息(NPR-35539)。

**互動式通訊**

* 提交翻譯的表單時，提交消息顯示為英文，不翻譯為適當的語言(NPR-35808)。

* 在附加的XDP或檔案片段中加入隱藏條件時，互動式通訊無法載入(NPR-35745)。

**通信管理**

* 編輯信函時，含有條件的模組需要較長的載入時間(NPR-35325)。

* 當您從左側導覽窗格中選取未包含在信函中的資產，然後選取下一個資產時，系統不會從先前選取的資產中移除藍色醒目提示(NPR-35851)。

* 編輯信函中的文字欄位時，[!DNL Experience Manager Forms]會顯示`Text Edit Failed`錯誤訊息(CQ-4313770)。

**工作流程**

* 當您嘗試在適用於iOS的[!DNL Experience Manager Forms]行動應用程式上開啟最適化表單時，應用程式會停止回應(CQ-4314825)。

* HTML工作區中的[!UICONTROL To-do]標籤會顯示HTML字元(NPR-35298)。

**XMLFM**

* 使用輸出服務生成XML文檔時，某些XML檔案(CQ-4311341、CQ-4313893)會出現`OutputServiceException`錯誤。

* 將上標屬性套用至項目符號的第一個字元時，項目符號的大小會變小(CQ-4306476)。

* 使用輸出服務產生的PDF forms不包含邊框(CQ-4312564)。

**設計工具**

* 在[!DNL Experience Manager Forms] Designer中開啟XDP檔案時，將在與XDP檔案(CQ-4309427、CQ-4310865)相同的資料夾中產生designer.log檔案。

**HTML5 表單**

* 當您在[!DNL Safari]網頁瀏覽器[!DNL iOS 14.1 or 14.2]中選取適用性表單的核取方塊時，不會顯示其他欄位(NPR-35652)。

**Forms管理**

* 沒有確認訊息可指出XDP檔案已成功大量上傳至CRX存放庫(NPR-35546)。

**文件安全性**

* 針對AdminUI上的[!UICONTROL 編輯原則]選項回報多個問題(NPR-35747)。

如需安全性更新的資訊，請參閱[Experience Manager安全性佈告欄頁面](https://helpx.adobe.com/security/products/experience-manager.html)。

## 安裝6.5.8.0 {#install}

**設定需求和詳細資訊**

* Experience Manager6.5.8.0需要Experience Manager6.5。有關詳細說明，請參閱[升級文檔](/help/sites-deploying/upgrade.md)。
* Service Pack下載可在Adobe[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)上取得。
* 在具有MongoDB和多個執行個體的部署上，使用套件管理器在其中一個製作執行個體上安裝Experience Manager6.5.8.0。

>[!NOTE]
>
>Adobe不建議移除或解除安裝[!DNL Adobe Experience Manager] 6.5.8.0套件。

### 安裝Service Pack {#install-service-pack}

要在[!DNL Adobe Experience Manager] 6.5實例上安裝Service Pack，請執行以下步驟：

1. 如果執行個體處於更新模式，請先重新啟動執行個體再進行安裝（從舊版更新執行個體時就是如此）。 Adobe還建議，如果實例的當前正常運行時間較長，則重新啟動。

1. 安裝之前，請拍攝快照或對[!DNL Experience Manager]實例進行新的備份。

1. 從[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.8.zip)下載Service Pack。

1. 開啟套件管理器，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。如需詳細資訊，請參閱[套件管理器](/help/sites-administering/package-manager.md)。

1. 選擇包，然後按一下&#x200B;**[!UICONTROL Install]**。

1. 若要更新S3連接器，請在安裝Service Pack後停止執行個體，以安裝資料夾中提供的新二進位檔案取代現有連接器，然後重新啟動執行個體。 請參閱[Amazon S3 Data Store](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)。

>[!NOTE]
>
>安裝Service Pack時，有時會退出Package Manager UI上的對話方塊。 Adobe建議您先等待錯誤記錄穩定，再存取部署。 請等待與卸載更新程式捆綁相關的特定日誌，然後確保安裝成功。 這通常會在[!DNL Safari]上發生，但可在任何瀏覽器上間歇性發生。

**自動安裝**

有兩種方式可在工作執行個體上自動安裝Adobe Experience Manager 6.5.8.0:

A.當伺服器可聯機時，將包放入`../crx-quickstart/install`資料夾。 程式包會自動安裝。

B.使用套件管理器](/help/sites-administering/package-manager.md#package-share)中的[HTTP API。 使用`cmd=install&recursive=true`以安裝嵌套的包。

>[!NOTE]
>
>Adobe Experience Manager 6.5.8.0不支援安裝Bootstrap。

**驗證安裝**

1. 產品資訊頁面(`/system/console/productinfo`)在[!UICONTROL Installed Products]下顯示更新的版本字串`Adobe Experience Manager (6.5.8.0)`。

1. 在OSGi控制台（使用Web控制台）中，所有OSGi套件組合均為&#x200B;**[!UICONTROL ACTIVE]**&#x200B;或&#x200B;**[!UICONTROL FRAGMENT]**:`/system/console/bundles`)。

1. OSGi套件組合`org.apache.jackrabbit.oak-core`為1.22.3版或更新版本(使用Web控制台：`/system/console/bundles`)。

若要了解經認證可與此版本搭配使用的平台，請參閱[技術需求](/help/sites-deploying/technical-requirements.md)。

### 安裝Adobe Experience Manager Forms附加元件套件{#install-aem-forms-add-on-package}

>[!NOTE]
>
>如果您未使用Experience ManagerForms，請略過。 Experience ManagerForms中的修正，會在排程的[!DNL Experience Manager] Service Pack發行一週後，透過個別的附加套件提供。

1. 確認您已安裝Adobe Experience Manager Service Pack。
1. 下載適用於您作業系統的 [AEM Forms 發行版本](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)所列出的對應 Forms 附加套件。
1. 依照[安裝Forms附加元件套件](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package)中所述安裝AEM Forms附加元件套件。

>[!NOTE]
>
>AEM 6.5.8.0包含新版[AEM Forms相容性套件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases)。 如果您使用舊版AEM Forms相容性套件並更新至AEM 6.5.8.0，請在安裝Forms附加元件套件後安裝最新版本的套件。

### 在JEE上安裝Adobe Experience Manager Forms {#install-aem-forms-jee-installer}

>[!NOTE]
>
>如果您沒有在JEE上使用AEM Forms，請略過。 JEE版Adobe Experience Manager Forms中的修正是透過個別安裝程式提供。

如需有關在JEE上安裝Experience ManagerForms的累積安裝程式和部署後設定的資訊，請參閱[發行說明](jee-patch-installer-65.md)。

>[!NOTE]
>
>在JEE上安裝Experience ManagerForms的Cumulative安裝程式後，請安裝最新的Forms附加元件套件，從`crx-repository\install`資料夾刪除Forms附加元件套件，然後重新啟動伺服器。

### UberJar {#uber-jar}

適用於Experience Manager6.5.8.0的UberJar位於[Maven Central存放庫](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.8/)中。

若要在Maven專案中使用UberJar，請參閱[如何使用UberJar](/help/sites-developing/ht-projects-maven.md)，並在您的專案POM中加入下列相依性：

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
>UberJar和其他相關成品可在Maven中央儲存庫中使用，而非AdobePublic Maven儲存庫(`repo.adobe.com`)。 主要UberJar檔案已重新命名為`uber-jar-<version>.jar`。 因此，`dependency`標籤沒有以`apis`作為值的`classifier`。

## 過時的功能 {#removed-deprecated-features}

以下是[!DNL Experience Manager] 6.5.7.0中標籤為過時的功能清單。在以後的版本中，標籤為過時的功能將先後刪除。 通常會提供替代選項。

查看您是否在部署中使用了功能。 此外，計畫變更實作，以使用替代選項。

| 區域 | 功能 | 替代方案 |
|---|---|---|
| Integrations | 已棄用&#x200B;**[!UICONTROL AEM雲端服務選擇加入]**&#x200B;畫面。 隨著Experience Manager6.5中更新Experience Manager和Adobe Target整合，以支援Adobe Target Standard API(透過AdobeIMS和I/O使用驗證)，以及AdobeLaunch在檢測Experience Manager頁面以用於分析和個人化方面的角色日益提升，選擇加入精靈在功能上已變得無關。 | 透過個別的Experience Manager雲端服務，設定系統連線、AdobeIMS驗證和[!DNL Adobe I/O]整合。 |
| 連接器 | Experience Manager6.5已不再使用Microsoft SharePoint 2010和Microsoft SharePoint 2013的AdobeJCR連接器。 | N/A |

## 已知問題 {#known-issues}

* 如果要將[!DNL Experience Manager]實例從6.5升級到6.5.8.0版，則可以在`error.log`檔案中查看`RRD4JReporter`異常。 重新啟動執行個體以解決問題。

* 如果您在[!DNL Experience Manager] 6.5上安裝[!DNL Experience Manager] 6.5 Service Pack 5或先前的Service Pack，則會刪除資產自訂工作流程模型（在`/var/workflow/models/dam`中建立）的執行階段副本。
若要擷取執行階段副本，Adobe建議使用HTTP API，將自訂工作流程模型的設計時間副本與其執行階段副本同步：
   `<designModelPath>/jcr:content.generate.json`。

* 如果您在[!UICONTROL 資料夾中繼資料結構Forms編輯器]和[!UICONTROL 中繼資料結構Forms編輯器]中，使用[!UICONTROL 定義規則]對話方塊編輯和建立階層式規則時遇到問題，請連絡Adobe客戶服務。 已建立和儲存的規則可如預期運作。

* 如果在[!DNL Experience Manager Assets]中重新命名階層中的資料夾，且包含資產的巢狀資料夾已發佈至[!DNL Brand Portal]，則在重新發佈根資料夾前，資料夾的標題不會在[!DNL Brand Portal]中更新。

* 當使用者首次選取以最適化表單設定欄位時，「屬性瀏覽器」中不會顯示儲存設定的選項。 在相同編輯器中選取以設定最適化表單的其他一些欄位，即可解決問題。

* 如果[!UICONTROL 連接的資產配置]嚮導在安裝後返回404錯誤消息，請使用包管理器手動重新安裝`cq-remotedam-client-ui-content`和`cq-remotedam-client-ui-components`包。

* 安裝Experience Manager6.5.x.x期間可能會顯示下列錯誤和警告訊息：
   * 「使用Target Standard API（IMS驗證）在Experience Manager中設定Adobe Target整合時，將體驗片段匯出至Target會導致建立錯誤的選件類型。 Target會建立數個選件，並改為類型「HTML」/來源「Adobe Target Classic」，而非「體驗片段」/來源「Adobe Experience Manager」。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`:在granite/operations/maintenance找不到維護窗口。
   * 使用SUM、MAX和MIN等匯總函式時(CQ-4274424)，適用性表單伺服器端驗證會失敗。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`  — 在granite/operations/maintenance處找不到維護窗口。
   * 透過Shopbable Banner檢視器預覽資產時，Dynamic Media互動式影像中的熱點不會顯示。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :等待登錄更改完成解除登錄的超時。

## 包含{#osgi-bundles-and-content-packages-included}的OSGi套件組合和內容套件

以下文本文檔列出[!DNL Experience Manager] 6.5.8.0中包含的OSGi套件組合和內容包：

* [Experience Manager6.5.8.0中包含的OSGi套件組合清單](assets/6580_bundles.txt)

* [Experience Manager6.5.8.0中包含的內容套件清單](assets/6580_packages.txt)

## 受限網站{#restricted-sites}

這些網站僅供客戶使用。 如果您是Adobe，且需要存取權，請聯絡您的客戶經理。

* [透過licensing.adobe.com下載產品](https://licensing.adobe.com/)
* 請參閱[如何聯絡Adobe客戶服務](https://experienceleague.adobe.com/docs/customer-one/using/home.html)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5發行說明](/help/release-notes/release-notes.md)
* [[!DNL Experience Manager] 產品頁面](https://www.adobe.com/tw/marketing/experience-manager.html)
* [[!DNL Experience Manager] 6.5檔案](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant)
* [訂閱 Adobe 優先產品更新](https://www.adobe.com/subscription/priority-product-update.html)

