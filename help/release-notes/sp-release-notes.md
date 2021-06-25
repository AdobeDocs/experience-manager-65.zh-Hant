---
title: '[!DNL Experience Manager] 6.5 service pack發行說明'
description: ' [!DNL Adobe Experience Manager] 6.5 service pack 9專屬的發行說明'
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: 557615a019fedee1863e4d1970445fbfa17736cb
workflow-type: tm+mt
source-wordcount: '3805'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager] 6.5 service pack發行說明 {#aem-service-pack-release-notes}

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.9.0 |
| 類型 | Service Pack發行 |
| 日期 | 2021 年 5 月 27 日 |
| 下載URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.9-1.0.zip) |

## [!DNL Adobe Experience Manager] 6.5.9.0中包含的內容 {#what-s-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.9.0包含自2019年4月發行6.5版以來所推出的新功能、客戶要求的重要增強功能，以及效能、穩定性和安全性等改善項目。Service Pack安裝在[!DNL Adobe Experience Manager] 6.5上。

[!DNL Adobe Experience Manager] 6.5.9.0中引入的主要功能和增強包括：

* [!DNL Experience Manager Sites] Dynamic Media Foundation元件現在可讓您在使用回應式影像預設集或智慧型裁切時，開啟或關閉高解析度裝置的最佳化。

* 為了改善效能，`hidden=false`條件從JCR查詢移至[!UICONTROL QueryBuilder]求值器。 要驗證更改後隱藏的謂語是否正在工作，[!DNL Experience Manager]檢查是否未顯示任何隱藏資料夾。

* 能夠還原[!DNL Experience Manager Sites]頁面上已刪除的頁面和樹狀結構。

* 支援新使用者使用郵件程式設定服務的重新整理Token來重新整理存取Token。

* [支援郵件設定服務的SMTP XOAUTH2](/help/sites-administering/notification.md#setting-up-oauth) 機制。

* 支援[!DNL MongoDB] 4.2和4.4版。

* 根據中國地區和地區的新命名慣例，會更新與香港、澳門和台灣相關的名稱出現次數。

* [!DNL Experience Manager] [[!DNL Assets]](#assets-accessibility-6590)和[[!DNL Dynamic Media]](#accessibility-dm-6590)中的協助工具增強功能。

* 智慧影像處理DPR（設備像素比率）和網路頻寬優化使您能夠高效地提供最佳質量影像；在具有高解析度顯示器且網路頻寬受限的設備上。 如需詳細資訊和時間軸，請參閱[智慧型影像常見問題集](/help/assets/imaging-faq.md)。

* [!DNL Dynamic Media] 傳送(`fmt` URL修飾元)支援新一代影像格式AVIF（AV1影像格式）。有關更多詳細資訊和時間軸，請參閱[影像提供和呈現API fmt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html)。

* 能夠使用[!UICONTROL 指派任務]工作流步驟向組發送通知電子郵件。

* 修改源互動式通信後檢索互動式通信草稿的功能。

* 在[!DNL Experience Manager Forms]中為載入、呈現和驗證reCAPTCHA服務設定自定義域名。

* [!UICONTROL 叫用表單資料模型服務]工作流程步驟的輸入資料增強功能。

* 在[!DNL Experience Manager Forms]的「記錄文檔」模板中使用多個首頁。

* [!DNL Experience Manager Forms]中記錄檔案中的支援分頁。

* 內建存放庫(Apache Jackrabbit Oak)更新至1.22.7。

如需[!DNL Experience Manager] 6.5.9.0中推出的完整功能和增強功能清單，請參閱[ [!DNL Adobe Experience Manager]  6.5 Service Pack 9](new-features-latest-service-pack.md)中的新功能。

>[!NOTE]
>
>從Service Pack 9開始，[!DNL Experience Manager]客戶可以使用OpenJDK的[!DNL Azul Zulu]版本編號開發和運行其[!DNL Experience Manager]應用程式，該版本符合Java SE的標準。
>[!DNL Experience Manager]客戶也可Adobe[!DNL Azul Zulu] JDK。
>您可以從[Adobe軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)下載[!DNL Azul Zulu] JDK的相關版本。
>oracleJava技術的使用權(由Adobe分發)將於2022年12月底屆滿。 [!DNL Experience Manager] 建議客戶在此日期之前規劃並實 [!DNL Azul Zulu] 作JDK的使用。有關[!DNL Oracle Java]技術和[!DNL Azul Zulu]技術使用的詳細資訊，請參閱相關的[常見問題集](https://experienceleague.adobe.com/docs/experience-manager-65/assets/adobe-azul-openjdk-license-agreement.pdf?lang=en)。

以下是[!DNL Experience Manager] 6.5.9.0版中提供的修正清單。

### [!DNL Sites] {#sites-6590}

* 已啟用「驗證需求」屬性的已發佈頁面不會重新導向至登入頁面並傳回404錯誤訊息(NPR-36354)。

* 建立超連結時，文字元件中無法使用搜尋連結的選項(NPR-35849)。

* 使用`com.day.cq.wcm.commons.ReferenceSearch` API時會觸發周遊查詢。 它會影響[!DNL Experience Manager]伺服器的效能(NPR-36407)。

* 另一個已調整大小的配置容器內的巢狀配置容器顯示其子元件的列數不正確，導致這些元件與網格不對齊(NPR-36359)。

* 外部連結檢查器將有效的外部連結顯示為無效連結(NPR-36289)。

* 顯示參考一段時間後，參考面板開始顯示錯誤訊息(NPR-36167)。

* 移動元件時，自動建立的parsys沒有`sling:resourceType`節點(NPR-36165)。

* 如果在LiveCopy主版中刪除元件，嘗試同步LiveCopy時（在Blueprint啟動時使用轉出設定[!UICONTROL 啟動]和在Blueprint啟動時[!UICONTROL 取消啟動]），同步會失敗並記錄`NullPointerException`(NPR-36127)。

* 當使用者輸入隨選文字中的標籤時（系統上不存在的標籤），並按下Enter時，標籤會出現在欄位下方，但當內容片段儲存並重新開啟時，隨選標籤會消失(NPR-36132)。

* 收件匣沒有顯示非同步操作狀態的選項(NPR-36104)。

* 還原繼承後會建立重複的元件(NPR-36000)。

* 使用`RemoteContentRenderingService`時，對`RemoteContentRendererRequestHandler.getRequest`的要求一律會包含`ComponentExporter`的根頁面，但如果根模型未根據遍歷深度和篩選選項設定包含要求的頁面，則不會包含該頁面。 要求必須一律包含要求的頁面，讓SPA有足夠的資訊來轉譯回應(NPR-35961)。

* onTime/offTime項目不會在預期的onTime/offTime上啟用/停用(NPR-35936)。

* 發佈包含沒有`cq:lastModified`屬性的體驗片段時，會發生`NullPointerException`(NPR-35914)。

* 嘗試在容器內調整元件大小時，無法將元件重新調整為原始大小。 元件容器大小縮小時，無法將大小設回原始容器(NPR-35809)。

* 在轉出對話方塊中，編輯器中或從即時副本概述中觸發，已分離、暫停或未建立頁面的狀態圖示錯誤(NPR-35691)。

* 多網站管理員主版的轉出頁面屬性忽略轉出頁面和子頁面核取方塊(NPR-35634)。

* 觸控式UI(CQ-4315352、CQ-4309415)缺少傳統UI中可用的還原樹功能。

* 在[!DNL Experience Manager Sites]頁面上還原繼承和轉出頁面時發生問題(NPR-36033)。

### [!DNL Assets] {#assets-6590}

[!DNL Adobe Experience Manager] 6.5.9.0修 [!DNL Assets] 正下列問題。

* 從[!UICONTROL 資料夾中繼資料結構]表單中的標籤選取元素內建立的標籤未儲存(NPR-36119)。

* 當使用小橢圓來注釋資產時，橢圓與打印版本中的注釋數重疊(NPR-36114)。

* 在欄檢視中，某些情況下，上傳重複資產時[!DNL Experience Manager]不會提示出現重複資產衝突(NPR-36048)。

* 如果「共用連結」對話方塊已開啟且未變更，按一下關閉按鈕就不會關閉(NPR-36030)。

* 選取多個資產以更新屬性時，有時會發生錯誤，或取消選取資產的屬性被更新(NPR-36002)。

* 當資產上傳時，資產檔案名稱的開頭或結尾新增了空格，其餘字元與存放庫中現有資產的名稱相同，現有資產會取代而未記錄任何錯誤(NPR-36001)。

* 在資產詳細資訊頁面中播放視訊時，播放和暫停選項無法運作(NPR-35999)。

* 大量取消發佈資產時，Brand Portal會產生錯誤，指出請求URI太長(NPR-35954)。

* 打印具有長注釋文本的資產時，即使空間可用，也會修剪注釋文本(NPR-35948)。

* 在「建立目錄」頁面的「選取範本」檢視上選取頁面時，系統會停用移至下一頁的選項(CQ-4315462)。

* 視訊資產上啟動更新資產工作流程時，頁面會重複重新整理(CQ-4313375)。

* 無法刪除或移動DAM資料夾，且會記錄例外狀況(NPR-35942)。

#### 資產中的增強功能 {#assets-enhancements}

* 在卡片、欄和前瞻分析檢視中導入[!UICONTROL 無]選項，依資產在JCR節點中的儲存順序來排序資產(NPR-36356)。

* 新增選項，以在來自Adobe Experience Manager的API回應中以小寫新增電子郵件ID(CQ-4317704)。

#### Assets中的協助工具增強功能 {#assets-accessibility-6590}

[!DNL Adobe Experience Manager] 6.5.9.0提供下 [!DNL Assets] 列協助工具增強功能。

改善下列文字和表徵圖的對比度（與背景），以便視力和顏色感知受限的用戶能夠理解：

* [!UICONTROL 屬性]頁面上的資產標題(NPR-35967)。
* 各處[!UICONTROL Rating]區段中的星級評等圖示(NPR-36009)。
* 資產和資料夾卡片檢視的文字(NPR-35966)。
* [!UICONTROL 時間軸]檢視上的預留位置文字(NPR-35965)。
* 資產搜尋結果上的資產名稱(NPR-35964)。
* [!UICONTROL 連結共用]對話方塊上的預留位置文字(NPR-35963)。
* [!UICONTROL View Settingsdialog(NPR-]35910)中的Listoption [!UICONTROL (檢]視設定)中的Metadata   、Status     和Othertext)。
*  在全 [!UICONTROL 域搜] 尋中定位並輸入searchplaceholder文字(NPR-35909)。
* 展開和折疊[!UICONTROL 內容樹]下的圖示(NPR-35908)。
* 顯示資產資料夾頁面上的[!UICONTROL Assets]文字(NPR-35905)。
* [!UICONTROL 資產中繼資料]中的文字，[!UICONTROL 資產詳細資料頁面中的[!UICONTROL 使用狀況統計資料]概述]選項(NPR-35904)。
* 資產詳細資訊頁面中[!UICONTROL properties]和[!UICONTROL edit]選項的快捷鍵文字(NPR-35904)。

### [!DNL Dynamic Media] {#dynamic-media-6590}

Adobe Experience Manager 6.5.9.0 Assets修正了[!DNL Dynamic Media]中的下列問題：

* 當[!DNL Dynamic Media]選擇性啟動並由[default](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/dynamicmedia/config-dm.html?lang=en#troubleshoot-dm-config)停用時，自訂檢視器預設集和CSS不會複製到[!DNL Dynamic Media](NPR-36232)。

* 嘗試在資產詳細資訊頁面上預覽視訊轉譯時，視訊載入速度緩慢(CQ-4320122)。

* 上傳超過200個資產且已啟用重複資產偵測器(CQ-4319633)時，瀏覽器頁面會停止回應並減慢速度。

* 將全景影像資產新增至頁面上的全景媒體元件時，會記錄未捕獲的參考錯誤(CQ-4317666)。

* 使用體驗片段實作互動式媒體檢視器時，不會從發佈者開啟體驗片段，且會記錄錯誤(CQ-4317655)。

* 以中繼資料編輯器檢視快速發佈中無法使用發佈至Dynamic Media選項(CQ-4317199)。

* 擁有唯讀權限的網站作者可以對資產使用智慧型裁切功能，並編輯智慧型裁切轉譯。 不過，擁有唯讀權限的使用者必須無法編輯Sites Dev執行個體中的資產屬性(CQ-4316450)。

* 資料夾路徑[!DNL where Dynamic]無法使用視訊註解即使[!DNL Experience Manager]例項是以[!DNL Dynamic Media]模式設定(CQ-4314950)，媒體設定亦未啟用。

* 當資產標題有雙位元組、多位元組、高ASCII、西里爾文、代理對、希伯來文、阿拉伯文和GB18030字元時，資產標題在發佈至Dynamic Media時會有問號(?) (CQ-4311872).

#### Dynamic Media中的協助工具增強功能 {#accessibility-dm-6590}

[!DNL Adobe Experience Manager] 6.5.9.0在中提 [!DNL Assets] 供下列協助工具增 [!DNL Dynamic Media]強功能。

* 在影像集編輯器中開啟對話方塊，使用鍵盤鍵來新增資產時：
   * 螢幕助讀程式會提供對話方塊已開啟的旁白。
   * 鍵盤焦點在開啟時會移至對話方塊。
   * 對話方塊關閉時，鍵盤焦點會移回「新增資產」選項(CQ-4312134)。

* 您現在可以使用熱點編輯器中的鍵盤鍵來新增及編輯資產上的熱點(CQ-4305965)。

* 您現在可以使用鍵盤鍵，透過熱點管理將超連結置於熱點上。 螢幕助讀程式焦點現在會移至欄位以編輯URL路徑，並選擇開啟選取對話方塊(CQ-4290735)。

* 改善影像集編輯器頁面上文字和控制項的對比（與背景），以便視力和顏色感知受限的使用者能夠理解(CQ-4290733)。

* 您現在可以導覽至檢視器預設集編輯器上的資產共用選項，並使用鍵盤鍵收合展開的共用選項(CQ-4290724)。

* 您現在可以使用鍵盤鍵，導覽及檢視「編輯視訊編碼」頁面「基本」和「進階」標籤上資訊圖示和警報圖示的工具提示(CQ-4290722)。

* 螢幕助讀程式現在會提供旁白，說明檢視器預設集編輯器上「外觀」標籤和「行為」標籤中各種欄位的指示(CQ-4290721)。

* 以「表單」模式導覽「編輯影像預設集」頁面時，螢幕助讀程式會提供各種欄位和控制項的用途和名稱旁白(CQ-4290717)。

* 導覽資產詳細資料頁面時，螢幕助讀程式現在會說明檢視器中各種選項的用途(CQ-4290716)。

* 改善資產詳細資訊頁面之預留位置文字的對比（與背景）「所有轉譯在轉譯中」選項，以便視力和顏色感知有限的使用者能夠理解(CQ-4290713)。

* 影像集編輯器中資產的標題欄位現在提供表示必填欄位的視覺星號，螢幕助讀程式會朗讀欄位的必要資訊(CQ-4290712)。

* 螢幕助讀程式現在可以在資產詳細資訊頁面的檢視器記憶體取及提供各種互動式選項的用途(CQ-4290708)。

### 平台 {#platform-6590}

* 當您產生Blueprint的縮圖並轉出對即時副本的變更時，某些欄位的繼承無法運作(CQ-4319517)。

* 建立資料夾時，選取「可排序」屬性並新增超過20個資產至資料夾，選取資料夾中的所有資產時，系統會顯示錯誤計數(CQ-4316243)。

* 重新整理頁面時，資料夾或資產的排序不會顯示適當的結果(CQ-4316200)。

* Handlebars JavaScript程式庫已升級至v4.7.7(NPR-36375)。

* 使用封裝管理器安裝新的程式碼封裝時，自訂套件組合沒有更新(NPR-35949)。

* `resourceresolver` Sling套件組合導致`Sling:alias`查詢失敗(NPR-35335)。

* 在Experience Manager中設定SSL時，內容路徑會遭到移除(NPR-35294)。

* 在長時間執行的工作階段之後傳回`SegmentNotFound`例外(NPR-36405)。

### Integrations {#integrations-6590}

* 無法儲存Cloud Services體驗片段已啟用繼承的頁面屬性(NPR-36107)。

* IMS使用者介面分頁和延遲載入未顯示適當結果(NPR-36046)。

* 建立A4T目標設定並選取報表來源為[!DNL Adobe Analytics]時，下拉式清單中沒有啟用Adobe Target的報表套裝可用(NPR-36006)。

### 專案 {#projects-6590}

* 無法儲存專案的屬性，因為專案的JCR路徑因專案路徑附加的額外正斜線(`/`)而未解析(NPR-36191)。

### 畫面 {#screens-6590}

* [!DNL Experience Manager Screens] 使用自訂的雙因素驗證處理常式時，播放器無法驗證(NPR-35854)。

### 商務 {#commerce-6590}

* [!UICONTROL 商務目錄]精靈無法在欄檢視中載入超過40個項目(CQ-4318379)。

### 翻譯專案 {#translation-6590}

* 將`es`重新轉譯為`es_es`頁面時未顯示更新或覆寫選項(NPR-36170)。

* 為具有人工翻譯的專案選取自動核准選項時，工作狀態會顯示為`Unknown`(NPR-35981)。

* 轉譯頁面時，[!DNL Experience Fragments]的參考路徑沒有更新為目標[!DNL Experience Fragment]參考路徑(NPR-35911)。

* 當您變更父頁面和子頁面，並傳送父頁面進行翻譯時，子頁面也會遭到錯誤的翻譯(NPR-35896)。

* 針對選取的頁面有多個同時翻譯專案時，[!UICONTROL 前往專案]選項不會連結至最新的翻譯專案(NPR-35454)。

* 將資產發佈至[!DNL Dynamic Media]時，[!DNL Experience Manager]會針對未發佈的標籤顯示錯誤訊息(CQ-4315914、CQ-4315913)。

* 開啟已刪除的作業時，[!DNL Experience Manager]顯示錯誤訊息(CQ-4315910)。

### 工作流程 {#workflow-6590}

* 按一下收件匣中可用項目的「完成」、「委派」或「開啟」動作時，沒有完成這些動作的視覺提示(NPR-36317)。

### [!DNL Communities] {#communities-6590}

* 在垃圾訊息篩選中，系統會耗用100%的Java堆積空間，導致Experience Manager伺服器無反應(NPR-36316、NPR-36493)。
* 在論壇中，源自`SearchCommentSocialComponentListProvider`的JCR會議資料被洩漏(NPR-36235)。
* 開啟特定收件匣訊息會反映所有郵件分頁錯誤及其他問題(NPR-35917)。

### [!DNL Brand Portal] {#brandportal-6590}

* 使用[!DNL Brand Portal]設定[!DNL Experience Manager Assets]時會自動啟用「資產來源補充」功能標幟(NPR-36010)。

### [!DNL Forms] {#forms-6590}

>[!NOTE]
>
>* [!DNL Experience Manager Forms] 會在排程的 [!DNL Experience Manager] Service Pack 發行日期一週後發行附加元件的套件。
>* 您現在可以在OSGi部署上，使用[!DNL OpenJDK]組建的[!DNL Azul Zulu]來開發和操作應用程式，以適用於[!DNL Experience Manager Forms]。


**調適型表單**

* 產生多個翻譯字典時[!DNL Experience Manager Forms] 6.5.7.0中的語言初始化問題(NPR-36439)。
* 將附件新增至最適化表單片段並提交表單時，[!DNL Experience Manager Forms]會顯示下列錯誤訊息(NPR-36195):

   ```TXT
    POST /content/forms/af/attachmentissue/jcr:content/guideContainer.af.submit.jsp HTTP/1.1] com.adobe.aemds.guide.servlet.GuideSubmitServlet [AF] Invalid file name or mime type for file resulted in submission failure
   ```

* 當您使用人工翻譯來更新字典並預覽最適化表單時，修改內容不會顯示(NPR-36035)。

**互動式通訊**

* 使用互動式通訊列印管道上傳影像並加以編輯時，影像不再顯示(NPR-36518)。

* 編輯文字資產和填入預留位置時，會從導覽窗格中移除所有互動式元素(NPR-35991)。

**工作流程**

* 在JBoss上呼叫[!DNL Experience Manager Forms]服務的REST端點時，[!DNL Experience Manager]會顯示下列錯誤訊息(NPR-36305):

   ```TXT
   Invalid input. The maximum length of 2000 characters was exceeded.
   ```

**後端整合**

* 將讀取服務引數系結至包含破折號的常值時，無法儲存表單資料模型(NPR-36366)。

**文件安全性**

* 當您設定GlobalSign的認證和HSM時，[!DNL Experience Manager Forms]在將時間戳記新增至LTV時顯示`Unsuported Algorithm`和`Invalid TSA Certificate`錯誤訊息(NPR-36026、NPR-36025)。

**文件服務**

* 更新[!DNL Gibson]程式庫以與[!DNL Experience Manager Forms]整合(NPR-36211)。

**Foundation JEE**

* 在AdminUI上選取「端點管理」時， [!DNL Experience Manager Forms]會顯示`endpoint registry failure`錯誤訊息(CQ-4320249)。

如需安全性更新的資訊，請參閱[[!DNL Experience Manager] 安全性佈告欄頁面](https://helpx.adobe.com/security/products/experience-manager.html)。

## 安裝6.5.9.0 {#install}

**設定需求和詳細資訊**

* Experience Manager6.5.9.0需要Experience Manager6.5。有關詳細說明，請參閱[升級文檔](/help/sites-deploying/upgrade.md)。
* Service Pack下載可在Adobe[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)上取得。
* 在具有MongoDB和多個執行個體的部署上，使用套件管理器在其中一個製作執行個體上安裝Experience Manager6.5.9.0。

>[!NOTE]
>
>Adobe不建議移除或解除安裝[!DNL Adobe Experience Manager] 6.5.9.0套件。

### 安裝Service Pack {#install-service-pack}

要在[!DNL Adobe Experience Manager] 6.5實例上安裝Service Pack，請執行以下步驟：

1. 如果執行個體處於更新模式，請先重新啟動執行個體再進行安裝（從舊版更新執行個體時就是如此）。 Adobe還建議，如果實例的當前正常運行時間較長，則重新啟動。

1. 安裝之前，請拍攝快照或對[!DNL Experience Manager]實例進行新的備份。

1. 從[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.9-1.0.zip)下載Service Pack。

1. 開啟套件管理器，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。如需詳細資訊，請參閱[套件管理器](/help/sites-administering/package-manager.md)。

1. 選擇包，然後按一下&#x200B;**[!UICONTROL Install]**。

1. 若要更新S3連接器，請在安裝Service Pack後停止執行個體，以安裝資料夾中提供的新二進位檔案取代現有連接器，然後重新啟動執行個體。 請參閱[Amazon S3 Data Store](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)。

>[!NOTE]
>
>安裝Service Pack時，有時會退出Package Manager UI上的對話方塊。 Adobe建議您先等待錯誤記錄穩定，再存取部署。 請等待與卸載更新程式捆綁相關的特定日誌，然後確保安裝成功。 這通常會在[!DNL Safari]上發生，但可在任何瀏覽器上間歇性發生。

**自動安裝**

有兩種方式可自動在工作執行個體上安裝[!DNL Experience Manager] 6.5.9.0:

A.當伺服器可聯機時，將包放入`../crx-quickstart/install`資料夾。 程式包會自動安裝。

B.使用套件管理器](/help/sites-administering/package-manager.md#package-share)中的[HTTP API。 使用`cmd=install&recursive=true`以安裝嵌套的包。

>[!NOTE]
>
>Adobe Experience Manager 6.5.9.0不支援安裝Bootstrap。

**驗證安裝**

1. 產品資訊頁面(`/system/console/productinfo`)在[!UICONTROL Installed Products]下顯示更新的版本字串`Adobe Experience Manager (6.5.9.0)`。

1. 在OSGi控制台（使用Web控制台）中，所有OSGi套件組合均為&#x200B;**[!UICONTROL ACTIVE]**&#x200B;或&#x200B;**[!UICONTROL FRAGMENT]**:`/system/console/bundles`)。

1. OSGi套件組合`org.apache.jackrabbit.oak-core`為1.22.3版或更新版本(使用Web控制台：`/system/console/bundles`)。

若要了解經認證可與此版本搭配使用的平台，請參閱[技術需求](/help/sites-deploying/technical-requirements.md)。

### 安裝Adobe Experience Manager Forms附加元件套件 {#install-aem-forms-add-on-package}

>[!NOTE]
>
>如果您未使用Experience ManagerForms，請略過。 Experience ManagerForms中的修正，會在排程的[!DNL Experience Manager] Service Pack發行一週後，透過個別的附加套件提供。

1. 確認您已安裝Adobe Experience Manager Service Pack。
1. 下載適用於您作業系統的 [AEM Forms 發行版本](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#forms-updates)所列出的對應 Forms 附加套件。
1. 依照[安裝Forms附加元件套件](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package)中所述安裝AEM Forms附加元件套件。

>[!NOTE]
>
>AEM 6.5.9.0包含新版[AEM Forms相容性套件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases)。 如果您使用舊版AEM Forms相容性套件並更新至AEM 6.5.9.0，請在安裝Forms附加元件套件後安裝最新版本的套件。

### 在JEE上安裝Adobe Experience Manager Forms {#install-aem-forms-jee-installer}

>[!NOTE]
>
>如果您沒有在JEE上使用AEM Forms，請略過。 JEE版Adobe Experience Manager Forms中的修正是透過個別安裝程式提供。

如需有關在JEE上安裝Experience ManagerForms的累積安裝程式和部署後設定的資訊，請參閱[發行說明](jee-patch-installer-65.md)。

>[!NOTE]
>
>在JEE上安裝Experience ManagerForms的Cumulative安裝程式後，請安裝最新的Forms附加元件套件，從`crx-repository\install`資料夾刪除Forms附加元件套件，然後重新啟動伺服器。

### UberJar {#uber-jar}

適用於Experience Manager6.5.9.0的UberJar位於[Maven Central存放庫](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.9-1.0/)中。

若要在Maven專案中使用UberJar，請參閱[如何使用UberJar](/help/sites-developing/ht-projects-maven.md)，並在您的專案POM中加入下列相依性：

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.9-1.0</version>
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
| 整合 | 已棄用&#x200B;**[!UICONTROL AEM雲端服務選擇加入]**&#x200B;畫面。 隨著Experience Manager6.5中更新Experience Manager和Adobe Target整合，以支援Adobe Target Standard API(透過AdobeIMS和[!DNL Adobe I/O]使用驗證)，以及AdobeLaunch在檢測Experience Manager頁面以用於分析和個人化方面的角色日益提升，選擇加入精靈在功能上已變得無關。 | 透過個別的[!DNL Experience Manager]雲端服務，設定系統連線、AdobeIMS驗證和[!DNL Adobe I/O]整合。 |
| 連接器 | Experience Manager6.5已不再使用Microsoft SharePoint 2010和Microsoft SharePoint 2013的AdobeJCR連接器。 | N/A |

## 已知問題 {#known-issues}

* 如果要將[!DNL Experience Manager]實例從6.5升級到6.5.9.0版，則可以在`error.log`檔案中查看`RRD4JReporter`異常。 重新啟動執行個體以解決問題。

* 如果您在[!DNL Experience Manager] 6.5上安裝[!DNL Experience Manager] 6.5 Service Pack 5或先前的Service Pack，則會刪除資產自訂工作流程模型（在`/var/workflow/models/dam`中建立）的執行階段副本。
若要擷取執行階段副本，Adobe建議使用HTTP API，將自訂工作流程模型的設計時間副本與其執行階段副本同步：
   `<designModelPath>/jcr:content.generate.json`。

* 如果在[!DNL Assets]中重新命名階層中的資料夾，並將包含資產的巢狀資料夾發佈至[!DNL Brand Portal]，則在重新發佈根資料夾前，資料夾的標題不會在[!DNL Brand Portal]中更新。

* 當使用者首次選取以最適化表單設定欄位時，「屬性瀏覽器」中不會顯示儲存設定的選項。 在相同編輯器中選取以設定最適化表單的其他一些欄位，即可解決問題。

* 安裝Experience Manager6.5.x.x期間可能會顯示下列錯誤和警告訊息：
   * 「使用Target Standard API（IMS驗證）在Experience Manager中設定Adobe Target整合時，將體驗片段匯出至Target會導致建立錯誤的選件類型。 Target會建立數個選件，並改為類型「HTML」/來源「Adobe Target Classic」，而非「體驗片段」/來源「Adobe Experience Manager」。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`:在granite/operations/maintenance找不到維護窗口。
   * 使用SUM、MAX和MIN等匯總函式時(CQ-4274424)，適用性表單伺服器端驗證會失敗。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`  — 在granite/operations/maintenance處找不到維護窗口。
   * 透過Shopbable Banner檢視器預覽資產時，Dynamic Media互動式影像中的熱點不會顯示。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :等待登錄更改完成解除登錄的超時。

## 包含的OSGi套件組合和內容套件 {#osgi-bundles-and-content-packages-included}

以下文本文檔列出[!DNL Experience Manager] 6.5.9.0中包含的OSGi套件組合和內容包：

* [Experience Manager6.5.9.0中包含的OSGi套件組合清單](assets/6590_bundles.txt)

* [Experience Manager6.5.9.0中包含的內容套件清單](assets/6590_packages.txt)

## 受限網站 {#restricted-sites}

這些網站僅供客戶使用。 如果您是Adobe，且需要存取權，請聯絡您的客戶經理。

* [透過licensing.adobe.com下載產品](https://licensing.adobe.com/)
* 請參閱[如何聯絡Adobe客戶服務](https://experienceleague.adobe.com/docs/customer-one/using/home.html)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5發行說明](/help/release-notes/release-notes.md)
* [[!DNL Experience Manager] 產品頁面](https://www.adobe.com/tw/marketing/experience-manager.html)
* [[!DNL Experience Manager] 6.5檔案](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant)
* [訂閱 Adobe 優先產品更新](https://www.adobe.com/subscription/priority-product-update.html)

