---
title: 顯示XFA型PDF forms和受原則保護檔案的相關問題
description: 顯示XFA型PDF forms和受原則保護檔案的相關問題
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ebb61f2c5056a780e829e64031f8eba69a8ae25b
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# 顯示XFA型PDF forms和受原則保護檔案的相關問題

如果您無法使用Adobe LiveCycle Rights Management開啟以XFA為基礎的PDF表單或受原則保護的檔案，請檢查以下原因：

* 以XFA為基礎的PDF forms和受原則保護的檔案需要Adobe® Acrobat®或Adobe® Reader®、版本8和更新版本。 請參閱[Adobe下載](https://www.adobe.com/downloads.html)以瞭解如何下載最新的Reader或Acrobat。
* Mozilla Firefox和Google Chrome等瀏覽器提供內建的PDF檢視器，不支援XFA型PDF forms。 若要在這些瀏覽器中檢視XFA型PDF forms，您必須設定為使用Acrobat或Reader開啟PDF。 如需詳細資訊，請參閱以XFA為基礎的Mozilla Firefox與Google ChromePDF forms 。
* Acrobat和Reader位於Microsoft® Windows®上，可讓您設定以受保護的檢視模式開啟PDF，如此可防止開啟XFA型PDF forms和受原則保護的檔案。 請確定Acrobat或Reader中的受保護檢視模式已停用。 如需詳細資訊，請參閱[受保護的檢視（僅限Windows）](https://helpx.adobe.com/tw/acrobat/kb/end-of-support-acrobat-x-reader-x.html)。
* 如果您嘗試在行動裝置上存取以XFA為基礎的PDF forms或受原則保護的檔案，請考慮下列事項：

   * 在行動裝置上開啟受原則保護的檔案需要適用於行動裝置的Adobe Reader。 如需詳細資訊，請參閱[Adobe Reader行動應用程式](https://www.adobe.com/in/acrobat/mobile/acrobat-reader.html)。
   * iOS、Android以及Blackberry行動裝置和智慧型手機不支援搭配XFA表單的Adobe Reader外掛程式。 LiveCycle ES4提供的服務是針對使用HTML5的行動裝置；表單建立者必須使用該服務才能允許表單用於這些裝置。
   * 如果您在Windows 8行動裝置上使用Metro風格，請變更為「傳統」檢視，或搭配LiveCycle ES4使用HTML5。

>[!NOTE]
>
>LiveCycle ES4支援將XFA型表單轉譯為HTML5，因此這些表單可以在支援HTML5的瀏覽器中開啟，包括在iPad等行動裝置上執行的那些表單。 表單的HTML5轉譯可維護表單設計的版面，並支援內嵌於XFA表單範本中的大部分表單邏輯(例如JavaScript、表單計算和表單驗證)。 如此一來，您對XFA表單的技術投資便可輕鬆轉移到無法執行Adobe Reader外掛程式的裝置上。
>如需詳細資訊，請參閱升級至[LiveCycle產品檔案](https://business.adobe.com/tw/products/experience-manager/forms/aem-forms.html)。

[法律注意事項](https://chl-author-preview.corp.adobe.com/content/help/en/legal/legal-notices.html)    |    [線上隱私權原則](https://www.adobe.com/tw/privacy.html)