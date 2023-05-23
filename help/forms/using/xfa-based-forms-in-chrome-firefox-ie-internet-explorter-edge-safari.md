---
title: 無法在GoogleChrome、Firefox、Microsoft和reg；中開啟基於XFA的PDF forms邊緣，Microsoft&reg;Internet Explorer或AppleSafari
seo-title: Unable to open XFA-based PDF forms in Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer, or Apple Safari
feature: Adaptive Forms
source-git-commit: c47b4dcfd2fbdcb0b98ad815f5b04d8f593e4f64
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---


# 無法在GoogleChrome、Firefox、Microsoft® Edge、Microsoft® Internet Explorer或AppleSafari中開啟基於XFA的PDF forms{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

許多最新的瀏覽器版本都包括了對基於XFA的PDF forms的有限支援。 雖然這些瀏覽器可以開啟基於XFA的PDF forms，但提供的功能有限。 如果無法在現代瀏覽器中開啟或提交基於XFA的PDF表單，請使用以下方法之一：

* 使用 [Adobe®Acrobat®](https://www.adobe.com/acrobat.html) 或 [Adobe®Adobe®Reader®](https://get.adobe.com/reader/)、版本8或更高版本以開啟和提交基於XFA的PDF forms。
* Acrobat和Reader，在Microsoft® Windows®上，允許您配置為在「受保護視圖」模式下開啟PDF，這會阻止基於XFA的PDF forms開啟。 確保禁用Acrobat或Reader中的「受保護視圖」模式。 有關詳細資訊，請參見 [受保護視圖（僅限Windows）](https://helpx.adobe.com/in/reader/using/protected-mode-windows.html)。
* (對於Forms開發商)Adobe Experience Manager Forms也提供支援：

   * [將基於XFA的表格呈現為HTML5Forms](https://experienceleague.adobe.com/docs/experience-manager-65/forms/html5-forms/introduction.html?#key-capabilities-of-html-forms-br) 這樣，表單就可以在支援HTML5的瀏覽器中開啟，包括那些在iPad等移動設備上運行的瀏覽器。 表單的HTML5格式副本維護表單設計的佈局，並支援嵌入XFA表單模板中的大多數表單邏輯（如JavaScript、表單計算和表單驗證）。
   * [將基於XFA的表單轉換為移動響應自適應Forms](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?#create-an-adaptive-form-based-on-an-xfa-form-template)。 這些表單提供了響應性佈局、個性化功能，並通過根據需要添加或刪除欄位或節來動態適應用戶響應。 它們還為各種資料源提供現成的連接器、記錄文檔功能，並且便於與Adobe Analytics進行效能評估。 有關詳細資訊，請參見 [關鍵特性和功能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=en)。

這樣，您在XFA表單中的技術投資就得到了保護，並能夠繼續為您的最終用戶提供最佳體驗。 有關詳細資訊，請參見 [Adobe Experience Manager Forms產品文檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html)。
