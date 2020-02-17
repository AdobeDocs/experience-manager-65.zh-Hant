---
title: HTML5表單的最佳範例
seo-title: HTML5表單的最佳範例
description: 調整您的XFA架構HTML5表單，以獲得最佳效能。
seo-description: 瞭解如何調整以XFA為基礎的HTML5表單，以獲得最佳效能。
uuid: 3804effd-f1f2-4d7a-8e52-717b5c1c62cf
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
content-type: reference
discoiquuid: db22f775-fab1-4a78-b334-a9c4fa613e43
docset: aem65
translation-type: tm+mt
source-git-commit: 3e83611f6b30cee774b72194bee1d03e323a6a57

---


# HTML5表單的最佳範例{#best-practices-for-html-forms}

## 概覽 {#overview}

AEM Forms有一個稱為HTML5 Forms的元件。 它可協助以HTML5格式轉換現有的XFA型PDF表單（XDP檔案）。 本檔案提供指引和建議，以縮短載入時間並改善行動裝置上HTML5表格的效能。

大部分行動裝置的處理能力和記憶體功能都有限。 它有助於改善行動裝置的待機時間。 在行動裝置上執行的網頁瀏覽器可存取有限的資源（記憶體和處理功能有限）。 達到限制後，瀏覽器行為就會變得呆滯。 本檔案提供建議，讓HTML5表格的大小保持核取。 較小的形狀不會突破裝置的記憶體和處理能力限制，提供順暢的體驗。

雖然本文中討論的建議目標是HTML5表單，但這些建議同樣適用於以XFA為基礎的PDF表單。 這些最佳實務可共同協助HTML5表格的整體效能。 它需要謹慎規劃，以開發有效率且具生產力的表單。 我們開始吧：

## 節點是HTML5表格的通用貨幣，可以明智地使用 {#nodes-are-currency-of-html-forms-spend-them-wisely}

通常，XFA表單包含多個元素。 例如，表格、文字欄位和影像。 每個元素都有許多屬性可控制元素的行為和外觀。 當XFA表單以HTML5格式呈現時，所有XFA元素和對應的屬性都會轉換為Model或HTML DOM節點。 這些節點增加了DOM的大小和複雜性。 讓HTML5表格轉換速度變慢。

瀏覽器可更輕鬆地轉換更精簡的DOM。 因此，您可以對XFA表單執行下列最佳化，以減少節點數。 因此，產生精簡的DOM結構：

* 使用標題屬性將標籤新增至欄位。 請勿使用個別的「文字」元素來新增標籤。 它有助於減輕額外的重量，從而提高效能。 它也有助於避免版面問題。
* 將表單上的「繪製」文字元素數目維持在最低。 繪圖元素有助於改善可讀性和外觀，但沒有任何資訊儲存功能。 建議將多個Draw文字元素合併為單一Draw文字元素。 不用再磨石頭，讓表格變得更精簡。

## 精簡表單的效能更佳，而且可保持資源的壓縮 {#lite-forms-perform-better-keep-the-resources-compressed}

HTML5表格可包含多種外部資源，例如影像、JavaScript和CSS檔案。 每次瀏覽器要求表單時，外部資源都會透過網路傳送。 通過網路傳輸所需的時間與檔案的大小成正比。

因此，減少外部資源的大小並僅使用絕對必要的資源是改善表單效能的較佳方法。 您可以對XFA表單執行下列最佳化，以減少表單的外部資源大小：

* 使用 [壓縮影像](/help/assets/best-practices-for-optimizing-the-quality-of-your-images.md)。 它可減少轉換表單所需的網路活動和記憶體量。 因此，形成載荷時間顯著減少。
* 使用AEM Configuration Manager(Day CQ HTML Library Manager)中的minify選項來壓縮JavaScript和CSS檔案。 如需詳細資訊，請參 [閱OSGi組態設定](/help/sites-deploying/osgi-configuration-settings.md)。
* 啟用網頁壓縮。 它可減少源自表單的請求和回應的大小。 如需詳細資訊，請 [參閱「AEM表單伺服器的效能調整」](https://helpx.adobe.com/aem-forms/6-3/performance-tuning-aem-forms.html)。

## 讓興趣持續存在，只顯示必填欄位 {#keep-the-interest-alive-show-only-required-fields}

HTML5表單可以執行到數百個頁面。 在瀏覽器中載入具有大量欄位的表單時，速度會變慢。 您可以對XFA表單執行下列最佳化，以最佳化包含大量欄位和頁面的表單：

* 評估將大型表單分割為多個表單。 您也可以使用表單集將所有較小的表單群組在一起，並以單一單位呈現。 表單集僅載入所需的表單。 此外，在表單集中，您可以設定不同表單中的常用欄位，以共用資料系結。 資料系結可協助使用者只填寫一次一般資訊；這些資訊會自動填入後續的表格，大幅提升效能。 如需表單集的詳細資訊，請參閱「 [AEM表單中的表單集」](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)。
* 請考慮分割區段，並將每個區段移至不同的頁面。 HTML5表格會動態載入頁面捲動要求上的每個頁面。 只有捲動的頁面（顯示的頁面及其前面的頁面）會儲存在記憶體中；其餘的頁面會隨選載入。 因此，分割和移動頁面上的某個區段會減少載入表單所需的時間。 您也可以將表單的第一頁當做登陸頁面。 它類似於書籍的目錄(TOC)。 表單的著陸頁面僅包含表單其他區段的連結。 它可大幅改善表單第一頁的載入時間，並改善使用者體驗。
* 依預設，將條件式區段保持隱藏。 只有在符合特定條件時，才能顯示這些區段。 它有助於將DOM的大小限制在最小。 您也可以使用標籤式導覽，一次只顯示一個區段。

## 少就是多，減少頁數 {#less-is-more-reduce-the-number-of-pages}

HTML5表格可包含資料導向欄位（表格和子表格）。 這些欄位會展開執行時期的表格大小。 例如，HTML5表單中的資料導向表格可以跨入數千列。 這類表格會導致版面配置和效能降低。 下列建議的最佳化功能可協助您使用資料導向欄位，縮短HTML5表單的載入時間：

* 使用XFA指令碼來實現分頁導覽，以顯示資料導向欄位（表格和子表單）。 在分頁導覽中，頁面上只會顯示特定資料。 它會限制瀏覽器繪圖操作一次顯示的欄位，並讓導覽表單變得更輕鬆。 此外，行動裝置上的使用者只對資料的子集感興趣。 它可協助您提供絕佳的使用者體驗，並縮短載入所需資料所需的時間。 您只要以一個價格，就能獲得兩種解決方案。  另請注意，分頁導覽無法立即使用。 您可以使用XFA指令碼來開發分頁導覽。

* 評估將多個唯讀欄合併為單一欄。 它減少了顯示表單所需的記憶體。 此外，請避免顯示不需要使用者輸入的欄。
* 如果上述建議未產生多項改進，請 [評估將資料導向的表單分割為表單集](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)。 例如，如果一個表格有1000多行，則每100行移動一次到不同的表格。 它有助於改善表單的載入時間和效能。  另請注意，表單集會為所有表單產生整合的提交XML。 若要區分每種形式的資料，請使用不同的資料根目錄。 如需詳細資訊，請參 [閱「AEM Forms中的表單集」](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)。

## 記錄檔案(DOR)的二重功能 {#power-of-two-for-document-of-record-dor}

XFA表格可以有許多區段，僅專用於記錄檔案(DOR)。 為了減少節點數並改善表單的效能，您可以維護不同的表單副本——一個用來填寫表單，另一個用來在伺服器上產生記錄檔案。 在要填寫XFA表單的復本中，會顯示僅擷取資料所需的欄位。 在「從」中生成記錄文檔XFA中，僅保留表單打印輸出中所需的欄位。 在選擇建議的方法之前，先評估效能增益和維護開銷。

## 建議的讀取 {#recommended-reads}

Adobe Experience Manager(AEM)表單可協助您將複雜的交易轉換為簡單、愉悅的數位體驗。 但是，它需要共同努力，以開發高效和有生產力的表單。 除了HTML5 Forms外，以下是針對一般AEM最佳實務的建議讀取：

* [部署和維護AEM的最佳實務](/help/sites-deploying/best-practices.md)
* [製作內容的最佳實務](/help/sites-authoring/best-practices.md)
* [管理AEM的最佳實務](/help/sites-administering/administer-best-practices.md)
* [開發解決方案的最佳實務](/help/sites-developing/best-practices.md)
* [使用最適化表單的最佳範例](/help/forms/using/adaptive-forms-best-practices.md)

## 快速參考卡 {#quick-reference-card}

您可列印下列卡片（按一下卡片即可下載高解析度版本），並將它保留在桌上以供快速參考：[![HTML5 Forms最佳範例快速參考資訊卡](do-not-localize/best-practices_reference_card.png)](assets/html5_forms_best_practices_reference_card.pdf)
