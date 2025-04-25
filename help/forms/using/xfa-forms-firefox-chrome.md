---
title: 如何在Firefox和Chrome上開啟XFA型PDF forms
description: 如何在Firefox和Chrome上開啟XFA型PDF forms
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ebb61f2c5056a780e829e64031f8eba69a8ae25b
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---

# 如何在Firefox和Chrome上開啟XFA型PDF forms

## 問題

隨Mozilla Firefox和Google Chrome推出的內建PDF檢視器不支援XFA型PDF forms。 因此，以XFA為基礎的PDF forms不會在較新版本的Firefox和Chrome中開啟。

## 解決方案

若要在Firefox和Chrome上使用XFA型PDF forms，請執行下列步驟來設定Firefox和Chrome，以使用Adobe Reader或Adobe Acrobat開啟PDF。

>[!NOTE]
> 
> 確認電腦上已安裝Adobe Reader或Adobe Acrobat。

### 設定Firefox

1. 在Firefox中，選擇&#x200B;**工具>選項**。

1. 在[選項]對話方塊中，按一下[**應用程式**]。

1. 在「應用程式」索引標籤的「搜尋」欄位中輸入PDF 。

1. 針對搜尋結果中的「可攜式檔案格式(PDF)」內容型別，從「動作」下拉式清單中選取「**使用Adobe Acrobat （在Firefox中）」**。
   ![use-adobe-acrobat](/help/forms/using/assets/use-adobe-acrobat.png)
1. 按一下「確定」。

1. 重新啟動Firefox。

### 設定Chrome

1. 在Chrome中，前往chrome://plugins/ 。

1. 按一下Chrome PDF Viewer底下的「停用」 ，然後按一下Adobe PDF Plug-In底下的「啟用」 。
   ![chrome-pdf-viewer](/help/forms/using/assets/chrome-image.png)
如需詳細資訊，請參閱Google的[Adobe PDF外掛程式](https://support.google.com/chrome/?hl=en&amp;visit_id=638803785294106945-2276548125&amp;rd=4&amp;topic=3421431#topic=7439538)檔案。

>[!NOTE]
> 
> LiveCycle ES4支援將XFA型表單轉譯為HTML5，因此這些表單可以在支援HTML5的瀏覽器中開啟，包括在iPad等行動裝置上執行的那些表單。 表單的HTML5轉譯可維護表單設計的版面，並支援內嵌於XFA表單範本中的大部分表單邏輯(例如JavaScript、表單計算和表單驗證)。 如此一來，您對XFA表單的技術投資便可輕鬆結轉至無法執行Adobe Reader外掛程式的裝置。
>如需詳細資訊，請參閱[LiveCycle產品檔案](https://business.adobe.com/products/experience-manager/forms/aem-forms.html)。

[法律注意事項](https://chl-author-preview.corp.adobe.com/content/help/en/legal/legal-notices.html)    |    [線上隱私權原則](https://www.adobe.com/tw/privacy.html)