---
title: 「教學課程：建立您的第一個調適性表單」
seo-title: 「教學課程：建立您的第一個調適性表單」
description: 瞭解如何建立商業類別、互動式和互動式表單。
seo-description: 瞭解如何建立商業類別、互動式和互動式表單。
uuid: ee351a3f-ea6a-4b4c-8045-4948ad51b7c1
topic-tags: introduction
discoiquuid: 1142bcd4-e3a7-41ce-a710-132ae6c21dbe
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 0%

---


# 教學課程：建立您的第一個最適化表單{#tutorial-create-your-first-adaptive-form}

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

## 簡介 {#introduction}

您是否在尋找可簡化註冊、增加參與度並縮短往返時間的行動裝置適用的&#x200B;**表單體驗**,**最適化表單**&#x200B;最適合您。 最適化表單提供行動、自動化和分析友好的表單體驗。 您可以輕鬆建立自然具有互動性的回應式表單、使用自動化流程來減少管理和重複性工作，以及使用資料分析來改善和個人化客戶對表單的體驗。

本教學課程提供端對端架構，以建立最適化表單。 本教學課程分為使用案例和多本指南。 每個指南都可協助您學習並新增功能至本教學課程中建立的最適化表單。 每個指南之後都有一個工作適應性表單。 有提供建立最適化表單的指南。 後續的指南即將推出。 在本教學課程結束時，您將能夠：

* 建立最適化表單和表單資料模型。
* 設定最適化表單的樣式。
* 使用最適化表單規則編輯器來建立業務規則。
* 測試並發佈最適化表單。

![create-adaptive-form-workflow](assets/create-daptive-form-workflow.png)

這個旅程從瞭解使用案例開始：

網站為不同的客戶提供多種產品。 客戶瀏覽入口網站，選擇並訂購產品。 每位客戶都會建立帳戶並提供運費和帳單地址。 現有客戶薩拉·羅斯正在尋找將她的送貨地址添加到網站上。 該網站提供線上表單，以新增和更新運送地址。

該網站在Adobe Experience Manager(AEM)上執行，AEM並使用[!DNL Forms]擷取和處理資料。 地址添加和更新表單是自適應表單。 該網站將客戶詳細資料儲存在資料庫中。 他們使用地址添加和更新表單來檢索和顯示可用地址。 他們還使用自適應表單來接受更新和新地址。

### 必備條件 {#prerequisite}

* 設定作AEM者例項。
* 在作者實例上安裝[AEM Forms附加元件](../../forms/using/installing-configuring-aem-forms-osgi.md)。
* 從資料庫提供程式獲取JDBC資料庫驅動程式（JAR檔案）。 教程中的示例基於[!DNL MySQL]資料庫，並使用[!DNL Oracle's] [ MySQL JDBC資料庫驅動程式](https://dev.mysql.com/downloads/connector/j/5.1.html)。

* 設定包含客戶資料的資料庫，其中欄位如下。 建立最適化表單並非必要資料庫。 本教學課程使用資料庫來顯示表單資料模型和AEM[!DNL Forms]的永續性功能。

![自適應格式資料](assets/adaptiveformdata.png)

## 步驟1:建立最適化表單{#step-create-an-adaptive-form}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

最適化表單是新一代、吸引人、回應速度快、動態性強、自適應性強的表單。 使用可調式表單，您可以提供個人化、針對性的體驗。 AEM[!DNL Forms]提供拖放式WYSIWYG編輯器，以建立最適化表單。 有關最適化表單的詳細資訊，請參閱[製作最適化表單的簡介](../../forms/using/introduction-forms-authoring.md)。

目標：

* 建立可讓客戶新增送貨地址的最適化表單
* 顯示並接受客戶資訊的最適化表單的版面欄位
* 建立提交動作以傳送包含表單內容的電子郵件
* 預覽並送出最適化表單

[![請參閱指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-adaptive-form.md)

## 步驟2:建立表單資料模型{#step-create-form-data-model}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

表單資料模型允許將自適應表單連接至不同的資料來源。 例如，AEM用戶配置檔案、REST風格的Web服務、基於SOAP的Web服務、OData服務和關係資料庫。 表單資料模型是連接資料來源中可用之商業實體和服務的統一資料表示模式。 您可以使用具有自適應表單的表單資料模型來擷取、更新、刪除並新增資料至連接的資料來源。

目標：

* 將網站的資料庫例項（[!DNL MySQL]資料庫）設為資料來源
* 使用[!DNL MySQL]資料庫作為資料源建立表單資料模型
* 新增資料模型物件以建立資料模型
* 為表單資料模型配置讀寫服務
* 測試表單資料模型及已設定的服務與測試資料

[![請參閱指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-form-data-model.md)

## 步驟3:將規則套用至最適化表單欄位{#step-apply-rules-to-adaptive-form-fields}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

最適化表單提供編輯器，可編寫最適化表單物件的規則。 這些規則會根據預設條件、使用者輸入和使用者在表單上的動作來定義要觸發表單物件的動作。 它有助於確保表單填寫的準確性並加速表單填寫體驗。

目標：

* 建立規則並套用至最適化表單欄位
* 使用規則觸發表單資料模型服務，將資料更新至資料庫

[![請參閱指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](apply-rules-to-adaptive-form-fields.md)

## 步驟4:設定最適化表單的樣式{#step-style-your-adaptive-form}

![](/help/forms/using/assets/09-style-your-adaptive-form-small.png)

最適化表單提供主題和[編輯器](../../forms/using/themes.md)，以建立最適化表單的主題。 主題包含元件和面板的樣式詳細資訊，您可以在不同的表單中重複使用主題。 樣式包括背景顏色、狀態顏色、透明度、對齊方式和大小等屬性。 當您將主題套用至表格時，指定的樣式會反映在表格的對應元件上。 最適化表單也支援表單特定樣式的內嵌樣式。

目標：

* 將立即可用的主題套用至最適化表單
* 使用主題編輯器建立最適化表單的主題
* 在自訂主題中使用網頁字型

[![請參閱指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](style-your-adaptive-form.md)

## 步驟5:測試您的最適化表單{#step-test-your-adaptive-form}

![11-test-your-adaptive-form](assets/11-test-your-adaptive-form.png)

最適化表單是客戶互動不可或缺的一部分。 請務必透過您在表單中所做的每項變更，來測試您的調適性表單。 測試表單的每個欄位都很麻煩。 AEM[!DNL Forms]提供SDK(Calvin SDK)，以自動測試最適化表單。 Calvin可讓您在網頁瀏覽器中自動測試您的調適性表單。

目標：

* 建立最適化表單的測試套裝
* 建立最適化表單的測試案例
* 執行測試案例

[![請參閱指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](testing-your-adaptive-form.md)

## 步驟6:發佈最適化表單{#step-publish-your-adaptive-form}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

您可以將最適化表單發佈為獨立表單（單頁應用程式）、包含在AEM[網站頁面](/help/forms/using/embed-adaptive-form-aem-sites.md)中，或使用[Forms入口網站](../../forms/using/introduction-publishing-forms.md)在AEM[!DNL Site]上列出。

目標：

* 將最適化表單發佈為頁AEM面
* 在[!DNL Sites]頁AEM面中內嵌最適化表單
* 將最適化表單嵌入外部網頁(非AEM外部網頁AEM)

[![請參閱指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](publish-your-adaptive-form.md)