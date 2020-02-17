---
title: 教學課程——建立您的第一個互動式通訊
seo-title: 建立您的第一個互動式通訊
description: 瞭解如何建立您的第一個互動式通訊。
seo-description: 瞭解如何建立您的第一個互動式通訊。
uuid: ed5003c6-ba3a-4fcb-8645-c7b607b22fb5
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications
discoiquuid: 954da8da-a30b-477d-bde7-3edd86a5be11
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 教學課程：建立您的第一個互動式通訊 {#tutorial-create-your-first-interactive-communication}

瞭解如何建立您的第一個互動式通訊。

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

互動式通訊可集中管理安全、個人化和互動式通訊的建立、組裝和傳遞，例如商業通訊、檔案、陳述、行銷郵件、帳單和歡迎套件。 互動式通訊可透過兩個通道提供：平面與網頁。 列印頻道用來建立PDF和紙本通訊，而網路頻道則用來提供線上體驗。

本教學課程提供端對端架構，以建立互動式通訊。 本教學課程分為使用案例和多本指南。 每個指南都可協助您建立用作建立區塊的功能，以建立互動式通訊。

下圖說明建立互動式通訊所需的建置區塊。

![工作流程](assets/workflow.gif)

在本教學課程結束時，您將能夠：

* 建立建置區塊（表單資料模型、檔案片段和範本）
* 建立互動式通訊
* 測試和發佈互動式通訊

## 使用案例 {#use-case}

這個旅程從瞭解使用案例開始：

電信營運商透過電子郵件傳送每月帳單給客戶。 這項法案是互動式通訊。 電子郵件包括：

* 受密碼保護的PDF，在本教學課程中稱為列印頻道。 它包括客戶詳細資訊、帳單詳細資訊、費用摘要、支付帳單的便利模式以及使用詳細資訊。
* 指向Web版帳單的連結，在本教學課程中稱為Web頻道。 除了PDF版中涵蓋的詳細資訊外，帳單的網頁版本還提供使用細節的圖形表示，以及以Adobe Target為基礎的個人化優惠。 網頁版本也包含線上付款表單。 線上支付不需離開IC就有幫助。
* 增值服務的連結，例如線上儲存空間、音樂訂閱和隨選視訊訂閱。

## 必備條件 {#prerequisites}

* 設定AEM作者例項。
* 在作 [者例項上安裝](/help/forms/using/installing-configuring-aem-forms-osgi.md) AEM Forms附加元件
* 設定MYSQL資料庫
* 從資料庫提供程式獲取JDBC資料庫驅動程式（JAR檔案）。 教程中的示例基於MySQL資料庫，並使用Oracle的 [MySQL JDBC資料庫驅動程式](https://dev.mysql.com/downloads/connector/j/5.1.html)。

## 步驟1:規劃互動式通訊 {#step-plan-the-interactive-communication}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

規劃互動式通訊的第一步是完成互動式通訊的內容。 完成內容後，您必須分析內容，以識別建立互動式通訊所需的各種資產類型。

**目標：**

要使用以下資料輸入模式為互動式通信建立結構：

* 靜態文字
* 表單資料模型
* Agent UI
* 條件式資料
* 影像

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/planning-interactive-communications.md)

## Step 2: Create form data model {#step-create-form-data-model}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

表單資料模型可讓您將互動式通訊連接至不同的資料來源。 例如，AEM使用者設定檔、REST風格的web services、SOAP架構的web services、OData服務和關係式資料庫。 表單資料模型是在連接資料源中可用的業務實體和服務的統一資料表示模式。 您可搭配互動式通訊使用表單資料模型，從連線的資料來源擷取資料。 如需表單資料模型的詳細資訊，請參閱「 [AEM Forms資料整合」](/help/forms/using/data-integration.md)。

**目標：**

* 將資料庫實例（MySQL資料庫）配置為資料源
* 使用MySQL資料庫作為資料源建立表單資料模型
* 新增資料模型物件以建立資料模型
* 為表單資料模型配置讀寫服務
* 在資料模型對象之間建立關聯
* 檢視自動產生的範例資料
* 編輯範例資料
* 測試表單資料模型及已設定的服務與測試資料

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-form-data-model0.md)

## 步驟3:建立檔案片段 {#step-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

文檔片段是用於構成互動式通信的通信的可重用元件。 文檔片段的類型有：文字、清單和條件。

**目標：**

* 建立檔案片段
* 建立變數
* 建立和套用規則

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-document-fragments.md)

## 步驟4:建立範本 {#step-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

若要建立互動式通訊，您必須在AEM伺服器上提供適用於列印和網路頻道的範本。

「列印」頻道的範本是在Adobe Forms Designer中建立，並上傳至AEM伺服器。 然後，這些範本便可在建立互動式通訊時使用。

網頁頻道的範本是在AEM中建立。 範本作者和管理員可以建立、編輯和啟用Web範本。 在建立並啟用後，這些範本就可在建立互動式通訊時使用。

**目標：**

* 使用Adobe Forms Designer建立適用於列印通道的XDP範本
* 將XDP範本上傳至AEM Forms Server
* 建立並啟用網頁頻道的範本

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-templates-print-web.md)

## 步驟5:建立互動式通訊 {#step-create-an-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

一旦您建立所有的建置區塊（例如表單資料模型、檔案片段和網頁版本的範本）後，就可以開始建立互動式通訊。

互動式通訊可透過兩個通道提供：平面與網頁。 您也可以以主版的方式建立互動式的列印通訊管道。 列印為網頁頻道的主選項，可確保網頁頻道的內容、繼承和資料系結是從列印頻道衍生而來。

**目標：**

* 建立適用於列印頻道的互動式通訊
* 建立適用於網路頻道的互動式通訊
* 以印刷為主的方式建立印刷與網路互動式通訊
* 在Web版互動式通訊中建立動態表格
* 在Web版互動式通訊中建立圖表
* 在網路版互動通訊中建立超連結

   [ ![see-the-guide-sm](assets/see-the-guide-sm.png)](/help/forms/using/create-interactive-communication0.md)

## 步驟6:測試您的互動式通訊 {#step-test-your-interactive-communication}

![11-test-your-adaptive-form](assets/11-test-your-adaptive-form.png)

建立互動式通訊後，請務必測試您在其中所做的每項變更。 測試互動式通訊的每個領域都很麻煩。 AEM Forms提供SDK(Calvin SDK)，以自動測試網頁瀏覽器中的互動式通訊。

**目標：**

* 建立測試套件
* 建立測試案例
* 執行測試案例

## 步驟7:發佈您的互動式通訊 {#step-publish-your-interactive-communication}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

當您使用列印和網路通道建立和測試互動式通訊後，就可以發佈這些資產。 本教學課程中說明的使用案例著重於將這些資產與電子郵件用戶端整合。 電子郵件用戶端是將互動式通訊傳送至多個電子郵件地址的橋梁。

**目標：**

* 將互動式通訊與電子郵件用戶端整合，以便將通訊傳送給客戶
* 將PDF檔案加入附件（在列印頻道中建立的互動式通訊）
* 加入互動式通訊網路版本的連結

