---
title: HTML5表單的最佳做法
seo-title: Best practices for HTML5 forms
description: 調整您基於XFA的HTML5Forms以獲得最佳效能。
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

# HTML5表單的最佳做法{#best-practices-for-html-forms}

## 概觀 {#overview}

AEM Forms有一個叫做HTML5形式的部分。 它幫助以HTML5格式呈現現有的基於XFA的PDF forms（XDP檔案）。 本文檔提供了指導和建議，以減少載入時間並改進移動設備上HTML5表單的效能。

大多數移動設備的處理能力和記憶體能力都有限。 它有助於提高移動設備的待機時間。 在移動設備上運行的Web瀏覽器能夠訪問有限的資源（有限的記憶體和處理能力）。 達到限制後，瀏覽器行為變得遲鈍。 此文檔提供一些建議，以保持對HTML5窗體大小的檢查。 較小的形式不會破壞設備的儲存器和處理功率限制，並提供平穩的體驗。

儘管本條所討論的建議針對HTML5種表格，但同樣適用於基於XFA的PDF forms。 這些最佳做法共同促進了HTML5表格的總體業績。 它需要認真規劃，以開發高效和生產性的形式。 我們開始吧：

## 節點是HTML5個表單的通貨，請明智地使用它們 {#nodes-are-currency-of-html-forms-spend-them-wisely}

通常， XFA表單具有多個元素。 例如，表、文本欄位和影像。 每個元素都具有許多屬性來控制元素的行為和外觀。 當XFA表單以HTML5格式呈現時，所有XFA元素和相應的屬性都將轉換為模型或HTMLDOM節點。 這些節點增加了DOM的大小和複雜性。 使HTML5形式呈現速度慢。

瀏覽器更容易呈現更精簡的DOM。 因此，可以對XFA表單執行以下優化，以減少節點數。 因此，生成一個精益DOM結構：

* 使用caption屬性將標籤添加到欄位。 不要使用單獨的Text元素添加標籤。 它有助於減輕額外的重量，從而提高效能。 它還有助於避免佈局問題。
* 將窗體上的「繪製」文本元素數保持為最小。 繪製元素有助於提高可讀性和外觀，但沒有任何資訊儲存功能。 建議將多個「繪製」文本元素合併到單個「繪製」文本元素中。 不要翻石，讓形體更瘦。

## 簡化表單效能更好，保持資源壓縮 {#lite-forms-perform-better-keep-the-resources-compressed}

HTML5表單可以包含多個外部資源，如image、JavaScript和CSS檔案。 每次瀏覽器請求表單時，外部資源都通過網路發送。 通過網路傳輸所需的時間與檔案的大小成正比。

因此，減少外部資源的規模並且僅使用絕對需要的資源是改善表格效能的優選方法。 可以對XFA表單執行以下優化，以減小表單的外部資源大小：

* 使用 [壓縮影像](/help/assets/best-practices-for-optimizing-the-quality-of-your-images.md)。 它減少了呈現表單所需的網路活動和記憶體量。 因此，成形載入時間顯著減少。
* 使用Configuration Manager(第AEMCQ天HTML庫管理器)中的minify選項壓縮JavaScript和CSS檔案。 有關詳細資訊，請參閱 [OSGi配置設定](/help/sites-deploying/osgi-configuration-settings.md)。
* 啟用Web壓縮。 它減少了從表單發出的請求和響應的大小。 有關詳細資訊，請參閱 [Forms伺服器AEM的效能調整](https://helpx.adobe.com/aem-forms/6-3/performance-tuning-aem-forms.html)。

## 保持利息有效，僅顯示必填欄位  {#keep-the-interest-alive-show-only-required-fields}

HTML5表單可以包含數百頁。 具有大量欄位的表單在瀏覽器中載入速度較慢。 可以對XFA表單執行以下優化，以使用大量欄位和頁面優化表單：

* 評估將大型窗體拆分為多個窗體。 您還可以使用表單集將所有較小的表單分組在一起，並將它們作為單個單元顯示。 表單集僅載入所需的表單。 此外，在表單集中，可以配置不同表單中的公用欄位以共用資料綁定。 資料綁定只幫助用戶填充一次公共資訊；這些資訊會以後的形式自動填充，從而大大改善了效能。 有關表單集的詳細資訊，請參閱 [表單集AEM合](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)。
* 請考慮拆分節並將每個節移動到不同的頁面。 HTML5表單在頁面滾動請求上動態載入每個頁面。 只有滾動的頁面（所顯示的頁面和它前面的頁面）被儲存在儲存器中；其餘的頁面按需載入。 因此，拆分和移動頁面本身會減少載入表單所需的時間。 您還可以將表單的第一頁用作登錄頁。 它類似於書的目錄(TOC)。 表單的登錄頁只包含指向表單其他部分的連結。 它顯著地改善了表單的第一頁的載入時間，並導致改進的用戶體驗。
* 預設情況下，將條件節隱藏。 僅當滿足特定條件時才可看到這些節。 它有助於將DOM的大小保持在最小。 也可以使用頁籤式導航一次只顯示一個截面。

## 少即多，減少頁數 {#less-is-more-reduce-the-number-of-pages}

HTML5表單可以包含資料驅動欄位（表和子表單）。 這些欄位將擴展運行時窗體的大小。 例如，HTML5窗體中的資料驅動表可以跨到數千行。 這樣的表可能會導致佈局和效能下降。 下面建議的優化可幫助您減少使用資料驅動欄位HTML5個表單的載入時間：

* 使用XFA指令碼實現分頁導航以顯示資料驅動欄位（表和子表單）。 在分頁導航中，頁面上只顯示特定資料。 它將瀏覽器上色操作限制為每次顯示的欄位，並使瀏覽表單更加容易。 此外，移動設備上的用戶只對資料子集感興趣。 它幫助您提供良好的用戶體驗，並減少載入所需資料所需的時間。 你只要買一個，就能得到兩個解決方案。  另請注意，分頁導航在框外不可用。 可以使用XFA指令碼開發分頁導航。

* 評估將多個只讀列合併到單個列中。 它減少了顯示表單所需的記憶體。 另外，避免顯示不需要用戶輸入的列。
* 評估將資料驅動表單拆分為 [表單集](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)如果上述建議沒有取得多大改進。 例如，如果一個表有1000多行，則每100行移動一個不同的窗體。 這有助於提高表格的載入時間和效能。  另請注意，表單集為所有表單生成一個合併的提交XML。 要區分每種形式的資料，請使用不同的資料根。 有關詳細資訊，請參見 [AEM Forms背景](https://helpx.adobe.com/aem-forms/6-3/formset-in-aem-forms.html)。

## 記錄文檔(DOR)的二權 {#power-of-two-for-document-of-record-dor}

XFA表單可以具有許多專用於記錄文檔(DOR)的部分。 要減少節點數並提高此類表單的效能，您可以維護表單的不同副本 — 一個副本用於填充表單，另一個副本用於在伺服器上生成記錄文檔。 在要填充XFA表單的副本中，顯示僅捕獲資料所需的欄位。 在生成記錄XFA的文檔中，僅在表單的打印輸出中保留必填欄位。 在選擇建議的方法之前，先評估效能增益和維護開銷。

## 建議的讀取  {#recommended-reads}

Adobe Experience Manager(AEM)表格可幫助您將複雜事務轉換為簡單、令人愉快的數字型驗。 但是，它需要共同努力，發展高效和生產性的形式。 除第5號FormsHTML外，以下是一般最佳做法的AEM建議讀法：

* [部署和維護的最佳做AEM法](/help/sites-deploying/best-practices.md)
* [創作內容的最佳做法](/help/sites-authoring/best-practices.md)
* [管理的最佳做AEM法](/help/sites-administering/administer-best-practices.md)
* [開發解決方案的最佳做法](/help/sites-developing/best-practices.md)
* [使用自適應表單的最佳做法](/help/forms/using/adaptive-forms-best-practices.md)
* [AEM Forms伺服器不將字型嵌入動態PDF窗體](https://helpx.adobe.com/aem-forms/kb/aem-forms-server-does-not-embed-fonts-to-dynamic-pdf-form.html)

## 快速參考卡 {#quick-reference-card}

您可以打印下列卡（按一下卡下載高解析度版本），並將其保留在案頭上，以便快速參考：
[ ![HTML5Forms最佳做法速查卡](do-not-localize/best-practices_reference_card.png)](assets/html5_forms_best_practices_reference_card.pdf)
