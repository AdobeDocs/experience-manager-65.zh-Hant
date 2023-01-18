---
title: 「教學課程：建立第一個最適化表單」
seo-title: "Tutorial: Create your first adaptive form"
description: 了解如何建立商業類別、互動式和回應式表單。
seo-description: Learn to create business class, interactive, and responsive forms.
uuid: ee351a3f-ea6a-4b4c-8045-4948ad51b7c1
topic-tags: introduction
discoiquuid: 1142bcd4-e3a7-41ce-a710-132ae6c21dbe
docset: aem65
feature: Adaptive Forms
exl-id: 77a05f83-ac9a-4221-85ac-439e82623a28
source-git-commit: 318347178fd626dea8e5a15caa7cdad8fe353eba
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 9%

---

# 教學課程：建立第一個最適化表單 {#tutorial-create-your-first-adaptive-form}

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

## 簡介 {#introduction}

您在尋找適合行動裝置 **表單體驗** 這樣可以簡化註冊，增加參與，並減少週轉時間， **適用性表單** 是你的完美選擇。 適用性表單提供適合行動裝置、自動化和分析的表單體驗。 您可以輕鬆建立回應式且互動式的表單、使用自動化流程來減少管理和重複性工作，以及使用資料分析來改善並個人化客戶對表單的體驗。

本教學課程提供端對端架構，以建立最適化表單。 本教學課程可整合為一個使用案例和多個指南。 每個指南都可協助您學習並新增功能至本教學課程中建立的最適化表單。 在每本指南之後，您都有有效的最適化表單。 提供建立最適化表單的指南。 後續指南即將推出。 在本教學課程結束時，您將能夠：

* 建立最適化表單和表單資料模型。
* 設定最適化表單的樣式。
* 使用最適化表單規則編輯器來建立業務規則。
* 測試並發佈最適化表單。

![create-adaptive-form-workflow](assets/create-daptive-form-workflow.png)

歷程從學習使用案例開始：

網站提供多種產品供不同客戶使用。 客戶瀏覽入口網站、選取和訂購產品。 每個客戶都建立一個帳戶，並提供運費和帳單地址。 現有客戶薩拉·羅斯正在向網站上添加自己的送貨地址。 該網站提供一個線上表單，用於添加和更新運送地址。

網站在Adobe Experience Manager(AEM)上執行且使用AEM [!DNL Forms] 用於資料擷取和處理。 地址添加和更新表單是最適化表單。 該網站將客戶詳細資訊儲存在資料庫中。 他們使用地址添加和更新表單來檢索和顯示可用地址。 他們也可使用最適化表單來接受更新和新的地址。

### 必備條件 {#prerequisite}

* 設定 [AEM製作例項](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html#author-and-publish-installs)
* 安裝 [AEM Forms附加元件](../../forms/using/installing-configuring-aem-forms-osgi.md) 在製作例項上。
* 從資料庫提供程式獲取JDBC資料庫驅動程式（JAR檔案）。 本教學課程中的範例以 [!DNL MySQL] 資料庫與使用 [!DNL Oracle's] [MySQL JDBC資料庫驅動程式](https://dev.mysql.com/downloads/connector/j/5.1.html).

* 設定包含客戶資料的資料庫，並顯示下方欄位。 資料庫不是建立最適化表單的必要條件。 本教學課程使用資料庫來顯示表單資料模型和AEM的持續性功能 [!DNL Forms].

![自適應格式資料](assets/adaptiveformdata.png)

## 步驟1:建立最適化表單 {#step-create-an-adaptive-form}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

最適化表單是新一代、吸引人、回應式、動態且最適化的表單。 使用最適化表單，您可以提供個人化和目標式體驗。 AEM [!DNL Forms] 提供拖放式WYSIWYG編輯器，以建立最適化表單。 如需適用性表單的詳細資訊，請參閱 [製作最適化表單簡介](../../forms/using/introduction-forms-authoring.md).

目標：

* 建立可讓客戶新增送貨地址的最適化表單
* 最適化表單的版面欄位，以顯示並接受客戶的資訊
* 建立提交動作，以傳送包含表單內容的電子郵件
* 預覽並提交最適化表單

[![請參閱指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-adaptive-form.md)

## 步驟2:建立表單資料模型 {#step-create-form-data-model}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

表單資料模型可將最適化表單連接至不同的資料來源。 例如，AEM用戶配置檔案、RESTful Web服務、基於SOAP的Web服務、OData服務和關係資料庫。 表單資料模型是業務實體和服務在連接資料源中提供的統一資料表示模式。 您可以使用具有最適化表單的表單資料模型來擷取、更新、刪除資料，以及將資料新增至連線的資料來源。

目標：

* 配置網站的資料庫實例([!DNL MySQL] 資料庫)作為資料源
* 使用建立表單資料模型 [!DNL MySQL] 資料庫作為資料源
* 添加資料模型對象以形成資料模型
* 為表單資料模型配置讀寫服務
* 測試表單資料模型和已配置的服務（含測試資料）

[![請參閱指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-form-data-model.md)

## 步驟3:將規則套用至最適化表單欄位 {#step-apply-rules-to-adaptive-form-fields}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

適用性表單提供編輯器，可針對適用性表單物件編寫規則。 這些規則會根據預設條件、使用者輸入和表單上的使用者動作，定義要在表單物件上觸發的動作。 有助於確保準確性並加快表單填寫體驗。

目標：

* 建立規則並套用至最適化表單欄位
* 使用規則觸發表單資料模型服務，將資料更新至資料庫

[![請參閱指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](apply-rules-to-adaptive-form-fields.md)

## 步驟4:設定最適化表單的樣式 {#step-style-your-adaptive-form}

![](/help/forms/using/assets/09-style-your-adaptive-form-small.png)

最適化表單提供主題和 [編輯者](../../forms/using/themes.md) 來建立最適化表單的主題。 主題包含元件和面板的樣式詳細資訊，您可以以不同的形式重複使用主題。 樣式包括背景顏色、狀態顏色、透明度、對齊方式和大小等屬性。 將主題應用到表單時，指定的樣式會反映在表單的相應元件上。 最適化表單也支援表單專用樣式的內嵌樣式。

目標：

* 將現成可用的主題套用至最適化表單
* 使用主題編輯器建立最適化表單的主題
* 在自訂主題中使用網頁字型

[![請參閱指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](style-your-adaptive-form.md)

## 步驟5:發佈最適化表單 {#step-publish-your-adaptive-form}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

您可以將適用性表單發佈為獨立表單（單頁應用程式），並納入AEM [網站頁面](/help/forms/using/embed-adaptive-form-aem-sites.md)，或列於AEM [!DNL Site] 使用 [Forms入口網站](../../forms/using/introduction-publishing-forms.md).

目標：

* 以AEM頁面發佈最適化表單
* 將最適化表單內嵌於AEM [!DNL Sites] 頁面
* 將最適化表單嵌入外部網頁(在AEM外部托管的非AEM網頁)

[![請參閱指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](publish-your-adaptive-form.md)
