---
title: HTML5表單的最佳實務
seo-title: Best practices for HTML5 forms
description: 調整您的XFA型HTML5 Forms以獲得最佳效能。
seo-description: Learn how to tune your XFA-based HTML5 Forms for best performance.
uuid: 3804effd-f1f2-4d7a-8e52-717b5c1c62cf
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
content-type: reference
discoiquuid: db22f775-fab1-4a78-b334-a9c4fa613e43
docset: aem65
feature: Mobile Forms
exl-id: 62ff6306-9989-43b0-abaf-b0a811f0a6a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 0%

---

# HTML5表單的最佳實務{#best-practices-for-html-forms}

## 概觀 {#overview}

AEM Forms有一個名為「HTML5表單」的元件。 有助於以HTML5格式轉譯現有XFA型PDF forms（XDP檔案）。 本檔案提供准則和建議，以縮短載入時間並改善行動裝置上HTML5表單的效能。

大多數移動設備的處理能力和記憶體能力有限。 有助於改善行動裝置的待機時間。 在行動裝置上執行的網頁瀏覽器可存取有限的資源（有限的記憶體和處理功能）。 達到限制後，瀏覽器行為變得緩慢。 本檔案提供建議，讓HTML5表單的大小可以保持控制。 較小的外形不會違反裝置的記憶體和處理能力限制，並提供流暢的體驗。

雖然本文討論的建議目標是HTML5表單，但這些表單同樣適用於XFA型PDF forms。 這些最佳實務共同貢獻了HTML5表單的整體效能。 它需要精心規劃，以開發高效和高效的形式。 我們開始吧：

## 節點是HTML5表格的貨幣，明智地使用 {#nodes-are-currency-of-html-forms-spend-them-wisely}

一般而言，XFA表單有多個元素。 例如，表格、文字欄位和影像。 每個元素都有許多屬性可控制元素的行為和外觀。 以HTML5格式呈現XFA表單時，所有XFA元素和對應的屬性會轉換為模型或HTMLDOM節點。 這些節點會增加DOM的大小和複雜度。 讓HTML5表單呈現速度變慢。

瀏覽器可更輕鬆轉譯更精簡的DOM。 因此，您可以對XFA表單執行下列最佳化，以減少節點數量。 因此，產生精益DOM結構：

* 使用註解屬性將標籤新增至欄位。 請勿使用個別的文字元素來新增標籤。 它有助於減輕額外的重量，從而提高效能。 這也有助於避免版面問題。
* 將表單上的「繪製」文本元素數量保持在最小。 繪製元素有助於改善可讀性和外觀，但沒有任何資訊儲存功能。 建議將多個繪製文本元素合併為單個繪製文本元素。 不要翻石，讓形狀更輕。

## Lite表單效能更好，資源保持壓縮 {#lite-forms-perform-better-keep-the-resources-compressed}

HTML5表單可包含多個外部資源，例如影像、JavaScript和CSS檔案。 每次瀏覽器要求表單時，外部資源都會透過網路傳送。 通過網路傳輸所需的時間與檔案的大小成正比。

因此，減少外部資源的大小並僅使用絕對需要的資源是改進表單效能的優選方法。 您可以對XFA表單執行下列最佳化，以縮小表單的外部資源大小：

* 使用 [壓縮影像](/help/assets/best-practices-for-optimizing-the-quality-of-your-images.md). 它減少了呈現表單所需的網路活動和記憶體量。 因此，形式載入時間顯著減少。
* 使用AEM Configuration Manager(Day CQHTML程式庫管理器)中的minify選項來壓縮JavaScript和CSS檔案。 如需詳細資訊，請參閱 [OSGi組態設定](/help/sites-deploying/osgi-configuration-settings.md).
* 啟用Web壓縮。 它可縮小來自表單的請求和回應的大小。 如需詳細資訊，請參閱 [AEM Forms伺服器效能調整](https://helpx.adobe.com/aem-forms/6-3/performance-tuning-aem-forms.html).

## 讓興趣持續存在，只顯示必填欄位  {#keep-the-interest-alive-show-only-required-fields}

HTML5表單可能會執行到數百個頁面。 具有大量欄位的表單在瀏覽器中載入速度緩慢。 您可以對XFA表單執行下列最佳化，以使用大量欄位和頁面來最佳化表單：

* 評估將大型表單分割為多個表單。 您也可以使用表單集將所有較小的表單分組，並以單一單位呈現。 表單集僅載入必要的表單。 此外，在表單集中，您可以配置不同表單中的公共欄位以共用資料綁定。 資料綁定幫助用戶只填寫一次公共資訊；後續的表單會自動填入資訊，大幅提升效能。 如需表單集的詳細資訊，請參閱 [AEM表單中設定的表單](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html).
* 請考慮分割區段，並將每個區段移至不同的頁面。 HTML5表單會動態載入頁面捲動請求上的每個頁面。 只有已捲動的頁面（顯示的頁面及其前面的頁面）會儲存在記憶體中；其餘的頁面會隨選載入。 因此，分割和移動頁面上的區段可縮短載入表單所需的時間。 您也可以使用表單的第一頁作為登錄頁面。 它類似於書籍的目錄(TOC)。 表單的登錄頁面僅包含表單其他區段的連結。 可大幅改善表單第一個頁面的載入時間，並改善使用者體驗。
* 預設情況下，將條件截面保持隱藏。 只有在符合特定條件時，才可顯示這些區段。 有助於將DOM大小維持在最小。 您也可以使用標籤式導覽，一次只顯示一個區段。

## 越少越多，則減少頁數 {#less-is-more-reduce-the-number-of-pages}

HTML5表單可包含資料導向欄位（表格和子表單）。 這些欄位會在執行階段上展開表單的大小。 例如，HTML5表單中的資料導向表格可跨越數千列。 此類表可導致佈局和效能降低。 以下建議的最佳化措施可協助您使用資料導向欄位縮短HTML5表單的載入時間：

* 使用XFA指令碼來實現分頁導覽，以顯示資料導向欄位（表格和子表單）。 在分頁導覽中，只會在頁面上顯示特定資料。 它會限制瀏覽器一次所顯示欄位的上色操作，並讓導覽表單更輕鬆。 此外，行動裝置上的使用者只對資料子集感興趣。 它可協助您提供絕佳的使用者體驗，並縮短載入所需資料所需的時間。 你只要買一個，就能得到兩個解決方案。  另請注意，分頁導覽無法立即使用。 您可以使用XFA指令碼來開發分頁導覽。

* 評估將多個只讀列合併為單個列。 它減少了顯示表單所需的記憶體。 此外，請避免顯示不需要使用者輸入的任何欄。
* 評估將資料導向表單分割為 [表單集](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)，如果上述建議並未產生許多改善。 例如，如果表格超過1000列，則每100列就移至不同的表單。 有助於改善表單的載入時間和效能。  另請注意，表單集會為所有表單生成統一的提交XML。 若要區分每種格式的資料，請使用不同的資料根。 如需詳細資訊，請參閱 [表單集於AEM Forms](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html).

## 記錄檔案(DOR)的二次冪 {#power-of-two-for-document-of-record-dor}

XFA表單可以有許多區段專用於記錄檔案(DOR)。 要減少節點數並提高此表單的效能，您可以維護不同的表單副本 — 一個副本用於填寫表單，另一個副本用於在伺服器上生成記錄文檔。 填寫XFA表單的復本中會顯示僅擷取資料所需的欄位。 在生成記錄XFA的源文檔中，保留僅在表單打印輸出中需要的欄位。 在選擇建議的方法之前，請評估效能增益和維護開銷。

## 建議讀取  {#recommended-reads}

Adobe Experience Manager(AEM)表單可協助您將複雜的交易轉換為簡單、令人愉悅的數位體驗。 但是，它需要協調努力，發展高效和有成效的形式。 除了HTML5 Forms外，以下為一般AEM最佳實務的建議讀數：

* [部署和維護AEM的最佳實務](/help/sites-deploying/best-practices.md)
* [製作內容的最佳作法](/help/sites-authoring/best-practices.md)
* [管理AEM的最佳作法](/help/sites-administering/administer-best-practices.md)
* [開發解決方案的最佳實務](/help/sites-developing/best-practices.md)
* [使用最適化表單的最佳實務](/help/forms/using/adaptive-forms-best-practices.md)
* [AEM Forms伺服器不會將字型內嵌至動態PDF表單](https://helpx.adobe.com/aem-forms/kb/aem-forms-server-does-not-embed-fonts-to-dynamic-pdf-form.html)

## 快速參考卡 {#quick-reference-card}

您可以打印下列卡（按一下卡下載高解析度版本），並將其保留在案頭上以供快速參考：
[ ![HTML5 Forms最佳實務快速參考卡](do-not-localize/best-practices_reference_card.png)](assets/html5_forms_best_practices_reference_card.pdf)
