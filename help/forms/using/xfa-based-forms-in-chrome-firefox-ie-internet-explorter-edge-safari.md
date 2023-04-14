---
title: 無法在Google Chrome、Firefox、Microsoft&reg；中開啟以XFA為基礎的PDF formsEdge, Microsoft&reg;Internet Explorer或Apple Safari
seo-title: Unable to open XFA-based PDF forms in Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer, or Apple Safari
feature: Adaptive Forms
source-git-commit: c47b4dcfd2fbdcb0b98ad815f5b04d8f593e4f64
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---


# 無法在Google Chrome、Firefox、Microsoft® Edge、Microsoft® Internet Explorer或Apple Safari中開啟以XFA為基礎的PDF forms{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

許多最新的瀏覽器版本都包含對XFA型PDF forms的有限支援。 雖然這些瀏覽器可以開啟XFA型PDF forms，但提供的功能有限。 如果您無法在現代瀏覽器中開啟或提交XFA型PDF表單，請使用下列其中一種方法：

* 使用 [Adobe®Acrobat®](https://www.adobe.com/acrobat.html) 或 [Adobe®Adobe®Reader®](https://get.adobe.com/reader/)，第8版或更新版本，以開啟並提交XFA型PDF forms。
* Acrobat和Reader(位於Microsoft® Windows®上)可讓您設定以「受保護檢視」模式開啟PDF，這會防止開啟以XFA為基礎的PDF forms。 請確定您的Acrobat或Reader中的「受保護檢視」模式已停用。 如需詳細資訊，請參閱 [受保護視圖（僅限Windows）](https://helpx.adobe.com/in/reader/using/protected-mode-windows.html).
* (適用於Forms開發人員)Adobe Experience Manager Forms也支援：

   * [將XFA型表單轉譯至HTML5 Forms](https://experienceleague.adobe.com/docs/experience-manager-65/forms/html5-forms/introduction.html?#key-capabilities-of-html-forms-br) 如此一來，表單就能在支援HTML5的瀏覽器中開啟，包括在iPad等行動裝置上執行的瀏覽器。 表單的HTML5轉譯可維護表單設計的版面配置，並支援內嵌於XFA表單範本中的大部分表單邏輯（例如JavaScript、表單計算和表單驗證）。
   * [將XFA型表單轉換為行動回應式適用性Forms](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?#create-an-adaptive-form-based-on-an-xfa-form-template). 這些表單提供回應式版面配置、個人化功能，並視需要新增或移除欄位或區段，以動態調整以適應使用者回應。 此外，還提供可立即用於各種資料來源的連接器、記錄檔案功能，以及輕鬆連線至Adobe Analytics以進行效能評估。 如需詳細資訊，請參閱 [主要功能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=en).

如此一來，您在XFA表單中的技術投資便能得到保護，並持續為使用者提供最佳的使用體驗。 如需詳細資訊，請參閱 [Adobe Experience Manager Forms產品檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html).
