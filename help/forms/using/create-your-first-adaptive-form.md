---
title: 「教程：建立第一個自適應窗體"
seo-title: "Tutorial: Create your first adaptive form"
description: 學習建立商務類、互動式和響應式表單。
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

# 教程：建立第一個自適應窗體 {#tutorial-create-your-first-adaptive-form}

![01-Create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

## 簡介 {#introduction}

你是在尋找一種方便移動的 **表單體驗** 簡化了入學，增加了參與，縮短了週轉時間， **自適應格式** 是你的完美選擇。 自適應表單提供了移動、自動化和分析友好的表單體驗。 您可以輕鬆構建具有響應性和交互性的表單，使用自動化流程減少管理和重複性任務，並使用資料分析來改進和個性化客戶對表單的體驗。

本教程提供了一個端到端框架以建立自適應表單。 本教程分為使用案例和多個指南。 每本指南都幫助您學習本教程中建立的自適應表單並將新功能添加到其中。 每個指南後面都有一個工作自適應表格。 建立自適應表單的指南可用。 隨後的指南將很快提供。 在本教程的結束時，您將能夠：

* 建立自適應表單和表單資料模型。
* 設定自適應窗體的樣式。
* 使用自適應表單規則編輯器構建業務規則。
* Test並發佈自適應表單。

![建立自適應表單工作流](assets/create-daptive-form-workflow.png)

這一過程始於學習使用案例：

一個網站為不同的客戶提供一系列產品。 客戶瀏覽門戶、選擇和訂購產品。 每個客戶都建立一個帳戶並提供發運和開單地址。 現有客戶薩拉·羅斯正打算將她的送貨地址添加到網站。 該網站提供一個線上表單以添加和更新發運地址。

該網站在Adobe Experience Manager(AEM)上運AEM用 [!DNL Forms] 用於資料捕獲和處理。 地址添加和更新表單是自適應表單。 該網站將客戶詳細資訊儲存在資料庫中。 他們使用地址添加和更新表單來檢索和顯示可用地址。 它們還使用自適應格式接受更新的地址和新地址。

### 必備條件 {#prerequisite}

* 設定 [AEM作者實例](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html#author-and-publish-installs)
* 安裝 [AEM Forms附加](../../forms/using/installing-configuring-aem-forms-osgi.md) 作者案。
* 從資料庫提供程式獲取JDBC資料庫驅動程式（JAR檔案）。 本教程中的示例基於 [!DNL MySQL] 資料庫和使用 [!DNL Oracle's] [MySQL JDBC資料庫驅動程式](https://dev.mysql.com/downloads/connector/j/5.1.html)。

* 使用下面顯示的欄位設定包含客戶資料的資料庫。 資料庫對於建立自適應表單並不重要。 本教程使用資料庫來顯示表單資料模型和持久性AEM能 [!DNL Forms]。

![自適應格式資料](assets/adaptiveformdata.png)

## 步驟1:建立自適應窗體 {#step-create-an-adaptive-form}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

適應性形式是新一代、具有吸引力、響應性、動態性和適應性。 使用自適應表單，您可以提供個性化和有針對性的體驗。 AEM [!DNL Forms] 提供拖放式WYSIWYG編輯器以建立自適應表單。 有關自適應表單的詳細資訊，請參見 [創作自適應表單簡介](../../forms/using/introduction-forms-authoring.md)。

目標：

* 建立允許客戶添加發運地址的自適應表單
* 用於顯示和接受客戶資訊的自適應表單的佈局欄位
* 建立提交操作以發送包含表單內容的電子郵件
* 預覽並提交自適應表單

[![請參閱指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-adaptive-form.md)

## 步驟2:建立表單資料模型 {#step-create-form-data-model}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

一種表單資料模型允許將自適應表單連接到不同的資料源。 例如，AEM用戶配置檔案、REST風格的Web服務、基於SOAP的Web服務、OData服務和關係資料庫。 表單資料模型是在連接資料源中可用的業務實體和服務的統一資料表示模式。 您可以使用帶有自適應表單的表單資料模型來檢索、更新、刪除資料，並將資料添加到連接的資料源。

目標：

* 配置網站的資料庫實例([!DNL MySQL] 資料庫)作為資料源
* 使用 [!DNL MySQL] 資料庫作為資料源
* 添加資料模型對象以形成資料模型
* 為表單資料模型配置讀和寫服務
* Test表單資料模型和具有test資料的配置服務

[![請參閱指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-form-data-model.md)

## 第3步：將規則應用於自適應表單域 {#step-apply-rules-to-adaptive-form-fields}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

自適應表單提供編輯器，用於在自適應表單對象上編寫規則。 這些規則根據表單上的預設條件、用戶輸入和用戶操作定義對表單對象觸發的操作。 它有助於確保準確性並加快填表體驗。

目標：

* 建立規則並將其應用於自適應表單域
* 使用規則觸發表單資料模型服務以將資料更新到資料庫

[![請參閱指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](apply-rules-to-adaptive-form-fields.md)

## 第4步：設定自適應窗體的樣式 {#step-style-your-adaptive-form}

![](/help/forms/using/assets/09-style-your-adaptive-form-small.png)

自適應表單提供主題和 [編輯器](../../forms/using/themes.md) 的子菜單。 主題包含元件和面板的樣式詳細資訊，您可以以不同的形式重新使用主題。 樣式包括背景顏色、狀態顏色、透明度、對齊方式和大小等屬性。 將主題應用於表單時，指定的樣式會反映在表單的相應元件上。 自適應表單還支援特定於表單的樣式的串聯樣式。

目標：

* 將現成主題應用於自適應窗體
* 使用主題編輯器為自適應窗體建立主題
* 在自定義主題中使用Web字型

[![請參閱指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](style-your-adaptive-form.md)

## 第5步：發佈自適應表單 {#step-publish-your-adaptive-form}

![12 — 發佈 — 自適應 — 窗體 — _small](assets/12-publish-your-adaptive-form-_small.png)

您可以將自適應表單作為獨立表單（單頁應用程式）發佈，包括AEM在 [「站點」頁](/help/forms/using/embed-adaptive-form-aem-sites.md)，或列AEM表 [!DNL Site] 使用 [Forms門戶](../../forms/using/introduction-publishing-forms.md)。

目標：

* 將自適應表單發佈為頁AEM面
* 將自適應表單嵌入AEM到 [!DNL Sites] 頁面
* 將自適應表單嵌入到外部網頁(外部托管AEM的非網頁AEM)

[![請參閱指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](publish-your-adaptive-form.md)
