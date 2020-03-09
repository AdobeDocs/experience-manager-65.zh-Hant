---
title: Adobe Experience Manager 6.5 Service Pack 4的新增功能
description: Adobe Experience Manager 6.5 Service Pack 4的新增功能
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 93521f102596a7f5cb247ddc430626d352338ce8

---


# Adobe Experience Manager 6.5 Service Pack 4的新增功能 {#aem-whats-new-service-pack-4}

在2020年，Adobe Experience Manager(AEM)6.5提供每季Service Pack的功能和持續的改進。 當客戶更快地採用創新時，這種新方法可讓他們受益。

最新的AEM Service Pack 4(6.5.4.0)將於2020年3 **月5日發行**。 本文著重說明最新Service Pack提供的功能，讓您的AEM旅程更加豐富。

## AEM Sites {#aem-sites}

### 不同領域的效能改進 {#performance-improvements}

* 縮短在網站(contexthub.kernel.js)中載入和初始化ContextHub的時間。 這可讓網站瀏覽時載入頁面的速度更快。

* 縮短在頁面編輯器畫布中拖放體驗片段後重新整理頁面的時間。

* 在即時副本概述中，當網站有超過200個即時副本時，可縮短載入項目的時間。

* 在範本編輯器中，已改進可觸發範本編輯器減慢速度的不完整或無效URL的處理。

此外，AEM 6.5 SP4還包含Style System增強功能。 您現在也可以在元件對話方塊中選取樣式。


## AEM Assets {#aem-assets}

### 透過Adobe I/O Console與品牌入口網站整合 {#assets-integration-bp}

AEM Assets現在已透過Adobe I/O設定品牌入口網站，Adobe I/O會購買IMS Token以授權品牌入口網站租戶。 之前，它是透過舊版OAuth閘道在傳統使用者介面中設定。

在2020年4月6日之後將不支援與舊版OAuth的新整合，並將改用Adobe I/O Console。 如果您未修改整合，現有的組態將繼續運作。

您可以建立新的整合，或將整合設定升級至Adobe I/O Console。

### 協助工具增強功能 {#accessibility-enhancements}

* 混合狀態核取方塊現在有aria-checked屬性，其值為&quot;mixed&quot;，以便將混合狀態公開給螢幕閱讀程式。

* 現在除了路徑型手勢外，支援鍵盤控制項，以在放大的影像周圍移動。

* 在欄位標籤中已提供日期格式限制，讓僅限鍵盤的使用者手動輸入日期。

* Alt屬性已新增至裝飾性圖示，並移除role=img屬性，因此這些圖示和影像不會公開給螢幕閱讀程式使用者。

* 已新增Alt屬性以關閉圖示，以在螢幕閱讀程式使用者在標籤上方時向他們指出。

## AEM Forms {#aem-forms}

### 在AEM Forms工作流程中產生可列印的輸出 {#generate-printable-output}

如果您想要解決方案列印來源範本檔案的多份副本，並將它與資料檔案整合，並包含許多記錄，AEM Forms提供新的「產生可列印的輸出」工作流程步驟。 例如，如果您想在每次打印源表單時使用不同的名稱來打印它，則可以在資料檔案中包含這些名稱，並將其與標準模板檔案整合。

利用此功能，使用「工 **具** >工作流 **** > **[!UICONTROL Workflow]** > **[!UICONTROL Create]****** Search for the Tools Printable Groupt Generate」（可打印輸出工作流程）步驟。

![產生可列印的輸出](assets/generate-print-output-demo.gif)

如需此功能的詳細資訊，請參 [閱「OSGi —— 步驟參考」上的「表單導向工作流程」](../forms/using/aem-forms-workflow-step-reference.md)。

### 在版面模式中支援自適應表單和互動式通訊的多欄 {#multi-column-adaptive-forms}

您現在可以在最適化表單和互動式通訊中，定義面板的欄數。

您可以切換至「版面」模式，點選您要轉換為多欄格式的面板，選取其父項並點選多欄圖示（如下圖所示），以定義面板的欄數。

![多欄版面](assets/multi-column-layout.gif)

如需詳細資訊，請參 [閱「使用版面模式調整元件大小](../forms/using/resize-using-layout-mode.md)」。

### AEM Inbox自訂 {#aem-inbox}

您是否曾感到需要自訂AEM標題中可用的選項？ 現在，我們推出新的Service Pack版本，並引入「管理控制」選 **[!UICONTROL 項]** 。

**自訂頁首文字**

屬於工作流程 **管理員群組的使用者** ，現在可以自訂位於頂端的頁首文字，以您自選的文字取代現有 **[!UICONTROL Adobe Experience Manager]** 。

您可以在檢視選取器( **[!UICONTROL 工具列右上角提供]** )>管理控制項下，找到新的「自訂頁首文字 **[!UICONTROL 」選項]**。

**自訂標誌**

與自訂頁首文字類似，屬於 **workflow-administrators** group的使用者現在可以自訂位於頁首的標誌，以及您自選的標誌。

您可以在「檢視選取器>管 **[!UICONTROL 理控制」(Admin Control]** )下找到新的「自訂標 **[!UICONTROL 志」(Customize Logo)選項]**。

有關此功能的詳細資訊，請參 [閱收件箱](../sites-authoring/inbox.md)。

### 使用者導覽控制 {#user-navigation-control}

屬於工作流程 **管理員群組的使用者** ，可以選擇讓使用者根據其角色，在受限制的模式中處理AEM。 管理員可以控制頁首中可用導覽選項的顯示，並限制使用者切換至工作流程製作模式，或導覽至「說明」或其他解決方案連結。

查看「檢視選取器 **[!UICONTROL >管理控制」]** 下方的 **[!UICONTROL 「隱藏導]**&#x200B;覽選項」。

有關此功能的詳細資訊，請參 [閱收件箱](../sites-authoring/inbox.md)。

### HTML5表格中的豐富式文字支援 {#rich-text-support}

文字欄位現在可顯示轉譯HTML5表單中的格式選項清單。 您必須為Forms Designer中的文本欄位定義欄位格式，才能將適當的設定應用於該欄位。

若要使用此功能，請在Forms Designer中點選「設 **[!UICONTROL 計檢視]** 」中的文字欄位。 在「欄 **[!UICONTROL 位]** 」索引標籤中，從「欄位格式 **[!UICONTROL 」下拉式清單中選]** 取「豐富式文字 **** 」以套用設定。 現在，當在HTML5表單中轉譯時，文字欄位會顯示格式選項。

如需詳細資訊，請 [參閱「設計HTML5表格的表格範本」](../forms/using/designing-form-template.md)。

## 主要亮點

除了新功能外，AEM 6.5 Service Pack 4還包含下列主要亮點：

* 現在，只有選擇性內容子樹狀結構可以同步至 *Dynamic Media - Scene7模式* ，而非全部 `content/dam`。

* 使用SOAP web service的表單資料模型整合現在支援元素上的選擇群組或屬性。

* SOAP輸入或輸出和複雜的資料結構現在支援動態群組替代。

## 舊版AEM 6.5 Service Pack的主要功能

### 適用於動態媒體的智慧型影像 {#smart-imaging}

智慧型影像處理運用每位使用者獨特的檢視特性，自動提供最適合其體驗的影像，進而提升效能和參與度。 智慧型影像功能可與您現有的影像預設集搭配使用，並在傳送時的最後一毫秒使用智慧功能，根據瀏覽器或網路連線速度進一步降低影像檔案大小。 請參閱 [智慧型影像](../assets/imaging-faq.md)。

### AEM資產的視覺搜尋 {#visual-search}

資產使用者可以搜尋視覺上類似的影像。 AEM會顯示來自DAM儲存庫的智慧型標籤影像，這些影像類似於使用者選取的影像。請參閱 [視覺搜尋](../assets/search-assets.md)。

### 共用並請求訪問用戶的收件箱項目 {#share-request-access}

您可以與其他使用者共用您的收件匣項目。 當其他使用者存取您的「收件匣」項目後，使用者就可以對共用項目宣告並採取適當動作。 同樣地，您也可以請求其他使用者存取「收件匣」項目。 請參 [閱共用並請求訪問用戶的收件箱項目](../forms/using/configure-shared-queues-osgi.md)。

### 為收件箱項目配置不在辦公室設定 {#configure-out-of-office}

如果您計畫離開辦公室，您可以指定該期間指派給您的項目會發生什麼情況。
您可以選擇指定開始日期和時間，以及結束日期和時間，讓您的離職設定生效。 您可以設定所有項目都傳送到的預設人員。 請參 [閱「設定不在辦公室」設定](../forms/using/configure-out-of-office-settings.md)。

### 使用Batch API產生多種互動式通訊 {#generate-multiple-ic}

您可以使用Batch API，從範本產生多種互動式通訊。 範本是互動式通訊，不含任何資料。 批次API將資料與範本結合，以產生互動式通訊。 API在大量製作互動式通訊時很實用。 例如，電話帳單、多名客戶的信用卡帳單。 請參 [閱使用批次API產生多種互動式通訊](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)。

### 最適化表單的標準驗證錯誤訊息 {#standard-validation}

最適化表單現在可與自訂服務整合，以執行資料驗證。 如果輸入值不符合驗證標準，且伺服器傳回的驗證錯誤訊息為標準訊息格式，則錯誤訊息會在表單的欄位層級顯示。 如果輸入值不滿足驗證標準並且伺服器驗證錯誤消息不是標準消息格式，則自適應表單提供將驗證錯誤消息轉換為標準格式以便它們在表單的欄位級顯示的機制。 請參 [閱最適化表單的標準驗證錯誤訊息](../forms/using/standard-validation-error-messages-adaptive-forms.md)。

## 自AEM 6.5 SP3以來的主要版本

在2019年12月12日至2020年3月5日之間，Adobe發佈了下列AEM核心可交付內容以外的功能：

* AEM Cloud Manager 2020.1.0和2020.2.0 Cloud Manager的每月改進，前兩個版本著重於改善管道狀態，以及下載不同步驟記錄檔的能力。 請閱讀完整的版本注意事項：
   * [Cloud Manager 2020.1.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-1-0.html)

   * [Cloud Manager 2020.2.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-current.html)

* AEM Cloud Manager CLI更新使用命令列工具自動執行Cloud Manager工作。 我們不斷擴展CLI —— 在 [GitHub上加入](https://github.com/adobe/aio-cli-plugin-cloudmanager/releases)。

* AEM Sites:專案原型23啟動新AEM專案的最佳方式。 Archetype 23將SPA專 [案原型與一般網站整合為一](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-23)，進一步提供預設主題，以開始您的前端開發。

* AEM Sites:WKND參考網站所 [有全新的參考專案](https://www.wknd.site/) ，都包含如何使用AEM建立網站的最佳實務。 閱讀完全更新的 [WKND教學課程](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html) ，並從 [GitHub擷取程式碼](https://github.com/adobe/aem-guides-wknd/releases)。

* AEM Sites:商務CIF核心元件0.7.0和0.9.0整合AEM網站和Magento商務。 我們持續擴 [充專屬的核心元件和專案原型，以商務為中心](https://github.com/adobe/aem-core-cif-components/releases)。

* AEM Assets:案頭應用程式2.0.1.1
   [取得對資產的案頭存取權](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html)

* AEM Screens:功能套件202001直接在AEM中使用數位標牌。 利用最新的功能套件取得最新的增強功能，這次我們 [將啟用跨多媒體播放器的同步播放](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202001.html)。

## 實用資源

* [AEM 6.5使用指南](../user-guide/capabilities.md)

* [Adobe Experience Manager 6.5的一般發行說明](release-notes.md)

* [Adobe Experience Manager 6.5的Service Pack發行說明](sp-release-notes.md)
