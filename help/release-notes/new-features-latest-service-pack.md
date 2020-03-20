---
title: Adobe Experience Manager 6.5 Service Pack 4的新增功能
description: Adobe Experience Manager 6.5 Service Pack 4的新增功能
contentOwner: AK
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: da9d682a0392e5de8e012e254fb82bd15547a542

---


# Adobe Experience Manager 6.5 Service Pack 4的新增功能 {#aem-whats-new-service-pack-4}

Adobe Experience Manager(AEM)6.5透過每季Service Pack提供功能和持續的改善。 新方法可讓客戶更快地採用創新技術，從而獲益。

最新的AEM Service Pack 4(6.5.4.0)將於2020年3 **月5日發行**。 本文著重說明最新Service Pack提供的功能，讓您的AEM旅程更加豐富。

## AEM Sites {#aem-sites}

AEM 6.5.4.0包含Style System增強功能。 您現在可以在元件對話方塊中選取樣式。

### 不同領域的效能改進 {#performance-improvements}

* 縮短在網站(`contexthub.kernel.js`)中載入和初始化ContextHub的時間。 這可縮短網站瀏覽時的頁面載入時間。

* 將「體驗片段」拖曳至「網站頁面編輯器」後，可縮短重新整理頁面的時間。

* 縮短「即時副本概述」中超過200個即時副本的「網站」頁面登入 **[!UICONTROL 時間]**。

* 已改善URL不完整或無效的處理。 這類URL會拖慢範本編輯器的速度。

## AEM Assets {#aem-assets}

### 使用品牌入口網站設定AEM資產 {#configure-assets-bp}

AEM Assets和品牌入口網站之間的授權渠道已變更。 之前，品牌入口網站是透過舊版OAuth閘道在傳統使用者介面中設定，該閘道使用JWT代號交換來取得IMS存取代號以進行授權。 AEM Assets現在已透過Adobe I/O設定品牌入口網站，Adobe I/O會購買IMS Token以授權您的品牌入口網站租用戶。

使用品牌入口網站設定AEM資產的步驟依您的AEM版本而異，以及您是首次設定或升級現有的設定。 如需詳 [細資訊，請參閱「設定AEM資產與品牌入口網站](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/configure-aem-assets-with-brand-portal.html) 」。


### 協助工具增強功能 {#accessibility-enhancements}

Experience Manager Assets包含下列協助工具增強功能：

* 鍵盤上的箭頭鍵可用來移動和平移縮放影像中的區域。 如需詳細資訊，請參閱 [僅使用鍵盤按鍵預覽資產](../assets/managing-assets-touch-ui.md#previewing-assets)。

* 「篩選器」面板中的混合狀態複選框（除非您選擇了所有嵌套的謂詞，否則不會選擇並刪除第一級複選框）由螢幕閱讀器讀取。

* 日期和時間格式約束在日期欄位的欄位標籤中提供，使用戶能夠使用鍵盤以正確的格式輸入日期。

   For example, `On Time (MM-DD-YYYY HH:mm)`. 其中MM是兩位數格式的月份，YYYY是年份，DD是兩位數格式的日，HH是24小時軍用格式的小時，而mm是分鐘。

* 現在 `X` 螢幕閱讀程式會公佈用來移除目前選取標籤的按鈕符號，以及選取的標籤數。

## AEM Forms {#aem-forms}

### 在AEM Forms工作流程中產生可列印的輸出 {#generate-printable-output}

新的「產生可列印的輸出」工作流程步驟可讓您將來源範本檔案與資料檔案整合。 此整合可讓您列印或儲存範本檔案的不同副本。 例如，您可以在每次打印源表單時打印不同的名稱。 將名稱儲存在資料檔案中，並將資料檔案與標準範本檔案整合。 如需此功能的詳細資訊，請參 [閱「OSGi —— 步驟參考」上的「表單導向工作流程」](../forms/using/aem-forms-workflow-step-reference.md)。

![產生可列印的輸出](assets/generate-print-output-demo.gif)

### 多欄支援在版面模式中自適應表單和互動式通訊 {#multi-column-adaptive-forms}

您現在可以在最適化表單和互動式通訊中，定義面板的欄數。 切換至版面模式，以使用新的多欄選項。 如需詳細資訊，請參 [閱「使用版面模式調整元件大小](../forms/using/resize-using-layout-mode.md)」。


![多欄版面](assets/multi-column-layout.gif)



### AEM Inbox自訂 {#aem-inbox}

新的「管理控制」選項可讓管理員：

* 自訂標題文字和標誌

* 控制頁首中可用導覽連結的顯示

「管理控制」選項僅對管理員或工作流程管理員群組的成員顯示。 有關此功能的詳細資訊，請參 [閱收件箱](../sites-authoring/inbox.md)。

### HTML5表格中的豐富式文字支援 {#rich-text-support}

現在，當在HTML5表單中轉譯時，您可以將XFA表單中的文字欄位轉換為豐富式文字欄位。 因此，文字欄位會在HTML5表單中顯示其他格式選項的清單。 如需詳細資訊，請 [參閱「設計HTML5表格的表格範本」](../forms/using/designing-form-template.md)。

### 協助工具增強功能 {#forms-accessibility-enhancements-6540}

Experience Manager Forms包含下列協助工具增強功能：

* 使用者可以調整標籤焦點，而不會針對最適化表單的Ultramarine-Accessible參考主題產生任何問題。

* 螢幕閱讀程式會在最適化表單中正確發佈核取方塊、連結、「日期選擇器」和「日期輸入」欄位。

* 最適化表單的每一頁現在都包含一個標題和一個主要地標標籤。

## 舊版AEM 6.5 Service Pack的主要功能

### 適用於動態媒體的智慧型影像(6.5.3.0) {#smart-imaging}

智慧型影像處理運用每位使用者獨特的檢視特性，自動提供最符合其體驗的影像，進而提高效能和參與度。 智慧型影像功能可與您現有的影像預設集搭配使用，並在傳送時的最後一毫秒使用智慧功能，根據瀏覽器或網路連線速度進一步降低影像檔案大小。 請參閱 [智慧型影像](../assets/imaging-faq.md)。

### AEM Assets的視覺搜尋(6.5.2.0) {#visual-search}

資產使用者可以搜尋視覺上類似的影像。 AEM會顯示來自DAM儲存庫的智慧型標籤影像，這些影像類似於使用者選取的影像。請參閱 [視覺搜尋](../assets/search-assets.md)。

### 共用並請求訪問用戶的收件箱項目(6.5.3.0) {#share-request-access}

您可以與其他使用者共用您的收件匣項目。 當其他使用者存取您的「收件匣」項目時，使用者就可以對共用項目宣告並採取適當動作。 同樣地，您也可以請求其他使用者存取「收件匣」項目。 請參 [閱共用並請求訪問用戶的收件箱項目](../forms/using/configure-shared-queues-osgi.md)。

### 為收件箱項目(6.5.3.0)配置不在辦公室的設定 {#configure-out-of-office}

如果您計畫離開辦公室，您可以指定該期間指派給您的項目會發生什麼情況。
您可以選擇指定開始日期和時間，以及結束日期和時間，讓您的離職設定生效。 您可以設定預設人員，將您的所有書籍項目傳送至該人員。 請參 [閱「設定不在辦公室」設定](../forms/using/configure-out-of-office-settings.md)。

### 使用Batch API(6.5.3.0)產生多種互動式通訊 {#generate-multiple-ic}

您可以使用Batch API，從範本產生多種互動式通訊。 範本是互動式通訊，不含任何資料。 批次API將資料與範本結合，以產生互動式通訊。 API在大量製作互動式通訊時很實用。 例如，電話帳單、多名客戶的信用卡帳單。 請參 [閱使用批次API產生多種互動式通訊](../forms/using/generate-multiple-interactive-communication-using-batch-api.md)。

## 自AEM 6.5 SP3以來的主要版本

從2019年12月12日到2020年3月5日，Adobe發佈了下列核心AEM可交付項目以外的功能：

* AEM Cloud Manager 2020.1.0和2020.2.0

   發行更新可改善管道狀態，並改善下載不同步驟記錄檔的能力。 如需詳細資訊，請參閱：

   * [Cloud Manager 2020.1.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-2020-1-0.html)


   * [Cloud Manager 2020.2.0](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/release-notes/release-notes-current.html)


* AEM Cloud Manager CLI更新

   發行更新包括使用命令列工具自動執行Cloud Manager工作。 請參 [閱GitHub](https://github.com/adobe/aio-cli-plugin-cloudmanager/releases)。

* AEM Sites:原型23

   開始新AEM專案的最佳方式。 Archetype 23將SPA專案原型與一般網站整合為一 [](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-23) ，並提供預設主題，以開始您的前端開發。

* AEM Sites:WKND參考網站

   [全新的參考專案](https://www.wknd.site/) ，內含如何使用AEM建立網站的最佳實務。 閱讀更新的 [WKND教學課程以進一步瞭解](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)。 您可從 [GitHub取得最新的程式碼](https://github.com/adobe/aem-guides-wknd/releases)。

* AEM Sites:商務CIF核心元件0.7.0和0.9.0

   將AEM Sites與Magento Commerce整合。 請參 [閱以商務為重點擴充專屬的核心元件和專案原型](https://github.com/adobe/aem-core-cif-components/releases)。

* AEM Assets:案頭應用程式2.0.1.1

   如需詳細資訊，請參 [閱「取得對資產的案頭存取權」](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/release-notes.html)。

* AEM Screens:功能套件202001

   直接從AEM內部的數位標牌。 安裝最新功能套件的增強功能，以 [在多種媒體播放器上同步播放](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/release-notes/release-notes-fp-202001.html)。

## 實用資源

* [AEM 6.5使用指南](../user-guide/home.md)

* [Adobe Experience Manager 6.5的一般發行說明](release-notes.md)

* [Adobe Experience Manager 6.5的Service Pack發行說明](sp-release-notes.md)
