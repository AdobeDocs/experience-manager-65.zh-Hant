---
title: AEM 6.5 Service Pack發行說明
description: Adobe Experience Manager 6.5 Service Pack 4的發行說明。
uuid: c7bc3705-3d92-4e22-ad84-dc6002f6fa6c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5
discoiquuid: 25542769-84d1-459c-b33f-eabd8a535462
docset: aem65
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: ff006375b9ac958c7a5f9adf122990bf23808834

---


# Adobe Experience Manager 6.5 Service Pack發行說明 {#aem-service-pack-release-notes}

## 發行資訊 {#release-information}

| 產品 | **Adobe Experience Manager 6.5** |
|---|---|
| 版本 | 6.5.4.0 |
| 類型 | Service Pack版本 |
| 日期 | 2020年3月05日 |
| 下載URL | [PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.4.0)，軟 [體散發（測試版）](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.4.zip) |

## Adobe Experience Manager 6.5.4.0包含的功能 {#what-s-included-in-aem}

Adobe Experience Manager 6.5.4.0是重要的更新，其中包含新功能、客戶要求的重要增強功能以及自2019年4月6.5版全面推出以來的效能、穩定性、安全性 **增強**。 它可安裝在Adobe Experience Manager(AEM)6.5之上。

AEM 6.5.4.0中引進的一些主要功能和增強功能包括：

* AEM Assets現在已透過Adobe I/O Console設定品牌入口網站。

* AEM Forms工 [作流程現在提供新的「產生可列印的輸出](../forms/using/aem-forms-workflow-step-reference.md) 」步驟。

* [多欄支援](../forms/using/resize-using-layout-mode.md) ，以版面配置模式建立最適化表單和互動式通訊。

* 支援 [HTML](../forms/using/designing-form-template.md) 5表單中的Rich Text。

* 資產中的協助工具增強功能。

* 內建儲存庫(Apache Jackrabbit Oak)已更新至1.10.8版。

如需先前AEM 6.5 Service Pack中所推出的完整功能清單、主要重點、主要功能，請參閱「 [Adobe Experience Manager 6.5 Service Pack 4的新增功能」](new-features-latest-service-pack.md)。

### 網站 {#sites-fixes}

* 當AEM Sites頁面的URL包含冒號(:)或百分比符號(%)時，基礎瀏覽器停止回應，而CPU週期顯示尖峰(NPR-32369、NPR-31918)。

* 當開啟AEM Sites頁面以進行編輯並複製元件時，某些預留位置仍無法使用貼上動作(NPR-32317)。

* 當「管理出版物」精靈開啟時，連結至核心元件的體驗片段不會顯示在發佈的參考清單中(NPR-32233)。

* Touch UI中的即時文案總覽要比Classic UI演算的時間長得多(NPR-32149)。

* 當伺服器時間和機器時間位於不同時區時，排程的發佈時間會在Touch UI中顯示伺服器時間，而在Classic UI中，則會顯示機器時間(NPR-32077)。

* AEM Sites無法開啟URL中含有尾碼的頁面(NPR-32072)。

* 當用戶編輯內容片段時，內容片段的已刪除變化被恢復(NPR-32062)。

* 使用者可以儲存內容片段，而不需在必填欄位中提供任何資訊(NPR-31988)。

* kernel.js和ui.js未預先編譯或快取。 這會增加轉換頁面的時間(NPR-31891)。

* 啟用PageEventAuditListener時，提交隊列的長度將增加。 它影響許多操作的效能，如批量發佈、導航、批量資產移動(NPR-31890)。

* 拖曳「體驗片段」時，會觀察到高回應時間(NPR-31878)。

* 當您在回應式格線的預留位置中選取「拖曳元件到此處」選項時，會傳送GET要求，並導致HTTP 403錯誤(NPR-31845)。

* 在相同資料夾中移動內容時，會停用頁面移動選項(NPR-31840)。

* 在可編輯的範本結構模式中，版面容器中允許的元件清單會顯示不正確的結果。 版面容器中只會顯示具有設計對話方塊的元件(NPR-31816)。

* 當頁面具有使用者的唯讀權限時，Open屬性選項會顯示在sites.html中，但不會顯示在editor.html中(NPR-31770)。

* 當使用者按一下「建立」按鈕時，頁面選項就無法使用(NPR-31756)。

* 無法同步包含OOTB（現成可用）設計匯入工具元件的Adobe促銷活動(NPR-31728)。

* 當您嘗試將項目符號清單變更為編號清單時，僅會變更清單的前兩個項目(NPR-31636)。

* 當頁面未編寫且選取子節點時，選擇對話方塊仍會顯示初始節點。 當製作頁面並使用者按一下瀏覽時，頁面會重新導向至根節點，而非製作的節點(NPR-31618)。

* 「查看配置」對話框對於「收件箱」自定義工作流功能（NPR-32503和NPR-32492）無法正常工作。

* 使用「收件箱」(CQ-4282168)查看工作流資訊時，會顯示錯誤消息。

### 資產 {#assets-6540-enhancements}

* 資產收集頁面上觸發工作流程的按鈕已停用(NPR-32471)。

* 在Experience Manager中使用Dynamic Media Scene7設定將資產從一個檔案夾移至另一個檔案夾時，無名稱的檔案夾會在SPS(Scene7 Publishing System)中建立。

* 將所有資產（使用「全選」然後移動）移至包含已發佈資產的檔案夾的動作會失敗並出現錯誤(NPR-32366)。

* 產生具有${extension}的資產的轉譯失敗(NPR-32294)。

* 版本歷史記錄URL顯示在資產屬性頁面上的「參考者」欄位下(NPR-31889)。

* 無法從DAM下載的ZIP檔案，無法使用WinZip開啟(NPR-32293)。

* 當開啟「檔案夾設定」以變更檔案夾標題或縮圖影像，然後儲存檔案夾的原始權限時，會更新檔案夾的權限(NPR-32292)。

* 已排程啟動的日曆圖示不會顯示在「狀態」欄（位於DAM資產清單的傳統UI中）中，以取得已排程在日後日期和時間啟動的資產(NPR-32291)。

* 使用程式碼片段範本建立程式碼片段會在程式碼片段建立程式期間搜尋系列時發生錯誤(NPR-32290)。

* 從搜尋篩選器選取多個標籤時，會引發多個搜尋查詢(NPR-32143)。

* 當上傳檔案名稱中超過50個字元的資產時，Experience Manager Assets UI會顯示截斷的檔案名稱(NPR-32054)。

* 當Adobe Stock中核取方塊樹狀結構的第2級核取方塊被選取時，「篩選」面板中的所有核取方塊都會被清除(NPR-31919)。

* 使用Omnisearch Facets的檔案和資料夾搜尋會產生例外(NPR-31872)。

* 即使在相應元資料模式表單中設定相關性規則時，在元資料編輯器中用於強制欄位選擇的欄位突出顯示也不會被刪除(NPR-31834)。

* 葉層級標籤的完整名稱（來自標籤階層）不會顯示在資產屬性頁面中(NPR-31820)。

* 使用Safari瀏覽器上資產屬性頁面的back命令會顯示錯誤(NPR-31753)。

* 觸控式UI搜尋（透過Omnisearch完成）結果頁面會自動捲動並遺失使用者的捲動位置(NPR-31307)。

* PDF資產的資產詳細資料頁面不會顯示動作按鈕，但Experience Manager中在Dynamic Media Scene7執行模式中執行的「至系列」和「新增轉譯」按鈕除外(CQ-4286705)。

* 超過2GB的資產現在可在Dynamic Media-Scene7中上傳(CQ-4286561)。

* 資產在完成Scene7的批次上傳程式時需要太長時間處理(CQ-4286445)。

* 當使用者未在動態媒體用戶端的設定編輯器中進行任何變更時，儲存按鈕不會匯入遠端設定(CQ-4285690)。

* 當支援的3D模型已收錄到AEM中時，3D資產縮圖不提供資訊(CQ-4283701)。

* 智慧型裁切影片檢視器預設集的未處理狀態會在橫幅文字上與預設名稱一起顯示兩次(CQ-4283517)。

* 在資產的詳細資料頁面(CQ-4283309)上，會發現在3D檢視器中預覽的已上傳3D模型容器高度不正確。

* 在IE 11中，Experience Manager Dynamic Media Hybrid模式(CQ-4255590)的轉盤編輯器無法開啟。

* 鍵盤焦點會卡在「下載」對話方塊、Chrome和Safari瀏覽器的「電子郵件」下拉式清單中(NPR-32067)。

* 嘗試在AEM上新增DM雲端設定時，預設不會啟用「同步所有內容」核取方塊(CQ-4288533)。

### Foundation UI {#foundation-ui-6540}

* 滑鼠控制項會移至先前的篩選欄位，而非在使用「篩選」面板搜尋資產時保留在現有的篩選欄位中(NPR-32538)。

* 平台標籤：在標籤欄位中輸入以搜尋標籤，會顯示根邊界以外的標籤，而不會 `rootPath` 尊重標籤欄位的屬性(NPR-31895)。

* 平台UI:如果在文字欄位中新增無效路徑，路徑瀏覽器會中斷(NPR-31884)。

* 通知會隱藏在頁面選擇的嚴格功能表後方(NPR-31628)。

### 平台 {#platform-sling-6540}

* (HTL)底線取代URL路徑區段中的冒號(NPR-32231)。

### 專案 {#projects-6540}

* 即使使用者有權在子資料夾中建立專案，使用者也看不到「建立」按鈕(NPR-31832)。

### 專案翻譯 {#projects-translation-6540}

* 在中激活「修剪空間」選項時，翻譯項目建立會中斷 `Apache Sling JSP Script Handler` UI(NPR-32154)。

* 將任何要翻譯的標籤添加到翻譯項目時，UI中出現錯誤，錯誤日誌中出現Null點異常(NPR-31896)。

### 整合 {#integrations-6540}

* 啟動程式庫URL的產生只 `path` 是以 `library_name` Launch API中的值為基礎，而不是 `library_path` 以值為基礎(NPR-31550)。

* 處理LiveFyre相關項目(FYR-12420)時會顯示錯誤訊息。

### WCM範本編輯器 {#wcm-template-editor-6540}

* 在可編輯的範本結構模式中，版面容器中允許的元件清單不會顯示連結按鈕元件(CQ-4282099)。

### WCM頁面編輯器 {#wcm-page-editor-6540}

* 選取覆蓋，然後選取回應式格點拖曳元件時，會出現錯誤(CQ-4283342)。

### 促銷活動定位 {#campaign-targeting-6540}

* Target雲端設定失敗，並出現錯誤get mbox請求失敗(CQ-4279880)。

### 品牌入口網站 {#assets-brand-portal}

* 中繼資料結構下拉式值在資產屬性中不可見(CQ-4283287)。

* 中繼資料子架構不會根據資產屬性中的mimetype顯示標籤(CQ-4283288)。

* 取消發佈中繼資料結構會填入錯誤訊息，雖然結構已在後端移除。

* 預覽影像不會針對已發佈的資產顯示(CQ-4285886)。

* 使用者無法發佈或取消發佈名稱中包含單引號的資產(CQ-4272686)。

* 下載多個資產時不會顯示條款與條件(CQ-4281224)。

* 已解決次要安全性弱點。

### 社群 {#communities}

* 「建立成員」表單顯示為空白頁(NPR-31997)。

* 使用者無法檢視作者例項的Analytics報表(NPR-30913)。

### Oak-索引與查詢 {#oak-indexing-6540}

* 使用Tika剖析器剖析包含JPEG影像的MS Word和MS Excel檔案時，無法剖析，並發現類別找不到錯誤(NPR-31952)。

### 表單 {#forms-6530}

>[!NOTE]
>
>AEM Service Pack不包含AEM Forms的修正。 它們是使用個別的Forms附加套件傳送。 此外，還會發行包含JEE上AEM Forms修正的累積安裝程式。 如需詳細資訊，請 [參閱「在JEE上安裝AEM Forms附加元件](#install-aem-forms-add-on-package)[和安裝AEM Forms」](#install-aem-forms-jee-installer)。

* 通信管理：信件在提交至後置處理工作流程後會顯示額外的字元(NPR-32626)。

* 通信管理：信件在提交至後處理工作流程後，會將下拉式預留位置顯示為文字元件(NPR-32539)。

* 通信管理：字母模板中定義的預設值不會顯示在預覽模式(NPR-32511)中。

* 行動表單：在HTML版本中轉譯XDP表單時，提交按鈕會顯示為已擴充的大小(NPR-32514)。

* 檔案服務：在套用Service Pack 2後，Letters和某些其他頁面的URL存取問題(NPR-32508、NPR-32509)。

* 檔案服務：如果伺服器上的交易數超過特定限制，HTML至PDF的轉換會失敗，而且檔案類型設定會從AEM Forms伺服器移除(NPR-32204)。

* 最適化表單：瀏覽器協助工具會根據WCAG2 Level AA准則，報告調適性表單的失敗(NPR-32312、NPR-32309、CQ-4285439)。

* 最適化表單：Chrome瀏覽器協助工具報告最佳實務失敗(NPR-32310)。

* 最適化表單：設定內嵌在AEM網站頁面中的最適化表單時的轉換問題(NPR-32168)。

* 工作台：使用「取得PDF公用程式」服務的「PDF屬性」作業時，會顯示錯誤訊息(NPR-32150)。

* 檔案安全性：將DisableGlobalOfflineSynchronizationData選項設為True時，受保護的PDF檔案無法離線開啟(NPR-32078)。

* 設計人員：如果啟用標籤選項，子表單邊框會消失在產生的PDF輸出中(NPR-32547、NPR-31983、NPR-31950)。

* 設計人員：如果表格中有合併的儲存格，則無障礙環境支援測試會失敗，無法針對使用輸出服務(CQ-4285372)從XDP表單轉換的輸出PDF檔案進行協助功能測試。

## Install 6.5.4.0 {#install}

**設定需求**

* AEM 6.5.4.0需要AEM 6.5。請查看 [升級檔案](/help/sites-deploying/upgrade.md) ，以取得詳細指示。
* Adobe Package Share提供Service Pack下載，您可以直接從AEM 6.5執行個體存取。
* 在使用MongoDB和多個執行個體的部署中，使用「套件管理員」將AEM 6.5.4.0安裝在其中一個「作者」執行個體上。
* 在安裝Service Pack之前，請確定您有AEM例項的快照或新鮮備份。
* 在安裝之前重新啟動實例。 雖然只有在實例仍處於更新模式時才需要此選項（這是從舊版更新實例時的情況），但建議在實例運行較長時段時使用此選項。

>[!CAUTION]
>
>Adobe不建議移除或解除安裝AEM 6.5.4.0套件。

### 透過Package Share安裝Service Pack {#install-service-pack-via-package-share}

請執行下列步驟，在現有的AEM 6.5執行個體上安裝Service Pack:

1. 從AEM登入至「Package Share」（封裝共用），或直接從您的瀏覽器登入並下載 [AEM 6.5.4.0套件](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/servicepack/AEM-6.5.4.0)。

1. 使用Package Manager安裝下載的套件。

>[!NOTE]
>
>**在安裝6.5.4.0時，Package Manager UI上的對話有時會無法正常退出**
>
>因此，建議您先等待錯誤記錄穩定，再存取執行個體。 在確保安裝成功之前，用戶必須等待與卸載更新程式包相關的特定日誌。 通常在Safari上會發生，但在任何瀏覽器上都會偶爾發生。

**自動安裝**

有兩種方式可自動將AEM 6.5.4.0安裝至執行中的例項：

答：將套件放入……*/crx-quickstart/install* folder whe the server is available online. 軟體包會自動安裝。

B.使用 [Package Manager的HTTP API](https://docs.adobe.com/content/docs/en/crx/2-3/how_to/package_manager.html) —— 請確定您使用cmd=install&amp;recursive=true —— 如此便會安裝巢狀封裝。

>[!NOTE]
>
>AEM 6.5.4.0不支援Bootstrap安裝。

**驗證安裝**

1. 「產品資訊」頁面(/system/console/ productinfo)會在「已安裝產品」下顯示更 `Adobe Experience Manager, Version 6.5.4.0` 新的版本字串。

1. 所有OSGi捆綁包都 **[!UICONTROL 是OSGi控制台中的]****[!UICONTROL ACTIVE或FRAGMENT]** (使用Web控制台：/system/console/bundles)。
1. OSGI套件org.apache.jackrabbit.oak-core是1.10.6版或更新版本(使用Web Console:/system/console/bundles)。

若要查看哪些平台已通過此版本的認證，請參閱技術 [要求](/help/sites-deploying/technical-requirements.md)。

### 安裝AEM Forms附加元件套件 {#install-aem-forms-add-on-package}

>[!NOTE]
>
>如果您不使用AEM Forms，請略過。 AEM Forms中的修正是透過個別的附加套件傳送。

>[!NOTE]
>
>AEM 6.5.4.0包含新版 [AEM Forms Compatibility套件](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/compatpack/AEM-FORMS-6.5.3.0-COMPAT)。 如果您使用舊版AEM Forms Compatibility套件並更新至AEM 6.5.4.0，請在安裝Forms Add-On套件後安裝最新版的AEM Forms Compatibility套件。

1. 請確定您已安裝AEM Service Pack。
1. 下載您作業系統的 [AEM Forms版本中列出的對應Forms附加元件套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 。
1. 如安裝AEM Forms附加元件套件中所述，安 [裝Forms附加元件套件](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package)。

### 在JEE上安裝AEM Forms {#install-aem-forms-jee-installer}

>[!NOTE]
>
>如果您未在JEE上使用AEM Forms，請略過。 JEE上的AEM Forms中的修正會透過個別安裝程式提供。

如需在JEE上安裝AEM Forms累積安裝程式和部署後設定的詳細資訊，請參閱修補程 [式0011的發行說明](https://helpx.adobe.com/aem-forms/quick-fixes/6-5/jee-patch-0011.html)。

#### 工作台安裝程式

由於是完整安裝程式，因此與修補程式版本相比，檔案大小更大。 在安裝新版本之前，請先解除安裝舊版Workbench。

### UberJar {#uber-jar}

Adobe Public Maven儲存庫中提供UberJar for AEM 6.5.4.0 [](https://repo.adobe.com/nexus/content/groups/public/com/adobe/aem/uber-jar/6.5.4/)。

要在Maven項目中使用UberJar，請參閱 [How to use UberJar](/help/sites-developing/ht-projects-maven.md) and include the following dependency in your project POM:

```shell
<dependency>
      <groupId>com.adobe.aem</groupId>
      <artifactId>uber-jar</artifactId>
      <version>6.5.4.0</version>
      <classifier>apis</classifier>
      <scope>provided</scope>
</dependency>
```

## 過時的功能 {#removed-deprecated-features}

本節列出已標示為不再支援的AEM 6.5.4.0功能。計畫在未來版本中移除的功能會先設為不建議使用，並提供替代選項。

建議客戶在目前的部署中是否使用功能，並規劃變更實施以使用替代選項。

| 區域 | 功能 | 替代方案 |
|---|---|---|
| 整合 | AEM Cloud **[!UICONTROL Services選擇加入畫面已過時]** 。 隨著AEM 6.5中的AEM和Target整合更新，以支援Target Standard API（透過Adobe IMS和I/O使用驗證），以及Adobe Launch在檢測AEM頁面以進行分析和個人化方面的角色日漸增加，「選擇加入」精靈在功能上已變得無關緊要。 | 透過個別的AEM雲端服務，設定系統連線、Adobe IMS驗證和Adobe I/O整合 |

## 已知問題 {#known-issues}

* 如果 **Connected assets configuration** wizard在安裝後傳回404錯誤訊息，請使用「套件管理器」手動重新安裝 **cq-remotedam-client-ui-content** 和 **** cq-remotedam-client-ui-components套件。
* 在安裝AEM 6.5.x.x時，可能會顯示下列錯誤和警告訊息：
   * 「當使用Target Standard API（IMS驗證）在AEM中設定Target整合時，將「體驗片段」匯出至Target會導致建立錯誤的選件類型。 Target會以「HTML」/來源「Adobe Target Classic」類型建立數個選件，而非「Experience Fragment」/來源類型「Adobe Target Classic」。
   * com.adobe.granite.maintenance.impl.TaskScheduler:在granite/operations/maintenance中找不到維護視窗。
   * 當使用SUM、MAX和MIN等集合函式時，Adaptive Form伺服器端驗證將失敗。 CQ-4274424
   * com.adobe.granite.maintenance.impl.TaskScheduler —— 在granite/operations/maintenance找不到維護視窗。
   * 透過可購買橫幅檢視器預覽資產時，不會顯示動態媒體互動影像中的熱點。

## 隨附的OSGi組合和內容套件 {#osgi-bundles-and-content-packages-included}

下列文字檔案列出AEM 6.5.4.0隨附的OSGi組合和內容封裝

AEM 6.5.4.0隨附的OSGi搭售清單

[取得檔案](assets/6540_bundles.txt)

AEM 6.5.4.0內容套件清單

[取得檔案](assets/6540_packages.txt)

## 受限制的網站 {#restricted-sites}

這些網站僅提供給客戶使用。 如果您是客戶，需要存取權，請連絡您的Adobe客戶經理。

* [產品下載，請造訪licensing.adobe.com](https://licensing.adobe.com/)
* [聯絡客戶支](https://daycare.day.com/public/contact.html)援如需有關存取支援入口網站的詳細資訊，請 [參閱存取支援入口網站](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html)。

>[!MORE 像這樣]
>
>* [AEM 6.5版本注意事項](/help/release-notes/release-notes.md)
>* [AEM產品頁面](https://www.adobe.com/solutions/web-experience-management.html)
>* [AEM 6.5 檔案](https://helpx.adobe.com/support/experience-manager/6-5.html)
>* 訂閱 [Adobe優先產品更新](https://www.adobe.com/subscription/priority-product-update.html)

